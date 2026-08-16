---
title: "Il kernel Linux dice basta alle patch scritte dall'AI (quasi ovunque)"
rilevanza: "MEDIA"
fonte: "https://itsfoss.com/news/linux-drivers-staging-ai-rejection/"
data_notizia: "2026-08-16"
tags: ["linux", "ai", "opensource", "kernel"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: raccontarlo come un caso studio di "governance
  dell'AI" in un progetto open source enorme, utile anche a chi gestisce
  community o repository più piccoli. Evidenziare il contrasto tra
  Kroah-Hartman (restrittivo su staging) e Torvalds (permissivo altrove) come
  esempio di come anche dentro lo stesso progetto ci possano essere policy
  diverse per contesti diversi. Buon collegamento con l'articolo sul
  rilascio di Linux 7.2 pubblicato oggi, dove Torvalds parla di AI come
  "nuova normalità".
---

Mentre Linus Torvalds accoglie di buon grado l'ondata di patch generate con l'aiuto dell'intelligenza artificiale che sta investendo lo sviluppo del kernel Linux (ne abbiamo parlato a proposito del rilascio di Linux 7.2 di oggi), Greg Kroah-Hartman — manutentore storico di una delle aree più delicate e allo stesso tempo più "per principianti" del kernel — ha deciso di tirare un freno a mano. Da ora la sezione `drivers/staging/` rifiuterà sistematicamente le patch generate da LLM, con una sola, strettissima eccezione.

## Cos'è la staging area e perché è speciale

Per chi non mastica quotidianamente lo sviluppo del kernel, `drivers/staging/` è una specie di area di quarantena: qui finiscono i driver hardware ancora acerbi, quelli che non rispettano tutti gli standard di qualità del kernel "vero" ma che vengono comunque inclusi per permettere di testarli su hardware reale e farli maturare nel tempo. Ma la staging area ha sempre avuto anche un secondo scopo, forse ancora più importante: è il posto dove i nuovi sviluppatori muovono i primi passi, alle prese con piccoli refactoring, pulizie di stile del codice e correzioni di warning — il classico "low hanging fruit" che permette di imparare il processo di invio delle patch senza rischiare di far esplodere un sottosistema critico. Ed è proprio questo secondo aspetto il cuore del problema.

## Il problema: un "onslaught" di patch automatiche

Kroah-Hartman ha raccontato di essersi trovato sommerso — la sua parola è stata proprio "onslaught", un'ondata travolgente — di patch generate da strumenti AI che si limitavano a ripulire codice o sistemare dettagli stilistici. Il punto, per lui, non è tanto la qualità (comunque non sempre impeccabile), quanto il fatto che automatizzare questo lavoro con un LLM vanifica lo scopo della staging area: se un modello linguistico può ripulire il codice al posto tuo, che senso ha usare quello spazio come palestra?

Nel suo messaggio alla community, Kroah-Hartman è stato diretto, avvisando chi pensasse di aggirare la regola nascondendo l'uso di strumenti AI: "And yes, it is VERY obvious when people submit LLM-generated patches, so don't think that just not disclosing the use of them will allow you to 'get away' with anything" — è molto evidente quando qualcuno invia patch generate da un LLM, quindi non pensate di farla franca non dichiarandolo.

## L'unica eccezione: i bug di sicurezza veri

La policy non è un divieto assoluto. Chi ritiene che un LLM abbia individuato un vero problema di sicurezza in un driver della staging area può ancora inviare la patch corrispondente — ma solo a patto di aver testato personalmente la correzione sull'hardware reale collegato a quel driver, e di essere in grado di descrivere in dettaglio come è stato condotto il test. In altre parole: l'AI può aiutarti a trovare il problema, ma la responsabilità di verificarlo resta umana, concreta e verificabile.

## Due filosofie, un solo progetto

La cosa che rende questa vicenda particolarmente interessante non è tanto la regola in sé, quanto il contrasto che rivela all'interno dello stesso progetto. Torvalds, commentando l'ondata di piccole patch (molte delle quali probabilmente assistite da AI) che ha caratterizzato il ciclo di sviluppo di Linux 7.2, ha preso una posizione decisamente più permissiva, arrivando a dire che Linux "non è uno di quei progetti anti-AI" e invitando chi non fosse d'accordo a fare un fork o a farsi da parte.

Come si conciliano le due posizioni? La restrizione di Kroah-Hartman è specifica per lo scopo didattico della staging area, non un giudizio generale sull'AI nel resto del kernel. Altrove — reti, gestione della memoria, filesystem — il lavoro assistito da intelligenza artificiale resta pienamente ammesso, e a giudicare dai numeri della release 7.2 è già ampiamente diffuso.

## Perché dovrebbe interessarti anche se non scrivi codice per il kernel

Questa vicenda è un piccolo caso di studio utile ben oltre il mondo kernel: mostra come anche i progetti open source più grandi del pianeta stiano ancora cercando l'equilibrio giusto fra i benefici concreti dell'AI (più velocità, meno lavoro ripetitivo) e la necessità di preservare spazi di apprendimento umano e responsabilità. Se gestite una community o contribuite a progetti open source, la lezione vale comunque: automatizzare tutto non è sempre un progresso, soprattutto quando lo spazio esiste apposta per far crescere le persone, non solo il codice.
