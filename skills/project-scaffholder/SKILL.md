---
name: project-scaffolder
description: >
  Usa questa skill quando l’utente descrive un progetto software e vuole progettare lo scaffolding iniziale della codebase prima dell’implementazione. La skill produce una proposta modulare, leggibile, scalabile, mantenibile e testabile: struttura di cartelle e file, README locali, note architetturali, convenzioni, regole di dipendenza, strategia di test, configurazione, error handling e linee guida di implementazione. Non genera codice applicativo.
---

# Skill: Project Scaffolder

## 1. Scopo della skill

Questa skill serve a progettare lo scaffolding iniziale di un progetto software partendo dalla descrizione dell’utente.

L’obiettivo non è generare tante cartelle, ma progettare una codebase iniziale in cui:

* ogni directory importante abbia una ragione chiara per esistere;
* ogni modulo abbia una responsabilità chiara;
* la direzione delle dipendenze sia esplicita;
* il codice futuro abbia un posto ovvio in cui andare;
* le decisioni architetturali siano comprensibili dai futuri contributor;
* il progetto sia facile da navigare, testare, mantenere ed evolvere.

Lo scaffolding deve aiutare l’utente ad avviare lo sviluppo con una codebase:

* modulare;
* leggibile;
* scalabile;
* mantenibile;
* testabile;
* facile da navigare;
* facile da evolvere;
* coerente con architettura, tecnologie e linguaggi scelti dall’utente.

La skill lavora nella fase iniziale di progettazione della codebase. Non deve implementare funzionalità applicative.

## 2. Ambito e limiti

### Cosa può produrre

Quando appropriato, la skill può produrre:

* albero delle cartelle proposto;
* file di root consigliati;
* contenuti o template dei README per directory importanti;
* responsabilità dei moduli;
* regole di dipendenza;
* convenzioni di naming;
* struttura dei test;
* strategia di configurazione;
* strategia di gestione degli errori;
* strategia di documentazione;
* punti di estensione futuri;
* note architetturali;
* domande aperte;
* decisioni da prendere prima dell’implementazione.

### Cosa non deve produrre

La skill non deve generare codice applicativo.

In particolare, non deve generare:

* implementazioni di feature;
* business logic;
* controller, handler, componenti UI o servizi già implementati;
* modelli ORM concreti;
* client API reali;
* script operativi non richiesti;
* configurazioni eseguibili complete se non sono state richieste esplicitamente;
* mockup UI;
* microservizi prematuri;
* astrazioni complesse non giustificate.

Sono ammessi solo placeholder testuali o file documentali chiaramente marcati come parte dello scaffold iniziale.

Esempio di intestazione per placeholder:

> Questo file sarà il contenitore per ..., le sue responsabilità sono ..., eccetera

## 3. Quando usare questa skill

Usa questa skill quando l’utente chiede di:

* iniziare un nuovo progetto software;
* generare o progettare uno scaffolding;
* organizzare una nuova codebase;
* creare una struttura iniziale di cartelle;
* creare README dentro le cartelle;
* definire convenzioni di progetto prima di scrivere codice;
* tradurre un’architettura in struttura di codice;
* preparare un repository mantenibile e modulare;
* chiarire responsabilità, confini e dipendenze tra moduli;
* progettare una codebase prima dell’implementazione.

Usa questa skill anche quando l’utente fornisce:

* un’idea di progetto;
* una descrizione del prodotto;
* tecnologie già scelte;
* linguaggi già scelti;
* architettura già scelta;
* moduli o funzionalità desiderate;
* requisiti di alto livello;
* aspettative di scalabilità;
* vincoli organizzativi o tecnici.

## 4. Quando non usare questa skill

Non usare questa skill quando l’utente vuole solo:

* una breve spiegazione teorica;
* aiuto su un singolo errore di codice;
* supporto sintattico specifico di un framework;
* configurazione di deployment soltanto;
* implementazione completa dell’applicazione;
* generazione di codice applicativo;
* mockup UI;
* progettazione dello schema database soltanto;
* scelta dei pacchetti o delle librerie soltanto;
* debugging;
* refactoring puntuale di codice esistente.

## 5. Principio operativo fondamentale

Questa skill non deve fare assunzioni arbitrarie quando le informazioni dell’utente sono incomplete.

Se un dettaglio mancante può cambiare in modo significativo la struttura della codebase, la scelta dei confini, la direzione delle dipendenze, il layout dei test, la separazione frontend/backend, la forma del monorepo o la documentazione generata, l’agente deve chiedere chiarimenti prima di proporre lo scaffold.

