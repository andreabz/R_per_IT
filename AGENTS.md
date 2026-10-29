# AGENTS.md — Istruzioni per gli agenti di R_per_IT

## 1. Scopo del progetto

R_per_IT è un corso per colleghi IT che devono comprendere le soluzioni realizzabili con R, valutarne i requisiti, confrontare architetture e collaborare con gli sviluppatori nelle scelte tecniche, nella diagnosi e nel rilascio.

Il corso non deve insegnare ai partecipanti a programmare in R. Il codice va mostrato quando serve a spiegare un comportamento, rendere concreto un esempio o produrre misure da interpretare. Gli esercizi devono concentrarsi su requisiti, architetture, evidenze, diagnosi e decisioni.

Il principio guida è capire quali prodotti si possono realizzare, come funzionano e quali condizioni richiedono.

R è un componente dello stack aziendale. Il materiale deve chiarire i confini tra R, database, scheduler, web server, sistemi di identità, storage, gateway e piattaforme di orchestrazione. Valutare il riuso dei componenti aziendali quando è appropriato.

## 2. Destinatari e risultato atteso

Al termine del corso i partecipanti devono saper:

- riconoscere i principali prodotti costruibili con R e i rispettivi modelli di esecuzione;
- individuare requisiti, dipendenze, risorse, sistemi esterni e responsabilità;
- comprendere a grandi linee il runtime R e l'uso di CPU e RAM;
- leggere misure e risultati di profiling, distinguendo osservazioni, ipotesi e conclusioni;
- orientare gli sviluppatori verso verifiche e alternative architetturali appropriate;
- comprendere il ruolo e i limiti di Git, `renv`, `testthat`, Docker e CI/CD;
- valutare le evidenze necessarie per test, rilascio, riproducibilità e gestione operativa.

Il livello tecnico deve essere approfondito sul piano concettuale, architetturale e diagnostico. I partecipanti non devono imparare a scrivere codice. Possono leggere esempi brevi, configurazioni, log, grafici e report già prodotti per comprenderne il significato e formulare decisioni.

## 3. Metodo di lavoro sugli artefatti esistenti

Prima di aggiungere contenuti:

1. leggere il file e i materiali collegati;
2. cercare sovrapposizioni, contraddizioni e contenuti da correggere o approfondire;
3. decidere se mantenere, riscrivere, spostare in appendice o eliminare;
4. mantenere coerenti manuale, indice, slide, esempi e configurazione di pubblicazione.

Riutilizzare il materiale valido. Evitare spiegazioni duplicate, capitoli aggiunti soltanto per elencare tecnologie e dettagli che non aiutano a capire un prodotto, valutarne i requisiti o interpretare evidenze.

La direzione didattica definita in questo file autorizza la riorganizzazione dei capitoli per allineare il corso agli obiettivi indicati. Le modifiche strutturali devono essere applicate con coerenza a indice, link, slide e pubblicazione.

Le modifiche a workflow GitHub Actions, destinazioni o impostazioni di pubblicazione devono essere motivate e verificate. Non modificarle per comodità.

## 4. Prodotti e architetture da coprire

Organizzare il corso a partire dai prodotti realizzabili con R e dai criteri per scegliere tra essi. Gli scenari sono una struttura di confronto, non una scala obbligatoria di maturità.

Copertura minima:

- script R personale o condiviso ed esecuzione batch con `Rscript`;
- package R per funzioni riusabili;
- client API con `httr2`;
- server API con `plumber2`;
- Shiny locale in `app.R`;
- Shiny separata in `ui.R`, `server.R` e, quando presente, `global.R`;
- Shiny strutturata come package con `golem`;
- Shiny distribuita in Docker e gestita da ShinyProxy;
- architetture con Docker Swarm o Kubernetes quando giustificate dai requisiti;
- architetture con proxy/web server, autenticazione, metriche, Grafana e servizi esterni come Redis quando utili allo scenario;
- pipeline analitiche e integrazioni con database, storage, scheduler, APEX, GIS e altri sistemi aziendali.

