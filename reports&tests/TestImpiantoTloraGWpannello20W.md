---
title: Test impianto Tlora GW con pannello 20W 
description: Messa in opera di pannello solare 20W per alimentare Tlora GW con supporto batteria Pb da 12V 7Ah e MPPT charge controller
published: true
date: 2023-09-01T14:24:44.424Z
tags: 
editor: markdown
dateCreated: 2023-09-01T14:05:07.953Z
---

## Premessa (by IU2RPO 1 Sett 2023)
L’avventura, di cui questa è un’ennesima puntata, ha già avuto espressione in miei precedenti documenti di cui a:
https://wiki.loraitalia.it/test_batteria2600_pannello_30w.pdf
https://wiki.loraitalia.it/test_tlora2_batt3500mah_ps30w.pdf 
https://wiki.loraitalia.it/test_pannelli_fotovoltaici_con_obiettivo_alimentazione_tlora_gw.pdf
dai quali emergeva una certa difficoltà nell’individuare giusto pannello e giuste batterie per mettere in piedi una stazione Tlora alimentata da pannello solare. 


Il secondo documento qui riportato prevedeva, nelle conclusioni, di allestire un impianto basato su pannello con regolatore di carica per una batteria da 12V 7Ah che a sua volta garantisse la carica della batteria del Tlora alimentato via USB del regolatore stesso.


Il terzo documento valutava l'utilizzo di 3 pannelli che avevo a disposizione e concludeva puntando su quello da 20W opportunamente valutato. 


Il presente documento descrive la messa in opera del pannello con un test valutativo di tutto l'impianto risultante messo alla prova dal 18 Agosto al 31.


## Messa in opera pannello 20W con controller MPPT
L'allestimento provvisorio è tutto meno che elegante e qui lo evidenzio per chi ha il gusto dell'orrido:
![impianto_panel_20w.jpg](/impianto_panel_20w.jpg)
Il pannello da 20W è montato su base di compensato da 4mm. Si notino l'antenna del Tlora provvisoriamente montata su questa base e i cavetti d'uscita del pannello solare che sono cablati sul retro.
![impianto_panel20w_retro.jpg](/impianto_panel20w_retro.jpg)
Si notino in basso la batteria da 12V 7Ah, in alto il controller MPPT e la scatola rossa contenente il Tlora2 oltre ai collegamenti pannello-MPPT, batteria-MPPT, alimentazione del Tlora2 via uscita USB del controller MPPT.


Questo insieme l'ho messo alla prova nei giorni fra il 18 e il 31 Agosto per lo più in condizioni di tempo sereno a parte il 26 e il 27 Agosto giornate di cielo coperto con pioggia anche forte e le giornate seguenti fino al 31 Agosto tutte molto nuvolose.


## Controllo delle prestazioni
L'obiettivo del controllo è verificare la tenuta in carica della batteria da 12V 7Ah che è il cuore del supporto all'alimentazione del Tlora2-1.1.6 che in verità potrebbe fare a meno della sua batteria Li-Ion da 3500mAh perché l'alimentazione su porta USB la fornisce di suo il controller MPPT. La batteria interna al Tlora2 la lasciamo per prolungargli la vita nel caso andasse sotto limite minimo (10.5V) la batteria Pb da 12V (se la tensione scende sotto i 10.5V il controller ferma il carico sulla batteria 'spegnendo' anche l'uscita di 5V sulle 2 USB).

Il Tlora2 è montato su una breadboard a 400 fori in modo da poter collegare batteria, controller ambientale BM280, controller corrente/tensione INA219 agevolmente come si vede nelle foto. La configurazione dei 2 controller è su interfaccia I2C, lo INA219 tiene sotto monitor sia la tensione della batteria da 12V che la corrente in entrata (carica) o in uscita (scarica - alimentazione Tlora2). 


