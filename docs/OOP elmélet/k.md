# 11. Osztályok Közötti Kapcsolatok és az UML Osztálydiagram

Amikor egy komplexebb szoftvert tervezünk, egyetlen osztály ritkán elegendő. A valós világ modellezése során az objektumok kapcsolatban állnak egymással, és a programunk akkor lesz jól karbantartható, ha ezeket a kapcsolatokat a megfelelő tervezési minták alapján építjük fel.

Az osztályok közötti kapcsolatoknak két fő típusa van: a specializáció ("is-a" kapcsolat) és az asszociáció/tartalmazás ("has-a" kapcsolat).

## 1. Specializáció (is-a kapcsolat)

A specializáció a hagyományos öröklődés (inheritance). Azt fejezi ki, hogy az egyik osztály egy speciálisabb változata a másiknak (például a `Car` is a `Vehicle` - Az autó egy jármű).
Ilyenkor a leszármazott osztály mindent megörököl az ősosztályától, amit kiegészíthet vagy módosíthat. Ezt a megoldást akkor használjuk, ha egyértelmű logikai alá-fölé rendeltségi viszony van az osztályok között.

## 2. Asszociáció és Tartalmazás (has-a kapcsolat)

Nagyon sokszor a specializáció nem logikus, vagy a memóriakezelés szempontjából pazarló. Ilyenkor a tartalmazást használjuk: az egyik osztály egy referenciát (adattagot) tartalmaz a másik osztályra. A tartalmazásnak is két fontos válfaja van az alapján, hogy az objektumok élettartama mennyire függ össze:

### A) Aggregáció (Laza kapcsolat)
Az aggregáció egy "laza" tartalmazás. Azt jelenti, hogy a tartalmazott objektum önállóan, a tartalmazó objektum nélkül is képes létezni és van értelme a rendszerben (például `Car has-a Engine`).

*   Az aggregációt általában úgy valósítjuk meg, hogy a tartalmazott objektumot egy paraméterként adjuk át a tartalmazó osztály konstruktorának.

*   *Példa:* Ha egy autó (Car) megsemmisül a programban, a benne lévő motor (Engine) objektumot még átszerelhetjük egy másik autóba, tehát nem kötelező megsemmisülnie vele együtt.

### B) Kompozíció (Erős kapcsolat)
A kompozíció egy elválaszthatatlan, erős kapcsolat. A tartalmazott objektum önmagában nem létezhet, csak mint az egésznek a része (például `University has-a Senate` - Az egyetemnek van szenátusa).

*   A kompozíciót gyakran példányszintű tagosztályokkal (beágyazott osztályokkal), vagy az objektum létrehozásának beágyazásával valósítják meg. Azaz a szenátus objektum magában az egyetem konstruktorában születik meg (`this.senate = new Senate();`).

*   *Példa:* Ha az egyetem megszűnik, a szenátus sem létezhet tovább önállóan.

## 3. Kapcsolatok számossága

A "has-a" kapcsolatokban a résztvevő objektumok száma alapján három esetet különböztetünk meg:

1.  **Egy-egy (1-1):** Az egyik osztály pontosan egy példánya kapcsolódik a másik egy példányához (pl. egy autónak egy motorja van). Ilyenkor egyszerű adattagként tároljuk a referenciát.

2.  **Egy-több (1-N):** A tartalmazó osztály egy objektumhoz több tartalmazott példány is tartozhat (pl. egy intézethez több tanszék is tartozik). Ezt általában egy tömb (`Típus[]`) vagy egy dinamikus lista (pl. `ArrayList<Department>`) adattaggal valósítjuk meg a tartalmazó osztályban.

3.  **Több-több (N-M):** Mindkét oldal több példánnyal kapcsolódhat a másikhoz (pl. egy diák több tantárgyat felvehet, és egy tantárgyat több diák is felvehet). Ilyenkor mindkét osztálynak tartalmaznia kell egy listát a másik osztály példányaiból, és figyelni kell az integritási szabályokra (a listák szinkronizálására).

## 4. Tervezési Alapelv: Kompozíció az Öröklődés helyett

