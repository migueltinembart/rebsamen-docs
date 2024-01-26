+++
title = 'Spanning Tree'
date = 2024-01-26T15:25:50+01:00
draft = false
+++

Spanning Tree ist ein eigenes Protokol zum Austausch von Schleifenbildungen in geswitchten Umgebungen. Das Ziel von Spanning Tree ist es anhand von Gewichts und Stammangaben der Switches einen eindeutigen Pfad du definieren und eventuelle Schleifen im Netzwerk zu identifizieren und sich davor zu schützen. Hauptsächlich aber verwendet man Spanning Tree zur Redundanzabsicherung in einem Netzwerk ohne, dass sogenante Broadcast-Loops entstehen können.

Ziel von Spanning Tree ist immer den Zustand eines Baumes zu erhalten. Äste auf einem Baum wachsen schliesslich auch nicht zusammen. Wenn ein Loop entdeckt wird, verwendet Spanning Tree einen Mechanismus um den Port auszuschalten und die Baumstruktur intakt sicherstellt.

> [!INFO]- Was sind Broadcast Loops
> Wenn man bei einem Netzwerkswitch von einem Port zum anderen ein Patchkabel einsteckt, entsteht ein Broadcast-Loop. Der Broadcast Loop entsteht weil im ersten Moment wenn ein Netzwerkgerät angeschlossen wird ein, Ethernet-Broadcast Frame ausgesandt wird. Dieses Frame wird an jedem Port ausgesandt, ausser bei dem Port von dem die Broadcastnachricht gesendet wurde. Bei einer Verkettung von Switches wird dies bei jedem Switch auch wiederholt bis diese Broadcast Frames an jedem Port ausgesandt wurde. Bei einem Loop würde dieses Frame auch immer wieder ausgesandt werden, da aus der Sicht des Switches ein neues Broadcast-Frame verschickt wurde und er seiner Aufgabe als Switch nachgehen möchte und diese wieder an alle Ports hinausflutet. Dieses Problem wiederholt sich so lange bis keine weiteren Nachrichten über die Switches mehr ausgesandt werden können und es zu einem Ausfall der Netzwerkkomponenten kommen kann.

## Basics

### Formen von Spanning Tree

Spanning Tree gibt es in mehreren Varianten. Meistens werden diese in ihrer Kurzform names STP unter Netzwerkadministratoren ausgetauscht.

Folgende Formen von STP kann man in der Wildnis antrefen:

- STP (Spanning Tree Protocol)
- RSTP (Rapid Spanning Tree Protocol)
- MSTP (Multiple Spanning Tree Protocol)
- PVST (Per Vlan Spanning Tree - Cisco Proprietär)
- CST (Common Spanning Tree)

Die meisten Netzwerke verwenden in der Regel eine Form von STP/RSTP oder bei grösseren komplexeren Netzwerken auf der man per VLAN einen eigenen Spanning Tree aufbauen möchte MSTP/PVST

### Protokolloperation

Zwei Wichtige Begriffe sind für Spanning Tree wichtig um zu verstehen was eingestellt werden muss um ein einfaches durch Spanning Tree geschütztes Netzwerk richtig zu implementieren. **Path cost** und **root bridge**. Spanning Tree ist ein eigenes Protokoll, welches in einem Layer-2 Netzwerk Verwendung findet. Spanning Tree versucht immer Loops zu identifizieren, da jeder Port welches mit einem anderen Spanning Tree tauglichen Switch verbunden ist als aller erstes über das Spanning Tree Protokol **BPDUs** aussendet um die root bridge zu definieren. In einer Spanning Tree Landschaft darf es immer nur eine Root Bridge geben. Denn dieser Switch hat als einziger Switch keinen Port, welches über STP ausgeschaltet werden kann.

#### Path cost

