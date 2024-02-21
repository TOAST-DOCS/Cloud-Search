## Search > Cloud Search > API v2.0 가이드

NHN Cloud Search에서 제공하는 Cloud Search API v2.0 를 설명합니다.

## 공통

**[요청]**

URI 정보

| 환경 | URI                                        |
| ---- | ------------------------------------------ |
| REAL | https://kr1-search.api.nhncloudservice.com |

Path 파라미터 정보

| 이름      | 설명                    |
| --------- | ----------------------- |
| appKey    | 콘솔에서 발급받은 앱 키 |
| serviceId | 사용자의 임의의 이름    |

## ZONE

### 1. 생성

**[요청]**

URI 정보

| 메서드 | URI                                       |
| ------ | ----------------------------------------- |
| POST   | /headquarter/v2.0/appkeys/{{appKey}}/zone |

**[응답]**

응답 본문

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

### 2. 조회

**[요청]**

URI 정보

| 메서드 | URI                                       |
| ------ | ----------------------------------------- |
| GET    | /headquarter/v2.0/appkeys/{{appKey}}/zone |

header 정보

| 이름      | 설명                  |
| --------- | --------------------- |
| X-NHN-uid | 콘솔에서 발급받은 UID |

**[응답]**

응답 본문

```
{
    "zone": "api-7ab1617e2df0f1d1"
}
```

### 3. 삭제

**[요청]**

URI 정보

| 메서드 | URI                                       |
| ------ | ----------------------------------------- |
| DELETE | /headquarter/v2.0/appkeys/{{appKey}}/zone |

**[응답]**

응답 본문

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

## 서비스

### 1. 생성

**[요청]**

URI 정보

| 메서드 | URI                                                     |
| ------ | ------------------------------------------------------- |
| POST   | /admin/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}} |

header 정보

| 이름      | 설명                  |
| --------- | --------------------- |
| X-NHN-uid | 콘솔에서 발급받은 UID |

BODY 정보

```
{
    "analysis": {
        "analyzer": {
            "default_analyzer": {
                "tokenizer": "default_tokenizer"
            },
            "atomic_analyzer": {
                "tokenizer": "atomic_tokenizer"
            },
            "bigram_analyzer": {
                "tokenizer": "bigram_tokenizer"
            }
        },
        "tokenizer": {
            "default_tokenizer": {
                "type": "linguist2_tokenizer",
                "method": "sgmt",
                "hanaterm_options": "seq_locinputenc=utf8outputenc=utf8+korea+japan+josacat+eomicat"
            },
            "atomic_tokenizer": {
                "type": "linguist2_tokenizer",
                "method": "atomic",
                "hanaterm_options": "seq_locinputenc=utf8outputenc=utf8"
            },
            "bigram_tokenizer": {
                "type": "linguist2_tokenizer",
                "method": "bigram",
                "hanaterm_options": "seq_locinputenc=utf8outputenc=utf8"
            }
        }
    },
    "store": {
        "stats_refresh_interval": "-1"
    },
    "number_of_shards": 3,
    "number_of_replicas": 1,
    "similarity": {
        "tcsbm25": {
            "type": "similarity-tcsbm25",
            "a": 0.25,
            "b": 1.2,
            "c": 0
        }
    }
}
```

**[응답]**

응답 본문

```
{}
```

### 2. 조회

**[요청]**

URI 정보

| 메서드 | URI                                       |
| ------ | ----------------------------------------- |
| GET    | /admin/v2.0/appkeys/{{appKey}}/serviceids |

header 정보

| 이름      | 설명                  |
| --------- | --------------------- |
| X-NHN-uid | 콘솔에서 발급받은 UID |

**[응답]**

응답 본문

```
[ ]
```

### 3. 삭제

**[요청]**

URI 정보

| 메서드 | URI                                                     |
| ------ | ------------------------------------------------------- |
| DELETE | /admin/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}} |

header 정보

| 이름      | 설명                  |
| --------- | --------------------- |
| X-NHN-uid | 콘솔에서 발급받은 UID |

**[응답]**

응답 본문

```
{}
```

## 필드

### 1. 생성

**[요청]**

URI 정보

| 메서드 | URI                                                           |
| ------ | ------------------------------------------------------------- |
| POST   | /admin/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/field |

