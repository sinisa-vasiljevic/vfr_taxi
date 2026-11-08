# VfR Taxi PWA v1.9.0

Vollständiger, konsolidierter Projektstand der VfR-Taxi-PWA.

## Rollen
- **Master:** fest hinterlegtes Hauptkonto; Benutzer- und Rollenverwaltung.
- **Admin:** Anfragen, Reservierungen, Fahrzeuge und Fahrten verwalten.
- **Nutzer:** eigene Anfragen erstellen/bearbeiten; als Anfragensteller oder eingetragener Fahrer Fahrten starten und beenden.
- Master und Admin werden in der sichtbaren App-Legende einheitlich als **Admin** bezeichnet.

## Anfrage und Reservierung
- Offene Anfragen blockieren keinen Bus.
- Erst die Zuweisung erzeugt eine verbindliche Reservierung.
- Reservierte oder gesperrte Busse können für kollidierende Zeiträume nicht zugewiesen werden.
- Der Anfragensteller bleibt unveränderbar; der Fahrer einer eigenen offenen Anfrage darf geändert werden.
- Ein Nutzer darf die eigene offene Anfrage oder die eigene bestätigte Reservierung löschen. Nach Löschen der Reservierung ist der Bus in diesem Zeitraum wieder frei.

## Fahrtstart und Fahrtende
- Start frühestens 24 Stunden vor dem Reservierungsbeginn und nur bis zum Reservierungsende, wenn die Fahrt noch nicht gestartet wurde.
- Startberechtigt: Master/Admin, Anfragensteller und eingetragener registrierter Fahrer.
- Ist eine Vorgängerfahrt noch aktiv, wird orange gewarnt. Nach Bestätigung wird sie automatisch abgeschlossen; der neue Abfahrts-KM-Stand wird als End-KM-Stand übernommen.
- Beim automatischen Abschluss werden Anfragensteller, Fahrer und auslösende Person als Snapshot gespeichert.
- Beenden dürfen Master/Admin, Anfragensteller und eingetragener Fahrer. Sobald eine Person beendet, verschwindet der Button für alle.

## Status und Farben
Gleiche Bedeutung verwendet überall dieselbe Farbe:
- Gelb: ANGEFRAGT
- Rot: RESERVIERT
- Blau: IN NUTZUNG
- Orange: ÜBERFÄLLIG
- Grau: VERGANGEN
- Grau/Orange: NICHT ORDNUNGSGEMÄSS / AUTOMATISCH ABGESCHLOSSEN
- Schwarz: GESPERRT / WERKSTATT
- Grün: FREI

## Fahrzeugstatus
- FREI mit „Frei bis …“
- RESERVIERT während der Reservierungszeit vor Fahrtstart
- IN NUTZUNG bei aktiver Fahrt
- ÜBERFÄLLIG nach Reservierungsende bei weiterhin aktiver Fahrt
- GESPERRT / WERKSTATT bei Sperre
- Früher Abschluss gibt den Bus sofort frei.

## Kalender
- Nur Monatsansicht.
- Ausführliche Legende direkt im Reiter Belegung.
- Monatsbalken und Tagesdetails verwenden dieselbe Statusberechnung.
- Automatisch abgeschlossene Fahrten zeigen Verantwortliche, Abschlusszeit, KM-Übernahme und auslösende Person.

## TÜV
- Anzeige und Eingabe als Monat/Jahr, z. B. 02 / 2027.
- Gültig bis zum letzten Kalendertag des angegebenen Monats.

## Veröffentlichung
1. Gesamten Inhalt des ZIP in das GitHub-Repository hochladen.
2. `firestore.rules` in Firebase unter Firestore Database > Regeln veröffentlichen.
3. Nach Aktualisierung die installierte PWA einmal vollständig schließen und neu öffnen.