Questi valori sono trasmessi dal protocollo Meshtastic - Telemetry ogni 10 minuti via radio al mesh e ogni minuto via BT alla App Android collegata. L'analisi di questi dati, nel corso della giornata per diversi giorni di seguito, danno la prospettiva del bilancio energetico carica - consumi che dovrà tenere la batteria sempre a tensione intorno ai 12V.

Nell'osservare le correnti in gioco e le variazioni di tensione della batteria Pb, teniamo presente che il Tlora2 qui configurato assorbe in ricezione circa 50mA che arrivano a 180-200mA in trasmissione e che la normale frequenza di trasmissione di protocollo / ora è di 6 Telemetry + 4 Position + 1 NodeInfo oltre a eventuali messaggi di text sollecitati dall'operatore.

Lo MPPT a sua volta assorbe circa 20mA di suo che si aggiungono ai 50mA su 5V del Tlora sicché in assenza di supporto dal pannello solare per mancanza di luce, la batteria si scaricherebbe in meno di 100 ore ovvero 4gg. Vedremo quest'inverno come sarà in pratica.

## Posizionamento del pannello durante le misure
Il pannello è stato posizionato sul balcone esposto a EST la cui insolazione è garantita, nel mese di Agosto, dalle 07:00 alle 11:30 dopo di che resta solo la luce diurna fino al tramonto intorno alle 19:30. Tutte le misure riportate sono riferite a questa condizione.

L'inizio dei test è stato il 18 Agosto alle ore 07:00 con batteria carica a 12.5V e le ultime misure sono del 31 Agosto sera con batteria a 12.3V. In 14 giorni di operatività la batteria è rimasta in equilibrio mantenendo operativo il Tlora2 (poi Tlora1-V1) per tutto il tempo.
## Esempio di comportamento sotto il sole
Il 18 Agosto, con cielo sereno dalle 10:30 alle 22:52 sotto sole sia la mattina che il pomeriggio:
![panel20w_1808_voltage.jpg](/panel20w_1808_voltage.jpg)![pannello20w_1808_current.jpg](/pannello20w_1808_current.jpg)
Questo è un esempio del comportamento in pieno sole dove si nota che il controller identifica  rapidamente il raggiungimento della tensione di blocco carica di 14.2V ma INA219 sul Tlora vede ancora valori fino a 18-20V sebbene la corrispondente corrente sia vicina a 0mA. Sul controller l'animazione di carica batteria è bloccata e mi aspettavo di vedere quindi il vero valore di tensione della batteria intorno a 14V, invece vedo la tensione che il pannello pare fornire ancora a dispetto del blocco.

E' vero che la corrente è prossima allo 0 ma non so se in queste condizione la batteria possa soffrire danni. In questi momenti si nota anche che i valori di tensione misurati da INA219 sono molto ballerini passando anche da 15 a 10V. Dopo un po' ovvero quando l'insolazione cala (vedi intorno alle 19) tutto sembra tornare normale.  Non ho capito se questo è un comportamento giusto oppure c'è qualche difetto nel controller MPPT. Vedrò cosa succede con un PWM al posto del MPPT.

### 20 Agosto
![panel20w_2008_voltage.jpg](/panel20w_2008_voltage.jpg)![panel20w_2008_corrente.jpg](/panel20w_2008_corrente.jpg)
Anche la campionatura del 20 Agosto mostra che raggiunta la soglia di 14.2V sulla batteria, il controller ferma la carica ma INA219 misura valori di tensione fra 15 e 20V come se il blocco fosse inefficace. I valori di corrente di carica , superati i 15V sono intorno allo 0 come già visto. Qui però si nota anche carica di 700mA circa in corrispondenza a 15V. Mi rimane il dubbio che il controller mal gestisca la sovratensione in carica. A fine giornata il livello batteria è intorno al valore di inizio giornata.

