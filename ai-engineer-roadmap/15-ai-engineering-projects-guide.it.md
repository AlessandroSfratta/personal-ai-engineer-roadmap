# 15 progetti di AI Engineering che fanno davvero ottenere il lavoro

> **Guida alla costruzione passo-passo per software engineer di livello mid che passano all'AI Engineering**
>
> BASWE | AiEngineerAccelerator™

---

> ℹ️ **Nota editoriale (non fa parte della guida originale)**
>
> Questa è la **traduzione italiana fluida** della guida. La **copia originale in inglese** è conservata in [`15-ai-engineering-projects-guide.md`](./15-ai-engineering-projects-guide.md) e resta la fonte canonica. La traduzione preserva il significato tecnico: i termini standard del settore (embeddings, prompt, fine-tuning, RAG, retrieval, chunking, reranking, guardrails, rate limiting, fallback, circuit breaker, ecc.) sono lasciati in inglese come nell'uso reale; nomi di prodotti/librerie, endpoint API e codice sono verbatim. La mappa di navigazione in cima e le righe `↪ Step roadmap` sono scaffolding aggiunto per l'integrazione nella roadmap. Due punti dell'originale arrivavano troncati dall'incolla (Project 7 Phase 6 e Project 14 Phase 1): sono segnalati con `[…]`.

---

## 🧭 Mappa progetti → Step roadmap (navigazione per agente AI)

> Aggiunta editoriale per collegare ogni progetto allo step opportuno della roadmap AI Engineer (`road-map-completa.md` privata / `ai-engineer-roadmap.md` pubblica).

| # | Progetto | Step roadmap di riferimento | Dimensione AI Engineering dimostrata |
| - | -------- | --------------------------- | ------------------------------------ |
| 1 | Model Regression Detection System | Step 22 (Evaluation & Testing in CI) · link Step 4, Step 17 | eval/regression gating, CI/CD per il comportamento del modello |
| 2 | LLM Cost Autopilot | Step 22 (model routing & cost) · link Step 15 | model routing, ottimizzazione dei costi |
| 3 | Failure Forensics Tool for AI Pipelines | Step 22 (tracing & failure analysis) | observability, root cause analysis |
| 4 | Self-Healing Technical Documentation | Step 20 (RAG/retrieval) · link Step 26 (GH-600, GitHub Action/CI) | embeddings, retrieval, agente in CI/CD |
| 5 | LLM Output Arbitration System | Step 21 (multi-agent, LangGraph) | evaluation multi-agente |
| 6 | RAG Pipeline with Hybrid Search Over Internal Docs | Step 19 (base) + Step 20 (full RAG) | hybrid retrieval, reranking, citation |
| 7 | Semantic Caching Layer for LLM APIs | Step 22 (semantic caching) · link Step 16 | efficienza infrastrutturale, riduzione costi/latenza |
| 8 | Text-to-SQL Interface with Guardrails & Hallucination Detection | Step 11-12 (SQL) · link Step 22 (guardrail/hallucination) | NL→SQL sicuro, guardrails, validazione |
| 9 | Prompt Versioning and A/B Testing Platform | Step 17 (Prompt Engineering: versioning/A-B/tracking) · link Step 22 | esperimentazione prompt, significatività statistica |
| 10 | Fine-Tuning Pipeline with LoRA on a Domain-Specific Dataset | Step 15.5 (Fine-tuning & Model Adaptation) | LoRA/PEFT, experiment tracking, eval pre/post |
| 11 | LLM Gateway with Rate Limiting, Fallback Routing & Observability | Step 22 (model routing, gateway, fallback) | gateway infrastrutturale, resilienza, observability |
| 12 | AI Feature Flag System with Gradual Rollout & Quality Monitoring | Step 22 (LLMOps, rollout, rollback) · link Step 17 | gradual rollout, quality gating, auto-rollback |
| 13 | Automated Eval Dataset Generator from Production Logs | Step 22 (eval pipeline) · link Step 7.5 (Dataset Engineering) | eval data dai log di produzione, flywheel |
| 14 | Multi-Modal Document Processor (OCR + LLM Extraction + Validation) | Step 14 (structured extraction da documenti) · link Step 15.5 (CV) | OCR, structured extraction, HITL, validazione |
| 15 | Agent Orchestration System with Tool Use, Memory & Human-in-the-Loop | Step 21 (agents/tools/memory) · link Step 28 (GH-600 multi-agent) | orchestrazione multi-agente, memoria, HITL |

---

## Come usare questa guida

Questa guida contiene quindici piani di costruzione completi. Ognuno è pensato per prendere un software engineer di livello mid con 3–5 anni di esperienza in produzione e produrre un progetto da portfolio che dimostra competenze di AI engineering a un livello che gli hiring manager cercano attivamente.

Non sono tutorial. Sono blueprint architetturali con dettaglio sufficiente a costruire ciascun sistema in autonomia, prendendo lungo la strada le tue decisioni di implementazione. Ed è intenzionale: le decisioni che prendi durante la costruzione sono esattamente quelle di cui parlerai ai colloqui.

### Cosa rende questi progetti diversi

- Ogni progetto risolve un problema operativo reale che i team AI affrontano in produzione, non un esercizio accademico.
- Sono pensati per sfruttare le tue competenze di production engineering già esistenti (Docker, CI/CD, API, database) come vantaggio strutturale.
- Ognuno dimostra una dimensione diversa della competenza di AI engineering: evaluation, ottimizzazione dei costi, observability, integrazione CI/CD, retrieval, fine-tuning e orchestrazione multi-agente.
- Nessuno di essi è del tipo "ho chiamato un'API LLM e ho deployato un chatbot".

### Tempistiche stimate

Ogni progetto è dimensionato per circa 12–14 giorni di lavoro focalizzato (2–3 ore al giorno). Non devi costruirli tutti e quindici. Scegli i due o tre più allineati ai ruoli che ti interessano e costruiscili in modo eccezionale. Due progetti profondi e rifiniti battono ogni volta cinque progetti superficiali.

---

## Project 1: Model Regression Detection System

↪ **Step roadmap:** Step 22 (Evaluation & Testing in CI) — collegamenti: Step 4 (CI/testing), Step 17 (prompt versioning/tracking).

**Cosa costruisci:** una pipeline in stile CI/CD che testa in continuo qualsiasi feature basata su LLM contro un golden dataset ogni volta che cambia un prompt o un modello, rileva le regressioni di qualità e avvisa il team via Slack prima che gli output sbagliati raggiungano gli utenti.

### Perché questo progetto fa colpo ai colloqui

Ogni team AI rilascia modifiche ai prompt "alla cieca". Questo progetto dimostra che ragioni su cosa succede dopo il deployment — esattamente la mentalità che gli hiring manager cercano disperatamente e che quasi nessun candidato dimostra.

### Stack tecnologico

| Componente | Tool / Libreria | Perché questa scelta |
| ---------- | --------------- | -------------------- |
| Linguaggio | Python 3.11+ | Standard di settore per il tooling ML |
| Provider LLM | OpenAI API (gpt-4o / gpt-4o-mini) | Ampiamente riconosciuto; facile da sostituire in seguito |
| Framework di eval | Custom + RAGAS o DeepEval | Mostra che capisci l'eval oltre la sola accuratezza |
| Storage dati | SQLite + file JSON | Zero infrastruttura, portabile, git-friendly |
| Alerting | Slack Webhooks | Ciò che i team reali usano davvero |
| Scheduling | GitHub Actions | Gira su ogni PR; il free tier basta |
| Visualizzazione | Streamlit o semplice report HTML | Dashboard rapida per le viste diff |
| Containerizzazione | Docker | Mostra production readiness |

### Guida alla costruzione passo-passo

#### Fase 1: Definire la feature LLM sotto test (Giorno 1–2)

1. **Costruisci una feature LLM semplice:** un classificatore di email di customer support che legge un'email e restituisce una categoria (billing, technical, account, general) più un riassunto di una frase. Incapsulalo in una singola funzione Python con il prompt come parametro configurabile.
2. **Versiona i tuoi prompt:** salva i prompt come file YAML versionati in una directory `/prompts`. Ogni file ha un ID di versione, un timestamp, il system prompt ed eventuali esempi few-shot. Questo è il "codice" contro cui esegui la CI.
3. **Crea il contratto di interfaccia:** definisci una semplice dataclass `PromptConfig` consumata dalla tua pipeline di eval. Input: testo dell'email. Output: JSON strutturato con categoria e riassunto. Tienila tipizzata con Pydantic.

#### Fase 2: Costruire il golden dataset (Giorno 2–4)

1. **Cura 50–100 casi di test a mano:** scrivi email clienti realistiche in tutte le categorie. Per ognuna, scrivi la categoria corretta e un riassunto ideale. NON generarle con un LLM — il punto è proprio che siano ground truth verificata da umani.
2. **Includi i casi limite di proposito:** aggiungi email ambigue che potrebbero appartenere a due categorie, email estremamente brevi, email con errori di battitura, email in lingue miste, email sarcastiche. Etichettale con un campo "expected_difficulty".
3. **Salva come JSON versionato:** ogni caso di test riceve un ID stabile, l'input, l'output atteso, il tag di difficoltà e un campo note che spiega perché quel caso conta. Versiona il file del dataset stesso, così puoi tracciare quando cambia l'asticella dell'eval.

> **Punto da raccontare al colloquio**
>
> Quando ti chiedono di questo progetto, parti da come hai costruito il golden dataset. Spiega che l'hai seminato con dati etichettati a mano e poi l'hai ampliato nel tempo usando i failure case. Questo segnala che hai capito che la qualità dell'evaluation è limitata dalla qualità dei dati — un'intuizione di produzione che la maggior parte dei candidati manca completamente.

#### Fase 3: Costruire il motore di evaluation (Giorno 4–7)

1. **Crea il test runner:** scrivi una funzione che prende un `PromptConfig` e il golden dataset, esegue ogni caso di test attraverso la feature LLM e raccoglie gli output grezzi. Usa il batching asincrono per tenere bassi i costi e alta la velocità.
2. **Implementa lo scoring multi-dimensionale:** non limitarti a controllare se la categoria coincide. Valuta su: match esatto di categoria (binario), rilevanza del riassunto (usa un LLM-as-judge con voto 1–5), latenza per richiesta e uso di token. Salva tutte le dimensioni per ogni caso di test.
3. **Costruisci la logica di confronto:** il valore centrale di questo sistema è il diffing. Per ogni run di eval, confronta con il run precedente. Calcola: delta del pass rate complessivo, delta di accuratezza per categoria, lista dei casi specifici passati da pass a fail (regressioni) e dei casi passati da fail a pass (miglioramenti).
4. **Aggiungi la significatività statistica:** se 2 casi su 80 cambiano, è segnale o rumore? Implementa un semplice sistema a soglia: warning se il delta supera il 3%, critical se supera l'8%. Rendi queste soglie configurabili.

#### Fase 4: Costruire il layer di alerting e reporting (Giorno 7–9)

1. **Crea il diff report:** genera un report HTML che mostra: metadati del run (versione prompt, modello, timestamp), una scorecard riassuntiva che confronta questo run con la baseline, una tabella di ogni caso regredito con il vecchio output vs. il nuovo affiancati e un grafico di trend dei punteggi sugli ultimi N run.
2. **Collega gli alert Slack:** usa l'API incoming webhook di Slack. Invia un messaggio strutturato con: stato pass/warn/fail, i numeri chiave (es. "3 regressioni rilevate, accuratezza scesa dal 94% all'89%") e un link al diff report HTML completo.
3. **Aggiungi la drift detection:** oltre ai diff per run, traccia una media mobile dei punteggi nel tempo. Se la media mobile su 7 run scende sotto una soglia anche se nessun singolo run ha fatto scattare un alert, lancia un warning di "slow drift". Questo cattura il degrado graduale che i controlli per-run perdono.

#### Fase 5: Integrare in CI/CD (Giorno 9–11)

1. **Crea un workflow GitHub Action:** fai partire la pipeline di eval su ogni PR che modifica file nella directory `/prompts`. L'action dovrebbe: eseguire l'eval, generare il report, postare un commento riassuntivo sulla PR con stato pass/fail e bloccare il merge se vengono rilevate regressioni critiche.
2. **Containerizza tutto:** scrivi un Dockerfile che impacchetta l'eval runner, il golden dataset e il layer di reporting. Il container deve accettare variabili d'ambiente per l'API key dell'LLM, l'URL del webhook Slack e le configurazioni delle soglie.
3. **Scrivi un README che sembri documentazione interna:** includi: un paragrafo che riassume cosa fa, istruzioni di setup, come aggiungere nuovi casi al golden dataset, come regolare le soglie e le decisioni architetturali con motivazione. NON scriverlo come un tutorial. Scrivilo come la documentazione di onboarding per un nuovo collega che entra nel team.

#### Fase 6: Rifinitura per il portfolio (Giorno 11–12)

1. **Registra una walkthrough Loom di 3 minuti:** mostra il sistema che gira end-to-end: cambia un prompt, fai partire l'eval, mostra l'alert Slack, ripercorri il diff report. È più persuasivo di qualsiasi README.
2. **Scrivi un breve blog post o una sezione del README:** spiega il problema (i team rilasciano modifiche ai prompt alla cieca), il tuo approccio (CI/CD per il comportamento del modello) e una decisione di design specifica di cui sei orgoglioso (es. perché tracci lo slow drift separatamente dalle regressioni per-run).

---

## Project 2: LLM Cost Autopilot

↪ **Step roadmap:** Step 22 (model routing & cost monitoring) — collegamento: Step 15 (model choice decision matrix).

**Cosa costruisci:** un layer di routing intelligente che si frappone davanti a più provider LLM, analizza la complessità di ogni richiesta in ingresso, la instrada al modello più economico in grado di gestirla a una qualità accettabile e valida in continuo che le decisioni di routing siano corrette.

### Perché questo progetto fa colpo ai colloqui

Ogni azienda che usa LLM su larga scala sta bruciando soldi in chiamate a modelli sovradimensionati. Costruire un cost optimizer segnala che capisci l'AI engineering come problema di business, non solo tecnico — ed è proprio il divario tra un'assunzione junior e una senior.

### Stack tecnologico

| Componente | Tool / Libreria | Perché questa scelta |
| ---------- | --------------- | -------------------- |
| Linguaggio | Python 3.11+ | Compatibilità con l'ecosistema |
| Provider LLM | OpenAI, Anthropic, Ollama (locale) | Mix di modelli cloud e locali |
| Router | FastAPI | Async-native, production-grade |
| Classificatore | Scikit-learn o piccolo modello fine-tuned | Scoring di complessità leggero |
| Eval | Scoring custom + LLM-as-judge | Loop di verifica della qualità |
| Logging | SQLite + log JSON strutturati | Audit trail completo per richiesta |
| Dashboard | Streamlit o Grafana | Visualizzazione costi e qualità |
| Containerizzazione | Docker + docker-compose | Orchestrazione multi-servizio |

### Guida alla costruzione passo-passo

#### Fase 1: Costruire l'interfaccia unificata ai modelli (Giorno 1–3)

1. **Crea un model registry:** definisci una dataclass `ModelConfig` con: nome del provider, ID modello, costo per token di input, costo per token di output, latenza media e un quality tier (high/medium/low). Popolala con il pricing reale di GPT-4o, GPT-4o-mini, Claude Sonnet, Claude Haiku e un modello Llama locale via Ollama.
2. **Costruisci il layer di astrazione:** scrivi un'unica funzione `send_request(prompt, model_config)` che gestisce le chiamate API specifiche per provider dietro un'interfaccia unificata. Ogni chiamata restituisce un oggetto `Response` standardizzato con: testo di output, token usati (input + output), latenza, costo e ID del modello.
3. **Testa ogni provider:** invia gli stessi 10 prompt a ogni modello del registry. Logga output, costi e latenze. Questo ti dà i dati baseline per la logica di routing e valida che il tuo layer di astrazione funzioni.

#### Fase 2: Costruire il classificatore di complessità (Giorno 3–6)

1. **Definisci i tier di complessità:** crea tre tier. Tier 1 (semplice): riformattazione, estrazione, Q&A di base da contesto fornito. Tier 2 (moderato): summarization, classificazione, analisi strutturata. Tier 3 (complesso): ragionamento multi-step, generazione creativa, giudizi sfumati.
2. **Costruisci un dataset etichettato:** scrivi 200+ prompt di esempio su tutti e tre i tier. Etichetta ognuno a mano. Includi le feature che estrarrai: conteggio token, presenza di istruzioni come "analizza" o "confronta", numero di vincoli, se è fornito del contesto e complessità del formato di output.
3. **Allena il classificatore:** parti da un semplice modello scikit-learn (logistic regression o random forest) sulle feature estratte. Non stai puntando alla perfezione del classificatore — stai costruendo lo scheletro del routing. Traccia accuratezza e confusion matrix. Qualunque valore sopra l'80% di accuratezza su un set held-out va bene per la V1.
4. **Crea la mappa di routing:** mappa ogni tier di complessità a un modello. Tier 1 → modello più economico (Haiku o Llama locale). Tier 2 → fascia media (GPT-4o-mini o Sonnet). Tier 3 → massima qualità (GPT-4o o Opus). Salvala come YAML configurabile, così puoi cambiare modelli senza toccare il codice.

