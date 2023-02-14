---
title: Test di Web Gui
description: Web Gui accessibile at https://client.meshtastic.org
published: true
date: 2023-02-14T21:09:15.579Z
tags: 
editor: markdown
dateCreated: 2023-02-14T18:52:28.175Z
---

## Test Meshtastic web gui (Vincenzo Lorenzale 6 Feb. 2023 )

 Dopo un anno di sosta ho ripreso i 4 device che avevo a versione 1.2.50 per aggiornarli a livello 2.0.x visto che questo livello segnava anche un bel salto di qualità.
 
Le cose nuove più interessanti sono l’interfaccia web innovativa, la connessione da App a device via IP in rete, la funzione di Gateway via rete con appoggio a server IOT. L’aggiornamento e la messa in rete del mio Gateway e l’aggiornamento dei miei 3 client non hanno avuto grosse difficoltà grazie anche al supporto del gruppo Telegram Meshtastic Italia di cui faccio parte dal Dicembre 2020. 

Per l’interfaccia web gui invece la lotta è stata più dura e ancora non può dirsi completamente conclusa. Tralascio di riportare alcune instabilità dell’insieme Andriod App / Router_Client e vengo subito allo stato dell’arte dell’interfaccia Web GUI accessibile via https://client.meshtastic.org
#
### https://client.meshtastic.org
Per questa interfaccia è indispensabile usare il web browser Microsoft Edge oppure Google Chrome che sono gli unici al momento in grado di supportare il collegamento in seriale USB
verso il device Tlora o Tbeam Meshtastic. 

Il device Meshtastic deve essere configurato con supporto server http collegato in rete attraverso il router internet domestico. Abbiamo due tipi di connessione verso il device Meshtastic che sono:
1. via indirizzo IP del device in rete locale
2. via porta serial USB che contemporaneamente alimenta il device

La connessione verso l’indirizzo IP del device va fatta in https e di fatto risulta un po’ macchinosa per via del fatto che il server http configurato nel device non ha un certificato di crittografia valido e richiede che il browser sia forzato nella sua accettazione per riuscire ad operare con questa interfaccia. Spesso questa procedura si interrompe con errori strani e il tutto diventa quindi macchinoso e disincentivante.

A fronte di queste difficoltà ho deciso di provare la connessione seriale constatando che questa è molto stabile, più rapida e funziona bene. Tutti i test successivi sono stati fatti utilizzando la connessione USB.


