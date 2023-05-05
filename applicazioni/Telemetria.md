---
title: Telemetria
description: 
published: true
date: 2023-05-05T07:21:10.939Z
tags: 
editor: markdown
dateCreated: 2023-02-12T22:00:02.689Z
---

# Telemetria e Sensori
Il sensore BMP280 è un sensore di pressione e temperatura ambiente. Viene utilizzato per misurare la pressione atmosferica e la temperatura nell'ambiente circostante. Questo tipo di sensore è utile in molti settori, tra cui la meteorologia, la navigazione aerea, la monitorizzazione della qualità dell'aria, la rilevazione di altitudine e altro ancora.

Il BMP280 utilizza un sensore di pressione piezoresistivo e un termistore per misurare la pressione atmosferica e la temperatura, rispettivamente. Il sensore è altamente preciso e robusto, il che lo rende adatto per una vasta gamma di applicazioni.

In sintesi, il sensore BMP280 serve a misurare la pressione atmosferica e la temperatura ambiente in modo preciso e affidabile, rendendolo utile in molte applicazioni diverse.

![bme280.jpg](/bme280.jpg)

Il sensore BME280 è un sensore ambientale completo che combina tre sensori in uno: un sensore di pressione barometrica, un sensore di temperatura e un sensore di umidità relativa. Questo rende il BME280 uno strumento versatile per la misura dell'ambiente.

Il sensore di pressione barometrica viene utilizzato per misurare la pressione atmosferica, che può essere utilizzata per calcolare l'altitudine. Il sensore di temperatura misura la temperatura ambiente e il sensore di umidità relativa misura l'umidità nell'aria. Questi dati combinati possono essere utilizzati per determinare il comfort ambientale, per monitorare la qualità dell'aria o per la meteorologia.

Inoltre, il BME280 è un sensore molto preciso e facile da utilizzare, il che lo rende adatto per molte applicazioni diverse, tra cui la progettazione di sistemi di controllo ambientale, la meteorologia, la navigazione aerea, la monitorizzazione della qualità dell'aria e molto altro ancora.

In sintesi, il sensore BME280 serve a misurare la pressione atmosferica, la temperatura ambiente e l'umidità relativa in modo preciso e affidabile, rendendolo utile in molte applicazioni differenti.

![s-l1600.jpg](/s-l1600.jpg)

Il sensore INA219 è un sensore di corrente e tensione per sistemi a bassa potenza. Questo sensore viene utilizzato per misurare la corrente e la tensione in sistemi elettronici a bassa potenza, come ad esempio i dispositivi alimentati a batteria o i sistemi di controllo delle energie rinnovabili.

Il sensore INA219 è un sensore a tensione a base di shunt, che significa che misura la corrente attraverso una resistenza nota, nota come shunt. Questo sensore è in grado di misurare correnti fino a 3.2A con un'accuratezza del ±1% e tensioni fino a 26V con un'accuratezza del ±3%.

Inoltre, il sensore INA219 ha un'elevata risoluzione e una rapida risposta, il che lo rende adatto per una vasta gamma di applicazioni, tra cui il monitoraggio della batteria, la misurazione dei carichi elettrici, il controllo dell'alimentazione e molto altro ancora.

In sintesi, il sensore INA219 serve a misurare corrente e tensione in sistemi a bassa potenza in modo preciso e affidabile, rendendolo utile in molte applicazioni diverse.

# Configurare la Tbeam e Tlora con i  Sensori

## Tlora-V1.0 (by IU2RPO)
**Premessa**
Tutto nasce dalla rottura del connettore micro usb del Tlora2-1.1.6 che usavo come GW su palo con antenna sul balcone. Senza connettore il device rimaneva congelato al firmware e alla configurazione del momento impedendomi ulteriori prove circa ottimizzazione di pannello solare e batteria da associare al progetto. 

Una via d'uscita immediata la vedevo nell'uso di un TloraV1.0 dei due in mio possesso ma occorreva che questa unità potesse fornire i dati di telemetry di batteria e di ambiente atmosferico così come li forniva il Tlora2-1.1.6 già sperimentato con successo.

### Approccio, problemi e soluzione
Sapendo che i sensori INA219 e BME280 funzionano utilzzando interfaccia I2C, affronto il problema andando a vedere nel pinout del Tlora-V1 (TTGO LoRa32-oled V1) quali pin scegliere per connettere i segnali SDA e SCL.

Va anche onsiderato che di versioni Tlora1 ne esistono due pin to pin compatibili e non distinguibili ad osservazione esterna. Vediamo allora le immagini dei rispettivi pinout:







