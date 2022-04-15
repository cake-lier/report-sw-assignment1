# Modello ontologico

## Che cos'è una Thing

Come già in parte anticipato nel capitolo precedente, una _thing_ ha per noi due aspetti costituenti: il suo comportamento e le sue "Interaction Affordances".
L'aspetto comportamentale comprende sia quello proprio della _thing_, sia quello legato alla corretta gestione delle "Interaction Affordances".
Queste rappresentano un modello di come un altro componente del sistema, uno che utilizza la _thing_, può interagire con quest'ultima attraverso dei metodi astratti, senza riferimenti a specifici protocolli di comunicazione o di codifica dei dati.
Per poter associare le "Interaction Affordances" a uno specifico protocollo di comunicazione supportato da questo progetto esistono i cosiddetti "Protocol Bindings", che non sono però di nostro interesse, così come non lo è la sua configurazione di sicurezza.
Questa rappresenta invece i meccanismi usati per controllare l'accesso alle "Interaction Affordances" e per gestire i metadati di sicurezza pubblici e privati associati. [@wot-architecture]

## Thing e interazioni

Tralasciando l'aspetto comportamentale, che è maggiormente legato alla sua implementazione e non alla sua definizione, è evidente che la componente più importante di una _thing_ è quella delle interazioni che è capace di avere.
Per questo motivo all'interno del progetto WoT è stato definito un "Interaction Model", capace di dare una definizione univoca all'astrazione di interazione utilizzata.
In questo modo, un'interazione può essere sia sufficientemente generale tale da poter essere utilizzata come modello per le sue concrete implementazioni associate alle varie _thing_, sia sufficientemente specifica tale da poter dare specifiche linee guida per la sua implementazione.

L'elemento fondante del modello di interazione che una _thing_ può avere con un altro componente sono le "Interaction Affordance", che possono essere di tre tipologie: "Proprietà", "Azioni" ed "Eventi".

Una "Proprietà" modella un'operazione capace di esporre lo stato di una _thing_, che dovrà perciò necessariamente poter essere letto, ma secondo WoT potrà anche essere modificato. Una proprietà può anche essere resa osservabile nel momento nel quale la _thing_ che la espone decide di effettuare l'operazione di "_push_" del suo stato ad ogni suo cambiamento a tutti coloro che si sono registrati per l'osservazione.
Possono essere modellati attraverso proprietà, ad esempio, un valore di un sensore o il risultato di una computazione, che possono essere unicamente letti, ma anche il valore di un attuatore dotato di uno stato interno o i parametri di una configurazione, che possono essere letti, ma anche scritti.

Un'"Azione" modella un'operazione che permette di invocare una funzione della _thing_. Il risultato può essere la manipolazione dello stato interno, non direttamente esposto, della _thing_, oppure la manipolazione dello stato esposto dalla _thing_, quindi una o più proprietà alla volta, seguendo una logica interna alla _thing_ stessa.
Un'azione può coinvolgere l'avvio di un processo per la modifica dello stato variamente complesso, che può durare nel tempo e che può avere anche dei risultati fisici.
Possono essere modellati come azioni, ad esempio, la riduzione della luminosità di una lampadina, che deve avvenire lungo un certo arco temporale, l'esecuzione di un flusso di controllo proprio della _thing_, che non deve essere pubblicamente esposto, oppure la stampa di un documento, che è un processo dalla durata non istantanea.

Un "Evento" modella una sorgente di eventi che effettua l'operazione di "_push_" dei dati in maniera asincrona dalla _thing_ alla componente che la usa.
I dati che vengono comunicati non sono perciò lo stato della _thing_, che abbiamo detto poter essere recuperato attraverso le sue proprietà, ma le transizioni di stato.
Un evento potrebbe verificarsi a seguito di condizioni che non sono direttamente manipolabili come proprietà.
Possono essere modellati come eventi, ad esempio, un allarme o il campionamento di una serie temporale di cui viene fatto il _push_ ad intervalli regolari.

Qualora il formato dei dati non possa essere interamente dedotto dal "Protocol Binding", è possibile per una qualsiasi "Interaction Affordance" contenere uno schema per i dati che descriva com'è strutturato lo stato esposto, per le proprietà, gli input e gli output, per le azioni, e i dati trasmessi e i messaggi di controllo della sottoscrizione, per gli eventi.

