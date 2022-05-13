# Introduction
## Project goals
We want to create a REST API that allows users to find the frequency of a specific error string in Helix build logs. So we want to be able to query an endpoint with a `repository`, `error_string`, and `date_range` to (?) get a list of all the error occurrences of the string in the build logs created within `date_range`. 

## High-level diagram

# Requirements
# User stories
User story | 
------ | 
As a user, I want to know how often a specific error appears in my application’s builds, so that I can investigate the underlying cause. || 
As a user, I want to know which builds are causing a repetitive error, so I can investigate the underlying cause. ||
As a user, I want to see repeatedly occurring errors over a certain date range, so that I have more details when I need to investigate a certain issue.|


# Technical Implementation
## Input
- Arguments
    - `repository`
    - `error_string`
    - `date_range`
- Other possible input needs to be further clarified + thought of

## Dependencies
- Kusto
- Azure Account Storage

## String Matching
- Will need to look into different methods
    - `contains`
    - regex
    - wildcard
    - etc.
 
## Logic
- Grab `WorkItem`s from Kusto and make a query in the code (See `KnownIssuesController` in helix services code for an example of interacting with Kusto)
- Parse the Kusto query result for the different column values.
- Grab the Azure storage path from the Kusto query result, and somehow go into that path in the code and use the logs text to do the string matching

## Output
- Number of occurrences of `error_string` in the log files within given `date_range`
- Builds and dates associated with each `error_string` occurrence
- PRs associate with that build

#### Possible JSON output:
    {[
        {
            "repository": "",
            "error_string": "",
            "date_range": "",
            "num_occurrences": 00,
            "build_ids": [],
        },
        {
            "repository": "",
            "error_string": "",
            "date_range": "",
            "num_occurrences": 00,
            "build_ids": [],
        },
        {
            "repository": "",
            "error_string": "",
            "date_range": "",
            "num_occurrences": 00,
            "build_ids": [],
        },
    ]}
 
## Proof-of-Concept
- Console app
