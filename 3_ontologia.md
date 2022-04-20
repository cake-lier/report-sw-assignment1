# Ontologia

## Struttura dell'ontologia

L'ontologia "_core_" delle "Thing Description" è costituita da 6 classi, 30 proprietà e 18 istanze. 
Le 30 proprietà sono suddivise in 16 "_object properties_", 8 "_datatype properties_" e 6 "_annotation properties_". [@td-ontology]
Il seguito del capitolo sarà dedicato a descrivere tutte le classi, le proprietà e le istanze in dettaglio.
È bene però sottolineare come l'ontologia contenga anche elementi che fanno riferimento alla prossima versione del progetto "Web Of Things", che però non è ancora stata rilasciata perché non ha ancora raggiunto lo status di "W3C Recommendation".
Si è comunque deciso di commentare la versione più recente dell'ontologia perché è quella attualmente disponibile _online_ e perché contiene tutta una serie di concetti che non erano presenti nella vecchia versione, ma che erano già presenti nel modello di riferimento.
Si è perciò ritenuto che sarebbe stata una scelta migliore quella di spendere più tempo nel descrivere l'ontologia, aggiungendo anche dettagli che non corrispondono esattamente con il modello, pur di coprire l'intero modello ontologico di riferimento.

Per prima cosa, si vuole evidenziare il fatto che questa ontologia si serve di altre nella sua definizione.
Essa utilizza le tre ontologie definite dallo stesso standard che abbiamo indicato come necessarie per la stesura di una "Thing Description", ovvero "Data Schema", "WoT Security" e "Hypermedia Controls".
Queste sono rappresentate rispettivamente dai _namespace_ "jsonschema", "wotsec" e "hctl".
Oltre a queste, l'ontologia _core_ si appoggia anche a "Schema.org", rappresentata dal namespace "schema", e "Dublin Core", rappresentata invece da "dcterms".
La prima è introdotta per utilizzare una serie di tipi di dato di base come "Text" e "Boolean", mentre la seconda per importare le proprietà "title" e "description".

### Classi

```{=latex}
\begin{table}[H]
	\centering
	\begin{tabularx}{\textwidth}{|l|X|l|}
        \hline
		\textbf{Nome} & \textbf{Commento} & \textbf{È sottoclasse di} \\ \hline
		Thing & Astrazione di un'entità fisica o virtuale i cui metadati e le cui interfacce sono descritti da una ``Thing Description''. Un entità virtuale può essere la composizione di una o più ``Thing''. & N/A \\ \hline
	\end{tabularx}
\end{table}

\begin{table}[H]
	\centering
	\begin{tabularx}{\textwidth}{|l|X|l|}
        \hline
		\textbf{Nome} & \textbf{Commento} & \textbf{È sottoclasse di} \\ \hline
        InteractionAffordance & Quei metadati di una ``Thing'' che indicano le possibili scelte che hanno i componenti che sfruttano la ``Thing'' nell'usarla, suggerendo loro come interagire con la ``Thing''. & N/A \\ \hline
        PropertyAffordance & Una ``InteractionAffordance'' che espone lo stato di una ``Thing''. Questo stato può essere ottenuto, cioè letto, e/o aggiornato, cioè scritto. Una ``Thing'' può decidere di rendere una ``PropertyAffordance'' osservabile effettuando il \textit{push} del suo nuovo stato dopo ogni modifica. & InteractionAffordance \\ \hline
        ActionAffordance & Una ``InteractionAffordance'' che permette di invocare una funzione della ``Thing'', che può manipolare il suo stato o attivare un processo su di essa. & InteractionAffordance \\ \hline
        EventAffordance & Una ``InteractionAffordance'' che descrive una sorgente di eventi, che in maniera asincrona fa \textit{push} dei dati di questi eventi ai componenti che utilizzano la ``Thing''. & InteractionAffordance \\ \hline
        OperationType & Enumerazione dei tipi di operazione necessari per implementare l'``Interaction Model'' di WoT. & N/A \\ \hline
	\end{tabularx}
\end{table}
```

