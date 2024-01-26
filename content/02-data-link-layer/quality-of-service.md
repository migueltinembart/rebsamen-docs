+++
title = 'Quality of Service'
date = 2024-01-26T15:25:21+01:00
draft = true
+++

QoS ermöglicht es uns mit der Einführung von [IEEE802.1p](https://de.wikipedia.org/wiki/IEEE_802.1p) Frames mit einer Prioritätsinformation auszustatten und dem Switch mitzuteilen mit welcher Priorität diese Frames verarbeitet werden. Somit können wir für zeitkritische Anwendungen (Telefonie, Video) sicherstellen, dass diese Frames bevorzugt behandelt werden.

QoS of Service wurde im erweiterten Ethernet Frame mit IEEE802.1p eingeführt und und ist ein 3 Bit grosses Feld und ermöglicht somit 8 Werte zur Unterscheidung der verschiedenen Priorisierungslevel.

| priority | Traffic-Eigenschaften |
| -------- | --------------------- |
| 0        | Hintergrund           |
| 1        | best Effort           |
| 2        | Excellent Effort      |
| 3        | Critial Application   |
| 4        | Video (< 100ms)       |
| 5        | Voice (< 10ms)        |
| 6        | Internetwork Control  |
| 7        | Network Control       |

Seit der Arbeit an 802.1p wurde die Definition für den 802.1Q Standard als Teil des Standards definiert.
