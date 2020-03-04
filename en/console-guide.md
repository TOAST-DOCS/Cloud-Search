## Search > Cloud Search > Console User Guide

## Prerequisites
- The host name, 'api-7ab1617e2df0f1d1-search.cloud.toast.com', within document, may be different for each user.
- The appkey, 'EMKPutYozUttWVY2', is different for each user.

## Getting Started
First, enable the Cloud Search Service.

1. Go to **TOAST Console** and click **Select Service**.

2. Click **Cloud Search**.

![](http://static.toastoven.net/prod_search/product-use-02-20200116.1057.png)<br>

Do as follows to check if service is enabled:

1. Click **Search** on the left menu on **TOAST Console**.
2. If you can find **Cloud Search**, the service has been enabled.

![](http://static.toastoven.net/prod_search/product-use-03-20200116.1148.png)

## Basic Usage

### 1. Creating Services

 Services can be created as follows:

1. Click **Create Services**.
2. Enter Service ID on **Create Services**.
   - Only English in lowercase, numbers, as well as _ (underscore) and - (hypen) are available.
   - Cannot start with a number, _ (underscore) or - (hypen).
   - At least two characters are required.
3. Click **Save**.

![](http://static.toastoven.net/prod_search/domain_create_prodedure-20200116.1710.png)<br>

Check the result of service creation.

1. Click Service ID which is created (test).

![](http://static.toastoven.net/prod_search/domain_create_result-20200116.1655.png)


### 2. Setting Fields

Fields can be added as follows:

1. Click **Set Fields**.

2. Click **Add Fields**.

3. Enter field name.

    - Only English in lowercase, numbers, as well as _ (underscore) and - (hypen) are available.
    - Cannot start with a number, _ (underscore) or - (hypen).
    - At least two characters are required.

4. Click **Save**.

![](http://static.toastoven.net/prod_search/field_create_procedure-20200116.1714.png)

### 3. Indexing

Do as follows to create and index files.

**Create Index Files**

- Create index request files in the format of example as below.
- Create files encoded in UTF-8.
  - Save the file on Windows memo, by specifying UTF-8 for encoding.
- It was created in the name of data/documents.json in the example.

```
[
  {
    "action": "add",
    "id": "id-1",
    "fields": {
      "title": "[Free Shipping] 195 types of Nike shoes!!",
      "body":"The one and only Nike shoes are best selling for good reasons. Nike's 195 Hot-selling shoes★ Guess you need at least one pair of them??"  
    }
  },
  {
    "action": "add",
    "id": "id-2",
    "fields": {
      "title": "[Super Low Prices]109 types of Nike shoes",
      "body": "Just 7-day Opportunities! [Super Low Prices] for 109 types of Addidas shoes. Hesiation only pushes early sold-out"
    }
  },
  {
    "action": "add",
    "id": "id-3",
    "fields": {
      "title": "[Addidas] 114 types of new
      sneakers/slides",
      "body": "[Collection of Addidas Shoes ♥] Free Shipping [Addidas] Get 114 types of new slides/Superstar Stan Smith/Tubular and more!"

    }
  }
]
```

* File Description
    * action
        * add: Document is added.  
            * Updated, if same ID exists.
        * delete: Document is deleted.
    * id
        * Original ID of document.
        * ID type is character strings.
    * The largest file size is 8MB.
        * Larger than 8 MB can be divided into many for indexing.

**How to Index**

1. Click **Index**.

2. Click **Select Files**.

3. Select a file to index.

4. Click **Open**.

5. Index command comes as REST API.

    - Use REST APIs to develop your search service.

6. Click **Index**.

7. Check index results.

![](http://static.toastoven.net/prod_search/indexing_procedure_01-20200116.1827.png)
![](http://static.toastoven.net/prod_search/indexing_procedure_02-20200117.1123.png)<br>

**REST API**

REST APIs are available like below:

- Index API
    - Request
        - By File Uploading
            ```
            curl -XPOST 'https://api-7ab1617e2df0f1d1-search.cloud.toast.com/indexing/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/indexing' -H 'Content-Type:multipart/form-data; charset=UTF-8' -F 'file=@documents.json'
            ```
        - By Payload
            ```
            curl -XPOST 'https://api-7ab1617e2df0f1d1-search.cloud.toast.com/indexing/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/indexing' -H 'Content-Type:application/json; charset=UTF-8' -d '
            [
              {
                "action": "add",
                "id": "id-1",
                "fields": {
                  "title": "[Free Shipping] 195 types of Nike shoes!!",
                  "body": "The one and only Nike shoes are best selling for good reasons. Nike's 195 Hot-selling shoes★ Guess you need at least one pair of them??"
                }
              },
              {
                "action": "add",
                "id": "id-2",
                "fields": {
                   "title": "[Super Low Prices]109 types of Nike shoes",
                  "body": "Just 7-day Opportunities! [Super Low Prices] for 109 types of Addidas shoes. Hesiation only pushes early sold-out"
                }
              }
            ]'
            ```
    - Response
        ```
        {
          "id" : 1
        }
        ```
- Index Result Check API
    - Request
        ```
        curl -i -XGET 'https://api-7ab1617e2df0f1d1-search.cloud.toast.com/indexing/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/indexing_log?id=1'
        ```
        - id 1 refers to the ID for Response of Index API in the above.
    - Response
        ```
        {
          "request_time" : "2017-10-23T12:36:43",
          "file_name" : "documents.json",
          "file_size" : 1185,
          "status" : 4
        }
        ```
        - status
            - 1: Waiting  
            - 2: Ignored (index requests before field setting change are ignored)
            - 3: Progressing
            - 4: Successful
            - 5: Failed

### 4. Search

Do as follows to search:

1. Click **Search**.

2. Check field name to search.

3. Set weighted value for each field to search.

    - Set a value between 0.0 and 1.0.

4. Check a field for output on the search result.

5. Set the length of search result.

6. Set the highlighted pre tag.

7. Set the highlighted post tag.

8. Specify the priority order for an output from search result.

    - Set '1' to to start with rank 1,or set '10' to start from rank 10.

9. Specify the number of search results.

    - Set '5' to show 5, or '10' to show 10.

10. Select a search operator.

11. Enter a word to search.

12. Click a search icon.

13. Settings from 2 to 11 come as REST API.
     - Use REST APIs to develop your search service.

14. The search result shows.  

![](http://static.toastoven.net/prod_search/basic-search-20200116.1847.png)<br>

**REST API**

Use REST APIs as below:

- Request
    ```
    curl -G -XGET 'https://api-7ab1617e2df0f1d1-search.cloud.toast.com/search/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/search?start=1&size=10&q_option=and,body*1.0,title*1.0&return=&passage.body=180&passage.title=180' --data-urlencode q='Nike sneakers' --data-urlencode highlight='<b>,</b>'
    ```
- Response
    ```
    {
      "message" : {
          "meta" : {
            "timezone" : "+09:00"
          },
          "result" : {
            "status" : {
            "code" : 200,
            "message" : "OK"
          },
          "query" : "Nike sneakers",
          "start" : 1,
          "itemCount" : 1,
          "total" : 1,
          "itemList" : {
            "item" : [
            {
              "_RELEVANCE" : 0.07575758,
              "_RANK" : 1,
              "_ID" : "id-2",
              "body" : "Just 7-day Opportunities! [Super Low Prices] for 109 types of Addidas shoes. Hesiation only pushes early sold-out"
              "title" : "[Super Low Prices]<b>Nike</b> <b>Sneakers</b> 109 types"
            }
            ]
          }
        }
      }
    }
    ```

### 5. Statistics

Do as follows to check statistics:

1. Click **Statistics**.

2. Select **Total Query Count** or **Query Count with No Results**.

3. Enter start date.

4. Enter end date.

5. Click **Query** and statistical graph comes as output.

6. Click **Download Data** to download statistical data for each query.

7. Select **Total Document Count** or **Total Index Size**.

8. Enter start date.

9. Enter end date.

10. Click **Query** and statistical graph comes as output.

![](http://static.toastoven.net/prod_search/stats-20200116.1950.png)<br>

**REST API**

- Request
    ```
    curl -i -XGET 'http://api-7ab1617e2df0f1d1-search.cloud.toast.com/stats/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/stats?kind=total_query_count&date=2019-01-08'
    ```
    - kind
        - total_query_count: Total query count
        - no_result_query_count: Query count with no search result
    - date: Date to query
- Response
    ````
    [ [ "Nike", 8 ], [ "Addidas", 4 ] ]
    ````
    - Query more than 3 counts only.

### 6. ACL

IPs may be restricted for equipment which may call index and search REST APIs.

- Make sure to set index ACL since data may be deleted by others.
- Testing on console is not relevant with ACL setting.

**How to Set ACL**

The example regards to setting which allows indexing only when the IP address is 202.179.177.21, while search requests are available from all IPs.

1. Click **ACL**.

2.  Enter IP address for **Enable** below **Index**.

3. Enter 'all' for **Enable Statistics**.

4. Enter 'all ' for **Enable Search**.

5. Click **Save**.

![](http://static.toastoven.net/prod_search/acl_procedure-20200116.1855.png)

## Feature Details

### Deleting Fields

Do as follows to delete fields:

1. Click **Delete** for a field to delete.
2. Click **Save**.
3. Click **Execute Now**.
    - Documents cannot be added, edited, or deleted while re-indexed.

![](http://static.toastoven.net/prod_search/field_delete-1-20200117.0835.png)
![](http://static.toastoven.net/prod_search/field_delete-2-20200117.0843.png)
![](http://static.toastoven.net/prod_search/field_delete-3-20200117.1201.jpg)

### Editing Fields

Editing is not supported. To edit, delete a field and add again.

### Filtering

**Set Fields**

![](http://static.toastoven.net/prod_search/filtering-field-20200117.0858.png)

**Index**

To test, index data as below:

```
[
{
  "action": "add",
  "id": "id-1",
  "fields": {
    "name" : "Nike Air Max",
    "category" : 1
  }
},
{
  "action": "add",
  "id": "id-2",
  "fields": {
    "name" : "Nike Cheyenne Solid",
    "category" : 2
  }
}
]
```

**Search**

1. Enter a filtering value.

![](http://static.toastoven.net/prod_search/filtering-search-20200117.0901.png)

Enter filtering values like below:

- Single-value Filtering
    - Example) category=1
        - category == 1
- Or Filtering
    - Example) category=1|2
        - category == 1 or category == 2
- And Filtering
    - Example) category=1&2
        - category == 1 and category == 2      
- Range-specific Filtering 		
    - Example) category=[1,2]
        - 1 <= category <= 2
    - Example) category={1,2]      
        - 1 < category <= 2
    - Example) category={,2]      
        - category <= 2
    - keyword, boolean, or geo_point type is not available for range-specific filtering.
- Not Filtering
    - Example) category=!1
        - category != 1
    - Example) category=!1|2
        - category !=1 or category == 2
- Date-type Filtering
    - filter='update=[2017-03-22T08:28:44,}'
        - 2017-03-22T08:28:44 <= update
    - filter='update=[,2018-10-02T15:26:28}'
        - update < 2018-10-02T15:26:28
    - filter='update=[2017-03-22T08:28:44,2018-10-02T15:26:28}'
        - 2017-03-22T08:28:44 <= update < 2018-10-02T15:26:28
- Keyword-type Filtering
    - filter='dealer="DNC Shop"|"With Shopping"'
        - Double quotes are recommended for the keyword type.
- Many-Field Filtering
    - filter='category=1&brand=2'
        - category == 1 and brand == 2
    - filter='category=1|brand=2'
        - category == 1 or brand == 2
    - filter='(category=1&brand=2)|(category=3&brand=4)'
        - (category == 1 and brand == 2) or (category == 3 and brand == 4)

### Geolocation Filtering

**Set Fields**

1. Select 'geo_point' as the field type for geolocation.

![S](http://static.toastoven.net/prod_search/geolocation-field-20200117.0910.png)

**Index**

To test, index data as below:

```
[
{
  "action": "add",
  "id": "id-1",
  "fields": {
    "name" : "FX Math Academy(에프엑스수학학원)",
    "location" : [10.1, 10.1]
  }
},
{
  "action": "add",
  "id": "id-2",
  "fields": {
    "name" : "Tree Thinking Math Academy (좋은나무 사고력수학학원)",
    "location" : [10.3, 10.4]
  }
},
{
  "action": "add",
  "id": "id-3",
  "fields": {
    "name" : "Morning of Math Academy (수학의아침학원)",
    "location" : [10.4, 10.3]
  }
}
]
```

- Enter value in the format of [{Longitude}, {Latitude}] for geo_point type.

**Search**

- Filter by Radius (*반경=radius으로 알고 있는데, 혹시 원문처럼 circle로 표기하는게 맞나요?)
    1. Enter a value to filter.
        - Format: [{Longitude},{Latitude}],{Circe}
        - Example: [10.3,10.3], 15km
            - Search documents that are located within 15 km in radius as of 10.3 in longitude and latitude, only.    
            - Radius units are 'km', 'm', and 'cm'.

![](http://static.toastoven.net/prod_search/geolocation-search-circle-20200117.0913.png)

- Filter by Polygon
    1. Enter a value to filter.
        - Format: [{Longitude 1},{Latitude 1}],[{Longitude 2},{Latitude 2}],[{Longitude N},{Latitude N}]
        - Example: [10.2,10.2],[10.3,10.5],[10.5,10.2]
        - Every point is connected in the clockwise.
        - Search documents within connected polygon, only.

![](http://static.toastoven.net/prod_search/geolocation-search-polygon-20200117.0914.png)

### Sorting

**Set Fields**

![](http://static.toastoven.net/prod_search/sorting-field-20200117.0923.png)

**Index**

To test, index data as below:

```
[
{
  "action": "add",
  "id": "id-1",
  "fields": {
    "name" : "Nike Air Max",
    "popular" : 10,
    "price" : 84180
  }
},
{
  "action": "add",
  "id": "id-2",
  "fields": {
    "name" : "Nike Air Zoom",
    "popular" : 5,
    "price" : 97200
  }
},
{
  "action": "add",
  "id": "id-3",
  "fields": {
    "name" : "Nike Air Force",
    "popular" : 5,
    "price" : 74680
  }
}
]
```

**Search**

1. Specify the sorting type.

    - "asc": In the ascending order
    - "desc": In the descending order  

2. Specify the sorting order.

    - Sort in the "popular" order in the above example.
    - When the "popular" index is same, sort in the "price" order.   
    - ![](http://static.toastoven.net/prod_search/sorting-search-20200117.0925.png)

### Summary

**Set Fields**

![](http://static.toastoven.net/prod_search/aggregation-field-20200117.0933.png)

- Only such fields in which index is checked can have Summary enabled.

**Index**

To test, index data as below:

```
[
{
  "action": "add",
  "id": "id-1",
  "fields": {
    "name" : "Nike Air Max",
    "category" : "Shoes"
  }
},
{
  "action": "add",
  "id": "id-2",
  "fields": {
    "name" : "Nike Air Zoom",
    "category" : "Shoes"
  }
},
{
  "action": "add",
  "id": "id-3",
  "fields": {
    "name" : "Nike Swoosh short sleeve t-shirt",
    "category" : "Clothing"
  }
}
]
```

**Search**

1. Check 'Summary' of the "category" field.  

![](http://static.toastoven.net/prod_search/aggregation-search-20200117.0933.png)

**Summary Result**

```
"summary": {
	"category": {
		"Shoes": 2,
		"Clothing": 1
	}
}
```

- Summary information shows along with the search result.
- The "category" has 2 findings with "shoes", and 1 finding with "clothing".  
- Available Types
    - Summary is not available for text and geo_point types.

### Boolean Query

**Set Fields**

![](https://static.toastoven.net/prod_search/boolean_query-field-20200117.0941.png)

**Index**

To test, index data as below:

```
[
{
  "action": "add",
  "id": "id-1",
  "fields": {
    "title" : "Nike Shoes"
  }
},
{
  "action": "add",
  "id": "id-2",
  "fields": {
    "title" : "Nike Shoes"
  }
},
{
  "action": "add",
  "id": "id-3",
  "fields": {
    "title" : "Nike Bags"
  }
}
]
```

**Search**

1. Select 'boolean'.

2. Enter boolean query by using &, |, (, ), or !.  

![](https://static.toastoven.net/prod_search/boolean_query-search-20200117.0943.png)

- In the priority of operators
    - In the order of (), !, &, and |.
- Processing Operands
    - Operands are processed with exact matching.
    - q=Nike Shoes &q_option=boolean
    - Targets which can be searched
        - "Popular Nike Shoes in Sales"
        - "Popular NikeShoes in Sales"
    - Targets which cannot be searched
        - "Popular Nike in Sales Shoes"
            - Due to another word inserted between "Nike" and "Shoes"
        - "Popular Shoes Nike in Sales"
            - Due to wrong order of "Nike" and "Shoes"  

### Specifying Document Weights

**Set Fields**

![](http://static.toastoven.net/prod_search/document_boosting-field-20200117.1006.png)

**Index**

To test, index data as below:

```
[
  {
    "action": "add",
    "id": "id-1",
    "weight": 0.1,
    "fields": {
      "title" : "Nike"
    }
  },
  {
    "action": "add",
    "id": "id-2",
    "weight": 0.9,
    "fields": {
      "title" : "Nike"
    }
  }
]
```

- For "weight", specify 0.1 for "id-1" and 0.9 for "id-2".
- Enter a value between 0.0 and 1.0 for "weight".

**Search**

- Search by "Nike".

![](http://static.toastoven.net/prod_search/document_boosting-search-20200117.1023.png)

**Search Results**

```
"itemList": {
  "item": [
    {
      "_RELEVANCE": 0.45151517,
      "_RANK": 1,
      "_ID": "id-2",
      "title": "<b>Nike</b>"
    },
    {
      "_RELEVANCE": 0.18484849,
      "_RANK": 2,
      "_ID": "id-1",
      "title": "<b>Nike</b>"
    }
  ]
}
```

- The "id-2" document with higher "weight" comes first on the search result.

**Adjust Weight Ratio**

- Use the doc_weight_ratio parameter to adjust the ratio.  
    ```
    curl -G -XGET 'https://api-7ab1617e2df0f1d1-search.cloud.toast.com/search/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/search?start=1&size=10&q_option=and,title*1.0&return=&passage.title=180&doc_weight_ratio=0.1' --data-urlencode q='Nike' --data-urlencode highlight='<b>,</b>'
    ```
    - Enter a value between 0.0 and 1.0.
    - Default is 1.0.

**Adjust Similarity Ratio Between User-input Search Word and Document**

- Use the similarity_ratio parameter to adjust the ratio.
    ```
    curl -G -XGET 'https://api-7ab1617e2df0f1d1-search.cloud.toast.com/search/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/search?start=1&size=10&q_option=and,title*1.0&return=&passage.title=180&similarity_ratio=0.1' --data-urlencode q='Nike' --data-urlencode highlight='<b>,</b>'
    ```
    - Enter a value between 0.0 and 1.0.  
    - Default is 1.0.

**Tip**

- Adjust similarity_ratio and doc_weight_ratio to customize the input order of search results.

### Specifying Document Ranks

**Set Fields**

![](http://static.toastoven.net/prod_search/document_ranking-field-20200117.1006.png)

**Index**

To test, index data as below:

```
[
  {
    "action": "add",
    "id": "id-1",
    "ranking": 2,
    "fields": {
      "title" : "Nike"
    }
  },
  {
    "action": "add",
    "id": "id-2",
    "ranking": 1,
    "fields": {
      "title" : "Nike"
    }
  }
]
```

- For "ranking", specify 1 for "id-1" and 2 for "id-2".
- Enter a value between 1 and 10000 for "ranking".

**Search**

- Search by "Nike".

![](http://static.toastoven.net/prod_search/document_ranking-search-20200117.1023.png)

**Search Results**

```
"itemList": {
  "item": [
    {
      "_RELEVANCE": 10000.151,
      "_RANK": 1,
      "_ID": "id-2",
      "title": "<b>Nike</b>"
    },
    {
      "_RELEVANCE": 9999.151,
      "_RANK": 2,
      "_ID": "id-1",
      "title": "<b>Nike</b>"
    }
  ]
}
```

- The "id-2" document specified as 1 for "ranking" comes first on the search result.
- In case of documents in the same "ranking", such document that has the highest similarity level as user-input search word shows first on the list.

### Downloading/Uploading Field Setting

**Download Setting**

1. Click "Download Setting" to download the current setting.

![](https://static.toastoven.net/prod_search/field-download-20200117.1101.png)

**Upload Setting**

1. Click **Upload Setting** to upload setting.     

![](https://static.toastoven.net/prod_search/filed-upload-20200117.1102.png)

- Only when there is no field setting, the **Upload Setting** button shows.

## Guide Details

### Field Type
Field type can be selected like below.

![](http://static.toastoven.net/prod_search/field_type-20200117.1111.png)

- text
    - To be selected for the fields to 'Search'.
    - Morpheme is analyzed.
        - In case the field value is 'Nikesneakers', search result is available when it is searched by 'Nikeshoes', 'Nike Shoes', 'Nike' or 'Sneakers'.
    - The maximum size is 32,768 bytes.
- keyword
    - To be selected for the fields to 'Filter', 'Sort', or 'Summarize'.
    - Morpheme is not analyzed.
        - In case the field value is 'Nikesneakers', it is 'filtered', 'sorted', and 'summarized' only by 'Nikesneakers'.
        - In case the field value is 'Nike Sneakers', it is 'filtered', 'sorted', and 'summarized' only by 'Nike Sneakers'.
    - The maximum size is 128 bytes.
- byte
    - 1-byte integer type.  
    - Represented from -128 to 127.
- short
    - 2-byte integer type.  
    - Represented in -32, 768~32, and to 767.
- integer
    - 4-byte integer type.  
    - Represented from -2^31~2^31, and to - 1.
- long
    - 8-byte integer type.
    - Represented from -2^63~2^63, and to- 1.
- float
    - 4-byte real number type.  
    - Represented from -3.4E38 to 3.4E38.
- double
    - 8-byte real number type.
    - Represented from -1.7E308 to 1.7E308.
- boolean
    - 1byte
    - true or false
- date
    - To be selected for a date field.
    - Supported Date Format
        - yyyy-MM-dd
            - Example) 2017-09-22
        - yyyy-MM-dd’T’HH:mm:ss
            - Example) 2017-09-22T15:39:28
        - yyyy-MM-dd’T’HH:mm:ss'Z'
            - Example) 2017-09-22T15:39:28Z
        - yyyy-MM-dd'T'HH:mm:ss.SSS
            - Example) 2017-09-22T15:39:28.248
        - yyyy-MM-dd'T'HH:mm:ss.SSS'Z'
            - Example) 2017-09-22T15:39:28.248Z
- All field types, excluding text, are available in the sequence format.
    - ["Nike", "Addidas"]
    - [1.0, 2.0]
    - ["2017-09-22T15:39:28", "2017-09-22T15:39:29"]

### Morpheme Analysis

Morpheme analyzer can be selected as below:

![](http://static.toastoven.net/prod_search/analyzer-20200117.1111.png)

- default
    - Use morpheme analyzer to separate words:
      - Example) "New Nike Shoes" -> "New" "Nike" "Shoes"
- whitespace
    - Use whitespace as delimiter to separate tokens.
      - Example) "New Nike Shoes" -> "Nike" "New Shoes"
- bigram
    - Separate words by two syllables 2글자씩 단어를 분리합니다.
      - Example) "New Nike Shoes (나이키 신상 슈즈)" -> "NewNi" "NiKe" "keShoes"  ("나이" "이키" "신상" "상슈" "슈즈" )
        (*이 부분은, 한글과 영어의 구조가 달라서 원문 그대로 번역하기엔 문제가 있습니다.
        한글은 한 글자가 '자음+모음 (+자음)으로 이루어지는 구조이니 해당 원문처럼 '2글자'씩 정확히 나눌 수 있지만, 영어는 알파벳 한 자가 '글자'이고, 글자가 (자음 또는 모음) 여러개 모여 하나의 단어로 구성됩니다. 따라서, 글자로 나눈다고 하면 N, e, w, N, i, k, e 등 각 알파벳의 모음일 뿐, 2 글자로 만들어도 발음이 되지 못하는 구조가 될 수도 있습니다. (예. Ne, ew, wN )
        따라서, syllable (음절) 단위로 나누는 것이 원문에 가장 비슷한 의미가 아닐까 싶은데요, '2글자'로 분리한다는 원문에 최대한 맞추자니 '2 syllables'로 표현하여, 'NewNi', 'Nike', KeShoes' 등으로 구분해보았습니다.
        그럼에도, 원문과의 의미 차이가 있다면, 영어식 예문을 따로 설정하는 것이 나을 것 같습니다.)'

### ACL

ACL can be set on the below page:  

![](http://static.toastoven.net/prod_search/acl-detail-20200117.1114.png)

- Input Format
    - Input is available in the IP format.
        - Example) 202.179.177.21
    - Input is available in the CIDR format.
        - Example) 202.179.177.0/24
    - Input of many number of IPs or CIDRs is available.
        - Example) 202.179.177.21, 202.179.177.0/24
    - All is matched for All.
    - All is unmatched if value is empty.
- Denied, if applied both to Allow and Deny.
- Denied, if not applied both to Allow and Deny

## Client Example Codes

Following shows the file-uploading type index example codes.

### Java

- dependency

``` java
compile group: 'org.apache.httpcomponents', name: 'httpclient', version: '4.5.6'
compile group: 'org.apache.httpcomponents', name: 'httpmime', version: '4.5.6'
```

- Index (by file uploading)
``` java
package com.toast.cloud.cloudsearch.client;

import org.apache.http.HttpEntity;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.ResponseHandler;
import org.apache.http.client.methods.HttpUriRequest;
import org.apache.http.client.methods.RequestBuilder;
import org.apache.http.entity.ContentType;
import org.apache.http.entity.mime.HttpMultipartMode;
import org.apache.http.entity.mime.MultipartEntityBuilder;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;

import java.io.File;
import java.io.IOException;
import java.io.PrintWriter;

public class IndexingClient {

  public static void main(String[] args) throws IOException {

    String documents = ""
      + "[\n"
      + "  {\n"
      + "    \"action\": \"add\",\n"
      + "    \"id\": \"id-1\",\n"
      + "    \"fields\": {\n"
      + "      \"title\": \"[Free Shipping]195 types of Nike shoes!!\",\n"
      + "      \"body\": \"The one and only Nike shoes are best selling for good reasons. Nike's 195 Hot-selling shoes★ Guess you need at least one pair of them??"\"\n"
      + "    }\n"
      + "  }\n"
      + "]";

    File tempFile = File.createTempFile("documents-",".json", new File("/tmp/"));
    tempFile.deleteOnExit();

    PrintWriter printWriter = new PrintWriter(tempFile);
    printWriter.println(documents);
    printWriter.close();

    try (CloseableHttpClient httpclient = HttpClients.createDefault()) {

      // build multipart upload request.
      HttpEntity data = MultipartEntityBuilder.create()
        .setMode(HttpMultipartMode.BROWSER_COMPATIBLE)
        .addBinaryBody("file", tempFile, ContentType.DEFAULT_BINARY, tempFile.getName())
        .build();

      // build http request and assign multipart upload data.
      HttpUriRequest request = RequestBuilder
    	  .post("https://api-7ab1617e2df0f1d1-search.cloud.toast.com/indexing/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/indexing")
        .setEntity(data)
        .build();

      System.out.println("Executing request " + request.getRequestLine());

      // Create a custom response handler.
      ResponseHandler<String> responseHandler = response -> {
        int status = response.getStatusLine().getStatusCode();
        if (status >= 200 && status < 300) {
          HttpEntity entity = response.getEntity();
          return entity != null ? EntityUtils.toString(entity) : null;
        } else {
          throw new ClientProtocolException("Unexpected response status: " + status);
        }
      };
      String responseBody = httpclient.execute(request, responseHandler);
      System.out.println(responseBody);
    }
  }
}
```

### PHP

- Index (by file uploading)

``` php
<?php
    $documents = ""
      . "[\n"
      . "  {\n"
      . "    \"action\": \"add\",\n"
      . "    \"id\": \"id-1\",\n"
      . "    \"fields\": {\n"
      . "      \"title\": \"[Free Shipping]195 types of Nike shoes!!\",\n"
      . "      \"body\": \"The one and only Nike shoes are best selling for good reasons. Nike's 195 Hot-selling shoes★ Guess you need at least one pair of them??"\"\n"
      . "    }\n"
      . "  }\n"
      . "]";

    $file = DIRECTORY_SEPARATOR.trim(sys_get_temp_dir(), DIRECTORY_SEPARATOR).DIRECTORY_SEPARATOR.ltrim("documents.json", DIRECTORY_SEPARATOR);
    file_put_contents($file, $documents);

    register_shutdown_function(function() use($file) {
        unlink($file);
    });

    $data = array(
        'file' => curl_file_create($file, "application/json", basename($file))
    );

    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL,"https://api-7ab1617e2df0f1d1-search.cloud.toast.com/indexing/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/indexing");
    curl_setopt($ch, CURLOPT_POST, 1);
    curl_setopt($ch, CURLOPT_HTTPHEADER, array("Content-Type:multipart/form-data; charset=UTF-8"));
    curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_HEADER, true);

    $response = curl_exec($ch) or die(curl_error($ch));
    print_r($response);

    curl_close($ch);
?>
```
