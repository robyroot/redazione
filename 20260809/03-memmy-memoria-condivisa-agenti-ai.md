---
title: "Memmy: la memoria condivisa open source per Claude Code, Codex e gli altri agenti AI"
rilevanza: "MEDIA"
fonte: "https://github.com/MemTensor/memmy-agent"
data_notizia: "2026-08-07"
tags: ["ai", "open-source", "privacy", "agenti-ai", "self-hosted"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: parlare del problema reale (ogni tool AI ha la sua memoria isolata, ti tocca
  rispiegare tutto ogni volta) prima di presentare lo strumento. Da menzionare con onestà il dettaglio
  che l'app di default punta a un servizio cloud del produttore anche se i dati restano in locale:
  è il tipo di distinzione che i lettori di RobyRoot orientati alla privacy apprezzano. Buon layer AI + privacy + self-hosting, tre temi del blog in un colpo solo.
---

Se usi più di un assistente AI per programmare — magari Claude Code per certe cose, Codex per altre, e ogni tanto un terzo strumento per completezza — probabilmente conosci già questa piccola frustrazione: ogni volta che passi da uno strumento all'altro, devi rispiegare da capo chi sei, cosa stai costruendo, quali convenzioni usi nel tuo progetto. Ogni agente ha la sua memoria, isolata dalle altre, e nessuno "ricorda" quello che hai già detto agli altri. È il classico problema dei silos, applicato agli assistenti AI.

Memmy, un progetto open source pubblicato su GitHub da MemTensor, prova ad attaccare esattamente questo problema. L'idea di base è semplice da spiegare anche se tecnicamente non banale da realizzare bene: creare un unico "hub" di memoria locale che diversi agenti AI — Claude Code, Codex, OpenClaw, Hermes Agent e altri — possono leggere e scrivere, così che il contesto costruito con uno strumento sia disponibile anche quando ne usi un altro.

**Come funziona, in pratica**

Memmy si presenta sia come applicazione desktop che come strumento a riga di comando, e si integra con gli altri agenti tramite MCP (Model Context Protocol), lo standard che ormai la maggior parte degli strumenti AI moderni usa per parlare con servizi esterni e tool di terze parti. Il progetto permette anche di importare la cronologia già accumulata da altri agenti, così non parti da zero se hai già mesi di conversazioni sparse tra vari strumenti. Oltre alla memoria condivisa, offre anche integrazioni verso servizi come Telegram, Discord, GitHub e Gmail, per usare l'agente come punto di raccordo anche fuori dal contesto puramente "coding".

**Il dettaglio che interessa a chi tiene alla privacy**

La documentazione del progetto è chiara su un punto che a noi di RobyRoot sta particolarmente a cuore: per impostazione predefinita, memoria, configurazione e stato dell'applicazione restano salvati sulla tua macchina, senza bisogno di caricare nulla sul cloud. È un'architettura "local-first", che si allinea bene con l'idea di mantenere il controllo sui propri dati anche quando si usano strumenti AI di terze parti — un tema su cui, giustamente, molti sviluppatori sono diventati più sensibili negli ultimi anni, complici gli innumerevoli casi di conversazioni AI finite dove non dovevano.

Va detto però, per completezza e onestà, che la configurazione predefinita dell'app desktop punta comunque a un servizio cloud del produttore (memmy-api.memtensor.cn), usato ad esempio per la modalità "account" con crediti di prova. Chi vuole restare rigorosamente offline può usare la modalità BYOK (bring-your-own-key, cioè porti la tua chiave API di OpenAI o di un altro provider) oppure compilare il progetto da sorgente e ospitarlo interamente in locale. La distinzione conta: "i dati stanno sul tuo disco" non è automaticamente la stessa cosa di "nessuna chiamata esce mai dalla tua rete", ed è il tipo di dettaglio che vale la pena leggere nella documentazione prima di fidarsi ciecamente del marketing.

**Licenza e stato del progetto**

Memmy è distribuito con licenza MIT, quindi permissiva anche per riuso commerciale, e al momento in cui scriviamo ha superato le 600 stelle su GitHub con uno sviluppo attivo (decine di commit sul branch principale nelle ultime settimane). Non è ancora un progetto enorme come altri strumenti dell'ecosistema AI-per-sviluppatori, ma il problema che affronta — la frammentazione della memoria tra agenti diversi — è reale e sentito, e non stupirebbe vederlo crescere rapidamente se l'esecuzione tecnica regge nel tempo.

**Perché tenerlo d'occhio**

Il tema della "memoria persistente" per gli agenti AI è uno dei fronti più caldi del momento nello sviluppo assistito da AI: ci sono già altri progetti simili in circolazione (claude-mem, Memorix, solo per citarne un paio), segno che il problema è sentito da più parti contemporaneamente, non da un singolo team isolato. Se lavori con più strumenti AI ogni giorno e sei stanco di ripetere sempre le stesse spiegazioni, vale la pena tenere d'occhio come evolve questo pezzo di ecosistema — magari partendo proprio dalla modalità self-hosted, per restare coerenti con lo spirito open source e privacy-first del progetto.
