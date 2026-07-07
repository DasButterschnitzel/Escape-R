# Escape-R

Ein Tool zur Generierung von REWE-Selbstbedienungskassen-Ausgangscodes.

## Hintergrund

An vielen REWE-Selbstbedienungskassen muss beim Verlassen des Marktes ein Barcode
von der Rechnung an einer Schranke gescannt werden. Der Code ist wie folgt aufgebaut:

| Teil | Länge | Beschreibung |
|---|---|---|
| Präfix | 4 Ziffern | immer `2300` |
| Kassennummer | 2 Ziffern | z.B. `06` |
| Timestamp | 10 Ziffern | Unix-Timestamp des Einkaufs |

Beispiel: `2300061748450386` → Präfix `2300`, Kasse `06`, Timestamp `1748450386`
(entspricht 2025-05-28).

An der Schranke wird offenbar nicht geprüft, ob der Code tatsächlich von einer
Kasse ausgestellt wurde — es wird nur geprüft, ob der Timestamp aktuell genug
ist. Ein Code mit dem maximalen 32-Bit-Unix-Timestamp `2147483647`
(19.01.2038) ist daher dauerhaft "aktuell genug" und bleibt gültig, bis dieses
Datum erreicht ist.

## Tool

`index.html` ist ein eigenständiges Web-Tool (keine Installation nötig), mit
dem sich solche Codes erzeugen lassen:

- Auswahl der Kassennummer (01–20)
- Modus **Aktuell**: nutzt den aktuellen Unix-Timestamp
- Modus **Universal**: nutzt den Timestamp `2147483647` (gültig bis 2038-01-19)
- Rendert den generierten Code als scanbaren ITF-Barcode

Einfach `index.html` im Browser öffnen.
