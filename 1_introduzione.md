# Introduzione

## Web of Things

Il progetto "Web of Things" nasce per iniziativa di un gruppo di lavoro del "World Wide Web Consortium", "W3C" in breve, per risolvere le problematiche inerenti allo sviluppo di progetti che riguardano l'"Internet of Things".
Il panorama di tecnologie disponibili per lo sviluppo sono innumerevoli, le quali consistono in svariati sistemi e servizi offerti da fornitori diversi tra di loro.
Le differenze sono a tutti i livelli: da quelli più bassi che coinvolgono protocolli di comunicazione, a quelli più alti che riguardano invece i modelli dati e i requisiti di sicurezza.
Nello sviluppo di applicazioni IoT serve perciò un notevole sforzo per casi d'uso specifici, senza possibilità di generalizzare.
Questo rende le applicazioni difficili da estendere, manutenere e riusare.

"Web of Things" si prefigge di fornire un insieme di elementi tecnologici di base standardizzati per semplificare lo sviluppo di queste applicazioni.
Questi elementi seguono il ben noto approccio utilizzato per costruire il _web_, ormai chiaramente rivelatosi di successo, capace di fornire maggiore flessibilità ed interoperabiità, nonché riuso di strumenti e standard consolidati.
Il successo del progetto porterà ad uno sperabile superamento della frammentazione del panorama IoT, portando ad un maggiore sviluppo di un settore già di forte interesse tecnologico e commerciale.[@wot]

## Things e Thing Descriptions

Al centro del progetto "WoT", così come nel campo dell'IoT, c'è il concetto di "_thing_", di oggetto.
Secondo la definizione data all'interno del progetto stesso, una _thing_ è:

> An abstraction of a physical or a virtual entity whose metadata and interfaces are described by a "WoT Thing Description", whereas a virtual entity is the composition of one or more Things.

> Un'astrazione di una entità fisica o virtuale i cui metadati e le cui interfacce sono descritte da una "WoT Thing Description" e un'entità virtuale è la composizione di una o più "things".

È evidente perciò che una _thing_ può essere qualsiasi cosa, fisica o virtuale, e nel caso fosse virtuale può essere a sua volta composizione di più _thing_, ad esempio potrebbe essere una stanza dotata di _smart objects_.
Il requisito fondamentale, però, che rende una _thing_ tale è la possibilità di essere descritta attraverso una "Thing Description".[@wot-architecture]
