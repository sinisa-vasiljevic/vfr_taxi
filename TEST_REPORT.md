# Prüfbericht VfR Taxi v1.9.5

## Umfang
Geprüft wurden `app.js`, `index.html`, `styles.css`, `config.js`, `sw.js`, `firebase.json`, `firestore.rules`, `manifest.webmanifest`, README und alle Icons.

## Automatisierte Prüfungen
- JavaScript-Syntaxprüfung mit Node.js
- JSON-Prüfung für Firebase-Konfiguration und Manifest
- ZIP-Integritätsprüfung
- einheitliche Versionsnummern in App, HTML, CSS-Verweis, Config und Service Worker
- Vorhandensein aller PWA-Dateien und Icons
- zentrale lokale Datumsbildung ohne UTC-Tagesverschiebung
- 24-Stunden-Startfenster und erneute Prüfung beim Speichern
- Start-/Endeberechtigung für Admin, Anfragensteller und eingetragenen Fahrer
- automatischer Abschluss mit Snapshot von Anfragensteller, Fahrer und Auslöser
- einheitliche Statusfarben in Monatskalender, Tagesdetails, Fahrzeugstatus und Legende
- Entfernung der alten Wochenansicht
- Verhinderung von doppelten generischen Fahrteinträgen aus dem Fahrzeugformular
- Eigene bestätigte Reservierung durch Nutzer nur löschbar, solange die Fahrt noch nie gestartet wurde
- Nach Löschung blockiert der Buchungsdatensatz den Bus nicht mehr

## Geprüfte Statusabläufe
1. ANGEFRAGT → RESERVIERT → IN NUTZUNG → VERGANGEN
2. IN NUTZUNG → ÜBERFÄLLIG → regulär beendet
3. ÜBERFÄLLIG → Start der nächsten Fahrt → automatisch abgeschlossen
4. Reservierung vor Start gelöscht → Bus wieder frei
5. Einmal gestartete Fahrt → Reservierungslöschung für Nutzer dauerhaft gesperrt, auch nach Fahrtende
6. Frühzeitiger regulärer Fahrtabschluss → Bus sofort frei
7. Nie gestartete Reservierung nach Endzeit → kein Startbutton
8. Start frühestens 24 Stunden vor Beginn

## Verbleibende Testgrenze
Eine echte Ende-zu-Ende-Prüfung gegen das produktive Firebase-Projekt und reale Benutzerkonten ist außerhalb der Firebase-Umgebung nicht ausführbar. Deshalb müssen `firestore.rules` veröffentlicht und die vier Rollen-/Nutzungsfälle einmal mit Master, Admin, Anfragensteller und Fahrer in der produktiven App gegengeprüft werden.

- KM-Prüfung: Start-KM unter dem Start-KM der zuletzt gestarteten Fahrt wird gesperrt.
- KM-Korrektur: Wert unter dem letzten End-KM, aber nicht unter dem letzten Start-KM, ist nur nach Bestätigung zulässig und wird dokumentiert.

- Benutzerverwaltung: kompakte Karten und dreispaltige mobile Aktionszeile geprüft.


### Ergänzende Prüfungen v1.9.5
- Pflichtauswahl für Mannschaft und Spielart in neuer und bearbeiteter Anfrage.
- U18 ist nicht in der Mannschaftsauswahl enthalten.
- Spielart und Ort/Ziel werden in den entscheidungsrelevanten Übersichten angezeigt.
- Reservierung aufheben führt `reserved -> requested` aus, entfernt `vehicleId` und behält den Buchungsdatensatz.
- Offene Anfrage zurückziehen löscht weiterhin ausschließlich den Anfrage-Datensatz.


### Ergänzende Prüfungen v1.9.5
- Pflichtauswahl für Mannschaft und Spielart in neuer und bearbeiteter Anfrage.
- U18 ist nicht in der Mannschaftsauswahl enthalten.
- Spielart und Ort/Ziel werden in den entscheidungsrelevanten Übersichten angezeigt.
- Reservierung aufheben führt `reserved -> requested` aus, entfernt `vehicleId` und behält den Buchungsdatensatz.
- Offene Anfrage zurückziehen löscht weiterhin ausschließlich den Anfrage-Datensatz.


#### Layoutpruefung v1.9.5
- Dieselbe requestPriorityPair-Struktur wird fuer alle Rollen verwendet.
- Finale CSS-Regel erzwingt auch unter 430 px zwei gleich breite Spalten.
