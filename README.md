# R per l'IT

**Capire, valutare e gestire soluzioni sviluppate in R**

Manuale tecnico per sistemisti, architetti, DevOps, team piattaforma e responsabili tecnici che devono comprendere, valutare, portare in esercizio e governare soluzioni sviluppate in R senza dover diventare sviluppatori R.

## Obiettivo

Il manuale insegna a riconoscere che cosa cambia quando il workload è R e a trasformare una richiesta tecnica in una specifica verificabile. L'obiettivo non è formare sviluppatori R, ma fornire a IT un modello per classificare una soluzione, valutarne ambiente e workload, definire il perimetro del deployment e gestirne l'esercizio.

Il percorso segue questa sequenza:

**contesto → runtime → performance → architettura → deployment → decisioni**

Il modello operativo è:

**requisito → evidenza → decisione → responsabilità → baseline**

L'attenzione è rivolta soprattutto a:

- ambiente R, package, library, repository, dipendenze e riproducibilità;
- processi, memoria, worker, thread, parallelismo e librerie native;
- misura, profiling, benchmark e diagnosi delle performance;
- architetture R e integrazione con database, filesystem, API e altri sistemi;
- diverse forme di soluzione: script personale, batch, report Quarto, Shiny, API plumber2, package e job in pipeline;
- build, test, artefatti, release e deployment;
- configurazione, sicurezza, logging, monitoring, rollback e continuità operativa;
- handover tra sviluppatore e IT;
- trasformazione delle evidenze in decisioni tecniche.

## Struttura

1. **Contesto e ambiente R** — che cosa compone una soluzione R, come sono organizzati runtime, package, library, repository e dipendenze.
2. **Runtime, memoria e parallelismo** — come R esegue il lavoro e come interpretare processi, worker, thread e memoria.
3. **Performance e diagnostica** — come misurare tempo, CPU, RAM, I/O, database, profiling e scaling.
4. **Architettura e integrazione** — dove collocare il calcolo e come presentare a IT i diversi tipi di soluzione R.
5. **Deployment e gestione operativa** — come trasformare codice e ambiente in una release riproducibile e gestibile.
6. **Decisioni operative** — come passare da requisito ed evidenza a decisione, baseline e ownership.


## Perché R può entrare nello stack IT

R non è un sostituto generale di Oracle, APEX, scheduler, web server o sistemi di storage. In una soluzione aziendale occupa normalmente **una parte dello stack**: quella in cui servono analisi statistiche, modellistica, simulazione, elaborazione dati o generazione di report analitici.

Un modo semplice per orientarsi è questo:

| Esigenza | Componente tipicamente coinvolto |
|---|---|
| Persistenza, integrità e query sui dati | Oracle |
| Applicazioni web gestionali e workflow vicino a Oracle | APEX |
| Scheduling e orchestrazione | piattaforma IT aziendale |
| Autenticazione, rete e TLS | infrastruttura aziendale |
| Analisi statistica, modellistica e simulazione | R |
| Report analitici riproducibili | Quarto + R |
| Interfacce analitiche interattive | Shiny + R |
| Servizi che espongono capacità analitiche | API + R |

Non è una classifica. Serve a chiarire **quale responsabilità viene aggiunta da R e quali componenti aziendali possono rimanere in carico allo stack esistente**.

Una domanda utile per IT è quindi:

> **Quale problema risolve R che non è già naturalmente coperto da un componente aziendale esistente?**

Se la risposta è chiara, diventa più semplice definire il confine della soluzione e non duplicare funzioni già disponibili.


## Come può presentarsi una soluzione R?

Il corso considera esplicitamente diversi modelli operativi:

| Soluzione | Domanda IT principale |
|---|---|
| Script personale | quale ambiente deve avere l'utente e quali dati può utilizzare? |
| Script batch | quando parte, quanto dura, quali risorse usa e come viene monitorato? |
| Report Quarto | come viene generato, con quale ambiente e dove viene pubblicato l'artefatto? |
| Applicazione Shiny | come vengono gestite sessioni, concorrenza, autenticazione e scaling? |
| API plumber2 | quale contratto espone, chi può chiamarla e quali sono timeout, limiti e monitoring? |
| Package R | quale API fornisce, quali dipendenze ha e come viene versionato e testato? |
| Job R in pipeline | quali sono input/output, dipendenze, retry, stato e responsabilità dello step? |

Una soluzione può combinare più modelli: per esempio un report Quarto generato da un job batch, oppure una Shiny che utilizza database e API.

## Principio guida

> **Prima di aumentare le risorse, capire perché servono.**

Una richiesta come «servono più CPU», «serve più RAM» o «serve un server dedicato» viene trattata come una richiesta da verificare, non come una specifica infrastrutturale già definita.

L'approccio parte da requisito e workload, passa attraverso misure ed evidenze e arriva a una decisione architetturale, operativa e governata.

## Handover sviluppatore → IT

Per portare una soluzione R in produzione devono essere espliciti almeno:

- applicazione, repository, commit/tag ed entrypoint;
- versione R, OS e dipendenze;
- package, lockfile e dipendenze native;
- modalità di esecuzione, workload, durata, frequenza e concorrenza;
- input, output, dimensioni e crescita dei dati;
- CPU, RAM, I/O, rete, worker e thread;
- database, API, filesystem, storage e altri sistemi esterni;
- configurazione, timeout, directory temporanee e variabili d'ambiente;
- autenticazione, autorizzazioni, segreti e TLS;
- test funzionali, integrazione, compatibilità e performance;
- deployment, smoke test, logging, monitoring, restart e rollback;
- ownership e responsabilità.

La regola è:

> **Lo sviluppatore fornisce una descrizione riproducibile del workload e delle evidenze; IT deve poter trasformare queste informazioni in una configurazione, un deployment e un esercizio verificabili.**

La checklist breve dell'appendice può essere usata già nella prima riunione: quando un'informazione manca, va registrata come informazione mancante e associata al responsabile o al test necessario per ottenerla.

## Kit operativo

Il manuale include un'appendice utilizzabile come traccia per l'handover sviluppatore → IT e per una prima verifica di production readiness. La scheda raccoglie identificazione, modello di esecuzione, ambiente R, dati, risorse, sicurezza, test, error handling, deployment, monitoring, aggiornamenti e ownership.

## Pubblicazione

Il manuale è scritto in Quarto e pubblicato tramite GitHub Actions su GitHub Pages.

- Repository: https://github.com/andreabz/R_per_IT
- Sito: https://andreabz.github.io/R_per_IT/

Il workflow di pubblicazione esegue il restore dell'ambiente renv, il render Quarto e il deploy dell'artefatto `_site` su GitHub Pages.

## Tecnologia

Il progetto usa Quarto per il manuale, R per gli esempi e il rendering dei contenuti, renv per la gestione riproducibile delle dipendenze R, GitHub Actions per build e pubblicazione e GitHub Pages per il sito.

## Stato del materiale

Il repository contiene la versione corrente del corso. Il materiale è organizzato come manuale tecnico per IT e viene mantenuto insieme alla configurazione necessaria alla pubblicazione.

## Licenza

Verificare il file di licenza del repository prima di riutilizzare o redistribuire il materiale.