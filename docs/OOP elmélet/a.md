# 1. Bevezetés a C# nyelvbe és az Objektumorientált Programozásba

A programozás tanulása során eddig valószínűleg procedurális módon írtad a kódokat, ahol a tervezés felülről lefelé halad, és a rendszert funkcionális egységekre, függvényekre bontjuk. Ennek azonban megvannak a hátrányai, például az adatszerkezet és az algoritmus szét van választva, ami jelentősen rontja az egységbezárást és a kód újrahasznosíthatóságát. Itt jön a képbe az Objektumorientált Programozás (OOP), amely a valós világ mintájára, önálló adatokkal és képességekkel rendelkező egységekre bontja a programot.

## A C# nyelv alapjai és működése

A C# egy teljesen objektumorientált programozási nyelv, amelyet a Microsoft a 2000-es években fejlesztett ki a .NET keretrendszer részeként. Logikailag a program osztályok halmazából áll, a belépési pontja pedig egy olyan futtatható osztály, amely tartalmazza a `Main` metódust.

A C# kód fordítása nem közvetlenül a gép által értelmezhető natív kódra történik. A forráskódból először egy köztes nyelv (MSIL) jön létre, majd a futtatás során a JIT (Just In Time) fordító készít belőle futtatható kódot. A nyelv kis- és nagybetű érzékeny, és szigorú konvenciókat követ: a metódusok és az osztályok nevei például mindig nagybetűvel kezdődnek.

## Változók, típusok és tömbök

Az OOP egyik legfontosabb eleme az adatok megfelelő tárolása. A C# nyelv szigorúan típusos, és a következő memóriakezelési szabályok érvényesek rá:

* Az érték típusú változók (mint például az `int` vagy a `bool`) magukat a konkrét értékeket tárolják a memóriában.
* Az osztályok adattagjainak mindig van egy automatikus, alapértelmezett kezdőértéke, a számoknál például ez `0`, logikai típusoknál pedig `false`.
* A metódusokon belüli lokális változókat viszont mindig a programozónak kell inicializálnia, mert az inicializálatlan változóra való hivatkozás azonnali fordítási hibát eredményez.
* A tömbök mérete futásidőben lekérdezhető a `.Length` tulajdonsággal, a modern C# verziókban pedig a tömbelemek hátulról is könnyedén elérhetők a `^` jellel (pl. `cars[^1]`), illetve tartományokat is kijelölhetünk.

A C# nyelv az osztályok mellett támogatja a struktúrákat (`struct`) is, amelyek olyan összetett adattípusok, ahol a különböző típusú adatok egy egységként kezelhetők, ráadásul saját függvényekkel és konstruktorral is rendelkezhetnek.

## Gyakorló feladat

Készíts egy `Pont` nevű struktúrát, amely egy 2D-s koordináta-rendszer pontját reprezentálja. Legyen két publikus egész szám mezője (`x` és `y`). Írj hozzá egy metódust, amely a pont koordinátáit nullára (az origóra) állítja be, majd a főprogramban hozz létre egy pontot, és hívd meg rajta ezt a beállító metódust.

??? success "A feladat megoldása"
    ```csharp
    struct Pont 
    {
        public int x, y;

        public void Origo()
        {
            this.x = 0;
            this.y = 0;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Pont p = new Pont();
            p.x = 10;
            p.y = 20;
            
            p.Origo();
            Console.WriteLine($"A pont az origóba került: {p.x}, {p.y}");
        }
    }
    ```