header 정보

| 이름      | 설명                  |
| --------- | --------------------- |
| X-NHN-uid | 콘솔에서 발급받은 UID |

BODY 정보 (예시)

```
{
    "title":{
        "name":"title",
        "type":"text",
        "index":true,
        "analyzer":"default_analyzer",
        "search_analyzer":"default_analyzer",
        "mandatory_filter":false
    },
    "compound_sort_info":{
        "type":"compound_sort"
    }
}
```

**[응답]**

응답 본문

```
{}
```

### 2. 조회

**[요청]**

URI 정보

| 메서드 | URI                                                           |
| ------ | ------------------------------------------------------------- |
| GET    | /admin/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/field |

header 정보

| 이름      | 설명                  |
| --------- | --------------------- |
| X-NHN-uid | 콘솔에서 발급받은 UID |

**[응답]**

응답 본문 (예시)

```
{
    "new": {
        "title": {
            "type": "text",
            "useIndex": true,
            "analyzer": "default_analyzer",
            "search_analyzer": "default_analyzer",
            "useFilter": false,
            "useSort": false,
            "useMultiple": false,
            "useGroup": false,
            "similarity": "tcsbm25",
            "term_vector": "with_positions_offsets",
            "mandatory_filter": false
        },
        "compound_sort_info": {
            "type": "compound_sort",
            "mandatory_filter": false
        },
        "_UPDATE_TIME": {
            "index": true,
            "type": "long",
            "mandatory_filter": false
        },
        "_WEIGHT": {
            "index": true,
            "type": "float",
            "mandatory_filter": false
        },
        "_RANKING": {
            "index": true,
            "type": "integer",
            "mandatory_filter": false
        }
    },
    "current": {
        "title": {
            "type": "text",
            "useIndex": true,
            "analyzer": "default_analyzer",
            "search_analyzer": "default_analyzer",
            "useFilter": false,
            "useSort": false,
            "useMultiple": false,
            "useGroup": false,
            "similarity": "tcsbm25",
            "term_vector": "with_positions_offsets",
            "mandatory_filter": false,
            "index": true
        }
    }
}
```

## 전체 색인

### 1. 시작

**[요청]**

URI 정보

| 메서드 | URI                                                                            |
| ------ | ------------------------------------------------------------------------------ |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing/full/begin |

**[응답]**

응답 본문

```
{}
```

### 2. 색인

**[요청]**

URI 정보

| 메서드 | URI                                                                      |
| ------ | ------------------------------------------------------------------------ |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing/full |

BODY 정보 (예시)

```
[
    {
        "action": "add",
        "id": "id-1",
        "fields": {
            "title": "대박!! 1등이다!!"
        }
    }
]
```

**[응답]**

응답 본문

```
{
    "id": 1
}
```

### 3. 끝

**[요청]**

URI 정보

| 메서드 | URI                                                                          |
| ------ | ---------------------------------------------------------------------------- |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing/full/end |

**[응답]**

응답 본문

```
{}
```

### 4. 취소

**[요청]**

URI 정보

| 메서드 | URI                                                                             |
| ------ | ------------------------------------------------------------------------------- |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing/full/cancel |

**[응답]**

응답 본문

```
{}
```

## 색인 로그

### 1. 색인 로그 조회

**[요청]**

URI 정보

| 메서드 | URI                                                                          |
| ------ | ---------------------------------------------------------------------------- |
| GET    | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing_log?id=1 |

파라미터 정보

| 이름 | 설명    |
| ---- | ------- |
| id   | 색인 ID |

**[응답]**

응답 본문 (예시)

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

### 2. 색인 로그 리스트 조회

**[요청]**

URI 정보

| 메서드 | URI                                                                                        |
| ------ | ------------------------------------------------------------------------------------------ |
| GET    | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing_log/list?from=0&size=1 |

파라미터 정보

| 이름 | 설명        |
| ---- | ----------- |
| from | 어디서 부터 |
| size | list의 크기 |

**[응답]**

응답 본문 (예시)

