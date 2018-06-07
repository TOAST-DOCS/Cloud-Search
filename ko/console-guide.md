## Search > Cloud Search > 콘솔 사용 가이드

## 문서 설명
* 문서 내의 호스트명 "alpha-api-search.cloud.toast.com"는 사용자별로 다를 수 있습니다.
* 문서 내의 앱키 "gFGDJfG4pyUKZ9RF"는 사용자별로 다를 수 있습니다.

## 상품 활성화
* Cloud Search 서비스를 활성화하기 위해서 Console로 이동합니다.
* 활성화 방법
    ![](http://static.toastoven.net/prod_search/product-use-02.png????)
    1. "서비스 선택"을 클릭합니다.
    2. "Cloud Search"를 클릭해서 서비스를 활성화합니다.
<br>
* 활성화 확인
    ![](http://static.toastoven.net/prod_search/product-use-03.png??)
    1. "Search" 클릭합니다.
    2. "Cloud Search"가 노출되면 활성화된 것입니다.
<br>

## 기본 사용법

### 서비스 생성
* 서비스 생성 방법
    ![](http://static.toastoven.net/prod_search/domain_create_procedure.png?)
    1. "서비스 생성" 버튼을 클릭합니다.
    2. 서비스 ID를 입력합니다.
        * 영문 소문자, 숫자 및 일부 특수 문자만 사용 가능합니다.
        * 사용 가능한 특수 문자
        ```
        '~' '@' '$' '&' '(' ')' ':' '_' '-'
        ```
    3. "저장" 버튼을 클릭합니다.
<br>
* 서비스 생성 결과
    ![](http://static.toastoven.net/prod_search/domain_create_result.png?)
    1. 생성된 서비스 ID(test)를 클릭합니다.
<br>

### 필드 설정
* 필드 설정 방법
    ![](http://static.toastoven.net/prod_search/field_create_procedure.png??)
    1. "필드 설정" 탭을 클릭합니다.
    2. "필드 추가" 버튼을 클릭합니다.
    3. 필드 이름을 입력합니다.
        * 영문, 숫자 및 일부 특수문자만 가능합니다.
        * 사용 가능한 특수 문자
        ```
        '~' '@' '$' '&' '(' ')' ':' '_' '-'
        ```
        * 필드명은 \_ (underscore)로 시작할 수 없습니다.
    4. "저장" 버튼을 클릭합니다.
<br>

### 색인
* 색인할 파일 생성
    * 아래 예제와 같은 형식으로 색인 요청 파일을 생성합니다.
    * <span style="color:red">색인할 파일은 UTF-8로 생성해야 합니다.</span>
        * Windows 메모장에서 파일 저장시 인코딩을 UTF-8로 지정해서 저장합니다.
    * 예제에서는 data/documents.json 이름으로 생성했습니다.
    ```
    [
      {
        "action": "add",
        "id": "633800446",
        "fields": {
          "title": "[무료배송]나이키 슈즈 195종!!",
          "body": "명불허전 나이키 인기슈즈 괜히 잘 팔리는게 아니죠~~ 나이키 핫!슈즈 195종★ 하나쯤은 있어야 하지 않아??"
        }
      },
      {
        "action": "add",
        "id": "685165462",
        "fields": {
          "title": "[슈퍼특가]나이키 운동화 109종",
          "body": "단 7일만 이가격!  [슈퍼특가] 아디다스 슈즈 109종 모음전 망설이면 품~절~"
        }
      },
      {
        "action": "add",
        "id": "610408574",
        "fields": {
          "title": "[아디다스]신상운동화/슬리퍼 114종",
          "body": "[아디다스슈즈모음♥] 무/료/배/송 [아디다스]신상슬리퍼 /슈퍼스타 스탠스미스 /튜블라외 114종 득템기회!"
        }
      }
    ]
    ```
    * action
        * add : 문서 추가 또는 기존 문서 수정시 "add"로 지정합니다.
        * delete : 문서 삭제시 "delete"로 지정합니다.
    * id
        * 문서의 고유한 ID입니다.
        * id의 타입은 문자열입니다.
    * 최대 파일 사이즈는 8Mb입니다.
        * 8Mb 이상의 데이터는 여러 개로 나누어서 색인해야 합니다.
<br>
* 색인 방법
    ![](http://static.toastoven.net/prod_search/indexing_procedure_01.png?)
    ![](http://static.toastoven.net/prod_search/indexing_procedure_02.png?)
    1. "색인" 탭을 클릭합니다.
    2. "파일 선택" 버튼을 클릭합니다.
    3. 색인할 파일을 선택합니다.
    4. "열기" 버튼을 클릭합니다.  
    5. 색인 명령어가 REST API로 출력됩니다.
        * Rest API를 이용해서 검색 서비스를 연동하시면 됩니다.
    6. "색인" 버튼을 클릭합니다.
    7. 색인 결과를 확인할 수 있습니다.
<br>    
* Rest API
    * 아래와 같이 REST API를 사용 가능합니다.
    * 색인 API
        * Request
            ```
            $ curl -XPOST 'https://alpha-api-search.cloud.toast.com/indexing/v1.0/appkeys/gFGDJfG4pyUKZ9RF/serviceids/test/indexing' -H 'Content-Type:multipart/form-data; charset=UTF-8' -F 'file=@documents.json'
            ```
        * Response
            ```        
            {
              "id" : 1
            }
            ```
    * 색인 결과 확인 API
        * Request
            ```
            curl -i -XGET 'https://alpha-api-search.cloud.toast.com/indexing/v1.0/appkeys/gFGDJfG4pyUKZ9RF/serviceids/test/indexing_log?id=1'
            ```  
            * id 1은 위의 색인 API Response 의 id입니다.
        * Response
            ```
            {
              "request_time" : "2017-10-23T12:36:43",
              "file_name" : "documents.json",
              "file_size" : 1185,
              "status" : 4
            }
            ```
            * status
                * 1 : 대기 중
                * 2 : 무시됨 (필드 설정 변경 이전의 색인 요청은 무시됨)
                * 3 : 진행 중
                * 4 : 성공
                * 5 : 실패

### 검색
* 검색 방법
    ![](http://static.toastoven.net/prod_search/search_procedure.png??)
    1. "검색" 탭을 클릭합니다.
    2. 검색할 필드명을 체크합니다.
    3. 검색할 필드별 가중치를 설정합니다.
        * 0.0 ~ 1.0 값을 설정합니다.
    4. 검색 결과에 출력할 필드를 체크합니다.
    5. 검색 결과 길이를 설정합니다.
    6. 강조(Highlight) pre 태그를 설정합니다.
    7. 강조(Highlight) post 태그를 설정합니다.
    8. 검색 결과에서 출력할 시작 순위를 지정합니다.
        * "1"로 설정하면 1등부터 출력되고, "10"으로 설정하면 10등부터 출력됩니다.
    9. 검색 결과 개수를 지정합니다.
        * "5"로 설정하면 5개 출력되고, "10"으로 설정하면 10개 출력됩니다.
    10. 검색 연산자를 선택합니다.
    11. 검색할 단어를 입력합니다.
    12. 검색 아이콘을 클릭합니다.
    13. 2 ~ 11번까지 설정한 내용이 REST API로 출력됩니다.
        * Rest API를 이용해서 검색 서비스를 연동하시면 됩니다.
    14. 검색 결과가 출력됩니다.   
<br>

* Rest API
    * 아래와 같이 REST API를 사용 가능합니다.
    * Request
        ```
        $ curl -G -XGET 'https://alpha-api-search.cloud.toast.com/search/v1.0/appkeys/gFGDJfG4pyUKZ9RF/serviceids/test/search?start=1&size=10&q_option=and,body*1.0,title*1.0&return=body,title' --data-urlencode q='나이키 운동화'
        ```
    * Response
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
              "query" : "나이키 운동화",
              "start" : 1,
              "itemCount" : 1,
              "total" : 1,
              "itemList" : {
                "item" : [
                {
                  "_RELEVANCE" : 0.2369668,
                  "_RANK" : 1,
                  "_ID" : "685165462",
                  "body" : "단 7일만 이가격!  [슈퍼특가] 아디다스 슈즈 109종 모음전 망설이품~절~",
                  "title" : "[슈퍼특가]<b>나이키</b> <b>운동화</b> 109종"
                }
                ]
              }
            }
          }
        }
        ```

### ACL
* 색인 및 검색 REST API를 호출할 수 있는 장비의 IP를 제한할 수 있습니다.
    * 콘솔에서 테스트하는 경우 ACL 설정과 관련 없습니다.
* ACL 설정 방법
    ![](http://static.toastoven.net/prod_search/acl_procedure.png??)
    1. "ACL" 탭을 클릭합니다.
    2. 색인 요청은 IP 주소가 202.179.177.21 인 경우만 색인이 가능하도록 설정한 예제입니다.
    3. 검색 요청은 모든 IP에서 가능하도록 설정한 예제입니다.
    4. "저장" 버튼을 클릭합니다.

## 기능 가이드

### 사전 준비
* 서비스 삭제
    * 기존에 "test" 서비스 ID가 존재하면 삭제합니다.
        ![](http://static.toastoven.net/prod_search/domain_delete_procedure.png??)
        1. "삭제" 버튼을 클릭합니다.
<br>
* 서비스 생성
    * 서비스 생성 방법
        ![](http://static.toastoven.net/prod_search/domain_create_procedure.png???)
        1. "서비스 생성" 버튼을 클릭합니다.
        2. 서비스 ID를 입력합니다.
        3. "저장" 버튼을 클릭합니다.
<br>
* 필드 설정
    * 필드 설정 방법
        ![](http://static.toastoven.net/prod_search/field_create_procedure-3_function.png??)
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
    ![](http://static.toastoven.net/prod_search/indexing_procedure_01.png????)
    ![](http://static.toastoven.net/prod_search/indexing_procedure_02.png??????)
    1. "색인" 탭을 클릭합니다.
    2. "파일 선택" 버튼을 클릭합니다.
    3. 색인할 파일을 선택합니다.
    4. "열기" 버튼을 클릭합니다.  
    5. 색인 명령어가 Rest API로 출력됩니다.
    6. "색인" 버튼을 클릭합니다.
    7. 색인 결과를 확인할 수 있습니다.
<br>

### 필터링 기능
* 색인된 필드만 필터링 가능합니다.
    * "필드 설정" 탭에서 "색인" 체크 박스에 체크한 경우만 "검색" 탭에 "필터" 체크 박스가 노출됩니다.
* 필터링 방법
    ![](http://static.toastoven.net/prod_search/search_procedure-filtering_function.png??)
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
        "category": 1,
        "title": "[무료배송]나이키 슈즈 195종!!"
      },
      {
        "dealer": "롯데아이몰",
        "update": "2017-09-20T13:23:38",
        "_RELEVANCE": 1,
        "_RANK": 2,
        "_ID": "685165462",
        "body": "단 7일만 이가격!  [슈퍼특가] 아디다스 슈즈 109종 모음전 망설이면 품~절~",
        "category": 1,
        "title": "[슈퍼특가]나이키 운동화 109종"
      }
    ]
    ```
    * "category" 가 1인 문서만 필터링 됩니다.
<br>

### 정렬 기능
* 색인된 필드만 정렬 가능합니다.
    * "필드 설정" 탭에서 "색인" 체크 박스에 체크한 경우만 "검색" 탭에 "정렬" 체크 박스가 노출됩니다.
* 정렬 방법
    ![](http://static.toastoven.net/prod_search/search_procedure-sorting_function.png?????)
    1. "색인" 탭을 클릭합니다.
    2. 소팅할 필드를 체크하고 소팅 Order(asc or desc)를 선택합니다.
    3. 다중 정렬일 경우 정렬 순서를 지정합니다.
        * 다중 정렬 : 예를 들어 update 필드로 정렬했는데 update 값이 동일한 경우 category 순으로 정렬하는 기능입니다.
    4. 검색 아이콘을 클릭합니다.
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
        "category": 2,
        "title": "[아디다스]신상운동화/슬리퍼 114종"
      },
      {
        "dealer": "롯데아이몰",
        "update": "2017-09-20T13:23:38",
        "_RELEVANCE": "NaN",
        "_RANK": 2,
        "_ID": "685165462",
        "body": "단 7일만 이가격!  [슈퍼특가] 아디다스 슈즈 109종 모음전 망설이면 품~절~",
        "category": 1,
        "title": "[슈퍼특가]나이키 운동화 109종"
      },
      {
        "dealer": "롯데아이몰",
        "update": "2017-09-19T12:34:28",
        "_RELEVANCE": "NaN",
        "_RANK": 3,
        "_ID": "633800446",
        "body": "명불허전 나이키 인기슈즈 괜히 잘 팔리는게 아니죠~~ 나이키 핫!슈즈 195종★ 하나쯤은 있어야 하지 않아??",
        "category": 1,
        "title": "[무료배송]나이키 슈즈 195종!!"
      }
    ]
    ```    
    * "update" 내림차순(desc)으로 정렬됩니다.

### 요약(Aggregation) 기능
* 색인된 필드만 요약 가능합니다.
    * "필드 설정" 탭에서 "색인" 체크 박스에 체크한 경우만 "검색" 탭에 "요약" 체크 박스가 노출됩니다.
* 요약 방법
    ![](http://static.toastoven.net/prod_search/search_procedure-summary_function.png????)
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
    * dealer 별 문서 개수가 출력됩니다.

### 필수 필터 기능
* 사용 예시
    * 예를 들어 메일 검색 서비스를 할 경우 다른 사용자의 메일이 검색되면 안 되기 때문에 반드시 사용자별로 필터링을 해야 합니다.
* 사용 방법
    ![](http://static.toastoven.net/prod_search/mandatory_search_filter_01.png??)
    ![](http://static.toastoven.net/prod_search/mandatory_search_filter_02.png??)
    1. "필드 설정" 탭을 클릭합니다.
    2. dealer 필드의 필수 검색 필터를 체크합니다.
        * 다른 설정도 그림과 같이 지정합니다.
    3. "저장" 버튼을 클릭합니다.
    4. "검색" 탭을 클릭합니다.
    5. dealer 필드의 필터링 값은 입력하지 않습니다.
    6. 검색 버튼을 클릭합니다.
    7. 필수 검색 필터로 지정된 필드에 필터링 값이 없기 때문에 실패 메시지가 출력됩니다.

### 필드 삭제
* 필드 삭제 방법
    ![](http://static.toastoven.net/prod_search/field_delete_procedure_01.png?)
    ![](http://static.toastoven.net/prod_search/field_delete_procedure_02.png??)
    1. "필드 설정" 탭을 클릭합니다.
    2. 삭제할 필드의 "삭제" 버튼을 클릭합니다.
    3. "저장" 버튼을 클릭합니다.
    4. "지금 수행" 버튼을 클릭합니다.
* 재색인 중에는 문서 추가, 수정, 삭제가 안됩니다.

## 상세 가이드

### 필드 타입
![](http://static.toastoven.net/prod_search/detail-field_type.png???)

* text
    * "검색"할 필드일 경우 선택합니다.
    * 형태소 분석을 합니다.
        * 필드 값이 "나이키운동화"일 경우 "나이키운동화", "나이키 운동화", "나이키" 또는 "운동화"로 검색했을 때 검색 결과가 나옵니다.
    * 최대 사이즈는 4,096Byte입니다.
* keyword
    * "필터", "정렬", "요약"할 필드일 경우 선택합니다.
    * 형태소 분석을 하지 않습니다.
        * 필드 값이 "나이키운동화"일 경우 "나이키운동화"로만 "필터", "정렬", "요약"이 됩니다.
        * 필드 값이 "나이키 운동화"일 경우 "나이키 운동화"로만 "필터", "정렬", "요약"이 됩니다.
    * 최대 사이즈는 64Byte입니다.
* byte
    * 1byte 정수형입니다.
    * -128 ~ 127까지 표현 가능합니다.
* short
    * 2byte 정수형입니다.
    * -32,768 ~ 32,767까지 표현 가능합니다.
* integer
    * 4byte 정수형입니다.
    * -2^31 ~ 2^31 - 1까지 표현 가능합니다.
* long
    * 8byte 정수형입니다.
    * -2^63 ~ 2^63 - 1까지 표현 가능합니다.
* float
    * 4byte 실수형입니다.    
    * -3.4E38 ~ 3.4E38까지 표현 가능합니다.
* double
    * 8byte 실수형입니다.
    * -1.7E308 ~ 1.7E308까지 표현 가능합니다.
* boolean
    * 1byte
    * true or false
* date
    * 필드 값이 날짜인 경우 선택합니다.
    * 지원하는 날짜 형식
        * yyyy-MM-dd
            * 예제) 2017-09-22
        * yyyy-MM-dd’T’HH:mm:ss
            * 예제) 2017-09-22T15:39:28
        * yyyy-MM-dd’T’HH:mm:ss'Z'
            * 예제) 2017-09-22T15:39:28Z
        * yyyy-MM-dd'T'HH:mm:ss.SSS
            * 예제) 2017-09-22T15:39:28.248
        * yyyy-MM-dd'T'HH:mm:ss.SSS'Z'
            * 예제) 2017-09-22T15:39:28.248Z
* 모든 필드 타입은 배열 행태로 입력 가능합니다.
    * ["나이키", "운동화"]
    * [1.0, 2.0]
    * ["2017-09-22T15:39:28", "2017-09-22T15:39:29"]

### 형태소 분석
![](http://static.toastoven.net/prod_search/detail-analysis.png??)

* default
    * 형태소 분석기를 이용해 단어을 분리한다.
      * 예제) "나이키 신상슈즈" -> "나이키" "신상" "슈즈"
* whitespace
    * whitespace를 구분자로 토큰을 분리한다.
      * 예제) "나이키 신상슈즈" -> "나이키" "신상슈즈"
* bigram
    * 2글자씩 단어를 분리한다.
      * 예제) "나이키 신상슈즈" -> "나이" "이키" "신상" "상슈" "슈즈"

### 필터링
![](http://static.toastoven.net/prod_search/detail-filter.png?)

* 단일 값 필터링
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
![](http://static.toastoven.net/prod_search/detail-acl.png??)

* 입력형식
    * IP 형식으로 입력 가능합니다.
        * 예제) 202.179.177.21
    * CIDR 형식으로 입력 가능합니다.
        * 예제) 202.179.177.0/24
    * IP 또는 CIDR 을 여러 개 입력 가능합니다.
        * 예제) 202.179.177.21, 202.179.177.0/24
    * all 일 경우 모두 매칭 됩니다.
    * 값이 비어 있을 경우 모두 매칭 안됩니다.  
* 허용, 거부 둘 다에 매칭이 될 경우 거부됩니다.
* 허용, 거부 둘 다에 매칭이 안될 경우 거부됩니다.
