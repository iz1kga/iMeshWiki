---
title: Produrre debug log mirati
description: permette di raccogliere log di errore in automatico
published: true
date: 2023-03-13T17:51:31.825Z
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
E' sviluppata in Python PyQT5 (Python ver. 3.11 ma anche 3.9 andrà bene) e quindi chi non avesse mai installato PyQT5 dovrà fare pip install pyqt5.
![debug_manager_2023-03-13_113956.png](/debug_manager_2023-03-13_113956.png)
### Tasto START
Avvia l'applicazione (ovvio) dopo aver inserito in Porta e Velocità i valori della COMx collegata al device e della velocità di trasmissione che è già set a 115200 b/s in accordo a quanto richiesto dall'interfaccia seriale dei nostri device.
### Tasto STOP
Normalmente non è necessario usarlo perché è tutto automatico come vedremo. Se vogliamo fermare la raccolta dati e produrre immediatamente il log, allora usiamo STOP.
### Skip msg on
Per default ho impostato di tralasciare i messaggi di tipo mqtt perché normalmente non interessanti a scopo diagnostico. Se li vogliamo tutti basta scrivere nella casella qualcosa che non sarà mai presente nei messaggi. Es.: lgbqt+.. 
### Stop su
Ho previsto di fermare il log quando si incotra la sequenza '[Screen] Done with boot' (senza apici) che è quella che compare sempre all'inizio del boot innescato da qualsivogli causa. Naturalmente il programma è aperto ad accettare qualunque altra sequenza che fosse necessaria.


