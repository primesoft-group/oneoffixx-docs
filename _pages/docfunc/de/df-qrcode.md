---
layout: page
title: QR-Code
permalink: "docfunc/de/df/qrcode"
language: de
---

Diese Dokument-Funktion ermöglicht das Erstellen von diversen Bar- und QR-Codes.

__Konfiguration:__
```xml
<Configuration>
  <QrCode id="StatischerQrCode" format="QR_CODE" type="text">Wert</QrCode>
</Configuration>
```

**Hinweise**
* Da ein QR-Code nicht leer sein kann, wird im Falle eines leeren Inhalt der Text "kein Inhalt" gesetzt.
* Bei vCards ist Vorsicht geboten, da schon bei kleinen Abstände oder nicht einhalten von Vorgaben Handyreader den QR-Code nicht lesen können.

## Attribute

**id**: Name Im Designer. Mit einem Punkt können Ordner erstellt werden (z.B. Ordner.QrCodeName) 

**type**: Typ des QR-Codes

*Mögliche Werte:*

{:.table .table-striped}
| Wert | Beschreibung | 
| ---- | ------------ | 
| text | Statischer Text, wird nicht verändert |
| data | Ein OneOffixx-Daten-Element, wie z.B. der Profilname oder die Firmenwebseite |
| dynamic | Statischer Text gemischt mit OneOffixx-Daten-Elementen. |

**height**: Höhe des QR-Codes. Das Attribut ist optional. Wenn es nicht angegeben wird, wird als Standard 100px genommen. 

**format**: Format des QR-Codes. Es findet keine Prüfung statt, ob der Wert in *value* überhaupt Platz in diesem Format hat.

*Mögliche Werte:*

{:.table .table-striped}
| Wert | Einschärnkungen | 
| ---- | ------------ | 
| AZTEC | |
| CODABAR | |
| CODE_39 | Nur Zahlen möglich |
| CODE_93 | Nur Zahlen möglich |
| CODE_128 | Nur Zahlen möglich |
| DATA_MATRIX | |
| EAN_8 | |
| EAN_13 | |
| ITF | |
| PDF_417 | |
| QR_CODE | |
| RSS_14 | |
| RSS_EXPANDED | |
| UPC_A | |
| UPC_E | |
| All_1D | |
| UPC_EAN_EXTENSION | |
| MSI | |
| PLESSEY | |


## Beispiele

Mit statischem Inhalt:
```xml
<QRCode id="StatischerQrCode" type="text">Dies ist ein statischer Text</QRCode>
<QRCode id="WLANQrCode" type="text">WIFI:S:ssidName;T:WAP2;P:password;;</QRCode>
```

Mit OneOffixx-Daten:
```xml
<QRCode id="OneOffixxDatenPerID" type="data">Profile.User.LastName</QRCode>
<QRCode id="OneOffixxDatenPerXPath" type="data">{*//Text[@id='Profile.User.LastName']}</QRCode>
```

Als dynamischer Code:
```xml
<QRCode id="TextMitDaten" type="dynamic">Hallo mein Name ist {Profile.User.FirstName} {Profile.User.LastName}</QRCode>
<QRCode id="vCard" height="300" type="dynamic">BEGIN:VCARD
	VERSION:3.0
	N:{Profile.User.LastName};{Profile.User.FirstName}
	FN:{Profile.User.FirstName} {Profile.User.LastName}
	ORG:{Profile.Org.Title}
	TITLE:{Profile.User.Title}
	TEL;TYPE=WORK,VOICE:{Profile.User.Phone}
	TEL;TYPE=HOME,VOICE:{Profile.User.Phone2}
	ADR;TYPE=WORK:;;{Profile.Org.Postal.Street};{Profile.Org.Postal.City};;{Profile.Org.Postal.Zip};{Profile.Org.Postal.Country}
	EMAIL;TYPE=PREF,INTERNET:{Profile.User.Email}
	URL:{Profile.Org.Web}
	REV:2015-03-31T08:30:10Z
	END:VCARD
</QRCode>
```

