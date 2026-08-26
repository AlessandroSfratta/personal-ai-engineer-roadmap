# AI Engineer Roadmap

> Roadmap personale per costruire competenze da AI Engineer, con focus su software engineering, machine learning, LLM, Hugging Face, RAG, agenti AI, LLMOps, sicurezza e preparazione ai colloqui tecnici.
>
> Questa versione è pensata per LinkedIn e portfolio: mostra direzione, metodo, competenze e deliverable senza includere note operative personali.

## 🎯 Principio guida — AI Engineering production-first

Questa roadmap non punta a formare un semplice utilizzatore di framework AI, ma una figura capace di progettare, misurare, debuggare, deployare e mantenere sistemi AI reali.

Un AI Engineer professionale sa quando una baseline semplice basta, quando serve un vector database, quando usare un modello più piccolo, quando introdurre caching, routing, valutazione, tracing e failure analysis. AI Engineering è soprattutto software engineering con AI dentro: il modello è un componente del sistema, non tutta l'applicazione.

### Definition of Done trasversale per ogni progetto AI

- esiste una baseline semplice prima della soluzione complessa
- sono documentati i trade-off tecnici
- ci sono metriche di qualità
- ci sono test minimi o smoke test
- ci sono log strutturati
- sono gestiti errori, timeout e retry
- è presente un README orientato a produzione
- sono tracciabili failure case e limiti del sistema
- non si introduce un framework solo per moda
- ogni scelta tecnica risponde alla domanda: "serve davvero?"

Ultimo aggiornamento: 17/08/2026

## Come leggere la roadmap

Legenda stato:

- ✅ **Completata**: step già studiato e validato con output pratico
- ⏳ **In corso**: step attivo
- 🕒 **Pianificata**: step da affrontare

Legenda badge:

- 🟦 **MASTER**: moduli o progetti del percorso formativo principale
- 🟩 **DATACAMP**: corsi o capitoli di supporto pratico
- 🏆 **SUMMER AI CUP**: corsi intermedi separati dal Master, pianificati dopo gli Step 4 e 5
- 🟨 **CERT**: competenze mappate alla checklist AI Engineering
- 🔎 **RESEARCH**: studio autonomo da documentazione, paper, articoli o tutorial tecnici
- 👑 **KING PROGRAMMING**: fondamenti di Computer Science, algoritmi e Software Engineering integrati come core, approfondimento avanzato o specializzazione post-core; non è una certificazione e non riapre automaticamente gli step completati
- 🆕 **SKILLS**: competenze professionali aggiunte alla roadmap
- 🎓 **GH600**: risorsa per la certificazione GitHub Certified: Agentic AI Developer (esame GH-600), Step 25-28
- 🛠️ **BASWE**: progetto portfolio di riferimento dalla guida (italiana, da usare come riferimento) [`15-ai-engineering-projects-guide.it.md`](./15-ai-engineering-projects-guide.it.md) ("15 AI Engineering Projects That Actually Land Jobs") — originale inglese in [`15-ai-engineering-projects-guide.md`](./15-ai-engineering-projects-guide.md). Non è uno step da completare: è un blueprint collegato allo step. Mappa completa progetti→step in cima alla guida.

## Obiettivo

L'obiettivo è trasformare lo studio in una sequenza di progetti verificabili: codice, notebook, API, report, demo, checklist di produzione e preparazione ai colloqui.

Il percorso non è solo teorico. Ogni fase deve produrre almeno uno tra:

- repository portfolio
- notebook riproducibile
- API o servizio deployabile
- report tecnico
- checklist di qualità, sicurezza o produzione
- mock interview o risposta tecnica strutturata

## Stato attuale

| Stato | Area | Step |
| ----- | ---- | ---- |
| ✅ | Software Engineering foundations | Step 1-3 |
| ⏳ | Testing e manutenibilità | Step 4 |
| 🕒 | Reliability Engineering | Step 5 |
| 🕒 | Summer AI Cup: Fondamenti ML + Agentic AI Foundations | checkpoint dopo Step 5 |
| 🕒 | ML, LLM, RAG, Agentic AI, LLMOps | Step 6-23 |
| 🕒 | Portfolio UI opzionale | Step 24 |
| 🕒 | Certificazione GitHub Agentic AI Developer (GH-600) | Step 25-28 |

## Percorsi Master Integrati

La roadmap integra i percorsi del Master Development dentro una sequenza orientata a progetti.

| Percorso | Step | Ruolo |
| -------- | ---- | ----- |
| Coding avanzato con Python | Step 4-5 | Software engineering, testing, logging |
| Fondamenti di AI per sviluppatori | Step 6-8 | Machine learning e NLP di base |
| REST API per Machine Learning | Step 9-10 | Serving e produzione di modelli |
| Database relazionali con SQL | Step 11-12 | Data analysis e reportistica |
| NoSQL per elaborazione dati | Step 13-14 | Data processing e dati semi-strutturati |
| Large Language Models | Step 15, 17, 19, 20 | LLM, prompt engineering e RAG |
| Hugging Face Transformers | Step 15, 15.5 | Foundation models, tokenization, fine-tuning |
| Agentic AI | Step 21-22 | Agenti, memoria, tool use e deploy |
| DevOps e ciclo di vita software | Step 10, 22 | CI/CD, monitoraggio, sicurezza |
| MERN su Vercel | Step 24 | UI/demo opzionale per portfolio |

## Percorsi DataCamp Integrati

DataCamp viene usato come pratica guidata a supporto degli step, senza sostituire progetti e deliverable.

