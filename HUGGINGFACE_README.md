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
  - meteorology
pretty_name: NOAA Significant US Storms (1950-2025)
size_categories:
  - 1K<n<10K
---

# NOAA Significant US Storms (1950-2025)

14,770 major tornadoes, hurricanes, and fatal weather events (1950-2025)

Curated subset of NOAA Storm Events database - 98.8% reduction from 1.23 million records to focus on significant events: F3/EF3+ tornadoes, Category 3+ hurricanes, fatal events, and storms with $1M+ damage.

## Dataset Structure

[Check the demo notebook for data exploration examples]

## Usage

```python
from datasets import load_dataset

# Load the dataset
dataset = load_dataset("lukeslp/noaa-significant-storms")

# Or load from local files
import json
with open('data.json') as f:
    data = json.load(f)
```

## Citation

```bibtex
@dataset{noaa_significant_storms_2026,
  title = {NOAA Significant US Storms (1950-2025)},
  author = {Steuber, Luke},
  year = {2026},
  url = {https://huggingface.co/datasets/lukeslp/noaa-significant-storms}
}
```


## Distribution

- **GitHub**: [lukeslp/noaa-significant-storms](https://github.com/lukeslp/noaa-significant-storms)
- **Kaggle**: [lucassteuber/noaa-significant-storms](https://www.kaggle.com/datasets/lucassteuber/noaa-significant-storms)

## Author

**Luke Steuber**
- Website: [lukesteuber.com](https://lukesteuber.com)
- Bluesky: [@lukesteuber.com](https://bsky.app/profile/lukesteuber.com)
- Email: luke@lukesteuber.com

## License

CC0-1.0
