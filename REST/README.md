RESTful API 설계 가이드의 제목을 보면 REST API 설계 가이드가 아닌 RESTful API 설계 가이드인 것을 확인할 수 있다. 
RESTful이란 REST 설계 원리로 구성된 시스템을 말한다. (RESTful의 공식적인 표준은 없다) 
공식적인 표준이 없기 때문에 REST API를 잘 모른다면 https://restfulapi.net의 내용을 토대로 REST API를 설계 구축해보자

## Restful API 

## 당신의 Restful API 가 아닌 5가지 단서

1. 한 가지 URL만 가지고 있는 경우
예를 들어 모든 요청이 http:///example.com/rest 로 구성되어 있다면 그것은 Restful하지 않다.
REST 자원의 핸들링 표현 그 자체이다. 각 자신의 URI에 의해 표현되고 그 자체를 직접 사용한다.

2. 모든 요청이 POSTs 인 경우
POST 요청은 당연히 Restful service이지만 만약 API에 대한 모든 요청들이 POST사용을 한다면 Resful하지 않을 것이다.
POST 요청은 새로운 자원을 만드므로, 모든 상황이 그러하다면 좋다. 만약 조회하는 것이라면 Resful service가 아니다.

3. 응답 메타데이터가 header가 아닌, body에 있는 경우
어떠한 데이터라도 응답 body 안에 status = successs를 가지고 있다면 Resful하지 않다.
REST는 HTTP 포맷의 이점을 가지며 headers에 모든 요청과 응답 메타데이터를 넣는다. body에서는 자원만 나타낼 뿐이다.

4. URL에 동사가 있는 경우
미묘하겠지만 subresources의 경우 극명하다. URL이 /item/42/activate 라면 /item/42/status 더 좋은 대안이다.
REST는 자원을 다루고 activate는 자원이 아니다.

5. URL이 method 이름을 포함하고 있는 경우

가장 분명하게 non-Restful한 부분은 ?action=getRecentItems 와 같은 부분을 가진 URL이다. 때때로 이러한 단서는 다른 단서를 지니고 있다.
method 이름이 body message 안에도 포함될 것이다. 분명히 Restful하지 않다.


### 우리는 RESTfulness를 신경쓰는가?
얼마나 이 API가 유용한지는 얼마나 RESTful한가와 전혀 상관이 없다고 생각한다. "HTTP 전송 데이터" Application을 설명할 때는 
Restful을 신경써야한다. 그렇지 않을 수도 있기때문에.
REST를 포함하는 어떤 것이든 살펴봐라. 왜냐하면 REST는 때때로 채택되기 매우 어려운 아주 구체적인 기준을 가지고 있다. 그래서 이러한 주제에
관심있는 사람들은 다른 이에게 그들이 틀렸다는 것을 말하는 것을 좋아한다




