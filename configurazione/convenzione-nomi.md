---
title: Convenzione del nome dei nodi
description: 
published: true
date: 2023-02-16T17:39:31.356Z
tags: 
editor: markdown
dateCreated: 2023-02-16T16:55:00.384Z
---

Per dare uno standard e aiutare gli utenti a entrare nel sistema abbiamo valutato che alcune informazioni debbano essere facilmente discernibili.

Purtroppo il protocollo attuale non dispone di tutte queste informazioni dobbiamo quindi poterle dedurre dal nome dei nodi stessi.

![namingconvention.jpg](/namingconvention.jpg)

É disponibile un **[Validatore](https://map.loraitalia.it/?page=validator)** per verificare la corretta semantica del nome nodo

## Nome nodo
Il nome nodo deve essere composto da caratteri alfanumerici, è consentito il solo carattere speciale "-".

```regexp
([A-Za-z0-9]+)
```

## Campo Gateway
Il campo è obbligatorio per permettere il riconoscimento dei nodi gateway

```regexp
(GW)
```

## Campo Frequency
Il campo è obbligatorio per nodi fissi e gateway per permettere di identificare la frequenza su cui operano i nodi già presenti un una zona.

```regexp
(433|868)
```

## Campo UID
Il campo è obbligatorio per i nodi mobili in modo da garantire l'unicità del nodo anche in presenza di molti nodi mobili

```regexp
([A-Fa-f0-9]{4})
```