| Percorso DataCamp | Step | Stato pubblico |
| ----------------- | ---- | -------------- |
| Introduzione all'API di OpenAI | Step 16 | Pianificato |
| Prompt Engineering con l'API di OpenAI | Step 17-18 | Pianificato |
| Introduzione a Hugging Face | Step 15, 15.5 | Pianificato |
| LLMOps e ciclo di vita delle applicazioni LLM | Step 22 | Pianificato |
| Sviluppare applicazioni AI con l'API di OpenAI | Step 16, 22, 14 | Pianificato |
| Embeddings con l'API di OpenAI | Step 19-20 | Pianificato |
| Database vettoriali per Embeddings con Pinecone | Step 20 | Pianificato |
| Ingegneria del Software per Data Science in Python | Step 2-4 | Completato, da rivedere |
| Sviluppare applicazioni LLM con LangChain | Step 20-21 | Pianificato |

## Summer AI Cup - Corsi intermedi

La Summer AI Cup è un percorso separato dal Master. I due corsi sono già inseriti nella roadmap e verranno svolti, in questo ordine, dopo aver completato gli Step 4 e 5:

- 🕒 **Fondamenti del Machine Learning** - 0%, 0/6 moduli
- 🕒 **Agentic AI Foundations** - 0%, 0/4 moduli

**Cosa abbiamo appreso dalla Summer AI Cup**

- analisi dei dataset e gestione dei dati mancanti
- preprocessing, encoding e scaling delle feature
- regressione, classificazione, metriche e cross-validation
- overfitting, regolarizzazione, bias-varianza e clustering
- differenza tra LLM, workflow e agente AI
- agentic loop, planning, memoria e output strutturato
- tool calling con LiteLLM, JSON Schema e Pydantic
- pattern ReAct, Plan & Execute e Reflexion
- LangChain, LangGraph, checkpoint e human-in-the-loop

## Percorso King Programming Integrato

La roadmap integra anche una traccia progressiva di Computer Science e Software Engineering. I contenuti fondamentali entrano negli step operativi; gli argomenti algoritmici e sistemistici più avanzati restano approfondimenti post-core, senza trasformare il percorso AI in una lista di nozioni da memorizzare.

| Area | Step principali | Integrazione |
| --- | --- | --- |
| Fondamenti di programmazione e strumenti | Step 1-5 | linguaggio, Git, Clean Code, debugging, testing, refactoring e reliability |
| Strutture dati e algoritmi | Step 2, 6, 23 | Big-O, strutture dati, sorting/searching, ricorsione, grafi, paradigmi algoritmici e ripasso avanzato |
| Matematica e numerica | Step 6 | logica, combinatoria, probabilità, ricorrenze, floating point, errore numerico e randomizzazione |
| Sistemi, rete e runtime | Step 5, 9-10 | processi/thread, memoria, HTTP/TLS, socket, container, virtualizzazione e deployment |
| Database e sistemi distribuiti | Step 11-13, 22 | indici, transazioni, query planner, NoSQL, replication, sharding, consistenza e fault tolerance |
| Architettura, performance e sicurezza | Step 9-10, 14, 17, 22 | pattern architetturali, profiling, concorrenza, threat modelling, least privilege e osservabilità |
| Engineering e capacità senior | Step 4, 9, 22-23 | code review, lettura codebase/RFC/paper, invarianti, failure mode, API/system design e trade-off |
| Product thinking e HCI | Step 24 | problem framing, modellazione, usability, feedback, accessibility e interaction design |
| Programmazione moderna con LLM | Step 4, 17, 21, 25-28 | specifica, decomposizione, architettura, verifica del codice generato, sicurezza ed edge case |

Gli approfondimenti specialistici — TAOCP avanzato, BDD/ZDD, generazione combinatoria, Exact Cover/DLX, SAT/CSP, compiler e compressione — sono tracciati come sviluppo post-core collegato agli Step 2, 6 e 23.

## Aggiornamento Mini-Progetti

Ogni volta che viene creato un esercizio o mini-progetto, aggiornare questa roadmap nello step corrispondente.

Formato consigliato:

```text
- `Nome progetto` - descrizione breve: competenza allenata, output prodotto, link repo/demo se disponibile.
```

Regole:

- inserire il progetto sotto **Mini-progetti / esercizi** dello step corretto
- usare descrizioni pubbliche, sintetiche e leggibili anche da recruiter o colleghi
- non inserire note personali, credenziali, dataset privati o contenuti non condivisibili
- se un esercizio diventa progetto portfolio, aggiornare anche **Portfolio Target**

---

## ✅ Step 1 - Setup + Workflow Pro

**Focus:** ambiente tecnico pronto per lavorare come AI engineer.

**Competenze**

- Setup Python, Colab e repository
- Git, branch, commit e README
- Linux, shell e scripting base
- Precisione numerica: float16, float32, bfloat16

**Badge**

- 🟦 MASTER: Google Colab e pensiero computazionale
- 🟩 DATACAMP: non applicabile
- 🟨 CERT: CERT-SWE - Git, Linux, numerical precision
- 🔎 RESEARCH: poetry/venv, pre-commit, git flow, bash scripting
- 👑 KING PROGRAMMING: Git avanzato, padronanza degli strumenti e basi del rapporto software-sistema

**Output:** repository base con setup, README e workflow riproducibile.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 1.

---

## ✅ Step 2 - Python Core

**Focus:** scrivere Python in modo fluido e leggibile.

**Competenze**

- Funzioni, I/O, eccezioni e moduli
- Strutture dati fondamentali
- Complessità Big-O
- Primi pattern per codice manutenibile

**Badge**

- 🟦 MASTER: Programmazione con Python
- 🟩 DATACAMP: Software Engineering per Data Science in Python - completato, da rivedere
- 🟨 CERT: CERT-SWE - Python programming, data structures, algorithms
- 🔎 RESEARCH: best practice di struttura progetto e DSA per ML engineer
- 👑 KING PROGRAMMING: linguaggio e standard library; array/list/stack/queue/hash/tree/heap/trie/graph; Big-O; ricerca, sorting, ricorsione e paradigmi algoritmici fondamentali

**Output:** mini CLI tool con gestione input e logging base.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 2.

