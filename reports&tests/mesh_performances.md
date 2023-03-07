---
title: Mesh performances
description: 
published: true
date: 2023-03-07T19:03:08.652Z
tags: 
editor: markdown
dateCreated: 2023-02-15T17:54:35.741Z
---

# Lo strumento di controllo sviluppato 
by Vincenzo Lorenzale il 6 Marzo 2023

---
Da Dicembre 2020  sto seguendo il progetto Meshtastic che si propone di creare una rete di comunicazione su banda 868Mhz con apparecchi basati su ESP32 e LoRa radio (es.: TTGO-LoRa32-oled). Fin da inizio 2021 ho pensato di costruire uno strumento atto al controllo dei messaggi di protocollo nel mesh e all'utilizzo degli stessi per una rappresentazione grafica, in tempo reale, della posizione gps dei vari nodi collegati verso il nodo di controllo centrale che raccogliesse anche tutti i messaggi di testo interccorsi in rete e ne conservasse il tutto in un archivio storico.

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

## Strumenti utili non indispensabil a supporto
1. DB Browser for Sqlite scaricabile at https://sqlitebrowser.org/ per controllare il DB meshDB.db
2. Open Office 4 scaricabile at https://www.openoffice.org/ per eventualmente elaborare gli output dell'applicazione

## Obiettivi dell'applicazione
Più che fare una lista mi pare più utile prsentare l'immagine della GUI desrivendone i componenti attraverso i quali vengono raggiunti gli obiettivi desiderati.
![mesh_data_show_1.png](/mesh_data_show_1.png)

### Campi Home lat e Home lon / scopo
Questi due campi di input devono contenere le coordinate geografiche del nostro router_client e attualmente riportano i valori del qth di vinloren_GW_0a78_868. Chi avesse installato l'applicazione dovrà al primo lancio sostituire queste coordinate con quelle del vero qth prima di dare START. A conclusione del primo lancio le nuove coordinate saranno salvate nel Sqlite3 DB meshDB.db che risiede nella stessa cartella del file python broadcast_msg_pyq5.py in modo che i lanci successivi troveranno automaticamente le nuove coordinate aggiornate.

Lo scopo della fissazione di queste coordinate è quello di poter poi misurare rilevamento e distanza di tutti i nodi presenti in mesh rispetto alla posizione del nostro client_router.

### Tasto SHOW MAP
Produce una geo map (default OpenStreetMap) con al centro la posizione del nostro router_clien (marker in blu) e tutti i GW presenti nel mesh (markers in rosso) come default. Se la combo box 'map nodes' punta su un nodo non GW anziché il default 'mappa solo i GW', oltre ai GW verra mappata anche la posisione del nodo scelto con un marker verde. 

La mappa apparirà poi cliccando sul tab 'geo map' subito sotto nell'immagine. Una volta aperta la mappa, cliccando sui marker appariranno le relative informazioni da questi riferite.

### Radio button 'storico giorno:'
Se questo widget non è selezionato la mappa conseguente sarà la foto del momento riferita alla posizione dei nodi riportati. Se invece è selezionato la mappa riporterà tutte le posizioni registrate nel giorno prescelto tramite la combo box che gli sta accanto. La scelta del giorno è limitata dai campi 'fra' ed 'e' precompilati ma alterabili a piacimento. Questa limitazione serviva a evitare di avere una lista dei giorni troppo lunga ma allo stato attuale, dato che i riferimenti di posizione geografica dei nodi sono poi stati limitati agli ultimi 7 giorni, oggi risulta ridondante.

### Combo box 'tipo map'
Oltre alla OpenStreetMap sono disponibili altre sorgenti che si possono scegliere fra quelle offerte dalla libreria python folium qui riportate.

