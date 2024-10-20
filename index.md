---
layout: default
title: Welcome to Address Verify and Update Documentation
---

# Welcome to Address Verify and Update Documentation

## Navigation

{% for item in site.nav %}
- [{{ item.name }}]({{ site.baseurl }}{{ item.link }})
{% endfor %}

## Introduction

This application is written to be helpful in compiling user addresses for submission to a company for verification, then using their results to update your database in the following ways:

- when an address for a person has changed their address and reported it to the US Postal Service
- when an address is found to be undeliverable by the US Postal Service
- when a person is found to be deceased in official public records

There are discrete steps in this program where our own verification is performed before any updates are made to the database, see [Detailed Description](#detailed-description)

## Background

Address verification is generally performed by a company that had developed a system in cooperation with the US Postal Service and gained access to their database of verified addresses, address change forms, and other types of data, such as deceased records.

Our addresses can be compiled into and submitted to one of these companies, then returned with address verification codes.  When possible, new addresses are included that have been obtained from a persons address change form or mail forwarding form from that they submitted to the US Postal Service.  Other data is also available, such as information on a persons deceased status, obtained by official means through public records.

## Detailed Description

Data files will be created along the way for review and submission.

Data file and log locations will be set through configuration parameters.

### Working Sessions

Each completed step starts a distinct session with all related files contained in a directory labeled with the start date of that session - each session will maintain state data that includes steps run, counts obtained for each step, next step

When The application starts, it will display the state of the last session that is incomplete in the configured DATA_DIRECTORY

### Application steps

This application is set to perform the following steps:
0. Preliminary Estimation: Get a count of records for estimation purposes [more detail on this step](#0-preliminary-estimation)
1. Create an initial records file and display the number of records in that file [more detail on this step](#1-creating-the-initial-upload-file)
2. Results summary can be generated after you receive your results [more detail on this step](#2-generating-the-results-summary)
3. Generate queries for updating the database [more detail on this step](#3-generating-the-queries)
4. Verify the generated queries [more detail on this step](#4-verifying-the-queries)
5. Run the verified queries to update the database [more detail on this step](#5-running-the-queries)
6. Retry any failed queries due to record locks [more detail on this step](#6-retrying-failed-queries)
7. Review the results of the query execution [more detail on this step](#7-reviewing-query-results)
8. Review results from other working sessions [more detail on this step](#8-reviewing-results-of-other-working-sessions)

### 0. Preliminary Estimation

This step can be run with 'avu estimate` (see terminal setup)

Configuration variables

- DATABASE_CONNECTION_STRING
- ESTIMATION_QUERY

This preliminary step allows users to quickly get an estimate of the number of records that will need verification without starting a full session or gathering actual data.

DATABASE_CONNECTION_STRING - The application will use this to connect to the database

ESTIMATION_QUERY - The application will use this query to get a count of records that would be selected for verification

The application will:

Connect to the database using the DATABASE_CONNECTION_STRING
Run the ESTIMATION_QUERY to get a count of records
Display the count to the user
Allow the user to decide whether to proceed with the full verification process

This step does not create any files or start a working session.

### 1. Creating the initial upload file

Configuration variables
- DATA_DIRECTORY
- INITIAL_UPLOAD_FILE_LOCATION
- DATABASE_CONNECTION_STRING
- SELECTION_QUERY

DATA_DIRECTORY - the location for The application to store data pertaining to each [working session](#working-sessions)

INITIAL_UPLOAD_FILE_LOCATION - The application will compile addresses that need to be verified and save them to a file at this location

DATABASE_CONNECTION_STRING - The application will use this to connect to the database

SELECTION_QUERY - The application will use this query to collect the data from the database

### 2. Generating the results summary

Configuration variables
- RESULTS_FILE_LOCATION
- RESULT_TYPES
- [[RESULT_TYPE]]_DEFINITION

RESULTS_FILE_LOCATION - The application will scan the results file and display the number of records for each type of result

RESULT_TYPES - The application will compile results for each result type listed

Suggested result types
- ADDRESS_IS_DELIVERABLE - Address is deliverable 
- ADDRESS_IS_CHANGED - Address is changed for user 
- ADDRESS_IS_UNDELIVERABLE - Address is found undeliverable 
- USER_IS_DECEASED - User is found to be deceased

[[RESULT_TYPE]]_DEFINITION - The application will find records of this RESULT_TYPE with these rules

### 3. Generating the queries

In this step, queries are only generated, not used to update the database yet

Configuration variables
- [[RESULT_TYPE]]_UPDATE_QUERIES
- PRIMARY_DATA_KEY

[[RESULT_TYPE]]_UPDATE_QUERY - The application will generate these update queries for the indicated result type

PRIMARY_DATA_KEY - The application will verify that each update query filters by this key in the where clause

During a working session, queries can be generated individually for each result type or queued for all result types.

Queries will be generated to 
- update the records
- add history records for each update

### 4. Verifying the queries

Query Verification can be queued for an individual result type or all

You can choose to halt on the first error or compile all results and list errors at the end

Counts will be displayed as verification progresses

You can watch the log as it is created with the following command

```powershell
Get-Content -Path "$env:DATA_DIRECTORY\query_verification_[[RESULT_TYPE]]_logfile.log" -Wait
```

```bash
tail -f "$DATA_DIRECTORY\query_verification_[[RESULT_TYPE]]_logfile.log"
```

Verification status can be

Ready, Queued, Halted, or Complete

Counts will be displayed to track progress

### 5. Running the queries

Update Queries can be queued to run for individual result types, or all

Counts will be displayed as verification progresses

You can watch the log as it is created with the following command

```powershell
Get-Content -Path "$env:DATA_DIRECTORY\query_run_for_[[RESULT_TYPE]]_logfile.log" -Wait
```

```bash
tail -f "$DATA_DIRECTORY\query_run_for_[[RESULT_TYPE]]_logfile.log"
```

Query run status can be

Ready, Queued, Halted, or Complete

Counts will be displayed to track progress

### 6. Retrying failed queries

Queries that fail for record lock will be retried once at the end of the process

After all queries have been run, the status will change to completed and counts will be displayed for each RESULT_TYPE processed

The opportunity will then be presented to check queries that failed, and re-run those that failed for record lock

Queries that failed for reasons other than record lock will need to be re-run by other means

### 7. Reviewing query results

Query results will be displayed and saved to the [working session](#working-sessions)

### 8. Reviewing results of other working sessions

A menu item is available for listing other working sessions that are stored on the system, 

## Quick Start

- [Installation Guide]({{ site.baseurl }}{{ site.nav | where: "name", "Installation" | map: "link" | first }})
- [User Guide]({{ site.baseurl }}{{ site.nav | where: "name", "User Guide" | map: "link" | first }})
- [Development Guide]({{ site.baseurl }}{{ site.nav | where: "name", "Development Guide" | map: "link" | first }})


