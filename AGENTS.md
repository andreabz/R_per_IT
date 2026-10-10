# AGENTS.md — Istruzioni per gli agenti di R_per_IT

## 1. Mandato del progetto

R_per_IT è un manuale tecnico rivolto a sistemisti, architetti, DevOps, team di piattaforma e responsabili tecnici che devono comprendere, valutare, integrare, distribuire e gestire soluzioni sviluppate in R.

L'obiettivo **non** è formare sviluppatori R né sostituire la formazione generale su sistemi operativi, reti, database o piattaforme. Il corso deve aiutare IT a capire che cosa cambia quando il workload è R e a trasformare una richiesta tecnica in requisiti verificabili, evidenze, decisioni, responsabilità e baseline.

Principio guida:

> Prima di aumentare le risorse, capire perché servono.

R è normalmente un componente dello stack aziendale, non un sostituto automatico di Oracle, APEX, scheduler, web server, identity management, storage, gateway o sistemi di orchestrazione. Il materiale deve chiarire i confini tra componenti e promuovere il riuso dello stack aziendale quando appropriato.

## 2. Destinatari e risultato atteso

Il destinatario deve poter:

- riconoscere la forma applicativa e il suo punto di ingresso;
- identificare runtime R, package, dipendenze native, driver e sistemi esterni;
- descrivere workload, input/output, frequenza, durata, concorrenza e risorse;
- distinguere misure ed evidenze da ipotesi;
- valutare requisiti di deployment, sicurezza, osservabilità, rollback e ownership;
- individuare le informazioni mancanti nell'handover e chiederle in modo concreto;
- confrontare alternative architetturali senza assumere che una soluzione sia sempre migliore delle altre.

Il livello tecnico è **approfondito sul piano operativo e architetturale**. Il codice va incluso quando rende verificabile un comportamento, chiarisce una configurazione o consente un esperimento riproducibile; non va usato per trasformare il corso in un tutorial di programmazione.

## 3. Metodo di lavoro sugli artefatti esistenti

Prima di aggiungere contenuti:

1. leggere la sezione e i file pertinenti già presenti;
2. cercare sovrapposizioni, contraddizioni e contenuti che possono essere corretti o approfonditi;
3. decidere se correggere, integrare, collegare o aggiungere materiale;
4. mantenere coerenti manuale, indice, slide, esempi e configurazione di pubblicazione.

Non creare una seconda spiegazione dello stesso concetto se è sufficiente migliorare o richiamare quella esistente. Non introdurre nuovi capitoli o sezioni di primo livello senza una motivazione esplicita.

### Autonomia e limiti delle modifiche

- **Correzioni locali:** gli agenti possono correggere direttamente errori tecnici, imprecisioni, esempi incompleti, problemi di formattazione, chunk Quarto, link e problemi di rendering.
- **Revisioni sostanziali:** gli agenti possono riscrivere o integrare sezioni esistenti quando migliorano chiarezza, accuratezza e utilità operativa senza cambiare l'impianto del corso.
- **Modifiche strutturali:** prima di spostare capitoli, cambiare la progressione degli scenari o ampliare significativamente il perimetro, presentare una proposta motivata. Non eseguire autonomamente queste modifiche.
- **Manuale e slide:** le modifiche tecniche al manuale devono essere riflesse nelle slide quando pertinenti; le slide non devono diventare una copia ridotta del manuale.
- **Configurazione di pubblicazione:** non modificare workflow GitHub Actions, destinazioni o impostazioni di pubblicazione per comodità. Se serve una modifica strutturale, motivarla prima.

## 4. Progressione didattica: scenari crescenti

Organizzare il materiale intorno a scenari operativi crescenti, non intorno a una lista astratta di tecnologie. Gli scenari sono una struttura narrativa e comparativa, **non** una scala obbligatoria di maturità aziendale.

### Livello 1 — Esecuzione e artefatti

- esplorazione e sviluppo locale;
- script personale o condiviso;
- esecuzione fuori dall'IDE tramite Rscript;
- job batch gestito da scheduler;
- report Quarto generato manualmente o in modo automatizzato.

### Livello 2 — Software riproducibile e pipeline

- package R;
- dipendenze, test, versionamento e release;
- pipeline e passaggio di artefatti;
- ambienti riproducibili e container;
- promozione tra test e produzione.

### Livello 3 — Servizi e applicazioni

- applicazioni Shiny, sessioni e reattività;
- deployment Shiny, ShinyProxy e, quando pertinente, ShinyProxy Operator su Kubernetes;
- API HTTP esposte con plumber2;
- consumo di API HTTP da R, incluso httr2;
- integrazione con Oracle, APEX, GIS e altri sistemi;
- concorrenza, autenticazione, autorizzazione, sicurezza e osservabilità.

