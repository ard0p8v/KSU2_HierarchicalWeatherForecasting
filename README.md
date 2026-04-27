# Hierarchické předpovídání teploty — Bottom-Up vs Top-Down

**Předmět:** Strojové učení II (KSU2)  
**Autor:** Bc. Pavel Ardolf  
**Název:** KSU2_HierarchicalWeatherForecasting

---

## Popis projektu

Cílem projektu je implementace a porovnání dvou základních metod předpovídání na hierarchicky uspořádaných datech: **Bottom-Up** a **Top-Down**. Jako datový zdroj slouží historické meteorologické záznamy (denní teploty) za období 2019–2023 pro více než 20 evropských měst, stažené pomocí Open-Meteo API.

### Hierarchická struktura dat

```
Evropa (kontinent)
├── CZ — Praha, Brno, Ostrava, Hradec Králové, Plzeň, Liberec
├── DE — Berlín, Mnichov, Hamburg, Frankfurt
├── AT — Vídeň, Salzburg, Innsbruck
├── PL — Varšava, Krakov, Wrocław
└── SK — Bratislava, Košice
```

### Metody předpovídání

| Metoda | Princip |
|---|---|
| **Bottom-Up** | Prophet model pro každé město zvlášť → agregace nahoru (město → stát → kontinent) |
| **Top-Down** | Prophet model na úrovni Evropy → disagregace dolů pomocí historických offsetů |

### Evaluační metriky

- **MAE** — střední absolutní chyba
- **RMSE** — odmocnina střední kvadratické chyby
- **R²** — koeficient determinace

## Technologie

- Python 3.9+
- Prophet (Facebook/Meta) — predikce časových řad
- Open-Meteo API — historická meteorologická data
- Pandas, NumPy, Matplotlib, scikit-learn
- Google Colab

## Spuštění

### Google Colab
### Lokální spuštění
```bash
pip install prophet openmeteo-requests requests-cache retry-requests pandas numpy matplotlib scikit-learn
python -m jupyter notebook HierarchicalForecasting.ipynb
```

## Struktura notebooku

| Sekce | Obsah |
|---|---|
| 1. Cíl projektu | Definice úlohy — hierarchické předpovídání |
| 2. Popis hierarchie a dat | Tříúrovňová struktura: kontinent → stát → město |
| 3. Metodika | Bottom-Up, Top-Down, Prophet, evaluace |
| 4. Vyhodnocení výsledků | Metriky MAE, RMSE, R²; porovnání metod |
| 5. Závěr | Shrnutí — Bottom-Up lepší lokálně, Top-Down efektivnější pro celkové trendy |

## Výstupy

```
data/
  weather_city.csv          — denní teploty na úrovni měst
  weather_country.csv       — agregace na úrovni států
  weather_continent.csv     — agregace na úrovni Evropy

output/
  metrics.csv               — MAE, RMSE, R² pro obě metody
  forecast_continent.png    — srovnání predikcí na úrovni Evropy
  forecast_country_CZ.png   — srovnání pro Českou republiku
  forecast_city_Praha.png   — srovnání pro Prahu
  ...
```

## Literatura

1. Štěkerová, K. *Predikce z hierarchických prodejních dat*. Podklady pro zápočtový úkol k předmětu SU2. UHK, 2026.
2. Makridakis, S. et al. *M5 accuracy competition: Results, findings, and conclusions*. International Journal of Forecasting, 2021.
3. Osipchyk, I. *Sales Forecasting using Gradient Boosting Trees*. Bakalářská práce, FIM UHK, 2021.
4. Taylor, S. J. a Letham, B. *Forecasting at scale (Prophet)*. Facebook Open Source, 2017.
5. Open-Meteo. *Historical Weather Data API*. https://open-meteo.com/
