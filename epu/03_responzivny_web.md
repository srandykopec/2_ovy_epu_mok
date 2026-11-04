# Responzívny web – poznámky

> Verzia 2 · skupina 2EPU/OVY · Prerekvizity: HTML základy (štruktúra stránky, odkazy, obrázky), základy CSS (selektory, farby, okraje, `padding`, `margin`).

---

## 1. Čo je responzívna stránka?

Responzívna stránka sa **automaticky prispôsobí veľkosti obrazovky**. Vyzerá dobre na počítači, na tablete aj na mobile. Mení sa veľkosť textu, rozloženie prvkov aj medzery medzi nimi.

| Neresponzívna stránka | Responzívna stránka |
| --- | --- |
| Pevná šírka (napr. `960px`) | Šírka sa prispôsobuje obrazovke |
| Na mobile treba scrollovať do strán | Obsah sa zmestí na šírku obrazovky |
| 3 stĺpce aj na malom displeji | 3 stĺpce na PC → 1 stĺpec na mobile |

**Kľúčová myšlienka:** Jeden HTML dokument a jeden CSS súbor majú fungovať na všetkých zariadeniach.

---

## 2. Čo potrebuješ na responzívny web

Zoradené podľa dôležitosti:

1. **Viewport meta tag** – povinný základ.
2. **Relatívne jednotky** (`%`, `rem`, `vw`, `clamp()`).
3. **`max-width`** na kontajneroch a obrázkoch.
4. **Flexbox a Grid** – automatické rozloženie.
5. **Media queries** – zmena štýlu pri určitej šírke.

---

## 3. Viewport meta tag – bez neho to nefunguje

Pridaj do `<head>` každej stránky:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**Čo to robí:** Hovorí mobilnému prehliadaču, aby použil šírku zariadenia, a nie šírku desktopovej verzie zmenšenú na displej. Bez tohto riadku je text na mobile nečitateľný.

```html
<!DOCTYPE html>
<html lang="sk">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Moja stránka</title>
</head>
```

✅ **Pravidlo:** Viewport je vždy ako prvý.

---

## 4. Jednotky – fixné a relatívne

### Fixné jednotky (`px`)

- Hodnota je vždy rovnaká, bez ohľadu na zariadenie.
- `font-size: 16px` je na mobile aj na 4K monitore rovnaké.
- **Problém:** Pevná šírka na malom displeji spôsobí horizontálny scroll.

```css
/* ZLE pre responzívnosť */
.container {
  width: 960px;       /* na mobile 375px → horizontálny scroll */
}
```

### Relatívne jednotky

- Menia sa podľa rodiča, nastavení prehliadača alebo veľkosti okna.
- Jeden CSS kód funguje na viacerých zariadeniach.

```css
/* DOBRE pre responzívnosť */
.container {
  width: 90%;         /* na mobile 337px, na desktope 1728px z 1920px */
  max-width: 1200px;  /* na veľkých obrazovkách obmedzenie */
  margin: 0 auto;     /* centrovanie */
}
```

### `%` – relatívne k rodičovi

```css
.rodic {
  width: 1000px;
}

.potomok {
  width: 50%;   /* 500px, pri zmene rodiča sa mení aj potomok */
}
```

**Použitie:** šírky kontajnerov, stĺpce.

### `rem` – relatívne k základnej veľkosti písma v `<html>`

```css
html {
  font-size: 100%;   /* zachová nastavenie prehliadača (zvyčajne 16px) */
}

h1 {
  font-size: 2rem;   /* 2 × základná veľkosť */
}

.spacing {
  margin: 1.5rem;
}
```

- Ak používateľ v prehliadači zväčší písmo, všetky hodnoty v `rem` sa zväčšia.
- Zmena na jednom mieste (`html`) ovplyvní celú stránku.
- **Odporúčanie:** Pre písmo a medzery používaj `rem`.

### `em` – relatívne k písmu rodiča

```css
.parent { font-size: 20px; }
.child  { font-size: 1.5em; }   /* 30px */
```

**Použitie:** menej časté. Hodnoty sa zdedia cez viac úrovní a môžu byť nečakané. Pre väčšinu prípadov použi `rem`.

### `vw`, `vh` – relatívne k oknu prehliadača

- `1vw` = 1 % šírky okna, `1vh` = 1 % výšky okna.
- `100vw` = celá šírka okna.

```css
.responsive-text {
  font-size: 4vw;   /* mení sa so šírkou okna */
}
```

**Pozor na mobile:** Na telefónoch sa výška okna mení, keď sa zobrazí alebo skryje panel prehliadača. Preto sa pre výšku používajú moderné jednotky:

| Jednotka | Význam |
| --- | --- |
| `svh` | výška, keď sú panely prehliadača zobrazené (najmenšia) |
| `lvh` | výška, keď sú panely skryté (najväčšia) |
| `dvh` | dynamická výška, prispôsobuje sa pri zmene panelov |

