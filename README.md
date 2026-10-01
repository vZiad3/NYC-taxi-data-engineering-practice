# NYC Taxi — PySpark practice

A hands-on project using a 10M-row NYC Taxi CSV. I used PySpark to explore the data, check quality issues, create a Silver layer, and build summaries with Spark SQL.

## Flow

Raw CSV → Profiling / Data Quality → Silver Parquet → SQL Analytics → Gold → Zone Join

The notebook checks nulls, exact duplicates, passenger counts, distances, trip durations, average speeds, and fares. Silver removes duplicate copies and keeps records with non-negative duration. Zero passengers, zero distance, zero duration, and financial mismatches get flags.

Gold contains monthly, payment, and pickup-location summaries. A left join adds zone and borough names to the pickup summary.

## Run

1. Install PySpark and Jupyter in a Python environment with a compatible Java runtime.
2. Put `taxi_trip_data.csv` and `taxi_zone_geo.csv` in `data/` (see its README).
3. Open `notebooks/nyc_taxi_pipeline.ipynb` and run the cells in order from the project folder or `notebooks/`.

Outputs are written to `output/silver/` and `output/gold/`. Re-running the write cells replaces those generated folders. Raw data and outputs are excluded from Git.

## Known issues

The previous run found **162 Silver records with pickup dates outside 2018**. They are retained, so the monthly summary may include months outside 2018. Negative fares and other suspicious values are also retained; these summaries should be read with those limitations in mind.

Historical counts: 10,000,000 raw rows, 607,571 duplicate copies, and 9,392,290 Silver rows. These counts were recorded during the earlier project work and have not been verified by a new execution of this cleaned notebook.

The attached notebook stopped at Data Quality. Later pipeline sections were restored from the project conversation. See [review notes](REVIEW_NOTES.md) for details.
