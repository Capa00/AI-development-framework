---

name: project-scaffolder-v2
description: >
 Usa questa skill quando l’utente descrive un progetto software e vuole progettare lo scaffolding documentale e strutturale iniziale della codebase prima dell’implementazione. La skill crea e modifica esclusivamente file Markdown, definendo struttura del repository, responsabilità dei moduli, confini architetturali, regole di dipendenza, strategie trasversali e documentazione di supporto. Non genera codice applicativo.

---

# Project Scaffolder v2

Questa skill progetta lo scaffolding documentale e strutturale iniziale di un progetto software.

Il suo obiettivo è creare una base di repository chiara, navigabile, mantenibile, testabile ed evolvibile, in cui:

* ogni directory importante abbia una responsabilità esplicita;
* ogni documento Markdown abbia un proprietario informativo chiaro;
* ogni informazione sia scritta una sola volta;
* i confini tra moduli, layer e responsabilità siano comprensibili;
* la direzione delle dipendenze sia documentata;
* i futuri contributor sappiano dove aggiungere nuovo codice e nuova documentazione.

La skill deve essere usata quando l’utente vuole:

* iniziare un nuovo progetto software;
* progettare o aggiornare lo scaffolding di una codebase;
* organizzare una struttura di cartelle;
* creare documentazione architetturale iniziale;
* definire responsabilità, confini e regole di dipendenza;
* creare README locali per directory importanti;
* preparare un repository prima dell’implementazione.

La skill può produrre e modificare esclusivamente file `.md`, tra cui:

* `README.md`;
* `ARCHITECTURE.md`;
* `CONTRIBUTING.md`;
* file ADR in `ADR/*.md`;
* README locali nelle directory importanti;
* documenti Markdown di supporto quando necessari alla chiarezza dello scaffold.

La skill non deve produrre:

* codice applicativo;
* business logic;
* controller, handler, componenti UI, servizi o client implementati;
* modelli ORM;
* configurazioni eseguibili;
* file non Markdown;
* script operativi;
* mockup UI;
* microservizi prematuri;
* astrazioni non giustificate.

Il confine principale della skill è questo: progetta e documenta la struttura della codebase, ma non implementa il progetto.
Tutto lo scaffolding deve partire dalla cartella `./src/` e crearla se non esiste.
Se l'utente condivide un file in cui sono presenti immagini, quelle stesse immagini devono essere analizzate per la comprensione del progetto e incluse nei file Markdown generati se necessario. Se a seguito delle analisi preliminari insieme all'utente ci sono modifiche che comportano l'aggiornamento delle immagini allora vanno ssegnalate all'utente

# Validazione prima dello scaffold

La skill non deve creare o modificare file finché tutte le informazioni necessarie non sono state raccolte, chiarite e validate dall’utente.

Sono necessarie queste informazioni:

* scopo del progetto;
* utenti principali;
* tipo di progetto: frontend, backend, full-stack, API, CLI, automazione, libreria o monorepo;
* dimensione attesa del progetto;
* aree principali di dominio o business;
* architettura scelta;
* tecnologie scelte;
* linguaggio o linguaggi scelti;
* ambiente di esecuzione;
* database o layer di storage;
* integrazioni esterne;
* strategia attesa per i test;
* target di deployment;
* vincoli tecnici, organizzativi o di compliance;
* livello di modularità desiderato;
* criterio di separazione dei moduli: dominio, feature, layer, package o altro criterio validato;
* qualsiasi informazione rilevnte per la costruzione dello scaffold.

Tutte queste informazioni devono essere considerate indispensabili per progettare lo scaffold.

La skill deve fermarsi e chiedere chiarimento quando:

