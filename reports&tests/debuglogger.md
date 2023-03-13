---
title: Produrre debug log mirati
description: permette di raccogliere log di errore in automatico
published: true
date: 2023-03-13T18:19:27.650Z
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
Ho previsto di fermare il log quando si incotra la sequenza '[Screen] Done with boot' (senza apici) che è quella che compare sempre all'inizio del boot innescato da qualsivogli causa. Naturalmente il programma è aperto ad accettare qualunque altra sequenza che fosse necessaria.# Size out file
### Size out file
E' una progress bar che indica la percentuale di dimensione massima raggiunta dal file che sarà prodotto come log. Il programma prevede di raccogliere 500 messaggi complessivi come dimensione standard (possono essere anche meno però). Sono 249 messaggi prima dell'incontro della sequenza di guardia e 250 messaggi successivi a questa sequenza. Praticamente avremo in uscita un file di dimensioni ridotte intorno a 75kB o anche meno contenente con sicurazza le informazioni che servono.
### Colori della progress bar
La progress bar parte e resta verde in tutta la fase di attesa. Diventa rossa nel momento in cui viene incontrata la sequenza di guardia. Dopo incontrata questa sequenza, il log va ancora avanti per 250 messaggi poi quando la barra diventerà gialla il file debugLog.log prodotto nella stessa cartella dell'applicazione sarà disponibile a successivo trattamento. 
### Altri dettagli
1) Se si preme START quando la raccolta dati è avviata si otterrà il clear dell'area di log. Ciò non influisce per nulla con la raccolta dati che prosegue normalmente.
2) Una volta finita la raccolta si può avviarne un'altra senza ricaricare l'applicazione ma semplicemente premendo nuovamente START.
### L'applicazione
La metterò in github insiame a quanto già esiste per il monitor del mesh. La posto anche qui dato che è un singolo file e chi vuole potrà scaricarlo.
[debug_monitor.py](/debug_monitor.py)




