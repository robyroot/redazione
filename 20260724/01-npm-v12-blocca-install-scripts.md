---
title: "npm v12 blocca gli install scripts di default: la fine di un incubo per la supply chain"
rilevanza: "ALTA"
fonte: "https://www.aikido.dev/blog/npm-v12-block-postinstall"
data_notizia: "2026-07-24"
tags: ["npm", "supply-chain", "cybersecurity", "javascript", "sviluppo"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: collegare la notizia agli attacchi npm degli ultimi mesi (AsyncAPI, Jscrambler)
  già trattati da altri siti italiani, per dare un taglio "cosa cambia ora, finalmente" invece che
  ripetere l'ennesima cronaca di breach. Ottimo pezzo da abbinare a una checklist pratica per chi
  gestisce pipeline CI/CD Node.js. Buon candidato anche per newsletter, perché tocca sia i dev che
  chi si occupa di sicurezza aziendale.
---

Se lavori con Node.js, JavaScript o npm da più di qualche mese, probabilmente hai già sentito parlare degli attacchi alla supply chain che negli ultimi due anni hanno trasformato l'ecosistema npm in un campo minato. Bene, con npm v12, in arrivo proprio in questi giorni di luglio 2026, il team di npm ha deciso di tirare una riga netta sotto uno dei problemi più seri: gli install script che partono automaticamente quando installi un pacchetto.

Fino ad oggi, quando lanci `npm install`, ogni pacchetto (e ogni sua dipendenza, e la dipendenza della dipendenza) può eseguire codice arbitrario sulla tua macchina tramite gli hook `preinstall`, `install` e `postinstall`. È una funzionalità nata per motivi legittimi — pensa alle librerie che devono compilare codice nativo — ma che negli ultimi anni è diventata l'arma preferita di chi vuole infilare malware in migliaia di progetti in un colpo solo.

## Una lunga scia di attacchi

La lista dei precedenti è, francamente, imbarazzante. Ad agosto 2025 l'attacco "Nx s1ngularity" ha rubato circa 2.300 credenziali sfruttando proprio questo meccanismo. A novembre 2025 è arrivato "Shai-Hulud", un worm auto-replicante che si è propagato attraverso oltre 500 pacchetti, infettando un pacchetto per poi usarne le credenziali per infettarne altri, a cascata. A marzo 2026 è toccato ad Axios, con un account compromesso usato per distribuire un RAT (Remote Access Trojan). E a maggio 2026 è spuntato "Mini Shai-Hulud", una variante ancora più insidiosa perché dotata di una firma di build valida, che la rendeva quasi indistinguibile da un pacchetto legittimo.

Se hai seguito anche solo di striscio le notizie di sicurezza di quest'anno, avrai notato che a questi si aggiungono i casi più recenti come l'attacco ad AsyncAPI di metà luglio, dove i pacchetti compromessi non usavano nemmeno più gli script di installazione classici, ma eseguivano il payload al semplice `import` del modulo — segno che gli attaccanti si stanno già adattando ai controlli che stanno per arrivare.

## Cosa cambia davvero con v12

Con npm v12 il comportamento di default si ribalta completamente: gli script di installazione non partono più a meno che tu non li abbia esplicitamente autorizzati. Il meccanismo si basa su due comandi nuovi:

- `npm approve-scripts`, per aggiungere un pacchetto a una allowlist di fiducia;
- `npm deny-scripts`, per bloccare esplicitamente un pacchetto sospetto.

E non è un blocco aggirabile con un trucchetto: anche i file `binding.gyp`, quelli usati per innescare compilazioni native (tipiche di pacchetti come `node-sass` o driver per database), vengono ora trattati come script dichiarati e richiedono la stessa approvazione manuale. Chi pensava di bypassare il controllo nascondendo la logica malevola in un passaggio di build si troverà comunque davanti al muro dell'allowlist.

La buona notizia è che non serve aspettare l'uscita ufficiale di v12 per iniziare a proteggersi: le protezioni sono già disponibili, in modalità "warning", a partire da npm 11.16.0. Il consiglio pratico per chi gestisce progetti Node è aggiornare subito a questa versione e lanciare `npm approve-scripts --allow-scripts-pending`, un comando che elenca tutti gli script che verrebbero bloccati con le nuove regole, così puoi rivedere con calma quali pacchetti fidarti e quali invece meritano un controllo più approfondito.

## Perché conta, anche se non sei uno sviluppatore

Potresti pensare che questa sia una notizia solo per chi scrive codice, ma la realtà è che gli attacchi alla supply chain di npm hanno un effetto a cascata che arriva ovunque: se un'azienda usa un'app web costruita su Node.js (e sono la stragrande maggioranza), un pacchetto compromesso può finire per rubare credenziali cloud, token GitHub, chiavi di wallet crypto o persino dati dei clienti finali. Ogni volta che senti parlare di un data breach "causato da una libreria di terze parti", probabilmente la causa a monte era proprio uno di questi install script eseguiti senza controllo.

Non è la soluzione definitiva — un pacchetto malevolo può comunque fare danni una volta importato ed eseguito nel codice applicativo — ma è il primo argine serio contro una delle tecniche di attacco più sfruttate degli ultimi due anni. Se gestisci pipeline CI/CD basate su Node.js, il momento di prepararti è adesso, prima che il cambiamento diventi obbligatorio.
