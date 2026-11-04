# 🌐 Responzívny web – poznámky

> 📘 Skupina 2EPU/OVY · Verzia 2
> 🔎 **Potrebuješ:** HTML základy (štruktúra, odkazy, obrázky) a CSS základy (selektory, farby, `padding`, `margin`).

---

## 🗺️ Obsah

- **Časť A – Základy:** čo je responzívnosť a prečo viewport
- **Časť B – Jednotky a šírky:** ako veľkosti prispôsobiť obrazovke
- **Časť C – Rozloženie:** Flexbox a Grid
- **Časť D – Prispôsobenie zariadeniu:** media queries
- **Časť E – Overenie a precvičenie:** testovanie, chyby, úlohy
- **Príloha – Nad rámec:** moderné nástroje pre pokročilých

---

# 🅰️ Časť A – Základy

## 🤔 Čo je responzívna stránka?

Stránka, ktorá sa **automaticky prispôsobí veľkosti obrazovky** 📱💻🖥️.

| ❌ Neresponzívna | ✅ Responzívna |
| --- | --- |
| Pevná šírka, na mobile treba scrollovať do strán | Obsah sa zmestí na šírku obrazovky |
| 3 stĺpce aj na malom displeji | 3 stĺpce na PC → 1 stĺpec na mobile |

💡 **Jeden HTML a jeden CSS majú fungovať na všetkých zariadeniach.**

## 🚨 Viewport meta tag – povinný riadok

Pridaj do `<head>` **každej** stránky ako **prvý**:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**Čo robí:** Hovorí mobilu, aby použil svoju šírku. Bez neho sa zobrazí zmenšený desktop a text je nečitateľný 🔍.

```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Moja stránka</title>
</head>
```

---

# 🅱️ Časť B – Jednotky a šírky

## 📏 Fixné a relatívne jednotky

| Typ | Jednotka | Správanie | Použitie |
| --- | --- | --- | --- |
| 🧱 Fixná | `px` | Vždy rovnaká veľkosť | Tenké čiary, ikony |
| 🌊 Relatívna | `%` | Podľa rodiča | Šírky kontajnerov |
| 🌊 Relatívna | `rem` | Podľa základného písma v `html` | Písmo, medzery |

❌ **Zle:** `width: 960px` → na mobile (375px) vznikne horizontálny scroll.

✅ **Dobre:** `width: 90%` a `max-width: 1200px`.

### 🧩 Pravidlo pre písmo a medzery

```css
html {
  font-size: 100%;   /* zachová nastavenie prehliadača (zvyčajne 16px) */
}

h1 {
  font-size: 2rem;   /* 2 × základ */
}
```

👵 Ak používateľ zväčší písmo v prehliadači, všetky hodnoty v `rem` sa zväčšia.

## 📦 Kontajner: `max-width`

```css
.container {
  width: 90%;          /* na mobile 90 % šírky */
  max-width: 1200px;   /* na veľkých obrazovkách nie viac */
  margin: 0 auto;      /* centrovanie */
}
```

| Zariadenie | Šírka okna | Šírka kontajnera |
| --- | --- | --- |
| 📱 Mobil | 375px | 337px |
| 🖥️ Desktop | 1920px | 1200px |

## 🖼️ Obrázky

```css
img {
  max-width: 100%;   /* nikdy nepresiahne rodiča */
  height: auto;      /* zachová pomer strán */
}
```

```html
<img src="foto.jpg" alt="Krajina pri západe slnka">
```

---

# 🅲 Časť C – Rozloženie

## 💪 Flexbox – jeden smer (riadok alebo stĺpec)

### 🔹 Tri pojmy

- **Flex kontajner** – rodič s `display: flex`
- **Hlavná os** – smer, kam sa prvky radia (predvolene vodorovne ➡️)
- **Priečna os** – kolmo na hlavnú (predvolene zvisle ⬇️)

### 🔹 Najdôležitejšie vlastnosti

```css
.kontajner {
  display: flex;               /* 1. aktivácia */
  gap: 1.25rem;                /* 2. medzery medzi prvkami */
  justify-content: center;     /* 3. zarovnanie na hlavnej osi */
  align-items: center;         /* 4. zarovnanie na priečnej osi */
}
```

### 🧭 Zmena smeru

```css
.kontajner {
  display: flex;
  flex-direction: column;      /* hlavná os sa zmení na zvislú */
}
```

💡 **Kľúčové:** Po zmene na `column` ovláda `justify-content` zvislé zarovnanie a `align-items` vodorovné.

### 🧪 Príklad: navigácia

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

✅ **Výsledok:** Odkazy sú vedľa seba a zvislo zarovnané.

---

## 🎨 Grid – mriežka (riadky aj stĺpce)

### 🧩 Grid v 3 krokoch

1. 🟦 `display: grid`
2. 📊 `grid-template-columns: repeat(3, 1fr)`
3. 🧩 `gap: 1.25rem`

```
┌─────────┬─────────┬─────────┐
│ Prvok 1 │ Prvok 2 │ Prvok 3 │
├─────────┼─────────┼─────────┤
│ Prvok 4 │ Prvok 5 │ Prvok 6 │
└─────────┴─────────┴─────────┘
```

