나는 CORS를 그냥 에러...의 한 종류라고 생각했다. 아주 단단히 오해를 하고 있었던 것이다. 그리고 이런 오해를 하고 있는 사람들이 많을 것이라고 생각한다. CORS는 자신도 모르게 많은 미움을 받았을 것이다. 그래서 우리는 CORS에 대해 정확히 알아야 한다.

<br>

# CORS

***Cross-Origin Resource Sharing***의 약자로 W3C에서 내놓은 *정책*이다.

> W3C (*World Wide Web Consortium*)
>
> W3C 의 규약 중 CORS 관련 규약이 존재한다. 이것을 각 브라우저 벤더들(크롬을 만드는 구글, IE를 만드는 마이크로소프트, 파이어폭스를 만드는 모질라 등등, 사파리를 만드는 애플 등등..)이 읽어보고 규약에 맞추어 브라우저를 만들게 된다.

<br>

Cross-Origin Resource Sharing는, Cross-Origin(다른 출처)의 Resrouce를 공유하는 정책이라고 해석할 수 있다. 우리가 마주치 거의 모든 CORS 관련 이슈는 이런 CORS 정책 위반에서 비롯된다. 

<br>

## SOP

***Same-Origin Policy***는 같은 출처에서만 리소스를 공유할 수 있다는 규칙이다. 브라우저에서 다른 서버에 요청할 경우에 해당되고, 브라우저를 거치지 않고 서버간 통신을 할 때는 이 정책이 적용되지 않는다. 

> 자바스크립트 엔진 표준 스팩에 존재하는 보안 규칙이다. 그럼 다른 도메인의 <script\></script\> 안에 있는 것말고 <img> 파일이나 css 파일을 가져 올 수 있는 것인가? 정답은 맞다. 가져올 수 있다.

그래, 원래는 다른 출처(Cross-Origin)의 자원은 사용할 수 없다.

### 왜 이런 규칙이 존재할까?

동일 출처가 아닌 경우 브라우저는 왜 접근을 차단할까? 

출처가 다른 두 개의 어플리케이션이 마음대로 소통할 수 있는 환경은 꽤 위험한 환경이다. ***CSRF Cross-Site Request Forgery*** 공격이 있다. 사용자의 권한을 도용해 중요 기능을 실행하는 공격이다. 

사용자가 웹사이트에 접근할 때는 브라우저의 쿠키에 토큰을 남기게 된다. 사용자는 해당 토큰을 사용해 매번 로그인 할 필요 없이 서비스를 이용할 수 있게 된다. 그러나 로그인 토큰이 남아있는 브라우저에서 사용자가 악성 사이트에 접속한다면 악성 사이트 역시 사용자 브라우저의 토큰에 접근할 수 있다.

그리고 그 토큰으로 정보를 나쁜 요청을 하는데, 브라우저는 SOP에 따라 이 상황을 막을 수 있다. 악성 사이트의 **요청 서버**와, 요청을 받고 응답을 주는 **응답 서버**의 **출처**가 다른 걸 보고 요청을 막는 것이다.

만약 SOP가 없다면 털털 털렸을 것이다.

### 하지만

그러나 다른 출처에 있는 리소스를 가져와서 사용하는 일은 굉장히 흔한 일이라 무작정 막을 수 없다. 

하지만 웹 서비스가 다양해지면서 여러 서비스간 보다 자유롭게 데이터를 주고받을 필요가 생겼다. 그런데 다른 사이트간의 요청을 브라우저가 막고 있으니까, 개발자들은 Jsonp 등의 방식으로 이를 우회해서 사용했다.

이걸 합의된 출처들간에 '합법적'으로 허용해주기 위해 **어떤 기준을 충족시키면 리소스 공유가 되도록 만들어진 매커니즘이 CORS**, 교차 출처 자원 공유 방식이다. CORS 정책을 지키면 SOP의 제약을 받지 않게 된다. 만약 정책을 지키지 않고 다른 출처간 요청을 보내면 CORS(를 사용하라는) 에러가 내려진다.

우리가 다른 출처로 리소스를 요청한다면 SOP 정책을 위반한 것이 되고, 거기다가 **SOP의 예외 조항인 CORS** 정책까지 지키지 않는다면 아예 다른 출처의 리소스를 사용할 수 없게 된다.

<BR>

**`SOP` 👉 `하지만 다른 사이트 간의 요청이 필요` 👉 `개발자들이 Jsonp로 우회` 👉 `합법적으로 해라` 👉 `SOP의 예외 정책, CORS`**

<br>

## Cross-Origin? Same-Origin?

*동일 출처*(*Same-Origin*)에서밖에 공유가 안 되었는데, CORS 정책으로 *다른 출처*(*Cross-Origin*)에서도 공유가 가능해졌다. 그러면 다르고, 같다를 구분하는 기준은 어떻게 될까.

<br>

Origin(출처)은 **① scheme**, **② host**, **③ port** 가 있다. 

그래서 *same-origin*이란 scheme(프로토콜), host(도메인), 포트가 같다는 말이며, 이 3가지 중 하나라도 다르면 *cross-origin*이다.

<img src="https://www.affde.com/uploads/article/22287/uutuA1y8TyrZ8GRC.jpg">

위 사진에서  origin은 protocol+host이다. 

<br>

여기서 중요한 사실 한 가지는 앞에서 언급했듯 이렇게 출처를 비교하는 로직이 서버에 구현된 스펙이 아니라 **브라우저에 구현되어 있는 스펙**이라는 것이다.

