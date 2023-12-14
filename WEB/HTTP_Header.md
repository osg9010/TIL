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