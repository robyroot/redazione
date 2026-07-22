---
title: "VEGA: il tool AI che sta scovando i bug del kernel Linux nascosti da decenni"
rilevanza: "MEDIA"
fonte: "https://nebusec.ai/vega/"
data_notizia: "2026-07-22"
tags: ["intelligenza artificiale", "cybersecurity", "linux", "vulnerabilità", "open source"]
livello: "beginner"
nota_editoriale: |
  Da collegare esplicitamente all'articolo su GhostLock (stesso giorno): qui l'angolo è
  più riflessivo/da editoriale — implicazioni della concentrazione di potere nella ricerca
  di vulnerabilità AI-driven, dato che VEGA non è open source nonostante scovi bug in
  software open source. Buono spunto per un commento personale dell'autore.
---

Dietro alla scoperta di GhostLock (di cui parliamo in un altro articolo di oggi) c'è un protagonista che merita un pezzo tutto suo: non un singolo ricercatore geniale chino sul codice per settimane, ma un'intelligenza artificiale. Si chiama VEGA, è sviluppata dall'azienda Nebula Security, e il suo bilancio di caccia al bug è da far girare la testa: 934 vulnerabilità validate, di cui 897 bug nel kernel Linux, 8 zero-day in Chrome e 98 CVE pubblici assegnati. Ha messo le mani su software che usiamo (quasi) tutti ogni giorno: Linux, Chrome, Firefox, nginx, curl, prodotti Microsoft.

Come funziona, in sintesi? VEGA è pensata per leggere codice sorgente su larga scala — repository di qualsiasi dimensione — e cercare pattern che indicano bug sfruttabili, non solo teorici. La piattaforma combina analisi statica del codice con verifica dinamica, cioè prova davvero a far scattare il bug invece di segnalarlo "a sentimento", genera automaticamente patch di correzione e si integra nel flusso di revisione delle pull request, così un team può vedere il problema e la soluzione proposta nello stesso posto. Per i clienti enterprise offre anche analisi della supply chain, tema caldissimo da quando gli attacchi alle dipendenze software sono diventati la norma piuttosto che l'eccezione.

Il caso GhostLock è l'esempio perfetto di cosa cambia con questo approccio. Il bug era nel codice del kernel Linux dal 2011: quindici anni durante i quali migliaia di sviluppatori e ricercatori di sicurezza hanno letto, modificato o comunque attraversato quella porzione di codice senza accorgersene di nulla. VEGA l'ha trovato, Nebula l'ha validato e segnalato responsabilmente, e Google ha pagato oltre 92.000 dollari di ricompensa tramite il programma kernelCTF. Non è un caso isolato: GhostLock si affianca ad altre scoperte recenti con lo stesso pattern, come Bad Epoll (CVE-2026-46242) e Copy Fail (CVE-2026-31431), a conferma di una tendenza del 2026 — gli strumenti AI-driven stanno diventando bravissimi a scovare bug di classe "use-after-free" e "memory corruption" che gli esseri umani, per quanto esperti, faticano a individuare a occhio perché richiedono di tenere a mente contemporaneamente molte condizioni che raramente si verificano tutte insieme.

Vale la pena essere chiari su un punto, perché non è scontato: VEGA non è open source. È un prodotto commerciale con un modello ad abbonamento — piano "Researcher" pay-as-you-go per chi lavora da solo, piano "Enterprise" per la copertura di più repository in azienda. Non è quindi uno strumento che puoi scaricare e far girare gratis sul tuo progetto, a differenza di tanti tool di security scanning nati nella community open source. E qui si apre una domanda interessante per il futuro: se la capacità di trovare bug critici in software fondamentale come il kernel Linux finisce per concentrarsi nelle mani di poche aziende con accesso a modelli AI potenti, chi decide quali vulnerabilità vengono segnalate prima ai vendor e quali, magari, restano sul tavolo più a lungo o finiscono vendute a chi le vuole sfruttare invece che patchare? Nebula sembra muoversi secondo pratiche corrette di responsible disclosure — GhostLock è stato segnalato e corretto mesi prima della pubblicazione — ma è un tema che vale la pena tenere d'occhio, soprattutto quando il software analizzato è quello su cui gira mezzo internet.

Per chi segue il mondo Linux e open source, comunque, la notizia di fondo resta positiva: l'AI applicata alla ricerca di vulnerabilità sta ripulendo codice che gira su miliardi di dispositivi da bug che aspettavano solo di essere trovati, nel bene e nel male, da qualcuno. Ed è decisamente meglio che a trovarli per primo sia un ricercatore con un tool AI e un programma di bug bounty, piuttosto che un attaccante con lo stesso identico strumento e nessuna intenzione di segnalare nulla a nessuno.
