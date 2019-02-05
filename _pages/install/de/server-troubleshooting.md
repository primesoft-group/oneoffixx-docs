---
layout: page
title: Troubleshooting
permalink: "install/de/server-troubleshooting/"
language: de
---

## Authentifizierung im Dashboard funktioniert nicht  

__Beschreibung__ 

Das Dashboard wurde eingerichtet und für AD-Rollen und Benutzer so oder ähnlich zugelassen:

```
<authorization>
    <allow roles="domainname\USERGROUP"/>
    <allow users="domainname\user1,domainname\user2,domainname\user3"/>
    <deny users="*"/>
</authorization>
```

Obwohl der Benutzer aufgelistet oder Mitglied der Gruppe ist, erscheint immer das Login-Fenster und danach ein HTTP-401-Fehler. Der Fehler tritt auch auf, wenn von ausserhalb auf die Maschine zugegriffen wird (nicht via localhost).


__Mögliche Lösungen__ 

1) Prüfen Sie, ob im IIS die 'Windows-Authentifizierung' aktiviert ist.

2) Falls Sie mit DNS-Einträgen arbeiten, prüfen Sie mit nslookup, ob die Domain und die IP übereinstimmen (in beide Richtungen).

3) Falls Sie mit SSL-Zertifikaten arbeiten, überprüfen Sie, ob die Bindings in IIS korrekt eingestellt sind.

4) Wenn alles obige stimmt, kann es trotzdem sein, dass durch Einträge in der Hosts-Datei das ___Name Checking___ nicht korrekt funktioniert. DAs kann folgendermassen deaktiviert werden (Neustart erforderlich):

```
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\lanmanserver\parameters]
"DisableStrictNameChecking"=dword:00000001
```
5) Der IIS beinhaltet ein Feature zur Verhinderung von Reflection Attacks. Dieses verhindert, dass vom Host selbst auf eine Seite zugegriffen werden kann. Es kann folgendermassen deaktiviert werden (Neustart erforderlich):

```
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa]
"DisableLoopbackCheck"=dword:00000001
```