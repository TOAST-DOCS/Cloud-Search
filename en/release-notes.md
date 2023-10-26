## Search > Cloud Search > Release Notes

### Sep 26, 2023

- Release of a new version
    - Modified REST API information
    - Refined field settings
    - Added indexing extraction options (BIGRAM, TRIGRAM, QUADGRAM)

### Nov 23, 2021
- Updated the Korean analyzer dictionary.

### June 23, 2020

- Converted into Official Service from the Beta version.

### May 26, 2020

- Added the feature of re-indexing the entire data.

### Mar 24, 2020

- Converted into Beta Service from the Alpha Service.

### Jan 29, 2019

- Added the statistics feature.

### Nov 27, 2018

- Added the feature of Boolean Search.  
    - q='Nike & (shoes | shoes) & ! Addidas'
- Added the downloading/uploading field setting feature.

### Oct 23, 2018

- Added the payload-type indexing
    - Only file-uploading type was available before

### Sept 11, 2018

- Added the feature of specifying document ranks.
    - The priority of search results can be specified for a specific document.

### July 24, 2018

- Added the feature of specifying weights in document.  
    - Specific documents can be exposed on top of search results.
- Added the geolocation feature.
- Added total index size and total number of documents to the index log

### June 26, 2018

- Added bigram morpheme analyzer.
- Added the multiple sorting feature.
- Allowed to enter data in sequence.

### May 3, 2018

- Modified error in morpheme analysis.
    - Different morpheme analysis methods were applied each for document indexing and search words.  
    - Fixed an issue in which words were not properly searched due to different morpheme analysis on index and search.  

### Feb 22, 2018

- Released the Cloud Search service
