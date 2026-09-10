# 4. Osztálydefiníció és Objektumok Létrehozása

Miután megismertük az objektumorientált programozás alapelveit, nézzük meg, hogyan épül fel a gyakorlatban egy osztály, és miként jönnek létre belőle az objektumok.

## 1. Az osztályok felépítése és módosítói

A C# nyelvben az osztályok definiálásakor többféle módosítót is használhatunk, amelyek meghatározzák az osztály viselkedését és elérhetőségét:

* **public**: A program bármely részéből elérhető osztály.

* **internal**: Csak az adott szerelvényen (assembly-n) belül látható.

* **abstract**: Nem példányosítható osztály, amelyet kizárólag ősosztályként (továbbfejlesztésre) használunk.

* **sealed**: Végleges osztály, amelyből nem lehet már újabb osztályokat leszármaztatni.

* **partial**: Lehetővé teszi, hogy az osztály definíciója több részből, akár több forrásfájlból álljon össze.

* **static**: Nem lehet példányosítani, és kötelezően minden tagjának statikusnak kell lennie.

Az osztálytagok definiálásának sorrendje technikailag tetszőleges, de a szakmai konvenció szerint a következő: adattagok, konstruktorok, destruktor, tulajdonságok, metódusok, majd a tagosztályok.

## 2. Adattagok (Mezők) és Hozzáférési kategóriák

Az adattagok (mezők) definiálásánál a típus és a név mellett különböző hozzáférési kategóriákat kell megadnunk. A C# a következő szinteket ismeri:

* **public**: A program bármely osztályából korlátozás nélkül elérhető.

* **internal**: Csak az adott szerelvényen belül látható.

* **protected**: Csak az adott osztályban, illetve annak leszármazott osztályaiban érhető el.

* **private**: Szigorúan csak az adott osztályon belül látható.

* **protected internal**: Az adott szerelvényen belül, valamint a leszármazott osztályokban is látható.

* **private protected**: Csak az adott osztályban, és az ugyanabban a szerelvényben definiált leszármazott osztályokban érhető el.

Ha egy osztályon belül nem adunk meg explicit hozzáférési módosítót, akkor a tagok alapértelmezés szerint `private` elérésűek lesznek. Fontos különbség a lokális változókhoz képest, hogy ha a programozó nem ad kezdőértéket egy adattagnak, az automatikusan inicializálódik (a számok `0`-ra, a logikai típusok `false`-ra, a referenciák `null`-ra).

Speciális adattag módosítók a C#-ban:

* **const**: Deklarációval egy időben kap értéket, amit futásidőben már nem lehet megváltoztatni.

* **readonly**: Csak olvasható adattag, amely futási időben kap értéket, de szigorúan csak egyszer (a deklarációban vagy a konstruktorban).

## 3. Metódusok és Adatrejtés

A metódusok felelnek az objektum viselkedéséért. C#-ban a metódusok neve konvenció szerint nagybetűvel kezdődik. A metódusokhoz is rendelhetünk speciális módosítókat:

* **static**: Osztályszintű metódus, nem kell példányosítani az osztályt a meghívásához.

* **virtual**: Olyan metódus, amely a leszármazott osztályban felülírható.

* **override**: Ezzel jelezzük, hogy egy leszármazott osztályban felülírtunk egy örökölt metódust.

* **new**: Örökölt metódust elrejtő, azonos nevű új metódus létrehozására szolgál.

Az adatrejtés (információrejtés) elve alapján az osztály adattagjait `private` (esetleg `protected`) módosítóval kell védeni. Kívülről ezeket az adatokat kizárólag ellenőrzött, `public` metódusokon (például Getter és Setter metódusokon) keresztül szabad elérhetővé tenni.

## 4. Referenciaváltozók és Példányosítás

Amikor létrehozunk egy osztályt, az valójában egy új típust jelent. Azonban egy változó deklarálása önmagában még nem hozza létre az objektumot.

* A referenciaváltozó deklarálásakor csak a hivatkozás (referencia) számára foglalódik hely a memóriában, az objektum számára nem.

