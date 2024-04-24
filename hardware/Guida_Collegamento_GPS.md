---
title: Come collegare il GPS
description: Guida al collegamento di un modulo GPS
published: true
date: 2024-04-24T20:56:39.538Z
tags: gps
editor: markdown
dateCreated: 2024-04-24T20:56:39.538Z
---

# Introduzione
 Questa guida informativa vi aiuterà nel processo di aggiungere un modulo GPS al vostro nodo Meshtastic. L'aggiunta di questo modulo fornisce funzionalità GPS precise e un orologio in tempo reale (RTC), eliminando la necessità del WiFi o di uno smartphone per poter mantenere il corretto orario. Questo miglioramento è particolarmente vantaggioso per la mesh, dove è fondamentale monitorare la durata dall'ultimo dispositivo visto. Tuttavia, è importante notare che il modulo GPS aumenterà il consumo di energia del tuo nodo. Affronteremo questo problema spiegando in dettaglio come incorporare un interruttore o un transistor NPN 2N2222 nella configurazione. Ciò consente la gestione dell'alimentazione da parte del firmware, preservando la durata della batteria senza sacrificarne le funzionalità.
 # Considerazioni sul consumo energetico
I moduli GPS hanno solitamente un elevato consumo energetico, che può potenzialmente ridurre la durata della batteria del nodo. Per mitigare questo, sono possibili due approcci:

1. Interruttore manuale: un semplice interruttore di accensione/spegnimento per il modulo GPS, che consente la gestione manuale dell'alimentazione.
2. Transistor NPN 2N2222: facilita il controllo automatico dell'alimentazione tramite il firmware, consentendo al dispositivo di spegnere il modulo GPS in base a condizioni specifiche o dopo un periodo prestabilito.

# Materiale Necessario
1. Il vostro nodo (heltec / Lilygo / RAK ...)
2. Modulo GPS (nel nostro esempio useremo un ATGM336H, ma i passaggi sono uguali per altri moduli) 
3. Un transistor NPN, consigliato il 2N2222
4. Filo, saldatore, stagno, flussante e materiale da saldatura
5. (opzionale) Un interruttore
