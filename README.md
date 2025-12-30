# Spotify Azure Data Engineering Project

## Overview
This project demonstrates a Data Warehousing solution for Spotify data using Azure Databricks and SQL. It implements a Star Schema to analyze user streaming habits, artist performance, and track popularity. The project handles both initial historical data loading and incremental data updates.

## Architecture & Schema
The project uses a **Star Schema** design optimized for analytical queries:

### Fact Table
- **FactStream**: Stores individual streaming events, including `listen_duration`, `device_type`, and timestamps.

### Dimension Tables
- **DimUser**: User details (subscription type, country, demographics).
- **DimArtist**: Artist information (genre, country).
- **DimTrack**: Track metadata (album, duration, release date).
- **DimDate**: Date dimension for temporal analysis.

## Repository Structure
- **Databricks Code/**: Contains the Databricks Archive (`.dbc`) file with the project notebooks.
- **source_scripts/**:
  - `spotify_initial_load.sql`: DDL statements to create tables and insert initial seed data.
  - `spotify_incremental_load.sql`: SQL scripts to simulate incremental data updates for testing CDC logic.
- **cdc.json**: Configuration file used to track the last load timestamp for Change Data Capture (CDC).

## Getting Started

### Prerequisites
- Azure Subscription
- Azure Databricks Workspace

### Setup Instructions
1. **Import Code**:
   - Upload the `Databricks Code/spotify_dab.dbc` file into your Databricks Workspace. This will unbundle into the project notebooks.

2. **Upload Data/Scripts**:
   - Ensure the `source_scripts` and `cdc.json` are accessible to your Databricks cluster (e.g., via DBFS or mounted storage).

3. **Run Initial Load**:
   - Execute the initialization notebook (derived from the `.dbc` import) to create the schema and populate historical data from `spotify_initial_load.sql`.

4. **Run Incremental Load**:
   - Execute the incremental load logic to process new data from `spotify_incremental_load.sql`. The process uses `cdc.json` to identify and process only new records.

## Features
- **Data Warehousing**: Robust Dimensional Modeling.
- **CDC Mechanism**: Tracks changes to ensure efficient incremental loading.
- **SQL Transformations**: Logic encapsulated in reusable SQL scripts.