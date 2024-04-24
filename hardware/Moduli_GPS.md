---
title: Moduli GPS
description: Raccolta di Moduli GPS consigliati e relative configurazioni 
published: true
date: 2024-04-24T20:43:02.127Z
tags: accessori, bds, galileo, glonass, gps, qzss, rak, rak12500, sbas
editor: markdown
dateCreated: 2024-04-24T14:50:47.747Z
---

# ATGM336H
![atgm336h_dito.png](/hardware/gps/atgm336h_dito.png)
GPS di dimensioni molto contenute, misura appena 16x13x6 mm e ha un costo di circa 7€ su [Aliexpress](https://it.aliexpress.com/item/4001147538089.html?spm=a2g0o.detail.pcDetailTopMoreOtherSeller.2.213649F549F5Bw&gps-id=pcDetailTopMoreOtherSeller&scm=1007.40050.354490.0&scm_id=1007.40050.354490.0&scm-url=1007.40050.354490.0&pvid=9b92e5de-296c-4fc7-864f-1aeea9d1d445&_t=gps-id:pcDetailTopMoreOtherSeller,scm-url:1007.40050.354490.0,pvid:9b92e5de-296c-4fc7-864f-1aeea9d1d445,tpp_buckets:668%232846%238109%231935&pdp_npi=4%40dis%21EUR%216.63%210.95%21%21%216.93%210.99%21%402103250717139894742103843e3fc2%2110000014894512456%21rec%21IT%21%21AB&utparam-url=scene%3ApcDetailTopMoreOtherSeller%7Cquery_from%3A). L'ATGM336H è un'ottima alternativa a basso profilo al modulo GPS NEO-6M simile comunemente utilizzato per Meshtastic. Usa lo stesso protocollo NMEA0183 e quindi sono completamente intercambiabili. 
Dai test eseguiti, sembra avere delle ottime prestazioni e riesce a stabilire la posizione in un minuto o due quando viene acceso dopo qualche ora. Ha una piccola batteria che gli permette di tenere memorizzate le informazioni per un paio d'ore (sto ancora misurando quanto effettivamente duri) ottenendo così un tempo di avvio di 1s.
Ha una precisione di 2,5 m ed è in grado di aggiornare le sue coordinate 1-10 volte al secondo.
Constellazioni supportate: BDS/GPS/GLONASS/GALILEO/QZSS/SBAS 
Consumo energetico: 25mA (acquisizione satelliti), 20mA (Tracking satelliti) 
Baud Rate: 9600 bps
[Datasheet](https://www.icofchina.com/d/file/xiazai/2016-12-05/b5c57074f4b1fcc62ba8c7868548d18a.pdf)
![atgm336h_anteriore.jpg](/hardware/gps/atgm336h_anteriore.jpg)
![atgm336h_rear.jpg](/hardware/gps/atgm336h_rear.jpg)
![atgm336h.jpg](/hardware/gps/atgm336h.jpg)


