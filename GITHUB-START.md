# Pokémon Burg v0.2 — GitHub-Test

1. ZIP entpacken. Den Inhalt des Ordners `pokemon-burg` in ein neues öffentliches Repository `pokemon-burg` auf GitHub hochladen (auch `.github` für Actions, falls gewünscht).
2. Einfachste Variante ohne Actions: den enthaltenen Ordner `docs` mit hochladen. Settings → Pages → Source: Deploy from a branch → main → /docs → Save.
3. Die URL steht anschließend unter Settings → Pages (typisch https://DEINNAME.github.io/pokemon-burg/).
4. App startet mit Testprofilen, zwei Starterbundles, 1000 Testpunkten und einem Beispiel-Champion. Rolle wechseln → Starterbundle wählen → Shop/Team testen → Admin → Kampf bestätigen und Ergebnis eintragen.
5. Alternative für Git-Nutzer: Source GitHub Actions auswählen; der enthaltene Workflow veröffentlicht `public`.

Keine Firebase-Konfiguration nötig. Daten sind lokal im Browser, nicht zwischen Spielern synchronisiert. Keine echten Admin-Zugangsdaten im Demo-Modus. Für einen neuen Test Browser-Sitedaten löschen. Die ältere v0.1 wird nicht migriert.

## Datenstand
M-C (9. September 2026 bis 2. Dezember 2026 UTC): manuell übertragene Pokémon-/Formenliste aus Bulbapedia, Mega-Zuordnungen und Kampfitems aus Serebii. 263 normale Pokémon/Formen, 81 Mega-Freischaltungen und 85 sonstige Kampfitems inkl. Beeren. Mega-Steine sind Teil der Mega-Freischaltung. Nicht mit dem vollständigen offiziellen Datensatz abgeglichen; abweichende Formen und fehlende Einträge sind möglich. Englische Namen, Typdaten nur für einige Beispiel-Pokémon. Keine vollständigen Learnsets oder SP-Legalitätsprüfung. Preise sind Testwerte. Champions-Sprite-Archiv wie v0.1, externe Bild-URLs nicht geprüft; keine garantierte offizielle Herkunft. 

Quellen:
- https://champions-news.pokemon-home.com/de/page/816.html
- https://bulbapedia.bulbagarden.net/wiki/Regulation_Set_M-C
- https://www.serebii.net/pokemonchampions/items.shtml

Firebase ist weiterhin als experimentelle Option enthalten (siehe README); nicht produktiv getestet. `public` und `docs` sind identische statische Kopien, nach Änderungen an public muss docs aktualisiert werden.
