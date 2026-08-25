# Jelentkezés Jegyzetelőnek

Szeretsz átlátható, szép jegyzeteket írni? Szeretnél aktívan hozzájárulni a csoport sikeréhez, és közben extrán elmélyíteni a saját tudásodat is? 

**Akkor téged kereslek!** Jelentkezz jegyzetkészítőnek!

---

## Mit csinál egy Jegyzetkészítő?

A jegyzetkészítő feladata, hogy a tanórákon elhangzott fontosabb információkat, kódpéldákat és magyarázatokat egy strukturált, digitális formátumban (elsősorban **Markdown** nyelven) rögzítse.

**Konkrét feladatok:**

* Az órai vázlat és a táblára/kivetítőre írt kódok átmásolása a gépedre, kiegészítve a saját megjegyzéseiddel és az általam elmondott extra infókkal.

* A jól sikerült, formázott jegyzetek elküldése (vagy GitHubon keresztül történő feltöltése) az óra végén vagy aznap délután.

* Ezek a jegyzetek felkerülnek ide, a hivatalos tananyag portálra, így **a te munkád fogja segíteni az egész évfolyamot** a vizsgafelkészülésben!

---

## Miért éri meg neked?

Természetesen a minőségi munkát és a közösségért tett erőfeszítést nem hagyom szó nélkül:

1. **🌟 Plusz pontok és Ötösök:** A rendszeres és igényes jegyzetelésért cserébe garantált az extra értékelés és a jó jegyek.
2. **🧠 Mélyebb megértés:** Aki jegyzetel, az sokkal jobban odafigyel az órán. Garantáltan jobban meg fogod érteni a bonyolultabb kódokat is!
3. **💼 Szakmai tapasztalat (Portfólió):** Megtanulsz profi szoftver-dokumentációt írni, és (ha a GitHubos utat választod) napi szinten használod a verziókövetést. Ezt bármilyen jövőbeli informatikai állásinterjún imádják hallani.
4. **👑 Örök dicsőség:** A te neved (mint készítő/szerző) mindig ott fog szerepelni a feltöltött tananyagok elején!

---

## Kit keresek?

Nem kell profi programozónak lenned, de a következő tulajdonságok fontosak:

* **Megbízhatóság:** Rendszeresen jársz órára és számíthatok a munkádra.

* **Precizitás:** Odafigyelsz a részletekre, a kódoknál figyelsz a helyes szintaktikára.

* **Alapvető Markdown ismeret:** Vagy legalábbis hajlandóság arra, hogy nagyon gyorsan megtanuld a formázás alapjait (címsorok, listák, kódblokkok).

---

## Hogyan tudsz jelentkezni?

Ha kedvet kaptál hozzá, ne habozz! Vedd fel velem a kapcsolatot az alábbi csatornák valamelyikén:

* **Személyesen:** Az óra elején vagy végén gyere oda hozzám, és beszéljük meg!

* **Online:** Küldd be az első próbajegyzetedet közvetlenül a GitHubon egy Pull Request formájában! Minden ehhez szükséges technikai infót megtalálsz lejjebb, illetve a [README](https://github.com/czegledi-david/REZSI_Tananyagok) fájlban.

---

## 🚀 Hogyan küldj be jegyzetet? (A GitHub Pull Request folyamat)

Mivel a tananyag hivatalos portáljára nem írhatsz bele közvetlenül, a fejlesztői világban szabványos **Fork & Pull Request** módszert fogjuk használni. Ez az állásinterjúkon is óriási piros pont!

### 1. Készíts egy másolatot (Fork)
1. Nyisd meg a hivatalos repót: [REZSI_Tananyagok](https://github.com/czegledi-david/REZSI_Tananyagok)
2. A jobb felső sarokban kattints a **Fork** gombra, majd a **Create fork** lehetőségre. 
*(Ezzel a teljes weblap lemásolódik a te saját GitHub fiókodba, amit bátran szerkeszthetsz.)*

### 2. Töltsd le a gépedre (Clone)
Nyiss egy terminált vagy VS Code-ot, és töltsd le a *saját* másolatodat:
```bash
git clone https://github.com/<a-te-felhasznaloneved>/REZSI_Tananyagok.git
cd REZSI_Tananyagok
```

### 3. Dolgozz a fájlokon!
* Keresd meg a megfelelő mappát (pl. a `docs` mappában), és írd meg a jegyzetet az `.md` fájlba.
* Ne felejtsd el beleírni a nevedet, mint szerző!

### 4. Töltsd fel a saját GitHubodra (Commit & Push)
Mentsd el a munkádat a megszokott módon:
```bash
git add .
git commit -m "Új jegyzet: [Téma neve] hozzáadása"
git push
```

### 5. Küldd be hozzám! (Pull Request)
Most már csak be kell küldened az elkészült anyagot jóváhagyásra:

1. Nyisd meg a *saját* repódat a böngészőben.

2. Kattints a **Contribute**, majd az **Open pull request** gombra.

3. Adj neki egy címet, majd kattints a zöld **Create pull request** gombra!

Ezután én kapok egy értesítést. Átnézem a kódodat, és ha minden szuper, egy gombnyomással beolvasztom, ami így **azonnal megjelenik a hivatalos weboldalon!**

!!! tip "Csapatmunka"
    Nem kell egyedül csinálnod! Ha többen jelentkeztek, beoszthatjátok egymás között a feladatokat és a témaköröket.