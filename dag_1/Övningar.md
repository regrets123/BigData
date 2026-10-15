# Övningar dag 1

## Övning 1 – Hur stor blir datan?

En anläggning har 2 500 maskiner. Varje maskin producerar ett meddelande på 160 byte två gånger per sekund.

Beräkna ungefär byte per sekund, GB per dygn och TB per år. Hur förändras lagringsbehovet om systemet sparar tre kopior?

Skriv också två antaganden som beräkningen inte tar hänsyn till.
2500x320 == 800mb bytes per sekund.
800mb x 60 x 24 == 1152000mb == 1152gb per dygn.
1152 x 356 == 410gb
Det tredubblas om vi ska ha 3 kopior. Det tar inte hänsyn till trasiga maskiner eller sensorer som kan sorteras bort ur datan.
Eller felaktiga värden.

## Övning 2 – Läs datasetets dokumentation

Öppna UCI-sidan:

https://archive.ics.uci.edu/dataset/601/ai4i+2020+predictive+maintenance+dataset

Besvara:

1. Är datan verklig eller syntetisk?
Syntetisk
2. Vad representerar en rad?
Ett värde och dess egenskaper.
3. Vilka kolumner är mätvärden?
Allt efter type.
4. Vilken kolumn är målvariabel?
Beror på vilket mål vi har. 
5. Vilka kolumner är identifierare?
6. Vilka kolumner riskerar att läcka svaret till en ML-modell?
7. Vilken licens gäller?

## Laboration – Första mötet med AI4I

Aktivera miljön och hämta datan vid behov:

```bash
source .venv/bin/activate
python dag_1/kod/python/download_data.py
```

```python
import pandas as pd

data = pd.read_csv("dag_1/kod/data/ai4i2020.csv", encoding="utf-8-sig")

print(data.head())
print(data.shape)
print(data.columns)
print(data.dtypes)
print(data.isna().sum())
print(data.duplicated().sum())
print(data.describe())
```

Besvara:

1. Hur många rader och kolumner finns? 5 rader 14 columner. totalt 10 000 och 14.
2. Finns saknade värden eller dubbletter? Nej
3. Hur stor andel av raderna har `Machine failure == 1`? 3.39%, alltså 339 fel.
4. Vad betyder `Type`? Kvalitets id för low medium high. L M H. 
5. Varför bör `UDI` och `Product ID` normalt inte användas som numeriska features? UID är unique id, product id är variant specifik id samt innehåller kvalitets id type. 

Beräkna felandelen:

```python
failure_rate = data["Machine failure"].mean()
print(f"Andel maskinfel: {failure_rate:.2%}")
```

## Individuell projektstart

Skriv högst en sida med:

- valt dataset och länk till källan,
- vad en rad representerar,
- en avgränsad analysfråga,
- tre relevanta kolumner,
- ett kvalitets- eller urvalsproblem,
- en tänkbar visualisering.

## Exit ticket

https://mentorsparks.com/g/2xhUdw

Svara individuellt:

1. Vad är den största begränsningen med datasetet?
2. Vilken kolumn behöver du förstå bättre?
3. Vilken analysfråga vill du arbeta vidare med?
4. Vad vill du repetera nästa lektion?
