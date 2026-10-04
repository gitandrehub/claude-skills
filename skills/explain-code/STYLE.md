# Regole di stile

## Tono

- Scrivi per un collega intelligente che non ha mai visto questo codice.
- Frasi brevi, voce attiva, niente marketing ("robusto", "potente", "elegante").
- Ogni termine tecnico o sigla del dominio va spiegato la prima volta, in una frase.
- Usa "oggi", "attualmente", "non ancora" per distinguere lo stato del codice dalle intenzioni.

## Cosa rende la guida utile

1. **Segui il flusso, non i file.** Le sezioni sono gli stadi del flusso, nell'ordine in cui
   il dato li attraversa. I file compaiono solo nella tabella finale (e come riferimento
   puntuale quando serve).
2. **Valori reali.** Ogni soglia, costante, variabile d'ambiente, timeout o limite con
   nome, valore e unità, in un blocco `text`. Se il valore arriva da env/config, dì da dove
   e qual è il default:
   ```text
   MAX_RETRY = 3 tentativi          (default in config.py, sovrascrivibile da env)
   ```
3. **Esempi concreti.** Per ogni regola non banale, un mini esempio con valori veri:
   "con timeout 5 s e 3 retry con backoff doppio, una chiamata che non risponde blocca
   l'utente per 5 + 10 + 20 = 35 s prima dell'errore".
4. **Disegni ASCII** per pipeline, diagrammi di sequenza, stati della UI, macchine a
   stati, strutture dati. Sempre in blocchi ```` ```text ````.
5. **Cosa NON fa.** Dichiara esplicitamente ciò che viene letto o calcolato ma non usato
   ("il valore X viene letto ma oggi non partecipa alla decisione"), e ciò che uno stadio
   riceve rispetto a ciò che ignora.
6. **Conseguenze.** Dopo i passaggi importanti, una frase "Una conseguenza importante è...".
7. **Ambiguità visibili.** Contraddizioni fra codice, docs e nomi → blocco
   `> Punto da verificare: ...` con le due versioni e come verificarlo.
8. **Limiti e miglioramenti divisi per stadio**, così chi legge un log sa dove guardare.
   I miglioramenti sono legati a un limite preciso, mai generici ("aggiungere test").
9. **Tabelle** per parametri, campi di log, mappatura parte→file. Prosa per i ragionamenti.

## Da evitare

- Elencare funzioni/file uno per uno senza raccontare il flusso.
- Parafrasare il codice riga per riga: spiega lo scopo di ogni passo e le regole.
- Inventare valori, comportamenti o motivazioni non presenti nel codice.
- Sezioni vuote o di riempimento ("Conclusioni", "Best practice").
- Gergo non spiegato, frasi in inglese quando esiste un termine italiano chiaro
  (i nomi di costanti, funzioni e campi restano invariati).

## Checklist finale

- [ ] Il titolo dice da dove a dove va il flusso.
- [ ] La vista d'insieme ASCII c'è e corrisponde alle sezioni numerate.
- [ ] Ogni costante citata ha valore e unità ed è stata letta nel codice.
- [ ] Almeno un esempio numerico per ogni regola non banale.
- [ ] Le cose calcolate ma non usate sono dichiarate.
- [ ] Le contraddizioni sono marcate "Punto da verificare", non risolte a intuito.
- [ ] Limiti e miglioramenti sono divisi per stadio e collegati fra loro.
- [ ] La tabella dei file copre ogni stadio descritto.
- [ ] Un collega che non conosce il codice capirebbe il flusso leggendo solo
      titolo, vista d'insieme e primi paragrafi di ogni sezione.
