# n8n AI Project Manager

Repository associato alla tesi magistrale:

**"Realizzazione di un agente AI per il supporto al Project Manager in ambito enterprise"**

Il progetto implementa un agente intelligente self-hosted progettato per supportare le attività informative e operative di un Project Manager in ambito enterprise.

La soluzione integra l'elaborazione di documenti ed e-mail con tecniche di Retrieval-Augmented Generation (RAG), consentendo l'interrogazione delle informazioni attraverso un'interfaccia conversazionale basata su Telegram.

L'architettura è stata progettata privilegiando l'esecuzione locale dei principali componenti, con l'obiettivo di limitare la trasmissione delle informazioni verso servizi esterni.

## Architettura

Il sistema è composto principalmente dai seguenti componenti:

- **n8n**, per l'orchestrazione dei workflow;
- **PostgreSQL + pgvector**, per la memorizzazione e il recupero delle informazioni;
- **Ollama**, per l'esecuzione locale dei modelli linguistici e di embedding;
- **Telegram**, come interfaccia conversazionale;
- **Docling**, per l'elaborazione dei documenti;
- servizi Python dedicati alla gestione di specifici formati documentali.

Il sistema utilizza inoltre una strategia di retrieval ibrida, combinando ricerca semantica e ricerca lessicale. Le classifiche ottenute vengono integrate mediante **Reciprocal Rank Fusion (RRF)**.

## Codice sorgente

Il codice sorgente e i file di configurazione sviluppati nell'ambito del progetto sono contenuti nell'archivio cifrato:

`AI-Agent-Thesis.7z`

La password necessaria per accedere all'archivio è riportata nell'elaborato di tesi associato al progetto.

L'archivio contiene una versione sanificata dell'ambiente utilizzato durante lo sviluppo e non include credenziali, dati personali, e-mail, documenti aziendali o database utilizzati durante la sperimentazione.

## Contenuto dell'archivio

```text
AI-Agent-Thesis/
├── compose.yaml
├── Dockerfile
├── Dockerfile.doc-converter
├── doc_converter.py
├── .env.example
├── .gitignore
│
├── p7m-parser/
│   ├── Dockerfile
│   └── app.py
│
├── pptx-parser/
│   ├── Dockerfile
│   ├── app.py
│   └── requirements.txt
│
└── workflows/
    ├── Esplora Drive.json
    ├── Q&A Telegram.json
    ├── RAG - Cerca Documenti Hybrid.json
    ├── SUB - Estrai ZIP ricorsivo.json
    └── TOOL - Cerca Email.json
```

## Workflow n8n

I workflow implementano le principali funzionalità dell'agente:

- **Esplora Drive** — acquisizione, elaborazione e indicizzazione dei documenti;
- **RAG - Cerca Documenti Hybrid** — retrieval ibrido basato su ricerca semantica e lessicale e fusione dei risultati mediante RRF;
- **TOOL - Cerca Email** — recupero delle informazioni dalla base dati delle e-mail;
- **Q&A Telegram** — interazione conversazionale, memoria dell'agente e generazione del recap giornaliero;
- **SUB - Estrai ZIP ricorsivo** — estrazione ricorsiva dei contenuti degli archivi ZIP.

## Servizi di elaborazione documentale

Il progetto comprende servizi dedicati alla gestione di specifici formati:

- **DOC Converter** — conversione dei documenti `.doc` in `.docx` mediante LibreOffice;
- **P7M Parser** — estrazione del contenuto dai documenti firmati digitalmente in formato `.p7m`;
- **PPTX Parser** — estrazione di titolo, testo e tabelle dalle slide PowerPoint.

## Configurazione

Per motivi di sicurezza, le credenziali utilizzate nell'ambiente originale non sono incluse.

Il file `.env.example` contiene le variabili necessarie alla configurazione dell'ambiente. Prima dell'esecuzione deve essere copiato in `.env` e opportunamente configurato.

È inoltre necessario configurare in n8n le credenziali relative ai servizi utilizzati, tra cui PostgreSQL, Google Drive, Telegram e Ollama.

Alcuni identificativi specifici dell'ambiente originale sono stati sostituiti con valori placeholder e devono essere configurati prima dell'utilizzo.

## Avvio

Una volta configurato l'ambiente, i container possono essere avviati dalla directory principale mediante:

```bash
docker compose up -d --build
```

Nella configurazione predefinita, n8n è successivamente raggiungibile all'indirizzo:

```text
http://localhost:5678
```

I workflow presenti nella directory `workflows/` possono quindi essere importati all'interno di n8n e associati alle rispettive credenziali.

## Modelli

L'architettura utilizza **Ollama** per l'esecuzione locale dei modelli.

Per la generazione degli embedding utilizzati nel retrieval semantico viene impiegato **bge-m3**.

Il modello linguistico può essere configurato nei relativi nodi n8n in funzione delle risorse hardware disponibili e delle esigenze sperimentali.

## Contesto accademico

Il progetto è stato sviluppato nell'ambito di una tesi magistrale e ha finalità di studio e sperimentazione.

Per una descrizione completa dell'architettura, delle scelte progettuali, dei workflow implementati e delle attività di validazione si rimanda all'elaborato di tesi associato al repository.
