# Groundhog Day Data Scraping Project


## Background

## Forecaster Data

``` python
import requests
from bs4 import BeautifulSoup
import pandas as pd
import io
```

``` python
link  = 'https://countdowntogroundhogday.com/forecasters/'
link_request = requests.get(link)
pd.to_pickle(link_request.text, 'forecasters.pkl')
```

``` python
forecasters_data = pd.read_pickle('forecasters.pkl')

table = pd.read_html(io.StringIO(forecasters_data), header=0)
forecasters = pd.concat(table)

forecasters
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
&#10;    .dataframe tbody tr th {
        vertical-align: top;
    }
&#10;    .dataframe thead th {
        text-align: right;
    }
</style>

|  | Name | Forecaster Type | Location | Year of Last Known Prediction |
|----|----|----|----|----|
| 0 | Punxsutawney Phil | Groundhog | Punxsutawney, PA | 2026 |
| 1 | Octoraro Orphie | Taxidermy mount Groundhog | Quarryville, PA | 2026 |
| 2 | Poor Richard | Taxidermied Groundhog | York, PA | 2026 |
| 3 | Dunkirk Dave | Groundhog | Dunkirk, NY | 2026 |
| 4 | Oscar the Groundhog | Groundhog | Kutztown, PA | 2021 |
| ... | ... | ... | ... | ... |
| 192 | Paulie the Rabbit | Rabbit | Milltown, NJ | 2026 |
| 193 | Tomothy | Eastern box turtle | Sewell, NJ | 2026 |
| 194 | Hudson the Polar Bear | Polar Bear | Toronto, ON | 2026 |
| 195 | Jessup Giuseppe | Ferret | Jessup, PA | 2026 |
| 196 | Duster | Prairie Dog | Prescott, AZ | 2026 |

<p>197 rows × 4 columns</p>
</div>

``` python
#use regex to make a column for deceased/alive and seperate city and state
```

## Prediction Data

``` python
years = ['2026','2025','2024','2023','2022','2021','2020','2019']
predictions = []

for year in years:
    link = f'https://countdowntogroundhogday.com/predictions/{year}_predictions'
    link_request = requests.get(link)
    table = pd.read_html(io.StringIO(link_request.text), header=0)
    year_predictions = pd.concat(table)
    year_predictions['Year'] = year
    predictions.append(year_predictions)

pd.to_pickle(predictions, 'predictions.pkl')
```

``` python
predictions_data = pd.read_pickle('predictions.pkl')
predictions = pd.concat(predictions_data,ignore_index=True)

predictions
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
&#10;    .dataframe tbody tr th {
        vertical-align: top;
    }
&#10;    .dataframe thead th {
        text-align: right;
    }
</style>

|     | Prediction   | Name              | Type                  | year |
|-----|--------------|-------------------|-----------------------|------|
| 0   | Long Winter  | Athene            | Burrowing owl mascot  | 2026 |
| 1   | Long Winter  | Bagley Beaver     | Beaver Mascot         | 2026 |
| 2   | Long Winter  | Balzac Billy      | Gopher mascot         | 2026 |
| 3   | Early Spring | Bay Beach Bernard | Groundhog             | 2026 |
| 4   | Early Spring | Beans             | Dachshund             | 2026 |
| ... | ...          | ...               | ...                   | ...  |
| 908 | Early Spring | Will and Wiley    | Grizzly bears         | 2019 |
| 909 | Early Spring | Winnipeg Wyn      | Groundhog             | 2019 |
| 910 | Early Spring | Woodstock Willie  | Groundhog             | 2019 |
| 911 | Early Spring | Woody             | Groundhog             | 2019 |
| 912 | Long Winter  | Yahdee            | Taxidermied Groundhog | 2019 |

<p>913 rows × 4 columns</p>
</div>