### Proprietà "object"

```{=latex}
\begin{table}[H]
	\centering
	\begin{tabularx}{\linewidth}{|>{\hspace{0pt}}p{0.2225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|}
        \hline
		\textbf{Nome} & \textbf{Domain} & \textbf{Range} & \textbf{È sottoproprietà di} \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{\textbf{Commento}} \\ \hline
		hasInteractionAffordance & Thing & InteractionAffordance & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Specifica una ``InteractionAffordance'' per interagire con una ``Thing''.} \\ \hline
        hasPropertyAffordance & N/A & PropertyAffordance & hasInteractionAffordance \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Specifica una ``InteractionAffordance'' di tipo ``Proprietà'' per interagire con una ``Thing''.} \\ \hline
        hasActionAffordance & N/A & ActionAffordance & hasInteractionAffordance \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Specifica una ``InteractionAffordance'' di tipo ``Azione'' per interagire con una ``Thing''.} \\ \hline
        hasEventAffordance & N/A & EventAffordance & hasInteractionAffordance \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Specifica una ``InteractionAffordance'' di tipo ``Evento'' per interagire con una ``Thing''.} \\ \hline
    \end{tabularx}
\end{table}

\begin{table}[H]
	\centering
	\begin{tabularx}{\linewidth}{|>{\hspace{0pt}}p{0.2225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|}
        \hline
		\textbf{Nome} & \textbf{Domain} & \textbf{Range} & \textbf{È sottoproprietà di} \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{\textbf{Commento}} \\ \hline
        hasForm & Thing, InteractionAffordance & hctl:Form & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Specifica un \textit{hypermedia control} di tipo \textit{form} che descrive come um'operazione può essere compiuta.} \\ \hline
        hasLink & N/A & hctl:Link & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Specifica un \textit{link} verso una risorsa arbitraria che è in relazione con la ``Thing Description'' che si sta specificando.} \\ \hline
        hasUriTemplateSchema & InteractionAffordance & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce variabili \textit{template} per l'URI di una risorsa come specifiche di schema. Non possono essere nè specifiche di schema per JSON object nè per JSON array.} \\ \hline
        hasInputSchema & ActionAffordance & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce lo schema per i dati di \textit{input} di un'``ActionAffordance''.} \\ \hline
        hasOutputSchema & ActionAffordance & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce lo schema dati per i dati di \textit{output} di un'``ActionAffordance''.} \\ \hline
        hasSubscriptionSchema & EventAffordance & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce lo schema dei dati che devono essere passati all'atto della sottoscrizione ad un'``EventAffordance''.} \\ \hline
        hasNotificationSchema & EventAffordance & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce lo schema dei dati delle istanze di evento che di cui la ``Thing'' effettua il \textit{push} attraverso un'``EventAffordance''.} \\ \hline
        hasNotificationResponseSchema & EventAffordance & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce lo schema dei dati per i messaggi di risposta alle istanze di evento di cui una ``Thing'' effettua il \textit{push} attraverso una ``EventAffordance''.} \\ \hline
        hasCancellationSchema & EventAffordance & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce lo schema dei dati che devono essere passati alla ``Thing'' per cancellare una sottoscrizione ad una ``EventAffordance''.} \\ \hline
        hasSecurityConfiguration & Thing, hctl:Form & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce l'utilizzo di una certa configurazione di sicurezza, ovvero uno schema di sicurezza applicato ad una o più ``InteractionAffordance''.} \\ \hline
        definesSecurityScheme & Thing & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Indica la definizione di uno schema di sicurezza, che può essere utilizzato per garantire un accesso sicuro ad una o più ``InteractionAffordance''.} \\ \hline
    \end{tabularx}
\end{table}

\begin{table}[H]
	\centering
	\begin{tabularx}{\linewidth}{|>{\hspace{0pt}}p{0.2225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|}
        \hline
		\textbf{Nome} & \textbf{Domain} & \textbf{Range} & \textbf{È sottoproprietà di} \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{\textbf{Commento}} \\ \hline
        hasConfigurationInstance & wotsec:SecurityScheme & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce l'associazione tra uno schema di sicurezza e la sua configurazione.} \\ \hline
    \end{tabularx}
\end{table}
```

