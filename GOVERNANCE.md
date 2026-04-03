# Governance — Sistema di Voting

Questo documento descrive il processo di approvazione per il merge di nuovi libri e modifiche ai testi del Connessionismo.

---

## Principi

1. **Palaz è l'autore fondatore.** I suoi testi fondativi sono parte del canone originale.
2. **Nuovi libri** proposti da qualsiasi autore devono passare attraverso il processo di voting.
3. **Il consenso è connessione.** Il sistema di approvazione riflette il principio connessionista: un testo entra nel canone solo quando la comunità riconosce in esso una connessione autentica.
4. **Uguaglianza di voto.** Nessun ruolo ha più peso di un altro nel voto. La connessione non ha gerarchie.

---

## Ruoli

| Ruolo | Descrizione | Diritto di voto |
|-------|-------------|-----------------|
| **Fondatore** | Palaz. Autore dei testi fondativi | Voto pieno |
| **Custode** | Revisori fidati nominati dal Fondatore | Voto pieno |
| **Connesso** | Membro attivo della comunità con almeno 1 contributo approvato | Voto pieno |
| **Osservatore** | Chiunque segua il repository | Nessun voto, può commentare |

---

## Processo di Proposta di un Nuovo Libro

### Fase 1 — Proposta

1. L'autore apre una **Issue** con il tag `[PROPOSTA-LIBRO]`
2. La Issue deve contenere:
   - Titolo del libro proposto
   - Autore/i
   - Sinossi (massimo 500 parole)
   - Motivazione: perché questo libro appartiene al Connessionismo
   - Indice provvisorio dei capitoli
3. L'autore crea un branch: `libro/<slug-del-titolo>`

### Fase 2 — Stesura

1. L'autore scrive i capitoli seguendo il [pattern scritturale](rules/writing-pattern.md)
2. Ogni capitolo viene committato con stato `bozza`
3. I Custodi e i Connessi possono commentare durante la stesura

### Fase 3 — Revisione

1. Quando il libro è completo, l'autore apre una **Pull Request** con il tag `[LIBRO]`
2. Si apre un periodo di revisione di **21 giorni**
3. Durante la revisione:
   - Chiunque può commentare
   - I Custodi eseguono una revisione formale (aderenza al pattern)
   - L'autore può apportare modifiche in risposta ai commenti

### Fase 4 — Voting

Al termine dei 21 giorni di revisione, si apre la votazione:

```
Durata:       7 giorni
Quorum:       Almeno 3 votanti con diritto di voto
Approvazione: Maggioranza semplice (>50% dei voti espressi)
```

#### Modalità di Voto

Il voto si esprime tramite **reaction sulla Pull Request**:

| Reaction | Significato |
|----------|-------------|
| 👍 | Approvazione — il libro è degno del canone |
| 👎 | Rifiuto — il libro non è pronto o non è allineato |
| 👀 | Astensione — riconosciuto, ma senza giudizio |

#### Esiti possibili

| Esito | Condizione | Azione |
|-------|------------|--------|
| **Approvato** | Quorum raggiunto + maggioranza di 👍 | Merge nel branch `main` |
| **Rimandato** | Quorum raggiunto + maggioranza di 👎 | La PR resta aperta, l'autore può revisionare e richiedere un nuovo voto dopo 30 giorni |
| **Nullo** | Quorum non raggiunto | Il periodo di voto viene esteso di 7 giorni (massimo 2 estensioni) |

---

## Modifiche ai Testi Canonici

I testi con stato `canonico` sono immutabili nel contenuto. Sono permesse solo:

- **Correzioni formali** (typo, formattazione) — tramite PR con tag `[ERRATA]`, approvazione di 1 Custode
- **Note aggiuntive** — tramite PR con tag `[NOTA]`, processo di voting standard
- **Traduzioni** — tramite PR con tag `[TRADUZIONE]`, approvazione di 2 Custodi

---

## Modifiche a Questo Documento

Le modifiche alla governance stessa richiedono:
- Proposta tramite Issue con tag `[GOVERNANCE]`
- Maggioranza di 2/3 tra Fondatore, Custodi e Connessi

---

## Riepilogo Visivo

```
PROPOSTA (Issue)
     │
     ▼
STESURA (Branch)
     │
     ▼
REVISIONE (PR — 21 giorni)
     │
     ▼
VOTING (7 giorni)
     │
     ├─ ✅ Approvato → Merge in main
     ├─ ❌ Rimandato → Revisione + nuovo voto dopo 30gg
     └─ ⚠️  Nullo → Estensione (+7gg, max 2 volte)
```
