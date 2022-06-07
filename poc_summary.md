# Helix Test Log Search POC Summary


## How it works



### Input
Run the console app in terminal and pass all of the following options:

- `errorString`: The error string the program will search for
- `repository`: The public repository whose test logs will be parsed
- `startDate`: The start date of the date range in which the test logs will be searched. This argument must be in the format **yyyy/MM/dd**.
- `endDate`: The end date of the date range in which the test logs will be searched. This argument must be in the format **yyyy/MM/dd**.
- `option`: Either 0 or 1. 0 corresponds to Hits - it will return an array of all occurences of `errorString`, including each occurrence's line number within it's test log file. 1 corresponds to HitsPerFile - it will return an array of hits per file, including the count of occurrences per file.

#### Example

    dotnet run -errorString=Exception --repository=microsoft-ui-xaml-lift --startDate=2022-05-30 --endDate=2022-06-02 --option=1
    
This command will search for all instances of the string "Exception" in all the `microsoft-ui-xaml-lift` Helix test logs created between May 30, 2022 and June 2, 2022. It will return the number of hits found per file. 

### Output

#### Hits per File
        {
          "filter": {
            "repository": "microsoft-ui-xaml-lift",
            "errorString": "Exception",
            "startDate": "2022-05-30T00:00:00",
            "endDate": "2022-06-02T00:00:00"
          },
          "hits": [
            {
              "occurrencesPerFile": 12,
              "jobId": 19881047,
              "friendlyName": "Foundation-Graphics-XamlDCompInteropTests",
              "status": "Fail",
              "started": "2022-05-30T08:12:21.956Z",
              "finished": "2022-05-30T08:15:36.1Z",
              "consoleUri": "https://helixri8s23ayyeko0k025g8.blob.core.windows.net/microsoft-ui-xaml-lift-refs-pull-7417450-merg463ff079316b4a2b8f/Foundation-Graphics-XamlDCompInteropTests/1/console.8a876ba6.log?sv=2019-07-07&se=2022-08-28T07%3A49%3A12Z&sr=c&sp=rl&sig=oS6qGvbSiiy4M0uE7WE355K3mxIyjmBPEDh2%2B4r6EiE%3D",
              "queueName": "windows.10.amd64.client20h2.xaml",
              "attempt": 1
            },
            {
              "occurrencesPerFile": 12,
              "jobId": 19887428,
              "friendlyName": "Foundation-Graphics-XamlWinRTCompInteropUnrestrictedTests",
              "status": "Fail",
              "started": "2022-05-31T15:21:22.254Z",
              "finished": "2022-05-31T15:24:39.16Z",
              "consoleUri": "https://helixri8s23ayyeko0k025g8.blob.core.windows.net/microsoft-ui-xaml-lift-refs-heads-master-9b1cf82d119a42b399/Foundation-Graphics-XamlWinRTCompInteropUnrestrictedTests/1/console.a60d038e.log?sv=2019-07-07&se=2022-08-29T15%3A06%3A34Z&sr=c&sp=rl&sig=bL0TWg1jDGyir1l8FCrdGTVTKsONYcHMyqRxKKmMUFM%3D",
              "queueName": "windows.10.amd64.client20h2.xaml",
              "attempt": 1
            },
            ...
          ],
          "occurrenceCount": 2009,
          "filesCount": 14
        }
        OCCURRENCES COUNT: 2009
        FILE COUNT: 14
        TIME ELAPSED: 00:00:31.6441235
        LINES SCANNED/SEC: 2697.309660038459
        FILES SCANNED/SEC: 0.44242021745364507
        TOTAL FILES SCANNED: 14



#### Hits 


## Findings

### Tests
