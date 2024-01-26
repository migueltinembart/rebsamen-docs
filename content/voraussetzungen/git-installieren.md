+++
title = 'Git installieren'
date = 2024-01-26T15:10:23+01:00
draft = false
+++

Git ist ein Versionierungstool, ähnlich wie SVN, welches den Fokus auf lokale Entwicklung und Kontrolle von textbasierten Files bietet. Git ist heute das meistverwendete Versionierungstool das es gibt. Git darf nicht mit Github verwechselt werden. Github ist ein Git Repository Provider und falls es dir nicht aufgefallen ist, liest du gerade dieses Dokument auf Azure DevOps, einem Konkurenzprodukt zu Github. Damit du im Workshop auf deiner lokalen Maschine mit den Tools arbeiten kannst die in diesem Workshop ersichtlich sind, wirst du somit Git brauchen um eine Kopie dieses Git Repositories auf deinen Rechner zu verwalten. Also starten wir mal mit der Installation:

## Installation in Windows

Für windows kann Git über 2 Wege installiert werden. Je nach Arbeitsumgebung lohnt sich für dich die eine oder andere Installation und und die Vor und Nachteile werden hier beschrieben

### Installation nativ

Die native Installation auf Windows ist perfekt für Nutzer die nicht auf Linuxumgebungen angewiesen sind und ihre Umgebungsvariabeln nicht getrennt halten müssen. Das heisst, für Softwareentwickler oder Mitabeiter die keine Scripts auf linuxähnlichen Umgebungen testen müssen würde ich raten diese Installation zu bevorzugen, da kein Mehrwert erreicht wird falls du eine Installation mit [WSL](https://learn.microsoft.com/de-de/windows/wsl/about) bevorzugen würdest.

Die neuste Version von Git kannst du [hier](https://github.com/git-for-windows/git/releases/download/v2.43.0.windows.1/Git-2.43.0-64-bit.exe) herunterladen.

Leider ist Git zum installieren auf Windows nicht die schönste Erfahrung, doch zum Glück bietet der Installer alle wichtigen Einstellungen um die Installation auf die meisten Bedürfnisse abzustimmen.

Git wird dich während der Installation einige Fragen stellen welche am einfachsten schon während der Installation eingerichtet werden, da Git sonst nur mit der Kommandozeile angepasst werden kann. ich stelle dir am Ende des Kapitels aber noch 1 Tool vor welches dir dein Leben mit Git etwas einfacher gestaltet.

Folgende Punkte müssen während der Installation beachtet werden somit beachtet werden:

- Der Standard Code-Editor kannst du auf deinen preferierten Editor setzen. Falls du vorhin einen neuen Code Editor im Kapitel [Text_Editor_installieren](https://dev.azure.com/Rebsamen-Group/_git/Netzwerk-Workshop?path=/00_Voraussetzungen/01_Text-Editor_installieren.md) installiert hast, kannst du dieses gleich als Standard hier einstellen
- Setze deinen initial branch für neue Projekte auf **main**
- Lasse die Einstellungen für den GIT Pfad so wie er ist und ändere dor nichts, sonst läufst du Gefahr dass andere Git Tools deine Git Installation nicht finden kann.
- Verwende die standard openSSH und openSSL Bibliotheken von Git
- Line Ending Einstellungen => Checkout Windows-style , Commit Unix-style
- Ändere den Terminal Emulator auf Windows Default
- Git Pull Einstellungen => fast-forward or merge
- Verwende den Git credential Manager
- Enable file system caching => ja

Wenn du sichergestellt hast dass alle Menupunkte wie oben beschrieben eingestellt wurden kannst du die Installation ausführen. Git ist nun auf deinem Rechner installiert

### Installation auf Windows mit WSL

Nach dem Einzug von Windows in die Welt von Open Source, hat Windows WSL entwickelt. WSL steht für _Windows Subsystem for Linux_ und ermöglicht es ein Linux Subsystem auf Windows zu betreiben. Windows hat dafür eigene Kernelimplementationen für ihre Systeme geschrieben um bekannte Distributionen wie Ubuntu, openSUSE, Kali Linux, Debian, Oracle Linux und viele weitere zu installieren. Dabei erhält das Subsystem ein eigenes virtuelles Laufwerk mit welches du auch über dein Subsystem auf deine Windows Umgebung zugreifen kannst. Doch am ehesten wird WSL heute in der Entwicklung und Containerisierung von Applikationen verwendet.

Je nach Distribution ist Git schon installiert. Am einfachsten überprüfst du ob git bei deiner Installation schon dabei ist in dem du in deinem WSL-Terminal einfach `git` schreibst...

Falls du die Man-Page (Anleitung) zur Nutzung von git bekommst, ist git bei deiner Distribution bereits schon installiert

Falls aber eine meldung kommt wie `bash: command not found: git`, dann ist Git auf dieser Distribution nicht vorhanden. Installiere somit mit dem Package Manager deiner Distribution einfach kurz git und du bist schon einsatzbereit.

### Optional

Git an sich benötigt keine Benutzerangaben des Users, ausser bei einer Sache. Commits. Damit Git weiss wer an welchem File Änderungen gemacht hat, musst du Git halt sagen wer du bist und was für eine E-Mail Adresse du besitzt. So kann Git diese Informationen immer auf die Commits als Metadaten ablegen und ermöglicht es dir bei Änderungen an Files zu sehen, wo und wer diese Änderungen gemacht hat.

Den Benutzernamen und deine Email kannst du wie folgt für Git setzen:

```
git config --global user.name Benutzername
git config --global user.email deine-email@contoso.com
```

Ersetze dabei die Felder Benutzername durch deine Angaben und schon kannst du herumcommiten wie dein Herz begehrt.

## Weitere Angaben

Falls du Git und seine Essenz lernen möchtest, biete ich dir ein paar Referenzseiten an. Beachte das Git für diesen Workshop nur für die initiale Kopie des Workshops benötigt wird. Trotzdem hier ein paar Beispiele:

- [Learn Git Branching](https://learngitbranching.js.org/) interaktives Tutorial
- [CodeCademy](https://www.codecademy.com/learn/learn-git) ist gratis und anfängerfreundlich
- Du kommst bei Miguel vorbei und fragst ihn nach seinem Buch über Git
