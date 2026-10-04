---
name: explain-code
description: Legge una cartella o un progetto e scrive una guida semplice, step by step, che segue il dato dall'ingresso all'uscita e spiega cosa fa oggi il codice, dove può rompersi e cosa si potrebbe migliorare. Use when the user asks to explain, read, summarize or walk through a folder, project, module or pipeline ("spiegami cosa fa", "leggi il codice e fammi un riassunto", "guida semplice", "step by step"), or invokes /explain-code.
argument-hint: "<cartella> [focus: flusso o domanda specifica]"
---

# Explain Code

Produce una guida in Markdown che fa capire a un umano **cosa fa oggi** il codice,
seguendo passo per passo una cosa che entra nel sistema (dato, richiesta, evento, azione
dell'utente) finché non ne esce. Non è una review e non è una reference API: è il
documento che si legge per capire il sistema e decidere dove intervenire.
Funziona su qualsiasi tipo di progetto: firmware, backend, frontend, pipeline dati, CLI,
librerie, infrastruttura.

## Quick start

```
/explain-code src/checkout
/explain-code . "cosa succede quando l'utente fa login"
/explain-code .            ← progetto intero: guida panoramica + flussi principali
```

## Workflow

Copia questa checklist e seguila:

- [ ] **1. Perimetro.** Individua la cartella e il focus. Se la cartella contiene più flussi
      indipendenti e l'utente non ha indicato quale, chiedi quale spiegare (una domanda,
      con le opzioni trovate). Un documento = un flusso.
- [ ] **2. Orientamento.** Leggi README, CLAUDE.md, docs esistenti, manifest (package.json,
      pyproject, CMakeLists, Dockerfile...) e la struttura delle cartelle. Riconosci il
      tipo di progetto e apri [PROJECT-TYPES.md](PROJECT-TYPES.md) per sapere cosa seguire,
      dove sono i punti d'ingresso e quali dettagli contano.
- [ ] **3. Segui il flusso.** Parti dall'ingresso e leggi davvero il codice, funzione per
      funzione, fino all'uscita. Per ogni stadio annota: input, trasformazione, output,
      configurazione con il suo valore (costanti, env var, timeout, limiti), condizioni
      di scarto o di errore, file:riga.
      Annota anche cosa viene calcolato o letto **ma non usato**.
      Su progetti grandi puoi usare sotto-agenti Explore per mappare gli stadi, ma ogni
      affermazione che finisce nella guida va verificata leggendo tu il codice.
- [ ] **4. Confronta con la documentazione.** Se docs, commenti o nomi contraddicono il
      codice, non scegliere: segnala con un blocco `> Punto da verificare:`.
- [ ] **5. Scrivi la guida** seguendo [TEMPLATE.md](TEMPLATE.md) e le regole di
      [STYLE.md](STYLE.md).
- [ ] **6. Salva il file** (vedi sotto) e rispondi in chat con: percorso del file,
      il flusso in 3-5 righe, i 2-3 limiti più importanti trovati.
- [ ] **7. Autocontrollo** con la checklist finale di STYLE.md prima di dichiarare finito.

## Dove salvare

1. Se il progetto ha già una cartella di documentazione (`Docs/`, `docs/`, ...), usa la
   sua convenzione: sottocartella più adatta (es. `architecture/`) e stile dei nomi file.
   Se c'è un indice (README della cartella docs), aggiungi la voce.
2. Altrimenti crea `docs/guides/<argomento>-guide.md`.
3. Se l'utente chiede solo una spiegazione in chat, non creare file.

## Regole non negoziabili

- Descrivi il codice **com'è oggi**, non come dovrebbe essere né come dicono i commenti.
- Ogni numero, soglia o comportamento citato deve venire dal codice letto, con il file
  nella tabella finale. Se non sei sicuro, scrivi che va verificato: non inventare.
- Lingua: quella dell'utente (default italiano), semplice, ogni termine tecnico spiegato
  alla prima occorrenza.
- Separa sempre ciò che il sistema **fa** dai **limiti** e dai **miglioramenti**: non
  mescolare critiche nella descrizione del flusso, salvo le conseguenze importanti.
