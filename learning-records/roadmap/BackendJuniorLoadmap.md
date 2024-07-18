# BackEnd Roadmap for java

```mermaid

graph TD
        Language:::red
    --> lang1[1. Java의 정석 - 남궁성]
    Language --> lang2[2. JAVA 언어로 배우는 디자인 패턴 입문 - 유키 히로시]
    lang1 & lang2 --> lang3[3. Effective Java - 조슈아 블로치] 
%%    lang3 --> lang4[ 절판도서 : java nio 관련 선택: JDK 1.4 튜토리얼 - 그레고리 M.트라비스]:::gray
    lang3 --> 
    oop[OOP]:::red
    oop --> oop1[ 선택: 객체지향의 사실과 오해 - 조영호]
    oop1 --> oop2[ 1. link: 조영호님의 우아한 객체지향 https://www.youtube.com/watch?v=dJ5C4qRqAgA ]
    oop1 --> oop3[ 2. 오브젝트 - 조영호]
    oop2 & oop3 --> 
    ddd[DDD :: MSA]:::red
    ddd --> ddd1[1. 도메인 주도 설계 - 에릭 에반스]
    ddd1 --> ddd2[2. 도메인 주도 설계 구현 - 반 버논]
   
    
    classDef red stroke:#f00
    classDef blue stroke:#00f
    classDef gray stroke:#808080

```

- 객체지향의 사실과 오해, 오브젝트 저자이신 조영호님의 우아한 객체지향 강의 링크 : https://www.youtube.com/watch?v=dJ5C4qRqAgA
    - 꼭 한번 보시길 추천드립니다! DDD 에 대한 직접적인 언급은 하지 않으셨지만 DDD 로 설계하는 기법에 대해 설명하고 계십니다.
- 아아.. [[JAVA 언어로 배우는 디자인 패턴 입문 - 유키 히로시](https://www.yes24.com/Product/Goods/115576266)] 는 신판이 나왔으니 꼭 신판으로 보세요! 요즘 트렌트에 맞게 더욱 자세히 설명 되어 있습니다.
- 오브젝트 - 조영호
    - 객체지향의 설계와 구현, 기본적인 원칙(SOLID, DRY, KISS 등)에 대해 자세히 다룹니다.
- [도메인 주도 설계 - 에릭 에반스](https://www.yes24.com/Product/Goods/5312881)
    - 실제 코드보다는 DDD에 대한 이론에 대해 다룹니다.
- [도메인 주도 설계 구현 - 반 버논](https://www.yes24.com/Product/Goods/25100510)
    - 위의 [[도메인 주도 설계 - 에릭 에반스](https://www.yes24.com/Product/Goods/5312881)] 를 기반으로 한 직접적인 구현에 대해 다루고 있습니다.
- 가상 면접 사례로 배우는 대규모 시스템 설계 기초 1
    - 기본적인 인프라 아키텍처에 대한 설계부터 분산시스템 설계 기법 및 알고리즘에 대해 다룹니다.
- 가상 면접 사례로 배우는 대규모 시스템 설계 기초 2
    - Database 에 대한 기반지식을 탄탄히 다지고 2권을 읽으시길 추천드립니다.

## System Architecture & Distributed System

```mermaid
graph TD
  DataBase[Database :: 분산시스템]:::red
    --> db1[RealMySql 8.0 - 백은빈,이성욱 :: inflearn 강의 참고]
    db1 --> db2[Database Internals - 알렉스 페트로프]
    db2 --> db3[데이터 중심 애플리케이션 설계 - 마틴 클레프만]:::gray
    
    

    Architectue[System 설계]:::red
    --> arch1[가상면접 사례로 배우는 대규모 시스템 설계 기초 1]
    arch1 --> arch2[가상면접 사례로 배우는 대규모 시스템 설계 기초 2]:::gray
    db3 --> arch2
    
    
		API[API 설계]:::red 
			API ---> api1[MSA, DDD :: 웹 API 설계 원칙 - 제임스 히긴보텀]
			
    
    classDef red stroke:#f00
    classDef blue stroke:#00f
    classDef gray stroke:#808080
```

## DevOps Roadmap

```mermaid

graph TD
    Network:::red
    --> network1[IT 엔지니어를 위한 네트워크 입문 - 고재성]
    network1 --> network2[...]
    network2 --> network3[ 비동기 함수형 프로그래밍; JAVA NIO, epoll 관련 참고 :: 리눅스 시스템 네트워크 프로그래밍 - 김선영]:::gray
    
    
    DevOps[Devops]:::blue --> Network
    DevOps --> OS[OS]:::blue --> os1[진리의 공룡책]
    DevOps --> Infra[인프라 입문]:::blue
    Infra --> devops1[그림으로 공부하는 IT 인프라 구조 - 야마자키 야스시]
    DevOps --> Kube[Docker/Kubernetes]:::blue
    Kube --> kube1[시작하세요! 도커/쿠버네티스 - 용찬호]
    kube1 --> kube2[쿠버네티스 인 액션 - 마르코 룩샤]
    kube2 --> kube3[쿠버네티스를 활용한 클라우드 네이티브 데브옵스 - 존 어런들]
%%    DevOps --> CICD["`CI/CD`"]
%%    CICD --> cicd1[젠킨스 2 시작하기 - 브렌트 래스터]

    classDef red stroke:#f00
    classDef blue stroke:#00f
    classDef gray stroke:#808080
    

```

1. 가장먼저 인프라의 전체적인 흐름에 대해 지식을 쌓는것을 추천드립니다. [그림으로 공부하는 IT 인프라 구조 - 야마자키 야스시]
2. 이후에 본인이 부족하다고 느끼는 기반지식을 습득하면 좋습니다.
    1. 네트워크, 운영체제 등
3. 그리고 필요하다면(업무에) 도커와 쿠버네티스 관련 기반지식을 쌓는 것을 추천드립니다. (DevOps 는 백엔드의 기본이 되어가고 있습니다.)


## Data Engineering Roadmap [작성중]

```mermaid
graph TD
    DE[Data Engineering]:::red
    --> de1[견고한 데이터 엔지니어링 - 조 라이스, 맷 하우슬리]
    de1 --> de2[...]
    de2 --> deLast[엔터프라이즈 데이터 플랫폼 구축 - 얀 쿠닉크]
    
    DDD:::red
    --> de2
    
    Hadoop[Hadoop Echosystem]:::red
    Hadoop --> Spark
    Spark --> deLast

    classDef red stroke:#f00
    classDef blue stroke:#00f
    classDef gray stroke:#808080
```


마지막으로..

이정도 공부한다면 앞으로 본인이 어떤 것을 추가적으로 습득해야하는지 그려질 것입니다! 화이팅!!