Per ogni prodotto descrivere scopo, punto di ingresso, modello di esecuzione, utenti o sistemi chiamanti, dipendenze, risorse, sicurezza, test, distribuzione, monitoraggio e limiti. Spiegare quando è appropriato e quali alternative valutare.

Distinguere esplicitamente:
- package riusabile e applicazione che lo utilizza;
- client API che invia richieste e server API che le riceve;
- struttura del codice e architettura di distribuzione;
- esecuzione locale, batch, servizio persistente e applicazione interattiva;
- stato specifico di una sessione Shiny, oggetti condivisi nel processo e stato esterno condiviso.

Non presentare `golem`, Docker, ShinyProxy, Kubernetes, Grafana o Redis come requisiti universali. Risolvono problemi diversi e vanno introdotti in base allo scenario.

## 5. Scheda operativa per ogni scenario

Quando pertinente, descrivere ogni scenario con una struttura uniforme. Non forzare sezioni irrilevanti: dichiarare invece perché un requisito non si applica.

1. **Prodotto e scopo:** che cosa fa e quale responsabilità ricade su R.
2. **Struttura e il punto di ingresso:** file principali, punto di avvio e artefatto distribuito.
3. **Esecuzione:** IDE, console, Rscript, scheduler, server, processo persistente o orchestratore.
4. **Ambiente:** versione R di riferimento quando nota, package, repository, dipendenze native, driver e file che registra le dipendenze.
5. **Input, output e dati:** formati, volumi, provenienza, persistenza, sensibilità e confini di responsabilità.
6. **carico di lavoro e risorse:** durata, frequenza, CPU, RAM, I/O, rete, concorrenza e variabilità.
7. **Verifiche:** test funzionali, d'integrazione, compatibilità e performance.
8. **Distribuzione:** build, artefatto, configurazione, promozione, rollback e dipendenze esterne.
9. **Sicurezza:** account, privilegi minimi, autenticazione, autorizzazione, segreti, TLS e dati esposti.
10. **Esercizio:** log, errori, exit code o codici HTTP, timeout, nuovo tentativo automatico, health check, monitoraggio e allarmi.
11. **passaggio di consegne e responsabilità operativa:** informazioni da consegnare, responsabilità dello sviluppatore e di IT, runbook e situazione di riferimento.

Distinguere sempre:
- **necessario:** requisito senza il quale lo scenario non è gestibile o non soddisfa il contratto;
- **condizionale:** necessario solo in presenza di uno specifico rischio o requisito;
- **buona pratica:** raccomandazione motivata, non requisito universale.

Non dichiarare un'applicazione pronta per la produzione soltanto perché si avvia o supera un test funzionale.

## 6. Runtime, memoria, parallelismo e performance

Spiegare il comportamento rilevante per IT senza promettere risultati universali. Distinguere processo R, worker, thread nativi, memoria logica degli oggetti e memoria osservata dal sistema operativo.

### Laboratori richiesti

Preparare **sia un caso integrato sia laboratori specifici**:

- **Caso integrato:** un carico di lavoro sintetico ma plausibile, con input e output definiti, usato per confrontare strategie di esecuzione e interpretare compromessi.
- **analisi dei tempi di esecuzione:** usare, dove appropriato, `system.time()`, `Rprof()`, `profvis` e metriche del sistema operativo; distinguere tempo CPU, tempo trascorso, I/O e attese esterne.
- **Memoria:** analizzare copie e oggetti intermedi, selezione di colonne, elaborazione per blocchi e picco di RSS; non dedurre il consumo di RAM dalla sola dimensione logica degli oggetti R.
- **Parallelismo:** confrontare esecuzione sequenziale e numero ragionevole di worker (per esempio 2, 4 e 8 quando sensato); misurare durata, speedup, efficienza, RAM, serializzazione e saturazione. Distinguere processi R e thread di librerie native/BLAS.
- **Database:** confrontare, su dati equivalenti, trasferimento completo e filtraggio/aggregazione lato database; registrare righe, colonne, volume trasferito e tempi lato database e lato R.

