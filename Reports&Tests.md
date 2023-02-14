---
title: Test di Web Gui
description: Web Gui accessibile at https://client.meshtastic.org
published: true
date: 2023-02-14T22:18:50.250Z
tags: 
editor: markdown
dateCreated: 2023-02-14T18:52:28.175Z
---

# Test Web Gui (Vincenzo Lorenzale 6 Feb. 2023 )

 Dopo un anno di sosta ho ripreso i 4 device che avevo a versione 1.2.50 per aggiornarli a livello 2.0.x visto che questo livello segnava anche un bel salto di qualità.
 
Le cose nuove più interessanti sono l’interfaccia web innovativa, la connessione da App a device via IP in rete, la funzione di Gateway via rete con appoggio a server IOT. L’aggiornamento e la messa in rete del mio Gateway e l’aggiornamento dei miei 3 client non hanno avuto grosse difficoltà grazie anche al supporto del gruppo Telegram Meshtastic Italia di cui faccio parte dal Dicembre 2020. 

Per l’interfaccia web gui invece la lotta è stata più dura e ancora non può dirsi completamente conclusa. Tralascio di riportare alcune instabilità dell’insieme Andriod App / Router_Client e vengo subito allo stato dell’arte dell’interfaccia Web GUI accessibile via https://client.meshtastic.org

Per questa interfaccia è indispensabile usare il web browser Microsoft Edge oppure Google Chrome che sono gli unici al momento in grado di supportare il collegamento in seriale USB verso il device Tlora o Tbeam Meshtastic. 

Il device Meshtastic deve essere configurato con supporto server http collegato in rete attraverso il router internet domestico. Abbiamo due tipi di connessione verso il device Meshtastic che sono:
1. via indirizzo IP del device in rete locale
2. via porta serial USB che contemporaneamente alimenta il device

La connessione verso l’indirizzo IP del device va fatta in https e di fatto risulta un po’ macchinosa per via del fatto che il server http configurato nel device non ha un certificato di crittografia valido e richiede che il browser sia forzato nella sua accettazione per riuscire ad operare con questa interfaccia. Spesso questa procedura si interrompe con errori strani e il tutto diventa quindi macchinoso e disincentivante.

A fronte di queste difficoltà ho deciso di provare la connessione seriale constatando che questa è molto stabile, più rapida e funziona bene. Tutti i test successivi sono stati fatti utilizzando la connessione USB.

## Ambiente di test
E’ consistito in:
1. una Tlora2-1.1.6 con firmware 2.0.18
2. una Tbeam con firmware 2.0.10
3. Uno smartphone Honor Lite 9.0 con Meshtastic App 2.0.14

## Configurazione device
Via interfaccia web sarebbe possibile configurare completamente il device collegato. Ho notato che dopo settato i parametri che ci interessa modificare, premendo Apply/Reboot effettivamente il device si reinizializza ma di fatto non per tutti i parametri le modifiche vanno a buon fine. Poco male perché l’interfaccia CLI python funziona egregiamente a riguardo.

## Visualizzazione dei nodi nel Mesh
I riferimenti dei nodi compaiono via via che giungono i messaggi di NODE_INFO e di POSITION dal mesh via radio o via rete cui il Gateway è connesso. Allo stato c’è il problema che i nomi dei nodi non sono quelli reali ma sono tutti Meshtastic_xxxx dove le x sono i primi 4 digit del NodeID. I nomi reali sono invece riportati se ci si connette al device via App. A questo proposito ho aperto una ‘issue’ su github Meshtastic/web.

## Visualizzazione della geoMap dei nodi
Funziona bene circa la collocazione geografica delle icone che rappresentano i nodi, non vengono invece riportati i nomi e le coordinate geografiche cliccando sulle relative immagini in mappa. Anche questo problema l’ho riportato su github Meshtastic/web.

## Ricezione e invio dei messaggi
La ricezione avviene regolarmente con un cerchietto biffato accanto al messaggio ricevuto sotto icona e long name del mittente, la trasmissione è risultata invece problematica e di
seguito fornisco i dettagli. Va subito detto, intanto, che è previsto invio di messaggi solo sul canale primario ovvero a tutto il Mesh. Non è previsto invio personalizzato.

