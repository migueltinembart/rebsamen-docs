+++
title = 'Netzwerkgeräte'
date = 2024-01-26T15:24:54+01:00
draft = false
+++

in der zweiten Schicht kennt man heutzutage nciht mehr viele Geräte. Der Netzwerkswitch hat sich seit Jahren als die einzige Alternative erwiesen und bleibt bis heute die Kernkomponente für Ethernetbasierte Netzwerke. Trotzdem beschreibe ich hier noch ein paar namenhafte Komponenten aus der Frühzeit und wie Ethernet mit diesen Komponenten funktionierte und Lösungen gefunden wurde um auf den Stand eines Switches zu kommen.

## Repeaters und Hubs

![Repeater mit Koaxialeingang und Twister-Pair Verbindung](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9e/Network_card.jpg/330px-Network_card.jpg){align=right}
Ein Netzwerkhub oder ein Netzwerkrepeater wurde früher noch benötigt um mehrfache Verbindungen über eine Bus-Topologie zu realisieren. Dies hatte zum Vorteil, dass so mehrere Geräte mit weniger teuren Kabeln in einem Netzwerk eingebunden werden konnte. Doch die Netzwerkstörungen nahmen schnell zu wenn immer mehr Netzwerkkomponenten in das Netzwerk geschlauft wurde. Darum wurden Kerntechnologien für das Ethernet-Protokol entwickelt um die Qualität der Verbindungen zu verbessern.

Repeater sind protokolunabhängig und verarbeiten keine Pakete wie ein Switch, sondern verteilen auf allen Ports jedes übermittelte Signal aus, ausser an dem Port von welcher Netzwerkframes eingegangen sind.

Der Vorteil von Hubs war offentsichtlich. Zumal konnte man mehrere Netzwerkgeräte mit weniger Kabelaufwand verbinden. Doch dies war auch der einzige Vorteil der angeboten wurde. Frames welche nur an ein Gerät gesendet werden musste, sind auf allen Ports ausgestrahlt worden und die Technologie basierte auf Halb-Duplex. Das heisst es konnte nur ein Gerät zur selben Zeit senden und alle anderen Geräte mussten Frames welche nicht an sie gerichtet wurden, trotzdem verarbeiten und schlussendlich verwerfen.

Um die Kommunikation über einen Hub zu vereinfachen und keine Signalkollisionen zu verursachen, musste ein Mechanismus entwickelt werden der Signalkollisionen entdecken und umgehen kann. Dafür wurde CSMA/CD entwickelt.

### CSMA/CD

