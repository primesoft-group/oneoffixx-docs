---
layout: page
title: TelSearchCHAddressProvider
permalink: "docfunc/de/df/ap/telsearch"
language: de
---

OneOffixx stellt den TelSearch Adressprovider zur Verfügung. Der Service wird von TelSearch.ch gratis zur Verfügung gestellt. Der Key für tel.search.ch ist auf 1000 Adressen pro Tag limitiert (hier zählt jeder Suchtreffer) pro Mailadress-Domain ist nur ein Key möglich. Ein Key kann auf der Seite http://admin.tel.search.ch/api/getkey (Grund OneOffixx angeben) bezogen werden. 

```xml
<AddressProvider id="D66AA3D8-B184-4AED-BE93-6AA86FA1867E" order="1" active="true">
  <!-- TelSearch api key -->
  <ApiKey>[telsearch API Key](http://admin.tel.search.ch/api/getkey)</ApiKey>
</AddressProvider>
```