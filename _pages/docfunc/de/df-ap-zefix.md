---
layout: page
title: ZefixAddressProvider
permalink: "docfunc/de/df/ap/zefix"
language: de
---

Der [Zefix Webservice](https://www.e-service.admin.ch/wiki/display/openegovdoc/Zefix+Webservice) bietet auf dem täglich nachgeführten Datenstand aller Schweizer Handelsregisterämter aktuellste Informationen zu den in der Schweiz registrierten Firmen. Die SOAP/XML Schnittstelle erlaubt dabei eine nahtlose Integration in bestehende Anwendungen und damit auch eine maschinelle Weiterverarbeitung der geholten Daten.

```xml
<AddressProvider id="AAA2E7F3-9E1E-4F1D-963F-C49C4886EAFD" order="4" active="true">
    <!-- User/password for Zefix web service-->
    <ServiceUser>info@oneoffixx.com</ServiceUser>
    <ServicePassword>{password}</ServicePassword>
    <EnableProxyCredentials>true</EnableProxyCredentials>
</AddressProvider>
```