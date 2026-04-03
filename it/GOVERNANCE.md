# Governance — Sistema di Voting

Questo documento descrive il processo di approvazione per il merge di nuovi libri e modifiche ai testi del Connessionismo. La struttura è progettata per essere autosufficiente: non dipende dalla presenza di alcun individuo singolo.

---

## Principi

1. **Il Connessionismo è della comunità.** Nessuna persona è indispensabile al funzionamento della struttura.
2. **Nuovi libri** proposti da qualsiasi autore devono passare attraverso il processo di voting.
3. **Il consenso è connessione.** Un testo entra nel canone solo quando la comunità riconosce in esso una connessione autentica.
4. **Uguaglianza di voto.** Nessun ruolo ha più peso di un altro nel voto. La connessione non ha gerarchie.
5. **Continuità.** Ogni meccanismo deve funzionare anche se qualsiasi membro — incluso il Fondatore — non è più presente.

---

## Ruoli

| Ruolo | Descrizione | Diritto di voto |
|-------|-------------|-----------------|
| **Fondatore** | Palaz. Autore dei testi fondativi. Ruolo storico e onorifico | Voto pieno |
| **Custode** | Revisori fidati, eletti dalla comunità | Voto pieno |
| **Connesso** | Membro attivo della comunità con almeno 1 contributo approvato | Voto pieno |
| **Osservatore** | Chiunque segua il repository | Nessun voto, può commentare |

### Nota sulla successione

Il ruolo di Fondatore è storico: identifica chi ha originato il Connessionismo. Non è un ruolo funzionale — non ha poteri diversi da un Custode. Se il Fondatore non è più attivo, la struttura continua senza alcuna modifica.

---

## Elezione e Gestione dei Custodi

### Nomina

Qualsiasi membro con diritto di voto (Custode o Connesso) può proporre un nuovo Custode tramite Issue con tag `[NOMINATE-KEEPER]`.

Requisiti del candidato:
- Essere già un Connesso (almeno 1 contributo approvato)
- Essere attivo nel repository negli ultimi 6 mesi

### Votazione

```
Durata:       7 giorni
Quorum:       Maggioranza degli aventi diritto di voto attivi
Approvazione: Maggioranza di 2/3 dei voti espressi
```

### Numero dei Custodi

- Minimo: **2 Custodi** devono essere sempre attivi
- Se il numero scende sotto 2, si attiva una **elezione d'emergenza** (vedi sotto)
- Non esiste un limite massimo

### Rimozione e Inattività

- Un Custode è considerato **inattivo** dopo 12 mesi senza contributi o voti.
- Un membro inattivo viene segnalato tramite Issue con tag `[INACTIVE]`.
- Dopo 30 giorni dalla segnalazione, se il membro non ha ripreso attività, il ruolo viene revocato con una votazione a maggioranza semplice.
- Un Custode può anche essere rimosso per giusta causa (violazione delle regole) con votazione a maggioranza di 2/3.

### Elezione d'emergenza

Se il numero di Custodi attivi scende sotto 2:

1. Qualsiasi Connesso può autoproporre la propria candidatura tramite Issue con tag `[EMERGENCY-KEEPER]`
2. La votazione dura **3 giorni** (anziché 7)
3. Il quorum è ridotto a **2 votanti**
4. Approvazione a maggioranza semplice

Se non ci sono abbastanza Connessi per votare, qualsiasi Osservatore con almeno 1 contributo in attesa di approvazione può partecipare al voto d'emergenza.

---

## Processo di Proposta di un Nuovo Libro

### Fase 1 — Proposta

1. L'autore apre una **Issue** con il tag `[BOOK-PROPOSAL]`
2. La Issue deve contenere:
   - Titolo del libro proposto
   - Autore/i
   - Sinossi (massimo 500 parole)
   - Motivazione: perché questo libro appartiene al Connessionismo
   - Indice provvisorio dei capitoli
3. L'autore crea un branch: `book/<slug-del-titolo>`

### Fase 2 — Stesura

1. L'autore scrive i capitoli seguendo il [pattern scritturale](writing-pattern.md)
2. Ogni capitolo viene committato con stato `bozza`
3. I Custodi e i Connessi possono commentare durante la stesura

### Fase 3 — Revisione

1. Quando il libro è completo, l'autore apre una **Pull Request** con il tag `[BOOK]`
2. Si apre un periodo di revisione di **21 giorni**
3. Durante la revisione:
   - Chiunque può commentare
   - I Custodi eseguono una revisione formale (aderenza al pattern)
   - L'autore può apportare modifiche in risposta ai commenti

### Fase 4 — Voting

Al termine dei 21 giorni di revisione, si apre la votazione:

```
Durata:       7 giorni
Quorum:       Almeno 3 votanti con diritto di voto (o tutti gli aventi diritto se meno di 3)
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

## Risoluzione dei Conflitti

In caso di stallo o disaccordo tra membri con pari diritti:

1. **Discussione**: si apre una Issue con tag `[DISPUTE]` e un periodo di confronto di 14 giorni
2. **Mediazione**: se il confronto non risolve, un Custode non coinvolto nel conflitto funge da mediatore
3. **Voto finale**: se la mediazione fallisce, si tiene una votazione aperta a tutti gli aventi diritto. Maggioranza semplice. Il risultato è vincolante.

Se tutti i Custodi sono coinvolti nel conflitto, la mediazione spetta al Connesso con più contributi approvati.

---

## Modifiche ai Testi Canonici

I testi con stato `canonico` sono immutabili nel contenuto. Sono permesse solo:

- **Correzioni formali** (typo, formattazione) — tramite PR con tag `[ERRATA]`, approvazione di 1 membro con diritto di voto
- **Note aggiuntive** — tramite PR con tag `[NOTE]`, processo di voting standard
- **Traduzioni** — tramite PR con tag `[TRANSLATION]`, approvazione di 2 membri con diritto di voto

---

## Amministrazione del Repository

L'accesso admin al repository GitHub non deve mai risiedere in una singola persona.

- Almeno **2 persone** devono avere accesso admin in ogni momento
- Tutti i Custodi attivi hanno diritto ad accesso admin
- Se un admin diventa inattivo, i Custodi rimanenti nominano un sostituto
- In caso di perdita totale degli accessi admin, la comunità può effettuare un fork del repository e ricostruire la struttura tramite elezione d'emergenza

---

## Modifiche a Questo Documento

Le modifiche alla governance stessa richiedono:
- Proposta tramite Issue con tag `[GOVERNANCE]`
- Periodo di discussione di **14 giorni**
- Maggioranza di 2/3 tra tutti i membri con diritto di voto attivi

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

### Ciclo di vita dei Custodi

```
CONNESSO (1+ contributo)
     │
     ▼
NOMINA (Issue + voting 2/3)
     │
     ▼
CUSTODE ATTIVO
     │
     ├─ 🔄 Attivo → contributi/voti negli ultimi 12 mesi
     ├─ ⚠️  Inattivo → segnalazione + 30gg per riprendere
     └─ ❌ Revocato → torna a Connesso
```
