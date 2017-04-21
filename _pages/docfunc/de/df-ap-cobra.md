---
layout: page
title: CobraAddressProvider
permalink: "docfunc/de/df/ap/cobra"
language: de
---

Cobra Adress Plus Schnittstelle.

```xml
<AddressProvider id="F3D23EE5-F722-4082-842C-1168F7FDF1B8" order="1" active="true">
  <!-- Connection string for cobra database -->
  <ConnectionString>{ConnectionString}</ConnectionString>
  <!-- Query for the Search -->
  <QueryNormal>
			 ('{company}' = '' OR COMPANY1 LIKE '%{company}%' OR COMPANY2 LIKE '%{company}%')
				      AND ('{lastName}' = '' OR LASTNAME0 LIKE '%{lastName}%')
				      AND ('{firstName}' = '' OR FIRSTNAME0 LIKE '%{firstName}%')
				      AND ('{street}' = '' OR STREET0 LIKE '%{street}%' OR STREET1 LIKE '%{street}%')
				      AND ('{plz}' = '' OR ZIP0 LIKE '%{plz}%' OR ZIP0 LIKE '%{plz}%')
				      AND ('{city}' = '' OR CITY0 LIKE '%{city}%' OR CITY0 LIKE '%{city}%')
		    </QueryNormal>
  <QueryCustom>{columnName} like '%{searchText}%'</QueryCustom>
  <QueryPhone>
				MOBILEPHONE0 like '%{phoneNumber}%'
				OR FAX0 like '%{phoneNumber}%'
				OR FAX1 like '%{phoneNumber}%'
				OR PHONE0 like '%{phoneNumber}%'
				OR PHONE1 like '%{phoneNumber}%'
				OR DIRECTPHONE0 like '%{phoneNumber}%'
				OR PRIVATEPHONE0 like '%{phoneNumber}%'
			</QueryPhone>
</AddressProvider>
```