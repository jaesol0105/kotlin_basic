# kotlin_basic

> ## 1. nullable type
> nullable type에서는 operator없이 non-Null type에 제공되는 메소드를 호출 할 수 없다.<br>
> 이러한 코드를 작성시 코틀린에서는 컴파일시 오류가 발생하게된다.<br>
> - <b>operator</b>의 종류
>   + safe (?.)
>   + non-null asserted (!!.)

<br>

> ## 2. 컴파일러와 빌드
> - 컴파일러  :<br>
> 소스코드 -> 기계어<br><br>
> - 빌드      :<br>
> 소드코드 -> 결과물로 변환하는 과정 (이 과정의 일부를 컴파일러가 수행하는것)

<br>

> ## 3. complie time 과 runtime
> - complie time :<br>
> 컴파일시 수행되는 시간. (컴파일 성공을 위한 요구사항들을 확인)<br><br>
> - runtime :<br>
> 컴파일 후 프로그램이 실행되는 시간. <b>런타임 오류</b>란 프로그램 실행 도중 발생하는 오류.

<br>

> ## 4. safe operator (?.)
> nullable type이 null이 아닐경우만 안전하게 실행 된다.
> ``` kotlin
> if (userName?.isEmpty())
> ```  
> 하지만 위와 같은 경우 에러가 발생한다. 왜?<br>
> userName이 null일 경우 isEmpty()함수가 호출되지않고, 괄호안의 값은 null of boolean 타입이 되기 때문이다.
> 
> 다음과 같은 방법으로 처리 가능.
> ```kotlin
> if (userName?.isEmpty() == true)
> if (userName.isNullOrEmpty())
> if (userName.isNullOrBlank()) // Best
> ```

<br>

> ## 5. 조건문으로 변수 할당
> 조건문을 이용하여 변수 값 할당이 가능하다. 조건문 block의 마지막 값을 반환하여 변수에 할당한다.
> ```kotlin
> val max = if (a>b)
>           {
>             print("a")
>             a
>           } else {
>             print("b")
>             b
>           }
>	 ```

<br>

> ## 6. Elvis operator (?:)
> if 식 대신에 사용 가능하다.
> ```kotlin
> var userName = readLine()
> if (userName == null) { username ="" }
> ```
> ```kotlin
> var userName = readLine() ?: ""
> ```
> readLine()의 값이 null이 아닐경우 입력받은 값을 반환, null일경우 "" 반환

<br>

> ## 7. not-null assertion operator (!!.)
> null이 발생할 수 있는 상태라도 우선 컴파일이 완료된다.
> 런타임에 NullPointerException이 발생 할 수 있다.

<br>

> ## 8. when
> ```kotlin
> when
> {
> 	userName.length < 4 -> { }
> 	userName.length > 16 -> { }
> 	userName.isBlank() -> { }
> 	else -> { }
> }
> ```

<br>

> ## 9. type check operator (is / !is)
> - 스마트 캐스트 : type 검사 이후에는 해당 type으로 자동변환됨.
> ```kotlin
> when (x)
> {
> 	is Int -> print(x+1) // x가 Int인지 검사하였기 때문에 Int 타입으로 스마트캐스트 되어 사칙연산이 가능.
> 	is IntArray -> print(x.sum())
> }
> ```

<br>

> ## 10. type cast operator
> - unsafe cast operator : <b>as</b>
> ```kotlin
> val num =1
> val text : String = num as String // 에러
> ```
>
> - safe cast operator : <b>as?</b>
> ```kotlin
> val text : String? = num as? String // 변환 실패 시 null 값을 반환
> ```
> ```kotlin
> val text : String? = num as String? // unsafe cast와 동일하게 동작
> ```

<br>

> ## 11. 반복문
> ```kotlin
> for (name in names) { name }
> ```
> ```kotlin
> for (index in 0 until names.size) { names[index] } // 인덱스로 접근 0 ~ names.size-1
> ```

<br>

> ## 12. break@레이블
> 실행 지점을 레이블 위치로 이동하여 반복문을 종료.
> ```kotlin
> loop@ for ( ... )
> {
>   for ( ... ) { break@loop }
> }
> ```
> <b>이중 for문을 한번에 탈출 가능!</b>

<br>

> ## 13. TODO 주석
> 개발 시 추후에 해야할 일을 작성한다
> ```kotlin
> // TODO 1. xxx 구현
> ```
> 눈에 더 잘띄고 검색이 용이해짐

<br>

