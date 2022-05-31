# Project Epic Draft

Developers for .NET applications need a way to easily find where a specific error has occurred in their failed tests. We want to build an API that given a repository and error message, will return the occurrences of the error in the repository's failed test logs.

## Business Objectives
- [ ] P0: Developers can make a call to an API to search for all available Helix test logs that contain a specific error message to help with error investigation
- [ ] P1: Developers can refer to written documentation to understand how to make calls to the API.
- [ ] P2: Developers can interact with the API through a CLI/UI


## Timeline
Week    | Milestone 
------  | ------
 1      | Onboarding + Introduction to project, Dev environment set-up    
 2      | Learn Helix basics, write design document
 3      | Get design document reviews and start implementing POC    
 4      | Finish implementing POC
 5      | POC testing + deployment (if possible) + start implementing API
 6      | Continue API implementation + integrate possible additional features from design doc
 7      | Finish API implementation  
 8      | API testing + documentation (Probably want to test out API on same Azure data centre as test logs?)
 9      | API testing + documentation
 10      | Prepare for customer presentation
 11      | Customer presentation
 12      | Final week :)
 
 
 
## One-pager

The one-pager PR can be found [here](https://github.com/dotnet/arcade/pull/9382) 
