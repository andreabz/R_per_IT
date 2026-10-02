# R per l'IT

**Capire, valutare e gestire soluzioni sviluppate in R**

Manuale tecnico pensato per chi, in ambito IT, deve comprendere richieste, valutare architetture, dimensionare risorse e governare soluzioni sviluppate in R senza dover diventare sviluppatore R.

## Obiettivo

Il corso fornisce un modello operativo per passare da una richiesta tecnica a una decisione IT motivata.

Il percorso segue questa sequenza:

**contesto → runtime → performance → architettura → deployment → governance → applicazione a casi concreti**

L'attenzione è rivolta soprattutto a:

- ambiente R, pacchetti e dipendenze;
- processi, thread, worker, parallelismo e memoria;
- misura e diagnosi delle performance;
- architetture R e integrazione con database e sistemi aziendali;
- VM, container, job, Shiny e API;
- build, test, artefatti, release e deployment;
- sicurezza, osservabilità, rollback e continuità operativa;
- responsabilità, evidenze, verifiche e governance;
- valutazione strutturata di richieste relative a soluzioni R.

Il corso distingue inoltre tre piani che non devono essere confusi:

1. **performance** — quanto costa eseguire il lavoro;
2. **software** — che cosa viene eseguito e come viene gestito;
3. **metodo** — se il metodo applicato è adeguato allo scopo secondo i requisiti pertinenti.

## Struttura

1. **Contesto e ambiente R** — componenti dell'ambiente software, pacchetti, dipendenze e riproducibilità.
2. **Runtime, processi e parallelismo** — modello di esecuzione e consumo delle risorse.
3. **Performance e diagnostica** — misura, profiling, benchmark, colli di bottiglia e scaling.
4. **Architettura e integrazione** — collocazione della soluzione e confini tra R e gli altri componenti.
5. **Deployment e gestione operativa** — dal codice all'artefatto, al rilascio e all'esercizio.
6. **Governance e responsabilità** — evidenze, ownership, verifiche, approvazioni e ricostruibilità.
7. **Caso finale e checklist** — scenari operativi e applicazione del metodo a un caso didattico.

## Pubblico

Il materiale è rivolto principalmente a:

- sistemisti e amministratori IT;
- architetti e responsabili di infrastruttura;
- team DevOps e piattaforme;
- IT governance e supporto applicativo;
- responsabili tecnici che devono valutare richieste relative a R.

Non è un corso introduttivo alla programmazione in R. Gli esempi di codice sono utilizzati per illustrare concetti utili alla valutazione tecnica.

## Principio guida

> **Prima di aumentare le risorse, capire perché servono.**

Una richiesta come «servono più CPU», «serve più RAM» o «serve un server dedicato» viene quindi trattata come una richiesta da verificare, non come una specifica infrastrutturale già definita.

L'approccio parte da requisito e workload, passa attraverso misure ed evidenze e arriva a una decisione architetturale, operativa e governata.

## Sito del corso

Il manuale è pubblicato come sito Quarto tramite GitHub Pages.

- Repository: https://github.com/andreabz/R_per_IT
- Sito: https://andreabz.github.io/R_per_IT/

## Tecnologia

Il materiale è scritto in Quarto e pubblicato automaticamente tramite GitHub Actions.

L'ambiente R del progetto è gestito con `renv`; il repository include il relativo lockfile per rendere riproducibile l'ambiente utilizzato dalla build.

## Stato del materiale

Il repository contiene la versione corrente del corso. Il contenuto è organizzato come manuale tecnico e viene mantenuto nel repository insieme alla configurazione necessaria per la pubblicazione.

## Licenza

Verificare il file di licenza del repository prima di riutilizzare o redistribuire il materiale.
