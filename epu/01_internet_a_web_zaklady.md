# 01 · Internet a web — základy 🌐

> **Cieľ hodiny:** Pochopiť, čo je internet, čo je web, ako spolu komunikuje prehliadač a server, a čo všetko je potrebné na to, aby bola stránka viditeľná na internete.

---

## 1. Čo je internet?

**Internet** je globálna sieť sietí — milióny počítačov, serverov, mobilov a iných zariadení po celom svete, ktoré medzi sebou komunikujú podľa dohodnutých pravidiel (tzv. **protokolov**).

Nie je to jedna firma ani jeden počítač. Je to obrovská, vzájomne prepojená sústava sietí, ktoré si navzájom rozumejú vďaka spoločným štandardom.

### 🕰️ Krátka história

| Obdobie | Čo sa stalo |
|---|---|
| **60. roky** | Vznikol **ARPANET** — vojensko-akademická sieť. Dáta sa posielali v malých "balíčkoch" (paketoch), ktoré si pri výpadku vedeli nájsť náhradnú cestu. |
| **80. roky** | Presadili sa protokoly **TCP/IP** — základ dnešného internetu, umožnili prepojiť rôzne typy sietí. |
| **90. roky** | Vznikol **World Wide Web (WWW)** — Tim Berners-Lee v CERN-e vytvoril web ako *službu*, ktorá beží na internete. |