#### Fase 3: Costruire il loop asincrono di verifica della qualità (Giorno 6–9)

1. **Definisci le soglie di qualità per caso d'uso:** per ogni tipo di richiesta, definisci cosa significa "abbastanza buono". Per i task di estrazione: ha preso tutti i campi chiave? Per la summarization: punteggio LLM-as-judge sopra 4/5. Per la classificazione: l'etichetta coincide con quella che avrebbe dato GPT-4o?
2. **Costruisci il verificatore asincrono:** dopo che la risposta è stata restituita all'utente, accoda un job asincrono che invia lo stesso prompt al modello di tier più alto e confronta gli output. Valuta l'accordo. Se l'output del modello economico diverge in modo significativo, loggalo come routing failure.
3. **Implementa l'auto-escalation:** se il verificatore intercetta un failure, ri-esegui automaticamente la richiesta con il modello di tier superiore e restituisci il risultato migliore (se la latenza lo permette). Logga l'evento di escalation con: modello originale, modello in escalation, delta di costo e il gap di qualità che l'ha innescata.
4. **Riporta i failure al classificatore:** ogni routing failure diventa un nuovo esempio di training per il classificatore di complessità. Costruisci un semplice feedback loop che ri-allena il classificatore settimanalmente usando i failure data accumulati. È il flywheel che rende il sistema più intelligente nel tempo.

#### Fase 4: Costruire il logging e la dashboard dei costi (Giorno 9–11)

1. **Logga tutto:** ogni richiesta riceve una riga nel database con: timestamp, hash del prompt, tier di complessità, modello instradato, costo, latenza, punteggio di qualità dal verificatore e se è andata in escalation. È il tuo audit trail.
2. **Costruisci la dashboard dei costi:** mostra: costo totale per giorno/settimana con confronto rispetto a quanto sarebbe costato usando GPT-4o per tutto ("hai risparmiato $X"), distribuzione del routing (grafico a torta di quali modelli gestiscono quale percentuale), distribuzione dei punteggi di qualità e tasso di escalation nel tempo.
3. **Aggiungi la metrica "money shot":** calcola e mostra in evidenza la percentuale di riduzione dei costi. Se instradare verso modelli più economici ha fatto risparmiare il 60% rispetto a inviare tutto al modello più costoso, quel numero è il titolo del tuo pezzo da portfolio.

#### Fase 5: Esporre come API (Giorno 11–13)

1. **Costruisci il servizio FastAPI:** un singolo endpoint `POST /v1/completions` che accetta una richiesta di chat completion standard. L'utente non sceglie il modello — lo fa il router. Restituisci la risposta con metadati che mostrano quale modello è stato selezionato e perché.
2. **Aggiungi gli endpoint di configurazione:** `GET /v1/models` (elenca i modelli disponibili e i loro costi), `GET /v1/stats` (riepilogo dei risparmi) e `PUT /v1/routing-config` (aggiorna le mappature tier→modello senza redeploy).
3. **Containerizza e documenta:** docker-compose con il servizio API, un background worker per la verifica asincrona e il database SQLite. Scrivi un README con diagramma dell'architettura, istruzioni di setup e il numero dei risparmi bene in vista.

#### Fase 6: Rifinitura per il portfolio (Giorno 13–14)

1. **Esegui un load test realistico:** invia 500–1.000 prompt diversi attraverso il sistema. Genera il report finale dei risparmi. Fai screenshot della dashboard. Questi artefatti sono ciò che metti nel portfolio.
2. **Scrivi il case study:** inquadralo come: "Ho costruito un sistema che ha ridotto i costi delle API LLM del X% mantenendo una parità di qualità del Y%." Parti dal numero. Spiega la logica di routing. Mostra il feedback loop. È una storia che un VP of Engineering capisce immediatamente.

---

## Project 3: Failure Forensics Tool for AI Pipelines

↪ **Step roadmap:** Step 22 (tracing & failure analysis / observability) — è la dimensione del Portfolio "Monitoring & Observability".

**Cosa costruisci:** un layer di observability per pipeline AI multi-step che traccia ogni step intermedio, identifica esattamente da dove origina un failure quando l'output finale è cattivo e riporta i failure flaggati in un dataset di evaluation in crescita.

### Perché questo progetto fa colpo ai colloqui

Quando una pipeline AI multi-step produce spazzatura, la maggior parte dei team non ha idea di quale step si sia rotto. Stai costruendo lo strumento che risponde a "dove è andato storto?" — in pratica un mini LangSmith/Braintrust. Saper articolare perché l'observability conta per i sistemi AI è un segnale da livello senior.

### Stack tecnologico

| Componente | Tool / Libreria | Perché questa scelta |
| ---------- | --------------- | -------------------- |
| Linguaggio | Python 3.11+ | Standard per il tooling ML |
| Framework di pipeline | Chain custom o LangChain | Dimostra conoscenza dell'orchestrazione |
| Provider LLM | OpenAI API | Ampiamente disponibile |
| Tracing | OpenTelemetry + span custom | Observability standard di settore |
| Storage | SQLite + file di trace JSON | Semplice, ispezionabile, git-friendly |
| Visualizzazione | Frontend React o Streamlit | Trace explorer interattivo |
| Feedback loop | Semplice REST API | Gli umani flaggano gli output cattivi |
| Containerizzazione | Docker | Packaging di produzione |

### Guida alla costruzione passo-passo

#### Fase 1: Costruire la pipeline multi-step (Giorno 1–3)

1. **Progetta una pipeline a 4 step:** Step 1 (Intake): accetta un documento grezzo (testo, markdown o testo PDF simulato). Step 2 (Extraction): usa un LLM per estrarre entità strutturate (nomi, date, importi, termini chiave). Step 3 (Classification): classifica il tipo di documento (contratto, fattura, report, corrispondenza). Step 4 (Summarization): genera un riassunto strutturato su misura per il tipo di documento.
2. **Rendi ogni step una funzione pulita e isolata:** ogni step prende un input tipizzato e restituisce un output tipizzato. Usa modelli Pydantic per ogni struttura dati intermedia. È fondamentale — se i tuoi step sono spaghetti, il tracing sarà privo di significato.
3. **Inietta failure mode realistici:** includi di proposito documenti che romperanno le cose: un contratto senza date, una fattura con importi in valute diverse, un documento ambiguamente a metà tra due categorie. Ti servono failure da tracciare.

#### Fase 2: Costruire il layer di tracing (Giorno 3–6)

1. **Crea un oggetto Trace:** ogni esecuzione della pipeline riceve un `trace_id` univoco. Il Trace contiene: una lista di oggetti Span (uno per step), l'output finale e uno status (success/failure/degraded).
2. **Strumenta ogni step con span:** avvolgi ogni step della pipeline in un context manager che cattura automaticamente: nome dello step, input (serializzato), output (serializzato), prompt LLM inviato, risposta grezza dell'LLM, conteggio token, latenza ed eventuali errori. Usa un pattern a decorator così strumentare un nuovo step è una riga di codice.
3. **Aggiungi il confidence scoring a ogni step:** dopo ogni chiamata LLM, fai produrre al modello anche un confidence score (1–5) sulla propria risposta. Salvalo nello span. Quando tracci all'indietro da un failure, gli span a bassa confidence sono i tuoi sospetti principali.
4. **Salva le trace come JSON strutturato:** scrivi ogni trace completa su un file JSON e indicizzala in SQLite (trace_id, timestamp, status, final_score). Così hai sia trace leggibili dagli umani sia metadati interrogabili.

#### Fase 3: Costruire l'analizzatore di trace all'indietro (Giorno 6–9)