Una singola soluzione può combinare più scenari: per esempio un job batch che genera un report Quarto, una Shiny che interroga Oracle o un'API R invocata da un sistema gestionale.

## 5. Scheda operativa per ogni scenario

Quando pertinente, descrivere ogni scenario con una struttura uniforme. Non forzare sezioni irrilevanti: dichiarare invece perché un requisito non si applica.

1. **Prodotto e scopo:** che cosa fa e quale responsabilità ricade su R.
2. **Struttura ed entry point:** file principali, punto di avvio e artefatto distribuito.
3. **Esecuzione:** IDE, console, Rscript, scheduler, server, processo persistente o orchestratore.
4. **Ambiente:** versione R di riferimento quando nota, package, repository, dipendenze native, driver e lockfile.
5. **Input, output e dati:** formati, volumi, provenienza, persistenza, sensibilità e confini di responsabilità.
6. **Workload e risorse:** durata, frequenza, CPU, RAM, I/O, rete, concorrenza e variabilità.
7. **Verifiche:** test funzionali, d'integrazione, compatibilità e performance.
8. **Distribuzione:** build, artefatto, configurazione, promozione, rollback e dipendenze esterne.
9. **Sicurezza:** account, privilegi minimi, autenticazione, autorizzazione, segreti, TLS e dati esposti.
10. **Esercizio:** log, errori, exit code o codici HTTP, timeout, retry, health check, monitoraggio e allarmi.
11. **Handover e ownership:** informazioni da consegnare, responsabilità dello sviluppatore e di IT, runbook e baseline.

Distinguere sempre:
- **necessario:** requisito senza il quale lo scenario non è gestibile o non soddisfa il contratto;
- **condizionale:** necessario solo in presenza di uno specifico rischio o requisito;
- **buona pratica:** raccomandazione motivata, non requisito universale.

Non dichiarare un'applicazione pronta per la produzione soltanto perché si avvia o supera un test funzionale.

## 6. Runtime, memoria, parallelismo e performance

Spiegare il comportamento rilevante per IT senza promettere risultati universali. Distinguere processo R, worker, thread nativi, memoria logica degli oggetti e memoria osservata dal sistema operativo.

### Laboratori richiesti

Preparare **sia un caso integrato sia laboratori specifici**:

- **Caso integrato:** un workload sintetico ma plausibile, con input e output definiti, usato per confrontare strategie di esecuzione e interpretare compromessi.
- **Profiling:** usare, dove appropriato, system.time(), Rprof(), profvis e metriche del sistema operativo; distinguere tempo CPU, tempo trascorso, I/O e attese esterne.
- **Memoria:** analizzare copie e oggetti intermedi, selezione di colonne, elaborazione per blocchi e picco di RSS; non dedurre il consumo di RAM dalla sola dimensione logica degli oggetti R.
- **Parallelismo:** confrontare esecuzione sequenziale e numero ragionevole di worker (per esempio 2, 4 e 8 quando sensato); misurare durata, speedup, efficienza, RAM, serializzazione e saturazione. Distinguere processi R e thread di librerie native/BLAS.
- **Database:** confrontare, su dati equivalenti, trasferimento completo e filtraggio/aggregazione lato database; registrare righe, colonne, volume trasferito e tempi lato database e lato R.

Ogni benchmark deve dichiarare ambiente, versione quando rilevante, input, metodo, metrica, strategie confrontate e limiti di generalizzazione. Evitare confronti non riproducibili o numeri presentati come universali.

Non assumere che parallelizzare migliori le prestazioni: può aumentare RAM, overhead, serializzazione e carico sui database, oppure peggiorare la contesa per le risorse.

## 7. Shiny: riconoscimento, ciclo di vita e gestione

Trattare Shiny come prodotto applicativo e workload concorrente, non soltanto come codice R.

### Strutture da riconoscere

- **app.R:** file singolo che può contenere interfaccia, logica server e inizializzazione.
- **ui.R e server.R:** struttura separata; individuare anche eventuale global.R e gli altri file richiamati.
- **global.R:** viene eseguito all'avvio dell'applicazione prima delle sessioni; oggetti e dati creati qui possono restare in memoria ed essere condivisi tra le sessioni servite dallo stesso processo.
- **Struttura di package o framework:** per esempio golem, Rhino o convenzioni personalizzate; individuare entry point, moduli, risorse, configurazione, dipendenze e procedura di avvio/build.

Non presentare queste strutture come modelli di esecuzione necessariamente diversi. Il comportamento va dedotto dal codice e dal modo in cui l'applicazione viene avviata.

### Ciclo di vita e risorse

Spiegare la differenza tra avvio del processo, creazione della sessione e oggetti condivisi. Distinguere stato reattivo e oggetti specifici della sessione da dati o cache condivisi. Un oggetto globale mutabile può causare interferenze tra utenti; una cache in memoria di un processo non è automaticamente condivisa fra processi o container.