만약 우리가 CORS 정책을 위반하는 요청을 하더라도 해당 서버가 같은 출처에서 보낸 요청만 받겠다는 로직을 가지고 있는 경우가 아닌 이상 서버는 정상적인 응답을 한다는 것이다. 단, 이후 브라우저가 이 응답을 분석해서 CORS 정책 위반이라고 판단되면 그 응답을 사용하지 않고 그냥 버릴 뿐이다. 

즉, CORS는 브라우저 구현 스펙에 포함되는 정책이기때문에 브라우저를 통하지 않고 서버 간 통신을 할 때는 이 정책이 적용되지 않는다. 또한 CORS 정책을 위반하는 리소스 요청때문에 에러가 발생했다고 해도 서버 쪽 로그에는 정상적으로 응답했다는 로그만 남기 때문에, CORS가 돌아가는 방식을 정확히 모르면 에러 트레이싱에 난항을 겪을 수도 있다.

> 서버가 아니라 브라우저에서 CORS 에러를 낸다는 점을, 출처를 브라우저에서 비교한다는 점을 기억하자.

<br>

## 방법

#### 1. Simple Request

브라우저는 다른 출처(cross-orgin) 요청이 보내질 때 *origin이라는 header*을 추가한다. origin 항목에는 내 사이트의 프로토콜, 도메인, 포트가 담긴다.

요청을 받는 api (ex 네이버 지도 api)는 지정된 *access-control-allow-origin* 정보를 실어 보낸다. 만약 내 사이트가 등록된 상태면 (허용된 상태면) 내 사이트의 url도 access-control-allow-origin 정보에 들어있다. 

브라우저는 이 둘을 비교한다. **origin에서 보낸 출처값이 서버의 답장에 담긴 access-control-allow-origin에 똑같이 있으면 안전한 요청으로 간주**하고 응답 데이터를 받아오게된다.

#### 2. Preflight Request 예비 요청

브라우저는 요청을 한번에 보내지 않고 예비 요청과 본 요청으로 나누어서 서버로 전송한다.

이 때 브라우저가 본 요청을 보내기 전에 보내는 예비 요청을 Preflight라고 부른다. 예비 요청에는 HTTP 메서드 중 **OPTIONS** 메서드가 사용된다. 예비 요청의 역할은 본 요청을 보내기 전에 브라우저 스스로 이 **요청을 보내는 것이 안전한지 확인**하는 것이다.

#### 3. [Credentialed](https://velog.io/@wiostz98kr/CORS%EC%9D%98-%EB%AA%A8%EB%93%A0-%EA%B2%83) [Request](https://evan-moon.github.io/2020/05/21/about-cors/en/)

인증된 요청을 사용하는 방법이다. CORS의 기본적인 방식이라기 보다는 다른 출처 간 통신에서 보안을 좀 더 강화하고 싶을 때 사용하는 방법이다.

요청에 인증과 관련된 정보를 담을 수 있게 해주는 옵션이 credentials옵션이다. 옵션에는 총 3가지 값을 사용할 수 있다. **① same-origin**(같은 출처 간 요청에만 인증 정보 담음)이 기본값이고 **②include**(모든 요청에 인증 정보 담음)와 **③omit**(모든 요청에 인증 정보 담지 않음)이 있다. 

브라우저는 Access-Control-Allow-Origin: *라는 응답을 보고 괜찮다, 결론 내리지만 credentials 옵션을 include로 변경하고 같은 요청을 보내면 상황이 달라진다. 인증 모드가 include일 경우 모든 요청을 허용한다는 의미의 *를 Access-Control-Allow-Origin 헤더에 사용하면 안 된다.

<br>

## 해결 방법

응답 헤더 Access-Control-Allow-Origin에 허용하고자 하는 도메인을 설정해준다. *는 모든 도메인을 허용한다.

### Spring Boot

1. ***Config 클래스를 만들어주는 방법***

```java
@Configuration
public class WebConfig implements WebMvcConfigurer{
    @Override
    public void addCorsMappings(CorsRegistry registry){
        registry.addMapping("/**")
            .allowedOrigins("*")
            .allowedMethods("GET","POST");
    }
}
```

`@Configuration` 어노테이션을 통해 설정 파일이라는 것을 알려준다. 

addCorsMappings(...) 메서드를 오버라이드한다.

`registry.addMapping`을 이용해서 자원 공유를 허용할 url 패턴을 정의한다. "/**"은 와일드카드이다. 

`allowedOrigins()` 메소드를 이용해서 자원 공유를 허락할 Origin을 지정할 수 있다.

```java
.allowedOrigins("http://localhost:8080", "http://localhost:7007");
```

한번에 여러 Origin을 설정할 수 있다.

`allowedMethods()`로 자원 공유를 허용할 HTTP Mehotd를 지정할 수 있다. 위처럼 여러개를 지정할 수 있고 마찬가지로 "*"를 이용해 모든 method를 허용할 수 있다.

2. ***Annotation 이용하는 방법***

```java
@RequestMapping("/")
@CrossOrigin(origins="*", allowedHeaders="*")
public class AController{
    
}
```

`@CrossOrigin` 애노테이션을 사용하면 configuration같이 허용할 origin이나 methods를 지정할 수 있다. origins, methods, maxAge, allowedHeadrs가 있다. 메서드에 적용되게 할 수도 있다.

