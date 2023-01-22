---
title: Teoria
description: Teoria della mesh
published: true
date: 2023-01-22T20:10:46.684Z
tags: 
editor: markdown
dateCreated: 2023-01-21T23:18:47.654Z
---

<!-- TITLE: Teoria Della Mesh -->
<!-- SUBTITLE: A quick summary of Teoria Della Mesh -->

## Tipologia di nodi
I nodi possono essere di diverso tipo:
* client
* router
* gateway

Il nodo di tipo client è quello che viene usato dagli utenti per accedere alla mesh e comunicare con gli altri utenti.
Il nodo di tipo router si occupa di instradare I pacchetti ma non è pensato per interfacciarsi con gli utenti.
Il nodo di tipo gateway instrada verso e da internet i pacchetti ricevuti, per fare questo utilizza la connesione a un broker MQTT.

Qeste tipologie di nodi possono essere unite, ad esempio può esistere un client gateway o un client_router.

## Una mesh efficiente

Quello che vorremmo ottenere è una mesh efficiente che permetta di far circolare i messaggi in modo rapido e affidabile. Per fare questo è importante la progettazione della rete in modo che i nodi siano configurati opportunamente.

### Nodi Backbone di primo livello

Questi sono i nodi principali della rete, sono dei nodi fissi installati in posizione strategica e sono quelli che garantiscono grazie l'elevata copertura il minimo numero di HOP che i pacchetti devono fare per raggiungere la loro destinazione. Questi nodi dovrebbero essere così configurati:
* Tipo - ROUTER o CLIENT_ROUTER
* Limite Hop - min 3 max 4

### Nodi Backbone di secondo livello

Questi sono i nodi secondari della rete, sono dei nodi fissi. Sono quei nodi che permettono ai nodi utente di raggiungere I nodi principali quando questi sono da loro direttamente raggiungibili.
Questi nodi dovrebbero essere così configurati:
* Tipo - ROUTER o CLIENT_ROUTER
* Limite Hop - min 4 max 5

### Nodi client o utente

Questi sono i nodi degli utenti della rete e dovrebbero essere così configurati:

* Tipo - CLIENT
* Limite Hop - min 5 max 7

### Gateway

I gateway sono dei nodi che instradando da e tramite internet i pacchetti ricevuti permettono di unire parti della mesh che altrimenti non sarebbero in comunicazione e di inviare informazioni ad alcuni server che permettono, ad esempio, di generare una mappa dinamica dei nodi della mesh (https://hub.iz1kga.it).

Bisogna ricordare che la filosofia della mesh è quella di garantire il suo **funzionamento in qualsiasi condizione**. Da questo si deduce che l'utilizzo dei gateway debba essere limitato il più possibile e possibilmente per la sola funzione della generazione della mappa. 

Questo si può ottenere progettando correttamente la rete. Al momento ci sono diversi gateway operativi che verranno disattivati e sostituiti da nodi di primo livello.

## Esempio di infrastruttura
![mesh-diagram.jpg](/mesh-map/mesh-diagram.jpg =450x671)

## Come funziona il routing
https://www.youtube.com/watch?v=7v6UbC5blJU&ab_channel=Meshtastic