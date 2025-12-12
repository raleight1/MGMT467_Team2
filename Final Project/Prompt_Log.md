```python
# ======================================================================
# MGMT 467 – Prompt Log (Code‑Comment Version)
# Contributors: twich13, caicaitlyn18
# Purpose: Capture all user prompts + evolution + failure points + validation
# ======================================================================


# ======================================================================
# 1. USER PROMPTS (CHRONOLOGICAL – USER MESSAGES ONLY)
# ======================================================================

# --- BigQuery & Data Loading Prompts ---
# give me a way to load this data into google colab mounting my google account then finish step 1 within colab
# NotFound: 404 Not found: URI gs://mgmt467-gym-raw/batch/gym_members_dataset.csv
# can I skip the drive aspect... the data is already within the table
# reset all instructions knowing that the data is in the GCP under the table GymData withing GymDB within the project mgmt467-project
# the data was already partitioned why is this necessary
# BadRequest: 400 Unrecognized name: Last_Visit_Date
# Schema of GymData_Raw: string_field_0 … string_field_14
# BadRequest: PARTITION BY expression must be DATE(...)
# the data is now loaded in properly please Provide one data quality check and one transformation logic explanation
# please also make these usable in colab python with a print statement so I can see results


# --- Streaming via Twitter / Reddit / Weather ---
# Streaming ingest (Twitter sentiment pipeline)
# For the API use please use a twitter account for a gym and use sentiment analysis…
# Empty DataFrame — why is the table empty?
# too much stuff in step 2 are not printable on colab
# maybe just switch the whole pub/sub system to weather…
# its still empty
# how can I run all this in colab
# TypeError: Object of type datetime is not JSON serializable


# --- BigQuery Errors & Fix Attempts ---
# Request couldn't be served
# Table is truncated
# AttributeError: 'str' object has no attribute 'query'
# I just dont understand why the streaming data cant populate a df
# please reset, I need a table that has the average weather per month…
# this after step 2: AttributeError: 'str' object has no attribute 'query'
# what to do after this DROP TABLE statement?
# why does my result look like this? (1 row only)
# can you pull data from the past 365 days…
# NotFound: Weather_Raw_Streaming not found
# now I run into this error… table not found
# Provided Schema does not match Table
# Can you give me an entirely new cleaned up python file
# Dont do every step just make it so that whats there has been cleaned up and can successfully run


# --- Curated Table Issues ---
# BadRequest: Unrecognized name: Last_Visit_Date
# table_id insert error — table not found
# "no such field: avg_temperature_c"
# give me what to do with that cell to fix it


# --- Historical Weather + Monthly Averages ---
# It's only pulling in 5 data points, I want it to look at the historical weather
# cell 3 failed with the same error
# and this is streaming live data in?
# 3


# --- Final Clarifications / Deliverables ---
# how to stream this to gcp now that its done
# can you consolidate all these prompts… as a markdown file
# B (user selection)
# can you make sure this is included: prompts evolved, where they failed, and how you validated
# regenerate full file
# no make it as a code/comments


# ======================================================================
# 2. PROMPT EVOLUTION • FAILURE POINTS • VALIDATION
# ======================================================================

# ----------------------------------------------------------------------
# SECTION 1 — DATA LOADING EVOLUTION
# ----------------------------------------------------------------------
# Evolution:
#   - Started with Drive-mounted CSV importing
#   - Moved to loading directly from BigQuery
#   - Rebuilt Raw + Curated tables due to schema mismatches

# Failure Points:
#   - GCS URI not found
#   - Autodetect schema mismatch
#   - Missing field Last_Visit_Date
#   - Raw table columns were strings → partitioning failed

# Validation:
#   - Queried schema directly
#   - Recreated tables using CREATE OR REPLACE
#   - Verified curated outputs via sample SELECT + DataFrames


# ----------------------------------------------------------------------
# SECTION 2 — TWITTER → REDDIT → WEATHER STREAMING EVOLUTION
# ----------------------------------------------------------------------
# Evolution:
#   - Twitter (failed) → Reddit (failed) → Weather API (stable)

# Failure Points:
#   - Twitter public API returns no data
#   - Reddit requires OAuth tokens
#   - Streaming tables stayed empty
#   - JSON payloads missing fields

# Validation:
#   - Printed API results directly
#   - Confirmed response JSON structure
#   - Inserted sample rows into BigQuery
#   - Verified table contents


# ----------------------------------------------------------------------
# SECTION 3 — HISTORICAL WEATHER (365 DAYS) + LIVE STREAMING
# ----------------------------------------------------------------------
# Evolution:
#   - 5-row live stream → 365-day batch history → monthly average generation

# Failure Points:
#   - DataFrame mismatch (aggregates inserted into raw table)
#   - Schema mismatch: avg_temperature_c not in raw schema
#   - Table deleted before insert → table not found
#   - Wrong table reference (table_ref vs project.dataset.table string)

# Validation:
#   - Recreated tables explicitly
#   - Loaded df_hist before streaming
#   - Verified ingestion via SELECT *
#   - Reran monthly aggregation successfully


# ----------------------------------------------------------------------
# SECTION 4 — MONTHLY AVERAGE TABLE
# ----------------------------------------------------------------------
# Evolution:
#   - Needed final monthly temperature/wind/humidity averages

# Failure Points:
#   - Aggregation executed with zero raw rows
#   - Wrong project ID format
#   - Schema mismatches

# Validation:
#   - Ensured raw streaming table populated first
#   - Recomputed monthly averages only after data existed
#   - Printed final DataFrame to validate


# ----------------------------------------------------------------------
# SECTION 5 — FINAL DELIVERABLES
# ----------------------------------------------------------------------
# Evolution:
#   - Needed cleaned Python file
#   - Needed GitHub markdown
#   - Needed prompt log with evolution summary
#   - Needed code-comment formatting

# Validation:
#   - Full prompt log reconstructed
#   - All errors tracked and documented
#   - Section rewritten as code-style documentation


# ======================================================================
# END OF FILE
# ======================================================================
```
