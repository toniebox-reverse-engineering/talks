
# 37th Chaos Communication Congress - Call for Participation
Editor: https://stackedit.io/app#

Here is our edit-space for the application to the 37C3
https://frab.cccv.de/de/37c3/cfp/events/new

## Titel
Toniebox Reverse Engineering

## Untertitel
Eine Musikbox für Kinder, Maker und Hacker

## Zusammenfassung
*kurzer Absatz, der Ihren Vorschlag prägnant beschreibt. (HTML)*

Ein Vortrag über den erfolgreichen Kinder-Audioplayer "Toniebox" mit kompletter Cloud-Abhängigkeit, der nicht nur Einblicke in die (un-) heimliche Datensammlungspraxis bietet, sondern auch gleich passende, datensparsame Lösungen dazu.
Custom-Firmware, Selfhosted Cloud-Ersatz und Tools zum Erzeugen von Inhalten ohne Herstellercloud.

## Beschreibung
*Eine längere Beschreibung Ihres Vorschlags. Hier kann alles rein, was nicht in den Abstract passt. (HTML)*

In unserem Vortrag über die Toniebox konzentrieren wir uns auf das Innenleben und die Funktionsweise dieses beliebten Audiogerätes für Kinder. Wir beginnen mit einer detaillierten Einführung in das Prinzip der Toniebox aus technischer Sicht und geben einen kurzen Überblick über die Hardwarekomponenten, insbesondere die verschiedenen Prozessorvarianten wie CC3200, CC3235 und ESP32.

Der Übergang zu den Limitationen des Systems ist fließend: Wir diskutieren die künstlichen Beschränkungen durch den Hersteller, den Zwang zur Verwendung von Originalfiguren, die Inkompatibilität mit NFC-Tags von Drittanbietern und die hohen Kosten für bespielbare Figuren. Besonders kritisch sehen wir die vollständige Abhängigkeit von einer Hersteller-Cloud, die bei einem Ausfall des Anbieters das Gerät obsolet macht. Ein weiterer Fokus liegt auf dem ausgeprägten Datenhunger des Herstellers, der fast schon paranoid das Nutzungsverhalten unserer Kinder aufzeichnet.

Im Kern des Vortrags stellen wir die von uns entwickelten Open-Source-Alternativen vor. Mit der TeddyBench stellen wir einen Offline-Editor vor, mit dem Audiodaten für eigene NFC-Tags erstellt und verwaltet werden können. Die TeddyCloud bietet als selbstgehostete Lösung volle Kontrolle über die eigenen Daten, eine persönliche Audio-Bibliothek und die Möglichkeit, Nutzungsdaten über MQTT in den Home Assistant einzuspeisen, ohne die Funktionalität der Box einzuschränken. Außerdem stellen wir Custom Firmwares für CC3200 und ESP32 vor, die neue Einsatzmöglichkeiten eröffnen, und berichten über unsere Hardware-Modifikationen, die unter anderem Bluetooth-Audio ermöglichen und die Toniebox barrierefreier machen.


Dauer der Kapitel in Minuten in [*d*] angegeben

Gesamtzeit 55min

### [2] Einleitung
 - [2] Willkommen

### [10] Was ist die Toniebox?
Zunächst planen wir, kurz das Prinzip der Toniebox vorzustellen und zu erklären, warum wir das Gerät nicht per se verteufeln.
 - [3] Grobbeschreibung aus Nutzersicht
 - [3] Abspielprinzip (inkl. Rolle der Cloud)
 - [4] Kleine Einblicke in die Hardware (Varianten: CC3200 / CC3235 / ESP32)

### [15] Kein Licht ohne Schatten
Dann gehen wir doch sehr schnell auf die Nachteile ein
 - [2] künstliche (wirtschaftlich begründete) Einschränkungen
	 - nur Originalfiguren
	 - keine eigenen NFC-Tags nutzbar
	 - teure "bespielbare" Figuren
	 - Zeitlimit der Inhalte
 - [5] Abhängig von der Cloud eines Herstellers
	 - Gerät nach Herstellerwunsch/-pleite nutzlos
	 - Ökosystem fußt komplett auf einem Privatunternehmen
 - [8] Datenhunger des Herstellers inkl. Auszüge
	 - Ausspähen/"Nutzungsverhalten" der Kinder
	 - paranoides Logging

### [15] Alternativen
Erarbeitete Lösungen
 - [5] TeddyBench - Offline-Editor der Audiodaten
	 - https://github.com/toniebox-reverse-engineering/teddy/releases
 - [5] TeddyCloud - Cloud zum selberhosten
	 - https://github.com/toniebox-reverse-engineering/teddycloud
	 - Eigene Bibliothek für mehr als nur eine Box
	 - MQTT/Home Assistant-Einbindung der Usage-Daten
 - [3] Custom Firmware (CC3200/ESP32)
	 - https://github.com/toniebox-reverse-engineering/hackiebox_cfw
	 - https://github.com/toniebox-reverse-engineering/hackiebox_cfw_ng
	 - https://github.com/toniebox-reverse-engineering/teddybox
 - [2] Hardware-Mods
	 - Bluetooth Audio (https://www.g3gg0.de/wordpress/hacks/toniebox-bluetooth-modification/)
	 - Barrierefreiheit

### [2] Outro
 - [2] Wer sind wir?

### [10] QnA

## Details zur Einreichung
Quellen
 - https://github.com/toniebox-reverse-engineering/hackiebox_cfw
 - https://github.com/toniebox-reverse-engineering/hackiebox_cfw_ng
 - https://github.com/toniebox-reverse-engineering/teddybox
 - https://gt-blog.de/
 - https://www.g3gg0.de/wordpress/hacks/toniebox-bluetooth-modification/
 
