---
title: Convenzione del nome dei nodi
description: 
published: true
date: 2023-02-17T14:40:11.114Z
tags: 
editor: markdown
dateCreated: 2023-02-16T16:55:00.384Z
---

Ciascun nodo Meshtastic è identificato da un nodeID, derivato dal MAC address Bluetooth. Il firmware assegna automaticamente un "Long Name" al nodo con la logica "Meshtastic" + spazio + ultimi quattro caratteri del Mac address Bluetooth, per esempio:

`Meshtastic af67`

L'utente ha la facoltà di modificare il Long Name come preferisce, perché l'identificazione univoca del nodo è garantita dal nodeID.

Tuttavia, per evitare che sulla mappa possano comparire nodi omonimi, è consigliabile che anche il Long Name sia univoco.

Per dare uno standard e aiutare gli utenti a entrare nel sistema abbiamo valutato che alcune informazioni debbano essere facilmente discernibili.

Purtroppo il protocollo attuale non dispone di tutte queste informazioni dobbiamo quindi poterle dedurre dal nome dei nodi stessi.

Abbiamo quindi pensato di consigliare una convenzione per la composizione del nome dei nodi per le reti Meshtatic di libero accesso:

**nome + gateway + frequency + UID**

Di seguito una spiegazione dei vari campi:

### Nome nodo
Il nome nodo deve essere composto da caratteri alfanumerici, è consentito il solo carattere speciale "-"

`([A-Za-z0-9]+)`

### Campo Gateway
Il campo è obbligatorio per permettere il riconoscimento dei nodi gateway

`(GW)
`
### Campo Frequency
Il campo è obbligatorio per nodi fissi e gateway per permettere di identificare la frequenza su cui operano i nodi già presenti un una zona.

`(433|868)`

### Campo UID
Il campo è obbligatorio per i nodi mobili in modo da garantire l'unicità del nodo anche in presenza di molti nodi mobili

`([A-Fa-f0-9]{4})`

I campi possono essere separati da trattini o spazi.

---

Di seguito una tabella che esemplifica i principi della convenzione:

![namingconvention.jpg](/namingconvention.jpg)

È disponibile un **[validatore interattivo](https://map.loraitalia.it/?page=validator)** per verificare la corretta semantica del nome nodo
