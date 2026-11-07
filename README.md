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

### v1.4.1
- Fahrzeugdatenspeicherung mit sichtbarer Fehlerausgabe korrigiert.
- Erfolgs-Popup nach dem Speichern eingebaut.
- Versionsnummer v1.4.1 im Header sichtbar.
- Pflichtfeld Parkplatz / Standort nach Nutzungsende ergänzt und in der Historie gespeichert.

### v1.4.3
- Sichtbare Versionszeile direkt unter Mannschaftsbusse.

#### v1.4.4
- Geblitzt-Anzeige eindeutig: gruen = Nicht geblitzt, rot = Geblitzt.

#### v1.4.5
- Busanfragen enthalten Datum von und Datum bis.
- Mehrtaegige Nutzungen werden in Anfrage-, Fahrzeug- und Kalenderuebersicht ueber den gesamten Zeitraum dargestellt.
- Bestehende eintägige Buchungen bleiben kompatibel.

##### v1.4.6
- Eigene offene Busanfragen koennen bearbeitet werden.
- Bearbeitbar: Mannschaft, Datum von/bis, Uhrzeit von/bis, Buswunsch und Ort/Ziel.
- Fremde Anfragen und bereits reservierte/zugewiesene Anfragen bleiben fuer normale Nutzer unveraenderbar.

##### v1.4.7
- Bearbeiten-Button gelb mit schwarzer Schrift, Bus-Zuweisungen bleiben unveraendert.

##### v1.4.8
- Bearbeiten bleibt optisch wie bisher, nur die Schrift ist schwarz.

###### v1.4.9
- Zaehler Reserviert zaehlt alle Reservierungen, deren Enddatum heute oder in der Zukunft liegt. Vollstaendig vergangene Reservierungen werden nicht mehr mitgezaehlt.


######## v1.5.0
- Mehrtaegige Anfragen/Reservierungen bleiben genau ein Buchungsdatensatz und werden im Monatskalender als zusammenhaengender Balken dargestellt.
- Bei Wochenwechsel wird der Balken in der naechsten Kalenderzeile optisch fortgesetzt.
- Statusfarben unveraendert: frei gruen, angefragt gelb, reserviert rot, Werkstatt/gesperrt schwarz.
- Bestaetigung/Zuweisung einer Anfrage bleibt eine einzelne Aktion fuer den gesamten Zeitraum.


########### v1.6.0
- Zaehlerbezeichnung Reservierungen.
- Gewuenschter Bus wird bei der Admin-Zuweisung gelb markiert.
- Zeitgenaue Kollisionspruefung bei Anfrage, Bearbeitung und Zuweisung.
- Fahrer ist Pflicht und getrennt vom Anfragesteller.
- Admin/Master kann externe Fahrer manuell erfassen.
- Registrierter Fahrer dokumentiert die Fahrt; bei externem Fahrer dokumentiert der Anfragesteller.
- Normale Bearbeitung endet 24 Stunden nach geplantem Fahrtende; Admin/Master dauerhaft.
- Wiederregistrierung geloeschter App-Benutzer mit bestehendem Auth-Konto und bisherigem Passwort.


############ v1.6.1
- Wunschbus-Zuweisungsbutton jetzt neongruen statt gelb.
- Fahrer-Auswahl aus v1.6.0 unveraendert enthalten und im fertigen ZIP verifiziert.


############# v1.7.1
- Neu auf der guten v1.6.1 aufgebaut; kein grosser Meine-Fahrten-Block.
- Fahrt starten/beenden erscheint nur an der passenden Buskarte des tatsaechlich eingetragenen Fahrers.
- Admin/Master sieht weiterhin zuerst und vollstaendig die vier Buskarten und erhaelt nicht automatisch fremde Fahrten.
- Externer Fahrer: Der Anfragesteller dokumentiert stellvertretend.
- Buswunsch/Fahrer bei offener Anfrage werden nach dem Bearbeiten gespeichert und verifiziert.
- Automatischer Abschluss einer offenen vorherigen Fahrt mit KM-Uebernahme und Warnhistorie.
- Historie zeigt Start, letzte Aenderung, Bearbeiter, letzten Fahrer und Ausloeser.
