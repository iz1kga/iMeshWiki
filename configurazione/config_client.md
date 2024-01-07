---
title: Configurazione Client
description: 
published: true
date: 2024-01-07T20:27:32.969Z
tags: 
editor: markdown
dateCreated: 2023-01-22T00:08:07.747Z
---

[Una buona configurazione è la base del buon funzionamento della mesh!](/teoria/Mesh)


## Nome dispositivo
Il nome del dispositivo permette agli altri nodi di identificare il nodo in maniera univoca, non ci sono vincoli particolari sul nome. Ci sono due nomi da impostare: il LongName e lo ShortName 

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
Le **normative** in ambito radiantistico non sono armonizzate in tutto il mondo è quindi **necessario** selezionare le impostazioni corrette in modo che il dispositivo si comporti come prescritto dalla normativa del paese dove viene utilizzato. Inoltre è necessario impostare *hopLimit* in modo da evitare un'eccessiva trasmissione dei pacchetti lora.

### Region
La regione è il parametro che configura il modem LoRa in modo che si attenga alle normative.

| Region    | Value | Description               |
| --------- | ------| -------------------------:|
| `UNSET`   | `0`   | Non Configurato           |
| `US`      | `1`   | Stati Uniti               | 
| `EU_433`  | `2`   | Unione Europea 433MHz     |
| `EU_868`  | `3`   | Unione Europea 868MHz     |
| `CN`      | `4`   | Cina                      |
| `JP`      | `5`   | Giappone                  |
| `ANZ`     | `6`   | Australia e Nuova Zelanda |
| `KR`      | `7`   | Corea                     |
| `TW`      | `8`   | Taiwan                    |
| `RU`      | `9`   | Russia                    |
| `IN`      | `10`  | India                     |
| `NZ_865`  | `11`  | Nuova Zelanda 865MHz      |
| `TH`      | `12`  | Tailandia                 |
| `LORA_24` | `13`  | Tutto il mondo 2.4GHz     |

**Python CLI:**
```bash
meshtastic --set lora.region 3
```

### HopLimit
Un pacchetto lora ha un **limite massimo** di nodi da cui può essere ripetuto. Ogni ripetizione di un nodo è chiamato **hop**. Un nodo client dovrebbe avere impostato l'***hopLimit*** a 3.

**Python CLI:**
```bash
meshtastic --set lora.hop_limit 3
```

## Role
Il ruolo di un nodo, salvo casi particolari, deve essere di tipo **CLIENT**

```bash
meshtastic --set device.role CLIENT
```

## Position

La posizione viene acquisita dal dispositivo in maniera automatica se dotato di ricevitore GPS integrato. In caso contrario è possibile impostare dei valori fissi di latitudine / longitudine oppure far si che questi vengano acquisiti, tramite bluetooth, dallo smartphone.

## Telemetry

Il dispositivo tramite dei sensori interni può inviare a intervalli regolari il livello di carica della batteria e anche, se dotato di sensori aggiuntivi, misure relative all'ambiente (T/H/P) o - ad esempio - alla corrente e alla tensione di un circuito di alimentazione solare.