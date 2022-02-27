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

> ## 15. 인스턴스(instance)
> 클래스로 만드는 객체

<br>

> ## 16. 상속
> - 코틀린의 최상위 클래스 'Any' (equals, hashcode, toString 등 함수를 가진다)
>   모든 클래스의 최상위 클래스이다.
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

> ## 18. 추상 클래스(abstract)
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

<br>

> ## 21. 함수의 반환값
> - 함수의 body가 블럭( { ... } )일 경우 함수명 뒤에 반환 타입을 기술.
> ```kotlin
> fun 함수 : type { ... } 
> ```
> 
> - Unit : 반환값이 없음을 나타내는 타입 , 생략 가능.
> ```kotlin
> fun 함수 { ... } 
> ```
>
> - 함수의 body가 식일 경우 (중괄호로 감싸지 않고 등호(=)로 반환 값을 만드는 방식)
> ```kotlin
> fun double(x:Int) : Int = x*2
> ```
> 값으로 타입을 추론할 수 있는경우에는 생략가능
> ```kotlin
> fun double(x:Int) = x*2
> ```

> ## 22. top-level 함수
> 함수가 클래스 안에 들어있지 않아도 호출 됨<br>
> main함수 등이 top-level 함수에 해당한다.<br><br>
> 
> (일반적인 클래스내부의 함수 : 클래스객체.func()로 호출)

<br>

> ## 23. 상속시 함수의 오버라이딩 막기 
> 함수를 final로 선언하면 서브 클래스에서 오버라이딩 할 수 없다.

<br>

> ## 24. super class와 sub class의 실행순서
> super class -> sub class

<br>

> ## 25. 프로퍼티(property) 오버라이딩
> <b>open 키워드가 붙은 프로퍼티</b>는 subclass에서 재정의 가능
>
> - mutable변수(var)를 val로 재정의 -> <b>불가능</b>
> - immutable변수(val)를 var로 재정의 -> <b>가능</b><br>
>   val변수는 read-only 즉, getter만 가진 변수이다. 재정의 하면서 setter를 추가 할수있기 때문에 var로 재정의가 가능하다.

<br>

> ## 26. 클래스 : toString, equals, hashCode.
> 최상위 클래스인 Any 클래스의 메소드들이므로, 오버라이딩 하여 사용가능

<br>

> ## 27. data class.
> ```kotlin
> data class ClassName(val v1: String, val v2: String="")
> ```
> ```kotlin
> val className  = ClassName("A", "B")
> println(className)
> ```
> data class는 toString을 오버라이딩 하지않고도 프로퍼티 값들을 출력가능하다.
> 또한 equals 함수를 오버라이딩 하지않아도, 내부 값들을 비교할 수 있도록 설계 되어있음.

<br>

> ## 28. data class : copy
> 동일한 값 프로퍼티는 유지하고, 지정한 값만 변경.
> ```kotlin
> val padding = Product("패션", "겨울패딩")
> val jacket = padding.copy(name ="자켓")
> ```
> * data class의 프로퍼티는 이후 연산으로 부터 영향받지 않도록 변수를 val로 선언하는것을 권장함.<br>
> 원본 객체에는 영향을 주지 않으면서 새로운 객체를 만드는 copy연산이 존재하기 때문

<br>

> ## 29. 컬렉션
> #### 29-1. 컬렉션이란? 동일한 type의 여러 데이터 집합<br>
> (1) read-only (immutable, 수정 불가) <br>
> - List : 순서를 가진 컬렉션으로 <b>index를 통해 원소접근</b>가능. listOf(1,2,2)
> - Set : <b>유니크</b>한 원소를 가짐. setOf(1,2,3)
> - Map : <b>키-값</b> 쌍. mapOf("first" to 1, ...)
>
> - iterator
> ```kotlin
> val iterator = list.iterator()
> while (iterator.hasNext() { print(iterator.next()) }
> ```
> 
> (2) mutable, 수정 가능
> ```kotlin
> mutableListOf(1,2,3)
> iterator.remove(idx)
> ```
>
> #### 29-2. 컬렉션 : retrieve(검색)
> (1) index
> ```kotlin
>	list.elementAt(idx)
>	list.elementAtOrNull(idx)
>	list.elementAtOrElse(idx) {-1}
>	```
>	
> (2) 확장함수
> ```kotlin
>	list.firstOrNull()
>	// 함수의 arg로 조건 전달
>	list.firstOrNull { it > 3 } // list.find { it > 3 }
>	list.lastOrNull { it > 3 } // list.findLast { it > 3 }
>	```
>	
> #### 29-3. 컬렉션 : 출력 값 변형
> (1) String 값 나타내기
> ```kotlin
> val numbers = listOf("one","two","three")
> println( numbers.joinToString( separator="|", prefix="start:", postfix=":end"))
> ```
> 
> #### 29-4. 컬렉션 : 필터링
> ```kotlin
> val longerThan3 = numbers.filter { it.length > 3 }
> println(longerThan3)
> ```
> 
> ```kotlin
> println(numbers.any { it.endsWith("e") } ) // 'e'로 끝나는 단어 하나라도 있을경우 true.
> ```
> 
> 필터링 함수로 any, none, all 이 존재한다
> 
> #### 29-5. 컬렉션 : 파티션
> ```kotlin
> val (match, rest)  = numbers.partition { it.length > 3 }
> ```
>
> #### 29-6. 컬렉션 : 그룹핑
> ```kotlin
> categories: Map<String,List<Product>> = products.groupBy { product -> product.categoryLabel } // Label 을 키값으로 그룹핑
> ```

<br>
  
