---
layout: page
title: TelSearchCHAddressProvider
permalink: "docfunc/de/df/ap/telsearch"
language: de
---

OneOffixx stellt den TelSearch Adressprovider zur Verfügung. Der Service wird von TelSearch.ch gratis zur Verfügung gestellt. Der Key für tel.search.ch ist auf 1000 Adressen pro Tag limitiert (hier zählt jeder Suchtreffer). Pro Mailadress-Domain ist nur ein Key möglich. Der erforderliche Key kann auf der Seite [telsearch API Key](http://admin.tel.search.ch/api/getkey) (Grund OneOffixx angeben) bezogen werden. 

Mehrere Keys können kombiniert werden um die Limite zu erhöhen.

```xml
<AddressProvider id="D66AA3D8-B184-4AED-BE93-6AA86FA1867E" order="1" active="true">
  <!-- TelSearch api key -->
  <ApiKey>{telsearch API Key}</ApiKey>
</AddressProvider>
```


```xml
<AddressProvider id="D66AA3D8-B184-4AED-BE93-6AA86FA1867E" order="1" active="true">
  <!-- Multiple TelSearch api key -->
  <ApiKey>{telsearch API Key1}</ApiKey>
  <ApiKey>{telsearch API Key2}</ApiKey>
  <ApiKey>{telsearch API Key3}</ApiKey>
  <ApiKey>{telsearch API Key4}</ApiKey>
</AddressProvider>
```
