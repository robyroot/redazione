---
title: "Squidbleed: il bug nel proxy Squid ha 29 anni ed è ancora lì — come proteggersi"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/06/29-year-old-squid-proxy-bug-squidbleed.html"
data_notizia: "2026-06-22"
tags: ["sicurezza", "squid", "proxy", "vulnerabilità", "CVE", "sysadmin"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Squidbleed è praticamente assente in italiano (solo un accenno ACN). La storia è ottima: bug con nome evocativo, radici nel 1997, impatto reale su reti aziendali/scolastiche/hotspot Wi-Fi. Il confronto con Heartbleed funziona benissimo per il pubblico italiano. Aggiungere i comandi pratici per chi gestisce Squid.
---

# Squidbleed: il bug nel proxy Squid ha 29 anni ed è ancora lì — come proteggersi

Un bug introdotto nel codice di Squid Proxy nel **1997** è rimasto nascosto per quasi tre decenni, e ora ha un nome: **Squidbleed** (CVE-2026-47729). I ricercatori di Calif.io lo hanno scoperto e reso pubblico questa settimana, e il paragone con Heartbleed — la famosissima vulnerabilità di OpenSSL del 2014 — non è casuale: anche Squidbleed fa trapelare memoria interna, e in certi scenari può esporre credenziali di altri utenti che condividono lo stesso proxy.

Se gestisci un proxy Squid in un ufficio, una scuola, o un hotspot Wi-Fi pubblico, fermati qui e leggi fino in fondo.

## Come funziona Squidbleed

La vulnerabilità si trova nel parser FTP di Squid, nella parte che gestisce le risposte dei vecchi server NetWare. Quando Squid analizza l'output di un comando FTP `LIST`, esegue un loop per cercare il nome del file usando `strchr`. Se un server FTP ostile manda una risposta troncata — una riga che finisce esattamente sul carattere nullo terminatore, senza il nome file — la funzione `strchr` scambia quel `\0` per l'inizio del nome da cercare, e il loop continua a leggere **oltre i limiti del buffer**, dentro la memoria heap adiacente.

Quella memoria heap? Squid la riutilizza senza azzerarla. Quindi contiene quasi integralmente la richiesta HTTP più recente di un altro utente: header `Authorization`, cookie, token API, tutto quanto.

```
[server FTP malevolo] → riga troncata →
[Squid legge oltre il buffer] → 
[restituisce memoria heap con dati di altri utenti]
```

È un **heap over-read**, esattamente come Heartbleed. E come Heartbleed, la cosa più inquietante è la semplicità: nessun'exploit sofisticato, solo una risposta FTP malformata.

## Chi è a rischio

Squidbleed non è una vulnerabilità da internet aperto. Per sfruttarla, l'attaccante deve già avere accesso al proxy — deve essere un utente legittimo dello stesso Squid. Questo la rende particolarmente pericolosa in ambienti **condivisi**:

- **Reti aziendali** dove tutto il traffico web passa per un proxy Squid
- **Istituti scolastici** con decine o centinaia di utenti sullo stesso proxy
- **Hotspot Wi-Fi pubblici** che usano Squid per il content filtering
- **Reti universitarie**

In pratica, un dipendente (o studente) scontento potrebbe leggere le credenziali dei colleghi semplicemente puntando il proprio client verso un server FTP controllato mentre usa il proxy.

Il CVSS è 6.5 (moderato), ma in contesti aziendali con traffico HTTP non cifrato il rischio reale è più alto di quanto il numero suggerisca.

## Lo stato delle patch

Attenzione: c'è stata confusione nella comunicazione. Il maintainer di Squid, Amos Jeffries, ha precisato che **Squid 7.6 NON contiene la fix di Squidbleed**. La versione 7.6 risolve una vulnerabilità diversa (CVE-2026-50012). La patch per CVE-2026-47729 è pianificata per **Squid 7.7**.

Finché 7.7 non è disponibile, la mitigazione consigliata dai ricercatori è semplice: **disabilitare il supporto FTP in Squid**.

## Come verificare la versione di Squid e mitigare

Controlla la versione installata:

```bash
squid -v | head -1
```

Per disabilitare il gateway FTP in Squid, aggiungi (o modifica) in `/etc/squid/squid.conf`:

```squid
# Disabilita il gateway FTP - mitigazione Squidbleed CVE-2026-47729
ftp_list_width 0
# oppure nega tutto il traffico FTP
acl FTP proto FTP
http_access deny FTP
```

Dopo la modifica, riavvia il servizio:

```bash
sudo systemctl reload squid
# oppure, se reload non è sufficiente:
sudo systemctl restart squid
```

Per verificare che la configurazione sia corretta:

```bash
sudo squid -k parse
```

Su sistemi con molti utenti, vale anche la pena verificare se il traffico FTP è effettivamente usato controllando i log:

```bash
grep " FTP " /var/log/squid/access.log | tail -20
```

Se non vedi traffico FTP, disabilitarlo è a costo zero e ti copre completamente.

## Perché un bug del 1997 è ancora lì

La risposta onesta è che Squid è un progetto di infrastruttura critica mantenuto da poche persone, con milioni di installazioni in produzione e anni di codice legacy accumulato. Il parser FTP non veniva toccato da decenni perché "funzionava" — nessuno ha avuto incentivo a rivedere codice funzionante scritto per server NetWare che oggi quasi non esistono più.

È lo stesso motivo per cui Heartbleed è rimasto nascosto per due anni in OpenSSL: codice vecchio, poco mantenuto, usato ovunque. La differenza è che Squidbleed è confinato a scenari specifici (FTP + proxy condiviso), mentre Heartbleed era universale.

Il takeaway pratico: se usi Squid, disabilita FTP adesso, e tieni d'occhio il rilascio di Squid 7.7. Se non usi Squid ma gestisci altra infrastruttura di rete, questa storia è un buon promemoria per andare a guardare cosa gira ancora sui vostri server con codice scritto nel secolo scorso.
