---
title: "npm v12 disattiva gli script di installazione: la svolta (tardiva ma benvenuta) per la sicurezza della supply chain"
rilevanza: "MEDIA"
fonte: "https://thehackernews.com/2026/07/npm-12-disables-install-scripts-by.html"
data_notizia: "2026-07-26"
tags: ["npm", "supply-chain", "sicurezza", "javascript", "open-source"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: taglio pratico per sviluppatori e sysadmin che gestiscono progetti Node.js,
  con mini tutorial sul comando npm approve-scripts. Collegare alla serie sulla supply chain
  (attacchi jscrambler, AsyncAPI) già citati nell'articolo, per dare contesto a chi non ha letto le notizie precedenti.
---

Se sviluppi in JavaScript o Node.js, o anche solo installi pacchetti npm come dipendenza di qualche progetto, questa è una notizia che ti riguarda direttamente, anche se probabilmente non ne hai ancora sentito parlare. npm sta per rilasciare la versione 12, che porta con sé quello che gli addetti ai lavori descrivono come "il redesign di sicurezza più significativo nei 16 anni di storia del gestore di pacchetti". La novità principale: gli script di installazione automatici, per la prima volta, saranno disattivati di default.

## Perché è un problema che dura da anni

Per capire perché questa mossa è importante, bisogna sapere come funzionava npm fino ad oggi. Ogni pacchetto può includere degli "script del ciclo di vita" — preinstall, install, postinstall — che vengono eseguiti automaticamente nel momento in cui digiti `npm install`, prima ancora che tu apra il codice o lo importi nel tuo progetto. È una funzionalità pensata per cose legittime, tipo compilare moduli nativi con node-gyp. Il problema è che per anni è stata anche la porta d'ingresso preferita degli attacchi alla supply chain: basta compromettere un solo pacchetto (o rubare le credenziali di chi lo pubblica) e milioni di macchine eseguiranno codice malevolo in automatico al primo `npm install`, senza che nessuno se ne accorga.

Non è un timore teorico. Solo nell'ultimo mese abbiamo visto due casi da manuale. L'11 luglio 2026, il pacchetto jscrambler — ironia della sorte, un tool di un vendor di sicurezza — è stato compromesso con credenziali rubate: la nuova versione conteneva un binario nascosto da 7,8 MB che, tramite un hook preinstall, scaricava e lanciava silenziosamente un infostealer scritto in Rust per Linux, Windows e macOS, puntando a credenziali cloud, token CI, wallet di criptovalute e persino i file di configurazione di tool AI come Claude Desktop e Cursor. Pochi giorni dopo, il 14 luglio, è toccato ai pacchetti del generatore AsyncAPI, compromessi attraverso l'accesso al ramo di sviluppo del repository GitHub: qui il codice malevolo scattava al semplice caricamento della libreria, non solo all'installazione.

## Cosa cambia con npm v12

Con la nuova versione, tre comportamenti passano da automatici a opt-in:

- Gli script del ciclo di vita (preinstall, install, postinstall) e le build node-gyp non partono più in automatico durante `npm install`.
- Le dipendenze Git non vengono risolte a meno che tu non lo autorizzi esplicitamente con `--allow-git`.
- Le dipendenze da URL remoti (tarball HTTPS) restano bloccate senza autorizzazione esplicita con `--allow-remote`.

In pratica, npm si allinea finalmente a quello che fanno già da tempo Yarn, pnpm e Bun, tutti gestori di pacchetti che bloccano gli script di installazione di default. Il dato che dà la misura di quanto fosse sproporzionato il rischio: solo il 2% circa dei pacchetti su npm ha effettivamente bisogno di eseguire script di installazione per funzionare. Il restante 98% eseguiva codice arbitrario sulla tua macchina senza alcun motivo tecnico reale.

## Cosa devi fare se sviluppi con npm

Se gestisci progetti Node.js, conviene iniziare a prepararsi già da ora, visto che le funzionalità sono già disponibili a partire da npm 11.16.0:

1. Esegui `npm approve-scripts --allow-scripts-pending` sui tuoi progetti per rivedere quali pacchetti richiedono davvero script di installazione.
2. Committa la allowlist generata nel tuo `package.json`, così il team (o la pipeline CI) sa esattamente quali script sono stati autorizzati e perché.
3. Se usi dipendenze Git dirette o tarball da URL remoti, preparati ad aggiungere i flag `--allow-git` o `--allow-remote` dove servono davvero.
4. Tieni d'occhio anche il cambio sui Granular Access Token: npm disabiliterà i GAT che bypassano la 2FA per operazioni sensibili, con restrizioni in vigore da agosto 2026 e limiti alla pubblicazione diretta a partire da gennaio 2027.

È una di quelle modifiche che generano un po' di attrito nel breve termine — qualche build che si rompe, qualche script legittimo da riautorizzare — ma che nel lungo periodo rendono l'intero ecosistema JavaScript sensibilmente più difficile da usare come vettore d'attacco. Vista la frequenza con cui negli ultimi mesi abbiamo scritto di pacchetti npm compromessi, è un cambiamento che arriva con qualche anno di ritardo, ma è comunque un ottimo segnale.
