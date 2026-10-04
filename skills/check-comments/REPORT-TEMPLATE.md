# Formato del report

Il report deve essere leggibile da una persona e interpretabile da `/fix-comments`.
Rispetta esattamente intestazioni delle voci, casella `Applica` e blocchi di codice.

````md
# Verifica commenti: <percorso analizzato>

- **Data:** <YYYY-MM-DD>
- **Commit:** <hash corto, se repo git; altrimenti "non in git">
- **File controllati:** <N>
- **Non corrispondenze:** <N> (<n> contraddizioni, <n> valori errati, <n> riferimenti
  obsoleti, <n> fuorvianti, <n> possibili bug nel codice)

## Come usare questo report

Le caselle `[x] Applica` indicano le correzioni che `/fix-comments` applicherà.
Togli la `x` per saltare una voce. Puoi modificare il testo in "Commento proposto":
verrà usato così com'è. Le voci "Possibile bug nel codice" sono deselezionate: decidi tu
se correggere il commento o il codice.

## Riepilogo

| ID | Posizione | Tipo | Confidenza |
|---|---|---|---|
| C-001 | `src/retry.ts:14` | Valore errato | alta |

## Dettaglio

### C-001 · `src/retry.ts:14` · Valore errato · confidenza alta

- [x] Applica

**Commento attuale:**
```ts
// Riprova fino a 3 volte prima di arrendersi
```

**Cosa fa il codice:** riprova fino a 5 volte: `MAX_RETRY = 5` (`src/config.ts:8`),
usato nel ciclo a `src/retry.ts:16`.

**Commento proposto:**
```ts
// Riprova fino a 5 volte (MAX_RETRY) prima di arrendersi
```

---

### C-002 · `src/range.ts:31` · Possibile bug nel codice · confidenza alta

- [ ] Applica

**Commento attuale:**
```ts
// Include il valore massimo
```

**Cosa fa il codice:** il controllo è `value < max` (`src/range.ts:32`), quindi il
massimo è escluso.

**Perché potrebbe essere il codice a sbagliare:** il nome della funzione
(`isInRangeInclusive`) e i chiamanti a `src/form.ts:55` si aspettano il massimo incluso.

**Commento proposto:**
```ts
// Esclude il valore massimo
```

---

## File controllati

- `src/retry.ts`
- `src/range.ts`
````

Regole di formato:

- ID progressivi `C-001`, `C-002`... nell'ordine dei file e delle righe.
- Il numero di riga è quello della **prima riga** del commento.
- Il blocco "Commento attuale" riporta il commento intero, carattere per carattere,
  con il linguaggio del file nel fence.
- "Perché potrebbe essere il codice a sbagliare" compare solo nelle voci di quel tipo.
