# Ontologia

## Struttura dell'ontologia

L'ontologia "_core_" di una "Thing Description" è costituita da 6 classi, 24 proprietà e 18 istanze. [@td-ontology]
Nel seguito del capitolo queste verranno presentate in maggior dettaglio.

### Classi

```{=latex}
\begin{table}[H]
	\centering
	\begin{tabularx}{\textwidth}{|l|X|l|}
        \hline
		\textbf{Nome} & \textbf{Commento} & \textbf{È sottoclasse di} \\ \hline
		Thing & L'astrazione di un'entità fisica o virtuale i cui metadati e le cui interfacce sono descritti da una ``Thing Description''. Un entità virtuale può essere la composizione di una o più ``Thing''. & N/A \\ \hline
        InteractionAffordance & I metadati di una ``Thing'' che indicano le possibili scelte che hanno i componenti che sfruttano la ``Thing'' nell'usarla, suggerendo loro come interagire con la ``Thing''. & N/A \\ \hline
        PropertyAffordance & Una ``InteractionAffordance'' che espone lo stato di una ``Thing''. Questo stato può essere ottenuto, cioè letto, e/o aggiornato, cioè scritto. Una ``Thing'' può decidere di rendere una ``PropertyAffordance'' osservabile effettuando il \textit{push} del suo nuovo stato dopo ogni modifica. & InteractionAffordance \\ \hline
        ActionAffordance & Una ``InteractionAffordance'' che permette di invocare una funzione della ``Thing'', che può manipolare il suo stato o attivare un processo su di essa. & InteractionAffordance \\ \hline
        EventAffordance & Una ``InteractionAffordance'' che descrive una sorgente di eventi, che in maniera asincrona fa \textit{push} dei dati di questi eventi ai componenti che utilizzano la ``Thing''. & InteractionAffordance \\ \hline
	\end{tabularx}
\end{table}

\begin{table}[H]
	\centering
	\begin{tabularx}{\textwidth}{|l|X|l|}
        \hline
		\textbf{Nome} & \textbf{Commento} & \textbf{È sottoclasse di} \\ \hline
        OperationType & Enumerazione di tipi di operazione ben noti necessari per implementare l'``Interaction Model'' di WoT. & N/A \\ \hline
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
        & \multicolumn{3}{p{0.675\linewidth}|}{Specifica una ''InteractionAffordance'' per interagire con una ``Thing''.} \\ \hline
        hasPropertyAffordance & N/A & PropertyAffordance & hasInteractionAffordance \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Specifica una ``InteractionAffordance'' per interagire con una ``Thing'' di tipo ``Proprietà''.} \\ \hline
        hasActionAffordance & N/A & ActionAffordance & hasInteractionAffordance \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Specifica una ``InteractionAffordance'' per interagire con una ``Thing'' di tipo ``Azione''.} \\ \hline
        hasEventAffordance & N/A & EventAffordance & hasInteractionAffordance \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Specifica una ``InteractionAffordance'' per interagire con una ``Thing'' di tipo ``Evento''.} \\ \hline
        hasForm & Thing, InteractionAffordance & hctl:Form & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Specifica un \textit{hypermedia control} di tipo \textit{form} che descrive come l'operazione può essere portata a termine.} \\ \hline
        hasLink & N/A & hctl:Link & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Specifica dei \textit{link} verso risorse arbitrarie che sono in relazione con la ``Thing Description'' che si sta specificando.} \\ \hline
        hasUriTemplateSchema & InteractionAffordance & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce delle variabili \textit{template} per l'URI della risorsa basate sulle specifiche dello schema. Non possono essere nè schemi per object o array JSON.} \\ \hline
        hasInputSchema & ActionAffordance & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce lo schema dati per l'\textit{input} di un'``ActionAffordance''.} \\ \hline
        hasOutputSchema & ActionAffordance & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce lo schema dati per l'\textit{output} di un'``ActionAffordance''.} \\ \hline
    \end{tabularx}
\end{table}

\begin{table}[H]
	\centering
	\begin{tabularx}{\linewidth}{|>{\hspace{0pt}}p{0.2225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|}
        \hline
		\textbf{Nome} & \textbf{Domain} & \textbf{Range} & \textbf{È sottoproprietà di} \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{\textbf{Commento}} \\ \hline
        hasSubscriptionSchema & EventAffordance & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce lo schema dei dati che devono essere passati all'atto della sottoscrizione ad un ``EventAffordance''.} \\ \hline
        hasNotificationSchema & EventAffordance & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce lo schema dei dati delle istanze di evento che di cui la ``Thing'' effettua il \textit{push} attraverso una ``EventAffordance''.} \\ \hline
        hasNotificationResponseSchema & EventAffordance & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce lo schema dei dati per i messaggi di risposta alle istanze di evento di una ``Thing'' effettua il \textit{push} attraverso una ``EventAffordance''.} \\ \hline
        hasCancellationSchema & EventAffordance & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce lo schema dei dati che devono essere passati alla ``Thing'' per cancellare una sottoscrizione ad una ``EventAffordance''.} \\ \hline
        hasSecurityConfiguration & Thing, hctl:Form & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Definisce l'utilizzo di una configurazione di sicurezza, ovvero uno schema di sicurezza applicato ad una o più ``InteractionAffordance''.} \\ \hline
        definesSecurityScheme & Thing & N/A & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Indica la definizione di uno schema di sicurezza, che può essere utilizzato per garantire un accesso sicuro ad una o più ``InteractionAffordance''.} \\ \hline
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
        & \multicolumn{3}{p{0.675\linewidth}|}{Indica se l'azione è ``deterministica'' o meno, ovvero se può essere invocata più volte e, a fronte dello stesso \textit{input}, fornisce lo stesso \textit{output}.} \\ \hline
    \end{tabularx}
\end{table}

\begin{table}[H]
	\centering
	\begin{tabularx}{\linewidth}{|>{\hspace{0pt}}p{0.2225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|>{\hspace{0pt}}p{0.225\linewidth}|}
        \hline
		\textbf{Nome} & \textbf{Domain} & \textbf{Range} & \textbf{È sottoproprietà di} \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{\textbf{Commento}} \\ \hline
        isObservable & PropertyAffordance & schema:Boolean & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Indica se per una certa ``PropertyAffordance'' sono supportate le operazioni di ``observeProperty'' e ``unobserveProperty''.} \\ \hline
        name & InteractionAffordance & schema:Text & N/A \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Proprietà per l'indicizzazione utilizzabile per salvare il nome dell'entità quando questa viene serializzata in una ``index map'' di JSON-LD.} \\ \hline
        title & Thing, InteractionAffordance, jsonschema:DataSchema & schema:Text & dcterms:title \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Nome o titolo dell'elemento.} \\ \hline
        titleInLanguage & Thing, InteractionAffordance, jsonschema:DataSchema & schema:Text & dcterms:title \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Nome o titolo dell'elemento con associata un'annotazione linguistica all'oggetto della tripla che ha questa proprietà per predicato.} \\ \hline
        description & Thing, InteractionAffordance, wotsec:SecurityScheme, jsonschema:DataSchema & schema:Text & dcterms:description \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Descrizione dell'elemento.} \\ \hline
        descriptionInLanguage & Thing, InteractionAffordance, wotsec:SecurityScheme, jsonschema:DataSchema & schema:Text & dcterms:description \\ \cline{2-4}
        & \multicolumn{3}{p{0.675\linewidth}|}{Descrizione dell'elemento con associata un'annotazione linguistica all'oggetto della tripla che ha questa proprietà per predicato.} \\ \hline 
    \end{tabularx}
\end{table}
```