Az OOP világában ismert ökölszabály a "Composite Reuse Principle" (Kompozíció az öröklődés felett). Ez kimondja, hogy az öröklődést csak akkor használjuk, ha feltétlenül muszáj, minden más esetben a kompozíciót/aggregációt érdemes előnyben részesíteni a polimorfizmus és a kód újrahasznosíthatósága érdekében.

*Példa:* Könyv (Book) és Könyvpéldány (BookInstance).
Ha öröklődést használnánk (`BookInstance extends Book`), akkor minden egyes könyvpéldány létrehozásakor újra memóriát kéne foglalnunk a címnek, szerzőnek stb.
Ehelyett az aggregáció a helyes megoldás: A `Book` osztály tárolja a címet és a szerzőt. A `BookInstance` osztály pedig csak egy leltári számot (`inventoryNo`) és egyetlen referenciát (`Book book`) tartalmaz, ami a megfelelő könyv objektumra mutat. Ezzel rengeteg memóriát spórolunk, és elkerüljük az adatanomáliákat.

## 5. Az UML Osztálydiagram

A komplex rendszereket a Unified Modeling Language (UML) segítségével tervezzük meg. Az osztálydiagramon az osztály egy téglalap, amely tartalmazza a nevét, attribútumait (adattagjait) és metódusait.

*   **Láthatóság:** A `+` jelzi a public, a `-` a private, a `#` pedig a protected elérést.

*   **Specializáció (Öröklődés):** Egy folyamatos, üres, háromszög alakú nyíl mutat a leszármazotttól az ősosztály felé.

*   **Interfész implementálása:** Ugyanolyan üres nyíl, de szaggatott vonallal.

*   **Aggregáció:** Üres rombuszfejű nyíl, amely a tartalmazó osztály felé mutat.

*   **Kompozíció:** Fekete (kitöltött) rombuszfejű nyíl, ami szintén a tartalmazó osztályhoz mutat.
A vonalak mellé írt számok (pl. 1, N, M) mutatják a kapcsolat számosságát.

---

## Gyakorló feladat

Készíts egy példát, amely bemutatja az **Egy-több (1-N) Aggregációt** C#-ban!

1. Hozz létre egy `Konyv` osztályt egy Címmel!

2. Hozz létre egy `Konyvtar` osztályt, aminek van neve, és egy dinamikus listát (`List<Konyv>`) használ a könyvek tárolására!

3. Írj egy metódust a könyvtárba (`UjKonyv`), ami egy meglévő könyv-referenciát fogad el (aggregáció), és hozzáadja a listához.

4. A főprogramban példányosíts két könyvet és egy könyvtárat, majd add hozzá a könyveket a könyvtárhoz.

??? success "A feladat megoldása"
    ```csharp
    using System;
    using System.Collections.Generic; // A List<T> használatához kötelező

    class Konyv
    {
        public string Cim { get; set; }

        public Konyv(string cim)
        {
            this.Cim = cim;
        }
    }

    class Konyvtar
    {
        public string Nev { get; set; }
        
        // 1-N Aggregáció: Egy könyvtárnak több könyve is lehet
        private List<Konyv> konyvek = new List<Konyv>();

        public Konyvtar(string nev)
        {
            this.Nev = nev;
        }

        public void UjKonyv(Konyv ujKonyv)
        {
            konyvek.Add(ujKonyv);
            Console.WriteLine($"A '{ujKonyv.Cim}' című könyv bekerült a(z) {this.Nev} könyvtárba.");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Könyvek létrehozása (Önállóan is léteznek)
            Konyv k1 = new Konyv("Harry Potter");
            Konyv k2 = new Konyv("A Gyűrűk Ura");

            // Könyvtár létrehozása
            Konyvtar varosiKonyvtar = new Konyvtar("Városi Főkönyvtár");

            // Az objektumok összekapcsolása (Aggregáció)
            varosiKonyvtar.UjKonyv(k1);
            varosiKonyvtar.UjKonyv(k2);

            Console.ReadKey();
        }
    }
    ```