# [Thymeleaf]Layout을 이용해 화면 구성하기(SpringBoot)

admin 자산관리 page를 작성하는 도중, 코드리뷰시간에 알아뒀으면 하는 부분으로 캐치해주셔서 간략히 파악해봄.

1. 레이아웃을 위한 Dependency 추가
implementation('nz.net.ultraq.thymeleaf:thymeleaf-layout-dialect')
 
타임리프를 위한 Dependency외에 위의 gradle을 추가해 줍니다.



2. 공통 양식 페이지 제작
2.1 NameSpace를 정의
2.2 공통양식 코드 작성

3. 본문 페이지 작성
3.1 html 태그에 layout:decorate 추가
3.2 본문영역 추가

4. 결과 페이지


![image](https://user-images.githubusercontent.com/104426801/172577182-2d313703-891f-4d87-91ae-ff6652835b90.png)


출처: https://chung-develop.tistory.com/7 [춍춍 블로그:티스토리]