> ## 14. 클래스
> 클래스를 <b>constructor</b>와 함께 정의하면 클래스 생성에 필요한 property를 파라메터와 함께 정의 할 수 있다.
> ```kotlin
> class ClassName constructor (val categoryLabel: String)
> ```
> - property가 한 개일 경우 constructor 생략 가능
> ```kotlin
> class ClassName (val categoryLabel: String)
> ```
> - 주 생성자와 부생성자를 분리할 경우 사용
> ```kotlin
> class ClassName (val categoryLabel: String) {
>   constructor(categoryLabel: String, name: String) : this(categoryLabel)
> }
> ```
> - 코틀린에서는 파라메터에 default값 설정이 가능
> ```kotlin
> class ClassName (val categoryLabel: String, val name: String = "")
> ```

<br>

> ## 15. 인스턴스
> 클래스로 만드는 객체

<br>

> ## 16. 상속
> - 코틀린의 최상위 클래스 'Any' (equals, hashcode, toString 등 함수를 가진다)
> 
> 모든 클래스의 최상위 클래스이다.
> ```kotlin
> open class Any
> ```
> 
> - 동시에 여러개의 super 클래스를 상속 받을수 없다.<br>
> <b>open</b> 키워드가 붙은 클래스만 상속 받을수 있다. (클래스의 기본 값인 final class는 상속이 불가능)
> ```kotlin
> open class base (p: Int)
> ```
> ```kotlin
> class Derived (p: Int) : Base(p) // super 클래스의 생성자 파라메터가 있다면, 서브클래스에도 전달해야함
> ```

<br>

> ## 17. 클래스 : 프로퍼티(Property)
> 클래스의 내부에서 데이터를 저장하는 field.<br>
> <b>getter() setter()</b>을 포함한다.<br><br>
> getter와 setter는 변수(field)를 선언할때 재정의 할 수 있다.
> ```kotlin
> val displayName: String
> get() = "$categoryLabel > $name"
> ```
> ```kotlin
> var counter =0
> set(value) {
> 	if (value >= 0)
> 	  field = value
> }
> ```

<br>

> ## 18. 추상 클래스
> class 앞에 <b>abstract</b> 키워드를 붙인다. open키워드가 없어도 subclass가 상속 가능하다.<br>
> 
> <b>인스턴스화 불가능 (객체생성 불가)</b><br>
> 
> abstract 변수/함수는 subclass에서 override해 구현방식을 재정의 할 수 있다.<br>
> <b>abstract 함수는 구현부를 작성 할 수 없음</b> -> subclass에서 구현해야함.
> ```kotlin
> abstract class Polygon {
> 	abstract fun draw()
> }
> class Rectangle : Ploygon() {
> 	override fun draw() { //구현 }
> }
> ```

<br>

> ## 19. 인터페이스(interface)
> 클래스간 계층 구조를 형성하는 또 다른 방식.<br>
> 프로퍼티 (val property: String) 는 정의 할 수 있지만, <b>값을 할당 할수는없음 (상태저장 X)</b><br>
> ```kotlin
> val property: String ="property" // 불가능
> ```
> - 프로퍼티의 접근자 제공 가능
> ```kotlin
> val:property
> get()="foo"
> ```
> - 본문이 있는 함수도 정의 가능
> ```kotlin
> fun foo()
> { ... }
> ```
>
> 인터페이스 구현 상속은 클래스와 다르게 <b>상속개수 제한이 없음</b><br>
> 하나의 클래스가 여러 인터페이스를 상속 받을 수 있다.

<br>

> ## 20. 함수
> - trailing comma를 지원:
> 마지막 파라메터 뒤에 콤마 추가가능. 추후 파라메터 추가 시의 편의를 위함.
> ```kotlin
> fun powerOf(
>   num: Int,
>   exponent: Int, //trailing comma
>   ) { ... }
>```
>
> - 파라메터 디폴트값:
> 함수 호출시, 디폴트 값이 선언된 파라메터를 생략하면 디폴트값이 적용됨.
> ```kotlin
> fun foo(
>   bar: Int = 0,
>   baz: Int,
>   ) { ... }
> ```
> ```kotlin
> foo(baz=1) // bar는 0이 할당됨
> ```
> 
> - named argument:
> 함수 호출시 named argument를 활용하면 시각적으로 코드를 이해하기 쉬워짐.
> ```kotlin
> fun namearg(
>	  "string",
>	  false,
>	  valueA = false,
>	  valueB = true,
>   )
> ```
