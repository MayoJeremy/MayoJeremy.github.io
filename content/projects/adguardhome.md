---
title: "AdGuardHome"
draft: false
---

[Home](/) | [Über mich](/private/me) | [Projekte](/projects/project_overview)

## Problem

Im Web sammeln im Hintergrund ununterbrochen Tracker, Telemetriedienste und
Werbenetzwerke Daten über Nutzungsverhalten. Dadurch wird nicht nur die
persönliche Privatsphäre auf jedem Gerät des Heimnetzwerks beeinträchtigt,
sondern auch ein unnötiger Datenballast verursacht. Zudem erhöht es die
Sicherheit, bekannte Malware- und Phishing-Domains auch auf DNS-Ebene zu
blockieren.

## Lösung

Ich kann mithilfe eines lokalen DNS-Servers mit übersichtlichem Dashboard
im Browser einsehen, wie gut die Filterung funktioniert,
Filterlisten einpflegen, habe eine einfache Möglichkeit DNS rewrites anzulegen und,
falls gewünscht, den Upstream-DNS auszuwählen.

## Umsetzung

### Installation

Mithilfe des [offiziellen Dockerimages](https://hub.docker.com/r/adguard/adguardhome)
als [Dockercontainer](/projects/docker) installiert. Als Deploymentmethode
habe ich Docker Compose verwendet.

### Konfiguration

#### Netzwerkeinstellungen

Ich nutze den DHCP-Service meiner FritzBox und habe in den DHCP-Einstellungen netzwerkweit
meine HomeserverIP als DNS-Server eingetragen.

#### Reverseproxy

##### DNS-Rewrite

Damit ich für meine verschiedenen Services passende Subdomains anlegen kann,
habe ich einen DNS-Rewrite angelegt, der sicherstellt, dass mein lokaler
_servername_ auch auf den lokalen Server bzw. dessen Apache-Dienst zeigt.

##### Subdomain

Zur einfacheren Administration habe ich die Weboberfläche über die Subdomain
_AGH.servername.local_ eingebunden. Realisiert durch einen Apache Webserver.

#### Blocklists

[HaGeZi](https://github.com/hagezi/dns-blocklists) hat eine schöne Liste von verschiedenen
Blocklisten die man je nach Bedarf auswählen und importieren kann.
Ich habe mich vorerst für [Multi Pro](https://github.com/hagezi/dns-blocklists#pro)
entschieden um zu sehen wie oft ich manuell nachbessern muss um eine angenehme
Userexperience beizubehalten. Hier konnte ich die Liste auch über das
Webinterface ```Filters -> DNS blocklists -> Add blocklist ->
Choose from the list``` auswählen und aktivieren.

## Fazit

Ich konnte erfolgreich einen großen Teil der Tracker filtern und bin nur selten
auf Websites gestoßen, die durch die Filterung ihre Funktion nicht mehr
vollständig anbieten konnten. Subjektiv wurde auch die Responsiveness mancher
Geräte erhöht.
