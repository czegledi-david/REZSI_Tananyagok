# 7. Referenciák Típusai, Típuskonverziók, Operátorok és Névterek

A korábbiakban megtanultuk, hogy egy osztály öröklődhet egy másiktól, és a leszármazott mindent tud, amit az ős. Ebből az alapelvből következik az objektumorientált programozás egyik legerősebb szabálya: **A leszármazott mindig helyettesítheti az őst**.

Ebből a fejezetből megtudhatod, hogyan kezeli a fordító a memóriában lévő objektumokat, és miként hivatkozhatsz rájuk dinamikusan.

## 1. A referencia változó két típusa

Mikor deklarálunk egy referenciaváltozót (például `Jarmu auto = new Szemelyauto();`), a változónak valójában két típusa van:

*   **Statikus típus:** Az a típus, amit a deklarációkor megadtunk a bal oldalon (a fenti példában ez a `Jarmu`). A fordító kizárólag a statikus típus alapján dönti el, hogy egy referencián keresztül **milyen metódusokat hívhatunk meg**. Tehát csak a `Jarmu` osztályban (és őseiben) definiált metódusokat használhatjuk.

*   **Dinamikus típus:** Az a típus, amilyen objektum ténylegesen létrejött a memóriában a jobb oldalon (a fenti példában ez a `Szemelyauto`). Ez mindig megegyezik a statikus típussal, vagy annak egy leszármazottja. 

*Következmény:* Mivel minden osztály az `Object` osztályból származik, egy `Object` típusú referenciaváltozó (mint statikus típus) az égvilágon bármilyen objektumra mutathat (mint dinamikus típus).

## 2. Dinamikus típusvizsgálat és Típuskonverziók (C#)

Sokszor futási időben (dinamikusan) kell ellenőriznünk, hogy egy ősosztályú referencia éppen milyen leszármazott objektumra mutat. 
A C# ehhez biztosítja az `is` operátort, amely egy logikai (igaz/hamis) értéket ad vissza, ha a referencia dinamikus típusa megegyezik a megadott típussal (vagy annak leszármazottjával). Ezen felül a pontos egyezés vizsgálatára használható a `typeof` operátor kombinálva a `.GetType()` metódussal.

Ha biztosak vagyunk benne, hogy a referencia a megfelelő objektumra mutat, a metódusainak eléréséhez **konvertálni (castolni)** kell a referenciát:

*   **Explicit típuskonverzió:** A C stílusú `(Tipus)valtozo` formátum. Ha a konverzió nem hajtható végre, a program futási idejű hibával elszáll.

*   **Az `as` operátor:** Biztonságos konverzió. Megpróbálja átkonvertálni a referenciát a kért típusra; ha ez nem lehetséges, hibadobás helyett egyszerűen `null` értéket ad vissza.

## 3. Operátorok Kiterjesztése (Operator Overloading)

A C# nyelvben az operátorok kiterjesztése a statikus polimorfizmus egy elegáns megvalósítása. Segítségével megtaníthatjuk a saját osztályainkat (például egy `Tort` osztályt) arra, hogy értelmezni tudják a hagyományos matematikai operátorokat (például `+`, `-`, `*`, `/`).


*   Az operátorok valójában `public static` metódusként vannak megvalósítva.

*   A szintaktikája: `public static Visszateres operator +(Tipus a, Tipus b)`.

*   Fontos szabály, hogy az operátorok precedenciája (sorrendje) és az operandusok száma nem módosítható.

*   Ezzel a módszerrel definiálhatunk a saját típusainkhoz implicit és explicit típuskonverziós (cast) operátorokat is.

## 4. Névterek és Csoportosítás (C#)

Nagyobb programok (projektek) esetén elkerülhetetlen, hogy különböző osztályoknak (például egy gombnak és egy ruhagombnak) ugyanaz legyen a neve. Ennek megelőzésére (a névütközések elkerülésére) a C# **névtereket (namespace)** használ.

*   A névtér egy logikai egység, amely önálló hatáskört definiál, ezen belül az azonosítóknak egyedinek kell lenniük.

*   Ha nem definiálunk névteret, a kódunk a "név nélküli" (globális) névtérbe kerül.

*   Más névterek tartalmát a `using` kulcsszóval tehetjük elérhetővé a kódunk számára (például `using System;`). Ekkor elegendő az osztály rövid nevét használni (a teljes, ponttal elválasztott hosszú név helyett).

*   Ha még így is névütközés lépne fel (mert több importált névtérben is van ugyanakkora nevű osztály), bevezethetünk aliasokat is: `using diag = System.Diagnostics.Tracing;`.

---

## Gyakorló feladat

Készíts egy programot, amely az operátorok kiterjesztését és a biztonságos típuskonverziót (`as` operátor) gyakoroltatja!

1. Hozz létre egy `Pont` osztályt két (`x` és `y`) egész típusú adattaggal!

2. Definiáld felül az `+` operátort úgy, hogy két `Pont` objektum összeadásakor a koordináták összeadódjanak, és egy új `Pont` objektumot adjon vissza.

3. Készíts egy `ToString()` felüldefiniálást az ellenőrzéshez!

4. A `Main` metódusban adj össze két pontot! Ezt az eredményt egy `Object` típusú referenciaváltozóba mentsd el, majd az `as` operátor segítségével konvertáld vissza `Pont` típusúra, és csak sikeres konverzió esetén írasd ki a képernyőre!

??? success "A feladat megoldása"
    ```csharp
    using System;

    class Pont
    {
        public int X { get; set; }
        public int Y { get; set; }

        public Pont(int x, int y)
        {
            this.X = x;
            this.Y = y;
        }

        // 2. Operátor kiterjesztés (Túlterhelés)
        public static Pont operator +(Pont a, Pont b)
        {
            return new Pont(a.X + b.X, a.Y + b.Y);
        }

        // 3. ToString() felülírása a formázott kiíráshoz
        public override string ToString()
        {
            return $"({this.X}, {this.Y})";
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Pont p1 = new Pont(2, 3);
            Pont p2 = new Pont(5, 7);

            // Összeadás, amit egy Object típusba rakunk (ősbe)
            Object eredmenyObj = p1 + p2;

            // 4. Visszakonvertálás az 'as' operátorral
            Pont konvertaltPont = eredmenyObj as Pont;

            if (konvertaltPont != null)
            {
                Console.WriteLine($"A két pont összege: {konvertaltPont.ToString()}");
            }
            else
            {
                Console.WriteLine("A típuskonverzió sikertelen volt.");
            }

            Console.ReadKey();
        }
    }
    ```