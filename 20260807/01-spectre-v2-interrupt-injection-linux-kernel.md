---
title: "Interrupt Injection: la nuova falla Spectre v2 che il kernel Linux ha appena patchato"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/08/new-interrupt-injection-attack-can.html"
data_notizia: "2026-08-07"
tags: ["linux kernel", "spectre", "cybersecurity", "cpu vulnerability", "sicurezza"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: spiegare in modo semplice cos'è Spectre v2 senza scadere nel tecnicismo puro,
  concentrandosi su "cosa devo fare io, oggi, sul mio PC Linux". Buona occasione per un box
  pratico con i comandi per verificare la versione del kernel e come aggiornare su Arch, Debian/Ubuntu
  e Fedora. Possibile collegamento a un futuro articolo su come funzionano gli attacchi speculative
  execution in generale (Meltdown/Spectre timeline).
---

Se pensavate che Spectre, la famiglia di vulnerabilità hardware che ha terrorizzato l'industria a partire dal 2018, fosse ormai storia archiviata, avete un motivo in più per aggiornare il kernel questa settimana. Un gruppo di ricercatori del MIT CSAIL ha scoperto una nuova variante chiamata **Interrupt Injection**, catalogata come **CVE-2026-68480**, che riesce a bypassare proprio le difese pensate per bloccare Spectre v2 sui processori AMD e, con qualche cautela in più, anche su quelli Intel.

Greg Kroah-Hartman, il mantainer che tiene le redini dei kernel stabili Linux, ha già rilasciato le patch: **6.18.43**, **6.6.149** e **6.1.181**. Non è finita qui: sono usciti anche aggiornamenti per i rami LTS più vecchi, **5.10.263** e **5.15.214**, perché la falla tocca anche il meccanismo Safe-RET che AMD usa per mitigare gli attacchi Speculative Return Stack Overflow sui processori Zen, dalla prima alla quarta generazione.

## Come funziona, in parole povere

Spectre v2 sfrutta l'esecuzione speculativa: le CPU moderne, per andare più veloci, "indovinano" quale ramo di codice verrà eseguito e lo eseguono in anticipo, buttando via il risultato se hanno sbagliato. Il problema è che, anche se il risultato viene scartato, resta una traccia misurabile nella cache, e da quella traccia un attaccante può risalire a dati che non dovrebbe vedere — tipo la memoria del kernel.

Safe-RET era una delle contromisure per chiudere questa falla: crea una finestra temporale in cui il processore verifica che il salto di ritorno sia legittimo prima di eseguire codice speculativo. Il trucco scoperto dai ricercatori MIT è che questa finestra, su un Zen 2, dura appena **due istruzioni, sei byte**. Se un attaccante riesce a far scattare un interrupt hardware con precisione al nanosecondo proprio dentro quella finestra, riesce a infilarci dentro l'esecuzione speculativa e leggere memoria che non gli appartiene.

Il numero che fa più impressione non è la velocità — 5,47 byte al secondo non sono un downpload fulmineo — ma l'accuratezza: **91,97%**. Con quella precisione, e un po' di pazienza, un processo senza privilegi su una macchina Linux 6.14 con tutte le mitigazioni Spectre v2 attive è riuscito a localizzare e leggere `/etc/shadow`, il file che su Linux contiene gli hash delle password di sistema.

## Chi deve preoccuparsi davvero

Va detto subito: questo non è un attacco che un sito web malevolo può lanciarvi contro navigando. Serve eseguire codice non privilegiato sulla macchina bersaglio, quindi il rischio reale riguarda soprattutto:

- **Server condivisi e hosting multi-tenant**, dove utenti diversi (magari con account limitati o container) girano sullo stesso hardware fisico;
- **Ambienti cloud e VPS economici**, dove non sempre si sa con certezza chi altro condivide la CPU fisica;
- **Postazioni condivise** in ambito universitario o aziendale.

Per il classico utente desktop Linux che usa il PC da solo, il rischio pratico è più basso — ma "più basso" non vuol dire "zero", ed è comunque una buona occasione per fare l'aggiornamento che probabilmente stavate rimandando.

AMD ha confermato la falla e pubblicato un bollettino a supporto della patch del kernel. Intel, dal canto suo, sostiene che le mitigazioni già in campo siano sufficienti, anche se alcuni ricercatori fanno notare che uno sfruttamento sulla loro architettura resta teoricamente possibile.

## Cosa fare adesso

La buona notizia è che il fix è già disponibile, quindi il lavoro da fare è quasi tutto meccanico:

1. **Controllate la versione del kernel** con `uname -r`.
2. **Aggiornate il sistema** con il gestore pacchetti della vostra distro (`pacman -Syu` su Arch, `apt update && apt upgrade` su Debian/Ubuntu, `dnf upgrade` su Fedora).
3. Se usate un kernel LTS "storico" (5.10 o 5.15), assicuratevi che il vostro pacchetto punti almeno alle versioni patchate indicate sopra.
4. **Riavviate**: le patch per le vulnerabilità speculative execution vengono applicate a livello di kernel e microcodice, quindi serve un reboot perché abbiano effetto reale.

Non serve panico, ma nemmeno procrastinare troppo: le vulnerabilità Spectre hanno la brutta abitudine di restare sfruttabili per anni dopo la scoperta, proprio perché toccano l'hardware e non solo il software. Meglio chiudere la porta finché è ancora un esercizio accademico da laboratorio MIT, e non uno strumento nel kit di un attaccante reale.