Prevedere un esempio che confronti il caricamento di un dataset nell'ambito globale con il caricamento per sessione, mostrando implicazioni su tempi, RAM, isolamento e aggiornamento dei dati. Non sostenere che ogni oggetto venga caricato nuovamente per ogni sessione.

Approfondire input/output/reactive expressions, invalidazione, caching, sessioni simultanee, diagnosi con uno e più utenti, operazioni bloccanti e comportamento al riavvio.

### Deployment

Confrontare, quando pertinente, esecuzione diretta su host, container e ShinyProxy; citare ShinyProxy Operator in Kubernetes se utile allo scenario. Fornire configurazioni e comandi **quasi eseguibili**, sufficientemente completi da mostrare i confini tra componenti e il percorso di avvio, ma adattabili all'infrastruttura aziendale.

Per ogni esempio:
- indicare prerequisiti e assunzioni;
- marcare chiaramente valori, host, percorsi, porte, immagini e segreti da sostituire;
- non inserire credenziali reali né suggerire segreti nel repository;
- distinguere TLS termination, autenticazione, autorizzazione, isolamento, gestione dei segreti e osservabilità;
- non presentare configurazioni illustrative come approvate o pronte per la produzione senza aver verificato compatibilità e requisiti.

## 8. API: plumber2 e consumo HTTP con httr2

Distinguere esplicitamente i due ruoli: **plumber2 espone servizi HTTP da R; httr2 consuma servizi HTTP da R**.

### API esposte

Aiutare a riconoscere:
- script o router con endpoint e punto di avvio;
- API suddivisa in più router/file e logica applicativa;
- API la cui logica è organizzata in un package R;
- servizio eseguito direttamente, in container o dietro proxy/gateway.

Descrivere il contratto HTTP: metodi, percorsi, parametri, body, header, formati, codici di stato e struttura degli errori. Trattare validazione input, richieste simultanee, operazioni bloccanti, connessioni ai sistemi esterni, timeout, limiti di richiesta, log, health check, versionamento, autenticazione e autorizzazione.

Distinguere una verifica di liveness dalla verifica della disponibilità delle dipendenze necessarie. Non assumere che un'API sia automaticamente asincrona, scalabile o sicura.

### API consumate con httr2

Includere almeno un esempio riproducibile di richiesta e gestione della risposta. Coprire GET/POST, URL, query parameters, header, body, parsing JSON, codici HTTP, timeout, errori, autenticazione, retry limitati e paginazione quando pertinente.

Evidenziare che i retry devono essere compatibili con l'operazione e con i codici di errore: non ripetere indiscriminatamente operazioni non idempotenti. Non inserire token o credenziali nel codice sorgente o nei log.

Collegare chiamante e servizio con un esempio HTTP/JSON che chiarisca il contratto tra componenti, la responsabilità degli errori e i confini di sicurezza.

## 9. Integrazioni con lo stack aziendale

Trattare le integrazioni dal punto di vista dei confini e dei contratti, non come corsi completi sui sistemi esterni.

- **Oracle:** driver, autenticazione, query, transazioni, pool quando pertinente, volumi, pushdown di filtri e aggregazioni, timeout e gestione delle connessioni.
- **APEX:** confine tra workflow gestionale e calcolo analitico; invocazione di servizi, scambio di parametri e risultati, gestione degli errori.
- **GIS:** dati spaziali, formati, database geografici, sistemi di coordinate e trasferimento dei dati.
- **Scheduler e orchestratori:** account, ambiente, working directory, exit code, log, timeout, retry, dipendenze e idempotenza.
- **Proxy e gateway:** routing, TLS, autenticazione, limiti, timeout e logging.
- **CI/CD e container:** test, build, artefatto, configurazione, promozione e rollback.

Non duplicare automaticamente in R funzioni già svolte in modo adeguato da database, scheduler, gateway o piattaforma aziendale. Dichiarare sempre dove viene eseguito il calcolo e quale componente è responsabile di ogni funzione.

## 10. Versioni e documentazione tecnica

Il manuale descrive le tecnologie in termini generali e **non impone una baseline fissa di versioni**.

Quando una procedura, una configurazione o un comportamento dipende dalla versione:
- indicare esplicitamente la dipendenza;
- distinguere comportamento generale e dettaglio version-specific;
- verificare la documentazione ufficiale pertinente prima di affermare che un comando o una configurazione siano validi;
- evitare di inventare opzioni, direttive, nomi di immagini, API o compatibilità;
- non dichiarare una configurazione compatibile con una versione non verificata.

Gli esempi di deployment devono essere quasi eseguibili, con comandi e configurazioni concreti, ma devono indicare prerequisiti, variabili da sostituire e punti da verificare sull'ambiente target. La concretezza non equivale a una garanzia di produzione.

