# Introduzione

## Web of Things

Il progetto "Web of Things" nasce per iniziativa di un gruppo di lavoro del "World Wide Web Consortium", "W3C" in breve, per risolvere le problematiche inerenti allo sviluppo di progetti che riguardano l'"Internet of Things".
Il panorama di tecnologie disponibili per lo sviluppo sono innumerevoli, le quali consistono in svariati sistemi e servizi offerti da fornitori diversi tra di loro.
Le differenze sono a tutti i livelli: da quelli più bassi che coinvolgono protocolli di comunicazione, a quelli più alti che riguardano invece i modelli dati e i requisiti di sicurezza.
Nello sviluppo di applicazioni IoT serve perciò un notevole sforzo per casi d'uso specifici, senza possibilità di generalizzare.
Questo rende le applicazioni difficili da estendere, manutenere e riusare.

"Web of Things" si prefigge di fornire un insieme di elementi tecnologici di base standardizzati per semplificare lo sviluppo di queste applicazioni.
Questi elementi seguono il ben noto approccio utilizzato per costruire il _web_, ormai chiaramente rivelatosi di successo, capace di fornire maggiore flessibilità ed interoperabilità, nonché riuso di strumenti e standard consolidati.
Il successo del progetto porterà ad uno sperabile superamento della frammentazione del panorama IoT, portando ad un maggiore sviluppo di un settore già di forte interesse tecnologico e commerciale.[@wot]

## Things e Thing Descriptions

Al centro del progetto "WoT", così come nel campo dell'IoT, c'è il concetto di "_thing_", di oggetto.
Secondo la definizione data all'interno del progetto stesso, una _thing_ è:

> An abstraction of a physical or a virtual entity whose metadata and interfaces are described by a "WoT Thing Description", whereas a virtual entity is the composition of one or more Things.

Una _thing_ può perciò essere qualsiasi cosa, fisica o virtuale che sia, e nel caso fosse virtuale può essere a sua volta composizione di più _thing_, ad esempio potrebbe essere una stanza che contiene più _smart objects_.
Il requisito fondamentale che rende una _thing_ tale è la possibilità di essere descritta attraverso una "Thing Description".
Ecco che allora questo elemento diventa fondamentale per comprendere, certamente nella pratica, ma anche a livello teorico, che cos'è effettivamente una _thing_.

Una "Thing Description", all'interno dello stesso progetto, è definita come:

> Structured data describing a Thing. A WoT Thing Description comprises general metadata, domain-specific metadata, Interaction Affordances (which include the supported Protocol Bindings), and links to related Things. The WoT Thing Description format is the central building block of W3C WoT.

Innanzitutto, è bene concentrarsi sulla seconda frase che costituisce la definizione: il formato usato in una descrizione è un elemento fondante di WoT.[@wot-architecture]
Una descrizione può essere vista, per il suo contenuto, come se fosse il "punto di ingresso" di un certo elemento di IoT. 
Essa infatti fornisce informazioni su quali dati e funzionalità fornisce la _thing_ associata, quale protocollo utilizza per comunicare, come i dati sono codificati e strutturati, il meccanismo di controllo degli accessi utilizzato, assieme ad altri metadati pensati per essere letti e interpretati da umani e da sistemi automatici.[@wot]

Questo riconferma ciò che avevamo affermato poc'anzi: le "Thing Description" sono fondamentali per poter letteralmente parlare di una _thing_, per sapere che cos'è e che cosa fa.
Non solo, sono anche fondamentali per poter dare una semantica agli elementi che sono parte del mio sistema IoT.
Senza descrizioni, non avrei modo di far capire a nessuno, sia esso macchina o umano, quali sono le componenti del mio sistema, a che cosa servono e come interagiscono tra loro.
Per ciò che contengono, le descrizioni fungono infatti sia come meccanismo che permette l'interazione tra macchine, sia come documentazione utile agli sviluppatori del sistema IoT.[@wot-architecture]

L'unica alternativa all'approccio proposto è creare delle descrizioni per le mie _thing_ in un modo progettato ad hoc per la soluzione implementata.
Quest'ultima scelta presenta chiaramente tutti quei rischi già elencati all'inizio.
Ecco che allora lo strumento concettuale per creare una "Thing Description" diventa di assoluta importanza, dato che, senza di esso, non sarebbe possibile né costruirle, né costruirle in un modo standardizzato.

Per questi motivi, nel prossimo capitolo andremo ad approfondire il significato della prima parte della definizione della "Thing Description", così da poter capire qual è il modello concettuale di una _thing_.
Questo ci porterà a motivare perché l'ontologia delle descrizioni è costruita nel modo che vedremo.

