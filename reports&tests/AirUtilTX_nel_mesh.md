---
title: AirUtilTx nel mesh Meshtastic Italia
description: misura di AirUtilTX nel mesh e valutazioni a riguardo
published: true
date: 2023-03-08T13:47:14.057Z
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

Forte di questa assunzione, mi sono dedicato per qualche giorno alle verifiche conseguenti per arrivare alla conclusione di oggi che qui riassumo:
>l'assunzione è erronea perché mentre è vero che qualunque nodo connesso a una porta seriale attiva in ricezione e trasmissione effettivamente emette un messaggio di Telemetry ogni minuto, ciò non avviene per i nodi non connessi a porte seriali. In questo caso la tramissione, analizzando i dati raccolti in questi giorni, avviene ogni 15 minuti
> 
Ho grossolanamente definito "porta attiva in ricezione e trasmissione" per evidenziare il fatto che il device collegato alla porta USB con attivo il mio monitor invia un messaggio di Telemetry ogni minuto avendo ricevuto in esordio gli effetti dell'apertura della meshtastic interface col comando meshtastic.serial_interface.SerialInterface().

In assenza di questa sollecitazione un qualunque nodo invia i messaggi di Telemetry contenenti le informazioni ChanUtil e AirUtilTX con una ferquenza che sperimentalmente ho verificato essere di uno ogni 15 minuti. Non so se esista un parametro che definisca questa condizione oppure è previsto così intrinsecamente al firmware.





