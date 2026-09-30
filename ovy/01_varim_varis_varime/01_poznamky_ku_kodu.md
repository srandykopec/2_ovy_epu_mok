# Recept – opakovanie HTML štruktúry a CSS premenných

## Čo sme dnes robili
Vytvorili sme stránku s receptom na omeletu (`index.html`) pomocou sémantických HTML značiek a naštýlovali ju podľa farebnej/fontovej predlohy (`style-guide.md`).

## Opakovanie
- **Sémantické značky** (`main`, `article`, `h1`/`h2`, `ul`, `ol`, `table`) – už poznáme, len sme ich použili v novom kontexte (recept namiesto vizitky/CV).
- **`normalize.css`** – zjednocuje predvolený vzhľad naprieč prehliadačmi, pridávame ho vždy pred vlastný `style.css`.
- **CSS premenné** (`:root { --stone-100: ...; }` + `var(--stone-100)`) – farby na jednom mieste, ľahšia zmena celej palety.
- **`@import url(...)`** na začiatku CSS – načítanie externého fontu z Google Fonts.
- Štýlovanie boxov cez `border-radius`, `padding`, farby v `hsl()`.

### CSS premenné – ako to funguje

CSS premenná je hodnota, ktorú si pomenujeme a môžeme ju použiť na viacerých miestach v štýloch. Definuje sa v selektore `:root` (platí pre celú stránku) a používa sa cez funkciu `var()`.

```css
:root{
  --stone-600: hsl(30, 10%, 34%);
}

body{
  color: var(--stone-600);
}
```

- `--stone-600` je názov premennej (musí začínať dvomi pomlčkami).
- `var(--stone-600)` na danom mieste "vloží" uloženú hodnotu.
- Výhoda: farbu zmeníš na **jednom mieste** (v `:root`) a zmení sa všade, kde sa premenná používa – nemusíš prechádzať celé CSS a hľadať každý výskyt farby.


## Otázky na opakovanie
- Na čo slúži `normalize.css` a prečo ho pridávame pred vlastný štýl?
- Ako by si pridal novú farbu do palety a použil ju v `h1`?
- Nájdi v CSS duplicitu a navrhni, ako by si ju zlúčil.
