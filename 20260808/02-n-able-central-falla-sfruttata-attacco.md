---
title: "N-able N-central sotto attacco: una falla bypassa il login e apre le porte a migliaia di endpoint"
rilevanza: "ALTA"
fonte: "https://www.bleepingcomputer.com/news/security/n-able-warns-of-n-central-auth-bypass-flaw-exploited-in-attacks/"
data_notizia: "2026-08-08"
tags: ["cybersecurity", "vulnerabilità", "rmm", "sysadmin"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: spiegare perché un bug in un software RMM è pericoloso "al quadrato"
  (compromette non un solo sistema ma tutta la catena di endpoint gestiti da un MSP).
  Utile collegarlo al tema supply chain / fiducia negli strumenti di gestione centralizzata,
  e dare indicazioni concrete per chi amministra o usa MSP in Italia (verificare versione,
  contattare il proprio fornitore di servizi gestiti).
---

Se lavori nell'IT, probabilmente conosci il concetto di RMM (Remote Monitoring and Management): sono quelle piattaforme che permettono a un reparto IT o a un MSP (Managed Service Provider) di controllare da un'unica console server, workstation, dispositivi di rete e tutto il parco macchine dei clienti. Utilissime, finché non diventano loro stesse il bersaglio. Ed è esattamente quello che sta succedendo a **N-able N-central**, una delle piattaforme RMM più diffuse al mondo.

## Il problema: CVE-2026-18577

La falla si chiama **CVE-2026-18577**, ha un punteggio CVSS di 8.2 ed è un bypass di autenticazione. Detto semplice: un attaccante remoto, **senza avere alcuna credenziale valida**, può aggirare il login e ottenere accesso amministrativo completo al server N-central. Da lì, può usare le funzionalità legittime della piattaforma — pensate progettate per aiutare i tecnici — per raggiungere tutti i sistemi gestiti a valle.

La cosa interessante (e un po' preoccupante) è che questa non è una falla nuova di zecca partita da zero: è il risultato di una **patch incompleta** per una vulnerabilità precedente, CVE-2026-18556, che a sua volta era già un bypass di autenticazione "tramite percorso alternativo". In pratica gli attaccanti hanno trovato un'altra strada per aggirare la correzione che avrebbe dovuto chiudere il problema originale.

## Come stanno agendo gli attaccanti

N-able ha notato i primi segnali il 31 luglio 2026, sotto forma di anomalie nelle licenze, e ha confermato lo sfruttamento attivo il 2 agosto. Una volta dentro, gli attaccanti sfruttano la funzione **"Take Control"** — pensata per permettere ai tecnici di connettersi da remoto agli endpoint dei clienti per assistenza — per raggiungere le macchine gestite. E qui arriva la parte più subdola: per garantirsi un accesso persistente anche dopo che l'accesso al server N-central viene revocato, gli attaccanti registrano un servizio che crea un **Cloudflare Tunnel**, uno strumento legittimo che però, usato così, diventa una backdoor difficile da individuare perché il traffico passa attraverso l'infrastruttura di Cloudflare invece che attraverso canali "sospetti" più facilmente bloccabili.

## Perché conta più del solito

Un bug del genere in un software RMM non è "solo" una falla in più: è un moltiplicatore. Un server N-central compromesso non espone un'unica azienda, ma potenzialmente **tutti i clienti gestiti da quell'istanza**, che si tratti di un reparto IT interno o — più spesso — di un MSP che serve decine o centinaia di aziende clienti. È lo stesso principio per cui gli attacchi alla supply chain del software fanno tanta paura: colpendo un solo punto centrale, si guadagna accesso a un numero enorme di sistemi a valle.

## Cosa fare

N-able ha rilasciato un hotfix, la versione **2026.3.1.7** (indicata anche come "2026.3 Hotfix 1"), il 2 agosto, seguita il 6 agosto da un secondo hotfix con mitigazioni aggiuntive per rafforzare la correzione. Le distribuzioni **hosted** (cioè quelle gestite direttamente da N-able in cloud) sono già state aggiornate automaticamente. Chi invece usa un'installazione **on-premise** deve applicare l'aggiornamento manualmente, e visto lo sfruttamento attivo confermato, non è il caso di rimandare.

Se in azienda usate N-central direttamente, controllate subito la versione installata e applicate l'hotfix. Se invece vi appoggiate a un MSP esterno per la gestione IT, ha senso fare una domanda diretta al vostro fornitore: "usate N-central, e se sì, avete già applicato la patch per CVE-2026-18577?". Non è invadenza, è due minuti ben spesi per verificare che la catena di fiducia su cui si basa tutto il vostro outsourcing IT sia effettivamente solida.

La vicenda, tra l'altro, insegna una lezione più generale valida ben oltre N-able: quando viene corretta una vulnerabilità di bypass dell'autenticazione, vale la pena verificare — soprattutto per chi sviluppa o gestisce software critici — che la correzione chiuda davvero tutte le porte, e non solo quella trovata dal primo ricercatore.
