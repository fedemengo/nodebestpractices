# Gestisci gli errori in modo centralizzato. Non all'interno di middlewares

### Spiegazione in un paragrafo
Senza un singolo oggetto oggetto per la gestione degli errori, è maggiore la possibilità di nascondere ai radar importanti errori dovuti ad una gestione impropria degli stessi. Questo oggetto di gestione degli errori è responsabile di rendere gli errori visibili, per esempio scrivendo un logger ben formattato, mandando eventi ad un prodotto di monitoring come [Sentry](https://sentry.io/), [Rollbar](https://rollbar.com/), o [Raygun](https://raygun.com/). La maggior parte dei web framework come [Express](http://expressjs.com/en/guide/error-handling.html#writing-error-handlers), mette a disposizione un meccanismo middleware di gestione degli errori. 
Un tipico flusso di gestione degli errori può essere: Alcuni moduli tirano un errore -> l'API router cattura l'errore -> propaga l'errore ad un middleware (es. Express, KOA) che è responsabile della cattura degli errori ->  un meccanismo di gestione degli errori centralizzato viene richiamato -> il middleware viene avvertito se l'errore è untrusted (non operazionale) così può eseguire il riavvio dell'app. Nota che è una comune, ma sbagliata, pratica gestire l'errore in middleware Express - facendo così non coprirai gli errori che sono tirati in interfacce non web.

### Codice di esempio – un tipico flusso di gestione di errori

```javascript
// DAL layer, we don't handle errors here
DB.addDocument(newCustomer, (error, result) => {
  if (error)
    throw new Error("Great error explanation comes here", other useful parameters)
});

// API route code, we catch both sync and async errors and forward to the middleware
try {
  customerService.addNew(req.body).then((result) => {
    res.status(200).json(result);
  }).catch((error) => {
    next(error)
  });
}
catch (error) {
  next(error);
}

// Error handling middleware, we delegate the handling to the centralized error handler
app.use(async (err, req, res, next) => {
  const isOperationalError = await errorHandler.handleError(err);
  if (!isOperationalError) {
    next(err);
  }
});
```

### Codice di esempio – gestire gli errori in un oggetto dedicato

```javascript
module.exports.handler = new errorHandler();

function errorHandler() {
  this.handleError = async function(error) {
    await logger.logError(err);
    await sendMailToAdminIfCritical;
    await saveInOpsQueueIfCritical;
    await determineIfOperationalError;
  };
}
```

### Codice di esempio – Anti Pattern: gestire gli errori in middleware

```javascript
// middleware handling the error directly, who will handle Cron jobs and testing errors?
app.use((err, req, res, next) => {
  logger.logError(err);
  if (err.severity == errors.high) {
    mailer.sendMail(configuration.adminMail, 'Critical error occured', err);
  }
  if (!err.isOperational) {
    next(err);
  }
});
```

### Nota da un Blog: "A volte livelli bassi non fanno nulla di utile eccetto propafare gli errori ai loro chiamanti"

Dal blog Joyent, classificato 1 dalle parole chiave “Node.js error handling”
>…Probabilmente finirai per gestire lo stesso errore a diversi livelli dello stack. Questo accade quando un livello basso non può fare nulla di utile eccetto propagare l'errore al loro chiamante, che propaga l'errore al loro chiamante e così via. Spesso, solo il chiamante top-level conosce la risposta appropriata, se l'operazione va riprovata, va riportato un errore all'utente o altro.  Ma ciò non significa che dovresti provare a riportare tutti gli errori al chiamante top-level, perchè la callback non conosce in quale contesto l'errore è stato generato…

### Nota da un Blog: "Gestire ogni errore individualmente porta a duplicazioni tremende"

Dal blog JS Recipes classificato 17 per le parole chiave “Node.js error handling”

> ……In Hackathon Starter api.js nel solo controller, ci sono più di 79 occorrenze di errore o oggetti errore. Gestire ogni err individualmente porta in un tremendo ammontare di codice duplicato. La prossima migliore cosa che tu possa fare è delegare la gestione logica di tutti gli errori in un middleware Express.

### Nota da un Blog: "Errori HTTP non hanno posto nel tuo database code"

Dal blog Daily JS classificato 14 per le parole chiave “Node.js error handling”

> ……Dovresti settare utili proprietà in oggetti errore, ma usarle come proprietà consistenti. E non incrociare gli streams: errori HTTP non hanno posto nel database code. O per sviluppatori web, errori Ajax hanno spazio nel codice che parla con i server ma non in quello che processa Mustache templates…
