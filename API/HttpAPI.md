# **HTTP API 설계**

## **📄 INDEX**
1. HTTP API - 컬렉션
    * POST 기반 등록
    * 예) 회원 관리 API 제공

2. HTTP API - 스토어
    * PUT 기반 등록
    * 예) 정적 컨텐츠 관리, 원격 파일 관리

3. HTTP FORM 사용
    * 웹 페이지 회원 관리
    * GET, POST 만 지원

## **API 설계 - POST 기반 등록**
### 1️⃣ 회원 관리 시스템
* 회원 목록/members -> GET 
  * 조건이 있다면 쿼리 파라미터에 추가해서 전달하면 된다.

* 회원 등록/members -> POST
* 회원 조회/members/{id} -> GET
* 회원 수정/members/{id} -> PATCH, PUT, POST
  * 보통 게시글 수정의 경우 부분이 바뀌더라도 PUT으로 일괄 변경 처리한다.

* 회원 삭제/members/{id} -> DELETE

### 2️⃣ POST - 신규 자원등록 특징
* 클라이언트는 등록될 리소스의 URL를 모른다.
  * 회원등록/members -> POST
  * POST/members

* 요청 메시지를 받은 서버가 새로 등록된 리소스의 URL을 생성해준다.
  * HTTP/1.1 201 Created
  * Location: /members/100

* 컬렉션(Collection)
  * 서버가 관리하는 리소스 디렉토리
  * 서버가 리소스의 URL을 생성하고 관리한다
  * 여기서의 컬렉션은 /members

> POST는 클라이언트가 서버에게 이 리소스를 등록해달라고 요청한다.  
> 그러면 서버는 해당 리소스의 URI를 만들어서 돌려준다. 

## **API 설계 - PUT 기반 등록**
### **📄 파일 관리 시스템**
* 파일 목록/files -> GET
* 파일 조회/files/{filename} -> GET
* 파일 등록/files/{filename} -> PUT 
  * 기존 파일이 있어도 덮어쓴다.

* 파일 삭제/files/{filename} -> DELETE
* 파일 대량 등록/files -> POST
  * POST는 상황에 맞게 쓸 수 있다. 이번 경우에는 대량 등록을 위해 사용

### **PUT - 신규 자원 등록 특징**
> 등록을 위해 POST 대신 PUT을 사용하고 있다. 어떤 차이점이 있을까?

* 클라이언트가 리소스 URL를 알고 있어야 한다.
  * 파일 등록/files/{filename} -> PUT
  * PUT /files/start.png

* 클라이언트가 직접 리소스의 URL을 지정한다.
* 스토어(store)
  * 클라이언트가 관리하는 리소스 저장소
  * 클라이언트가 리소스의 URI를 알고 관리한다
  * 여기서 스토어는 /files

> PUT은 클라이언트가 관리하는 리소스의 URL을 지정해서 서버에게 등록해달라고 요청한다.  
> 그러면 서버는 해당 리소스를 전달 받은 URI에 등록해준다.

**"대부분 POST기반의 Collection의 관리 시스템을 사용한다."**