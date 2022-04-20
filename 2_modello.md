# Modello ontologico

## Che cos'è una Thing

Come già in parte anticipato nel capitolo precedente, una _thing_ ha due aspetti costituenti: il suo comportamento e le sue "Interaction Affordances".
Il primo comprende sia il comportamento proprio della _thing_, sia quello legato alla corretta gestione del secondo aspetto.
Le "Interaction Affordances" rappresentano un modello di come un altro componente del sistema, uno che utilizza la _thing_, può interagire con quest'ultima attraverso delle operazioni astratte, senza riferimenti a specifici protocolli di comunicazione o di codifica dei dati.
Per poter associare le "Interaction Affordances" a un'implementazione concreta, attraverso un protocollo di comunicazione supportato da WoT, esistono i cosiddetti "Protocol Bindings", che però non sono di interesse per questa analisi.
Allo stesso modo, non è di interesse la configurazione di sicurezza di una _thing_, ovvero i meccanismi usati per controllare l'accesso alle "Interaction Affordances" e per gestire i metadati di sicurezza pubblici e privati associati.

Una _thing_ è però anche una risorsa _web_, nello stesso modo in cui lo è una pagina di un sito _web_.
In quanto tale, essa è capace anche di tutte quelle interazioni di cui una risorsa è capace, ovvero quelle di navigazione, che permettono di raggiungerla tramite _link_ e da questa poi passare ad altre ad essa collegate attraverso altri _link_.
Più in generale, esistono per una risorsa _web_ i cosiddetti "_hypermedia control_", ovvero dei comandi che sono parte della risorsa stessa a cui un _client_ sta accedendo e che vengono perciò dinamicamente generati dal _server_ che la fornisce e programmaticamente scoperti da chi la ottiene.
In questo modo chi fornisce la risorsa può tenere conto dello stato dell'applicazione di cui la prima fa parte per capire quali _control_ includere.
Un "_hypermedia control_" ha per caratteristica il riuscire a descrivere come effettuare l'interazione di cui il comando è capace, e può perciò essere o un _link_, come già detto, ma anche un _web form_, un comando che rende possibile qualsiasi tipo di operazione. [@wot-architecture]

La definizione di "_link_" e "_form_" fa parte di un'ontologia parallela a quella di nostro interesse, perciò non entreremo ulteriormente nel dettaglio.
Per quanto ci riguarda, ci basta essere a conoscenza della loro esistenza, così come della configurazione di sicurezza di una _thing_, dato che saranno menzionati nell'ontologia che è invece lo scopo di questa relazione.

## Che cos'è un'Interaction Affordance

Tralasciando l'aspetto comportamentale, che è maggiormente legato alla sua implementazione e non alla sua definizione, è evidente come l'unica componente fondamentale di una _thing_ è quella che modella le interazioni che questa è capace di avere.
Per questo motivo, all'interno del progetto WoT è stato definito un "Interaction Model", un modello capace di dare una descrizione univoca dell'astrazione di interazione utilizzata.
Grazie all'uso di un "Interaction Model", una generica interazione è sia sufficientemente generale tale da poter essere utilizzata come modello per le sue concrete implementazioni associate alle _thing_, sia sufficientemente specifica tale da poter dare specifiche linee guida per la sua implementazione.

L'elemento fondante del modello di interazione che una _thing_ può avere con un altro componente sono quindi le "Interaction Affordances", che possono essere di tre tipologie: "Proprietà", "Azione" ed "Evento".

Una "Proprietà" modella un'operazione capace di esporre lo stato di una _thing_, che dovrà perciò necessariamente poter essere letto, ma potrà anche essere modificato, a seconda della specifica operazione.
Una proprietà può anche essere resa osservabile nel momento nel quale la _thing_ che la espone decide di effettuare l'operazione di "_push_" del suo stato ad ogni suo cambiamento a tutti coloro che si sono registrati per l'osservazione.
Possono essere modellate come proprietà, ad esempio, il valore di un sensore o il risultato di una computazione, i quali possono essere unicamente letti, ma anche il valore di un attuatore dotato di uno stato interno o i parametri di una configurazione, che possono essere sia letti che scritti.

