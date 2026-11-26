# Pokémon Burg v0.9 – Beta-Kandidat

Inoffizielles Fanprojekt. Siehe GITHUB-START.md für die Aktualisierung. Lokal: `python -m http.server 8000 --directory docs`. Tests: `node test.mjs`.

## Online einrichten
1. Firebase-Projekt erstellen, Web-App registrieren. Authentication → E-Mail/Passwort aktivieren. Firestore-Datenbank erstellen. Cloud Functions benötigen den Blaze-Tarif (Zahlungsmittel, nutzungsabhängige Kosten; Budgetwarnungen setzen). Die lokale Demo ist kostenlos.
2. Web-Konfigurationsobjekt aus Firebase in `public/config.mjs` und `docs/config.mjs` anstelle von `null` eintragen. Keine Service-Account-Schlüssel oder Admin-Zugangsdaten veröffentlichen.
3. Node.js 22 und Firebase CLI installieren (`npm install -g firebase-tools`). `firebase login`, `firebase use --add` und Projekt auswählen. `cd functions && npm install && cd ..`; `firebase deploy --only functions,firestore:rules`.
4. App lokal mit dem Server starten und Admin-Account registrieren. Für Adminrechte in einer vertrauenswürdigen lokalen Umgebung Application Default Credentials mit `gcloud auth application-default login` einrichten (Konto muss die erforderlichen Firebase-Auth-IAM-Rechte besitzen). Dann `cd functions && node admin.mjs PROJEKT_ID ADMIN_EMAIL`. Abmelden, neu anmelden. Adminprofil erstellen. Niemals diese Zugangsdaten ins Repository hochladen.
5. GitHub-Repository erstellen, Projektdateien hochladen, Standardbranch `main`. Settings → Pages → Source: Deploy from a branch → main → /docs (oder GitHub Actions für public). Die URL der App anschließend in Firebase Authentication → Settings → Authorized domains ergänzen. Keine Secrets für die öffentliche Firebase-Web-Konfiguration nötig.
6. Katalog und Starterbundles einrichten, Preise prüfen, erster Champion festlegen. Mit zwei Testaccounts den kompletten Spielablauf testen, bevor echte Spieler zugelassen werden.

## Grenzen

- Firebase verwendet ein gemeinsames Firestore-Dokument (1 MiB Limit), Callable Functions, Transaktionen und gesperrten direkten Datenbankzugriff. Kein Firebase-Livetest, keine produktive Sicherheitsprüfung, keine automatische Live-Synchronisierung; Aktualisieren-Schaltfläche nutzen. Blaze kann Kosten verursachen.
- M-C-Katalog aus v0.2, nicht offiziell vollständig verifiziert. PokéAPI liefert optionale allgemeine Hinweise, keine Champions-Legalitätsgarantie. SP werden als EVs im Champions-Showdown-Format exportiert; Import nicht live getestet. Alte Freitextteams bleiben lesbar.
- Sprites aus externem Drittanbieterarchiv https://github.com/KevinToodlepoot/pokemon-champions-sprites ; keine bestätigte offizielle Herkunft oder Nutzungsrechte. Keine Ersatzsprites anderer Generationen.
- Karte: eigene Gen-3-inspirierte SVG-Pixelgrafik, variable Route, keine vollständig prozedurale Landschaft.
- Champion-Stellvertretung muss extern abgesprochen werden. Titelablehnung lässt bisherigen Champion im Amt. Historische Teams bleiben nach Run-Löschung erhalten.
- Ergebnisrücknahme nur für das letzte Nicht-Champion-Ergebnis vor weiteren Käufen/Teamregistrierungen. Adminprotokoll auf 150 Einträge begrenzt. JSON-Export ohne integrierte Wiederherstellung.
- Keine abgeschlossene Closed Beta. Browserprüfung durch Umgebungs-Netzwerksperre blockiert.

Datenhinweise: https://champions-news.pokemon-home.com/de/page/816.html ; https://pokeapi.co/ ; https://github.com/Seancheey/PokeDD (möglicher künftiger Champions-Datensatz, nicht integriert).