```css
.hero {
  min-height: 100svh;   /* hero na celú výšku, bez skákania na mobile */
}
```

✅ **Pravidlo:** Pre výšku sekcie používaj `min-height` a jednotku `svh` alebo `dvh`, nie `height: 100vh`.

### `clamp()` – plynulé hodnoty bez media queries

```css
h1 {
  font-size: clamp(1.75rem, 4vw, 3rem);
}
```

Zápis `clamp(min, preferovaná, max)`:
- nikdy nebude menšie ako `1.75rem`,
- nikdy nebude väčšie ako `3rem`,
- medzi tým sa mení podľa šírky okna (`4vw`).

**Použitie:** nadpisy, medzery, odstupy sekcií.

---

## 5. max-width a responzívne obrázky

Na veľkých obrazovkách nechceš text cez celú šírku, lebo sa číta zle.

```css
.container {
  width: 90%;
  max-width: 1200px;
  margin: 0 auto;
}
```

| Zariadenie | Šírka okna | Šírka kontajnera |
| --- | --- | --- |
| Mobil | 375px | 337px (90 %) |
| Tablet | 768px | 691px (90 %) |
| Desktop | 1920px | 1200px (`max-width`) |

### Obrázky

```css
img {
  max-width: 100%;   /* nikdy nepresiahne rodiča */
  height: auto;      /* zachová pomer strán */
}
```

Pri obrázkoch v HTML pridaj aj `loading="lazy"` (načítanie až pri priblížení) a atribút `alt`.

```html
<img src="foto.jpg" alt="Krajina pri západe slnka" loading="lazy">
```

### Pomer strán – `aspect-ratio`

```css
.karta-obrazok {
  aspect-ratio: 16 / 9;
  object-fit: cover;     /* obrázok vyplní rámček bez skreslenia */
}
```

---

## 6. Flexbox – rozloženie v jednom smere

**Flexbox** = jednorozmerné rozloženie (prvky v **riadku** alebo v **stĺpci**).

### Terminológia

- **Flex kontajner** – rodič s `display: flex`.
- **Flex položky** – priami potomkovia kontajnera.
- **Hlavná os** – smer, kam sa prvky radia.
- **Priečna os** – kolmá na hlavnú os.

### Krok 1: aktivácia

```css
.kontajner {
  display: flex;
}
```

Priami potomkovia sa automaticky zoradia vedľa seba. Bez `display: flex` sa zobrazia pod sebou ako bloky.

### Krok 2: osi

Pri `flex-direction: row` (predvolené):

```
HLAVNÁ OS (→)  →  justify-content
┌───────────────────────────────────┐
│  ┌───┐   ┌───┐   ┌───┐            │  ↑
│  │ 1 │   │ 2 │   │ 3 │            │  PRIEČNA OS (↓)
│  └───┘   └───┘   └───┘            │  →  align-items
└───────────────────────────────────┘
```

- `justify-content` zarovnáva **pozdĺž hlavnej osi**.
- `align-items` zarovnáva **pozdĺž priečnej osi**.

### Krok 3: zmena smeru

```css
.kontajner {
  display: flex;
  flex-direction: column;   /* hlavná os sa zmení na zvislú */
}
```

Teraz `justify-content` ovláda zvislé zarovnanie a `align-items` vodorovné.

**Kľúčové pochopenie:** Ktorá os je hlavná, záleží na `flex-direction`. Vlastnosti `justify-content` a `align-items` sa nemenia, mení sa len smer, ktorý ovládajú.

### Medzery – `gap`

```css
.kontajner {
  display: flex;
  gap: 1.25rem;   /* medzery medzi prvkami, bez margin na každom prvku */
}
```

### Najdôležitejšie vlastnosti

**Na kontajneri:**

```css
display: flex;
flex-direction: row;        /* row (vedľa seba) / column (pod sebou) */
justify-content: center;    /* zarovnanie na hlavnej osi */
align-items: center;        /* zarovnanie na priečnej osi */
flex-wrap: wrap;            /* zalomenie na ďalší riadok */
gap: 1rem;                  /* medzery */
```

**Hodnoty `justify-content`:**
- `flex-start` – na začiatok,
- `center` – na stred,
- `flex-end` – na koniec,
- `space-between` – prvý a posledný prvok sú pri okrajoch, medzi nimi rovnaké medzery,
- `space-around` – rovnaké okolo každého prvku (okraje majú polovičný odstup).

**Hodnoty `align-items`:**
- `stretch` – prvky sa natiahnu cez celú výšku (predvolené),
- `center` – na stred,
- `flex-start` – hore,
- `flex-end` – dole.

### Praktický príklad: navigácia

