# Helix Test Log Search POC Summary
To recall, this POC queries Kusto for failed test logs for a specified repository and date range, and parses these logs line by line for a given string.

In general, since we are limiting the number of days a user can search for a string, depending on the number of files that are returned by the Kusto query, the program will run for anywhere between 20s and 1m30s. 

## 📋 How to use
The program requires all arguments to be passed when running it in command line:

        dotnet run --errorString={SEARCH_STRING} --repository={REPOSITORY_NAME} --startDate={STARTING_DATE_RANGE} --endDate={ENDING_DATE_RANGE} --option={RESULT_TYPE}
        
See the Input section below for more details on input constraints.


### Input
Run the console app in terminal and pass all of the following options:

- `errorString`: The error string the program will search for
- `repository`: The public repository whose test logs will be parsed
- `startDate`: The start date of the date range in which the test logs will be searched. This argument must be in the format **yyyy/MM/dd**.
- `endDate`: The end date of the date range in which the test logs will be searched. This argument must be in the format **yyyy/MM/dd**.
- `option`: Either 0 or 1. 0 corresponds to Hits - it will return an array of all occurences of `errorString`, including each occurrence's line number within its test log file. 1 corresponds to HitsPerFile - it will return an array of hits per file, including the count of occurrences per file.

#### Example

    dotnet run --errorString=Exception --repository=microsoft-ui-xaml-lift --startDate=2022-05-30 --endDate=2022-06-02 --option=1
    
This command will search for all instances of the string "Exception" in all the `microsoft-ui-xaml-lift` Helix test logs created between May 30, 2022 and June 2, 2022. It will return the number of hits found per file. 

### Output

Here is some sample output showing the 2 different response types.

#### Hits per File
        {
          "filter": {
            "repository": "microsoft-ui-xaml-lift",
            "errorString": "Registering TestPoolFilter: LayoutExceptionPoolFilter",
            "startDate": "2022-06-01T00:00:00",
            "endDate": "2022-06-07T00:00:00"
          },
          "hits": [
            {
              "occurrencesPerFile": 12,
              "jobId": 19898155,
              "friendlyName": "External.Foundation.Graphics.SwapChain",
              "status": "Fail",
              "started": "2022-06-01T22:27:18.448Z",
              "finished": "2022-06-01T22:32:40.479Z",
              "consoleUri": "https://helixri8s23ayyeko0k025g8.blob.core.windows.net/microsoft-ui-xaml-lift-refs-heads-release-reu0e358632a2bd4e9cae/External.Foundation.Graphics.SwapChain/1/console.096db451.log?sv=2019-07-07&se=2022-08-30T22%3A04%3A21Z&sr=c&sp=rl&sig=qPB6%2BlJpAIhWjQPZ4SSXsMS2xHbPei8kRePMW7w5izQ%3D",
              "queueName": "windows.10.amd64.clientrs5.xaml",
              "attempt": 1
            },
            {
              "occurrencesPerFile": 11,
              "jobId": 19923930,
              "friendlyName": "Foundation-Graphics-LTETests",
              "status": "Fail",
              "started": "2022-06-06T11:51:44.894Z",
              "finished": "2022-06-06T11:55:36.26Z",
              "consoleUri": "https://helixri8s23ayyeko0k025g8.blob.core.windows.net/microsoft-ui-xaml-lift-refs-heads-release-10-074226e7c9ef4d8e8a/Foundation-Graphics-LTETests/1/console.de79ef72.log?sv=2019-07-07&se=2022-09-04T11%3A23%3A13Z&sr=c&sp=rl&sig=SqtoHztUOUPk0mTAc8LP7l8mmK7KQVcOH7yKHnPIM3c%3D",
              "queueName": "windows.10.amd64.clientrs5.xaml",
              "attempt": 1
            },
            ...
          ],
          "occurrenceCount": 547,
          "filesCount": 17
        }
        OCCURRENCES COUNT: 547
        FILE COUNT: 17
        TIME ELAPSED: 00:00:31.2928707
        LINES SCANNED/SEC: 2572.3111430617323
        FILES SCANNED/SEC: 0.7030355319878019
        TOTAL FILES SCANNED: 22