---

## ✅ Step 3 - OOP + Moduli + Typing

**Focus:** passare da script a package Python strutturati.

**Competenze**

- Classi, dataclass e typing
- Moduli installabili
- Docstring e interfacce chiare
- Primi standard di qualità del codice

**Badge**

- 🟦 MASTER: Programmazione con Python
- 🟩 DATACAMP: Software Engineering per Data Science in Python - completato, da rivedere
- 🟨 CERT: CERT-SWE - OOP, typing, moduli
- 🔎 RESEARCH: mypy e typing quickstart
- 👑 KING PROGRAMMING: Clean Code, Pragmatic Programmer, SICP, paradigmi di programmazione, modularità e design pattern applicati con criterio

**Output:** package installabile con struttura pulita.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 3.

---

## ⏳ Step 4 - Testing + Manutenibilita

**Focus:** rendere il codice verificabile e sostenibile.

**Competenze**

- pytest
- fixture e casi limite
- logging
- refactor
- CI/CD iniziale
- test sulle parti non-AI: parsing, validazione input, contratti API e gestione errori
- base riusabile per test, logging, config e smoke test

**Badge**

- 🟦 MASTER: Coding avanzato con Python
- 🟩 DATACAMP: Software Engineering per Data Science in Python - completato, da rivedere
- 🟨 CERT: CERT-SWE - Testing, coverage, CI/CD
- 🔎 RESEARCH: GitHub Actions e cache pytest
- 👑 KING PROGRAMMING: debugging sistematico, unit/integration/E2E/regression/property-based test, mocking, refactoring e review del codice generato dall'AI

**Output:** pipeline CI verde con coverage minimo, test riproducibili e base riusabile per i progetti successivi.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 4.

---

## 🕒 Step 5 - Reliability Engineering

**Focus:** costruire codice robusto, osservabile e prevedibile.

**Competenze**

- Error handling
- Retry e backoff
- Timeouts
- Logging strutturato
- Tassonomia degli errori
- Failure case tracciabili
- Regola operativa: prima debuggo il sistema, poi il prompt

**Badge**

- 🟦 MASTER: Coding avanzato con Python
- 🟩 DATACAMP: manutenibilita + reliability per applicazioni AI
- 🟨 CERT: consolidamento software engineering
- 🔎 RESEARCH: timeouts, retries e fail-safe design
- 👑 KING PROGRAMMING: processi, thread, async/event loop, sincronizzazione, race condition, deadlock, IPC e ragionamento sui failure mode

**Output:** libreria con logging strutturato, retry/backoff, timeout, error taxonomy e comportamento fail-safe.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 5.

---

## 🕒 Step 6 - ML Baseline + Math Foundations

**Focus:** costruire baseline ML solide e comprendere le basi matematiche essenziali.

**Competenze**

- Train/validation/test split
- Metriche di valutazione
- Data leakage
- Statistica e probabilità
- Algebra lineare
- Calcolo differenziale per gradienti e backpropagation

**Badge**

- 🟦 MASTER: AI applicata per sviluppatori
- 🟩 DATACAMP: Hugging Face Datasets e ideazione LLMOps come supporto
- 🟨 CERT: CERT-SWE math foundations + CERT-ML
- 🔎 RESEARCH: leakage examples, 3Blue1Brown, StatQuest
- 👑 KING PROGRAMMING: logica e matematica discreta, combinatoria, ricorrenze, complessità, numerica/floating point, probabilità, PRNG e Monte Carlo

**Output:** notebook baseline con metriche, seed fisso e mini cheat sheet matematica.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 6.

---

## 🕒 Step 7 - ML Improvement + Evaluation

**Focus:** migliorare un modello con metodo, non per tentativi casuali.

**Competenze**

- Preprocessing
- Feature engineering
- Hyperparameter tuning
- Cross validation
- Error analysis
- Bias-variance tradeoff

**Badge**

- 🟦 MASTER: AI applicata per sviluppatori
- 🟩 DATACAMP: non specifico
- 🟨 CERT: CERT-ML - algorithms, overfitting, underfitting
- 🔎 RESEARCH: ablation study e cross validation

**Output:** primo progetto portfolio ML con confronto baseline -> modello migliorato.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 7.

---

## 🕒 Step 7.5 - Dataset Engineering

**Focus:** creare dataset di qualità per training, evaluation e fine-tuning.

**Competenze**

- Data acquisition
- Data quality assessment
- Cleaning e deduplicazione
- Annotation guidelines
- Data augmentation e synthetic data

**Badge**

- 🟦 MASTER: applicazione nei progetti
- 🟩 DATACAMP: non specifico
- 🟨 CERT: CERT-DS - acquisition, quality, processing, annotation, augmentation
- 🔎 RESEARCH: Snorkel, Label Studio, synthetic data generation

**Output:** pipeline dataset con quality report automatico.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 7.5.

---

## 🕒 Step 8 - Portfolio ML: Language Identification

**Focus:** completare un progetto ML end-to-end su classificazione testuale.

**Competenze**

- Text classification
- Language identification
- Metriche di classificazione
- Benchmarking
- README tecnico

**Badge**

- 🟦 MASTER: progetto identificazione lingua
- 🟩 DATACAMP: facoltativo
- 🟨 CERT: consolidamento CERT-ML
- 🔎 RESEARCH: fastText language identification

**Output:** progetto portfolio ML pulito, riproducibile e documentato.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 8.

---

## 🕒 Step 9 - REST API per ML

**Focus:** servire un modello ML tramite API.

**Competenze**

- FastAPI
- Contratti endpoint
- Input validation
- API versioning
- Health checks
- System architecture basics
- Schema JSON input/output
- Error response standard
- Modello AI/ML trattato come componente interno dietro contratti chiari

**Badge**

