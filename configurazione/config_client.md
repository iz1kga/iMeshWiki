---
title: Configurazione Client
description: 
published: true
date: 2023-01-22T09:21:28.546Z
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

Python CLI:
```bash
meshtastic --set-owner 'NODE-NAME_af38'
```

### ShortName
Lo short name viene utilizzato per identificare il nodo nella chat. Ha un vincolo sulla lunghezza di 4 caratteri.

```bash
meshtastic --set-owner-short  'A1B2'
```

## Radio Lora
lorem ipsum
### Region
lorem ipsum
### HopLimit
lorem ipsum

## Role
lorem Ipsum

## Position

## Telemetry

