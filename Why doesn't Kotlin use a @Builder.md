> 부제: Hey, Kotiln (코틀린 기본 상식 알아가기)

솔직히 흥미롭다. 그렇지 않은가? lombok에서 가장 많이 쓰는 애노테이션 두 개를 뽑는다면 나는 `@Getter`와... `@Builder`을 뽑을 것이다. 어김없이 Kotlin에서도 `@Builder` 애노테이션을 사용하려고 했는데, 잠깐, 필요가 있을까요?

<br>

우리의 친구 구글에 당장 찾아봤습니다. 친구의 대답은, ***Kotlin을 사용할 경우 Builder 패턴을 굳이 사용할 필요 없다.***

<br>

### 우리가 Builder Pattern을 쓰는 이유

> Builder Pattern에 관한 건 깃허브 languageStudy->Java에 정리해뒀다. 😓

Builder Pattern의 장점으로는

1. 각 인자가 어떤 의미인지 알기 쉽다. 

   타입이 같은 매개변수가 연달아 있을 때 생성자로 객체를 생성한다면 값을 잘못 전달했을 때 찾기 어려운 버그로 이어질 수 있다.

2. setter 메서드가 없으므로 변경 불가능 객체를 만들 수 있다. (객체 일관성이 깨지지 않는다.)

3. 객체들마다 들어가야할 인자가 각각 다를 때 유연하게 사용할 수 있다.

등이 있다.

<br>

### Kotlin constructor

다시 보자.

1. 각 인자가 어떤 의미인지 알기 쉽다.
2. 필드가 선언된 순서와 상관없이 객체를 생성할 수 있다.
3. 불변 객체를 만들 수 있다.
4. 객체들마다 들어가야할 인자가 다를 때 유연하게 사용할 수 있다.

코틀린에서는 모두 constructor로 해결이 가능하다. (정말?)

> Java의 생성자와는 다른 점이 Kotlin은 default 변수 선언을 통해 여러 생성자를 한 번에 정의 가능하다는 것이다. [좋은 글.](https://thdev.tech/kotlin/2017/03/09/Kotlin-Constructor-Init/)

#### Named Argument: 네임드 파라미터

```kotlin
User(email="email@gmail.com", "nickname", "password")
```

네임드 파라미터로 각 인자가 어떤 의미인지 알기 쉽다. 그리고 필드의 순서 상관없이 객체를 생성할 수 있어진다. (개인적으로 의미를 알기 쉬운건 Builder parttern을 사용하는 게 훨씬 쉽지만.... 그래서 무조건 Kotlin에서 Builder Pattern? 안 돼,는 아니다.)

👉 각 인자가 어떤 의미인지 알기 쉽다. / 필드가 선언된 순서와 상관 없이 객체를 생성할 수 있다.

#### Setter가 없으므로, 불변

생성자로 객체를 생성하기 때문에 불변이다. 해당 컬럼에 기본값을 주게 되면 그 인자는 값을 할당해주지 않더라도 기본값이 들어가므로 생성 할 수 있게 되기 때문입니다.

👉 불변 객체를 만들 수 있다.

#### Default Argument: default 파라미터

```kotlin
class User(name: String, age: Int = 10)
```

age처럼 기본 인자를 사용하여 인자에 값을 할당해주지 않아도 되게 할 수 있다.  객체들마다 들어가야할 인자가 다를 때 유연하게 사용할 수 있다.가 해결된다.

👉 객체들마다 들어가야할 인자가 다를 때 유연하게 사용할 수 있다.




<br>

### Lombok? 😋 We have a data class

lombok도 필요 없다. 왜? Kotlin에는 data class가 있으니까. 

data 클래스는 toString(), hashCode(), equals(), copy() 메서드를 자동으로 만들어준다. Kotlin 코드를 처음 짤 때 data class의 여부를 알고 깜짝 놀랐다. **데이터만을 다루는 클래스에 대해 간편한 문법을 제공**해주고, 사용법도 그냥 클래스 앞에 data를 붙여주면 된다. `data class User()`

#### 특징

* 상속 받을 수 없다.
* 1개 이상의 프로퍼티를 가지고 있어야 한다.
* `toString()`은 생성자에 정의된 프로퍼티만 출력된다.

#### **`copy()`**

신기한 걸 방금 하나 더 발견했다. 하나의 데이터를 단순 필드 값만 변경해서 추가적으로 사용하고 싶을 때 data class의 copy를 이용한다.

```kotlin
val fUser = User("name", "pass", 30)
val sUser = fUser.copy(name = "nickname")
```

정말 신기하다. 

<br>

이런 Kotlin 특성 상 id를 아래로 넣는 게 좋다는 글을 보았다.

```kotlin
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
val id: Long = 0L
```

id 값을 넣어 줄 필요 없는 경우에 id를 앞에 넣으면 생성자로 생성할 때 파라미터 순서가 맞지 않기에 컴파일 에러가 발생하게 된다. (이메일을 넣었더니 여기 id 자리인데요.)

네임드 파라미터를 사용함으로써 해결할 수 있지만, 더 좋은 방법이 존재한다. **id를 맨 아래에 선언**하는 것. 네임드 파라미터를 사용할 필요가 없기 때문에 더 깔끔하게 작성이 가능할 것이다. 

<br>

### 참고

[Builder Pattern - 봄석 님 블로그](https://beomseok95.tistory.com/240)

[Id를 선언할 때, 생성자의 파라미터 순서 상 가장 밑으로 두는 것이 좋은 이유 - Hyung 님 블로그](https://junghyungil.tistory.com/m/205)

[data class 이해하기 - Kenneths 님 블로그](https://medium.com/kenneth-android/kotlin-kotlin-data-class-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-7d7f51885075)

[Kotlin init이란? - Taehwan 님 블로그](https://thdev.tech/kotlin/2017/03/09/Kotlin-Constructor-Init/)