### Proprietà "datatype"

```{=latex}
\begin{table}[H]
	\centering
	\begin{tabularx}{\linewidth}{|>{\hspace{0pt}}p{0.2225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|}
        \hline
		\textbf{Nome} & \textbf{Domain} & \textbf{Range} & \textbf{È sottoproprietà di} \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{\textbf{Commento}} \\ \hline
        isSafe & ActionAffordance & schema:Boolean & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Indica se un'``ActionAffordance'' non è ``mutabile'' o meno, cioè se non modifica lo stato interno della ``Thing''.} \\ \hline
        isIdempotent & ActionAffordance & schema:Boolean & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Indica se un'``ActionAffordance'' è ``deterministica'' o meno, ovvero, se invocata più volte, a fronte dello stesso \textit{input} fornisce sempre lo stesso \textit{output}.} \\ \hline
        isObservable & PropertyAffordance & schema:Boolean & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Indica se per una certa ``PropertyAffordance'' sono supportate le operazioni di ``observeProperty'' e ``unobserveProperty'', ovvero se può essere oggetto di osservazione o meno.} \\ \hline
        name & InteractionAffordance & schema:Text & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Proprietà per l'indicizzazione utilizzabile per salvare il nome dell'entità quando questa viene serializzata in una ``index map'' di JSON-LD.} \\ \hline
        title & Thing, InteractionAffordance, jsonschema:DataSchema & schema:Text & dcterms:title \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Titolo dell'entità.} \\ \hline
        titleInLanguage & Thing, InteractionAffordance, jsonschema:DataSchema & schema:Text & dcterms:title \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Titolo dell'entità con associata un'annotazione linguistica all'oggetto della tripla che ha questa proprietà per predicato.} \\ \hline
        description & Thing, InteractionAffordance, wotsec:SecurityScheme, jsonschema:DataSchema & schema:Text & dcterms:description \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Descrizione dell'entità.} \\ \hline
    \end{tabularx}
\end{table}

\begin{table}[H]
	\centering
	\begin{tabularx}{\linewidth}{|>{\hspace{0pt}}p{0.2225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|}
        \hline
		\textbf{Nome} & \textbf{Domain} & \textbf{Range} & \textbf{È sottoproprietà di} \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{\textbf{Commento}} \\ \hline
        descriptionInLanguage & Thing, InteractionAffordance, wotsec:SecurityScheme, jsonschema:DataSchema & schema:Text & dcterms:description \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Descrizione dell'entità con associata un'annotazione linguistica all'oggetto della tripla che ha questa proprietà per predicato.} \\ \hline 
    \end{tabularx}
\end{table}
```

### Istanze

