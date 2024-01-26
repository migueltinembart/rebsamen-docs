+++
title = 'Netzwerkadapter'
date = 2024-01-26T15:21:53+01:00
draft = false
+++

Ein Netzwerkadapter, auch bekannt als Netzwerkkarte oder Netzwerkinterfacekarte (NIC), ist ein Hardwaregerät, das es einem Computer ermöglicht, mit einem Netzwerk zu kommunizieren. Es wandelt die Daten, die vom Computer gesendet werden, in ein Format um, das über das Netzwerk übertragen werden kann, und umgekehrt. Netzwerkadapter stehen in der Grenze zur physikalischen Beschaffenheit für die digitale èbertragung von Bits und der Hardware die über den TCP/IP Stack kommunizieren.

## Schnittstellen

Netzwerkadapter können verschiedene Arten von Schnittstellen haben, abhängig von der Art des Netzwerks, mit dem sie kommunizieren sollen. Einige gängige Schnittstellen sind Ethernet (für kabelgebundene Netzwerke), Wi-Fi (für drahtlose Netzwerke) und Bluetooth (für kurze Distanzen). Ethernet-Adapter können RJ-45-Stecker verwenden, während Wi-Fi- und Bluetooth-Adapter in der Regel intern sind und keine physischen Stecker haben.

### Übertragung von Bits

Netzwerkadapter verwenden verschiedene Methoden zur Übertragung von Bits, abhängig von der Art der Schnittstelle. Ethernet-Adapter verwenden beispielsweise elektrische Signale zur Übertragung von Bits über Kupferkabel, während Wi-Fi-Adapter Radiowellen zur Übertragung von Bits über die Luft verwenden.

### Weitere Eigenschaften

Ein Netzwerkadapter ist das Bindeglied zwischen der physikalischen Schicht und der zweiten Schicht (gemäss OSI-Model) dem Data-Link Layer. Das heisst dass für die Übertragung von Ethernet Ethernet Frames auch gewisse Eigenschaften vom Data-Link Layer vorhanden sind. Alle Netzwerkadapter besitzen eine [Mac-Adresse](https://de.wikipedia.org/wiki/MAC-Adresse). Diese Adresse ist meist schon vom Hersteller auf dem Adapter fest vergeben.

Ein Netzwerkadapter muss sich ausserdem damit befassen, wie die Daten kontrolliert und sicher übertragen werden. Die folgenden Mechanismen beschreiben zusätzliche Eigenschaften von heutigen Netzwerkschnittstellen, unabhängig des Übertragungsmedium:

**Duplex-Einstellungen**: Netzwerkadapter können in Full-Duplex-Modus (gleichzeitiges Senden und Empfangen von Daten) oder Half-Duplex-Modus (abwechselndes Senden und Empfangen von Daten) arbeiten.

**Auto-Negotiation**: Dies ist eine Funktion, die es dem Netzwerkadapter ermöglicht, die beste Übertragungsrate und den Duplex-Modus automatisch mit dem verbundenen Gerät auszuhandeln.

**Error Checking and Correction**: Netzwerkadapter verwenden verschiedene Techniken zur Fehlerprüfung und -korrektur, um sicherzustellen, dass die übertragenen Daten korrekt sind.

**Buffering**: Netzwerkadapter haben einen Puffer, der dazu dient, Daten temporär zu speichern, wenn der Computer oder das Netzwerk nicht in der Lage ist, die Daten schnell genug zu verarbeiten.

**Traffic Shaping**: Einige Netzwerkadapter können den Datenverkehr formen, um die Netzwerkleistung zu optimieren. Dies kann durch Priorisierung bestimmter Arten von Datenverkehr oder durch Begrenzung der Bandbreite für bestimmte Anwendungen erfolgen.
