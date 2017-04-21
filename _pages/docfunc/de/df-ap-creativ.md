---
layout: page
title: CreativAddressProvider
permalink: "docfunc/de/df/ap/creativ"
language: de
---

Addressprovider zum OM von [Creativ](http://www.creativ.ch/)

```xml
<AddressProvider id="328E6C4E-549B-4108-8ED2-D76B7E422F6B" order="9" active="false" hiddenIfNotAvailable="true">
    <DataType>(sevAddresses|Adresses)(sevAddressesCommon|Common)(sevAddressesCredit|Credit)(sevAddressesLegalProtection|Protection)</DataType>
    <Uri>https://{HOST}/CreativData/CreativData.asmx</Uri>
</AddressProvider>
```

__DataType__ Zeigt eine Auswahlliste an mit allen Objekten die Durchsucht werden können. Die Liste ist eine Key-Value Liste (key1|Anzeigetext1)(key2|Anzeigetext2)
__Uri__ Webserviceschnittstelle