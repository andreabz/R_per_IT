# Fase 0 — Ricognizione e mappatura del corso R_per_IT

- **Repository:** andreabz/R_per_IT
- **Branch esaminato:** main
- **Commit di riferimento:** 1b3b8760af15eaa55169509b8a8ab890f65ca04e
- **Data della ricognizione:** 29 ottobre 2026
- **Scopo:** audit diagnostico; nessun contenuto didattico corretto o riorganizzato durante questa fase.

## 1. Sintesi esecutiva

Il repository presenta una struttura didattica riconoscibile e coerente con il target IT: introduzione, sei capitoli in progressione, guida pratica, scheda di passaggio di consegne e slide. La copertura più solida riguarda riconoscimento dei prodotti R, runtime, memoria, processi/worker/thread, diagnosi delle performance, integrazione con Oracle e distinzione tra responsabilità applicative e infrastrutturali. Il caso integrato è presente sia nella guida pratica sia nelle slide.

La criticità didattica più netta è la **mancata trattazione esplicita di `testthat` e del suo ruolo nei controlli automatici**, benché sia richiesto dagli obiettivi di `AGENTS.md`. Test e gate di rilascio sono discussi in termini generali, ma manca una spiegazione mirata del ciclo di test di un package R e del significato operativo dei relativi risultati.

Sono inoltre da completare o verificare:
- la copertura concreta di orchestrazione con Docker Swarm/Kubernetes e dei componenti di osservabilità nominati in `AGENTS.md`;
- la verificabilità degli esempi: la configurazione globale Quarto disabilita l'esecuzione dei chunk e non esiste una suite di test del materiale;
- la separazione tra dipendenze necessarie a costruire il manuale e dipendenze necessarie a eseguire i laboratori;
- il rispetto puntuale della densità massima delle slide e la convenzione delle label per i diagrammi Mermaid;
- la licenza del materiale, perché nel tree esaminato non è presente un file di licenza.

### Valutazione sintetica

| Dimensione | Valutazione | Evidenza sintetica |
|---|---|---|
| Coerenza con lo scopo | Adeguata | Manuale e README dichiarano un target IT e privilegiano requisiti, evidenze e decisioni. |
| Utilità per il target | Adeguata con lacune | Schede operative, laboratori e caso integrato sono utilizzabili; manca il riferimento esplicito a `testthat`. |
| Progressione narrativa | Adeguata | Il percorso contesto → runtime → performance → architettura → deployment → decisioni è leggibile. |
| Accuratezza tecnica | Da verificare in alcuni punti | Il rendering del sito è riuscito, ma i chunk R non vengono eseguiti dal rendering globale. |
| Coerenza editoriale | Parziale | Le slide sono per lo più concise; l'agenda supera il limite di otto elementi e alcune formule-guida sono ripetute. |
| Riproducibilità degli esempi | Parziale | `renv.lock` supporta il build del manuale; non costituisce l'ambiente completo di tutti i laboratori e non c'è una suite di test. |

### Priorità complessive rilevate

| Priorità | Numero di interventi pianificati | Significato |
|---|---:|---|
| P0 | 0 | Non è emerso un blocco certo e immediato della pubblicazione. |
| P1 | 1 | Lacuna rispetto a un obiettivo didattico esplicito: test automatici con `testthat`. |
| P2 | 6 | Lacune di copertura, verificabilità, dipendenze dei laboratori, licenza e densità delle slide. |
| P3 | 5 | Rifiniture editoriali, label Mermaid e gestione locale degli artefatti di audit. |

Le priorità riguardano il piano proposto, non modifiche già eseguite. La fase 0 non ha modificato il materiale didattico.

## 2. Perimetro e metodo

### 2.1 Artefatti individuati

Il tree ricorsivo di GitHub per il commit di riferimento restituisce 20 file e le directory tecniche `.github/`, `.github/workflows/` e `renv/`. Non risultano directory sorgente R, cartelle dati, suite di test o progetti di esempio autonomi.

