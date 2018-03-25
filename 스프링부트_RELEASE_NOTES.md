# 스프링 부트 2.0 Release


# Overview
스프링 부트 2.0 에서 변경 된 내용을 정리한다. 해당 글은 스프링 공식 GitHub 릴리스 노트 페이지를 참고한 것이다. 최대한 객관적으로 레퍼런스 문서를 참고할려고 했으나, 필자의 부족한 영어 실력 으로 인한, 번역상 오류가 있을 수는 있다. 

> 잘못된 부분이 있다면 피드백 부탁드립니다. 

[https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/](https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/)
[https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Release-Notes](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Release-Notes)
[https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Configuration-Changelog](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Configuration-Changelog) 


# 변경 사항

## Java 8 이상 버전만 지원
최소 자바8 을 사용해야 한다. 현재 프로젝트가 자바7 이라면, JDK 업그레이드를 해야만 스프링 부트 2.0 을 사용할 수 있다. 

## 스프링 프레임워크 5
스프링 프레임워크 5 가 적용 된다. 아래 링크에서 스프링 5에 대한 내용은 아래 링크를 참고하자. 
[https://github.com/spring-projects/spring-framework/wiki/What%27s-New-in-Spring-Framework-5.x](https://github.com/spring-projects/spring-framework/wiki/What%27s-New-in-Spring-Framework-5.x)

## 서드파티 라이브러리 
서드파티 라이브러리가 업그레이드 됐다. 

- Tomcat 8.5
- Flyway 5
- Hibernate 5.2
- Thymeleaf 3

## Reactive Spring
스프링의 많은 프로젝트에서는 리액티브 개발을 위한 지원을 제공하고 있다. 리액티브 애플리케이션은 비동기, Non-Blocking 하게 동작한다. 
[https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html](https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html)

스프링 부트 2.0 에서는 리액티브 애플리케이션 개발을 위한, 오토 컨피그레이션을 제공한다. 또한 기존에는 톰캣 임베디드만 제공했다면, 2.0 부터는 리액티브 환경을 위한 임베디드 서버 구성 지원을 한다. 

#### Spring WebFlux
WebFlux는 Non-Blocking 리액티브 프로그래밍이다.  스프링 부트는 WebFlux를 위한 오토 컨피그레이션을 제공하고, Functional(?) 프로그래밍을 할 수 있다.  *spring-boot-starter-webflux* 스타터를 사용하면 된다. 
[https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/#boot-features-webflux](https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/#boot-features-webflux)

#### Reactive Spring Data
Spring Data 는 리액티브 애플리케이션을 지원하는데, 카산드라, 몽고DB, 카우치베이스, 레디스 등에 대한 리액티브 API 지원을 한다. 

- spring-boot-starter-data-mongodb-reactive
- spring-boot-starter-data-cassandra-reactive
- spring-boot-starter-data-couchbase-reactive
- spring-boot-starter-data-redis-reactive

[https://github.com/spring-projects/spring-boot/tree/master/spring-boot-project/spring-boot-starters](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-project/spring-boot-starters)

#### 네티 서버
WebFlux 를 위해서, 임베디드 네티 서버를 제공한다. 


## HTTP/2 Support
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

#### Property Origins
[https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Release-Notes#property-origins](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Release-Notes#property-origins)

#### Converter Support
[https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Release-Notes#converter-support](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Release-Notes#converter-support)

## Gradle 플러그인 개선
Gradle 플러그인이 많이 변경되었는데, 최소 Gradle 4.X 이상 버전을 사용해야 한다. 

## 코틀린 지원
[https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/#boot-features-kotlin](https://docs.spring.io/spring-boot/docs/2.0.x-SNAPSHOT/reference/htmlsingle/#boot-features-kotlin)

## Actuator 개선


작성 중...
