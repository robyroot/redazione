---
title: "Attacco supply chain su npm: dietro il dirottamento di debug e chalk c'era la Corea del Nord"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/amazon-links-debug-and-chalk-npm-hijack.html"
data_notizia: "2026-07-30"
tags: ["npm", "supply chain", "cybersecurity", "open source", "Corea del Nord"]
livello: "intermediate"
nota_editoriale: |
  Ottimo angolo per RobyRoot: spiegare in modo pratico come un singolo maintainer phishato possa mettere a rischio il 10% del cloud mondiale in due ore. Utile aggiungere box con consigli concreti (npm audit, lockfile, Socket.dev, Renovate con revisione manuale) per chi gestisce progetti Node.js personali o professionali. Possibile collegamento con articoli precedenti su supply chain attack.
---

Se gestisci anche solo un progetto Node.js con un `package.json` pieno di dipendenze, questa notizia dovrebbe farti drizzare le antenne. Amazon Threat Intelligence ha pubblicato una ricerca che collega ufficialmente uno degli attacchi supply chain più estesi della storia di npm — il dirottamento dei pacchetti **debug** e **chalk** nel settembre 2025 — a un gruppo di hacker nordcoreano già noto: **Sapphire Sleet**, conosciuto anche come BlueNoroff o Stardust Chollima.

Per chi non li conoscesse, `debug` e `chalk` sono due delle librerie JavaScript più usate al mondo: piccoli pacchetti di utilità che finiscono, direttamente o indirettamente, nelle dipendenze di praticamente ogni progetto Node.js moderno. Parliamo di oltre **2 miliardi di download settimanali combinati** solo considerando i pacchetti coinvolti (almeno 18 in totale). Numeri che danno il senso della scala del problema.

## Come è successo

La tecnica alla base non è particolarmente sofisticata, ed è proprio questo il punto inquietante: un maintainer legittimo è stato preso di mira con un attacco di **phishing mirato**, attirato su un dominio civetta che imitava npmjs.com. Una volta ottenute le credenziali, gli attaccanti hanno pubblicato versioni compromesse dei pacchetti, iniettando uno script "wallet-draining" pensato per intercettare e dirottare transazioni di criptovalute direttamente nel browser o nell'ambiente di esecuzione delle vittime.

Il risultato? Secondo Amazon, l'infezione ha raggiunto circa il **10% degli ambienti cloud monitorati nel giro di due ore** dalla pubblicazione dei pacchetti malevoli. Una velocità di propagazione che la dice lunga su quanto siano profonde e poco visibili le catene di dipendenze nell'ecosistema JavaScript.

## Non è un episodio isolato

La parte forse più interessante della ricerca di Amazon non è l'attacco in sé — di cui si era già parlato mesi fa — ma la scoperta che si tratta di **un solo pezzo di una campagna molto più lunga e coordinata**. Gli analisti hanno collegato quattro incidenti precedentemente considerati slegati:

- marzo 2025: compromissione del pacchetto minore `typo-crypto`, che sembra essere servito come "banco di prova" per testare le tecniche;
- settembre 2025: l'attacco a `debug` e `chalk`, la fase di massima diffusione;
- fasi successive che hanno coinvolto anche il popolare pacchetto `axios`.

In pratica, Sapphire Sleet ha affinato gradualmente le proprie tecniche di ingegneria sociale contro i maintainer open source, passando da bersagli minori a librerie sempre più centrali nell'ecosistema, in un'operazione che si estende per oltre un anno.

## Perché ti riguarda, anche se non "gestisci server"

Non serve essere una grande azienda per essere colpiti: basta avere `npm install` in un README, un progetto hobby, un tool interno o anche solo un ambiente CI/CD che tira giù dipendenze in automatico. La minaccia non arriva "dall'esterno" nel senso classico — arriva **dalla tua stessa catena di fornitura software**, spesso composta da centinaia di pacchetti transitivi che nessuno controlla mai a mano.

Qualche accorgimento pratico, utile a chiunque smanetti con Node.js:

- **Blocca le versioni** con lockfile (`package-lock.json`, `pnpm-lock.yaml`) e non aggiornare "alla cieca" con `npm update` senza controllare i changelog.
- Valuta strumenti come **Socket.dev** o **npm audit** che analizzano i pacchetti per comportamenti sospetti prima che finiscano nel tuo progetto.
- Se usi bot di aggiornamento automatico (Renovate, Dependabot), configura una **revisione manuale obbligatoria** per le nuove major/minor version dei pacchetti critici, invece del merge automatico.
- Diffida di richieste di "verifica account" o reset password che arrivano via email per il tuo account npm: è esattamente così che è iniziato tutto.

La morale, purtroppo non nuova ma sempre più urgente, è che gli attacchi supply chain sono diventati lo strumento preferito di gruppi statali per colpire in modo indiscriminato e su vasta scala. E finché la sicurezza dei maintainer open source dipenderà da account personali protetti (nella migliore delle ipotesi) da una 2FA, episodi come questo continueranno a ripetersi.
