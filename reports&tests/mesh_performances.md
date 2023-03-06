---
title: Mesh performances
description: 
published: true
date: 2023-03-06T17:08:59.838Z
tags: 
editor: markdown
dateCreated: 2023-02-15T17:54:35.741Z
---

# Lo strumento di controllo sviluppato 
by Vincenzo Lorenzale il 6 Marzo 2023

---
Da Dicembre 2020  sto seguendo il progetto Meshtastic che si propone di creare una rete di comunicazione su banda 868Mhz con apparecchi basati su ESP32 e LoRa radio (es.: TTGO-LoRa32-oled). Fin da inizio 2021 ho pensato di costruire uno strumento atto al controllo dei messaggi di protocollo nel mesh e all'utilizzo degli stessi per una rappresentazione grafica, in tempo reale, della posizione gps dei vari nodi collegati verso il nodo di controllo centrale che raccogliesse anche tutti i messaggi di testo interccorsi in rete e conservasse il tutto in un archivio storico.

Sono passati due anni d'allora e tutto il progetto ha avuto la sensibile evoluzione che mi ha portato a integrare/perfezionare lo strumento sviluppato due anni fa per arrivare alla versione attuale che qui presento.
## Requisiti hw/sw
1. PC standard che supporti Windows 10
2. Python3 ver. 3.9 o superiore (oggi meshtastic python richiede appunto minimo la ver. 3.9)
3. un Tlora TTGO-LoRa32-oled o equivalente per collegamento seriale a PC via USB
4. configurazione del suddetto Tlora come router_client http host e mqtt client verso il server che connette tutti i mesh router (nel nostro caso meshtastic.iz1kga.it)
5. avendo la python CLI meshtastic già installata, occorre installare in python anche i seguenti moduli:
- pip install pyqt5
- pip install pyqtwebengine
- pip install folium 

L'applicazione python-PyQt5 oggetto di questa descrizione si chiama broadcast_msg_pyq5.py ed è scaricabile da https://github.com/vinloren/meshtastic_broadcast clonando il repository o via download in formato  zip (il relativo README.md fa ancora riferimento alla vecchia versione non avendolo ancora aggionato alla descrizione attuale)
## Obiettivi dell'applicazione
Più che fare una lista mi pare più utile prsentare l'immagine della GUI desrivendone i componenti attraverso i quali vengono raggiunti gli obiettivi desiderati.