```{=latex}
\begin{table}[H]
	\centering
	\begin{tabularx}{\textwidth}{|l|X|l|}
        \hline
		\textbf{Nome} & \textbf{Commento} & \textbf{È istanza di classe} \\ \hline
        readProperty & Si usa per leggere il valore di una proprietà. & OperationType \\ \hline
        writeProperty & Si usa per scrivere il valore di una proprietà. & OperationType \\ \hline
        observeProperty & Si usa per osservare il valore di una proprietà. & OperationType \\ \hline
        unobserveProperty & Si usa per cancellare l'osservazione del valore di una proprietà. & OperationType \\ \hline
        readMultipleProperties & Si usa per leggere il valore di più proprietà alla volta. & OperationType \\ \hline
        writeMultipleProperties & Si usa per scrivere il valore di più proprietà alla volta. & OperationType \\ \hline
        readAllProperties & Si usa per leggere il valore di tutte le proprietà. & OperationType \\ \hline
        writeAllProperties & Si usa per scrivere il valore di tutte le proprietà. & OperationType \\ \hline
        observeAllProperties & Si usa per osservare il valore di tutte le proprietà. & OperationType \\ \hline
        unobserveAllProperties & Si usa per cancellare l'osservazione del valore di tutte le proprietà. & OperationType \\ \hline
        invokeAction & Si usa per invocare un'azione. & OperationType \\ \hline
        queryAction & Si usa per controllare lo stato di un'azione. & OperationType \\ \hline
        cancelAction & Si usa per cancellare un'azione. & OperationType \\ \hline
        queryAllActions & Si usa per controllare lo stato di tutte le azioni. & OperationType \\ \hline
        subscribeEvent & Si usa per effettuare la sottoscrizione ad un evento di un certo tipo. & OperationType \\ \hline
        unsubscribeEvent & Si usa per cancellare la sottoscrizione ad un evento di un certo tipo. & OperationType \\ \hline
        subscribeAllEvents & Si usa per effettuare la sottoscrizione a tutti i tipi di evento. & OperationType \\ \hline
        unsubscribeAllEvents & Si usa per cancellare la sottoscrizione a tutti i tipi di evento. & OperationType \\ \hline
	\end{tabularx}
\end{table}
```

### Proprietà "annotation"

```{=latex}
\begin{table}[H]
	\centering
	\begin{tabularx}{\textwidth}{|l|X|}
        \hline
		\textbf{Nome} & \textbf{Commento} \\ \hline
        supportContact & Fornisce informazioni sul manutentore della ``Thing Description''. \\ \hline
        followsProfile & Indica i meccanismi ``WoT Profile'' che la ``Thing Description'' segue e così l'implementazione di ``Thing'' associata. \\ \hline
        baseURI & Definisce l'URI base per tutti gli URI relativi contenuti nella ``Thing Description''. \\ \hline
        versionInfo & Fornisce informazioni sulla versione. \\ \hline
        instance & Fornisce un identificatore di versione per questa istanza di ``Thing Description''. \\ \hline
        model & Fornisce un identificatore di versione per il modello della ``Thing'' sottostante, quello associato alla ``Thing'' descritta da questa ``Thing Description''. \\ \hline
	\end{tabularx}
\end{table}
```

## Esempi di utilizzo

Il seguente esempio è ispirato a quello contenuto nella descrizione ufficiale dell'ontologia [@td-ontology].
È nel formato JSON-LD perché lo standard richiede che le "Thing Description" possano essere serializzate in almeno questo formato.

L'esempio rappresenta una lampada _smart_, denominata "MyLampThing", che permette di ottenere il suo stato, cioè se è accesa o spenta, sotto forma di stringa testuale, attraverso un'operazione di lettura di proprietà, e di farla passare da uno stato all'altro, come se utilizzassimo il suo interruttore.
La lampada permette anche di registrarsi per ricevere notifiche che riguardano l'evento di surriscaldamento, sotto forma di stringa testuale, attraverso il meccanismo di "_long polling_", ovvero il meccanismo di richiesta continuativa e periodica dei dati dell'evento.
Per ognuna di queste interazioni esiste un URL corrispondente utilizzabile per effettuare l'operazione associata o, per meglio dire, è messo a disposizione un _form_ di cui è noto il _target_ che abilita l'esecuzione dell'operazione corrispondente alla specifica interazione.

\newpage

    {
        "@context": {
            "https://www.w3.org/2019/wot/td/v1",
            { "@base": "http://example.org/MyLampThing/" }
        },
        "id": "urn:dev:ops:32473-WoTLamp-1234",
        "title": "MyLampThing",
        "description" : "MyLampThing uses JSON serialization",
        "securityDefinitions": { "nosec_sc": { "scheme": "nosec" } },
        "security": ["nosec_sc"],
        "properties": {
            "status": {
                "description": "Shows the current status of the lamp",
                "type": "string",
                "forms": [{ 
                    "op": "readproperty",
                    "href": "https://mylamp.example.com/status" 
                }]
            }
        },
        "actions": {
            "toggle": {
                "description": "Turn on or off the lamp",
                "forms": [{ "href": "https://mylamp.example.com/toggle" }]
            }
        },
        "events": {
            "overheating": {
                "description": "Lamp reaches a critical temperature (overheating)",
                "data": { "type": "string" },
                "forms": [{
                    "href": "https://mylamp.example.com/oh",
                    "subprotocol": "longpoll"
                }]
            }
        }
    }

