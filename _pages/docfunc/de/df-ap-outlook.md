---
layout: page
title: OutlookAddressProvider
permalink: "docfunc/de/df/ap/outlook"
language: de
---

Adressprovider für Outlook 2010/2013 und 2017. Der Zugriff via Interop wird von Office gesperrt, wenn kein Virusscanner installiert ist, welcher die Office Schnittstelle unterstützt. 

![]({{ site.baseurl }}/assets/content-images/docfunc/de/objectModelGuard.png)

Um dieses Problem zu umgehen steht im OneOffixx Programmverzeichnis die Registry Datei _C:\Program Files (x86)\OneOffixx\ObjectModelGuard-2010.reg_ zur Vergügung. Damit kann der Dialog deaktiviert werden.

```xml
<AddressProvider id="A244D5EF-93F6-4A2C-9B62-F6DA64590B8C" order="0" active="true">
  <AllowPublicAddressbooks>true</AllowPublicAddressbooks>
  <WhitelistedAddressbooks>
    <Name>Kontakte</Name>
    <Name>Globale Adressliste</Name>
    <Name>All Rooms</Name>
    <Name>Kontakte Sevitec</Name>
  </WhitelistedAddressbooks>
  <SelectedAddressbook>
    <Name>Kontakte</Name>
  </SelectedAddressbook>
</AddressProvider>
```

* __AllowPublicAddressbooks__ true => Öffentliche Adressbücher werden angeigt.
<span class="label label-info">NEU ab 2.3.50030</span>
* __WhitelistedAddressbooks__ Liste aller Adressbücher die zur Auswahl gestellt werden sollen.
* __SelectedAddressbook__ Dieses Adressbuch wird ber Default angezeigt.
