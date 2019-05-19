# Usa Async-Await o le promises per la gestione degli errori asincroni

### Spiegazione in un paragrafo
Le callback non scalano correttamente poiché la maggior parte dei programmatori non le conosce. Costringono a controllare gli errori dappertutto, a gestire il pessimo codice e rendono difficile ragionare sul flusso di esecuzione.
Librerie di Promise come BlueBird, async e Q impacchettano uno stile di codice standard usando RETURN e THROW per controllare il flusso del programma. Più nello specifico, loro supportano lo stile preferito di gestione degli errori tramite try-catch  che consente di liberare il flusso del codice principale dagli errori in ogni funzione

### Esempio di codice - usando promises per gestire gli errori

```javascript
doWork()
 .then(doWork)
 .then(doOtherWork)
 .then((result) => doWork)
 .catch((error) => {throw error;})
 .then(verify);
```

### Esempio di codice Anti pattern – stile di gestione degli errori con callbacks

```javascript
getData(someParameter, function(err, result) {
    if(err !== null) {
        // do something like calling the given callback function and pass the error
        getMoreData(a, function(err, result) {
            if(err !== null) {
                // do something like calling the given callback function and pass the error
                getMoreData(b, function(c) {
                    getMoreData(d, function(e) {
                        if(err !== null ) {
                            // you get the idea? 
                        }
                    })
                });
            }
        });
    }
});
```

### Nota da un Blog: "Abbiamo un problema con promises"

 Dal blog pouchdb.com

 > ……E in effetti, le callback fanno qualcosa di ancora più sinistro: ci privano dello stack, cosa che di solito diamo per scontato nei linguaggi di programmazione. Scrivere codice senza uno stack è un po' come guidare una macchina senza il pedale del freno: non ti rendi conto di quanto ne hai bisogno finché quando ne hai bisogno non è lì. Il punto centrale di promises è di restituirci i fondamenti linguistici che abbiamo perso quando siamo andati in asincrono: return, throw e stack. Ma devi sapere come usare le promises correttamente per trarne vantaggio.

### Nota da un Blog: "Il metodo promises è molto più compatto"

 Dal blog gosquared.com

 > ………Il metodo delle promises è molto più compatto, più chiaro e veloce da scrivere. Se si verifica un errore o un'eccezione all'interno di una delle operazioni, viene gestito dal singolo gestore di .catch(). Avere questo unico posto per gestire tutti gli errori significa che non è necessario scrivere il controllo degli errori per ogni fase del lavoro.

### Nota da un Blog: "Le Promises sono native in ES6, possono essere usate con generatori"

 Dal blog StrongLoop

 > …Le callback hanno una pessima storia di gestione degli errori. Le Promises sono meglio. Adotta la gestione degli errori incorporata in Express con promises e riduci significativamente le possibilità di un'eccezione non rilevata. Le promises sono native in ES6, possono essere utilizzate con generatori e proposte ES7 come async/await attraverso compilatori come Babel

### Nota da un Blog: "Tutti quei costrutti di controllo del flusso regolari a cui sei abituato sono completamente danneggiati"

 Dal blog Benno’s

 > ……Una delle cose migliori della programmazione asincrona basata sulle callback è che fondamentalmente tutti quei costrutti di controllo del flusso regolari a cui siete abituati sono completamente rotti. Tuttavia, quello che trovo più rotto è la gestione delle eccezioni. Javascript fornisce una prova abbastanza familiare... costruisci il costrutto per gestire le eccezioni. Il problema con le eccezioni è che forniscono un ottimo modo di correggere gli errori su uno stack di chiamate, ma finiscono per essere completamente inutili se l'errore si verifica su uno stack diverso...
