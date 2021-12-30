>  [J2EE](https://cheershennah.tistory.com/74)란? (=[Java EE](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=mk1126sj&logNo=220970553716))
>
>  Java 2 Enterprise Edition으로 자바 기술로 기업 환경의 어플리케이션을 만드는 데 필요한 스펙의 집합이다. J2EE를 만든것은 Sun Microsystems이고 SUN에서 J2EE스펙을 시범적으로 구현하지만 Java진영 여러 개발자들이 같이 만들어가고 공유하는 기술이라고 볼수있다.
>
>  
>
>  엔터프라이즈 시스템이란?
>
>  서버에서 동작하며 기업과 조직의 업무를 처리해주는 시스템이다. 많은 사용자들의 요청을 동시 처리해야 하므로 서버 자원을 효율적으로 공유하고 분배해서 사용할 수 있어야 한다. 또 기업의 핵심 정보를 다루기때문에 보안, 안정성, 확장성이 요구된다.

<BR>

자바로 엔터프라이즈 애플리케이션을 개발하는 방법은 **E**nterprise**J**ava**B**ean를 사용하는 것이 있었다.

애플리케이션에는 (비즈니스와 관련된) 객체가 많다. *객체를 관리하는 컨테이너를 만들어* 필요할 때마다 **컨테이너로부터 객체를 받는 식으로 관리하면 좋겠다**라는 생각으로 **EJB가 탄생**하였다.  EJB의 등장으로 개발자는 비즈니스 로직에 집중할 수 있는 환경을 갖추었지만 ***그럼에도 기업형 애플리케이션을 EJB로 개발하는 것은 어려웠다***.

1. 너무 많은 작업 수행을 개발자에게 요구했다.

2. 객체지향적인 특징과 장점을 포기해야 했다.  

   EJB 빈은 상속과 다형성등의 혜택을 제대로 누릴 수가 없다. 

3. 실제 비즈니스 로직보다 EJB 컨테이너를 사용하기 위한 코드들이 많다는 문제가 발생했다.

   EJB는 침투적이다. EJB 애플리케이션은 개발의 복잡도를 제거했지만 한편으로 더 많은 문제와 복잡성을 가지고 왔다.

   > 침투적이라는 것은 특정 기술을 적용하려면 그 기술에서 하라는 대로 무언가를 해 주어야 하는 것이다. Spring은 비침투적인 반면 EJB는 침투적이다.

컨테이너로부터 객체를 받는 식으로 관리하면 좋겠다는 생각. 👉  Enterprise 개발을 단순화하기 위해 EJB 탄생. 👉 여전히 개발이 어려움.

<br>

이런 어려움이 있던 시기를 개발자들은 **Java의 겨울**에 비유했고 새로 나온 J2EE Framework를 그 *겨울이 끝나고 봄이 찾아오게 될 것*이라는 의미로 🌱 ***스프링***이라고 이름 짓는다. 특정 기술에 종속되지 않고 (기술 비침투적) 객체를 관리할 수 있는 컨테이너를 제공하는 것이 스프링의 [기본 철학](https://victorydntmd.tistory.com/158)이다.

<br>

## Spring Framework

**자바 엔터프라이즈 개발을 편리하게 해주는 오픈 소스 경량급 애플리케이션 프레임워크**이다.

> 라이브러리나 프레임워크는 일반적으로 특정 문제에 대한 불편함을 해소시키고자 등장한다. 하지만 스프링은 애플리케이션 프레임 워크라는 단어를 사용한다.
>
> 애플리케이션 프레임워크? 이는 어플리케이션 전체에서 발생하는 불편함을 해소하고자 한다는 의미이다. 
>
> **경량급**? 불필요하게 무겁지 않다는 의미이다. 다양한 기능을 제공해 코드 수는 엄청나다. 하지만 해당 기능을 제공하기 위해서 최소한의 코드만 포함되어 있다고 생각해도 좋을 것 같다.
>
> 애플리케이션을 개발할 때 기술적인 복잡성과, 비즈니스 로직의 복잡성 두 가지의 문제가 존재하고 이 둘이 합쳐졌을 때 복잡도는 엄청나게 증가했다. 스프링은 이 둘을 분리하기 위해 로우 레벨의 기술을 분리하고 추상화하여 개발자가 비즈니스 로직에만 집중할 수 있도록 해주었다. 이 과정에서 추가적인 복잡함을 만들어내지 않는 것도 스프링의 장점이다.

엔터프라이즈의 개발이 편리하지 않았기 때문에 스프링이 나타났다. 역시 스프링의 목적은 엔터프라이즈 애플리케이션 개발을 편하게 하는 것이다. 현재 전자정부 프레임워크 (eGov)가 스프링을 기반으로 하여 만들어졌다.

> 전자 정부 표준 프레임워크는 국가에서 공공기관 웹 프로젝트 제작 시 사용할 수 있도록 만든 프레임워크다. 자바 기반의 웹 프로젝트의 개발과 운영에 있어 필요한 기본적인 기능들을 국가적으로 표준화해 만들었다.

[복잡함을 상대하는 스프링 전략에 대해 다른 분이 정리한 글이다.](https://ee-22-joo.tistory.com/7)

[왜 스프링을 사용할까에 관해 다른 분이 정리한 글이다.](https://seolin.tistory.com/119)

<BR>

### DI와 IOC

스프링의 가장 좋은 기능 중 하나는 DI를 지원해 **느슨하게 결합된 애플리케이션을 개발**할 수 있다는 것이다. 이렇게 하면 한 클래스를 수정했을 때 다른 클래스를 수정해야 하는 상황을 막아준다. (느슨하게 개발된 애플리케이션은 쉽게 단위 테스트를 할 수 있다.) 개발자가 *직접 객체를 생성하고 관리하던 것을 Spring의 IOC Container가 대신 해 준다*.

<**의존성 주입이 없는 [예시](https://centbin-dev.tistory.com/45)**>

아래를 보면 A는 `new`를 사용하여 B에 의존한다.

```java
class A {
    private B b;
    
    public A() {
        this.b = new B();
    }
}
```

<**의존성 주입이 있는 [예시](https://dzone.com/articles/spring-vs-spring-boot)**>

@Component나 @Autowired 같은 애노테이션으로 쉽게 B를 얻을 수 있다. 이는 밀접하게 결합되지 않는다.

```java
@Autowired
private B b;
```

```java
public class A {
	private final B b;

	@Autowired
	public A(B b) {
		this.b = B;
	}
}
```

이렇게 하면 B가 변화되더라도 A는 변경할 필요가 없어진다.

<BR>

스프링이 가지고 있는 장점 잘 알았다. 그러면 Spring Boot는 왜 쓸까?

## Spring Boot

스프링 프레임워크는 기능이 많은 만큼 [환경 설정이 복잡한 편](https://sas-study.tistory.com/274)이다. 이에 어려움을 느끼는 사용자들을 위해 나온 것이 바로 스프링 부트다. 스프링 부트는 **스프링 프레임워크를 사용하기 위한 설정의 많은 부분을 자동화**하여 ***사용자가 정말 편하게 스프링을 활용할 수 있도록 돕는다***.

> ***Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".***

<br>

### 설정 자동화: Spring Boot Starter

1. **설정 자동화.**
2. **라이브러리 버전 자동 관리.**

Spring에서는 여러 의존성을 xml 파일에 직접 설정해야했다. Spring Boot는 Starter을 이용해 프로젝트에 설정해야 할 다수의 의존성들을 사전에 미리 정의해 제공한다.

[예](https://lifeinprogram.tistory.com/7)) `spring-boot-starter-jpa` 모듈을 추가함으로써 jpa를 사용하는데 필요한 모듈을 따로 정리하고 관리할 필요가 없다. `spring-boot-starter-web` 모듈을 추가함으로써 json, webmbc의 모듈은 따로 관리할 필요가 없다. 

그리고 버전 충돌 문제도 해결해 준다. 프로젝트 시작 시 다양한 라이브러리를 사용하게 되면 라이브러리 버전 간 충돌 문제가 발생할 수 있는데 starter을 사용하면 의존성 버전도 권장 버전으로 자동 설정된다. 따라서 **개발자는 버전 충돌 문제를 피할 수 있고 의존성을 설정하기 훨씬 쉬워진다**.

[start에 있는 설정이 어떻게 자동으로 적용되는걸까.](https://velog.io/@adam2/SpringBoot-%EC%9E%90%EB%8F%99-%ED%99%98%EA%B2%BD-%EC%84%A4%EC%A0%95AutoConfiguration)

<br>

### 내장 톰캣

외부 라이브러리로 포함된 `org.springframework.boot.autoconfigure.web.servlet` 에서 `ServletWebServerFactoryAutoConfiguration.java` 를 열어보면 내장 Tomcat을 사용할지, Jetty를 사용할지, Undertow를 사용할지에 대한 설정이 있다.

`org.springframework.boot.web.embedded.tomcat` 에서 `TomcatServletWebServerFactory.java` 를 열어보면 톰캣을 생성하는 코드가 있다. 즉, 자동 설정 안에 톰캣과 서블릿 등 웹 서버 기본 설정들이 포함되어 있고, 따라서 단지 main()을 실행하는 방식으로 톰캣이 생성되고 서블릿이 추가되어 서버를 구동할 수 있다. [톰캣이 아닌 다른 서버를 사용할 수도 있다.](https://velog.io/@dsunni/Spring-Boot-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%EC%9B%90%EB%A6%AC-%EB%82%B4%EC%9E%A5-%EC%84%9C%EB%B2%84-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88%EC%99%80-%ED%8F%AC%ED%8A%B8) 

=> **Jar 형식을 사용하여 배포할 수 있다.**

웹 프로젝트라면 War 파일로 패키징을 해야하는데 Spring Boot는 내장 톰캣을 지원하기 때문에 Jar 파일로 패키징해서도 웹 애플리케이션을 실행시킬 수 있다.

[이 외의 장점들.](https://sas-study.tistory.com/299)

<br>

## Gradle vs Maven

***Why do I use Gradle?***

Maven은 pom.xml을 이용한 정형화된 빌드 시스템이다. Apache의 이름 하에 Ant를 사용하던 개바자들의 불편함을 해소하고 부가기능을 추가했다.

Gradle은 Groovy 문법을 사용하고 Groovy는 JVM에서 실행되는 스크립트 언어로 문법이 자바와 [가깝다](https://galid1.tistory.com/647).

XML으로 Build를 정의하기엔 설정 내용이 길어지고 가독성이 떨어진다. 또 Gradle이 Maven보다 훨씬 [빠르다](https://gradle.org/gradle-vs-maven-performance/).

그럼에도 현재 Maven이 Gradle보다 사용률이 앞서는 이유는 단지 러닝커브 때문인 것 같다.

<br>

## WAR vs JAR

**J**ava **AR**chive는 path 정보를 유지한 상태로 압축한다. Java 클래스 파일과, 각 클래스들이 사용하는 관련 리소스파일 및 메타데이터를 압축한 파일이다. = **클래스 파일을 압축**.

> 여기서 [메타데이터란?](https://scshim.tistory.com/265)
>
> 애플리케이션이 처리해야할 데이터가 아닌 컴파일 과정과 실행 과정에서  코드를 어떻게 컴파일하고 처리할 것인지 알려주는 정보이다. ex 애노테이션

**W**eb application **AR**chive는 웹 프로젝트에서 배포를 위한 최소한의 단위이다. 그래서 웹 애플리케이션을 어떻게 설정할 지에 대한 정의가 있는 web.xml 파일이 있고, application을 구성할 때 필요한 자원을(자바 서블릿, 정적 웹페이지 등) 압축한 Jar 파일이다. [war](https://goodgid.github.io/Jar-vs-War/)로 올리면 WAS (Web Application Server)가 압축을 해제하여 배포해준다. (web.xml이 있는 이유.) = **웹 애플리케이션을 통째로 압축**.

***Jar가 가장 적은 압축 범위를 가지고 있고 War은 Jar의 모든 파일 + War만의 파일을 더 압축한다***.
