# 5. Metódusok, Paraméterátadás és Inicializálás

Az előző anyagokban láttuk, hogyan épül fel egy osztály és miként jönnek létre az objektumok. Most mélyebben megvizsgáljuk, hogy az objektumok hogyan kommunikálnak egymással a metódusokon és a paramétereken keresztül.

## 1. Metódusok paraméterezése

A metódusok fejlécében definiáljuk, hogy milyen bemenő adatokra van szükségük a működéshez.

### Java specifikumok:

*   **Változó hosszúságú argumentumlista:** A Java támogatja a tetszőleges számú paraméter átadását a `típus... azonosító` formátummal (például `double... b`). Ezt csak az utolsó paraméterként lehet használni. A háttérben a fordító egy tömböt készít, és abban tárolja az átadott értékeket.

*   A `final` módosítóval a paraméter csak olvashatóvá válik.

### C# specifikumok:
A C#-ban a paraméterek előtt különböző módosítókat használhatunk a működés finomhangolására:

*   **Alapértelmezett (módosító nélkül):** Érték szerinti paraméterátadás.

*   **ref**: Referencia szerinti átadás. A híváskor átadott változónak már inicializáltnak kell lennie, és a módosítás a hívó félnél is megmarad.

*   **in**: Konstans (readonly) paraméter, a metódus nem változtathatja meg az értékét.

*   **out**: Kimeneti paraméter. A hívó félnél nem kell inicializálni a változót, de a metóduson belül kötelező értéket adni neki.

*   **params**: Változó hosszúságú paraméterlista (hasonló a Java `...` megoldásához). Kizárólag tömbök előtt használható, és csak utolsó paraméter lehet.

A C# támogatja az alapértelmezett paramétereket (opcionális argumentumokat) és a nevesített argumentumokat is, így híváskor tetszőleges sorrendben adhatjuk meg az értékeket, ha megadjuk a nevüket (például `Add(y: 3, x: 12)`).

## 2. A metódusok túlterhelése (Overloading)

A metódusok túlterhelése a statikus (fordítási idejű) polimorfizmus egyik megvalósítása. Lényege, hogy egy osztályon belül több azonos nevű metódus is létezhet, feltéve, hogy a paraméterszignatúrájuk (a paraméterek típusa vagy sorrendje) különbözik.

*   **Célja:** Ugyanarra a viselkedésformára nem kell új nevet kitalálni, csupán a paraméterezés módja tér el. A konstruktorokra is érvényes a túlterhelés szabálya.

*   **C# Szabály:** Nem lehet két metódust pusztán az alapján túlterhelni, hogy az egyik `ref`, a másik pedig `out` vagy `in` paramétert vár.

## 3. Osztályszintű vs. Példányszintű tagok

Amikor egy változót vagy metódust definiálunk, el kell döntenünk, hogy az az objektumhoz (példányhoz) vagy magához a tervrajzhoz (osztályhoz) tartozik-e. Ezt a `static` módosítóval szabályozzuk.

*   **Példányszint (nincs static):** Minden egyes létrehozott objektum (példány) saját memóriaterülettel és saját értékekkel rendelkezik ezekből a tagokból. A példányszintű metódusok automatikusan megkapják a `this` láthatatlan paramétert, amely arra az objektumra hivatkozik, amelyre a metódust meghívták.

*   **Osztályszint (static):** Az osztály minden példánya egyetlen közös memóriaterületen osztozik. A statikus metódusok (például a `Main()`) nem kapják meg a `this` paramétert, így példányosítás nélkül is meghívhatók (az osztály nevével minősítve). Egy statikus metódusból nem lehet közvetlenül (minősítés nélkül) meghívni egy példányszintű adattagot vagy metódust.

Ezt a tudást gyakran használják a Singleton (Egyke) tervezési mintánál, ahol az osztály írója statikus tagokkal biztosítja, hogy az osztályból szigorúan csak egyetlen példány jöhessen létre.

## 4. Inicializálás és C# Tulajdonságok (Properties)

Az objektumok adattagjainak beállítására a konstruktorok mellett speciális eszközök is rendelkezésre állnak.
A C# bevezette a Tulajdonságok (Properties) fogalmát. Ezek kívülről adattagnak látszanak, de valójában metódusok, amelyek `get` (olvasás) és `set` (írás) blokkokkal rendelkeznek.

*   A `set` blokkban a beállítani kívánt értéket a `value` pszeudo-változó tartalmazza.

*   A C# 3.0-tól elérhető az automatikus tulajdonság (például `public string Name { get; set; }`), amelynél a fordító automatikusan létrehoz egy rejtett `private` adattagot a háttérben.

Ezek a tulajdonságok tökéletesen megvalósítják az információrejtés elvét, miközben a szintaxisuk olyan egyszerű marad, mintha közvetlenül egy változót módosítanánk.

---

## Gyakorló feladat

Készíts egy C# programot, amely egy `Diak` osztályt modellez. 

1. Készíts egy **automatikus tulajdonságot** a név tárolására (`Nev`).

2. Készíts egy **osztályszintű (static)** adattagot, amely azt számolja, hány diák objektum jött létre. 

3. A konstruktorban állítsd be a nevet, és növeld meg a statikus számlálót.

4. Készíts egy **statikus metódust**, ami visszaadja a létrehozott diákok számát.

5. A `Main` metódusban hozz létre két diákot, és írasd ki az osztályszintű számláló értékét!

??? success "A feladat megoldása"
    ```csharp
    using System;

    class Diak
    {
        // 1. Automatikus tulajdonság
        public string Nev { get; set; }

        // 2. Osztályszintű (static) adattag a számláláshoz
        private static int diakokSzama = 0;

        // 3. Konstruktor
        public Diak(string nev)
        {
            this.Nev = nev;
            diakokSzama++; // Minden példányosításnál növeljük a közös változót
        }

        // 4. Osztályszintű (static) metódus a lekérdezéshez
        public static int GetDiakokSzama()
        {
            return diakokSzama;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // 5. Példányosítás
            Diak d1 = new Diak("Kovács Béla");
            Diak d2 = new Diak("Nagy Anna");

            // Statikus metódus meghívása közvetlenül az osztály nevén keresztül
            Console.WriteLine($"Összesen {Diak.GetDiakokSzama()} diák jött létre.");
            
            Console.ReadKey();
        }
    }
    ```