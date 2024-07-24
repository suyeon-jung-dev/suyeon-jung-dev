
### 고민해볼 것들.
- 패키지 설계
- 가시성 제어
  - `package-info.java`
  - java 11 이상만 제한해도 될지?
- GraphQL 서버(api-server) 유저 입장에서의 고민
  - 얼마나 커스텀 가능하게 열어둘 것인지
- artifact 분리가 필요한지?
- 의존성 추가시 신중하게.

### 찾아보기
- GraphQL java-sdk 오픈소스
- [Spring RestClient](https://github.com/spring-projects/spring-framework/tree/main/spring-web/src/main/java/org/springframework/http/client)
  - https://spring.io/blog/2023/07/13/new-in-spring-6-1-restclient
  - https://docs.spring.io/spring-framework/reference/integration/rest-clients.html#rest-restclient
### 참고하기
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