Un'"Azione" modella un'operazione che permette di invocare una funzione della _thing_. 
Il suo risultato può essere la manipolazione dello stato interno della _thing_, quello cioè non direttamente esposto, oppure la manipolazione dello stato esposto, quindi una o più proprietà alla volta, seguendo una logica propria della _thing_ stessa.
Un'azione può consistere nell'avvio di un processo per la modifica dello stato più o meno complesso, che può durare nel tempo e che può avere anche dei risultati fisici.
Possono essere modellate come azioni, ad esempio, la riduzione della luminosità di una lampadina, che viene fatta durare per un certo tempo, l'esecuzione di un flusso di controllo proprio della _thing_, che non deve essere pubblicamente esposto, oppure la stampa di un documento, che ha una durata non istantanea.

Un "Evento" modella una sorgente di eventi che effettua l'operazione di "_push_" dei dati in maniera asincrona dalla _thing_ alla componente del sistema che la usa.
I dati che vengono comunicati non contengono lo stato della _thing_, che abbiamo detto poter essere recuperato attraverso le sue proprietà, ma le transizioni di stato.
Un evento potrebbe infatti verificarsi a seguito di condizioni che non sono direttamente manipolabili come proprietà.
Possono essere modellati come eventi, ad esempio, un allarme o il campionamento di una serie temporale di cui viene fatto il _push_ ad intervalli regolari.

Qualora il formato dei dati non possa essere interamente dedotto dal "Protocol Binding", è possibile per una qualsiasi "Interaction Affordance" contenere uno schema per i dati.
Questo descrive com'è strutturato lo stato esposto, per le proprietà, come sono strutturati gli input e gli output, per le azioni, e come sono strutturati i dati trasmessi e i messaggi di controllo della sottoscrizione, per gli eventi. [@wot-architecture]

## Modellare una Thing Description

Una "Thing Description" è descritta attraverso quattro ontologie di base:

* l'ontologia cosiddetta "_core_", che riflette l'"Interaction Model" presentato;
* l'ontologia "Data Schema", che contiene la definizione di un sottoinsieme di termini derivanti dallo standard "JSON Schema";
* l'ontologia "WoT Security", che identifica i meccanismi di sicurezza utilizzabili e i requisiti necessari alla loro configurazione;
* l'ontologia "Hypermedia Controls", che codifica i principi fondamentali della comunicazione "RESTful" attraverso i _link_ e i _form_ già presentati.

Quella di nostro interesse è solamente l'ontologia "_core_", il cui modello sarà l'unico ad essere qui di seguito illustrato.
La sua descrizione tramite diagramma delle classi UML è visibile in figura \ref{model}.
Le classi che fanno parte del modello sono solo quelle colorate in azzurro, mentre le altre fanno parte dei modelli delle altre tre ontologie.