### Tab 'Messaggi'
Contiene i dettagli su tutti i messaggi di protocollo e di testo scambiati nel mesh in tempo reale. Il contenuto di questi messaggi oltre ad apparire in questa pagina di Tab, può anche essere salvato in un file .csv per successiva elaborazione su excell se ls checkbox 'genera csv file' a fondo pagina è selezionata. Il file risultante 'meshtastic_data.csv' sarà disponibile nella cartella contenente l'applicazione, deselezionando la checkbox una volta selezionata.
### Tab 'Connessi'
Contiene i riferimenti in tempo reale a tutti i nodi del mesh che al momento colloquiano col nostro client_router. I dati riportati sono autoesplicativi.
### Tab 'GeoMap'
Si spiega da sola ovvero con le note accennate col tasto 'SHOW MAP' e col radio button 'storico giorno:' visti sopra. 
### Text area 'Log protocollo'
Sono sintetizzati in tempo reale i messaggi di protocollo ricevuti e trasmessi da 'mioGW'. Vengono riportati 'date-time', 'user_id', 'longname', 'dest_id', 'tipo messaggio'. Questi campi sono separati da tab e scritti in font 'courier new' (fixed size) in modo che se copiamo tutto il contenuto della text area negli appunti possimo poi creare agevolmente un file di testo in .csv atto a essere caricato in excell (o meglio in OpenOffice) per successive elaborazioni. 
### Text area 'Texts ricevuti/trasmessi'
Qui vengono riportati i messaggi di testo intercorsi nel mesh con riferimenti temporali e indicazione del longname che li ha inviati.
### Tasto 'START'
Serve ad avviare l'applicazione e se premuto una volta avviata, fa recepire al programma l'invio di un nostro messaggio immediato al mesh o il cambiamento di stato fra 'solo ricezione' ovvero invio periodico di messaggio di test ogni 10 minuti.

l'invio periodico del messaggio riportato dal text field 'Dati inviati' accanto a START avviene automaticamente con cadenza ogni 10 minuti se la checkbox 'solo ricezione' non è marcata. Questi messaggi hanno, oltre a data-ora, una numerazione progressiva atta alla verifica di quanto è stato ricevuto nel mesh. 

### Campo di testo 'Dati inviati'
Il contenuto di questo campo sarà inviato periodicamente oppure immediatamente premendo START se la checkbox 'Mess. immediato' è marcata.
### Checkbox 'solo ricezione'
Già spiegato sotto tasto 'START'
### Checkbox 'Mess. immediato'
Già spiegato sotto campo di testo 'Dati inviati'.
### Checkbox 'Autorisposta'
Se questa checkbox è marcata, qualunque messaggio di testo in arrivo contenete la parola 'qsl?' (senza apici) avrà immediata risposta automatica di conferma ricezione. Il messaggio di risposta verrà mostrato sotto quello ricevuto in 'Texts ricevuti/trasmessi'.
### Checkbox 'Genera csv file'
Già descritta sotto 'Tab Messaggi'
### Progress bar ChUtil e AirUtilTXx10
Ogni messaggio Telemetry trasmesso dal nostro router_client contenete valori di ChanUtil e AirUtilTX viene intercettato per riprodurre sulle rispettive progress bar i relativi valori percentuali. ChanUtil è arrotondato all'unità nella progress bar come pure AirUtilTx moltiplicato per 10. 

Le barre sono rappresentate con 3 colori possibili: 
1. verde per ChanUtil e AirUtilTx < 51 (51 - 5.1)
2. giallo per ChanUtil fra 51 e 75 e AirUtilTx fra 51 e 99 (9.9)
3. rosso per ChanUtil > 75 e AirUtilTx = 100 (10.0)

Com'è noto se AirUtilTX raggiunge il 10% l'unità che ha registrato questo valore non trasmette più e avere quindi sotto mano la situazione presso i vari router può dare un'idea dell'affidabilità della consegna dei messaggi in rete. Avere impostato tutti i devices in MEDIUM_FAST al posto del precedente LONG_FAST ha sensibilmente migliorato la situazione generale, per quanto ho però constatato, il 10% viene ancora a volte raggiunto dal mio GW mentre ciò apparentemente non capita con tutti gli altri nel mesh.

