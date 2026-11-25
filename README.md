# Pokémon Burg – v0.1
Inoffizielles Fanprojekt, deutschsprachiger funktionsfähiger Prototyp. Keine offizielle Pokémon-Anwendung.

## Lokal ausprobieren
Im Projektordner `python -m http.server 8000 --directory public` ausführen, dann http://localhost:8000 öffnen. Ohne Firebase läuft die App ausschließlich lokal mit Demo-Rollenwechsel. Adminprofil anlegen, Admin → Beispielkatalog laden → Katalog speichern. Starterbundles als JSON anlegen:

```json
[{"id":"starter1","name":"Starter 1","mons":["gengar","charizard","garchomp","lucario"]}]
```

Admin kann sich selbst einen Run erstellen oder über Rollenwechsel ein Spielerprofil anlegen, anschließend als Admin freigeben. Für den ersten Champion im Adminbereich ein Team erstellen. Standardwerte: 3 Leben, 0 Punkte, 100 Punkte je Sieg, keine Checkpoints. Alle Werte sind editierbar.

## Online einrichten
1. Firebase-Projekt erstellen, Web-App registrieren. Authentication → E-Mail/Passwort aktivieren. Firestore-Datenbank erstellen. Cloud Functions benötigen den Blaze-Tarif (Zahlungsmittel, nutzungsabhängige Kosten; Budgetwarnungen setzen). Die lokale Demo ist kostenlos.
2. Web-Konfigurationsobjekt aus Firebase in `public/config.mjs` anstelle von `null` eintragen. Keine Service-Account-Schlüssel oder Admin-Zugangsdaten veröffentlichen.
3. Node.js 22 und Firebase CLI installieren (`npm install -g firebase-tools`). `firebase login`, `firebase use --add` und Projekt auswählen. `cd functions && npm install && cd ..`; `firebase deploy --only functions,firestore:rules`.
4. App lokal mit dem Server starten und Admin-Account registrieren. Für Adminrechte in einer vertrauenswürdigen lokalen Umgebung Application Default Credentials mit `gcloud auth application-default login` einrichten (Konto muss die erforderlichen Firebase-Auth-IAM-Rechte besitzen). Dann `cd functions && node admin.mjs PROJEKT_ID ADMIN_EMAIL`. Abmelden, neu anmelden. Adminprofil erstellen. Niemals diese Zugangsdaten ins Repository hochladen.
5. GitHub-Repository erstellen, Projektdateien hochladen, Standardbranch `main`. Settings → Pages → Source: GitHub Actions. Workflow ausführen. Die URL der App anschließend in Firebase Authentication → Settings → Authorized domains ergänzen. Keine Secrets für die öffentliche Firebase-Web-Konfiguration nötig.
6. Katalog und Starterbundles einrichten, Preise prüfen, erster Champion festlegen. Mit zwei Testaccounts den kompletten Spielablauf testen, bevor echte Spieler zugelassen werden.

## Katalog und Grafiken
Der mitgelieferte Katalog enthält nur sieben Beispielangebote, **nicht** den vollständigen M-C-Pool. Admin importiert ein geprüftes JSON-Array. Beispielstruktur in `public/sample.json`; IDs sind eindeutig, `kind` = pokemon / mega / item, `price` = nichtnegative Ganzzahl, Mega benötigt `base` und englischen `stone`. `showdown` ist der englische Name, `types` ist ein Suchtext, `disabled` sperrt Verkäufe. Optional `sprite` als geprüfte Bild-URL. Die App lädt standardmäßig Champions-Bilder aus https://github.com/KevinToodlepoot/pokemon-champions-sprites (Drittanbieter, laut README aus Bulbapedia; keine bestätigte offizielle Lizenz, keine Bilddateien mitgeliefert). Fehlende Bilder werden ausgeblendet, nicht durch andere Generationen ersetzt. Offizielle Regelquelle: https://champions-news.pokemon-home.com/en/page/816.html . Vor öffentlicher Veröffentlichung Nutzungsrechte prüfen. Karte: selbst gezeichnete SVG-Pixeloptik nach Gen-3-Vorbild, keine kopierten Tiles.

## Grenzen und Entscheidungen
- Kleingruppen-Prototyp: ein gemeinsames Firestore-Dokument, serverseitige Transaktionen und ausschließlich Callable Functions; Firestore-Clients haben keinen direkten Zugriff. Dokumentlimit 1 MiB, für größere Gruppen auf getrennte Collections migrieren. Keine produktive Sicherheitsprüfung durchgeführt.
- Der Katalog ist admin-gepflegt, keine automatisierte vollständige M-C-Importierung. Die Adminprüfung kontrolliert die tatsächliche Champions-Legalität. Teambuilder bietet freie Showdown-Textfelder statt vollständiger Attacken-/Fähigkeiten-/SP-Datenbank; keine automatische SP→EV-Umrechnung. Items und Mega-Besitz sowie doppelte Items werden geprüft. Mega-Stein inklusive. Rabatt basiert auf aktuellem Normalpreis, auch bei Gratisstartern. Keine normalen Entwicklungen.
- Historische Teams werden als Kopien gespeichert, aber Namen im Export werden aus dem aktuellen Katalog aufgelöst. Titelablehnung lässt bisherigen Champion im Amt. Frühere Champions können als Gegner/Vertreter ausgewählt werden; Abstimmung erfolgt extern über Discord. Kein automatischer Discord-Bot. Ein bereits eingereichtes Team bleibt unveränderlich bis zur Entscheidung.
- Preise und Regeln gelten zum Zeitpunkt des Kaufs bzw. Ergebnisses; keine eingefrorenen Regelversionen. Karte nutzt ein festes Landschaftslayout mit zufällig verteilten Typen, keine prozedural generierte Geografie. Gelöschte Runs können nicht wiederhergestellt werden. Historische Champions bleiben erhalten. Keine Live-Synchronisierung; Aktualisieren-Schaltfläche vorhanden.
- Kein tatsächliches Firebase-Projekt verbunden, keine Veröffentlichung oder Browser-End-to-End-Tests durchgeführt. Vor Produktivbetrieb testen und Daten sichern.
