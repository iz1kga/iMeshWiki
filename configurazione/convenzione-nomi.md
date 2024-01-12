---
title: Convenzione del nome dei nodi
description: 
published: true
date: 2024-01-12T15:14:05.038Z
tags: 
editor: markdown
dateCreated: 2023-02-16T16:55:00.384Z
---

Ciascun nodo Meshtastic è identificato da un nodeID, derivato dal MAC address Bluetooth. Il firmware assegna automaticamente un "Long Name" al nodo con la logica "Meshtastic" + spazio + ultimi quattro caratteri del Mac address Bluetooth, per esempio:

`Meshtastic af67`

L'utente ha la facoltà di modificare il Long Name come preferisce, perché l'identificazione univoca del nodo è garantita dal nodeID.

Tuttavia, per evitare che sulla mappa possano comparire nodi omonimi, è consigliabile che anche il Long Name sia univoco.