L’agente deve chiedere chiarimenti ogni volta che:

* una richiesta è ambigua;
* bisogna scegliere tra più alternative valide;
* l’utente non ha specificato una tecnologia necessaria alla struttura;
* l’architettura non è chiara;
* non è chiaro se il progetto sia frontend, backend, full-stack, CLI, API, automazione o monorepo;
* non è chiaro il livello di complessità atteso;
* non è chiaro se separare moduli per dominio, feature, layer o package;
* una scelta avrebbe conseguenze importanti sulla manutenibilità futura.

L’agente non deve procedere inventando decisioni importanti.

Sono ammesse solo assunzioni minori, locali e non strutturali, purché vengano dichiarate chiaramente. Le assunzioni non devono sostituire decisioni che spettano all’utente.

## 6. Primo passo: raccogliere le informazioni necessarie

Prima di generare lo scaffolding, identifica dal prompt dell’utente queste informazioni:

* Scopo del progetto:
* Utenti principali:
* Aree principali di dominio/business:
* Architettura scelta:
* Tecnologie scelte:
* Linguaggio o linguaggi scelti:
* Ambiente di esecuzione:
* Frontend, backend, full-stack, CLI, API, automazione o monorepo:
* Database o layer di storage:
* Integrazioni esterne:
* Dimensione attesa del progetto:
* Aspettative sui test:
* Target di deployment:
* Vincoli importanti:

Se una o più informazioni mancano, valuta se sono indispensabili per progettare lo scaffold.

### Se mancano informazioni importanti

Fai domande di chiarimento mirate prima di generare la proposta.

Le domande devono essere concrete e orientate alle decisioni strutturali.

Esempio:

> Prima di proporre lo scaffold devo chiarire 3 decisioni che cambiano molto la struttura:
>
> 1. Il progetto sarà backend API, full-stack o monorepo?
> 2. Hai già scelto framework e linguaggio?
> 3. Vuoi una struttura semplice per MVP o una struttura più rigorosa per crescita futura?

### Se mancano solo dettagli minori

Puoi procedere, ma indica le assunzioni minori in una sezione Assunzioni minori o in ASSUMPTIONS.md.

Esempi di assunzioni minori accettabili:

* Si assume che il progetto debba includere test fin dallo scaffold iniziale.
* Si assume che la documentazione architetturale possa partire da un file ARCHITECTURE.md sintetico.
* Si assume che i dettagli infrastrutturali vadano isolati dalla logica di dominio.
* Si assume che i provider esterni vadano nascosti dietro adapter.

Non inventare:

* regole di business;
* moduli complessi non suggeriti;
* provider esterni non citati;
* vincoli di deployment non dichiarati;
* scelte di framework o database quando cambiano la struttura;
* decisioni di architettura che l’utente non ha scelto o approvato.

## 7. Comportamento principale

Quando attivata, la skill trasforma la descrizione del progetto dell’utente in una proposta di struttura iniziale coerente del repository.

La proposta deve comunicare:

* responsabilità dei moduli;
* confini tra layer;
* direzione delle dipendenze;
* separazione tra dominio, applicazione, interfacce e infrastruttura;
* dove mettere nuovo codice;
* dove mettere test, configurazione e documentazione;
* quali dipendenze sono consentite o vietate;
* quali decisioni sono state prese e quali restano aperte.

Se sono disponibili strumenti per creare file crea effettivamente lo scaffolding documentale.

Se non sono disponibili strumenti per creare file, restituisci struttura e contenuti dei file in Markdown.

Anche quando la creazione di file è possibile, non generare codice applicativo.

## 8. Principi dello scaffolding

### 8.1 Struttura per significato, non solo per tecnologia

Preferisci cartelle che riflettano il dominio e le responsabilità del progetto.

Esempi di concetti top-level o module-level:

* users
* auth
* billing
* orders
* payments
* notifications
* catalog
* reports
* permissions
* projects
* documents

Evita contenitori generici:

* utils
* helpers
* common
* misc
* managers
* core
* shared
* services

Cartelle generiche possono esistere solo quando il loro scopo è ristretto, necessario ed esplicitamente documentato.

### 8.2 Rendi espliciti i confini dei moduli

Ogni modulo principale deve avere un README che spieghi:

* Scopo
* Responsabilità
* Cosa appartiene qui
* Cosa non appartiene qui
* Punti di ingresso pubblici
* Dipendenze consentite
* Dipendenze vietate
* Aspettative sui test
* Note di estensione

