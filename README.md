# Dachlast Open Data — Dachzelte, Dachboxen, Dachträger und Fahrzeugmarkisen

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21798284.svg)](https://doi.org/10.5281/zenodo.21798284)

Offene Datensätze zum deutschen Markt für Dachaufbauten, erhoben von [dachlast.de](https://dachlast.de/).
Vier Datensätze, jede Zeile mit Quell-URL, Lizenz **CC BY 4.0**.

*[English version below](#english)*

| Datensatz | Zeilen | Hersteller | Kern-Felder |
|---|---:|---:|---|
| [`dachzelte`](data/dachzelte.csv) | 646 | 107 | Bauart, Liegefläche, **Packhöhe geschlossen**, Gewicht |
| [`dachboxen`](data/dachboxen.csv) | 157 | 19 | Außenmaße, Volumen, Eigengewicht, max. Zuladung |
| [`dachtraeger`](data/dachtraeger.csv) | 191 | 58 | Montagearten, Eigengewicht, **Traglast dyn./stat.** |
| [`markisen`](data/markisen.csv) | 272 | 39 | Länge, Auslage, Gewicht, **Montagebasis** |

Jeder Datensatz liegt als JSON und als CSV (UTF-8, Komma-getrennt) vor.

## Warum es diese Daten gibt

Wer ein Dachzelt oder eine Dachbox kaufen will, braucht zwei Zahlen, die kein Hersteller vergleichbar veröffentlicht:

1. **Die Packhöhe im geschlossenen Zustand.** Sie bestimmt den Luftwiderstand und damit den Mehrverbrauch — nicht das Gewicht. Auf ebener Strecke gehen 95 bis 98 % des Mehrverbrauchs auf die Luft.
2. **Das Gesamtgewicht auf dem Dach.** Träger, Aufbau und Markise zusammen müssen unter der zulässigen Dachlast des Fahrzeugs bleiben, die bei Pkw meist zwischen 50 und 100 kg liegt.

Beides steht verstreut in Produktseiten, PDF-Datenblättern und Händlerangaben. Diese Datensätze führen es zusammen.

## Was die Daten besonders macht

**Lücken sind dokumentiert, nicht geschätzt.** Eine leere Zelle heißt: der Hersteller veröffentlicht den Wert nicht. Nichts ist interpoliert, nichts von einer anderen Modellgröße übernommen.

**Bei den Dachträgern ist die Lücke selbst ein Ergebnis.** Für 132 der 191 Träger nennt der Hersteller eine Traglast. Bei den übrigen 59 steht im Feld `traglast_notiz`, warum nicht — Rhino-Rack, Upracks, Front Runner und horntools veröffentlichen bewusst keine Systemtraglast und verweisen stattdessen auf die Dachlast des jeweiligen Fahrzeugs. Vier Hersteller geben die Traglast *pro Querträger* an; diese Werte stehen in einer eigenen Spalte, damit sie niemand als Systemwert verrechnet.

**Bei den Markisen beantwortet `montagebasis` die eigentliche Frage.** Eine Markise zählt nur dann zur Dachlast, wenn sie auf dem Dach sitzt: 150 der 272 Varianten tun das, 73 hängen an der Seitenwand und 49 in der Kederschiene — deren Gewicht geht in die Wand, nicht ins Dach.

## Felder

Vollständige Feldbeschreibungen: <https://dachlast.de/daten/>

Die JSON-Dateien enthalten zusätzlich Metadaten (`stand`, `anzahl`, `lizenz`, `hinweis`) sowie bei `markisen.json` das Regelwerk zur Zuordnung Markise → Fahrzeugklasse (16 Zuordnungs- und 13 Prüfregeln).

## Nutzung

```python
import pandas as pd
t = pd.read_csv("https://dachlast.de/daten/dachzelte.csv")
print(t.nsmallest(10, "packhoehe_cm")[["marke", "name", "packhoehe_cm", "gewicht_kg"]])
```

Die Dateien werden mit `Access-Control-Allow-Origin: *` ausgeliefert und lassen sich direkt im Browser laden.

## Lizenz und Zitation

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.de) — jede Nutzung erlaubt, auch kommerziell, einzige Bedingung ist die Namensnennung:

```
dachlast.de (2026): Dachlast Open Data. Version 1.0.0. Zenodo.
https://doi.org/10.5281/zenodo.21798284 (CC BY 4.0)
```

Kurzform ohne DOI:

```
Datenquelle: dachlast.de – https://dachlast.de/daten/ (CC BY 4.0)
```

Angaben ohne Gewähr; verbindlich sind die Angaben des Herstellers und die Betriebsanleitung des Fahrzeugs. Die Zuordnung Markise → Fahrzeug ist eine Einschätzung nach Länge, Bauart und Montagebasis, **keine Herstellerfreigabe**.

## Korrekturen

Fehler gefunden oder ein fehlendes Modell? [Issue eröffnen](../../issues) — mit Link auf die Herstellerseite, von der der Wert stammt. Korrekturen fließen in die Datenbank auf dachlast.de zurück.

Methodik: <https://dachlast.de/methodik.html>

---

<a name="english"></a>

## English

Open datasets on the German market for roof-mounted equipment, compiled by [dachlast.de](https://dachlast.de/): 646 roof tents, 157 roof boxes, 191 roof racks and 272 vehicle awnings. Every row carries the source URL of the manufacturer page it was taken from. JSON and CSV, licensed **CC BY 4.0**.

Two numbers drive every buying decision and neither is published comparably by manufacturers: the **packed height** of a roof tent (which determines aerodynamic drag and therefore fuel consumption — not the weight) and the **combined weight** of rack, tent and awning, which has to stay below the vehicle's permissible roof load, typically 50 to 100 kg on a passenger car.

Empty cells mean the manufacturer does not publish the value. Nothing is estimated or inferred from a different size. For roof racks, the `traglast_notiz` column explains each gap: several manufacturers deliberately publish no system load rating and refer to the vehicle's roof load instead. For awnings, `montagebasis` states whether the awning is mounted on the roof (and thus counts against the roof load) or on the side wall.

Field documentation: <https://dachlast.de/daten/> · Methodology: <https://dachlast.de/methodik.html>

Attribution: `Data source: dachlast.de – https://dachlast.de/daten/ (CC BY 4.0)`
