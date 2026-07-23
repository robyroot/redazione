---
title: "Patch Tuesday luglio 2026: Microsoft chiude 570 falle inclusi 3 zero-day e un bug wormable"
rilevanza: "ALTA"
fonte: "https://www.bleepingcomputer.com/news/microsoft/microsoft-july-2026-patch-tuesday-fixes-massive-570-flaws-3-zero-days/"
data_notizia: "2026-07-15"
tags: ["windows", "patch-tuesday", "zero-day", "sicurezza", "microsoft", "vulnerabilita", "wormable"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Anche per chi usa Linux, questo Patch Tuesday è rilevante per chi gestisce sistemi misti o server Windows. Focus sui bug più critici con consigli pratici su prioritizzazione.
---

# Patch Tuesday luglio 2026: Microsoft chiude 570 falle inclusi 3 zero-day e un bug wormable

Luglio 2026 segna un record poco invidiabile per Microsoft: il **Patch Tuesday di questa settimana** ha corretto la cifra record di **570 vulnerabilità** (alcune fonti riportano 622 CVE contando tutti i componenti), tra cui 3 zero-day e un bug classificabile come "wormable" — cioè capace di auto-propagarsi da un sistema all'altro senza intervento umano.

Anche se usi Linux come sistema principale, se amministri server Windows o hai macchine Windows nella rete di casa o di lavoro, questo aggiornamento non puoi ignorarlo.

## Il numero record: perché così tante falle?

Secondo Microsoft stessa, l'aumento esponenziale del numero di vulnerabilità corrette è in parte attribuibile all'introduzione di strumenti di **vulnerability discovery alimentati dall'AI**, che hanno permesso di trovare difetti nel codebase di Windows a una velocità mai vista prima. Un'arma a doppio taglio: meglio scoprirle prima degli attaccanti, ma dover gestire centinaia di patch al mese è una sfida reale per i team IT.

Su 570 falle, 59 sono classificate "Critical", con 48 di queste che consentono l'esecuzione remota di codice.

## I bug più pericolosi

Ecco le vulnerabilità che meritano attenzione immediata:

### CVE-2026-56188 — Windows Server Network Driver (wormable, CRITICA)

Questo è il bug che tiene svegli i sysadmin di notte. È una **race condition nel driver di rete di Windows Server** che permette a un attaccante remoto di eseguire codice privilegiato *senza alcuna interazione da parte dell'utente*. Non è necessario fare clic su nulla, aprire allegati o visitare siti malevoli.

La caratteristica più allarmante: il bug è **wormable**. Un malware che sfruttasse questa vulnerabilità potrebbe diffondersi autonomamente da un server all'altro attraverso la rete, esattamente come WannaCry nel 2017. Tutti i Windows Server esposti in rete sono a rischio fino al patching.

### CVE-2026-56155 — Active Directory Federation Services (ADFS), zero-day attivamente sfruttato

Questo zero-day è già in uso da parte di attaccanti reali. Un utente con privilegi bassi può sfruttarlo per **ottenere privilegi di amministratore** in ambienti che usano ADFS per l'autenticazione federata. Chiunque usi ADFS in azienda — e sono in tanti — deve dare priorità assoluta a questo aggiornamento.

### CVE-2026-50661 — BitLocker Security Feature Bypass

Questo zero-day richiede accesso fisico al dispositivo, ma permette di bypassare la crittografia BitLocker senza la password. Particolarmente rilevante per laptop aziendali e dispositivi portatili: anche senza credenziali, un attaccante con accesso fisico potrebbe accedere ai dati cifrati.

### Buffer overflow nel server DHCP

Due ulteriori vulnerabilità critiche — **CVE-2026-50370** e **CVE-2026-50518** — sono heap-based buffer overflow nel servizio Windows DHCP Server. Un attaccante nella stessa rete potrebbe sfruttarle per eseguire codice arbitrario sul server DHCP, con impatti devastanti su tutta l'infrastruttura di rete.

## Cosa fare adesso

Se gestisci sistemi Windows, l'azione è semplice ma urgente. Via PowerShell (con privilegi amministrativi):

```powershell
# Verifica aggiornamenti disponibili
Get-WindowsUpdate

# Installa tutto e riavvia automaticamente se necessario
Install-WindowsUpdate -AcceptAll -AutoReboot
```

In alternativa, usa Windows Update dalle Impostazioni di sistema. Per ambienti enterprise con WSUS o Microsoft Endpoint Configuration Manager, approva e distribuisci gli aggiornamenti con priorità alta, partendo dai server esposti a Internet e da quelli che ospitano ADFS.

**Priorità consigliata di patching:**
1. Windows Server con CVE-2026-56188 (wormable, rischio rete)
2. Server ADFS con CVE-2026-56155 (zero-day attivo)
3. Server DHCP con CVE-2026-50370/50518
4. Laptop/dispositivi portatili con CVE-2026-50661 (BitLocker bypass)

**Per chi gestisce reti miste con sistemi Linux:** verifica che il firewall limiti l'accesso ai servizi Windows Server solo alle reti interne necessarie. Ridurre la superficie di attacco esposta è sempre la prima difesa, specialmente di fronte a bug wormable.

## Una riflessione

570 vulnerabilità in un mese fanno pensare. L'AI sta accelerando la scoperta di bug — il che è una buona notizia a lungo termine per la sicurezza — ma crea anche una pressione enorme sui team IT che devono testare e distribuire centinaia di patch ogni mese. Per gli utenti finali, il messaggio rimane invariato: **aggiorna subito, senza aspettare**.

I bug wormable come CVE-2026-56188 non lasciano tempo: la storia di WannaCry ha insegnato che anche solo poche ore di esposizione possono essere catastrofiche su reti non protette.
