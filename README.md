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
  - hurricanes
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
    - name: event_type
      dtype: string
    - name: magnitude
      dtype: string
    - name: injuries
      dtype: int64
    - name: fatalities
      dtype: int64
    - name: damage_property
      dtype: float64
    - name: state
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
- Category 3+ hurricanes
- Fatal events (1+ deaths)
- High-damage storms ($1M+)
- Full coordinates for mapping

## Filtering Criteria

This dataset reduces NOAA's massive storm events database by 98.8% to focus on significant events:

| Criterion | Threshold |
|-----------|-----------|
| Major Tornadoes | F3/EF3 and higher |
| Major Hurricanes | Category 3+ |
| Fatal Events | 1+ direct deaths |
| High Damage | $1,000,000+ property damage |
| High Injuries | 10+ injuries |
| Severe Flash Floods | Fatal (1+ deaths) |
| Severe Winter Storms | Fatal (5+ deaths) |

Events meeting ANY criterion are included.

## Record Structure

```json
{
  "latitude": 35.2271,
  "longitude": -97.4395,
  "name": "Oklahoma City",
  "description": "EF5 tornado, 210 mph winds",
  "category": "noaa_storms",
  "date": "2013-05-20",
  "event_type": "Tornado",
  "magnitude": "EF5",
  "injuries": 212,
  "fatalities": 24,
  "damage_property": 2000000000,
  "state": "OKLAHOMA"
}
```

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
fatal = df[df['fatalities'] > 0]
```

## Source & License

**Public Domain** - U.S. Government Work

Data from NOAA National Centers for Environmental Information (NCEI).

## Distribution

- **Kaggle**: [lucassteuber/noaa-significant-storms](https://www.kaggle.com/datasets/lucassteuber/noaa-significant-storms)
- **HuggingFace**: [lukeslp/noaa-significant-storms](https://huggingface.co/datasets/lukeslp/noaa-significant-storms)
- **GitHub Gist**: [Demo Notebook](https://gist.github.com/lukeslp/cf4bbf5219bb0db3c360696fbcc25c52)

## Author

Luke Steuber | luke@lukesteuber.com | @lukesteuber.com (Bluesky)

## Structured Data (JSON-LD)

```json
{
  "@context": "https://schema.org",
  "@type": "Dataset",
  "name": "NOAA Significant US Storms (1950-2025)",
  "description": "14,770 significant weather events curated from NOAA's 1.23 million storm records. Includes F3+ tornadoes, Category 3+ hurricanes, fatal events, and high-damage storms.",
  "url": "https://www.kaggle.com/datasets/lucassteuber/noaa-significant-storms",
  "sameAs": "https://huggingface.co/datasets/lukeslp/noaa-significant-storms",
  "license": "https://creativecommons.org/publicdomain/zero/1.0/",
  "creator": {
    "@type": "Person",
    "name": "Luke Steuber",
    "url": "https://lukesteuber.com"
  },
  "keywords": ["weather", "storms", "tornadoes", "hurricanes", "natural disasters", "NOAA", "geospatial"],
  "temporalCoverage": "1950/2025",
  "spatialCoverage": {
    "@type": "Place",
    "name": "United States"
  },
  "distribution": [
    {
      "@type": "DataDownload",
      "encodingFormat": "application/json",
      "contentUrl": "https://www.kaggle.com/datasets/lucassteuber/noaa-significant-storms"
    }
  ]
}
```
