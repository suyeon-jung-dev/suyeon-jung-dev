
### 고민해볼 것들.
- 패키지 설계
- 가시성 제어
  - `package-info.java`
  - java 11 이상만 제한해도 될지?
- GraphQL 서버(api-server) 유저 입장에서의 고민
  - 얼마나 커스텀 가능하게 열어둘 것인지
- artifact 분리가 필요한지?
- 의존성 추가시 신중하게.

[java-sdk 개발시 주의할 점 - about Multi threading]
1.
syncronized 사용하지 말자.
자바 17버전 에서 지원하는 virtual thread는 동기화가 안되기 때문..!

2.
cas compare and swap

atomic integer 대신
lonng adder 사용하는게 낫다. (성능상 이점이 있다고 한다.)
adder, Accumulator 로 끝내는 클래스를 사용

3.
thread executor graceful 하게 종료하는 방법
https://easywritten.com/post/best-way-to-shutdown-executor-service-in-java/



### 찾아보기
- GraphQL java-sdk 오픈소스
- [Spring RestClient](https://github.com/spring-projects/spring-framework/tree/main/spring-web/src/main/java/org/springframework/http/client)
  - https://spring.io/blog/2023/07/13/new-in-spring-6-1-restclient
  - https://docs.spring.io/spring-framework/reference/integration/rest-clients.html#rest-restclient
### 참고하기 - GraphQL
- [Building Beyond Boundaries: A Developer's Guide to Crafting Custom SDKs in Java](https://blogs.halodoc.io/sdks-in-action-real-world-examples-of-java-sdk-success-stories/)
- [IBM - SDK Developer's Guide](https://www.ibm.com/docs/en/taddm/7.3.0?topic=integration-sdk-developers-guide)
- [참고할만한 도서일까?](https://product.kyobobook.co.kr/detail/S000003573657)
- Spring for GraphQL > https://spring.io/projects/spring-graphql
- GitHub > spring-project/spring-graphql > https://github.com/spring-projects/spring-graphql
- spring-graphql based on > https://www.graphql-java.com/
  - GraphQL Java - Getting stated > https://www.graphql-java.com/documentation/getting-started/
    - It required at least `java 11`
- Spring Getting Started GraphQL > https://spring.io/guides/gs/graphql-server
- GitHub > spring-projects/spring-graphql-examples > https://github.com/spring-projects/spring-graphql-examples

### SDK implementation
- [클라이언트 SDK 구현](https://learn.microsoft.com/ko-kr/azure/architecture/best-practices/api-implementation?source=recommendations#implement-a-client-sdk)
- [Azure SDK client guidelines](https://azure.github.io/azure-sdk/general_azurecore.html)


## java-sdk project proposal

[멘토님이 생각하신 스펙]
- maven >> maven repository 등록 목적으로 일단 maven 기반 채택
- java 17 로 일단 먼저 시작

---
[요구사항]
함수형으로 만들면 좋을 것 같다
메소드 체이닝 하도록 (빌더로)

옵셔널한 정보는 최대한 빼거나 추가하거나

코드가 

grpahqlql 을 직접 호출하는게 아니라 nginx proxy 먼저 호출
frontend proxy rk duffudlTdma

auth server 구조
- grpc 
- rest api

admin 접속시 api token 발급하는
litmus api token 이 있는데,
모든 request 에 barer 붙여주게 하면 된다.

참고 자료
https://docs.litmuschaos.io/docs/integrations/backstage 

---
[작업 절차]
auth 
project 를 먼저 구현하는게 좋다 >> release - 0.1.0 

operation management >> 

그 전에 
proposal 작성하면서 어떻게 sdk 만들지

---
[proposal]
- 이 프로젝트로 무엇을 할 것인지 목표를 명확하게 제시

참고
https://github.com/litmuschaos/litmus/blob/master/proposals/backstage-plugin.md

