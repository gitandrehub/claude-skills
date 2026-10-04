# Adattare la guida al tipo di progetto

Il metodo è sempre lo stesso: **segui una cosa che entra nel sistema finché non ne esce**.
Cambia solo che cosa è "la cosa", dove si entra e quali dettagli contano.
Se il progetto non rientra in nessuna riga, scegli quella più vicina e dichiaralo.

| Tipo | Cosa segui | Ingressi da cercare | Uscita |
|---|---|---|---|
| Firmware / embedded | un campione di sensore, un interrupt, un comando | `main`, task RTOS, ISR, macchine a stati | attuatore, pacchetto radio/seriale, stato salvato |
| Backend / API | una richiesta | router, controller, handler, middleware | risposta, scrittura su DB, messaggio su coda |
| Frontend / app mobile | un'azione dell'utente | componenti di pagina, event handler, store, routing | ciò che viene mostrato, chiamate di rete, stato locale |
| Pipeline dati / ETL / ML | un record o un batch | script/job, DAG, notebook, `train`/`predict` | file, tabella, modello, metrica |
| CLI / script | un'invocazione del comando | parser degli argomenti, `main` | output a terminale, file scritti, exit code |
| Libreria / SDK | una chiamata dell'API pubblica | funzioni/classi esportate | valore restituito, errori sollevati, side effect |
| Sistema a eventi / worker | un messaggio | consumer, subscriber, scheduler/cron | messaggi emessi, stato persistito |
| Infrastruttura (IaC, CI/CD) | un deploy o una pipeline di build | workflow CI, moduli Terraform/Helm, Dockerfile | risorse create, artefatti, ambienti |

## Cosa diventano le sezioni del template

| Sezione | Firmware | Backend / frontend / dati |
|---|---|---|
| Configurazione e parametri | costanti `#define`, registri, parametri runtime | variabili d'ambiente, file di config, feature flag, timeout, retry, limiti, dimensioni di pagina/batch |
| Esempi numerici | soglie in mm, ms, campioni | timeout, retry con backoff, limiti di rate, dimensioni batch, TTL della cache |
| Disegno ASCII | pipeline del segnale, griglia, macchina a stati | pipeline, diagramma di sequenza (client → API → DB), stati della UI, schema delle tabelle toccate |
| Diagnostica | log seriale, contatori, LED | log, metriche, codici di errore HTTP, eventi di analytics, messaggi in dead-letter |
| Limiti tipici da cercare | buffer, timing, perdita di dati fra stadi | errori ingoiati, race condition, N+1 query, assenza di idempotenza, validazione mancante, stato duplicato fra client e server |

## Progetti con più flussi

Un'applicazione intera ha quasi sempre più flussi (login, checkout, sincronizzazione...).

- Se l'utente indica un flusso: una guida su quello.
- Se chiede "spiegami il progetto": scrivi prima una **guida panoramica** con la vista
  d'insieme dei componenti, l'elenco dei flussi principali (una riga ciascuno, con il punto
  d'ingresso) e i file chiave. Poi proponi quale flusso approfondire in una guida dedicata.

## Diagramma di sequenza ASCII (per richieste e chiamate tra servizi)

```text
Browser          API                 DB             Coda
   │  POST /ordini  │                  │               │
   │───────────────▶│  INSERT ordine   │               │
   │                │─────────────────▶│               │
   │                │  evento creato   │               │
   │                │─────────────────────────────────▶│
   │   201 Created  │                  │               │
   │◀───────────────│                  │               │
```
