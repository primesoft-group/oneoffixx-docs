---
layout: page
title: StaticSyncSource
permalink: "install/de/sync/sync-static"
language: de
---

## StaticSyncSource

Just return "static" properties or claims for each "pipeline" request

```xml
<StaticSyncSource name="Static">
    <Property name="test1">helloworld</Property>
    <Property name="test2">helloworld2</Property>
    <Claims>
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/test">WERT!</Claim>
    </Claims>
  </StaticSyncSource>
```