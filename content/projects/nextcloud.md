---
title: Nextcloud AIO
draft: false
summary: Lokale Cloudlösung
---
## Problem

Ich möchte eine Möglichkeit, unter anderem, meine Dateien, Kalender und
ToDo-List auf allen meinen Geräten verfügbar zu haben und ggf. zu
synchronisieren. Cloudlösungen bieten das auch an, jedoch zu begrenzter
Kapazität, oder laufenden Abonnement-Kosten.

## Lösung

Selfhosted Nextcloud-Instanz in einem Dockercontainer. Zur Härtung der Sicherheit
ist der Zugang bewusst nur im lokalen Netz verfügbar. Sobald ich mein Heimnetz
verlasse, verbinde ich mich via WireGuard ins Heimnetz.

## Umsetzung

### Installation

Das Containerpaket Nextcloud AIO wird über Docker installiert. Da ich es
lokal betreiben möchte und nur nach Bedarf über VPN erreichbar sein soll,
installiere ich wie in der [offiziellen Dokumentation](https://github.com/nextcloud/all-in-one#how-can-i-access-nextcloud-locally)
beschrieben und setze die Domäne via [AdGuards](/projects/adguardhome) DNS-Rewrite
auf die lokale IP-Adresse des Apache Reverse Proxys.

#### Docker Compose File

```yaml
name: nextcloud-aio
services:
  nextcloud-aio-mastercontainer:
    image: ghcr.io/nextcloud-releases/all-in-one:latest
    init: true
    restart: always
    container_name: nextcloud-aio-mastercontainer
    volumes:
      - nextcloud_aio_mastercontainer:/mnt/docker-aio-config
      - /var/run/docker.sock:/var/run/docker.sock:ro
    ports:
      - "8080:8080/tcp"
    env_file:
      - .env
volumes:
  nextcloud_aio_mastercontainer:
    name: nextcloud_aio_mastercontainer
networks:
  nextcloud-aio:
    name: nextcloud-aio
    driver: bridge
```

### Synchronisation

#### Geräte im Heimnetz

Über die angebotene Clientsoftware lässt sich zügig eine Verbindung aufbauen.
Eine Ordnersynchronisation lässt sich dann ebenfalls einrichten.

#### Mobile Geräte

Neben der offiziellen App muss man hier noch zusätzlich WireGuard einrichten,
sodass eine Verbindung hergestellt werden kann.

## Fazit

Bei Cloudanbietern lassen sich vermutlich mit weniger Reibung gewisse Dienste
und Services integrieren; ich denke hier speziell an Google Calendar auf
Android Mobilgeräten. Dennoch konnte es allen Anforderung sehr gut nachkommen.
