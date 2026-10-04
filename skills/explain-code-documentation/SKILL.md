---
name: explain-code-documentation
description: Variante di explain-code che scrive la stessa guida semplice e step by step di una cartella o di un progetto, ma come pura documentazione: descrive cosa fa oggi il codice e i suoi vincoli, senza proporre miglioramenti né modifiche. Use when the user wants documentation of a folder, project, module or flow without suggestions ("documenta", "scrivi la documentazione", "senza migliorie", "solo cosa fa"), or invokes /explain-code-documentation.
argument-hint: "<cartella> [focus: flusso o domanda specifica]"
---

# Explain Code — Documentation

Stessa guida di `explain-code`, ma è **documentazione**: racconta cosa fa il sistema e come
si comporta, per chi deve usarlo, mantenerlo o capirlo. Non giudica e non propone.

## Quick start

```
/explain-code-documentation src/checkout
/explain-code-documentation . "cosa succede quando l'utente fa login"
```

## Workflow

Segui il workflow, le regole e i file di `explain-code`, che si trovano nella cartella
sorella `../explain-code/`:

- workflow e regole: [../explain-code/SKILL.md](../explain-code/SKILL.md)
- struttura: [../explain-code/TEMPLATE.md](../explain-code/TEMPLATE.md)
- stile e checklist: [../explain-code/STYLE.md](../explain-code/STYLE.md)
- tipi di progetto: [../explain-code/PROJECT-TYPES.md](../explain-code/PROJECT-TYPES.md)

Se quella cartella non esiste, fermati e di' all'utente che va installata anche
`explain-code` (stesso repo).

## Differenze rispetto a explain-code

Queste regole prevalgono su quelle di `explain-code`:

1. **Niente proposte.** Ometti le sezioni "Spunti di miglioramento" e "Metodo pratico per
   decidere cosa cambiare". In nessun punto del documento scrivere cosa si dovrebbe,
   potrebbe o converrebbe cambiare, aggiungere o sostituire.
2. **I limiti diventano vincoli di comportamento.** La sezione "Limiti attuali" si chiama
   "Vincoli e comportamenti da conoscere" ed elenca fatti verificabili, divisi per stadio,
   senza giudizi né rimedi.
   - Sì: "Ogni cella produce al massimo un bersaglio: due oggetti nella stessa cella
     vengono riportati come uno."
   - No: "Ogni cella produce un solo bersaglio, il che è un limite: andrebbe esteso a due."
3. **Tono neutro.** Evita parole valutative ("debole", "fragile", "problema", "purtroppo",
   "migliorabile"). Descrivi la conseguenza e lascia la valutazione al lettore.
4. **"Punto da verificare" resta**, ma solo per contraddizioni fra codice e documentazione,
   formulato come domanda aperta, non come correzione.
5. **Apertura.** Il paragrafo iniziale dice cosa documenta la guida e per chi è utile
   (uso, manutenzione, onboarding), non "dove intervenire".
6. **Risposta in chat:** percorso del file e flusso in 3-5 righe. Niente elenco di limiti.

## Autocontrollo aggiuntivo

- [ ] Cercando nel documento "dovrebbe", "potrebbe", "converrebbe", "migliorare",
      "proposta", "suggerimento", "limite" non resta nessuna proposta.
- [ ] Ogni vincolo descritto è un fatto con la sua conseguenza, non un giudizio.
