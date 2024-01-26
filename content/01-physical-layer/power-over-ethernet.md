+++
title = 'Power Over Ethernet'
date = 2024-01-26T15:22:15+01:00
draft = false
+++

Power over Ethernet bezeichnet das Verfahren mit dem das Ethernet-Kabel mit dem das Netzwerkendgerät angeschlossen ist, zur Stromversorgung verwendet wird. Der Standard IEEE 802.3 (Ethernet) hält die Vorgaben und die Implemenetation für Hersteller und Anwender fest und besitzt weitere Normierungen. Darunter zählen die Standards 802.3at, 802.3af und neu auch 802.3bt zu den Power over Ethernet Substandards mit welchen Leistungsangaben, Speisungsart und sonstiges spezifiziert werden.

Einsatzmöglichkeiten sind VoIP Telefone, IP-Videokameras, kleine Switches, WLAN Access Points und vieles weitere. Dabei kann man davon ausgehen, dass meistens mit wenig Leistung am Endgerät zu rechnen ist. Für die meisten PoE Anwendungen wird mindestens eine 4-drähtige Verbindung vorausgesetzt (100Base-T), ist seit der Entstehung aber auch für wollwertige Verkabelungslösungen vorgesehen (> 1000Base-T) und wurde abwärtskompatibel gehalten.

## Voraussetzungen und Spezifikation für Power over Ethernet

Eine Herausforderung stellt sich vorallem in den Kabelspezifikationen um eine saubere PoE Spannung ans Endgerät zu bekommen und sicherzustellen dass die Datenübertragung weiterhin bestehen bleibt.

Es gibt zurzeit 3 PoE Standards:

| Standard      | Leistung am Versorgenden Gerät | Leistung am Endgerät | Benutzte Aderpaare |
| ------------- | ------------------------------ | -------------------- | ------------------ |
| PoE 802.3af   | 15.4 W                         | 12.95 W              | 2                  |
| PoE+ 802.at   | 30 W                           | 25.5 W               | 2                  |
| PoE++ 802.3bt | 45, 60, 75, 90 W               | 40, 51, 62, 71       | 4                  |

Die Ausgangsspannung variieren zwischen 36 - 57 Volt je nach Standard. PoE setzt je nach Standard auf eine Spare pair oder Phantom pair Speisung.

### Spare Pair

Bei einer Versorgung mittels Spare Pair, wird die Speisung über nicht verwendete Drähte. Dies war früher meistens der Fall, da bei 100 Mbit nur 2 Aderpaare verwendet wurden.

### Phantom Pair

Bei einer Versorgung mittels Phantom Pair werden bestehende Datenleitungspaare auch für die Stromversorgung verwendet. Diese Art der Übertragung wird heute in den meisten Fällen verwendet, da Gigabit-Ethernet falls überall anzutrefen ist und mit dem neueren PoE++ sogar unumgänglich, da alle 4 Aderpaare verwendet werden müssen, wo ja schon auf allen Paaren übertragen wird. PoE++ wird meist sogar als 4PoE beziechnet.

### Kabelspezifikation

Die höhere Stromstärke stellt auch die Datenverkabelung vor Herausforderungen. Da höhere Ströme durch die Datenverkabelung fliessen (ca. 400 - 600mA), müssen diese auch für solche Ströme ausgelegt sein. Somit muss ein höherer Querschnitt eingerechnet werden und wurde seitdem in die ISO Norm aufgenommen.

Für die verschiedenen Kategorien hat man sich auf folgende [AWG](https://blog.tripplite.com/whats-the-difference-between-24-awg-26-awg-and-28-awg-network-cables#:~:text=It%20stands%20for%20American%20Wire,used%20primarily%20in%20North%20America.) Querschnitte geeinigt. AWG ist die Beziechnung für American Wire Gauge und ist ein standartisiertes Grössensystem für die Querschnittsberechnung und die Darstellung für Datenkabel. Auf einem Datenkabel wird diese Grösseneinheit bevorzugt und zeigt einfach ausgesprochen den Querschnitt der einzelnen Adern in einem Datenkabel auf.

| Kategorie | AWG | Querschnitt pro Ader |
| --------- | --- | -------------------- |
| Kat 5/5e  | 24  | 0.51 mm              |
| Kat 6/6A  | 23  | 0.57 mm              |
| Kat 7/7A  | 22  | 0.64 mm              |

### Aktivierungsschritte für PoE

Die Speisung mittels PoE funktioniert in der Regel bei Switches automatisch und muss meist auch nicht weiter im Detail behandelt werden. Diese Aktivierungsschritte dienen lediglich zum Vorzeigen und zur Fehlersuche bei potenziellen Problemen mit Power of Ethernet.

Damit ein Endgerät überall mit PoE gespiessen werden kann hat man einen Widerstand eingebaut und mit diesem Widerstand in der Netzwerkschnittstelle des Netzwerkgeräts kann der PoE Netzteiladapter identifizieren ob dieses Endgerät nun eine Speisung benötigt oder nicht. So wird nur an den Ports PoE ausgegeben, welche tatsächlich mit PoE gespiessen werden müssen.

| Schritt          | Aktion                                                                 |
| ---------------- | ---------------------------------------------------------------------- |
| Detektion        | Feststellung ob das Endgerät einen Widerstand aufweist                 |
| Klassifikation   | Messen des genauen Widerstandwertes zur Identifizierung der PoE Klasse |
| Startup          | Eigentliche Stromversorgung aktivieren                                 |
| Normaler Betrieb | Stromversorung im Versorgungsmodus                                     |
