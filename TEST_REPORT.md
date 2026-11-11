# Prüfbericht VfR Taxi v1.9.6

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


### Ergänzende Prüfungen v1.9.6
- Pflichtauswahl für Mannschaft und Spielart in neuer und bearbeiteter Anfrage.
- U18 ist nicht in der Mannschaftsauswahl enthalten.
- Spielart und Ort/Ziel werden in den entscheidungsrelevanten Übersichten angezeigt.
- Reservierung aufheben führt `reserved -> requested` aus, entfernt `vehicleId` und behält den Buchungsdatensatz.
- Offene Anfrage zurückziehen löscht weiterhin ausschließlich den Anfrage-Datensatz.


### Ergänzende Prüfungen v1.9.6
- Pflichtauswahl für Mannschaft und Spielart in neuer und bearbeiteter Anfrage.
- U18 ist nicht in der Mannschaftsauswahl enthalten.
- Spielart und Ort/Ziel werden in den entscheidungsrelevanten Übersichten angezeigt.
- Reservierung aufheben führt `reserved -> requested` aus, entfernt `vehicleId` und behält den Buchungsdatensatz.
- Offene Anfrage zurückziehen löscht weiterhin ausschließlich den Anfrage-Datensatz.


#### Layoutpruefung v1.9.6
- Dieselbe requestPriorityPair-Struktur wird fuer alle Rollen verwendet.
- Finale CSS-Regel erzwingt auch unter 430 px zwei gleich breite Spalten.


##### Ergänzende Prüfungen v1.9.6
- Identische Standortauswahl in Fahrtende und Fahrzeugdokumentation geprüft.
- Freie Standortdefinition wird nur bei „Anderer Standort / freie Eingabe“ eingeblendet und ist dann Pflicht.
- Schaden Nein blendet Beschreibung aus; Schaden Ja blendet sie ein und verlangt Text.
- Schadensmeldung schreibt weiterhin `damageText`, `damages` und `openDamage`; keine automatische Sperre.
- Bestehende Rollenprüfung für Fahrtende bleibt für Master, Admin, Anfragensteller und Fahrer unverändert.

## Vollprüfung v1.9.9
Navigationsumbau, Master-only-Benutzeransicht, Syntax, JSON, Dateiverweise, Versionskonsistenz und ZIP-Integrität geprüft. Echte produktive Firebase-Ende-zu-Ende-Tests bleiben als Testgrenze bestehen.


### Ergänzende Prüfungen v1.9.9
- Kalender-Direktsprung nutzt die eindeutige bookingId und öffnet nur weiterhin offene Anfragen.
- Monatsbalken und Tagesdetailkarten unterstützen den Direktsprung.
- Aktionsbuttons in Tagesdetails lösen den Direktsprung nicht versehentlich aus.
- Während der Buszuweisung werden Zuweisungsbuttons deaktiviert.
- Nach erfolgreicher Firestore-Aktualisierung erscheint ein modaler Bestätigungsdialog mit Bus, Mannschaft, Zeitraum, Anfragensteller und Ziel.
- Bei Fehlern werden die Buttons wieder aktiviert und eine Fehlermeldung angezeigt.


### Vollprüfung und Korrektur v1.9.9
- Fehlendes Manifest im vorherigen ZIP ergänzt.
- Race Condition bei paralleler Buszuweisung durch Firestore-Transaktion reduziert.
- Zuweisungsdialog blockiert während Prüfung und Speicherung vollständig.
- Syntax, JSON, lokale Dateiverweise, Rollenpfade, Konfliktlogik und ZIP-Integrität geprüft.


### Prüfung v2.1.1
- JavaScript-Syntaxprüfung, Versionskonsistenz und Manifest-JSON geprüft.
- Service-Worker-Aktivierung, automatische Neuladung bei Controllerwechsel und Updateprüfung bei Fokus/Sichtbarkeit statisch geprüft.
- Direkte Serveraktualisierung aller sechs Firestore-Sammlungen bei Rückkehr in die App geprüft.
- Werkstattdaten werden aus dem bestehenden Sperrdatensatz vorbefüllt; Speichern aktualisiert denselben Datensatz statt Duplikate anzulegen.
- Vorzeitige Freigabe entfernt die Sperre und setzt den Standort auf „im Gelände“.
- Kalender besitzt vier feste Fahrzeugspuren; offene Anfragen bleiben über einen Tageshinweis erreichbar.
- Produktive Ende-zu-Ende-Prüfung gegen Firebase und iOS-PWA-Lifecycle bleibt technisch nur in der veröffentlichten App möglich.


#### Nachprüfung v2.1.1
- Vorzeitige Werkstattfreigabe ist jetzt atomar: Sperrdatensatz und Fahrzeugstandort werden gemeinsam geschrieben oder gemeinsam verworfen.
- Vor der Freigabe muss ein tatsächlicher Standort ungleich „Werkstatt“ ausgewählt werden.
- Werkstatt-Bis-Datum vor Von-Datum wird abgefangen.
- Eine zukünftige Werkstattreservierung setzt den aktuellen Fahrzeugstandort nicht vorzeitig auf „Werkstatt“.
- Mehrere zeitlich getrennte Buchungen desselben Busses am selben Tag werden in der festen Busspur mit +N gekennzeichnet und vollständig in den Tagesdetails angezeigt.


### Prüfung v2.1.2
- 60-Sekunden-Intervall entfernt und statisch ausgeschlossen.
- Service Worker aktiviert eine neue Version nicht mehr selbstständig; die Aktivierung erfolgt ausschließlich über die Nachricht SKIP_WAITING vom Pflichtdialog.
- Pflichtdialog besitzt weder Schließen-Schaltfläche noch Später-Option und blockiert die restliche Oberfläche.
- Prüfung wird bei Start, visibilitychange auf visible und Fokus ausgelöst; parallele Prüfungen werden verhindert.
- controllerchange lädt genau einmal neu.
- Updatecode enthält keine Schreiboperation für bookings, trips, vehicles, users, invites oder damages.
- Bestehende Fahrtstart-, Fahrtende-, Kilometer-, Reservierungs- und Rollenlogik blieb unverändert.


### Korrekturprüfung v2.1.3
- Ursache v2.1.2: Die Erkennung stützte sich auf Service-Worker-reg.update() und visibilitychange/focus. Auf iOS-PWAs wird der Vordergrundwechsel bzw. die Worker-Aktualisierung nicht in jedem Fall rechtzeitig gemeldet.
- version.json als unabhängiger, cachefreier Versionskanal ergänzt.
- pageshow, visibilitychange und focus lösen dieselbe gedrosselte Vordergrundprüfung aus.
- Bei Versionsabweichung bleibt die Oberfläche gesperrt, bis der Benutzer das Pflichtupdate ausführt.
- Update-Lifecycle enthält weiterhin keine Firestore-Schreiboperation.
