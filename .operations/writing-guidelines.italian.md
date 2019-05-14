# Il nostro manifesto di scrittura

Come miglioriamo l'esperienza di lettura e apprendimento per i nostri lettori

## 1. Semplice é meglio che migliore

<br/>
La nostra mission é fare in modo che la lettura e l'assorbimento di informazioni sia semplice. Per questo ci concentriamo nel trasformare argomenti complessi ed esaustivi in una lista semplificata, informazioni sovraccaricate in dettagli meno accurati e abbreviati. Evitiamo argomenti caldi e contestati in favore di pratiche generalmente accettare

<br/>

## 2. Presenta prove e sii affidabile

<br/>

I nostri lettori devono avere fiducia nel fatto che i contenuti che leggono siano affidabili. Per garantire questo presentiamo citazioni, dati e altre risorse disponibili per l'argomento in questione. Nel concreto, sforzati di includere citazioni da fonti attendibili, mostra benchmarks e design patterns inerenti o qualsiasi altro tipo di misura scientifica che sostiene le tue affermazioni

## 3. MECE (Mutualmene Esclusivo e Complessivamente Esaustivo)

Indipendetemente dal fatto che i contenuti siano notevolmente curati e affidabili, una veloce lettura deve garantire una completa comprensione dell'argomento. Nessun sotto argomento deve essere tralasciato

## 4. Formattazione consistente

I contenuti sono presentati utilizzando template. Ogni contenuto deve rispettare lo stesso template. Se vuoi aggiungere nuovi elenchi puntati, copiane il formato da uno esistente ed estendilo in base alle tue necessità. Per ulteriori informazioni dai un'occhiata a [questo template](https://github.com/i0natan/nodebestpractices/blob/master/sections/template.md)

## 5. Riguarda Node.js

Ogni sugerimento deve essere inerente a Node.js e non allo sviluppo software in generale. Quando suggeriamo di implementare pattern e regole generiche in Node.js, i contenuti devono concentrarsi sulla implementazione in Node.js. Ad esempio, quando consigliamo di sanificare le richieste di input per ragioni di sicurezza, deve essere utilizzato il gergo Node.js - "Usa un middleware per sanificare le richieste di input". Se alcuni elementi non hanno una implementazione spefica in Node.js (e.g é simile in Python e Java) - aggiungi l'elemento all'interno di un generico articolo, per esempio il punto 6.5

## 6. Solamente i principali fornitori

A volte é utile includere i nomi degli sviluppatori/fornitori che possono risolvere certe difficoltà e problemi come pacchetti npm, strumenti open source o anche prodotti commerciali. Per evitare di scrivere immense liste o di raccomandre progetti instabili e non rispettabili, abbiamo deciso di seguire alcune regole:

- Solamente i migliore 3 fornitori possono essere consigliati - un fornitore che appare nei primi 3 risultati di un motore di ricerca (Google o GitHub ordinato per popolarità) per una keywork rilevante può essere incluso.
- Se si tratta di un pacchetto npm, deve essere scaricato, in media, almento 750 volte al giorno
- Se si tratta di un progetto open-source, deve essere stato aggiornato almeno una volta negli utlimi 6 mesi
