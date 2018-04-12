

# 스프링 부트 2.0 Release


# Overview
스프링 부트 2.0 에서 변경 된 내용을 정리한다. 해당 글은 스프링 공식 GitHub 릴리스 노트 페이지를 참고한 것이다. 최대한 객관적으로 레퍼런스 문서를 참고할려고 했으나, 필자의 부족한 영어 실력 으로 인한, 번역상 오류가 있을 수는 있다. 

> 잘못된 부분이 있다면 피드백 부탁드립니다. 

[https://spring.io/blog/2018/03/01/spring-boot-2-0-goes-ga](https://spring.io/blog/2018/03/01/spring-boot-2-0-goes-ga)  
[https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/](https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/)  
[https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Release-Notes](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Release-Notes)  
[https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Configuration-Changelog](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Configuration-Changelog)   
[http://www.baeldung.com/new-spring-boot-2](http://www.baeldung.com/new-spring-boot-2)  


스프링 공식 페이지에서는 주요 변경 사항을 아래와 같이 소개한다. 

- A Java 8 baseline, and Java 9 support.
- Reactive web programming support with Spring WebFlux/WebFlux.fn.
- Auto-configuration and starter POMs for reactive Spring Data Cassandra, MongoDB, Couchbase and Redis.
- Support for embedded Netty.
- HTTP/2 for Tomcat, Undertow and Jetty.
- Kotlin support.
- A brand new actuator architecture, with support for Spring MVC, WebFlux and Jersey.
- Micrometer based metrics with exporters for Atlas, Datadog, Ganglia, Graphite, Influx, JMX, New Relic, Prometheus, SignalFx, StatsD and Wavefront.
- Quartz scheduler support.
- Greatly simplified security auto-configuration.


# 스프링 부트 2.0 변경 사항

## Java 8 이상 버전만 지원
최소 자바8 을 사용해야 한다. 현재 프로젝트가 자바7 이하이면, JDK 업그레이드를 해야만 스프링 부트 2.0 을 사용할 수 있다. JDK9 에서도 테스트가 잘 되었기 때문에 Java9 을 도입하겠다면 스프링 부트 2.0 으로 반드시 업그레이드 하자. 

## Spring Framework 5.X
스프링 프레임워크 5 가 적용 된다. 아래 링크에서 스프링 5에 대한 내용은 아래 링크를 참고하자. 
[https://github.com/spring-projects/spring-framework/wiki/What%27s-New-in-Spring-Framework-5.x](https://github.com/spring-projects/spring-framework/wiki/What%27s-New-in-Spring-Framework-5.x)
다 아는 내용이지만, 가장 큰 특징은 Spring WebFlux 의 도입이다. 물론, Spring MVC 와 함께 사용할 수 있다. Framework 버전이 올라가면서 서드파티 라이브러리가 함께 업그레이드 됐다. 

**주요 업그레이드**
- Tomcat 8.5
- Flyway 5
- Hibernate 5.2
- Thymeleaf 3

**기타 Spring Framework 5.X Upgrade**
- Servlet 3.1 / 4.0
- JPA 2.1 / 2.2
- Bean Validation 1.1 / 2.0
- JMS 2.0
- JSON Binding API 1.0
- Jetty 9.4+
- WildFly 10+
- WebSphere 9+
- with the addition of Netty 4.1 and Undertow 1.4 for Spring WebFlux
- Jackson 2.9+
- EhCache 2.10+
- Hibernate 5.0+
- OkHttp 3.0+
- XmlUnit 2.0+

전부 나열하기엔 부끄러우니, 공식 링크를 참고하자. 
https://github.com/spring-projects/spring-framework/wiki/Upgrading-to-Spring-Framework-5.x


## Reactive Spring
스프링의 많은 프로젝트에서는 리액티브 개발을 위한 지원을 제공하고 있다. 리액티브 애플리케이션은 비동기, Non-Blocking 하게 동작한다. 스프링 부트 2.0 에서는 리액티브 애플리케이션 개발을 위한, 오토 컨피그레이션을 제공한다. 또한 기존에는 톰캣 임베디드만 제공했다면, 2.0 부터는 리액티브 환경을 위한 Netty 등의 임베디드 서버 구성 지원을 한다.
[https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html](https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html)


#### Spring WebFlux
WebFlux는 Non-Blocking 리액티브 프로그래밍이다.  스프링 부트는 WebFlux를 위한 오토 컨피그레이션을 제공하고, Functional하게 프로그래밍을 할 수 있다.  *spring-boot-starter-webflux* 스타터를 사용하면 된다. 
[https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/#boot-features-webflux](https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/#boot-features-webflux)

#### Reactive Spring Data
Spring Data 는 리액티브 애플리케이션을 지원하는데, 카산드라, 몽고DB, 카우치베이스, 레디스 등에 대한 리액티브 API 지원을 한다.

- spring-boot-starter-data-mongodb-reactive
- spring-boot-starter-data-cassandra-reactive
- spring-boot-starter-data-couchbase-reactive
- spring-boot-starter-data-redis-reactive

[https://github.com/spring-projects/spring-boot/tree/master/spring-boot-project/spring-boot-starters](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-project/spring-boot-starters)

#### 네티 서버
WebFlux 를 위해서, 임베디드 네티 서버를 제공한다. 참고로 Netty API 는 아래 링크를  참고하자. 
[http://projectreactor.io/docs/netty/release/api/](http://projectreactor.io/docs/netty/release/api/)



## HTTP/2 Support
스프링 부트 2.0에서는 HTTP/2 를 지원한다. 
```java
server.http2.enabled 
```
아 근데, HTTP/2 가 뭔지 알아야 한다. HTTP/2 는 HTTP 프로토콜의 두 번째 버전이다. 기존의 HTTP1.1과 호환성을 유지한다. 다음과 같은 특징이 있다. 

- HTTP 헤더 데이터 압축
- 서버 푸시 기술
- 요청을 HTTP 파이프라인으로 처리
- HTTP 1.X 의 HOL blocking 문제 해결
- TCP 연결 하나로 여러 요청을 다중화 처리 

이런 특징으로 인해서 네트워크 지연 시간을 줄이고, 웹브라우저 렌더링 속도를 향상시킬 것이다. HTTP/2 에 관련된 자세한 내용은 아래 링크를 참고하자. 
https://developers.google.com/web/fundamentals/performance/http2/?hl=ko

그리고 스프링 부트 2.0 에서의 HTTP/2 에 대한 내용은 아래 링크를 참고하자. 역시나 스프링 레퍼런스는 상세하게 나와있지 않다. ㅠㅠ
[https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/#howto-configure-http2](https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/#howto-configure-http2)


## Configuration Property Binding


#### Binder API
Binder(바인더) API는 프로퍼티 속성 값을 사용할 수 있다.  @ConfigurationProperties 스코프 밖에서도 사용할 수 있도록 제공한다. 

```java
List<PersonName> people = Binder.get(environment)
    .bind("custom.property", Bindable.listOf(PersonName.class))
    .orElseThrow(IllegalStateException::new);
```

```java
custom:
  property:
  - first-name: Sieun
    last-name: Kim
```

#### ConfigurationProperties
근데 이번에 ConfigurationProperties 어노테이션에 변경사항이 있다. 기존에는 underscore, camelcase 를 지원했지만, 부트2.0 에서부터는 소문자와 kebab-case만 지원한다. 참고로 kebab-case 는 하이픈(-) 으로 단어를 연결하는 방법이다. 근데, 기존의 속성 방식을 사용은 가능한 것 같다. 흠... 아직은 확 와닿지가 않는데, 

```java
spring.jpa.database-platform=mysql
spring.jpa.databasePlatform=mysql
spring.JPA.database_platform=mysql
```
위 속성 값들은 전부 아래의 형태로 매핑될 것 이다. 
```java
spring.jpa.databaseplatform=mysql
```
그래서 부트 레퍼런스에서는 kebab-case 를 소문자 조합으로 사용하는 것을 추천한다. 이렇게!!
> `my.property-name=foo`.

리스트 타입은 [] 를 사용하면 된다. 
```
spring.my-example.url[0]=http://example.com
spring.my-example.url[1]=http://spring.io
```
콤마도 지원한다. 
```
spring.my-example.urls=http://example.com,http://spring.io
```
yml 파일에 대해서도 대략 비슷한 거 같은데 자세히 확인은 못했다. 자세한 내용은 아래 링크를 참고하자. 
[https://github.com/spring-projects/spring-boot/wiki/Relaxed-Binding-2.0](https://github.com/spring-projects/spring-boot/wiki/Relaxed-Binding-2.0)

#### Property Origins
생략... 영어 번역이 잘 안되어서 정확히 무슨 내용인지 모르겠다. 
[https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Release-Notes#property-origins](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Release-Notes#property-origins)

#### Converter Support
생략... 영어 번역이 잘 안되어서 정확히 무슨 내용인지 모르겠다. 
[https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Release-Notes#converter-support](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Release-Notes#converter-support)


## Gradle 플러그인 개선
Gradle 플러그인이 많이 변경되었는데, 최소 Gradle 4.X 이상 버전을 사용해야 한다. 뭐가 많이 변경되었다는 걸까??? 

#### management plugin 디펜던시
부트 2.0 부터는 management plugin이 자동으로 추가되지 않는다. 부트 2.0 에서는 build.gradle 파일에 따로 설정을 해야 한다. 
```
apply plugin: 'org.springframework.boot'
apply plugin: 'io.spring.dependency-management' // <-- add this to your build.gradle
```

#### Building Executable Jars and Wars
bootRepackage 명령이 bootjar 와 bootwar 로 대체 된다. 
https://docs.spring.io/spring-boot/docs/current/gradle-plugin/api/org/springframework/boot/gradle/tasks/bundling/BootJar.html

#### 레퍼런스
일단 상세한 Gradle Plugin 에 대한 레퍼런스는 아래 링크를 참고하자.  
[https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/gradle-plugin/reference/html/](https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/gradle-plugin/reference/html/)



## 코틀린 지원
디펜던시로 org.jetbrains.kotlin:kotlin-stdlib-jdk8 , org.jetbrains.kotlin:kotlin-reflect 등을 추가해야 한다. 자세한 설정은 아래 링크를 통해서 참고하자. 
https://start.spring.io/#!language=kotlin


상세한 내용은 생략한다. 레퍼런스 문서를 참고하자 
[https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/#boot-features-kotlin](https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/#boot-features-kotlin)

[https://docs.spring.io/spring/docs/5.0.5.RELEASE/spring-framework-reference/languages.html#kotlin](https://docs.spring.io/spring/docs/5.0.5.RELEASE/spring-framework-reference/languages.html#kotlin)

## Actuator 개선
[https://docs.spring.io/spring-boot/docs/current-SNAPSHOT/actuator-api/html/](https://docs.spring.io/spring-boot/docs/current-SNAPSHOT/actuator-api/html/)

## Data Support

#### 커넥션 풀
부트 2.0에서 기본 데이터베이스 커넥션 풀이 톰캣에서 HikariCP 로 변경 되었다. HikariCP 는 매우 뛰어난 성능과 속도를 제공한다고 한다. 

#### 데이터베이스 스키마 초기화
데이터베이스 초기화 로직이 계층화되었다. 스프링 배치, Spring Integration, 스프링 세션, 쿼츠 등 임베디드 DB 를 사용하는 경우에만 기본으로 제공한다. 

```java
//예
spring.quartz.jdbc.schema=always
spring.batch.initialize-schema=always
spring.session.jdbc.initialize-schema
... 
//등등
```

#### JOOQ
생략



## Quartz (쿼츠)
쿼츠 스케쥴러 라이브러리에 대한 스타터를 제공한다. 
[https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/#boot-features-quartz](https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/#boot-features-quartz)


## Animated ASCII Art
마지막으로, 중요한 내용은 아니지만 스프링 부트 실행시에 GIF 배너를 표현할 수 있다. 
https://github.com/snicoll-demos/demo-animated-banner

