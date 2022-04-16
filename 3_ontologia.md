# Ontologia

## Struttura dell'ontologia

L'ontologia "_core_" di una "Thing Description" è costituita da 6 classi, 24 proprietà e 18 istanze. [@td-ontology]

### Classi

| Nome | Commento | È sottoclasse di |
|------|----------|------------------|
| Thing | L'astrazione di un'entità fisica o virtuale i cui metadati e le cui interfacce sono descritti da una "Thing Description". Un entità virtuale può essere la composizione di una o più "Thing". | N/A |
| InteractionAffordance | I metadati di una "Thing" che indicano le possibili scelte che hanno i componenti che sfruttano la "Thing" nell'usarla, suggerendo loro come interagire con la "Thing". | N/A |
| PropertyAffordance | Una "InteractionAffordance" che espone lo stato di una "Thing". Questo stato può essere ottenuto, cioè letto, e/o aggiornato, cioè scritto. Una "Thing" può decidere di rendere una "PropertyAffordance" osservabile effettuando il _push_ del suo nuovo stato dopo ogni modifica. | InteractionAffordance |
| ActionAffordance | Una "InteractionAffordance" che permette di invocare una funzione della "Thing", che può manipolare il suo stato o attivare un processo su di essa. | InteractionAffordance |
| EventAffordance | Una "InteractionAffordance" che descrive una sorgente di eventi, che in maniera asincrona fa _push_ dei dati di questi eventi ai componenti che utilizzano la "Thing". | InteractionAffordance |
| OperationType | Enumerazione di tipi di operazione ben noti necessari per implementare l'"Interaction Model" di WoT. | N/A |
[@td-ontology]

### Proprietà "object"

| Nome | Commento | Domain | Range | È sottoproprietà di |
|------|----------|--------|-------|---------------------|
| hasInteractionAffordance | Specifica una "InteractionAffordance" per interagire con una "Thing". | Thing | InteractionAffordance | N/A |
| hasPropertyAffordance | Specifica una "InteractionAffordance" per interagire con una "Thing" di tipo "Proprietà". | N/A | PropertyAffordance | hasInteractionAffordance |
| hasActionAffordance | Specifica una "InteractionAffordance" per interagire con una "Thing" di tipo "Azione". | N/A | ActionAffordance | hasInteractionAffordance |
| hasEventAffordance | Specifica una "InteractionAffordance" per interagire con una "Thing" di tipo "Evento". | N/A | EventAffordance | hasInteractionAffordance |
| hasForm | Specifica un _hypermedia control_ di tipo _form_ che descrive come l'operazione può essere portata a termine. | Thing, InteractionAffordance | hctl:Form | N/A |
| hasLink | Specifica dei _link_ verso risorse arbitrarie che sono in relazione con la "Thing Description" che si sta specificando. | N/A | hctl:Link | N/A |
| hasUriTemplateSchema | Definisce delle variabili _template_ per l'URI della risorsa Define URI template variables basate sulle specifiche dello schema. Non possono essere nè schemi per object o array JSON. | InteractionAffordance | N/A | N/A |
| hasInputSchema | Definisce lo schema dati per l'_input_ di un'"ActionAffordance". | ActionAffordance | N/A | N/A |
| hasOutputSchema | Definisce lo schema dati per l'_output__ di un'"ActionAffordance". | ActionAffordance | N/A | N/A |
| hasSubscriptionSchema | Definisce lo schema dei dati che devono essere passati all'atto della sottoscrizione ad un "EventAffordance". | EventAffordance | N/A | N/A |
| hasNotificationSchema | Definisce lo schema dei dati delle istanze di evento che di cui la "Thing" effettua il _push_ attraverso una "EventAffordance". | EventAffordance | N/A | N/A |
| hasNotificationResponseSchema | Definisce lo schema dei dati per i messaggi di risposta alle istanze di evento di una "Thing" effettua il _push_ attraverso una "EventAffordance". | EventAffordance | N/A | N/A |
| hasCancellationSchema | Definisce lo schema dei dati che devono essere passati alla "Thing" per cancellare una sottoscrizione ad una "EventAffordance". | EventAffordance | N/A | N/A |
| hasSecurityConfiguration | Definisce l'utilizzo di una configurazione di sicurezza, ovvero uno schema di sicurezza applicato ad una o più "InteractionAffordance". | Thing, hctl:Form | N/A | N/A |
| definesSecurityScheme | Indica la definizione di uno schema di sicurezza, che può essere utilizzato per garantire un accesso sicuro ad una o più "InteractionAffordance". | Thing | N/A | N/A |
| hasConfigurationInstance | Definisce l'associazione tra uno schema di sicurezza e la sua configurazione. | wotsec:SecurityScheme | N/A | N/A |
[@td-ontology]