```html
<nav class="nav">
  <a href="#">Domov</a>
  <a href="#">Produkty</a>
  <a href="#">Kontakt</a>
</nav>
```

```css
.nav {
  display: flex;
  gap: 2rem;
  align-items: center;
}
```

✅ **Výsledok:** Odkazy sú vedľa seba s rovnakými medzerami a zvislo zarovnané.

---

## 7. Grid – rozloženie v mriežke

**Grid** = dvojrozmerné rozloženie (riadky **aj** stĺpce).

### Grid v 3 krokoch

1. **Kontajner:** `display: grid`
2. **Stĺpce:** `grid-template-columns: repeat(3, 1fr)`
3. **Medzery:** `gap: 1.25rem`

Prvky sa automaticky umiestnia do buniek mriežky.

```
┌─────────┬─────────┬─────────┐
│ Prvok 1 │ Prvok 2 │ Prvok 3 │  ← riadok 1
├─────────┼─────────┼─────────┤
│ Prvok 4 │ Prvok 5 │ Prvok 6 │  ← riadok 2
└─────────┴─────────┴─────────┘
```

### Jednotka `fr`

`fr` = zlomok dostupného priestoru.

```css
grid-template-columns: 1fr 1fr 1fr;   /* 3 rovnaké stĺpce (každý 1/3) */
grid-template-columns: 1fr 2fr 1fr;   /* stredný je 2× širší (polovica priestoru) */
```

### Skratka `repeat()`

```css
grid-template-columns: repeat(3, 1fr);   /* to isté ako 1fr 1fr 1fr */
```

### Príklad: galéria (3 stĺpce)

```css
.galeria {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.25rem;
}
```

### Responzívna galéria bez media queries

```css
.galeria {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.25rem;
}
```

**Ako to funguje:**
- `minmax(250px, 1fr)` – stĺpec má aspoň 250px, môže sa roztiahnuť na 1 zlomok.
- `auto-fit` – vytvorí toľko stĺpcov, koľko sa zmestí.
- Na širokej obrazovke bude viac stĺpcov, na úzkej jeden.

⚠️ **Pozor:** Ak je okno užšie ako 250px plus medzery, prvok pretečie. Na veľmi malých displejoch zváž menšie minimum, napr. `minmax(min(250px, 100%), 1fr)`.

**Rozdiel `auto-fit` a `auto-fill`:** `auto-fit` roztiahne prázdne stĺpce na šírku obsahu, `auto-fill` ich nechá prázdne. Pre väčšinu kariet používaj `auto-fit`.

### Pokročilé: roztiahnutie prvkov

```css
grid-column: 1 / 3;    /* cez 2 stĺpce */
grid-column: 1 / -1;   /* cez všetky stĺpce */
grid-row: span 2;      /* cez 2 riadky */
```

---

## 8. Media queries – iný štýl pre iné zariadenie

### Problém

Na mobile chceš navigáciu pod sebou, na desktope vedľa seba. Jeden CSS štýl nevie, na akom zariadení beží, preto potrebujeme **podmienky**.

### Syntax

```css
@media (min-width: 768px) {
  /* štýly, ktoré platia, keď je okno aspoň 768px široké */
}
```

### Mobile first

Základný CSS píšeme pre mobil (bez media query). Väčšie obrazovky pridávame cez `min-width`.

```css
/* MOBILE – základ */
.nav {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

/* TABLET a väčšie */
@media (min-width: 768px) {
  .nav {
    flex-direction: row;
    gap: 2rem;
  }
}
```

**Prečo mobile first?** Mobilné štýly sú jednoduchšie a zvyčajne sa začínajú v jednoduchšom layoute. Väčšie obrazovky len pridávajú.

### Breakpointy

**Breakpoint** = šírka, pri ktorej sa layout zmení.

- Hodnoty `768px` a `1024px` sú **štartovací bod**, nie pravidlo.
- Správny postup: začni s mobilom, zväčšuj okno a sleduj, **kedy sa obsah zle zobrazí** (napr. riadky sú príliš dlhé alebo sa text láme). Vtedy pridaj breakpoint.

```css
@media (min-width: 768px)  { /* tablet */ }
@media (min-width: 1024px) { /* desktop */ }
```

### Príklad: počet stĺpcov

```css
.produkty {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
}

@media (min-width: 768px) {
  .produkty {
    grid-template-columns: repeat(2, 1fr);
    gap: 1.5rem;
  }
}

@media (min-width: 1024px) {
  .produkty {
    grid-template-columns: repeat(3, 1fr);
    gap: 2rem;
  }
}
```

### Príklad: responzívne písmo

Dá sa riešiť aj `clamp()` bez breakpointov (pozri kapitolu 4). Media query je vhodná, keď potrebuješ úplne iný layout.

---

## 9. Moderné nástroje (nad rámec základov)

### Container queries

