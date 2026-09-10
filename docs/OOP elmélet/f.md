# 6. Öröklődés és a Metódusok Felüldefiniálása

Az objektumorientált programozás harmadik alappillére az öröklődés (inheritance). Az öröklődés azt jelenti, hogy egy új osztályt úgy is létrehozhatunk, hogy az egy már meglévő osztály leszármazottja lesz. Ilyenkor a leszármazott osztály (subclass / derived class) automatikusan örökli az ősosztály (superclass / base class) adattagjait és metódusait.

Az öröklődés fő célja a kód újrahasznosítása és a valós életbeli hierarchikus osztályozások (például `Jármű` -> `Autó`) modellezése. 
Fontos szabály, hogy a Java és a C# is szigorúan **egyszeres öröklést** engedélyez, azaz egy osztálynak csakis egyetlen közvetlen őse lehet. Egy osztályból azonban több osztály is leszármaztatható, és egy leszármazott osztály lehet egy újabb osztály őse.

## 1. Az öröklődés szintaktikája és szabályai

A C# nyelvben az öröklődést egy kettősponttal (`:`) jelöljük. Ha egy osztály definíciójában nem adunk meg explicit ősosztályt, akkor a C# automatikusan a `System.Object` osztályt tekinti ősnek, így közvetve minden osztály ebből származik.

```csharp
class LeszarmazottOsztaly : OsOsztaly 
{
    // A leszármazott osztály új tagjai
}
```

Ha egy osztályt `sealed` módosítóval látunk el, abból nem lehet újabb osztályt leszármaztatni (Javában ez a `final`).

A leszármazott osztály örökli az ősosztály tagjait, de nem mindegyikhez férhet hozzá szabadon:

*   A `public` és `protected` tagokat korlátozás nélkül használhatja.

*   Az ősosztály `private` tagjait a leszármazott ugyan megörökli, de közvetlenül nem hivatkozhat rájuk.

## 2. A konstruktorok viselkedése az öröklődésben

**A konstruktor sosem öröklődik!** Amikor azonban példányosítunk egy leszármazott objektumot (azaz meghívjuk a konstruktorát), az automatikusan meghívja az ősosztályának konstruktorát is. Így egy konstruktor hívási lánc alakul ki, ami egészen a hierarchia csúcsáig (az `Object` osztályig) felmegy.

C#-ban a `: base(paraméterek)` szintaxissal explicite megadhatjuk a konstruktor fejlécében, hogy az ősosztály melyik konstruktorát szeretnénk meghívni az inicializáláshoz. Ha nem adjuk meg, a fordító automatikusan egy paraméter nélküli `: base()` hívást illeszt be.

```csharp
public class Szemelyauto : Jarmu 
{
    public Szemelyauto(int kerekek) : base(kerekek) 
    {
        // Először a Jarmu(int) konstruktor fut le, utána folytatódik a kód itt
    }
}
```

*Figyelmeztetés:* Ha az ősosztályban csak olyan konstruktor van, amely vár valamilyen paramétert, de a leszármazott osztályban megpróbáljuk használni az implicit (paraméter nélküli) `base()` hívást, a fordító azonnal hibát jelez.

## 3. Metódusok felüldefiniálása és elrejtése

Az öröklődés igazi ereje abban rejlik, hogy a leszármazott osztály nemcsak új metódusokat tud írni, hanem a meglévőket is képes módosítani a saját igényei szerint. Két módszer létezik az ősosztályból örökölt metódusok kezelésére:

### A) Elrejtés (Hiding) - Statikus polimorfizmus
Ha az ősosztályban van egy metódus, és a leszármazottban írunk egy pont ugyanolyat, a leszármazott metódusa "eltakarja" az örököltet.

*   C#-ban az elrejtést (és a fordító figyelmeztetésének elnémítását) a `new` kulcsszóval jelezzük.

*   Az elrejtés **korai kötéssel** (fordítási időben) valósul meg.

