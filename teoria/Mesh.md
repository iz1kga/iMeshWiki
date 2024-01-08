---
title: Teoria
description: Teoria della mesh
published: true
date: 2024-01-08T18:17:33.957Z
tags: 
editor: markdown
dateCreated: 2023-01-21T23:18:47.654Z
---

<!-- TITLE: Teoria Della Mesh -->
<!-- SUBTITLE: A quick summary of Teoria Della Mesh -->

## Tipologia di nodi
Le configurazioni che abbiamo pensato per il buon funzionamento della rete prevedono 3 tipologie di nodi:
* client
* router
* gateway

Il nodo di tipo client è quello che viene usato dall'utente finale per accedere alla mesh e comunicare con gli altri.
Il nodo di tipo router ha una funzione infrastrutturale e asseconda la necessità di risparmio energetico dettata da una probabile installazione a fotovoltaico.
Il nodo di tipo gateway instrada, attraverso la connessione internet a un broker MQTT, il traffico ricevuto, sostituendo una tratta radio non ancora in essere.

Qeste tipologie di nodi possono essere unite: può, ad esempio, esistere un client-gateway o un gateway-router.

## Una mesh efficiente

Quello che vorremmo ottenere è una mesh efficiente che permetta di far circolare i messaggi in modo rapido e affidabile. 
Con questo scopo si è progettata la rete e la configurazione dei nodi che ne entrano a far parte.

### Nodi Backbone di primo livello

Questi sono i nodi principali della rete: sono installati in modo fisso in posizione strategica e garantiscono, grazie all'elevata copertura geografica, il minimo numero di HOP che i pacchetti devono fare per raggiungere la loro destinazione. Questi nodi dovrebbero essere così configurati:
* Tipo - ROUTER
* Limite Hop - 3

### Nodi Backbone di secondo livello

Questi sono i nodi secondari della rete: sono fissi e permettono ai nodi client di raggiungere i nodi principali quando questi non sono da loro direttamente raggiungibili.
Questi nodi dovrebbero essere così configurati:
* Tipo - ROUTER
* Limite Hop - 3

### Nodi client o utente

Questi sono i nodi finali della rete, quelli effettivamente utilizzati dagli utenti e dovrebbero essere così configurati:

* Tipo - CLIENT
* Limite Hop - min 3 max 5

### Gateway

I gateway sono dei nodi che instradamo da e tramite internet i pacchetti ricevuti permettendo di unire parti della mesh che altrimenti non sarebbero in comunicazione.
Trasmettono inoltre alcune informazioni ad alcuni server che permettono, ad esempio, di generare una mappa dinamica dei nodi della mesh (https://map.loraitalia.it).

Merita di essere sottolineato che lo spirito della mesh è quella di garantire il suo **funzionamento in qualsiasi condizione**. Da questo si deduce che l'utilizzo dei gateway (e di internet, quindi) debba essere limitato il più possibile, idealmente per la sola funzione di generazione della mappa. 

Questo importante obiettivo è raggiungibile ponendo la massima attenzione nella realizzazione dei link radio, curandone la realizzazione in ogni dettaglio.

## Esempio di infrastruttura
![mesh-diagram.jpg](/mesh-map/mesh-diagram.jpg =450x671)

## Come funziona il routing
https://www.youtube.com/watch?v=7v6UbC5blJU&ab_channel=Meshtastic

## LongFast or ShortFast

In ambito LoRa (Long Range), la terminologia "long range" e "short range" si riferisce alla distanza di trasmissione dei dati.

> ### sdf
> |Channel setting | Alt Channel Name | Data-Rate | SF / Symbols | Coding Rate | Bandwidth | Link Budget |
> |Short Range / Fast | Short Fast |	10.94 kbps |	7 / 128 |	4/5 |	250 |	137dB |
> |Short Range / Slow |	Short Slow |	6.25 kbps |	8 / 256 |	4/5 |	250 |	140dB |
> |Medium Range / Fast |	Medium Fast |	3.52 kbps |	9 / 512 |	4/5 |	250 |	143dB |
> |Medium Range / Slow |	Medium Slow |	2.95 kbps |	10 / 1024 |	4/5 |	250 |	146dB |
> |Long Range / Fast |	Long Fast |	1.07 kbps (default) |	11 / 2048 |	4/5 |	250 |	148.5dB |
> |Long Range / Moderate |	Long Moderate |	0.335 kbps |	11 / 2048 |	4/8 |	125 |	151dB |
> |Long Range / Slow |	Long Slow |	0.18 kbps |	12 / 4096 |	4/8 |	125 |	154dB |
> |Very Long Range / Slow |	Very Long Slow |	0.09 kbps |	12 / 4096 |	4/8 |	62.5 |	157dB |

"Long range" indica una trasmissione a lunga distanza, con una portata che può superare i 100 km, a seconda delle condizioni ambientali e dell'antenna utilizzata. Questo tipo di trasmissione è ideale per la comunicazione tra dispositivi distanti, come ad esempio tra sensori in una rete di sensori distribuiti in un'area vasta.

"Short range" indica invece una trasmissione a corto raggio, con una portata che può variare da poche decine di metri a un massimo di un paio di chilometri. Questo tipo di trasmissione è utile per la comunicazione tra dispositivi vicini, come ad esempio tra sensori in un edificio o in un campus.

In sintesi, la differenza tra "long range" e "short range" in LoRa si basa sulla distanza di trasmissione dei dati, con la prima che è adatta per coprire grandi aree e la seconda per coprire aree più ridotte. "Long" implica però velocità di trasmissione ridotte, mentre "Short" velocità più elevate.
.
Nel video che segue è possibile vedere un test che mette confronto la trasmissione di tipo "Short/Fast" con quella "Long/Fast":

https://www.youtube.com/watch?v=LbvAMmKtjcE




> ### Relazione tra canali e frequenze:
> |canale | frequenza (433 MHz)| frequenza (868 MHz)|
> |---|---|---|
> |Very Long Slow | 433,000 MHz|869,542 MHz|
> |Long Slow | 433,300 MHz|869,506 MHz|
> |Long Moderate | 433,550 MHz|869,383 MHz|
> |Long Fast | 433,875 MHz|869,482 MHz|
> |Medium Slow | 433,875 MHz|869,449 MHz|
> |Medium Fast | 433,125 MHz|869,453 MHz|
> |Short Slow | 433,600 MHz|869,448 MHz|
> Short Fast | 433,875 MHz|869,448 MHz|
N.B. Non è necessario cambiare la frequenza sul dispositivo; la selezione del canale imposta automaticamente la frequenza.


