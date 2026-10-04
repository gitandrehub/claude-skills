# Struttura della guida

Adatta i titoli al dominio (vedi [PROJECT-TYPES.md](PROJECT-TYPES.md)), ma mantieni
l'ordine. Esempi di titolo: "Da un clic su Paga all'ordine salvato", "Dal CSV grezzo alla
dashboard", "Dal sensore al pacchetto radio". Le sezioni marcate *(se serve)* si
omettono quando non c'è materiale reale: meglio una sezione in meno che una riempita a vuoto.

````md
# Da <ingresso> a <uscita>: guida semplice a <argomento>

Paragrafo d'apertura (3-5 righe): cosa fa **oggi** il codice, quale percorso segue la
guida (da dove parte il dato, dove arriva) e perché serve leggerla (es. capire dove si
perde/si duplica/si rompe qualcosa, per scegliere miglioramenti mirati).

I concetti da tenere separati sono:          ← (se serve) 2-4 concetti che si confondono
- **concetto A**: una riga;
- **concetto B**: una riga.

## Vista d'insieme

```text
<ingresso>
    │
    │  <trasformazione in parole>
    ▼
<stadio 1: cosa esce>
    │
    ▼
...
    ▼
<uscita>
```

Una o due frasi sulla conseguenza più importante della pipeline
(es. "uno stadio successivo non può recuperare informazione persa prima").

## 1. <Primo stadio: da dove arriva il dato>

Spiegazione semplice. Disegno ASCII se aiuta a visualizzare.

### Configurazione / parametri attuali     ← (se serve)

| Parametro | Valore | Significato |
|---|---:|---|

## 2. <Stadio successivo>

### 2.1 <Sotto-passo>
Cosa fa, con la costante in un blocco:

```text
NOME_COSTANTE = valore unità
```

Esempio numerico concreto del comportamento.

> **Limite chiave in grassetto**, se è uno dei punti critici del sistema.

### Risultato di questo stadio
Cosa esce, in che forma, cosa vale un dato "vuoto/non valido".

## N. Come leggere log / diagnostica           ← (se serve)

| Campo | Significato |
|---|---|

| Firma | Lettura probabile |
|---|---|

## N+1. Limiti attuali da tenere presenti

### <Stadio 1>
1. **Limite in breve.** Spiegazione e conseguenza concreta.

### <Stadio 2>
1. ...

## N+2. Spunti di miglioramento

Premessa: non vanno applicati tutti insieme; prima capire dove nasce il problema.

### Se il problema nasce in <stadio>
- idea concreta, legata al limite corrispondente.

## N+3. Metodo pratico per decidere cosa cambiare    ← (se serve)

1. Classificare il problema per stadio.
2. Metriche utili.
3. Sequenza di esperimenti: un cambiamento per volta.

## N+4. File principali

| Parte | File |
|---|---|
| <stadio o responsabilità> | `percorso/file.ext` |
````
