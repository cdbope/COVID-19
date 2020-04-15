# Data insights for COVID-19 response: resources for producing mobility indicators and analysis from CDR data

## Overview

This repository provides mobile network operators with code and guidelines to produce aggregates from their raw CDR data (Call Detail Records) in the context of the COVID-19 pandemic. A description of each aggregate is provided alongside the code, together with suggestions for how it can be used. For more information about the aggregates, and for additional resources on how to utilise them to produce mobility indicators, please visit [covid19.flowminder.org](https://covid19.flowminder.org).

We have initially focused on producing code and guidelines for mobile network operators that may have limited technical capacity,
especially those in low- and middle-income countries. This means that the code we have provided is both simple to modify,
and also should not be extremely computationally intensive to run. However, we will continually add more resources to the repository,
including material that is suitable for settings where more capacity is available, and where higher phone usage results in higher frequency
data. In these cases, it will be possible to produce more complex outputs and analyses.

## Technical usage

The code will need to be adapted to each MNO's system.
The names of tables and columns will need to be changed, and the code may need to be optimised to suit the structure of the data.

The code has been written assuming that the following tables exist:

`calls` is the call events table, including the columns:

-   `msisdn`: SIM identifier,
-   `call_date`: event date,
-   `call_datetime`: event timestamp,
-   `location_id`: identifier of the cell tower.

`cells` is a table with information about cell towers, including the columns:

-   `cell_id`: identifier of the cell tower,
-   `locality`: the geographic area that the cell tower is in (for example, administrative region). We are able to provide assistance with mapping cell tower locations to administrative (or other) localities, if you do not already have this mapping.

[core_tables.sql](core_tables.sql) contains definitions of the expected `calls` and `cells` tables.

## Content

This repository currently contains SQL code and descriptions for the following aggregates:

-   [Count of unique subscribers, per locality per time interval](count_subscribers.md)
-   [Aggregate 5: ‘Connectivity’ between pairs of regions - count of unique subscribers seen at each pair of locations, each day](aggregate_5.md)
-   [Aggregate 6: Directional connections between pairs of regions - count of unique subscribers moving between each pair of locations, each day](aggregate_6.md)
-   [Aggregate 7: Total number of calls per region per day](aggregate_7.md)
-   [Aggregate 8: Home location counts per region](aggregate_8.md)
-   [Count of subscribers that are seen only in one region per region per day](count_subscribers_single_region.md)
-   [Trips between consecutive locations per day](od_matrix_directed_consecutive_pairs.md)
-   [Static resident counts per region per day](count_subscribers_home_region_per_day.md)
-   [Count of ‘home’ and ‘away’ visits (‘home-away matrix’), per day](count_visits_home_away_per_day.md)
-   [Count of home relocations per week](count_home_relocations_per_week.md)

## Privacy

All aggregates included in this repository produce aggregated outputs (i.e. one result per locality, not one result per subscriber), to protect subscribers' privacy and personal data. Additionally, to ensure that no locational information about individual subscribers is revealed, only aggregates containing more than 15 subscribers are produced as outputs. The limit of 15 is in line with the standard that is used by many statistics offices.

Note that the queries in [intermediate_queries.sql](intermediate_queries.sql) produce per-subscriber data. These intermediate results should not be shared outside of the MNO's system, and are intended for use only as components of the aggregate queries.

## Feedback

We welcome all suggestions and feedback. Please open an issue, submit a pull request, or contact the team at covid19@flowminder.org.
