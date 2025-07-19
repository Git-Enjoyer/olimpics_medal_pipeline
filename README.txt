
Pre Project breif: 

The goal is to build a dashboard to display the live statistics of our olympic medal blind sweepstakes in the luchroom at work.

People bet up to £3, £1 = 2 random countries. Most people end up whith have 6 random countries, while some have 2 or 4 (usa & china where excluded from the draw for fairness).

Points will be allocated per medal, the some of a persons top performing country is the score they are ranked by (as decided by office politics).
  'gold' = 3 points 
  'silver'= 2 points 
  'bronze'= 1 points 

The buy in will be given out as the prize. 
The person with the 1st country gets 50% of the price pool, while the person with the 103rd country gets 25%.
The remaining 25% will go to the winner of a hat draw, all countries with 0 go in a hat and a winner is drawn at random (the UK loves a lst place prize).

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


# Olympic Medal Dashboard

End-to-end pipeline to scrape, store, and visualise live Olympic medal data using Python, PostgreSQL, and Grafana. Built for reliability, automation, and real-time visibility.

---

## Overview

This project ingests medal data from a dynamic public website, parses and cleans it, stores it in a structured PostgreSQL schema, and exposes it through a Grafana dashboard. It runs on a scheduled basis via cron on an Ubuntu host.

Designed to demonstrate applied data engineering skills across ingestion, transformation, storage, automation, and reporting.

---

## Stack

- **Scraping**: Python, `BeautifulSoup`, `Selenium`
- **Data Storage**: PostgreSQL 14
- **Visualisation**: Grafana (Docker-hosted or local)
- **Automation**: Cron (Ubuntu), Bash
- **Infra**: Ubuntu 22.04 VPS

---

## Pipeline

1. **Scraper** (`/scraper`)
   - Loads medal data from a structured table on the Olympics site.
   - Supports fallback logic for dynamic elements via Selenium.
   - Normalises country names and medal fields.

2. **Loader** (`/database/insert.py`)
   - Inserts records into `medals` table with upsert handling.
   - Includes timestamping and basic logging.

3. **Scheduler** (`cron_job.sh`)
   - Runs the scraper and loader every 4 hours via cron.
   - Output logs piped to local files for review.

4. **Dashboard**
   - Connected directly to the DB.
   - Visualises live medal counts by country.
   - Auto-refresh every 5 minutes.

---

## Schema

```sql
CREATE TABLE medals (
    id SERIAL PRIMARY KEY,
    country TEXT NOT NULL,
    gold INTEGER DEFAULT 0,
    silver INTEGER DEFAULT 0,
    bronze INTEGER DEFAULT 0,
    total INTEGER GENERATED ALWAYS AS (gold + silver + bronze) STORED,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
Pre Project breif: 

The goal is to build a dashboard to display the live statistics of our olympic medal blind sweepstakes in the luchroom at work.

People bet up to £3, £1 = 2 random countries. Most people end up whith have 6 random countries, while some have 2 or 4 (usa & china where excluded from the draw for fairness).

Points will be allocated per medal, the some of a persons top performing country is the score they are ranked by (as decided by office politics).
  'gold' = 3 points 
  'silver'= 2 points 
  'bronze'= 1 points 

The buy in will be given out as the prize. 
The person with the 1st country gets 50% of the price pool, while the person with the 103rd country gets 25%.
The remaining 25% will go to the winner of a hat draw, all countries with 0 go in a hat and a winner is drawn at random (the UK loves a lst place prize).

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


# Olympic Medal Dashboard

End-to-end pipeline to scrape, store, and visualise live Olympic medal data using Python, PostgreSQL, and Grafana. Built for reliability, automation, and real-time visibility.

---

## Overview

This project ingests medal data from a dynamic public website, parses and cleans it, stores it in a structured PostgreSQL schema, and exposes it through a Grafana dashboard. It runs on a scheduled basis via cron on an Ubuntu host.

Designed to demonstrate applied data engineering skills across ingestion, transformation, storage, automation, and reporting.

---

## Stack

- **Scraping**: Python, `BeautifulSoup`, `Selenium`
- **Data Storage**: PostgreSQL 14
- **Visualisation**: Grafana (Docker-hosted or local)
- **Automation**: Cron (Ubuntu), Bash
- **Infra**: Ubuntu 22.04 VPS

---

## Pipeline

1. **Scraper** (`/scraper`)
   - Loads medal data from a structured table on the Olympics site.
   - Supports fallback logic for dynamic elements via Selenium.
   - Normalises country names and medal fields.

2. **Loader** (`/database/insert.py`)
   - Inserts records into `medals` table with upsert handling.
   - Includes timestamping and basic logging.

3. **Scheduler** (`cron_job.sh`)
   - Runs the scraper and loader every 4 hours via cron.
   - Output logs piped to local files for review.

4. **Dashboard**
   - Connected directly to the DB.
   - Visualises live medal counts by country.
   - Auto-refresh every 5 minutes.

---

## Schema

```sql
CREATE TABLE medals (
    id SERIAL PRIMARY KEY,
    country TEXT NOT NULL,
    gold INTEGER DEFAULT 0,
    silver INTEGER DEFAULT 0,
    bronze INTEGER DEFAULT 0,
    total INTEGER GENERATED ALWAYS AS (gold + silver + bronze) STORED,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