* A változó értéke egy memóriacím lesz, amely a tényleges objektumra mutat, vagy `null` értéket vesz fel, ha még nem mutat sehova.

* Az objektumokat futás közben, dinamikusan a `new` kulcsszóval hozzuk létre (példányosítjuk).

Egy már létrehozott objektumra több referencia is mutathat egyszerre. Ha az egyenlőségvizsgálót (`==`) két referenciaváltozón használjuk, az nem az objektumok belső tartalmát hasonlítja össze, hanem azt ellenőrzi, hogy a két referencia pontosan ugyanarra a memóriacímre (objektumra) mutat-e.

## 5. Konstruktorok

A konstruktor egy speciális metódus, amely automatikusan hívódik meg az osztály példányosításakor (a `new` kulcsszó használatakor), feladata pedig az objektum kezdeti állapotának beállítása.

* Nincs visszatérési típusa, a neve pedig kötelezően megegyezik az osztály nevével.

* Explicite nem hívható meg egy már létező objektumon.

* Ha nem írunk saját konstruktort, a fordító létrehoz egy alapértelmezett (üres) konstruktort.

* A konstruktorok nem öröklődnek.

Egy osztálynak több konstruktora is lehet, amennyiben eltér a paraméterlistájuk (túlterhelés). A kódismétlés elkerülése érdekében C#-ban a `: this(paraméterek)` szintaxissal az egyik konstruktorból meghívhatjuk az osztály egy másik konstruktorát.

## 6. Az objektum élettartama és a Destruktor

Az objektum a példányosításkor (a `new` hívásakor) jön létre a dinamikus memóriaterületen. 

* Az objektumok memóriából való törlését a .NET CLR (Common Language Runtime) automatikus szemétgyűjtője (Garbage Collector) végzi.

* A szemétgyűjtő nyilvántartja az objektumokra mutató referenciákat, és ha egy objektumra már egyetlen hivatkozás sem mutat, automatikusan megszünteti azt.

A C# ismeri a destruktor fogalmát, amely egy speciális, paraméter és módosító nélküli metódus, neve pedig a `~` jellel kezdődik (pl. `~Osztalynev()`). Ezt a szemétgyűjtő hívja meg az objektum megszüntetése előtt, jellemzően a lefoglalt külső erőforrások felszabadítására. A fordító a destruktort automatikusan egy `Finalize()` metódusra konvertálja.

---

## Gyakorló feladat

Készíts egy `Teglalap` nevű osztályt!

1. Legyen két `private` adattagja: `szelesseg` és `magassag`.

2. Írj hozzá két különböző konstruktort! Az egyik paraméter nélküli (üres) legyen, amely mindkét értéket 1-re állítja. A másik várjon két paramétert, és állítsa be velük az adattagokat.

3. Készíts egy `public` metódust `Terulet()` néven, ami kiszámolja és visszaadja a téglalap területét.

4. A főprogramban példányosíts két téglalapot (mindkét konstruktort kipróbálva), és írasd ki a területüket!

??? success "A feladat megoldása"
    ```csharp
    class Teglalap
    {
        // 1. Private adattagok (Adatrejtés)
        private double szelesseg;
        private double magassag;

        // 2/A. Paraméter nélküli konstruktor
        public Teglalap()
        {
            szelesseg = 1;
            magassag = 1;
        }

        // 2/B. Paraméteres konstruktor
        public Teglalap(double sz, double m)
        {
            szelesseg = sz;
            magassag = m;
        }

        // 3. Public metódus
        public double Terulet()
        {
            return szelesseg * magassag;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // 4. Példányosítás és tesztelés
            Teglalap alapTeglalap = new Teglalap();
            Teglalap egyediTeglalap = new Teglalap(5.5, 4.0);

            Console.WriteLine($"Az alap téglalap területe: {alapTeglalap.Terulet()}");
            Console.WriteLine($"Az egyedi téglalap területe: {egyediTeglalap.Terulet()}");
        }
    }
    ```