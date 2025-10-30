## Real-Time German Energy System Balance and Generation Dashboard

## Problem Statement/Abstract
Germany's energy transition (Energiewende) has introduced high levels of variable renewable generation, creating significant volatility for Transmission System Operators. Grid operators require immediate, system wide situational awareness, but monitoring tools are often fragmented. This fragmented approach delays the ability to get a holistic of the grid's state. A simplified, unified dashboard is needed to ingest key data streams and provide visualisation of the national generation mix and the real-time balance between electricity supply and demand. 
The objective is to provide a single source of truth for high level system status, enabling faster, and more informed operational awareness. 
Success will be measured by the continuous display of system-wide load versus generation with a data latency of under 30 minutes and 99% system availability during testing.

## Goals/Requirements
- Provide a single, unified interface displaying Germany's real-time electricity load versus total generation.

- Visualise the live national generation mix (wind, solar, conventional) to clearly show the contribution of variable renewables.

- Calculate and display the real-time system balance to quickly identify potential supply or demand mismatches.

- Establish a lightweight, automated data pipeline from the public ENTSO-E API to a dashboard.

- Create an intuitive dashboard that provides immediate, high level situational awareness with minimal user training.


## Tech stack

### Data Ingestion Layer

- API: ENTSO-E Transparency Platform as the single source for load and generation data.

### Data Processing Layer
- Scripting: Python, using requests for API polling and pandas for data transformation and calculation.

- Scheduling: Cron system scheduler to execute the Python script every 15 minutes.

### Data Storage Layer

- Database: SQLite to append and serve time-series data.

### Visualization and Presentation Layer
- Dashboard Framework: Streamlit.

- Visuals:
    - Line Chart: Real-time "Actual Load" vs "Total Generation".
    - Stacked Area Chart: "Generation by Type" over the last 24 hours.
    - Line Chart: "System Balance Indicator" over the last 24 hours.

## Phase status
- Currently in Conception Phase
- Abstract and system architecture defined
- Initial UML diagrams drafted
- **Next**: Working on python script and cron job.

## Risk Considerations
This project relies on a single external data source, creating a primary point of failure.

### Data API Reliability Risk

**Description**: The entire dashboard is dependent on the continuous availability, timeliness, and accuracy of the ENTSO-E Transparency Platform API. Any API downtime, rate-limiting, or data delays will directly break the dashboard.

**Impact**: The dashboard will fail to update, showing stale or no data. This defeats the project's primary objective of providing "real-time" situational awareness.

**Mitigation**:

- Implement robust error handling, logging, and retry logic in the Python data ingestion script.

- Clearly display a "Last Updated" timestamp on the dashboard so users are immediately aware of data freshness.

- Implement a simple "heartbeat" check that visually flags if the latest data fetch has failed.
