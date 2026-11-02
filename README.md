# VfR Taxi PWA 1.1.0

Vollständiger Stand mit Einladungssystem und Benutzerverwaltung.

## In Firebase noch ausführen
1. Den kompletten Inhalt aus `firestore.rules` in Firestore > Regeln einsetzen und veröffentlichen.
2. Authentication > Einstellungen > Autorisierte Domains: die GitHub-Pages-Domain hinzufügen.
3. Die Dateien dieses Ordners vollständig in das GitHub-Repository hochladen.
4. Als Master in der App mit `v.sinisa@gmx.de` über „Mit Einladung registrieren“ registrieren. Für diese E-Mail ist kein Einladungscode nötig.
5. Danach im Reiter „Benutzer“ Einladungen für Trainer anlegen.

## Einladungsablauf
- Der Master legt Name und E-Mail an; die App erzeugt einen Einladungscode.
- Die eingeladene Person registriert sich mit exakt dieser E-Mail und dem Code.
- Erst dann entstehen Authentication-Konto und `users/{uid}`.
- Ungültige Registrierungskonten werden sofort wieder entfernt.
- Nur der Master kann Benutzer zu Admins machen oder Adminrechte entziehen.

## Enthalten
Fahrzeuge, Kennzeichen, Belegung, Anfragen, Reservierung durch Admins, Fahrtdokumentation, Schäden, TÜV-Warnstufen, Werkstattsperren, Rollen und PWA-Icons.
