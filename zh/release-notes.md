## Search > Cloud Search > Release Notes

### 2020. 05, 26.

- 전체 데이터를 다시 색인하는 기능을 추가했습니다.

### Mar. 24, 2020
* Converted into Beta Service from the Alpha Service.

### Jan. 29, 2019
* Added the statistics feature.

### Nov. 27, 2018
* Added the feature of Boolean Search.  
    * q='Nike & (shoes | shoes) & ! Addidas'
* Added the downloading/uploading field setting feature.

### Oct. 23, 2018
* Added the payload-type indexing
    * Only file-uploading type was available before

### Sept. 11, 2018
* Added the feature of specifying document ranks.
    * The priority of search results can be specified for a specific document.

### July 24, 2018
* Added the feature of specifying weights in document.  
    * Specific documents can be exposed on top of search results.
* Added the geolocation feature.
* Added total index size and total number of documents to the index log

### June 26, 2018
* Added bigram morpheme analyzer.
* Added the multiple sorting feature.
* Allowed to enter data in sequence.

### May 3, 2018
* Modified error in morpheme analysis.
    * Different morpheme analysis methods were applied each for document indexing and search words.  
    * Fixed an issue in which words were not properly searched due to different morpheme analysis on index and search.  

### Feb. 22, 2018
* Released the Cloud Search service
