+++
title = 'Address Resolution Protocol'
date = 2024-01-26T15:27:43+01:00
draft = false
+++

ARP ist ein Layer-3 Protokoll welches MAC-Adressen mit IP-Adressen in einer Tabelle asoziiert. ARP vereinfacht die Kommunikation mit anderen IP-fähigen Endgeräten, da für die erfolgreiche Kommunikation in einem Netzwerk ohne MAC-Adresse ein IP-Paket kein Ziel finden kann. So kann in einer Broadcast-Domäne die MAC-Adresse aller Endgeräte mit denen über IP-Kommuniziert werden soll, die Relation der Hardwareadresse zur logischen IP-Adresse hergestellt werden.

## Wieso ist das wichtig?

Damit über ein Netzwerkkabel erfolgreich Frames versendet werden können, die auch ankommen, müsste im Prinzip die MAC-Adresse des Ziels bekannt sein. Doch in den meisten Fällen, wird diese nicht bekannt sein und die Arbeit jede MAC-Adresse in einem Netzwerk an jeden Computer zu übermitteln wäre ein zu grosser Arbeitsaufwand. Layer-2 befasst sich bekannterweise nur mit der direkten Kommunikation zwischen 2 Schnittstellen und Layer-3 versucht mit dem IP-Protokol die Verbindung von mehreren Broadcastdomänen zu überbrücken. Damit also ein IP-Paket überhaupt zum richtigen Endgerät kommen kann, müsste in diesem die MAC-Adresse bekannt sein, oder zumindest die MAC-Adresse des nächsten Routers, falls sich das Endgerät nicht im selben Netzwerk befindet.

ARP stellt dabei die Verbindung zwischen Layer-2 und Layer-3 bereit um die Aushandlung und die Kommunikation in einem IPv4-Netzwerk zu vereinfachen.

Oder ganz einfach. Wenn du den Namen deines Kollegen weist, aber nicht seine Telefonnummer, dann gehst du ins Telefonbuch und suchst die Nummer anhand des Namens. ARP ist sozusagen das Telefonbuch für MAC-Adressen

## Wie funktioniert ARP

In diesem Beispiel möchte