Ogni modulo dovrebbe essere descrivibile in una sola frase.

Se un modulo non può essere descritto semplicemente, dividilo o rinominalo.

### 8.3 Separa business logic e dettagli tecnici

Lo scaffolding deve separare:

* Logica di dominio
* Casi d’uso applicativi
* Adapter di interfaccia
* Adapter infrastrutturali
* Configurazione
* Test
* Documentazione
* Script

I nomi esatti delle cartelle possono variare in base a linguaggio, framework o architettura, ma la separazione delle responsabilità deve restare chiara.

### 8.4 Controlla la direzione delle dipendenze

I README generati devono spiegare la direzione delle dipendenze.

Regola di default:

* Layer di interfaccia → Layer applicativo → Layer di dominio
* Layer infrastrutturale → Contratti applicativi o di dominio
* Layer di dominio → Nessuna dipendenza da framework, database o provider esterni

Il dominio non dovrebbe dipendere da:

* framework HTTP
* framework UI
* implementazione database
* modelli ORM
* client di API esterne
* message broker
* SDK di file storage
* SDK cloud
* variabili d’ambiente

### 8.5 Rendi sostituibile l’infrastruttura

I sistemi esterni devono essere isolati dietro adapter o gateway.

Esempi di responsabilità infrastrutturali:

* database
* cache
* email
* pagamenti
* file storage
* code
* API di terze parti
* provider di autenticazione
* logging
* analytics

Non spargere chiamate infrastrutturali dentro la logica di business.

### 8.6 Evita complessità prematura

Non generare layer, pattern o astrazioni inutili.

Usa una struttura adatta alla dimensione del progetto o della feature descritta dell’utente.

Per progetti/feature piccoli:

* Preferisci moduli semplici.
* Evita nesting eccessivo.
* Evita astrazioni per ogni cosa.
* Mantieni convenzioni leggere.

Per progetti/feature medi o grandi:

* Usa confini di layer più chiari.
* Usa casi d’uso applicativi espliciti.
* Usa adapter infrastrutturali.
* Usa regole di dipendenza più rigorose.
* Usa documentazione architetturale.

### 8.7 Rendi il progetto auto-documentante

Lo scaffolding deve insegnare ai futuri contributor dove mettere le cose.

Ogni directory importante dovrebbe includere un README che risponde a:

* Perché esiste questa directory?
* Che tipo di codice appartiene qui?
* Che tipo di codice non appartiene qui?
* Da quali altre directory può dipendere?
* Quali directory possono dipendere da questa?
* Come dovrebbe essere testata quest’area?

### 8.8 Ottimizza per il cambiamento futuro

La struttura deve rendere locali i cambiamenti comuni.

Prima di finalizzare la proposta, chiediti internamente:

* Se cambia il database, dove avviene il cambiamento?
* Se cambia un provider esterno, dove avviene il cambiamento?
* Se cambia una regola di business, dove avviene il cambiamento?
* Se viene aggiunta una nuova interfaccia, cosa può essere riusato?
* Se viene aggiunto un nuovo modulo, dove dovrebbe andare?

Se la risposta è “in molte cartelle non correlate”, migliora la struttura.

## 9. File consigliati nella root

Genera o raccomanda file di root rilevanti in base al progetto.

File comuni:

* README.md
* ASSUMPTIONS.md
* ARCHITECTURE.md
* CONTRIBUTING.md
* .env.example
* .editorconfig

File o directory opzionali:

* ADR/
* docs/
* scripts/
* tests/
* config/

Non aggiungere file inutili se l’utente vuole uno scaffolding minimale.

Non far sembrare il progetto più implementato o maturo di quanto sia.

## 10. README principale

Il file README.md principale dovrebbe includere:

* Panoramica del progetto
* Stato attuale
* Tech stack
* Sintesi architetturale
* Struttura delle cartelle
* Come eseguire localmente, se già definito
* Come eseguire i test, se già definito
* Come configurare il progetto
* Convenzioni principali
* Regole di dipendenza
* Dove aggiungere nuovo codice
* Mappa della documentazione
* Domande aperte

Se il progetto non è ancora implementato, marca le sezioni come placeholder.

Usa frasi come:

* Da implementare
* Pianificato
* Placeholder
* Scaffold iniziale
* Decisione da confermare

Non fingere che funzionalità non ancora esistenti siano già presenti.

## 11. Template README per directory

Ogni README di directory importante dovrebbe seguire questa struttura:

