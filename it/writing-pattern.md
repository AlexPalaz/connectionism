# Pattern Scritturale

Questo documento definisce le regole formali per la stesura di ogni file Markdown all'interno dei libri del Connessionismo.

---

## 1. Frontmatter

Ogni capitolo **deve** iniziare con un blocco YAML frontmatter:

```yaml
---
book: "Il Libro di Palaz"
chapter: 1
title: "Titolo del Capitolo"
author: "Palaz"
status: "draft"          # draft | review | approved | canonical
version: "0.1.0"
created: "YYYY-MM-DD"
modified: "YYYY-MM-DD"
---
```

### Campi obbligatori

| Campo | Tipo | Descrizione |
|-------|------|-------------|
| `book` | string | Nome del libro di appartenenza |
| `chapter` | int | Numero progressivo del capitolo |
| `title` | string | Titolo del capitolo |
| `author` | string | Autore originale |
| `status` | enum | Stato del testo (vedi sezione 6) |
| `version` | semver | Versione del capitolo |
| `created` | date | Data di prima stesura |
| `modified` | date | Data dell'ultima modifica |

---

## 2. Struttura del Capitolo

Ogni capitolo segue questa struttura:

```markdown
# Capitolo N — Titolo

> Epigrafe o citazione introduttiva (opzionale)

## Corpo del testo

Il contenuto principale del capitolo.

### Sottosezioni

Se necessario, il testo può essere diviso in sottosezioni con `###`.

---

## Versetti

Se il capitolo contiene insegnamenti o precetti numerati, usare il formato versetto:

**1.** Testo del primo versetto.

**2.** Testo del secondo versetto.

---

## Nota del capitolo

Note contestuali, riferimenti interni o chiarimenti dell'autore.
```

---

## 3. Convenzioni Tipografiche

### Gerarchia dei titoli
- `#` — Titolo del capitolo (uno solo per file, formato: `Capitolo N — Titolo`)
- `##` — Sezioni principali del capitolo
- `###` — Sottosezioni
- `####` — Non usare oltre il terzo livello

### Formattazione del testo
- **Grassetto** per concetti fondamentali introdotti per la prima volta
- *Corsivo* per enfasi, termini stranieri, o riferimenti a concetti già definiti
- `Codice inline` non va usato nei testi sacri
- Le citazioni usano il blocco `>`
- I separatori `---` dividono le sezioni principali

### Versetti e precetti
- I versetti sono numerati con **N.** in grassetto
- Ogni versetto è separato da una riga vuota
- Un capitolo può contenere sia prosa libera che versetti

---

## 4. Naming dei File

Il nome del file segue il pattern:

```
NN-nome-breve.md
```

- `NN` — Numero del capitolo con zero-padding a 2 cifre (00, 01, 02...)
- `nome-breve` — Slug del titolo in kebab-case
- Il capitolo `00` è sempre riservato alla prefazione del libro

Esempi:
- `00-prefazione.md`
- `01-la-connessione.md`
- `02-il-flusso.md`

---

## 5. Riferimenti Interni

Per riferirsi ad altri capitoli o libri:

```markdown
Come scritto nel [Capitolo 1 — La Connessione](01-la-connessione.md)...
```

Per riferimenti tra libri diversi:

```markdown
Come riportato nel [Libro di Palaz, Cap. 3](../../it/libro-di-palaz/03-capitolo.md)...
```

---

## 6. Ciclo di Vita del Testo

Ogni capitolo attraversa quattro stati:

```
draft → review → approved → canonical
```

| Stato | Significato |
|-------|-------------|
| `draft` | Prima stesura, soggetta a modifiche sostanziali |
| `review` | Testo stabile, in attesa di revisione comunitaria |
| `approved` | Approvato tramite il sistema di voting (vedi GOVERNANCE.md) |
| `canonical` | Testo definitivo. Non modificabile se non per correzioni formali |

---

## 7. Versionamento

Ogni capitolo segue il versionamento semantico:

- **MAJOR** (X.0.0) — Riscrittura sostanziale del capitolo
- **MINOR** (0.X.0) — Aggiunta di nuove sezioni o versetti
- **PATCH** (0.0.X) — Correzioni formali, typo, formattazione

---

## 8. Lingua

- I testi nella cartella `it/` sono scritti in italiano
- Si usa un registro solenne ma accessibile
- Si evitano anglicismi quando esiste un equivalente italiano
- Le future traduzioni vanno in cartelle dedicate (`en/`, `es/`, ecc.)