Ogni prova comparativa deve dichiarare ambiente, versione quando rilevante, input, metodo, metrica, strategie confrontate e limiti di generalizzazione. Evitare confronti non riproducibili o numeri presentati come universali.

Non assumere che parallelizzare migliori le prestazioni: può aumentare RAM, overhead, serializzazione e carico sui database, oppure peggiorare la contesa per le risorse. Gli esercizi devono chiedere ai partecipanti di interpretare i risultati e proporre la verifica successiva; non devono richiedere loro di modificare il codice.

## 7. `Shiny`: riconoscimento, ciclo di vita e gestione

Trattare `Shiny` come prodotto applicativo e carico di lavoro concorrente, non soltanto come codice R.

### Strutture da riconoscere

- **app.R:** file singolo che può contenere interfaccia, logica server e inizializzazione.
- **ui.R e server.R:** struttura separata; individuare anche eventuale global.R e gli altri file richiamati.
- **global.R:** viene eseguito all'avvio dell'applicazione prima delle sessioni; oggetti e dati creati qui possono restare in memoria ed essere condivisi tra le sessioni servite dallo stesso processo.
- **Struttura di package o framework:** per esempio `golem`, `Rhino` o convenzioni personalizzate; individuare punto di ingresso, moduli, risorse, configurazione, dipendenze e procedura di avvio/build.

Non presentare queste strutture come modelli di esecuzione necessariamente diversi. Il comportamento va dedotto dal codice e dal modo in cui l'applicazione viene avviata.

### Ciclo di vita e risorse

Spiegare la differenza tra avvio del processo, creazione della sessione e oggetti condivisi. Distinguere stato reattivo e oggetti specifici della sessione da dati o cache condivisi. Un oggetto globale mutabile può causare interferenze tra utenti; una cache in memoria di un processo non è automaticamente condivisa fra processi o container.

Prevedere un esempio che confronti il caricamento di un dataset nell'ambito globale con il caricamento per sessione, mostrando implicazioni su tempi, RAM, isolamento e aggiornamento dei dati. Non sostenere che ogni oggetto venga caricato nuovamente per ogni sessione.

Approfondire input/output/reactive expressions, invalidazione, caching, sessioni simultanee, diagnosi con uno e più utenti, operazioni bloccanti e comportamento al riavvio.

### distribuzione

Confrontare, quando pertinente, esecuzione diretta su host, container e ShinyProxy; citare ShinyProxy Operator con orchestratori Docker, Docker Swarm o Kubernetes se utile allo scenario. Fornire configurazioni e comandi **quasi eseguibili**, sufficientemente completi da mostrare i confini tra componenti e il percorso di avvio, ma adattabili all'infrastruttura aziendale.

Per ogni esempio:
- indicare prerequisiti e assunzioni;
- marcare chiaramente valori, host, percorsi, porte, immagini e segreti da sostituire;
- non inserire credenziali reali né suggerire segreti nel repository;
- distinguere TLS termination, autenticazione, autorizzazione, isolamento, gestione dei segreti e osservabilità;
- non presentare configurazioni illustrative come approvate o pronte per la produzione senza aver verificato compatibilità e requisiti.

## 8. API: `plumber2` e consumo HTTP con `httr2`

Distinguere esplicitamente i due ruoli: **`plumber2` espone servizi HTTP da R; `httr2` consuma servizi HTTP da R**.

### API esposte

Aiutare a riconoscere:
- script o router con endpoint e punto di avvio;
- API suddivisa in più router/file e logica applicativa;
- API la cui logica è organizzata in un package R;
- servizio eseguito direttamente, in container o dietro proxy/gateway.

