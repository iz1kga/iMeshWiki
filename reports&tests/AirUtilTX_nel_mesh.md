---
title: AirUtilTx nel mesh Meshtastic Italia
description: misura di AirUtilTX nel mesh e valutazioni a riguardo
published: true
date: 2023-03-08T13:21:30.868Z
tags: 
editor: markdown
dateCreated: 2023-03-08T10:53:04.155Z
---

# Valutazione misura AirUtilTX
by Vincenzo Lorenzale addì 8 Marzo 2023

---

### I dati raccolti questa mattina
![merge_from_ofoct.jpg](/merge_from_ofoct.jpg)
### Analisi e commenti
Questa mattina sono stati raccolti dati i dati di Telemetry intercorsi nel mesh fra le ore 7:13 e le 10:08 con lo scopo di valutare l'occupazione AirUtilTX presso i 10 router oggi attivi nel mesh per capire se questa potesse avere peso nella capacità di consegna dei messaggi fra i nodi. 

Per una corretta valutazione dello stato di saturazione della rete sarebbe utile poter conoscere in tempo reale lo stato del valore di AerUtilTX presente al momento presso i router attivi nel mesh. Secondo la lettura delle specifiche meshtastic, sembrerebbe che ogni nodo invii alla rete un messaggio di Telemetry ogni minuto qundi, se così fosse, sarebbe piuttosto agevole avere la costante misura di AerUtilTX presso un router di controllo centrale.

Forte di questa assunzione, mi sono dedicato per qualche giorno alle verifiche conseguenti per arrivare alle conclusioni di oggi che qui riassumo:
1. l'assunzione è erronea perché mentre è vero che qualunque nodo connesso a una porta seriale attiva in ricezione e trasmissione effettivamente emette un messaggio di Telemetry ogni minuto, ciò non avviene per i nodi non connessi a porte seriali. In questo caso la tramissione, analizzando i dati raccolti in questi giorni, avviene ogni 15 minuti