Lo stesso esempio è quindi presentato nuovamente, ma nel formato Turtle, più familiare e più facilmente comprensibile.
Questo secondo esempio mette più facilmente in evidenza i legami che esistono tra questo e l'ontologia presentata, ancor di più che l'esempio in JSON-LD.

\newpage

    @prefix td: <https://www.w3.org/2019/wot/td>.
    @prefix hctl: <https://www.w3.org/2019/wot/hypermedia>.
    @prefix wotsec: <https://www.w3.org/2019/wot/security>.
    @prefix jsonschema: <https://www.w3.org/2019/wot/json-schema>.

    <urn:dev:ops:32473-WoTLamp-1234>
        td:title "MyLampThing";
        td:description "MyLampThing uses JSON serialization";
        td:definesSecurityScheme [
            a wotsec:NoSecurityScheme;
            td:hasConfigurationInstance <http://example.org/MyLampThing/nosec_sc>
        ];
        td:hasSecurityConfiguration <http://example.org/MyLampThing/nosec_sc>;
        td:hasPropertyAffordance [
            td:name "status";
            td:description "Shows the current status of the lamp";
            a jsonschema:StringSchema;
            td:hasForm [ 
                hctl:hasOperationType td:readProperty;
                hctl:hasTarget "https://mylamp.example.com/status" 
            ]
        ];
        td:hasActionAffordance [
            td:name "toggle";
            td:description "Turn on or off the lamp";
            td:hasForm [ hctl:hasTarget "https://mylamp.example.com/toggle" ]
        ];
        td:hasEventAffordance [
            td:name "overheating";
            td:description "Lamp reaches a critical temperature (overheating)";
            td:hasNotificationSchema [ a jsonschema:StringSchema ];
            td:hasForm [
                hctl:forSubProtocol "longpoll";
                hctl:hasTarget "https://mylamp.example.com/oh"
            ];
        ].

## Allineamenti con altre ontologie

L'ontologia _core_ condivide alcune similarità con altre.
Essa infatti è stata costruita in relazione ad un'altra ontologia preesistente il cui dominio sono i sensori, ovvero "Semantic Sensor Network" [@ssn].
I vincoli che legano "Thing" alle entità presenti in SSN sono i seguenti:

* "Thing" può essere sottoclasse di "Sensor", cioè un qualcosa che risponde ad uno stimolo proveniente dall'ambiente esterno o a combinazioni di osservazioni precedenti per generare un risultato;
* "Thing" può essere sottoclasse di "Actuator", cioè un dispositivo che implementa o viene usato per effettuare una procedura capace di cambiare lo stato dell'ambiente esterno;
* "Thing" può essere sottoclasse di "Platform", perciò un'aggregazione di altri "Sensor", "Actuator" e "Platform";
* "Thing" può essere sottoclasse di "FeatureOfInterest", cioè quel qualcosa le cui proprietà stanno venendo osservate da un "Sensor" oppure modificate da un "Actuator";
* Se una "Thing" è sottoclasse di "FeatureOfInterest", allora il range della proprietà "hasProperty" è ristretto a quelle entità le quali possiedono la proprietà "isObservedBy", la quale ha a sua volta il proprio range ristretto ad entità sottoclassi di "Sensor", e a quelle le quali possiedono la proprietà "isActedOnBy", la quale ha a sua volta il proprio range ristretto ad entità sottoclassi di "Actuator". Questo perché, per definizione, una "FeatureOfInterest" possiede una o più proprietà osservate da un "Sensor" o modificate da un "Actuator";
* Se una "Thing" è sottoclasse di "Sensor", allora per essa vale la proprietà "observes" e il range di quest'ultima è ristretto alle entità sottoclassi di "ObservableProperty". Questo perché, data la definizione di "Sensor", una "Thing" in quanto "Sensor" deve osservare una proprietà osservabile.
* Se una "Thing" è sottoclasse di "Actuator", allora per essa vale la proprietà "actsOnProperty" e il range di quest'ultima è ristretto alle entità sottoclassi di "ActuatableProperty". Questo perché, data la definizione di "Actuator", una "Thing" in quanto "Actuator" deve poter agire su una proprietà su cui è possibile farlo.
* Se una "Thing" è sottoclasse di "Platform", allora per essa vale la proprietà "hosts", il cui range sarà ristretto alle entità sottoclassi di "Sensor", per cui è vera la proprietà "observes", il cui range è a sua volta ristretto ad entità sottoclassi di "ObservableProperty", e alle entità sottoclassi di "Actuator", per cui è vera la proprietà "actsOnProperty", il cui range è a sua volta ristretto ad entità sottoclassi di "ActuatableProperty". Questo perché, data la definizione di "Platform", una "Thing" che è anche una "Platform" deve necessariamente ospitare altri componenti di tipo "Sensor" o "Actuator".

