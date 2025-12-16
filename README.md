# Triple Momentum Indicator

Ein umfassender TradingView-Indikator, der drei EMAs plottet und Buy/Sell-Signale generiert, wenn der Fast EMA den Slow EMA kreuzt.

## Features

### Moving Averages (MAs)
- **Fast MA**: Schneller gleitender Durchschnitt (Standard: 10 EMA auf Close)
- **Slow MA**: Langsamer gleitender Durchschnitt (Standard: 30 EMA auf Close)
- **Filter MA**: Filter-MA für Trendrichtung (Standard: 200 EMA auf Open)

Alle MAs unterstützen folgende Typen:
- EMA (Exponential Moving Average)
- SMA (Simple Moving Average)
- WMA (Weighted Moving Average)
- VWMA (Volume Weighted Moving Average)
- RMA (Relative Moving Average)
- HMA (Hull Moving Average)

### Signale
- **Buy Signal**: Wenn Fast MA den Slow MA von unten nach oben kreuzt (bullisch)
- **Sell/Short Signal**: Wenn Fast MA den Slow MA von oben nach unten kreuzt (bärisch)

### Filter
- **Filter MA**: Signale können gefiltert werden, sodass nur Buys über dem Filter MA und nur Sells unter dem Filter MA erscheinen
- **Range Detector**: Erkennt Seitwärtsphasen und filtert Signale während dieser Phasen heraus

### Targets & Stop Loss
- **Stop Loss**: Basierend auf ATR, Prozent oder Punkten
- **3 Target-Level**: Jedes konfigurierbar als R:R (Risk:Reward), ATR, Prozent oder Punkte
- **Breakeven**: Automatische BE-Trigger-Funktion mit konfigurierbarem Auslösepunkt

### Visuelle Elemente
- Farbige Linien für Entry, Stop Loss, Targets und BE-Trigger
- Labels mit Preisinformationen
- Gefüllte Boxen zwischen den Target-Levels
- Info-Tabelle mit aktuellen MA-Werten

### Alerts
- Entry Alerts (Buy/Sell)
- Target Alerts (wenn Targets erreicht werden)
- Stop Loss Alerts
- Riskier Alerts (Signale die nicht alle Filter erfüllen)

## Installation

1. Öffne TradingView
2. Gehe zu Pine Script Editor
3. Kopiere den Code aus `TripleMomentumIndicator.pine`
4. Klicke auf "Add to Chart"

## Einstellungen

### ALERTS
| Einstellung | Beschreibung | Standard |
|------------|--------------|----------|
| Filter alerts with the filter MA | Filtert Signale mit dem Filter MA | Aus |
| Filter alerts with the range detector | Filtert Signale in Seitwärtsphasen | An |
| Show entry alerts | Zeigt Entry-Signale an | An |
| Show target alerts | Zeigt Target-Alerts an | An |

### FAST MA
| Einstellung | Beschreibung | Standard |
|------------|--------------|----------|
| Typ | MA-Typ | EMA |
| Quelle | Preisquelle | Close |
| Länge | Periode | 10 |

### SLOW MA
| Einstellung | Beschreibung | Standard |
|------------|--------------|----------|
| Typ | MA-Typ | EMA |
| Quelle | Preisquelle | Close |
| Länge | Periode | 30 |

### FILTER MA
| Einstellung | Beschreibung | Standard |
|------------|--------------|----------|
| Typ | MA-Typ | EMA |
| Quelle | Preisquelle | Open |
| Länge | Periode | 200 |
| Füllen | Füllt Bereich zwischen Preis und Filter MA | Aus |

### TARGETS
| Einstellung | Beschreibung | Standard |
|------------|--------------|----------|
| Target 1-3 | Target-Werte und Berechnungsmethode | 1, 2, 3 R:R |
| Stop Loss | Stop Loss Berechnung | 1 ATR |
| Breakeven | BE-Trigger Einstellungen | 1 R:R, Move 0 |
| Line style | Linienstil | Gestrichelt |
| Label size | Labelgröße | Normal |
| Include price | Preis im Label anzeigen | An |
| Offset | Label-Abstand | 10 Bars |

## Beispiel-Nutzung

1. **Einfaches Setup**: 
   - Verwende die Standardeinstellungen
   - Buy bei bullischem Crossover (Fast über Slow)
   - Sell bei bärischem Crossover (Fast unter Slow)

2. **Konservatives Setup**:
   - Aktiviere "Filter alerts with the filter MA"
   - Nur Long-Trades wenn Preis über 200 EMA
   - Nur Short-Trades wenn Preis unter 200 EMA

3. **Aggressive Setup**:
   - Deaktiviere alle Filter
   - Nutze kürzere MA-Perioden (z.B. 5/15)

## Lizenz

Mozilla Public License 2.0
