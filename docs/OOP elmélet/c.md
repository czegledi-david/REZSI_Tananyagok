# 3. Az Objektumorientált Programozási Paradigma és Alapelvei

A programkészítés valójában egy modellezési feladat, ahol a valós világ egy jól körülhatárolt részét, absztrakt modelljét képezzük le. Az objektumorientált (OO) programozási eszközök absztrakciós szintje a legmagasabb, mivel a valós élethez nagyon közeli nyelvi elemeket használnak. 

Az OOP szemlélete szerint a programozás során a valóságot egymással kapcsolatban lévő, együttműködő objektumok halmazaként tekintjük. Egy valós objektum fő jellemzői az egyéniség (különállás), az állapot (struktúra) és a viselkedés. A működés során a viselkedés módosíthatja az aktuális állapotot, és az állapot is befolyásolhatja a viselkedést. 

Ahhoz, hogy egy programozási nyelvet objektumorientáltnak nevezhessünk, négy fő alapelvet kell megvalósítania.

## 1. Egységbezárás és Adatrejtés (Encapsulation)

Az egységbezárás során az osztály szorosan egyetlen egységbe zárja az adott típusú objektumok adatait és az azokkal dolgozó műveleteket (metódusokat). Szabály, hogy az osztályon kívül nem definiálunk semmit, az osztályon belül pedig az adatok és metódusok korlátlanul elérik egymást.

Szorosan ide kapcsolódik az adatrejtés (information hiding) elve, amely kimondja, hogy az osztály műveleteinek implementációja az osztályon kívül nem látható. 

* Az osztály adatai közvetlenül nem érhetők el a külvilág számára, kizárólag a publikus metódusokon keresztül.

* Ennek előnye, hogy az adathozzáférés független az adatábrázolástól.

* A programozó szigorúan szabályozni tudja, hogy írásra vagy olvasásra ad-e hozzáférést, és az adatok írása előtt logikai ellenőrzést is végezhet.

## 2. Öröklődés (Inheritance) és Kompozíció

Az öröklés segítségével egy új osztály úgy is létrehozható, hogy egy már létező, úgynevezett ősosztályt bővítünk ki. Ez a fogalmak hierarchikus osztályozásán (általánosítás és specializáció) alapul.

* A leszármazott osztály automatikusan örökli az ős adatait és metódusait, így azokat nem kell újra definiálni, ami a kód újrahasznosításának (is-a kapcsolat) alapja.

* A leszármazott osztályban lehetőség van új adatok és metódusok megadására, valamint az örökölt metódusok felülírására is.

* Az objektumorientált tervezés során a kód újrahasznosítására gyakran az öröklés helyett a tartalmazási kapcsolatot (kompozíciót, azaz has-a kapcsolatot) javasolják (Composite Reuse Principle).

## 3. Polimorfizmus (Többalakúság)

A polimorfizmus azt jelenti, hogy bizonyos viselkedések, illetve metódusok működése attól függ, hogy pontosan milyen környezetben alkalmazzuk őket.

* **Statikus (korai kötés):** Ez már a fordítás idején eldől. Ide tartozik a metódusok túlterhelése (overloading) és az operátorok kiterjesztése.

* **Dinamikus (késői kötés):** A hívott metódus csak futási időben rendelődik hozzá az objektumhoz. Ennek legismertebb formája a metódusok felülírása (overriding) az öröklődés során.

## 4. Kommunikáció (Üzenetküldés)

Az OOP programok egymással kommunikáló objektumokból állnak. Az objektumokat úgynevezett üzeneteken (metódushívásokon) keresztül kérjük meg a feladatok elvégzésére. Egy objektum csak akkor küldhet üzenetet egy másiknak, ha ismeri vagy tartalmazza azt, de önmagának is küldhet üzenetet.

---

## Gyakorlati Példa: A Kör Objektum

Képzeljük el az elméletet a gyakorlatban! Létrehozunk egy `Circle` (Kör) objektumot, amelynek adatai (állapota) a sugár és a középpont koordinátái. Az objektumnak üzeneteket küldünk: először felszólítjuk a sugarának megnövelésére, majd kérjük, hogy számítsa ki és adja vissza a területét.

??? success "Példa kód megtekintése"
    ```csharp
    using System;

    class Circle
    {
        // Adatrejtés: private mezők
        private int radius;
        private int x;
        private int y;

        // Konstruktor az állapot beállításához
        public Circle(int r, int x, int y)
        {
            this.radius = r;
            this.x = x;
            this.y = y;
        }

        // Metódus: állapot módosítása
        public void IncreaseRadius(int amount)
        {
            this.radius += amount;
        }

        // Metódus: viselkedés (számítás)
        public double GetArea()
        {
            return this.radius * this.radius * Math.PI;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Objektum létrehozása az adatok (állapot) megadásával
            Circle c = new Circle(2, 50, 50);
            
            // Üzenetküldés (metódushívás): állapot módosítása
            c.IncreaseRadius(5);
            
            // Üzenetküldés (metódushívás): viselkedés végrehajtása
            double c_area = c.GetArea();
            
            Console.WriteLine($"A kör területe: {c_area}");
        }
    }
    ```