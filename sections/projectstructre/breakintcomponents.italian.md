# Struttura la tua soluzione in componenti

<br/><br/>

### Spiegazione in un paragrafo
Per applicazioni di medie e grandi dimensioni, sviluppare monoliti è molto sbagliato - avendo un grosso software con tante dipendenze è difficile ragionarci sopra e spesso porta a produrre pessimo codice. Anche gli architetti intelligenti - quelli che sono abbastanza abili da "domare la bestia" e modularizzarla - impiegano un grosso sforzo mentale nella progettazione, ed ogni cambiamento richiede un'attenta valutazione dell'impatto che potrebbe avere su oggetti da esso dipendenti. 
La soluzione migliore è sviluppare piccole porzioni di software: dividere l'intero stack in componenti autosufficienti che non condividono files con altri, ognuno costituito da pochi file (es. API, servizi, data access, tests ecc.) in modo tale che sia molto semplice ragionarci sopra. 
Alcuni chiamano questa suddivisione architettura a 'microservizi' - è importante capire che i microservizi non sono specifiche che devi seguire, ma sono un insieme di principi. Puoi adottare tanti o pochi principi all'interno di una vera e propria architettura a microservizi. Entrambe le strade sono giuste finché si mantiene la complessità del software bassa.
L'unica cosa che dovresti fare è creare 'bordi di base' tra i componenti, assegnare una cartella nella root del progetto per ogni componente di business e renderlo autonomo - gli altri componenti possono usufruire delle  funzionalità di un componente solamente attraverso la sua interfaccia pubblica o API. 
Questa è la base per mantenere i tuoi componenti semplici, evitare problemi infernali di dipendenze e aprire la strada ad una vera e propria architettura a microservizi futura, quando la tua applicazione crescerà. 

<br/><br/>

### Citazione da blog: "Il ridimensionamento richiede il ridimensionamento dell'intera applicazione"

 Dal blog MartinFowler.com

> Le applicazioni monolitiche possono avere successo, ma un numero incrementale di persone si sentono frustrate nell'utilizzarle - specialmente poiché molte applicazioni vengono distribuite in cloud. I cicli di cambiamento sono legati assieme - un cambiamento fatto ad una piccola parte dell'applicazione, richiede che l'intero monolite sia ri-prodotto e ri-distribuito. Nel tempo, è spesso difficile mantenere una buona struttura modulare, rendendo arduo  mantenere le modifiche che dovrebbero interessare solo un modulo all'interno di quel modulo. Il ridimensionamento richiede il ridimensionamento dell'intera applicazione piuttosto che parti di esso che richiedono una maggiore risorsa.

<br/><br/>

### Citazione da blog: "Quindi, cosa urla l'architettura della tua applicazione?"

 Dal blog [uncle-bob](https://8thlight.com/blog/uncle-bob/2011/09/30/Screaming-Architecture.html) 

> ... se stavi guardando l'architettura di una libreria, probabilmente avrai visto un'entrata grandiosa, un'area per i commessi di check-in-out, aree di lettura, piccole sale conferenze ed una galleria dopo l'altra in grado di contenere scaffali per tutti i libri della biblioteca. Quella architettura urlerebbe: Biblioteca.<br/>

Quindi, cosa urla l'architettura della tua applicazione? Quando si guarda la struttura di directory di primo livello e i file di origine nel package di livello più alto; gridano: sistema sanitario, sistema contabile o sistema di gestione delle scorte? Oppure urlano: Rails, Spring / Hibernate o ASP ?.

<br/><br/>

### Giusto: Struttura la tua soluzione in componenti

![alt text](https://github.com/i0natan/nodebestpractices/blob/master/assets/images/structurebycomponents.PNG "Structuring solution by components")

<br/><br/>

### Sbagliato: Raggruppamento dei file per ruolo tecnico

![alt text](https://github.com/i0natan/nodebestpractices/blob/master/assets/images/structurebyroles.PNG "Structuring solution by technical roles")