![Kruskal Algorithmus](https://he-s3.s3.amazonaws.com/media/uploads/6322896.jpg){align=right width=300}

Spanning Tree definierte ein paar Regeln für den sauberen Aufbau eines Spanning Tree. Jeder Switchport hat Kosten hinterlegt, die sogenannte Path cost. Die Kosten werden anhand der Geschwindigkeit des Ports meist automatisch errechnet, können aber auch selber definiert werden. In der Regel teil man die Kosten nach der Geschwindigkeit des Ports auf, so nach der Regel umso länger und beschwerlich der Weg, umso mehr Kosten entstehen auf dem Weg. Somit müsste ja der schnellste Weg, der kürzere und Kostenunaufwendigere Weg dafür genutzt werden. Mit der Kostendefinition von Ports können somit Kalkulationen erstellt werden um den kürzesten Weg zu einer RootBridge herstellen zu können. hier mal ein Beispiel mit dem Kruskal Algorithmus wie die Kosten Einfluss auf ein Spanning Tree haben kann:

In diesem Beispiel sieht man wie alle Knoten miteinander verbunden sind. Alle Knotenverbindungen definieren ihre Kosten mit einer Zahl, dabei spielt die Distanz zu den anderen Knoten hier überhaupt keine Rolle. Nun sollten alle Knoten über den günstigsten Weg miteinander verbunden werden. So können wir eine gespannte Baumstruktur zwischen allen Knotenpunkten herstellen. Bei Spanning Tree würden somit nur die Leitungen aktiv erhalten bleiben welche für eine _nicht-kreisförmige_ Konstellation benötigt werden.

Die IEEE standardisierte die Pfadkosten für Ports anhand der Übertragungsgeschwindigkeiten. Schnellere Ports kosten weniger, langsame Ports kosten mehr. Hier eine Abbildung der von der IEEE802.X definierten Path Cost:

| Bandbreite | Originale STP Kosten IEEE802.1D | Neue STP Kosten IEEE802.1w |
| ---------- | ------------------------------- | -------------------------- |
| 4 Mbit/s   | 250                             | 5'000'000                  |
| 10 Mbit/s  | 100                             | 2'000'000                  |
| 16 Mbit/s  | 62                              | 1'250'000                  |
| 100 Mbit/s | 19                              | 200'000                    |
| 1 Gbit/s   | 4                               | 20'000                     |
| 2 Gbit/s   | 3                               | 10'000                     |
| 10 Gbit/s  | 2                               | 2'000                      |
| 100 Gbit/s | N/A                             | 200                        |
| 1Tbit/s    | N/A                             | 20                         |

Beachte die alten Definitionen der Kosten gegenüber den Neuen Definitionen. Dies sind nur Vorgaben von IEEE und können auf jeden Fall für jeden Port angepasst werden um allenfalls die Baumkonstelation selbst anzupassen.

#### Root Bridge

![Rood Bridgke Konfiguration](https://www.prosec-networks.com/wp-content/uploads/2021/08/PSN_KB_spanning_tree.jpg){align=right width=400}

Die Root Bridge in einer Spanning Tree Konstellation ist der Switch mit der kleinsten Bridge ID. Die Bridge ID ein 8-Byte grosses Feld in einem BPDU Frame und wird aufgebaut aus der Priorität und der Mac-Adresse eines Switches. Die Root Bridge dient als Referenzpunk für alle anderen im Spanning Tree angeschlossenen Switches und dient als zentraler Ausgangspunkt eines Spanning Tree. Als einziger Switch in der Baumstruktur kann bei der Root Bridge kein Port mittels STP augeschaltet werden um die Redundanz sicherzustellen, ausser natürlich bei einem internet Loop. Eine Root Bridge wird in einem spanning tree Netzwerk mit einem Verfahren ermittelt. Die Root Bridge kann im Auschlussverfahren so definiert werden:

1. Hat der Switch die kleinste Priorität (4096), dann ist dieser Switch automatisch die Root Bridge in einem Spanning Tree
2. Falls >2 Switches die kleinste Priorität aufweisen, dann ist der Switch mit der kleinsten Priorität und der kleinsten MAC-Adresse die Root Bridge

#### Arten von Ports in einem Spanning Tree

Um zu verstehen wie die Switches in einer Spanning Tree Konstellation die auschzuschaltenden Ports definieren, müssen folgende Portdefinitionen erklärt werden:

- Designated Port
- Root Port
- Blocked Port

##### Designated Port

Dem designated Port ist es erlaubt Daten mit anderen Switches auszutauschen Frames weiterzuleiten. In einer Root Bridge sind alle Ports designated Ports und kann im Normalfall auch nicht geändert werden.

##### Root Port

Ein Root Port ist der Anschluss welches in Richtung einer Root Bridge geführt ist. Ein Root Port ist somit immer mit einem Designated Port verbunden. Der Zustand eines Root Ports startet immer in einem Listening State

##### Blocked Port

Ein Port welches nach der Spanning Tree Toplogie nicht für eine Verbindung vorgesehen ist. BPDUs werden immer noch ausgetausch, jedoch keine Nutzdaten. Ein Blocked Port ist wie der Root Port auch mit einem Designated Port verbunden.

#### Spanning Tree Portzustände

In einem Spanning Tree sind potenzielle Schleifen nicht gleich komplett ausgeschaltet. Sie übermitteln aber keine Nutzdaten wie Ethernet Frames. Dabei tauschen alle Ports weiterhin BPDUs, welche den aktuellen Zustand von benachbarten Switches anhand von Statusveränderungen verstehen kann. Ein Port kann folgende Zustände haben:

| Zustand des Ports | Beschreibung                                                                  |
| ----------------- | ----------------------------------------------------------------------------- |
| Disabled          | Verwirft Frames, lernt keine Adressen, empfängt und verarbeitet keine BPDUs   |
| Blocking          | Verwirft Frames, lernt keine Adressen, empfängt und verarbeitet BPDUs         |
| Listening         | Verwirft Frames, lernt keine Adressen, empfängt, verarbeitet und sendet BPDUs |
| Learning          | Verwirft Frames, lernt Adressen, empfängt, verarbeitet und sendet BPDUs       |
| Forwarding        | Leitet Frames weiter, lernt Adressen, empfängt, verarbeitet und sendet BPDUs  |

Die Zustände _Blocking_, _Listening_, _Learning_ sind Zustände von blocked Ports. Ports welche inaktiv sind in der Regel blocking. Wird ein Port aktiv, durchläuft dieser Port alle Zustände bis zum Forwarding Zustand, Wird aber ein Loop erkannt bleibt dieser Port automatisch im _Blocking_ Zustand und empfängt nur noch BPDUs zur Erkennung von Änderungen an der Konstellation.

## Ablauf von Spanning Tree Portstatuswechsel in Betrieb

Es werden 2 Szenarien erklärt um die Wechsel der Zustände verstehen zu können und somit feststellen zu können wie Spanning Tree funktioniert.

### Szenario 1: Netzwerkgerät wird in einen Switch eingesteckt

Wenn ein Netzwerkgerät an einen Switch mit Spanning Tree geknüpft wird, durchläuft der Port die oben beschriebenenen Zustände. Der Port startet von Anfang an im _Blocking_ State und versucht BPDUs zu empfangen, werden als erstes keine BPDUs empfangen, versucht der Port in den _Listening_ State überzugehen und sendet eigene BPDUs mit Feldern Priorität und Bridge ID. Falls auch dann keine Antwort in Form von BPDUs zurückkommt geht der Port in den _Learning_ State über und empfängt die Mac-Adresse des Geräts und bei Erfolg wird der Port in den Forwarding Zustand gehoben. Das Endgerät kann nun im Netzwerk kommunizieren und Broadcasts verschicken.

### Szenario 2: Netzwerkswitch wird an einen anderen Switch eingesteckt

Wenn 2 mit Spanning Tree konfigurierten Switches miteinander verbunden ändert sich die ganze Spanning Tree von alleine und durchläuft mehrere Schritte um den Spanning Tree aufrecht zu halten.

Beide Switches nehmen zuerst an sie seien die Root Bridge solange bis sie miteinander verbunden werden. Bei beiden Switches starten die entsprechenden Ports im _Blocking_ Zustand und danach in den Listening Zustand. Nun übertragen beide Switches ihre Bridge ID und können nun anhand des [oben](#root-bridge) gennanten Verfahrens ausmachen welcher Switch nun die Root Bridge ist. Nachdem die Root Bridge auserwählt wurde, wird automatisch der Port an der Root Bridge zu einem Designated Port und der Port der nicht-Root Bridge zu einem Root Port.
