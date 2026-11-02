# VfR Taxi PWA v1.3.2

Vollständiger Stand nach dem bewährten Trainingsplaner-Aufbau.

## Registrierung und Benutzerverwaltung
- Master-E-Mail: `v.sinisa@gmx.de`
- Master legt in der App Einladungen mit Name und E-Mail an.
- Einladung enthält `active: true` und `used: false`.
- Erstzugang erfolgt mit Einladungscode, passender E-Mail und eigenem Passwort.
- Nach Firebase Authentication werden `users/{uid}` und der Verbrauch der Einladung in einem gemeinsamen Firestore-Batch geschrieben.
- Die Regeln validieren den gemeinsamen Endzustand mit `getAfter()`.
- Bei Fehlschlag entfernt die App das zuvor erzeugte Authentication-Konto wieder.
- Master kann registrierte Trainer zu Admins machen und Adminrechte entziehen.
- Mehrere Admins sind möglich; nur der Master verwaltet Rollen.

## Veröffentlichung
1. Den gesamten Inhalt dieses Ordners ins GitHub-Repository laden.
2. In Firebase unter Firestore Database > Regeln den vollständigen Inhalt von `firestore.rules` einsetzen und veröffentlichen.
3. In Firebase Authentication unter autorisierte Domains die GitHub-Pages-Domain hinterlegen.
4. Auf der Anmeldeseite „Mit Einladung registrieren“ wählen und den Master mit `v.sinisa@gmx.de` anlegen; der Master benötigt keinen Einladungscode.
5. Danach im Reiter „Benutzer“ Trainer-Einladungen erstellen.

## Enthaltene Fachfunktionen
- Vier Busse mit Kennzeichen
- Statusfarben: frei grün, angefragt gelb, reserviert rot, Werkstatt/gesperrt schwarz
- Alle Benutzer sehen alle Anfragen und Reservierungen inklusive Trainer
- Verbindliche Zuweisung nur durch Admin/Master
- Fahrtdokumentation: KM Abfahrt/Ankunft, getankt, geputzt, gewaschen
- Schäden/Mängel als Freitext
- TÜV-Warnung: 8 Wochen gelb, 4 Wochen rot, abgelaufen rotes Kreuz
- Werkstattaufenthalte und Sperrzeiten
- PWA-Service-Worker und bestätigtes Homescreen-Icon


## Korrektur v1.3.2
Firebase Web API-Key exakt aus der Firebase-Konsole übernommen.


## Fehlerkorrektur v1.3.2
- Firebase-Konfiguration Zeichen für Zeichen aus dem bereitgestellten Projektblock übernommen.
- `app.js` und `config.js` erhalten Versionsparameter.
- Service Worker cached ausführbare JavaScript- und Konfigurationsdateien nicht mehr.
- Dadurch kann eine installierte PWA nicht länger eine ältere Firebase-Konfiguration aus einem vorherigen Cache verwenden.


## Korrekturen v1.3.2
- Anmeldefenster wird nach erfolgreicher Anmeldung zuverlässig ausgeblendet (`[hidden]`).
- Master-Selbstregistrierung entfernt; vorhandener Master nutzt ausschließlich „Anmelden“.
- Monatsansicht als Standardansicht eingebaut.
- Direkter Sprung zu jedem Monat über Monatsauswahl.
- Umschaltung Monat/Woche und Heute-Schaltfläche.
- Tagesdetails mit Bus, Mannschaft, Trainer, Zeit, Status und Zweck.


### Layoutkorrektur v1.3.2
- Benutzerverwaltung sauber getrennt: Titel/Beschreibung und Einladungsschaltflaeche.
- Vier Hauptreiter mit groesserer Schrift bei weiterhin vier festen Spalten.
- Getankt, Geputzt und Gewaschen kompakter und gleich gross.


### v1.3.5
Auf Basis der vom Nutzer bereitgestellten v1.3.2. Nur TÜV, Werkstatt Von und Bis schmaler; Fahrzeughistorie sichtbar in den Busdetails. Sonst kein Redesign.
