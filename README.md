# Medical Waste Collection Analytics

A Python data-analysis project adapted from the structure of the linked traffic
analytics project. It tracks waste weight and emptying events for six bins, and
analyzes when collections happen and how often each bin is emptied each day.

## Important

The included `data/medical_waste_sample.csv` is **synthetic demo data**. It is
not hospital data and must not be presented as real operational measurements.
The six labels (`Bin 1` through `Bin 6`) are generic placeholders, not
biomedical-waste classifications or regulatory guidance. Replace them with
your institution's approved labels and use records collected by your project.

## Data format

Each row represents one bin-emptying event. If a bin is emptied three times in
a day, it should have three rows for that date and bin.

| Column | Meaning |
| --- | --- |
| `event_id` | Unique collection event identifier |
| `bin_id` | Stable bin identifier |
| `bin_label` | Editable name for the bin or waste stream |
| `collection_timestamp` | Local date and time the bin was emptied |
| `waste_weight_kg` | Weight collected during that emptying, in kilograms |

The daily emptying frequency is calculated by counting event rows per date and
bin. Collection date and hour are derived from `collection_timestamp`.

## Run

Requires Python 3.9 or newer.

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python data_cleaning.py
python data_analysis.py
python data_visualization.py
```

By default, the scripts use `data/medical_waste_sample.csv`. Replace that file
with your own CSV using the same columns before running the scripts. The
cleaning script validates records and writes
`data/medical_waste_cleaned.csv`; invalid records cause a clear error rather
than being silently discarded.

## Outputs

`data_analysis.py` writes:

- `outputs/waste_by_bin.csv` — total weight and event count by bin
- `outputs/daily_clearing_counts.csv` — number of emptying events per bin/day
- `outputs/daily_waste_totals.csv` — daily collected weight
- `outputs/collections_by_hour.csv` — event count and weight by collection hour

`data_visualization.py` creates corresponding charts in `visualizations/`.
The output CSVs can also be imported into Power BI to build an interactive
dashboard with bin, date, and collection-time filters.

## Project files

- `generate_sample_data.py` regenerates the deterministic synthetic example
- `data_cleaning.py` validates and cleans the input CSV
- `data_analysis.py` calculates collection and emptying summaries
- `data_visualization.py` creates charts from the cleaned data
# medwaste