## Problemi di invio
Con la Tbeam client in linea provo invio messaggio da web GUI e noto che a volte immediatamente, a volte dopo una decina di secondi, il cerchietto alla sinistra del messaggio sullo schermo va a contenere un ! al posto del biff che mi aspettavo. Il messaggio sulla Tbeam client di fatto non compare / arriva.

Provato varie volte sempre senza successo. Provo allora da App collegata via IP alla Tlora Router_Client andando sul riferimento di canale 0 LongFast per indirizzare tutto il mesh e vedo che la nuvoletta a volte viene barrata, a volte biffata ma in ogni caso il messaggio arriva in un tempo da 10 a 40 secondi sulla Tbeam e anche su tutti i nodi attivi al momento.

Ritengo allora che l’interfaccia web abbia un problema e apro una ‘issue’ su github Meshtastic/web. Oggi mi accorgo che la mia deduzione era errata ovvero la web GUI effettivamente manda il messaggio e il ! che è segno di fallimento si comporta come la barra sulla nuvoletta nella App Android ovvero non è ritornato ack ma il messaggio potrebbe anche essere arrivato a segno. 

Un grazie a Bosc, JSNM e xlw che oggi mi hanno dato conferma che i messaggi da web GUI effettivamente funzionano, occorre però porre attenzione a:

1. l fatto che il ! nel cerchietto appaia non immediatamente ma dopo un certo tempo compreso fra sei / 50 secondi. Nel tempo di attesa vedremo invece tre puntini.
2. Se il ! appare immediatamente il messaggio è sicuramente fallito e la causa non sta nell’interfaccia web bensì nel device Router_Client che in qualche modo vede compromessa la connessione uplink oppure AirUtilTx del nostro client_router ha superato il 10%.
3. In ogni caso però il messaggio via radio diretto alla Tbeam client NON arriva e questo è stato l’elemento principale che mi aveva erroneamente indotto a pensare che l’invio messaggi via web GUI non funzionasse del tutto.

Anche l’invio messaggi da App collegata o in BT al client Tbeam o alla Tlora Router_Client via IP (il mio BT sulla Tlora è down ma in ogni caso non funzionerebbe essendo attiva la connessione wifi al router internet locale) può essere in qualche modo problematico: anche qui se la barra arriva sulla nuvoletta immediatamente il messaggio è sicuramente fallito perché l’upload channel non funziona nel Router_Client causa AirUtilTx in eccesso. Se invece la barra o il biff arrivano dopo 8-50 secondi il messaggio è andato verosimilmente a buon fine.

## Conclusione
L’elemento fondamentale che mi aveva fatto pensare al fallimento dell’invio messaggi via web GUI è stato quello di non vedere il messaggio sul client Tbeam che avevo come monitor in mesh via radio col Tlora Router_Client.

Ora ripensandoci con più calma posso dedurre che ciò è normale stante la connessione del Tlora come Gateway, ovvero che in trasmissione sfrutta il solo canale http uplink e non anche la radio e quindi il mio client non avrebbe potuto mai ricevere il messaggio. In ricezione radio invece i messaggi vengono ruotati verso il canale uplink http e il resto del mesh viene soddisfatto.

Esistono ancora problemi e questioni da chiarire anche sulla App che a volte vede nei nodi ??? al posto dei nomi che un attimo prima erano presenti o ancora sul Router_Client connesso via USB che a volte fa autoreboot o ncora la stessa App che inopinatamente perde la connessione con IP o anche via BT (verso il client) ma l’insieme che vedo ora è più solido e lascia sperare verso una migliore stabilità del tutto.

Allego schermata del test di oggi
![test_messagi.png](/test_messagi.png)

## Aggiornamento al 12 Feb 2023
In questa data è stata reso disponibile at https://client.meshtastic.org una nuova versione aggiornata di Web Gui che ha risolto il problema dell'invio messaggi oltre ad aver creato un insieme più gradevole e funzionale. Con questa versione aggiornata risultano corrette anche le malfunzioni sui comandi di configurazione del device.

