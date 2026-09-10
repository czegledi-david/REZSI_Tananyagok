# 2. Nyelvi elemek: Vezérlési szerkezetek, I/O és Tömbök

A C# nyelv alapvető szintaktikai egységeit és utasításait használjuk a program logikájának felépítésére. Miután megismertük az osztályokat és objektumokat, fontos tisztázni a metódusokon belüli utasítások helyes használatát.

## 1. Utasítások és vezérlési szerkezetek

A C# nyelvben a programunk logikáját különféle utasításokkal irányíthatjuk.

*   **Blokk utasítások:** Az utasításokat kapcsos zárójelek `{ }` közé zárva blokkokat hozhatunk létre, amelyek az utasításokat sorban hajtják végre. A blokkon belül deklarált lokális változók hatásköre és élettartama az adott blokkra korlátozódik. Fontos szabály, hogy a lokális változókat inicializálni kell, mert ha nem adunk nekik kezdőértéket, nem kapnak automatikusan alapértelmezett értéket.
*   **Feltételes utasítások:** A döntéshozatalhoz az `if` és `switch` szerkezetek használhatók. A C# nyelvben a `switch` kifejezés típusa többféle lehet, megengedett például az `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char` vagy akár a `string` típus is.
*   **Ciklusok (while, do-while, for):** A `while` és `do-while` ciklusok vezérlőfeltétele kizárólag logikai típusú lehet. Emiatt a C nyelvben megszokott `while(1)` szintaxis itt nem működik, végtelen ciklushoz a `while(true)` forma használatos. A `for` ciklus szintaktikája megegyezik a C nyelvben megszokottal, a ciklusváltozót gyakran a fejben deklarálják, így annak hatásköre a ciklusra terjed ki.
*   **A foreach ciklus:** A `foreach (tipus azonosító in kifejezés)` ciklus kifejezetten tömbök vagy gyűjtemények bejárására szolgál. Ennek a szerkezetnek a használatához a bejárandó gyűjteménynek implementálnia kell a `System.Collections.IEnumerable` interfészt, és rendelkeznie kell egy `GetEnumerator` metódussal.
*   **Vezérlésátadó utasítások:** A folyamat megszakítására vagy módosítására a `break`, a `continue` és a `return` utasítások szolgálnak, továbbá a C# támogatja a `goto` utasítást is címkézett vezérlésátadáshoz.

## 2. C# Specifikus utasítások

A nyelv tartalmaz speciális utasításokat a hibakezelés és a memóriabiztonság növelésére.

*   A `checked` és `unchecked` blokkokkal az egész típusokon végzett aritmetikai műveletek túlcsordulását tudjuk szabályozni. A `checked` blokkban a veremtúlcsordulás kivételt (hibát) dob, míg az `unchecked` blokkban a művelet lefut, de jegyvesztés történik.
*   Többszálú programozásnál a `lock` utasítás kijelöl egy blokkot, amelyhez egyszerre csak egy szál férhet hozzá, ehhez pedig egy referenciatípusú tokent zár le.
*   Kivételkezeléshez a nyelv a `throw`, valamint a `try-catch-finally` blokkokat használja.

## 3. Standard Input és Output (Konzol)

A C# programokban a konzolos műveleteket a `System` névtérben található `Console` osztállyal végezzük.

**Kiíratás a képernyőre:**

*   A `Console.Write` és `Console.WriteLine` metódusok bármilyen típusú változót képesek automatikusan konvertálni és kiírni.

*   A formázott kiíratáshoz használhatunk formátum sztringeket argumentum helyettesítő sorszámokkal (például `{0}`), de a modern C# már támogatja az interpolációt is (például `$"Szöveg {valtozo}"`).

*   Karaktertömb (`char[]`) kiírásakor a metódus képes a teljes tömböt, vagy akár egy adott indextartományt is egyben kiírni.

**Beolvasás a billentyűzetről:**

