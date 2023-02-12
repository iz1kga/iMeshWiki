---
title: Teoria
description: Teoria della mesh
published: true
date: 2023-02-12T13:11:26.959Z
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

## LongFast or ShortFast

In ambito LoRa (Long Range), la terminologia "long range" e "short range" si riferisce alla distanza di trasmissione dei dati.

    "Long range" indica una trasmissione a lunga distanza, con una portata che può superare i 10 km, a seconda delle condizioni ambientali e dell'antenna utilizzata. Questo tipo di trasmissione è ideale per la comunicazione tra dispositivi distanti, come ad esempio tra sensori in una rete di sensori distribuiti in un'area vasta.

    "Short range" indica invece una trasmissione a corto raggio, con una portata che può variare da poche decine di metri a un massimo di un paio di chilometri. Questo tipo di trasmissione è utile per la comunicazione tra dispositivi vicini, come ad esempio tra sensori in un edificio o in un campus.

In sintesi, la differenza tra "long range" e "short range" in LoRa si basa sulla distanza di trasmissione dei dati, con la prima che è adatta per coprire grandi aree e la seconda per coprire aree più ridotte.

https://youtu.be/LbvAMmKtjcE