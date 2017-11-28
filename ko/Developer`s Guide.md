## Upcomming Products > Search > Developer's Guide

## 기능 설명

### 사전 준비
* 도메인 삭제
    * 기존에 "test" 도메인이 존재하면 삭제합니다.
        ![](http://static.toastoven.net/prod_search/domain_delete_procedure.png?)
        1. "삭제" 버튼을 클릭합니다.
<br>
* 도메인 생성
    * 도메인 생성 방법
        ![](http://static.toastoven.net/prod_search/domain_create_procedure.png??)
        1. "도메인 생성" 버튼을 클릭합니다.
        2. 도메인 이름을 입력합니다.
        3. "저장" 버튼을 클릭합니다.
<br>
* 필드 설정
    * 필드 설정 방법
        ![](http://static.toastoven.net/prod_search/field_create_procedure-3_function.png?????)
        1. "필드 설정" 탭을 클릭합니다.
        2. "필드 추가" 버튼을 클릭합니다.
        3. "필드명"을 입력합니다.
        4. "category" 필드는 "integer" 타입을 선택합니다.
        5. "dealer" 필드는 "keyword" 타입을 선택합니다.
        6. "update" 필드는 "date" 타입을 선택합니다.
        7. "저장" 버튼을 클릭합니다.
<br>
* 색인 파일 생성
    * 필터링, 정렬, 요약 기능 테스트를 위해 아래와 같은 데이터를 생성합니다.
    ```
    [
      {
        "action": "add",
        "id": "633800446",
        "fields": {
          "title": "[무료배송]나이키 슈즈 195종!!",
          "body": "명불허전 나이키 인기슈즈 괜히 잘 팔리는게 아니죠~~ 나이키 핫!슈즈 195종★ 하나쯤은 있어야 하지 않아??",
          "category": 1,
          "dealer": "롯데아이몰",
          "update": "2017-09-19T12:34:28"
        }
      },
      {
        "action": "add",
        "id": "685165462",
        "fields": {
          "title": "[슈퍼특가]나이키 운동화 109종",
          "body": "단 7일만 이가격!  [슈퍼특가] 아디다스 슈즈 109종 모음전 망설이면 품~절~",
          "category": 1,
          "dealer": "롯데아이몰",
          "update": "2017-09-20T13:23:38"
        }
      },
      {
        "action": "add",
        "id": "610408574",
        "fields": {
          "title": "[아디다스]신상운동화/슬리퍼 114종",
          "body": "[아디다스슈즈모음♥] 무/료/배/송 [아디다스]신상슬리퍼 /슈퍼스타 스탠스미스 /튜블라외 114종 득템기회!",
          "category": 2,
          "dealer": "신세계몰",
          "update": "2017-09-20T23:58:12"
        }
      }
    ]
    ```
<br>
* 색인
    ![](http://static.toastoven.net/prod_search/indexing_procedure_01.png?????)
    ![](http://static.toastoven.net/prod_search/indexing_procedure_02.png???????)
    1. "색인" 탭을 클릭합니다.
    2. "파일 선택" 버튼을 클릭합니다.
    3. 색인할 파일을 선택합니다.
    4. "열기" 버튼을 클릭합니다.  
    5. 색인 명령어가 Rest API 로 출력됩니다.
    6. "색인" 버튼을 클릭합니다.
    7. 색인 결과를 확인할 수 있습니다.

### 필터링 기능
* 필터링 방법
    ![](http://static.toastoven.net/prod_search/search_procedure-filtering_function.png?)
    1. "색인" 탭을 클릭합니다.
    2. 필터링할 필드를 체크하고 필터링할 값을 입력합니다.
    3. 검색 아이콘을 클릭합니다.
<br>
* 검색결과
    ```
    [
      {
        "dealer": "롯데아이몰",
        "update": "2017-09-19T12:34:28",
        "_RELEVANCE": 1,
        "_RANK": 1,
        "_ID": "633800446",
        "body": "명불허전 나이키 인기슈즈 괜히 잘 팔리는게 아니죠~~ 나이키 핫!슈즈 195종★ 하나쯤은 있어야 하지 않아??",
        "category": "1",
        "title": "[무료배송]나이키 슈즈 195종!!"
      },
      {
        "dealer": "롯데아이몰",
        "update": "2017-09-20T13:23:38",
        "_RELEVANCE": 1,
        "_RANK": 2,
        "_ID": "685165462",
        "body": "단 7일만 이가격!  [슈퍼특가] 아디다스 슈즈 109종 모음전 망설이면 품~절~",
        "category": "1",
        "title": "[슈퍼특가]나이키 운동화 109종"
      }
    ]
    ```
    * "category" 가 1인 문서만 필터링 됩니다.

### 정렬 기능
* 정렬 방법
    ![](http://static.toastoven.net/prod_search/search_procedure-sorting_function.png????)
    1. "색인" 탭을 클릭합니다.
    2. 소팅할 필드를 체크하고 소팅 Order(asc or desc) 를 선택합니다.
    3. 검색 아이콘을 클릭합니다.
<br>
* 검색 결과
    ```
    [
      {
        "dealer": "신세계몰",
        "update": "2017-09-20T23:58:12",
        "_RELEVANCE": "NaN",
        "_RANK": 1,
        "_ID": "610408574",
        "body": "[아디다스슈즈모음♥] 무/료/배/송 [아디다스]신상슬리퍼 /슈퍼스타 스탠스미스 /튜블라외 114종 득템기회!",
        "category": "2",
        "title": "[아디다스]신상운동화/슬리퍼 114종"
      },
      {
        "dealer": "롯데아이몰",
        "update": "2017-09-20T13:23:38",
        "_RELEVANCE": "NaN",
        "_RANK": 2,
        "_ID": "685165462",
        "body": "단 7일만 이가격!  [슈퍼특가] 아디다스 슈즈 109종 모음전 망설이면 품~절~",
        "category": "1",
        "title": "[슈퍼특가]나이키 운동화 109종"
      },
      {
        "dealer": "롯데아이몰",
        "update": "2017-09-19T12:34:28",
        "_RELEVANCE": "NaN",
        "_RANK": 3,
        "_ID": "633800446",
        "body": "명불허전 나이키 인기슈즈 괜히 잘 팔리는게 아니죠~~ 나이키 핫!슈즈 195종★ 하나쯤은 있어야 하지 않아??",
        "category": "1",
        "title": "[무료배송]나이키 슈즈 195종!!"
      }
    ]
    ```    
    * "update" 내림차순(desc)으로 정렬됩니다.

### 요약 기능
* 요약 방법
    ![](http://static.toastoven.net/prod_search/search_procedure-summary_function.png???)
    1. "색인" 탭을 클릭합니다.
    2. 요약할 필드를 체크합니다.
    3. 검색 아이콘을 클릭합니다.
<br>
* 검색 결과
    ```
    {
      "dealer": {
        "롯데아이몰": 2,
        "신세계몰": 1
      }
    }
    ```
    * dealer별 문서 개수가 출력됩니다.

### 필드 삭제
* 필드 삭제 방법
    ![](http://static.toastoven.net/prod_search/field_delete_procedure_01.png)
    ![](http://static.toastoven.net/prod_search/field_delete_procedure_02.png?)
    1. "필드 설정" 탭을 클릭합니다.
    2. 삭제할 필드의 "삭제" 버튼을 클릭합니다.
    3. "저장" 버튼을 클릭합니다.
    4. "지금 수행" 버튼을 클릭합니다.

## 상세 설명

### 필드 타입
![](http://static.toastoven.net/prod_search/detail-field_type.png???)

* text
    * 필드값이 문자열인 경우 선택합니다.
    * 형태소 분석 방법을 지정할 수 있습니다.
* keyword
    * 필드값을 형태소 분석 할 필요가 없는 경우 선택합니다.
    * 예를 들어 카테고리, 우편 번호, 태그 등과 같은 데이터에 사용합니다.
    * 필터링, 정렬, 요약 기능을 사용할 수 있습니다.
* integer
    * 필드 값이 숫자인 경우 선택합니다.
* date
    * 필드 값이 날짜인 경우 선택합니다.
    * 지원하는 날짜 형식
        * yyyy-MM-dd
            * 예제) 2017-09-22
        * yyyy-MM-dd’T’HH:mm:ss
            * 예제) 2017-09-22T15:39:28
        * yyyy-MM-dd'T'HH:mm:ss.SSS
            * 예제) 2017-09-22T15:39:28.248
        * yyyy-MM-dd'T'HH:mm:ss.SSSXXX
            * 예제) 2017-09-22T15:39:28.248+09:00

### 형태소 분석
![](http://static.toastoven.net/prod_search/detail-analysis.png)

* default
    * 형태소 분석기를 이용해 토큰을 분리한다.
      * 예제) "나이키 신상슈즈" -> "나이키" "신상" "슈즈"
* whitespace
    * whitespace 를 구분자로 토큰을 분리한다.
      * 예제) "나이키 신상슈즈" -> "나이키" "신상슈즈"

### 필터링
![](http://static.toastoven.net/prod_search/detail-filter.png)

* 단일값 필터링
    * 예제) 1
        * category == 1
* or 필터링
    * 예제) 1|2
    * category == 1 or category == 2
* and 필터링
    * 예제) 1&2
        * category == 1 and category == 2      
* 범위 지정 필터링
    * 예제) [1,2]
        * 1 <= category <= 2
    * 예제) {1,2]      
        * 1 < category <= 2
    * 예제) {,2]      
        * category <= 2
* not 필터링
      * 예제) !1
          * category != 1
      * 예제) !1|2
          * category !=1 or category == 2

### ACL
![](http://static.toastoven.net/prod_search/detail-acl.png?)

* 입력형식
    * IP 형식으로 입력 가능합니다.
        * 예제) 202.179.177.21
    * CIDR 형식으로 입력가능합니다.
        * 예제) 202.179.177.0/24
    * IP 또는 CIDR 을 여러개 입력 가능합니다.
        * 예제) 202.179.177.21, 202.179.177.0/24
    * all 일 경우 모두 매칭됩니다.
    * 값이 비어 있을 경우 모두 매칭안됩니다.  
* Allow, Deny 둘다에 매칭이 될 경우 Deny 됩니다.
* Allow, Deny 둘다에 매칭이 안될 경우 Deny 됩니다.
