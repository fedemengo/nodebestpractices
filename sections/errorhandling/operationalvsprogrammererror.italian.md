# Distingui gli errori operativi da quelli dei programmatori

### Spiegazione in un paragrafo
Distiguere i seguenti due tipi di errore minimizzarà il tempo di inattività della tua app e aiuterà ad evitare strani bug:
Errori operativi si riferiscono a situazioni nelle quali tu puoi capire cosa accade e l'impatto che esso ha
- ad esempio, una query a qualche servizio HTTP si blocca per qualche problema di connessione. D'altra parte, gli errori dei programmatori si riferiscono a casi in cui tu non hai idea del perchè ed a volte da dove gli errori provengano - potrebbe essere una riga di codice che prova a leggere da un valore indefinito o un pool di connessioni DB che perde memoria. Gli errori operativi sono relativamente semplici da gestire - solitamente loggare l'errore è sufficiente. Le cose si fanno più dure quando si presenta un errore di un programmatore, l'applicazione può passare ad uno stato inconsistente e non c'è niente di meglio che tu possa fare se non riavviare gentilmente l'applicazione. 

### Esempio di codice – fare un errore operativo (verificato)

```javascript
// marking an error object as operational 
const myError = new Error("How can I add new product when no value provided?");
myError.isOperational = true;

// or if you're using some centralized error factory (see other examples at the bullet "Use only the built-in Error object")
class AppError {
  constructor (commonType, description, isOperational) {
    Error.call(this);
    Error.captureStackTrace(this);
    this.commonType = commonType;
    this.description = description;
    this.isOperational = isOperational;
  }
};

throw new AppError(errorManagement.commonErrors.InvalidInput, "Describe here what happened", true);

```

### Nota da un blog: "Gli errori del programmatore sono bug nel programma"

Dal blog, Joyent classificato 1 per le parole chiave “Node.js error handling”

 > … Il modo migliore per recuperare dagli errori del programmatore è arrestare immediatamente. Dovresti eseguire i tuoi programmi usando un restarter che riavvierà automaticamente il programma in caso di crash. Con un restarter, arrestare il programma è il modo più rapido per ripristinare un servizio affidabile di fronte a un errore transitorio del programmatore…

### Nota da un blog: "Nessun modo sicuro di andarsene senza creare uno stato fragile indefinito"

Dalla documentazione ufficiale Node.js

 > …Per la natura stessa di come funziona throw in JavaScript, non c'è quasi mai alcun modo di "riprendere da dove si era interrotto" in modo sicuro, senza perdite di riferimenti o creando qualche altro tipo di fragile stato indefinito. Il modo più sicuro per rispondere a un errore generato è arrestare il processo. Ovviamente, in un normale server Web, potresti avere molte connessioni aperte e non è ragionevole interromperle bruscamente perché un errore è stato attivato da qualcun altro. L'approccio migliore consiste nell'inviare una risposta di errore alla richiesta che ha attivato l'errore lasciando che gli altri finiscano nel loro tempo normale e interrompere l'ascolto di nuove richieste in quell'operatore.

### Nota da un blog: "Altrimenti rischi lo stato della tua applicazione"

Dal blog, debugable.com classificato 3 per le parole chiave “Node.js uncaught exception”

 > …Quindi, a meno che tu non sappia davvero cosa stai facendo, dovresti eseguire un riavvio graduale del tuo servizio dopo aver ricevuto un evento di eccezione "uncaughtException". Altrimenti, rischi che lo stato della tua applicazione o quello delle librerie di terze parti diventi inconsistente, portando a tutti i tipi di bug strani…

### Nota da un blog: "Ci sono tre scuole di pensiero sulla gestione degli errori"

Dal blog: JS Recipes

> …Ci sono principalmente tre scuole di pensiero sulla gestione degli errori:
1. Lasciare che l'applicazione vada in crash e riavviarla.
2. Gestire tutti gli errori possibili e non arrestarsi mai.
3. Un approccio equilibrato tra i due
