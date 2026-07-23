---
title: "NetworkManager 1.58: addio dhclient, benvenuto Wi-Fi 6GHz e tunnel GENEVE"
rilevanza: "MEDIA"
fonte: "https://9to5linux.com/networkmanager-1-58-officially-released-with-new-features-and-improvements"
data_notizia: "2026-07-20"
tags: ["linux", "networkmanager", "rete", "wifi", "ipv6", "open-source", "networking"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Articolo pratico focalizzato su cosa cambia per gli utenti Linux desktop e server. Spiegare la rimozione di dhclient e cosa fare se si hanno script che lo usavano ancora.
---

# NetworkManager 1.58: addio dhclient, benvenuto Wi-Fi 6GHz e tunnel GENEVE

Il 20 luglio 2026 è uscita **NetworkManager 1.58**, la nuova versione del gestore di connessioni di rete che trovi praticamente su tutte le distribuzioni Linux desktop e su molti server. Dieci settimane di sviluppo per un aggiornamento che porta alcune novità significative — e almeno una breaking change che è bene conoscere prima di aggiornare.

## Addio dhclient, per sempre

La notizia più importante per chi amministra sistemi Linux: **dhclient è stato rimosso definitivamente**. Non è deprecato, non è opzionale: è sparito.

`dhclient` era il client DHCP storico, presente su Linux praticamente da sempre. Per anni NetworkManager lo aveva supportato come backend alternativo accanto al proprio client DHCP interno. Con la versione 1.58, la scelta è fatta: si usa il client DHCP interno di NetworkManager e basta.

La maggior parte degli utenti non si accorgerà di niente — se non avevi mai toccato la configurazione DHCP di NetworkManager, il cambio è trasparente. Ma se hai script o configurazioni che richiamano esplicitamente `dhclient` come backend, dovrai aggiornarli:

```bash
# Verifica se hai ancora impostato dhclient nel file di configurazione
grep -i dhcp /etc/NetworkManager/NetworkManager.conf

# Se trovi "dhcp=dhclient", sostituiscila con:
# [main]
# dhcp=internal
```

Oltre a dhclient, viene deprecato il supporto alle **Wireless Extensions** (WEXT), la vecchia API per la gestione Wi-Fi. NetworkManager 1.58 richiede ora il moderno stack **nl80211**. Quasi tutti i driver Linux recenti lo supportano già, ma se hai hardware molto datato potresti incontrare qualche problema.

## Wi-Fi 6GHz: finalmente supportato

Buone notizie per chi ha un router Wi-Fi 6E o Wi-Fi 7: NetworkManager 1.58 introduce il supporto alla **banda 6GHz** nella gestione delle connessioni wireless.

Ora puoi forzare una connessione a usare specificamente la banda 6GHz dalla configurazione o dalla riga di comando:

```bash
# Modifica una connessione esistente per usare solo la banda 6GHz
nmcli connection modify "NomeRete" 802-11-wireless.band 6GHz

# Oppure specifica la banda durante la creazione di una nuova connessione
nmcli con add type wifi ssid "NomeRete" \
  802-11-wireless.band 6GHz \
  802-11-wireless.channel 0
```

Utile per chi vuole ottimizzare le connessioni su reti moderne, evitando la congestione delle bande 2.4GHz e 5GHz ormai sempre più affollate.

## GENEVE e 464XLAT: per il networking avanzato

Per gli amministratori di sistemi più esperti, ci sono due aggiunte importanti.

**GENEVE** (Generic Network Virtualization Encapsulation) è un protocollo di tunneling usato in ambienti cloud e datacenter per instradare traffico tra hypervisor e switch virtuali. Con NetworkManager 1.58 puoi creare e gestire interfacce GENEVE direttamente via `nmcli`:

```bash
# Crea un'interfaccia GENEVE
nmcli con add type geneve \
  con-name "geneve-tunnel" \
  ifname geneve0 \
  geneve.id 100 \
  geneve.remote 192.168.1.10
nmcli con up geneve-tunnel
```

**464XLAT/CLAT** (Customer-side Translator) risolve invece un problema pratico delle reti IPv6-only: le applicazioni legacy che parlano solo IPv4. NetworkManager 1.58 può creare automaticamente un'interfaccia CLAT virtuale che intercetta il traffico IPv4 uscente e lo traduce in IPv6, permettendo alle app legacy di funzionare su reti moderne senza nessuna modifica al codice applicativo.

È una tecnologia sempre più rilevante mentre gli ISP accelerano la transizione verso IPv6-only.

## Stato managed persistente tra i riavvii

Una piccola ma utile aggiunta: ora puoi configurare che lo stato "managed/unmanaged" delle interfacce di rete persista tra i riavvii. Prima, alcune configurazioni si perdevano al reboot; ora puoi controllarlo esplicitamente via `nmcli`:

```bash
# Imposta un'interfaccia come unmanaged e mantieni l'impostazione ai riavvii
nmcli device set eth0 managed no

# Verifica lo stato
nmcli device show eth0 | grep MANAGED
```

Utile per chi vuole che NetworkManager non tocchi determinate interfacce (ad esempio quelle gestite manualmente o da altri strumenti come Docker o Podman).

## Miglioramenti alla sicurezza

NetworkManager 1.58 introduce la **certificate access verification** per le connessioni private: il sistema verifica che i certificati usati per connessioni sicure (VPN, Wi-Fi Enterprise) siano accessibili correttamente, riducendo il rischio di errori di configurazione che possono portare a connessioni non cifrate silenziosamente.

Vengono anche corretti alcuni problemi di **memory safety** nel client DHCPv4 interno — nulla di critico, ma manutenzione preventiva importante.

## Come verificare e aggiornare

La 1.58 sta arrivando gradualmente nei repository delle distribuzioni principali. Per vedere cosa hai installato:

```bash
nmcli --version
# Oppure
NetworkManager --version
```

Su Debian/Ubuntu arriverà presto negli aggiornamenti stabili; Fedora e Arch la riceveranno nei prossimi giorni. Se gestisci sistemi dove `dhclient` è usato come backend esplicito, controlla prima la tua configurazione in `/etc/NetworkManager/NetworkManager.conf` — è l'unica cosa da verificare prima di aggiornare per evitare sorprese.
