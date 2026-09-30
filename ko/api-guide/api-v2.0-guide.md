<!-- pre-align:aligned sig=4d379b3fcba7 -->

<a id="search-cloud-search-api-v20-guide"></a>
## Search > Cloud Search > API v2.0 가이드 { #search-cloud-search-api-v20-guide }

Cloud Search에서 제공하는 Cloud Search API v2.0을 설명합니다.

<a id="common"></a>
## 공통 { #common }

<a id="api-endpoint"></a>
### API 엔드포인트 { #api-endpoint }

<a id="api-endpoint-uri-information"></a>
#### URI 정보

| 환경 | URI                                        |
| ---- | ------------------------------------------ |
| REAL | https://kr1-search.api.nhncloudservice.com |

<a id="api-endpoint-path-parameter-information"></a>
#### Path 파라미터 정보

| 이름      | 설명                    |
| --------- | ----------------------- |
| appKey    | 콘솔에서 발급 받은 앱키 |
| serviceId | 사용자의 임의의 이름    |

<a id="authentication-and-authorization"></a>
### 인증 및 권한 { #authentication-and-authorization }

Cloud Search API를 사용하려면 Appkey가 필요합니다. Appkey는 API 호출 시 요청 URL에 포함하여 특정 리소스를 가리키고 식별하는 데 사용됩니다.
Appkey 확인 및 사용에 대한 자세한 내용은 [Appkey](/nhncloud/ko/public-api/appkey)를 참고하세요.

<a id="full-indexing"></a>
## 전체 색인 { #full-indexing }

전체 색인을 실행하면 기존에 색인했던 파일은 사라집니다.

반드시 시작-색인-끝의 순서로 진행해야 합니다.

<a id="start"></a>
### 1. 시작 { #start }

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

<a id="indexing"></a>
### 2. 색인 { #indexing }

**[요청]**

URI 정보

| 메서드 | URI                                                                      |
| ------ | ------------------------------------------------------------------------ |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing/full |

BODY 정보(예시)

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

응답 본문(예시)

```
{
    "id": 1
}
```

<a id="end"></a>
### 3. 끝 { #end }

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

<a id="cancel"></a>
### 4. 취소 { #cancel }

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

<a id="additional-indexing"></a>
## 추가 색인 { #additional-indexing }

색인은 기존 ID가 있을 경우 업데이트되며, ID가 없는 경우에 추가됩니다.

<a id="additional-indexing-2"></a>
### 1. 추가 색인 { #additional-indexing-2 }

**[요청]**

URI 정보

| 메서드 | URI                                                                 |
| ------ | ------------------------------------------------------------------- |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing |

BODY 정보(예시)

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

응답 본문(예시)

```
{
    "id": 2
}
```

<a id="index-log"></a>
## 색인 로그 { #index-log }

색인 결과를 표시합니다.

<a id="view-the-index-log"></a>
### 1. 색인 로그 조회 { #view-the-index-log }

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

응답 본문(예시)

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

<a id="search"></a>
## 검색 { #search }

색인을 이용해 필드를 검색할 수 있습니다.

<a id="search-2"></a>
### 1. 검색 { #search-2 }

**[요청]**

URI 정보(예시)

| 메서드 | URI                                                                                                                            |
| ------ | ------------------------------------------------------------------------------------------------------------------------------ |
| GET    | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/search?q=&q_option=and,title\*1.0&start=1&size=10&passage.title=180 |

파라미터 정보

| 이름             | 설명                                    |
| ---------------- | --------------------------------------- |
| start            | 시작 번호(필수)                        |
| size             | 크기(필수)                             |
| q_option         | and, or, boolean, 필드 \* 가중치(필수) |
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

응답 본문(예시)

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
            "itemCount": 2
        },
        "meta": {
            "timezone": "+09:00"
        }
    }
}
```

<a id="statistics"></a>
## 통계 { #statistics }

통계는 전체 쿼리와 결과 없는 쿼리의 수를 날짜(일)별로 표시합니다.

<a id="view-stat"></a>
### 1. stat 조회 { #view-stat }

**[요청]**

URI 정보(예시)

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
        <td rowspan="2">kind</td>
        <td>total_query_count - 전체 쿼리 수</td>
    </tr>
    <tr>
        <td>no_result_query_count - 결과 없는 쿼리 수</td>
    </tr>
    <tr>
        <td>date</td>
        <td>날짜</td>
    </tr>
</table>

**[응답]**

응답 본문(예시)

```
[["", 13]]
```
