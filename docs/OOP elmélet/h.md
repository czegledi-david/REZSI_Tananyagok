# 8. Absztrakt Osztályok és Interfészek

A korábbiakban megtanultuk, hogy a Java-ban és C#-ban is szigorúan egyszeres öröklés létezik, azaz egy osztálynak csakis egy közvetlen őse lehet. Sok esetben azonban ez a szabály túl szigorú. Ezen a problémán segít az objektumorientált programozás negyedik fontos koncepciója, az absztrakció, amelyet absztrakt osztályokkal és interfészekkel valósíthatunk meg.

## 1. Absztrakt Metódusok és Osztályok

Gyakran előfordul a tervezés során, hogy tudjuk: az ősosztályból származó minden objektumnak képesnek kell lennie egy adott műveletre, de az, hogy ezt a műveletet pontosan hogyan hajtja végre, már csak a leszármazott osztályban dőlhet el.

Például minden `Sokszog` osztálynak kell, hogy legyen egy `Terulet()` metódusa, de ezt egy háromszögnél vagy egy téglalapnál teljesen más matematikai képlettel számoljuk ki. Magára az általános sokszögre nem tudunk képletet írni. Ekkor a metódust csak deklaráljuk, de nem adunk neki törzset (definíciót).

*   Az ilyen törzs nélküli metódusokat az `abstract` kulcsszóval jelöljük.

*   Ha egy osztály akár csak egyetlen absztrakt metódust is tartalmaz, magát az osztályt is kötelezően `abstract` minősítővel kell ellátni.

### Az Absztrakt Osztály Szabályai

*   **Példányosítás:** Egy absztrakt osztályt szigorúan tilos és nem is lehet példányosítani (a `new` kulcsszóval objektumot létrehozni belőle).

*   **Öröklődés és Implementáció:** Kizárólag arra szolgál, hogy ősosztály legyen. A leszármazott osztály(ok) feladata, hogy az összes örökölt absztrakt metódust felüldefiniálják (megvalósítsák). Ha egy leszármazott osztály nem valósítja meg az összes absztrakt metódust, akkor neki magának is absztrakt osztálynak kell maradnia.

*   **Konstruktor és Egyéb tagok:** Az absztrakt osztálynak lehet (és gyakran van is) konstruktora, amellyel a leszármazottak beállíthatják az örökölt adattagok kezdőértékeit. Ezenkívül tartalmazhat nem absztrakt, teljesen kifejtett metódusokat is.

*   **C# Specifikum:** C#-ban egy absztrakt metódus implicite virtuális is (hiszen felül kell írni), de a `virtual` kulcsszót tilos kiírni.

## 2. Az Interfész (Interface)

Az interfész tulajdonképpen egy szerződés vagy viselkedésminta, amelyet egy osztály magára nézve kötelezően megvalósít (implementál). Szemantikájában nagyon hasonlít egy tisztán absztrakt osztályra, de egy hatalmas különbséggel: **Nem része az osztályhierarchiának!**

Mivel az interfész nem kötődik az osztályok vérvonalához, egy osztály továbbra is csak egyetlen ősosztályból származhat, de emellett **tetszőleges számú interfészt implementálhat**. Ezzel a módszerrel valósítják meg a C#-ban a többszörös öröklést (egy osztály egy összetett viselkedésmintát vesz fel).

### Az Interfész Szabályai

*   C#-ban az interfészek neve konvenció szerint `I` betűvel kezdődik (pl. `ICheckable`).

*   A benne lévő metódusok mind implicite absztraktok és `public` hozzáférésűek, ezért nem is szokás (és sokszor nem is lehet) kiírni ezeket a módosítókat.

*   Nincsenek példányszintű adattagjai és nincs konstruktora sem, így értelemszerűen nem példányosítható.

*   Bár az interfészből nem lehet objektumot létrehozni, egy interfész **lehet egy referenciaváltozó statikus típusa**. Ez azt jelenti, hogy ha egy metódus egy `ICheckable` típusú paramétert vár, akkor bármilyen osztályt átadhatunk neki, ami megvalósította ezt az interfészt (legyen az egy MunkaDarab, egy Háromszög vagy egy Szerződés).

### Implementálás C#-ban
Ha egy osztály egy ősosztályból is származik, és interfészt is implementál, a kettőspont (`:`) után először mindig az ősosztály nevét kell megadni, majd vesszővel elválasztva az interfészeket.

```csharp
class Triangle : Polygon, ICheckable 
{
    // A Polygon abstract metódusainak felülírása (override)
    // Az ICheckable metódusainak megvalósítása
}
```

---

## Gyakorló feladat

Készíts egy absztrakt osztályt és egy interfészt a többes implementáció gyakorlására!

1. Hozz létre egy `IKapcsolhato` nevű interfészt! Legyen benne két metódus (törzs nélkül): `Bekapcsol()` és `Kikapcsol()`.

2. Hozz létre egy `Gep` nevű absztrakt ősosztályt! Legyen benne egy `public string Gyarto { get; set; }` tulajdonság, valamint egy `abstract void Teszteles()` metódus.

3. Készíts egy `Mosogep` osztályt, ami a `Gep` osztályból származik **ÉS** implementálja az `IKapcsolhato` interfészt is.

4. A `Mosogep` osztályban kötelezően valósítsd meg az absztrakt metódust (override), és implementáld az interfész két metódusát is (írj ki a konzolra tájékoztató szövegeket).

5. A `Main` metódusban példányosíts egy mosógépet, és teszteld az összes metódusát!

??? success "A feladat megoldása"
    ```csharp
    using System;

    // 1. Interfész (Viselkedésminta)
    interface IKapcsolhato
    {
        void Bekapcsol();
        void Kikapcsol();
    }

    // 2. Absztrakt ősosztály (Hierarchia)
    abstract class Gep
    {
        public string Gyarto { get; set; }

        public abstract void Teszteles(); // Absztrakt metódus
    }

    // 3. Leszármazás ÉS Implementáció
    class Mosogep : Gep, IKapcsolhato
    {
        // Ősosztály absztrakt metódusának felülírása
        public override void Teszteles()
        {
            Console.WriteLine($"{this.Gyarto} mosógép tesztelése folyamatban...");
        }

        // 4. Interfész metódusainak megvalósítása
        public void Bekapcsol()
        {
            Console.WriteLine("A mosógép bekapcsolva. A dob forogni kezd.");
        }

        public void Kikapcsol()
        {
            Console.WriteLine("A mosógép kikapcsolva. A mosás lejárt.");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // 5. Példányosítás és metódusok hívása
            Mosogep m = new Mosogep();
            m.Gyarto = "Bosch";

            m.Bekapcsol();
            m.Teszteles();
            m.Kikapcsol();

            Console.ReadKey();
        }
    }
    ```