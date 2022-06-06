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

#### Hits 

#### Hits per File

## Findings

### Tests
