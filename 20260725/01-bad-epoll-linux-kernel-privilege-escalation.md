---
title: "Bad Epoll: il bug del kernel Linux che dà i permessi di root a chiunque"
rilevanza: "ALTA"
fonte: "https://www.linuxcompatible.org/story/linux-security-roundup-for-week-29-2026"
data_notizia: "2026-07-18"
tags: ["linux", "sicurezza", "kernel", "vulnerabilità", "privilege-escalation"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Spiegare la vulnerabilità in modo chiaro anche ai non esperti, con consigli pratici su come verificare la versione del kernel e aggiornare. Ottimo per enfatizzare l'importanza degli aggiornamenti del kernel.
---

# Bad Epoll: il bug del kernel Linux che dà i permessi di root a chiunque

Avete aggiornato il kernel ultimamente? Se la risposta è no, forse è il momento di farlo. Una vulnerabilità battezzata **Bad Epoll** è stata scoperta nel kernel Linux e permette a qualsiasi utente normale — senza privilegi speciali — di diventare root in pochi secondi. Sì, avete letto bene: da utente normale a superutente completo, senza password.

## Come funziona Bad Epoll

Il bug si trova nell'**epoll subsystem**, un meccanismo che Linux usa per monitorare più descrittori di file contemporaneamente in modo efficiente. È uno strumento fondamentale per applicazioni web, server, e qualsiasi programma che gestisce connessioni multiple.

Il problema è una classica vulnerabilità **use-after-free**: due parti diverse del kernel tentano di pulire lo stesso oggetto interno contemporaneamente. È come se due camerieri cercassero di sparecchiare lo stesso tavolo nello stesso momento — prima o poi qualcosa va a finire male, e in questo caso "male" significa che un attaccante può sfruttare la finestra temporale per manipolare la memoria del kernel.

Il risultato? Privilege escalation locale. Un qualsiasi processo in esecuzione con permessi normali può sfruttare questo bug per eseguire codice con i pieni privilegi di root.

## Chi è a rischio?

Praticamente chiunque utilizzi un sistema Linux non aggiornato. La vulnerabilità colpisce una vasta gamma di versioni del kernel, il che la rende particolarmente pericolosa in ambienti aziendali dove gli aggiornamenti vengono rimandati per motivi di compatibilità.

L'aspetto più preoccupante è che **non serve alcun tipo di accesso privilegiato** per sfruttarla. Basta avere un account normale sul sistema — anche un utente con pochissimi permessi può diventare root.

## Come proteggersi

La buona notizia è che i maintainer del kernel hanno già rilasciato le patch. Le versioni corrette sono state incluse nelle ultime release stabili, tra cui le sei versioni LTS rilasciate il 24 luglio 2026 (da 5.10.261 a 6.18.40) e la versione 7.1.5.

Per verificare la versione del kernel che state usando:

```bash
uname -r
```

Per aggiornare il kernel su distribuzioni basate su Debian/Ubuntu:

```bash
sudo apt update && sudo apt full-upgrade
```

Su Fedora/RHEL:

```bash
sudo dnf update kernel
```

Su Arch Linux:

```bash
sudo pacman -Syu
```

Dopo l'aggiornamento, è necessario riavviare il sistema per caricare il nuovo kernel. Non basta installare il pacchetto: finché non si riavvia, il sistema continua a girare sul kernel vecchio e vulnerabile.

## Verificare dopo il riavvio

Dopo il reboot, controllate che il kernel aggiornato sia effettivamente in uso:

```bash
uname -r
```

Se gestite più server, potete verificare la versione del kernel in remoto con:

```bash
ssh utente@server "uname -r"
```

Oppure, per una panoramica rapida su un gruppo di host:

```bash
for host in server1 server2 server3; do
  echo "$host: $(ssh $host uname -r)"
done
```

## Perché questa vulnerabilità è seria

Bad Epoll rientra nella categoria delle vulnerabilità più pericolose per i sistemi Linux: la **local privilege escalation**. A differenza delle vulnerabilità remote (che permettono attacchi dall'esterno senza alcun accesso), questo tipo di bug richiede già un accesso al sistema — ma una volta dentro, il danno è totale.

In uno scenario aziendale, questo significa che un dipendente malintenzionato, un account compromesso, o un container Docker con una fuga potrebbero usare questo bug per prendere il controllo completo del server host. Non è fantascienza: è uno scenario realistico in ambienti multi-tenant o condivisi.

Vale la pena ricordare che epoll viene usato praticamente in ogni applicazione server moderna — da Node.js a nginx, da Redis a PostgreSQL. La superficie d'attacco è quindi enorme.

## Conclusione

Aggiornate il kernel. È il solito consiglio, lo sappiamo, ma Bad Epoll dimostra ancora una volta perché è fondamentale non rimandare. La buona notizia è che la comunità Linux ha risposto velocemente con patch rilasciate in tempi record — esattamente come dovrebbe funzionare il processo di sicurezza open source.

Se avete sistemi critici da aggiornare e non potete permettervi downtime immediato, pianificate una finestra di manutenzione urgente. Questa vulnerabilità non è da sottovalutare: privilege escalation locale a root, su praticamente qualsiasi sistema Linux non aggiornato, è il tipo di bug che i threat actor cercano attivamente.