| Percorso | Funzione | Stato dell'ispezione |
|---|---|---|
| `AGENTS.md` | Obiettivi, vincoli tecnici/editoriali e processo di revisione | Letto integralmente; usato come riferimento normativo. |
| `README.md` | Presentazione del corso, struttura, pubblicazione e tecnologie | Letto integralmente. |
| `_quarto.yml` | Configurazione del libro, navigazione, appendici, output ed esecuzione | Letto integralmente. |
| `index.qmd` | Introduzione, obiettivi, lessico e metodo decisionale | Letto integralmente. |
| `01-contesto.qmd` | Ambiente R, package, repository e riproducibilità | Letto integralmente. |
| `02-runtime.qmd` | Memoria, garbage collection, processi, worker, thread e parallelismo | Letto integralmente. |
| `03-performance.qmd` | Misure, profiling, memoria, database e confronti | Letto integralmente. |
| `04-architettura.qmd` | Prodotti, architetture, Shiny, API e integrazioni | Letto integralmente. |
| `05-deployment.qmd` | Build, release, container, configurazione e gestione operativa | Letto integralmente. |
| `06-decisioni.qmd` | Casi decisionali, prove quantitative e gate di rilascio | Letto integralmente. |
| `strumenti-pratici.qmd` | Guida di diagnosi e laboratorio integrato | Letto integralmente. |
| `appendice-kit-operativo.qmd` | Scheda di handover e checklist operativa | Letto integralmente. |
| `slides.qmd` | Presentazione RevealJS | Letto integralmente e sottoposto a controllo statico della densità. |
| `styles.css` | Stili aggiuntivi del sito | Letto; file breve. |
| `.Rprofile` | Attivazione di `renv` | Letto; contiene il richiamo a `renv/activate.R`. |
| `.gitignore` | Esclusioni Git | Letto integralmente. |
| `renv/settings.json` | Impostazioni di `renv` | Letto integralmente. |
| `renv/.gitignore` | Esclusioni della directory di supporto | Letto integralmente. |
| `renv.lock` | Versione R e dipendenze dell'ambiente di build | Letto per metadati e inventario dei package; non è stata verificata singolarmente la compatibilità di ogni package. |
| `renv/activate.R` | Codice di attivazione generato da `renv` | Identificato e letto come artefatto di supporto; non sottoposto a revisione riga per riga, perché non contiene materiale didattico. |
| `.github/workflows/quarto-pages.yml` | Build Quarto e pubblicazione su GitHub Pages | Letto integralmente; confrontato con la configurazione del progetto e con lo stato del workflow. |

Il tree non contiene `docs/audit/ricognizione-corso.md` prima di questa fase. Non risultano file separati di dati o script per i laboratori, un `DESCRIPTION`, un `NAMESPACE`, un `Dockerfile`, file Compose, una cartella `tests/` o un file `LICENSE`. L'assenza di `DESCRIPTION` e `NAMESPACE` è coerente con un repository didattico e non un package R; l'assenza di test, dati e licenza ha invece le implicazioni indicate nella matrice.

### 2.2 Controlli eseguiti

