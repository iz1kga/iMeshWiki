---
title: Teoria
description: Teoria della mesh
published: true
date: 2024-04-28T08:17:30.638Z
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

## Tipi di canale

Esistono 6 canali predefiniti, che prevedono valori diversi dei seguenti parametri:
*Spreading Factor (SF)* - Quanto i dati vengono distribuiti nel tempo.
*Bandwidth* - Quant'è grande la porzione di spettro che andiamo ad impegnare.
*Coding Rate* - Quanta ridondanza aggiungiamo per proteggerci dal rumore.

> ### Canali predefiniti
> |Channel setting | Alt Channel Name | Data-Rate | SF / Symbols | Coding Rate | Bandwidth | Link Budget |
> |---|---|---|---|---|---|---|
> |Short Range / Fast | Short Fast |	10.94 kbps |	7 / 128 |	4/5 |	250 |	137dB |
> |Short Range / Slow |	Short Slow |	6.25 kbps |	8 / 256 |	4/5 |	250 |	140dB |
> |Medium Range / Fast |	Medium Fast |	3.52 kbps |	9 / 512 |	4/5 |	250 |	143dB |
> |Medium Range / Slow |	Medium Slow |	2.95 kbps |	10 / 1024 |	4/5 |	250 |	146dB |
> |Long Range / Fast |	Long Fast |	1.07 kbps (default) |	11 / 2048 |	4/5 |	250 |	148.5dB |
> |Long Range / Moderate |	Long Moderate |	0.335 kbps |	11 / 2048 |	4/8 |	125 |	151dB |
> |Long Range / Slow |	Long Slow |	0.18 kbps |	12 / 4096 |	4/8 |	125 |	154dB |
> |Very Long Range / Slow |	Very Long Slow |	0.09 kbps |	12 / 4096 |	4/8 |	62.5 |	157dB |

Il data rate è inversamente proporzionale alla distanza teoricamente raggiungibile.
La rete attualmente è configurata sul canale Medium / Fast e garantisce collegamenti stabili di oltre 100 km tra un nodo e l'altro.

Nel video che segue è possibile vedere un test che mette confronto la trasmissione di tipo "Short/Fast" con quella "Long/Fast":

https://www.youtube.com/watch?v=LbvAMmKtjcE




## Relazione tra canali e frequenze:
Per conoscere l'effettiva frequenza di trasmissione è possibile utilizzare il tool disponibile all'indirizzo https://meshtastic.org/docs/overview/radio-settings/#frequency-slot-calculator

Nel caso specifico di LoraItalia viene utilizzato di comune accordo il range di frequenze EU_868 e in Meshtastic il preset MEDIUM_FAST.
![freq_calc_mediumfast.png](/freq_calc_mediumfast.png)
Questo implica che la frequenza effettivamente utilizzata è 869.525MHz  (si veda la voce [Normativa](/teoria/Normativa) per ulteriori dettagli).

**N.B. Non è necessario cambiare la frequenza sul dispositivo: la selezione del modem-preset imposta automaticamente la frequenza (come detto nel caso specifico di LoraItalia 869.525MHz).**

