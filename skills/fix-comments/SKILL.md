---
name: fix-comments
description: Applica un report prodotto da check-comments, riscrivendo i commenti selezionati perché corrispondano al codice, senza mai modificare il codice. Use when the user asks to fix, rewrite or align comments using a comment-check report ("sistema i commenti", "applica il report", "riscrivi i commenti seguendo il codice"), or invokes /fix-comments.
argument-hint: "<report .md> [ID da applicare, es. C-001,C-004 | tutte]"
---

# Fix Comments

Prende il report di `/check-comments` e riscrive i commenti marcati `[x] Applica`.
Tocca **solo commenti**: se una correzione richiederebbe di cambiare il codice, la salta.

Il formato del report è descritto in
[../check-comments/REPORT-TEMPLATE.md](../check-comments/REPORT-TEMPLATE.md).

## Quick start

```
/fix-comments comment-check-payments.md
/fix-comments comment-check-payments.md C-001,C-004
```

## Quali voci applicare

- Nessun ID indicato → tutte le voci con `- [x] Applica`.
- ID indicati → solo quelli, anche se la casella è vuota.
- "tutte" → tutte le voci **tranne** "Possibile bug nel codice", a meno che l'utente non
  le nomini esplicitamente.

## Workflow

- [ ] **1. Leggi il report** ed elenca le voci da applicare. Se il report non è nel
      formato atteso, fermati e dillo.
- [ ] **2. Per ogni voce, controlla che sia ancora valida:**
      - il commento attuale è ancora nel file, uguale a quello citato (anche se la riga è
        cambiata: cercalo vicino alla posizione indicata);
      - il codice fa ancora ciò che il report descrive.
      Se una delle due non vale più, salta la voce e annota il motivo.
- [ ] **3. Riscrivi il commento** con il testo di "Commento proposto" (l'utente può averlo
      modificato: usalo così com'è). Mantieni indentazione, stile, delimitatori e tag
      (`@param`, `\brief`, `"""`...). Non toccare altre righe.
- [ ] **4. Verifica che sia cambiato solo testo di commento.** Se il progetto è in git,
      controlla `git diff` dei file toccati: ogni riga modificata deve essere un commento.
      Se no, confronta prima/dopo leggendo i file.
- [ ] **5. Aggiorna il report:** sotto la casella di ogni voce aggiungi lo stato:
      `Stato: applicato` oppure `Stato: saltato — <motivo>`.
- [ ] **6. Rispondi in chat** con: voci applicate, voci saltate con motivo, file modificati.

## Regole

- Mai modificare codice, nemmeno per "sistemare" una voce "Possibile bug nel codice":
  in quel caso correggi solo il commento, e solo se l'utente l'ha chiesto.
- Non fare commit: lascia le modifiche all'utente.
- Non correggere altri commenti che noti strada facendo: segnalali in chat e suggerisci
  di rilanciare `/check-comments`.
