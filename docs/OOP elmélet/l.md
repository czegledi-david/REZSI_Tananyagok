# 12. A java.lang és a System névtér alapvető osztályai

Ahhoz, hogy hatékonyan programozzunk objektumorientált környezetben, ismernünk kell a nyelvünk beépített alaptípusait és azok működését. A Java esetében ezeket az osztályokat a `java.lang` csomag, míg a C# esetében a `System` névtér tartalmazza.

## 1. A Mindenek Őse: Az Object osztály

Mind a Java-ban, mind a C#-ban létezik egy legfelsőbb ősosztály, amelyből (közvetve vagy közvetlenül) minden más osztály származik. Ez a Java-ban a `java.lang.Object`, a C#-ban pedig a `System.Object`. 

Mivel ez a közös ős, a benne definiált metódusokat **minden** saját osztályunk megörökli. A legfontosabbak, amelyeket saját osztályainkban gyakran felül is definiálunk (override):


*   **`ToString()` / `toString()`**: Visszaadja az objektum adatait szöveges formában. Alapértelmezésben a C#-ban az osztály nevét, Java-ban pedig az osztály nevét és a memóriacímet (hash kódot) adja vissza, ezért saját osztályoknál **mindig érdemes felülírni**, hogy az objektum tényleges adatait (pl. egy ember nevét és korát) adja vissza.

*   **`Equals(Object)` / `equals(Object)`**: Két objektum összehasonlítására szolgál. Alapértelmezésben csak azt vizsgálja, hogy a két referencia ugyanarra a memóriacímre mutat-e. Ha tartalmi egyezőséget akarunk vizsgálni (pl. két különböző memóriacímen lévő, de azonos nevű és azonosítóval rendelkező ember egyenlő-e), akkor felül kell definiálnunk.

*   **`GetHashCode()` / `hashCode()`**: Egy egyedi számot (hash kódot) állít elő az objektumból, ami gyorsítja a keresést a gyűjteményekben. Szabály: Ha két objektum az `Equals` szerint egyenlő, akkor a hash kódjuknak is kötelezően egyenlőnek kell lennie.

## 2. Értéktípusok és a Boxing (Bedobozolás)

A C#-ban az egyszerű típusok (mint az `int`, `double` stb.) értéktípusok. Létezik azonban egy mechanizmus, amellyel ezeket referenciatípusként (objektumként) is tudjuk kezelni.

*   **Boxing (Bedobozolás):** Amikor egy értéktípusból egy `object` (referencia) típust hozunk létre (pl. `object obj = 10;`). Ilyenkor a memóriában lefoglalódik egy objektum, és az érték bemásolódik oda.

*   **Unboxing (Kidobozolás):** Amikor a bedobozolt objektumból visszanyerjük az eredeti értéktípust egy explicit konverzióval (pl. `int x = (int)obj;`).

A memóriakímélés érdekében a C# biztosítja a **Struktúrákat** (`struct`). Ezek olyanok, mint az osztályok, de az `Object` helyett a `System.ValueType` osztályból származnak, azaz **értéktípusként** viselkednek. Értékadáskor (`=`) egy struktúráról mindig egy teljesen új, független másolat készül a memóriában, nem pedig egy új referencia mutató. A struktúrák automatikusan véglegesek (sealed), nem lehet belőlük örökölni.

## 3. Szövegkezelés (String és StringBuilder)

