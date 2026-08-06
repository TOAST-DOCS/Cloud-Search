<!-- pre-align:aligned sig=51287bc99a9c -->

<a id="search-cloud-search-overview"></a>
## Search > Cloud Search > Overview { #search-cloud-search-overview }

Search service can be implemented with no additional infrastructure or search solution.

- Enter data to search by using Index REST API.
- Get search results by using Search REST API. to get search results.

<a id="developing-search-service"></a>
### Developing Search Service { #developing-search-service }

**Service Configuration**

![img](http://static.toastoven.net/prod_search/block_diagrm-en-20200304.png)

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
