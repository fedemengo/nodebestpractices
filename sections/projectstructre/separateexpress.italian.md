# Separa 'app' e 'server' di Express

<br/><br/>

### Spiegazione in un paragrafo

L'ultima versione di Express generator è dotata di una pratica che vale la pena seguire - la dichiarazione dell API è separata della configurazione della connessione (porta, protocollo, etc). Questo permette di testare l'API all'intero di un singolo file/processo, senza dover effettuare richieste di rete, con tutti i vantaggi che seguono: rapida esecuzione dei tests e semplice acquisizione di metriche di copertura del codice. Permette anche di distribure la stessa API in maniera più flessibile e con diverse condizione di rete. Bonus: miglior separazione dei rouli e codice più pulito.

<br/><br/>

### Esempio di codice: la dichiarazione dell' API dovrebbe trovarsi in app.js

```javascript
var app = express();
app.use(bodyParser.json());
app.use("/api/events", events.API);
app.use("/api/forms", forms);
```

<br/><br/>

### Esempio di codice: La configurazione della connessione del Server, dovrebbe trovarsi in /bin/www

```javascript
var app = require('../app');
var http = require('http');

/**
 * Get port from environment and store in Express.
 */

var port = normalizePort(process.env.PORT || '3000');
app.set('port', port);

/**
 * Create HTTP server.
 */

var server = http.createServer(app);
```

### Esempio: test dell'API con supertest (un popolare pacchetto di testing)

```javascript
const app = express();

app.get('/user', function(req, res) {
  res.status(200).json({ name: 'tobi' });
});

request(app)
  .get('/user')
  .expect('Content-Type', /json/)
  .expect('Content-Length', '15')
  .expect(200)
  .end(function(err, res) {
    if (err) throw err;
  });
````
