---
title: "Attacco supply chain su AUR: 1.500 pacchetti Arch compromessi dalla campagna Atomic Arch"
rilevanza: "ALTA"
fonte: "https://www.stepsecurity.io/blog/400-aur-packages-hijacked-atomic-arch-campaign"
data_notizia: "2026-06-11"
tags: ["arch-linux", "sicurezza", "supply-chain", "malware", "aur"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: urgente avviso di sicurezza per la comunità Arch/Manjaro/EndeavourOS
  italiana. Focus pratico su come controllare se si è stati colpiti e le azioni immediate da intraprendere.
---

# Attacco supply chain su AUR: 1.500 pacchetti Arch compromessi dalla campagna "Atomic Arch"

Se usi Arch Linux, Manjaro, EndeavourOS o qualsiasi altra distro basata su Arch con l'AUR abilitato,
devi leggere questo articolo *adesso*. Tra il 9 e il 12 giugno 2026 è stata scoperta una delle più
grandi campagne di attacco alla supply chain mai viste nella comunità Linux.

## Cosa è successo

La campagna, soprannominata **Atomic Arch**, ha preso di mira l'Arch User Repository (AUR), il
famosissimo repository comunitario dove chiunque può pubblicare pacchetti. Gli attaccanti hanno
sfruttato una funzionalità legittima dell'AUR: l'adozione di pacchetti *orfani*, cioè pacchetti i
cui maintainer originali avevano abbandonato.

In pratica, i criminali informatici hanno richiesto la manutenzione di oltre **1.500 pacchetti orfani**
su AUR, e dopo averla ottenuta, hanno modificato i file `PKGBUILD` — gli script che dicono agli AUR
helper come `yay` e `paru` come costruire e installare il software. Ogni `PKGBUILD` modificato
scaricava silenziosamente il pacchetto npm maligno `atomic-lockfile` (da cui il nome della campagna).

## Il malware: credential stealing + rootkit eBPF

Il payload è un binario scritto in **Rust**, progettato per fare due cose molto brutte:

1. **Rubare credenziali**: password salvate nei browser, token SSH, credenziali AWS/GCP/Azure, chiavi
   API e qualsiasi altra cosa trovasse nella home directory e nelle variabili di ambiente.
2. **Installare un rootkit eBPF**: sui sistemi in cui il malware ottiene i privilegi di root, viene
   dispiegato un rootkit basato su eBPF (Extended Berkeley Packet Filter) — la tecnologia del kernel
   Linux usata normalmente per monitoring e networking. Questo rootkit si nasconde tra i processi
   legittimi ed è progettato per sopravvivere ai riavvii.

I sistemi più a rischio sono stati le workstation degli sviluppatori e gli ambienti CI/CD che usano
runner Arch Linux — dove i pacchetti AUR vengono spesso installati in modo automatico senza che
nessuno legga il PKGBUILD.

## La risposta di Arch Linux

Il team di Arch Linux ha reagito rapidamente: non appena la campagna è stata scoperta l'11-12 giugno,
hanno **disabilitato temporaneamente le registrazioni di nuovi account su AUR** per fermare ulteriori
adozioni maligne. Nelle ore successive hanno lavorato per identificare e ripulire tutti i pacchetti
compromessi, ma la situazione è rimasta caotica per diversi giorni, con nuove ondate di pacchetti
malevoli scoperte anche dopo la prima pulizia.

## Come capire se sei stato colpito

Prima cosa: controlla quando hai installato o aggiornato pacchetti AUR. La **finestra di rischio è
9-12 giugno 2026**. Se hai usato `yay`, `paru` o altri AUR helper in quel periodo, potresti essere
a rischio.

Esiste uno strumento apposito creato dalla community:

```bash
# Clona il tool di verifica della community
git clone https://github.com/lenucksi/aur-malware-check
cd aur-malware-check
bash check.sh
```

Controlla anche la presenza del pacchetto npm incriminato:

```bash
# Cerca atomic-lockfile nel sistema
find / -name "atomic-lockfile" 2>/dev/null
npm list -g atomic-lockfile 2>/dev/null
```

Se usi un sistema Arch-based, verifica i log di sistema per attività sospette nel periodo critico:

```bash
# Controlla connessioni di rete sospette nei log
journalctl --since "2026-06-09" --until "2026-06-13" | grep -E "curl|wget|nc " | head -50
```

## Cosa fare ora

- **Aggiorna tutto** con `yay -Syu` per assicurarti di avere le versioni pulite dei pacchetti
- **Cambia le credenziali** se hai installato o aggiornato pacchetti AUR tra il 9 e il 12 giugno:
  password browser, token SSH, chiavi API
- **Ruota i token cloud**: AWS, GCP, Azure — considera di rigenerarli tutti per sicurezza
- **Se hai un rootkit eBPF**, la soluzione più sicura è reinstallare il sistema da zero
- **Valuta di usare `aurutils`** invece di `yay`/`paru` — ti permette di ispezionare i PKGBUILD
  prima di eseguirli, build per build

## Il problema strutturale dell'AUR

Questo attacco riaccende il dibattito sulla sicurezza strutturale dell'AUR. Il modello
"fidati della community" funziona bene la maggior parte del tempo, ma i pacchetti orfani
rappresentano un vettore di attacco quasi perfetto: sono già presenti nell'indice AUR, spesso con
anni di recensioni positive, e qualsiasi utente registrato può adottarli.

La lezione da portare a casa? **Tratta sempre i pacchetti AUR come codice di terze parti non
verificato**. Leggi i PKGBUILD prima di installare, specialmente per pacchetti che non aggiorni da
tempo. La community ce l'ha messa tutta per sistemare questo casino, ma la responsabilità finale
è sempre dell'utente.