- Lettura del contenuto dei sorgenti didattici e degli artefatti di configurazione elencati sopra.
- Ricostruzione della navigazione dichiarata in `_quarto.yml` e confronto con i file presenti.
- Controllo statico dei link relativi Markdown rilevati nei sorgenti Quarto: i tre riferimenti a file individuati puntano a file presenti.
- Controllo delle label dei chunk R: 31 chunk R, 31 label, nessun duplicato rilevato.
- Ricognizione dei fence Mermaid: i diagrammi usano il fence Quarto ````{mermaid}` e impostano `%%| echo: false`; le label esplicite non risultano presenti nei diagrammi.
- Controllo statico della densità delle slide: l'agenda contiene otto punti elenco e una frase aggiuntiva; la slide del gate di rilascio contiene un diagramma articolato e una frase esplicativa.
- Ricerca nei sorgenti del corso dei riferimenti a `testthat`, Docker Swarm, Kubernetes, Grafana e Redis.
- Lettura dei metadati di `renv.lock`: R 4.6.0, repository CRAN dichiarato e 30 package registrati.
- Verifica dello stato GitHub Actions: il run 227, associato al commit di riferimento, risulta completato con esito `success`. [Dettaglio del run](https://github.com/andreabz/R_per_IT/actions/runs/40865331953).

### 2.3 Limiti e controlli non eseguiti

- Non è stato eseguito un rendering locale indipendente: l'accesso disponibile in questa fase è al repository remoto.
- Non è stata eseguita l'esecuzione indipendente dei chunk R, né una validazione funzionale di ciascun esempio.
- Non sono state eseguite prove con Oracle, Shiny, API, container o sistemi aziendali reali.
- Non è stata verificata esternamente ogni affermazione dipendente dalla versione di package o piattaforme. I punti che richiedono documentazione ufficiale sono indicati nel piano.
- Il successo del workflow prova che la build e la pubblicazione configurate sono passate in quel run; non prova che tutti gli esempi didattici siano stati eseguiti, perché `_quarto.yml` imposta `execute.enabled: false`.

## 3. Mappa del corso e relazioni tra artefatti

### 3.1 Percorso attuale

1. **Introduzione — `index.qmd`:** target, obiettivi, lessico, metodo requisito → evidenza → decisione → responsabilità → situazione di riferimento.
2. **Contesto e ambiente — `01-contesto.qmd`:** R e RStudio, package/library/repository, dipendenze, `renv`, componenti nativi e riproducibilità.
3. **Runtime — `02-runtime.qmd`:** processi, worker, thread, memoria, garbage collection, serializzazione, BLAS/LAPACK e strategie di parallelismo.
4. **Performance — `03-performance.qmd`:** tempi, profiling, RSS, I/O, database, confronto di implementazioni e scaling.
5. **Architettura — `04-architettura.qmd`:** forme applicative, reference architecture, Shiny, API, pipeline, database e integrazioni.
6. **Deployment — `05-deployment.qmd`:** artefatti, Git, `renv`, container, test, segreti, GitHub Actions, logging, ripristino e passaggio di consegne.
7. **Decisioni — `06-decisioni.qmd`:** casi RAM/CPU/Shiny/database/package/container, prova quantitativa e gate di rilascio.
8. **Supporti operativi — `strumenti-pratici.qmd` e `appendice-kit-operativo.qmd`:** raccolta delle evidenze, laboratorio integrato e scheda compilabile.
9. **Presentazione — `slides.qmd`:** sintesi del percorso, dei criteri decisionali e del caso integrato.

### 3.2 Configurazione e pubblicazione

- `_quarto.yml` definisce un progetto Quarto di tipo libro, output `_site`, capitoli 1–6, introduzione e due appendici.
- Il rendering del libro include i file `*.qmd` e esclude esplicitamente `slides.qmd`.
- Il workflow `.github/workflows/quarto-pages.yml` ripristina l'ambiente `renv`, esegue `quarto render`, renderizza separatamente `slides.qmd` e copia `slides.html` e `slides_files` in `_site/presentazione/`.
- Il link di navigazione `presentazione/slides.html` è coerente con la destinazione creata dal workflow.
- `.Rprofile` attiva `renv`; `renv.lock` e la versione R dichiarata nel workflow sono entrambi impostati su 4.6.0.
- `.gitignore` esclude `docs/` oltre a output e artefatti generati. Il file di audit creato via GitHub sarà tracciato, ma nuove risorse create localmente sotto `docs/` potrebbero essere ignorate fino a un'eventuale gestione esplicita delle esclusioni.

### 3.3 Relazioni manuale–slide–supporti

Le slide seguono sostanzialmente il percorso del manuale e riprendono i suoi elementi principali: prodotti, runtime, misure, Oracle, Shiny, API, distribuzione e handover. Non sono una copia integrale del testo. I supporti operativi si collegano esplicitamente al capitolo 4 e fra loro; la scheda di handover è dichiarata come riferimento unico, mentre `strumenti-pratici.qmd` svolge funzione di guida al colloquio e alla diagnosi.

La coerenza generale è buona. Restano da verificare puntualmente gli aggiornamenti delle slide quando le fasi successive introdurranno o modificheranno contenuti, esempi, termini o diagrammi.

## 4. Matrice dei contenuti e degli interventi

**Legenda:** Adeguato = copertura sufficiente per il target; Parziale = presente ma incompleta; Assente = non trovato nei materiali; Fuori scopo = sproporzionato rispetto agli obiettivi; Da verificare = evidenze insufficienti. Le priorità si riferiscono agli interventi futuri.

| ID | Obiettivo / posizione | Contenuto attuale ed evidenza | Valutazione | Intervento proposto | Priorità | Dipendenze | Criterio di accettazione |
|---|---|---|---|---|---|---|---|
| COV-01 | Forme applicative — `index.qmd:65-80`; `04-architettura.qmd:67-162` | Script, batch, report Quarto, package, API, Shiny e pipeline sono classificati per responsabilità e verifiche IT. | Adeguato | Conservare; controllare coerenza dopo le revisioni. | — | Slide e README | Ogni forma ha scopo, punto di ingresso, dipendenze e criteri di presa in carico riconoscibili. |
| COV-02 | Runtime e ambiente — `01-contesto.qmd`; `02-runtime.qmd` | Package, library, repository, lockfile, componenti nativi, memoria, processi, worker e thread sono trattati. | Adeguato | Conservare; verificare gli esempi durante la revisione finale. | — | `renv.lock` | Distinzione tra ambiente R, librerie native, OS e sistemi esterni resta esplicita. |
| COV-03 | CPU, RAM e profiling — `03-performance.qmd:48-350` | Sono presenti misure, laboratori di tempi, memoria, profiling e confronto con Oracle; alcune prove sono escluse dal rendering. | Parziale sul piano della verifica | Integrare controlli riproducibili e istruzioni per raccogliere gli esiti senza richiedere programmazione ai partecipanti. | P2 | Ambiente dei laboratori, capitolo 2, appendice operativa | Ogni laboratorio dichiara input, ambiente, metodo, metriche, risultato atteso e limiti; il codice è verificato in un ambiente adeguato. |
| COV-04 | Test automatici e `testthat` — `AGENTS.md` §2 e §4; `05-deployment.qmd:190-236` | I test sono citati come gate generali; la ricerca nei sorgenti didattici non ha trovato riferimenti a `testthat` né una spiegazione del suo ruolo. Non esiste una cartella `tests/`. | Assente rispetto al requisito esplicito | Aggiungere una sezione breve orientata a IT: cosa verifica `testthat`, come leggere esito e report, confini tra test unitari, integrazione e performance, responsabilità dello sviluppatore. | **P1** | Capitoli 1 e 5; caso package; slide | Il partecipante sa chiedere e interpretare evidenze di test, distinguere un test superato dalla prontezza alla produzione e capire che cosa non copre il test. |
| COV-05 | Package R — `01-contesto.qmd:96-190`; `04-architettura.qmd:138-162` | Il package è descritto come unità riusabile e come fonte di dipendenze; sono meno espliciti il ciclo di versionamento, i controlli automatici e il passaggio da sorgente ad artefatto. | Parziale | Collegare package, test, versione, dipendenze e release con una scheda di evidenze, senza trasformare il corso in un tutorial di sviluppo. | P2 | COV-04, capitolo 5 | La scheda indica repository/versione, dipendenze, test richiesti, artefatto e compatibilità da verificare. |
| COV-06 | API client/server — `04-architettura.qmd:371-520` | Distinzione tra `plumber2` e `httr2`, contratto HTTP, errori, paginazione, timeout e retry. | Adeguato sul piano concettuale | Conservare; verificare gli esempi dipendenti dalla versione ufficiale. | — | Esempi API e configurazione target | È sempre chiaro quale componente espone il servizio e quale lo consuma; retry e idempotenza sono spiegati con limiti. |
| COV-07 | Shiny e ciclo di vita — `04-architettura.qmd:214-327`; `slides.qmd:193-225` | `app.R`, `ui.R`/`server.R`, `global.R`, `golem` e `Rhino`; sessioni, stato condiviso e concorrenza. | Adeguato, con verifica version-specific pendente | Conservare; validare struttura e avvio degli esempi sulle versioni dichiarate come riferimento. | P2 | Fonti ufficiali Shiny, golem e Rhino | I nomi e i punti di ingresso descritti corrispondono alla documentazione ufficiale della versione scelta; le differenze tra processo e sessione restano corrette. |
| COV-08 | Distribuzione e orchestrazione — `05-deployment.qmd:87-190` | Container e specifica ShinyProxy sono illustrati; Kubernetes è citato nelle slide, ma non è presente una trattazione concreta di Docker Swarm e il confronto tra orchestratori è limitato. | Parziale | Definire il livello minimo necessario per riconoscere quando serve un orchestratore e quali responsabilità restano a piattaforma e applicazione. | P2 | Architettura, deployment, requisiti aziendali | Il corso distingue esecuzione diretta, container e orchestrazione; non presenta Swarm/Kubernetes come requisiti universali e segnala le verifiche di compatibilità. |
| COV-09 | Osservabilità e componenti di piattaforma — `AGENTS.md` §4 e §9; `05-deployment.qmd:325-370` | Logging, metriche, alert e monitoraggio sono trattati in generale; Grafana e Redis non compaiono nei contenuti didattici. | Parziale rispetto all'elenco di scenari, ma non necessariamente lacuna obbligatoria | Valutare se un esempio breve di metriche/dashboard e cache condivisa risolve un bisogno didattico reale; in caso contrario documentare perché restano fuori dal percorso. | P3 | Scenari Shiny/API e piattaforma aziendale | La decisione su Grafana/Redis è motivata dal caso d'uso; nessuno strumento è presentato come componente universale. |
| COV-10 | Integrazioni aziendali — `04-architettura.qmd:535-678`; `03-performance.qmd:297-350` | Oracle, APEX, GIS, filesystem, API e scheduler sono usati per chiarire confini e trasferimento del calcolo. | Adeguato | Conservare; mantenere chiaro dove avviene il calcolo e chi gestisce ciascun confine. | — | Slide e caso integrato | Le responsabilità di R e dei sistemi esterni sono distinguibili in ogni scenario. |
| COV-11 | Git, `renv`, CI/CD e release — `05-deployment.qmd:55-87` e `253-282` | Git e lockfile sono spiegati; la pipeline reale pubblica il manuale Quarto tramite GitHub Actions. La CI/CD di un'applicazione R è descritta più come concetto che come pipeline verificabile. | Parziale | Esplicitare il ruolo e i limiti del workflow didattico rispetto a build/test/release di un'applicazione R. | P2 | COV-04, workflow di pubblicazione | Il partecipante distingue la CI del sito didattico dalla pipeline necessaria a testare e rilasciare un prodotto R. |
| COV-12 | Caso integrato — `strumenti-pratici.qmd:99-296`; `slides.qmd:332-341` | Caso batch su Oracle con raccolta delle evidenze, diagnosi, architettura e handover; il testo dichiara che non sono disponibili misure reali. | Adeguato | Conservare; non introdurre numeri presentati come misure reali. | — | Capitoli 1–6 | Il caso richiede di distinguere fatti, dati mancanti, ipotesi, test e decisioni, senza inventare misure. |
| TECH-01 | Esecuzione dei chunk — `_quarto.yml:80-86` | `execute.enabled: false` disabilita l'esecuzione dei chunk durante il rendering. Il workflow riuscito conferma il render, non la correttezza funzionale degli esempi. | Da verificare | Decidere un meccanismo separato per verificare gli esempi essenziali, senza eseguire carichi pesanti in ogni build. | P2 | COV-03, COV-04, dipendenze dei laboratori | Esiste un controllo documentato che esegue in ambiente controllato gli esempi selezionati e registra esito e prerequisiti; i laboratori costosi restano opt-in. |
| TECH-02 | Ambiente dei laboratori — `renv.lock`; `03-performance.qmd`; `04-architettura.qmd` | Il lockfile registra 30 package utili all'ambiente del manuale, tra cui knitr e profvis; non registra, tra gli altri, DBI, dplyr, data.table, Shiny, httr2, plumber2 o testthat. Alcuni esempi sono marcati `eval: false` e dichiarano prerequisiti. | Parziale, non errore del build | Distinguere esplicitamente l'ambiente di build del libro dagli ambienti necessari ai singoli laboratori; elencare i prerequisiti senza aggiungerli indiscriminatamente al lockfile del manuale. | P2 | TECH-01, capitoli 3–5 | Ogni laboratorio esterno al lockfile indica package, driver, accessi e configurazione richiesti; nessuno presume che il lockfile del libro basti a eseguirlo. |
| TECH-03 | Label Quarto/Mermaid — sorgenti Quarto | I 31 chunk R rilevati hanno label univoche; i diagrammi Mermaid non mostrano una label esplicita, pur usando il fence corretto e `echo: false`. | Parziale rispetto alla regola editoriale | Applicare una convenzione stabile anche ai diagrammi, se supportata dalla sintassi Quarto adottata. | P3 | `AGENTS.md` §13, revisione tecnica | Tutti i chunk per cui Quarto supporta label hanno una label descrittiva e univoca; il render resta valido. |
| TECH-04 | Densità slide agenda — `slides.qmd:48-59` | La slide contiene otto punti elenco più una frase esplicativa: nove elementi testuali, oltre il limite di otto. | Parziale | Eliminare o spostare la frase finale, oppure ridistribuire il contenuto. | P2 | `AGENTS.md` §14 | Nessuna slide supera otto elementi testuali, salvo eccezione visiva motivata e verificata nel render. |
| TECH-05 | Densità slide gate — `slides.qmd:345-359` | Diagramma con più passaggi e frase esplicativa finale. Il conteggio testuale automatico non è sufficiente per valutare l'ingombro visivo del diagramma. | Da verificare | Controllare la slide renderizzata e, se necessario, separare diagramma e nota. | P3 | Rendering RevealJS | Diagramma leggibile alla risoluzione prevista e testo di accompagnamento non compresso. |
| TECH-06 | Link e navigazione — `_quarto.yml`, `appendice-kit-operativo.qmd:12`, `strumenti-pratici.qmd:10` | I link relativi Markdown rilevati puntano a file presenti; i capitoli e le appendici dichiarati nella configurazione esistono. La destinazione delle slide è generata dal workflow. | Adeguato sul piano statico | Conservare; verificare i link nel sito pubblicato dopo le modifiche successive. | — | Workflow Pages | Tutti i collegamenti interni continuano a risolvere nel sito pubblicato, incluse le slide generate. |
| TECH-07 | Licenza — tree del repository; `README.md:135-137` | Il README invita a verificare il file di licenza, ma nel tree esaminato non è presente un file `LICENSE`. | Da chiarire | Stabilire la licenza del materiale e aggiungere il file appropriato solo dopo una decisione autorizzata. | P2 | Proprietà e riuso del materiale | La licenza è esplicita nel repository oppure il README dichiara chiaramente che non è stata assegnata; nessuna licenza viene inventata dall'agente. |
| TECH-08 | Ignorati Git — `.gitignore:9` | La regola `docs/` esclude la directory. Il file di audit creato via API sarà tracciato, ma nuovi file creati localmente sotto `docs/` possono essere ignorati. | Rischio operativo minore | Valutare in futuro un'eccezione mirata per gli artefatti di audit, senza cambiare il file in questa fase. | P3 | Gestione futura degli audit | Il comportamento di Git è documentato e non impedisce il versionamento intenzionale degli audit. |
| EDIT-01 | Stile e ripetizioni — `index.qmd:13-19`; `README.md:83-87`; `03-performance.qmd:541-568` | La formula guida sul dimensionamento è ripetuta in più artefatti; alcune frasi introduttive spiegano che il corso non è un corso di programmazione. La ripetizione ha una funzione di orientamento, ma va controllata rispetto al divieto di slogan. | Parziale | Conservare il criterio operativo, riducendo le ripetizioni non necessarie e privilegiando formulazioni informative. | P3 | `AGENTS.md` §11–12; slide | Il principio resta chiaro senza slogan ripetuti o formule retoriche; il contenuto utile non viene eliminato. |
| EDIT-02 | Convenzioni nel codice — `03-performance.qmd:374-410` | Alcuni nomi di funzione sono racchiusi tra backtick anche all'interno di chunk R, ad esempio ``data.frame``. È sintatticamente valido, ma la convenzione testuale non deve essere applicata meccanicamente al codice eseguibile. | Rifinitura | Verificare in revisione editoriale senza modificare il codice se non necessario. | P3 | `AGENTS.md` §11 e §13 | La regola dei backtick è applicata al testo discorsivo e non altera il codice eseguibile. |
| EDIT-03 | Ridondanza tra strumenti e appendice — `strumenti-pratici.qmd:6-22`; `appendice-kit-operativo.qmd:6-24` | La guida pratica rinvia alla scheda unica e dichiara di non essere una seconda scheda. Il confine è esplicito, ma va mantenuto durante la revisione. | Adeguato con controllo futuro | Conservare le funzioni distinte: guida alla diagnosi versus scheda compilabile. | — | Fasi 2–4 | I due artefatti non duplicano checklist complete e mantengono rimandi validi. |

## 5. Valutazione puntuale per capitolo

### Introduzione — `index.qmd`

**Punti di forza**
- Definisce chiaramente target e risultato operativo.
- Fornisce lessico minimo e una sequenza decisionale riutilizzabile.
- Spiega i confini tra R e componenti aziendali e rimanda al laboratorio integrato.

**Da mantenere sotto controllo**
- La formula guida sul dimensionamento ricorre anche in README e capitoli successivi. In fase editoriale valutare se serve ripeterla in tutti i punti.
- Gli obiettivi includono test e rilascio, ma non nominano `testthat`; la lacuna emerge confrontando il testo con `AGENTS.md`.

### Capitolo 1 — `01-contesto.qmd`

**Punti di forza**
- Distingue package, library, repository, file delle dipendenze e componenti esterni.
- Spiega che `renv.lock` non congela OS, librerie native, driver, credenziali o dati.
- Include diagnosi di package mancanti e un laboratorio di ricostruzione in ambiente di prova.

**Da verificare**
- Gli esempi di gestione delle dipendenze non sostituiscono un ambiente di test pulito che dimostri la ricostruzione end-to-end.
- Il contenuto è concettualmente adeguato per IT; non va esteso verso istruzioni di programmazione non necessarie.

### Capitolo 2 — `02-runtime.qmd`

**Punti di forza**
- Distingue processi, worker e thread nativi.
- Spiega copie, garbage collection, RSS, serializzazione e parallelismo.
- Il laboratorio di memoria dichiara input, metriche e limiti; le prove costose sono escluse dall'esecuzione automatica.

**Da verificare**
- Il confronto con worker deve essere eseguito separatamente e in condizioni controllate prima di essere usato come evidenza didattica.
- La verifica statica non dimostra il comportamento di memoria sul sistema operativo target.

### Capitolo 3 — `03-performance.qmd`

**Punti di forza**
- Distingue user, system ed elapsed e sottolinea la necessità di misure ripetute.
- Integra profiling, metriche del processo e tempi esterni.
- Il laboratorio Oracle confronta trasferimento completo e aggregazione lato database e indica i limiti del confronto.

**Da verificare**
- Gli esempi di confronto tra base R, `dplyr` e `data.table` non sono eseguiti dal build. I risultati vanno raccolti in un ambiente di prova e non presentati come universali.
- I prerequisiti dei laboratori database e profiling devono restare separati dal lockfile usato per pubblicare il libro.

### Capitolo 4 — `04-architettura.qmd`

**Punti di forza**
- È il capitolo più esteso e copre prodotti, responsabilità, reference architecture, Shiny, API, pipeline, database e container.
- La distinzione tra `plumber2` (server HTTP) e `httr2` (client HTTP) è esplicita.
- Il testo tratta retry, idempotenza, health check, stato condiviso e dipendenze esterne.

**Da verificare**
- Esempi ShinyProxy e API dichiarano dipendenze dalla versione. La correttezza delle proprietà di configurazione deve essere verificata sulle versioni target prima di considerarli quasi eseguibili.
- L'assenza di una trattazione concreta di Docker Swarm e la copertura limitata di Kubernetes vanno valutate in relazione agli scenari realmente utili al target.
- Non aggiungere Grafana o Redis solo per citarli: decidere sulla base di un caso didattico concreto.

### Capitolo 5 — `05-deployment.qmd`

**Punti di forza**
- Distingue sorgente, artefatto, ambiente e configurazione.
- Include container, gestione dei segreti, test, log, ripristino e handover.
- Rimanda alla documentazione ufficiale quando la configurazione dipende dalla versione.

**Da verificare**
- La pipeline GitHub Actions del repository pubblica il corso; non costituisce di per sé un esempio completo di CI/CD per un'applicazione R.
- I gate di test devono essere collegati a evidenze concrete, includendo il ruolo di `testthat` dove pertinente.

### Capitolo 6 — `06-decisioni.qmd`

**Punti di forza**
- I casi RAM, CPU, Shiny, database, package e container richiedono di distinguere misure e ipotesi.
- L'esercizio quantitativo esplicita il compromesso tra durata e RAM.
- La scheda decisionale e il gate di rilascio collegano diagnosi e responsabilità.

**Da verificare**
- Le tabelle numeriche dell'esercizio devono essere riconoscibili come dati didattici sintetici, non come benchmark trasferibili ad altre macchine.
- Il capitolo deve restare un luogo di sintesi, evitando di duplicare la scheda completa dell'appendice.

### Supporti operativi e slide

- `strumenti-pratici.qmd` offre una sequenza completa di raccolta, ricostruzione, diagnosi, architettura e decisione. Il testo specifica correttamente che non sono disponibili misure reali nel caso.
- `appendice-kit-operativo.qmd` contiene una scheda di handover articolata e utilizzabile. È il riferimento operativo da mantenere unico.
- `slides.qmd` segue il manuale e contiene sei diagrammi Mermaid. L'agenda supera il limite di otto elementi testuali; la slide del gate richiede un controllo visivo del diagramma e della nota.
- Le slide non sostituiscono i dettagli del manuale e non mostrano una contraddizione strutturale evidente con il percorso dei capitoli.

## 6. Copertura degli obiettivi di `AGENTS.md`

| Obiettivo | Stato | Evidenza / lacuna |
|---|---|---|
| Riconoscere prodotti e scegliere tra alternative | Adeguato | Introduzione, capitolo 4 e capitolo 6. |
| Comprendere runtime, ambiente e dipendenze | Adeguato | Capitoli 1 e 2; distinzione fra lockfile e sistema esterno. |
| Interpretare CPU, RAM, tempi e profiling | Adeguato sul piano concettuale; esecuzione da verificare | Capitoli 2 e 3; chunk non eseguiti dal render globale. |
| Distinguere processi, worker, thread e sessioni | Adeguato | Capitoli 2 e 4. |
| Valutare architetture, integrazioni e responsabilità | Adeguato | Capitolo 4 e caso integrato. |
| Distinguere script, package, client/server API e Shiny | Parziale | Script/API/Shiny coperti; ciclo package-test-release e `testthat` insufficienti. |
| Comprendere distribuzione, container, sicurezza, osservabilità ed esercizio | Parziale | Copertura generale buona; orchestrazione specifica e verifica degli esempi da completare. |
| Comprendere Git, `renv`, `testthat`, Docker e CI/CD | Parziale | Git, `renv`, Docker e workflow sono trattati; `testthat` è assente e la CI/CD applicativa è poco concreta. |
| Valutare test, riproducibilità, rilascio e gestione operativa | Parziale | Gate e checklist presenti; mancano evidenze di test automatici del materiale e un percorso esplicito su `testthat`. |
| Formulare domande tecniche e orientare verifiche | Adeguato | Checklist, casi e scheda di handover. |
| Script e batch con `Rscript` | Adeguato | Capitoli 1, 4, 5 e caso integrato. |
| Package R | Parziale | Concetto presente; ciclo di test/versionamento/release non abbastanza esplicito. |
| Client API `httr2` e server API `plumber2` | Adeguato sul piano concettuale | Capitolo 4 e slide; esempi da verificare sulle versioni target. |
| Shiny in `app.R` e file separati | Adeguato | Capitolo 4 e slide. |
| Shiny organizzata con `golem` | Parziale | Riconoscimento e struttura presenti; nessuna verifica di build eseguita. |
| Shiny in Docker e ShinyProxy | Parziale | Esempi presenti, ma compatibilità e configurazione da verificare per versione. |
| Docker Swarm/Kubernetes quando giustificati | Parziale | Kubernetes è citato; Docker Swarm non è trattato. |
| Proxy, autenticazione, metriche, Grafana, Redis | Parziale | Proxy, autenticazione e monitoraggio generico sono presenti; Grafana e Redis assenti. La loro inclusione dipende dal caso d'uso. |
| Oracle, APEX, GIS, scheduler e pipeline | Adeguato | Confini e responsabilità trattati nel capitolo 4 e nei laboratori. |
| Laboratori specifici di tempo, memoria, parallelismo e database | Adeguato come progetto didattico; esecuzione da verificare | I laboratori sono presenti, alcuni esclusi dal rendering automatico. |
| Caso integrato | Adeguato | `strumenti-pratici.qmd` e slide. |

## 7. Piano operativo per le fasi successive

L'ordine seguente rispetta le fasi definite in `AGENTS.md`. Le attività non sono state eseguite in questa ricognizione.

### Fase 1 — Rimozione del materiale fuori scopo

1. **EDIT-01 (P3):** verificare le ripetizioni della formula guida tra introduzione, README, capitolo 3 e slide. Conservare il criterio operativo, riducendo le ripetizioni puramente enfatiche.
2. **EDIT-03 (—):** mantenere distinta la guida di diagnosi dalla scheda di handover; eliminare solo eventuali duplicazioni individuate durante il confronto puntuale.

**Criterio di passaggio:** ogni rimozione è motivata e non riduce la copertura di obiettivi necessari; rimandi e slide restano coerenti.

### Fase 2 — Scrittura dei contenuti mancanti

1. **COV-04 (P1):** integrare il ruolo di `testthat` e dei test automatici per package e funzioni. Il livello deve restare rivolto a IT: lettura dell'esito, significato dei test, limiti e responsabilità.
2. **COV-05 (P2):** completare il collegamento tra package, test, versionamento e artefatto di release.
3. **COV-11 (P2):** chiarire la differenza tra il workflow che pubblica il manuale e una pipeline CI/CD applicativa.
4. **COV-08/COV-09 (P2/P3):** decidere se aggiungere un confronto sintetico tra container e orchestrazione e un esempio di osservabilità/cache. La decisione deve dipendere dagli scenari aziendali pertinenti, non dalla necessità di citare ogni tecnologia.

**Criterio di passaggio:** ogni lacuna prioritaria ha una collocazione coerente, un esempio o un'evidenza utile e nessuna duplicazione evitabile.

### Fase 3 — Riscrittura e riorganizzazione del materiale superstite

1. Collegare le evidenze di test e release ai casi decisionali del capitolo 6.
2. Verificare che il caso integrato usi gli stessi termini, le stesse responsabilità e gli stessi gate del manuale.
3. Rendere esplicite le dipendenze dei laboratori senza trasformare il lockfile del manuale nell'ambiente indiscriminato di ogni scenario.
4. Riesaminare gli esempi version-specific di ShinyProxy, API e container.

**Criterio di passaggio:** filo narrativo continuo, termini coerenti, requisiti e buone pratiche distinguibili, esempi con prerequisiti chiari.

### Fase 4 — Omogeneizzazione editoriale e didattica

1. **TECH-04 (P2):** portare la slide Agenda entro otto elementi testuali.
2. **TECH-05 (P3):** controllare visivamente la densità della slide Gate di rilascio.
3. **TECH-03 (P3):** aggiungere label descrittive ai diagrammi Mermaid se supportato dalla sintassi Quarto adottata.
4. **EDIT-01/EDIT-02 (P3):** uniformare stile e backtick senza alterare il codice eseguibile.
5. Verificare allineamento di README, introduzione, manuale, slide e appendice.

**Criterio di passaggio:** tutte le slide rispettano il limite o hanno eccezioni visive motivate; i diagrammi sono leggibili; terminologia e formattazione sono uniformi.

### Fase 5 — Revisione finale e valutazione dello scostamento

1. **TECH-01/TECH-02 (P2):** definire ed eseguire controlli riproducibili per gli esempi selezionati e per i laboratori con dipendenze esterne.
2. Verificare link interni, navigazione, label, fence, diagrammi e configurazione Quarto.
3. Eseguire il rendering completo del libro e della presentazione dopo le modifiche; consultare gli esiti del workflow.
4. **TECH-07 (P2):** risolvere la questione della licenza con una decisione autorizzata.
5. Valutare ogni obiettivo didattico, registrare scostamenti residui e distinguere controlli eseguiti da quelli non eseguibili.

**Criterio di passaggio:** report finale con punteggi motivati, evidenze, difetti residui e limiti; nessun controllo dichiarato senza riscontro.

## 8. Criteri di accettazione complessivi

La fase 0 può essere considerata conclusa perché:
- il tree del repository è stato ricostruito e i file didattici principali sono stati letti;
- gli obiettivi di `AGENTS.md` sono stati confrontati con i contenuti effettivi;
- le lacune principali hanno riferimenti e criteri di accettazione;
- le priorità sono motivate e ordinate per fase;
- sono registrati i controlli eseguiti e quelli non eseguiti;
- non sono stati modificati capitoli, slide, configurazioni o workflow.

Prima di iniziare la fase 1 è opportuno conservare questa matrice come riferimento e aggiornare le righe solo quando emergono nuove evidenze. Le questioni che richiedono una decisione organizzativa — in particolare licenza e livello di dettaglio per Grafana/Redis/orchestratori — non vanno risolte assumendo preferenze non dichiarate.

## 9. Questioni aperte

1. **Test:** quale forma di evidenza minima deve essere richiesta a uno sviluppatore R per test unitari, integrazione e performance? La proposta è introdurre `testthat` a livello concettuale e usare esempi di report, senza richiedere di scrivere test ai partecipanti.
2. **Ambienti dei laboratori:** si vuole mantenere un unico lockfile per il rendering oppure fornire specifiche separate per i laboratori con database, Shiny e API? La ricognizione raccomanda di non mescolare le dipendenze del sito con quelle di ogni esempio.
3. **Orchestrazione:** Docker Swarm e Kubernetes sono effettivamente scenari che i partecipanti devono saper riconoscere nel contesto aziendale? La profondità va decisa in base agli ambienti in uso.
4. **Osservabilità:** Grafana e Redis sono strumenti realmente usati o previsti nei casi aziendali del corso? Se non lo sono, è sufficiente descrivere i requisiti funzionali senza introdurre i prodotti.
5. **Licenza:** quale licenza è autorizzata per il materiale del corso?
6. **Configurazioni version-specific:** quali versioni di ShinyProxy e degli strumenti collegati devono essere prese come riferimento per verificare gli esempi?

## 10. Resoconto dei controlli

| Controllo | Esito |
|---|---|
| Tree ricorsivo del repository | Eseguito; 20 file e directory tecniche individuati. |
| Lettura dei sorgenti didattici | Eseguita per introduzione, sei capitoli, supporti operativi e slide. |
| Lettura configurazione Quarto/workflow | Eseguita. |
| Link relativi e riferimenti di navigazione | Controllo statico eseguito; nessun link relativo Markdown rotto rilevato tra quelli individuati. |
| Label dei chunk R | 31 rilevate, 31 univoche. |
| Label Mermaid | Non presenti nei diagrammi; registrato come rifinitura. |
| Densità slide | Controllo statico eseguito; agenda sopra il limite, slide gate da verificare visivamente. |
| Presenza di `testthat` | Ricerca eseguita; assente dai sorgenti didattici. |
| Stato workflow remoto | Run 227 sul commit di riferimento: completato con esito success. |
| Rendering locale indipendente | Non eseguito. |
| Esecuzione indipendente degli esempi R | Non eseguita. |
| Test con sistemi esterni o infrastruttura reale | Non eseguiti. |
| Modifiche ai contenuti didattici/configurazione/workflow | Nessuna. |

**Esito della fase 0:** mappa, matrice e piano sono stati predisposti. Non è stata avviata la fase 1.