### 27 Agosto
Giornata con cielo coperto al 100% e pioggia per tutto il tempo. Qualche giorno fa si è rotta la radio del Tlora2 e ora funziona solo il BT e i dati di Telemetry li posso solo prendere a mano leggendoli sulla App Android. Mostro allora solo alcune campionature nella giornata con i seguenti risultati:
	1. 07:00 11.90V
	2. 12:00 12.50V 
	3. 16:40 12.45V
	4. 17:40 12.27V
	5. 19:10 12.18V
	6. 20:15 12.12V
	7. 22:10 12.08V

Le correnti di carica vanno da 20 a 50mA, quelle di consumo in media 42mA. Esposizione del pannello verso EST per tutto il tempo.

### 28 Agosto
Giornata con cielo molto nuvoloso inizialmente coperto a EST (verso cui il pannello è rivolto). Qualche sprazzo di sole fra la 9:30 e le 9:45 dove il pannello risponde con tensione di 14V su batteria e carica da 800mA a 1060mA. Poi il cielo si scurisce ancora di più e alle 11:00 piove a dirotto con cielo plumbeo. Anche smessa la pioggia, per tutto il pomeriggio cielo coperto al 100%.

06:30 11.86V consumo 41.8mA
07:00 12.00V consumo 41.0mA
12:20 12.38V carica  16.0mA
12:30 12.46V carica  32.7mA
14:15 12.75V carica  81.7mA
14:35 12.61V carica  30.2mA
15:05 12.65V carica  50.3mA
15:40 12.61V carica  34.2mA
16:00 12.59V carica  37.0mA
16:40 12.40V consumo 11.2mA
17:10 12.39V consumo  5.7mA
17:50 12.24V consumo 35.2mA
18:25 12.22V consumo 37.9mA
19:10 12.20V consumo 40.5mA
20:15 12.14V consumo 43.5mA
21:05 12.14V consumo 43.6mA
21:45 12.12V consumo 43.4mA
22:15 12.11V consumo 43.2mA
22:35 12.09V consumo 43.3mA

### 29 Agosto
Cielo nuvoloso / coperto la mattina a EST.

06:45 11.97V consumo 44.1mA
07:05 11.99V consumo 35.6mA
07:30 12.02V consumo 29.1mA
08:05 12.22V carica  16.5mA
09:15 12.65V carica  99.9mA
09:20 12.92V carica 192.1mA
09:30 15.42V carica 791.3mA  sprazzo di sole, 14.2V su disp.MPPT e carica boccata, giro panel in ombra verso cielo per proteggere batteria da sovraccarica visto che anche con MPPT bloccato la tensione verso la batteria è > 15V
09:45 12.74V carica 122.4mA
09:50 13.15V carica 319.5mA
10:35 13.16V carica 276.8mA
10:50 13.12V carica 236.1mA
11:30 12.42V consumo  6.3mA cielo coperto sole sparito, rigiro il pannello verso il sole
11:35 12.60V carica  63.0mA
12:00 12.67V carica  70.6mA
12:45 12.72V carica  82.1mA
13:00 12.74V carica  82.4mA
13:15 12.78V carica  91.3mA
13:30 12.79V carica  90.1mA
13:55 12.65V carica  42.3mA
14:55 12.71V carica  66.0mA
15:40 12.68V carica  48.7mA
16:00 12.60V carica  25.7mA
16:55 12.45V consumo  6.0mA
17:30 12.47V carica  10.1mA
18:05 12.34V consumo 19.3mA
20:00 12.19V consumo 76.6mA
20:30 12.21V consumo 45.5mA
22:00 12.19V consumo 45.9mA

### 30 Agosto
Cielo coperto, poi si schiarisce a sprazzi e allora giro pannello fuori da insolazione diretta per non sovraccaricare la batteria. Avendo ripristinato, con un Tlora1-v1 la stazione alimentata dal pannello solare, ora ricevo i dati di telemetry via radio sul GW collegato al PC e quindi posso riprendere nuovamente le campionature ogni 10 minuti nel DB Sqlite3 per poi creare i grafici seguenti.

