# Changelog: ewige-Addon (LMOnext)

Dieses Addon war bis LMOnext 1.9.0-beta Teil des Core-Pakets. Mit der
Einführung des Addon-Manager-Frameworks (Beitrag Torsten Hofmann) wurde es
als eigenständiges, self-contained Paket extrahiert.

Die vollständige Entwicklungshistorie bis zur Extraktion steht im
CHANGELOG.md des LMOnext-Kernprojekts unter den Abschnitten
`addon/ewige/*`.

## Aktuelle Version: 1.0.2

- Als eigenständiges addon.json-Paket verpackt (Templates/Sprachdateien
  jetzt lokal im Addon statt zentral im Core), installierbar über
  Administrator → Addons.

## addon/ewige/lmo-ewigetab.php

- Changelog: 1.1.0 - Alle hartcodierten deutschen Texte durch tf()-Aufrufe ersetzt (Seiten-/Tabellentitel, Fehlermeldungen bei fehlendem Parameter/Template, Fußzeilen). Zusätzlich fehlte der loadLanguages()-Aufruf komplett - Sprachdateien wurden bislang nie geladen. Jetzt ergänzt mit korrektem Manifest-Namen "ewige-tabelle" (nicht Ordnername "ewige").

## Sprachdateien (lang/de.php, lang/en.php)

- Neu hinzugefügt: enthalten jetzt die 9 ewige_*-Schlüssel für Titel,
  Fehlermeldungen und Fußzeilen des Ewige-Tabelle-Addons.

## Version 1.2.0 (Sicherheitsüberarbeitung)

- HINWEIS: Version bewusst auf 1.2.0 gesprungen (nicht 1.1.1), da eine
  Version 1.1.1 mit anderen, extern angekündigten inhaltlichen Fixes
  (Sortierung, $wertung-Parameter, Docblock) noch nicht vorlag und keine
  Versionskollision riskiert werden sollte - siehe frühere Chat-Notiz.
  Falls diese Fixes nachgereicht werden, bitte in einer FOLGEVERSION
  (z.B. 1.2.1) einarbeiten lassen, nicht rückwirkend als 1.1.1.
- lmo-ewigetab.php 1.2.0: Aufruf-Erkennung auf die neue Konstante
  LMO_ADDON_STANDALONE_CALL umgestellt (gesetzt vom neuen zentralen
  Controller /addon-run.php). Der direkte URL-Aufruf ist per
  addon/.htaccess jetzt komplett gesperrt - Einbettungen müssen ab sofort
  über /addon-run.php?addon=ewige-tabelle&file=lmo-ewigetab.php&...
  laufen, NICHT mehr über /addon/ewige/lmo-ewigetab.php.
- Neues Manifest-Feld "standalone_entrypoints": ["lmo-ewigetab.php"].
- Asset-Pfadauflösung (ewigeProjectRootUrlPrefix()) nutzt jetzt bevorzugt
  die vom Controller gelieferte LMO_ADDON_WEB_BASE.

**WICHTIG für bestehende Einbettungen:** URL wie oben anpassen, falls
bereits per iframe/URL extern eingebunden.
