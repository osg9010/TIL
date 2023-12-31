# HTTP 헤더 2

## 캐시 기본 동작

### 1. 캐시가 없을 때
 - 데이터가 변경되지 않아도 계속 네트워크를 통해서 데이터를 다운로드 받아야 한다.
 - 인터넷 네트워크는 매우 느리고 비싸다.
 - 브라우저 로딩 속도가 느리다.
 - 느린 사용자 경험
 
### 2. 캐시 적용
 - 캐시 덕분에 캐시 가능 시간동안 네트워크를 사용하지 않아도 된다.
 - 비싼 네트워크 사용량을 줄일 수 있다.
 - 브라우저 로딩 속도가 매우 빠르다.
 - 빠른 사용자 경험
 
### 3. 캐시 시간 초과
 - 캐시 유효 시간이 초과하면, 서버를 통해 ㄷ데이터를 다시 조회하고, 캐시를 갱신한다.
 - 이때 다시 네트워크 다운로드가 발생한다.
 
 1. 서버에서 기존 데이터를 변경함 
 2. 서버에서 기존 데이터를 변경하지 않음
 
   - 검증 헤더 추가
     - Last-Modified : 검증 헤더 (응답)
     - If-modified-since : 조건부 요청 (요청)
     
   - 캐시 유효 시간이 초과해도, 서버의 데이터가 갱신되지 않으면 304 Not Modified + 헤더 메타정보만 응답 바디 X
   - 클라이언트는 서버가 보낸 응답 헤더 정보로 캐시의 메타 정보를 갱신
   - 클라이언트는 캐시에 저장되어 있는 데이터 재활용
   - 결과적으로 네트워크 다운로드가 발생하지만 용량이 적은 헤더 정보만 다운로드
   - 매우 실용적임
  
 ### 검증 헤더와 조건부 요청
 
 1 검증 헤더
  - Last-Modified <-> If-modified-since
  - ETag <-> If-None-Match
  
 2 조건부 요청
 - If-modified-since
 - If-None-Match
 
 3 예시
  - 데이터 미변경 시
    - 캐시와 서버가 같은 값일 경우 304 응답, 헤더 데이터만 전송
    - 전송 용량 0.1M(헤더0.1M, 바디 1.0M)
    
  - 데이터 변경 시
    - 캐시와 서버가 다른 값일 경우 200 응답, 모든 데이터 전송
    - 전송 용량 1.1M(헤더0.1M, 바디 1.0M)
    
 4 서버에서 별도의 캐시 로직을 관리하고 싶은 경우
   - 예) 스페이스나 주석처럼 크게 영향이 없는 변경에서 캐시를 유지하고 싶은 경우
   
   - ETag (Entity Tag) 를 통해 해결 가능하다.
     - 단순하게 ETag 값을 서버에 보내서 같으면 유지, 다르면 다시 받는다.
     - 캐시 제어 로직을 서버에서 완전히 관리
     - 클라이언트는 단순히 이 값을 서버에 제공 (클라이언트는 캐시 메커니즘을 모름)
     - 예) 
       - 서버는 배타 오픈기간동안 파일이 변경되어도 ETag 값을 동일하게 유지
       - 애플리케이션 배포 주기에 맞추어 ETag 모두 갱신
       
 ### 캐시 제어 헤더
 - Cache-Control*** : 캐시 제어
   - max-age : 캐시 유효 시간, 초 단위
   - no-cache : 데이터는 캐시해도 되지만, 항상 원(origin) 서버에 검증하고 사용
   - no-store : 데이터에 민감한 정보가 있음으로 저장하면 안됨(메모리에서 사용 후 빨리 삭제)
   - 프록시
     - public : 응답이 public 캐시에 저장되어도 됨
     - private : private 캐시에 저장되어야 함
     - s-maxage : 프록시 캐시에만 적용되는 max-age
     - Age:60 (HTTP 헤더) : 오리진 서버에서 응답 후 프록시 캐시 내에 머문 시간(초)
   
 - Pragma : 캐시 제어 (하위 호환) - HTTP/1.0    
   
 - Expires : 캐시 유효 기간 (하위 호환) - HTTP/1.0
 
 
### 캐시 무효화
 - Cache-Control
   - no-cache : 데이터는 캐시해도 되지만, 항상 원 서버에 검증하고 사용
   - no-store : 저장하면 안됨(메모리에서 사용 후 빨리 삭제)
   - must-revalidate : 
     - 캐시 만료 후 최초 조회 시 원 서버에 검증해야함
     - 원 서버에 접근 실패시 반드시 504 (Gateway Timeout) 이 발생 해야함
   
   - no-cache vs must-revalidate
     - no-cache : 원 서버에 네트워크 접속 실패 시 경우에 따라 프록시 서버에서 200을 내려서 오래된 데이터라도 보여줄 수 있음
     - must-revalidate : 원 서버 네트워크 접속 실패 시에는 무조건 504 에러 발생
   
   
 - Pragma
   - no-cache : HTTP/1.0 (하위호환)
   
 
 