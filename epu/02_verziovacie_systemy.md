# Git a GitHub – poznámky (2EPU)

## Verziovací systém

Program, ktorý si pamätá **históriu zmien** v projekte. Vieš sa vrátiť k starej verzii, vidíš **kto, kedy a čo** zmenil a viacerí môžu pracovať na jednom projekte bez chaosu.

Nahrádza súbory typu `projekt_final2_NAOZAJ_posledny.html`.

## Git vs. GitHub

| | **Git** | **GitHub** |
|---|---|---|
| Čo to je | program | webová služba |
| Kde beží | na tvojom počítači | na internete |
| Na čo slúži | sleduje históriu zmien | ukladá repozitáre online, umožňuje spoluprácu |
| Internet | netreba | treba |

**Git** = fotoaparát a album doma. **GitHub** = Instagram, kde albumy zdieľaš.

## Základné pojmy

- **Repozitár (repo)** – priečinok s projektom aj s jeho históriou. Môže byť **lokálny** (u teba) alebo **vzdialený** (na GitHube).
- **Commit** – uložená snímka projektu s krátkou správou (ako uloženie pozície v hre). Dobrá správa: *„Pridané menu na úvodnú stránku"*, zlá: *„zmeny"*.
- **Hash** – unikátny 40-znakový identifikátor každého commitu, napr. `a3f5c9e2b7d1…`. Nikdy sa neopakuje, v praxi stačí prvých 7 znakov (`a3f5c9e`).
- **Push** – pošle commity z počítača **na GitHub**.
- **Pull** – stiahne zmeny **z GitHubu** do počítača.

> ⚠️ **Commit ≠ Push.** Commit uloží zmenu len u teba (bez internetu). Kým neurobíš push, nikto iný ju nevidí.



## Spolupráca

Na GitHube je **jeden spoločný repozitár**, každý má svoju kópiu na počítači.

**Postup:** `pull` → práca → `commit` → `push`

> 🔑 Vždy najprv **`git pull`**, až potom pracuj.

- **Vetva (branch)** – samostatná odnož projektu na skúšanie nových vecí. Hlavná je `main`.
- **Pull request** – návrh na zlúčenie tvojej vetvy do `main`; ostatní zmeny skontrolujú.
- **Konflikt** – dvaja zmenili to isté miesto. Nie je to chyba, treba sa dohodnúť a vybrať správnu verziu.

## Úlohy

1. Aký je rozdiel medzi Gitom a GitHubom?
2. Prečo po `commit` zmeny ešte nevidia spolužiaci?
3. Na čo slúži hash?
4. Napíš príkazy, ktorými uložíš zmeny a pošleš ich na GitHub.