1. **Implementa la logica di root cause analysis:** quando una trace è flaggata come failed, percorri all'indietro gli span. A ogni step chiediti: l'output di questo step è una trasformazione ragionevole del suo input? Usa un LLM-as-judge per valutare la qualità dell'output di ogni step dato il suo input. Il primo step con un calo di qualità significativo è la tua root cause.
2. **Categorizza i tipi di failure:** crea una tassonomia: Extraction Hallucination (entità estratte che non esistono nella fonte), Misclassification (tipo di documento sbagliato), Propagation Error (lo step N era corretto ma lo step N+1 ha interpretato male il suo output), Prompt Failure (l'LLM ha ignorato le istruzioni) e Context Loss (informazioni importanti dagli step precedenti sono andate perse).
3. **Costruisci la catena di evidenze:** per ogni failure diagnosticato, produci una spiegazione strutturata: "Lo Step 2 (Extraction) ha allucinato l'entità 'John Smith' che non compare nel documento sorgente. Questo si è propagato allo Step 4, che l'ha inclusa nel riassunto." Includi le specifiche coppie input/output come evidenza.

#### Fase 4: Costruire il trace explorer visuale (Giorno 9–11)

1. **Crea la trace view:** una rappresentazione visuale della pipeline in cui ogni step è un nodo. Codifica per colore lo status: verde (sano), giallo (bassa confidence), rosso (root cause identificata). Cliccando un nodo si vedono i dettagli completi dello span — input, output, prompt, confidence score.
2. **Aggiungi la diff view:** per le trace failed, mostra un confronto affiancato: cosa ha ricevuto lo step vs. cosa ha prodotto vs. cosa avrebbe dovuto produrre (in base al golden dataset o alla correzione umana). Evidenzia la divergenza specifica.
3. **Costruisci l'interfaccia di flagging:** un semplice pulsante che permette a un utente di marcare qualsiasi trace come "bad output". Al click, il sistema esegue l'analisi all'indietro e mostra la diagnosi di root cause. L'utente può confermare o ribaltare la diagnosi.

#### Fase 5: Costruire il loop feedback→eval (Giorno 11–13)

1. **Auto-genera casi di eval dai flag:** ogni volta che un umano flagga un output cattivo e conferma la root cause, crea automaticamente un nuovo caso di test: l'input originale, lo step che ha fallito, l'output cattivo, l'output corretto dall'umano e la categoria di failure. Appendilo a un dataset di eval in crescita.
2. **Costruisci il regression tracking:** ri-esegui periodicamente il dataset di eval accumulato contro la pipeline corrente. Traccia se i failure case noti stanno ancora fallendo o sono stati risolti. Mostra una trend line di "known issues resolved" nel tempo.
3. **Crea le failure analytics:** una dashboard che mostra: i tipi di failure più comuni, quale step della pipeline fallisce più spesso, il tasso di failure nel tempo e il tempo medio alla root cause. Sono i dati che dicono a un product team dove investire sforzo ingegneristico.

#### Fase 6: Rifinitura per il portfolio (Giorno 13–14)

1. **Prepara uno scenario demo:** processa 50 documenti attraverso la pipeline. Assicurati che almeno 8–10 producano failure di tipi diversi. Registra un Loom che mostra: un output cattivo, l'apertura del trace explorer, la diagnosi della root cause, il flagging e il dataset di eval che cresce.
2. **Scrivi il documento di architettura:** includi un diagramma della pipeline con il layer di tracing, il flusso di analisi all'indietro e il feedback loop. Inquadralo come: "Ho costruito un sistema di observability che riduce il mean time to root cause dei failure di pipeline AI da ore di debugging manuale a secondi di diagnosi automatica."

---

## Project 4: Self-Healing Technical Documentation

↪ **Step roadmap:** Step 20 (RAG: embeddings + retrieval) come tecnologia core; Step 26 (Track GH-600, GitHub Action in CI) per la parte di esecuzione in pipeline.

**Cosa costruisci:** una GitHub Action che monitora una codebase, rileva quando le modifiche al codice rendono la documentazione inaccurata, identifica le sezioni stantie specifiche e o auto-genera una PR con i doc corretti o segnala le discrepanze per la revisione umana.

### Perché questo progetto fa colpo ai colloqui

Questo progetto vive dentro una pipeline CI/CD, non in una demo Streamlit. Risolve un pain point ingegneristico universale che ogni intervistatore ha vissuto in prima persona. E dimostra l'intero stack di AI engineering — embeddings, retrieval, generazione LLM e deployment in produzione — in un sistema che altri ingegneri vorrebbero davvero installare.

### Stack tecnologico

| Componente | Tool / Libreria | Perché questa scelta |
| ---------- | --------------- | -------------------- |
| Linguaggio | Python 3.11+ / TypeScript | A tua scelta; entrambi funzionano nelle GitHub Actions |
| Embeddings | OpenAI text-embedding-3-small | Economico, veloce, alta qualità |
| Vector store | ChromaDB (file-based) | Nessun server; persiste su disco |
| LLM | GPT-4o o Claude Sonnet | Forte comprensione del codice |
| Integrazione Git | PyGithub + git diff | Creazione PR e parsing dei diff |
| CI/CD | GitHub Actions | Integrazione nativa, free tier |
| Containerizzazione | Docker (per la Action) | Run riproducibili |

### Guida alla costruzione passo-passo

#### Fase 1: Costruire la mappatura codice→doc (Giorno 1–4)

1. **Parsa la codebase in chunk semantici:** scrivi un parser che percorre la codebase ed estrae unità significative: firme di funzione con docstring, definizioni di classe, definizioni di endpoint API, schemi di configurazione e definizioni di comandi CLI. Ogni chunk riceve un identificatore stabile (path del file + nome funzione/classe).
2. **Parsa la documentazione in sezioni:** dividi i doc markdown in sezioni per heading. Ogni sezione riceve: il suo heading path (es. "Configuration > Environment Variables"), il contenuto grezzo e una lista dei riferimenti al codice che menziona (nomi di funzioni, classi, config key, comandi CLI).
3. **Costruisci il link graph:** crea collegamenti espliciti tra sezioni di doc e chunk di codice. Parti da euristiche semplici: se una sezione di doc menziona un nome di funzione che esiste nella codebase, collegali. Poi potenzia con gli embeddings: calcola gli embedding sia per i chunk di codice sia per le sezioni di doc e collega ogni coppia con cosine similarity sopra una soglia.
4. **Salva la mappatura:** persisti il grafo codice→doc come file JSON nel repo. È il tuo indice. Quando il codice cambia, interrogherai questo grafo per trovare quali sezioni di doc potrebbero essere colpite.

#### Fase 2: Costruire la pipeline di change detection (Giorno 4–7)

1. **Parsa il git diff:** su ogni PR, estrai la lista dei file modificati e le modifiche specifiche (righe aggiunte/rimosse/modificate). Mappa ogni modifica ai chunk di codice che colpisce usando il tuo code parser.
2. **Filtra per le modifiche significative:** non ogni modifica al codice impatta i doc. Salta: modifiche ai soli commenti, modifiche di whitespace, refactor interni che non cambiano il comportamento e modifiche ai file di test. Concentrati su: modifiche alle firme API, modifiche di configurazione, feature nuove/rimosse e modifiche comportamentali a funzioni esistenti.
3. **Identifica le sezioni di doc colpite:** per ogni modifica di codice significativa, interroga il tuo grafo codice→doc per trovare le sezioni di documentazione collegate. Sono i tuoi "sospetti" — sezioni che potrebbero ora essere stantie.
4. **Verifica la staleness con un LLM:** per ogni sezione di doc sospetta, invia all'LLM: il vecchio codice, il nuovo codice e il contenuto della sezione di doc. Chiedigli di determinare se la documentazione è ancora accurata data la modifica al codice. Se no, chiedigli di spiegare cosa c'è di sbagliato di preciso. Questo step filtra i falsi positivi.

#### Fase 3: Costruire il motore di riparazione dei doc (Giorno 7–10)

1. **Genera correzioni mirate:** per ogni sezione stantia confermata, invia all'LLM: la sezione di doc attuale, il nuovo codice e la diagnosi di staleness dalla Fase 2. Chiedigli di riscrivere solo le parti stantie, preservando stile, tono e struttura originali. Istruiscilo esplicitamente a non riscrivere le parti ancora accurate.
2. **Valida le correzioni:** esegui un secondo passaggio LLM che controlla: il doc corretto descrive accuratamente il nuovo codice? Ha preservato le parti già corrette? Lo stile di scrittura è coerente con il resto del documento? È il tuo quality gate prima di creare una PR.
3. **Gestisci diverse modalità di correzione:** non tutte le staleness sono uguali. Per modifiche semplici (parametro rinominato, valore di default aggiornato), auto-fix con alta confidence. Per modifiche complesse (nuova feature, capacità rimossa), genera una bozza con chiari marker TODO e richiedi revisione umana. Lascia che sia il livello di confidence a determinare la modalità.

#### Fase 4: Costruire la GitHub Action (Giorno 10–12)

1. **Impacchetta come GitHub Action:** crea un Dockerfile e un `action.yml` che definisce gli input della Action (API key dell'LLM, soglia di confidence, auto-merge per i fix ad alta confidence), gli output (lista delle sezioni stantie trovate, correzioni generate) e i trigger (gira sulle PR che modificano file di codice).
2. **Implementa il workflow delle PR:** per i fix ad alta confidence: crea un nuovo branch, applica le correzioni, apri una PR con una descrizione chiara di cosa è cambiato e perché. Per i flag a bassa confidence: aggiungi un commento sulla PR originale che elenca le sezioni di doc da rivedere a mano, con link alle sezioni specifiche.
3. **Aggiungi un commento riassuntivo sulla PR:** su ogni PR che innesca la Action, posta un commento: "Doc Check Results: 3 sezioni verificate accurate, 1 auto-fixata (vedi PR #42), 2 segnalate per revisione." Includi i link a tutto. È ciò che fa sentire lo strumento integrato e professionale.

#### Fase 5: Testare su un repository reale (Giorno 12–13)

1. **Fai il fork di un progetto open-source reale:** scegli un progetto ben documentato (FastAPI, Pydantic o simili). Fai il fork, installa la tua Action e fai di proposito modifiche al codice che dovrebbero invalidare i doc. Verifica che la Action identifichi correttamente la staleness e generi fix ragionevoli.
2. **Misura l'accuratezza:** sui tuoi casi di test, traccia: true positive (doc stantii correttamente identificati), false positive (doc accurati flaggati come stantii), false negative (staleness reale mancata) e qualità delle correzioni (i fix sono davvero giusti?). Riporta questi numeri nel README.

#### Fase 6: Rifinitura per il portfolio (Giorno 13–14)

1. **Rendilo installabile:** pubblicalo sul GitHub Actions marketplace (è gratis). Avere una Action che altri possono davvero installare è un segnale da portfolio fondamentalmente diverso da un repo che resta lì fermo.
2. **Registra la demo:** mostra: una modifica al codice che viene pushata, la Action che gira, il commento sulla PR che compare e la PR di fix dei doc auto-generata. Tienila sotto i 3 minuti. Parti dal problema ("i doc di ogni team sono perennemente stantii") e finisci con il risultato.

---

## Project 5: LLM Output Arbitration System

↪ **Step roadmap:** Step 21 (LangChain/LangGraph, multi-agent) — dimensione di evaluation multi-agente; collegamento a Step 22.C (LLM-as-judge, eval).

**Cosa costruisci:** una pipeline multi-agente che prende qualsiasi output generato da un LLM, lo instrada verso più modelli critici in competizione che lo valutano in modo indipendente per accuratezza, coerenza e completezza, poi sintetizza le loro critiche in un unico verdetto con confidence score e callout azionabili.

### Perché questo progetto fa colpo ai colloqui

Invece di costruire l'ennesimo sistema che genera risposte, ne stai costruendo uno che intercetta le risposte cattive. Questo ribalta il copione rispetto a ogni altro progetto da portfolio e dimostra la mentalità da evaluation che i team AI cercano attivamente ma vedono raramente nei candidati.

### Stack tecnologico

| Componente | Tool / Libreria | Perché questa scelta |
| ---------- | --------------- | -------------------- |
| Linguaggio | Python 3.11+ | Standard dell'ecosistema |
| Agent framework | LangGraph | Framework più richiesto nei ruoli AI eng |
| Provider LLM | OpenAI + Anthropic + Ollama | Il confronto multi-provider è il punto |
| Structured output | Pydantic + libreria instructor | Output LLM type-safe |
| Storage | SQLite + JSON | Audit trail per ogni arbitraggio |
| API | FastAPI | Serving production-grade |
| Visualizzazione | React o Streamlit | UI di esplorazione dei verdetti |

### Guida alla costruzione passo-passo

#### Fase 1: Progettare l'architettura degli agenti critici (Giorno 1–3)

1. **Definisci le dimensioni di evaluation:** crea tre ruoli di critic specializzati. Il Factual Accuracy Critic controlla se le affermazioni sono verificabili e internamente coerenti. Il Logical Consistency Critic controlla se il ragionamento regge e se le conclusioni sono supportate. Il Completeness Critic controlla se la risposta affronta tutte le parti della domanda e segnala le lacune.
2. **Progetta il formato strutturato delle critiche:** ogni critic restituisce un modello Pydantic con: dimensione (accuracy/logic/completeness), punteggio (1–5), lista dei problemi specifici trovati (ognuno con una citazione dall'originale, la descrizione del problema e la severità) e una confidence complessiva sulla propria valutazione. Usa la libreria instructor per imporre output strutturati da ogni modello.
3. **Assegna modelli diversi a critic diversi:** è deliberato. Instrada l'accuracy critic su GPT-4o, il logic critic su Claude e il completeness critic su un modello Llama locale. I disaccordi tra modelli sono il segnale più prezioso. Se tutti e tre usassero lo stesso modello, condividerebbero gli stessi punti ciechi.

#### Fase 2: Costruire il layer di orchestrazione con LangGraph (Giorno 3–6)

1. **Definisci il grafo:** crea uno state graph LangGraph con nodi per: parsing dell'input, dispatch parallelo dei critic, raccolta delle critiche, rilevamento dei disaccordi, adjudication e sintesi del verdetto. Il grafo deve gestire l'intero ciclo di vita dal ricevere un output al consegnare un verdetto.
2. **Implementa il dispatch parallelo dei critic:** tutti e tre i critic dovrebbero girare in parallelo, non in sequenza. Usa il branching di LangGraph per fare il fan-out verso tutti i critic simultaneamente e il fan-in quando tutti i risultati sono raccolti. Questo tiene ragionevole la latenza e rispecchia come sono costruiti i sistemi multi-agente reali.
3. **Costruisci il disagreement detector:** dopo aver raccolto tutte le critiche, confrontale. Segnala i casi in cui i critic non concordano sul fatto che qualcosa sia un problema, in cui i rating di severità differiscono di più di 2 punti o in cui un critic ha trovato problemi che gli altri hanno completamente mancato. Questi disaccordi sono i casi interessanti.
4. **Gestisci i casi limite nel grafo:** cosa succede se la chiamata API di un critic fallisce? Implementa retry logic e graceful degradation — il sistema dovrebbe comunque produrre un verdetto dai critic rimanenti, con una nota che una dimensione ha confidence più bassa. E se tutti i critic concordano che è perfetto? Cortocircuita l'adjudicator e restituisci un pass ad alta confidence.

#### Fase 3: Costruire l'agente adjudicator (Giorno 6–8)

1. **Progetta il prompt di adjudication:** l'adjudicator riceve: l'output originale in valutazione, tutti e tre i report dei critic e la lista dei disaccordi rilevati. Il suo compito è pesare le evidenze, risolvere i conflitti e produrre un verdetto finale. Istruiscilo a ragionare esplicitamente su ogni disaccordo.
2. **Implementa la risoluzione basata sulle evidenze:** quando i critic non concordano su un'affermazione fattuale, l'adjudicator dovrebbe tentare di verificarla. Quando non concordano sulla logica, dovrebbe ripercorrere la catena di ragionamento step by step. Quando non concordano sulla completezza, dovrebbe rileggere la domanda originale e determinare cosa era effettivamente richiesto.
3. **Produci il verdetto finale:** un output strutturato con: punteggio di qualità complessivo (1–10), livello di confidence, una lista di problemi confermati (con severità ed evidenza), una lista di flag scartati (problemi sollevati da un critic ma ribaltati dall'adjudicator, con motivazione) e un riassunto di un paragrafo della valutazione.

#### Fase 4: Costruire la UI di esplorazione dei verdetti (Giorno 8–10)

1. **Crea la vista principale del verdetto:** mostra l'output originale con annotazioni inline. Ogni problema flaggato dovrebbe essere evidenziato nel testo con un marker colorato (rosso per i problemi confermati, giallo per i flag a bassa confidence, verde per le affermazioni esplicitamente validate). Cliccando un marker si vede l'intera catena di evidenze.
2. **Costruisci il pannello di confronto dei critic:** una vista affiancata che mostra le valutazioni di tutti e tre i critic una accanto all'altra. Evidenzia gli accordi in verde e i disaccordi in arancione. Questa visuale rende l'architettura multi-agente immediatamente comprensibile a chiunque guardi il tuo portfolio.
3. **Aggiungi una modalità batch:** consenti di sottomettere più output per l'arbitraggio. Mostra i risultati in una tabella ordinabile con: estratto dell'output, punteggio complessivo, numero di problemi trovati e confidence. Questo dimostra che il sistema funziona su scala, non solo per demo isolate.

#### Fase 5: Esporre come API e aggiungere analytics (Giorno 10–12)

1. **Costruisci il servizio FastAPI:** `POST /v1/arbitrate` accetta un output LLM (e opzionalmente il prompt originale) e restituisce il verdetto completo. `POST /v1/arbitrate/batch` accetta più output. `GET /v1/arbitrations/{id}` recupera un verdetto passato. Tieni l'API pulita e ben documentata con specifiche OpenAPI.
2. **Aggiungi analytics sul comportamento dei critic:** su molti arbitraggi, traccia: quale critic trova più problemi, quale critic viene ribaltato più spesso dall'adjudicator, quali tipi di failure sono più comuni e quanto spesso i critic concordano vs. dissentono. Questa meta-analisi è oro per il portfolio.
3. **Containerizza tutto:** docker-compose con il servizio FastAPI, la pipeline LangGraph e il database SQLite. Includi un `docker-compose.yml` che avvia Ollama in locale per il completeness critic, così chi rivede può eseguire l'intero sistema senza API key a pagamento per tutti e tre i provider.

#### Fase 6: Rifinitura per il portfolio (Giorno 12–14)

1. **Prepara casi di test convincenti:** esegui il sistema contro: una risposta LLM fattualmente errata (errori piantati), un argomento logicamente difettoso, una risposta che tecnicamente risponde alla domanda ma manca il punto e una risposta genuinamente buona (per mostrare che può dare anche un esito pulito). Fai screenshot dei verdetti per tutti e quattro.
2. **Scrivi la narrazione:** inquadrala come: "Ho costruito un sistema in cui i modelli AI fanno l'audit del lavoro l'uno dell'altro. Tre critic specializzati valutano in modo indipendente qualsiasi output LLM e un adjudicator risolve i loro disaccordi in un unico verdetto." Parti dal diagramma di architettura che mostra il pattern di fan-out parallelo. Concludi con le analytics che mostrano che la critica multi-modello intercetta problemi che l'auto-valutazione single-model manca.

---

## Project 6: RAG Pipeline with Hybrid Search Over Internal Docs

↪ **Step roadmap:** Step 19 (Embeddings + Semantic Search, base) + Step 20 (Vector DB + RAG, versione production). Allineato al Portfolio #3 "Production RAG (Ask My Docs)".

**Cosa costruisci:** un sistema di Retrieval-Augmented Generation production-grade che ingerisce la documentazione interna di un'azienda, la indicizza sia con dense vector search sia con sparse keyword search, recupera il contesto più rilevante per qualsiasi domanda e genera risposte fondate con citazioni inline alle fonti.

### Perché questo progetto fa colpo ai colloqui

RAG è la singola skill più richiesta nelle job description di AI engineering. Ma la maggior parte dei candidati costruisce una demo giocattolo con un singolo PDF. Tu stai costruendo un sistema con hybrid retrieval, decisioni sulla strategia di chunking e verifica delle citazioni — le preoccupazioni di produzione che separano un vero RAG engineer da chi ha seguito una quickstart di LangChain.

### Stack tecnologico

| Componente | Tool / Libreria | Perché questa scelta |
| ---------- | --------------- | -------------------- |
| Linguaggio | Python 3.11+ | Standard dell'ecosistema |
| Embeddings | OpenAI text-embedding-3-small | Conveniente, alta qualità |
| Vector store | ChromaDB o Qdrant | File-based o containerizzato |
| Sparse search | BM25 via rank_bm25 | Keyword matching per termini esatti |
| LLM | GPT-4o o Claude Sonnet | Forte grounding e citazioni |
| Chunking | LangChain text splitters | Overlap e dimensione configurabili |
| API | FastAPI | Async-native, production-grade |
| Containerizzazione | Docker | Deployment riproducibile |

### Guida alla costruzione passo-passo

#### Fase 1: Costruire la pipeline di ingestion e chunking (Giorno 1–3)

1. **Costruisci un document loader multi-formato:** accetta file markdown, testo, HTML e PDF. Normalizza tutto in plaintext pulito con metadati (file sorgente, heading di sezione, numero di pagina). Salva i documenti grezzi accanto alle versioni processate, così puoi re-indicizzare senza ricaricarli.
2. **Implementa un chunking configurabile:** costruisci tre strategie di chunking e rendile commutabili: fixed-size con overlap (baseline), recursive character splitting per heading di sezione (consapevole della struttura) e semantic chunking che divide sui confini di topic usando la similarità degli embedding. Traccia quale strategia ha usato ogni chunk.
3. **Genera e salva gli embeddings:** fai l'embedding di ogni chunk con text-embedding-3-small. Salva in ChromaDB con metadati: documento sorgente, indice del chunk, heading di sezione, strategia di chunking e conteggio caratteri. Costruisci in parallelo l'indice BM25 sugli stessi chunk. I due indici devono restare sincronizzati.
4. **Aggiungi la deduplicazione:** prima di inserire un chunk, controlla i quasi-duplicati (cosine similarity > 0.95 rispetto ai chunk esistenti). Segnala e salta i duplicati. Questo evita che il retriever sprechi slot della context window su contenuto ridondante quando la stessa informazione compare in più doc.

#### Fase 2: Costruire il motore di hybrid retrieval (Giorno 3–6)

1. **Implementa il dense retrieval:** interroga il vector store con la domanda utente embeddata. Restituisci i top-k chunk ordinati per cosine similarity. Parti da k=10.
2. **Implementa lo sparse retrieval:** passa la stessa query attraverso BM25 sul corpus di chunk. Restituisci i top-k per BM25 score. Questo cattura i match esatti di keyword che la ricerca semantica potrebbe perdere — fondamentale per documentazione tecnica con nomi di funzione specifici, config key o codici di errore.
3. **Costruisci il layer di fusione:** implementa la Reciprocal Rank Fusion (RRF) per combinare i risultati dense e sparse in un'unica lista ordinata. RRF assegna punteggi in base alla posizione di rank tra le due liste e le fonde. Rendi la pesatura configurabile (es. 0.7 dense / 0.3 sparse) così puoi tararla per caso d'uso.
4. **Aggiungi un reranker:** dopo la fusione, passa i top 20 candidati attraverso un cross-encoder reranker (usa un modello piccolo o un LLM-as-judge) che valuta la rilevanza di ogni chunk rispetto alla domanda reale. Tieni i top 5. Questo secondo passaggio migliora drasticamente la precisione ed è un forte punto da raccontare al colloquio.

#### Fase 3: Costruire il layer di generation e citazione (Giorno 6–9)

1. **Progetta il prompt di generazione fondata:** costruisci un system prompt che istruisce l'LLM a rispondere solo dal contesto fornito, a citare i chunk specifici con riferimenti tra parentesi ([1], [2]) e a dichiarare esplicitamente quando il contesto non contiene informazioni sufficienti per rispondere. Includi i chunk recuperati come blocchi di contesto numerati.
2. **Implementa la verifica delle citazioni:** dopo la generazione, parsa le citazioni del modello e verificane ognuna. [1] supporta davvero l'affermazione a cui è attaccata? Invia ogni coppia citazione-affermazione a un LLM-as-judge per la verifica. Segnala le citazioni non supportate. È il quality layer che la maggior parte dei sistemi RAG salta del tutto.
3. **Costruisci lo scorer di confidence della risposta:** valuta ogni risposta su: confidence del retrieval (quanto erano rilevanti i top chunk?), copertura delle citazioni (quale percentuale di affermazioni ha citazioni verificate?) e completezza della risposta (ha affrontato tutte le parti della domanda?). Restituisci un confidence score composito accanto alla risposta.
4. **Gestisci con grazia il caso "non lo so":** se la confidence del retrieval è sotto una soglia, non allucinare. Restituisci una risposta strutturata che dice cosa ha trovato il sistema, cosa non ha trovato e quali documenti varrebbe la pena controllare a mano. È più utile di una risposta inventata e segnala maturità di produzione.

#### Fase 4: Costruire il framework di evaluation (Giorno 9–11)

1. **Crea un golden dataset di Q&A:** scrivi 50+ coppie domanda-risposta a mano, ognuna legata a sezioni specifiche del tuo corpus di documenti. Includi lookup diretti, domande multi-hop (la risposta richiede di combinare informazioni da due documenti), domande senza risposta nel corpus e domande ambigue.
2. **Implementa metriche di eval automatiche:** per ogni caso di test misura: correttezza della risposta (LLM-as-judge contro la golden answer), faithfulness (tutte le affermazioni sono fondate nel contesto recuperato?), rilevanza del retrieval (sono stati recuperati i chunk giusti?) e accuratezza delle citazioni (le citazioni supportano davvero le affermazioni?). Esegui l'intera suite a ogni modifica della pipeline.
3. **Costruisci un confronto tra strategie di chunking:** esegui la stessa suite di eval su tutte e tre le tue strategie di chunking. Genera un report di confronto che mostra quale strategia vince su quali metriche. Questi dati guidano le tue decisioni architetturali e ti danno numeri concreti per i colloqui.

#### Fase 5: Esporre come API e dashboard (Giorno 11–13)

1. **Costruisci il servizio FastAPI:** `POST /v1/ask` accetta una domanda e restituisce la risposta con citazioni, confidence score e metadati delle fonti. `GET /v1/documents` elenca i documenti indicizzati. `POST /v1/ingest` accetta nuovi documenti per l'indicizzazione. Includi la documentazione OpenAPI.
2. **Costruisci una semplice dashboard di query:** un frontend Streamlit o React dove puoi porre domande e vedere: la risposta generata con citazioni cliccabili, i chunk recuperati ordinati per rilevanza, i confidence score scomposti per dimensione e un toggle per confrontare hybrid vs. dense-only retrieval affiancati.
3. **Containerizza tutto:** docker-compose con il servizio API, ChromaDB e il frontend. Includi uno script di seed che indicizza un corpus di documentazione di esempio, così chi rivede può avviarlo e testarlo subito.

#### Fase 6: Rifinitura per il portfolio (Giorno 13–14)

1. **Registra una walkthrough demo:** mostra: l'ingestion di un set di documenti, domande di difficoltà variabile, la verifica delle citazioni che intercetta un'allucinazione e il confronto hybrid vs. dense-only. Tienila sotto i 4 minuti.
2. **Scrivi il case study:** inquadralo come: "Ho costruito un sistema RAG con hybrid search che raggiunge il X% di faithfulness e il Y% di accuratezza delle citazioni su una suite di eval da 50 domande." Parti dai numeri. Spiega perché l'hybrid batte il dense-only per la documentazione tecnica. Mostra i dati del confronto tra strategie di chunking.

---

## Project 7: Semantic Caching Layer for LLM APIs

↪ **Step roadmap:** Step 22 (semantic caching / prompt caching, caching architectures) — collegamento: Step 16 (production API hygiene, caching).

**Cosa costruisci:** un servizio middleware di caching che si frappone tra la tua applicazione e qualsiasi provider LLM, rileva richieste semanticamente simili a cui è già stata data risposta e serve istantaneamente le risposte in cache, abbattendo la latenza quasi a zero e riducendo i costi delle API del 30–60% su carichi tipici.

### Perché questo progetto fa colpo ai colloqui

Ogni azienda che usa LLM su larga scala ha lo stesso problema: chiamate API ridondanti che bruciano soldi e aggiungono latenza. Costruire una semantic cache dimostra che ragioni sull'efficienza infrastrutturale, non solo sull'accuratezza del modello, ed è il tipo di sistema di cui gli engineering manager capiscono immediatamente il ROI.

### Stack tecnologico

| Componente | Tool / Libreria | Perché questa scelta |
| ---------- | --------------- | -------------------- |
| Linguaggio | Python 3.11+ | Compatibilità con l'ecosistema |
| Embeddings | OpenAI text-embedding-3-small | Veloce, economico, alta qualità |
| Vector store | Redis + RedisVL o Qdrant | Lookup sub-millisecondo |
| Layer di proxy | FastAPI | Sostituzione drop-in dell'API |
| Cache policy | TTL custom + soglia di similarità | Hit rate vs. freschezza tarabili |
| Monitoring | Prometheus + Grafana | Dashboard di hit rate in tempo reale |
| Containerizzazione | Docker + docker-compose | Orchestrazione multi-servizio |

### Guida alla costruzione passo-passo

#### Fase 1: Costruire l'indice di cache e il motore di similarità (Giorno 1–3)

1. **Progetta la strategia di cache key:** non puoi usare il match esatto delle stringhe — "What is Python?" e "Explain Python to me" dovrebbero colpire la stessa cache entry. Fai l'embedding di ogni prompt in ingresso con text-embedding-3-small e salva l'embedding accanto alla risposta nel tuo vector store.
2. **Costruisci il lookup di similarità:** su ogni richiesta in ingresso, fai l'embedding del prompt e interroga il vector store per il nearest neighbor. Se la cosine similarity supera una soglia configurabile (parti da 0.95), è una cache hit. Restituisci la risposta salvata. Se è sotto soglia, è una miss — inoltra al provider LLM.
3. **Implementa lo storage della cache:** dopo una cache miss, inoltra la richiesta all'LLM reale, cattura la risposta completa (inclusi conteggi token, ID modello e finish reason) e salvala accanto all'embedding del prompt. Includi metadati: timestamp, scadenza TTL, hit count e il testo del prompt originale per il debug.
4. **Gestisci system prompt e parametri:** due prompt utente identici con system prompt o temperature diverse NON dovrebbero condividere cache entry. Incorpora l'hash del system prompt e i parametri chiave di generazione (temperature, max_tokens, model) nella cache key. Questo evita contaminazioni incrociate tra casi d'uso diversi.

#### Fase 2: Costruire il proxy API drop-in (Giorno 3–5)

1. **Rispecchia il contratto dell'API OpenAI:** costruisci un servizio FastAPI che accetta lo stesso identico formato di richiesta dell'endpoint chat completions di OpenAI. Significa che qualsiasi applicazione può passare al tuo cache proxy semplicemente cambiando la base URL — zero modifiche al codice. Restituisci lo stesso formato di risposta con un header aggiuntivo che indica cache hit/miss.
2. **Aggiungi il provider routing:** dietro al proxy, supporta più provider LLM (OpenAI, Anthropic, Ollama). Instrada in base al campo model nella richiesta. Il layer di cache è provider-agnostic — una risposta OpenAI in cache non può essere servita per una richiesta Anthropic, ma la logica di cache in sé è condivisa.
3. **Implementa il supporto allo streaming:** le cache hit dovrebbero tornare istantaneamente (niente streaming). Le cache miss dovrebbero fare streaming della risposta dal provider al client mentre contemporaneamente la bufferizzano per lo storage in cache. È la parte delicata — devi gestire le risposte parziali e mettere in cache solo le risposte complete e andate a buon fine.

#### Fase 3: Costruire le cache policy e l'eviction (Giorno 5–8)

1. **Implementa la scadenza basata su TTL:** ogni cache entry riceve un TTL configurabile. Per query fattuali/stabili, imposta TTL lunghi (24h+). Per query che fanno riferimento al tempo o a eventi correnti, imposta TTL brevi (1h) o disabilita del tutto il caching. Costruisci un classificatore che assegna automaticamente i tier di TTL in base al contenuto del prompt.
2. **Aggiungi i trigger di invalidazione della cache:** quando il system prompt di una feature cambia, invalida tutte le cache entry associate a quell'hash di system prompt. Quando un modello viene aggiornato (es. GPT-4o a una versione più recente), invalida le entry per quel modello. Fornisci endpoint API per l'invalidazione manuale per prefisso o tag.
3. **Costruisci il tuner della soglia di similarità:** esponi un endpoint che ti permette di testare diverse soglie di similarità su dati storici. Mostra: con soglia 0.90 l'hit rate è X% ma il Y% degli hit ha restituito risposte leggermente sbagliate. Con soglia 0.98 l'hit rate scende a Z% ma l'accuratezza è quasi perfetta. Questa visualizzazione del trade-off è il punto centrale da raccontare al colloquio.
4. **Implementa soglie adattive:** tipi di richiesta diversi hanno tolleranze diverse per i match approssimati. I task di classificazione possono tollerare similarità più basse (0.90) perché lo spazio delle risposte è vincolato. I task di generazione creativa hanno bisogno di similarità più alte (0.98) o dovrebbero saltare il caching del tutto. Lascia che il sistema impari queste soglie dal feedback.

#### Fase 4: Costruire monitoring e analytics (Giorno 8–10)

1. **Strumenta tutto con metriche Prometheus:** traccia: hit rate della cache (complessivo e per modello), latenza media per hit vs. miss, risparmio stimato di costo per ora/giorno, dimensione della cache e tasso di eviction e distribuzione dei similarity score per hit e near-miss. Esporta come metriche Prometheus.
2. **Costruisci la dashboard Grafana:** crea pannelli che mostrano: hit rate in tempo reale, risparmio cumulativo di costo (il "money shot"), confronto di latenza (cached vs. uncached P50/P95/P99), utilizzo della capacità della cache e una serie temporale dell'effetto della soglia di similarità sull'hit rate negli ultimi 7 giorni.
3. **Aggiungi un analizzatore di near-miss:** traccia le query che sono cadute appena sotto la soglia di similarità. Sono potenziali cache hit se la soglia fosse leggermente più bassa. Analizzare i near-miss ti permette di tarare la soglia con dati reali e di individuare opportunità di normalizzazione delle query (es. rimuovere le parole di riempimento prima dell'embedding).

#### Fase 5: Containerizzare e fare load test (Giorno 10–12)

1. **Metti l'intero stack in docker-compose:** servizi: proxy FastAPI, Redis (con RedisVL), Prometheus, Grafana e un'istanza Ollama opzionale per il test di modelli locali. Includi dashboard Grafana pre-configurate così chi rivede vede subito i dati.
2. **Esegui un load test realistico:** invia 2.000+ richieste attraverso il sistema usando un mix di query uniche e ripetute (simulando pattern d'uso realistici). Misura: convergenza dell'hit rate nel tempo, percentili di latenza e risparmio totale di costo. Questi numeri sono il titolo del tuo portfolio.
3. **Scrivi il README come una proposta interna:** inquadralo come: "Ecco cosa ci farebbe risparmiare se deployato davanti alle nostre chiamate LLM." Includi i risultati del load test, la proiezione dei risparmi e una guida di deployment. Non è un tutorial — è un business case con codice annesso.

#### Fase 6: Rifinitura per il portfolio (Giorno 12–14)

1. **Registra la demo:** mostra: una query fresca che colpisce l'LLM (con latenza), la stessa query che colpisce la cache (istantanea), una query semanticamente simile che colpisce anch'essa la cache e la dashboard Grafana che mostra i risparmi accumularsi in tempo reale.
2. **Parti dal numero:** "Un layer di caching drop-in che ha ridotto i costi delle API LLM […]"

> ℹ️ **Nota editoriale:** la frase finale del Project 7 (Fase 6, punto 2) arrivava troncata nell'incolla originale subito dopo "reduced LLM API costs". Il resto della frase non è stato fornito.

---

## Project 8: Text-to-SQL Interface with Guardrails and Hallucination Detection

↪ **Step roadmap:** Step 11-12 (SQL: query, progetto analytics) come dominio dati; Step 22 (guardrails, hallucination detection, validazione output) per la parte di sicurezza LLM.

**Cosa costruisci:** un'interfaccia in linguaggio naturale che traduce domande in inglese semplice in query SQL su un database reale, le esegue in sicurezza con guardrail che impediscono operazioni distruttive, valida che l'SQL generato risponda davvero alla domanda posta e presenta i risultati con un confidence score.

### Perché questo progetto fa colpo ai colloqui

Il text-to-SQL è una delle applicazioni di LLM a più alto valore in ambito enterprise, ed è notoriamente difficile da far funzionare bene. Costruirne uno con guardrail e hallucination detection dimostra che sai rilasciare feature AI che un team di compliance approverebbe davvero — che è l'asticella per l'AI di produzione in qualsiasi azienda seria.

### Stack tecnologico

| Componente | Tool / Libreria | Perché questa scelta |
| ---------- | --------------- | -------------------- |
| Linguaggio | Python 3.11+ | Standard per il tooling dati |
| LLM | GPT-4o o Claude Sonnet | Forte structured output |
| Database | PostgreSQL o DuckDB | Motore SQL reale, non un giocattolo SQLite |
| Estrazione schema | SQLAlchemy | Introspezione automatica dello schema |
| Guardrails | Middleware custom | Impedisce query distruttive |
| Validazione | LLM-as-judge + controllo risultati | Hallucination detection |
| API | FastAPI | Serving production-grade |
| Containerizzazione | Docker + docker-compose | Orchestrazione DB + API |

### Guida alla costruzione passo-passo

#### Fase 1: Costruire il prompt engine consapevole dello schema (Giorno 1–3)

1. **Auto-estrai lo schema del database:** usa SQLAlchemy per fare introspezione del database e produrre una rappresentazione strutturata: tabelle, colonne con tipi, relazioni di primary/foreign key e valori di esempio per le colonne categoriche. Questo diventa il contesto che l'LLM usa per scrivere l'SQL.
2. **Costruisci il costruttore dinamico del prompt:** per ogni domanda utente, assembla un prompt con: lo schema rilevante (non l'intero database — filtra alle tabelle probabilmente necessarie), le relazioni di foreign key, valori di esempio per la disambiguazione ed eventuali descrizioni di colonna o termini di glossario di business. Includi 3–5 esempi few-shot di coppie domanda-SQL specifiche per questo schema.
3. **Implementa il filtraggio dello schema:** per database grandi, inviare l'intero schema spreca contesto e confonde il modello. Costruisci un filtro di rilevanza leggero: fai l'embedding della domanda utente, fai l'embedding delle descrizioni di tabella/colonna e includi solo le tabelle sopra una soglia di similarità. Questo tiene il prompt focalizzato e migliora l'accuratezza di generazione.
4. **Gestisci l'ambiguità esplicitamente:** quando la domanda dell'utente mappa a più interpretazioni possibili (es. "revenue" potrebbe significare lordo o netto), restituisci una richiesta di chiarimento strutturata invece di tirare a indovinare. Elenca le interpretazioni con query di esempio per ognuna. È una feature di produzione che la maggior parte delle demo salta.

#### Fase 2: Costruire il layer di generazione SQL e sicurezza (Giorno 3–6)

1. **Genera l'SQL con structured output:** usa la libreria instructor o il function calling per garantire che l'LLM restituisca: la query SQL, una spiegazione in linguaggio naturale di cosa fa, un confidence score e una lista di tabelle e colonne accedute. Valida la sintassi SQL prima dell'esecuzione usando sqlparse.
2. **Implementa il middleware di guardrail:** prima che qualsiasi query venga eseguita, passala attraverso un layer di sicurezza che: blocca tutto il DDL (CREATE, ALTER, DROP), blocca tutte le scritture DML (INSERT, UPDATE, DELETE), impone un limite di righe (LIMIT 1000 se non specificato), rifiuta query con subquery più profonde di 3 livelli e blocca query che si stima scansionino più di N righe usando EXPLAIN. Rendi ogni regola configurabile e logga ogni query bloccata con la motivazione.
3. **Aggiungi il sandboxing delle query:** esegui tutte le query generate in una transazione read-only che fa rollback automatico. Usa un utente di database con permessi SELECT-only come secondo livello di difesa. Anche se il layer di guardrail manca qualcosa, i permessi del database impediscono danni.
4. **Costruisci il layer di esecuzione:** esegui l'SQL validato, cattura i risultati come DataFrame e impacchetta la risposta con: risultati grezzi (limitati al limite di righe), tempo di esecuzione, righe restituite e l'EXPLAIN plan. Logga tutto per l'auditabilità.

#### Fase 3: Costruire il sistema di hallucination detection (Giorno 6–9)

1. **Implementa la verifica SQL→domanda:** dopo aver generato l'SQL, rimanda la query all'LLM con il prompt: "A quale domanda risponde questa query SQL?" Confronta la domanda ri-tradotta con quella originale. Se divergono in modo significativo, l'SQL probabilmente non risponde alla domanda giusta. Valuta l'allineamento e segnala le traduzioni a bassa confidence.
2. **Aggiungi i sanity check sui risultati:** dopo l'esecuzione, fai controlli di buon senso di base: i valori aggregati sono in range plausibili? I conteggi corrispondono a ordini di grandezza attesi? I range di date rientrano nell'arco temporale dei dati? Ci sono colonne piene di NULL che potrebbero indicare un JOIN sbagliato? Segnala le anomalie con spiegazioni specifiche.
3. **Costruisci la multi-query validation:** per domande complesse, genera in modo indipendente due approcci SQL diversi (es. con strategie di JOIN o metodi di aggregazione diversi). Esegui entrambi. Se i risultati coincidono, la confidence è alta. Se divergono, segnala la discrepanza e presenta entrambi i risultati con spiegazioni. L'accordo tra approcci indipendenti è un forte segnale di correttezza.
4. **Crea un sistema di confidence scoring:** combina i segnali in un unico confidence score: validità della sintassi SQL, allineamento della ri-traduzione, tasso di superamento dei sanity check, accordo della multi-query e copertura dello schema (la query ha usato le tabelle/colonne che ti aspetteresti per questo tipo di domanda?). Mostra la confidence in evidenza accanto a ogni risultato.

#### Fase 4: Costruire l'interfaccia di query (Giorno 9–11)

1. **Costruisci gli endpoint API:** `POST /v1/query` accetta una domanda in linguaggio naturale e restituisce: l'SQL generato, i risultati dell'esecuzione, il confidence score ed eventuali warning dei guardrail. `GET /v1/schema` restituisce lo schema del database. `GET /v1/history` restituisce query e risultati passati della sessione.
2. **Crea un frontend Streamlit o React:** un'interfaccia pulita con: un input testuale per le domande in linguaggio naturale, l'SQL generato mostrato con syntax highlighting (modificabile per i power user), i risultati in una tabella dati ordinabile, il confidence score con la scomposizione dei segnali che lo determinano e un pannello di history con le query passate.
3. **Aggiungi un feedback loop:** lascia che gli utenti marchino i risultati come corretti o sbagliati. Salva questo feedback accanto alla query. I risultati sbagliati diventano nuovi casi di test per la suite di eval. I risultati corretti diventano nuovi esempi few-shot che migliorano la generazione futura. È il flywheel.

#### Fase 5: Costruire la suite di evaluation (Giorno 11–13)

1. **Crea un golden dataset di query:** scrivi 50+ domande in linguaggio naturale con SQL corretto verificato e risultati attesi. Includi: lookup semplici, JOIN multi-tabella, aggregazioni con GROUP BY, filtri su range di date, domande con frasi ambigue e domande a cui il database non può rispondere. È la tua regression suite.
2. **Esegui le eval automatiche:** per ogni caso di test misura: SQL exact match (l'SQL generato coincide con la golden query?), execution match (i risultati coincidono indipendentemente dall'approccio SQL?), tasso di hallucination detection (il sistema segnala correttamente le query cattive?) ed efficacia dei guardrail (le query pericolose sono bloccate?).
3. **Containerizza e documenta:** docker-compose con: PostgreSQL seminato con dati di esempio, il servizio FastAPI e il frontend. Includi un README che parte dai numeri di eval: "X% di execution accuracy, Y% di tasso di hallucination detection, zero query non sicure eseguite su Z casi di test."

#### Fase 6: Rifinitura per il portfolio (Giorno 13–14)

1. **Registra la demo:** mostra: una domanda in linguaggio naturale tradotta in SQL, il guardrail che blocca una query pericolosa, l'hallucination detector che intercetta una traduzione sbagliata e la multi-query validation che risolve una discrepanza. Sotto i 4 minuti.
2. **Scrivi la narrazione:** inquadrala come: "Ho costruito un sistema text-to-SQL con un tasso di accuratezza del X% che blocca il 100% delle operazioni distruttive e rileva il Y% delle query allucinate prima che raggiungano l'utente." Parti dalla sicurezza. Alle aziende interessa più non rompere le cose che le percentuali di accuratezza.

---

## Project 9: Prompt Versioning and A/B Testing Platform

↪ **Step roadmap:** Step 17 (Prompt Engineering: versioning, A/B testing, prompt tracking) — collegamento a Step 22 (eval pipeline, significatività).

**Cosa costruisci:** una piattaforma che tratta i prompt come artefatti versionati (come il codice), permette ai team di deployare più varianti di prompt simultaneamente, divide il traffico tra di esse, misura le performance su metriche custom e dichiara i vincitori statisticamente significativi — portando il rigore del feature flagging e dell'experimentation alle feature basate su LLM.

### Perché questo progetto fa colpo ai colloqui

La maggior parte dei team AI cambia i prompt modificando una stringa in produzione e sperando che vada bene. Questo progetto dimostra che hai capito che il prompt engineering su scala è un problema di experimentation, non di indovinello. Segnala il tipo di maturità operativa che distingue gli AI engineer senior dai junior.

### Stack tecnologico

| Componente | Tool / Libreria | Perché questa scelta |
| ---------- | --------------- | -------------------- |
| Linguaggio | Python 3.11+ | Standard per il tooling ML |
| Provider LLM | OpenAI / Anthropic | Supporto multi-provider |
| Storage | PostgreSQL | Versioning, esperimenti, risultati |
| Statistica | scipy.stats | Test di significatività |
| API | FastAPI | Gestione esperimenti + serving |
| Dashboard | React o Streamlit | Monitoraggio degli esperimenti |
| Containerizzazione | Docker + docker-compose | Orchestrazione dell'intero stack |

### Guida alla costruzione passo-passo

#### Fase 1: Costruire il prompt registry (Giorno 1–3)

1. **Progetta lo schema di versioning:** ogni prompt riceve un ID univoco, un numero di versione (auto-incrementante), il testo del system prompt, eventuali esempi few-shot, i parametri del modello (temperature, max_tokens), un commit message che spiega la modifica e un timestamp. Salva in PostgreSQL. È git per i prompt.
2. **Costruisci la registry API:** `POST /prompts` crea un nuovo prompt. `POST /prompts/{id}/versions` crea una nuova versione. `GET /prompts/{id}/versions` elenca tutte le versioni con i diff. `GET /prompts/{id}/versions/{v}` recupera una versione specifica. Aggiungi un endpoint di diff che mostra esattamente cosa è cambiato tra due versioni qualsiasi.
3. **Aggiungi il supporto al rollback:** qualsiasi versione può essere marcata come la versione "attiva" per la produzione. Fare rollback è solo cambiare quale versione è attiva — nessun deploy di codice. Logga ogni evento di attivazione/disattivazione con chi l'ha innescato e perché. Questo audit trail è fondamentale per la fiducia in produzione.
4. **Implementa i template di prompt con variabili:** i prompt dovrebbero supportare variabili di template (es. `{{user_name}}`, `{{context}}`) riempite al momento della richiesta. Il sistema di versioning versiona il template, non il prompt riempito. Valida che tutte le variabili nel template siano fornite al momento del serving.

#### Fase 2: Costruire il motore degli esperimenti (Giorno 3–6)

1. **Progetta lo schema dell'esperimento:** un esperimento ha: un nome, l'ID del prompt sotto test, due o più versioni varianti, le percentuali di split del traffico (es. 50/50 o 80/10/10), la metrica primaria (cosa definisce "migliore"), la dimensione campionaria target per la significatività e uno status (draft/running/completed/cancelled).
2. **Costruisci il traffic splitter:** quando arriva una richiesta per un prompt che ha un esperimento attivo, lo splitter assegna la richiesta a una variante in base alle percentuali configurate. Usa consistent hashing su uno user ID o session ID, così lo stesso utente vede sempre la stessa variante. Logga l'assegnazione.
3. **Implementa l'endpoint di serving:** `POST /v1/completions` accetta un ID di prompt e le variabili di input. Il sistema: risolve la versione attiva (o la variante dell'esperimento), riempie il template, chiama l'LLM, logga l'intera richiesta/risposta con l'assegnazione della variante e restituisce la risposta. Il chiamante non sa né si cura dell'esperimento.
4. **Aggiungi guardrail per gli esperimenti:** auto-stoppa gli esperimenti se l'error rate di una variante supera una soglia (es. 10% di fallimenti API). Auto-stoppa se la variante perdente sta performando significativamente peggio della baseline sulla metrica primaria. Notifica il proprietario dell'esperimento quando scatta una delle due condizioni. Questo evita che prompt cattivi colpiscano troppi utenti.

#### Fase 3: Costruire il layer di metriche e analisi (Giorno 6–9)

1. **Definisci dei metric collector pluggabili:** costruisci un framework di metriche dove i team possono registrare funzioni di evaluation custom. Metriche built-in: latenza, uso di token, costo ed error rate. Metriche custom: punteggio di qualità LLM-as-judge, accuratezza specifica del task, segnali di soddisfazione utente. Ogni metrica gira in modo asincrono dopo che la risposta è stata restituita.
2. **Implementa il test di significatività statistica:** per ogni esperimento, calcola in continuo: media e varianza di ogni metrica per variante, un t-test a due campioni (o Mann-Whitney U per distribuzioni non normali) che confronta le varianti, il p-value e l'intervallo di confidenza e la dimensione minima dell'effetto rilevabile data la dimensione campionaria corrente. Mostra se l'esperimento ha raggiunto la significatività.
3. **Costruisci la dashboard dei risultati:** per ogni esperimento in corso, mostra: confronto delle metriche in tempo reale tra le varianti (bar chart con intervalli di confidenza), avanzamento della dimensione campionaria verso il target di significatività, una serie temporale dei valori delle metriche per rilevare trend o instabilità e uno status chiaro "winner/no winner/inconclusive" con la statistica a supporto.
4. **Aggiungi la dichiarazione automatica del vincitore:** quando un esperimento raggiunge la significatività statistica al livello di confidenza configurato (default 95%), automaticamente: marca la variante vincente, notifica il proprietario dell'esperimento e opzionalmente auto-promuove il vincitore a versione attiva. Includi un periodo di attesa di 24 ore prima dell'auto-promozione in caso di problemi di qualità dei dati.

#### Fase 4: Costruire l'interfaccia di gestione (Giorno 9–11)

1. **Crea la UI di gestione degli esperimenti:** una dashboard dove i team possono: creare nuovi esperimenti dal prompt registry, configurare gli split di traffico e le metriche, monitorare gli esperimenti in corso, vedere i risultati degli esperimenti conclusi con la piena analisi statistica e promuovere i vincitori in produzione con un click.
2. **Aggiungi strumenti di confronto dei prompt:** una vista affiancata dove puoi scegliere due versioni di prompt qualsiasi, inviare a entrambe lo stesso set di input di test e vedere gli output confrontati con punteggi di qualità automatici. È utile per sanity check rapidi prima di lanciare un esperimento completo.
3. **Costruisci l'audit log:** ogni azione è loggata: creazione di prompt, modifiche di versione, start/stop degli esperimenti, assegnazioni delle varianti, promozioni dei vincitori e rollback. Questo log risponde a "chi ha cambiato il prompt che ha rotto la feature martedì scorso?" — una domanda a cui ogni team AI prima o poi deve rispondere.

#### Fase 5: Integrazione e testing (Giorno 11–13)

1. **Costruisci uno scenario demo:** semina il sistema con un classificatore di email di customer support. Crea tre varianti di prompt con approcci significativamente diversi (es. zero-shot vs. few-shot vs. chain-of-thought). Esegui un esperimento con 500+ richieste sintetiche. Lascialo convergere a un vincitore.
2. **Containerizza l'intero stack:** docker-compose con: PostgreSQL, il servizio FastAPI, la dashboard degli esperimenti e un worker per il calcolo asincrono delle metriche. Includi dati di seed così chi rivede vede subito un esperimento concluso.
3. **Scrivi test di integrazione:** testa: versioning e rollback dei prompt, consistenza del traffic splitting (lo stesso utente riceve sempre la stessa variante), accuratezza della raccolta metriche, correttezza del calcolo di significatività (usa distribuzioni note) e auto-stop sui picchi di error rate.

#### Fase 6: Rifinitura per il portfolio (Giorno 13–14)

1. **Registra la demo:** ripercorri: creazione di un prompt, lancio di un esperimento, le metriche che convergono, il sistema che dichiara un vincitore con supporto statistico e la promozione del vincitore in produzione. Mostra l'audit log. Sotto i 4 minuti.
2. **Scrivi la narrazione:** inquadrala come: "Ho costruito una piattaforma di experimentation dei prompt che porta il rigore del feature flagging allo sviluppo LLM. I team possono testare le modifiche ai prompt contro traffico reale e ottenere risultati statisticamente significativi invece di tirare a indovinare." Posizionala come infrastruttura, non come un giocattolo.

---

## Project 10: Fine-Tuning Pipeline with LoRA on a Domain-Specific Dataset

↪ **Step roadmap:** Step 15.5 (Fine-tuning & Model Adaptation) — allineato al Portfolio #4 "Fine-Tuning LoRA & DPO".

**Cosa costruisci:** una pipeline end-to-end che prende un dataset specifico di dominio, applica il fine-tuning LoRA (Low-Rank Adaptation) a un modello base open-source, valuta il modello fine-tuned contro il modello base su benchmark specifici del task e impacchetta il risultato per il deployment — con tracciamento completo degli esperimenti e riproducibilità.

### Perché questo progetto fa colpo ai colloqui

Il fine-tuning è dove l'AI engineering incontra l'ML engineering. La maggior parte dei candidati o non sa fare fine-tuning del tutto o esegue un notebook una volta e lo dà per fatto. Costruire una pipeline riproducibile con evaluation e experiment tracking dimostra che sai gestire l'intero ciclo di vita di customizzazione del modello di cui i team AI di produzione hanno bisogno.

### Stack tecnologico

| Componente | Tool / Libreria | Perché questa scelta |
| ---------- | --------------- | -------------------- |
| Linguaggio | Python 3.11+ | Standard dell'ecosistema ML |
| Modello base | Llama 3 8B o Mistral 7B | Forti opzioni open-source |
| Fine-tuning | Hugging Face PEFT + TRL | Tooling LoRA standard di settore |
| Training | Unsloth o QLoRA | Memory-efficient su GPU consumer |
| Dataset | Custom specifico di dominio | Il tuo valore aggiunto unico |
| Eval | Custom + lm-eval-harness | Benchmarking rigoroso |
| Experiment tracking | Weights & Biases o MLflow | Run riproducibili |
| Deployment | vLLM o Ollama | Serving di inferenza veloce |

### Guida alla costruzione passo-passo

#### Fase 1: Costruire il dataset di training (Giorno 1–4)

1. **Scegli un dominio e un task specifici:** scegli un task ristretto e ben definito dove puoi dimostrare un miglioramento netto sul modello base. Esempi: classificazione di clausole legali, summarization di note mediche, generazione di commenti di code review o matching del tono nel customer support. Il dominio non deve essere esotico — deve essere misurabile.
2. **Cura e formatta i dati di training:** raccogli o crea 500–2.000 esempi di alta qualità in formato instruction-following (instruction, input, output). La qualità conta più della quantità — ogni esempio dovrebbe rappresentare esattamente il comportamento che vuoi far imparare al modello. Pulisci con aggressività: rimuovi i duplicati, correggi le incoerenze di formattazione e verifica la correttezza.
3. **Costruisci gli split train/validation/test:** dividi i tuoi dati 80/10/10. Assicurati che non ci sia data leakage tra gli split (particolarmente importante se gli esempi derivano dagli stessi documenti sorgente). Il test set è sacro — non allenarti mai su di esso, non tarare mai gli iperparametri contro di esso. È la tua misura onesta di performance.
4. **Crea il benchmark di evaluation:** oltre allo split di test, crea 30–50 esempi di evaluation costruiti a mano che coprono casi limite, esempi difficili e failure mode che ti aspetti. Valuta ognuno con metriche specifiche del task (non solo la perplexity). Questo benchmark è come dimostri che il modello fine-tuned è migliore, non solo diverso.

#### Fase 2: Configurare la pipeline di training (Giorno 4–7)

1. **Configura i parametri LoRA:** imposta PEFT con LoRA che prende di mira i layer di attention (q_proj, v_proj come baseline). Iperparametri chiave: rank (parti da 16), alpha (2x il rank), dropout (0.05). Documenta perché hai scelto questi valori. Usa QLoRA (quantizzazione a 4 bit) se giri su una GPU consumer con VRAM limitata.
2. **Costruisci lo script di training con experiment tracking:** scrivi uno script di training configurabile che logga su Weights & Biases (o MLflow): tutti gli iperparametri, le curve di training loss, le metriche di validation a ogni checkpoint, l'uso della memoria GPU e la durata del training. Ogni run dovrebbe essere riproducibile dal solo file di config.
3. **Implementa early stopping e checkpointing:** salva i checkpoint del modello a intervalli regolari. Traccia la validation loss e ferma il training quando si appiattisce o inizia a crescere. Questo evita l'overfitting e risparmia compute. Logga quale checkpoint è stato selezionato come migliore e perché.
4. **Esegui uno sweep di iperparametri:** testa almeno 3 configurazioni variando rank (8, 16, 32), learning rate (1e-4, 2e-4, 5e-4) e numero di epoche (1, 3, 5). Logga tutti i run sull'experiment tracker. Produci una tabella di confronto che mostra come ogni configurazione performa sul validation set. Questi dati guidano la scelta della tua configurazione finale.

#### Fase 3: Valutare e confrontare i modelli (Giorno 7–10)

1. **Esegui il modello base contro il tuo benchmark:** prima di qualsiasi affermazione sul fine-tuning, stabilisci la baseline. Esegui il modello base (con lo stesso prompt template) contro l'intero benchmark di evaluation. Valuta ogni esempio. Salva questi risultati — sono il denominatore in ogni affermazione di miglioramento che fai.
2. **Esegui il modello fine-tuned contro lo stesso benchmark:** usando il miglior checkpoint dal training, valuta sullo stesso identico benchmark con gli stessi identici criteri di scoring. Confronta testa a testa su ogni esempio. Calcola: miglioramento complessivo di accuratezza/qualità, breakdown delle performance per categoria, esempi in cui il fine-tuning ha aiutato ed esempi in cui ha peggiorato (regressioni).
3. **Aggiungi l'evaluation LLM-as-judge:** oltre alle metriche automatiche, usa un modello forte (GPT-4o) come giudice per confrontare alla cieca gli output base vs. fine-tuned su ogni esempio di test. Fagli valutare la qualità su scala 1–5 e spiegare il suo ragionamento. Questo ti dà un segnale di qualità interpretabile dagli umani accanto alle metriche automatiche.
4. **Testa il catastrophic forgetting:** il fine-tuning può degradare le capacità generali. Esegui un sottoinsieme di benchmark standard (common sense QA, instruction following) sia sul modello base sia su quello fine-tuned. Se le performance generali sono calate in modo significativo, potresti dover ridurre le epoche di training o aggiustare il rank LoRA. Documenta i trade-off.

#### Fase 4: Costruire la pipeline di inferenza (Giorno 10–12)

1. **Impacchetta l'adapter LoRA per il deployment:** esporta i pesi dell'adapter LoRA allenato (non l'intero modello). L'adapter è minuscolo (tipicamente <100MB) mentre il modello base è grande (16GB+). Questa separazione significa che puoi cambiare adapter senza ricaricare il modello base — utile per servire più modelli specifici di dominio da un'unica base.
2. **Configura il serving di inferenza:** deploya usando vLLM (per inferenza batched production-grade) o Ollama (per un deployment locale più semplice). Carica il modello base, collega l'adapter LoRA ed esponi un'API di chat completions. Fai benchmark: token al secondo, latenza P50/P95 e massimo numero di richieste concorrenti.
3. **Costruisci un endpoint di confronto A/B:** crea un'API che accetta un prompt e restituisce le risposte sia del modello base sia di quello fine-tuned affiancate. Includi i punteggi di qualità dall'eval automatica. Questo endpoint alimenta la tua demo e rende il miglioramento immediatamente visibile.

#### Fase 5: Containerizzare e documentare (Giorno 12–13)

1. **Impacchetta l'intera pipeline:** crea un setup riproducibile con: uno script di training ri-eseguibile con un singolo comando, una pipeline di data processing che produce dataset pronti per il training a partire dagli input grezzi, una eval harness che fa benchmark di qualsiasi modello contro la tua test suite e un inference server con il modello fine-tuned caricato.
2. **Scrivi il report dell'esperimento:** un documento strutturato che mostra: il problema e perché il fine-tuning era l'approccio giusto (vs. il few-shot prompting o il RAG), le statistiche del dataset e la metodologia di curation, i risultati dello sweep di iperparametri, il confronto testa a testa (base vs. fine-tuned) con esempi specifici e l'analisi del catastrophic forgetting.

#### Fase 6: Rifinitura per il portfolio (Giorno 13–14)

1. **Registra la demo:** mostra: il modello base che fatica con un task specifico di dominio, il modello fine-tuned che lo gestisce correttamente, la dashboard W&B con le curve di training e l'endpoint di confronto A/B con esempi reali. Sotto i 4 minuti.
2. **Scrivi il titolo:** "Ho fatto fine-tuning di Llama 3 8B su dati di [dominio] usando LoRA e ho migliorato la performance del task dal X% al Y% mantenendo il Z% delle capacità generali." Ogni numero dovrebbe essere supportato dai dati di evaluation nel tuo repo.

---

## Project 11: LLM Gateway with Rate Limiting, Fallback Routing, and Observability

↪ **Step roadmap:** Step 22 (model routing & gateways, fallback strategy, observability) — infrastruttura di produzione per chiamate LLM.

**Cosa costruisci:** un API gateway di produzione che si frappone davanti a tutte le chiamate LLM dell'organizzazione, impone rate limit e budget per team, fa automaticamente fallback verso provider alternativi quando un provider primario ha un'interruzione o ti rate-limita e fornisce observability unificata su ogni interazione LLM.

### Perché questo progetto fa colpo ai colloqui

Ogni azienda con più di un team che usa LLM finisce per costruire qualcosa di simile. È puro infrastructure engineering applicato all'AI — esattamente il set di competenze che i SWE mid già hanno e di cui i team AI hanno disperatamente bisogno. Questo progetto ti permette di partire dai tuoi punti di forza in production engineering dimostrando al contempo profonda conoscenza dei sistemi AI.

### Stack tecnologico

| Componente | Tool / Libreria | Perché questa scelta |
| ---------- | --------------- | -------------------- |
| Linguaggio | Python 3.11+ o Go | Layer di proxy ad alto throughput |
| Proxy | FastAPI o net/http | Gestione richieste async-native |
| Rate limiting | Redis + token bucket | Enforcement distribuito, sub-ms |
| Config | YAML + hot reload | Cambi di policy senza deploy |
| Observability | OpenTelemetry + Prometheus | Tracing standard di settore |
| Dashboard | Grafana | Visualizzazione unificata delle metriche |
| Provider | OpenAI, Anthropic, Ollama | Supporto multi-provider |
| Containerizzazione | Docker + docker-compose | Orchestrazione dell'intero stack |

### Guida alla costruzione passo-passo

#### Fase 1: Costruire il layer di proxy unificato (Giorno 1–3)

1. **Costruisci l'astrazione dei provider:** crea un'interfaccia unificata che normalizza le richieste tra OpenAI, Anthropic e Ollama. Le richieste in ingresso usano un formato standard. Il gateway traduce verso il formato API di ciascun provider, chiama il provider e ritraduce la risposta nel formato standard. Il chiamante non sa mai quale provider ha servito la richiesta.
2. **Implementa autenticazione e routing delle richieste:** ogni richiesta include una team API key. Il gateway valida la chiave, recupera la configurazione del team (modelli permessi, rate limit, budget) e instrada al provider appropriato. I team possono essere limitati a modelli o provider specifici in base al loro piano.
3. **Aggiungi il passthrough dello streaming:** supporta sia risposte streaming sia non-streaming. Per lo streaming, il gateway agisce da proxy trasparente: inoltra i chunk dal provider al client in tempo reale mentre contemporaneamente logga la risposta completa per l'observability. È fondamentale per applicazioni sensibili alla latenza.
4. **Gestisci l'arricchimento delle richieste:** il gateway può iniettare system prompt standard, appendere disclaimer di compliance o aggiungere content filter prima di inoltrare al provider. Rendi questo configurabile per team. Questo centralizza l'enforcement delle policy senza richiedere che ogni team lo implementi da sé.

#### Fase 2: Costruire rate limiting ed enforcement del budget (Giorno 3–6)

1. **Implementa il rate limiting a token bucket:** usa Redis per mantenere token bucket per team con rate configurabili (richieste al minuto, token al minuto). Imponi i limiti prima di inoltrare la richiesta. Restituisci risposte 429 standard con header Retry-After quando i limiti vengono raggiunti. Deve essere atomico e safe in ambiente distribuito.
2. **Aggiungi i cap di budget:** ogni team riceve un budget mensile o giornaliero in dollari. Traccia la spesa calcolando il costo per richiesta (token input * prezzo input + token output * prezzo output). Quando un team si avvicina al limite (80%), invia un warning. Quando lo raggiunge, blocca le richieste e restituisci un errore chiaro che spiega il cap di budget.
3. **Costruisci rate limit a fasce:** tipi di richiesta diversi ricevono limiti diversi. Un job di batch data processing dovrebbe avere priorità più bassa di una richiesta real-time rivolta all'utente. Implementa code di priorità così le richieste ad alta priorità vengono servite anche quando i limiti complessivi sono vicini alla capacità.
4. **Crea l'admin API:** endpoint per: vedere lo stato corrente dei rate limit per team, aggiustare limiti e budget senza riavvio, vedere le dashboard di spesa e impostare alert quando i team si avvicinano ai limiti. Tutte le modifiche sono loggate con chi le ha fatte e quando.

#### Fase 3: Costruire il layer di fallback e resilienza (Giorno 6–9)

1. **Implementa l'health checking:** il gateway monitora in continuo la salute di ogni provider: invia richieste di test leggere ogni 30 secondi, traccia error rate e latenza P99 su finestre mobili e mantiene uno status (healthy/degraded/down) per ogni combinazione provider-modello. Salva lo storico di salute per l'analisi post-incidente.
2. **Costruisci il fallback routing automatico:** quando un provider primario è degraded o down, instrada automaticamente le richieste verso un fallback configurato. Esempio: se OpenAI GPT-4o va in timeout, instrada verso Anthropic Claude Sonnet. Definisci le catene di fallback per model tier (non per modello specifico) così il sistema trova sempre un'opzione disponibile.
3. **Aggiungi retry con exponential backoff:** prima di fare fallback verso un altro provider, riprova il primario con exponential backoff (fino a 3 retry). Distingui tra errori ritentabili (rate limit, timeout) ed errori non ritentabili (fallimenti di auth, violazioni di content policy). Fai fallback solo per gli errori ritentabili che esauriscono i retry.
4. **Implementa i circuit breaker:** se un provider fallisce più di N volte in M secondi, apri il circuito — smetti del tutto di inviare richieste a quel provider e instrada tutto verso i fallback. Dopo un periodo di cooldown, invia una singola richiesta di test (stato half-open). Se ha successo, chiudi il circuito e riprendi il routing normale. Logga ogni cambio di stato.

#### Fase 4: Costruire il layer di observability (Giorno 9–11)

1. **Strumenta con OpenTelemetry:** aggiungi span di distributed tracing per: ricezione della richiesta, autenticazione, controllo del rate limit, selezione del provider, chiamata API LLM, processing della risposta e consegna della risposta. Ogni span include: team ID, modello richiesto, modello servito, conteggi token, latenza e costo.
2. **Esporta metriche Prometheus:** metriche chiave: richieste al secondo (per team, modello, provider), error rate (per team, modello, provider, tipo di errore), percentili di latenza (P50, P95, P99 per provider), throughput di token (token input + output al secondo), costo per team al giorno, tasso di trigger dei fallback e cambi di stato dei circuit breaker.
3. **Costruisci le dashboard Grafana:** crea tre dashboard. Operations: salute dei provider, error rate, eventi di fallback, stato dei circuit breaker. Business: spesa per team, utilizzo del budget, trend di utilizzo. Performance: percentili di latenza, throughput di token, cache hit rate (se integrato con il Project 7).
4. **Aggiungi regole di alerting:** configura alert per: error rate di un provider sopra soglia, team che si avvicina al cap di budget, latenza P99 sopra l'SLA e apertura di un circuit breaker. Instrada gli alert su Slack con contesto azionabile: cosa è successo, quali team sono colpiti e lo status dell'auto-fallback.

#### Fase 5: Test di integrazione e load test (Giorno 11–13)

1. **Costruisci una suite di test di integrazione:** testa: che il rate limiting si imponga correttamente sotto carico concorrente, che i cap di budget blocchino le richieste alla soglia giusta, che il fallback routing si attivi quando il primario fallisce (simula i fallimenti), che i circuit breaker si aprano e chiudano correttamente e che le risposte streaming passino senza corruzione.
2. **Esegui un load test:** invia 5.000+ richieste concorrenti attraverso il gateway con un mix di chiavi di team, modelli e priorità. Misura: latenza di overhead del gateway (dovrebbe essere <10ms), accuratezza del rate limiting sotto carico, comportamento del fallback sotto interruzioni di provider simulate e accuratezza della dashboard (le metriche mostrate corrispondono alla realtà?).
3. **Containerizza l'intero stack:** docker-compose con: il servizio gateway, Redis, Prometheus, Grafana (con dashboard pre-configurate) ed endpoint di provider mock per il testing. Includi uno script di setup che crea team demo con rate limit diversi, così chi rivede vede subito il sistema in azione.

#### Fase 6: Rifinitura per il portfolio (Giorno 13–14)

1. **Registra la demo:** mostra: le richieste che fluiscono attraverso il gateway con metriche Grafana in tempo reale, un'interruzione di provider simulata che innesca il fallback routing, il rate limiting che scatta per un team ad alto volume e il circuit breaker che si apre e si riprende. Sotto i 4 minuti.
2. **Scrivi la narrazione:** inquadrala come: "Ho costruito un API gateway LLM che gestisce X richieste/secondo con <10ms di overhead, failover multi-provider automatico ed enforcement di budget per team." È infrastruttura. Parti dai numeri di affidabilità e dal problema operativo che risolve.

---

## Project 12: AI Feature Flag System with Gradual Rollout and Quality Monitoring

↪ **Step roadmap:** Step 22 (LLMOps: gradual rollout, quality monitoring, auto-rollback) — collegamento a Step 17 (A/B testing dei prompt).

**Cosa costruisci:** una piattaforma di feature flag pensata specificamente per le feature basate su AI che supporta rollout graduali basati su percentuale, monitora automaticamente le metriche di qualità durante il rollout e innesca un rollback automatico se la qualità dell'output della feature AI degrada sotto una soglia configurabile.

### Perché questo progetto fa colpo ai colloqui

Ogni team di engineering usa i feature flag per il software tradizionale. Quasi nessuno ha adattato il pattern alle feature AI, dove "funzionare" non è binario — è un gradiente di qualità. Questo progetto dimostra che hai capito che rilasciare feature AI richiede pattern operativi diversi dal rilasciare codice tradizionale e che sai costruire il tooling per supportarli.

### Stack tecnologico

| Componente | Tool / Libreria | Perché questa scelta |
| ---------- | --------------- | -------------------- |
| Linguaggio | Python 3.11+ | Standard per il tooling AI |
| Storage | PostgreSQL + Redis | Config durevole + evaluation veloce |
| Quality eval | Custom + LLM-as-judge | Scoring di qualità in tempo reale |
| SDK | Libreria client Python | Integrazione drop-in per le app |
| Dashboard | React o Streamlit | Monitoraggio del rollout |
| Alerting | Slack Webhooks | Notifiche di rollback |
| Containerizzazione | Docker + docker-compose | Orchestrazione dell'intero stack |

### Guida alla costruzione passo-passo

#### Fase 1: Costruire il motore di valutazione dei flag (Giorno 1–3)

1. **Progetta lo schema dei feature flag AI:** oltre ai flag booleani tradizionali, i flag AI hanno bisogno di: una percentuale di rollout (0–100%), una soglia di qualità (punteggio di qualità minimo accettabile), un trigger di rollback (condizioni che causano il rollback automatico), una configurazione baseline (cosa servire quando il flag è off — es. la versione di prompt precedente o un fallback non-AI) e la configurazione sperimentale (la nuova feature AI sotto test).
2. **Costruisci l'SDK di valutazione:** un client Python leggero che le applicazioni importano. Il metodo centrale: `flag_client.evaluate(flag_name, user_context)` restituisce quale variante servire. L'SDK gestisce: assegnazione utente consistente (lo stesso utente riceve sempre la stessa variante via hashing), rollout basato su percentuale, caching locale delle configurazioni dei flag e graceful degradation se il servizio dei flag è irraggiungibile (default alla baseline).
3. **Implementa le targeting rule:** oltre agli split casuali per percentuale, supporta il targeting: per segmento utente (es. prima gli utenti interni, poi i beta user, poi tutti), per geografia, per metadati della richiesta (es. abilita solo per certi tipi di input) e allowlist/blocklist per specifici user ID. Questo permette ai team rollout attenti e controllati.
4. **Costruisci la flag management API:** endpoint CRUD per i flag, più: `POST /flags/{id}/rollout` per aggiornare la percentuale, `POST /flags/{id}/pause` per fermare il rollout alla percentuale corrente e `POST /flags/{id}/rollback` per spostare immediatamente tutto il traffico alla baseline. Tutte le modifiche sono loggate con l'attore e la motivazione.

#### Fase 2: Costruire il layer di quality monitoring (Giorno 3–6)

1. **Definisci le metriche di qualità per flag:** ogni feature flag AI specifica come misurare la qualità. Opzioni built-in: scoring LLM-as-judge (invia ogni output a un modello giudice per un voto 1–5), segnali di feedback utente (thumbs up/down, rating espliciti), soglie di latenza (le feature AI troppo lente degradano la UX anche se l'output è buono) ed error rate (fallimenti API, output malformati, tassi di timeout).
2. **Costruisci il quality evaluator asincrono:** dopo ogni risposta gestita da un flag AI, accoda una valutazione di qualità asincrona. Il valutatore valuta l'output usando le metriche configurate del flag e scrive il punteggio nel database. Questo non deve aggiungere latenza alla risposta rivolta all'utente. Usa un background worker con una message queue.
3. **Implementa finestre di qualità mobili:** traccia i punteggi di qualità in finestre mobili (ultime 100 valutazioni, ultima 1 ora, ultime 24 ore). Calcola: punteggio di qualità medio, deviazione standard, qualità P10 (decimo percentile peggiore) e il trend di qualità (in miglioramento, stabile, in degrado). Confronta in continuo i punteggi sperimentale vs. baseline.
4. **Costruisci il trigger di rollback automatico:** quando la qualità della variante sperimentale scende sotto la soglia configurata del flag per un periodo sostenuto (es. P10 sotto 3.0 per più di 50 valutazioni consecutive), automaticamente: imposta la percentuale di rollout a 0%, invia un alert Slack con i dati di qualità e logga l'evento di rollback con contesto completo. Includi un cooldown per evitare il flapping.

#### Fase 3: Costruire l'automazione del gradual rollout (Giorno 6–9)

1. **Implementa schedule di rollout a fasi:** definisci un piano di rollout come una serie di fasi: 1% per 2 ore, 5% per 6 ore, 25% per 24 ore, 50% per 24 ore, 100%. A ogni confine di fase, il sistema controlla le metriche di qualità. Se la qualità è sopra soglia, avanza automaticamente alla fase successiva. Se la qualità cala, mette in pausa e avvisa.
2. **Aggiungi la canary analysis:** a ogni fase di rollout, confronta le metriche della variante sperimentale con la baseline. Usa il test statistico (simile al Project 9) per determinare se c'è una differenza di qualità significativa. Il rollout avanza solo quando la variante sperimentale è statisticamente non peggiore della baseline.
3. **Costruisci la dashboard di rollout:** per ogni rollout attivo, mostra: fase e percentuale correnti, confronto delle metriche di qualità (sperimentale vs. baseline) nel tempo, le prossime transizioni di fase e le loro condizioni, eventuali pause o rollback innescati con le motivazioni e il tempo stimato al rollout completo in base ai trend di qualità correnti.
4. **Supporta il dark mode testing:** prima di qualsiasi rollout reale, supporta lo "shadow mode": esegui la variante sperimentale su tutto il traffico ma non mostrare i risultati agli utenti. Invece, logga cosa sarebbe stato mostrato e valuta la qualità offline. Questo cattura i fallimenti catastrofici prima che un solo utente sia colpito.

#### Fase 4: Costruire la dashboard e l'integrazione (Giorno 9–11)

1. **Crea la UI di gestione dei flag:** una dashboard che mostra: tutti i flag e il loro status corrente (off/in rollout/completamente on/rolled back), metriche di qualità in tempo reale per i flag attivi, lo schedule di rollout con indicatori di avanzamento e un pulsante di rollback one-click con conferma.
2. **Costruisci la vista di analytics:** dati storici per ogni flag: metriche di qualità su tutta la storia del rollout, l'impatto della feature AI sulle metriche di business (se tracciate), un riepilogo di tutti gli eventi di rollback e le loro cause e il tempo-al-rollout-completo per le feature riuscite.
3. **Scrivi la documentazione dell'SDK client:** mostra esattamente come uno sviluppatore integra il flag nella sua applicazione con esempi di codice. Sottolinea che l'integrazione è minima (3–5 righe di codice) e che il quality monitoring avviene automaticamente. Includi esempi per i pattern comuni: fallback AI vs. non-AI, A/B testing di versioni di prompt e test di sostituzione del modello.

#### Fase 5: Test di integrazione e demo (Giorno 11–13)

1. **Costruisci un'applicazione demo:** crea una semplice app (es. un generatore di subject line di email basato su AI) che usa il sistema di flag. Mostra: il flag che parte da 0%, il rollout graduale con quality monitoring, il sistema che rileva una variante di prompt deliberatamente cattiva e fa auto-rollback e un rollout riuscito di una buona variante al 100%.
2. **Scrivi test di integrazione:** testa: assegnazione utente consistente tra le valutazioni, che il rollback automatico si inneschi correttamente sul degrado di qualità, che il rollout a fasi avanzi correttamente sulle soglie di qualità e che l'SDK gestisca con grazia le interruzioni del servizio dei flag.
3. **Containerizza tutto:** docker-compose con: PostgreSQL, Redis, l'API del servizio dei flag, il quality evaluator in background, la dashboard e l'applicazione demo. Includi uno script che esegue l'intero scenario demo di rollout end-to-end.

#### Fase 6: Rifinitura per il portfolio (Giorno 13–14)

1. **Registra la demo:** mostra l'intero ciclo di vita: flag creato, rollout avviato all'1%, qualità controllata e avanzamento attraverso le fasi, una variante cattiva rilevata e rolled back automaticamente con alert Slack, una buona variante che raggiunge il 100%. Sotto i 4 minuti.
2. **Scrivi la narrazione:** inquadrala come: "Ho costruito un sistema di feature flag per l'AI che intercetta le regressioni di qualità durante il rollout e fa auto-rollback prima che gli utenti siano colpiti. I feature flag tradizionali non possono farlo perché le feature AI falliscono su un gradiente, non su un binario." Quella distinzione è tutto il punto.

---

## Project 13: Automated Eval Dataset Generator from Production Logs

↪ **Step roadmap:** Step 22 (eval pipeline, evaluation regression) — collegamento a Step 7.5 (Dataset Engineering: acquisition, quality, annotation).

**Cosa costruisci:** un sistema che fa mining in continuo dei log LLM di produzione, identifica le interazioni interessanti, di casi limite e di failure mode e le converte automaticamente in casi di test di evaluation etichettati — costruendo un dataset di eval sempre in crescita e rappresentativo della produzione, senza curation manuale.

### Perché questo progetto fa colpo ai colloqui

La parte più difficile dell'evaluation AI non è costruire la eval harness — è costruire il dataset. La maggior parte dei team si affida a golden set curati a mano che diventano stantii. Tu stai risolvendo il problema dell'approvvigionamento dei dati trasformando il traffico di produzione in dati di eval automaticamente. È un moltiplicatore di forza che i team AI sognano.

### Stack tecnologico

| Componente | Tool / Libreria | Perché questa scelta |
| ---------- | --------------- | -------------------- |
| Linguaggio | Python 3.11+ | Standard per le pipeline ML |
| Storage dei log | PostgreSQL o ClickHouse | Log warehouse interrogabile |
| Clustering | scikit-learn + HDBSCAN | Scoperta dei pattern di interazione |
| LLM | GPT-4o o Claude Sonnet | Labeling e valutazione di qualità |
| Eval runner | Harness custom | Esegue le eval contro il dataset |
| Dashboard | Streamlit | Esplorazione e curation del dataset |
| Scheduler | Cron o Celery | Processing notturno automatico |
| Containerizzazione | Docker + docker-compose | Orchestrazione dell'intera pipeline |

### Guida alla costruzione passo-passo

#### Fase 1: Costruire il layer di ingestion e normalizzazione dei log (Giorno 1–3)

1. **Progetta lo schema dei log:** ogni entry di log di produzione cattura: il prompt utente, il system prompt, il modello usato, la risposta grezza dell'LLM, la latenza, i conteggi token, eventuali segnali di feedback utente (thumbs up/down, edit, retry), la feature applicativa che ha generato questa chiamata e un timestamp. Normalizza tutti i punti di chiamata LLM in questo formato unificato.
2. **Costruisci la pipeline di ingestion:** crea adapter per le sorgenti di logging comuni: log JSON strutturati, trace OpenTelemetry e letture dirette dal database. La pipeline deduplica, valida la conformità allo schema e scrive nel log store centrale. Gestisci le PII offrendo regole di redaction configurabili (pattern regex, named entity detection) che ripuliscono i dati sensibili prima dello storage.
3. **Implementa le strategie di campionamento:** non ti serve ogni entry di log — ti serve un campione rappresentativo. Costruisci tre modalità di campionamento: uniform random (diversità di baseline), stratified per feature/modello/stato-di-errore (assicura che tutti i segmenti siano rappresentati) e signal-boosted (sovracampiona le entry con feedback utente negativo, retry o alta latenza). Rendi il campionamento configurabile per ogni run della pipeline.

#### Fase 2: Costruire il classificatore di interazioni (Giorno 3–6)

1. **Clusterizza le interazioni per similarità semantica:** fai l'embedding di tutti i prompt campionati e clusterizzali con HDBSCAN. Questo rivela le categorie naturali di domande che il tuo sistema gestisce. Nomina ogni cluster in base a esempi rappresentativi. Traccia le dimensioni dei cluster per capire la distribuzione del tuo traffico.
2. **Identifica casi limite e anomalie:** segnala le interazioni che sono outlier: prompt che non clusterizzano bene (richieste nuove), risposte con confidence score bassi, interazioni in cui l'utente ha riprovato subito con una domanda riformulata, risposte insolitamente lunghe o corte e risposte che hanno innescato i content filter. Questi outlier sono i tuoi candidati di eval più preziosi.
3. **Categorizza la qualità delle interazioni:** usa un LLM-as-judge per valutare ogni interazione campionata: la risposta era utile, accurata e completa? Assegna un punteggio di qualità (1–5). Le interazioni di alta qualità diventano casi di test positivi (verifica che il modello continui a farlo bene). Le interazioni di bassa qualità diventano casi di test negativi (verifica che i modelli futuri lo correggano).
4. **Costruisci uno stimatore di difficoltà:** classifica ogni interazione per difficoltà: simple (domanda diretta, risposta chiara), moderate (richiede ragionamento o risposta multi-step), hard (ambigua, multi-parte o che richiede expertise di dominio) e adversarial (volutamente subdola, tentativi di prompt injection o input di casi limite). Le etichette di difficoltà aiutano a bilanciare il dataset di eval.

#### Fase 3: Costruire la pipeline di auto-labeling (Giorno 6–9)

1. **Genera golden answer per i casi di test:** per ogni candidato caso di test, genera una risposta di riferimento usando un modello forte (GPT-4o) con ragionamento chain-of-thought. Per le domande fattuali, verifica contro i dati sorgente se disponibili. Per le domande soggettive, genera una rubrica di qualità invece di una singola golden answer. Salva sia il riferimento sia la rubrica.
2. **Crea etichette multi-dimensionali:** ogni caso di test viene etichettato su: punteggio di qualità atteso (1–5), comportamento atteso (dovrebbe rispondere, dovrebbe rifiutare, dovrebbe chiedere chiarimenti), asserzioni chiave che la risposta DEVE contenere, asserzioni chiave che la risposta NON deve contenere (trappole di allucinazione) e la difficoltà e categoria dal classificatore.
3. **Implementa il routing basato su confidence:** non tutte le etichette auto-generate sono affidabili. Quando la confidence del modello di labeling è alta (forte accordo tra più run di labeling), aggiungi il caso di test al dataset automaticamente. Quando la confidence è bassa, instradalo a una coda di revisione umana. Questo fa crescere il dataset senza sacrificare la qualità.
4. **Costruisci la deduplicazione contro i dati di eval esistenti:** prima di aggiungere un nuovo caso di test, controlla la similarità contro tutti i casi di test esistenti. Se esiste un quasi-duplicato (cosine similarity > 0.92), saltalo. Traccia le metriche di copertura: quali cluster sono ben rappresentati e quali hanno bisogno di più esempi? Dai priorità alla generazione per le categorie sotto-rappresentate.

#### Fase 4: Costruire l'eval runner e il regression tracker (Giorno 9–11)

1. **Costruisci la eval harness:** un runner configurabile che: prende qualsiasi endpoint di modello, esegue l'intero dataset di eval contro di esso, valuta ogni risposta usando le rubriche e le metriche salvate e produce un report strutturato con tassi di pass/fail per categoria, per livello di difficoltà e per dimensione di metrica.
2. **Implementa il regression detection:** confronta ogni run di eval con il run precedente. Segnala: nuovi failure (casi di test che prima passavano e ora falliscono), nuovi pass (casi che fallivano e ora sono risolti), cambi di punteggio sopra una soglia e shift di performance a livello di categoria. È il sistema di allerta precoce per il degrado del modello.
3. **Traccia la crescita del dataset nel tempo:** dashboard che mostra: numero totale di casi di test nel tempo, distribuzione per categoria e difficoltà, conteggi auto-labeled vs. revisionati da umani, heatmap di copertura (quali cluster sono ben testati vs. sparsi) e la "freschezza" del dataset di eval (quale percentuale di casi di test proviene dagli ultimi 30 giorni di traffico di produzione).

#### Fase 5: Costruire la dashboard di curation (Giorno 11–13)

1. **Crea l'esploratore del dataset:** una UI dove chi rivede può: navigare i casi di test per categoria, difficoltà e qualità, vedere l'intera interazione (prompt, risposta, etichette), approvare, modificare o rifiutare le etichette auto-generate e aggiungere annotazioni o note manuali. È dove avviene la supervisione human-in-the-loop.
2. **Costruisci la coda di revisione:** le etichette auto-generate a bassa confidence finiscono in una coda di revisione. Mostra a chi rivede: il candidato caso di test, le etichette auto-generate con i confidence score, casi di test esistenti simili per contesto e pulsanti di azione rapida (approva così com'è, modifica le etichette, rifiuta). Traccia il throughput dei revisori e l'inter-annotator agreement.
3. **Containerizza e schedula:** docker-compose con: il log store, la pipeline di classificazione, il servizio di auto-labeling, l'eval runner e la dashboard di curation. Imposta un cron job notturno che esegue l'intera pipeline: campiona nuovi log, classifica, auto-etichetta, deduplica e aggiunge al dataset. La suite di eval cresce mentre dormi.

#### Fase 6: Rifinitura per il portfolio (Giorno 13–14)

1. **Registra la demo:** mostra: i log di produzione che vengono processati, il clustering che rivela i pattern di interazione, l'auto-labeling che genera i casi di test, l'eval runner che intercetta una regressione e la crescita del dataset nel tempo. Sotto i 4 minuti.
2. **Scrivi la narrazione:** inquadrala come: "Ho costruito un sistema che converte automaticamente i log LLM di produzione in un dataset di eval in crescita. In due settimane di traffico di produzione simulato, ha generato X casi di test su Y categorie con il Z% di accuratezza dell'auto-labeling." L'aspetto auto-crescente è il titolo.

---

## Project 14: Multi-Modal Document Processor with OCR, LLM Extraction, and Validation

↪ **Step roadmap:** Step 14 (structured extraction da documenti, PII) come dominio; Step 15.5 (vision transformer basics) per la parte CV/OCR.

**Cosa costruisci:** una pipeline end-to-end di document processing che accetta qualsiasi formato di documento (PDF, immagine, scansione), esegue l'OCR per estrarre il testo grezzo, usa gli LLM per estrarre dati strutturati dal testo e valida ogni estrazione contro regole di business configurabili — con un'interfaccia di revisione human-in-the-loop per i risultati a bassa confidence.

### Perché questo progetto fa colpo ai colloqui

Il document processing è una delle più grandi categorie di deployment AI enterprise. Combina computer vision (OCR), natural language understanding (extraction) e production engineering (validazione, error handling, scala). Questo progetto tocca ogni layer dello stack di AI engineering e risolve un problema che ogni grande azienda sta pagando attivamente per risolvere.

### Stack tecnologico

| Componente | Tool / Libreria | Perché questa scelta |
| ---------- | --------------- | -------------------- |
| Linguaggio | Python 3.11+ | Standard dell'ecosistema ML |
| OCR | Tesseract + EasyOCR | Open-source, multi-engine |
| Vision model | GPT-4o vision o Claude | Comprensione diretta delle immagini |
| LLM extraction | GPT-4o + instructor | Enforcement dello structured output |
| Validazione | Pydantic + regole custom | Business rule type-safe |
| Queue | Celery + Redis | Processing asincrono dei documenti |
| Review UI | React o Streamlit | Interfaccia human-in-the-loop |
| Containerizzazione | Docker + docker-compose | Orchestrazione dell'intera pipeline |

### Guida alla costruzione passo-passo

#### Fase 1: Costruire il layer di ingestion e OCR (Giorno 1–3)

1. **Costruisci un document loader multi-formato:** accetta PDF (testo nativo e scansionati), immagini (JPEG, PNG, TIFF) e documenti scansionati. Per i PDF, prova prima l'estrazione di testo nativa (PyMuPDF). Se il PDF ha immagini o l'estrazione di testo produce spazzatura, ripiega sull'OCR. Rileva la strategia giusta automaticamente controllando la densità di testo per pagina.
2. **Implementa l'OCR a doppio motore:** esegui sia Tesseract sia EasyOCR su ogni pagina scansionata. Confronta gli output. Quando concordano, la confidence è alta. Quando dissentono, usa l'allineamento a livello di carattere per identificare le discrepanze e scegli la lettura a confidence più alta per ogni segmento. Questo approccio ensemble riduce significativamente gli errori di OCR.
3. **Aggiungi il fallback al vision model:** per i documenti dove l'OCR fatica (scrittura a mano, scansioni di scarsa qualità, layout complessi come le tabelle), invia l'immagine della pagina direttamente a GPT-4o vision o Claude vision. Chiedi al modello di estrarre il testo preservando la struttura del documento. È più costoso ma gestisce casi limite che l'OCR tradizionale non può.
4. **Costruisci la pipeline di preprocessing:** prima dell'OCR, applica: deskewing (raddrizzamento delle scansioni ruotate), binarizzazione (conversione in bianco e nero ad alto contrasto), no […]

> ℹ️ **Nota editoriale:** il punto 4 della Fase 1 del Project 14 arrivava troncato nell'incolla originale subito dopo "binarizzazione (conversione in bianco e nero ad alto contrasto), no". Il resto dell'elenco di preprocessing non è stato fornito.

#### Fase 2: Costruire il motore di estrazione LLM (Giorno 3–6)

1. **Definisci schemi di estrazione per tipo di documento:** crea modelli Pydantic per ogni tipo di documento che processi. Per le fatture: nome fornitore, numero fattura, voci di riga (descrizione, quantità, prezzo unitario, totale), tasse, importo totale, termini di pagamento, scadenza. Per i contratti: parti, data di efficacia, durata, obbligazioni chiave, clausole di risoluzione. Rendi gli schemi configurabili ed estensibili.
2. **Costruisci la pipeline di estrazione:** per ogni documento, classifica prima il suo tipo (usando il testo OCR + un classificatore LLM). Poi carica lo schema di estrazione corrispondente. Invia il testo OCR all'LLM con: la definizione dello schema, 2–3 esempi few-shot per quel tipo di documento e istruzioni esplicite di restituire solo le informazioni presenti nel testo (nessuna inferenza, nessun default). Usa la libreria instructor per imporre lo schema Pydantic nell'output dell'LLM.
3. **Implementa il chunk-and-merge per i documenti lunghi:** i documenti più lunghi della context window devono essere processati a chunk. Dividi per pagina o sezione, estrai da ogni chunk in modo indipendente, poi fai il merge dei risultati. Gestisci i conflitti: se due chunk estraggono valori diversi per lo stesso campo, segnala il conflitto e includi entrambi i valori con la loro posizione sorgente.
4. **Aggiungi i confidence score di estrazione:** per ogni campo estratto, calcola un confidence score basato su: quanto chiaramente il valore compariva nel testo OCR (match esatto vs. fuzzy), la confidence auto-riportata dall'LLM, se più chunk concordavano sul valore e se il valore supera la validazione di formato (es. le date si parsano correttamente, gli importi sono numerici). Restituisci la confidence per campo accanto all'estrazione.

#### Fase 3: Costruire il motore di validazione e business rule (Giorno 6–9)

1. **Implementa la validazione a livello di tipo:** usando i validator di Pydantic, imponi: le date sono valide e in range plausibili, gli importi monetari sono positivi e formattati correttamente, i campi obbligatori sono presenti, gli enum corrispondono ai valori permessi e la coerenza cross-field (es. i totali delle voci di riga sommano al totale della fattura). Restituisci messaggi di errore di validazione specifici per campo.
2. **Aggiungi la validazione delle business rule:** oltre al type checking, implementa regole specifiche di dominio. Per le fatture: il fornitore esiste nella lista dei fornitori noti? Il totale è nei range attesi per questo fornitore? I termini di pagamento sono standard? Per i contratti: la data di efficacia è nel futuro? Tutti i tipi di clausola richiesti sono presenti? Ci sono clausole di risoluzione insolitamente ampie?
3. **Costruisci l'anomaly detector:** confronta ogni estrazione con i dati storici per quel tipo di documento e quella fonte. Segnala gli outlier statistici: importi significativamente più alti o più bassi del tipico, nomi di fornitore insoliti, date che non seguono il pattern atteso e qualsiasi campo che è cambiato drasticamente rispetto ai documenti precedenti della stessa fonte.
4. **Crea il routing basato su confidence:** in base al confidence score complessivo e ai risultati di validazione, instrada ogni documento: alta confidence + tutte le validazioni superate → auto-approva, media confidence o warning di validazione minori → coda di revisione umana (revisione rapida), bassa confidence o fallimenti di validazione critici → coda di revisione umana (revisione dettagliata). Traccia i tassi di auto-approvazione e l'accuratezza nel tempo.

#### Fase 4: Costruire l'interfaccia di revisione umana (Giorno 9–11)

1. **Crea la dashboard di revisione:** un'interfaccia affiancata che mostra: il documento originale (renderizzato come immagine) da un lato e i dati estratti dall'altro. Evidenzia la posizione sorgente nel documento per ogni campo estratto. Codifica i campi per colore in base alla confidence: verde (alta), giallo (media), rosso (bassa/validazione fallita).
2. **Costruisci l'editing inline:** chi rivede può cliccare qualsiasi campo estratto per modificarlo. Quando modificato, logga: il valore estratto originale, il valore corretto, chi ha corretto e se l'originale era sbagliato (errore di estrazione) o la business rule era troppo rigida (falso positivo di validazione). Questi dati alimentano il miglioramento sia dell'estrazione sia della validazione.
3. **Implementa workflow di revisione batch:** per il processing ad alto volume, costruisci un workflow basato su coda: chi rivede vede una lista prioritizzata di documenti che necessitano revisione, può approvare/rifiutare/modificare in bulk e vede le proprie statistiche di throughput e accuratezza. Includi scorciatoie da tastiera per le azioni comuni per massimizzare l'efficienza dei revisori.

#### Fase 5: Costruire i feedback loop e le analytics (Giorno 11–13)

1. **Riporta le correzioni alla pipeline di estrazione:** ogni correzione umana diventa un segnale di training. Accumula le correzioni e periodicamente: aggiorna gli esempi few-shot con esempi corretti, identifica gli errori sistematici di estrazione e aggiusta i prompt, tara le soglie di confidence in base all'accuratezza reale e genera report su dove la pipeline fallisce di più.
2. **Costruisci la dashboard di analytics del processing:** mostra: documenti processati per giorno/settimana, tasso di auto-approvazione nel tempo (la metrica chiave di efficienza), accuratezza di estrazione per tipo di documento e campo, tempo medio di revisione per documento e confronto delle performance dei motori OCR. Queste metriche raccontano la storia della maturità operativa della pipeline.
3. **Containerizza l'intera pipeline:** docker-compose con: l'API di ingestion, gli OCR worker, gli LLM extraction worker, il servizio di validazione, la review UI, PostgreSQL, Redis e i Celery worker. Includi documenti di esempio per scopi dimostrativi.

#### Fase 6: Rifinitura per il portfolio (Giorno 13–14)

1. **Registra la demo:** mostra: il caricamento di una fattura scansionata, l'OCR che estrae il testo, l'LLM che estrae dati strutturati, la validazione che intercetta un'anomalia, il revisore che corregge un campo e la dashboard di analytics. Sotto i 4 minuti.
2. **Scrivi la narrazione:** inquadrala come: "Ho costruito una pipeline di document processing che auto-estrae dati strutturati da documenti scansionati con il X% di accuratezza, auto-approva il Y% dei documenti senza revisione umana e riduce il tempo di processing manuale del Z%." Parti dai numeri di efficienza.

---

## Project 15: Agent Orchestration System with Tool Use, Memory, and Human-in-the-Loop

↪ **Step roadmap:** Step 21 (agenti, tool use, memoria, guardrail) come base; Step 28 (Track GH-600, multi-agent orchestration, autonomy levels, HITL) per la versione GitHub-specifica.

**Cosa costruisci:** una piattaforma di orchestrazione multi-agente dove un supervisor agent scompone task complessi, delega i subtask ad agenti specializzati che usano tool, mantiene una memoria persistente tra le interazioni ed esegue l'escalation a un operatore umano quando la confidence è bassa o il task richiede approvazione — con observability completa su ogni decisione degli agenti.

### Perché questo progetto fa colpo ai colloqui

Gli agenti sono la frontiera dell'AI engineering, e la maggior parte dei progetti dei candidati sono demo giocattolo single-agent. Costruire un sistema multi-agente con vero tool use, memoria persistente ed escalation human-in-the-loop dimostra che sai architettare il tipo di sistemi AI autonomi che le aziende stanno costruendo e per cui stanno assumendo proprio adesso.

### Stack tecnologico

| Componente | Tool / Libreria | Perché questa scelta |
| ---------- | --------------- | -------------------- |
| Linguaggio | Python 3.11+ | Standard dell'ecosistema |
| Orchestrazione | LangGraph | State machine per i workflow degli agenti |
| Provider LLM | OpenAI + Anthropic | Routing multi-modello degli agenti |
| Tool framework | Custom + MCP | Integrazione estensibile dei tool |
| Memoria | PostgreSQL + ChromaDB | Short-term + semantica long-term |
| Queue | Redis + Celery | Esecuzione asincrona dei task |
| Review UI | React o Streamlit | Interfaccia human-in-the-loop |
| Containerizzazione | Docker + docker-compose | Orchestrazione dell'intero sistema |

### Guida alla costruzione passo-passo

#### Fase 1: Costruire l'architettura degli agenti (Giorno 1–4)

1. **Progetta la gerarchia degli agenti:** crea tre layer. Il Supervisor Agent riceve task complessi, crea piani di esecuzione e delega agli specialist. Gli Specialist Agent possiedono ognuno un dominio (research, data analysis, writing, code execution) e hanno accesso a tool specifici di dominio. Il Reviewer Agent valida gli output degli specialist prima di restituirli al supervisor. Modella ogni agente come un nodo LangGraph con schemi di input/output definiti.
2. **Costruisci il motore di decomposizione dei task:** la capacità centrale del supervisor: prendere una richiesta complessa e scomporla in una lista ordinata di subtask, ognuno assegnato a uno specialist. Includi le dipendenze (il subtask B ha bisogno dell'output del subtask A). Usa structured output per imporre un piano di esecuzione valido con: descrizione del subtask, specialist assegnato, input richiesti, formato di output atteso e complessità stimata.
3. **Implementa il tool registry:** costruisci un registry dove i tool sono registrati con: un nome, una descrizione, schemi di input/output, gli specialist agent che possono usarli e i rate limit. Parti da: web search, file read/write, code execution (sandboxed), database query e API call. Ogni invocazione di tool è loggata con input, output, latenza e success/failure.
4. **Costruisci la state machine LangGraph:** collega gli agenti in un grafo LangGraph con: task intake → planning → esecuzione parallela/sequenziale degli specialist → review → sintesi → consegna. Includi edge condizionali: se uno specialist fallisce, riprova con un approccio diverso; se il reviewer rifiuta l'output, instrada di nuovo allo specialist con il feedback; se la confidence è bassa, instrada all'escalation umana.

#### Fase 2: Costruire il sistema di memoria (Giorno 4–7)

1. **Implementa la working memory a breve termine:** durante l'esecuzione di un task, tutti gli agenti condividono uno store di working memory: il piano di esecuzione corrente, gli output dei subtask completati, i risultati intermedi e i log di errore. Salva in Redis per un accesso veloce. Questa memoria è scoped a un singolo task e azzerata quando il task si completa.
2. **Costruisci la memoria semantica a lungo termine:** dopo il completamento del task, estrai e fai l'embedding delle informazioni chiave: cosa ha chiesto l'utente, quale approccio ha funzionato, quali tool sono stati usati, eventuali fatti specifici di dominio scoperti e le preferenze utente osservate. Salva in ChromaDB. I task futuri possono interrogare questa memoria per informare il planning. È così che il sistema diventa più intelligente nel tempo.
3. **Implementa il recupero della memoria per il planning:** quando il supervisor crea un piano di esecuzione, interroga prima la memoria a lungo termine per: task passati simili e i loro piani di esecuzione, approcci che hanno funzionato bene (e quelli che non l'hanno fatto), preferenze e contesto specifici dell'utente e fatti di dominio rilevanti. Le memorie recuperate vengono iniettate nel prompt di planning.
4. **Aggiungi la gestione della memoria:** implementa: scoring di importanza della memoria (le memorie accedute di frequente sono più importanti), consolidamento della memoria (fondi memorie simili in riassunti di livello più alto), scadenza della memoria (le memorie stantie decadono nel tempo) e una dashboard di memoria che mostra cosa il sistema "ricorda" di ogni utente. Includi un endpoint di cancellazione per le richieste sui dati dell'utente.

#### Fase 3: Costruire il sistema human-in-the-loop (Giorno 7–10)

1. **Definisci i trigger di escalation:** il sistema fa escalation a un umano quando: la confidence del supervisor nel suo piano è sotto una soglia, uno specialist fallisce due volte sullo stesso subtask, il task coinvolge operazioni sensibili (transazioni finanziarie, cancellazione di dati, comunicazioni esterne), il punteggio di qualità del reviewer per un deliverable è sotto soglia o l'utente richiede esplicitamente la revisione umana.
2. **Costruisci la coda di approvazione:** quando scatta l'escalation, il sistema: mette in pausa l'esecuzione allo step corrente, impacchetta il contesto completo (task originale, piano, step completati, step corrente che necessita approvazione, l'azione proposta dall'agente), lo spinge in una coda di revisione e notifica il revisore umano. Il sistema attende approvazione, rifiuto o modifica prima di continuare.
3. **Implementa livelli di approvazione granulari:** non tutte le escalation hanno bisogno della stessa profondità di revisione. Definisci i livelli: Notify (procedi ma informa l'umano), Approve action (l'umano conferma lo step successivo), Approve plan (l'umano rivede l'intero piano di esecuzione prima che inizi qualsiasi lavoro) e Take over (l'umano fornisce direttamente l'output, gli agenti si fermano). Mappa i trigger di escalation ai livelli appropriati.
4. **Costruisci l'interfaccia di revisione:** una UI che mostra: il contesto del task e l'avanzamento dell'esecuzione, il punto decisionale specifico che richiede input umano, l'azione proposta dall'agente con il suo ragionamento, memorie rilevanti e decisioni simili passate e pulsanti di azione (approva, modifica, rifiuta, prendi il controllo). Includi un pannello di chat perché l'umano possa porre domande di chiarimento all'agente prima di decidere.

#### Fase 4: Costruire observability e debugging (Giorno 10–12)

1. **Implementa il tracing completo dell'esecuzione:** ogni esecuzione di task produce un albero di trace: le decisioni di planning del supervisor, le chiamate di tool e gli step di ragionamento di ogni specialist, le valutazioni del reviewer, i recuperi di memoria e la loro influenza sulle decisioni e gli eventi di escalation umana e le loro risoluzioni. Usa span OpenTelemetry con attributi custom.
2. **Costruisci la UI di trace explorer:** una rappresentazione visuale del workflow degli agenti come albero/grafo. Ogni nodo mostra: l'agente che ha agito, cosa ha deciso, quali tool ha chiamato, latenza e costo ed eventuali errori. Codifica per colore lo status (success/warning/failure/escalated). Cliccando un nodo si espande il contesto completo incluso il prompt LLM e la risposta.
3. **Aggiungi il tracciamento di costo e performance:** per task, traccia: token LLM totali usati (per agente e modello), totale delle chiamate di tool, tempo totale wall-clock, tempo di revisione umana (se in escalation) e costo totale. Aggrega tra i task per mostrare: costo per tipo di task, agenti più costosi, pattern di uso dei tool e trend del tasso di escalation.
4. **Costruisci il sistema di replay:** per il debugging, consenti di rieseguire qualsiasi esecuzione di task passata: carica il task e il contesto originali, percorri passo passo ogni decisione degli agenti, modifica qualsiasi input a qualsiasi step e vedi come l'esecuzione diverge e confronta l'esecuzione rieseguita con l'originale. È preziosissimo per diagnosticare i failure e testare i miglioramenti.

#### Fase 5: Integrazione e testing end-to-end (Giorno 12–13)

1. **Costruisci uno scenario demo convincente:** progetta un task complesso che mostri l'intero sistema: un task di research che richiede web search, data extraction, analisi e un riassunto scritto. Mostra: il supervisor che scompone il task, gli specialist che lavorano in parallelo, il reviewer che intercetta un problema e lo rimanda indietro, la memoria che informa una decisione e un umano che approva il deliverable finale.
2. **Containerizza l'intero sistema:** docker-compose con: l'API di orchestrazione, Redis (working memory), PostgreSQL (stato persistente), ChromaDB (memoria a lungo termine), Celery worker (specialist asincroni), la UI di trace explorer e la UI di revisione umana. Includi uno script demo che esegue lo scenario vetrina automaticamente.
3. **Scrivi test end-to-end:** testa: che la decomposizione dei task produca piani validi, che gli specialist usino correttamente i loro tool, che il reviewer intercetti output deliberatamente cattivi, che il recupero della memoria migliori il planning per task simili ripetuti, che l'escalation umana scatti nei momenti giusti e che il sistema si riprenda con grazia dai failure degli agenti.

#### Fase 6: Rifinitura per il portfolio (Giorno 13–14)

1. **Registra la demo:** mostra l'intero ciclo di vita del task: richiesta complessa in ingresso, planning del supervisor, specialist che eseguono con chiamate di tool, reviewer che valida, umano che approva uno step sensibile, memoria che salva le lezioni apprese e il trace explorer che mostra ogni decisione. Sotto i 5 minuti.
2. **Scrivi la narrazione:** inquadrala come: "Ho costruito un sistema di orchestrazione multi-agente dove gli agenti AI scompongono task complessi, usano tool per eseguirli, imparano dalle interazioni passate via memoria persistente e fanno escalation agli umani quando la confidence è bassa. Non è una demo AI — è infrastruttura di produzione per workflow AI autonomi." Parti dal diagramma di architettura che mostra la gerarchia degli agenti e il flusso decisionale.
