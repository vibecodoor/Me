# Wearable Data

## Device

| Field | Value |
|---|---|
| Device | — |
| App | — |

## How to Import

1. Export data from your wearable app (JSON/CSV)
2. Drop the file into chat → AI parses and updates tables below

## Daily Data

| Date | Steps | Distance (m) | Calories | Active (min) | Avg HR | Min HR | Max HR | SpO2 | Notes |
|---|---|---|---|---|---|---|---|---|---|
| | | | | | | | | | |

## Sleep Data (from wearable)

| Date | Total (h) | Deep (min) | Light (min) | REM (min) | Awake (min) | Score |
|---|---|---|---|---|---|---|
| | | | | | | |

## Import Log

| Date | Source | Records | Status |
|---|---|---|---|
| | | | |

---

## AI Import Instructions

When user drops a wearable export file:

1. Aggregate raw data **per day**
2. HR: calculate avg, min, max per day
3. Sleep: sum phase durations per night
4. Steps: daily total
5. Append new rows, skip duplicates
6. Log import in "Import Log" table
7. Update [sleep.md](sleep.md) with wearable sleep data if user confirms
