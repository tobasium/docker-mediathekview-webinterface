# docker-mediathekview-webinterface

Fork von [conrad784/docker-mediathekview-webinterface](https://github.com/conrad784/docker-mediathekview-webinterface). Der Container stellt die Desktop-Anwendung MediathekView über die Browseroberfläche von [jlesage/baseimage-gui](https://github.com/jlesage/docker-baseimage-gui) bereit.

## Version

Das Image installiert MediathekView **15.0.0** aus dem offiziellen Linux-Archiv. Das Archiv enthält die benötigte JetBrains Runtime; sie muss nicht separat installiert werden.

**Wichtig:** MediathekView 15.0.0 ist laut [Changelog](https://github.com/mediathekview/MediathekView/blob/master/CHANGELOG.md) nicht rückwärtskompatibel mit älteren MediathekView-Versionen. Sichere vor dem ersten Start mit Version 15 das persistente `/config`-Verzeichnis. Verwende danach nicht dieselbe Konfiguration mit einer älteren Version.

## Container starten

Die Compose-Datei baut das Image lokal und bindet die Konfiguration sowie Downloads aus dem Benutzerverzeichnis ein:

```sh
docker compose up -d --build
```

Die Weboberfläche ist anschließend auf Port `5800` erreichbar. Passe die Pfade in `docker-compose.yml` an deine Umgebung an. Weitere Optionen wie Benutzer-ID und Anzeigeeinstellungen sind in der [Dokumentation von baseimage-gui](https://github.com/jlesage/docker-baseimage-gui#environment-variables) beschrieben.

## Image bauen

```sh
docker build --pull -t mediathekview-webinterface:15.0.0 .
```

Der Workflow `.github/workflows/docker-ghcr.yml` baut bei Pushes auf `master` oder `main` und veröffentlicht `latest` sowie `15.0.0` in der GitHub Container Registry. Der Workflow `publish.yml` veröffentlicht bei einem Git-Tag zusätzlich den gleichnamigen Image-Tag:

```sh
docker pull ghcr.io/tobasium/docker-mediathekview-webinterface:15.0.0
```

Das Projekt ist ein Fork und veröffentlicht sein Image unter dem eigenen GHCR-Namespace. Die Docker-Hub-Images und Badges des Upstream-Projekts gehören nicht zu diesem Fork.