### Istanze

```{=latex}
\begin{table}[H]
	\centering
	\begin{tabularx}{\textwidth}{|l|X|l|}
        \hline
		\textbf{Nome} & \textbf{Commento} & \textbf{È istanza di class} \\ \hline
        readProperty & Si usa per leggere il valore di una proprietà. & OperationType \\ \hline
        writeProperty & Si usa per scrivere il valore di una proprietà. & OperationType \\ \hline
        observeProperty & Si usa per osservare il valore di una proprietà. & OperationType \\ \hline
        unobserveProperty & Si usa per terminare l'osservazione del valore di una proprietà. & OperationType \\ \hline
        readMultipleProperties & Si usa per leggere il valore di una proprietà. & OperationType \\ \hline
        writeMultipleProperties & Si usa per scrivere il valore di una proprietà. & OperationType \\ \hline
        readAllProperties & Si usa per leggere il valore di tutte le proprietà. & OperationType \\ \hline
	\end{tabularx}
\end{table}

\begin{table}[H]
	\centering
	\begin{tabularx}{\textwidth}{|l|X|l|}
        \hline
		\textbf{Nome} & \textbf{Commento} & \textbf{È istanza di class} \\ \hline
        writeAllProperties & Si usa per scrivere il valore di tutte le proprietà. & OperationType \\ \hline
        observeAllProperties & Si usa per osservare il valore di tutte le proprietà. & OperationType \\ \hline
        unobserveAllProperties & Si usa per terminare l'osservazione del valore di tutte le proprietà. & OperationType \\ \hline
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
        supportContact & Fornisce informazioni sul manutentore della "Thing Description". \\ \hline
        followsProfile & Indica i meccanismi "WoT Profile" che la "Thing Description" segue e così l'implementazione di "Thing" associata. \\ \hline
        baseURI & Definisce l'URI base per tutti gli URI relativi contenuti nella "Thing Description". \\ \hline
        versionInfo & Fornisce informazioni sulla versione. \\ \hline
        instance & Fornisce un identificatore di versione per questa istanza di "Thing Description". \\ \hline
        model & Fornisce un identificatore di versione per il modello della "Thing" sottostante, quello associato alla "Thing" descritta da questa "Thing Description". \\ \hline
	\end{tabularx}
\end{table}
```