```markdown
# Nome Directory

## Scopo

Descrivi perché questa directory esiste.

## Responsabilità

Elenca cosa possiede questa directory.

## Cosa appartiene qui

Elenca cosa dovrebbe essere collocato qui.

## Cosa non appartiene qui

Elenca cosa non dovrebbe essere collocato qui.

## Regole di dipendenza

Spiega da cosa questa directory può dipendere e da cosa non deve dipendere.

## Convenzioni di naming

Descrivi le aspettative locali sui nomi.

## Linee guida per i test

Spiega come dovrebbe essere testato il codice in questa directory.

## Note di estensione

Spiega come aggiungere nuovo codice qui in modo sicuro.
```

Adatta i titoli quando necessario, ma preserva l’intento.

I README devono essere specifici, non generici.

README debole:

> Questa cartella contiene servizi.

README buono:

> Questo modulo coordina i workflow di registrazione utente. Possiede i casi d’uso applicativi legati alla creazione account, ma non possiede persistenza, routing HTTP, invio email o implementazioni di hashing password.

Ogni README dovrebbe aiutare uno sviluppatore a decidere se un nuovo file appartiene a quella directory.

## 12. Documentazione architetturale

Crea o raccomanda un file ARCHITECTURE.md quando il progetto non è banale.

Dovrebbe includere:

* Stile architetturale
* Responsabilità dei layer
* Confini dei moduli
* Direzione delle dipendenze
* Flusso dei dati
* Strategia di gestione degli errori
* Strategia di configurazione
* Strategia di testing
* Trade-off noti
* Note di evoluzione futura

Non far sembrare l’architettura più matura di quanto sia.

Distingui chiaramente tra:

* Decisioni attuali
* Assunzioni minori
* Prossime decisioni consigliate
* Domande aperte

## 13. ADR

Per progetti con decisioni architetturali importanti, crea o raccomanda una directory ADR/.

Non creare molti ADR se non sono utili.

Quando appropriato, preferisci un solo ADR iniziale sull’architettura scelta.

Formato ADR:

```markdown
# ADR-0001: Titolo della decisione

## Stato

Proposta | Accettata | Deprecata | Superata

## Contesto

Quale problema o vincolo ha portato a questa decisione?

## Decisione

Cosa è stato deciso?

## Conseguenze

Cosa diventa più facile?

Cosa diventa più difficile?

Quali trade-off vengono accettati?

## Alternative considerate

Quali altre opzioni sono state considerate?

Perché non sono state scelte?
```

## 14. Strategia dei test

Lo scaffolding dovrebbe includere una strategia di testing adatta al progetto.

Possibili categorie di test:

* unit test
* integration test
* end-to-end test
* contract test
* test architetturali sui confini
* fixture
* utility di test

I README dei test dovrebbero chiarire:

* Che tipo di comportamento viene testato qui
* Cosa non dovrebbe essere testato qui
* Come nominare i test
* Come isolare l’infrastruttura
* Come gestire dipendenze esterne

Dai priorità ai test su:

* regole di dominio
* casi d’uso applicativi
* workflow critici
* percorsi di errore
* confini di integrazione

Evita di incoraggiare test che rispecchiano solo dettagli implementativi.

## 15. Strategia di configurazione

La configurazione deve essere esplicita e centralizzata.

Raccomanda o genera documentazione per:

* .env.example
* README di configurazione
* documentazione delle variabili d’ambiente
* separazione tra configurazione locale, test, staging e produzione

Evita:

* segreti hardcoded
* configurazione sparsa tra moduli
* accesso all’ambiente dentro la logica di dominio
* impostazioni globali nascoste

## 16. Strategia di gestione degli errori

Lo scaffolding dovrebbe definire dove gli errori sono rappresentati e gestiti.

Documenta:

* errori di validazione
* errori di dominio
* errori applicativi
* errori infrastrutturali
* errori di sistema inattesi
* confini del logging
* traduzione degli errori per l’utente
* fallimenti ritentabili

Evita:

* fallimenti silenziosi
* catch-all senza contesto
* esposizione di errori interni agli utenti
* miscela tra messaggi utente e diagnostica interna

## 17. Convenzioni di naming

Includi linee guida di naming nel README principale o in CONTRIBUTING.md.

Copri:

* nomi dei moduli
* nomi dei file
* nomi di classi e funzioni
* nomi dei test
* nomi di interfacce o contratti
* nomi degli adapter
* nomi dei casi d’uso
* nomi degli eventi
* nomi degli errori
* nomi della configurazione

