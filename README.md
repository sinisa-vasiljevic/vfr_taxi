# VfR Taxi PWA 1.0.0

## Enthalten
- Firebase Authentication mit E-Mail/Passwort
- Firestore-Echtzeitspeicherung und Offline-Persistenz
- Rollen: `master`, `admin`, `user`
- Vier Busse, Kennzeichen, TÜV, Kilometerstände, Zustand und Schäden
- Anfragen für alle sichtbar; verbindliche Zuweisung nur durch Admin/Master
- Wochenbelegung, Werkstatt-/Sperrzeiten und Fahrtdokumentation
- installierbare PWA mit Service Worker und randfüllenden Icons

## Einmalige Einrichtung
1. In Firebase ein neues Projekt für **VfR Taxi** erstellen.
2. Unter **Authentication > Sign-in method** E-Mail/Passwort aktivieren.
3. Unter **Firestore Database** eine Datenbank anlegen.
4. Eine Web-App registrieren und die sechs Werte nach `config.js` kopieren.
5. In `config.js` bei `MASTER_EMAIL` die eigene Anmelde-E-Mail eintragen.
6. Dieselbe E-Mail in `firestore.rules` bei `DEINE-MASTER-EMAIL@BEISPIEL.DE` einsetzen.
7. Regeln veröffentlichen: `firebase deploy --only firestore:rules`.
8. Hosting veröffentlichen, z. B. über Firebase Hosting oder GitHub Pages. Bei GitHub Pages bleiben Authentication und Firestore funktionsfähig, sofern die Domain in Firebase Authentication unter **Autorisierte Domains** hinterlegt ist.

## Wichtige Sicherheitsentscheidung
Trainer können Fahrzeugzustände und Fahrtdokumentationen eintragen, aber keine verbindliche Reservierung freigeben. Nur Admin/Master dürfen Fahrzeuge zuweisen, Werkstattzeiten verwalten und Rollen ändern. Nur der Master darf Adminrollen vergeben oder entziehen.

## Icon
Die Dateien `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` und `apple-touch-icon.png` sind bereits eingebunden. Das Motiv ist randfüllend und ohne weißen Außenrand. Wenn das endgültige Vereinsicon verwendet werden soll, die Dateien bei unveränderten Dateinamen ersetzen.
