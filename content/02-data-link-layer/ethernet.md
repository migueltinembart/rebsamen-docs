+++
title = 'Ethernet'
date = 2024-01-26T15:24:06+01:00
draft = true
+++

Das Ethernet Protokol ist eine Familie von kabelgebundenen Technologien und wurde 1980 unter dem IEEE Standard IEEE802.3 festgelegt. Ethernet wurde über die Jahre immer weiterentwickelt um schnellere Übertragungen zu ermöglichen, längere Distanzen zu überbrücken um das darunterliegenden Twisted Pair Kabel besser ausnützen zu können oder einfachere Mehrverbindungen zuzulassen. In der Zeit ist aber Ethernet immer abwärtskompatibel zu deren älteren Definitionen gehalten worden.

Das originale [10BASE5](https://en.wikipedia.org/wiki/10BASE5) wurde damals mit dicken Koaxialkabeln betrieben und nach kurzer Zeit durch Twisted Pair und Optischen Kabeln ersetzt. In den letzten Jahren wurde Ethernet soweit entwickelt, dass bis zu 400Gbit/s übertragen werden können.

Ethernet beschreibt mehrere Verkabelungs- und Signalisierungsvarianten und definiert sich über das OSI-Model über die ersten 2 Schichten, vorallem in der MAC-Subschciht auf Layer-2.

## Ethernet Frame

Ethernet arbeitet auf der 2 OSI-Layer Schicht und verarbeitet üblicherweise Frames. Ethernet Frames sind die letzte logische Einheit bevor diese Daten dann schlussendlich zu Bit verarbeitet wird beim Senden. beim Empfangen werden die Bits wieder zu einem Frame zusammengesetzt. Ein Frame besteht aus einem sogenannten Header, die Kopfzeile eines Frames und den eigentlichen zugrundeliegenden Daten. Am Ende des Frames wird noch eine CRC Checksume angereiht und um sicherzustellen, dass keine Fehler bei der Übertragung passiert sind. Wir gehen in [CRC Checksumme](#crc-checksumme) näher darauf ein.

![Ethernet Frame](https://upload.wikimedia.org/wikipedia/commons/thumb/1/13/Ethernet_Type_II_Frame_format.svg/700px-Ethernet_Type_II_Frame_format.svg.png)

## Headers

Headers sind die Kopfzeile eines jeden Ethernet Frames. Darin stehen alle Addressinformationen die nötig sind um einem Switch zu sagen von wo und wohin ein Frame übertragen werden sollte. Folgende Einträge im Header definieren hauptsächlich die Hauptbestandteile des Headers

### Destination MAC Adresse

Dieses Feld hält den Wert der Mac-Adresse des Empfängergeräts bei sich.

### Source MAC Adresse

Dieses Feld hält den Wert der Mac-Adresse des Absendergeräts bei sich.

### EtherType

Beschreibt mit einem vordefinierten Wert den Inhalt des überliegenden Protokols auf Layer 3. In einem reinen TCP/IP IP-Netzwerk wird dass meistens IPv4 sein. Der Wert für IPv4 in einem EtherType Feld wäre zum Beispiel 0x0800.

Das Ethertype Feld dient dazu, das nächste übergeordnete Protokoll zu beschreiben, damit das ausgekapselte Paket an die richtige Protokolverarbeitung gelangt. Im Falle von IPv4 wird das ausgekapselte IP-Paket an die ÎP-Verarbeitungsschicht im Rechner weiterübergeben.

### Daten

Daten sind in diesem Fall das IP-Paket. Das Ethernet-Frame befasst sich nicht mit den darüberliegenden Daten. In den meisten Fällen sind das IP-Pakete, kann aber auch jedes andere Layer-3 Protokol sein.

### CRC Checksumme

Am Ende nach den Daten wird die Quersumme der Daten für die Checksumme ausgerechnet. Falls sich and den darunterliegenden Daten während der Übertragung etwas verändert hätte, würde die Neuberechnung nicht derselben Quersumme entsprechen und auf einen Fehler bei der Übertragung hindeuten. So kann das Ethernetprotokoll eine Neuübertragung des Frames anfragen und sicherstellen, dass alle Frames eindeutig übertragen werden. Dies ist eine leichte Erklärung auf eine komplexe Lösung von CRC-Checksummen.

> [!NOTE]- Trivia
> Im hintergrund läuft da noch mehr ab. Falls du mehr wissen möchtest kannst du gerne [hier](https://de.wikipedia.org/wiki/Zyklische_Redundanzpr%C3%BCfung) die bessere Erklärung lesen.

## Bilden eines Netzwerks auf Basis von Ethernet

Ein einfaches Ethernet Netzwerk kann am einfachsten mit einem einfachen Switch erstellt. Dabei benötigt es noch keinen Router oder sonstige Komponenten. Dabei bildet sich automatisch über dieses kleine Netzwerk eine Broadcast Domain. Die Broadcast Domain ist ein einfacher Begriff für ein Netzwerk über das alle Komponenten über jeden Port an diesem Switch kommunizieren können und Broadcasts versendet werden. Somit kann man davon ausgehen, dass wenn ein Broadcast von einem Gerät versendet wird, dass dieses an jedem Port ausgesandt wird. Nun nimmt man einen weiteren Switch dazu und verbindet dieses mit dem bestehenden Switch. Nun auch gehört dieser Switch derselben Broadcast domain an und Broadcast Pakete können dort empfangen und wieder an alle Ports weitergeleitet werden. Gratuliere du hast ein [LAN](https://de.wikipedia.org/wiki/Local_Area_Network) erstellt.

### Was ist ein Broadcast

Broadcast definiert den Versandt einer Information an alle in einem Netzwerk. Im Falle von Ethernet ist dies eine wichtige Art sich im Netzwerk auszutauschen und vorallem wenn man auf Layer 3 wichtige Operationen durchführen sogar essenziel. Denn ein Broadcast ermöglicht gleich von Anfang an Möglichkeiten um den Standort und weitere Informationen zu bestimmen.

Ein Broadcast im Ethernet Bereich ist ganz einfach definiert. Möchte ein Rechner eine Broadcast-Nachricht an alle Computer im Netzwerk senden, so schreibt dieser seine Nachricht einfach an die Destination MAC-Adresse _ff:ff:ff:ff:ff:ff_. Diese MAC-Adresse ist standartisiert und wird von jedem Switch verstanden und führt dazu, dass diese Frames dann an jedem Port ausgesandt wird.

#### Wieso benötigt man Broadcast-Anfragen

Da kann man einfache praktische und in der Praxis verwendete Beispiele verwenden:

- Wenn ein Client in einem Netzwerk sich verbindet und gerne per DHCP eine IP-Adresse hätte, müsste der Computer raten oder schon bereits wissen mit welcher MAC-Adresse dieser angesprochen wird. Wenn der Client jedoch einfach eine Broadcast Anfrage mit der Bitte um eine DHCP Adresse macht, kann der DHCP Server ihm die Antwort mit einer neuen IP-Adresse weiterreichen.

- Hat man einen MAC-Filter auf einem Switch, kann einfach das Gerät identifiziert werden, da jedes Gerät beim Einstieg in ein Netzwerk direkt eine Broadcast-Nachricht an alle Empfänger übermitteln würde.

- Wenn man die MAC-Adresse eines Geräts kennenlernen möchte in der Broadcast-Domain, kann man ja einfach alle Rechner im Netzwerk fragen wer die IP-Adresse besitzt und bekommt die MAC-Adresse in der Antwort des Empfängergeräts.

Wichtig ist auf jeden Fall zu wissen, dass Broadcast-Anfragen nur von diesem Netzwerkgerät beantwortet werden, welches für diese Anfrage auch zuständig ist. Somit werden nicht unnötigerweise noch Antworten im Netzwerk verschickt, welche schlussendlich überflüssig wären und keinen Nutzen bringen würden.

## Was wenn ich meine Broadcast Domäne aufteilen möchte?

Wie schon betont, spannt sich eine Broadcast Domäne über jeden Port auf allen Switches. Doch mit der Einführung von [VLAN](https://www.ionos.de/digitalguide/server/knowhow/vlan-grundlagen/). Mit VLANs lassen sich virtuelle LANs bilden und lässt somit das aufteilen eines physikalischen Netzwerks in mehrere logische Netzwerke. So können auf einem Switch mehrere eigenständige Broadcast-Domänen existieren, welche auf dem selben phyischen Switch nicht miteinander kommunizieren können. Die Technik und der Standard dahinter wurde mit [IEEE 802.1Q](https://de.wikipedia.org/wiki/IEEE_802.1Q) umfassend definiert.

Mit IEEE 802.1Q wurde für das bisherige Ethernetframe ein zusätzliches Feld eingebaut. Der 802.1Q Header, mit 32Bit, wurde nach dem Source-MAC Feld eingefügt und beschreibt folgende Datenfelder:

- Protokoll-ID
- Priorität
- Canonical Format
- VLAN-ID

Vorallem die Protokoll-ID, die Priorität und die VLAN-ID sind wichtig. Die _protocol-id_ beschreibt den Frame als ein _vlan-tagged-frame_ und so weiss ein Switch, dass in dieser Frame in einem bestimmten VLAN ist. Die Priorität ist ein Feld zur Bestimmung von QoS-Priorisierungsleveln auf einem Frame (siehe [QoS](./QoS.md)). die letzten 12 Bit benötigen wir um VLAN-IDs zu setzen.

![802.1Q Header im Ethernet Frame](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0e/Ethernet_802.1Q_Insert.svg/1125px-Ethernet_802.1Q_Insert.svg.png)

VLAN-IDs sind die Kennungsziffern von jedem virtuellen Netzwerk und so kann der Switch über die VLAN-ID die Frames in das richtige VLAN übertragen.

Das Arbeiten mit VLANs ermöglicht uns viele Möglichkeiten ein Netzwerk mit weniger Switches in mehrere Subnetze aufzuteilen. Das Arbeiten mit VLAN-Tagging ermöglicht das gleichzeitige Übertragen von Frames aus mehreren VLANs auf einem Kabel und erspart somit die grössere Kabelungsarbeiten. Das Festlegen von einem fix definierten VLAN für normale Arbeitsgeräte, macht es möglich dass man einzelne Ports als _untagged ports_ definiert und somit nur auf einem spezifischen VLAN sitzt.

### Welche Geräte unterstützen VLANs

- Managebare Switches unterstützen in der Regel VLAN-Tagging
- Server mit Servernetzwerkschnittstellen müssen auch ein Betriebssystem und die richtigen Treiber besitzen um mit VLAN Informationen klarzukommen (Windows Server, Linux)
