---
title: Configurazione Router - Gateway
description: 
published: true
date: 2023-01-30T14:47:56.115Z
tags: 
editor: markdown
dateCreated: 2023-01-30T13:59:05.219Z
---

[Una buona configurazione è la base del buon funzionamento della mesh!](/teoria/Mesh)


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
Un pacchetto lora ha un **limite massimo** di nodi da cui può essere ripetuto. Ogni ripetizione di un nodo è chiamato **hop**. Un nodo ROUTER GATEWAY dovrebbe avere impostato l'***hopLimit*** da un minimo di 3 a un massimo di 4 hop (il massimo consentito dal LoRa).

**Python CLI:**
```bash
meshtastic --set lora.hop_limit 3
```

## Role
Per i client l'impostazione del ruolo deve essere di tipo **ROUTER_CLIENT**

```bash
meshtastic --set device.role ROUTER_CLIENT
```

## Position
Per impostare la posizione eseguire il comando seguente

```bash
meshtastic --setlat 45.12 --setlon 7.24 --setalt 250
```

Impostare l'invio della posizione ogni due ore.

```bash
meshtastic --set position.broadcast_secs 7200
```

## MQTT
L'impostazione MQTT permette al dispositivo di collegarsi al broker e instradare e riceve i dati dei nodi via internet. Ricordate il carattere di escape **\\** davanti ai punti esclamativi **!**

```bash
meshtastic --set mqtt.address meshtastic.iz1kga.it
meshtastic --set mqtt.username <USERNAME>
meshtastic --set mqtt.password <PASSWORD>
meshtastic --set mqtt.json_enabled true
meshtastic --set mqtt.encryption_enabled false
meshtastic --set mqtt.enabled true
```

Al fine di ricevere è trasmettere i pacchetti tramite MQTT è necessario configurare il downlink e l'uplink rispettivamente sul canale principale.

```bash
meshtastic --ch-index 0 --ch-set downlink_enabled true
meshtastic --ch-index 0 --ch-set uplink_enabled true
```

## WiFi
Ovviamente è necessario collegare il dispositivo ad una rete WiFi connessa a internet

```bash
meshtastic --set network.wifi_enabled true --set network.wifi_ssid "<SSID>" --set network.wifi_psk "<WiFiPASSWORD>"
```

