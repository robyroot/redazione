---
title: "PraisonAI, un framework open source per agenti IA, aveva una falla che dava accesso root con un semplice messaggio in chat"
rilevanza: "MEDIA"
fonte: "https://radar.offseq.com/threat/cve-2026-61445-improper-limitation-of-a-pathname-t-188171a28e18ac5b"
data_notizia: "2026-07-12"
tags: ["ai", "open-source", "cybersecurity", "agenti-ai", "vulnerabilita"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: usare questa notizia come caso di studio per spiegare cos'è la "prompt
  injection" e perché i framework di agenti AI open source (sempre più diffusi anche tra
  sviluppatori italiani/hobbisti) vanno trattati con la stessa cautela di un server esposto
  su internet, non come un giocattolo. Buon collegamento con altri articoli RobyRoot su AI
  e sicurezza. Menzionare anche che PraisonAI ha avuto più CVE in rapida successione
  (path traversal, RCE, SQL injection) — segnale di un progetto che sta crescendo più
  velocemente della sua maturità in sicurezza.
---

Negli ultimi mesi i framework open source per costruire "agenti AI" — cioè assistenti basati su modelli linguistici capaci non solo di rispondere, ma anche di eseguire azioni concrete come scrivere file, lanciare comandi o richiamare altri programmi — sono diventati popolarissimi tra sviluppatori e appassionati. Uno di questi si chiama **PraisonAI**, ed è finito sotto i riflettori per un motivo poco piacevole: una falla che permetteva di ottenere **accesso root completo semplicemente scrivendo un messaggio nella chat**.

## Cos'è PraisonAI

PraisonAI è un framework open source pensato per orchestrare agenti AI: in pratica, permette di costruire flussi di lavoro automatizzati in cui uno o più "agenti" basati su modelli linguistici collaborano per portare a termine compiti — scrivere codice, elaborare documenti, interagire con altri sistemi. Uno dei suoi componenti si chiama **AICoder**, ed è pensato proprio per far scrivere codice all'agente AI e farlo eseguire in autonomia.

## Il problema: zero controlli su cosa scrive e cosa esegue l'AI

La vulnerabilità, catalogata come **CVE-2026-61445**, ha un punteggio di gravità di **9,4 su un massimo di 10** — nella fascia "critica". Il problema è semplice da spiegare anche se tecnicamente delicato: il componente AICoder **non validava correttamente i percorsi dei file né sanificava i comandi** generati a partire dalle richieste fatte in chat.

Tradotto: un attaccante poteva scrivere un messaggio nella chat dell'applicazione — quello che in gergo si chiama **prompt injection**, cioè un input pensato per manipolare il comportamento del modello AI e fargli fare cose che non dovrebbe — e convincere l'agente a scrivere file in **qualsiasi posizione del filesystem** e a **eseguire comandi shell arbitrari con privilegi di root**. Tutto questo senza bisogno di autenticarsi prima, con un attacco a bassa complessità che non richiede alcuna interazione da parte di un utente legittimo.

In pratica, l'AI dell'applicazione — che avrebbe dovuto limitarsi a scrivere codice per l'utente — diventava lo strumento con cui l'attaccante prendeva il controllo dell'intero server.

## Perché è stata scansionata così in fretta

Un dato interessante emerso dall'analisi di questa (e di altre) vulnerabilità recenti in PraisonAI è la velocità con cui gli scanner automatici hanno iniziato a testare le installazioni esposte online: nel caso di un bug simile trovato nello stesso progetto qualche settimana prima, il probing è iniziato appena **3 ore e 44 minuti** dopo la divulgazione pubblica. Un promemoria di quanto, oggi, il tempo tra "una falla viene resa nota" e "qualcuno la sta già sfruttando su scala" si sia ridotto quasi a zero.

## Non è un caso isolato

CVE-2026-61445 non è l'unico problema di sicurezza scovato di recente in PraisonAI: nello stesso periodo sono stati segnalati anche un altro bug di esecuzione di codice remoto (RCE), un'iniezione SQL/CQL tramite un parametro non validato, e in precedenza persino un componente API che aveva l'autenticazione **disabilitata di default** per errore di configurazione. Un progetto open source cresciuto rapidamente in popolarità, insomma, che a quanto pare fatica un po' a tenere il passo sul fronte della sicurezza.

## Cosa significa per chi usa strumenti come questo

Questa vicenda è un buon esempio di un problema più ampio che riguarda tutto l'ecosistema degli agenti AI "agentici": dare a un modello linguistico la capacità di scrivere ed eseguire codice reale sul tuo sistema è potente, ma introduce una superficie d'attacco completamente nuova. Se l'input arriva da utenti non fidati (una chat esposta pubblicamente, per esempio), ogni comando che l'agente esegue va trattato con lo stesso sospetto con cui tratteresti un input arrivato da un modulo web non validato.

## Cosa fare

- Se usi PraisonAI, **aggiorna immediatamente alla versione 4.6.78 o successiva**, che corregge questa falla;
- **Non esporre mai** l'interfaccia chat di un agente AI con capacità di scrittura/esecuzione file a utenti non fidati o direttamente su internet, senza un livello di autenticazione e sandboxing adeguato;
- Se gestisci un progetto di questo tipo, valuta di far girare gli agenti AI in ambienti isolati (container, macchine virtuali dedicate) con permessi minimi, così che anche in caso di exploit il danno resti contenuto;
- Tieni d'occhio gli aggiornamenti di sicurezza dei framework AI open source che usi: sono progetti giovani, in rapidissima evoluzione, e — come dimostra questo caso — non sempre la sicurezza tiene il passo con le nuove funzionalità.

Il messaggio di fondo, valido ben oltre PraisonAI: più un'AI ha "le mani" per agire sul tuo sistema, più va trattata come un utente potenzialmente ostile finché non dimostra il contrario.
