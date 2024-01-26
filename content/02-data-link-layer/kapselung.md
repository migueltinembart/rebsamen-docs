+++
title = 'Kapselung'
date = 2024-01-26T15:24:21+01:00
draft = false
+++

Eines der wichtigsten Konzepte, besonders wenn man mit allen Schichten in einem OSI-Model die richtige Herangehensweise verstehen kann wie aus den Daten welche zum Beispiel bei einem Webaufruf die Daten darstellen kann, muss mit dem Begriff der Kapselung angefangen werden. Die Kapselung beschreibt in kurzer Form wie Daten von verschiedenen Softwareschichten miteinander Daten austauschen können ohne die dabei zugrundeliegende Datenkapsel manipulieren zu müssen.

## OSI 7-Schichten Model

![OSI und TCP/IP Model](https://i.stack.imgur.com/FOfAU.jpg){align=right width=400}
Doch bevor die Kapselung verstanden werden kann muss das Grundgerüst der Netzwerkübertragung definiert werden. 1970 Musste ein gemeinsamer Kommunikatioinsstandard entwickelt werden um die Datenkommunikation zu vereinfachen und festzuhalten. Bis dahin haben Firmen mit proprietären Kommunikationstechnologien gearbeitet und es musste jedes mal neu verstanden werden wie die Kommuniation in einer Anlage definiert und aufgebaut ist. Dies führte zu Fehlern und verlangsamte die Entwicklung von neuen Kommunikationsmodellen. Das amerikanische Militär arbeitete zum Beispiel an ihrem [DoD Model](https://de.wikipedia.org/wiki/DoD-Schichtenmodell), wurde aber schnell vom OSI-Model ersetzt. Doch seit den 90er Jahren hat sich das TCP/IP-Model standardisiert. Das TCP/IP Model lehnt sich jedoch sehr start an das OSI Model und kann als Zusammenfassung von einzelnen Schichten im OSI-Model betrachtet werden.

Bei der Kommunikation zwischen den Schichten wird auf die Entkapsulation / Einkapselung gesetzt. So wird sichergestellt, dass die Daten zwischen den Schichten keinen Einfluss auf die Übertragung und deren Methoden hat und löst Abhängigkeiten ab. So kann zum Beispiel statt IPv4 auf IPv6 gewechselt werden, ohne dass das Ethernetprotokol sich mit den darin liegenden Daten befassen muss, da die Implementation für jede Schicht unabhängig ist.

Man kann sich das so vorstellen als würde man eine kleine Matrjoschka Puppe mit der eigentlichen Nachricht in eine grössere Matrjoschka Puppe hineinpacken und dies so weiterführen bis keine grössere Puppe mehr vorhanden ist. In jeder anderen Puppe stehen Instruktionen wie man zur nächsten Puppe gelangt. Bei der Übergabe der finalen Puppe muss die Gegenstelle anhand der Instruktionen alle Puppen auseinander **entkapseln** um zum Schluss die letzte Puppe mit der eigentlichen Nachricht auspacken. Das Zwiebelschalenprinzip kann in diesem Fall auch angewendet werden um den Begriff der Kapselung verstehen zu können. Das Problem dabei ist mehr, wie man die Schale wieder zusammenführt und sollte hier nicht noch näher behandelt werden.

### Beispiel

Man siehe ein Beispiel aus dem alltäglichen. Du gehst auf deinen Lieblingsbrowser und startest als erstes die Website von Google (https://google.com).
Sobald du ++enter++ drückst, durchläuft die Kommunikation alle 7 Schichten des OSI-Models, oder im Fall des TCP/IP Models alle 4 Schichten.

- **Layer 7 - Applikationsschicht:** Der Browser erstellt eine HTTP GET Anfrage an den Server auf https://google.com. Die GET-Anfrage möchte gerne die HTML-Seite und dessen Medien über die Anfrage aufrufen. Eine solche Anfrage kann kurz so zusammengefasst werden: _GET /, content-type: "text/html" HTTP/1.0_. Dies beschreibt in kurzer Form was der WebBrowser vom Webserver google.com möchte. Anschliessend wird die Anfrage, da es sich um https hält (hypertext transfer protocol secure), an Layer 6 weitergereicht wo die Daten verschlüsselt werden.

- **Layer 6 Präsentationsschicht:** Der SSL Dienst erhält von der darüberliegenden Schicht in der Applikation die GET-Anfrage. Die darunterliegenden Daten wurde schon bereitgestellt und muss nur noch verschlüsselt werden. Mit welchem Verfahren dies geschieht, wird mit anderen Anfragen an den selben Server aus dem Kontext der GET-Anfrage mit google.com abgehandelt und schlussendlich ausgeführt. Diese Anfragen, geschehen separat und durchlaufen die selben Schichten ab, wie die eigentliche Abfrage. Die eigentliche Anfrage wird in die SSL Prozedur **eingekapselt** und verschlüsselt. Danach werden die verschlüsselten Daten weitergereicht an die 5. Schicht.

- **Layer 5 Sitzungsschicht:** Bevor die Applikation die verschlüsselten Daten weiter in die Transportschicht übergibt, muss eine Sitzung für die Verbindung erstellt werden um die Verbindungungen in der Software assozieren zu können. Es ist ja möglich mit einer Applikation mehrere Verbindungen an verschiedene Dienste zu richten oder auch mehrere Programme können ja über die gleiche Hardwareschnittstelle kommunizieren ohne dass die Software von anderen Netzwerkverbindungen gestört werden kann oder dessen Daten einlesen kann. Mit der Sitzungsschicht wird schlussendlich sichergestellt, dass die richtige Dateninstruktion welches ins Betriebssystem über die unterliegenden Schichten 2-4 an die richtige Software übergeben wird.

- **Layer 4 Transportschicht:** Die eigentliche Applikation wird verlassen (der Web-Browser) und die darüberliegenden Daten aus der Sitzungsschicht wurden erreichen die Transportschicht. Zur Zuordnung der Daten einer Applikation im Rechner müssen diese Daten adressiert werden. So weiss der Rechner von welcher Applikation gesendet und empfangen wird. Die darüberliegende Applikation öffnet einen Port und beschreibt das Protokolverfahren mit welchem die Datenintegrität sichergestellt wird. Üblich wird bei HTTP Anfragen mit TCP (Transmission Control Protocol) die Integrität sichergestellt. Ausserdem wird ein Zielport für die Übertragung definiert. Mit dieser weiss der Empfängerrechner an welche Applikation die Anfrage gerichtet wird. Nach dem die Daten in ein TCP Segment eingekapselt wird, gehts weiter zur nächsten Schicht. Layer 3 über das IP-Protokol

- **Layer 3 Netzwerkschicht:** TCP übergibt seine bereits enkapsulierten Daten weiter an die zuständige Netzwerkkomponente und Führt seine Headerinformationen an die übergeordneten Daten. Die Sender und Empfänger IP-Adresse wird an die gekapselte Information angeführt und wird als IP-Paket weitergereicht an die zweite Schicht. Dem Ethernet Frame.

- **Layer 2 Data-Link-Schicht:** Das IP-Paket wird an das Ethernetprotokoll eingegliedert. Die Mac Adresse der benachbarten Netzwerkschnittstelle wird als Destination weitergereicht und die eigene Mac Adresse wird als Source eingetragen. Am Ende wird von allen Daten im Ethernet Frame noch eine CRC Checksumme ausgerechnet und somit übernimmt die Netzwerkkarte dann das Modulieren des Frames in Bits und die Übertragung auf das Kabel erfolgt.

In dieser Abbildung wird der Prozess simpler dargestellt
![Encapsulation and de-encapsulation](https://afteracademy.com/images/what-is-data-encapsulation-in-networking-process-148532037a490a19.jpg)

In den weiteren Kapiteln wird näher auf die Protokolspezifische Implementation der Kapselung eingegangen, da jede Schicht mit ihren Protokollen anders mit dem Verfahren umgehen.
