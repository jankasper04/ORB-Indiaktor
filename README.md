# Opening Range Breakout (ORB) Trading Strategy

## Übersicht / Overview

Diese Pine Script Strategie implementiert das **Opening Range Breakout** Konzept mit folgenden Kernfunktionen:

1. **15-Minuten Opening Range** (einstellbar)
2. **5-Minuten Kerzen-Breakout** für Entry-Bestätigung
3. **Flexible Stop Loss Optionen**
4. **Flexible Take Profit Optionen**

---

## Dateien / Files

| Datei | Beschreibung |
|-------|--------------|
| `Opening_Range_Breakout_Strategy.pine` | Basis-Version der Strategie |
| `Opening_Range_Breakout_Strategy_Extended.pine` | Erweiterte Version mit zusätzlichen Features |

---

## Strategie Konzept

### Opening Range (OR)
Die Opening Range wird definiert als das High und Low der ersten X Minuten nach Markteröffnung (Standard: 15 Minuten).

```
ORH (Opening Range High) = Höchster Preis während der OR Periode
ORL (Opening Range Low) = Tiefster Preis während der OR Periode
ORM (Opening Range Mid) = (ORH + ORL) / 2 = 50% Level
OR Breite = ORH - ORL
```

### Breakout Signal
Nach Abschluss der OR wartet die Strategie auf einen Breakout:
- **Long Entry**: Wenn der Preis über ORH schließt (auf 5-Min Basis)
- **Short Entry**: Wenn der Preis unter ORL schließt (auf 5-Min Basis)

---

## Stop Loss Optionen

### 1. 50% Level (ORM) - Standard
Der Stop Loss wird an der Mitte der Opening Range platziert.
```
SL = ORM = (ORH + ORL) / 2
```

### 2. ATR Basiert
Stop Loss basierend auf dem Average True Range:
```
Long SL = Entry - (ATR × Multiplikator)
Short SL = Entry + (ATR × Multiplikator)
```

### 3. Market Structure
Stop Loss am nächsten Swing High/Low:
```
Long SL = Niedrigstes Swing Low der letzten X Kerzen
Short SL = Höchstes Swing High der letzten X Kerzen
```

### 4. OR Gegenseite (Extended Version)
```
Long SL = ORL
Short SL = ORH
```

### 5. Fester Prozentsatz (Extended Version)
```
Long SL = Entry × (1 - Prozentsatz/100)
Short SL = Entry × (1 + Prozentsatz/100)
```

---

## Take Profit Optionen

### 1. Standard Deviation (SD)
Basierend auf der OR Breite:
```
1. SD: TP = ORH + OR_Breite (Long) oder ORL - OR_Breite (Short)
2. SD: TP = ORH + (OR_Breite × 2) (Long) oder ORL - (OR_Breite × 2) (Short)
```

### 2. Risk:Reward Verhältnis
Basierend auf der SL Distanz:
```
R:R 1:1: TP = Entry + Risk_Distanz (Long)
R:R 1:2: TP = Entry + (Risk_Distanz × 2) (Long)
R:R 1:3: TP = Entry + (Risk_Distanz × 3) (Long)
Custom R:R: TP = Entry + (Risk_Distanz × Custom_Faktor) (Long)
```

### 3. ATR Basiert (Extended Version)
```
Long TP = Entry + (ATR × Multiplikator)
Short TP = Entry - (ATR × Multiplikator)
```

### 4. Fester Prozentsatz (Extended Version)
```
Long TP = Entry × (1 + Prozentsatz/100)
Short TP = Entry × (1 - Prozentsatz/100)
```

---

## Einstellungen / Settings

### Opening Range Settings
| Parameter | Beschreibung | Standard |
|-----------|--------------|----------|
| OR Periode | Dauer der Opening Range in Minuten | 15 |
| OR Start Zeit | Startzeit im Format HHMM | 0930 |
| Zeitzone | Zeitzone für OR Berechnung | UTC-5 / America/New_York |

### Breakout Settings
| Parameter | Beschreibung | Standard |
|-----------|--------------|----------|
| Breakout Timeframe | Timeframe für Breakout-Bestätigung | 5 Minuten |
| Breakout Bestätigung | Close, Wick, oder Beide | Kerzen Close |
| Allow Long/Short | Handelsrichtung erlauben | Beide aktiviert |
| Nur erster Breakout | Nur erstes Signal pro Tag | Aktiviert |