## 11. Standard editoriali

- Scrivere in italiano tecnico, preciso e diretto.
- Preferire spiegazioni concrete, tabelle comparative e diagrammi utili a decidere.
- Evitare slogan, frasi motivazionali, ripetizioni e affermazioni generiche non verificabili.
- Non introdurre codice solo per decorazione; spiegare perché ogni esempio serve a una decisione IT.
- Definire i termini tecnici al primo uso quando non sono ovvi per il destinatario.
- Separare fatti, assunzioni, esempi e raccomandazioni.
- Evitare di presentare una buona pratica come obbligo universale.
- Mantenere nomenclatura e significato dei termini coerenti tra capitoli e slide.
- Usare Mermaid solo quando migliora la comprensione di flussi, confini o decisioni; i diagrammi devono essere validi e leggibili.

## 12. Standard Quarto e codice

- Per i chunk eseguibili Quarto usare fence con **tre backtick** e opzioni nel formato Quarto corretto.
- Ogni chunk deve avere una label esplicita e univoca, ad esempio `#| label: benchmark-rss`.
- Le label devono essere stabili, descrittive e non duplicate nell'intero progetto.
- Per i diagrammi Mermaid usare il fence Quarto corretto, per esempio `\x60\x60\x60{mermaid}`, e `%%| echo: false` quando il codice sorgente del diagramma non deve apparire nel documento renderizzato.
- Non racchiudere codice destinato a essere eseguito da Quarto in fence alternativi che ne impediscano l'esecuzione. I fence Markdown per codice mostrato come testo sono ammessi quando intenzionali.
- Non lasciare chunk incompleti, label provvisorie, link rotti, riferimenti a file inesistenti o output che contraddicono il testo.
- Rendere gli esempi riproducibili quando ragionevole; documentare input, dipendenze e limiti quando non possono esserlo integralmente.
- Evitare di aggiungere dipendenze R non necessarie agli esempi.

## 13. Standard per le slide

Il manuale è la fonte autorevole per spiegazioni, esempi, comandi, configurazioni, confronti e caveat. Le slide sintetizzano lo stesso percorso decisionale: non sono un documento indipendente né una copia integrale del manuale.

Ogni modifica tecnica pertinente al manuale deve essere valutata anche per le slide, mantenendo coerenti:
- scenari e loro progressione;
- termini e definizioni;
- decisioni, diagrammi e confini tra componenti;
- conclusioni tecniche e avvertenze.

Vincoli editoriali:
- massimo **otto righe di testo o elementi** per slide, salvo casi in cui una struttura visiva renda il contenuto chiaramente leggibile;
- evitare frasi motivazionali o formule retoriche: arrivare al punto;
- limitare il codice alle righe necessarie a chiarire un comportamento o una decisione;
- usare tabelle brevi e diagrammi leggibili;
- usare fence Mermaid validi, senza sostituirli con tilde quando il renderer si aspetta il fence Quarto.

Se una modifica non è adatta alle slide, non forzarne la riproduzione: sintetizzare la conseguenza operativa o il criterio decisionale.

## 14. Verifiche prima di concludere

Le verifiche devono essere proporzionate all'intervento e dichiarate con precisione.

### Controlli sui sorgenti

- verificare che i link interni e i riferimenti ai file siano validi;
- controllare la numerazione dei capitoli e la coerenza con `index.qmd`;
- verificare che i chunk Quarto abbiano triple backtick, opzioni corrette e label univoche;
- controllare la sintassi dei diagrammi Mermaid;
- cercare duplicazioni, termini incoerenti, placeholder non dichiarati e affermazioni tecniche non supportate.

### Rendering e pubblicazione

- per modifiche editoriali limitate, eseguire i controlli mirati pertinenti;
- per modifiche a chunk, diagrammi, navigazione o configurazione, eseguire il rendering Quarto appropriato;
- per modifiche a configurazione Quarto o GitHub Actions, verificare la build completa e il workflow di pubblicazione, quando gli strumenti disponibili lo consentono;
- distinguere chiaramente i controlli eseguiti da quelli non eseguiti; non dichiarare un render, test o deploy riuscito senza evidenza;
- non modificare il workflow solo per aggirare un errore senza comprenderne la causa.

Prima di concludere, fornire un riepilogo conciso di file modificati, decisioni rilevanti, verifiche eseguite e problemi residui. Non affermare che la pubblicazione sia avvenuta se è stato verificato soltanto il sorgente o il rendering locale.

## 15. Criterio di completamento

Un intervento è completo quando il contenuto è tecnicamente corretto, utile per una decisione o una presa in carico IT, coerente con il resto del corso, formattato correttamente e verificato al livello appropriato. Le modifiche strutturali restano soggette alla proposta motivata descritta nella sezione 3.
