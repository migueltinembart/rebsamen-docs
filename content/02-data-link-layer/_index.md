+++
title = 'Data Link Layer'
date = 2024-01-26T15:23:17+01:00
draft = true
+++

Der Data-Link Layer ist die zweite Schicht im OSI-Modell und ist verantwortlich für die Übertragung von Datenpaketen von einem Knoten zum nächsten. Er stellt eine zuverlässige Verbindung zwischen zwei **direkt** verbundenen Netzwerkknoten her und ermöglicht die Kommunikation zwischen ihnen. Der Data-Link Layer ist in zwei Subschichten unterteilt: 

- Logical Link Control (LLC) und Media Access Control (MAC).
- Die LLC-Schicht ist verantwortlich für die Fehlerkontrolle, Flusskontrolle und Rahmen-Synchronisation.

Zusammen bieten beide Subschichten das Fundament für das Ethernet Protokol und werden im Kapitel [Ethernet](../02_Data-Link_Layer/Ethernet.md)

## MAC Schicht

Die MAC-Schicht ist verantwortlich für die Kontrolle des Zugriffs auf das gemeinsame Medium. Der Data-Link Layer verwendet Hardwareadressen (MAC-Adressen) zur Identifizierung von Geräten in einem Netzwerk. Er kann auch Fehlererkennung und -korrektur durchführen, um die Integrität der übertragenen Daten zu gewährleisten. Der Data-Link Layer ist auch für die Erstellung und Verarbeitung von Frames verantwortlich. Er ist der Vermittler zwischen dem physischen Layer, der sich mit den physischen Aspekten der Datenübertragung befasst, und dem Netzwerk-Layer, der sich mit der Datenrouting befasst. Insgesamt spielt der Data-Link Layer eine entscheidende Rolle bei der Bereitstellung einer zuverlässigen und effizienten Kommunikation zwischen Netzwerkknoten. Die MAC-Subschicht ist in diesem Fall auch der Träger für das eigentliche Ethernet-Protokol und dessen Implemenation.

## LLC Schicht

Die Logical Link Control befasst sich mit den Apsekten der ordentlichen Bitübertragung in der direkten Verbindung. Sie stellt die Integrität der Datenübertragung her und verwaltet die Logik für verschiedene Übertragungsformen wie Multiplexing und Fehlerkorrekturen. Die LLC Schicht übernimmt die Zuweisungen von der Layer-3 übergebenen Schichten an die MAC-Schicht und kontrolliert den Paketflow wie aber auch die sequenzielle Zuweisung bei mehreren Verbindungen über die Netzwerkschnittstelle. Mit der LLC Schicht befassen wir uns in diesem Workshop nicht.