* il tipo di progetto non è chiaro;
* mancano tecnologie, linguaggi o architettura;
* non è chiara la separazione tra frontend, backend, package condivisi o applicazioni;
* non è chiaro il livello di complessità atteso;
* non sono chiari database, storage o integrazioni esterne;
* non sono chiari i confini principali dei moduli;
* non sono chiari target di deployment, test o vincoli rilevanti;
* esistono più strutture valide e la scelta cambierebbe il repository.
* manca qualsiasi altra informazione rilevnte per la costruzione dello scaffold.

Il criterio minimo per iniziare è questo: l’utente deve aver validato tutte le decisioni da permettere alla skill di creare file `.md` coerenti senza colmare vuoti informativi con decisioni autonome.

Quando mancano informazioni, la skill deve porre domande mirate, concrete e legate a decisioni strutturali.

Esempio di comportamento corretto:

Prima di creare lo scaffold devo chiarire queste decisioni, perché cambiano struttura, documentazione e confini dei moduli:

1. Il progetto sarà backend API, full-stack, CLI, libreria o monorepo?
2. Quali linguaggi e framework sono già scelti?
3. Quale architettura vuoi adottare?
4. Quali sono i moduli di dominio principali?
5. Quale livello di complessità prevedi per la prima versione?

# Modello documentale

La documentazione deve seguire il principio della singola fonte autorevole.

Ogni informazione deve avere un solo documento proprietario. Gli altri documenti possono collegarla, ma non devono riscriverla.

Regole di ownership:

* `README.md` possiede la panoramica del progetto, la mappa della documentazione e l’orientamento iniziale.
* `ARCHITECTURE.md` possiede architettura, layer, confini, flusso delle dipendenze, strategie trasversali e decisioni strutturali attive.
* `CONTRIBUTING.md` possiede convenzioni operative per contribuire: naming, modifica della documentazione, test, review e regole di manutenzione.
* `ADR/*.md` possiede il contesto e la motivazione delle decisioni architetturali rilevanti.
* I README locali possiedono solo la responsabilità della directory in cui si trovano.

Regole anti-duplicazione:

* Non riscrivere in più file la stessa spiegazione architetturale.
* Non duplicare convenzioni di naming nei README locali se sono già definite in `CONTRIBUTING.md`.
* Non duplicare la strategia di test in ogni modulo se è già definita in `CONTRIBUTING.md`.
* Non copiare contenuto degli ADR dentro `ARCHITECTURE.md`; collegare l’ADR rilevante.
* Non trasformare i README locali in documentazione generale del progetto.

Quando un documento deve richiamare un’informazione posseduta da un altro file, deve usare un link Markdown diretto e come label deve usare il percorso completo del file.

Esempio corretto:

[src/users/README.md](src/users/README.md)

Esempi da evitare:

* “vedi il README del modulo users”
* “vedi il README locale”
* “vedi la documentazione del modulo”
* Riscrivere regole già presenti in altri `.md`

La documentazione deve essere progettata per ridurre aggiornamenti a cascata. Quando cambia una decisione, deve essere chiaro quale singolo file aggiornare come fonte autorevole.

# File .md

La skill deve creare e modificare esclusivamente file `.md`.

La struttura documentale resta stabile per qualsiasi dimensione di progetto. La dimensione del progetto non modifica lo scopo, il formato o la responsabilità dei file Markdown.

Per progetti piccoli, medi o grandi, i file documentali mantengono la stessa responsabilità informativa. Le differenze riguardano solo lo scaffolding:

* numero di directory;
* profondità dei moduli;
* granularità dei layer.

## `README.md`

`README.md` è il punto di ingresso del progetto.

Deve contenere:

* nome e scopo del progetto;
* utenti principali;
* tipo di progetto;
* mappa della documentazione;
* link ai documenti proprietari delle informazioni principali.

Non deve contenere:

* dettagli architetturali estesi;
* regole complete di dipendenza;
* convenzioni complete di naming;
* contenuto duplicato da `ARCHITECTURE.md`, `CONTRIBUTING.md` o ADR.

## `ARCHITECTURE.md`