- 🟦 MASTER: sviluppo REST API per Machine Learning
- 🟩 DATACAMP: sviluppo applicazioni AI con OpenAI API come supporto ai contratti applicativi
- 🟨 CERT: CERT-SWE - API design e architecture concepts
- 🔎 RESEARCH: Pydantic validation e API versioning
- 👑 KING PROGRAMMING: IP/TCP/UDP, DNS, HTTP(S), TLS, socket, client-server/RPC, autenticazione/autorizzazione e architetture modulari

**Output:** API v1 `/predict` e `/health` con validazione input/output, error response standard, healthcheck e test di integrazione.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 9.

---

## 🕒 Step 10 - ML in Produzione

**Focus:** portare un modello da notebook a servizio deployabile.

**Competenze**

- Packaging
- Docker
- Cloud basics
- Logging e monitoring
- Healthcheck
- Metriche operative
- Runbook minimo
- Eseguibilità da parte di un'altra persona

**Badge**

- 🟦 MASTER: progetto messa in produzione
- 🟩 DATACAMP: LLMOps e best practice per applicazioni AI in produzione
- 🟨 CERT: CERT-SWE - Docker, Cloud, Monitoring
- 🔎 RESEARCH: Docker FastAPI, Cloud Run, Prometheus/Grafana
- 👑 KING PROGRAMMING: sistemi operativi applicati, filesystem/memoria, container e virtualizzazione, proxy/load balancing, benchmark e profiling iniziale

**Output:** progetto portfolio dockerizzato con logging, metriche, healthcheck, deploy documentato e runbook minimo.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 10.

---

## 🕒 Step 11 - SQL Fundamentals

**Focus:** usare SQL in modo operativo per analisi e debugging dati.

**Competenze**

- Join
- Aggregazioni
- Query analysis
- KPI
- Ottimizzazione base

**Badge**

- 🟦 MASTER: database relazionali con SQL
- 🟩 DATACAMP: applicazioni AI con OpenAI API come supporto su dati testuali sensibili
- 🟨 CERT: pratica data engineering
- 🔎 RESEARCH: SQL optimization basics
- 👑 KING PROGRAMMING: modello relazionale, chiavi e vincoli, indici/B-tree, transazioni ACID, isolation, query planner, WAL e recovery

**Output:** report SQL con query documentate e riproducibili.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 11.

---

## 🕒 Step 12 - Analytics Project: E-commerce Sales

**Focus:** trasformare dati grezzi in insight comunicabili.

**Competenze**

- Analisi vendite
- KPI
- Data storytelling
- Reportistica

**Badge**

- 🟦 MASTER: progetto analisi vendite e-commerce
- 🟩 DATACAMP: non specifico
- 🟨 CERT: progetto SQL
- 🔎 RESEARCH: data storytelling for analytics
- 🛠️ BASWE: Project 8 — Text-to-SQL Interface with Guardrails & Hallucination Detection ([guida](./15-ai-engineering-projects-guide.it.md))

**Output:** report finale con note su dataset e definizione KPI.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 12.

---

## 🕒 Step 13 - NoSQL + Data Processing

**Focus:** progettare pipeline dati su document store e dati semi-strutturati.

**Competenze**

- NoSQL mental model
- ETL
- Schema validation
- Data quality checks

**Badge**

- 🟦 MASTER: NoSQL per elaborazione dati
- 🟩 DATACAMP: non specifico
- 🟨 CERT: pratica NoSQL e data processing
- 🔎 RESEARCH: schema validation patterns
- 👑 KING PROGRAMMING: document/key-value/graph database, storage esterno, log e snapshot, replication, sharding, consistenza e fault tolerance di base

**Output:** pipeline ETL con controlli di qualità.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 13.

---

## 🕒 Step 14 - Privacy-Aware Text Data Project

**Focus:** analizzare dati testuali sensibili con attenzione a privacy e qualità.

**Competenze**

- Analisi di testi clinici
- PII detection
- Redaction
- Privacy note
- Data quality

**Badge**

- 🟦 MASTER: progetto analisi cartelle cliniche
- 🟩 DATACAMP: non specifico
- 🟨 CERT: CERT-SEC - PII detection and redaction
- 🔎 RESEARCH: Presidio e PII handling
- 👑 KING PROGRAMMING: input validation, threat modelling, data protection e principio del privilegio minimo applicati ai dati sensibili
- 🛠️ BASWE: Project 14 — Multi-Modal Document Processor (OCR + LLM Extraction + Validation) ([guida](./15-ai-engineering-projects-guide.it.md))

**Output:** report con data quality e note privacy, senza PII nel repository.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 14.

---

## 🕒 Step 15 - LLM Fundamentals + Foundation Models

**Focus:** comprendere come funzionano i foundation model, come valutarli e come scegliere tra modelli API, open-weight e toolchain Hugging Face.

**Competenze**

- Tokenization
- Transformer
- Attention e KV cache
- Scaling laws
- SFT, RLHF, DPO
- Costi, performance e licensing
- Benchmarking
- Hugging Face model hub e pipeline di base
- Scelta modello: grande, piccolo, API esterna, locale o open-weight
- Trade-off costo, latenza, qualità, licenza e privacy

**Badge**

- 🟦 MASTER: Large Language Models + introduzione Hugging Face Transformers
- 🟩 DATACAMP: Introduzione a Hugging Face + LLMOps come supporto pratico
- 🟨 CERT: CERT-FM - transformer, attention, scaling, post-training
- 🔎 RESEARCH: Chinchilla, RLHF explained, lm-eval-harness, Hugging Face docs

**Output:** LLM Decision Guide e notebook di benchmark con scelta modello motivata.

**Mini-progetti / esercizi**

- `Local SLM App (Ollama)` - app LLM completamente offline con Ollama: benchmark di inferenza e confronto di 3 modelli sullo stesso hardware, con report sui trade-off qualità/velocità e note su privacy, latenza e costi. Output: report di benchmark + demo offline.