E' questo un argomento sul quale sto indagando anche perché vedo che il mio GW invia messaggi di Telemetry ogni minuto con grande precisione senza perderne alcuno, mentre questi messaggi non mi giungono dagli altri nodi / router con la stessa cadenza ma apparentemente in modo saltuario.

## Note sul DB meshDB.db
Il DB è costituito da tre tabelle:
Tabella per dati ChanUtil e AirUtilTX
1. CREATE TABLE "airtx" (
	"data"	TEXT,
	"ora"	TEXT,
	"nodenum"	INTEGER,
	"longname"	TEXT,
	"chanutil" REAL,
	"airutiltx" REAL
	)
  
Tabella per dati di monitor posizione geografica devices in tempo reale
 2. CREATE TABLE "connessioni" (
	"data"	TEXT,
	"ora"	TEXT,
	"user"	TEXT,
	"alt"	INTEGER,
	"lat"	REAL,
	"lon"	REAL,
	"batt"	INTEGER,
	"snr"	REAL,
	"dist"	REAL,
	"rilev"	REAL,
	"_id"	INTEGER UNIQUE,
	PRIMARY KEY("_id" AUTOINCREMENT)
)

Tabella per registazione dati di ciascun nodo aggiornati nel tempo
3. CREATE TABLE "meshnodes" (
	"data"	TEXT,
	"ora"	TEXT,
	"nodenum"	INTEGER UNIQUE PRIMARY KEY,
	"longname"	TEXT,
	"alt"	INTEGER,
	"lat"	REAL,
	"lon"	REAL,
	"batt"	INTEGER,
	"snr"	REAL,
	"dist"	REAL,
	"rilev"	REAL,
	"chanutil" REAL,
	"airutiltx" REAL,
	"pressione" REAL,
	"temperat" REAL,
	"umidita" REAL
	)

La tabella connessioni contiene un record per ogni singolo nodo per ogni singola variazione di distanza di oltre 100mt verso il router_client Home. In questo modo è possibile tracciare i percorsi effettuati dai nodi nel tempo.

La tabella meshnodes contiene un singolo record per ciascun nodo identificato da chiave unica non duplicabile costituita dal nodenumber (integer su 4 bytes) attraverso il quale si risale a longname. Ad ogni variazione di dati il relativo record viene aggiornato anche nella data. Questi dati sono la base di riferimento ad ogni ripartenza dell'applicazione consentendoci così di identificare i nodi già dal primo messaggio qualunque sia il tipo di messaggio ricevuto.

I dati vecchi oltre i 7 giorni vengono automaticamente cancellati ad ogni ripartenza in tutt'e tre le tabelle.

## Esempio di vista 'connessioni'
![mesh_data_show_2.png](/mesh_data_show_2.png)

## Esempio di vista 'GeoMap'
![mesh_data_show_3.jpg](/mesh_data_show_3.jpg)
## Note pratiche d'uso
1. Avendo raggiunto un numero di nodi gestiti nel mesh intorno alla trentina capita abbastanza spesso che la connessione seriale al device vada in time-out alla partenza. Questa evenienza è segnalata nella text area log protocollo con le istruzioni atte ad aggirare il problema: staccare e riattaccare la connessione USB, poi lanciare il comando CLI 'meshtastic --info' e ripeterlo fino a che finisca senza errore di time-out. A questo punto rilanciare l'applicazione.

2. Il primo messaggio che normalmente esce dal device è un ADMIN_APP con origine e destinazione pari a node_id dello stesso. E' importante che questo messaggio arrivi nei primi inviati pervhé è per questo tramite che viene identificato il nodenum che è la chiave identificativa di mioGW ovvero il nodo Home. Se il messaggio ADMIN_APP non esce nei primi sette / otto basta al volo un reset per reboot e la cosa si risolve.
