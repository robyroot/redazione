---
title: "Linux 6.18.40 e altri cinque LTS: il luglio da record del kernel"
rilevanza: "MEDIA"
fonte: "https://www.linuxcompatible.org/story/linux-kernel-61840-and-five-lts-branches-released-in-massive-july-stable-cycle"
data_notizia: "2026-07-24"
tags: ["linux", "kernel", "LTS", "sicurezza", "aggiornamento", "KVM"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: inquadrare il rilascio come evento notevole (sei LTS in un colpo), spiegare cos'è il branch LTS 6.18 e perché le patch KVM/BPF contano anche per utenti desktop e sviluppatori.
---

# Linux 6.18.40 e altri cinque LTS: il luglio da record del kernel

Il 24 luglio 2026 Greg Kroah-Hartman ha rilasciato **sei versioni LTS del kernel Linux in un unico ciclo stabile**. Non capita spesso: normalmente i release arrivano a cadenza variabile e su branch separati, ma questa volta tutti e sei sono usciti insieme, con un totale di migliaia di patch distribuite tra i vari rami. È uno dei cicli di aggiornamento più corposi della storia recente del progetto kernel.

## Le versioni rilasciate

Il rilascio copre tutti i branch Long Term Support attivi:

- **6.18.40** — il branch LTS più recente, con 1.624 patch
- **6.12.x**
- **6.6.x**
- **6.1.x**
- **5.15.x**
- **5.10.x**

Se usi una distro moderna — Arch, Fedora, Ubuntu, Debian, openSUSE, AlmaLinux — è molto probabile che uno di questi branch sia quello su cui gira il tuo sistema. Arch Linux ha già integrato 6.18.40 nel repository `core-testing`, e le altre distribuzioni seguiranno nei loro canali di aggiornamento abituali.

## Le correzioni più rilevanti

### CVE-2026-46113 — KVM/x86 shadow paging

La patch più critica riguarda il sottosistema **KVM** (Kernel-based Virtual Machine), il componente che permette a Linux di eseguire macchine virtuali con performance vicine all'hardware nativo.

Il bug è nel meccanismo di **shadow paging**, che è la tecnica usata per tradurre gli indirizzi di memoria delle VM in indirizzi fisici reali. Una vulnerabilità qui può avere impatti seri sulla sicurezza degli ambienti virtualizzati: in scenari estremi, un bug di questo tipo potrebbe consentire a codice in esecuzione nella VM di accedere a zone di memoria al di fuori dei confini della VM stessa.

Per i sysadmin che gestiscono server di virtualizzazione (anche home lab con QEMU/KVM), aggiornare è fortemente consigliato:

```bash
# Verifica se stai usando KVM
lsmod | grep kvm
# oppure
ls /dev/kvm && echo "KVM disponibile"
```

### XFS — Correzione corruzione dati

Il filesystem XFS riceve una correzione per un caso di potenziale corruzione dei dati in certi scenari di I/O. XFS è il filesystem predefinito di Fedora e Red Hat, e viene usato anche in molti sistemi di archiviazione. Se usi XFS su partizioni importanti, aggiornare è la mossa giusta.

### BPF/s390 — Regressione nel verifier

Il verifier BPF sull'architettura s390 (i mainframe IBM) aveva una regressione introdotta in un kernel precedente. Non è una cosa che tocca la maggior parte di voi, ma è interessante perché dimostra come il testing del kernel su architetture non-x86 sia preso sul serio dal progetto.

## Come aggiornare

Su **Arch Linux** (e derivate Manjaro, EndeavourOS, ecc.):

```bash
sudo pacman -Syu
# Poi riavvia per caricare il nuovo kernel
sudo reboot
```

Su **Debian/Ubuntu** e derivate:

```bash
sudo apt update && sudo apt upgrade
sudo reboot
```

Su **Fedora**:

```bash
sudo dnf upgrade
sudo reboot
```

Dopo il riavvio, verifica la versione caricata:

```bash
uname -r
# Output atteso: qualcosa tipo 6.18.40-arch1-1 o 6.18.40-1.fc41
```

## Cos'è il kernel 6.18 e perché è importante

Il branch 6.18 è stato dichiarato **Long Term Support** a fine 2025, il che significa che riceverà aggiornamenti di sicurezza per almeno 2-4 anni. È la scelta naturale per chi vuole un kernel stabile e longevo — server, embedded, sistemi dove la continuità conta più dell'ultima feature sperimentale.

Con 1.624 patch solo nell'ultimo aggiornamento, il ritmo di sviluppo è intenso. Centinaia di sviluppatori da aziende come Google, Intel, Red Hat, SUSE e Meta continuano a contribuire ogni settimana: la sicurezza e la stabilità del kernel Linux sono ormai un interesse industriale globale.

## Dove seguire gli sviluppi

- **kernel.org** — tutti i tarball e i release notes ufficiali
- **lkml.org** — la mailing list Linux Kernel, dove avvengono le discussioni tecniche vere
- **kernelnewbies.org** — riepiloghi delle novità per ogni release, in linguaggio più accessibile

Se vuoi restare aggiornato senza seguire la mailing list (che ha volumi altissimi), il feed RSS di Phoronix copre bene le notizie kernel con un buon livello di dettaglio tecnico.
