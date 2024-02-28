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

## 전체 색인

전체 색인은 전체를 색인함으로 기존에 색인 했던 파일은 사라집니다.

반드시 시작 - 색인 - 끝으로 해야 합니다.

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

## 추가 색인

추가 색인은 id 가 기존에 있던 것은 업데이트 되고 없던 것은 새로 추가 됩니다.

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

## 색인 로그

색인 후에 결과가 어떻게 나왔는지 보여줍니다.

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

## 검색

검색은 색인을 통해서 필드를 검색할 수 있습니다.

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

## 통계

통계는 일별로 보여줍니다.

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
