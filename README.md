---
license: cc0-1.0
task_categories:
  - feature-extraction
language:
  - en
tags:
  - weather
  - storms
  - tornadoes
  - natural-disasters
  - noaa
  - geospatial
  - united-states
  - climate
pretty_name: NOAA Significant US Storms (1950-2025)
size_categories:
  - 10K<n<100K
dataset_info:
  features:
    - name: latitude
      dtype: float64
    - name: longitude
      dtype: float64
    - name: name
      dtype: string
    - name: description
      dtype: string
    - name: category
      dtype: string
    - name: date
      dtype: string
    - name: country
      dtype: string
    - name: event_type
      dtype: string
    - name: state
      dtype: string
    - name: magnitude
      dtype: string
    - name: injuries
      dtype: string
    - name: fatalities
      dtype: string
    - name: damage_property
      dtype: string
    - name: source
      dtype: string
  splits:
    - name: train
      num_examples: 14770
---

# NOAA Significant US Storms (1950-2025)

14,770 significant weather events curated from NOAA's 1.23 million storm records.

## What's Inside

- 14,770 major storms across 75 years
- F3/EF3+ tornadoes (severe/violent)
- Fatal events (1+ deaths)
- High-damage storms ($1M+)
- Full coordinates for mapping

## Filtering Criteria

This dataset keeps 1.2% of NOAA's storm events database: the events that meet at least one of these thresholds.

| Criterion | Threshold |
|-----------|-----------|
| Major Tornadoes | F3/EF3 and higher |
| Fatal Events | 1+ direct deaths |
| High Damage | $1,000,000+ property damage |
| High Injuries | 10+ injuries |
| Severe Flash Floods | Fatal (1+ deaths) |
| Severe Winter Storms | Fatal (5+ deaths) |

Events meeting any one criterion are included. No hurricane records came through the filter: the file has one tropical storm and no hurricanes.

## Record Structure

```json
{
  "latitude": 35.303,
  "longitude": -97.605,
  "name": "Tornado in OKLAHOMA, CLEVELAND",
  "description": "207 injuries, 24 fatalities; $2.00B property damage",
  "category": "significant_us_storms",
  "date": "2013-05-20",
  "country": "USA",
  "event_type": "Tornado",
  "state": "OKLAHOMA",
  "magnitude": null,
  "injuries": "207",
  "fatalities": "24",
  "damage_property": "2.00B",
  "source": "NOAA Storm Events Database"
}
```

- `injuries` and `fatalities` are stored as text, so convert them to integers before doing math.
- `damage_property` keeps NOAA's shorthand: `K` for thousands, `M` for millions, `B` for billions. It is empty for 368 records.
- `magnitude` is NOAA's raw value (hail size in inches, wind speed in knots) and is empty for 7,648 records. Tornado F and EF ratings are not in the file.

## Event Distribution

| Event Type | Count | Percentage |
|------------|-------|------------|
| Tornado | 6,334 | 42.9% |
| Flash Flood | 2,358 | 16.0% |
| Thunderstorm Wind | 2,257 | 15.3% |
| Flood | 1,777 | 12.0% |
| Hail | 1,246 | 8.4% |
| Lightning | 574 | 3.9% |
| Other | 224 | 1.5% |

## Top States

Texas (1,450), Missouri (648), Arkansas (602), Mississippi (570), Georgia (562)

## Usage

```python
import json
import pandas as pd

with open('noaa_significant_storms.json') as f:
    storms = json.load(f)

df = pd.DataFrame(storms)
print(f"Total events: {len(df):,}")

# Filter by type
tornadoes = df[df['event_type'] == 'Tornado']
fatal = df[df['fatalities'].astype(int) > 0]
```

## Source & License

Public domain (U.S. government work). Data from the NOAA National Centers for Environmental Information (NCEI).

## Distribution

- **Kaggle**: [lucassteuber/noaa-significant-us-storms](https://www.kaggle.com/datasets/lucassteuber/noaa-significant-us-storms)
- **HuggingFace**: [lukeslp/noaa-significant-storms](https://huggingface.co/datasets/lukeslp/noaa-significant-storms)
- **GitHub Gist**: [Demo Notebook](https://gist.github.com/lukeslp/cf4bbf5219bb0db3c360696fbcc25c52)

## Structured Data (JSON-LD)

```json
{
  "@context": "https://schema.org",
  "@type": "Dataset",
  "name": "NOAA Significant US Storms (1950-2025)",
  "description": "14,770 significant weather events curated from NOAA's 1.23 million storm records. Includes F3+ tornadoes, fatal events, and high-damage storms.",
  "url": "https://www.kaggle.com/datasets/lucassteuber/noaa-significant-us-storms",
  "sameAs": "https://huggingface.co/datasets/lukeslp/noaa-significant-storms",
  "license": "https://creativecommons.org/publicdomain/zero/1.0/",
  "creator": {
    "@type": "Person",
    "name": "Luke Steuber",
    "url": "https://lukesteuber.com"
  },
  "keywords": ["weather", "storms", "tornadoes", "natural disasters", "NOAA", "geospatial"],
  "temporalCoverage": "1950/2025",
  "spatialCoverage": {
    "@type": "Place",
    "name": "United States"
  },
  "distribution": [
    {
      "@type": "DataDownload",
      "encodingFormat": "application/json",
      "contentUrl": "https://www.kaggle.com/datasets/lucassteuber/noaa-significant-us-storms"
    }
  ]
}
```
