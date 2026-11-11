# VfR Taxi PWA v1.9.6

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


### Kilometerlogik v1.9.6
- Harte Untergrenze beim Fahrtstart ist der Start-KM der zuletzt gestarteten Fahrt desselben Busses.
- Ein möglicherweise falsch zu hoch eingetragener letzter End-KM blockiert die nächste Fahrt nicht.
- Liegt der neue Start-KM unter dem letzten End-KM, aber nicht unter dem letzten Start-KM, erscheint eine Warnung mit bewusster Bestätigung.
- Die bestätigte Korrektur wird im neuen Fahrteintrag mit vorherigem Start-KM, vorherigem End-KM, neuem Tachostand, Benutzer und Zeitstempel dokumentiert.


### Benutzerverwaltung v1.9.6
- Mobile Benutzerkarten deutlich kompakter.
- Name und E-Mail/Rolle nutzen die volle Kartenbreite.
- Aktionen Admin/Entfernen, Sperren/Entsperren und Löschen stehen in einer kompakten Dreierreihe.
- Kein zusätzlicher Seitenabstand für den schwebenden „+ Bus anfragen“-Button hinzugefügt.


#### Anfragepriorisierung v1.9.6
- Mannschaft ist ein Pflicht-Auswahlfeld: PT18, PT17, U11 bis U17, U19 und HERREN. U18 ist bewusst nicht enthalten.
- Spielart ist ein Pflicht-Auswahlfeld: LIGA, Testspiel, TR-Lager, Pokal, Turnier und Event.
- Mannschaft und Spielart stehen im Anfragefenster platzsparend nebeneinander.
- Spielart und Ort/Ziel werden in der Anfrageübersicht, den Kalender-Tagesdetails, der WhatsApp-Admin-Nachricht und beim nächsten Fahrzeugtermin angezeigt.
- „Reservierung aufheben“ löscht die Anfrage nicht mehr. Der Status wird auf ANGEFRAGT zurückgesetzt, die Buszuweisung entfernt und der Bus freigegeben.
- Nur „Anfrage zurückziehen“ löscht eine offene Anfrage vollständig.


#### Anfragepriorisierung v1.9.6
- Mannschaft ist ein Pflicht-Auswahlfeld: PT18, PT17, U11 bis U17, U19 und HERREN. U18 ist bewusst nicht enthalten.
- Spielart ist ein Pflicht-Auswahlfeld: LIGA, Testspiel, TR-Lager, Pokal, Turnier und Event.
- Mannschaft und Spielart stehen im Anfragefenster platzsparend nebeneinander.
- Spielart und Ort/Ziel werden in der Anfrageübersicht, den Kalender-Tagesdetails, der WhatsApp-Admin-Nachricht und beim nächsten Fahrzeugtermin angezeigt.
- „Reservierung aufheben“ löscht die Anfrage nicht mehr. Der Status wird auf ANGEFRAGT zurückgesetzt, die Buszuweisung entfernt und der Bus freigegeben.
- Nur „Anfrage zurückziehen“ löscht eine offene Anfrage vollständig.


#### Layoutkorrektur v1.9.6
- Mannschaft und Spielart werden im Anfrageformular fuer alle Rollen und auch mobil zwingend zweispaltig nebeneinander dargestellt.


##### Rückgabe und Schäden v1.9.6
- Parkplatz/Standort ist in Fahrtende und administrativer Fahrzeugdokumentation identisch auswählbar: Badstraße, Theresienstr., DLRG, im Gelände, Werkstatt oder freie Eingabe.
- Schaden/Mangel wird über Nein/Ja ausdrücklich gewählt. Bei Ja ist eine Beschreibung Pflicht.
- Eine Schadensmeldung erzeugt einen offenen Eintrag in `damages` und erhöht `openDamage` am Fahrzeug. Eine automatische Werkstattsperre erfolgt nicht.
- Die Fahrt-beenden-Funktion gilt unverändert für Master, Admin, Anfragensteller und eingetragenen Fahrer.


### Bedienverbesserungen v1.9.9
- Offene Anfragen können aus Monatskalender und Tagesdetails direkt geöffnet werden.
- Die zugehörige Anfrage wird automatisch zentriert und kurz hervorgehoben.
- Nach erfolgreicher Buszuweisung blockiert ein Bestätigungsdialog weitere Eingaben, bis OK gedrückt wird.


### Sicherheitskorrektur v1.9.9
- Die Buszuweisung läuft atomar in einer Firestore-Transaktion.
- Während der gesamten Prüfung und Speicherung blockiert ein modales Fortschrittsfenster weitere Eingaben.
- Parallele Zuweisungen werden anhand des aktuellen Serverstands erneut geprüft.

### Version 2.0.1
- Benutzername und Handynummer können durch den Master bearbeitet werden.
- Reservierungsdetails zeigen Anfragensteller und Fahrer getrennt an.
- Nach erfolgreicher Buszuweisung kann der Anfragensteller bei hinterlegter Handynummer direkt per WhatsApp informiert werden.


#### Version 2.1.1
- Service Worker wird ohne Browser-Cache geprüft; aktive und im Hintergrund gehaltene App-Fenster laden beim Aktivieren des neuen Service Workers automatisch neu. Zusätzlich erfolgt die Updateprüfung alle 60 Sekunden sowie bei Rückkehr in die App.
- Firestore-Daten werden bei Rückkehr/Fokus zusätzlich direkt vom Server geladen, damit bearbeitete Anfragen nicht als veralteter lokaler Stand sichtbar bleiben.
- Werkstatt/Sperre zeigt Werkstatt statt Verein, vorhandene Von-/Bis-Daten und Grund werden beim erneuten Öffnen angezeigt und können geändert werden.
- Eine aktive Werkstatt/Sperre kann über „Bus vorzeitig freigeben“ beendet werden.
- Monatskalender verwendet vier feste Spuren: Bus 1, Bus 2, Bus 3 und Bus 4. Mehrtägige Belegungen wechseln innerhalb einer Kalenderwoche nicht mehr die Zeile.


##### Version 2.1.2
- Die 60-Sekunden-Prüfung wurde vollständig entfernt.
- Eine Versionsprüfung erfolgt beim App-Start und sofort bei Rückkehr aus dem Hintergrund bzw. erneutem Fokus.
- Während der Prüfung ist die App kurz blockiert, damit keine neue Eingabe begonnen werden kann.
- Bei einer neuen Version erscheint ein nicht schließbarer Pflichtdialog. Erst „JETZT AKTUALISIEREN“ aktiviert die neue Version und lädt die App neu.
- Der Updatevorgang verändert keine Firestore-Daten. Aktive Fahrten, Start-KM, Reservierungen und Fahrerzuordnungen bleiben erhalten und werden nach dem Neustart erneut aus Firestore geladen.
- Ohne neue Version wird der Pflichtbereich geschlossen und anschließend der aktuelle Firestore-Serverstand geladen.
