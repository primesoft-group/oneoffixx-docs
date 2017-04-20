---
layout: page
title: Empfängeradresse
permalink: "docfunc/de/df/recipientaddress"
language: de
---

Die Dokumentfunktion ‘Empfängeradresse’ muss einer Vorlage angehängt werden, wenn der Empfängerdialog angezeigt werden soll. Im Konfiguratonsfenster kann der Empfängerdialog auf verschiedene Weisen auf die Lösung massgeschneidert werden. In der Konfiguration verweisen mehrere Links auf den globalen Konfigurationsprovider, wo die Konfiguration der verschiedenen Gruss- und Abschiedsformeln hinterlegt sind. Der genaue Wortlaut und Übersetzungen der Formeln können im globalen Übersetzungsprovider angepasst werden.


## Adressprovider
Adressprovider sind Plugins welche eine Schnittstelle zu einer Adressquelle implementieren. Auf Wunsch werden Adressprovider Kundenspezifisch implementiert. Die Verwendung der Adressprovider ist Lizenzpflichtig.

{:.table .table-striped}
Adressprovider | Beschreibung
------- | -------
AbacusAddressProvider | Ruft die Abacus Webservices Schnittstelle http://www.abacus.ch/abaconnect/2007.10 auf. Da die Schnittstelle wie Indices verwendet werden, empfehlen wir für Abacus direkt auf die SQL DB zuzugreifen.
CobraAddressProvider | Cobra Adress Plus Schnittstelle.
CreativAddressProvider | Adressprovider zum OM von [Creativ](http://www.creativ.ch/)
DynamicsNavisionAddressProvider | Webservice Schnittstelle zu Microsoft Dynamics Navision
EGDVAddressProvider | RUF Schnittstelle 
ExchangeAddressProvider | Adressabfrage direkt auf die Exchange Server API
GenericSqlAddressProvider | 
GoogleMapsAddressProvider | 
LDAPAddressProvider | 
LotusNotesAddressProvider | 
NestAddressProvider | 
OutlookAddressProvider | 
SAPPulsAddressProvider | 
SharepointAddressProvider | 
TelSearchCHAddressProvider | 
UserDefinedAddressProvider | 
VertecAddressProvider | 
ZefixAddressProvider | 
