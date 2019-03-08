---
layout: page
title: Dynamics CRM
permalink: "docfunc/de/df/dynamicscrm"
language: de
---

Bietet die Möglichkeit, Dokumente direkt aus Word ins Dynamics CRM hochzuladen.

__Konfiguration:__
```xml
<Configuration>
    <BaseUrl>http://mycrm.local/</BaseUrl>
    <OrganizationName>org</OrganizationName>
    <Annotation>
        <SubjectSource>//Text[@id='DocParam.Subject']</SubjectSource>
        <NoteTextSource>//Text[@id='DocParam.Notes']</NoteTextSource>
        <FileNameSource>//Text[@id='DocParam.FileName']</FileNameSource>
        <ReferenceObjectTypeNameSource>//Value[@key='CRMObject.EntityTypeName']</ReferenceObjectTypeNameSource>
        <ReferenceObjectIdSource>//Value[@key='CRMObject.ID']</ReferenceObjectIdSource>
    </Annotation>
    <ShowDialog>true</ShowDialog>
</Configuration>

```
