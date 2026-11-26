# Pokémon Burg v0.9 – Beta-Kandidat

## Bestehendes Repository aktualisieren
1. Sichere die bisherige Version (GitHub: Code → Download ZIP). Optional im Adminbereich der neuen Version eine JSON-Sicherung herunterladen.
2. Entpacke das neue ZIP und öffne `pokemon-burg-v09`. Lade den **Inhalt** in dein bestehendes Repository `dragonkeks/Pokemon-Burg` hoch. Insbesondere müssen alle Dateien in `docs/` die alten ersetzen. Nicht den gesamten übergeordneten Ordner in einen Unterordner hochladen.
3. Settings → Pages: Deploy from a branch, `main`, `/docs`. Die Einstellungen aus v0.2 können bleiben. Alternativ GitHub Actions verwenden, dann wird `public/` veröffentlicht.
4. Nach erfolgreichem Deployment: https://dragonkeks.github.io/Pokemon-Burg/ öffnen und Cmd+Shift+R drücken. Im Kopf steht v0.9 BETA.
5. Der Demo-Modus nutzt denselben localStorage-Schlüssel wie v0.2; vorhandene Runs, Preise und Teams bleiben grundsätzlich erhalten. Vor Änderungen sichern. Bei einem frischen Browser startet die Demo mit Beispielwerten. Demo-Daten sind nicht mit Firebase synchronisiert.

## Neue Funktionen testen
- Team: Pokémon hinzufügen, Wesen und Fähigkeit, vier Attacken und sechs SP-Werte einstellen. Maximal 32 pro Wert und 66 insgesamt. Bei Bedarf Pokédex-Hinweise laden (Internet erforderlich; allgemeine PokéAPI-Daten, nicht Champions-verifiziert).
- Karte: neue Runs besitzen eine variable Wegführung und Vegetation; Küstenkontur und Bergregionen sind fest.
- Admin: Kategoriepreise gesammelt ändern, Starterbundles über Auswahlfelder erstellen/entfernen, letzte Adminaktionen ansehen, JSON-Sicherung exportieren, letztes Kampfergebnis zurücknehmen (vor Folgekäufen bzw. neuem Team, kein Championsieg).
- Firebase: siehe README. Für echte Accounts ist Konfiguration und Deployment nötig. Es gibt noch keinen Live-Multiplayertest.

## Beta-Freigabe
Dies ist ein Entwicklungsstand, keine abgeschlossene Closed Beta. `node test.mjs` prüft die Spiellogik. Der Browser-End-to-End-Test war in der Entwicklungsumgebung durch eine Netzwerksperre nicht ausführbar. Externe Daten und Sprites wurden nicht live verifiziert. Der Katalog bleibt der manuell erstellte M-C-Katalog aus v0.2 (263 Pokémon/Formen, 81 Mega, 85 Items). Vollständiger Champions-Abgleich, deutsche Katalognamen, Pokémon-spezifische Legalität und Showdown-Importtest fehlen. Eine JSON-Sicherung ist ein Export, keine Wiederherstellung über die App.