Descrivere il contratto HTTP: metodi, percorsi, parametri, body, header, formati, codici di stato e struttura degli errori. Trattare validazione input, richieste simultanee, operazioni bloccanti, connessioni ai sistemi esterni, timeout, limiti di richiesta, log, health check, versionamento, autenticazione e autorizzazione.

Distinguere una verifica di liveness dalla verifica della disponibilità delle dipendenze necessarie. Non assumere che un'API sia automaticamente asincrona, scalabile o sicura.

### API consumate con `httr2`

Includere almeno un esempio riproducibile di richiesta e gestione della risposta. Coprire GET/POST, URL, query parameters, header, body, parsing JSON, codici HTTP, timeout, errori, autenticazione, nuovo tentativo automatico limitati e paginazione quando pertinente.

Evidenziare che i nuovi tentativi automatici devono essere compatibili con l'operazione e con i codici di errore: non ripetere indiscriminatamente operazioni non idempotenti. Non inserire token o credenziali nel codice sorgente o nei log.

Collegare chiamante e servizio con un esempio HTTP/JSON che chiarisca il contratto tra componenti, la responsabilità degli errori e i confini di sicurezza.

## 9. Integrazioni con lo stack aziendale

Trattare le integrazioni dal punto di vista dei confini e dei contratti, non come corsi completi sui sistemi esterni.

- **Oracle:** driver, autenticazione, query, transazioni, `pool` quando pertinente, volumi, esecuzione dei filtri e delle aggregazioni nel database di filtri e aggregazioni, timeout e gestione delle connessioni.
- **APEX:** confine tra workflow gestionale e calcolo analitico; invocazione di servizi, scambio di parametri e risultati, gestione degli errori.
- **GIS:** dati spaziali, formati, database geografici, sistemi di coordinate e trasferimento dei dati.
- **Scheduler e orchestratori:** account, ambiente, working directory, exit code, log, timeout, nuovo tentativo automatico, dipendenze e idempotenza.
- **Proxy e gateway:** routing, TLS, autenticazione, limiti, timeout e logging.
- **CI/CD e container:** test, build, artefatto, configurazione, promozione e rollback.

Non duplicare automaticamente in R funzioni già svolte in modo adeguato da database, scheduler, gateway o piattaforma aziendale. Dichiarare sempre dove viene eseguito il calcolo e quale componente è responsabile di ogni funzione.

## 10. Versioni e documentazione tecnica

Il manuale descrive le tecnologie in termini generali e **non impone una versione di riferimento fissa**.

Quando una procedura, una configurazione o un comportamento dipende dalla versione:
- indicare esplicitamente la dipendenza;
- distinguere comportamento generale e dettaglio version-specific;
- verificare la documentazione ufficiale pertinente prima di affermare che un comando o una configurazione siano validi;
- evitare di inventare opzioni, direttive, nomi di immagini, API o compatibilità;
- non dichiarare una configurazione compatibile con una versione non verificata.

Gli esempi di distribuzione devono essere quasi eseguibili, con comandi e configurazioni concreti, ma devono indicare prerequisiti, variabili da sostituire e punti da verificare sull'ambiente target. La concretezza non equivale a una garanzia di produzione.

## 11. Stile, linguaggio e filo narrativo

Scrivere in italiano tecnico, sobrio e diretto. Il testo deve essere preciso, comprensibile e piacevole da leggere, senza enfasi artificiale.