Regole:

* I nomi devono rivelare l’intento.
* Parole diverse dovrebbero indicare concetti diversi.
* Evita nomi vaghi come helper, manager, processor, utils, misc.
* Usa verbi coerenti in tutto il progetto.

## 18. Adattamento alla dimensione del progetto

### Progetto piccolo

Usa meno layer.

Caratteristiche consigliate:

* struttura semplice
* README chiari
* astrazioni minime
* test di base
* configurazione centralizzata
* nessun ADR inutile
* nessun nesting eccessivo

### Progetto medio

Usa confini più chiari.

Caratteristiche consigliate:

* moduli orientati al dominio
* casi d’uso applicativi
* adapter infrastrutturali
* README a livello di modulo
* integration test
* documentazione architetturale
* configurazione per ambiente

### Progetto grande

Usa una struttura più rigorosa.

Caratteristiche consigliate:

* bounded context espliciti
* regole di dipendenza forti
* documentazione architetturale
* ADR
* contract test
* struttura pronta per CI
* note di ownership dei moduli
* convenzioni condivise
* controlli sui confini delle dipendenze

## 19. Adattamento al tipo di progetto

### Monorepo

Per monorepo, preferisci una struttura che separi:

* applicazioni
* package riutilizzabili
* contratti condivisi
* tooling
* documentazione

Documenta:

* quali app esistono
* quali package sono riutilizzabili
* quali package sono dettagli implementativi privati
* quali dipendenze sono consentite
* come introdurre codice condiviso
* come evitare che i package shared diventino discariche

Presta particolare attenzione alle cartelle condivise.

Il codice condiviso deve avere ownership e scopo chiari.

### Full-stack

Per progetti full-stack, chiarisci i confini tra:

* frontend
* backend
* tipi o contratti condivisi
* schemi API
* infrastruttura
* documentazione
* test

Evita di duplicare regole di business tra frontend e backend.

Documenta dove appartiene la validazione.

Documenta quale codice condiviso è sicuro condividere.

### API

Per progetti API, includi linee guida per:

* route o controller
* validazione delle richieste
* casi d’uso applicativi
* regole di dominio
* persistenza
* integrazioni esterne
* mapping delle risposte
* traduzione degli errori
* documentazione API

I controller devono restare sottili.

Le decisioni di business devono vivere fuori dal codice di routing.

### Frontend

Per progetti frontend, includi linee guida per:

* pagine o route
* feature
* componenti
* gestione stato
* client API
* modelli di dominio
* form
* validazione
* design system
* test

Evita di mettere logica di business direttamente dentro componenti visuali quando può essere separata.

Distingui tra componenti UI riutilizzabili e componenti specifici di una feature.

### Backend

Per progetti backend, includi linee guida per:

* moduli di dominio
* servizi applicativi o casi d’uso
* adapter infrastrutturali
* accesso al database
* background job
* eventi
* configurazione
* logging
* gestione errori
* test

Evita di mettere tutta la logica in generici “services” senza ownership chiara del modulo.

### CLI o automazione

Per progetti CLI o automazione, includi linee guida per:

* comandi
* casi d’uso
* logica di dominio
* adapter
* configurazione
* logging
* formattazione input/output
* test

Gli handler dei comandi devono parsare l’input e delegare il comportamento.

La logica centrale deve restare testabile senza invocare la CLI.

## 20. Gestione dell’architettura fornita dall’utente

Se l’utente ha già scelto un’architettura, rispettala.

Non sostituirla salvo conflitti con gli obiettivi dichiarati.

Invece:

* Mappa l’architettura in cartelle.
* Documenta le responsabilità dei layer.
* Documenta la direzione delle dipendenze.
* Crea README che rinforzino i confini.
* Identifica rischi o decisioni mancanti.
* Suggerisci miglioramenti minimi.

Se l’architettura scelta sembra troppo complessa, avvisa con cautela e suggerisci una variante più semplice.

Se l’architettura scelta sembra troppo debole per la scala prevista, suggerisci confini più forti.

Se per procedere serve scegliere tra varianti architetturali, chiedi chiarimento prima di generare lo scaffold.

## 21. Gestione delle tecnologie fornite dall’utente

Se l’utente ha già scelto tecnologie e linguaggi, rispettali.

Usa le loro convenzioni quando conosciute.

Non raccomandare di cambiare stack salvo rilevanza diretta per modularità, mantenibilità o scalabilità.

