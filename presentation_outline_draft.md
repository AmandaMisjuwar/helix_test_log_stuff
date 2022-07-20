# Test Log Search Presentation Outline

## What is the problem?
- Developers could use some more insight into test failures to make error investigation easier. 
- For example (quote from a .NET engineer email): 

> "I’m interested in both build and test failures but, almost always, I’m looking for a specific failure message in a job’s console log, the test results, or in Helix logs."

> Wants to move from "that’s an odd failure” to "that’s an odd failure, it’s happened 50 times in the past two days, and it’s affecting dotnet/windows desktop too"

Basically, we want to know more about how often a specific error message is occurring in a project's test over a range of time.

## How project is addressing the problem

In my project, I added an endpoint to Helix Services so that one can make a query as follows:

- Given a repository, a string, start date, and end date, search through a specified repository's failed test logs created within the date range for the given string.
- We return a list of string matches in the test logs and include information such as 
  - Number of total occurrences of the given string
  - Number of logs/tests that contained the string
  - The full line in the log in which the string was found
  - The line number within the log that the string was found
  - Number of occurrences per file 
  - The associated job ID, job friendly name, when the test work item started and finished, the test log's console URI, the queue name, and the attempt number of the test

With this functionality, one is able to investigate a specific error and see how often it occurs in a project's tests along with relevant information that may be useful in their investigation.

## High level architecture overview (refer to design doc)
(Briefly talk about how this works based on the design document diagram - i.e Execute a Kusto query to get the tests for a specific repo, grab their log file content and scan each line by line for the target string, return the matches)

## Some data for running times 
We want this tool to run within a reasonable time, here are some runs on production data and how long it took:

- Include a table like the one included in the POC Insights document
  
## How the project should be used

Show a demo of the endpoint
  1. Go through passing the correct query arguments 
     - URL encoded repository name and search string (since I'm testing using my browser)
     - Date range format (currently limited to past 14 days to avoid too much data being queried)
     - Response types (Hits and HitsPerFile)
     - Optional parameters: Timeout maximum (default is 2 min)
  2. Go through outputs
     1. Hits: Show how it returns a list of every single occurrence. For each occurrence, we include whole line content as well as line number. 
     2. HitsPerFile: Show how it returns the number of occurrences per log file.
     3. Both include The associated job ID, job friendly name, when the test work item started and finished, the test log's console URI, the queue name, and the attempt number of the test, total occurrences, and total logs with occurrences.
   
## Future considerations
- Running the service on the same data centres that the logs are stored (it would probably be much faster)
- Including other information that would possibly be useful to the customer in the output
