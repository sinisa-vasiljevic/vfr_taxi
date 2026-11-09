# VfR Taxi PWA v1.9.4

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
- Ein Nutzer darf die eigene offene Anfrage und die eigene bestätigte Reservierung nur löschen, solange diese Reservierung noch nie als Fahrt gestartet wurde. Sobald die Fahrt einmal gestartet wurde, ist eine Löschung durch den Nutzer dauerhaft ausgeschlossen, auch nach regulärem oder automatischem Fahrtabschluss. Wird eine noch nicht gestartete Reservierung gelöscht, ist der Bus in diesem Zeitraum wieder frei.

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


### Kilometerlogik v1.9.4
- Harte Untergrenze beim Fahrtstart ist der Start-KM der zuletzt gestarteten Fahrt desselben Busses.
- Ein möglicherweise falsch zu hoch eingetragener letzter End-KM blockiert die nächste Fahrt nicht.
- Liegt der neue Start-KM unter dem letzten End-KM, aber nicht unter dem letzten Start-KM, erscheint eine Warnung mit bewusster Bestätigung.
- Die bestätigte Korrektur wird im neuen Fahrteintrag mit vorherigem Start-KM, vorherigem End-KM, neuem Tachostand, Benutzer und Zeitstempel dokumentiert.


### Benutzerverwaltung v1.9.4
- Mobile Benutzerkarten deutlich kompakter.
- Name und E-Mail/Rolle nutzen die volle Kartenbreite.
- Aktionen Admin/Entfernen, Sperren/Entsperren und Löschen stehen in einer kompakten Dreierreihe.
- Kein zusätzlicher Seitenabstand für den schwebenden „+ Bus anfragen“-Button hinzugefügt.


#### Anfragepriorisierung v1.9.4
- Mannschaft ist ein Pflicht-Auswahlfeld: PT18, PT17, U11 bis U17, U19 und HERREN. U18 ist bewusst nicht enthalten.
- Spielart ist ein Pflicht-Auswahlfeld: LIGA, Testspiel, TR-Lager, Pokal, Turnier und Event.
- Mannschaft und Spielart stehen im Anfragefenster platzsparend nebeneinander.
- Spielart und Ort/Ziel werden in der Anfrageübersicht, den Kalender-Tagesdetails, der WhatsApp-Admin-Nachricht und beim nächsten Fahrzeugtermin angezeigt.
- „Reservierung aufheben“ löscht die Anfrage nicht mehr. Der Status wird auf ANGEFRAGT zurückgesetzt, die Buszuweisung entfernt und der Bus freigegeben.
- Nur „Anfrage zurückziehen“ löscht eine offene Anfrage vollständig.


#### Anfragepriorisierung v1.9.4
- Mannschaft ist ein Pflicht-Auswahlfeld: PT18, PT17, U11 bis U17, U19 und HERREN. U18 ist bewusst nicht enthalten.
- Spielart ist ein Pflicht-Auswahlfeld: LIGA, Testspiel, TR-Lager, Pokal, Turnier und Event.
- Mannschaft und Spielart stehen im Anfragefenster platzsparend nebeneinander.
- Spielart und Ort/Ziel werden in der Anfrageübersicht, den Kalender-Tagesdetails, der WhatsApp-Admin-Nachricht und beim nächsten Fahrzeugtermin angezeigt.
- „Reservierung aufheben“ löscht die Anfrage nicht mehr. Der Status wird auf ANGEFRAGT zurückgesetzt, die Buszuweisung entfernt und der Bus freigegeben.
- Nur „Anfrage zurückziehen“ löscht eine offene Anfrage vollständig.
