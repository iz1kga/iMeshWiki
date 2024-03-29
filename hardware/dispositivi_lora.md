---
title: Schede LoRa
description: Schede LoRa compatibili con Meshtastic
published: true
date: 2024-02-22T14:35:57.569Z
tags: 
editor: markdown
dateCreated: 2023-01-27T13:28:35.196Z
---

# Schede compatibili con MeshTastic

L'elenco ufficiale e sempre aggiornato è disponibile sul sito ufficiale di Meshtastic all'indirizzo https://meshtastic.org/docs/hardware/devices/

## T-LoRa (Lora 32)
![lora32.jpg](/hardware/lora32.jpg =250x)
Scheda basata su ESP32, è economica, piccola e integra display, BLE, Wi-Fi ma non il GPS.
Basso assorbimento e buona affidabilità la rendono adatta all'uso come nodo fisso autoalimentato.

Si può aggiungere agevolmente un ricevitore GPS per trasformare questa scheda in un ottimo nodo mobile.

![pin-diagram_lora32v2.1_1.6_600x600.webp](/hardware/pin-diagram_lora32v2.1_1.6_600x600.webp)
[Modulo GPS (Aliexpress)](https://it.aliexpress.com/item/1005005594442876.html)
[Modulo GPS (Amazon)](https://www.amazon.it/ICQUANZX-GY-NEO6MV2-Controller-ceramica-resistente/dp/B088LR3488/)

[![gpsconn.png](/hardware/gpsconn.png =250x)](/hardware/gpsconn.png)
Connessione modulo GPS. 
Attenzione, rispetto all'immagine , i pin RX e tX sono da invertire (soltanto su un lato!). Nella configurazione del dispositivo andranno esplicitati i pin sul quale la scheda GPS è stata collegata: 
GPS_RX_PIN: 15
GPS_TX_PIN: 13


## T-Beam
![t-beam.jpg](/hardware/t-beam.jpg =250x)
Scheda basata su ESP32, integra BLE, Wi-Fi, GPS e un alloggiamento per una batteria 18650 Li-ion con circuito di ricarica, rendendola molto comoda per uso portatile.
Il display è opzionale ed è necessario saldarlo per l'installazione.
## T-Echo
![t-echo.jpg](/hardware/t-echo.jpg =250x)

## Heltec LoRa32
![helteclora32.png](/hardware/helteclora32.png =250x)

## RAK WisBlock

### modulo Core RAK4631 su Base RAK19007

![rak4631on19007.jpg](/hardware/rak4631on19007.jpg =250x)
[Sistema modulare](https://store.rakwireless.com/pages/wisblock) composto da una scheda madre "Base" su cui installare i moduli per le funzionalità richieste.
Un [kit Meshtastic](https://store.rakwireless.com/products/wisblock-meshtastic-starter-kit) minimo richiede un modulo Core RAK4631 per avere LoRa e BLE, a cui possono essere aggiunti un modulo sensore ed un modulo GPS.
Il display è opzionale e non è possibile avere contemporaneamente funzionalità LoRa e Wi-Fi.
In compenso, questo sistema offre i consumi più bassi e l'aggiornamento firmware più semplice tra tutti i dispositivi compatibili con Meshtastic.