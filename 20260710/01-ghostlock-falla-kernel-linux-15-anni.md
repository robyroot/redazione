---
title: "GhostLock: la falla nel kernel Linux che si nascondeva da 15 anni (e ora ha un exploit pubblico)"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/15-year-old-ghostlock-flaw-enables-root.html"
data_notizia: "2026-07-10"
tags: ["linux", "kernel", "sicurezza", "cve", "vulnerabilità", "container"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: taglio pratico "cosa devi fare oggi stesso". Spiegare bene la differenza tra
  vulnerabilità locale (serve un accesso, non è remota) e perché comunque è gravissima su server
  multi-utente, hosting condiviso e ambienti containerizzati (Docker/Kubernetes). Vale la pena
  aggiungere un box con i comandi per verificare la versione del kernel e capire se si è esposti.
  Buon gancio anche per parlare di come funzionano i bug bounty (kernelCTF di Google).
---

Se gestisci un server Linux, un NAS, un cluster Kubernetes o anche solo il tuo PC con più utenti, oggi c'è una notizia che merita la tua attenzione: si chiama **GhostLock**, ha il nome ufficiale di **CVE-2026-43499**, ed è una falla che si nasconde nel cuore del kernel Linux da **ben 15 anni**. Sì, hai letto bene: dal 2011.

## Cos'è di preciso

GhostLock è una vulnerabilità di tipo *use-after-free* che si trova nel codice del kernel che gestisce i **rt_mutex**, i mutex a priorità ereditata usati dal sottosistema **futex** (quello che coordina la sincronizzazione tra processi e thread). In parole povere: il kernel, in certe condizioni, continua a usare un pezzo di memoria che ha già "liberato", e questo apre la porta a chi sa come sfruttarlo.

Il problema è stato scoperto dai ricercatori di **Nebula Security**, che l'hanno soprannominato GhostLock come seconda parte di una ricerca più ampia (chiamata "IonStack"). Il bug è così vecchio che è presente praticamente in **ogni distribuzione Linux mainstream rilasciata dal 2011 in poi**: Ubuntu, Debian, Fedora, RHEL, CentOS, AlmaLinux, CloudLinux e chi più ne ha più ne metta.

## Perché fa così paura

Qui arriva la parte davvero preoccupante: per sfruttarla **non serve nessun privilegio speciale**. Nessuna configurazione particolare, nessun accesso di rete, nessun trucco esotico. Bastano normali chiamate di threading che qualsiasi programma locale può fare. Un utente qualsiasi, anche il meno privilegiato del sistema, può usarla per diventare **root** in pochi secondi.

E non finisce qui: l'exploit funziona anche **dall'interno di un container** per scappare verso l'host. Questo significa che se hai ambienti Docker o Kubernetes multi-tenant, dove diversi utenti o applicazioni condividono lo stesso kernel, GhostLock è un incubo reale. Un container "isolato" smette di esserlo.

Nebula ha trasformato la scoperta in un exploit funzionante che, nei loro test, ha un tasso di successo del **97%**. E - dettaglio non da poco - hanno pubblicato il codice dell'exploit, quindi ora è alla portata di chiunque voglia provarlo. Per la scoperta, Google ha premiato il team con **92.337 dollari** attraverso il programma di bug bounty kernelCTF.

## La buona notizia (relativa)

Al momento non risultano attacchi in circolazione che sfruttino GhostLock. La segnalazione è stata fatta responsabilmente a **security@kernel.org**, e il fix è già stato integrato nel ramo principale del kernel (commit `3bfdc63936dd`), disponibile a partire da **Linux 7.1**. Le distribuzioni basate su RHEL come AlmaLinux e CloudLinux hanno già rilasciato aggiornamenti o richieste di test per i loro kernel.

Ma con l'exploit pubblico e un bug così diffuso, la finestra tra "nessuno la sfrutta" e "tutti la sfruttano" può chiudersi in fretta.

## Cosa fare adesso

Se amministri sistemi Linux, la lista delle cose da fare è breve ma non rimandabile:

1. **Aggiorna il kernel** appena la tua distribuzione rilascia la patch (molte l'hanno già fatto o sono in fase di test).
2. Se usi **hosting condiviso, VPS multi-utente o ambienti container multi-tenant**, considera GhostLock una priorità assoluta: è esattamente lo scenario in cui questa falla fa più danni.
3. Controlla la versione del tuo kernel con `uname -r` e confrontala con le note di rilascio della tua distro per capire se sei già protetto.
4. Se non puoi aggiornare subito, valuta soluzioni di mitigazione temporanea (come restrizioni via seccomp o AppArmor/SELinux sui container più esposti), anche se la patch resta l'unica soluzione definitiva.

Questa storia è anche un promemoria interessante su come funziona la sicurezza open source: un bug vecchio 15 anni, sepolto in migliaia di righe di codice del kernel, scovato non da un attaccante ma da ricercatori che lo hanno segnalato responsabilmente prima che diventasse un problema per tutti. È il sistema che funziona come dovrebbe — a patto che tu faccia la tua parte e aggiorni.