Media query reaguje na **šírku okna**. Container query reaguje na **šírku rodiča**, takže komponent sa prispôsobí miestu, kde je vložený.

```css
.karta-obal {
  container-type: inline-size;
}

@container (min-width: 400px) {
  .karta {
    display: grid;
    grid-template-columns: 1fr 2fr;
  }
}
```

**Použitie:** karta, ktorá môže byť v úzkom alebo širokom stĺpci.

### Redukovaný pohyb

Niektorí používatelia nechcú animácie. Rešpektuj nastavenie systému:

```css
@media (prefers-reduced-motion: reduce) {
  * {
    animation: none !important;
    transition: none !important;
  }
}
```

---

## 10. Ako testovať responzívnosť

1. Otvor stránku vo **VS Code** cez Live Server alebo v prehliadači.
2. Stlač **F12** (DevTools) → ikona **Toggle device toolbar** (Ctrl + Shift + M).
3. Vyber zariadenie (iPhone, iPad) alebo zadaj vlastnú šírku.
4. Pomaly zväčšuj a zmenšuj okno.
5. Skontroluj, či sa **nezobrazuje vodorovný scroll**.
6. Over, či je text čitateľný a tlačidlá dosiahnuteľné palcom.

**Porovnanie s Figmou:** Figma má frame pre každú šírku (mobil, tablet, desktop). Vo Figme a v kóde sa rozhoduje podobne: čo sa má zmeniť pri inej šírke.

---

## 11. Najčastejšie chyby

| Chyba | Dôsledok | Riešenie |
| --- | --- | --- |
| Chýba viewport meta tag | Mobil zobrazí zmenšený desktop | Pridať riadok z kapitoly 3 |
| `width: 960px` na kontajneri | Horizontálny scroll | `width: 90%` + `max-width` |
| Obrázok bez `max-width: 100%` | Obrázok pretečie | `img { max-width: 100%; height: auto; }` |
| `height: 100vh` na mobile | Sekcia sa „hýbe“ pri paneloch | `min-height: 100svh` |
| Všetko v `px` | Text sa nepriateľsky škáluje | Písmo a medzery v `rem` |
| Max-width media query bez logiky | Zmätok v kaskáde | Používaj `min-width` (mobile first) |

---

## 12. Kontrolný zoznam

- [ ] Stránka má viewport meta tag.
- [ ] Kontajner má `max-width` a `width` v `%`.
- [ ] Obrázky majú `max-width: 100%` a `height: auto`.
- [ ] Písmo a medzery sú v `rem` alebo `clamp()`.
- [ ] Flexbox je použitý pre jeden smer, Grid pre mriežku.
- [ ] Media queries sú v štýle mobile first.
- [ ] Na žiadnej šírke nie je vodorovný scroll.
- [ ] Text je čitateľný na mobile aj na desktope.

---

## 13. Zhrnutie

| Nástroj | Kedy | Kľúčová vlastnosť |
| --- | --- | --- |
| Viewport | vždy | `width=device-width` |
| `%`, `rem` | šírky, písmo, medzery | relatívne k rodičovi alebo `html` |
| `clamp()` | plynulé písmo a medzery | min – preferované – max |
| `max-width` | kontajnery, obrázky | obmedzenie na veľkých obrazovkách |
| Flexbox | jeden riadok alebo stĺpec | `display: flex`, `gap`, `justify-content`, `align-items` |
| Grid | mriežka | `repeat()`, `fr`, `auto-fit` + `minmax()` |
| Media queries | iný layout pri šírke | `@media (min-width: …)` |
| Container queries | komponent podľa rodiča | `@container` |

---

## 14. Prepojenie s postupom práce

**Figma** (wireframe, rozloženie pre mobil a desktop) → **HTML** (štruktúra, viewport) → **CSS** (jednotky, Flexbox, Grid, media queries) → **BEM a CSS premenné** (`--farba-primary`) → **Git** (commit po každom kroku) → **nasadenie**.

Responzívnosť sa rieši už vo Figme, dolaďuje sa v CSS a overuje sa v DevTools.

---

## 15. Úlohy na precvičenie

1. **Čo sa stane, ak…?** Zmeň `minmax(250px, 1fr)` na `minmax(400px, 1fr)`. Koľko stĺpcov uvidíš na 1000px šírke?
2. **Oprava:** Kontajner má `width: 960px`. Oprav ho tak, aby sa na mobile nezobrazoval horizontálny scroll.
3. **Navigácia:** Pri šírke pod 768px sú odkazy pod sebou, od 768px vedľa seba. Napíš CSS mobile first.
4. **Galéria:** Vytvor mriežku 6 obrázkov, ktorá bude mať na mobile 1 stĺpec, na tablete 2 a na desktope 3.
5. **Hero sekcia:** Nastav výšku na `100svh` a over na mobilnom zobrazení v DevTools, že sekcia nepreteká.