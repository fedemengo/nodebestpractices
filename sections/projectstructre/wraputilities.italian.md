# Confeziona le utilità comuni come pacchetti npm

<br/><br/>

### Spiegazione in un paragrafo
Una volta che il tuo progetto ha iniziato a crescere ed avere diversi componenti su diversi server che utilizzano le stesse utilità, dovresti iniziare a gestirne le dipendenze - come puoi mantenere 1 copia del tuo codice di utilità e lasciare che più componenti consumatori lo utilizzino e distribuiscano? Bene, esiste un tool per questo, si chiama npm... Inizia confezionando pacchetti di utilità di terze parti nel tuo codice per rendere più facile un rimpiazzamento futuro e pubblica il tuo codice come pacchetto npm privato. Ora, tutta la tua code base può importare quel codice e beneficiare dello strumento gratuito di gestione delle dipendenze. E' possibile pubblicare pacchetti npm per il tuo uso privato senza condividerli pubblicamente usando [private modules](https://docs.npmjs.com/private-modules/intro), [private registry](https://npme.npmjs.com/docs/tutorials/npm-enterprise-with-nexus.html) o [local npm packages](https://medium.com/@arnaudrinquin/build-modular-application-with-npm-local-modules-dfc5ff047bcc)

<br/><br/>

### Condividi le tue utilità comuni tra ambienti e componenti

![alt text](https://github.com/i0natan/nodebestpractices/blob/master/assets/images/Privatenpm.png "Structuring solution by components")