*   A `Console.ReadLine()` metódus a bemeneti pufferből olvasott teljes sort adja vissza szövegként (`string`).

*   A `Console.Read()` metódus a bemeneti pufferből beolvassa a következő karaktert, és annak ASCII kódjával tér vissza.

*   A `Console.ReadKey()` a felhasználó által leütött billentyűt adja meg, ezt gyakran a konzolablak nyitva tartására használják.

**Biztonságos konverzió (Parse és TryParse):**
Mivel a `ReadLine()` mindig szöveget ad vissza, azt számításokhoz konvertálni kell.

*   A konverzió elvégezhető a `Convert` osztály metódusaival (például `Convert.ToInt32()`), vagy a .NET típusok saját `Parse()` metódusával (például `Int32.Parse()`).

*   A legbiztonságosabb módszer a `TryParse()` használata. Ez a metódus egy logikai értékkel (`bool`) tér vissza, amely megmutatja, sikeres volt-e a konverzió, az eredményt pedig egy `out` paraméterként adja vissza.

## 4. Többdimenziós tömbök

A C# nyelvben a többdimenziós adatszerkezeteknek két alapvető típusa van.

**1. Tömbök tömbje (Jagged array)**

*   Olyan tömb, amelynek elemei maguk is különálló tömbök.

*   Mivel minden sora egy külön tömb, a sorok hossza (az oszlopok száma) eltérő lehet.

*   Létrehozása például: `int[][] jagged = new int[5][];`.

*   Egy adott elemre való hivatkozás dupla indexeléssel történik, például: `jagged[1][1]`.

**2. Mátrix (Szabályos többdimenziós tömb)**

*   Ezeknél a tömböknél minden sorban szigorúan azonos az elemek száma.

*   Létrehozása egyetlen vesszővel történik a szögletes zárójelben: `int[,] twodim = new int[2,3];`.

*   Egy adott elemre való hivatkozás a vesszővel elválasztott indexekkel történik, például: `twodim[1,1] = 2;`.

*   A mátrix dimenzióinak számát a `.Rank` tulajdonsággal kérdezhetjük le.

*   Egy adott dimenzió (például a sorok vagy oszlopok) méretét a `.GetLength(0)` vagy `.GetLength(1)` metódusokkal tudjuk megállapítani.

---

## Gyakorló feladat

Készíts egy programot, amely egy biztonságos adatbekérő ciklus (TryParse) segítségével bekér egy 1 és 5 közötti számot a felhasználótól. Ha a beolvasás sikeres és a szám a megfelelő tartományban van, hozz létre egy olyan mátrixot (szabályos 2D tömböt), amelynek sorai és oszlopai megegyeznek ezzel a számmal. Végül egy dupla for ciklussal (a `GetLength()` metódust használva) írd tele a mátrixot a `0` számmal, és írasd ki a képernyőre!

??? success "A feladat megoldása"
    ```csharp
    using System;

    class Program
    {
        static void Main(string[] args)
        {
            int meret = 0;
            bool sikeres = false;

            // Biztonságos beolvasás
            do
            {
                Console.Write("Kérek egy számot 1 és 5 között: ");
                string bemenet = Console.ReadLine();
                sikeres = Int32.TryParse(bemenet, out meret);

                if (!sikeres || meret < 1 || meret > 5)
                {
                    Console.WriteLine("Hibás adat! Próbáld újra.");
                    sikeres = false;
                }
            } while (!sikeres);

            // Mátrix létrehozása
            int[,] matrix = new int[meret, meret];

            // Mátrix feltöltése és kiíratása
            Console.WriteLine("A generált mátrix:");
            for (int i = 0; i < matrix.GetLength(0); i++)
            {
                for (int j = 0; j < matrix.GetLength(1); j++)
                {
                    matrix[i, j] = 0; // Feltöltés nullákkal
                    Console.Write(matrix[i, j] + " ");
                }
                Console.WriteLine(); // Új sor minden sor végén
            }
            
            Console.ReadKey();
        }
    }
    ```