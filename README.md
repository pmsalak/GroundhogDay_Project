# Groundhog Day Project


## Groundhog Day!

``` python
import requests
from bs4 import BeautifulSoup
import pandas as pd
```

``` python
link  = 'https://countdowntogroundhogday.com/forecasters/'
link_request = requests.get(link)
pd.to_pickle(link_request.text, 'forecasters.pkl')
```

``` python
forecasters_data = pd.read_pickle('forecasters.pkl')

import io
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
