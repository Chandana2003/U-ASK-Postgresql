# U-ASK-Postgresql
---
### U-ASK: Spatial-Textual Query Engine – Setup Guide

**Project Overview**
U-ASK is a spatial-textual query processing system designed to retrieve geospatial data using advanced algorithms like POWER and Boolean Range. It integrates **PostgreSQL** with **PostGIS** and **OpenSearch** to support scalable, efficient querying of location-based textual data. This guide outlines the steps to set up the environment, process data, build indexes, and run various query algorithms.

---

### System Requirements

Before starting, make sure your system meets the following prerequisites:

* **OS:** Windows, Linux, or macOS
* **Python:** Version 3.11
* **PostgreSQL:** 13+ with PostGIS enabled
* **OpenSearch:** 2.x or higher
* **Tools:** `pip`, and a Python IDE (VS Code recommended)

---

### Step 1: Install Dependencies

Use pip to install the required libraries:

```bash
pip install psycopg2-binary
pip install geopy
pip install scikit-learn
pip install numpy
pip install concurrent.futures
pip install streamlit
pip install opensearch-py
pip install pandas
```

Enable PostGIS in PostgreSQL:

```sql
CREATE EXTENSION postgis;
```

---

### Step 2: PostgreSQL Setup

Initialize the database and schema:

```sql
CREATE DATABASE tweet_data;
\c tweet_data;
CREATE TABLE tweets (
  tweet_id BIGINT PRIMARY KEY,
  latitude DOUBLE PRECISION,
  longitude DOUBLE PRECISION,
  keywords TEXT[],
  keyword_weights FLOAT[]
);
CREATE EXTENSION IF NOT EXISTS postgis;
```

---

### Step 3: Data Processing & Indexing

1. **Preprocess Raw Tweets**
   Clean and format tweets for ingestion:

   ```bash
   python process_tweets.py
   ```

2. **Further Cleaning**
   Remove unnecessary characters and noise:

   ```bash
   python clean.py
   ```

3. **Index Tweets into OpenSearch**

   ```bash
   python teq_indexing.py
   ```

4. **Load Cleaned Tweets into PostgreSQL**

   ```bash
   python load_indexed_data.py
   ```

---

### Step 4: Run Query Algorithms

* **POWER Algorithm (Top-k Spatial-Textual Search):**

  ```bash
  python power_algorithm.py
  ```

* **Boolean Range Query with Negative Keyword Filtering:**

  ```bash
  python power_boolean_range.py
  ```

* **RCA Algorithm Execution:**

  ```bash
  python rca_algorithm.py
  ```

---

