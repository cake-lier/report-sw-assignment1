# Modello ontologico

## Che cos'è una Thing

Come già in parte anticipato nel capitolo precedente, una _thing_ ha per noi tre aspetti costituenti: il suo comportamento, le sue "Interaction Affordances" e la sua configurazione di sicurezza. 
L'aspetto comportamentale comprende sia quello proprio della _thing_, sia quello legato alla corretta gestione delle "Interaction Affordances".
Queste rappresentano un modello di come un altro componente del sistema, uno che utilizza la _thing_, può interagire con quest'ultima attraverso dei metodi astratti, senza riferimenti a specifici protocolli di comunicazione o di codifica dei dati.
Per poter associare le "Interaction Affordances" a uno specifico protocollo di comunicazione supportato da questo progetto esistono i cosiddetti "Protocol Bindings", che non sono però di nostro interesse.
La configurazione di sicurezza rappresenta invece i meccanismi usati per controllare l'accesso alle "Interaction Affordances" e per gestire i metadati di sicurezza pubblici e privati associati. 

## Che cos'è un'interazione

Tralasciando l'aspetto comportamentale, che è maggiormente legato alla sua implementazione e non alla sua definizione, è evidente che la componente più importante di una _thing_ è quella delle interazioni che è capace di avere.
Per questo motivo all'interno del progetto WoT è stato introdotto un "Interaction Model", capace di dare una definizione univoca all'astrazione di interazione utilizzata.
In questo modo, un'interazione può essere sia sufficientemente generale tale da poter essere utilizzata come modello per le sue concrete implementazioni associate alle varie _thing_, sia sufficientemente specifica tale da poter dare specifiche linee guida per la sua implementazione.

Una qualsiasi _thing_ è innanzitutto una risorsa web.
Come tale, essa possiede tutte le interazioni proprie delle risorse, cioè quelle di navigazione che permettono di raggiungerla tramite dei _link_.
Oltre a queste, si aggiungono le "Interaction Affordance" già indicate, che sono di tre tipologie: "Proprietà", "Azioni" ed "Eventi".

Una "Proprietà" modella un'operazione capace di esporre lo stato di una _thing_, che dovrà perciò necessariamente poter essere letto, ma secondo WoT potrà anche essere modificato. Una proprietà può anche essere resa osservabile nel momento nel quale la _thing_ che la espone decide di effettuare l'operazione di "_push_" del suo stato ad ogni suo cambiamento a tutti coloro che si sono registrati per l'osservazione.
Possono essere modellati attraverso proprietà, ad esempio, un valore di un sensore o il risultato di una computazione, che possono essere unicamente letti, ma anche il valore di un attuatore dotato di uno stato interno o i parametri di una configurazione, che possono essere letti, ma anche scritti.

Un'"Azione" modella un'operazione che permette di invocare una funzione della _thing_. Il risultato può essere la manipolazione dello stato interno, non direttamente esposto, della _thing_, oppure la manipolazione dello stato esposto dalla _thing_, quindi una o più proprietà alla volta, seguendo una logica interna alla _thing_ stessa.
Un'azione può coinvolgere l'avvio di un processo per la modifica dello stato variamente complesso, che può durare nel tempo e che può avere anche dei risultati fisici.
Possono essere modellati come azioni, ad esempio, la riduzione della luminosità di una lampadina, che deve avvenire lungo un certo arco temporale, l'esecuzione di un flusso di controllo proprio della _thing_, che non deve essere pubblicamente esposto, oppure la stampa di un documento, che è un processo dalla durata non istantanea.

Un evento modella una sorgente di eventi che effettua l'operazione di "_push_" dei dati in maniera asincrona dalla _thing_ alla componente che la usa.
I dati che vengono comunicati non sono perciò lo stato della _thing_, che abbiamo detto poter essere recuperato attraverso le sue proprietà, ma le transizioni di stato.
Un evento potrebbe verificarsi a seguito di condizioni che non sono direttamente manipolabili come proprietà.
Possono essere modellati come eventi, ad esempio, un allarme o il campionamento di una serie temporale di cui viene fatto il _push_ ad intervalli regolari.

