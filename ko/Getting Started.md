## Upcomming Products > Search > Getting Started

## 서비스 활성화
Search 서비스를 사용하기 위해서는 Console에서 [Upcoming Products] > [Search] 을 선택한 후 [상품이용] 버튼을 클릭하여 서비스를 활성화시킵니다.
![](http://static.toastoven.net/prod_search/product-use-01.png)
![](http://static.toastoven.net/prod_search/product-use-02.png)

1. "Upcoming Proucts"를 클릭합니다.
2. "Search"를 클릭합니다.
3. "상품이용" 버튼을 클릭합니다.
<br>

## 기본 사용법

### 도메인 생성
* 도메인 생성 방법
    ![](http://static.toastoven.net/prod_search/domain_create_procedure.png???)
    1. "도메인 생성" 버튼을 클릭합니다.
    2. 도메인 이름을 입력합니다.
        * 영문, 숫자 및 특수문자만 가능합니다.
        * 사용 불가 문자 : "\\", "/", "*", "?", "\"", "<", ">", "|", " ", ",", "#", "^", "!"
    3. "저장" 버튼을 클릭합니다.
<br>
* 도메인 생성 결과
    ![](http://static.toastoven.net/prod_search/domain_create_result.png)
    1. 생성된 도메인(test)를 클릭합니다.
<br>
* 제약 사항
    * 하나의 appKey(사용자) 당 도메인은 최대 32개 까지 생성 가능합니다.

### 필드 설정
* 필드 설정 방법
    ![](http://static.toastoven.net/prod_search/field_create_procedure.png???????)
    1. "필드 설정" 탭을 클릭합니다.
    2. "필드 추가" 버튼을 클릭합니다.
    3. 필드 이름을 입력합니다.
        * 필드명은 \_ (underscore)로 시작할 수 없습니다.
    4. "저장" 버튼을 클릭합니다.
<br>

### 색인
* 색인할 파일 생성
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
<br>
* 색인 방법
    ![](http://static.toastoven.net/prod_search/indexing_procedure_01.png?????)
    ![](http://static.toastoven.net/prod_search/indexing_procedure_02.png????????)
    1. "색인" 탭을 클릭합니다.
    2. "파일 선택" 버튼을 클릭합니다.
    3. 색인할 파일을 선택합니다.
    4. "열기" 버튼을 클릭합니다.  
    5. 색인 명령어가 Rest API 로 출력됩니다.
    6. "색인" 버튼을 클릭합니다.
<br>    
* 색인할 파일 생성
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
* Rest API
    * 아래와 같이 Rest API를 사용 가능합니다.
    ```
    [admin@NHNEnt:data]$ curl -XPOST 'https://alpha-api-search.cloud.toast.com/indexing/v1.0/appkeys/rjmIWV4TQuTaxvAc/domains/test/indexing' -H 'Content-Type:multipart/form-data; charset=UTF-8' -F 'file=@documents.json'

    {
      "result" : "success",
      "code" : 1
    }
    ```

### 검색
* 검색 방법
    ![](http://static.toastoven.net/prod_search/search_procedure.png)
    1. "검색" 탭을 클릭합니다.
    2. 검색할 필드명을 체크합니다.
    3. 검색할 필드별 가중치를 설정합니다.
        * 0.0 ~ 1.0 값을 설정합니다.
    4. 검색 결과에 출력할 필드를 체크합니다.
    5. 검색 연산자를 선택합니다.
    6. 검색할 단어를 입력합니다.
    7. 검색결과에서 출력할 시작 순위를 지정합니다.
        * "1"로 설정하면 1등부터 출력되고, "10"으로 설정하면 10등부터 출력됩니다.
    8. 검색결과 개수를 지정합니다.
        * "5"로 설정하면 5개 출력되고, "10"으로 설정하면 10개 출력됩니다.
    9. 검색 아이콘을 클릭합니다.
    10. 1 ~ 8 번까지 설정한 내용이 Rest API 로 출력됩니다.
        * Rest API 를 이용해서 검색 서비스를 연동하시면 됩니다.
    11. 검색 결과가 출력됩니다.   
<br>
* Rest API
    * 아래와 같이 Rest API를 사용 가능합니다.
        ```
        [admin@NHNEnt:~]$ curl -G -XGET 'https://alpha-api-search.cloud.toast.com/search/v1.0/appkeys/rjmIWV4TQuTaxvAc/domains/test/search?start=1&size=10&q_option=and,body*1.0,title*1.0&return=body,title' --data-urlencode q='나이키 운동화'
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
                  "body" : "단 7일만 이가격!  [슈퍼특가] 아디다스 슈즈 109종 모음전 망설이면 품~절~",
                  "title" : "[슈퍼특가]<b>나이키</b> <b>운동화</b> 109종"
                }
                ]
              }
            }
          }
        }
        ```

### ACL
* ACL 설정 방법
    ![](http://static.toastoven.net/prod_search/acl_procedure.png?)
    1. "ACL" 탭을 클릭합니다.
    2. 색인 요청은 IP 주소가 202.179.177.21 인 경우만 색인이 가능하도록 설정한 예제입니다.
    3. 검색 요청은 모든 IP 에서 가능하도록 설정한 예제입니다.
    4. "저장" 버튼을 클릭합니다.
