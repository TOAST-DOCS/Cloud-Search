## Search > Cloud Search > 콘솔 사용 가이드

## 알아두기

- 문서 내의 앱키 'CwSx6kv99g0QuNtM'는 사용자별로 다릅니다.

## 시작하기

먼저 Cloud Search 서비스를 활성화합니다.

1. **NHN Cloud Console**에서 **서비스 선택**을 클릭합니다.

2. **Cloud Search**를 클릭합니다.

![img](http://static.toastoven.net/prod_search/product-use-02-ko-20210506.jpg)<br>

서비스가 활성화되었는지 확인하는 방법은 다음과 같습니다.

1. **NHN Cloud Console** 왼쪽 메뉴에서 **Search**를 클릭합니다.

2. **Cloud Search**가 보이면 서비스가 활성화된 것입니다.

![img](http://static.toastoven.net/prod_search/product-use-03-ko-20210506.jpg)

## 기본 사용법

### 1. 서비스 생성

서비스를 생성하는 방법은 다음과 같습니다.

1. **서비스 생성** 버튼을 클릭합니다.

2. **서비스 생성** 창에서 서비스 ID를 입력합니다.

    - 영어 소문자, 숫자 및 \_(밑줄)와 -(하이픈)만 사용할 수 있습니다.
    - 숫자, \_(밑줄), -(하이픈)로 시작할 수 없습니다.
    - 최소 두 글자 이상 가능합니다.

3. **저장** 버튼을 클릭합니다.

![img](http://static.toastoven.net/prod_search/domain_create_prodedure-ko-20210506.jpg)<br>

생성된 서비스 결과를 확인합니다.

1. 생성된 서비스 ID(test)를 클릭합니다.

![img](http://static.toastoven.net/prod_search/domain_create_result-ko-20210506.jpg)

### 2. 필드 설정

필드를 추가하는 방법은 다음과 같습니다.

1. **필드 설정** 탭을 클릭합니다.

2. **필드 추가** 버튼을 클릭합니다.

3. 필드 이름을 입력합니다.

	- 영어 대소문자, 숫자 및 \_(밑줄)와 -(하이픈)만 사용할 수 있습니다.
	- 숫자, \_(밑줄), -(하이픈)로 시작할 수 없습니다.
	- 최소 두 글자 이상 가능합니다.

4. 다중 값 사용 여부를 체크합니다.

	- 필드 값의 구분자는 ,(쉼표)만 사용 가능하며 최대 30개까지 사용할 수 있습니다.

5. 색인 사용 여부를 체크합니다.

6. 필터 사용 여부를 체크합니다.

7. 정렬 사용 여부를 체크합니다.

8. 요약 사용 여부를 체크합니다.

9. **저장** 버튼을 클릭합니다.

![img](http://static.toastoven.net/prod_search/field_create_procedure-ko-20230831.jpg)

### 3. 색인

색인할 파일을 생성하고 색인하는 방법은 다음과 같습니다.

**색인 파일 생성**

- 아래 예제와 같은 형식으로 색인 요청 파일을 생성합니다.
- 색인할 파일은 UTF-8로 생성해야 합니다.
    - Windows 메모장에서 파일 저장 시 인코딩을 UTF-8로 지정해서 저장합니다.
- 예제에서는 data/documents.json 이름으로 생성했습니다.

```
[
  {
    "action": "add",
    "id": "id-1",
    "fields": {
      "title": "[무료배송]나이키 슈즈 195종!!",
      "body": "명불허전 나이키 인기슈즈 괜히 잘 팔리는게 아니죠~~ 나이키 핫!슈즈 195종★ 하나쯤은 있어야 하지 않아??"
    }
  },
  {
    "action": "add",
    "id": "id-2",
    "fields": {
      "title": "[슈퍼특가]나이키 운동화 109종",
      "body": "단 7일만 이가격!  [슈퍼특가] 아디다스 슈즈 109종 모음전 망설이면 품~절~"
    }
  },
  {
    "action": "add",
    "id": "id-3",
    "fields": {
      "title": "[아디다스]신상운동화/슬리퍼 114종",
      "body": "[아디다스슈즈모음♥] 무/료/배/송 [아디다스]신상슬리퍼 /슈퍼스타 스탠스미스 /튜블라외 114종 득템기회!"
    }
  }
]
```

- 파일 설명
	- action
		- add: 해당 문서가 추가됩니다.
			- 기존에 동일한 id가 존재하면 업데이트 됩니다.
		- delete: 해당 문서가 삭제됩니다.
	- id
		- 문서의 고유한 id입니다.
		- id의 타입은 문자열입니다.
	- 최대 파일 사이즈는 8MB입니다.
		- 8MB 이상의 데이터는 여러 개로 나누어서 색인해야 합니다.

**색인 방법**

1. **색인** 탭을 클릭합니다.

2. **파일 선택** 버튼을 클릭합니다.

3. 색인할 파일을 선택합니다.

4. **열기** 버튼을 클릭합니다.

5. 색인 명령어가 REST API로 출력됩니다.

	- REST API를 이용하여 검색 서비스를 개발할 수 있습니다.

6. **색인** 버튼을 클릭합니다.

7. 색인 결과를 확인합니다.

![img](http://static.toastoven.net/prod_search/indexing_procedure_01-ko-20230831.jpg)
![img](http://static.toastoven.net/prod_search/indexing_procedure_02-ko-20230831.jpg)<br>

**REST API**

아래와 같이 REST API를 사용 가능합니다.

- 색인 API
    - Request
        - 파일 업로드 방식
          ```
          curl -XPOST 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing' -H 'Accept-Language:ko' -H 'Content-Type:multipart/form-data; charset=UTF-8' -F 'file=@documents.json'
          ```
        - 페이로드(payload) 방식
          ```
          curl -XPOST 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing' -H 'Accept-Language:ko' -H 'Content-Type:application/json; charset=UTF-8' -d '
          [
            {
              "action": "add",
              "id": "id-1",
              "fields": {
              "title": "[무료배송]나이키 슈즈 195종!!",
              "body": "명불허전 나이키 인기슈즈 괜히 잘 팔리는게 아니죠~~ 나이키 핫!슈즈 195종★ 하나쯤은 있어야 하지 않아??"
              }
            },
            {
              "action": "add",
              "id": "id-2",
              "fields": {
              "title": "[슈퍼특가]나이키 운동화 109종",
              "body": "단 7일만 이가격!  [슈퍼특가] 아디다스 슈즈 109종 모음전 망설이면 품~절~"
              }
            }
          ]'
          ```
	- Response
		```
		{
		  "id": 1
		}
		```
- 색인 결과 확인 API
	- Request
		```
		curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing_log?id=1' -H 'Accept-Language:ko'
		```
		- id 1은 위의 색인 API Response의 id입니다.
	- Response
		```
		{
		  "request_time": "2017-10-23T12:36:43",
		  "file_name": "documents.json",
		  "file_size": 1185,
		  "status": 4
		}
		```
    - status
		- 1: 대기 중
		- 2: 무시됨(필드 설정 변경 이전의 색인 요청은 무시됨)
		- 3: 진행 중
		- 4: 성공
		- 5: 실패
		- 6: 취소

### 4. 검색

검색 방법은 다음과 같습니다.

1. **검색** 탭을 클릭합니다.

2. 검색할 필드명을 체크합니다.

3. 검색할 필드별 가중치를 설정합니다.

    - 0.0~1.0 값을 설정합니다.

4. 정렬할 필드를 선택합니다.

    - 다중 정렬할 경우 다중 정렬 필드를 선택합니다.
    - 정렬 방식을 지정합니다.

5. 검색 결과에 출력할 필드를 체크합니다.

6. 검색 결과 길이를 설정합니다.

7. 강조(highlight) pre 태그를 설정합니다.

8. 강조(highlight) post 태그를 설정합니다.

9. 검색 결과에서 출력할 시작 순위를 지정합니다.

    - '1'로 설정하면 1등부터 출력되고, '10'으로 설정하면 10등부터 출력됩니다.

10. 검색 결과 개수를 지정합니다.

    - '5'로 설정하면 5개 출력되고, '10'으로 설정하면 10개 출력됩니다.

11. 검색 연산자를 선택합니다.

12. 검색할 단어를 입력합니다.

13. 검색 아이콘을 클릭합니다.

14. 2~11번까지 설정한 내용이 REST API로 출력됩니다.

    - REST API를 이용하여 검색 서비스를 개발할 수 있습니다.

15. 검색 결과가 출력됩니다.

![img](http://static.toastoven.net/prod_search/basic-search-ko-20230831.jpg)<br>

**REST API**

아래와 같이 REST API를 사용할 수 있습니다.

- Request
	```
	curl -G -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,body*1.0,title*1.0&return=&passage.body=180&passage.title=180' -H 'Accept-Language:ko' --data-urlencode q='나이키 운동화' --data-urlencode highlight='<b>,</b>' -H 'Accept-Language:ko'
	```
- Response
    ```
    {
      "message": {
        "meta": {
          "timezone": "+09:00"
        },
        "result": {
          "status": {
          "code": 200,
          "message": "OK"
        },
        "query": "나이키 운동화",
        "start": 1,
        "itemCount": 1,
        "total": 1,
        "itemList": {
          "item": [
            {
              "_RELEVANCE": 100,
              "_RANK": 1,
              "_ID": "id-2",
              "body": "단 7일만 이가격!  [슈퍼특가] 아디다스 슈즈 109종 모음전 망설이품~절~",
              "title": "[슈퍼특가]<b>나이키</b> <b>운동화</b> 109종"
            }
          ]
        }
      }
    }
    ```

### 5. 통계

통계를 확인하는 방법은 다음과 같습니다.

1. **통계** 탭을 클릭합니다.

2. **전체 쿼리수** 또는 **결과 없는 쿼리수**를 선택합니다.

3. 시작 날짜를 입력합니다.

4. 종료 날짜를 입력합니다.

5. **조회** 버튼을 클릭하면 통계 그래프가 출력됩니다.

6. **데이터 다운로드**를 클릭하면 쿼리별 통계 데이터가 다운로드됩니다.

7. **전체 문서수** 또는 **전체 색인 사이즈**를 선택합니다.

8. 시작 날짜를 입력합니다.

9. 종료 날짜를 입력합니다.

10. **조회** 버튼을 클릭하면 통계 그래프가 출력됩니다.

![img](http://static.toastoven.net/prod_search/stats-ko-20200304.jpg)<br>

**REST API**

- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/stats/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/stats?kind=total_query_count&date=2020-03-09' -H 'Accept-Language:ko'
	```
    - kind
        - total_query_count: 전체 쿼리수
        - no_result_query_count: 검색 결과 없는 쿼리수
    - date: 조회할 날짜
- Response
	```
	[ [ "나이키", 8 ], [ "아디다스", 4 ] ]
	```
    - 쿼리수 3 이상만 조회됩니다.

### 6. ACL

색인 및 검색 REST API를 호출할 수 있는 장비의 IP를 제한할 수 있습니다.

- 다른 사람이 데이터를 삭제할 수 있으므로 색인 ACL은 반드시 설정해 주세요.
- 콘솔에서 테스트하는 경우 ACL 설정과 관련 없습니다.

**ACL 설정 방법**

아래는 IP 주소가 202.179.177.21인 경우에만 색인이 가능하고 검색 요청은 모든 IP에서 가능하도록 설정한 예입니다. 쿼리 통계 데이터 다운로드 요청은 모든 IP에서 가능하도록 설정한 예제입니다.

1. **ACL** 탭을 클릭합니다.

2. **색인** 아래 **허용**에 IP 주소를 입력합니다.

3. **통계** **허용**에 'all'을 입력합니다.

4. **검색** **허용**에 'all'을 입력합니다.

5. **저장**버튼을 클릭합니다.

![img](http://static.toastoven.net/prod_search/acl_procedure-ko-20200304.jpg)

## 기능 상세 설명

### 필드 삭제

필드를 삭제하는 방법은 다음과 같습니다.

1. 삭제할 필드의 **삭제** 버튼을 클릭합니다.

    - 다중 정렬 필드로 사용되는 필드는 삭제가 안 됩니다. 다중 정렬 필드 삭제 후 진행합니다.

2. **저장** 버튼을 클릭합니다.

3. **지금 재색인** 버튼을 클릭합니다.

    - 재색인 중에는 문서 추가나 수정, 삭제가 안 됩니다.

![img](http://static.toastoven.net/prod_search/field_delete-1-ko-20230831.jpg)
![img](http://static.toastoven.net/prod_search/field_delete-2-ko-20230831.jpg)
![img](http://static.toastoven.net/prod_search/field_delete-3-ko-20230831.jpg)

### 필드 수정

필드 수정은 지원하지 않습니다. 삭제 후 다시 추가해야 합니다.

### 필터링

**필드 설정**

1. 대상 필드의 필터 사용 여부를 체크합니다.
2. 'text' 타입의 경우 필터 기능을 지원하지 않습니다.

![img](http://static.toastoven.net/prod_search/filtering-field-ko-20230831.jpg)

- 필터가 체크된 필드만 기능을 사용할 수 있습니다.

**색인**

테스트를 위해 아래 데이터를 색인합니다.

```
[
  {
    "action": "add",
    "id": "id-1",
    "fields": {
      "name": "나이키 에어맥스",
      "category": 1
    }
  },
  {
    "action": "add",
    "id": "id-2",
    "fields": {
      "name": "나이키 샤이엔 솔리드",
      "category": 2
    }
  }
]
```

**검색**

1. 필터링 값을 입력합니다.

![img](http://static.toastoven.net/prod_search/filtering-search-ko-20230831.jpg)

필터링 값 입력 방법입니다.

1. filter_and: 단일값 필터링, 필터 필드 간 and 연산 필요시 사용합니다.
2. filter_or: 필터 필드 간 or 연산 필요시 사용합니다.
    - 범위 지정, 위경도 필터링에 사용할 수 없습니다.

- 단일값 필터링
    - 예제) filter_and='category=1'
        - category == 1
- or 필터링
    - 예제) filter_and='category=1|2'
        - category == 1 or category == 2
- and 필터링
    - 예제) filter_and='category=1&2'
        - category == 1 and category == 2
- 범위 지정 필터링
    - 예제) filter_and='category=[1,2]'
        - 1 <= category <= 2
    - 예제) filter_and='category={1,2]'
        - 1 < category <= 2
    - 예제) filter_and='category={,2]'
        - category <= 2
    - keyword, boolean, geo_point 타입은 범위 지정 필터링에 사용할 수 없습니다.
- not 필터링
    - 예제) filter_and='category=!1'
        - category != 1
- date 타입 필터링
    - filter_or='update=[2017-03-22T08:28:44,}'
        - 2017-03-22T08:28:44 <= update
    - filter_or='update=[,2018-10-02T15:26:28}'
        - update < 2018-10-02T15:26:28
    - filter_or='update=[2017-03-22T08:28:44,2018-10-02T15:26:28}'
        - 2017-03-22T08:28:44 <= update < 2018-10-02T15:26:28
- keyword 타입 필터링
    - filter_and='dealer="DNC샵"|"위드쇼핑"'
        - keyword 타입은 큰따옴표 사용을 추천합니다.
- 여러 개의 필드 필터링
    - filter_and='category=1&brand=2'
        - category == 1 and brand == 2
    - filter_or='category=1|brand=2'
        - category == 1 or brand == 2
    - filter_or='(category=1&brand=2)|(category=3&brand=4)'
        - (category == 1 and brand == 2) or (category == 3 and brand == 4)

### 위경도(geolocation) 필터링

**필드 설정**

1. 위경도를 입력할 필드 타입으로 'geo_point'를 선택합니다.

![img](http://static.toastoven.net/prod_search/geolocation-field-ko-20230831.jpg)

**색인**

테스트를 위해 아래 데이터를 색인합니다.

```
[
  {
    "action": "add",
    "id": "id-1",
    "fields": {
      "name": "에프엑스수학학원",
      "location": [10.1, 10.1]
    }
  },
  {
    "action": "add",
    "id": "id-2",
    "fields": {
      "name": "좋은나무 사고력수학학원",
      "location": [10.3, 10.4]
    }
  },
  {
    "action": "add",
    "id": "id-3",
    "fields": {
      "name": "수학의아침학원",
      "location": [10.4, 10.3]
    }
  }
]
```

- geo_point 타입에는 [{경도}, {위도}] 형식으로 값을 입력합니다.

**검색**

- 반경(circle) 필터링
1. 필터링 값을 입력합니다.
	- 형식: [{경도},{위도}],{반경}
	- 예제: [10.3,10.3],15km
		- 경도 10.3, 위도 10.3 중심으로 반경 15km 이내인 문서만 검색됩니다.
		- 반경 단위는 'km', 'm', 'cm'를 사용할 수 있습니다.

![img](http://static.toastoven.net/prod_search/geolocation-search-circle-ko-20230831.jpg)

- 영역(polygon) 필터링
1. 필터링 값을 입력합니다.
	- 형식: [{경도 1},{위도 1}],[{경도 2},{위도 2}],[{경도 N},{위도 N}]
	- 예제: [10.2,10.2],[10.3,10.5],[10.5,10.2]
	- 각 점들은 시계 방향으로 연결됩니다.
	- 연결된 다각형 내의 문서만 검색됩니다.

![img](http://static.toastoven.net/prod_search/geolocation-search-polygon-ko-20230831.jpg)

### 정렬

**필드 설정**

1. 대상 필드의 정렬 사용 여부를 체크합니다.
2. 'text' 타입의 경우 정렬 기능을 지원하지 않습니다.
3. 다중 값을 사용할 경우 정렬 기능을 지원하지 않습니다.

![img](http://static.toastoven.net/prod_search/sorting-field-01-ko-20230831.jpg)

- 정렬이 체크된 필드만 기능을 사용할 수 있습니다.

**다중 정렬 설정**

1. 필드명을 입력합니다.
2. 대상 필드를 추가 후 선택해 순서를 조정합니다.
    - 정렬이 2개 이상 되면 출력됩니다.
    - 선택 순서대로 정렬합니다.
3. 각 필드의 정렬 방식을 선택합니다.

![img](http://static.toastoven.net/prod_search/sorting-field-02-ko-20230920.jpg)

- 2개 이상 필드의 정렬이 체크된 경우에 기능을 사용할 수 있습니다.

**색인**

테스트를 위해 아래 데이터를 색인합니다.

```
[
  {
    "action": "add",
    "id": "id-1",
    "fields": {
      "name": "나이키 에어맥스",
      "popular": 10,
      "price": 84180
    }
  },
  {
    "action": "add",
    "id": "id-2",
    "fields": {
      "name": "나이키 에어줌",
      "popular": 5,
      "price": 97200
    }
  },
  {
    "action": "add",
    "id": "id-3",
    "fields": {
      "name": "나이키 에어포스",
      "popular": 5,
      "price": 74680
    }
  }
]
```

**검색**

1. 정렬 필드를 선택 후 방식을 지정합니다.

    - "asc": 오름차순 정렬
    - "desc": 내림차순 정렬

2. 다중 정렬 필드를 선택 후 방식을 지정합니다.

    - "asc": 오름차순 정렬
    - "desc": 내림차순 정렬

![img](http://static.toastoven.net/prod_search/sorting-search-01-ko-20230831.jpg)
![img](http://static.toastoven.net/prod_search/sorting-search-02-ko-20230831.jpg)

- 1개의 정렬 필드만 선택 가능합니다.

### 요약

**필드 설정**

1. 대상 필드의 요약 사용 여부를 체크합니다.
2. 'text', 'geo_point' 타입의 경우 요약 기능을 지원하지 않습니다.

![img](http://static.toastoven.net/prod_search/aggregation-field-ko-20230831.jpg)

- 요약이 체크된 필드만 기능을 사용할 수 있습니다.

**색인**

테스트를 위해 아래 데이터를 색인합니다.

```
[
  {
    "action": "add",
    "id": "id-1",
    "fields": {
      "name": "나이키 에어맥스",
      "category": "신발"
    }
  },
  {
    "action": "add",
    "id": "id-2",
    "fields": {
      "name": "나이키 에어줌",
      "category": "신발"
    }
  },
  {
    "action": "add",
    "id": "id-3",
    "fields": {
      "name": "나이키 스우시 반팔티",
      "category": "의류"
    }
  }
]
```

**검색**

1. category 필드의 '요약'을 체크합니다.

![img](http://static.toastoven.net/prod_search/aggregation-search-ko-20230831.jpg)

**요약 결과**

```
"summary": {
  "category": {
    "신발": 2,
    "의류": 1
  }
}
```

- 검색 결과와 함께 요약 정보가 출력됩니다.
- category가 '신발'인 검색 결과가 2건, '의류'인 검색 결과가 1건이라는 의미입니다.
- 요약 가능한 타입
	- 'text' 및 'geo_point' 타입은 요약 기능을 사용할 수 없습니다.

### 불리언 쿼리

**필드 설정**

![img](https://static.toastoven.net/prod_search/boolean_query-field-ko-20230831.jpg)

**색인**

테스트를 위해 아래 데이터를 색인합니다.

```
[
  {
    "action": "add",
    "id": "id-1",
    "fields": {
      "title": "나이키 신발"
    }
  },
  {
    "action": "add",
    "id": "id-2",
    "fields": {
      "title": "나이키 슈즈"
    }
  },
  {
    "action": "add",
    "id": "id-3",
    "fields": {
      "title": "나이키 가방"
    }
  }
]
```

**검색**

1. 'boolean'을 선택합니다.

2. &, |, (, ), ! 을 이용한 불리언 쿼리를 입력합니다.

![img](https://static.toastoven.net/prod_search/boolean_query-search-ko-20230831.jpg)

- 연산자 우선순위
	- (), !, &, | 순입니다.
- 피연산자 처리
	- 피연산자는 Exact matching으로 처리됩니다.
	- q=나이키 신발&q_option=boolean
	- 검색이 되는 검색 대상
		- "인기 나이키 신발 할인"
		- "인기 나이키신발 할인"
	- 검색이 안되는 검색 대상
		- "인기 나이키 할인 신발"
			- "나이키"와 "신발" 사이에 다른 단어를 포함하고 있기 때문임
		- "인기 신발 나이키 할인"
			- "나이키"와 "신발"의 순서가 다르기 때문임

### 필드 가중치 지정

**검색**

- "나이키"로 검색합니다.

![img](http://static.toastoven.net/prod_search/document_boosting-search-01-ko-20230831.jpg)
![img](http://static.toastoven.net/prod_search/document_boosting-search-02-ko-20230831.jpg)

**검색 결과**

```
"itemList": {
  "item": [
    {
      "_RELEVANCE": 200,
      "_RANK": 1,
      "_ID": "id-2",
      "title": "<b>나이키</b>"
      "body": "<b>나이키</b>"
    },
    {
      "_RELEVANCE": 200,
      "_RANK": 2,
      "_ID": "id-1",
      "title": "<b>나이키</b>"
      "body": "<b>나이키</b>"
    }
  ]
}
```

- "title" 필드에 가중치가 높게 부여되어 "id-2" 문서가 검색 결과 상위에 노출됩니다.

**가중치 반영 비율 조정**

- doc_weight_ratio 파라미터를 이용해서 반영 비율을 조정합니다.
	```
	curl -G -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,title*1.0&return=&passage.title=180&doc_weight_ratio=0.1' --data-urlencode q='나이키' --data-urlencode highlight='<b>,</b>' -H 'Accept-Language:ko'
	```
	- 0.0~1.0 사이의 값을 입력할 수 있습니다.
	- default는 1.0입니다.

**Tip**

- 검색 가중치와 문서 랭킹을 조정해서 검색 결과 출력 순서를 커스터마이징할 수 있습니다.

### 문서 랭킹 지정

**필드 설정**

![img](http://static.toastoven.net/prod_search/document_ranking-field-ko-20230831.jpg)

**색인**

테스트를 위해 아래 데이터를 색인합니다.

```
[
  {
    "action": "add",
    "id": "id-1",
    "ranking": 2,
    "fields": {
      "title": "나이키"
    }
  },
  {
    "action": "add",
    "id": "id-2",
    "ranking": 1,
    "fields": {
      "title": "나이키"
    }
  }
]
```

- "id-1"에는 "ranking"을 2, "id-2"에는 "ranking"을 1로 지정합니다.
- "ranking"은 1~10000 사이의 값을 입력할 수 있습니다.

**검색**

- "나이키"로 검색합니다.

![img](http://static.toastoven.net/prod_search/document_ranking-search-ko-20230831.jpg)

**검색 결과**

```
"itemList": {
  "item": [
    {
      "_RELEVANCE": 100,
      "_RANK": 1,
      "_ID": "id-2",
      "title": "<b>나이키</b>"
    },
    {
      "_RELEVANCE": 100,
      "_RANK": 2,
      "_ID": "id-1",
      "title": "<b>나이키</b>"
    }
  ]
}
```

- "ranking"을 1로 지정한 "id-2" 문서가 검색 결과 1등으로 노출됩니다.
- "ranking"을 동일하게 지정한 경우 사용자가 입력한 검색어와 유사도가 높은 문서가 먼저 노출됩니다.

### 필드 설정 다운로드/업로드

**설정 다운로드**

1. "설정 다운로드" 버튼을 클릭해서 현재 설정을 다운로드합니다.

![img](https://static.toastoven.net/prod_search/field-download-ko-20230831.jpg)

**설정 업로드**

1. **설정 업로드** 버튼을 클릭해서 설정을 업로드합니다.

![img](https://static.toastoven.net/prod_search/filed-upload-ko-20230831.jpg)

- 설정된 필드가 하나도 없을 때만 **설정 업로드** 버튼이 나타납니다.

### 전체 데이터 다시 색인

전체 데이터를 다시 색인할 때는 Full indexing API를 사용합니다.

- Full indexing 시작
	```
	curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing/full/begin'
	```
	- 새로운 index(저장소)가 생성됩니다.
	- Full indexing을 반영하기 전까지는 기존 index로 서비스됩니다.
- Full indexing 요청
	```
	curl -XPOST 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing/full' -H 'Content-Type:multipart/form-data; charset=UTF-8' -F 'file=@documents-001.json'
	```
	- documents-002.json, documents-003.json 등 여러 번 색인 요청을 합니다.
- Full indexing 반영
	```
	curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing/full/end'
	```
	- 색인된 데이터를 서비스에 반영합니다.
- Full indexing 취소
	```
	curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing/full/cancel'
	```
	- 색인이 진행 중일 때는 동작하지 않습니다.

### 동의어 사전

**URL**

1. 등록
	- POST	/dictionary/v2.0/appkeys/EMKPutYozUttWVY/serviceids/test/dictionary/thesaurus?way=1
2. 삭제
	- DELETE	/dictionary/v2.0/appkeys/EMKPutYozUttWVY/serviceids/test/dictionary/thesaurus
3. 리셋
	- POST	/dictionary/v2.0/appkeys/EMKPutYozUttWVY/serviceids/test/dictionary/thesaurus/reset

**파라미터**

- 파라미터
	- way	
- 값
	- 1: 단방향(기본값)
	- 2: 양방향
	
**형식**
- 단어 사이를 콤마(',')로 구분. 단어 내에 공백 및 구분자 사용 불가

**동의어**

1. 초기 상태
- '신발' 검색
	- Request
	```
	curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=신발&passage.productName=180'
	```
	
	- Response
	```
	"itemList": {
	  "item": [
	    {
	      "_ID": "100433865",
	      "_RANK": "0",
	      "_RELEVANCE": 100,
	      "productName": "부티크 리얼래빗퍼 슬리퍼 털슬리퍼 사무실<b>신발</b>"
	    }
	  ]
	}
	```
	
2. 동의어 사전 등록(단방향)
	- Request
	```
	curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/dictionary/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/dictionary/thesaurus?way=1'
	```
	```
	신발,운동화,스포츠화
	```
- '신발' 검색
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=신발&passage.productName=180'
	```

	- Response
	```
	"itemList": {
      "item": [
        {
          "_ID": "100433865",
          "_RANK": "0",
          "_RELEVANCE": 100,
          "productName": "부티크 리얼래빗퍼 슬리퍼 털슬리퍼 사무실<b>신발</b>"
        },
        {
          "_ID": "101874425",
          "_RANK": "0",
          "_RELEVANCE": 1,
          "productName": "아이보리도트운동화"
        },
        {
	      "_ID": "101714054",
	      "_RANK": "0",
	      "_RELEVANCE": 1,
	      "productName": "나이키/Nike Free TR 8 - Womens/Nike/기능성 스포츠화/라패셔니스타"
	    }
	  ]
	}
	```
- '운동화' 검색
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=운동화&passage.productName=180'
	```

	- Response
	```
	"itemList": {
      "item": [
        {
          "_ID": "101874425",
          "_RANK": "0",
          "_RELEVANCE": 100,
          "productName": "아이보리도트<b>운동화</b>"
        }
	  ]
	}
	```

	
4. 동의어 삭제(단방향)

	- Request
	```
	curl -i -XDELETE 'https://kr1-search.api.nhncloudservice.com/dictionary/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/dictionary/thesaurus'
	```
	```
	신발
	```
- '신발' 검색
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=신발&passage.productName=180'
	```
	
	- Response
	```
	"itemList": {
      "item": [
        {
          "_ID": "100433865",
          "_RANK": "0",
          "_RELEVANCE": 100,
          "productName": "부티크 리얼래빗퍼 슬리퍼 털슬리퍼 사무실<b>신발</b>"
        }
	  ]
	}
	```

- '운동화' 검색
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=운동화&passage.productName=180'
	```
	
	- Response
	```
	"itemList": {
      "item": [
        {
          "_ID": "101874425",
          "_RANK": "0",
          "_RELEVANCE": 100,
          "productName": "아이보리도트<b>운동화</b>"
        }
	  ]
	}
	```

5. 동의어 초기화
	- Request
	```
	curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/dictionary/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/dictionary/thesaurus/reset'
	```

### 불용어 사전

**URL**

1. 등록
	- POST	/dictionary/v2.0/appkeys/EMKPutYozUttWVY/serviceids/test/dictionary/stopwords
2. 삭제
	- DELETE	/dictionary/v2.0/appkeys/EMKPutYozUttWVY/serviceids/test/dictionary/stopwords
3. 리셋
	- POST	/dictionary/v2.0/appkeys/EMKPutYozUttWVY/serviceids/test/dictionary/stopwords/reset

**형식**

- 단어 사이를 new line('\n') 단위로 구분. 단어 내 공백 사용 불가

**불용어**

1. 초기 상태
- '커피' 검색
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=커피&passage.productName=180'
	```
	
	- Response
	```
	"itemList": {
      "item": [
        {
          "_ID": "100433702",
          "_RANK": "0",
          "_RELEVANCE": 100,
          "productName": "(STANLEY) 스탠리 마운틴 <b>커피</b>시스템 500미리"
        }
      ]
	}
	```

2. 불용어 사전 등록
	- Request
	```
	curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/dictionary/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/dictionary/stopwords'
	```
	```
	커피
	콜드브루				
	```
	
- '커피' 검색
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=커피&passage.productName=180'
	```

	- Response
	```
	{
      "message": {
        "result": {
          "total": 0,
          "query": "커피",
          "start": 1,
          "status": {
             "code": 200,
             "message": "OK"
          },
          "itemCount": 0
        },
        "meta": {
          "timezone": "+09:00"
        }
      }
    }
	```
	
- '콜드브루' 검색
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=콜드브루&passage.productName=180'
	```

	- Response
	```
	{
      "message": {
        "result": {
          "total": 0,
          "query": "콜드브루",
          "start": 1,
          "status": {
             "code": 200,
             "message": "OK"
          },
          "itemCount": 0
        },
        "meta": {
          "timezone": "+09:00"
        }
      }
    }
	```
	
2. 불용어 사전 삭제
	- Request
	```
	curl -i -XDELETE 'https://kr1-search.api.nhncloudservice.com/dictionary/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/dictionary/stopwords'
	```
	```
	콜드브루				
	```


- '콜드브루' 검색
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=콜드브루&passage.productName=180'
	```
	
	- Response
	```
    "itemList": {
      "item": [
        {
          "_ID": "101704573",
          "_RANK": "0",
          "_RELEVANCE": 100,
          "productName": "[블루빅센] 티모르레스떼 <b>콜드브루</b> 더치커피 750ml (고급형)"
        }
      ]
    }
	```

3. 불용어 사전 초기화
	- Request
	```
	curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/dictionary/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/dictionary/stopwords/reset'
	```

	
## 상세 가이드

### 필드 타입

필드 타입 선택 화면은 다음과 같습니다.

![img](http://static.toastoven.net/prod_search/field_type-ko-20230831.jpg)

- text
	- '검색'할 필드일 경우 선택합니다.
	- 형태소 분석을 합니다.
		- 필드값이 '나이키운동화'일 경우 '나이키운동화', '나이키 운동화', '나이키' 또는 '운동화'로 검색했을 때 검색 결과가 나옵니다.
	- 최대 사이즈는 32,768바이트입니다.
- keyword
	- '필터', '정렬', '요약'할 필드일 경우 선택합니다.
	- 형태소 분석을 하지 않습니다.
		- 필드값이 '나이키운동화'일 경우 '나이키운동화'로만 '필터', '정렬', '요약'이 됩니다.
		- 필드값이 '나이키 운동화'일 경우 '나이키 운동화'로만 '필터', '정렬', '요약'이 됩니다.
	- 최대 사이즈는 128바이트입니다.
- byte
	- 1byte 정수형입니다.
	- -128~127까지 표현 가능합니다.
- short
	- 2byte 정수형입니다.
	- -32,768~32,767까지 표현 가능합니다.
- integer
	- 4byte 정수형입니다.
	- -999,999,999~999,999,999까지 표현 가능합니다.
- long
	- 8byte 정수형입니다.
	- -999,999,999,999,999,999~999,999,999,999,999,999까지 표현 가능합니다.
- float
	- 4byte 실수형입니다.
	- -3.4E38~3.4E38까지 표현 가능합니다.
- double
	- 8byte 실수형입니다.
	- -1.7E308~1.7E308까지 표현 가능합니다.
- boolean
	- 1byte
	- true or false
- date
	- 필드값이 날짜인 경우 선택합니다.
	- 지원하는 날짜 형식
		- yyyy-MM-dd
			- 예제) 2017-09-22
		- yyyy-MM-dd’T’HH:mm:ss
			- 예제) 2017-09-22T15:39:28
		- yyyy-MM-dd’T’HH:mm:ss'Z'
			- 예제) 2017-09-22T15:39:28Z
- text를 제외한 모든 필드 타입은 배열 형태로 입력할 수 있습니다.
	- ["나이키", "아디다스"]
	- [1.0, 2.0]
	- ["2017-09-22T15:39:28", "2017-09-22T15:39:29"]

### 형태소 분석

형태소 분석기 선택 화면은 다음과 같습니다.

![img](http://static.toastoven.net/prod_search/analyzer-ko-20230831.jpg)

- default
	- 형태소 분석기를 이용해 단어를 분리합니다.
		- 예제) "나이키 신상슈즈" -> "나이키" "신상" "슈즈"
- whitespace
	- whitespace를 구분자로 토큰을 분리합니다.
		- 예제) "나이키 신상슈즈" -> "나이키" "신상슈즈"
- bigram
	- 2글자씩 단어를 분리합니다.
		- 예제) "나이키 신상슈즈" -> "나이" "이키" "신상" "상슈" "슈즈"
- quadgram
	- 4글자씩 단어를 분리합니다.
		- 예제) "스탠스미스" -> "스탠스미" "탠스미스"
- trigram
	- 3글자씩 단어를 분리합니다.
		- 예제) "스탠스미스" -> "스탠스" "탠스미" "스미스"
- unigram
	- 1글자씩 단어를 분리합니다.
		- 예제) "스탠스미스" -> "스" "탠" "스" "미" "스"

### ACL

ACL 설정 화면은 다음과 같습니다.

![img](http://static.toastoven.net/prod_search/acl-detail-ko-20200304.jpg)

- 입력 형식
	- IP 형식으로 입력 가능합니다.
		- 예제) 202.179.177.21
	- CIDR 형식으로 입력 가능합니다.
		- 예제) 202.179.177.0/24
	- IP 또는 CIDR 을 여러 개 입력 가능합니다.
		- 예제) 202.179.177.21, 202.179.177.0/24
	- all일 경우 모두 매칭됩니다.
	- 값이 비어 있을 경우 모두 매칭 안 됩니다.
- 허용, 거부 둘 다에 해당되면 거부됩니다.
- 허용, 거부 둘 다에 해당되지 않으면 거부됩니다.

## 클라이언트 예제 코드

다음은 파일 업로드 방식의 색인 예제 코드입니다.

### java

- dependency

```java
compile group: 'org.apache.httpcomponents', name: 'httpclient', version: '4.5.6'
compile group: 'org.apache.httpcomponents', name: 'httpmime', version: '4.5.6'
```

- 색인(파일 업로드 방식)

```java
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
      + "      \"title\": \"[무료배송]나이키 슈즈 195종!!\",\n"
      + "      \"body\": \"명불허전 나이키 인기슈즈 괜히 잘 팔리는게 아니죠~~ 나이키 핫!슈즈 195종★ 하나쯤은 있어야 하지 않아??\"\n"
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

### php

- 색인(파일 업로드 방식)

```php
<?php
    $documents = ""
      . "[\n"
      . "  {\n"
      . "    \"action\": \"add\",\n"
      . "    \"id\": \"id-1\",\n"
      . "    \"fields\": {\n"
      . "      \"title\": \"[무료배송]나이키 슈즈 195종!!\",\n"
      . "      \"body\": \"명불허전 나이키 인기슈즈 괜히 잘 팔리는게 아니죠~~ 나이키 핫!슈즈 195종★ 하나쯤은 있어야 하지 않아??\"\n"
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
