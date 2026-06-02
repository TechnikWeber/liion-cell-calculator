# Li-Ion Zell-Test-Rechner (18650 / 21700)

**🔗 Live-Demo:** <https://technikweber.github.io/liion-cell-calculator/>

Ein eigenständiges HTML-Tool zur Planung, Auswertung und Plausibilisierung von Tests an zylindrischen Lithium-Ionen-Zellen (18650, 21700) der gängigen Chemien NMC, NCA und LFP. Eine einzige Datei, keine Installation, läuft offline in jedem modernen Browser.

## Hintergrund

Lithium-Ionen-Zellen altern grundlegend anders als Blei-Batterien:

- Die Lebensdauer halbiert sich näherungsweise je **10 °C** über 25 °C (Battery University), nicht je 7 °C wie bei Blei.
- Bei **Kälte** altern Li-Ion-Zellen durch Lithium-Plating *schneller*, nicht langsamer — die Faustformel gilt nur für erhöhte Temperaturen.
- Statt bloßer Entladetiefe (DoD) bestimmt das genutzte **SoC-Fenster** die Lebensdauer (10–90 % ist deutlich schonender als 0–100 %).
- Geladen wird nach **CC-CV** auf feste Schlussspannung (4,2 V NMC/NCA, 3,65 V LFP) — *ohne* Temperaturkompensation wie bei Blei.

Wer Li-Ion-Zellen testet, kann die Werkzeuge eines Blei-Tools deshalb nicht 1:1 übernehmen. Dieses Tool ist auf die Li-Ion-Realität zugeschnitten.

## Funktionsumfang

Sieben Module, oben die Chemie wählbar (setzt Spannungsfenster und Defaults):

- **▶ Temp→Zyklen** — Zyklen bei 25 °C auf andere Temperatur umrechnen (mit Kältewarnung unter ~15 °C).
- **◀ Rückwärts** — Testzyklen bei erhöhter Temperatur auf 25-°C-Äquivalent zurückrechnen.
- **▭ SoC-Fenster** — Effekt eines engeren Ladefensters (Fensterbreite + obere Grenze).
- **⏱ Testdauer** — Zyklen × Zeit/Zyklus + Auslastung → Testdauer; mit Zeitersparnis durch Prüftemperatur. Warnt ab >45 °C, wo sich Alterungsmechanismen verschieben.
- **⚡ CC-CV Laden** — Ladestrom und grobe Ladezeit aus Kapazität (mAh) und C-Rate; Schlussspannung je Chemie.
- **↻ C-Rate** — Umrechnung mAh / C-Rate / Strom / Dauer in Li-Ion-Konvention.
- **▤ Grenzwerte** — Referenztabelle: Schluss-, Nenn-, Cutoff-Spannung, Lager-SoC, Lade-Rate je Chemie.

## Benutzung

1. `LiIon_Zell_Test_Rechner.html` herunterladen
2. Datei im Browser öffnen (Doppelklick reicht)
3. Oben Chemie wählen, Reiter aufrufen, rechnen

Alle Eingaben werden live ausgewertet. Jedes Modul zeigt den Rechenweg und eine Bandbreite, damit der Charakter als Näherung sichtbar bleibt.

## Formel-Grundlagen

| Modul | Quelle / Konstante |
|---|---|
| Temperatur-Faustformel | `0,5^((T−25)/10)` — Battery University, Arrhenius-Vereinfachung für Li-Ion |
| CC-CV Laden | Standard-Ladeverfahren Li-Ion; Schlussspannung 4,2 V (NMC/NCA) bzw. 3,65 V (LFP) |
| C-Rate | Strom = C-Rate × Kapazität, Dauer = 1/C-Rate |
| SoC-Fenster-Modell | Heuristik: Fensterbreite und obere Grenze als getrennte Faktoren — grobe Größenordnung |
| Grenzwerte | Übliche Datenblattwerte zylindrischer Zellen (je Hersteller leicht abweichend) |

## Sicherheitshinweise

- **Überladung** über die Schlussspannung oder **Tiefentladung** unter den Cutoff schädigt Zellen irreversibel und kann zu thermischem Durchgehen führen.
- Laden **unter 0 °C** vermeiden — Lithium-Plating-Gefahr.
- Lagerung am längsten haltbar bei **~40–50 % SoC** (≈ 3,7 V bei NMC).
- Beschleunigte Alterung über **~45 °C** ist nicht mehr repräsentativ für den Realbetrieb — Alterungsmechanismen verschieben sich.

## Einschränkungen

- Faustformeln und Näherungen — nicht für Sicherheits- oder Zertifizierungsaussagen geeignet.
- Werte gelten für zylindrische Li-Ion-Zellen (NMC/NCA/LFP) und streuen je Hersteller deutlich.
- Pouch- und prismatische Zellen werden nicht explizit abgedeckt, die meisten Formeln sind aber übertragbar.
- Für den relativen Vergleich mehrerer Zellen unter identischen Bedingungen ist keine Umrechnung nötig — das Tool ersetzt keinen Test, es ordnet ein.

## Technik

- Eine einzige HTML-Datei (~20 KB)
- Vanilla JavaScript, kein Build, keine Abhängigkeiten
- Kein Tracking, keine externen Calls — vollständig offline lauffähig

## Lizenz

MIT — Nutzung, Anpassung und Weitergabe frei. Verwendung auf eigene Verantwortung; das Tool ersetzt keine fachliche Prüfung.