Alle 06:40 abbiamo 11.94V consumo 44.2mA. Poi sostituito il Tlora2 difettoso con un Tlora1-v1 vado ad accumulare dati in Sqlite3 DB iniziando alle ore 09:37.
![30agostotensione.jpg](/30agostotensione.jpg)
![30agostocorrente.jpg](/30agostocorrente.jpg)
![30agostobilancio.jpg](/30agostobilancio.jpg)
Il calcolo del bilancio energetico nel corso della giornata, ovvero i mAh consumati o ricevuti in carica cumulativa, è calcolato sommando algebricamente i valori di mA consumati o caricati per ciascuno slot di 10 minuti (campionatura Telemetry) ovvero corrente slot in mA/6 = mAh dato che 10 minuti sono 1/6 di ora.

Come si vede da questo grafico il bilancio energetico del 30 Agosto è positivo ovvero a fine giornata abbiamo un accumulo di circa 400mAh in più del valore di carica a inizio giornata. 

Questi 400mAh saranno spesi durante la notte in circa 8 ore dato che il Tlora1-V1 configurato consuma circa 60mA su 5V che sommati al consumo del controller fanno circa 50mA su 12V (visto sperimentalmente) il che porta a concludere che la batteria a 12V resterà sempre carica come di fatto è stato sin da inizio test ovvero dal 18 Agosto al 30.

### 31 Agosto
Anche oggi si ripete la giornata di ieri con cielo molto nuvoloso / coperto con sole a sprazzi nella mattinata. Il pannello solare è rivolto a EST e così resta per tutta la giornata.

![31agostotensione.jpg](/31agostotensione.jpg)
![31agostocorrente.jpg](/31agostocorrente.jpg)
![31agostobilancio.jpg](/31agostobilancio.jpg)
La mattina del 1°Settembre la tensione di batteria alle ore 06:30 era di 12.10V quindi le 8 ore notturne dalle 22:30 hanno comportato un abbassamento di circa 200mV da 12.3V a 12.10V che corrispondono al consumo di circa 50mA per 8 ore = 400mAh.

## Conclusioni
1. La prima conclusione riguarda la scelta del pannello da 20W (costo 19.76€ compresa spedizione) perfettamente rispondente alle aspettative a: https://www.amazon.it/Pannello-Fotovoltaico-Energia-Coccodrillo-campeggio/dp/B0BL7KPC9B/ref=sr_1_2?__mk_it_IT=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=NO3YNL2JJUG3&keywords=YASTA+pannello+solare+20W&qid=1693558931&sprefix=yasta+pannello+solare+20w%2Caps%2C140&sr=8-2
2. La resa dell'impianto nel test di 14 giorni è risultata soddisfacente anche col cielo coperto o con pannello non esposto direttamente al sole (esposizione a EST con sole visibile dalle 07:00 alle 11:30).
3. L'unico appunto riguarda il comportamento del controller MPPT (preso su Aliexpress per 15€, è un Javpoo solar charger da 60A) che sembra rispondere bene, sul display, bloccando la carica quando la batteria è sottoposta a oltre 14.2V. Inopinatamente lo INA219 configurato nel Tlora per misurare tensione di batteria e corrente di carica / consumo continua a misurare tensione fra 16V e 21V anche se la corrente che circola non supera 1mA. Questa situazione, in pieno sole agostano, si raggiunge nel giro di 10 minuti, non so a questo punto se ciò possa davvero danneggiare la batteria quindi nei test ho evitato l'esposizione diretta al sole quando la soglia dei 14.2V veniva raggiunta. Anche senza esposizione diretta la corrente di carica si attesta comunque sui 300mA (in esposizione diretta arrivava invece anche a oltre 1A).

Il tutto lascia ben sperare per un responso positivo anche nella stagione autunnale e invernale. Starò a vedere.







