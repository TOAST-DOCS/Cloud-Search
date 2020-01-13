## Search > Cloud Search > 개요

* 별도의 인프라 및 검색 솔루션 설치 없이 간편하게 검색 서비스를 구축할 수 있습니다.
    * 색인 REST API를 이용해서 검색할 데이터를 입력합니다.
    * 검색 REST API를 이용해서 검색 결과를 받아옵니다.

### 자동완성 서비스 개발 과정

* 서비스 구성도
![](http://static.toastoven.net/prod_autocomplete/block_diagrm-20200113.png)

* 서비스 개발 과정
    1. 서비스 생성
        * 검색 서비스를 생성합니다.
    2. 필드 설정
        * 검색 데이터의 스카마를 설정합니다.
    3. 색인
        * Cloud Search의 입력 형식에 맞게 JSON 데이터를 생성합니다.
        * 생성된 JSON 데이터를 REST API를 이용해서 Cloud Search에 입력합니다.
    4. 검색
        * 검색 REST API의 결과를 이용해서 Front 화면을 구성합니다.
