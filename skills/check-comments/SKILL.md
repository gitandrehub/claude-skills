---
name: check-comments
description: Controlla che commenti, docstring e header di documentazione corrispondano a ciò che il codice fa davvero, e scrive un report Markdown con tutte le non corrispondenze (commento dice A, codice fa B) e una correzione proposta per ciascuna. Non modifica il codice. Use when the user asks to check, verify or audit comments against code ("i commenti sono allineati?", "controlla i commenti", "commenti obsoleti", "commento dice A e il codice B"), or invokes /check-comments. To apply the report afterwards, use fix-comments.
argument-hint: "<file o cartella>"
---

# Check Comments

Trova i commenti che **non dicono il vero** sul codice e li raccoglie in un report che
l'utente rivede prima di passarlo a `/fix-comments`. Il report è l'unico output: nessun
file sorgente viene toccato.

## Quick start

```
/check-comments src/payments
/check-comments App/detect/detect.c
```

## Cosa conta come non corrispondenza

| Tipo | Esempio |
|---|---|
| **Contraddizione** | "restituisce null se non trovato" ma il codice lancia un'eccezione |
| **Valore errato** | "riprova 3 volte" ma `MAX_RETRY = 5`; unità o soglie diverse |
| **Riferimento obsoleto** | cita parametri, funzioni, campi, file o flag che non esistono più o sono rinominati |
| **Fuorviante** | descrive solo una parte e porta a una conclusione sbagliata (omette un ramo, un side effect, un caso d'errore rilevante) |
| **Possibile bug nel codice** | il commento esprime un'intenzione chiara e plausibile, ed è il codice a sembrare sbagliato (es. "include il massimo" ma usa `<`) |

**Non segnalare:** commenti mancanti, stile, refusi, lingua, codice commentato, header di
licenza, TODO generici (solo se il TODO descrive qualcosa già fatto → riferimento obsoleto),
commenti vaghi ma non falsi.

## Workflow

- [ ] **1. Perimetro.** Elenca i file sorgente nel percorso (escludi vendor, build,
      generati, dipendenze, lock file). Se sono molti, dillo e procedi a gruppi.
- [ ] **2. Leggi ogni commento con il codice che descrive.** Docstring → tutta la funzione;
      commento inline → il blocco successivo; header (`.h`, interfacce, tipi) →
      l'implementazione. Se il commento parla di comportamento che sta altrove (costanti,
      funzioni chiamate, config), apri anche quello.
- [ ] **3. Verifica prima di segnalare.** Ogni voce deve citare la riga di codice che
      dimostra la differenza. Se dipende da runtime o configurazione esterna e non puoi
      confermarlo, confidenza "media"; se è solo un sospetto, non segnalarlo.
      Su cartelle grandi puoi dividere i file fra sotto-agenti, ma rileggi tu ogni voce
      prima di metterla nel report: i falsi positivi rendono il report inutilizzabile.
- [ ] **4. Proponi la correzione** del commento, allineata al codice, nello stesso stile,
      lingua e formato (Doxygen, JSDoc, docstring...) del commento originale.
      Per "Possibile bug nel codice" proponi comunque il testo, ma la casella resta vuota.
- [ ] **5. Scrivi il report** seguendo [REPORT-TEMPLATE.md](REPORT-TEMPLATE.md).
- [ ] **6. Rispondi in chat** con: percorso del report, numero di voci per tipo, elenco
      delle voci "Possibile bug nel codice" (sono quelle da guardare per prime).

## Dove salvare

`comment-check-<nome-cartella-o-file>.md` nella root del progetto (o del repo git).
Se esiste già, sovrascrivilo solo dopo aver avvisato l'utente; altrimenti aggiungi la data
al nome.

## Regole

- Non modificare nessun file sorgente.
- Cita il commento **esattamente** com'è nel file (serve a `/fix-comments` per ritrovarlo).
- Una voce per commento. Se lo stesso errore si ripete in più punti, una voce per punto.
- Se non trovi non corrispondenze, scrivi comunque il report con "Nessuna non
  corrispondenza trovata" e l'elenco dei file controllati.