A `String` típus (C#-ban `string`) egy karakterekből álló sorozat. 
A legfontosabb tulajdonsága mindkét nyelvben, hogy **megváltoztathatatlan (immutable)**. Ez azt jelenti, hogy ha egy már létező stringhez hozzáadunk egy új szót, akkor a memóriában nem a régi objektum bővül ki, hanem létrehoz a gép egy teljesen új string objektumot a memóriában. Ciklusban történő, többszöri szöveg-összefűzés esetén ez nagyon lelassítja a programot.

A string osztály fontosabb metódusai a C#-ban: `.Split()`, `.Replace()`, `.Substring()`, `.Contains()`.

Ha sokszor akarunk módosítani egy szöveget, akkor a `StringBuilder` osztályt kell használni. Ez nem hoz létre minden módosításnál új objektumot, hanem egy allokált memóriaterületen belül módosítja magát a szöveget, így sokkal gyorsabb. Metódusai például az `.Append()` (hozzáfűzés) és a `.Clear()`.

## 4. Dátum és Idő kezelése (C#)

A C#-ban a pontos idő és dátum kezelésére a `System.DateTime` struktúra szolgál.

*   Aktuális időpont lekérése: `DateTime.Now`.

*   Példányosítás megadott adatokkal: `new DateTime(2020, 4, 20)`.

*   Egyes összetevők (év, hónap, nap) kiolvasására a `.Year`, `.Month`, `.Day` tulajdonságok szolgálnak.

Ha két `DateTime` objektumot kivonunk egymásból, az eredmény nem egy dátum lesz, hanem egy **időintervallum**, amit a `System.TimeSpan` struktúra tárol.

*   A `TimeSpan` segítségével lekérdezhetjük, hány nap, óra vagy másodperc telt el a két időpont között (pl. `.TotalDays`).

*   Dátumokhoz egyszerűen adhatunk is hozzá időt az `.AddDays()`, `.AddHours()` metódusok segítségével.

---

## Gyakorló feladat

Készíts egy programot, amely bemutatja az `Object` osztály metódusainak felüldefiniálását és a dátumok kezelését!


1. Hozz létre egy `Szerzodes` nevű osztályt! Legyen két tulajdonsága: `UgyfelNev` (string) és `Lejarat` (DateTime).

2. Írj egy paraméteres konstruktort, amely beállítja ezeket.

3. Definiáld felül (override) a `ToString()` metódust úgy, hogy egy szép formátumban kiírja az ügyfél nevét és a szerződés lejáratának dátumát.

4. Írj egy metódust `HatranyosNapok()` néven a `Szerzodes` osztályon belül! Ez a metódus a `DateTime.Now` és a lejárat dátumának különbségéből (`TimeSpan`) számolja ki, hogy hány nap van még hátra a lejáratig.

5. A `Main` metódusban hozz létre egy szerződést egy jövőbeli dátummal, írasd ki az adatait (ami a saját ToString-edet fogja meghívni), majd írasd ki a hátralévő napok számát is!

??? success "A feladat megoldása"
    ```csharp
    using System;

    class Szerzodes
    {
        public string UgyfelNev { get; set; }
        public DateTime Lejarat { get; set; }

        public Szerzodes(string nev, DateTime lejarat)
        {
            this.UgyfelNev = nev;
            this.Lejarat = lejarat;
        }

        // 3. ToString() felüldefiniálása
        public override string ToString()
        {
            return $"Szerződés: {this.UgyfelNev}, Lejárat: {this.Lejarat.ToShortDateString()}";
        }

        // 4. Hátralévő napok kiszámítása TimeSpan segítségével
        public int HatranyosNapok()
        {
            DateTime ma = DateTime.Now;
            TimeSpan kulonbseg = this.Lejarat - ma;
            
            // A TotalDays egy tört szám, ezért (int)-re castoljuk
            return (int)kulonbseg.TotalDays;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // 5. Tesztelés jövőbeli dátummal
            DateTime jovohet = DateTime.Now.AddDays(10);
            Szerzodes sz1 = new Szerzodes("Nagy Kft.", jovohet);

            // Ez a háttérben meghívja a felülírt ToString() metódust!
            Console.WriteLine(sz1); 
            
            Console.WriteLine($"A szerződés lejáratáig még {sz1.HatranyosNapok()} nap van hátra.");

            Console.ReadKey();
        }
    }
    ```