#### Hits 
        {
          "filter": {
            "repository": "microsoft-ui-xaml-lift",
            "errorString": "Registering TestPoolFilter: LayoutExceptionPoolFilter",
            "startDate": "2022-06-01T00:00:00",
            "endDate": "2022-06-07T00:00:00"
          },
          "hits": [
            {
              "lineContent": "Registering TestPoolFilter: LayoutExceptionPoolFilter",
              "lineNumber": 193,
              "jobId": 19907315,
              "friendlyName": "External.Controls.ListBox",
              "status": "Fail",
              "started": "2022-06-03T02:54:50.893Z",
              "finished": "2022-06-03T03:00:38.11Z",
              "consoleUri": "https://helixri8s23ayyeko0k025g8.blob.core.windows.net/microsoft-ui-xaml-lift-refs-heads-master-56659122ec5e48668e/External.Controls.ListBox/1/console.8e2f700e.log?sv=2019-07-07&se=2022-09-01T02%3A29%3A47Z&sr=c&sp=rl&sig=cGaAAP3veBprqoo%2FhOAhSruyPG0fPrxAwaPt8rKKzRI%3D",
              "queueName": "windows.10.amd64.client20h2.xaml",
              "attempt": 1
            },
            {
              "lineContent": "Registering TestPoolFilter: LayoutExceptionPoolFilter",
              "lineNumber": 220,
              "jobId": 19923624,
              "friendlyName": "WPF-External.Controls.Flyout",
              "status": "Fail",
              "started": "2022-06-06T10:28:57.149Z",
              "finished": "2022-06-06T10:34:06.403Z",
              "consoleUri": "https://helixri8s23ayyeko0k025g8.blob.core.windows.net/microsoft-ui-xaml-lift-refs-heads-master-7cecd6e7d1454a989b/WPF-External.Controls.Flyout/1/console.6baf9fd3.log?sv=2019-07-07&se=2022-09-04T09%3A55%3A21Z&sr=c&sp=rl&sig=WXbw0LU0nk826JFG6Cz1lltb30sfJ88icQ6Z3U8hE24%3D",
              "queueName": "windows.10.amd64.client20h2.xaml",
              "attempt": 1
            },
            ...
          ],
          "occurrenceCount": 547,
          "filesCount": 17
        }
        OCCURRENCES COUNT: 547
        FILE COUNT: 17
        TIME ELAPSED: 00:00:31.5154119
        LINES SCANNED/SEC: 2554.1471663265806
        FILES SCANNED/SEC: 0.6980711554653677
        TOTAL FILES SCANNED: 22


## 🔍 Performance findings

We can take a look at how long the program ran for different volumes of logs retrieved and parsed, as well as for different lengths of the search string.

Repository: `microsoft-ui-xaml-lift`, String: `"Exception"`

| Start date  | End date    | # of Occurrences | # of Files with hits     | Total time elapsed | Lines scanned/sec | Files scanned/sec | Total files scanned 
| ----------- | ----------- |-------------- | --------------------- | ------------------ | ----------------- | ----------------- | ------------------ | 
| 2022/06/01  | 2022/06/07   | 2528           | 20                    | 00:00:31.7819027   | 2532.73           | 0.69              | 22
| 2022/05/25  | 2022/06/07   | 22768           | 510                   | 00:00:35.2533931   | 41198.75        | 14.60              | 515
| 2022/05/07  | 2022/06/07   | 124973           | 3023                   | 00:00:41.9848476   | 193610.51        | 79.95             | 3357

Repository: `microsoft-ui-xaml-lift`, String: `"Registering TestPoolFilter: LayoutExceptionPoolFilter"`

| Start date  | End date    | # of Occurrences | # of Files with hits     | Total time elapsed | Lines scanned/sec | Files scanned/sec | Total files scanned 
| ----------- | ----------- |-------------- | --------------------- | ------------------ | ----------------- | ----------------- | ------------------ | 
| 2022/06/01  | 2022/06/07   | 547           | 17                    | 00:00:31.2928707   | 2572.31           | 0.70              | 22
| 2022/05/25  | 2022/06/07   | 6106           | 124                   | 00:00:28.0314279   | 51813.12         | 18.37              | 515
| 2022/05/07  | 2022/06/07   | 16431           | 310                   | 00:00:49.0204510   | 165822.79         | 68.48              | 3357

Note that the time taken can vary based on the repository, date range, network, etc so this is just a snapshot of a couple of times of running the program. But in general the times are pretty consistent and stay under a minute. 

## 🤔 Future considerations
- More input sanitization to limit number of rows returned by Kusto and avoid timeouts, also to avoid injections into the query
- Error handling for if we try to parse a file that doesn't exist on the server anymore