- Preferire frasi brevi e verbi concreti.
- Eliminare retorica, slogan, frasi motivazionali, tono promozionale e gergo manageriale.
- Evitare formule antitetiche come «non è X, è Y», «non si tratta di X, ma di Y» e varianti usate per creare enfasi. Scrivere direttamente la definizione o la differenza rilevante.
- Evitare aperture generiche, introduzioni che ripetono il titolo, conclusioni rituali e frasi che non aggiungono informazioni.
- Non usare domande retoriche come espediente narrativo. Usare domande dirette quando introducono un controllo concreto.
- Evitare superlativi, promesse non dimostrate, metafore decorative e formule da comunicazione social.
- Preferire parole italiane comuni quando sono precise. Mantenere inalterati i nomi ufficiali di funzioni, package, file, opzioni e tecnologie.
- Definire le sigle al primo uso quando non sono ovvie per il pubblico, per esempio API, HTTP, CPU, RAM, RSS, TLS, CI/CD e BLAS.
- Distinguere fatti, ipotesi, esempi, raccomandazioni e requisiti obbligatori.
- Non presentare una buona pratica come obbligo universale.
- Evitare ripetizioni tra capitoli. Richiamare con un collegamento un concetto già spiegato.
- Usare tabelle per confronti reali e liste quando migliorano la leggibilità.
- Ogni paragrafo deve aggiungere una definizione, una spiegazione, un'evidenza, un esempio o una conseguenza operativa.

### Nomi di funzioni e package R

Nel testo discorsivo, racchiudere tra singoli backtick Markdown ogni nome di funzione R e ogni nome di package R citato, anche in frasi, tabelle e titoli. Esempi: `system.time()`, `renv::restore()`, `data.table` e `testthat`. Non applicare la regola al codice nei chunk o nei blocchi di codice; non modificare il codice eseguibile.

## 12. Standard editoriali

- Scrivere in italiano tecnico, preciso e diretto.
- Preferire esempi concreti, tabelle comparative e diagrammi utili a capire una scelta.
- Evitare slogan, frasi motivazionali, retorica, ripetizioni e affermazioni generiche non verificabili.
- Non introdurre codice solo per decorazione: spiegare quale comportamento chiarisce o quale evidenza produce.
- Definire i termini tecnici al primo uso quando possono essere nuovi per il destinatario.
- Separare fatti, assunzioni, esempi e raccomandazioni.
- Mantenere nomenclatura e significato dei termini coerenti tra capitoli e slide.
- Usare Mermaid quando chiarisce flussi, confini o decisioni; i diagrammi devono essere validi e leggibili.

## 13. Standard Quarto e codice

- Per i chunk eseguibili Quarto usare fence con **tre backtick** e opzioni nel formato Quarto corretto.
- Ogni chunk deve avere una label esplicita e univoca, ad esempio `#| label: prova comparativa-rss`.
- Le label devono essere stabili, descrittive e non duplicate nell'intero progetto.
- Per i diagrammi Mermaid usare il fence Quarto corretto, usando un fence composto da tre backtick seguito da `{mermaid}`, e `%%| echo: false` quando il codice sorgente del diagramma non deve apparire nel documento renderizzato.
- Non racchiudere codice destinato a essere eseguito da Quarto in fence alternativi che ne impediscano l'esecuzione. I fence Markdown per codice mostrato come testo sono ammessi quando intenzionali.
- Non lasciare chunk incompleti, label provvisorie, link rotti, riferimenti a file inesistenti o output che contraddicono il testo.
- Rendere gli esempi riproducibili quando ragionevole; documentare input, dipendenze e limiti quando non possono esserlo integralmente.
- Evitare di aggiungere dipendenze R non necessarie agli esempi.

## 14. Standard per le slide

Il manuale è la fonte autorevole per spiegazioni, esempi, configurazioni, confronti e caveat. Le slide sintetizzano lo stesso percorso decisionale senza copiare il manuale integralmente.

Ogni modifica tecnica pertinente al manuale va valutata anche per le slide, mantenendo coerenti scenari, termini, definizioni, diagrammi e conclusioni.

- Massimo otto righe di testo o elementi per slide, salvo strutture visive chiaramente leggibili.
- Usare frasi brevi, tecniche e dirette. Evitare retorica, formule antitetiche e frasi motivazionali.
- Limitare il codice alle righe necessarie a chiarire un comportamento.
- Usare tabelle brevi e diagrammi leggibili.
- Usare fence Mermaid validi e verificare che i diagrammi vengano renderizzati.
- Se il contenuto è troppo denso, dividerlo in più slide o spostare i dettagli nel manuale.
- Non forzare nelle slide dettagli che si comprendono meglio nel manuale; sintetizzare il criterio decisionale.

