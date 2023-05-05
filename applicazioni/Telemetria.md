---
title: Telemetria
description: 
published: true
date: 2023-05-05T16:28:42.425Z
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
**Tlora-V1.0**
![lora_v1.0_600x600.webp](/lora_v1.0_600x600.webp)

**Tlora-V1.3**
![tlora-v1.3.jpg](/tlora-v1.3.jpg)
Questa versione è pin to pin compatibile con la versione V1.0.

Comparison between Lora V1.3 and Lora V1.0:
1.Product low power design
2.Optimize LORA RF circuit
3.Add battery voltage detection Pin IO35

Ambedue le versioni riportano un bus I2C sui pin 21 (SDA) e 22 (SCL). Ambedue le versioni segnano Oled montato su altro I2C bus (SDA) 4 e (SCL) 15. Tutto lascia quindi pensare che collegare SDA e SCL dei sensori che vogliamo usare a questo I2C bus sia logico. Il fatto che meshtastic abbia previsto un firmware specifico per ciascuna di queste versioni di Tlora1 mi lascia curioso ma posso pensare che sia motivato dal "voltage detection" presente solo sulla versione 1.3.

### Primo tentativo di telemetry
Vado a cablare INA219 e BM280 sulla mia Tlora-V1.0 sulla I2C con SDA 21 / SCL 22, configuro telemetry environment con la Android App e osservo il primo risultato: il Tlora1 sembra funzionare regolarmente ma i dati di telemetry non escono per nulla.

Il supporto sia di Discourse sia di Discord non porta a nulla se non al consiglio di cambiare schedina dato che il Tlora1 è in "phase out" come prodotto usabile.

Non mi do per vinto e vado allora a clonare il git di meshtastic sul mio PC per controllare i sorgenti con platformIO / VScode. Nella definizione delle schede vedo che per la Tlora-V1.0 SDA e SDL sono attribuiti ai pin 4 - 15 mentre per la Tlora-V1.3 SDA / SDL sono sui pin 21 - 22. Avendo io cablato i snsori su questi pin vado allora a caricare il firmware V1_3 al posto del V1 a noto subito che i sensori funzionano bene a scapito però dell' Oled che rimane spento.

Il microcontroller ESP32 cuore del Tlora ha due interfacce IC2 anche se nel pinout ne viene mostrata solo una (quella sui pin 21 - 22) mentre l'altra non viene mostrata come tale ma di supporto a altri servizi tipo il touch screen mentre sotto esiste sui pin 4 - 15. Evidentemente la scelta fatta al momento dello sviluppo del firmware Tlora1 è stata quella di supportare una sola interfaccia I2C che era qualla su cui era cablato il display oled che vede per la Tlora-v1.0 la I2C sui pin 4 - 15 mentre l'hardware della versione 1.3 vede l'oled cablato sulla I2C facente capo ai pin 21 - 22.  

La scelta invece di supportare ambedue le interfacce sulla Tlora-V1.0 avrebbe evitato di creare confusione per chi avesse voluto installare sensori su questa scheda osservandone il pinout che mette in evidenza la IC2 sui pin 21 - 22 mentre invece questa interfaccia è di fatto del tutto ignorata. L'unico modo per capire dove cablare il sensore su TLora-V1.0 è quello di osservare il file variant.h dell'ambiente Tlora-v1 nei sorgenti del progetto git meshtastic non esendo disponibili note a riguardo in nessun wiki.

### Secondo tentativo
Col primo tentativo avevo capito che il firmware Tlora-V1_3 supporta la I2C sui pin 21 - 22 (visibile da pinout comune alle 2 due versioni) mentre sulla scheda Tlora-V1.0 che ha cablato l'oled sull'altra I2C facente capo ai pin 4 - 15 sarebbe richiesto di cablare qui anche i sensori. Mi rimaneva allora da provare ricaricando il firmware Tlora-V1 dopo aver cablato i sensori sulla I2C (non visibile nello schema del pinout) che fa capo ai pin 4 - 15. Detto fatto ho ottenuto il giusto funzionamneto sia del display oled che dei sensori INA219 e BME280 contemporaneamente.

## Conclusioni
1. Se si è in possesso di una Tlora1, prima di tutto va capito se si tratta di una V1.0 o di una V1.3
2. Per capire se è una V1.0 si carica il firmware V1 e se l'oled si accende è una V1 altrimenti è una V1.3 o in alternativa l'oled è guasto.
3. Se abbiamo una V1.0 i sensori vanno cablati sui pin SDA 4 - SCL 15 altrimenti SDA 21 - SCL 22.

### Cablaggio del sensore INA219
1. Vin al +3.3
1. Gnd a un Gnd della Tlora
1. Scl al pin 15 o 22 a seconda se una V1.0 o una V1.3
1. Sda al pin  4 0 21 a seconda se una V1.0 o una V1.3
1. Negativo della batteria al filo nero del connettore JST innestato nella Tlora1
1. Positivo della batteria al V+ del sensore INA219
1. V- del sensore INA219 al filo rosso del connettore JST innestato nella Tlora1

### Dati telemetry environment dai sensori
Temperatura,PA,umidità ambiente si spiegano da soli mentre per il sensore INA219 è interessante notare come un valore di corrente positivo indica il consumo di corrente della batteria che alimenta il Tlora mentre un valore negativo indica l'attuale corrente che sta caricando la batteria grazie a pannello solare o alimentazione via USB.

**Alimentazione via batteria**
![ina219_scarica.jpg](/ina219_scarica.jpg)

**Alimentazione via USB (carica batteria)**
![ina219_carica.jpg](/ina219_carica.jpg)

### Consumi di un Tlora1 senza WiFi
Dall'osservazione fatta grazie al sensore INA219 abbiamo un consumo medio di 58mA che può salire a picchi di 160mA se in trasmissione

### Corrente di carica via USB
Sempre grazie al sensore INA219 vediamo una corrente di carica via porta USB di un PC che parte da 150mA per arrivare gradatamente a 0 dopo circa 14 ore quando il valore di tensione ha raggiunto 4.20V. A questo punto il led rosso di carica si spegne.