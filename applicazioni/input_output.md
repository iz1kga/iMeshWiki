---
title: Gestione I/O
description: Gestione I/O
published: true
date: 2023-02-12T14:50:41.082Z
tags: 
editor: markdown
dateCreated: 2023-02-10T10:50:18.072Z
---

## Configurazione di periferiche GPIO

GPIO, o General Purpose Input/Output, si riferisce a un set di pin su un microcontrollore o computer a scheda singola che possono essere programmati come pin di input o output. LoRa, o Long Range, è una tecnologia di comunicazione wireless che consente la trasmissione di dati a lungo raggio con un basso consumo energetico.

Se utilizzati insieme, GPIO e LoRa possono essere utilizzati per creare un sistema di comunicazione wireless in cui i pin GPIO possono essere utilizzati per controllare la comunicazione e il trasferimento dei dati utilizzando la tecnologia LoRa. Ad esempio, è possibile utilizzare un microcontrollore con pin GPIO e un modulo LoRa per creare una rete di sensori wireless, in cui il microcontrollore legge i dati del sensore e li invia a un dispositivo centrale utilizzando il modulo LoRa.

![329989445_724949482593138_2375873192942626684_n.jpg](/329989445_724949482593138_2375873192942626684_n.jpg)

Tieni presente che avrai bisogno di un modulo LoRa compatibile con i pin GPIO del microcontrollore e potresti anche dover scrivere codice per controllare la comunicazione e il trasferimento dei dati tra il microcontrollore e il modulo LoRa.

Attivazione GPIO su T-Beam e T-Lora con firmware Meshtastic 

Per impedire l'accesso da parte di utenti non attendibili, occorre attivare un canale gpio che verrà utilizzato per l'accesso autenticato a questa funzione. Occorrerà installare questo canale sia sul nodo LOCALE che su quello REMOTO.

Collegare il dispositivo LOCALE tramite USB

**Creare un canale GPIO:**

```plaintext
meshtastic --port comXX --ch-add gpio
```

(per cancellare un canale già precedentemente creato)

```plaintext
meshtastic --port comXX --ch-index 1 --ch-del
```

ATTENZIONE: In caso di collegamento ad un server MQTT, verificare che i seguenti settaggi siano ancora attivi:

```plaintext
meshtastic --port comXX --ch-index 0 --ch-set uplink_enabled true --ch-index 0 --ch-set downlink_enabled true
```

Se esegui test locali, potresti anche voler modificare la velocità del canale:

```plaintext
meshtastic --port comXX --ch-medfast
```

Verificare che il canale sia stato creato e copiare il lungo "URL completo" che contiene tutti i canali su quel dispositivo:

```plaintext
meshtastic --port comXX --info
```

example: Complete URL (includes all channels): https://meshtastic.org/e/#CgMSAf1u4nP9oZfsC9-aAnDwt3xHSAk1Hls2mYeaNB4gu0aBGdwaW8SCggBOANAA0gBUBs

Connettere il dispositivo REMOTO tramite USB (o usare la funzione di amministrazione remota per raggiungerlo attraverso la rete)

Abilitare la gestione hardware remota

```plaintext
meshtastic --port comXX  --set remote_hardware.enabled true
```
--------------------------------------------------------------------
(con canale gpio aggiungere --dest !xxxxxxxxx per comando remoto)

meshtastic --ch-index 0 --ch-set downlink_enabled true
meshtastic --ch-index 0 --ch-set uplink_enabled true
meshtastic --ch-index 0 --ch-set psk none

meshtastic --ch-index 1 --ch-set downlink_enabled true
meshtastic --ch-index 1 --ch-set uplink_enabled true
meshtastic --ch-index 1 --ch-set psk none

----------------------------------------------

meshtastic --port com54  --set remote_hardware.enabled true
Attenzione : Con la versione firmware 2.0.3 non occorre attivare questa funzione, con quelle successive non funziona da console, ma occorre collegarsi con l'APP al dispositivo remoto e nella sezione: "Module Setting" > Remote Hardware Config > Remote Hardware enabled >Abilitare il Servizio (ON)

 Successivamente occorre configurare il dispositivo REMOTO per unire il canale gpio che creato sul dispositivo LOCALE:

```plaintext
meshtastic --port comXX --seturl "URL completo copiato dal quello LOCALE"
```

Dal dispositivo LOCALE ora si possono inviare i comandi di scrittura sui GPIO, vedere tabellina di quelli disponibili su TBEAM e TLORA

dispositivo LOCALE:

```plaintext
meshtastic --port comXX --gpio-wrb 2 0 --dest !25a77b70 
```

 (id del dispositivo remoto) , setta a valore 0 il gpio 2

```plaintext
meshtastic --port comXX --gpio-wrb 2 1 --dest !25a77b70
```

 (id del dispositivo remoto) , porta a valore 1 il gpio 2

```plaintext
meshtastic --port comxx --gpio-rd 0x10 --dest !25a77b70
```

 legge il valore del gpio 4.

GPIO disponibili sui seguenti dispositivi:

TBEAM v2.0 perfettamente funzionanti: 2, 13, 14, 15, 25

TLORA V.1.1.6 perfettamente funzionanti: 2, 12, 13, 15, 19

https://www.youtube.com/Ej2QexL5kts