## Thing e risorse web

Una _thing_ è però anche una risorsa _web_, nello stesso modo in cui lo è la una pagina di un sito _web_.
In quanto tale, essa possiede anche tutte le interazioni di cui una risorsa è capace, ovvero quelle di navigazione, che permettono di raggiungerla tramite _link_ e da questa poi passare ad altre ad essa collegate sempre attraverso _link_.
Questi possono sì essere utilizzati dagli esseri umani seguendoli, ma anche dalle macchine, nel momento nel quale un _link_ è poi descritto dal tipo di relazione che lega le due risorse collegate e un insieme di attributi atti allo scopo.
Più in generale, esistono sul _web_ i cosiddetti "_hypermedia control_", ovvero dei comandi che sono parte della risorsa stessa a cui un _client_ sta accedendo e che vengono perciò dinamicamente generati da chi la fornisce e scoperti da chi la ottiene.
In questo modo chi fornisce la risorsa può tenere conto dello stato dell'applicazione di cui questa fa parte per capire quali di essi includere.
Un "_hypermedia control_" è per sua natura accessibile alle macchine e descrive come effettuare l'interazione stessa.
Questo può essere o un _link_, come già detto, ma anche un _web form_, un comando che rende possibile qualsiasi tipo di operazione.

Un _link_ permette ad un componente capace di sfruttare _thing_ di cambiare il contesto corrente con cui sta lavorando, così come ad esempio fa un _web browser_ impostando la nuova risorsa da visualizzare, oppure permette di includere risorse addizionali nel contesto corrente, dipendentemente dalla relazione tra il contesto e il _target_ del _link_.
Queste due operazioni sono effettuate attraverso la dereferenziazione dell'URI della risorsa _target_, ovvero seguendo il collegamento ed ottenendo la risorsa associata.
Un _link_ è costituito da un contesto, un tipo di relazione che lega il contesto con la risorsa _target_, il _target_ e, opzionalmente, degli attributi per il _target_.
In WoT, i _link_ sono perciò utilizzati per effettuare l'operazione di scoperta di altre _thing_, nonché per esprimere relazioni tra esse, come ad esempio di tipo gerarchico o funzionale, o tra _thing_ ed altre risorse _web_ più in generale.

Un _form_ invece permette di effettuare operazioni che vanno oltre la semplice dereferenziazione di un URI, come ad esempio la manipolazione dello stato della _thing_.
Questo è permesso attraverso il riempimento e l'invio del _form_ stesso al _target_ di invio.
Effettuare un'operazione di questo genere di norma richiede informazioni più dettagliate sul messaggio che viene inviato rispetto a quelle che un _link_ può portare con sè, come ad esempio il metodo utilizzato per effettuare la richiesta, i campi _header_ eccetera.
Un _form_ può essere visto come un _template_ per una richiesta, dove chi lo mette a disposizione fornisce delle parti di informazione già compilate, che dipendono dalla sua interfaccia e dal suo stato, e lascia delle parti vuote che devono essere riempite da chi lo riceve.
Secondo WoT, un _form_ è costituito da un contesto, un tipo di operazione, un _target_ di invio, un metodo per la richiesta di invio e, opzionalmente, i campi del _form_ stesso.
L'idea è che un _form_ possa effettuare un'operazione di un certo tipo sul suo contesto attraverso l'emissione di una richiesta con un certo metodo al _target_ di invio.
Sia il contesto che il _target_ del _form_ sono risorse e in particolar modo il _target_ deve implementare l'operazione che il _form_ esegue su di esso.
Il tipo dell'operazione è quello che ne identifica la semantica.
Il metodo della richiesta deve necessariamente essere uno di quelli che il protocollo utilizzato definisce.
I campi del _form_ sono opzionali perché vengono utilizzati per specificare ulteriormente il messaggio inviato come richiesta per la data operazione, influenzando non solo il contenuto del messaggio, ma anche gli _header_ della richiesta.
I campi potrebbero perciò dipendere dal protocollo utilizzato per l'invio, come ad esempio _header_ HTTP, opzioni CoAP, il "_media type_" del contenuto del form oppure informazioni sulla risposta attesa. [@wot-architecture]
