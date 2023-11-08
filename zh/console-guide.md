## Search > Cloud Search > Console User Guide

## Prerequisites

- The appkey, 'CwSx6kv99g0QuNtM', is different for each user.

## Getting Started

First, enable the Cloud Search Service.

1. Go to **NHN Cloud Console** and click **Select Service**.

2. Click **Cloud Search**.

![img](http://static.toastoven.net/prod_search/product-use-02-en-20210506.jpg)<br>

Do as follows to check if service is enabled:

1. Click **Search** on the left menu on **NHN Cloud Console**.

2. If you can find **Cloud Search**, the service has been enabled.

![img](http://static.toastoven.net/prod_search/product-use-03-en-20210506.jpg)

## Basic Usage

### 1. Creating Services

 Services can be created as follows:

1. Click **Create Services**.

2. Enter Service ID on **Create Services**.

    - Only English in lowercase, numbers, as well as \_(underscore) and -(hypen) are available.
    - Cannot start with a number, \_(underscore) or -(hypen).
    - At least two characters are required.

3. Click **Save**.

![img](http://static.toastoven.net/prod_search/domain_create_prodedure-en-20210506.jpg)<br>

Check the result of service creation.

1. Click Service ID which is created (test).

![img](http://static.toastoven.net/prod_search/domain_create_result-en-20210506.jpg)

### 2. Setting Fields

Fields can be added as follows:

1. Click **Set Fields**.

2. Click **Add Fields**.

3. Enter field name.

    - Only English in lowercase, numbers, as well as \_(underscore) and -(hypen) are available.
    - Cannot start with a number, \_(underscore) or -(hypen).
    - At least two characters are required.

4. Check whether to use multivalued.

    - You can only use , (comma) as a delimiter for field values, and you can have up to 30 commas.

5. Check whether to use index.

6. Check whether to use filter.

7. Check whether to use sorting.

8. Check whether to use summary.

9. Click **Save**.

![img](http://static.toastoven.net/prod_search/field_create_procedure-en-20230831.jpg)

### 3. Indexing

Do as follows to create and index files.

**Create Index Files**

- Create indexing request files in the format of example as below.
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
      "title": "[Addidas] 114 types of new sneakers/slides",
      "body": "[Collection of Addidas Shoes ♥] Free Shipping [Addidas] Get 114 types of new slides/Superstar Stan Smith/Tubular and more!"
    }
  }
]
```

- File Description
    - action
        - add: Document is added.  
            - Updated, if same ID exists.
        - delete: Document is deleted.
    - id
        - Original ID of document.
        - ID type is character strings.
    - The largest file size is 8MB.
        - Larger than 8 MB can be divided into many for indexing.

**How to Indexing**

1. Click **Indexing**.

2. Click **Select File**.

3. Select a file to indexing.

4. Click **Open**.

5. Indexing command comes as REST API.

    - Use REST APIs to develop your search service.

6. Click **Indexing**.

7. Check indexing results.

![img](http://static.toastoven.net/prod_search/indexing_procedure_01-en-20230831.jpg)
![img](http://static.toastoven.net/prod_search/indexing_procedure_02-en-20230831.jpg)<br>

**REST API**

REST APIs are available like below:

- Indexing API
    - Request
        - By File Uploading
            ```
            curl -XPOST 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing' -H 'Accept-Language:en' -H 'Content-Type:multipart/form-data; charset=UTF-8' -F 'file=@documents.json
            ```
        - By Payload
            ```
            curl -XPOST 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing' -H 'Accept-Language:en' -H 'Content-Type:application/json; charset=UTF-8' -d '
            [
              {
                "action": "add",
                "id": "id-1",
                "fields": {
                  "title": "[Free Shipping] 195 types of Nike shoes!!",
                  "body": "The one and only Nike shoes are best selling for good reasons. Nike'\''s 195 Hot-selling shoes★ Guess you need at least one pair of them??"
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
- Indexing Result Check API
    - Request
        ```
        curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing_log?id=1' -H 'Accept-Language:en'
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
            - 2: Ignored (indexing requests before field setting change are ignored)
            - 3: Progressing
            - 4: Successful
            - 5: Failed
            - 6: Canceled

### 4. Search

Do as follows to search:

1. Click **Search**.

2. Check field name to search.

3. Set weighted value for each field to search.

    - Set a value between 0.0 and 1.0.
    
4. Select a field to sort by.

    - If you want to multisort, select the multisort fields.
    - Specify how you want to sort.

5. Check a field for output on the search result.

6. Set the length of search result.

7. Set the highlighted pre tag.

8. Set the highlighted post tag.

9. Specify the priority order for an output from search result.

    - Set '1' to to start with rank 1,or set '10' to start from rank 10.

10. Specify the number of search results.

    - Set '5' to show 5, or '10' to show 10.

11. Select a search operator.

12. Enter a word to search.

13. Click a search icon.

14. Settings from 2 to 11 come as REST API.

     - Use REST APIs to develop your search service.

15. The search result shows.  

![img](http://static.toastoven.net/prod_search/basic-search-en-20230831.jpg)<br>

**REST API**

Use REST APIs as below:

- Request
    ```
    curl -G -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,body*1.0,title*1.0&return=&passage.body=180&passage.title=180' --data-urlencode q='Nike shoes' --data-urlencode highlight='<b>,</b>' -H 'Accept-Language:en'
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
		        "query" : "Nike shoes",
		        "start" : 1,
		        "itemCount" : 1,
		        "total" : 1,
		        "itemList" : {
		          "item" : [
		          {
		            "_RELEVANCE" : 100,
		            "_RANK" : 1,
		            "_ID" : "id-2",
		            "body" : "Prices for 109 types of Addidas <b>shoes</b>. Hesiation only pushes early",
		            "title" : "[Super Low Prices]<b>Nike</b> <b>shoes</b> 109 types"
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

![img](http://static.toastoven.net/prod_search/stats-en-20200304.jpg)<br>

**REST API**

- Request
    ```
    curl -i -XGET 'http://kr1-search.api.nhncloudservice.com/stats/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/stats?kind=total_query_count&date=2020-03-09' -H 'Accept-Language:en'
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

- Make sure to set indexing ACL since data may be deleted by others.
- Testing on console is not relevant with ACL setting.

**How to Set ACL**

The example regards to setting which allows indexing only when the IP address is 202.179.177.21, while search requests are available from all IPs.

1. Click **ACL**.

2.  Enter IP address for **Enable** below **Indexing**.

3. Enter 'all' for **Enable Statistics**.

4. Enter 'all ' for **Enable Search**.

5. Click **Save**.

![img](http://static.toastoven.net/prod_search/acl_procedure-en-20200304.jpg)

## Feature Details

### Deleting Fields

Do as follows to delete fields:

1. Click **Delete** for a field to delete.

   - Fields used as multisort fields cannot be deleted. Delete the multi-sort field before proceeding.

2. Click **Save**.

3. Click **Reindex now**.

    - Documents cannot be added, edited, or deleted while re-indexing.

![img](http://static.toastoven.net/prod_search/field_delete-1-en-20230831.jpg)
![img](http://static.toastoven.net/prod_search/field_delete-2-en-20230831.jpg)
![img](http://static.toastoven.net/prod_search/field_delete-3-en-20230831.jpg)

### Editing Fields

Editing is not supported. To edit, delete a field and add again.

### Filtering

**Set Fields**

1. Check whether to use filter for the target field.
2. For 'text' type, the filter feature is not supported.

![img](http://static.toastoven.net/prod_search/filtering-field-en-20230831.jpg)

- The feature is only available for fields with filters checked. 

**Indexing**

To test, index request data as below:

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

![img](http://static.toastoven.net/prod_search/filtering-search-en-20230831.jpg)

Enter filtering values like below:

1. filter_and: Used when single-value filterig, and AND operations between filter fields are required.
2. filter_or: Used when OR operations between filter fields are required.
   - Not available for scoping, latitude filtering.

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

![img](http://static.toastoven.net/prod_search/geolocation-field-en-20230831.jpg)

**Indexing**

To test, index data as below:

```
[
  {
    "action": "add",
    "id": "id-1",
    "fields": {
      "name" : "FX Math Academy",
      "location" : [10.1, 10.1]
    }
  },
  {
    "action": "add",
    "id": "id-2",
    "fields": {
      "name" : "Tree Thinking Math Academy",
      "location" : [10.3, 10.4]
    }
  },
  {
    "action": "add",
    "id": "id-3",
    "fields": {
      "name" : "Morning of Math Academy",
      "location" : [10.4, 10.3]
    }
  }
]
```

- Enter value in the format of [{Longitude}, {Latitude}] for geo_point type.

**Search**

- Filter by Radius
    1. Enter a value to filter.
        - Format: [{Longitude},{Latitude}],{Radius}
        - Example: [10.3,10.3], 15km
            - Search documents that are located within 15 km in radius as of 10.3 in longitude and latitude, only.    
            - Radius units are 'km', 'm', and 'cm'.

![img](http://static.toastoven.net/prod_search/geolocation-search-circle-en-20230831.jpg)

- Filter by Polygon
    1. Enter a value to filter.
        - Format: [{Longitude 1},{Latitude 1}],[{Longitude 2},{Latitude 2}],[{Longitude N},{Latitude N}]
        - Example: [10.2,10.2],[10.3,10.5],[10.5,10.2]
        - Every point is connected in the clockwise.
        - Search documents within connected polygon, only.

![img](http://static.toastoven.net/prod_search/geolocation-search-polygon-en-20230831.jpg)

### Sorting

**Set Fields**

1. Check whether to use sorting for the target field.
2. For 'text' type, the sorting feature is not supported.
3. Sorting is not supported when using multiple values.

![img](http://static.toastoven.net/prod_search/sorting-field-01-en-20230831.jpg)

- The feature is only available for fields with sorting checked.

**Setting up multiple sorting**

1. Enter a field name.
2. After adding the destination fields, select them to adjust their order.
- If there is more than one sort, it will be output.
   - Sort in the order of your choice.
3. Select how you want each field to be sorted.

![img](http://static.toastoven.net/prod_search/sorting-field-02-en-20230920.jpg)

- The feature is available when 2 or more fields have sorting checked.

**Indexing**

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

    - Sort in the "popular" order in the below example.
    - When the "popular" index is same, sort in the "price" order.   

![img](http://static.toastoven.net/prod_search/sorting-search-01-en-20230831.jpg)
![img](http://static.toastoven.net/prod_search/sorting-search-02-en-20230831.jpg)

- You can select one sorting field.

### Summary

**Set Fields**

1. Check whether to use summary for the target field.
2. For 'text', 'geo_point' types, the summary feature is not supported.

![img](http://static.toastoven.net/prod_search/aggregation-field-en-20230831.jpg)

- Only such fields in which index is checked can have Summary enabled.

**Indexing**

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

![img](http://static.toastoven.net/prod_search/aggregation-search-en-20230831.jpg)

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

![img](https://static.toastoven.net/prod_search/boolean_query-field-en-20230831.jpg)

**Indexing**

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

![img](https://static.toastoven.net/prod_search/boolean_query-search-en-20230831.jpg)

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

### Specify field weight

**Search**

- Search for "Nike".

![img](http://static.toastoven.net/prod_search/document_boosting-search-01-en-20230831.jpg)
![img](http://static.toastoven.net/prod_search/document_boosting-search-02-en-20230831.jpg)

**Search result**

```
"itemList": {
  "item": [
    {
      "_RELEVANCE": 200,
      "_RANK": 1,
      "_ID": "id-2",
      "title": "<b>Nike</b>"
      "body": "<b>Nike</b>"
    },
    {
      "_RELEVANCE": 200,
      "_RANK": 2,
      "_ID": "id-1",
      "title": "<b>Nike</b>"
      "body": "<b>Nike</b>"
    }
  ]
}
```

- The "title" field is heavily weighted so that the "id-2" document appears at the top of the search results.

**Adjust the weight ratio**

- Use the doc_weight_ratio parameter to adjust the reflection ratio.
  ```
  curl -G -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,title*1.0&return=&passage.title=180&doc_weight_ratio=0.1' --data-urlencode q='Nike' --data-urlencode highlight='<b>,</b>' -H 'Accept-Language:en'
  ```
- You can enter a value between 0.0 and 1.0.
- The default is 1.0.

**Tip**

- You can customize the order in which search results are displayed by adjusting the search weight and document ranking.


### Specifying Document Ranks

**Set Fields**

![img](http://static.toastoven.net/prod_search/document_ranking-field-en-20230831.jpg)

**Indexing**

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

![img](http://static.toastoven.net/prod_search/document_ranking-search-en-20230831.jpg)

**Search Results**

```
"itemList": {
  "item": [
    {
      "_RELEVANCE": 100,
      "_RANK": 1,
      "_ID": "id-2",
      "title": "<b>Nike</b>"
    },
    {
      "_RELEVANCE": 100,
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

![img](https://static.toastoven.net/prod_search/field-download-en-20230831.jpg)

**Upload Setting**

1. Click **Upload Setting** to upload setting.     

![img](https://static.toastoven.net/prod_search/filed-upload-en-20230831.jpg)

- Only when there is no field setting, the **Upload Setting** button shows.

### Re-indexing Entire Data
To re-index the entire data, use Full Indexing API.

- Start Full indexing
    ```
    curl -i -XPOST 'http://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing/full/begin'
    ```
    - A new index (repository) is created.
    - Before Full indexing is applied, service is provided with the existing index.
- Request Full indexing
    ```
    curl -XPOST 'http://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing/full' -H 'Content-Type:multipart/form-data; charset=UTF-8' -F 'file=@documents-001.json'
    ```
    - Indexing is requested for many times, such as documents-002.json, and documents-003.json.
- Apply Full indexing
    ```
    curl -i -XPOST 'http://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing/full/end'
    ```
    - Indexed data is applied to service.
- Cancel Full indexing
    ```
    curl -i -XPOST 'http://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing/full/cancel'
    ```
    - Service becomes inoperable while indexing is underway.

## Guide Details

### Field Type
Field type can be selected like below.

![img](http://static.toastoven.net/prod_search/field_type-en-20230831.jpg)

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

![img](http://static.toastoven.net/prod_search/analyzer-en-20230831.jpg)

- default
    - Use morpheme analyzer to separate words:
      - Example) "New Nike Shoes" -> "New" "Nike" "Shoes"
- whitespace
    - Use whitespace as delimiter to separate tokens.
      - Example) "New Nike Shoes" -> "Nike" "New Shoes"
- bigram
    - Separate words by two characters
      - Example) "New Nike Shoes" -> "ne" "nw" "ni" "ik" "ke" "sh" "ho" "oe" "es"
- quadgram
  - Separate words by 4 letters.
    - Example) "Stansmith" -> "Stans" "tansmith"
- trigram
  - Separate words by 3 letters.
    - Example) "Stansmith" -> "Stans" "tansmith" "smith"
- unigram
  - Separate words by 1 letter.
    - Example) "Stansmith" -> "S" "tan" "s" "mi" "th"

### ACL

ACL can be set on the below page:  

![img](http://static.toastoven.net/prod_search/acl-detail-en-20200304.jpg)

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
    	  .post("https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing")
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
    curl_setopt($ch, CURLOPT_URL,"https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing");
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