```
{
    "took": 7,
    "time_out": true,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": 1,
        "max_score": 1.0,
        "hits": [
            {
                "_index": "indexing_log",
                "_type": "indexing_log",
                "_id": "O4XBItjxwTLNvcie^sangho-test-1",
                "_score": 1.0,
                "_source": {
                    "alias_name": "O4XBItjxwTLNvcie^sangho-test",
                    "id": 1,
                    "file_name": "payload-1.json",
                    "file_size": 355,
                    "request_time": 1706591521000,
                    "status": 4,
                    "total_doc_count": 3,
                    "total_index_file_size": 209689
                }
            }
        ]
    }
}
```

## 추가 색인

### 1. 추가 색인

**[요청]**

URI 정보

| 메서드 | URI                                                                 |
| ------ | ------------------------------------------------------------------- |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing |

BODY 정보 (예시)

```
[
    {
        "action": "add",
        "id": "id-2",
        "fields": {
            "title": "대박!! 2등이다!!"
        }
    }
]
```

**[응답]**

응답 본문

```
{
    "id": 2
}
```

## 재색인

### 1. 재색인

**[요청]**

URI 정보

| 메서드 | URI                                                                   |
| ------ | --------------------------------------------------------------------- |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/reindexing |

**[응답]**

응답 본문

```
{}
```

### 2. 재색인 조회

**[요청]**

URI 정보

| 메서드 | URI                                                                   |
| ------ | --------------------------------------------------------------------- |
| GET    | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/reindexing |

**[응답]**

응답 본문

```
{
    "running": 0,
    "necessary": 0
}
```

## 검색

### 1. 검색

**[요청]**

URI 정보

| 메서드 | URI                                                                                                                            |
| ------ | ------------------------------------------------------------------------------------------------------------------------------ |
| GET    | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/search?q=&q_option=and,title\*1.0&start=1&size=10&passage.title=180 |

파라미터 정보

| 이름             | 설명                                    |
| ---------------- | --------------------------------------- |
| start            | 시작 번호 (필수)                        |
| size             | 크기 (필수)                             |
| q_option         | and, or, boolean, 필드 \* 가중치 (필수) |
| return           | 결과 출력                               |
| q                | 쿼리                                    |
| sort             | 정렬                                    |
| passage.\*       | 결과 길이                               |
| summary.\*       | 요약                                    |
| filter_and       | 필터 And                                |
| filter_or        | 필터 Or                                 |
| highlight        | 하이라이트                              |
| doc_weight_ratio | 가중치                                  |

**[응답]**

