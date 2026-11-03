---
title: "Quad9 abbandona la Francia il 24 novembre: cosa significa per la privacy DNS in Europa"
rilevanza: "ALTA"
fonte: "https://www.eff.org/issues/privacy"
data_notizia: "2026-10-28"
tags: ["privacy", "dns", "quad9", "europa", "censura", "diritti digitali"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: privacy DNS e pressione legale sull'infrastruttura internet in Europa, con focus sulle alternative disponibili per gli utenti italiani. Utile per sensibilizzare sul tema DNS-over-HTTPS.
---

# Quad9 abbandona la Francia il 24 novembre: cosa significa per la privacy DNS in Europa

Quad9, il resolver DNS focalizzato sulla privacy, ha annunciato che dal 24 novembre 2026 smetterà di servire gli utenti francesi. Non è solo un problema francese: è un segnale preoccupante per la privacy digitale in tutta Europa, Italia inclusa.

## Cos'è Quad9 e perché è importante

Quad9 (l'indirizzo è 9.9.9.9) è un resolver DNS non-profit con sede in Svizzera, nato con una missione chiara: offrire un servizio DNS che non registra gli indirizzi IP degli utenti, blocca i domini malevoli conosciuti e non vende i dati a terzi.

Per capire perché è importante bisogna ricordare come funziona il DNS: ogni volta che digiti un indirizzo nel browser, il tuo computer interroga un server DNS per tradurre il nome del sito (es. `robyroot.net`) in un indirizzo IP. Questo server vede tutto ciò che visiti. Google (8.8.8.8) e Cloudflare (1.1.1.1) sono i resolver più usati, ma entrambi sono aziende commerciali con i propri interessi sui dati.

Quad9 è l'alternativa pensata per chi vuole più controllo sulla propria privacy in rete, senza cedere queste informazioni a nessuno.

## Perché se ne va dalla Francia

Il problema è legale. Sony Music France ha intentato una causa chiedendo a Quad9 di bloccare l'accesso a determinati siti di pirateria tramite il proprio resolver DNS. Il tribunale francese ha dato ragione a Sony, ordinando a Quad9 di filtrare specifici domini.

Quad9 ha preferito ritirarsi completamente dalla Francia piuttosto che compromettere la propria policy di neutralità: il servizio blocca solo i domini malevoli (malware, phishing), non quelli soggetti a richieste commerciali o censura basata su copyright.

La ritirata è la conclusione di una lunga battaglia legale e segnala un problema strutturale: i resolver DNS privati, anche quelli non-profit, operano in un contesto legale sempre più complicato in Europa.

## L'impatto per gli utenti europei

Se sei in Francia, dal 24 novembre 9.9.9.9 non risponderà più alle tue query. Ma la situazione merita attenzione anche in Italia:

- **Precedente legale**: la decisione francese potrebbe fare scuola per richieste simili in altri paesi UE
- **Modello da replicare**: se i titolari di diritti iniziano a usare sistematicamente questa strategia legale, altri resolver privacy-friendly potrebbero trovarsi nella stessa posizione
- **Dipendenza da un singolo provider**: se usi solo Quad9, è il momento di pensare a un backup

## Alternative privacy-friendly a Quad9

Ecco alcune opzioni valide se cerchi un resolver DNS che rispetti la tua privacy:

```bash
# Cloudflare con blocco malware (1.1.1.2) e senza logging
# Non è non-profit ma ha una policy privacy robusta
echo "nameserver 1.1.1.2" | sudo tee /etc/resolv.conf

# AdGuard DNS - blocca annunci e tracker, no log
echo "nameserver 94.140.14.14" | sudo tee /etc/resolv.conf

# NextDNS - altamente personalizzabile, piano gratuito disponibile
# Registrati su nextdns.io per ottenere un ID univoco

# Mantenere Quad9 (per ora funziona ancora in Italia)
echo "nameserver 9.9.9.9" | sudo tee /etc/resolv.conf
```

## Configura DNS over HTTPS per proteggerti meglio

La vera protezione contro il filtraggio DNS passa dal DNS over HTTPS (DoH) o DNS over TLS (DoT): queste tecnologie cifrano le query DNS, rendendo molto più difficile intercettarle e filtrarle.

Su Linux con `systemd-resolved` è semplice da configurare:

```bash
# Modifica la configurazione di systemd-resolved
sudo nano /etc/systemd/resolved.conf
```

Aggiungi o modifica queste righe:

```ini
[Resolve]
DNS=9.9.9.9#dns.quad9.net
FallbackDNS=1.1.1.1#cloudflare-dns.com
DNSOverTLS=yes
DNSSEC=yes
```

Poi riavvia il servizio:

```bash
sudo systemctl restart systemd-resolved

# Verifica che il DoT sia attivo
resolvectl status | grep "DNS over TLS"
```

## Conclusioni

La ritirata di Quad9 dalla Francia non è solo una notizia tecnica: è un sintomo di come la pressione legale delle major dell'entertainment stia ridisegnando l'architettura di Internet in Europa. Per ora in Italia non cambia nulla, ma il precedente è preoccupante.

Il consiglio pratico è doppio: attiva DNS over HTTPS sul tuo sistema per rendere le tue query DNS molto più difficili da intercettare e filtrare, e non dipendere da un unico provider DNS — avere un server di fallback è sempre una buona idea.
