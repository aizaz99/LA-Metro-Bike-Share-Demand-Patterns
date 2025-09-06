LA Metro Bike Share Demand Patterns

Goal: Analyze when and where demand spikes, and how it changes by hour, weekday, and season for LA Metro Bike Share.

Dataset: Trip-level CSV with:

Trip ID

Duration

Start Time, End Time

Starting Station ID, Latitude, Longitude

Ending Station ID, Latitude, Longitude

This analysis ran in a Kaggle notebook using your file at /kaggle/input/bike-dataset/metro-bike-share-trip-data.csv.

Key results

Time span analyzed: 267 days 19:28:00

Rows after cleaning: 131,276

Peak hour: 17:00 (11,654 rides)

Peak day: Thursday (20,191 rides)

Median trip distance: 0.96 km

Median trip duration: 55 min

Median speed: 6.8 km/h

Top station (from summary): Station 3069 (5,091 rides)

Notes:

Duration units are auto-detected and cross-checked against timestamps.

Coordinates are limited to a Los Angeles bounding box to drop obvious errors.

Trips faster than 35 km/h are removed as likely anomalies.

Methods

Ingestion and normalization

Case and spacing insensitive column rename to a clean schema.

Parse start_time and end_time.

Validation and cleaning

Detect duration units (seconds vs minutes) by distribution and verify with timestamps.

Geographic filter to LA bounds.

Keep trips between 1 minute and 24 hours.

Filter speeds above 35 km/h.

Feature engineering

Time features: date, year, month, ISO week, hour, day of week, weekend flag.

Trip geometry: haversine distance in km and speed in km/h.

Station catalog: median coordinates per station ID built from trips.

Temporal patterns (when)

Rides by hour of day.

Rides by day of week when the data spans more than one day.

Daily series with 7-day moving average when the span is at least 8 days.

Hour by day heatmap.

Spatial patterns (where)

Top origin stations with median trip length and duration.

Interactive station hotspot map saved as HTML.

Top origin to destination flows with an optional flow map.

Diagnostics

Distributions of distance, duration, and speed.

Speed vs distance scatter to surface anomalies.

Interpretation guide

Commuter patterns usually show morning peaks around 7 to 9 am and evening peaks around 5 to 7 pm on weekdays.

Leisure and visitor usage tends to lift weekend afternoons.

Hotspot stations point to places where rebalancing or more docks could help.

Top flows spotlight corridors that may need targeted rebalancing windows.

Caveats

Station IDs do not include names or regions in this file. You can add them by joining an official Station Table on station_id.

Very long pauses or operational artifacts can appear in raw data. Speed and duration filters reduce their impact.

If the file covers a short period, month-to-month seasonality will be limited.

Next steps

Join the official Station Table to show readable station names and regions in charts and maps.

Break out patterns by passholder type or bike type if those fields are available.

Add a small forecasting section that compares a lag-7 baseline to a simple model with month, day of week, and lagged rides.

Export a one-pager with the top 10 stations, top 10 flows, and the hour by day heatmap for quick sharing.
