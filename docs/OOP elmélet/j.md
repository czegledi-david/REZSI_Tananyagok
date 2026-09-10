# 10. Kivételkezelés és Fájlkezelés

A programozás során elkerülhetetlen, hogy különböző hibák lépjenek fel. A hagyományos hibakezelés során a funkcionális és a hibakezelő kódrészek gyakran összekeverednek, a hibákat pedig speciális visszatérési értékekkel jelzik, ami jelentősen rontja a kód olvashatóságát. Ezt a problémát hivatott kiküszöbölni az objektumorientált kivételkezelés.

## 1. A kivételek és a kivételkezelés alapjai

A kivétel (exception) egy olyan esemény a programvégrehajtás során, amely megzavarja a normál programműködést. 

* Az objektumorientált programozásban a kivétel egy objektum, ami a hiba bekövetkezésekor jön létre.

* Ez a kivételobjektum fontos információkat tartalmaz: megadja a hiba típusát, és rögzíti a program állapotát a kivétel bekövetkezésekor.

* Kivétel keletkezhet automatikusan egy utasítás végrehajtása közben (például I/O hiba, tömbindex túllépés, sikertelen típuskonverzió), de a programkódban kiadott `throw` utasítás hatására is kiváltható.

* Amikor egy kivétel létrejön, a kivételt kiváltó utasítással az adott blokk végrehajtása azonnal befejeződik.

## 2. A try-catch-finally szerkezet

A kivételkezelő utasítás a C# és a Java nyelvben egyaránt a `try-catch-finally` blokk.


* **A try blokk:** Ebbe a blokkba kell írni a normál működéshez tartozó olyan kódrészeket, amelyek kivételt dobhatnak. A `try` blokkok egymásba is ágyazhatók.

* **A catch blokk:** Ha a `try` blokkban kivétel dobódik, a rendszer megkeresi a megfelelő `catch` blokkot, ami képes azt lekezelni. A `catch` paramétere egy kivételobjektum referencia. Kivétel bekövetkezésekor az első olyan `catch` blokk kapja el a kivételt, amelyik képes a kezelésére, így több `catch` blokk esetén a sorrendjük rendkívül fontos. Minden `try` blokkhoz kötelező legalább egy `catch` blokkot írni.

* **A finally blokk:** Ennek a blokknak a feladata az erőforrások felszabadítása. Úgy kell megírni, hogy mindig lefuthasson, függetlenül attól, mi történt a `try` blokkban. Ugyanakkor a jegyzet felhívja a figyelmet egy speciális esetre: ha a `try` blokk `return` utasítást tartalmaz és az végrehajtásra kerül, akkor a `finally` blokk nem fut le.

## 3. A C# kivételosztályainak hierarchiája

Minden kivétel őse a `System.Exception` osztály. Ennek az osztálynak nagyon fontos tulajdonságai vannak:

* **StackTrace:** Ennek a tulajdonságnak a segítségével állapítható meg pontosan, hogy a programkódban hol keletkezett a kivétel.

* **Message:** Ez a tulajdonság tartalmazza a kivétel szöveges leírását.

* **InnerException:** Akkor kap értéket, ha több kivétel is történik; a legutoljára keletkezett kivétel ezen keresztül követhető 
vissza az eredeti (kiváltó) kivételig.

A C# kivételek két fő csoportra oszthatók:

* **SystemException:** A futtatókörnyezet (CLR) által kiváltott kivételek (például `DivideByZeroException`, `IndexOutOfRangeException`, `NullReferenceException`).

* **ApplicationException:** Kifejezetten a program által kiváltott kivételek.

Amikor egy kivételt a `catch` blokkban elkapunk, dönthetünk úgy, hogy továbbdobjuk. C#-ban a legjobb megoldás az egyszerű `throw;` utasítás használata, vagy egy új kivétel dobása az eredeti kivétel beágyazásával. A `throw ex;` használata rossz megoldás, mert teljesen törli a kivétel stack-et (a visszakövethetőséget).

## 4. Fájlkezelés (I/O műveletek) a C#-ban

A C# adatfolyamokat (stream) használ az I/O (Input/Output) műveletek elvégzéséhez. Az ehhez szükséges osztályok a `System.IO` névtérben találhatók.

A karakteres fájlkezelés lépései a következők:

1. **Fájl adatfolyam létrehozása:** A `FileStream` osztály segítségével. A konstruktorának első paramétere a fájl neve, a második a `FileMode` (például `Create`, `Open`, `Append`), a harmadik a `FileAccess` (például `Read`, `Write`), a negyedik pedig a `FileShare` (ami a más processzekkel való megosztást szabályozza).

2. **Író/olvasó adatfolyam létrehozása:** Szöveges fájlok írásához a `StreamWriter`, olvasásához a `StreamReader` osztályokat használjuk, átadva nekik a létrehozott fájl adatfolyamot. Bináris adatokhoz a `BinaryReader` és `BinaryWriter` osztályok használatosak. Bináris olvasásnál kiemelten figyelni kell arra, hogy a kiolvasás mindig a típusnak megfelelő metódussal történjen (pl. `ReadInt32()`), különben kivétel keletkezik.

3. **Lezárás:** A megnyitott adatfolyamokat a műveletek végeztével fordított sorrendben le kell zárni a `.Close()` metódussal. Ennek egy modernebb és biztonságosabb alternatívája a `using` blokk, amely automatikusan lezárja a paraméterében megnyitott adatfolyamot.

A statikus `File` osztály metódusaival is végezhetünk műveleteket; például a `File.CreateText()` vagy `File.OpenText()` hívásokkal, amelyeket szintén egy `using` blokkba érdemes tenni.

---

## Gyakorló feladat

Készíts egy programot, amely bekér egy fájlnevet és egy szöveget a felhasználótól, majd megpróbálja elmenteni a szöveget a megadott fájlba! Használj megfelelő `try-catch` blokkot a lehetséges IO hibák (például ha a fájl neve érvénytelen karaktereket tartalmaz) lekezelésére! A fájlba íráshoz használd a `StreamWriter` osztályt egy `using` blokkon belül.

??? success "A feladat megoldása"
    ```csharp
    using System;
    using System.IO;

    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Kérem a fájl nevét kiterjesztéssel (pl. teszt.txt): ");
            string fajlNev = Console.ReadLine();

            Console.Write("Kérem a szöveget, amit menteni szeretnél: ");
            string szoveg = Console.ReadLine();

            try
            {
                // A using blokk gondoskodik a StreamWriter lezárásáról
                using (StreamWriter sw = new StreamWriter(fajlNev))
                {
                    sw.WriteLine(szoveg);
                }
                
                Console.WriteLine("A mentés sikeresen megtörtént!");
            }
            catch (Exception ex)
            {
                // Kivételkezelés, ha bármilyen hiba történik az írás során
                Console.WriteLine("Hiba történt a fájl írása közben!");
                Console.WriteLine($"A hiba részletei (Message): {ex.Message}");
            }
            
            Console.ReadKey();
        }
    }
    ```