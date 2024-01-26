+++
title = 'Wi-Fi'
date = 2024-01-26T15:26:23+01:00
draft = true
+++

WIFI - auch bekannt als [IEEE 802.11](https://de.wikipedia.org/wiki/IEEE_802.11) schaffte die Standartisierung der Funkübertragung in einem Ethernetfähigen Netzwerk. Technisch gesehen ist 802.11 eigentlich eine Layer 1 Spezifikation, schafft aber so auch eine Schnittstelle für die Ethernet Kommunikation auf Layer 2. Darum bekommt WIFI ein eigenes Kapitel, welches näher den Fokus auf praktische Tipps und die technischen Aspekte der elektromagnetischen Eigenschaften setzt.

## Geschichte zu IEEE 802.11

IEEE 802.11 ist eine Normenfamilie für [WLAN](https://de.wikipedia.org/wiki/Wireless_Local_Area_Network). Die Normen beschreiben den Zugriff auf ein Netzwerk auf Basis von Luftübertragungsmedien, im spezifischen mit elektromagnetischen Wellen. 1997 wurde die erste Norm veröffentlicht und seit 2018 wurden spezifische Branchenbeziechnung _WIFI 4_, _WIFI 5_ und _WIFI 6_ zur Vereinfachung der Vermarktung eingeführt. In den Normen werden die Verfahren beschrieben mit welche Daten über EM-Wellen moduliert werden und über Multiplexingverfahren für Mehrkanalübertragungen, sowie die Festlegung der Frequenzbänder. Bekannte Modulationsverfahren sind heutzutage:

- OFDM (Orthogonal Frequency-Division Multiplexing)
- OFDMA (Orthogonal Frequency-Division Mutiple Access)
- DSSS (Direct Sequence Spreac Spectrum)

Speziell den Fokus legen wir hier auf OFDM bzw. OFDMA.

## Normen im Detail

![WIFI Certified Bild](https://upload.wikimedia.org/wikipedia/commons/4/48/Wifi_certified_logo.png){width=300 align=right}

Die verschiedenen Unternormen zu IEEE 802.11 sind über die Jahre entstanden und die heutigen Normen haben möglichst versucht die Rückwärtskompatibilität zu älteren Normen beizubehalten, doch einige Aspekte mussten in Folge von technischen Durchbrüchen durch neuere Modulationsverfahren, schenllere Übertragungsraten oder besseren Sicherheitsanforderungen standhalten. Firmen welche ihre Endgeräte WLAN-tauglich verkaufen wollen, müssen sich an die Zielnormen halten und können sich bei der Zertifizierung sogar als _WIFI Certified_ beziechnen. Die klassischen IEEE 802.11 Standards wurden seit 2018 mit ihren einfachen Versionsnamen für die breite Masse übersetzt.

Mit den verschiedenen Frequenzbändern, vorallem in neuen WLAN-Netzwerken, kann die Kompatibilität für ältere oder sendearme Endgeräte auf ein 2.4GHz Band festgelegt werden und die Endgeräte mit erhöhtem Datenverkehr mit dem schnelleren 5 GHz Frequenband verbinden. Die Übertragung erfolgt auf den beiden Frequenzbändern separat, da die Übertragung in den meisten Fällen über separate Antennen ausgestrahlt werden.

### Sender und Empfänger

In den letzten Jahren sind die Anzahl an WLAN fähigen Geräten stark gestiegen. im Jahr 2022 wurden 4.4 Milliarden Endgeräte welche durch die WIFI-Alliance zertifiziert wurden weltweit verkauft. Seit beginn der WIFI-Alliance im Jahr 1999 wurden bislang 18 Milliarden WLAN-fähige Geräte verkauft. Die meisten dieser Geräte bilden Empfängergeräte. Doch die Anzahl an Sendegeräten steigt stark weiter. Manche Geräte bieten ja sogar die Funktionalität für Senden oder emfpangen von WLAN-Signalen (Smartphones, etc.), somit ist die klare  Unterscheidung der Spezifikationen für Sender und Empfängergeräte und deren Unterschiedliche Implementation wichtig. Man sollte in diesem Fall klar unterscheiden zwischen dem eigentlichen Senden und Empfangen von Daten und der eigentlichen Funktionalität eines WIFI-konformen Endgeräts. Beide Endgerätetypen können Senden und Empfangen, vorgesehen sind sie aber für andere Dienstzwecke. Aber nur Sendegeräte strahlen aktiv WLAN-Signale aus, die anderen Endgeräte übertragen nutzen das bestehende Signal als Träger für Nutzdaten.

Auch WLAN fähige Geräte besitzen eine oder mehrere MAC-Adressen, unabhängig ob diese nun Sender oder Empfänger sind. Empfängergeräte sind die Schnittstelle zu einem Layer-2 Netzwerk für Ethernet und Empfängeräte können dann über die Sendeübertragung über diese Umwandlung mit über Ethernet auf Netzwerkgeräte im gesamten Netzwerk sich verbinden. 

#### Sender

Fast überall wo ein Gebäude, ein Kampus, oder ein Haus steht, wird sicher mit WLAN ein kabelloses Netzwerk seinen Platz haben. Die Art und Form wie die WIFI-Landschaft aufgabaut ist, kann sehr unterschiedlich umgesetzt sein. In einer Wohnung oder bei kleineren Betrieben, können bekannterweise Internetrouter schon die Funktion eines WLAN-Senders übernehmen. Bei grösseren Flächen und komplexeren Bauten werden meistens mit WLAN Access Points oder Repeater gearbeitet und eine genügende örtliche Abdeckung zu gewährleisten. Access Points und Repeater werden über ein normales kabelgebundenes Netzwerk betrieben und besitzen eine eigene Stromversorgung. Für die Stromversorgung kann entweder ein separates Netzteil verwendet werden oder über Switches mit [PoE](../01_Physical_Layer/Power_over_Ethernet.md) Funktionalität über das bereits verwendete Netzwerkkabel mit Strom versorgt werden. Mittels einem über den Access Point zur Verfügung gestellten Webinterface können die Einstellungen wie [SSID](#SSID), Übertragungsfrequenzen und Frequenzbänder und weitere Paramter angepasst werden. Bei einer Vielzahl an WLAN-Sendern ist es wichtig dass alle Sender zentral verwaltet werden. Bei industriellen WIFI-Produktelinien kann in diesem Fall ein WLAN-Controller bei der Verwaltung eine Hilfe sein. Dies sind herstellerabhängige Merkmale und müssen somit für den Einsatz möglichst richtig evaluiert werden.

#### Empfänger

Die klassischen Empfängergeräte heutzutage können kurz zusammengefasst werden in: 

- Smartphones
- Notebooks
- Tablets
- Wearables (Smartwatch, etc.)
- TV

Doch auch schon in den Bereichen von IoT wird häufiger auf WLAN gesetzt. Empfängergeräte können klassischer Weisse als Verbraucher in betrachtet werden und sorgen nicht für die Ausstrahlung von WLAN-Netzwerken, nutzen daher die bestehenden ausgestrahlten Signale zur Datenübermittlung. Somit sind Empfängergeräte von einem ausgestrahlten WLAN-Netzwerk abhängig. Ausgestrahlte Netzwerke können dann von Empfängergeräten aufgenommen werden und mittels Authentifizierungsverfahren mit diesem ausgestrahlten WLAN-Netzwerk verbunden werden. 

## Technische Aspekte für die Integration und Inbetriebnahme

Nun genug von Normen. Unabhängig wie stark die Ausstrahlung oder ob der Access Point WIFI-6 tauglich wäre oder nicht, gibt es klare Parameter, Ausdrücke und Definitionen welche auf ein WLAN-Netzwerk zutreffen und mit unseren Endgeräten verwendet werden kann um ein WLAN Netzwerk herszustellen, sich damit zu verbinden und die Verbindung sicherzustellen. 

Ein WLAN-Netzwerk hat folgende technische Eigenschaften:

- Ein WLAN kann nur in einer Broadcast-Domäne sein
- Ein WLAN besitzt eine SSID => ausgestrahlte Identifikation des ausgestrahlten Netzwerks
- Ein WLAN _kann_ Passwortgeschützt sein. Bekannte Authentifizierungsverfahren sind WPA2, WPA3, WPA-Enterprise
- Ein Access Point kann auch mehrere WLANs austrahlen und mit diesen WLANs in mehreren Broadcastdomänen sein => siehe [VLAN]()