> 💡 **Prvá webová stránka na svete** vznikla 6. augusta 1991 (Tim Berners-Lee, CERN). Dodnes ju nájdeš na [https://info.cern.ch/](https://info.cern.ch/) — obsahovala len text a odkazy, žiadny dizajn.

### 💡 Internet vs. Web — v čom je rozdiel?

> **Internet** je infraštruktúra (globálna sieť počítačov).
> **Web (WWW)** je len JEDNA zo služieb, ktorá na internete beží — popri e-maile, videohovoroch a ďalších.

### Tri piliere webu (1991, Tim Berners-Lee)

- **HTML** (HyperText Markup Language) – jazyk na štruktúrovanie dokumentov
- **URL** (Uniform Resource Locator) – presná adresa každého zdroja na webe
- **HTTP** (HyperText Transfer Protocol) – spôsob prenosu dát medzi prehliadačom a serverom

### Služby, ktoré bežia na internete

- **WWW**  (World Wide Web) alebo aj **WEB** – prehliadanie webových stránok pomocou hypertextových odkazov (HTTP/HTTPS)
- **Email** (SMTP, POP3, IMAP)
- **FTP** – prenos súborov medzi počítačmi
- **Cloud storage** (Google Drive, Dropbox...)
- **Streaming** – prenos videa a zvuku v reálnom čase (YouTube, Spotify, Netflix)
- **VoIP** – hlasové a video hovory cez internet (Zoom, Teams, Discord, Skype)
- **Správy v reánom čase** (Instant Messaging) – komunikácia v reálnom čase (Messenger, WhatsApp, Telegram)
- **Online gaming** – hranie hier cez internet s inými hráčmi
- **IoT** (Internet of Things) – komunikácia inteligentných zariadení (smart domácnosti, senzory)

Každá služba používa svoje vlastné **protokoly** — dohodnuté pravidlá, ako si zariadenia vymieňajú dáta.

---

## 2. Ako funguje komunikácia klient – server?

- **Klient** = zariadenie/program, ktorý si niečo *pýta* (napr. tvoj prehliadač)
- **Server** = výkonný počítač, ktorý *čaká na požiadavky* a odpovedá na ne

```
Klient (prehliadač)  ──Požiadavka (Request)──▶  Server
Klient (prehliadač)  ◀──Odpoveď (Response)────  Server
```

### Čo je HTTP a HTTPS?

**HTTP** (HyperText Transfer Protocol) = dohodnutý spôsob, akým si prehliadač a server vymieňajú webový obsah.

**HTTPS** = **bezpečná (šifrovaná)** verzia HTTP. Používa SSL/TLS certifikáty, ktoré chránia prenášané dáta pred odpočúvaním.

**Ako spoznať HTTPS?**
- V adresnom riadku je **zámok** 🔒
- Adresa začína `https://` (nie `http://`)

> ✅ **Zapamätaj si:** HTTP = nešifrované (nebezpečné pre citlivé dáta) · HTTPS = šifrované (dnešný štandard)

---

## 🚀 3. Ako sa stránka dostane na internet?

Máš hotové HTML/CSS/JS súbory na svojom počítači. Aby ich videli aj iní ľudia, potrebuješ:

### 1️⃣ Server
Počítač pripojený **24 hodín denne, 7 dní v týždni** k internetu, na ktorom beží softvér sprístupňujúci stránky verejnosti.

### 2️⃣ Hosting
Služba **prenájmu priestoru a výkonu** na serveri. Predtým, než si vyberieš hosting, musíš vedieť, či tvorí **statickú** alebo **dynamickú** stránku.

**📄 Statická stránka:**
- Obsah je **vopred pripravený** a rovnaký pre všetkých návštevníkov
- Stránka sa skladá len z HTML, CSS a JavaScriptu
- **Nepotrebuje databázu** ani serverové programovanie (PHP, Python, Node.js...)
- **Rýchla** a jednoduchá na nasadenie
- **Príklady použitia:**
  - Portfólio, osobná vizitka
  - Firemná prezentácia (o firme, služby, kontakt)
  - Blog bez komentárov a prihlásenia
  - Dokumentácia projektu
  - Landing page (vstupná stránka kampane)

**⚙️ Dynamická stránka:**
- Obsah sa **vytvára na základe dát** – pre každého používateľa iný
- Potrebuje komunikovať so serverom cez jazyky PHP, Python, Node.js
- Používa **databázu** (MySQL, PostgreSQL, MongoDB...)
- Umožňuje **prihlásenie, registráciu, ukladanie dát**
- **Príklady použitia:**
  - E-shop (košík, objednávky, platby)
  - Sociálna síeť (profily, príspevky, správy)
  - Blog s komentármi a prihlásením
  - Online aplikácie (úlohy, projekty, tímy)
  - Systémy na správu obsahu (CMS)

**Kedy stačí statická stránka?**
- Obsah sa mení zriedka
- Všetci vidia to isté
- Netreba prihlásenie ani ukladanie dát od používateľov

### 3️⃣ Doména
**Doména** = zapamätateľná adresa tvojho webu (napr. `mojaskola.sk`). Bez nej by si si musel pamätať číselnú IP adresu ako `185.25.116.47`.
- Kupuje sa u registrátora (Websupport, Endora, Webnode...)
- Platí sa ročný poplatok (cca 10 – 20 € za `.sk`/`.com`)

### 4️⃣ Prehliadač
Program (Chrome, Firefox, Edge, Safari), ktorý:
1. Pošle požiadavku na server cez HTTP/HTTPS
2. Stiahne HTML, CSS, JS a obrázky
3. Vykreslí stránku na obrazovke

---

## 🏠 4. Webové sídlo a jeho štruktúra

**Webové sídlo** = logicky prepojená skupina stránok, ktoré tvoria jeden celok (napr. portfólio so sekciami Domov, O mne, Portfólio, Kontakt).

**Prečo záleží na štruktúre priečinkov?**

```
mojportfolio/
├── index.html              (Domov)
├── o-mne.html
├── portfolio.html
├── kontakt.html
└── assets/
    ├── css/
    │   └── style.css
    └── js/
        └── script.js
```

- ✅ Používateľ sa rýchlo zorientuje
- ✅ Vyhľadávače lepšie pochopia obsah
- ✅ Ľahšia údržba

---

## 5. Prístupnosť a responzivita (úvod)

### ♿ Prístupnosť (Accessibility)
Stránka by mala byť použiteľná pre **každého** — vrátane ľudí so zrakovým, sluchovým, motorickým či kognitívnym obmedzením.

Základné pravidlá:
- Používaj správne HTML elementy (`<nav>`, `<main>`, `<article>`...)
- Zmysluplná hierarchia nadpisov (`h1 → h2 → h3`)
- Vždy vyplň `alt` pri obrázkoch
- Dostatočný farebný kontrast
- Stránka ovládateľná aj klávesnicou

### 📱 Responzivita
Znamená, že sa rozloženie stránky prispôsobí **rôznym veľkostiam obrazoviek** (mobil, tablet, PC).

---

## 6. Nástroje, ktoré budeme používať

### Editor / IDE
Nástroj na písanie kódu. Budeme používať **Visual Studio Code** (zdarma, najpopulárnejší).

Prečo editor a nie obyčajný textový súbor?
- ✅ Zvýrazňovanie syntaxe (farebný kód)
- ✅ Automatické dopĺňanie
- ✅ Upozornenia na chyby
- ✅ Rozšírenia a Git integrácia

### DevTools (Vývojárske nástroje prehliadača)
Otvoríš pravým klikom na stránku → **Preskúmať / Inšpekcia**. Umožňujú:
- Pozrieť si a upravovať HTML/CSS naživo
- Spúšťať JavaScript a vidieť chyby
- Testovať stránku na rôznych veľkostiach obrazovky

---

## 7. SEO — Search Engine Optimization

**SEO** = súbor postupov, vďaka ktorým **vyhľadávače aj ľudia lepšie nájdu tvoj web**.

Čo zlepšuje umiestnenie vo vyhľadávaní?
1. Zmysluplná štruktúra HTML (jeden `<h1>`, logická hierarchia nadpisov)
2. Kvalitný, originálny obsah
3. Výstižný `<title>`, popis stránky, `alt` texty
4. Zrozumiteľné URL (`/o-mne` namiesto `stranka.php?id=123`)
5. Rýchlosť načítania a funkčnosť na mobile
6. HTTPS - bezpečné pripojenie

---

## 8. Git a GitHub (systém na správu verzií kódu)

**Git** = systém, ktorý zaznamenáva históriu zmien v kóde — môžeš sa vrátiť k staršej verzii projektu, vidieť kto čo zmenil a bezpečne spolupracovať s inými.

### Na čo to slúži?
- ✅ **Záloha** – nikdy nestratíš kód, všetko je v histórii
- ✅ **Spolupráca** – viacero ľudí pracuje na jednom projekte bez konfliktov
- ✅ **Experimentovanie** – môžeš skúšať zmeny bez rizika pokazenia fungujúceho kódu
- ✅ **História** – vieš, kto a kedy urobil zmenu

- **Repository (repozitár)** – priečinok s projektom a celou jeho históriou
- **Commit** – "odfotenie" stavu projektu v danom čase s popisom zmeny
- **GitHub / GitLab** – cloudové úložisko pre zálohu a spoluprácu (+ **GitHub Pages** = bezplatný hosting pre statické stránky)

---

## ✅ Zhrnutie

- **Internet** = globálna sieť sietí. **Web** = jedna zo služieb, ktorá na nej beží.
- Komunikácia funguje na princípe **klient (prehliadač) ↔ server**, cez protokol **HTTP/HTTPS**.
- Aby bola stránka na internete, potrebuješ **server, hosting, doménu** a **prehliadač** na jej zobrazenie.
- Stránky delíme na **statické** (HTML/CSS/JS) a **dynamické** (+ databáza, serverové jazyky).
- Dôležité pojmy: **prístupnosť, responzivita, SEO, Git/GitHub**.

## 🧠 Otázky a úlohy na precvičenie

1. Vysvetli vlastnými slovami rozdiel medzi internetom a webom.
2. Čo znamená skratka HTTP a čím sa líši od HTTPS?
3. Aký je rozdiel medzi statickou a dynamickou webovou stránkou? Ku každej vymysli jeden príklad z bežného života.
4. Čo všetko potrebuješ, aby bola tvoja stránka dostupná na internete pre kohokoľvek na svete?
5. Vyskúšaj otvoriť si na svojej obľúbenej stránke DevTools (`F12` alebo pravý klik → Preskúmať) a nájdi v nej záložku "Console".
6. Prečo je dôležitá prístupnosť webu? Vymenuj aspoň 3 skupiny ľudí, ktorým pomáha.
