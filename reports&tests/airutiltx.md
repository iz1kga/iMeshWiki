---
title: AirUtilTx nel mesh Meshtastic Italia
description: misura di AirUtilTX nel mesh e valutazioni a riguardo
published: true
date: 2023-03-15T16:27:37.825Z
tags: 
editor: markdown
dateCreated: 2023-03-08T10:53:04.155Z
---

# Valutazione misura AirUtilTX
by Vincenzo Lorenzale (IU2RPO) addì 8 Marzo 2023

---

### I dati raccolti questa mattina
![merge_from_ofoct.jpg](/merge_from_ofoct.jpg)
### Analisi e commenti
Questa mattina sono stati raccolti i dati di Telemetry intercorsi nel mesh, fra le ore 7:13 e le 10:08, con lo scopo di valutare l'occupazione AirUtilTX presso i 10 router oggi attivi per capire se questa potesse avere peso nella capacità di consegna dei messaggi fra i nodi. 

Per una corretta valutazione dello stato di saturazione della rete sarebbe utile poter conoscere in tempo reale lo stato del valore di AerUtilTX presente al momento presso i router attivi. Secondo la lettura delle specifiche meshtastic, sembrerebbe che ogni nodo invii alla rete un messaggio di Telemetry ogni minuto e quindi, se così fosse, sarebbe piuttosto agevole avere la costante misura di AerUtilTX presso un router di controllo centrale.

Forte di questa assunzione, mi sono dedicato per qualche giorno alle verifiche conseguenti per arrivare alla conclusione di oggi che qui riassumo:
>l'assunzione è erronea perché mentre è vero che qualunque nodo connesso a una porta seriale attiva in ricezione e trasmissione effettivamente emette un messaggio di Telemetry ogni minuto, ciò non avviene per i nodi non connessi a porte seriali. In questo caso la tramissione, analizzando i dati raccolti in questi giorni, avviene ogni 15 minuti. Poi avendo approfondito questa cosa ho imparato che il parametro è configurabile come da https://meshtastic.org/docs/settings/moduleconfig/telemetry e il default è effettivamente 900 secs. (15 minuti)
> 
Ho grossolanamente definito "porta attiva in ricezione e trasmissione", per evidenziare il fatto che il device collegato alla porta USB con attivo il mio monitor invia un messaggio di Telemetry ogni minuto avendo ricevuto in esordio gli effetti dell'apertura della meshtastic interface col comando meshtastic.serial_interface.SerialInterface().

In assenza di questa sollecitazione, e in assenza di connessione BLE con l'App meshtastic o con la Web Gui in BLE o in seriale, qualunque nodo invia i messaggi di Telemetry contenenti le informazioni ChanUtil e AirUtilTX con una frequenza che sperimentalmente ho verificato essere di uno ogni 15 scoprendo poi questo essere il default di configurazione del modulo 'telemetry' come ho acennato sopra.

## Conclusioni
1. A fronte delle constatazioni sopra espresse, mi risuta ora chiaro perché stranamente solo il mio GW desse spesso segni di saturazione arrivando a superare la soglia di guardia. Stamattina poi, analizzando i dati qui esposti, notavo che il mio GW non era solitario perché anche IK1JNS-00 GW_868 superava la soglia alle ore 08:08:13 arrivando al valore di 10.04%. Dall'analisi temporale vedevo anche che questo nodo inviava i messaggi di Telemetry ogni minuto al pari del mio essendo sicuramente connesso in quel periodo a una porta seriale attiva. Vedere il mio router eccedere la soglia nonostante l'invio di messaggi Telemetry ogni 15 minuti (non collegato alla seriale) sta a significare una durata di superamento soglia superiore a questo lasso di tempo: durate inferiori passano verosimilmente inosservabili. 

2. Altra notazione di rilievo è quella che alle 08:13 la rete in toto era probabilmente in saturazione perché in questa condizione si trovavano contemporaneamente sia il mio GW che quello di nome IK1JNS-00. Probabilmente anche altri che però non potevano risultare non avendo inviato messaggi di superamento soglia ovvero avendola magari superata per un lasso di tempo più breve di 15 minuti.

3. Per avere un'immagine più reale della situazione di occupazione di rete occorrerebbe che tutti i router_client avessero configurato nel modulo 'telemetry' il valore 60 al posto di 900 di default in 'Device Metrics Update Interval'. Va però detto che così la rete risulterebbe già di per sè appesantita per il fatto stesso di inviare queste informazioni con una frequenza così alta. E allora il gioco magari non "vale la candela". Si potrebbe però provare..





