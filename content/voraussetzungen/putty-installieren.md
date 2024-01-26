+++
title = 'Putty Installieren'
date = 2024-01-26T15:17:22+01:00
draft = true
+++

Putty zu installieren ist genauso einfach wie die Installation eines Text-Editors. Lade den Installer [hier](https://the.earth.li/~sgtatham/putty/latest/w64/putty-64bit-0.79-installer.msi) herunter und installiere durch bestätigen jedes Kontext-Menus bi sPutty installiert ist.

## Was ist Putty

Damit man Putty einfacher verwenden kann, muss evtl. zuerst verstanden werden was Putty genau ist.

Putty trägt den Namen, weil die 3 letzten Buchstaben für TTY stehen. TTY (Teleprinter oder TeletypeWriter) waren früher Computer welche über eine Telefonleitung Textnachrichten an ein fernes System übermitteln konnten. Das heistt die Anzeige und die Eingabe erfolgte dabei über ein [Terminal](<https://de.wikipedia.org/wiki/Terminal_(Computer)>). Den Namen Terminal für Konsoleumgebungen wurde heute für verschiedene Anwenungen welches auf dem selben Prinzip arbeiteten verwendet. Heutzuttage kennt man das Terminal vorallem in Linuxumgebungen, aber auch Windows ist seit jüngster Zeit mit einem Terminal ausgestattet.

Die heutigen modernen Terminalemulatoren wie Putty können über verschiedene Protokolle eine tty-session starten. Darunter zählen SSH, telnet oder serial zu einer der meistgenutzten Protokolle und Umgebungen in denen Putty Abhilfe schafft.

### Wieso Putty und nicht das neue Windows Terminal

Das neue Windows Terminal besitzt einen SSH Client, doch basiert dieser auf SSH2.0 und ist mit neuen Verschlüsselungsformaten ausgestattet. Somit ist dieser Terminalemulator für die meisten herkömmlichen Fälle eine valide Ablöse für Putty. Doch ältere Geräte welche vorallem auf ältere Verschlüsselungstechnologien wie diffie-hellman und weiteres angewiesen sind, werden durch SSH2.0 nicht mehr unterstützt. Dies natürlich aus dem Grund der Sicherheit, da solche Protokolle nicht mehr in heutigen produktiven Endgeräten eingesetzt werden. Leider können wir das Problem, bei vielen Kunden nicht durch einen Systemaustausch einfach so lösen und die meisten Systeme welche über SSH erreichbar sind, sind in der Regel nicht im Internet erreichbar. Wer sehr gewagt ist, kann gerne alle alten Protokolle über SSH2.0 mit Optionen und dem Austausch von protokollen bedienen, wird dabei während eines Servicefalls nicht gerade effizient sein.

Geräte welche evtl. mit alten SSH Verschlüsselungsprotokollen arbeiten sind:

- Switches
- Router
- Firewalls
- Access Points
- Ältere Linux Maschinnen welche noch keinen Support für SSH 2.0 besitzen

Die meisten heutzutags verkauften Endgeräte mit SSH-Support unterstützen unterdessen SSH2.0 mit neueren Standards, doch man trifft in der Arbeitswelt auf so manche Implementationen von SSH und kann mit Putty die Kopfschmerzen für manchen Techniker ersparen.

# Verwenden von Putty

Nach der Installation kannst du Putty gerne starten. Folgendes Fenster wird dir dann angezeigt. ![Putty Hauptfenster](https://hpc.nmsu.edu/discovery/_images/tutorials/PuTTY/putty_configure.jpg){align=right} Zu beachten gibt es da eigentlich noch nicht viel. In der Regel kommt der Startbildschirm mit Fokus auf die Eingabe einer IP-Adresse. Im selben Bereich werden auch die verschiedenen Verbindungstypen dargestellt, darunter SSH, Telnet und Serial. In 99% der Fälle wirst du meistens nur eine SSH Verbingung benötigen und kannst somit dich direkt auf die Ziel-IP-Adresse des Endgeräts stürzen. Für alle anderen Fälle wird dringend Erfahrung mit den verschiedenen Verbindungstypen benötigt.
