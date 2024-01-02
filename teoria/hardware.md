---
title: Hardware
description: 
published: true
date: 2024-01-02T20:57:13.322Z
tags: 
editor: markdown
dateCreated: 2023-01-27T13:28:35.196Z
---

# Hardware compatibile con MeshTastic

## T-LoRa (Lora 32)
![lora32.jpg](/hardware/lora32.jpg =250x)
Scheda basata su ESP32, è economica, piccola e integra display, BLE, Wi-Fi ma non il GPS.
Basso assorbimento e buona affidabilità la rendono adatta all'uso come nodo fisso autoalimentato.

Si può aggiungere agevolmente un ricevitore GPS per trasformare questa scheda in un ottimo nodo mobile.

[Modulo GPS](https://it.aliexpress.com/item/1005005594442876.html)

[![gpsconn.png](/hardware/gpsconn.png =250x)](/hardware/gpsconn.png)
Connessione modulo GPS


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