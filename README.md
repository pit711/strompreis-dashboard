# Strompreis-Dashboard

Einseitiges HTML-Dashboard für **Day-Ahead Strompreise DE-LU** (EPEX Spot) mit realistischer Endpreis-Berechnung inklusive Netzentgelten, Steuern und Umlagen. Kein Build, kein Server, keine Anmeldung – einfach `index.html` im Browser öffnen.

![single-file](https://img.shields.io/badge/single--file-HTML-blue) ![data](https://img.shields.io/badge/data-a%C3%9Fttar%20API-orange) ![license](https://img.shields.io/badge/license-MIT-green)

## Features

- **Live Day-Ahead Preise** von der [aWATTar API](https://www.awattar.de/services/api) (EPEX Spot DE-LU)
- **Tages-** und **Wochenansicht** mit Navigation (vor/zurück)
- **Vollständige Endpreis-Berechnung** aus:
  - EPEX Spot-Preis (stündlich)
  - Netzentgelt des gewählten Verteilnetzbetreibers
  - Stromsteuer (2,05 ct/kWh)
  - Umlagen (§19 StromNEV, KWKG, Offshore, Abschaltbare Lasten ≈ 2,226 ct/kWh)
  - Konzessionsabgabe (1,66 ct/kWh, Haushalt)
  - Messstellenbetrieb (0,50 ct/kWh)
  - 19 % Mehrwertsteuer (umschaltbar netto/brutto)
- **22 deutsche Verteilnetzbetreiber** vorkonfiguriert mit Netzentgelten 2026 (BW, BY, RLP, NRW, NI, SH, HH, HB, BB, SN, TH, BE, SL) + eigener Wert
- **Farbcodierung**: günstig (grün), mittel (gelb), teuer (rot), negativ (blau)
- **Spot-only Modus** für den nackten Börsenpreis ohne Aufschläge
- **Tagesübersicht** mit Min/Max/Durchschnitt

## Nutzung

1. [`index.html`](index.html) herunterladen
2. Im Browser öffnen (Chrome, Firefox, Edge, Safari) – oder direkt im Browser unter [raw.githubusercontent.com/pit711/strompreis-dashboard/main/index.html](https://raw.githubusercontent.com/pit711/strompreis-dashboard/main/index.html)
3. Oben rechts den Verteilnetzbetreiber (DSO) auswählen – die Liste ist nach Bundesland gruppiert
4. Optional zwischen **Tag/Woche** und **netto/brutto** umschalten

Die aWATTar API ist frei zugänglich (kein Key nötig), Preise werden stündlich aktualisiert. Morgen's Preise werden üblicherweise gegen 14 Uhr CET veröffentlicht.

## Datenquellen

- **Spot-Preise**: [api.awattar.de/v1/marketdata](https://www.awattar.de/services/api) (EPEX Spot Auktion, Day-Ahead DE-LU)
- **Netzentgelte 2026**: Eigene Recherche aus den Preisblättern 2026 der jeweiligen Netzbetreiber sowie GET AG Trendanalyse / BNetzA-Veröffentlichungen (Stand November 2025)
- **Steuern/Umlagen**: Bundesnetzagentur, Energieversorger-Preisblätter Haushaltskunden < 6.000 kWh/a

## Genauigkeit

Die Endpreis-Berechnung ist eine **gute Schätzung** für dynamische Tarife (z. B. Tibber, aWATTar, Octopus, Rabot Charge) auf Basis typischer Haushaltskunden-Konditionen. Abweichungen von wenigen Cent je kWh sind normal, weil:

- Konzessionsabgabe je nach Gemeindegröße zwischen 1,32 und 2,39 ct/kWh variiert
- Messstellenbetrieb anbieterabhängig ist
- Manche Tarife feste Aufschläge auf den Spot-Preis haben
- Bilanzkreismanagement und Vertriebsmarge individuell sind

Für die **vergleichende Einordnung günstig/mittel/teuer** reicht die Genauigkeit allemal.

## Technik

- Vanilla JS, Chart.js nicht nötig (natives SVG/DOM)
- Source Serif 4 + Source Sans 3 – werden lokal genutzt, falls installiert (kein externer Font-Load)
- CORS-freundlich (aWATTar erlaubt Browser-Requests)
- Cache im Speicher pro Tag

## Rechtliches

Keine Anlage-, Energie- oder Steuerberatung. Alle Preisbestandteile sind öffentlich recherchiert und können sich ändern (insbesondere Netzentgelte werden jährlich neu festgesetzt). Verbindlich ist immer dein Liefervertrag.

### Datenquellen & Nutzungsbedingungen

- **aWATTar API** (`api.awattar.de`): Die Nutzung der API ist für den **persönlichen, nicht-kommerziellen Gebrauch** bestimmt. Für kommerzielle Nutzung bitte die [Nutzungsbedingungen von aWATTar](https://www.awattar.de) beachten.
- **EPEX Spot SE**: Die Marktdaten (Day-Ahead-Preise DE-LU) stammen von der EPEX Spot SE und werden durch die aWATTar API bereitgestellt. Die Daten unterliegen den Nutzungsbedingungen von EPEX Spot SE und dürfen nicht für kommerzielle Zwecke weiterverwendet werden.

### Datenschutz

Alle Berechnungen erfolgen lokal im Browser. Es werden keine Cookies gesetzt, kein Tracking eingesetzt und keine externen Dienste (außer der aWATTar API für die Preisdaten) geladen. Google Fonts und ähnliche externe Ressourcen werden **nicht** eingebunden (DSGVO-konform).

## Lizenz

MIT
