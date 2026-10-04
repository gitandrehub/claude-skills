---
name: explain-code-documentation
description: Variante di explain-code che scrive la stessa guida semplice e step by step di una cartella o di un progetto, ma come pura documentazione: descrive solo cosa fa oggi il codice, senza limiti, punti da verificare né proposte di miglioramento. Use when the user wants documentation of a folder, project, module or flow without suggestions ("documenta", "scrivi la documentazione", "senza migliorie", "solo cosa fa"), or invokes /explain-code-documentation.
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

1. **Niente proposte né limiti.** Ometti le sezioni "Limiti attuali", "Spunti di
   miglioramento" e "Metodo pratico per decidere cosa cambiare". In nessun punto del
   documento scrivere cosa si dovrebbe, potrebbe o converrebbe cambiare, né elenchi di
   limiti o punti deboli. Le frasi "Una conseguenza importante è..." restano solo se
   spiegano come si comporta il sistema, non se lo giudicano.
2. **Niente "Punto da verificare".** Se codice e documentazione esistente si contraddicono,
   nel documento descrivi solo ciò che fa il codice. Segnala la contraddizione
   esclusivamente nella risposta in chat, in una riga.
3. **Tono neutro.** Evita parole valutative ("debole", "fragile", "problema", "purtroppo",
   "migliorabile", "limite"). Descrivi il comportamento e lascia la valutazione al lettore.
4. **Apertura.** Il paragrafo iniziale dice cosa documenta la guida e per chi è utile
   (uso, manutenzione, onboarding), non "dove intervenire".
5. **Risposta in chat:** percorso del file, flusso in 3-5 righe ed eventuali
   contraddizioni con la documentazione esistente. Niente elenco di limiti.
6. **Checklist di STYLE.md:** ignora le voci su "Punto da verificare" e su limiti e
   miglioramenti divisi per stadio.

## Autocontrollo aggiuntivo

- [ ] Cercando nel documento "dovrebbe", "potrebbe", "converrebbe", "migliorare",
      "proposta", "suggerimento", "limite", "da verificare" non resta nulla di valutativo.
- [ ] Non ci sono sezioni di limiti, vincoli, miglioramenti o punti da verificare.
