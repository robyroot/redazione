---
title: "Fedora 45 Beta è qui: GNOME 51, KDE Plasma 6.7 e kernel Linux 7.2"
rilevanza: "MEDIA"
fonte: "https://linuxiac.com/arch-linux-september-2026-iso-is-out-with-linux-kernel-7-2/"
data_notizia: "2026-09-17"
tags: ["fedora", "linux", "gnome", "kde", "desktop", "distro"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: ottima occasione per parlare delle novità del desktop Linux a chi vuole tenersi aggiornato senza installarle subito. Enfatizzare che la beta serve per testare e contribuire, non per la produzione. Menzionare anche Arch come alternativa rolling che ha già il kernel 7.2.
---

# Fedora 45 Beta è qui: GNOME 51, KDE Plasma 6.7 e kernel Linux 7.2

Se stai aspettando la prossima versione stabile di Fedora per aggiornare il tuo desktop Linux, hai un'anteprima su cui mettere le mani. **Fedora 45 Beta è disponibile** e porta con sé un pacchetto di novità molto interessante: GNOME 51, KDE Plasma 6.7 e il kernel Linux 7.2. Non male per un rilascio ancora in fase beta.

## Cosa c'è in Fedora 45 Beta

La beta di Fedora 45 è pensata per chi vuole testare le novità prima della release stabile e — se ha voglia — contribuire a segnalare bug. Non è una versione per la produzione, ma se hai una macchina di test o ti senti avventuroso, vale la pena darci un'occhiata.

Le novità principali:

### GNOME 51 nel Fedora Workstation

Il Fedora Workstation (la variante con GNOME) arriva con **GNOME 51**, la versione che sarà rilasciata ufficialmente a breve. GNOME 51 porta con sé miglioramenti all'interfaccia di GNOME Software, ottimizzazioni nelle animazioni e aggiornamenti ai componenti di base.

Il team GNOME ha lavorato molto sulla coerenza visiva e sulla stabilità — meno "effetto wow" rispetto a release precedenti, ma più robustezza nel quotidiano. Esattamente quello che vuoi da un desktop che usi ogni giorno.

### KDE Plasma 6.7 nel Fedora KDE Spin

Per chi preferisce KDE, la variante Fedora KDE Plasma Desktop Edition arriva con **KDE Plasma 6.7**. Le versioni 6.x di Plasma hanno progressivamente portato a una pulizia architetturale profonda, e la 6.7 continua questo lavoro con miglioramenti al sistema di gestione finestre e all'integrazione Wayland.

Se usi uno schermo HiDPI o hai più monitor, Wayland su KDE 6.x è diventato molto più affidabile rispetto alle versioni 5.x.

### Kernel Linux 7.2 e toolchain aggiornate

Il cuore del sistema è **Linux kernel 7.2**, con tutti i miglioramenti che porta: migliore supporto hardware recente, ottimizzazioni nello scheduler e fix di sicurezza. Per chi vuole sapere cosa c'è nella 7.2 rispetto alla 7.1, i changelog completi sono su kernel.org.

Fedora 45 porta anche toolchain aggiornate: GCC, LLVM, Python e Rust nelle versioni più recenti. Per chi sviluppa software, questo significa poter usare le ultime funzionalità dei linguaggi senza configurazione aggiuntiva.

## Come provare la Beta

Se vuoi metterci le mani:

```bash
# Se hai già Fedora 44 installato, puoi fare upgrade alla beta
sudo dnf upgrade --refresh
sudo dnf install dnf-plugin-system-upgrade
sudo dnf system-upgrade download --releasever=45

# Controlla che non ci siano problemi prima di procedere
sudo dnf system-upgrade reboot
```

Oppure scarica l'ISO beta direttamente da [getfedora.org](https://getfedora.org) e provala in una VM:

```bash
# Con QEMU/KVM, rapido per testare
virt-install \
  --name fedora45-beta \
  --ram 4096 \
  --vcpus 2 \
  --disk size=20 \
  --cdrom /path/to/Fedora-45-beta.iso \
  --os-variant fedora39
```

## Nel frattempo, Arch Linux ha già il kernel 7.2

Se usi una distro rolling release, non devi aspettare Fedora 45: **Arch Linux ha già aggiornato la sua ISO di settembre 2026** al kernel 7.2.2. La ISO 2026.09.01 è il salto dalla 7.1.5 del mese scorso alla 7.2.2 attuale.

È uno dei vantaggi delle rolling release: ottieni le novità del kernel in tempo reale, senza dover aspettare un ciclo di rilascio semestrale.

## Le novità di Raspberry Pi OS e le altre distro

Settembre 2026 è stato ricco di aggiornamenti anche su altri fronti:

- **Raspberry Pi OS** ha ricevuto un nuovo dock, controlli desktop riprogettati, un nuovo strumento screenshot e il kernel 6.18.50 LTS
- **KaOS 2026.09** porta Dinit come init system, il window manager Niri e Limine come bootloader di default
- **Grml 2026.09** aggiorna il suo set di strumenti di recovery/sysadmin con kernel 7.1 e pacchetti da Debian Testing/Forky

Il panorama delle distro è insomma molto attivo. Buon momento per fare un giro e vedere se qualcosa si adatta meglio al tuo workflow attuale.

---

**Fonti:**
- [Arch Linux September 2026 ISO - Linuxiac](https://linuxiac.com/arch-linux-september-2026-iso-is-out-with-linux-kernel-7-2/)
- [Tux Machines: Fedora, Flatpak, and GNOME](https://news.tuxmachines.org/n/2026/09/17/Fedora_Flatpack_and_GNOME.shtml)
- [Tux Machines: Akademy, KDE, and GNOME](https://news.tuxmachines.org/n/2026/09/22/Akademy_KDE_and_GNOME.shtml)
