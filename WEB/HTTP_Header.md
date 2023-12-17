# HTTP 헤더 
 - 개요 : 헤더필드 : 필드내임 (필드네임은 대소무낮 구분 없음)
 - 용도 :
   - HTTP 전송에 필요한 모든 부가정보
   - 예) 메세지 바디의 내용, 바디의 크기, 인증, 서버정도, 캐시관리 등등...
   - 필요 시 임의의 헤더 추가 가능
   
   <div align="center">
       <img src="img/header1.png" alt="이미지 설명" width="500" height="500">
     </div>
     
 - 헤더의 종류 (RFC 2616 - 과거)
   - General 헤더 : 메세지 전체에 적용되는 정보
   - Request 헤더 : 요청 정보
   - Response 헤더 : 응답 정보
   - Entity 헤더 : 엔티티 바디 정보
 
 - RFC 7230 - 최신
   - 엔티티 -> 표현
   - 표현 : 표현 메타데이터 + 표현데이터
   
 - HTTP BODY
   - message body - RFC7230  
   
    <div align="center">
          <img src="img/header2.png" alt="이미지 설명" width="500" height="500">
        </div>
        
      - 메세지 본문을 통해 표현 데이터 전달
      - 메세지 본문  = 페이로드
      - 표현은 요청이나 응답에서 전달할 실제 데이터
      - 표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공
        - 데이터 유형 (HTML, json), 데이터 길이, 압축 정보 등등
      

## 표현 헤더
- Content-Type : 표현 데이터의 형식
  - 표현 데이터의 형식 설명
  - 미디어 타입, 문자 인코딩
  - 예) 
    - text/html; charset=utf-8
    - application/json
    - image/png
  
- Content-Encoding : 표현 데이터의 압축 방식
  - 표현 데이터 인코딩
  - 표현 데이터를 압축하기 위해 사용
  - 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
  - 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
  - 예)
    - gzip
    - deflate
    - identity
    
- Content-Language : 표현 데이터의 자연 언어
  - 표현 데이터의 자연 언어를 표현
  - 예)
    - ko
    - en
    - en-US
    
- Content-Length : 표현 데이터의 길이
- 표현 헤더는 전송, 응답 둘다 사용 


## 협상 헤더 (콘텐트 네고시에이션)
클라이언트가 선호하는 표현 요청

- Accept : 클라이언트가 선호하는 미디어 타입(콘텐트 타입) 전달
- Accept-Charset : 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding : 클라이언트가 선호하는 압축 인코딩
- Accept-Language : 클라이언트가 선호하는 자연 언어
- 협상 헤더는 요청시에만 사용

### 협상과 우선순위 1
Quality Values(q)

- Quality Values(q) 값 사용
- 0~1, 클수록 높은 우선순위
- 생략하면 1
- Accept-Language:ko-KR,ko;q=0.9,en-US;q=0.8,en;Q=0.7
 1. ko-KR;q=1(q생략)
 2. ko;q=0.9
 3. en-US;q=0.8
 4. en;Q=0.7
  
 ### 협상과 우선운위 2
 - 구체적인 것이 우선한다.
 - Accept:text/*, text/plain, text/plain;format=flowed, \*/\*
  1. text/plain;format=flowed
  2. text/plain
  3. text/*
  4. \*/\*
  
  
 ### 전송 방식 설명
 - 단순 전송
   - 단순히 전송
   
 - 압축 전송
   - 콘텐트 인코딩 헤더 필요
   
 - 분할 전송
   - 일정 바이트씩 나눠서 전달
   
 - 범위 전송
   - 이미지등 큰 파일 전송 시 취소된 경우 사용
   
   
 ### 일반 정보 헤더
 
 - From : 유저 에이전트의 이메일 정보
   - 일반적으로 잘 사용 X
   - 검색 엔진 등에서 사용
   - 요청에서 사용
   
 - Referer : 이전 웹페이지 주소 ** 많이 사용
    - 현재 요청된 페이지의 이전 웹 페이지 주소
    - A -> B 로 이동하는 경우 B를 요청할 때 Referer:A를 포함해서 요청
    - *** Referer을 사용해서 유입 경로 분석 가능
    - 요청에서 사용
    - 참고 : referer은 단어 referrer의 오타
 
 - User-Agent : 유저 에이전트의 애플리케이션 정보
   - Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
   - 클라이언트의 애플리케이션 정보(웹 브라우저 정보 등등)
   - 통계 정보
   - 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
   - 요청에서 사용
   
 - Server : 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
   - Server: Apache/2.2.22(Debian)
   - server: nginx
   - 응답에서 사용
   
 - Date : 메세지가 발생한 날짜와 시간
   - Date: Fri, 15 Dec 2023 01:18:00 GMT
   - 응답에서 사용
   

### 특별한 정보
  - Host : 요청한 호스트 정보(도메인) 
    - 요청에서 사용
    - 필수 ***
    - 하나의 서버가 여러 도메인을 처리해야 할 때
    - 하나의 IP 주소에 여러 도메인이 적용되어 있을 때
    
  - Location : 페이지 리다이렉션
    - 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면 해당 위치로 자동 이동
    - 응답 코드 3xx에서 설명
    - 201 : Location 값은 요청에 의해 생성된 리소스 URI
    - 3xx : Location 값은 요청을 자동으로 리다이렉션 하기 위한 대상 리소스를 가리킴
    
  - Allow : 허용 가능한 HTTP 메서드
    - 405 (Method Not Allowed) 에서 응답에 포함해야함
    - Allow : GET, HEAD, PUT
    
  - Retry-After : 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
    - 503 : 서비스가 언제까지 불능인지 알려줄 수 있음
    - Retry-After : Fri, 15 Dec 2023 01:18:00 GMT(날짜표기)
    - Retry-After : 120 (초단위 표기)
    
 ### 인증
  - Authorization : 클라이언트 인증 정보를 서버에 전달
  - WWW-Authenticate : 리소스 접근 시 필요한 인증 방법 정의
    - 리소스 접근 시 필요한 인증 방법 정의
    - 401 Unauthorized 응답과 함께 사용
    - WWW-Authenticate : Newauth realm="apps", type=1, title="Login to \\"apps\\"", Basic realm="simple"
    
 ### 쿠키
 
 - 사용처 :
   - 사용자 로그인 세션 관리
   - 광고 정보 트래킹
 - 쿠키 정보는 항상 서버에 전송됨
   - 네트워크 트래픽 추가 유발
   - 최소한의 정보만 사용(세션ID, 인증토큰)
   - 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지(localStorage, sessionStorage) 참고
 - 주의!
   - 보안에 민감한 데이터는 저장 X
 
 - Set-Cookie : 서버에서 클라이언트로 쿠키 전달.(응답)
   - expires=Sat, 17-Dec-2023 04:39:21 GMT 
   - max-age= 3600(3600초) (0이나 음수면 쿠키 삭제)
   - 세션 쿠키 : 만료 날짜를 생략 하면 브라우저 종료시 까지만 유지
   - 영속 쿠키 : 만료 날짜를 입력하면 해당 날짜까지 유지
   
 - Cookie : 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달
   
 - 쿠키 - 보안
   - Secure
     - HTTPS 인 경우에만 쿠키 전송
     
   - HttpOnly
     - XSS 공격 방지
     - 자바스크립트에서 접근 불가
     - HTTP 전송에만 사용
     
   - SameSite
     - XSRF 공격 방지
     - 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송 
 
 