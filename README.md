# IT Oktatási Portál & Tananyagok

Ez a repozitórium az informatikai, webfejlesztési és programozási kurzusaimhoz készült hivatalos tudásbázis. A dokumentációs portál egy modern, könnyen áttekinthető felületen gyűjti össze az elméleti jegyzeteket, a kódolási alapokat és a gyakorló feladatsorokat.

## Kinek készült?

Ez a portál **elsősorban a Remenyikes diákok számára** készült. 
A fő célja, hogy a tanórákon, szakkörökön vagy az informatikai táborokban leadott anyagok, az órai vázlatok és a vizsgakövetelmények egyetlen, bárhonnan elérhető helyen legyenek. 

Természetesen a tudás mindenkié – így ha nem vagy a diákcsoportok tagja, de érdekel a programozás és a fejlesztés világa, te is bátran használhatod a segédanyagokat önálló tanuláshoz!

## Mit találsz az oldalon?

A portál úgy lett felépítve, hogy a lehető legnagyobb segítséget nyújtsa a tanulásban:
* **Lépésről lépésre felépített elmélet:** A legkisebb alapoktól a haladó algoritmusokig, emberi nyelven, érthető példákkal elmagyarázva.
* **Gyakorló feladatsorok:** Minden nagyobb blokk végén kihívások várnak, hogy azonnal próbára is tedd, amit megtanultál.
* **Másolható kódrészletek:** A példakódok egyetlen gombnyomással a vágólapra tehetők, így könnyen kipróbálhatod őket a saját szerkesztődben (pl. Visual Studio Code).
* **Színes kiemelések és tippek:** A gyakori buktatókra és a legjobb programozói gyakorlatokra (Best Practices) külön kiemelések hívják fel a figyelmet.

## A motorháztető alatt

A tananyagok egy egyszerű és letisztult Markdown (`.md`) formátumban íródtak, a weboldal megjelenítéséért pedig a [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) keretrendszer felel. Ez biztosítja a gyors működést, a reszponzív (mobilon is tökéletesen olvasható) dizájnt, a kényelmes beépített keresőt és az éjszakai (Dark) módot a kódoláshoz.

---

## 🛠️ Lokális fejlesztés és szerkesztés (Contributor Guide)

Ha szeretnéd a saját gépeden is futtatni és szerkeszteni a weblapot (például ha te is csatlakozol a jegyzetkészítő csapathoz), az alábbi lépésekkel tudod felépíteni a környezetet:

### 1. A kód letöltése
Nyisd meg a terminált, és klónozd le a repozitóriumot:
```bash
git clone https://github.com/czegledi-david/REZSI_Tananyagok
cd REZSI_Tananyagok
```

### 2. Virtuális környezet létrehozása (Ajánlott)
Hogy ne keveredjenek a csomagok a gépeden, hozz létre egy izolált Python környezetet:
```bash
# Létrehozás
python3 -m venv venv

# Aktiválás Mac/Linux alatt:
source venv/bin/activate
# Aktiválás Windows alatt:
venv\Scripts\activate
```

### 3. Függőségek telepítése
Az oldal megjelenítéséhez és az extra funkciókhoz (letöltés, képnagyítás, menürendszer) fel kell telepíteni az MkDocs csomagjait:
```bash
pip install mkdocs-material mkdocs-awesome-pages-plugin mkdocs-glightbox mkdocs-pdf
```

### 4. Szerver indítása
Indítsd el a lokális szervert:
```bash
mkdocs serve
```
A weboldal most már elérhető a böngésződben a `http://127.0.0.1:8000` címen. Ha bármit módosítasz az `.md` fájlokban, az oldal automatikusan frissülni fog.

---
**Készítette:** Czeglédi Dávid