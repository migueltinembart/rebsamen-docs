+++
title = 'Internet Protocol'
date = 2024-01-26T15:27:19+01:00
draft = true
+++

Das Internetprotokol ist das meistverbreitete Protokol unter den Netzwerkprotokollen und stellt somit die Grundlage für unser Internet dar. Durch das IP-Protokol wird die Übertragungs über weite gespannte Netzwerke vereinfacht und mit Rounting sichergestellt, dass IP-Pakete an die richtige Stelle weitergeleitet werden.

In einem IP-Netzwerk werden keine Frames, sondern Pakete gesendet. Dieser Ausdruck wird zur Unterscheidung der einzelnen Layer-Komponenten verwendet und somit wissen Netzwerkadministratoren auf Anhieb ob man von Switching- oder Routing-Thematiken redet. Das IP-Protokol gibt es in 2 Varianten und wird werden auf ersteres besonderen Wert legen. _IPv4_ und _IPv6_. IPv4 gibt es schon seit 1981 und ist bis jetzt immernoch weiter verbreitet als der jüngere Standard.

## Aufbau eines IP-Pakets

![Aufbau eines IP-Pakets](https://www.tutorialspoint.com/de/ipv4/images/ip_header.jpg)

Das IP-Paket ist in 2 Teile aufgeteilt. Den Header und den Payload. Der Header ist der Teil des Pakets, welcher die Informationen über das Paket beinhaltet. Der Payload ist der Teil des Pakets, welcher die Daten beinhaltet welche übertragen werden sollen.

### Version

Die Version gibt an, um welche Version des IP-Protokols es sich handelt.

### IHL

Das Internet Header Length (IHL) Feld beschreibt die Länge des Headers in 32 Bit Wörtern. Das heisst, wenn das IHL Feld den Wert 5 hat, dann ist die Länge des Headers 5x32 Bit gross.

### Type of Service (DSCP und ECN)

Das Type of Service Feld beschreibt die Art des Service. Wird für QoS mittels [DSCP](https://www.techtarget.com/whatis/definition/Differentiated-Services-DiffServ-or-DS#:~:text=types%20of%20traffic.-,DiffServ%20code%20point,range%20from%200%20to%2063.) (differentiated services code point) verwendet. Früher gab es das IPP Verfahren um IP-Pakete zu priorisieren, DSCP vereinfacht die Weise verschiedene Netzwerkdienste (Telefonie, Video, Best Effort, etc.) unterschiedlich zu behandeln.

### Total Length

Das Total Length Feld beschreibt die Gesamtlänge des IP-Pakets. Das heisst, wenn das IP-Paket eine Gesamtlänge von 1500 Bytes hat, dann ist das Total Length Feld 1500 Bytes gross. Dieses Feld kennt man auch als Maximum Transmission Unit (MTU)

### Identification

Das Identification Feld beschreibt die Identifikation des IP-Pakets. Dieses Feld wird für die Fragmentierung und die Defragmentierung des Payloads verwendet. So können mehrere IP-Pakete wieder zusammengeführt werden, wenn alle angekommen sind.

### Flags

Das Flags Feld beschreibt den Status der Fragmentierung. Damit wird sichergestellt ob dieses Paket fragmentiert werden kann, oder ob dies das Ende des Fragments ist.

### Fragment Offset

Beschreibt die Position im Fragment und kennzeichnet die Position im orginalen Paket.

### Time to Live

Das Time to Live Feld beschreibt die Lebensdauer des IP-Pakets. Wird verwendet um die Lebensdauer eines IP-Pakets festzustellen. So wird sichergestellt, dass IP-Pakete nicht unendlich lange weiterversendet werden. Bei jedem durchwandern eines IP-Pakets durch einen Router, wird dieser Wert um 1 verringert. wenn das Time To Live 0 erreicht, wird es vom empfangenen Router abgeworfen und nicht mehr weiterverarbeitet.

### Protocol

Das Protocol Feld beschreibt das darüberliegende Protokol. Das heisst, wenn ein IP-Paket an ein Gerät gesendet wird, muss dieses Gerät wissen, wie es das IP-Paket verarbeiten soll. Dafür wird das Protocol Feld verwendet. Meistens wird da ein Wert für TCP oder UDP verwendet.

### Header Checksum

Das Header Checksum Feld prüft wie bei einer CRC Checksumme die Richtigkeit eines IP-Pakets und kann bei einem Fehler, ein Wiedersenden des Pakets anfordern.

### Source und Destination Address

In den Source- und Destionationfeldern sind schliesslich die Sender und Empfängeradressen eingetragen. Diese helfen dem Router die IP-Pakete in die richtigen Subnetze weiterzuschicken.

## Geschichte

Mit den vorherigen Information können wir vielleicht ein IP-Paket analysieren, viel anfangen können wir damit aber nicht viel. Ausserdem fehlen uns ein paar Angaben mit denen wir die Kommunikation in einem IP-basierten Netzwerk festlegen können. Anders als bei Ethernet, gibt es in einem IP-Netzwerk keine fest eingebauten Adressen oder Endgeräte welche immer mit einer einzigen IP-Adresse ab Werk kommunizieren. Das bedeutet das Komponenten welche in einem IP-Netzwerk mitwirken möchten, auch für die Arbeit mit den IP-Protokollen ausgelegt werden müssen. Dafür aber zuerst ein paar Definitionen und etwas Geschichte.

### IP-Adressen - Entstehung und Zukunft

Wir betrachten die Geschichte ab der Entstehung von IPv4. Die Entstehung des ersten IP-Protokols kann auf den Mai 1974 zurückgeführt werden, doch musste das anfängliche Protokol noch einige Male überarbeitet werden. Nicht lange und das IP Protokol Version 4 wurde zum ersten richtigen Standard mit der Einführung von TCP/IP als neues etabliertes Referenzmodel für Netzwerke im Jahr 1983. Eine IP-Adresse ist ein 32bit langer Wert und definiert die Adresse mit der ein Endgerät in einem IP-basiertem Netzwerk seine Pakete empfängt und für die Source Adresse verwendet wird um mitzuteilen von welcher IP-Adresse Pakete adressiert wurden. Das Internet wurde dadurch auf das heutzutage weltweit gespannte Netzwerk erweitert und einige Änderungen wurden seither eingeführt.

Zu den Zeiten als nur Computer für die Verwendung für die IP-Kommunikation genutzt wurden, dachte man dass mit 32 Bit, also einer Möglichkeit 2,147,483,647 mögliche eindeutige IP-Adressen, genug Adressen für die ganze Welt offen stehen. Dieser Gedanke zeigte sich in den 80/90er Jahren als Fehler, denn die Neuzuweisung von IP-Adressen stieg drastisch an und die IP-Adressen wurden langsam knapp. Während dieser Zeit wurde noch an IPv6 gearbeitet, doch man fand eine Lösung mit der man IPv4 weiterhin mit der Addressknappheit weiternutzen konnte.

Die Organisation IANA 1981 gegründet und regelte mit dem Prinzip von Netzklassen anhand von Subnetzmasken die Verteilung von Netzwerken verschiedenen Grössen zur Aufteilung des kompletten Adressbereichs von IPv4 in mehrere _Subnetze_. Das IP-Routing wurde dadurch geboren und Routernetzwerke konnten IP-Pakete in die richtigen unterteilten Netzwerke verteilen und ein Standard-Gateway war nötig um zwischen Netzwerke zu kommunizieren. Leider stieg die Knappheit der Adressen weiterhin an. Internet Service Provider in der ganzen Welt kauften weiterhin massenhaft Netzwerke um Privatkunden und Firmen in ihre bestehenden Netzwerke zu integrieren und die Anzahl an IP-Endgeräten pro Haushalt stieg noch rasanter an. Die Lösung - [RFC 1918](https://de.wikipedia.org/wiki/Private_IP-Adresse), auch bekannt als private IP-Adressen kombiniert mit NAT.

#### RFC 1918

Der Aufwand zur Adressvergabe durch die IANA war enorm. Jedes Gerät, welches eine IP-Adresse hat, konnte auch direkt mit dem Internet kommunizieren. Rechnernetze wollten weiterhin über IP-miteinander kommunizieren, doch Teil eines grossen Netzwerks zu sein, hatte auch Nachteile. RFC 1918, beschreibt in seinem Dokument, die Wahl von IP-Adressen welche nicht durch eine zentrale Einheit, wie die IANA vergeben werden dürfen und somit für eigenständige Netzwerke ohne Internetzugriff verwendet werden können. Man unterteilte die ausgeschlossenen Adressbereiche in vordefinierte Klassen und setzze ihre Bereichsgrössen wie folgt um:

**Klasse A:** 10.0.0.0 - 10.255.255.255
**Klasse B:** 172.16.0.0 - 172.31.255.255
**Klasse C:** 192.168.0.0 - 192.168.255.255

Diese Bereiche dürfen durch jede Person ein eigenes Netzwerk bilden und müssen nicht mehr durch die IANA gesteuert werden, doch RFC 1918 beschreibt auch wie der Zugriff ins Internet gesteuert werden kann. NAT (Network Address Resolution) ist ein Weg wie private IP-Adressen mit einer öffentlichen IP-Adresse in einer Tabelle übersetzt werden kann. Das Prinzip seit RFC 1918 wurde wie folgt aufgebaut: Jeder Haushalt oder eine Firma müssen nun nur noch eine öffentliche IP-Adresse besitzen und alle Endgeräte hinter dem Internet Router bsitzen nun private IP-Adressen. Beim versenden von IP-Paketen ins Internet, wird nun die private IP-Adresse im Source-Adress Feld in die öffentliche IP-Adresse des Internetrouters umgeschrieben. Dabei trägt NAT die private IP-Adresse mit dem Quell-TCP/UDP Port ein um beim Empfangen der Antwort die Assoziation zum internen Endgerät nicht zu verlieren und schreibt neu im Destination-Header die eigentliche private IP-Adresse rein. So können alle Endgeräte in einem privaten Netzwerk trotzdem mit dem Internet kommunizieren und müssen keine öffentliche IP-Adresse mehr festlegen.

#### Die Zukunft

RFC 1918 konnte bekannterweise die Adressknappheit in die Mangel nehmen, doch am Ende reichen 2,147,483,647 IP Adressen auch nicht für das heutige Internet aus. Die obere Limite wird immer die 32 Bit Grösse einer IPv4 Adresse sein und lässt sich nur in die Länge zögern bis die Knappheit endgültig ein Problem darstellt. Internet Service Provider verwenden weltweit bereits Techniken zur Verwendung einer öffentlichen IP-Adresse für mehrere Haushalte mit CG-NAT oder versuchen durch das neuere und modernere IPv6 Techniker in den Wahnsinn zu werfen. Für die Verwendung des Internets an sich ist CG-NAT kein Problem, doch für Firmen die gerne ihre Dienste auch über das Internet erreichbar machen möchten, stellt dies meist neue Herausforderungen und IPv6 ist heutzutage immernoch nicht so weit im Umlauf und geniesst nicht denselben Ruhm wie IPv4. Man darf sich aber sicher sein, dass IPv4 noch lange weiterhin verwendet wird und somit immernoch als der Standard für die Kommunikation im Internet sein wird.

## Verwendung von IP-Adressen und Subnetting

### Definition von IP-Adressparametern

Eine IP-Adresse ist eine Folge von 4x8 Bits oder 4 Bytes. Jedes Byte wird auch als Oktet in einer IP-Adresse beziechnet und werden mit einem Punkt voneinander getrennt. Mit diesem Wert kann die logische eindeutige Adresse für das Endgerät welches es verwendet, ergänz werden. Zusätzlich muss aber auch die _Subnetzmaske_ festgelegt sein. Die Subnetzmaske definiert die Grösse eines Netzwerks durch das setzen von Host und Netzbits (wir gehen weiter darauf ein in [Subnetz berechnen](#Subnetz-berechnen)). Die Definition der Subnetzmaske ist wichtig. So weiss ein Hostsystem ob ein IP-Paket nun von einer privaten IP-Adresse in der selben Broadcast-Domäne senden muss oder ob das Paket an den Default Gateway gesendet werden muss, damit dieser das Paket ins richtige Zielnetz routen kann.

![Adaptereinstellungen IPv4 Windows](https://support.flir.com/Answers/A3666/6.PNG){align=right width=500}

Rechts im Beispiel sieht mann die einzelnen Felder für die Definition der IP-Adresse (A) und der Subnetzmaske (B). Der Default Gateway ist ein optionaler Parameter und muss nicht angegeben werden.

Mit der Angabe von 192.168.1.205 und der Subnetzmaske 255.255.255.0 können wir sagen, dass dieser Host die IP-Adresse 192.168.1.205 hat und mit Geräten im Netzbereich zwischen 192.168.1.0 - 255 miteinander direkt kommunizieren kann, ohne dabei die Broadcastdomäne zu verlassen. Doch wie kann man diese Aussage auch beweisen.

#### Subnetz-berechnen

Eine IP-Adresse ist eine Abfolge von 4 Bytes. Das heisst wenn wir die IP-Adresse von dezimal auf binär umschreiben würden würde das so aussehen:

> [!ERROR] Binär zählen von Vorteil
> Damit du auch alles verstehen kannst, was in diesem und weiteren IP-basierten Beispielen passiert, muss umbedingt dein Wissen zum Binärzählen vorhanden sein. Falls du gerne mehr darüber wissen möchtest oder wieder dein Binärwissen auffrischen möchtest, kannst du gerne [hier](https://youtu.be/OkcVk_PGYL4?si=aJ5bgdmV9OR7A4QW) entspannt ein Kaffee geniessen eine kurze Pause einlegen.

| Dezimal       | Binär                               |
| ------------- | ----------------------------------- |
| 192.168.1.205 | 11000000 10101000 00000001 11001000 |

Da die Subnetzmaske auch nicht fehlen darf nun auch die Berechnung der Subnetzmaske.

| Dezimal       | Binär                               |
| ------------- | ----------------------------------- |
| 255.255.255.0 | 11111111 11111111 11111111 00000000 |

Die Subnetzmaske wird in der Weise wie diese gezählt wird anders gehandhabt, als eine IP-Adresse. Eine Subnetzmaske darf nur durchgängig durch 0 oder 1 gefüllt sein und keine Wertänderung in der Kette bilden. Eine Subnetzmaske von 255.255.255.211 wäre in diesem Fall nicht gültig, denn die binäre Einheit würde somit 11111111 11111111 11111111 11010011 bilden. Die klare Trennung zwischen 1 und 0 definiert 2 Bereiche für die Netzwerkerkennung. 1 definiert die _Netz-Bits_ und die 0 die _Host-Bits_. Die Host Bits definieren damit die Anzahl an verfügbaren IP-Adressen in einem Subnetz und die Netzbits bezeichen dass Netzwerk in dem man sich befindet. Bei einer Subnetzmaske von 255.255.255.0 können somit 254 Hosts adressiert werden. Das Netz wäre somit 192.168.1.0. Wieso dass wir nicht von 256 Hosts sprechen, hat 2 Gründe. Die erste Adresse in einem Netzwerk darf nicht verwendet werden. Diese Adresse nennt man die Netz-ID und entspricht immer der ersten Adresse in einem Netzwerk. Die letzte Adresse wurde für Broadcast reserviert um Pakete an alle Geräte in einem Netzwerk zu senden. Ein eigenständiges Netzwerk wird meist aus einer Kombination aus Netz-ID und Subnetzmaske repräsentiert und zeigt auf einem Blick in welchem Bereich das Netzwerk und welche Grösse dieses Netzwerk hat. Anhand des obigen Beispiels kann gesagt werden, dass man sich in einem 192.168.1.0/24 Netz befindet.

> [!INFO] CIDR Notation
> Da eine subnetzmaske immer aus durchgängigen 1 und 0 geschrieben wird, kann für eine verkürzte Form der Subnetzmaske auch die CIDR Notation verwendet werden. CIDR steht für Classes Inter-domain Routing und beschreibt die eigentliche Aufteilung von IP-Adressen in Blöcke. Ein klassisches Netzwerk aus Netz-ID 192.168.1.0 und Subnetzmaske 255.255.255.0 kann somit einfacher mit 192.168.1.0/24 beschrieben werden, da die Anzahl an Netzwerk-Bits (Binär 1) genau 24 entspricht. In diesem Workshop wird noch häufig auf die CIDR Notation gesetzt, da diese Schreibweise zielführender und kompakter daher kommt.

Der Standard Gateway, im Netzwerk auch next-hop-router genannt, ist der nächste sich im selben Netzwerk befindende Router im Netzwerk. Der Standardgateway muss zwingend ein Router sein und dient der IP-Adressierung in andere Netzwerke, wie zum Beispiel dem Internet. Damit aber IP-Pakete an den Standardgateway zum weiterleiten in andere Netzwerke geschickt werden können, muss folgendes Kriterium erfüllt sein:

- Die Ziel-IP-Adresse darf sich nicht im selben Subnetz befinden wie die Quell-IP-Adresse

Wie kann ein Endgerät nun errechnen ob sich die Ziel-IP-Adresse nun im selben Netzwerk oder in einem anderen Netzwerk befindet? Anhand der eigenen IP-Adresse und der Subnetzmaske.

##### Erklärung

**Quell-IP:** 192.168.6.9
**Subnetzmaske:** 255.255.255.0
**Ziel-IP:** 192.168.21.56

|               | Oktet 1                                    | Oktet 2                                    | Oktet 3                                                                    | Oktet 4  |
| ------------- | ------------------------------------------ | ------------------------------------------ | -------------------------------------------------------------------------- | -------- |
| Quelle:       | <span style="color: green">11000000</span> | <span style="color: green">10101000</span> | <span style="color: green">00000110</span>                                 | 00001001 |
| Subnetzmaske: | <span style="color: blue">11111111</span>  | <span style="color: blue">11111111</span>  | <span style="color: blue">11111111</span>                                  | 00000000 |
|               |                                            |                                            |                                                                            |
| Ziel:         | <span style="color: green">11000000</span> | <span style="color: green">10101000</span> | <span style="color: green">000</span><span style="color: red">10101</span> | 00111000 |

![XOR Operation](data:image/png;base64,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){align=right}

Bei der Entscheidung ob nun ein IP-Paket im selben Netzwerk versendet wird, oder ob das Paket an den Standard-Gateway weitergeleitet wird, wird mit XOR die Gleichheit von Bits anhand einer Maske errechnet. Die Subnetzmaske (blau) definiert mit jedem 1 in der Kette die Länge der XOR Operation. Das heisst es werden 24 einzelne Bits in einer Reihe zwischen Quelle und Ziel verglichen. XOR gibt bei einer Kombination aus 2 gleichen Zuständen eine 0 raus und bei ungleichen Zuständen eine 1. Wenn also während eines Bitvergleichs nur einmal eine 1 als Resultat ausgegeben ist (rot), weiss der Rechner sofort dass die Zieladresse nicht im selben Subnetz ist und leitet das IP-Paket direkt an den Standardgateway. Mit der XOR Berechnung lässt sich somit innert schnellster Zeit die Zuweisung des IP-Pakets feststellen und ist auch der Grund wieso Router so schnell und effizient IP-Pakete innert weniger einer Millisekunde an das richtige Netzwerk übertragen kann.

Gratuliere du hast erfolgreich Subnetting angewendet.

### IP Routing

Ein Router ist in einem Layer-3 Netzwerk das Bindeglied zwischen mehreren Netzwerken. Mit diesem Satz definieren wir schon grundlegend folgende Kriterien:

- Ein Router muss sich mindestens in 2 Netzwerken gleichzeitig befinden
- Ein Router besitzt für jedes Netzwerk eine IP-Adresse
- Ein Router muss mindestens eine Schnittstelle zu jedem Netzwerk besitzen

In einem Router wird mit einer Routing Tabelle operiert. In der Routing Tabelle sind folgende Felder vorhanden:

- Zielnetzwerk
- Next-Hop-Router zum Zielnetzwerk

Eine Routing-Tabelle sieht dementsprechend wie folgt aus:

Der Router in diesem Beispiel hat die Adresse 192.168.1.2

| Zielnetzwerk     | Next-Hop (Gateway) |
| ---------------- | ------------------ |
| 192.168.2.0/24   | 192.168.1.1        |
| 192.168.3.128/25 | 192.168.1.1        |
| 0.0.0.0/0        | 58.12.13.124       |

Die ersten beiden Einträge sind für 2 andere interne Netzwerke welche sich hinter einem anderen Router mit der Adresse 192.168.1.1 befinden. Der letzte Eintrag ist eine spezielle Regel und trifft meistens im letzten Fall ein, wenn keine passende Route für eine Adresse gefunden wird und ist auch die Definition eines Standard-Gateways. Mit 0.0.0.0/0 wird angezeigt dass alle IP-Pakete welche nicht ans selbe Subnetz gehen oder eine vordefinierte Route besitzen einfach an den Next-Hop-Router weitergeleitet werden. Sozusagen der Standard-Gateway eines anderen Standard-Gateways. 

Nicht nur Router können IP-Routen anlegen, auch PC-Clients, Firewalls und sonstige Layer-3-bewusste Geräte haben die Möglichkeiten eine Route zu definieren. Dabei hängt die Implementation stark von den Tools ab, welche mit diesen Systemen herumkommen. 