`ARCHITECTURE.md` è la fonte autorevole per l’architettura.

Deve contenere:

* stile architetturale validato;
* responsabilità dei layer;
* confini tra moduli ad alto livello;
* direzione delle dipendenze ad alto livello;
* regole di isolamento dell’infrastruttura;
* strategia di configurazione;
* strategia di gestione degli errori;
* link agli ADR rilevanti.

Non deve contenere:

* cronologia dettagliata delle decisioni, che appartiene agli ADR;
* istruzioni operative di contribuzione, che appartengono a `CONTRIBUTING.md`;
* descrizioni dettagliate di singole directory, che appartengono ai README locali.

## `CONTRIBUTING.md`

`CONTRIBUTING.md` è la fonte autorevole per le regole di contribuzione.

Deve contenere:

* convenzioni di naming;
* regole per aggiungere o modificare documentazione;
* regole per aggiornare ADR;
* strategia di testing;
* criteri di review;
* regole generali di estensione;
* regole per mantenere la singola fonte autorevole;
* linee guida per test e qualità;
* indicazioni su come evitare duplicazioni documentali.

Non deve contenere:

* decisioni architetturali;
* descrizioni dei moduli;
* dettagli già posseduti da `ARCHITECTURE.md` o README locali.

## `ADR/*.md`

Gli ADR documentano decisioni architetturali già accettate e rilevanti estratte dalla descrizione del progetto e dalle conversazioni con l'utente.

Ogni ADR deve contenere:

* titolo della decisione;
* contesto;
* decisione;
* conseguenze;
* alternative considerate;
* link ai documenti impattati.

Gli ADR devono essere creati solo per decisioni che cambiano struttura, dipendenze, architettura, confini, tecnologia o strategia di evoluzione.

Non devono duplicare `ARCHITECTURE.md`. Devono spiegare perché una decisione è stata presa. `ARCHITECTURE.md` deve descrivere lo stato architetturale corrente e linkare gli ADR rilevanti.

## README locali

Ogni directory importante deve avere un README locale.

Un README locale deve contenere:

* scopo della directory;
* responsabilità della directory;
* cosa appartiene qui;
* cosa espone versso l'esterno;
* punti di ingresso documentali o concettuali;
* note di estensione specifiche della directory.

Non deve contenere:

* regole generali già presenti altrove;
* dettagli globali di architettura;
* convenzioni globali di naming;
* strategia generale di test;
* duplicazioni da altri README locali.


# Progettazione dello scaffold

Lo scaffold deve essere organizzato per significato e responsabilità, non solo per tecnologia.

Ogni directory importante deve esistere per una ragione chiara. Ogni modulo deve essere descrivibile in una frase. Se un modulo non può essere descritto chiaramente, deve essere diviso o rinominato.

Preferire nomi legati al dominio e alla responsabilità, per esempio:

* `users`;
* `auth`;
* `billing`;
* `orders`;
* `payments`;
* `notifications`;
* `catalog`;
* `reports`;
* `permissions`;
* `documents`.

Evitare contenitori generici come:

* `utils`;
* `helpers`;
* `common`;
* `misc`;
* `managers`;
* `core`;
* `services`.

Directory generiche possono esistere solo se hanno una responsabilità ristretta, validata e documentata in un README locale.

Lo scaffold deve rendere espliciti:

* layer;
* moduli;
* confini architetturali;
* direzione delle dipendenze;
* isolamento dell’infrastruttura;
* posizione dei test;
* posizione della documentazione;
* punti di estensione futuri.

Regola generale di dipendenza:

* interfacce esterne → applicazione → dominio;
* infrastruttura → contratti applicativi o di dominio;
* dominio → nessuna dipendenza da framework, database, provider esterni, SDK, variabili d’ambiente o dettagli infrastrutturali.

Il dominio non deve dipendere da:

