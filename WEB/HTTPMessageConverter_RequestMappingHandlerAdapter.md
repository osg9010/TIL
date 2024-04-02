# HTTP 메시지 컨버터

- canRead() , canWrite() : 메시지 컨버터가 해당 클래스, 미디어타입을 지원하는지 체크
- read() , write() : 메시지 컨버터를 통해서 메시지를 읽고 쓰는 기능

## 우선순위
- 1 ByteArrayHttpMessageConverter : 클래스 타입: byte[] , 미디어타입: \*/\* 
- 2 StringHttpMessageConverter : 클래스 타입: String , 미디어타입: \*/\*
- 3 MappingJackson2HttpMessageConverter : 클래스 타입: 객체 또는 HashMap , 미디어타입 application/json

## 스프링 MVC는 다음의 경우에 HTTP 메시지 컨버터를 적용한다.
- HTTP 요청: @RequestBody , HttpEntity(RequestEntity) ,
- HTTP 응답: @ResponseBody , HttpEntity(ResponseEntity) , 

# 요청 맵핑 핸들러 어댑더 구조

###ArgumentResolver (HandlerMethodArgumentResolver)
- ArgumentResolver 를 호출하며 컨트롤러(핸들러) 가 파라미터 처리에 필요한 다양한 값들을 생성한다.

### 동작 방식
- ArgumentResolver 의 supportsParameter() 를 호출해서 해당 파라미터를 지원하는지 체크하고, 지원하면
 resolveArgument() 를 호출해서 실제 객체를 생성한다. 그리고 이렇게 생성된 객체가 컨트롤러 호출시 넘어가는
 것이다.

- ArgumentResolver 자체적으로 해결 불가능할 경우 HTTP 메시지 컨버터를 통해 해결한다.


# HTTP 메시지 컨버터 위치
- 스프링 MVC는 @RequestBody @ResponseBody 가 있으면 RequestResponseBodyMethodProcessor()
  HttpEntity 가 있으면 HttpEntityMethodProcessor() 를 사용한다.
  
  