응답 본문

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
                        "_RELEVANCE": 100,
                        "title": "대박!! 1등이다!!"
                    },
                    {
                        "_ID": "id-2",
                        "_RANK": "0",
                        "_RELEVANCE": 100,
                        "title": "대박!! 2등이다!!"
                    }
                ]
            },
            "status": {
                "code": 200,
                "message": "OK"
            },
            "itemCount": 10
        },
        "meta": {
            "timezone": "+09:00"
        }
    }
}
```

## 동의어 사전

### 1. 생성

**[요청]**

URI 정보

| 메서드 | URI                                                                                      |
| ------ | ---------------------------------------------------------------------------------------- |
| POST   | /dictionary/v2.0/appkeys/{{appkey}}/serviceids/{{serviceids}}/dictionary/thesaurus?way=1 |

파라미터 정보

| 이름 | 설명                         |
| ---- | ---------------------------- |
| way  | 1: 단방향(기본값), 2: 양방향 |

BODY 정보

```
신발,운동화,스포츠화
```

**[응답]**

응답 본문

```
{
    "statusCode": 1
}
```

### 2. 삭제

**[요청]**

URI 정보

| 메서드 | URI                                                                               |
| ------ | --------------------------------------------------------------------------------- |
| DELETE | /dictionary/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/dictionary/thesaurus |

**[응답]**

응답 본문

```
{
    "statusCode": 1
}
```

### 3. 리셋

**[요청]**

URI 정보

| 메서드 | URI                                                                                     |
| ------ | --------------------------------------------------------------------------------------- |
| POST   | /dictionary/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/dictionary/thesaurus/reset |

**[응답]**

응답 본문

```
{
    "statusCode": 1
}
```

## 불용어 사전

### 1. 생성

**[요청]**

URI 정보

| 메서드 | URI                                                                                |
| ------ | ---------------------------------------------------------------------------------- |
| POST   | /dictionary/v2.0/appkeys/{{appkey}}/serviceids/{{serviceids}}/dictionary/stopwords |

BODY 정보

```
커피
콜드브루
```

**[응답]**

응답 본문

```
{
    "statusCode": 1
}
```

### 2. 삭제

**[요청]**

URI 정보

| 메서드 | URI                                                                               |
| ------ | --------------------------------------------------------------------------------- |
| DELETE | /dictionary/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/dictionary/stopwords |

**[응답]**

응답 본문

```
{
    "statusCode": 1
}
```

### 3. 리셋

**[요청]**

URI 정보

| 메서드 | URI                                                                                     |
| ------ | --------------------------------------------------------------------------------------- |
| POST   | /dictionary/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/dictionary/stopwords/reset |

**[응답]**

응답 본문

```
{
    "statusCode": 1
}
```

## 통계

### 1. stat 조회

**[요청]**

URI 정보

| 메서드 | URI                                                                                                  |
| ------ | ---------------------------------------------------------------------------------------------------- |
| GET    | /stats/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/stats?kind=total_query_count&date=2024-01-29 |

파라미터 정보

<table>
    <tr>
        <th>이름</th>
        <th>설명</th>
    </tr>
    <tr>
         <td rowspan="4">kind</td>
        <td>total_query_count - 전체 쿼리 수</td>
    </tr>
    <tr>
        <td>no_result_query_count - 결과 없는 쿼리 수</td>
    </tr>
    <tr>
        <td>total_doc_count - 전체 문서 수</td>
    </tr>
    <tr>
        <td>total_index_size - 전체 색인 크기</td>
    </tr>
    <tr>
        <td>date</td>
        <td>날짜</td>
    </tr>
</table>

**[응답]**

응답 본문 (예시)

```
[]
```

### 2. admin 조회

**[요청]**

URI 정보

| 메서드 | URI                                                                                                                                           |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------- |
| GET    | /admin/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/stats?kind=total_query_count&resolution=day&start_date=2024-01-29&end_date=2024-01-29 |

파라미터 정보

<table>
    <tr>
        <th>이름</th>
        <th>설명</th>
    </tr>
    <tr>
        <td rowspan="4">kind</td>
        <td>total_query_count - 전체 쿼리 수</td>
    </tr>
    <tr>
        <td>no_result_query_count - 결과 없는 쿼리 수</td>
    </tr>
    <tr>
        <td>total_doc_count - 전체 문서 수</td>
    </tr>
    <tr>
        <td>total_index_size - 전체 색인 크기</td>
    </tr>
    <tr>
        <td>start_date</td>
        <td>시작 날짜</td>
    </tr>
    <tr>
        <td>end_date</td>
        <td>끝 날짜</td>
    </tr>
    <tr>
        <td>resolution</td>
        <td>month, day 구분</td>
    </tr>
</table>

**[응답]**

응답 본문 (예시)

```
[
    [
        "2024-01-29",
        6
    ]
]
```

## ACL

### 1. 조회

**[요청]**

URI 정보

| 메서드 | URI                                                         |
| ------ | ----------------------------------------------------------- |
| GET    | /admin/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/acl |

**[응답]**

응답 본문

```
{
    "version": "0.0.1",
    "indexing": {
        "order": [
            "allow",
            "deny"
        ],
        "allow": "all"
    },
    "search": {
        "order": [
            "allow",
            "deny"
        ],
        "allow": "all"
    },
    "admin": {
        "order": [
            "allow",
            "deny"
        ],
        "allow": "all"
    },
    "log": {
        "order": [
            "allow",
            "deny"
        ],
        "allow": "all"
    }
}
```

### 2. 삽입

**[요청]**

URI 정보

| 메서드 | URI                                                         |
| ------ | ----------------------------------------------------------- |
| PUT    | /admin/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/acl |

BODY 정보

```
{
    "indexing": {
        "order": [
            "allow",
            "deny"
        ],
        "allow": "all",
        "deny" : ["127.0.0.1"]
    },
    "search": {
        "order": [
            "allow",
            "deny"
        ],
        "allow": "all"
    },
    "admin": {
        "order": [
            "allow",
            "deny"
        ],
        "allow": "all"
    },
    "log": {
        "order": [
            "allow",
            "deny"
        ],
        "allow": "all"
    }
}
```

**[응답]**

응답 본문

```
{}
```