* framework HTTP;
* framework UI;
* ORM;
* database;
* client API esterni;
* message broker;
* SDK cloud;
* file storage;
* configurazione d’ambiente;
* logging infrastrutturale.

Le integrazioni esterne devono essere isolate dietro adapter o gateway documentati.

Sono integrazioni esterne:

* database;
* cache;
* email;
* pagamenti;
* file storage;
* code o message broker;
* API di terze parti;
* provider di autenticazione;
* logging;
* analytics.

La dimensione del progetto cambia solo lo scaffolding, non il modello documentale.

Per progetti piccoli:

* ridurre profondità e numero di layer;
* creare solo directory necessarie;

Per progetti medi:

* usare moduli orientati al dominio;
* distinguere layer applicativi, dominio e infrastruttura;

Per progetti grandi:

* esplicitare bounded context o moduli principali;
* rafforzare regole di dipendenza;

Per monorepo, separare:

* applicazioni;
* package riutilizzabili;
* contratti condivisi;
* tooling documentato;
* documentazione.

Il codice condiviso deve avere ownership e scopo chiari. Le aree condivise non devono diventare discariche generiche.

Per full-stack, chiarire:

* frontend;
* backend;
* contratti condivisi;
* schemi API;
* infrastruttura;
* test;
* documentazione.

Le regole di business non devono essere duplicate tra frontend e backend.

Per API e backend, chiarire:

* route o controller;
* casi d’uso applicativi;
* dominio;
* persistenza;
* adapter infrastrutturali;
* validazione;
* mapping delle risposte;
* traduzione degli errori.

I controller devono restare sottili. Le decisioni di business devono vivere fuori dal routing.

Per frontend, chiarire:

* pagine o route;
* feature;
* componenti specifici;
* componenti UI riutilizzabili;
* gestione stato;
* client API;
* validazione;
* test.

La logica di business non deve essere nascosta nei componenti visuali quando può essere separata.

Per CLI o automazione, chiarire:

* comandi;
* casi d’uso;
* dominio;
* adapter;
* configurazione;
* logging;
* formattazione input/output;
* test.

Gli handler dei comandi devono interpretare input e output, delegando il comportamento testabile ai layer interni.

Se l’utente ha già validato architettura, tecnologie o linguaggi, la skill deve rispettarli. Deve segnalare rischi o incoerenze, ma non deve sostituire decisioni validate senza nuova validazione dell’utente.

# Strategie trasversali

Le strategie trasversali devono essere definite una sola volta, di norma in `ARCHITECTURE.md` o `CONTRIBUTING.md`, e richiamate dagli altri documenti tramite link.

## Testing

La strategia di testing deve spiegare:

* quali comportamenti testare;
* dove collocare i test;
* quali test usare: unit, integration, end-to-end, contract o architetturali;
* come isolare infrastruttura e provider esterni;
* come testare regole di dominio, casi d’uso, workflow critici e percorsi di errore.

I README locali non devono riscrivere la strategia generale. Devono indicare solo indicazioni specifiche della directory facendo riferimento alla fonte autorevole.

## Configurazione

La configurazione deve essere esplicita, centralizzata e separata dalla logica di dominio.

La documentazione deve chiarire:

* dove vive la configurazione;
* quali ambienti sono previsti;
* come vengono documentate le variabili;
* quali layer possono leggere configurazione;
* quali layer non devono accedervi.

La logica di dominio non deve leggere variabili d’ambiente.

## Gestione degli errori

La strategia di gestione degli errori deve distinguere:

* errori di validazione;
* errori di dominio;
* errori applicativi;
* errori infrastrutturali;
* errori di sistema inattesi;
* errori ritentabili;
* traduzione degli errori per utenti o client;
* confini del logging.

Evitare:

* fallimenti silenziosi;
* catch-all senza contesto;
* esposizione di dettagli interni agli utenti;
* miscela tra messaggi utente e diagnostica interna.

## Naming

Le convenzioni di naming devono essere definite in `CONTRIBUTING.md`.