![Diagramma UML che mostra le classi parte del modello dell'ontologia "_core_"\label{model}](images/td.png){ width=100% }

I tipi dei membri che descriveremo sono o classi del modello, o tipi standard di JSON - come String, Boolean, Array -, oppure ancora dei tipi né standard né spiegati altrove in questo documento, ma di semplice comprensione.
Questi sono "DateTime", che rappresenta un _timestamp_ contenente un riferimento ad una data e ad un'ora, e "URI", che fa riferimento ad un "Uniform Resource Identifier" serializzato in forma di stringa.
Le cardinalità di ciascun membro sono espresse secondo lo standard UML.

La prima classe per importanza è chiaramente "Thing".
Questa rappresenta una _thing_ così come l'abbiamo descritta, ovvero come astrazione di un'entità fisica o virtuale, eventualmente composta a sua volta da più _thing_.
Questa classe è definita dai seguenti membri:

```{=latex}
\begin{table}[H]
	\centering
	\begin{tabularx}{\textwidth}{|l|X|l|l|}
        \hline
		\textbf{Nome} & \textbf{Commento} & \textbf{Tipo} & \textbf{Cardinalità} \\ \hline
		@context & Permette di definire delle abbreviazioni per i termini utilizzati nella ``Thing Description'', è definito dallo standard JSON-LD. & URI | Array<String> & 1 \\ \hline
        @type & Permette di associare alla ``Thing'' dei tipi o etichette semantiche, è definito dallo standard JSON-LD. & String & 0..* \\ \hline
        id & Identificatore della ``Thing'' sotto forma di URI. & URI & 0..1 \\ \hline
        title & Il titolo della ``Thing'' in formato \textit{human-readable} in una lingua di default. & String & 1 \\ \hline
        titles & I titoli della ``Thing'' in formato \textit{human-readable} in più lingue alternative. & MultiLanguage & 0..1 \\ \hline
        description & La descrizione della ``Thing'', contenente informazioni aggiuntive, in formato \textit{human-readable} in una lingua di default. & String & 0..1 \\ \hline
        descriptions & Le descrizioni della ``Thing'', contenenti informazioni aggiuntive, in formato \textit{human-readable} in più lingue alternative. & MultiLanguage & 0..1 \\ \hline
        version & Fornisce informazioni sulla versione della ``Thing''. & VersionInfo & 0..1 \\ \hline
        created & Fornisce informazioni su quando la ``Thing'' è stata creata. & DateTime & 0..1 \\ \hline
        modified & Fornisce informazioni su quando la ``Thing'' è stata modificata l'ultima volta. & DateTime & 0..1 \\ \hline
        support & Fornisce informazioni sul manutentore della ``Thing'' sotto forma di URI, come ad esempio la sua \textit{e-mail}, il suo numero di telefono o una pagina \textit{web} a lui associata. & URI & 0..1 \\ \hline
        base & Definisce l'URI di base per tutti quelli relativi presenti all'interno della ``Thing Description'', senza alcun effetto su quelli definiti in ``@context''. & URI & 0..1 \\ \hline
        properties & Le ``PropertyAffordance'' che questa ``Thing'' possiede. & PropertyAffordance & 0..* \\ \hline
        actions & Le ``ActionAffordance'' che questa ``Thing'' possiede. & ActionAffordance & 0..* \\ \hline
        events & Le ``EventAffordance'' che questa ``Thing'' possiede. & EventAffordance & 0..* \\ \hline
	\end{tabularx}
\end{table}

\begin{table}[H]
	\centering
	\begin{tabularx}{\textwidth}{|l|X|l|l|}
        \hline
		\textbf{Nome} & \textbf{Commento} & \textbf{Tipo} & \textbf{Cardinalità} \\ \hline
        links & I ``Link'' alle risorse collegate a quella a cui questa ``Thing Description'' fa riferimento. & Link & 0..* \\ \hline
        forms & I ``Form'' che definiscono il come le operazioni di modifica di tutte le sue proprietà in una sola volta possono essere portate a termine. & Form & 0..* \\ \hline
        security & Uno o più nomi di configurazioni di sicurezza che devono essere soddisfatte per avere accesso alla ``Thing'', scelti tra quelli contenuti in ``securityDefinitions''. & String & 1..* \\ \hline
        securityDefinitions & Le definizioni delle configurazioni di sicurezza adottate, ma non necessariamente applicate. & SecurityScheme & 1..* \\ \hline
	\end{tabularx}
\end{table}
```

La seconda classe per importanza è "InteractionAffordance", che rappresenta una possibile modalità con la quale un componente interagisce con una "Thing".
Questa classe è definita dai seguenti membri:

```{=latex}
\begin{table}[H]
	\centering
	\begin{tabularx}{\textwidth}{|l|X|l|l|}
        \hline
		\textbf{Nome} & \textbf{Commento} & \textbf{Tipo} & \textbf{Cardinalità} \\ \hline
        @type & Permette di associare all'``InteractionAffordance'' dei tipi o etichette semantiche, è definito dallo standard JSON-LD. & String & 0..* \\ \hline
        title & Il titolo dell'``InteractionAffordance'' in formato \textit{human-readable} in una lingua di default. & String & 0..1 \\ \hline
        titles & I titoli dell'``InteractionAffordance'' in formato \textit{human-readable} in più lingue alternative. & MultiLanguage & 0..1 \\ \hline
        description & La descrizione dell'``InteractionAffordance'', contenente informazioni aggiuntive, in formato \textit{human-readable} in una lingua di default. & String & 0..1 \\ \hline
        descriptions & Le descrizioni dell'``InteractionAffordance'', contenenti informazioni aggiuntive, in formato \textit{human-readable} in più lingue alternative. & MultiLanguage & 0..1 \\ \hline
        forms & I ``Form'' che definiscono il come l'operazione associata può essere portata a termine. & Form & 1..* \\ \hline
        uriVariables & Le variabili \textit{template} contenute nell'URI associato a questa ``InteractionAffordance'', definite attraverso il formato dei dati che devono essere forniti in corrispondenza di quella variabile. & DataSchema & 0..* \\ \hline
	\end{tabularx}
\end{table}
```

Come ci si poteva aspettare, la classe "InteractionAffordance" ha poi tre sottoclassi: "PropertyAffordance", "ActionAffordance" ed "EventAffordance".
La classe "PropertyAffordance" possiede solamente il seguente membro:

```{=latex}
\begin{table}[H]
	\centering
	\begin{tabularx}{\textwidth}{|l|X|l|l|}
        \hline
		\textbf{Nome} & \textbf{Commento} & \textbf{Tipo} & \textbf{Cardinalità} \\ \hline
        observable & Indica qualora questa proprietà possa essere osservata in un qualche modo messo a disposizione dal protocollo utilizzato per implementare la ``Thing''. & Boolean & 0..1 \\ \hline
	\end{tabularx}
\end{table}
```

Questa classe è però anche sottoclasse della classe "DataSchema", la quale non verrà ulteriormente approfondita perché non fa parte di questa ontologia.
Non di meno, è importante sottolinearlo perché questo ci permette di fare un'osservazione importante.
Di fatto, una proprietà è di per sé una variabile, perciò il modello deve mettere a disposizione un modo per poter descrivere tutte le proprietà di una variabile, come il suo tipo, se è immutabile o meno, qual è l'insieme dei valori accettabili, eccetera.

La classe "ActionAffordance" possiede invece i membri:

```{=latex}
\begin{table}[H]
	\centering
	\begin{tabularx}{\textwidth}{|l|X|l|l|}
        \hline
		\textbf{Nome} & \textbf{Commento} & \textbf{Tipo} & \textbf{Cardinalità} \\ \hline
        input & Definisce il formato dei dati che costituiscono l'\textit{input} dell'``ActionAffordance''. & DataSchema & 0..1 \\ \hline
        output & Definisce il formato dei dati che costituiscono l'\textit{output} dell'``ActionAffordance''. & DataSchema & 0..1 \\ \hline
        safe & Indica se l'azione non è ``mutabile'' o meno, ovvero se non ha dei \textit{side effect} che modificano il suo stato interno o meno. Questo significa che se l'azione è ``sicura'' si può fare \textit{caching} del risultato. & Boolean & 0..1 \\ \hline
        idempotent & Indica se l'azione è ``deterministica'' o meno, ovvero se a fronte degli stessi \textit{input} fornisce gli stessi \textit{output} e può perciò essere chiamata più volte senza rischiare che il risultato cambi. & Boolean & 0..1 \\ \hline
	\end{tabularx}
\end{table}
```

Infine, la classe "EventAffordance" possiede i membri:

```{=latex}
\begin{table}[H]
	\centering
	\begin{tabularx}{\textwidth}{|l|X|l|l|}
        \hline
		\textbf{Nome} & \textbf{Commento} & \textbf{Tipo} & \textbf{Cardinalità} \\ \hline
        subscription & Definisce il formato dei dati che devono essere passati per effettuare la sottoscrizione all'evento, come eventuali filtri o formati di messaggio. & DataSchema & 0..1 \\ \hline
        data & Definisce il formato dei messaggi dell'istanza di evento che la ``Thing'' genera. & DataSchema & 0..1 \\ \hline
        cancellation & Definisce il formato dei dati che devono essere passati per effettuare la cancellazione di una sottoscrizione precedentemente contratta. & DataSchema & 0..1 \\ \hline
	\end{tabularx}
\end{table}
```

Concludiamo dettagliando le due classi "accessorie" al modello, che sono utili per completarne la descrizione, ma che non sono di particolare interesse, tant'è che non saranno presenti nell'ontologia.
Queste due classi sono "VersionInfo" e "MultiLanguage".
La prima è utile per fornire informazioni di versione sulla "Thing Description" ed è costituita da un solo membro: "instance".
Questo campo contiene l'indicatore di versione della risorsa, come ad esempio la versione secondo lo schema "Semantic Versioning".
La seconda classe invece rappresenta un dizionario che associa le varie lingue alle traduzioni in quelle stesse lingue di uno stesso testo.
È perciò utile per includere stringhe internazionalizzate all'interno della "Thing Description" oltre a quelle scritte nella lingua scelta come default. 
Questo è ad esempio il caso di "title" e "description" di una "Thing" o di una "InteractionAffordance", che possono essere quindi mostrate sia nella lingua di default che in tutte le altre lingue supportate. [@wot-td]