## 15. Verifiche prima di concludere

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

## 16. Criterio di completamento

Un intervento è completo quando il contenuto è tecnicamente corretto, utile per una decisione o una presa in carico IT, coerente con il resto del corso, formattato correttamente e verificato al livello appropriato. Le modifiche strutturali restano soggette alla proposta motivata descritta nella sezione 3.

## 17. Processo di revisione complessiva del corso

Quando viene richiesta una revisione complessiva del materiale, procedere per fasi distinte e verificabili. Non anticipare le modifiche di una fase successiva e non considerare conclusa una fase se i relativi criteri di accettazione non sono soddisfatti.

### Fase 0 — Ricognizione e mappatura

- Inventariare i file pertinenti al corso: sorgenti Quarto, indice, slide, appendici, configurazione, risorse, esempi, test e workflow di build/pubblicazione.
- Ricostruire la struttura effettiva del corso e individuare capitoli, sezioni, esempi, diagrammi e dipendenze tra artefatti.
- Mappare ogni contenuto rilevante agli obiettivi didattici della sezione 2 e alla copertura richiesta nelle sezioni 4–9.
- Classificare i contenuti come adeguati, parziali, assenti, duplicati, fuori scopo, incoerenti o tecnicamente da verificare.
- Registrare lacune, ripetizioni, problemi di progressione, affermazioni da verificare, link e riferimenti sospetti, dipendenze e impatti sulle slide o sulla pubblicazione.
- Produrre una matrice dei contenuti con almeno: obiettivo didattico, posizione nel repository, contenuto esistente, valutazione, intervento proposto, priorità, dipendenze e criterio di accettazione.
- Produrre un piano ordinato di intervento e indicare quali evidenze servono per risolvere le incertezze.

**Vincoli:** questa fase è diagnostica. Non eliminare, riscrivere, spostare o aggiungere contenuti didattici. È consentito creare o aggiornare soltanto gli artefatti di audit espressamente richiesti. Non formulare conclusioni come certe quando derivano da un'ispezione parziale: indicare i limiti e le verifiche mancanti.

**Criteri di accettazione:** inventario del perimetro verificato; mappa contenuti-obiettivi; lacune e duplicazioni documentate con riferimenti puntuali; priorità motivate; piano d'azione con criteri verificabili; incertezze esplicite.

### Fase 1 — Rimozione del materiale fuori scopo

- Applicare la mappa approvata per identificare contenuti da eliminare, ridurre o spostare.
- Rimuovere retorica, slogan, motivazioni generiche, ripetizioni e approfondimenti che non aiutano il target a riconoscere prodotti R, valutare requisiti, confrontare architetture o interpretare evidenze.
- Non eliminare un dettaglio tecnico solo perché specialistico: valutarne prima l'utilità per una decisione, una diagnosi o la gestione operativa.
- Se un contenuto è fuori posto ma potenzialmente utile, proporre una destinazione coerente prima di eliminarlo.
- Aggiornare indice, collegamenti e slide interessati.

**Criteri di accettazione:** ogni rimozione è motivata e tracciabile; nessun obiettivo didattico perde contenuti necessari senza una sostituzione pianificata; riferimenti e navigazione restano coerenti.

### Fase 2 — Scrittura dei contenuti mancanti

- Colmare le lacune prioritarie individuate nella mappa, nei capitoli o nelle sezioni più appropriate.
- Dare precedenza agli obiettivi fondamentali assenti o trattati solo superficialmente, senza creare capitoli isolati che duplicano materiale esistente.
- Per ogni nuovo contenuto, definire scopo, livello di dettaglio, prerequisiti, legami con altri capitoli ed evidenze o esempi necessari.
- Verificare le affermazioni dipendenti da versioni e documentazione tecnica secondo la sezione 10.
- Aggiornare manuale, indice, slide e artefatti correlati quando necessario.