---

## 🕒 Step 15.5 - Fine-tuning, Hugging Face & Model Adaptation

**Focus:** adattare modelli pre-trained a task specifici usando Hugging Face, PEFT e valutazione pre/post fine-tuning.

**Competenze**

- Hugging Face Transformers
- Model hub, trainer e dataset integration
- PEFT
- LoRA e QLoRA
- Tokenizzazione avanzata e custom tokenizers
- Transformers per NLP e CV
- Training loop, scheduler, checkpoint ed evaluation loop
- Distillation
- Model merging
- Multi-task fine-tuning
- Valutazione pre/post fine-tuning

**Badge**

- 🟦 MASTER: Reti neurali e transformer applicate con Hugging Face
- 🟩 DATACAMP: Introduzione a Hugging Face come supporto pratico
- 🟨 CERT: CERT-FT - PEFT, LoRA, distillation, merging
- 🔎 RESEARCH: Hugging Face PEFT, mergekit, Axolotl
- 🛠️ BASWE: Project 10 — Fine-Tuning Pipeline with LoRA on a Domain-Specific Dataset ([guida](./15-ai-engineering-projects-guide.it.md))

**Output:** notebook Hugging Face/LoRA su task custom con metriche comparative.

**Mini-progetti / esercizi**

- `Fine-Tuning LoRA & DPO` - fine-tuning su task specifico (estrazione JSON o tool-calling) con LoRA/QLoRA e preference tuning via DPO. Output: notebook con metriche before/after e numeri reali. Allenato: PEFT, training efficiente, valutazione comparativa.

---

## 🕒 Step 16 - OpenAI API Hands-on

**Focus:** costruire applicazioni pratiche basate su API LLM.

**Competenze**

- API basics
- Chat e conversazioni
- Rate limits
- Retry e idempotency
- Logging richieste
- Caching
- Limiti token
- Controllo costi e stima costo per richiesta

**Badge**

- 🟦 MASTER: concetti da LLM
- 🟩 DATACAMP: Introduzione API OpenAI + sviluppo applicazioni AI
- 🟨 CERT: consolidamento foundation models hands-on
- 🔎 RESEARCH: rate limits, retries, idempotency

**Output:** mini app LLM con caching, retry/idempotenza, logging richieste, gestione rate limit e stima costo per richiesta.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 16.

---

## 🕒 Step 17 - Prompt Engineering Professionale

**Focus:** progettare, testare e tracciare prompt in modo sistematico.

**Competenze**

- Zero-shot e few-shot
- In-context learning
- Prompt injection
- Prompt tracking
- A/B testing
- Failure cases
- Regola anti prompt tweaking infinito: dopo 2-3 iterazioni senza miglioramento si controllano retrieval, dati, codice, modello, contesto, validazione output e architettura

**Badge**

- 🟦 MASTER: supporto da LLM
- 🟩 DATACAMP: Prompt Engineering
- 🟨 CERT: CERT-PE + CERT-SEC
- 🔎 RESEARCH: promptfoo, Langfuse, injection patterns
- 👑 KING PROGRAMMING: specifica del problema, vincoli, verifica delle assunzioni, review dell'AI e controllo di sicurezza, performance ed edge case
- 🛠️ BASWE: Project 9 — Prompt Versioning and A/B Testing Platform ([guida](./15-ai-engineering-projects-guide.it.md))

**Output:** prompt catalog con report A/B, test di sicurezza e failure analysis oltre il prompt.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 17.

---

## 🕒 Step 18 - Q&A Application Project

**Focus:** costruire una piccola applicazione Q&A end-to-end.

**Competenze**

- Prompting applicativo
- Caching
- Quality checks
- README riproducibile

**Badge**

- 🟦 MASTER: non applicabile
- 🟩 DATACAMP: progetto Q&A
- 🟨 CERT: consolidamento prompt engineering
- 🔎 RESEARCH: caching prompts/responses

**Output:** mini repository con demo riproducibile.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 18.

---

## 🕒 Step 19 - Embeddings + Semantic Search

**Focus:** costruire ricerca semantica misurabile.

**Competenze**

- Embeddings
- Similarity search
- BM25 vs dense retrieval
- Hybrid search
- Recall@k e MRR
- Baseline keyword/BM25 prima di vector DB
- Confronto tra ricerca lessicale, semantica e ibrida

**Badge**

- 🟦 MASTER: supporto da LLM
- 🟩 DATACAMP: Embeddings con OpenAI API
- 🟨 CERT: CERT-RAG + CERT-EVAL
- 🔎 RESEARCH: reciprocal rank fusion e embedding evaluation
- 👑 KING PROGRAMMING: ricerca lineare/binaria, hashing, alberi/trie, ranking e confronto tra strutture di indicizzazione applicati al retrieval
- 🛠️ BASWE: Project 6 — RAG Pipeline with Hybrid Search Over Internal Docs (fase base) ([guida](./15-ai-engineering-projects-guide.it.md))

**Output:** retriever v1 con metriche base e confronto BM25 vs semantic search vs hybrid search.

**Mini-progetti / esercizi**

- `Hybrid Retrieval (BM25 + vector)` - retriever ibrido che combina BM25 e ricerca vettoriale, valutato con recall@k e MRR. Base del progetto Production RAG dello Step 20. Output: retriever v1 + report metriche.

---

## 🕒 Step 20 - Vector DB + RAG Base

**Focus:** costruire un sistema RAG iniziale con retrieval controllato.

**Competenze**

- Vector database
- Chunking strategies
- Reranking
- Query expansion
- Context construction
- Evaluation set minimo
- Decisione esplicita: vector DB solo se serve
- Citation enforcement
- Failure analysis
- Regression test

**Badge**

