---
layout: page
title: Vorlagenverteilung
permalink: "docfunc/de/df/templatedistribution"
language: de
---

Mit der Dokumentfunktion "Vorlagenverteilung" können verschiedene Objekte verteilt werden. Diese könnten beispielsweise extentions für Excel oder PowerPoint sein.

Unter dem `Path` Tag kann der Ablageort der Datei gewählt werden. 

Mit dem `Lockfile` kann verhindert werden, dass eine geöffnete Datei verändert wird. Dazu kann ganz einfach das betroffene File samt Endung angegeben werden.

Mit Hilfe des `Merge` Tags kann festgelegt werden, ob die Datei(en) ersetzt, entfernt oder zusammengeführt werden soll(en).

Die Standardkonfiguration sieht wie folgt aus:


```xml
<Configuration>
  <!-- This module distributes the content of the underlying "Document". This behaviour can be changed with:
      <Configuration SourceTemplateDocumentType="NuGet"> or <Configuration SourceTemplateDocumentType="Zip">
   -->
  
  <!-- Deployment Path for UpdateMode: Merge, Replace, Remove. (Normalisiert wie zum Beispiel "%APPDATA%\ActPlus\PowerPoint"-->
  <Path>%APPDATA%\SubFolder\</Path>
  <!--Test Retry File for UpdateMode: Merge, Replace, Remove (welches File soll geprüft werden. Wenn zum Beispiel das File PPAM überschrieben werden kann, dann ist sicher kein PowerPoint geöffnet. Dann das komplette Verzeichnis löschen und neu importieren.-->
  <LockFile>Beispiel_xyz.ppam</LockFile>
  
  <!--
    Merge, Replace or Remove, (InstallFonts, RemoveFonts) 
    "Advanced File Mode": viafiles
  -->
  <UpdateMode>Merge</UpdateMode>

  <!--
  <Files>
    <File Source="*.*" Target="%APPDATA%\SubFolder\SubSubFolder" />
    <File Source="Content" Target="%APPDATA%\SubFolder\SubSubFolder" />
    <File Source="Content/*.*" Target="%APPDATA%\SubFolder\SubSubFolder\" />
    <File Source="Content/*.txt" Target="%APPDATA%\SubFolder\SubSubFolder\test.txt" />
    <File Source="Content/test.txt" Target="%APPDATA%\SubFolder\SubSubFolder" />
    <File Source="Content/test.txt" Target="%APPDATA%\SubFolder\SubSubFolder\test.txt" />
    
    <File Target="%APPDATA%\SubFolder\SubSubFolder\test.txt">
      Hello World!
    </File>
  </Files>
  -->

  <!-- Installiert einen Verknüpfungsdatei auf LockFile im folgenden Verzeichnis. Eintrag löschen wenn kein Shortcut erstellt werden soll. Für EXCEL AddIns notwendig -->
  <!-- <Shortcut>%APPDATA%\Microsoft\Excel\XLSTART\</Shortcut> -->
  <Registry>
    <!-- 
        Root          = "HKCU" 
        Action        = "createAndUpdate" | "create" | "update" | "remove"
        
        Type (case sensitive!) :
        Unknown       = An unsupported registry data type.
        String        = A null-terminated string. This value is equivalent to the Win32 API registry data type REG_SZ.
        ExpandString  = A null-terminated string that contains unexpanded references to environment variables, such as %PATH%, that are expanded when the value is retrieved.
                        This value is equivalent to the Win32 API registry data type REG_EXPAND_SZ.
        Binary        = Binary data in any form. This value is equivalent to the Win32 API registry data type REG_BINARY.
        DWord         = An array of null-terminated strings, terminated by two null characters. This value is equivalent to the Win32 API registry data type REG_MULTI_SZ.
        MultiString   = An array of null-terminated strings, terminated by two null characters. This value is equivalent to the Win32 API registry data type REG_MULTI_SZ.
        QWord         = A 64-bit binary number. This value is equivalent to the Win32 API registry data type REG_QWORD.
        
        Expand        = "true" (expand references to environments variables) false = do nothing

      sample:
      <RegistryKey Root="HKCU" Key="Software\Microsoft\Office\14.0\PowerPoint\AddIns\ACTplus" Action="createAndUpdate" >
        <RegistryValue Type="String" Name="Path" Expand="true">%APPDATA%\ACTplus\PowerPoint\Beispiel_xyz.ppam</RegistryValue>
        <RegistryValue Type="DWord" Name="AutoLoad">00000001</RegistryValue>
      </RegistryKey>   
      
      or
      
      <RegistryFile ImportInKey="HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\...">Content/deploy.reg</RegistryFile>
      <RegistryFile>deploy.reg</RegistryFile>
    -->
  </Registry>
</Configuration>

<!--

Sample Config for Outlook Theme Distribution:

<?xml version="1.0" encoding="utf-8" ?>
<Configuration SourceTemplateDocumentType="Zip">
  <UpdateMode>ViaFiles</UpdateMode>
  <Files>
    <File Source="*.dotx" Target="%APPDATA%\Microsoft\QuickStyles\DemoStyle.dotx" />
    <File Target="%APPDATA%\Microsoft\QuickStyles\OneOffixxTheme.config">DemoStyle</File>
  </Files>
  <Registry>
    <RegistryFile>mailsettings.reg</RegistryFile>
  </Registry>
</Configuration>
-->
```