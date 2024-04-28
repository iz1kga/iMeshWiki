---
title: Come collegare il GPS
description: Guida al collegamento di un modulo GPS
published: true
date: 2024-04-28T09:22:11.150Z
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

# Istruzioni
Heltec V3:
![schema_collegamento.webp](/hardware/gps/schema_collegamento.webp)
1. Saldare un filo dal pin TX del GPS al pin GPIO 48 di Heltec (o un altro GPIO libero)
2. Saldare un filo dal pin RX del GPS al pin GPIO 47 di Heltec (o un altro GPIO libero)
3. Saldare un filo dal pin GND del GPS al pin GND di Heltec
4. Saldare un filo dal piedino sinistro del transistor npn (guardandolo dal lato piatto) al pin VCC del gps
5. Saldare un filo dal piedino destro del transistor npn al pin 3V3 di Heltec
6. Saldare un filo dal piedino centrale del transistor npn al pin GPIO 48 di Heltec (o un altro GPIO libero)
7. Accendere il nodo e andare nelle sue impostazioni usando l'app su telefono o il client web o CLI
8. Nel menù 'Position' impostare il GPS come 'Enabled'
9. Impostare GPS_RX_PIN con il numero del GPIO usato per il collegamento al pin TX del GPS (si, devono essere invertiti. questo perchè il GPS trasmette dati dal pin TX e la scheda li riceve dal pin RX e viceversa)
10. Impostare GPS_TX_PIN con il numero del GPIO usato per il collegamento al pin RX del GPS
11. PIN_GPS_EN con il numero del GPIO usato per il collegamento al piedino centrale del transistor
12. Salvare le impostazioni

Una volta che la scheda sarà riavviata, potrete scorrere tra le pagine e verificare nell'ultima che il GPS sia stato riconosciuto. Se è così, leggerete inizialmente 'No GPS fix' che indicherà che il GPS sta cercando satelliti. Una volta trovati, vi mostrerà le vostre coordinate.
Se invece viene mostrato 'GPS disabled' basterà premere velocemente 3 volte il tasto utente (quello che usate per scorrere tra le pagine) per attivarlo
Se la scritta riporta 'GPS not present', ricontrollate i vostri collegamenti e le impostazioni
