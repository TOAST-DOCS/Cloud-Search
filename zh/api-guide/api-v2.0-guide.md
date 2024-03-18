## Search > Cloud Search > API v2.0 Guide

This document describes the Cloud Search API v2.0 provided by NHN Cloud Search.

## Common

**[Request]**

URI Information

| Environment | URI                                        |
| ---- | ------------------------------------------ |
| REAL | https://kr1-search.api.nhncloudservice.com |

Path Parameter Information

| Name      | Description                    |
| --------- | ----------------------- |
| appKey    | Appkey issued from the console |
| serviceId | A random name for the user    |

## Full indexing

If you run full indexing, previously indexed files will disappear.

You must proceed in the start-index-end order.

### 1. Start

**[Request]**

URI Information

| Method | URI                                                                            |
| ------ | ------------------------------------------------------------------------------ |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing/full/begin |

**[Response]**

Response Body

```
{}
```

### 2. Indexing

**[Request]**

URI Information

| Method | URI                                                                      |
| ------ | ------------------------------------------------------------------------ |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing/full |

BODY Information (example)

```
[
    {
        "action": "add",
        "id": "id-1",
        "fields": {
            "title": "Awesome!! You're in first place!!"
        }
    }
]
```

**[Response]**

Response body (example)

```
{
    "id": 1
}
```

### 3. End

**[Request]**

URI Information

| Method | URI                                                                          |
| ------ | ---------------------------------------------------------------------------- |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing/full/end |

**[Response]**

Response Body

```
{}
```

### 4. Cancel

**[Request]**

URI Information

| Method | URI                                                                             |
| ------ | ------------------------------------------------------------------------------- |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing/full/cancel |

**[Response]**

Response Body

```
{}
```

## Additional Indexing

The index is updated if an existing ID exists, or added if it does not.

### 1. Additional Indexing

**[Request]**

URI Information

| Method | URI                                                                 |
| ------ | ------------------------------------------------------------------- |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing |

BODY Information (example)

```
[
    {
        "action": "add",
        "id": "id-2",
        "fields": {
            "title": "Yay!! You're in second place!!"
        }
    }
]
```

**[Response]**

Response body (example)

```
{
    "id": 2
}
```

## Index log

Displays the index results.

### 1. View the index log

**[Request]**

URI Information

| Method | URI                                                                          |
| ------ | ---------------------------------------------------------------------------- |
| GET    | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing_log?id=1 |

Parameter Information

| Name | Description    |
| ---- | ------- |
| id   | Indexing ID |

**[Response]**

Response body (example)

```
{
    "total_doc_count" : 3,
    "request_time" : "2024-01-30T14:12:01",
    "file_name" : "payload-1.json",
    "total_index_file_size" : 355,
    "file_size" : 355,
    "status" : 4
}
```

## Search

You can use the index to search for fields.

### 1. Search

**[Request]**

URI Information (example)

| Method | URI                                                                                                                            |
| ------ | ------------------------------------------------------------------------------------------------------------------------------ |
| GET    | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/search?q=&q_option=and,title\*1.0&start=1&size=10&passage.title=180 |

Parameter Information

| Name             | Description                                    |
| ---------------- | --------------------------------------- |
| start            | Start number (required)                        |
| size             | Size (required)                             |
| q_option         | AND, OR, BOOLEAN, field * weight (required) |
| return           | Output the results                               |
| q                | Query                                    |
| sort             | Sorting                                    |
| passage.*       | Result length                               |
| summary.*       | Summary                                    |
| filter_and       | Filter And                                |
| filter_or        | Filter Or                                 |
| highlight        | Highlight                              |
| doc_weight_ratio | Weight                                  |

**[Response]**

Response body (example)

```
{
    "message": {
        "result": {
            "total": 2,
            "query": "",
            "start": 1,
            "itemList": {
                "item": [
                    {
                        "_ID": "id-1",
                        "_RANK": "0",
                        "_relevance": 100,
                        "title": "Awesome!! We're in first place!!"
                    },
                    {
                        "_ID": "id-2",
                        "_RANK": "0",
                        "_relevance": 100,
                        "title": "Awesome!! You're in second place!!"
                    }
                ]
            },
            "status": {
                "code": 200,
                "message": "OK"
            },
            "itemCount": 2
        },
        "meta": {
            "timezone": "+09:00"
        }
    }
}
```

## Statistics

Statistics show the number of total queries and queries without results by date.

### 1. View stat

**[Request]**

URI Information (example)

| Method | URI                                                                                                  |
| ------ | ---------------------------------------------------------------------------------------------------- |
| GET    | /stats/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/stats?kind=total_query_count&date=2024-01-29 |

Parameter Information

<table>
    <tr>
        <th>Name</th>
        <th>Description</th>
    </tr>
    <tr>
        <td rowspan="2">kind</td>
        <td>total_query_count - Total number of queries</td>
    </tr>
    <tr>
        <td>no_result_query_count - Number of queries without results</td>
    </tr>
    <tr>
        <td>date</td>
        <td>Date</td>
    </tr>
</table>

**[Response]**

Response body (example)

```
[["", 13]]
```
