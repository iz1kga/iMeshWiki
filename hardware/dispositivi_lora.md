---
title: Schede LoRa
description: Schede LoRa compatibili con Meshtastic
published: true
date: 2024-04-28T07:55:52.419Z
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
Disponibili in diverse vesioni (normale, tracker, ink, stick), siamo ad oggi alla rel. 3.1 basata su ESP32 e SX1262, integra WiFi 2.4GHz e BT, connettore USB-C per scambio dati e alimentazione. Dispone di un connettore per collegare una eventuale batteria LiPo di cui gestisce anche la ricarica. Dotata a seconda delle versioni di display OLED o INK. Perfetta per chi comincia mostra però qualche lacuna di caso di nodi autoalimentati (pannelli solari) e non presidiati: consuma un pò di più rispetto altri dispositivi e tende a bloccarsi se la tensione della batteria LiPo scende sotto certi valori e potrebbe poi non ripartire. Un funzionamento talvolta erratico in funzione della tensione di alimentazione. Da attenzionare nel caso di installazioni remote.

Modello base con display OLED:
![heltec4.png](/heltec4.png =250x)

Display Ink:
![heltec3.png](/heltec3.png =250x)

Stick:
![heltec2.png](/heltec2.png =250x)

Tracker con GPS:
![heltec1.png](/heltec1.png =250x)


## RAK WisBlock

### modulo Core RAK4631 su Base RAK19007

![rak4631on19007.jpg](/hardware/rak4631on19007.jpg =250x)
[Sistema modulare](https://store.rakwireless.com/pages/wisblock) composto da una scheda madre "Base" su cui installare i moduli per le funzionalità richieste.
Un [kit Meshtastic](https://store.rakwireless.com/products/wisblock-meshtastic-starter-kit) minimo richiede un modulo Core RAK4631 per avere LoRa e BLE, a cui possono essere aggiunti un modulo sensore ed un modulo GPS.
Il display è opzionale e non è possibile avere contemporaneamente funzionalità LoRa e Wi-Fi.
In compenso, questo sistema offre i consumi più bassi e l'aggiornamento firmware più semplice tra tutti i dispositivi compatibili con Meshtastic.