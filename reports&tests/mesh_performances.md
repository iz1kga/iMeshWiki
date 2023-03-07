---
title: Mesh performances
description: 
published: true
date: 2023-03-07T12:02:10.901Z
tags: 
editor: markdown
dateCreated: 2023-02-15T17:54:35.741Z
---

# Lo strumento di controllo sviluppato 
by Vincenzo Lorenzale il 6 Marzo 2023

---
Da Dicembre 2020  sto seguendo il progetto Meshtastic che si propone di creare una rete di comunicazione su banda 868Mhz con apparecchi basati su ESP32 e LoRa radio (es.: TTGO-LoRa32-oled). Fin da inizio 2021 ho pensato di costruire uno strumento atto al controllo dei messaggi di protocollo nel mesh e all'utilizzo degli stessi per una rappresentazione grafica, in tempo reale, della posizione gps dei vari nodi collegati verso il nodo di controllo centrale che raccogliesse anche tutti i messaggi di testo interccorsi in rete e conservasse il tutto in un archivio storico.

Sono passati due anni d'allora e tutto il progetto ha avuto la sensibile evoluzione che mi ha portato a integrare/perfezionare lo strumento sviluppato due anni fa per arrivare alla versione attuale che qui presento.
## Requisiti hw/sw
1. PC standard che supporti Windows 10
2. Python3 ver. 3.9 o superiore (oggi meshtastic python richiede appunto minimo la ver. 3.9)
3. un Tlora TTGO-LoRa32-oled o equivalente per collegamento seriale a PC via USB
4. configurazione del suddetto Tlora come router_client http host e mqtt client verso il server che connette tutti i mesh router (nel nostro caso meshtastic.iz1kga.it)
5. avendo la python CLI meshtastic già installata, occorre installare in python anche i seguenti moduli:
- pip install pyqt5
- pip install pyqtwebengine
- pip install folium 

L'applicazione python-PyQt5 oggetto di questa descrizione si chiama broadcast_msg_pyq5.py ed è scaricabile da https://github.com/vinloren/meshtastic_broadcast clonando il repository o via download in formato  zip (il relativo README.md fa ancora riferimento alla vecchia versione non avendolo ancora aggionato alla descrizione attuale)

Insieme con broadcast_msg_pyq5.py, nella cardella che conterrà questo file, dovrà essere copiato il file meshDB.db che è lo Sqlite3 DB di supporto all'applicazione.

## Obiettivi dell'applicazione
Più che fare una lista mi pare più utile prsentare l'immagine della GUI desrivendone i componenti attraverso i quali vengono raggiunti gli obiettivi desiderati.
![mesh_data_show_1.png](/mesh_data_show_1.png)

### Campi Home lat e Home lon / scopo
Questi due campi di input devono contenere le coordinate geografiche del nostro router_client e attualmente riportano i valori del qth di vinloren_GW_0a78_868. Chi avesse installato l'applicazione dovrà al primo lancio sostituire queste coordinate con quelle del vero qth prima di dare START. A conclusione del primo lancio le nuove coordinate saranno salvate nel Sqlite3 DB meshDB.db che risiede nella stessa cartella del file python broadcast_msg_pyq5.py in modo che i lanci successivi troveranno automaticamente le nuove coordinate aggiornate.

Lo scopo della fissazione di queste coordinate è quello di poter poiu misurare rilevamento e distanza di tutti i nodi presenti in mesh rispetto alla posizione del nostro client_router.

### Tasto SHOW MAP
Produce una geo map (defaulut OpenStreetMap) con al centro la posizione del nostro router_clien (marker in blu) e tutti i GW presenti nel mesh (markers in rosso) come default. Se la combo box 'map nodes' punta su un nodo non GW anziché il default 'mappa solo i GW', oltre ai GW verra mappata anche la posisione del nodo scelto con un marker verde. 

La mappa apparirà poi cliccando sul tab 'geo map' subito sotto nell'immagine. Una volta aperta la mappa, cliccando sui marker appariranno le relative informazioni da questi riferite.

### Readio button 'storico giorno:'
Se questo widget non è selezionato la mappa conseguente sarà la foto del momento riferita alla posizione dei nodi riportati. Se invece è selezionato la mappa riporterà tutte le posizioni registrate nel giorno prescelto tramite la compo box che gli sta accanto. La scelta del giorno è limitata dai campi 'fra' ed 'e' precompilati ma alterabili a piacimento. Questa limitazione serviva a evitare di avere una lista dei giorni troppo lunga ma allo stato attuale, dato che i riferimenti di posizione geografica dei nodi sono poi stati limitati agli ultimi 7 giorni, oggi risulta ridondante.

### Combo box 'tipo map'
Oltre alla OpenStreetMap sono disponibili altre sorgenti che si possono scegliere fra quelle offerte dalla libreria python folium qui riportate.

### Tab 'Messaggi'
Contiene i dettagli su tutti i messaggi di protocollo e di testo scambiati nel mesh in tempo reale. Il contenuto di questi messaggi oltre ad apparire in questa pagina di Tab, può anche essere salvato in un file .csv per successiva elaborazione su excell se ls checkbox 'genera csv file' a fondo pagina è selezionata. Il file risultante 'meshtastic_data.csv' sarà disponibile nella cartella contenente l'applicazione, deselezionando la checkbox una volta selezionata.
### Tab 'Connessi'
Contiene i riferimenti in tempo reale a tutti i nodi del mesh che al momento colloquiano col nostro client_router. I dati riportati sono autoesplicativi.
### Tab 'GeoMap'
Si spiega da sola ovvero con le note accennate col tasto 'SHOW MAP' e col radio button 'storico giorno:' visti sopra. 
### Text area 'Log protocollo'
Sono sintetizzati in tempo reale i messaggi di protocollo ricevuti e trasmessi da 'mioGW'. Vengono riportati 'date-time', 'user_id', 'longname', 'dest_id', 'tipo messaggio'. Questi campi sono separati da tab e scritti in font 'courier new' (fixed size) in modo che se copiamo tutto il contenuto della text area negli appunti possimo poi creare agevolmante un file di testo in .csv atto a essere caricato in excell (o meglio in OpenOffice) per successive elaborazioni. 