Quando servono cartelle specifiche della tecnologia, rendile subordinate alla chiarezza architetturale.

Se mancano tecnologie che cambiano la struttura, chiedi all’utente prima di procedere.

## 22. Formato di output quando non si creano file

Quando l’utente vuole una proposta di scaffold ma non la creazione effettiva dei file, rispondi con questa struttura:

```markdown
# Scaffolding proposto

## Informazioni confermate

## Domande aperte bloccanti, se presenti

## Assunzioni minori, se presenti

## Albero delle cartelle

## File di root

## Regole di dipendenza

## Strategia di testing

## Strategia di configurazione

## Strategia di gestione degli errori

## Convenzioni principali

## Prossimi passi di implementazione
```

Se esistono domande aperte bloccanti, non generare lo scaffold completo.

In quel caso, restituisci prima le domande necessarie e spiega brevemente perché cambiano la struttura.

Mantieni l’output pratico.

Non spiegare troppa teoria generale se l’utente non la chiede.

## 23. Formato di output quando si creano file

Quando la creazione di file è possibile:

* verifica prima se ci sono decisioni bloccanti;
* se ci sono decisioni bloccanti, chiedi chiarimenti prima di creare file;
* se non ci sono decisioni bloccanti, crea le cartelle;
* crea i file di root documentali;
* crea README nelle directory importanti;
* crea file placeholder solo quando utili;
* non generare codice applicativo;
* non generare grandi quantità di codice implementativo;
* riassumi cosa è stato creato;
* indica assunzioni minori e domande aperte residue.

## 24. Regole di creazione file

Quando generi file reali:

* non sovrascrivere file esistenti salvo autorizzazione esplicita;
* se un file esiste già, ispezionalo prima di modificarlo;
* preserva il contenuto scritto dall’utente;
* preferisci aggiungere documentazione mancante invece di sostituire documentazione esistente;
* se esistono conflitti, segnalali chiaramente;
* mantieni i README generati concisi ma utili;
* evita directory vuote, salvo supporto dell’ambiente o presenza di README;
* marca chiaramente i placeholder;
* non creare file di codice applicativo.

## 25. Checklist sui confini delle dipendenze

Prima di finalizzare lo scaffold, verifica:

* La logica di dominio può esistere senza il framework?
* I casi d’uso possono essere testati senza infrastruttura reale?
* I provider esterni sono isolati?
* La configurazione è centralizzata?
* Le cartelle utility generiche sono ridotte al minimo?
* Le responsabilità dei moduli sono chiare?
* La direzione delle dipendenze è documentata?
* Esiste un posto chiaro per i test?
* Esiste un posto chiaro per la documentazione?
* Un nuovo sviluppatore può capire dove aggiungere codice?

## 26. Red flag da evitare

Non generare scaffolding che incoraggi:

* logica di business nei controller
* logica di business nei componenti UI
* chiamate database sparse ovunque
* chiamate ad API esterne sparse ovunque
* cartelle generiche services
* grandi cartelle utils
* god module
* dipendenze circolari
* leak del framework nella logica di dominio
* configurazione nascosta in file casuali
* naming incoerente
* astrazioni non spiegate
* microservizi prematuri

## 27. Standard di qualità dello scaffold

Uno scaffold è buono solo se uno sviluppatore futuro può rispondere a:

* Dove aggiungo una nuova feature?
* Dove metto le regole di business?
* Dove metto il codice specifico del framework?
* Dove metto il codice database?
* Dove metto integrazioni con provider esterni?
* Dove metto i test?
* Dove documento decisioni architetturali?
* Quali dipendenze sono vietate?
* Come evito di creare una discarica di utility generiche?

Se lo scaffold non risponde a queste domande, miglioralo.

## 28. Risposta finale

Quando concludi un’attività di scaffolding, fornisci un riepilogo conciso con:

* cosa è stato generato o proposto
* perché è stata scelta quella struttura
* assunzioni minori importanti
* regole di dipendenza principali
* da dove l’utente dovrebbe iniziare a implementare
* eventuali domande aperte

Non ripetere l’intero contenuto di ogni README se i file sono stati creati realmente.

## 29. Regola finale

Questa skill deve progettare lo scaffold, non implementare il progetto.

Quando qualcosa non è chiaro o ci sono più alternative strutturali valide, chiedi chiarimento prima di procedere.

Non prendere decisioni importanti al posto dell’utente.

Non generare codice applicativo.

Produci una base documentale e architetturale chiara, utile e pronta a guidare l’implementazione successiva.
