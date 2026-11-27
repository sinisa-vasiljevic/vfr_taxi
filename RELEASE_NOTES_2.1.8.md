# VfR Taxi 2.1.8 - Reifenanzeige, gezieltes Update von 2.1.7

Aenderungen: app.js (Reifenanzeige, Admin-/Master-Auswahl und Speicherung), styles.css (Reifenzeile in TUeV-Kachel), Versionsreferenzen in app.js/config.js/index.html/sw.js/version.json. Originalmanifest aus dem Chat aufgenommen.

Unveraendert: Buchungs-, Fahrt-, Status-, Rollen- und Werkstattlogik; firebase.json; alle Icons. Keine CSS-Bereinigung und keine Formularrefaktorierung. Keine Aenderung an Gewaschen.

Geprueft: JavaScript-Syntax, JSON, ZIP-Integritaet, Existenz der Reifen-Felder und Anzeigen, Versionsreferenzen, bytegenaue Uebereinstimmung der unveraenderten Dateien.

Nicht getestet: Firebase-Live-Schreib-/Lesetest, echte Rollen im Browser, iPhone-Layout, Service-Worker-Update auf echtem Geraet. Keine Garantie fuer produktiven Betrieb.

Die Versionsnummer ist 2.1.8, damit die bestehende PWA-Updateerkennung den neuen Stand erkennt.
