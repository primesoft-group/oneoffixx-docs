---
layout: page
title: AddressPlus (Cobra)
permalink: "docfunc/de/df/addressplus"
language: de
---

Diese Dokument-Funktion wird benötigt, um aus Cobra heraus Dokumente in OneOffixx zu erstellen.

__Konfiguration:__
```xml
<?xml version="1.0"?>
<AdressPlusConfiguration>

  <!-- Salutation configuration -->
  {[Recipients.SalutationConfiguration]}

  <!-- Letter salutation configuration -->
  {[Recipients.LetterSalutationConfiguration]}
  
  <!-- Greeting formula configuration -->
  {[Recipients.GreetingFormulaConfiguration]}
  
</AdressPlusConfiguration>
```