---
title: Configurazione Client
description: 
published: true
date: 2023-01-22T09:26:45.635Z
tags: 
editor: markdown
dateCreated: 2023-01-22T00:08:07.747Z
---

## Nome dispositivo
Il nome del dispositivo permette agli altri nodi di identificare il nodo in maniera univoca, non ci sono vincoli particolari sul nome. Ci sono due nomi da impostare: il LongName e lo ShortName 

### LongName
il LongName viene usato per visualizzare l'elenco dei nodi ricevuti e la mappa. 

Si di inserire al fondo del nome gli ultimi quatro caratteri dell'ID dispositivo in modo da garantire l'unicità del nome, esempio:

*Nome_Nodo_Lora_**a2db***

**Python CLI:**
```bash
meshtastic --set-owner 'NODE-NAME_af38'
```

### ShortName
Lo short name viene utilizzato per identificare il nodo nella chat. Ha un vincolo sulla lunghezza di 4 caratteri.

**Python CLI:**
```bash
meshtastic --set-owner-short  'A1B2'
```

## Radio Lora
Le normative in ambito radiantistico non sono armonizzate in tutto il mondo è quindi necessario selezionare le impostazioni corrette in modo che il dispositivo si comporti come prescritto dalla normativa del paese dove viene utilizzato. Inoltre è necessario impostare *hopLimit* in modo da evitare un'eccessiva trasmissione dei pacchetti lora.

### Region
La regione è il paraqmetro che configura il modem LoRa in modo che si attenga alle normative.


Region Code	Description
UNSET	Unset
US	United States
EU_433	European Union 433MHz
EU_868	European Union 868MHz
CN	China
JP	Japan
ANZ	Australia & New Zealand
KR	Korea
TW	Taiwan
RU	Russia
IN	India
NZ_865	New Zealand 865MHz
TH	Thailand
LORA_24	2.4 GHz band worldwide

**Python CLI:**
```bash
meshtastic --set lora.region 3
```

### HopLimit
lorem ipsum

## Role
lorem Ipsum

## Position

## Telemetry