I vincoli che invece legano "InteractionAffordance" e le sue sottoclassi alle entità presenti in SSN sono i seguenti:

* Se una "PropertyAffordance" possiede la proprietà "hasForm" e questa ha per oggetto un'entità la cui proprietà "hasOperationType" ha valore "readProperty", allora deve anche possedere la proprietà "forProperty", il cui range deve essere ristretto alle "ObservableProperty". Questo perché una "PropertyAffordance" così definita è legata ad una proprietà che può essere letta, cioè osservata, perciò questo va indicato anche secondo la semantica di SSN.
* Se una "PropertyAffordance" possiede la proprietà "hasForm" e questa ha per oggetto un'entità la cui proprietà "hasOperationType" ha valore "writeProperty", allora deve anche possedere la proprietà "forProperty", il cui range deve essere ristretto alle "ActuatableProperty". Questo perché una "PropertyAffordance" così definita è legata ad una proprietà che può essere scritta, cioè modificata, perciò questo va indicato anche secondo la semantica di SSN.
* Se una "ActionAffordance" possiede la proprietà "forProperty", il range di quest'ultima deve essere ristretto alle "ActuatableProperty". Questo deve essere vero perché un'azione è sempre compiuta su di una proprietà della "Thing" che può essere modificata, perciò questa non può che essere una "ActuatableProperty".
* Se una "EventAffordance" possiede la proprietà "forProperty", il range di quest'ultima deve essere ristretto alle "ObservableProperty". Questo deve essere vero perché una sorgente di eventi può fare riferimento solamente ad una proprietà della "Thing" che può essere osservata, perciò questa non può che essere una "ObservableProperty".

Non solo, esistono anche dei legami tra questa ontologia e quella di "Schema.org", in particolar modo nella sua parte inerente alle interazioni. 
Non a caso, nell'"Interaction Model" di una "Thing Description" si parla di interazioni tra le "Thing" ed altri componenti, che sono particolari tipi di azioni.
I vincoli che legano perciò "InteractionAffordance" con le entità presenti nell'ontologia di "Schema.org" sono i seguenti:

* Una "InteractionAffordance" è sottoclasse di "Action" e, se possiede la proprietà "actionStatus", allora il valore di questa proprietà sarà "PotentialActionStatus". Questo perché le interazioni presenti in una "Thing Description" sono, appunto, la descrizione delle possibili azioni che possono essere intraprese, non sono azioni in corso o compiute.
* La proprietà "hasInteractionAffordance" è sottoproprietà di "potentialAction". Questo è un diretto risultato della considerazione precedente: se una "InteractionAffordance" è sempre una "PotentialAction", allora se una "Thing" possiede una "InteractionAffordance" possiede anche un'azione che può essere potenzialmente compiuta.