> ## 30. object
> <b>프로젝트 전역에서 단일객체로 사용</b>됨. 각기 다른 클래스에서 데이터 접근 및 유지 가능.
> - 싱글턴 패턴:
>   인스턴스를 하나만 만들고 이를 프로젝트 전역에서 사용하는 방법.<br>
>   단점은 어느위치에서 값을 수정하였는지 파악하기 힘들다.
> ```kotlin
> object objName {
>   private val ...
>   fun ...
> }
> ```

<br>
  
> ## 31. object expressions - 무명객체
> (1) 무명객체생성<br>
> object 키워드를 통해, <b>이름을 선언하지 않고</b> 객체를 생성하는방법.
> ```kotlin
> val cartItem = object { val ...	fun ... }
> ```
>
> (2) 클래스/인터페이스를 상속하고 이름을 생략한채 객체생성<br>
> <b>앱 개발시 실질적으로 많이 보게되는 부분</b>
> ```kotlin
> interface ClickListener { fun onClick() ... }
>
> val clickListener = object : ClickListener {
>	  override fun onClick() ...
> }
> ```
> - 무명객체를 변수에 저장하는 이유:<br>
>   프로젝트 전역에서 사용되는 단일객체와 다르게, 무명객체는 코드를 실행할때 마다 매번 새로운 객체를 생성하게되기 때문에<br>
>   매번 새로운 객체를 만들지 않도록 <b>변수에 저장한다</b>.

<br>
  
> ## 32. companion object (동반객체)
> 클래스 내부에서 쓰이며, 이때 해당 클래스의 생성자(constructor)는 private으로 변경하여 외부에서 생성자를 통해 인스턴스를 만드는것을 방지한다.
> ```kotlin
> class Store private constructor( ... ) {
>   ...
>   companion object {
>     fun create(id : String) : Store { return Stroe(id) }
>   }
> }
> ```
> ```kotlin
> val store = Store.create("id")
> ```

<br>
  
> ## 33. const
> complie time에 값을 알수있는 read-only 프로퍼티<br>
> 컴파일할때 값이 고정되어야함으로, 프로퍼티를 요청할때 값을 반환하는 <b>getter는 선언 불가능</b>.

<br>
  
> ## 34. 중첩된 클래스.
> 클래스 내부에 다른 클래스를 선언가능
> ```kotlin
> class Outer {
> 	class Nested { fun foo() ... }
> }
> ```
> ```kotlin
> val v = Outer.Nested().foo()
> ```
> 하지만, Nested에서 Outer의 프로퍼티나 함수에 접근하는것은 불가능하다.

<br>
  
> ## 35. 중첩된 인터페이스
> ```kotlin
> interface A{
>   class B
>   interface C
> }
> ```
> ```kotlin
> class A{
>	  class B
>	  interface C
> }
> ```

<br>
  
> ## 36. inner class
> 위의 Nested class와는 다르게 Outer class의 멤버에 접근이 가능.
> ```kotlin
> class Outer {
>   private val bar = 1
>	  inner class Inner { fun foo() = bar }
> }
> ```
> ```kotlin
> val v = Outer().Inner().foo()
> ```

<br>
  
> ## 37. 무명 inner class
> 이름이 없는 지역 내부 클래스 객체
> ```kotlin
> window.addMouseListener (object : MouseAdapter() { ... }) // MouseAdapter를 구현한 object
>
> /* MouseAdapter라는 추상 클래스의 객체를 내부 클래스 형태로 생성하였기 때문에,
> 실제로는 MouseAdapter클래스를 상속한 내부 클래스가 만들어지게 됨. */
> ```
> [참고] https://data-make.tistory.com/213

<br>
  
> ## 38. this
> 현재 수신하고있는 객체를 가르킬때 this 표현식을 사용한다.<br>
> - (1) 같은 클래스의 멤버를 호출할때는 this 생략 가능<br>
> - (2) 중첩된 클래스 구조를 가질때 this@label 로 구분한다<br>
> ```kotlin
> class Store {
> 	inner class Favorite {
> 			fun List<Product>.filterFavoriteItems() {  // List<Product>타입에서만 호출 할 수있는 확장 함수의 표현 방법
> 				this // 현재 함수의 수신 객체인 List<Product>를 참조
> 				this@filterFavoriteItems // 함수에 대한 참조
> 				this@Favorite // Favorite 클래스에 대한 참조
> 				this@Store	// Store 클래스에 대한 참조
> 			}
> 	}
> }
> ```

<br>
  
> ## 39. 확장 함수
> 클래스를 상속받지 않아도 기능을 확장 할 수 있다.
> - 확장 함수 선언하기
> ```kotlin
> fun Receiver Type(확장할 클래스).함수명() { ... }
> ```
  
> ```kotlin
> fun MutableList<Int>.swap (idx1:Int, idx2:Int) { // MutableList<Int>에 대한 확장 함수 swap 선언.
>   val tmp = this[idx1]
>   this[idx1] = this[idx2]
>   this[idx2] = tmp
> }
> ```
> ```kotlin
> val list = mutableListOf(1,2,3)
> list.swap(0,2)
> ```
>
> - Receiver Type(확장할 클래스)에 대한 함수 뿐 아니라 프로퍼티도 추가가능하다.
> ```kotlin
> public val <T> List<T>.lastIndex : Int
> get() = this.size -1
> ```
> T는 제네릭 개념으로, T는 lastIndex를 호출하는 List타입의 원소로 모든 타입을 허용한다.
> ```kotlin
> val list = listOf("a","b","c","d")
> println(${list.lastIndex})
> ```

<br>