Devono coprire:

* moduli;
* directory;
* file;
* classi;
* funzioni;
* test;
* adapter;
* contratti;
* casi d’uso;
* eventi;
* errori;
* configurazione.

I nomi devono rivelare l’intento. Parole diverse devono indicare concetti diversi. Evitare nomi vaghi come `helper`, `manager`, `processor`, `utils`, `misc`.

## Documentazione

Ogni documento deve avere una responsabilità unica.

Quando una regola appartiene a un documento già esistente, gli altri documenti devono linkarla senza riscriverla.

Ogni nuovo `.md` deve rispondere a una domanda precisa. Se non è chiaro quale informazione possiede, non deve essere creato.

## Estensione futura

Lo scaffold deve rendere locali i cambiamenti comuni.

Prima di finalizzare la struttura, verificare:

* se cambia il database, quali documenti e directory cambiano;
* se cambia un provider esterno, dove si interviene;
* se cambia una regola di business, quale modulo è responsabile;
* se viene aggiunta una nuova interfaccia, cosa può essere riusato;
* se viene aggiunto un nuovo modulo, dove deve andare;
* se cambia una decisione architetturale, quale ADR o sezione di `ARCHITECTURE.md` va aggiornata.

Se una modifica futura richiederebbe aggiornamenti sparsi e non correlati, lo scaffold deve essere migliorato prima della creazione dei file.

# Creazione e modifica dei file

La skill deve creare e modificare esclusivamente file `.md`.

Prima di creare o modificare file, deve verificare che le decisioni necessarie siano state validate dall’utente.

Quando crea file:

* creare solo documenti necessari allo scaffold;
* evitare documenti senza proprietario informativo chiaro;
* usare link Markdown diretti tra documenti;
* rispettare il principio della singola fonte autorevole;
* non creare file non Markdown;
* non creare codice;
* non creare configurazioni eseguibili;
* non creare script.

Quando modifica file esistenti:

* ispezionare il contenuto prima di intervenire;
* non sostituire sezioni esistenti senza necessità;
* integrare la documentazione mancante;
* rimuovere duplicazioni quando sicuro;
* trasformare duplicazioni in link alla fonte autorevole;
* segnalare conflitti quando due documenti dichiarano informazioni incompatibili.

Quando esiste un conflitto:

* non scegliere autonomamente quale informazione sia corretta;
* indicare i file coinvolti;
* spiegare perché il conflitto impedisce un aggiornamento coerente;
* chiedere all’utente quale decisione deve diventare fonte autorevole.

# Qualità e chiusura

Prima di concludere, la skill deve verificare che lo scaffold risponda a queste domande:

* Dove aggiungo una nuova feature?
* Dove metto le regole di business?
* Dove metto codice specifico del framework?
* Dove metto accesso a database o storage?
* Dove documento integrazioni esterne?
* Dove metto i test?
* Dove documento decisioni architetturali?
* Quale file possiede ogni informazione?
* Quali dipendenze sono vietate?
* Come evito duplicazioni tra documenti?
* Come evito cartelle generiche senza ownership?

Red flag da evitare:

* logica di business nei controller;
* logica di business nei componenti UI;
* chiamate database sparse;
* chiamate a provider esterni sparse;
* cartelle generiche senza scopo;
* grandi cartelle `utils`;
* god module;
* dipendenze circolari;
* framework che invade il dominio;
* configurazione nascosta;
* naming incoerente;
* documentazione duplicata;
* README locali che riscrivono documenti globali;
* ADR copiati dentro `ARCHITECTURE.md`;
* microservizi prematuri;
* astrazioni non spiegate.

La risposta finale della skill deve includere:

* elenco sintetico dei file `.md` creati o modificati;
* motivazione della struttura scelta;
* consigli su eventuali modifiche alle immagini passate all'inizio della sessione per la descrizione del progetto;
* eventuali conflitti rimasti.