**Criteri di accettazione:** ogni lacuna prioritaria affrontata; contenuti collocati nella progressione didattica; esempi e affermazioni verificabili; nessuna duplicazione evitabile; artefatti correlati coerenti.

### Fase 3 — Riscrittura e riorganizzazione del materiale superstite

- Integrare i contenuti validi preesistenti con quelli aggiunti nella fase 2.
- Riordinare capitoli e sezioni per sostenere una progressione chiara: prodotti e criteri di scelta, runtime e ambiente, performance e diagnosi, architetture e integrazioni, distribuzione ed esercizio, riproducibilità e rilascio, caso integrato.
- Riscrivere i passaggi ambigui, frammentari o ridondanti; preservare i dettagli utili e le evidenze tecniche valide.
- Distinguere esplicitamente requisiti, opzioni condizionali, buone pratiche, assunzioni ed esempi.
- Aggiornare navigazione, rimandi, slide e configurazione solo quando necessario e motivato.

**Criteri di accettazione:** filo narrativo continuo; responsabilità e confini architetturali chiari; transizioni comprensibili; contenuti collocati una sola volta salvo richiami utili; coerenza con gli obiettivi del corso.

### Fase 4 — Omogeneizzazione editoriale e didattica

- Uniformare terminologia, stile, livello di dettaglio, struttura degli esempi, titoli, tabelle, diagrammi e convenzioni di formattazione.
- Applicare la regola dei backtick ai nomi di funzioni e package R nel testo discorsivo.
- Verificare che le slide sintetizzino il manuale, rispettino il limite indicato nella sezione 14 e non introducano affermazioni discordanti.
- Controllare consistenza di definizioni, sigle, nomi di file, prodotti e convenzioni tra tutti gli artefatti.

**Criteri di accettazione:** stile uniforme e conforme alle sezioni 11–14; terminologia coerente; slide allineate al manuale e leggibili; assenza di violazioni editoriali note.

### Fase 5 — Revisione finale e valutazione dello scostamento

- Eseguire controlli tecnici, editoriali, didattici e di navigazione sull'intero perimetro modificato e sui relativi artefatti dipendenti.
- Verificare rendering Quarto, diagrammi, chunk, link, codice e configurazione di pubblicazione in misura proporzionata alle modifiche e agli strumenti disponibili.
- Valutare separatamente, con punteggio motivato e riscontri puntuali: coerenza con lo scopo, utilità per il target, leggibilità e chiarezza, progressione narrativa, accuratezza tecnica e completezza della copertura.
- Per ogni obiettivo didattico indicare copertura raggiunta, evidenze, scostamenti residui e gravità.
- Separare difetti bloccanti, miglioramenti raccomandati e aspetti non verificati. Non dichiarare completata una verifica che non è stata eseguita.

**Criteri di accettazione:** report finale esaustivo; valutazioni motivate da evidenze; problemi residui e limiti dichiarati; controlli realmente eseguiti elencati; nessun difetto bloccante noto lasciato senza motivazione o piano d'azione.

### Regole trasversali per tutte le fasi

- Leggere queste istruzioni e gli artefatti pertinenti prima di intervenire.
- Usare la matrice di ricognizione come riferimento comune e aggiornarla quando emergono nuove evidenze.
- Ordinare gli interventi per priorità: prima correttezza e lacune bloccanti, poi copertura degli obiettivi, struttura e chiarezza, infine uniformità e rifiniture.
- Al termine di ogni fase, riesaminare gli artefatti interessati, individuare eventuali nuovi problemi introdotti e correggerli prima di passare oltre.
- Mantenere una traccia di decisioni, file modificati, verifiche e problemi residui.
- Non inventare esiti di test, rendering, build o deploy. Distinguere sempre fra eseguito, non eseguibile e non ancora verificato.
- Se una modifica richiede una decisione non determinabile dalle istruzioni o dalle evidenze, documentare l'opzione consigliata e la motivazione invece di nascondere l'incertezza.