[Carrier Sense Multiple Access/Collision Detection](https://de.wikipedia.org/wiki/Carrier_Sense_Multiple_Access/Collision_Detection) bezeichnet ein asynchrones Medienzugriffsverhalten, dass den Zugriff verschiedener Stationen auf ein gemeinsames Übertragungsmedium regelt.

Damit mehrere Komponenten gleichzeitig senden und lauschen können musste ein Verfahren entwickelt werden, welches diese Handhabung regelt und standardisiert. Der Ablauf sieht insofern so aus:

**Schritt 1 Horchen: Überprüfe ob das Medium belegt ist**

Frei: => Weiter mit Schritt 2

Belegt: => Weiter mit Schritt 1

**Schritt 2 Senden: Während dem Abhören wird die Information auf das Medium übertragen**

Erfolg: => Die Übertragung ist erfolgreich. Weiter mit Schritt 5

Kollision: => Wird eine Kollision entdeckt, beendet die Komponente die Übertragung und sendet ein Jam-Signal welches alle Geräte informiert, dass eine Kollision stattgefunden hat. Weiter mit Schritt 3

**Schritt 3 Leitung ist belegt: Überprüfe die Anzahl der Übertragungsversuche**

Maximum nicht erreicht: eine zufällige Backof-Zeit wird abgewartet. Weiter mit Schritt 1

Maximux erreicht: Weiter mit Schritt 4

**Schritt 4 Fehler: Maximale Anzahl an Übertragunsversuchen wurde überschritten und ein Fehler wird an die übergeordnete Schicht (Layer 3) zurückgeschickt.**

Weiter mit Schritt 5

**Schritt 5** Übertragungsmodus beenden

## Switches

![Netzwerkswitches von Cisco](https://cdn.competec.ch/images2/3/9/0/56267093/56267093_xxl3.jpg){align=right width=400}
Switches sind die weiterentwicklung von Hubs und bieten nebst dem Komfort mehrere Geräte in ein Netzwerk aufzunehmen auch die Kapazizät mit dem Ethernet Protokol zu arbeiten. Switches funktionieren wahrlich auf der zweiten Schicht, d.h. der Switch kann gezielt Frames anhand der Quell- und Zieladresse die Datenpakete am richtigen Port raussenden, ohne dabei alle Ports mit Frames zu überschütten. Anders als bei einem Hub, sind bei Switches intelligente Komponenten eingebaut um die Verarbeitung von Daten schnell zu verarbeiten.

Seit der Erfindung des Switches im Vergleich zu den heutigen am Markt verfügbaren Geräten hat sich einiges geändert. Switches kommen mit Voll-Duplex hervorragend aus und haben sogar gelernt Verkabelungsfehler vorzeitig zu korrigieren. Wie zum Beispiel das zusammenstecken von 2 Switches mit einem nicht-Crossoverkabel führte früher zu Problemen, da Switches anders als Computer nicht über die gleichen Pins senden und empfangen. Heute einigen sich Switches selbstständig mit welchen Pins sie senden und empfangen wollen.

Switches können in verschienenen Arten und Formen auftauchen. Festverbaut oder modular in einem Chassis, mit RJ45 oder SFP+ Modulen zu Erweiterung von Schnittstellen oder auch mit direkter Spannungsversorgung über das Netzwerkkabel mittels PoE.

Wichtig ist zu verstehen dass Switches in ihren Operationen rein auf Layer 2 arbeiten und die darüberliegenden Layer nicht versteht oder verstehen muss. Trotzdem hat man im Laufe der Zeit an vielen Stellen mit Layer 3 Switches (sogenannte Multilayer Switches) eine Variante des Netzwerkswitches gemacht, welches Routing auch möglich macht. Obwohl diese Switches auch auf Layer 3 operieren können, heisst das nicht dass diese Switches nicht ihre Aufgabe als Switch wahrnehmen, sondern dass die Funktionalität von Routern virtuell auf solche Switches abgewältzt wurde um für spezielle Fälle eine andere Alternative bietet ohne Router mit mehreren Netzwerken einfach umzugehen.

## Access Points

![Cisco Access Point](https://www.cisco.com/c/dam/en/us/support/web/images/series/wireless-aironet-700-series.jpg){align=right width=450}
Ein Access Point dient zur Erweiterung des Netzwerks für nichtkabelgebundene Endgeräte. Ein Access Point operiert genau betrachtet auf der ersten und zweiten Schicht und dient als Brücke der kabelgebundenen Protokolle auf kabellose Protokolle. Access Points arbeiten anders als Switches mit dem 802.11 Wlan-Standard und arbeitet wie bei Ethernet mit Mac-Adressen, aber auch mit anderen Parametern um die Verbindungen zu steuern.

> [!INFO]- Gut zu wissen
> Trotz der guten Datenübertragungsgeschwindigkeit mit WLAN, funktioniert die Übertragung nur über Halb-Duplex. Das heisst der WLAN-Sender und die gebundenen Geräte können nicht gleichzeitig Senden und empfangen.
>
> Man hat sich dabei auf sehr gewagte Übertragungsmethoden und Konzepte orientiert und ist ein Thema welches für jeden interessierten besser in einer Selbststudie angeschaut werden soll. Das beschriebene Verfahren [CSMA/CA](https://de.wikipedia.org/wiki/Carrier_Sense_Multiple_Access/Collision_Avoidance) (Nicht verwechseln mit CSMA/CD) dient dabei als eine der wichtigsten Fundamente wie Halbduplex für solche Fälle bestens geeignet ist.
