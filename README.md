# UMontpellier-ICal-API

## Description

This repository has for goal to provide an API to get the ICal of the courses of the University of Montpellier. For now, it only provides ICals for the Fac des Sciences and Fac de Droit et Science Politique 2023-2024 (open for pull requests to add other faculties).

You can either get JSON data or directly the ICal file. In JSON, you get a "raw" key to access the raw ICal event read by the API. The ICal version served does not contain some data due to the fact that ADE generates new unusefull `UID`, `SEQUENCE`, `LAST-MODIFIED` and `CREATED` each time.

## Usage

Routes are:

- `/search` ➜ Get the courses with the given parameters:
  - `start` ➜ Get the courses starting at this timestamp
  - `end` ➜ Get the courses ending at this timestamp
  - `after` ➜ Get the courses starting at and after this timestamp
  - `before` ➜ Get the courses ending at and before this timestamp
  - `location` ➜ Get the courses at this location
    - `locationMatchType` ➜ The type of match for the location ([`""`(use SQL, LIKE %location%), `strict`, `regex`]; default: `""`)
  - `summary` ➜ Get the courses with this summary
    - `summaryMatchType` ➜ The type of match for the summary ([`""`(use SQL, LIKE %summary%), `strict`, `regex`]; default: `""`)
  - `description` ➜ Get the courses with this description
    - `descriptionMatchType` ➜ The type of match for the description ([`""`(use SQL, LIKE %description%), `strict`, `regex`]; default: `""`)
  - `raw` ➜ Get the raw ICal of the courses ([`""`(include it), `only`(size ~-28.5%), `exclude`(size ~-70%)]; default: `""`)
  - `sort` ➜ Get the courses sorted by start date ([`""` (not sorted), `asc`, `desc`]; default: `""`)
  - `format` ➜ The format of the response ([`json`, `ical`, `ics`]; default: `json`)
- `/id/:id` ➜ Get the course with the given id
  - `format` ➜ The format of the response ([`json`, `ical`, `ics`]; default: `json`)
- `/length` ➜ Get the number of courses (1➜length; are the ids). `{"count": length}`

Examples of usage: \
`/search?location=Amphi%205.02&format=ical` ➜ Get the ICal of the courses in the Amphi 5.02 \
`/search?start=2024-03-15T08:00:00Z` ➜ Get courses starting at 8 a.m the 2024-03-15  \
`/search` ➜ Get the JSON of all the courses \
`/id/1` ➜ Get the JSON of the course with the id in the database

## Hosted version

You can use the latest version at [https://um-ical-api.home.mma.dev/](https://um-ical-api.home.mma.dev/). ⚠️ Uptime is not guaranteed. Generally down between 00:00-08:15 UTC+1.
