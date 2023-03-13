---
title: Produrre debug log mirati
description: permette di raccogliere log di errore in automatico
published: true
date: 2023-03-13T17:35:13.494Z
tags: 
editor: markdown
dateCreated: 2023-03-13T16:48:48.281Z
---

# Debug manager
by IU2RPO Vincenzo Lorenzale il 13 Mar 2023

---
## Obiettivo dell'applicazione
Spesso occorre indagare su presunte malfunzioni o risposte inattese nell'utilizzo delle unità collegate in rete meshtastic e magari sono necessarie ore di attesa circa l'evento da prendere in esame. Ad esempio, il mio GW va spesso in autoboot e apparentemente quando airUtilTx superava il 10% il problema era capire la causa del reboot inaspetato e quindi impostare un 'trigger' che potesse salvare il debug log un certo numero di messaggi prima e dopo l'evento.
## L'applicazione 
E' sviluppata in Python PyQT5 (Python ver. 3.11 ma anche 3.9 andrà bene) e quindi chi non avesse mai installato PyQT5 dovrà fare pip install 
