# 9. Tagosztályok, Tömbök és Enum Típusok

Az objektumorientált programozás egységbe zárás (encapsulation) elvét nemcsak adatokra és metódusokra, hanem magukra az osztályokra is ki lehet terjeszteni. Ebben a fejezetben megvizsgáljuk, hogyan definiálhatunk osztályokat más osztályokon belül, miként működnek a tömbök referencia szinten, és hogyan használhatjuk az Enumeráció (Enum) típust.

## 1. Tagosztályok (Beágyazott osztályok)

Egy osztályt definiálhatunk egy másik osztály törzsén belül is. Ezt C#-ban **beágyazott osztálynak (Nested Class)** nevezzük. Ennek a fő célja, hogy azokat az osztályokat, amelyeknek önállóan nincsen értelme vagy kizárólag egy másik osztály használja őket, egyetlen, logikailag zárt egységbe foglaljuk. Ezáltal a kód sokkal karbantarthatóbb lesz.


*   A C#-ban a beágyazott osztályok alapértelmezés szerint `private` elérésűek, ami azt jelenti, hogy csak a beágyazó osztály használhatja őket.

*   Ha `public` elérésűnek deklaráljuk, akkor a külvilág is példányosíthatja, de csak a beágyazó osztály nevével minősítve (például: `Container.Nested nest = new Container.Nested();`).

*   A beágyazott osztály hozzáférhet az őt tartalmazó osztálypéldány **minden** (akár `private`) tagjához, de ehhez explicit módon tárolnia kell egy referenciát a beágyazó osztályra (ezt általában konstruktor paraméterként adják át neki).

## 2. Névtelen Osztályok (Anonymous Classes)

A C# lehetőséget biztosít arra, hogy úgy hozzunk létre és példányosítsunk egy objektumot, hogy az osztálynak valójában nem adunk nevet a kódban. A `new` operátor és egy objektum inicializáló (`{ }`) együttes használatával a fordító a háttérben generál egy nevet az osztálynak.

*   Ezeknek az osztályoknak a tagjai kizárólag csak-olvasható (readonly) publikus tulajdonságok lehetnek.

*   Névtelen osztályt nagyon gyakran használnak adatbázis lekérdezéseknél vagy LINQ kifejezéseknél (például `select new { prod.Color, prod.Price }`).

*   Mivel nem tudjuk a pontos típusnevét, a példányosításkor kötelező a `var` kulcsszót használni. A névtelen osztály közvetlenül az `Object` osztály leszármazottja.

## 3. Tömbök (Arrays) és Dinamikus Tömbök

A C#-ban a tömb nem csupán egy nyelvi elem, hanem egy valódi objektum, amely a `System.Array` osztály leszármazottja.

*   Mivel a tömb **referencia típus**, a deklaráláskor (pl. `int[] tomb;`) még nem jön létre maga az objektum, csak egy mutató, amely a memóriában lefoglalt területre hivatkozik majd. Az objektumot a `new` operátorral kell létrehozni.

*   Ha a tömb típusa is referencia típus (például `String[] s = new String[2];`), akkor a tömb létrehozásával még nem jön létre a két String objektum, csupán két `null` értéket tartalmazó referencia a tömbön belül.

*   A C# fordító futásidőben ellenőrzi a tömbindexek helyességét, túllépés esetén `IndexOutOfRangeException` kivételt dob.

**Dinamikus tömbök:** Ha a program írásakor még nem tudjuk, pontosan hány elemre lesz szükségünk, a beépített `ArrayList` (vagy modern C#-ban a `List<T>`) osztályt használjuk, amely automatikusan képes átméretezni magát. Ennek elemeit az `.Add()`, `.RemoveAt()` vagy `.Clear()` metódusokkal módosíthatjuk.

## 4. Az Enum (Felsorolás) Típus

Az Enumeráció (`enum`) egy speciális értéktípus a C#-ban, amely elnevezett konstansok fix halmazát tárolja. Minden `enum` a `System.Enum` absztrakt osztályból származik.
*   A felsorolás minden tagjának a háttérben megfelel egy egész számérték. Ha nem adjuk meg másképp, ez az érték 0-tól kezdődik, és balról jobbra egyesével növekszik.
*   Mivel az értékek mögött számok állnak, egyszerű típuskonverzióval (`(int)a`) megkaphatjuk a konstans számértékét, vagy fordítva, egy számot konvertálhatunk vissza Enum konstanssá (`(Season)1`).
*   A beépített `Enum.GetNames()` és `Enum.GetValues()` metódusok segítségével könnyedén lekérdezhetjük és bejárhatjuk egy felsorolás összes szöveges nevét vagy lehetséges értékét.

---

## Gyakorló feladat

Készíts egy programot, amely bemutatja egy saját `enum` és a névtelen osztályok használatát!


1. Definiálj az osztályodon kívül (a névtérben) egy `Szin` nevű felsorolást (enum), amely három értéket tartalmaz: `Piros`, `Zold`, `Kek`. (Alapértelmezetten ezek mögött a 0, 1, 2 számok fognak állni).

2. A `Main` metódusban készíts egy tömböt, ami tartalmazza a `Szin.Zold` és `Szin.Piros` értékeket.

3. Hozz létre egy névtelen objektumot a `new { ... }` és a `var` kulcsszó segítségével, aminek legyen egy `Nev` tulajdonsága (például "Auto") és egy `Szin` tulajdonsága (ahol értékként a korábbi tömböd egyik elemét adod meg).

4. Írasd ki a konzolra a névtelen objektum nevét, a színét szövegesen, és egy explicit (int) castolással írasd ki a színéhez tartozó számértéket is!

??? success "A feladat megoldása"
    ```csharp
    using System;

    // 1. Enum definíció
    public enum Szin 
    { 
        Piros, 
        Zold, 
        Kek 
    }

    class Program
    {
        static void Main(string[] args)
        {
            // 2. Enumokat tartalmazó tömb létrehozása
            Szin[] valasztottSzinek = new Szin[] { Szin.Zold, Szin.Piros };

            // 3. Névtelen objektum létrehozása
            var termek = new { 
                Nev = "Sportautó", 
                Szin = valasztottSzinek[1] // Ez a Szin.Piros lesz
            };

            // 4. Eredmények kiíratása
            Console.WriteLine($"A termék neve: {termek.Nev}");
            Console.WriteLine($"A termék színe (szöveg): {termek.Szin}");
            
            // Explicit konverzió int-té, hogy megkapjuk a Piros mögötti számértéket (ami a 0)
            Console.WriteLine($"A termék színének azonosítója (int): {(int)termek.Szin}");

            Console.ReadKey();
        }
    }
    ```