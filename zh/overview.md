## Search > Cloud Search > Overview

Search service can be implemented with no additional infrastructure or search solution.

- Enter data to search by using Index REST API.
- Get search results by using Search REST API. to get search results.

### Developing Search Service

**Service Configuration**

![](http://static.toastoven.net/prod_search/block_diagrm-en-20200304.png)

**Development Process**

1. Create Service

    - The Search Service is created.

2. Set Fields

    - Set scheme for search data.

3. Indexing

    - Create JSON data according to the Cloud Search input format.
    - Use REST API to enter created JSON data for Cloud Search.

4. Search

    - Configure the front page with the result of Index REST API.