### Proprietà "datatype"

| Nome | Commento | Domain | Range | È sottoproprietà di |
|------|----------|--------|-------|---------------------|
| isSafe | Indica se un'"ActionAffordance" non è "mutabile" o meno, cioè se non modifica lo stato interno della "Thing". | ActionAffordance | schema:Boolean | N/A |
| isIdempotent | Indica se l'azione è "deterministica" o meno, ovvero se può essere invocata più volte e, a fronte dello stesso _input_, fornisce lo stesso _output_. | ActionAffordance | schema:Boolean | N/A |
| isObservable | Indica se per una certa "PropertyAffordance" sono supportate le operazioni di "observeproperty" e "unobserveproperty". | PropertyAffordance | schema:Boolean | N/A |
| name | Proprietà per l'indicizzazione utilizzabile per salvare il nome dell'entità quando questa viene serializzata in una "index map" di JSON-LD. | InteractionAffordance | schema:Text | N/A |
| title | Nome o titolo dell'elemento. | Thing, InteractionAffordance, jsonschema:DataSchema | schema:Text | dcterms:title |
| titleInLanguage | Nome o titolo dell'elemento con associata un'annotazione linguistica all'oggetto della tripla che ha questa proprietà per predicato. | Thing, InteractionAffordance, jsonschema:DataSchema | schema:Text | dcterms:title |
| description | Descrizione dell'elemento. | Thing, InteractionAffordance, wotsec:SecurityScheme, jsonschema:DataSchema | schema:Text | dcterms:description | 
| descriptionInLanguage | Descrizione dell'elemento con associata un'annotazione linguistica all'oggetto della tripla che ha questa proprietà per predicato. | Thing, InteractionAffordance, wotsec:SecurityScheme, jsonschema:DataSchema | schema:Text | dcterms:description | 
[@td-ontology]

### Istanze

| Nome | Commento | Istanza della classe |
|------|----------|----------------------|
| readProperty | Si usa per leggere il valore di una proprietà. | OperationType |
| writeProperty | Si usa per scrivere il valore di una proprietà. | OperationType |
| observeProperty | Si usa per osservare il valore di una proprietà. | OperationType |
| unobserveProperty | Si usa per terminare l'osservazione del valore di una proprietà. | OperationType |
| readMultipleProperties | Si usa per leggere il valore di una proprietà. | OperationType |
| writeMultipleProperties | Si usa per scrivere il valore di una proprietà. | OperationType |
| readAllProperties | Si usa per leggere il valore di tutte le proprietà. | OperationType |
| writeAllProperties | Si usa per scrivere il valore di tutte le proprietà. | OperationType |
| observeAllProperties | Si usa per osservare il valore di tutte le proprietà. | OperationType |
| unobserveAllProperties | Si usa per terminare l'osservazione del valore di tutte le proprietà. | OperationType |
| invokeAction | Si usa per invocare un'azione. | OperationType |
| queryAction | Si usa per controllare lo stato di un'azione. | OperationType |
| cancelAction | Si usa per cancellare un'azione. | OperationType |
| queryAllActions | Si usa per controllare lo stato di tutte le azioni. | OperationType |
| subscribeEvent | Si usa per effettuare la sottoscrizione ad un evento di un certo tipo. | OperationType |
| unsubscribeEvent | Si usa per cancellare la sottoscrizione ad un evento di un certo tipo. | OperationType |
| subscribeAllEvents | Si usa per effettuare la sottoscrizione a tutti i tipi di evento. | OperationType |
| unsubscribeAllEvents | Si usa per cancellare la sottoscrizione a tutti i tipi di evento. | OperationType |
[@td-ontology]

### Proprietà "annotation"

| Nome | Commento |
|------|----------|
| supportContact |
| followsProfile |
| baseURI |
| versionInfo |
| instance |
| model |

## Esempi

## Allineamenti con altre ontologie

## Progetti in cui è presente