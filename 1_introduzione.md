# Introduzione

## Il Web of Things

Il progetto "Web of Things" nasce per iniziativa di un gruppo di lavoro appartenente al "World Wide Web Consortium", "W3C" in breve, per risolvere una serie di problematiche inerenti allo sviluppo di progetti il cui dominio è l'"Internet of Things".
L'insieme delle tecnologie disponibili per questi progetti è molto ampio ed è costituito da svariati sistemi e servizi che sono offerti da fornitori diversi tra di loro.
Questo implica l'esistenza di molte differenze tra le tecnologie utilizzabili, differenze che si possono riscontrare a tutti i livelli.
Dai livelli più bassi, che coinvolgono i protocolli di comunicazione, a quelli più alti, che riguardano invece i modelli dei dati e i requisiti di sicurezza.
Nello sviluppo di applicazioni IoT serve perciò fare un notevole sforzo per soddisfare anche solo casi d'uso specifici, senza possibilità di generalizzazione.
Questo rende le applicazioni sviluppate difficili da estendere, da manutenere e da riusare, aumentandone i costi e diminuendone la qualità.

"Web of Things" si prefigge di fornire un insieme di strumenti di base standardizzati con il fine di semplificare lo sviluppo di applicazioni IoT.
Queste tecnologie seguono il ben noto approccio utilizzato per modellare e costruire il _web_, ormai chiaramente rivelatosi di successo, il quale è capace di fornire maggiore flessibilità ed interoperabilità, nonché di permettere di riusare strumenti e standard consolidati.
Il successo del progetto porterà ad uno sperabile superamento della frammentazione del panorama IoT, il cui risultato sarà il maggiore sviluppo di un settore già di forte interesse tecnologico e commerciale. [@wot]

## Le Thing e le Thing Description

Al centro del progetto WoT, così come al centro dell'IoT in generale, c'è il concetto di "_thing_", di oggetto "intelligente".
Secondo la definizione utilizzata all'interno del progetto stesso, una _thing_ è:

> An abstraction of a physical or a virtual entity whose metadata and interfaces are described by a "WoT Thing Description", whereas a virtual entity is the composition of one or more Things. [@wot-architecture]

Una _thing_ può perciò essere qualsiasi cosa, fisica o virtuale, e nel caso fosse virtuale può essere a sua volta composizione di più _thing_, in tal caso potrebbe essere ad esempio una stanza che contiene più _smart objects_.
Il requisito fondamentale che rende una _thing_ tale è il poter essere descritta attraverso una "Thing Description", la quale conterrà tutte le informazioni che giustificano la sua "_smartness_".
Ecco che allora questo nuovo concetto diventa fondamentale per comprendere, certamente a livello pratico, ma anche a livello teorico, che cos'è effettivamente una _thing_.

Una "Thing Description", all'interno di WoT, è definita come:

> Structured data describing a Thing. A WoT Thing Description comprises general metadata, domain-specific metadata, Interaction Affordances (which include the supported Protocol Bindings), and links to related Things. The WoT Thing Description format is the central building block of W3C WoT. [@wot-architecture]

È bene iniziare l'analisi della definizione a partire dalla terza frase che la costituisce: il formato usato in una "Thing Description" è un elemento fondante di WoT.
Come una descrizione è strutturata, che cosa contiene, che cosa è "capace di dire" e che cosa no, sono tutti concetti che stanno alla base di WoT e di come perciò è possibile modellare la realtà, fatta di _thing_, secondo lo standard contenuto in questo progetto.
Una "Thing Description" può essere vista, per il suo contenuto, come se fosse il "punto di ingresso" di un certo elemento del sistema IoT. 
Essa infatti fornisce informazioni su quali dati e funzionalità fornisce la _thing_ associata, quale protocollo utilizza per comunicare, come i dati sono codificati e strutturati, qual è il meccanismo di controllo degli accessi utilizzato, assieme ad altri metadati pensati per essere letti e interpretati da umani e da sistemi automatici. [@wot]

Anche questo conferma ciò che avevamo detto poc'anzi: le "Thing Description" sono fondamentali per poter letteralmente "parlare" di una _thing_, per sapere che cos'è e che cosa fa.
Sono quindi fondamentali per poter dare una semantica agli elementi che sono parte di un sistema IoT.
Senza le loro descrizioni, non avrei modo di far capire a nessuno, sia esso una macchina o un essere umano, quali sono le componenti del mio sistema, a che cosa servono e come interagiscono tra di loro.
Per le informazioni che contengono, le "Thing Description" fungono sia come meccanismo che permette l'interazione tra macchine, sia come documentazione utile agli sviluppatori del sistema IoT. [@wot-architecture]

L'unica alternativa all'approccio proposto da WoT è creare delle descrizioni per le _thing_ secondo un formato progettato ad hoc per la soluzione implementata.
Questa scelta presenta chiaramente tutti i rischi che sono già stati elencati all'inizio di questo capitolo.
Ecco che allora lo strumento concettuale per creare una "Thing Description", ovvero il suo modello e quindi la sua ontologia, diventa di assoluta importanza, dato che, senza di esso, non sarebbe possibile né costruirle, né tantomeno costruirle in un modo standardizzato.

Per questi motivi, nel prossimo capitolo andremo ad approfondire il significato e le implicazioni della prima parte della definizione di una "Thing Description", così da poter capire qual è il modello ontologico di una _thing_.
Questo ci porterà poi a motivare perché l'ontologia delle descrizioni è stata costruita nel modo scelto da WoT.
