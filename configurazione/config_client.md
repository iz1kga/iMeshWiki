---
title: Configurazione Nodi
description: 
published: true
date: 2024-01-12T17:56:47.491Z
tags: 
editor: markdown
dateCreated: 2023-01-22T00:08:07.747Z
---

[Una buona configurazione è la base del buon funzionamento della mesh!](/teoria/Mesh)

## Nome dispositivo
Il nome del dispositivo permette agli altri nodi di identificare il proprio in maniera univoca.
Ci sono due nomi da impostare: il LongName e lo ShortName 

### LongName
il LongName viene usato nell'elenco dei nodi ricevuti e nella mappa. 
Può contenere lettere, numeri, simboli ed anche icone

**Python CLI:**
```bash
meshtastic --set-owner 'NODE-NAME'
```

### ShortName
Lo short name viene utilizzato per identificare il nodo nella chat. Ha un vincolo sulla lunghezza di 4 caratteri, oppure un'icona.

**Python CLI:**
```bash
meshtastic --set-owner-short  'A1B2'
```

## Radio Lora
Le **normative** in ambito radiantistico non sono armonizzate in tutto il mondo ed è quindi **necessario** selezionare le impostazioni corrette in modo che il dispositivo si comporti come prescritto dalla normativa del paese dove viene utilizzato. Inoltre è necessario impostare *hopLimit* in modo da evitare un'eccessiva propagazione dei pacchetti lora.

### Region
La regione è il parametro che configura il modem LoRa in modo che si attenga alle normative del proprio paese. 
Per l'Italia, selezionare EU_868.

**Python CLI:**
```bash
meshtastic --set lora.region 3
```

### HopLimit
Un pacchetto lora ha un **limite massimo** di nodi da cui può essere ripetuto. 
Ogni ripetizione di un nodo è chiamato **hop**. 
Un nodo client dovrebbe avere impostato l'***hopLimit*** a 3.

**ATTENZIONE NODI CON ALTO NUMERO DI HOPLIMIT POSSONO GENERARE MOLTO TRAFFICO SULLA MESH**


**Python CLI:**
```bash
meshtastic --set lora.hop_limit 3
```

## Role
Il ruolo di un nodo deve essere di tipo **CLIENT**.

```bash
meshtastic --set device.role CLIENT
```
## NodeInfo

Un nodo comunica i propri dettagli tramite un pacchetto di tipo nodeInfo contenente Longname, shortName e modello Hardware. Per i nodi di tipo client i tempi di invio di questo pacchetto non devono essere inferiori ai 3600s per i nodi **mobili** e non inferiore a 10800 per i nodi **fissi**.

## Position

La posizione viene acquisita dal dispositivo in maniera automatica se dotato di ricevitore GPS integrato. In caso contrario è possibile impostare dei valori fissi di latitudine / longitudine oppure far si che questi vengano acquisiti, tramite bluetooth, dallo smartphone.
Impostare non meno di **3600** secondi un nodo **mobile**.
Impostare non meno di **43200** secondi per un nodo **fisso**.

## Telemetry

Il dispositivo, tramite dei sensori interni, può inviare a intervalli regolari il livello di carica della batteria e anche, se dotato di sensori aggiuntivi, misure relative all'ambiente (T/H/P) o - ad esempio - alla corrente e alla tensione di un circuito di alimentazione solare.
Le tempistiche di invio dei pacchetti di telemetria devono essere non inferiori ai **3600** secondi per le **telemetrie del dispositivo** e non inferiori ai **1800** secondi per le **telemetrie ambientali**.

## Neighbor Info

Questo modulo invia in rete informazioni circa i nodi con i quali il nostro nodo riesce a stabilire una comunicazione radio diretta. Attivare questa opzione solo sui nodi **fissi** Questo permette di visualizzare sulla [mappa](https://map.loraitalia.it/) la topologia di rete e ci restituisce informazioni preziose circa la bontà dei link che vengono stabiliti. E' bene attivarlo ed impostare a 3600 secondi la frequenza di invio.

## Tabella Riassuntiva tempistiche pacchetti

### Nodi Mobili

|           Parametro App             |           Parametro CLI               | Tempo (s) |
|-------------------------------------|---------------------------------------|-----------|
|     NodeInfo Broadcast Interval     |    position.position_broadcast_secs   |    3600   |
|     Position Broadcast Interval     |    position.position_broadcast_secs   |    3600   |
|    Device Metrics Update Interval   |    telemetry.device_update_interval   |    3600   |
| Environment Metrics Update Interval | telemetry.environment_update_interval |    1800   |
{.dense}

### Nodi Fissi

|           Parametro App             |           Parametro CLI               | Tempo (s) |
|-------------------------------------|---------------------------------------|-----------|
|     NodeInfo Broadcast Interval     |    position.position_broadcast_secs   |    10800   |
|     Position Broadcast Interval     |    position.position_broadcast_secs   |    43200   |
|    Device Metrics Update Interval   |    telemetry.device_update_interval   |    3600   |
| Environment Metrics Update Interval | telemetry.environment_update_interval |    1800   |
|    Neighbor Info Update Interval    |      neighbor_info.update_interval    |    3600   |
{.dense}