- 🟦 MASTER: RAG in LLM o Agentic AI
- 🟩 DATACAMP: Embeddings, Pinecone e LangChain RAG
- 🟨 CERT: CERT-RAG + CERT-APP
- 🔎 RESEARCH: chunking, reranking, HyDE
- 👑 KING PROGRAMMING: costo delle strutture di ricerca, indici su memoria/storage, caching e trade-off spazio-tempo nella pipeline RAG
- 🛠️ BASWE: Project 6 — RAG Pipeline with Hybrid Search (versione production, Portfolio #3) · Project 4 — Self-Healing Technical Documentation ([guida](./15-ai-engineering-projects-guide.it.md))

**Decision matrix retrieval**

- BM25 basta quando il dominio è piccolo, lessicale, controllato o con keyword precise.
- Vector DB serve quando servono similarità semantica, sinonimi, concetti impliciti o documenti lunghi.
- Hybrid search serve quando serve più robustezza.

**Output:** portfolio RAG skeleton con baseline BM25, scelta vector/hybrid motivata, A/B test chunking, reranking, citation enforcement, eval set e regression test.

**Mini-progetti / esercizi**

- `Production RAG ("Ask My Docs")` - sistema RAG domain-specific con retrieval ibrido (BM25 + vettoriale), reranking con cross-encoder, citation enforcement e pipeline di valutazione gated in CI. Output: Portfolio #3 production-ready. Allenato: retrieval, reranking, eval automatica.

---

## 🕒 Step 21 - LangChain, Agents + RAG

**Focus:** costruire agenti con tool, memoria, retrieval e guardrail.

**Competenze**

- Chains
- Agents
- Tool integration
- Memory systems
- ReAct e planning
- Guardrails
- Agent evaluation
- Criteri per scegliere chain semplice, routing, tool calling o agent
- Permission guardrails e output validation

**Badge**

- 🟦 MASTER: Agentic AI
- 🟩 DATACAMP: LangChain + concetti LLMOps su chain e agenti
- 🟨 CERT: CERT-AGT
- 🔎 RESEARCH: LangGraph, tool error handling, agent benchmarks
- 👑 KING PROGRAMMING: decomposizione, ricerca/backtracking, stato, concorrenza, message passing e streaming come basi per workflow agentici controllabili
- 🎓 GH600: fondamenta concettuali dei domini D1-D4 dell'esame GH-600 (versione GitHub-specifica negli Step 25-28)
- 🛠️ BASWE: Project 5 — LLM Output Arbitration System · Project 15 — Agent Orchestration System (Tool Use, Memory, HITL) ([guida](./15-ai-engineering-projects-guide.it.md))

**Output:** agent con due tool, memoria, guardrail, gestione tool failure, output validation e task success rate.

**Mini-progetti / esercizi**

- `Real-Time Multimodal Assistant` - voice assistant o pipeline in streaming con budget di latenza end-to-end dettagliato, graceful degradation e gestione dei timeout. Output: demo real-time + scomposizione del latency budget. Allenato: sistemi real-time, robustezza.

---

## 🕒 Step 22 - Production, LLMOps + Inference Optimization

**Focus:** prepararsi a portare sistemi AI/LLM in produzione.

**Competenze**

- Architetture applicative LLM
- Function calling
- Model routing
- Fallback strategy
- Semantic caching e prompt caching
- Orchestrazione asincrona
- Quantization
- Batching
- KV cache
- Tracing
- Failure analysis
- Cost monitoring
- Latenza p50/p95
- Automated evaluation
- Evaluation regression in CI
- LLM-as-judge
- Hallucination, toxicity e bias testing
- Prompt injection mitigation
- PII redaction
- Secure sandboxing
- GDPR, AI Act e AI ethics
- Feedback loops e human-in-the-loop
- Incident/runbook

**Badge**

- 🟦 MASTER: DevOps e ciclo di vita
- 🟩 DATACAMP: LLMOps + sviluppo applicazioni AI con OpenAI API
- 🟨 CERT: CERT-INF, CERT-APP, CERT-EVAL, CERT-SEC, CERT-FB
- 🔎 RESEARCH: vLLM, secrets management, monitoring, EU AI Act
- 👑 KING PROGRAMMING: sistemi distribuiti, code/eventi, consistenza e fault tolerance, performance engineering, caching, concorrenza, sicurezza e trade-off architetturali
- 🎓 GH600: fondamenta dei domini D4 (evaluation/tuning) e D6 (guardrails/accountability) dell'esame GH-600
- 🛠️ BASWE (hub produzione/LLMOps): Project 1 — Model Regression Detection · Project 2 — LLM Cost Autopilot · Project 3 — Failure Forensics · Project 7 — Semantic Caching · Project 11 — LLM Gateway · Project 12 — AI Feature Flags · Project 13 — Eval Dataset Generator ([guida](./15-ai-engineering-projects-guide.it.md))

**Output:** production readiness kit collegato ai progetti portfolio, con runbook, dashboard, security checklist, eval plan, tracing, p50/p95, cost monitoring e regression gate.

**Mini-progetti / esercizi**

- `Monitoring & Observability` - tracing, latenza p50/p95, costo per richiesta e metriche di qualità applicati al sistema RAG, con regression gating in CI. Output: dashboard di osservabilità + gate CI. Allenato: LLMOps, monitoring di produzione.

---

## 🕒 Step 23 - AI/ML Interview Prep

**Focus:** trasformare studio e progetti in risposte tecniche da colloquio.

**Competenze**

- ML fundamentals
- Probabilità e statistica
- LLM, Hugging Face, RAG, fine-tuning e inference
- Python framework: scikit-learn, pandas, NumPy, PyTorch
- Data engineering per AI
- System design AI/LLM
- Trade-off e comunicazione tecnica
- Domande system design AI: RAG production-ready, BM25 vs vector DB, riduzione latenza/costi, monitoraggio hallucination/qualità, tool calling failure e scelta modello

**Badge**

- 🟦 MASTER: ripasso finale dei moduli AI, LLM, Agentic AI, DevOps
- 🟩 DATACAMP: ripasso mirato ML/LLM/API/RAG/LLMOps
- 🟨 CERT: consolidamento finale delle competenze AI Engineering
- 🔎 RESEARCH: ML interview, LLM system design, RAG evaluation interview
- 👑 KING PROGRAMMING: primi 30 algoritmi, traccia DSA avanzata e capacità senior — leggere codebase/RFC/paper, riconoscere invarianti e failure mode, scegliere strutture dati e motivare i trade-off

**Output:** flashcard, gap list, mock interview e risposte system design AI.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 23.

---

## 🕒 Step 24 - Full-Stack MERN per Demo Portfolio

**Focus:** creare una UI o demo web solo quando aiuta a presentare meglio i progetti AI.

**Competenze**

- HTML, CSS e JavaScript
- Layout responsive con Grid/Flexbox
- React per interfacce di progetto
- Node.js ed Express
- Persistenza dati
- Deploy su Vercel

**Badge**

- 🟦 MASTER: Full-Stack Web Development con stack MERN su Vercel
- 🟩 DATACAMP: non prioritario
- 🟨 CERT: supporto portfolio/demo, non core AI Engineering
- 🔎 RESEARCH: Vercel deploy, ML demo UI, portfolio project UX
- 👑 KING PROGRAMMING: product framing, data model e interaction design, usability, feedback, cognitive load e accessibility

**Output:** UI portfolio/demo per esporre progetti AI, con README e link deploy.

**Mini-progetti / esercizi**

- _Da aggiornare_: aggiungere qui i mini-progetti completati per Step 24.

---

## 🎓 Track Certificazione — GitHub Certified: Agentic AI Developer (GH-600)

Dopo il percorso core, la roadmap punta a una certificazione verticale sull'**agentic AI dentro il ciclo di sviluppo**, con GitHub come control plane.

**Certificazione:** GitHub Certified: Agentic AI Developer (beta) — Esame **GH-600** "Developing in Agentic AI Systems" (erogato da Microsoft, mantenuto da GitHub). 120 minuti, proctored, passing score 700.

**Stack:** GitHub Copilot, MCP servers, GitHub Actions/CI, custom agents, custom instructions, multi-agent orchestration. Le fondamenta agentiche arrivano dagli Step 21-22; qui diventano GitHub-specifiche.

**Risorse:** moduli gratuiti su Microsoft Learn (*Foundations of Agentic AI in GitHub*, *Designing Agent Architecture and SDLC Integration*, *Tooling, MCP, and Agent Execution Environments*) + documentazione GitHub Copilot.

---

## 🕒 Step 25 - Agent Architecture & SDLC su GitHub

**Focus:** progettare agenti dentro il ciclo SDLC con GitHub come system of record, separando planning da execution. *(Dominio esame D1, 15-20%)*

**Competenze**

- Integrazione agenti nel SDLC: step, anti-pattern, input/output/success criteria
- Boundaries planning/reasoning/action: structured plan, validazione, nessuna azione prima dell'approvazione
- Observability e control: degree of autonomy, guardrails, artefatti ispezionabili, human intervention

**Badge**

- 🟨 CERT: CERT-GH600 - D1
- 🎓 GH600: MS Learn *Foundations of Agentic AI in GitHub* + *Designing Agent Architecture and SDLC Integration*
- 🔎 RESEARCH: docs GitHub Copilot su custom agents e structured plan
- 👑 KING PROGRAMMING: specificare il problema, decomporlo, esplicitare vincoli e progettare l'architettura prima della generazione

**Output:** agente con structured-plan e validation gate, con artefatti ispezionabili in repo.

---

## 🕒 Step 26 - Tool Use, MCP & Execution Environment

**Focus:** dare all'agente tool, MCP server e un ambiente GitHub sicuro (repo/branch scope, CI, PR autonome). *(Dominio esame D2, 20-25%)*

**Competenze**

- Selezione e configurazione tool, tool permissions
- MCP servers: tool, remote MCP server GitHub, registries, allow lists
- Agenti nell'ambiente: execution context, repo/branch scope, invocazione in CI workflow, branch e PR autonome
- Esecuzione sicura: error handling, retries, rollbacks, escalation, traceability

**Badge**

- 🟨 CERT: CERT-GH600 - D2
- 🎓 GH600: MS Learn *Tooling, MCP, and Agent Execution Environments*
- 🔎 RESEARCH: docs GitHub su MCP server, allow list e CI agents
- 👑 KING PROGRAMMING: verificare implementazioni e assunzioni, progettare API/tool boundary e controllare sicurezza, performance ed errori
- 🛠️ BASWE: Project 4 — Self-Healing Technical Documentation (GitHub Action in CI, PR autonome) ([guida](./15-ai-engineering-projects-guide.it.md))

**Output:** MCP server + allow list collegati a un agente invocato in CI che apre una PR su branch scoped, con rollback ed escalation.

---

## 🕒 Step 27 - Memory/State + Evaluation & Tuning

**Focus:** gestire memoria/stato durevoli e chiudere il loop di valutazione, analisi errori e tuning. *(Domini esame D3 10-15% + D4 15-20%)*

**Competenze**

- Memory strategies: short/long/external, scoping, expiration/pruning/reset
- State e context drift: durable artifacts, resume senza ripetere, drift detection
- Success criteria e eval signals, automated scanning tools
- Failure analysis da logs/traces e classificazione root cause
- Tuning di instructions, memory e tool access

**Badge**

- 🟨 CERT: CERT-GH600 - D3 + D4
- 🎓 GH600: docs GitHub Copilot su memory e implementation planner
- 🔎 RESEARCH: code scanning e root cause analysis per agenti
- 👑 KING PROGRAMMING: ragionare su stato, invarianti, control/data flow, complessità e failure durante review e tuning

**Output:** agente con stato persistente, drift detection e report di failure analysis che guida un tuning concreto.

---

## 🕒 Step 28 - Multi-Agent Orchestration + Guardrails & Esame GH-600

**Focus:** coordinare più agenti in sicurezza, definire autonomy levels e guardrail, poi sostenere l'esame. *(Domini esame D5 15-20% + D6 10-15%)*

**Competenze**

- Orchestration pattern, isolation parallela, conflict resolution su code changes
- Observability multi-agent, audit e analisi post-hoc
- Failure multi-agent e recovery (rollback + human-in-the-loop)
- Lifecycle agenti: add/update/replace/retire
- Autonomy levels per rischio, guardrails HITL, least-privilege, authorization per cambi irreversibili

**Badge**

- 🟨 CERT: CERT-GH600 - D5 + D6
- 🎓 GH600: docs GitHub Copilot su cloud agent guardrails e risks/mitigations
- 🔎 RESEARCH: multi-agent orchestration e autonomy levels
- 👑 KING PROGRAMMING: modellare concorrenza, dipendenze e conflitti; applicare least privilege, review umana e trade-off espliciti
- 🛠️ BASWE: Project 15 — Agent Orchestration System with Tool Use, Memory, and Human-in-the-Loop ([guida](./15-ai-engineering-projects-guide.it.md))

**Output:** workflow multi-agent con conflict resolution, autonomy levels e guardrail documentati + superamento dell'esame GH-600.

---

## Portfolio Target

| Portfolio | Output | Area |
| --------- | ------ | ---- |
| #1 | ML text classification project | Machine Learning |
| #2 | Dockerized ML API | ML Engineering |
| #3 | Production RAG "Ask My Docs" (hybrid retrieval, reranking, citation enforcement, eval CI-gated) | LLM/RAG |
| #4 | Agent with tools, memory and guardrails + Real-Time Multimodal App | Agentic AI |
| #5 | Production readiness kit + Monitoring & Observability | LLMOps |
| #6 | Optional web demo / portfolio UI | Full-stack demo |

## Portfolio Production-Ready (5 progetti)

Non costruisco demo AI. Costruisco sistemi AI affidabili, misurabili e mantenibili.

| # | Progetto | Step | Decisioni ingegneristiche dimostrate |
| - | -------- | ---- | ------------------------------------ |
| 1 | Production RAG ("Ask My Docs") | Step 19-20 | BM25 vs vector DB vs hybrid, chunking, reranking, eval, citation enforcement |
| 2 | Local SLM App (Ollama) | Step 15 | scelta modello piccolo, latenza, privacy, benchmark, costo zero API |
| 3 | Monitoring & Observability | Step 22 | tracing, costi, p50/p95, regression gating, failure analysis |
| 4 | Fine-Tuning LoRA & DPO | Step 15.5 | quando fine-tuning serve davvero rispetto a RAG o prompting, metriche before/after |
| 5 | Real-Time Multimodal App | Step 21 | timeout, fallback, graceful degradation, latency budget |

## Skills Coverage

| Area | Coverage |
| ---- | -------- |
| Computer Science & Algorithms | DSA core, complessità, matematica discreta, ricerca/ordinamento, grafi e traccia algoritmica avanzata King Programming |
| Software Engineering | Python, Git, testing, CI/CD, API design, DataCamp percorso 8 completato e da rivedere |
| Math Foundations | Statistics, linear algebra, calculus |
| Machine Learning | Baselines, metrics, tuning, error analysis |
| Dataset Engineering | Data quality, annotation, augmentation |
| Data Engineering | SQL, NoSQL, ETL |
| Foundation Models | Transformers, scaling laws, model selection |
| Hugging Face Applied | Tokenizers, Transformers, fine-tuning, training loops |
| Prompt Engineering | Prompt design, testing, tracking, defense |
| RAG Systems | Embeddings, vector DB, chunking, retrieval eval |
| Agent Systems | Tools, memory, planning, guardrails |
| Production AI | Docker, monitoring, LLMOps, inference optimization |
| Security & Privacy | PII, prompt injection, GDPR, AI ethics |
| Interview Readiness | ML/LLM/system design communication |
| Portfolio UI | Optional MERN/Vercel demo layer |
| GitHub Agentic AI Certification | GH-600: SDLC agents, MCP, multi-agent orchestration, guardrails |

## LinkedIn Summary

Sto costruendo una roadmap personale da AI Engineer basata su progetti, non solo su teoria.

Il percorso copre fondamenti di Computer Science e algoritmi, software engineering, machine learning, dataset engineering, LLM, Hugging Face, fine-tuning, prompt engineering, RAG, agenti AI, LLMOps, sicurezza e preparazione ai colloqui tecnici.

Come obiettivo finale punto alla certificazione GitHub Certified: Agentic AI Developer (esame GH-600), portando le competenze sugli agenti dentro il ciclo di sviluppo con GitHub come control plane: SDLC agentico, MCP, orchestrazione multi-agente e guardrail.

Repository pubblico:
https://github.com/AlessandroSfratta/ai-engineer-roadmap

## 🧠 Decision Log da compilare per ogni progetto

```markdown
# Decision Log — <nome progetto>

- Qual è il problema reale?
- Qual è la baseline più semplice?
- Perché non basta una soluzione più semplice?
- Serve davvero un LLM?
- Serve davvero un vector database?
- BM25 sarebbe sufficiente?
- Serve RAG, fine-tuning o solo prompting?
- Quale modello uso e perché?
- Quali metriche misuro?
- Quali failure case conosco?
- Come gestisco errori, timeout e retry?
- Come controllo costi e latenza?
- Quale struttura dati o algoritmo uso e con quale complessità rilevante?
- Quali invarianti devono restare vere e quali trade-off spazio-tempo accetto?
- Come faccio debug quando qualcosa va male?
- Come capisco se il sistema è migliorato o peggiorato?
```
