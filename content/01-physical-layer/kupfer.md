+++
title = 'Kupfer'
date = 2024-01-26T15:20:56+01:00
draft = false
+++

Kupfer hat sich in der heutigen Zeit als schnelles Übertragungsmedium etabliert. Sie bieten kostentechnisch den besten Mehrwert und bieten durch ihre physikalische Beschaffenheit stabilität vor Stössen und Rissen. Physische Limitationen sind heute fast nicht zu erkennen, obwohl doch einige dieser Nachteile stets vorhanden sein werden. Noch mals kurzaufgeführt die wichtigsten Merkmale von Kupfer als Übertragungsmedium:

- Unkompliziert in der Anwendung und Verarbeitung
- Sicher for Stössen und anderen physischen Ausseneinflüssen
- Gute Übertragsunlängen je nach Kabeltyp (z.B. 100m bei Twisted Pair)
- Kann durch elektromagenische Stöfelder belastet werden

## Twisted Pair Verbindungen

Twisted-Pair-Kabel bestehen aus zwei oder mehr Adern, die miteinander verdrillt sind. In einem klassischem UKV/EDV Kabel sind meistens 4 Aderpaare vorhanden und sind gemäss ISO/IEC 11801 genormt.

![Twisted-Par Kabel](https://cdn.shopify.com/s/files/1/1268/5407/files/Balanced_Twsited_Pair_Cable.jpg?v=1572455526)

### Wissenschaft dahinter

Die Verdrillung hat zwei wesentliche Vorteile:

Sie verringert das Übersprechen zwischen den Adernpaaren.
Sie bietet einen besseren Schutz vor elektrischen und magnetischen Störfeldern.
Das Übersprechen entsteht, wenn sich die elektrischen Felder zweier Adern überlagern. Dies kann zu Signalstörungen führen. Die Verdrillung der Adernpaare verringert das Übersprechen, indem sie die elektrischen Felder der beiden Adern in entgegengesetzte Richtungen lenkt.

Die Verdrillung bietet auch einen gewissen Schutz vor elektrischen und magnetischen Störfeldern. Elektrische Störfelder können sich durch die Verdrillung der Adern nicht so leicht übertragen. Magnetische Störfelder können die Verdrillung der Adern ebenfalls beeinflussen, aber der Effekt ist in der Regel geringer als bei parallel geführten Adern.

Bekannte Kabel mit Twisted Pair Drähten sind:

- UKV/EDV Verbindungen und deren Patchkabel
- analoge und digitale Telefonleitungen

### Kategorien und Klassen bei UKV/EDV Verbindungen

UKV Kabel weisen immer die Kategorie des Kabels auf. Die Kategorie beschreibt die technische Spezifikation einer Komponente in Zusammenhang mit der Erstellungsqualität eines solchen Kabels. Die Normen für die Kategorien werden in [ISO/IEC 11801](https://fr.wikipedia.org/wiki/ISO/IEC_11801).

Der Unterschied von Klassen und Kategoerien geht wie folgt:

- Klassen beschreiben das gesammte Kabel von Ende zu Ende
- Kategorien beschreiben die einzelnen Komponenten in einem Kabel, kann aber wenn alle Komponenten gleichwertig sind auf das Kabel mittels Klassen übertragen werden

### Schirmung

Da Twisted Pair Kabel den natürlichen Gesetzen des Elektromagnetismus ausgesetzt sind, können äussere Störeinflüsse die Qualität des Signals stark beinträchtigen. In vielen industriellen Gebeiten werden heutzutags nur noch geschirmte Twisted Pair Kabel verwendet. Denn diese bieten folgende Vorteile gegenüber nichtgeschirmten Kabeln:

- Das Übersprechen zwischen Kabeln wird verringert
- elektromagnetische Interferenzen vom Kabel werden andere Kabel schächer weiterübertragen

Folgende Formen von geschirmten Twisted-Pair Verkabelungen sind möglich

- Schrimung mit Folie
- Schirmung mit Drahtschirmen

Kabelbezeichnung werden von Herstellern somit in folgender Form kombiniert

- TP für Twisted Pair
- S für Schirm (drahtgeflecht)
- F für Schirm mit Folie als Mantel

Diese Bezeichnung werden dann zusammen zu einer Bezeichnung der Charakteristik angewandt. Ein Kabel welches als FTP-Kabel verkauft wird, besitzt dabei für jedes Aderpaar eine Folie zur Schirmung. ein S/FTP bietet zusätzlich ein drahtgefelcht um alle Aderpaare für eine zusätzliche Abschirmung.

### Vorteile

Das Prinzip von UKV/EDV hat sich heutzutage etabliert und das Rad muss somit nicht neu erfunden werden. Mit heutigen Patchkabeln und UKV-Verkabelungen der Kategorie 6a lassen sich schon Verbindungen für 10Gbit/s realisieren. Handelsübliche Netzwerkgeräte unterstützden die Steckerarchitektur mit RJ45 schon seit anbeginn der ersten Ethernetfähigen Swtiches und Routern und wird auch in den nächsten Jahr seinen Stellenwert für Netzwerke nicht verlieren.

Folgendes sind Vorteile für eine Twisted-Pair Verkabelung:

- Kostengünstige Anschaffungskosten
- Kompatibel mit den meisten Netzwerkgeräten
- Installation der Kabel ist einfacher

## Koaxiale Verbindungen

Koaxiale Kabel sind 2 polige Kabel mit einem einfachen Aufbau. Einem Innenleiter und einem Aussenleiter. Dieser Aufbau ist konzenrisch, d.h. die Auslagerung der Verbindungen vom Zentrum gesehen immer symmetrisch aufgebaut ist.

![Koaxiales Kabel - Aufbau](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7c/Coaxial_cable_cutaway_new.svg/330px-Coaxial_cable_cutaway_new.svg.png){align=right}

Folgend ein kurzes Aufbauprinzip:

1. Innenleiter
2. isolierendes Dielektrikum
3. Aussenleiter und Abschirmung
4. Schutzmantel

Zu beachten ist, dass im Falle eines Koaxialkabels der Aussenleiter gleichzeit als Schirm verwendet wird.

### Vorteile

Durch den erhöhten Abstand des Aussen- und Innenleiters durch das Dielektrikum sind Störeinflüsse durch elektrische Felder einfacher geschützt und mit dem Aussenleiter als Schirm werden elektromagnetische Interferenzen zusätzlich abgefangen. Durch den Aufbau sind Koaxiale Verbindungen vorallem bei hochfrequenten Verbindungen beliebt. Bei manchen Kabeltypen sind sogar Frequenzen von 110GHz möglich. Somit können Internetprovider welche über Koaxiale Verbindungen ihre Infrastruktur für ihre Kunden zur Verfügung stellen trotz der Limitationen von Kupferverbindungen, schnelle Bandbreiten für ihre Kunden anbieten.