*   Ha a leszármazott osztály kódjában mégis szükség lenne az ősosztály elrejtett példányszintű metódusára, azt a `base.MetodusNev()` hivatkozással érhetjük el.

### B) Felüldefiniálás (Overriding) - Dinamikus polimorfizmus
Ha azt akarjuk, hogy a híváskor mindig futási időben (késői kötéssel) dőljön el, hogy pontosan melyik osztály metódusának kell lefutnia az objektum tényleges típusa alapján, felüldefiniálást használunk.

*   Az ősosztályban a metódus elé a `virtual` vagy az `abstract` kulcsszót kell tenni, jelezve, hogy engedélyezzük a felülírást.

*   A leszármazott osztályban a felülíró metódus elé az `override` kulcsszót kell írni.

*   A metódus felüldefiniálás csakis példányszintű metódusokra működik, osztályszintűek (static) esetén csak az elrejtés lehetséges.

## 4. Az Object osztály és az objektumok másolása

Mivel C#-ban közvetve minden osztály a `System.Object` osztály leszármazottja, ezért minden saját osztályunk automatikusan örököl néhány alapvető metódust:

*   `ToString()`: Visszaadja az objektum szöveges leírását. Ezt szinte minden saját osztályban felül (`override`) szoktuk definiálni, hogy értelmes információt adjon.

*   `Equals(Object o)`: Két objektum összehasonlítására szolgál.

**Objektumok másolása:**
Tudni kell, hogy ha egy objektumot egyenlőségjellel adunk át egy másik változónak (`c2 = c1`), akkor nem jön létre új objektum, csak egy új referencia (mutató) másolódik ugyanarra a memóriacímre.

*   Ha valódi másolatot akarunk, a `MemberwiseClone()` metódust használhatjuk, de ez csak úgynevezett sekély másolatot (shallow copy) készít.

*   Ha az objektumunk más referenciákat is tartalmaz (pl. egy kör objektum tartalmaz egy pont objektumot), akkor a sekély másolatnál a belső objektumról nem készül másolat. Ilyenkor saját logikát kell írnunk a mély másolat (deep copy) elkészítéséhez.

---

## Gyakorló feladat

Készíts egy kis osztályhierarchiát, ahol gyakorolhatod az öröklődést, a konstruktor-hívásokat és a metódusok felüldefiniálását!

1. Hozz létre egy `Allat` nevű ősosztályt! Legyen egy `protected` szöveges adattagja (`nev`), és egy paraméteres konstruktora, ami beállítja ezt a nevet. Írj bele egy `virtual` metódust `HangotAd()` néven, ami annyit ír ki: "(Néma csend)".

2. Készíts egy `Kutya` osztályt, ami az `Allat` osztályból származik! A konstruktorában a `: base()` segítségével add át a nevet az ősosztálynak.

3. A `Kutya` osztályban az `override` kulcsszóval definiáld felül a `HangotAd()` metódust úgy, hogy kiírja: "[név] ugat: Vau-vau!".

4. A főprogramban példányosíts egy kutyát, és hívd meg a metódusát!

??? success "A feladat megoldása"
    ```csharp
    using System;

    // 1. Az ősosztály
    class Allat
    {
        protected string nev;

        // Ősosztály konstruktora
        public Allat(string nev)
        {
            this.nev = nev;
        }

        // Virtuális metódus, ami felülírható
        public virtual void HangotAd()
        {
            Console.WriteLine("(Néma csend)");
        }
    }

    // 2. A leszármazott osztály
    class Kutya : Allat
    {
        // Konstruktor hívási lánc: átadjuk a nevet az ősnek
        public Kutya(string nev) : base(nev)
        {
        }

        // 3. Metódus felüldefiniálása
        public override void HangotAd()
        {
            Console.WriteLine($"{this.nev} ugat: Vau-vau!");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // 4. Példányosítás és tesztelés
            Kutya bloki = new Kutya("Blöki");
            bloki.HangotAd(); // Kimenet: Blöki ugat: Vau-vau!
            
            Console.ReadKey();
        }
    }
    ```