## Esempi

    {
        "@context": {
            "https://www.w3.org/2019/wot/td/v1",
            {"@base": "http://example.org/MyLampThing/"}
        },
        "id": "urn:dev:ops:32473-WoTLamp-1234",
        "title": "MyLampThing",
        "securityDefinitions": {
            "basic_sc": {"scheme": "basic", "in":"header"}
        },
        "security": ["basic_sc"],
        "properties": {
            "status" : {
                "type": "string",
                "forms": [{"href": "https://mylamp.example.com/status"}]
            }
        },
        "actions": {
            "toggle" : {
                "forms": [{"href": "https://mylamp.example.com/toggle"}]
            }
        },
        "events":{
            "overheating":{
                "data": {"type": "string"},
                "forms": [{
                    "href": "https://mylamp.example.com/oh",
                    "subprotocol": "longpoll"
                }]
            }
        }
    }

Si ripresenta ora lo stesso esempio nel linguaggio "Turtle".

    @prefix td: <https://www.w3.org/2019/wot/td>.
    @prefix hctl: <https://www.w3.org/2019/wot/hypermedia>.
    @prefix wotsec: <https://www.w3.org/2019/wot/security>.
    @prefix jsonSchema: <https://www.w3.org/2019/wot/json-schema>.

    <urn:dev:ops:32473-WoTLamp-1234>
        td:title "MyLampThing";
        td:definesSecurityScheme [
            a wotsec:BasicSecurityScheme;
            wotsec:in "header";
            td:hasConfigurationInstance <http://example.org/MyLampThing/basic_sc>
        ];
        td:hasSecurityConfiguration <http://example.org/MyLampThing/basic_sc>;
        td:hasPropertyAffordance [
            td:name "status";
            a jsonSchema:StringSchema;
            td:hasForm [ hctl:hasTarget "https://mylamp.example.com/status" ]
        ];
        td:hasActionAffordance [
            td:name "toggle";
            td:hasForm [ hctl:hasTarget "https://mylamp.example.com/toggle" ]
        ];
        td:hasEventAffordance [
            td:name "overheating";
            td:hasNotificationSchema [ a jsonSchema:StringSchema ];
            td:hasForm [
                hctl:forSubProtocol "longpoll";
                hctl:hasTarget "https://mylamp.example.com/oh"
            ];
        ].

## Allineamenti con altre ontologie

## Progetti in cui è presente