### ✨ Jednotka `fr`

- `1fr 1fr 1fr` = 3 rovnaké stĺpce
- `1fr 2fr 1fr` = stredný je 2× širší
- `repeat(3, 1fr)` = skratka za `1fr 1fr 1fr`

### 🪄 Responzívna galéria bez media queries

```css
.galeria {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.25rem;
}
```

- `minmax(250px, 1fr)` – stĺpec má aspoň 250px
- `auto-fit` – toľko stĺpcov, koľko sa zmestí

⚠️ Na úzkom displeji môže prvok pretiecť. Vtedy použi `minmax(min(250px, 100%), 1fr)`.

---

## 🔀 Flexbox alebo Grid?

| Situácia | Nástroj |
| --- | --- |
| Menu, tlačidlá, hlavička | 💪 Flexbox |
| Galéria, karty produktov | 🎨 Grid |

---

# 🅳 Časť D – Prispôsobenie zariadeniu

## 📱 Media queries

**Problém:** Na mobile chceš navigáciu pod sebou, na desktope vedľa seba. Jeden CSS štýl nevie, na akom zariadení beží.

**Riešenie:** Podmienka „ak je okno aspoň X široké, použi tieto štýly“.

```css
@media (min-width: 768px) {
  /* štýly pre okno od 768px */
}
```

## 🧭 Mobile first

1. Základný CSS píšeš pre **mobil** (bez media query).
2. Väčšie obrazovky pridávaš cez `min-width`.

```css
/* 📱 Mobil – základ */
.nav {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

/* 🖥️ Od 768px */
@media (min-width: 768px) {
  .nav {
    flex-direction: row;
    gap: 2rem;
  }
}
```

## 📏 Breakpointy

- **Breakpoint** = šírka, pri ktorej sa layout zmení 💡
- `768px` a `1024px` sú **štartovací body**, nie pravidlo
- Postup: zväčšuj okno a sleduj, **kedy sa obsah rozbije**. Vtedy pridaj breakpoint.

---

# 🅴 Časť E – Overenie a precvičenie

## 🧪 Ako testovať

1. 🛠️ **F12** → **Toggle device toolbar** (Ctrl + Shift + M)
2. 📱 Vyber zariadenie alebo zadaj šírku
3. ↔️ Pomaly zväčšuj a zmenšuj okno
4. 👀 Skontroluj, že **nie je vodorovný scroll**

## ⚠️ Najčastejšie chyby

| ❌ Chyba | ✅ Riešenie |
| --- | --- |
| Chýba viewport | Pridaj riadok z časti A |
| `width: 960px` | `width: 90%` + `max-width` |
| Obrázok pretečie | `img { max-width: 100%; height: auto; }` |
| Všetko v `px` | Písmo a medzery v `rem` |

## ✅ Kontrolný zoznam

- [ ] 🏷️ Viewport meta tag je v každej stránke
- [ ] 📦 Kontajner má `max-width`
- [ ] 🖼️ Obrázky majú `max-width: 100%`
- [ ] 💪 Flexbox pre jeden smer, 🎨 Grid pre mriežku
- [ ] 📱 Media queries sú mobile first
- [ ] 👀 Na žiadnej šírke nie je vodorovný scroll

## 🧠 Úlohy

1. 🔍 **Čo sa stane, ak…?** Zmeň `minmax(250px, 1fr)` na `minmax(400px, 1fr)`. Koľko stĺpcov uvidíš na 1000px?
2. 🛠️ **Oprava:** Kontajner má `width: 960px`. Oprav ho, aby nebol scroll na mobile.
3. 🧭 **Navigácia:** Pod 768px pod sebou, od 768px vedľa seba. Napíš CSS mobile first.
4. 🖼️ **Galéria:** 6 obrázkov – 1 stĺpec na mobile, 2 na tablete, 3 na desktope.

---

# 🧰 Príloha – Nad rámec (pre rýchlejších)

> Tieto témy nie sú povinné. Použi ich, keď základy zvládaš.

### 📐 Pomer strán obrázka
```css
.karta-obrazok {
  aspect-ratio: 16 / 9;
  object-fit: cover;   /* vyplní rámček bez skreslenia */
}
```

### ✨ Plynulé písmo – `clamp()`
```css
h1 {
  font-size: clamp(1.75rem, 4vw, 3rem);   /* min – preferované – max */
}
```

### 📱 Výška na mobile – `svh`
```css
.hero {
  min-height: 100svh;   /* nepreteká pri lištách prehliadača */
}
```
❌ `height: 100vh` na mobile môže spôsobiť, že sekcia „poskakuje“.

### 📦 Container queries
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
💡 Media query reaguje na **okno**, container query na **rodiča**.

### 🐢 Redukovaný pohyb
```css
@media (prefers-reduced-motion: reduce) {
  * {
    animation: none !important;
    transition: none !important;
  }
}
```

---

## 🔗 Kde sa responzívnosť rieši v projekte

🎨 **Figma** (frame pre mobil a desktop) → 🧱 **HTML** (viewport) → 🎨 **CSS** (jednotky, Flexbox, Grid, media queries) → 🌿 **Git** (commit po každom kroku) → 🚀 **nasadenie**
