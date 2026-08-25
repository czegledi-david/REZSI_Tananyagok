# 1. A Microsoft .NET Framework és a C# alapjai

## 1. A Microsoft .NET Framework

A Microsoft.NET Framework egy keretrendszer, amely programcsomagként működik a Windows operációs rendszer alatt. Használatával sok hiba elkerülhető, ami nagyban segíti a kezdő programozók munkáját. Lényege, hogy megbízható és gyors programfejlesztési környezetet, valamint programfuttatást tesz lehetővé, továbbá gazdag osztálykönyvtár rendszerrel is rendelkezik. 

Ezt a keretrendszert használja többek között a C#, J#, VB.NET, és a Jscript nyelv is.

---

## 2. A programozás szintjei és a C# nyelv

A programozási nyelvek fejlődése során a számítógép számára közvetlenül érthető gépi kódtól (amely bináris vagy hexadecimális alakban lett megadva) az assembly nyelveken át jutottunk el a magas szintű nyelvekig. 

A magas szintű nyelvek (például a C#, PHP, Python, Perl, Ruby, Java) könnyebben használhatóak és platform függetlenek.

### A C# nyelv főbb jellemzői
* Az első változata 2001-ben jelent meg, és folyamatos fejlesztés alatt áll.
* A fejlesztést a kezdetektől Anders Hejlsberg vezeti, aki a Turbo Pascal kidolgozásában is részt vett.
* A C++-ra épülő, objektumorientált nyelv.
* **Automatikus szemétgyűjtés (garbage collection):** Ez a futás közben nagyon hasznos funkció felszabadítja a dinamikusan lefoglalt memóriaterületeket, ami nagymértékben gyorsítja a program futását.

### A C# beszerzése
A program ingyenesen letölthető az internetről a Microsoft honlapjáról (Visual Studio). A letöltéshez és telepítéshez folyamatos on-line internet kapcsolat szükséges, a helyes működéshez pedig regisztráció egy létező e-mail címmel.

---

## 3. A programkészítés lépései

Egy konkrét feladat megoldása során több, jól meghatározott lépést kell tennünk:

1. **Specifikálás:** A feladat rövid, tömör, egyértelmű leírása. Itt határozzuk meg a bemeneteket (előfeltétel) és a kimeneteket (utófeltétel).
2. **Tervezés:** A megoldás algoritmusának elkészítése. Ezt nyelvfüggetlen eszközökkel (folyamatábra, struktogram, Jackson-diagram, mondatszerű elemek) szokás leírni.
3. **Kódolás:** A megtervezett algoritmus megvalósítása a kiválasztott programozási nyelven.
4. **Tesztelés:** A program kipróbálása különböző tesztadatokkal a hibák feltárása érdekében.
5. **Hibakeresés és Hibajavítás:** A hiba pontos helyének beazonosítása és kijavítása, majd a módosított kód ismételt tesztelése.
6. **Minőségvizsgálat, hatékonyság:** A program jobbá és gyorsabbá tétele.
7. **Dokumentálás:** Fejlesztői, felhasználói és telepítési dokumentáció készítése.
8. **Használat, karbantartás:** Szükséges módosítások (például adókulcsváltozás egy könyvelőprogramnál) elvégzése.

---

## 4. A C# indítása és az első program

A programok nagyrészt kulcsszavakból (utasításokból) és azonosítókból állnak. 
* **Kulcsszó (utasítás):** Olyan szavak, amelyeket a programnyelv képes értelmezni.
* **Azonosító:** Olyan karaktersorozat, amely betűvel kezdődik és betűvel vagy számjeggyel folytatódhat. A programozó ezzel nevezi meg a saját eszközeit (pl. változókat).

!!! warning "Szintaktika vs. Szemantika"
    * **Szintaktika:** A szöveg összeállítására vonatkozó nyelvtani szabályok összessége.
    * **Szemantika:** A program működésére vonatkozó szabályok összessége. Egy nyelvtanilag jó program nem biztos, hogy azt csinálja, amit szeretnénk.

### Új projekt létrehozása
1. Indítás után válasszuk a `File -> New Project` menüpontot.
2. A program típusa legyen `Console Application`.
3. A `Name` részben adjunk nevet a projektnek (pl. `Elso`).

### A program váza és kiíró utasítások

A programunkat egyelőre kizárólag a `static void Main(string[] args)` kapcsos zárójelei közé fogjuk írni. 

* `Console.WriteLine()`: A képernyőre írja az idézőjelek közötti szöveget, és a kurzor a következő sor elejére ugrik. A sort mindig pontosvessző `;` zárja.
* `Console.ReadKey()`: A program futásának megállítására szolgál, mindaddig várakozik, amíg egy billentyűt meg nem nyomunk.

**Példa az első programunkra:**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Elso
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Az első C# programom");
            Console.ReadKey();
        }
    }
}
```

!!! tip "Tipp"
    A C# utasítások nagybetűvel kezdődnek. A nyelv szövegszerkesztője támogatást nyújt a gépelés során (legördülő menü), ahonnan a `Tab` billentyűvel szúrhatjuk be a helyes utasítást.