### Stop Loss Settings
| Parameter | Beschreibung | Standard |
|-----------|--------------|----------|
| SL Typ | Art des Stop Loss | 50% Level (ORM) |
| ATR Periode | Periode für ATR Berechnung | 14 |
| ATR Multiplikator | Multiplikator für ATR SL | 1.5 |
| Swing Lookback | Kerzen für Market Structure | 5 |
| SL Buffer | Zusätzlicher Puffer in Ticks | 0 |

### Take Profit Settings
| Parameter | Beschreibung | Standard |
|-----------|--------------|----------|
| TP Typ | Art des Take Profit | 1. Standard Deviation |
| SD Multiplikator | Multiplikator für SD | 1.0 |
| Custom R:R | Benutzerdefiniertes Verhältnis | 1.5 |

---

## Installation in TradingView

1. Öffne TradingView und gehe zu **Pine Editor**
2. Erstelle ein neues Skript (Strg/Cmd + N)
3. Kopiere den gesamten Code aus einer der `.pine` Dateien
4. Füge den Code im Pine Editor ein
5. Klicke auf **Zur Chart hinzufügen** oder **Add to Chart**
6. Konfiguriere die Einstellungen nach Bedarf

---

## Beispiel-Konfigurationen

### Konservativ (geringes Risiko)
```
SL Typ: 50% Level (ORM)
TP Typ: Risk:Reward 1:1
Nur erster Breakout: Aktiviert
```

### Moderat
```
SL Typ: 50% Level (ORM)
TP Typ: 1. Standard Deviation
SD Multiplikator: 1.0
```

### Aggressiv (höheres Risiko/Reward)
```
SL Typ: ATR Basiert (Mult: 1.0)
TP Typ: Risk:Reward 1:2
Nur erster Breakout: Deaktiviert
```

### Mit Market Structure
```
SL Typ: Market Structure
Swing Lookback: 5
TP Typ: 2. Standard Deviation
```

---

## Visuelle Darstellung

Die Strategie zeigt folgende Elemente auf dem Chart:

| Element | Farbe | Beschreibung |
|---------|-------|--------------|
| OR Box | Grau (gefüllt) | Opening Range Bereich |
| ORH Linie | Grau | Opening Range High |
| ORL Linie | Grau | Opening Range Low |
| ORM Linie | Grau (gestrichelt) | Opening Range Mid (50%) |
| SL Linie | Rot (gepunktet) | Stop Loss Level |
| TP Linie | Grün (gepunktet) | Take Profit Level |
| Entry Linie | Blau | Einstiegspreis |
| Long Signal | Grünes Dreieck ▲ | Long Entry Signal |
| Short Signal | Rotes Dreieck ▼ | Short Entry Signal |

---

## Alerts

Die Strategie bietet folgende Alert-Bedingungen:

1. **Long Breakout Signal** - Wenn Long Entry ausgelöst wird
2. **Short Breakout Signal** - Wenn Short Entry ausgelöst wird
3. **Opening Range Complete** - Wenn die OR fertig etabliert ist
4. **EOD Close** - Wenn Positionen am Tagesende geschlossen werden

---

## Filter Optionen (Extended Version)

| Filter | Beschreibung |
|--------|--------------|
| Direction Bias | Nur Trades in Richtung des Bias (vorheriger ORM Vergleich) |
| EMA Trend Filter | Nur Long über EMA, Short unter EMA |
| Volumen Filter | Nur bei überdurchschnittlichem Volumen |
| Min/Max OR Größe | Filter basierend auf OR Breite |
| Handelszeiten | Nur innerhalb definierter Zeiten handeln |
| Freitag Filter | Freitags nicht handeln |

---

## Partial Take Profit (Extended Version)

Die erweiterte Version bietet Partial Take Profit:

1. Einen Teil der Position (z.B. 50%) am ersten Target schließen
2. SL auf Breakeven verschieben nach Partial TP
3. Restposition bis zum Haupt-TP laufen lassen

---

## Wichtige Hinweise

⚠️ **Risiko-Warnung**: Diese Strategie ist nur zu Bildungszwecken gedacht. Trading birgt erhebliche finanzielle Risiken. Testen Sie jede Strategie ausführlich im Paper Trading bevor Sie echtes Kapital einsetzen.

💡 **Best Practices**:
- Backtesten auf verschiedenen Märkten und Zeiträumen
- Parameter an den gehandelten Markt anpassen
- Nicht während wichtiger Nachrichten handeln
- Risikomanagement beachten (max. 1-2% Risiko pro Trade)

---

## Lizenz

This work is licensed under a Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)
https://creativecommons.org/licenses/by-nc-sa/4.0/

Based on concepts from LuxAlgo Opening Range Indicator.
