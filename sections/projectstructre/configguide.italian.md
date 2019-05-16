# Usa una configurazione gerarchica, sicura e integrabile con l'ambiente

<br/><br/>

### Spiegazione in un paragrafo

Gestendo dati di configurazione, molti fattori possono infastidire e rallentare:

1. settare tutte le chiavi usando variabili d'ambiente diventa veramente noioso quando è necessario iniettare 100 chiavi (invece che salvarle in un file di configurazione), nonostante questo, utilizzare esclusivamente file non permette agli amministratori DevOps di modificare il comportamento dell'applicazione senza modificare il codice. Una soluzione efficace per gestire la configurazione, deve combinare sia file sia la sovrascrittura di alcuni valori con variabili di processo/ambiente.

2. quando si specificano tutte le chiavi in un semplice JSON, diventa frustrante trovare e modificare le chiavi quando la lista diventa grande. Un file JSON organizzato in gerarchia e raggrupato in sezioni può risolvere questi problemi, in più, alcune librerie permettono di salvare la configurazione in diversi file e unirli a run time. Guarda l'esempio in basso.

3. salvare informazione sensibili come password di database è ovviamente non consigliato ma non esistono ancora soluzioni semplici e pratiche. Alcune librerie di configurazione permettono di criptare file, altre permettono di criptare solo i valori sensibili durante GIT commits. Più semplicemente non salvare valori reali e specificali durante il rilascio attraverso variabili d'ambiente.

4. in alcuni casi di configurazione avanzata è necessario iniettare valori di configurazione da linea di comando (vargs) o sincronizzare la configurazione attraverso una cache centralizzata come Redis, in modo tale da permettere a più server di usare gli stessi dati di configurazione.

Alcune librerie di configurazione si occupano di molte di queste funzionalità, dai un'occhiata a pacchetti npm come [rc](https://www.npmjs.com/package/rc), [nconf](https://www.npmjs.com/package/nconf) e [config](https://www.npmjs.com/package/config) che risolvono molti di questi problemi.

<br/><br/>

### Esempio di codice – una configurazione gerarchica aiuta a ritrovare in modo semplice ogni voce ed a mantenere enormi file di configurazione

```js
{
  // Customer module configs 
  "Customer": {
    "dbConfig": {
      "host": "localhost",
      "port": 5984,
      "dbName": "customers"
    },
    "credit": {
      "initialLimit": 100,
      // Set low for development 
      "initialDays": 1
    }
  }
}
```

<br/><br/>
