<br><br>  

<h1>자바 vs 코틀린</h1>  

  <br><br><br><br>

<h2>1. 기본 자료형</h2> 

<br>

<h3>숫자</h3>

숫자를 표현하는 모든 자료형(Byte, Double, Float, Int, Long, Short)은 **Number 클래스**를 상속하며 자바의 Number 클래스와 마찬가지로 코틀린에서도 `toInt()`, `toDouble()`등 값을 다른 자료형으로 바꿔주는 함수를 제공합니다. 

<br>

숫자 연산에 사용하는 연산자의 경우 사칙연산은 자바와 동일하나 비트 연산자의 이름은 자바에 비해 좀 더 직관적입니다.    **※ 비트 연산 != 논리 연산 **

| Java | Kotlin | 의미                               |
| ---- | ------ | ---------------------------------- |
| &    | and    | 비트 연산 AND                      |
| \|   | or     | 비트 연산 OR                       |
| ^    | xor    | 비트 연산 XOR                      |
| ~    | inv    | 비트 연산 NOT                      |
| <<   | shl    | 왼쪽으로 시프트 (부호 비트 유지)   |
| >>   | shr    | 오른쪽으로 시프트 (부호 비트 유지) |
| >>>  | ushr   | 오른쪽으로 시프트 (부호 비트 무시) |

<br>

<br>

<h3>문자</h3>

자바에서는 문자에 해당하는 아스키 코드를 문자 자료형에 숫자 형태로 대입할 수 있지만, 코틀린에서는 문자만 대입할 수 있습니다.

| Java                                       | Kotlin                                                       |
| ------------------------------------------ | ------------------------------------------------------------ |
| char c = 65;  // 문자 'A'의 아스키 코드 값 | // 컴파일 에러 : Char 자료형 값에 Int 자료형인 65 대입 불가<br>val c : Char = 65<br /><br />//성공<br>val c : Char = 'A' |

<br>

<br>

<h3>논리</h3>

논리 자료형은 자바  boolean의 래퍼인 **Boolean**과 사용 방법이 동일하며 사용 가능한 연산자(&&, ||, !)도  자바와 동일합니다.

<br>

<br>

<h3>문자열</h3>

자바의 문자열과 거의 유사합니다. 자바에서는 문자열 내 특정 위치의 문자에 `charAt()`메서드를 통해 접근하지만, 코틀린에서는 `get()` 메서드 또는 `[]`를 사용합니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| String foo = "Lorem ipsum";<br><br />char ch = foo.charAt(4); | val foo: String = "Lorem ipsum"<br /><br />val ch: Char = foo.get(4)<br />val ch2 : Char = foo[7] |

<br>

템플릿 문자열에 포함할 인자는 앞에 `$`를 붙여 구분합니다. 인자로 값이나 변수 대신 표현식을 넣고 싶다면 중괄호로 구분하면 됩니다.

```kotlin
val text: String = "Lorem ipsum"

val lengthText: String = "TextLength : ${text.length}"
```

<br>

<br>

<h3>배열</h3>

배열 타입이 별도로 존재하는 자바와 달리 코틀린에서의 배열은 타입 인자를 갖는 **Array 클래스**로 표현합니다. `arrayOf()`메서드는 입력받은 인자로 구성된 배열을 생성합니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| String[] words = new String[] {<br />      "Lorem", "ipsum", "dolor"}; | val words: Array<String> = arrayOf<br />     ("Lorem", "ipsum", "dolor") |

<br>

자바의 원시 타입(int, float, …)은 코틀린 배열 클래스의 타입 인자로 사용할 수 없고 그에 상응하는 특수한 클래스를 다음과 같이 사용합니다.

| Java                                        | Kotlin                                            |
| ------------------------------------------- | ------------------------------------------------- |
| int[] intArr = new int[] { 1, 2, 3, 4, 5 }; | val intArr : IntArray = intArrayOf(1, 2, 3, 4, 5) |

<br>

원시 타입이 아닌 래퍼 타입(Integer, String, …)은 코틀린의 배열 형태를 그대로 사용할 수 있습니다.

| Java                                          | Kotlin                                           |
| --------------------------------------------- | ------------------------------------------------ |
| Integer[ ] intArr = new Int[] {1, 2, 3, 4, 5} | val intArr : Array<Int> = arrayOf(1, 2, 3, 4, 5) |

<br>

<br>

<br>

<br>

<h2>2. 컬렉션</h2>

자바와는 달리 코틀린에서는 컬렉션 내 자료의 **수정 가능 여부**에 따라 컬렉션의 종류를 구분합니다. 각각의 자료구조와 자료 수정 가능 여부에 따라 제공되는 인터페이스는 다음과 같습니다.

| 자료 구조 | 자료 수정 불가          | 자료 수정 가능                 |
| --------- | ----------------------- | ------------------------------ |
| List      | kotlin.collections.List | kotlin.collections.MutableList |
| Map       | kotlin.collections.Map  | kotlin.collections.MutableMap  |
| Set       | kotlin.collections.Set  | kotlin.collections.MutableSet  |

```kotlin
val immutableList: List<String> = listOf("Lorem", "ipsum", "dolor", "sit")

// 첫 번째 항목 읽기 - get(0)와 동일
val firstItem: String = immuatableList[0]

// 컴파일 에러 : List는 컬렉션 내 자료의 수정이 불가
immutableList[0] = "Lollypop"

val mutableList: MutableList<String> = mutableListOf("Lorem", "ipsum", "dolor", "sit")

// 자료 수정 가능
mutableList[0] = "Lollypop"
```

<br>

맵은 숫자 인덱스 대신 키 값을 넣어 항목에 접근할 수 있으며, `to`함수를 사용하면 맵 자료구조를 간단하게 생성할 수 있습니다.

```kotlin
val immutableMap: Map<String, Int> = mapOf("A" to 65, "B" to 66)

// 키 "A"에 해당하는 값 - get("A")와 동일
val code: Int = immutableMap["A"]
```

<br>

<br>

<br>

<br>

<h2>3. 클래스 및 인터페이스</h2>

<br>

<h3>클래스와 인터페이스의 선언 및 인스턴스 생성</h3>

클래스와 인터페이스를 선언하는 방법은 자바와 거의 동일합니다.  코틀린은 선언된 내용이 없는 경우 클래스 이름만으로 선언할 수 있습니다.

| Java                      | Kotlin                                                       |
| ------------------------- | ------------------------------------------------------------ |
| public class Foo {<br />} | class Foo {<br />}<br /><br />// 클래스 본체 없이 클래스 선언 가능<br />class Foo |

<br>

자바에서는 클래스의 인스턴스를 생성하기 위해 new 키워드를 사용했지만, 코틀린에서는 이를 사용하지 않습니다.

| Java                                            | Kotlin                                          |
| ----------------------------------------------- | ----------------------------------------------- |
| Foo foo = new Foo();<br />Bar bar = new Bar(1); | val foo: Foo = Foo()<br />val bar: Bar = Bar(1) |

<br>

추상 클래스는 자바와 동일한 방법으로 선언하지만, 추상 클래스의 인스턴스를 생성하는 형태는 매우 다릅니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| // 추상 클래스 선언<br />abstract class Foo {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;public abstract void bar();<br />}<br /><br />// 추상 클래스의 인스턴스 생성<br />// 클래스 생성과 동일하게 new 사용<br />Foo foo = new Foo() {<br />&nbsp;&nbsp;&nbsp;&nbsp;@Override<br />&nbsp;&nbsp;&nbsp;&nbsp;public void bar() {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 메서드 구현<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />}; | // 추상 클래스 선언<br />abstract class Foo {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;abstract fun bar();<br />}<br /><br />// 추상 클래스의 인스턴스 생성<br />// **Object: [생성자] 형태**로 선언<br />val foo = Object: Foo() {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;override fun bar() {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 함수 구현<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />}; |

<br>

<br>

<h3>프로퍼티</h3>

자바에서는 클래스에서 다루는 자료의 값에 접근하기 위해서 Getter/Setter 메서드를 추가해야하지만, 코틀린은 **프로퍼티(property)**를 사용하여 자료를 저장할 수 있는 필드와 이에 상응하는 Getter/Setter를 함께 제공합니다.

```kotlin
class Person {
	// 필드뿐만 아니라 Getter,Setter도 함께 제공
	
    val name: String? = null // 값을 읽을 수만 있는 val 
    var address : String? = null // 값을 읽고 쓸 수 있는 var
}
```

<br>

코틀린의 프로퍼티도 **val**(값 할당 후 변경 불가, 자바의 final) 혹은 **var**(값 할당 후 변경 가능, 변수) 중 하나로 선언합니다.  코틀린에서는 클래스의 멤버로 사용하는 **프로퍼티는 초깃값을 무조건 지정**해야 하며 그렇지 않을 경우 컴파일 에러가 발생합니다.

<br>

프로퍼티 선언 시점이나 생성자 호출 시점에 값을 할당할 수 없는 경우에는 **var 프로퍼티에 한해서만** `lateinit` 키워드를 사용하여 이 프로퍼티의 값이 나중에 할당될 것임을 명시할 수 있습니다.

```kotlin
class Person {
	// val 프로퍼티는 항상 선언과 함께 값을 할당해야 합니다.
	val name: String? = null    
    
    // lateinit 키워드를 사용했기 때문에 선언 시점에 값을 할당하지 않아도 컴파일 에러 없음
    lateinit var address : String? 
}
```

<br>

<br>

<h3>접근 제한자</h3>

코틀린에서 접근 제한자를 사용하는 방법은 자바와 매우 유사하지만 일부 차이가 있습니다. 코틀린에서는 접근 제한자가 없으면 public으로 간주하며, 자바에서는 접근 제한자가 없는 경우 이에 대한 접근 범위를 패키지 단위로 제한합니다. 그러나 **단순히 같은 패키지에 있으면 접근이 가능하다는 단점**이 있습니다. 

<br>

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public class Foo {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;public int a = 1;<br />&nbsp;&nbsp;&nbsp;&nbsp;protected int b =2;<br />&nbsp;&nbsp;&nbsp;&nbsp;private int c = 3;<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;// 패키지 단위 제한자(별도 표기 없는 경우)<br />&nbsp;&nbsp;&nbsp;&nbsp;int d = 4;<br />} | class Foo {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 접근 제한자가 없으면 **public**으로 간주합니다.<br />&nbsp;&nbsp;&nbsp;&nbsp;val a= 1<br />&nbsp;&nbsp;&nbsp;&nbsp;<br />&nbsp;&nbsp;&nbsp;&nbsp;**protected** val  b = 2<br />&nbsp;&nbsp;&nbsp;&nbsp;**private** val c = 3<br />&nbsp;&nbsp;&nbsp;&nbsp;<br />&nbsp;&nbsp;&nbsp;&nbsp;// internal을 대신 사용합니다.<br />&nbsp;&nbsp;&nbsp;&nbsp;**internal** val d = 4<br />} |

코틀린은 이러한 단점을 보완하기 위해 **internal 접근 제한자**가 추가되어 동일한 모듈내에 있는 클래스들로의 접근을 제한합니다.

<br>

<br>

<h3>생성자</h3>

코틀린은 자바와 달리 init 블록을 사용하여 기본 생성자를 대체합니다. 다음은 인자가 없는 기본생성자를 정의하는 예입니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public class Foo {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;public Foo() {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 생성자에서 수행할 작업<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} | class Foo {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;**init** {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 생성자에서 수행할 작업 <br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} |

<br>

생성자에 인자가 필요한 경우 다음과 같이 인자를 받을 수 있으며, 코틀린에서는 이를 **주 생성자**라 부르고 여기에서 받은 인자는 init 블록에서도 사용할 수 있습니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public class Foo {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;public Foo(int a) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.d("Foo", "Number: " + a);<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} | class Foo(a: Int) {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;init {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.d("Foo", "Number: $a") <br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} |

<br>

또한 코틀린에서는 **생성자의 인자를 통해 바로 클래스 내부의 프로퍼티에 값을 할당**할 수 있습니다. 이 경우 생성자의 인자를 통해 프로퍼티 선언을 대신하므로 추가로 프로퍼티를 선언하지 않아도 됩니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public class Foo {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;int a;<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;char b;<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;public Foo(int a, char b) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;this.a = a;<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;this.b =b;<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} | // 자바에 비해서 비약적으로 코드가 줄어듭니다.<br />class Foo(val a: Int, var b: Char) |

<br>

주 생성자 외에 다른 형태의 생성자가 필요한 경우 `constructor` 키워드를 사용하여 추가로 생성자를 선언할 수 있습니다. 자바에서는 새로운 생성자를 정의할 때 다른 생성자를 필요에 따라 선택적으로 호출할 수 있지만, 코틀린에서는 **추가 생성자를 정의하는 경우 반드시 주 생성자를 호출**해야 합니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public class Foo {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;int a;<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;char b;<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;public Foo(int a, char b) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;this.a = a;<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;this.b =b;<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;// a의 값만 인자로 받는 추가 생성자<br />&nbsp;&nbsp;&nbsp;&nbsp;public Foo(int a) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;this(a, 0);<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} | class Foo(val a: Int, var b: Char) {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;// a의 값만 인자로 받는 추가 생성자<br />&nbsp;&nbsp;&nbsp;&nbsp;// 기본 생성자를  **※반드시 호출※**<br />&nbsp;&nbsp;&nbsp;&nbsp;**constructor**(a: Int) : **this(a, 0)**<br />} |

<br>

<br>

<h3>함수</h3>

코틀린에서는 자바의 클래스 내 메서드를 함수로 표현합니다. 표기법만 약간 다를 뿐 역할은 동일합니다. 

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public class Foo {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//  아무 값도 반환하지 않는 메서드<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;public void foo(int a, char b) {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;// 정수 값을 반환 하는 메서드<br />&nbsp;&nbsp;&nbsp;&nbsp;private int bar () {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return 0;<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} | class Foo {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//  아무 값도 반환하지 않는 함수<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;fun foo : **Unit** {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;// 정수 값을 반환 하는 메서드<br />&nbsp;&nbsp;&nbsp;&nbsp;private fun bar () : Int {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return 0;<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} |

코틀린에서 특별한 값을 반환하지 않는(자바의 void) 함수는 Unit 타입을 반환하며, Unit 타입을 반환하는 함수는 선언 시 반환 타입을 생략할 수 있습니다.

<br>

<br>

<h3>상속 및 인터페이스 구현</h3>

자바에서는 클래스의 상속과 인터페이스 구현은 `extends`와 `implements`로 구분하지만, 코틀린에서는 이를 구분하지 않고 `콜론(:)` 뒤에 상속한 클래스나 구현한 인터페이스를 표기합니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public class MainActivity **extends**<br />&nbsp;&nbsp;&nbsp;&nbsp;AppCompatActivity **implements**<br />&nbsp;&nbsp;&nbsp;&nbsp;View.OnClickListener {<br />&nbsp;&nbsp;&nbsp;&nbsp;...<br />} | class MainActivity : AppCompatActivity**()**,<br />&nbsp;&nbsp;&nbsp;&nbsp;View.OnClickListener{<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...<br />} |

<br>

또한, 클래스를 상속하는 경우 반드시 부모 클래스의 생성자를 호출해야하며, 생성자가 여러 형태일 경우 다음과 같이 별도의 생성자 선언에서 부모 클래스의 생성자를 호출하도록 구현할 수 있습니다.

```kotlin
class MyView : View{
    
    constructor(context: Context) super(context){
        // 뷰 초기화
    }
    
    constructor(context: Context, attrs: AttributeSet?) super(context, attrs){
        // 뷰 초기화
    }
}
```

<br>

자바에서는 부모 클래스의 메서드를 재정의하거나 인터페이스를 구현한 메서드를 `@Override` 어노테이션으로 구분합니다. 코틀린에서는 상속받거나 구현한 함수의 앞에 **무조건** `override`키워드를 붙이도록 강제합니다.

```kotlin
class MainActivity : AppCompatActivity(), View.OnClickListener{
    
    // AppCompatActivity의 onCreate() 메서드 상속
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
    }
    
    // View.ONClickListener 인터페이스 구현
    override fun onClick(v: View){
        
    }
}
```

<br/>

자바에서는 클래스나 메서드에 `final`키워드를 붙여 클래스를 더 이상 상속받지 못하게 하거나, 메서드 재정의를 못하게 할 수 있습니다. 하지만 코틀린에서는 그 반대로 `open` **키워드를 붙인 클래스나 함수가 아니라면** 클래스를 상속하거나 함수를 재정의할 수 없습니다.

<br/>

<br/>

<h3>this</h3>

자바에서의 this 키워드는 해당 키워드를 사용한 클래스 자신을 지칭할 때 사용하며, 코틀린에서도 동일한 용도로 사용됩니다. 

<br/>

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| class MyActivity extends AppCompatActivity {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;@Override<br />&nbsp;&nbsp;&nbsp;&nbsp;protected void onCreate(@Nullable Bundle<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;savedInstanceState) {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Toast.makeText(**MyActivity.this**, "Hello", Toast.LENGTH_SHORT).show();<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} | class MyActivity : AppCompatActivity() {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;override fun onCreate(savedInstanceState:<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bundle?) {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Toast.makeText(**this@MyActivity**, "Hello", Toast.LENGTH_SHORT).show();<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} |

클래스 내에서 다른 클래스나 인터페이스의 인스턴스를 동적으로 생성하여 사용하는 경우 키워드를 사용하는 위치에 따라 this가 의미하는 클래스가 달라질 수 있습니다. 이러한 문제를 해결하기 위해 위처럼 자바에서는 **{클래스 이름}.this** 형태로 가리키는 클래스를 명시하며, 코틀린에서는 이를 **this@{클래스 이름}** 형태로 표기합니다.

<br/>

<br/>

<h3>정적 필드 및 메서드</h3>

자바에서는 정적 필드와 메서드를 사용하여 상수를 정의하거나 인스턴스 생성 없이 사용할 수 있는 메서드를 만들 수 있는데, 코틀린에서는 지원하지 않으므로 **패키지 단위로 선언**하거나 **동반 객체**를 사용해야합니다. 다음은 패키지 단위로 선언하는 예입니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| // Foo.java<br />package foo.bar;<br /><br />public class Foo {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;// FOO를 클래스 Foo의 정적 필드로 선언<br />&nbsp;&nbsp;&nbsp;&nbsp;public **static** final int FOO = 123;<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;// 메서드 foo를 클래스 Foo의 정적 메서드로 선언<br />&nbsp;&nbsp;&nbsp;&nbsp;public **static** void foo() { }<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;메서드 bar는 Foo의 인스턴스를 생성해야 사용 가능<br />&nbsp;&nbsp;&nbsp;&nbsp;public void bar() { }<br />} | // Foo.kt<br />package foo.bar<br /><br />// 값 FOO를 패키지 foo.bar에 선언<br />const val FOO = 123<br /><br />// 함수  foo를 패키지 foo.bar에 선언<br />fun foo() { }<br /><br />class Foo {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;// 함수 bar는 Foo의 인스턴스를 생성해야 사용가능 <br />&nbsp;&nbsp;&nbsp;&nbsp;fun bar() { }<br />} |

<br/>

클래스가 아니라 패키지 단위로 선언하는 경우 패키지에 종속되므로 다음과 같이 **import {패키지 이름}. {값 또는 함수 이름}**를 사용하여 자바의 정적 필드와 메서드를 대체할 수 있습니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| import foo.bar.Foo;<br /><br />public class Bar {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;public void bar() {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// Foo 클래스 내의 정적 필드 FOO 값 참조<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;int foo = Foo.FOO;<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// Foo 클래스 내의 정적 메서드 foo 호출<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Foo.foo();&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} | import foo.bar.FOO<br />import foo.bar.foo<br /><br />class Bar {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;fun bar() {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// foo.bar 패키지 내의 값 FOO를 참조<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;val foo = FOO<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// foo.bar 패키지 내의 함수 foo를 호출<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;foo()<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} |

<br/>

그러나, 클래스 내 **private**으로 선언된 멤버에 접근해야 하는 팩토리 메서드는 패키지 단위로 구현할 수 없습니다. 이런 경우 **동반 객체(companion object)**를 사용하면 클래스 내 모든 멤버에 접근할 수 있으며 인스턴스 생성 없이 호출할 수 있는 함수를 작성할 수 있습니다.

```kotlin
// 생성자의 접근 제한자가 priavte으로 외부에선 접근할 수 없습니다.
class user private constructor(val name: String, val registerTime: Long) {
    
    companion object {
      
        // companion object는 클래스 내부에 존재하므로 
        // priavte에 접근 가능
        fun create(name: String) : User {
            return User(name, System.currentTimeMillis())
        }
    }
}
```

<br/>

<br/>

<h3>싱글톤</h3>

자바에서는 싱글톤 패턴을 만족하는 클래스를 작성하기 위해 몇가지 작업이 필요하지만, 코틀린에선 오브젝트(object)를 사용하여 이를 간편하게 선언할 수 있습니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public final class Singleton {<br />&nbsp;&nbsp;&nbsp;&nbsp;private static Singleton instance = null;<br />&nbsp;&nbsp;&nbsp;&nbsp;String name = "jongwon"<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;private Singleton() { } <br /><br />&nbsp;&nbsp;&nbsp;&nbsp;public static synchronized Singleton<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;getInstance() {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if( instance == null) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;instnace = new Singleton();<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return instance;<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} | object Singleton {<br />&nbsp;&nbsp;&nbsp;&nbsp;val name = "jongwon"<br />} |

<br/>

<br/>

<h3>enum 클래스</h3>

코틀린의 enum클래스는 자바의 enum 타입과 동일한 역할을 하며, 선언 형태만 약간 다릅니다. 다음은 label이라는 이름으로 필드와 프로퍼티를 추가한 예입니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public enum Direction {<br />&nbsp;&nbsp;&nbsp;&nbsp;NORTH("N"), SOUTH("S"), WEST("W"), EAST("E");<br />&nbsp;&nbsp;&nbsp;&nbsp;public String label;<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;Direction(String label) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;this.label = label;<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} | enum class Direction(val label: String) {<br />&nbsp;&nbsp;&nbsp;&nbsp;NORTH("N"), SOUTH("S"), WEST("W"), EAST("E")<br />} |

<br/>

<br/>

<h3>중첩 클래스</h3>

특정 클래스 간 종속관계가 있는 경우  **중첩 클래스(nested class)**로 표현할 수 있습니다. 자바에서는 정적 중첩 클래스를 선언하기 위해 `static`키워드를 추가하지만 코틀린에서는 별도의 키워드를 붙이지 않습니다. 반대로 비 정적 중첩 클래스의 경우 자바에서는 아무런 키워드를 추가하지 않는 반면, 코틀린에서는 `inner`키워드를 추가해야합니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| class Outer {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;// &nbsp;&nbsp;&nbsp;&nbsp;를 사용하여 정적 중첩 클래스 선언<br />&nbsp;&nbsp;&nbsp;&nbsp;**static** class StaticNested {<br />&nbsp;&nbsp;&nbsp;&nbsp;<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;// 키워드가 없으면 비 정적 중첩 클래스로 간주<br />&nbsp;&nbsp;&nbsp;&nbsp;class NonStaticNested {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} | class Outer { <br /><br />&nbsp;&nbsp;&nbsp;&nbsp;// 키워드가 없으면 정적 중첩 클래스로 간주<br />&nbsp;&nbsp;&nbsp;&nbsp;class StaticNested {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;}<br /><br /><br />&nbsp;&nbsp;&nbsp;&nbsp;// **inner 키워드**를 사용하여 비 정적 중첩 클래스 선언<br />&nbsp;&nbsp;&nbsp;&nbsp;**inner** class NonStaticNested {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} |

<br/>

<br/>

<br/>

<br/>

<h2>4. 자료/자료형의 확인 및 변환</h2>

<br/>

<h3>자료의 동일성 확인 : ==, === 연산자</h3>

자바에서는 자료의 동일성을 확인하기 위해 == 연산자를 사용할 수 있지만, 대부분의 일반 객체는 객체 자체가 동일한지 여부도 함께 확인하기 때문에 객체의 값만 비교하려면 `equals()` 메서드를 사용해야 합니다. 하지만 코틀린에서는 비교 대상이 **객체의 값**인 경우 **== 연산자**를 사용하고, **객체 자체**인 경우 **=== 연산자**를 사용하면 됩니다.

```kotlin
val a : Pair<Char, Int> = Pair('A', 65)
val b = a
val c : Pair<Char, Int> = Pair('A', 65)

// a와 b의 값이 동일하므로 true
val aEqualsToB : Boolean = a == b

// a와 c의 값이 동일하므로 true
val aEqualsToC : Boolean = a == c

// a와 b는 동일한 객체이므로 true
val aIdenticalToB : Boolean = a === b

// a와 c는 동일한 객체가 아니므로 false
val aIdenticalToC : Boolean = a === c
```

<br>

<br>

<h3>자료형 확인 : is 연산자</h3>

코틀린에서는 자료형을 확인하기 위해 **is 연산자**를 사용하며, 이는 자바의 instanceOf 연산자와 동일한 기능을 합니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public void printTypeName(Object obj) {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;If ( obj **instanceof** Integer) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.d("Type", "Type = Integer");<br />&nbsp;&nbsp;&nbsp;&nbsp;} else If ( obj **instanceof** Float) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.d("Type", "Type = Float");<br />&nbsp;&nbsp;&nbsp;&nbsp;} elseIf ( obj **instanceof** String) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.d("Type", "Type = String");<br />&nbsp;&nbsp;&nbsp;&nbsp;} else {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.d("Type", "Unknown type");<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} | fun printTypeName(obj : Any) {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;If ( obj **is** Integer) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.d("Type", "Type = Integer");<br />&nbsp;&nbsp;&nbsp;&nbsp;} else If ( obj **is** Float) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.d("Type", "Type = Float");<br />&nbsp;&nbsp;&nbsp;&nbsp;} elseIf ( obj **is** String) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.d("Type", "Type = String");<br />&nbsp;&nbsp;&nbsp;&nbsp;} else {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.d("Type", "Unknown type");<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} |

<br>

<br>

<h3>자료형 변환 : as 연산자</h3>

자바에서는 특정 변수의 자료형을 변환하기 위해 괄호를 사용합니다. 코틀린에서는 괄호 대신 **as 연산자**를 사용하여 자료형을 변환합니다. 

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public void processNumber(Number number) {<br />&nbsp;&nbsp;&nbsp;&nbsp;Integer foo = **(**Integer**)** number; <br />} | fun processNumber (number: Number) {<br />&nbsp;&nbsp;&nbsp;&nbsp;val foo : Int = number **as** Int<br />} |

<br>

또한 코틀린에서는 자료형 추론이 가능할 경우 캐스팅 없이 해당하는 자료형으로 객체를 사용할 수 있도록 **스마트 캐스트 기능**을 val 변수에 한해서만 지원합니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| @Override<br />public void onBindViewHolder(<br />&nbsp;&nbsp;&nbsp;&nbsp;RecyclerView.ViewHolder holder, <br />&nbsp;&nbsp;&nbsp;&nbsp;int position) {<br /><br /><br />&nbsp;&nbsp;&nbsp;&nbsp;if(holder instanceof PhotoHolder) {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// PhotoHolder 내의 메서드 호출 위해 다시 캐스팅<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(**(**PhotoHolder**)** holder).setImageUrl(mImageUrl);<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;} else if (holder instanceof TextHolder) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(**(**TextHolder**)** holder).setText(mTitles[position]);<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} | override fun onBindViewHolder (<br />&nbsp;&nbsp;&nbsp;&nbsp;holder: RecyclerView.ViewHolder, <br />&nbsp;&nbsp;&nbsp;&nbsp;position: Int) {<br />&nbsp;&nbsp;&nbsp;&nbsp;if(holder **is** PhotoHolder) {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 스마트 캐스트가 지원되어 캐스팅 없이 사용 가능<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;holder.setImageUrl(mImageUrl)<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;} else if (holder **is** TextHolder) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;holder.setText(mTitles[position])<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} |

<br/>

<br/>

<br/>

<br/>

<h2>5. 흐름 제어</h2>

<br>

<h3>if-else 문</h3>

코틀린에서도 자바와 동일하게 **if-else문**을 사용하여 조건문을 작성할 수 있습니다. 코틀린의 if-else문은 추가적으로 값을 반환할 수 있습니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| int age = 25;<br />String ageRange;<br /><br />if (age >= 10 && age < 20) {<br />&nbsp;&nbsp;&nbsp;&nbsp;ageRange = "10대";<br />} else if (age >= 20 && age < 30) {<br />&nbsp;&nbsp;&nbsp;&nbsp;ageRange = "20대";<br />} else {<br />&nbsp;&nbsp;&nbsp;&nbsp;ageRange = "기타";<br />} | val age: Int = 25<br />val ageRange : String = if (age >= 10 && age < 20) {<br />&nbsp;&nbsp;&nbsp;&nbsp;"10대"<br />} else if (age >= 20 && age < 30) {<br />&nbsp;&nbsp;&nbsp;&nbsp;"20대"<br />} else {<br />&nbsp;&nbsp;&nbsp;&nbsp;"기타"<br />} |

<br>

<br>

<h3>when 문</h3>

코틀린의 **when 문**은 자바의 switch 문을 대체합니다. 자바에서는 break를 사용하여 각 경우를 구분하지만, 코틀린은 중괄호를 사용하여 구분합니다.  when 문도 if-else문과 마찬가지로 값을 반환할 수 있습니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| int bags = 1;<br /><br />switch (bags) {<br />&nbsp;&nbsp;&nbsp;&nbsp;case 0:<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.d("Bags", "We have no bags");<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;break;<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;case 1:<br />&nbsp;&nbsp;&nbsp;&nbsp;case 2:<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.i("Bags", "Extra charge required");<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.d("Bags", "We have : "+ bag + "bag(s)");<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;break;<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;default: <br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.e("Bags", "Cannot have more");<br />} | val bags: Int = 1<br /><br />when (bags) {<br />&nbsp;&nbsp;&nbsp;&nbsp;// 각 case에 해당하는 값만 적습니다.<br />&nbsp;&nbsp;&nbsp;&nbsp;0 -> Log.d("Bags", "We have no bags")<br /><br /><br />&nbsp;&nbsp;&nbsp;&nbsp;// 여러 개의 case는 **쉼표**로 구분하여 적습니다.<br />&nbsp;&nbsp;&nbsp;&nbsp;1**,** 2 -> {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.i("Bags", "Extra charge required");<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log.d("Bags", "We have $bags bag(s)");<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;// default 대신 **else**로 표현합니다.<br />&nbsp;&nbsp;&nbsp;&nbsp;**else** -> log.e("Bags", "Cannot have more")<br />} |

<br>

각 경우의 조건을 상수 값만 지정할 수 있었던 자바와 달리, 코틀린에서는 각 조건을 표현식으로 작성할 수 있습니다.

```kotlin
val e : Exception = ... // 값 e에 여러 종류의 예외가 대입될 때

// 예외의 종류에 알맞은 로그 메세지를 출력합니다.
when (e) {
    is IOException -> Log.d("Message", "Network Error")
    is IllegalStateException -> Log.d("Message", "Invalid State")
    ...
}

val str : String = ... // 값 str에 임의의 문자열이 대입될 때

// 문자열의 첫 문자에 따라 알맞은 로그 메세지를 출력합니다.
when (str) {
    str.startsWith('a') -> Log.d("Message", "A for Android")
    str.startsWith('k') -> Log.d("Message", "K for Kotlin")
}
```

<br>

<br>

<h3>while 문</h3>

코틀린의 while 문과 do while 문의 기능 및 문법은 코틀린 문법의 일반적인 특징(세미콜론이 없다, ...)을 제외하면 자바와 **완전히 동일**합니다.
<br>

<br>

<h3>for 문</h3>

자바가 for 문과 for-each 문을 지원하는 반면 코틀린은 **for-each 형태만** 지원하며, 반복자를 통해 접근하는 인자의 타입을 생략할 수 있습니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| List<String> names = ... // 이름 목록<br /><br /><br />// for-each<br />for(String name : names) {<br />&nbsp;&nbsp;&nbsp;&nbsp;// 이름과 함께 로그 출력<br />&nbsp;&nbsp;&nbsp;&nbsp;Log.d("Name", "name=" + name);<br />} | val names : List<String> = ... // 이름 목록<br /><br />// 변수 name의 타입은 리스트 names를 통해 추론하므로<br />// 타입을 적지 않아도 됩니다.<br />for(name in names) {<br />&nbsp;&nbsp;&nbsp;&nbsp;// 이름과 함께 로그 출력<br />&nbsp;&nbsp;&nbsp;&nbsp;Log.d("Name", "name = $name"<br />) |

<br>

for 문 내에서 현재 항목의 인덱스가 필요할 경우, **Collection.indicies** 프로퍼티를 사용하면 인덱스 인자로 배열 내 항목에 접근할 수 있습니다.

```kotlin

```

<br>

<br>

<h3>범위</h3>

범위(range)는 코틀린에만 있는 독특한 자료구조로, **.. 연산자**를 사용하여 특정 범위를 순환하거나 해당 범위 내에 특정 항목이 포함되어 있는지 확인합니다.  **until 함수**를 사용하면 가장 마지막 값을 포함하지 않는 범위를 생성할 수 있습니다.

```kotlin
// 시작과 끝을 포함하는 범위를 정의합니다.
val myRange : IntRange = 0..10 // 0부터 10까지

// myRange와 동일한 항목을 포함하는 범위
val myRange2 : IntRange = 0 until 11

// 앞에서 정의한 범위 내를 순환하는 for문
for(i in myRange) { /* Do Something */ }

// for 문 내에서 바로 범위를 정의할 수 있습니다.
for(i in 0..10) { /* Do Something */ }
```

<br>

범위 내에 특정 항목이 있는지 알아보려면 **in 연산자**를 사용합니다.

```kotlin
val myRange : IntRange = 0..10 // 범위 지정

// 5가 myRange 내에 포함되어 있는지 확인 : true 반환
val foo : Boolean = 5 in myRange
```

<br>

항목들의 순서가 반대로 정렬된 범위를 생성하려면 **downTo()**함수를 사용합니다. 첫 번째 인자로 시작 값을, 두 번째 인자로 마지막 값을 대입합니다. downTo() 함수는 기본적으로 1씩 감소시키며, **step()** 함수를 사용하면 감소 폭을 변경할 수 있습니다.

```kotlin
// '54321' 출력
for(i in 5 downTo 1) {
    System.out.print(i)
}

// '531' 출력
for(i in 5 downTo 1 step 2) {
    System.out.print(i)
}
```

<br>

<br>

<br>

<br>

<h2>6. 제네릭</h2>

제네릭(generics) 혹은 제네릭 타입(generic type)은 인자로 사용하는 타입에 따라 구체화되는 클래스나 인터페이스를 의미합니다.

<br>

<h3>제네릭 클래스의 인스턴스 생성 및 사용</h3>

코틀린에서의 제네릭 클래스는 자바와 동일하게 **꺽쇠 <> 안에 타입을 넣어 표현**합니다. 제네릭 클래스에 타입을 넣지 않고 선언이 가능한 자바와 달리, 코틀린은 반드시 타입을 넣어 주어야 합니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Map<String, String> entries;<br /><br />// 컴파일 가능<br />// List<Object>로 암시적으로 선언<br />List names; | val entries : Map<String, String><br /><br />// 컴파일 오류<br />val names: List |

<br>

<br>

<h3>제네릭 클래스/인터페이스 정의</h3>

제네릭을 사용하는 클래스나 인터페이스를 정의하는 방법과 인자로 받을 수 있는 타입을 한정하는 방법 또한 자바와 동일합니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| class Car{<br />&nbsp;&nbsp;&nbsp;&nbsp;...<br />}<br /><br />// 항목을 담거나 뺄 수 있는<br />// 제네릭 인터페이스 Container 정의<br />interface Container<T> {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;void put(T item);<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;T take();<br />}<br /><br />// 자동차(Car)를 담거나 뺄 수 있는<br />// 클래스 Garage 정의<br /><br />class Garage implements Container<Car> {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;@Override<br />&nbsp;&nbsp;&nbsp;&nbsp;public void put (Car item) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;@Override<br />&nbsp;&nbsp;&nbsp;&nbsp;public Car take (Car item) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} | class Car{<br />&nbsp;&nbsp;&nbsp;&nbsp;...<br />}<br /><br />// 항목을 담거나 뺄 수 있는<br />// 제네릭 인터페이스 Container 정의<br />interface Container<T> {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;fun put(item : T)<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;fun take() : T<br />}<br /><br />// 자동차(Car)를 담거나 뺄 수 있는<br />// 클래스 Garage 정의<br /><br />class Garage : Container<Car> {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;override fun put (item: Car) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br /><br /><br />&nbsp;&nbsp;&nbsp;&nbsp;override fun take(): Car {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} |

<br>

<br>

<h3>제네릭을 인자로 받는 함수</h3>

타입이 정의되어 있는 제네릭을 인자로 받거나 호출 시점에 타입을 지정하는 함수는 자바와 동일한 방법으로 정의합니다. 자바에서의 **? super T, ? extends T**는 코틀린에서 각각 **in T, out T**로 사용가능합니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| // 자동차 클래스<br />class Car { ... }<br /><br />// 승용차 클래스<br />class Sedan extends Car { ... }<br /><br />// 트럭 클래스<br />class Truck extends Car { ... }<br /><br />// dst로 받은 목록을 dest에 추가합니다.<br /><T> void append(List<? super T> dest,<br />&nbsp;&nbsp;&nbsp;&nbsp;List<? extends T> dest) { <br />&nbsp;&nbsp;&nbsp;&nbsp;dest.addAll(dst);<br />}<br /><br />// 사용 예<br /><br />// 일반 승용차 리스트 생성<br />List<Sedan> sedans = ...;<br /><br />// 트럭 리스트 생성<br />List<Truck> trucks = ...;<br /><br />// 자동차를 담을 수 있는 리스트 생성<br />List<Car> cars = ...;<br /><br />// 자동차를 담는 리스트에 승용차 리스트 추가<br />append.(cars, sedans);<br /><br />// 자동차를 담는 리스트에 트럭 리스트 추가<br />append(cars, trucks); | // 자동차 클래스<br />open class Car { ... }<br /><br />// 승용차 클래스<br />class Sedan : Car { ... }<br /><br />// 트럭 클래스<br />class Truck : Car { ... }<br /><br />// src로 받은 목록을 dest에 추가합니다.<br />fun <T> append(dest: MutableList<in T>,<br />&nbsp;&nbsp;&nbsp;&nbsp;src: List<out T>) { <br />&nbsp;&nbsp;&nbsp;&nbsp;dest.addAll(src)<br />}<br /><br />// 사용 예<br /><br />// 일반 승용차 리스트 생성<br />val sedans: List<Sedan> = ...<br /><br />// 트럭 리스트 생성<br />var trucks: List<Truck> = ...<br /><br />// 자동차를 담을 수 있는 리스트 생성<br />val cars: MutableList<Car> cars = ...<br /><br />// 자동차를 담는 리스트에 승용차 리스트 추가<br />append.(cars, sedans)<br /><br />// 자동차를 담는 리스트에 트럭 리스트 추가<br />append(cars, trucks) |

<br>

<br>

<br>

<br>

<h2>7. 예외</h2>

코틀린에서의 예외는 자바와 거의 동일합니다. 객체 생성 시와 마찬가지로 new 키워드는 사용하지 않습니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public void checkAge(int age) {<br />&nbsp;&nbsp;&nbsp;&nbsp;if (age < 0) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;throw new IllegalArgumentException<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;("Invalid age: " + age);<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} | fun checkAge(age:Int) {<br />&nbsp;&nbsp;&nbsp;&nbsp;if (age < 0) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;throw IllegalArgumentException<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;("Invalid age: $age")<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} |

<br>

예외 처리를 하려면 자바와 동일하게 try-catch 및 finally 문을 사용하면 됩니다. 단, 코틀린에서 Checked exception을 따로 검사하지 않으며 try-catch 문은 값을 반환할 수 있습니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public String readFromJson<br />&nbsp;&nbsp;&nbsp;&nbsp;(String fileName) throws IOException {<br />&nbsp;&nbsp;&nbsp;&nbsp;// IOException 유발 코드<br />}<br /><br />public void process() {<br />&nbsp;&nbsp;&nbsp;&nbsp;String json = null;<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;try {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;json = readFromJson("foo.json")<br />&nbsp;&nbsp;&nbsp;&nbsp;} catch (IOException e) {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...<br />&nbsp;&nbsp;&nbsp;&nbsp;}<br />} | fun readFromJson(fileName: String)<br />&nbsp;&nbsp;&nbsp;&nbsp;: String {<br />&nbsp;&nbsp;&nbsp;&nbsp;// IOException 유발 코드<br />}<br /><br />fun process() {<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;// try-catch 문을 사용하지 않아도 됩니다.<br />&nbsp;&nbsp;&nbsp;&nbsp;val json: String = readFromJson("foo.json")<br />} |

<br>

<br>

<br>

<br>

<h2>8. 널 안정성</h2>

코틀린은 널 포인터 예외 문제를 해결하기 위해 모든 타입에 명시적으로 널 허용 여부를 함께 표기합니다.

<br>

<h3>널 허용 여부 표기</h3>

코틀린은 별도 표기가 없을 경우 **널 값을 허용하지 않습니다**. 또한 널 값을 허용하지 않는 값을 **초기화하지 않거나, null을 대입하면** 컴파일 오류를 발생시킵니다. 널 값을 가질 수 있도록 하려면 명시적으로 타입 뒤에 `?` 를 붙여주어야 합니다.

```kotlin
val nullableString : String? = null
val nonNullString : String = "Foo"

val name : String           // 오류 : 값이 초기화되지 않음
val address : String = null // 오류 : null을 허용하지 않는 값에 null 대입
```

<br>

<br>

<h3>널 값을 대신하는 방법 : 엘비스(?:) 연산자</h3>

널 값을 허용하지 않는 값 혹은 변수에 널 값을 반환할 수 있는 함수의 결과를 대입해야 하는 경우 엘비스 연산자를 사용합니다. 엘비스 연산자는 **null이 아닐 경우에는 스스로(좌항)를, null인 경우에는 기본값(우항)**을 반환합니다.

```kotlin
// foo가 null이 아닐 경우에는 foo를, null이라면 bar(기본값)를 반환
foo ?: bar

// 함수가 널 값을 반환하는 경우 PostalCode.NONE 값을 대입
val postal : PostalCode = findPostalCode("311 Dokmak Mapo") ?: PostalCode.NONE
```

<br>

<br>

<h3>널 값 확인과 처리를 한번에 : 안전한 호출(?.) 연산자</h3>

코틀린에서는 안전한 호출 연산자를 사용하여 객체가 널 값이 아는 경우에만 연산자 뒤의 문장을 수행합니다. 널 값일 경우에는 뒤의 문장을 수행하지 않고 널 값을 반환합니다.

```kotlin
// bar가 null이 아닐 경우에만 해당 값을 대입, 그렇지 않은 경우 null을 foo에 대입
val foo = bar?.baz

// foo가 null이 아닐 경우에만 bar() 호출
foo?.bar()
```

<br>

엘비스(?:) 연산자를 함께 사용하면 널 값을 반환할 때, 대신 사용할 값을 지정할 수 있습니다.

```kotlin
val contact : Contact = ... // 주소록 항목 객체

// 주소가 없거나 line2가 없을 경우 기본값인 "No address" 반환
val line : String = contact.address?.line2 ?: "No address"
```

<br>

<br>

<h3>안전한 자료형 변환 : as? 연산자</h3>

안전한 변환(as?) 연산자는 **자료형 변환이 실패할 경우** 예외를 발생시키는 대신 **널 값을 반환**합니다. 변환에 실패했을 때 널 값을 반환하므로, 엘비스 연산자를 함께 사용하면 변환에 실패할 경우 기본값을 지정할 수 있습니다.

```kotlin
val foo : String = "foo"

// 자료형 변환에 실패하므로 bar에는 널 값이 할당됩니다.
val bar : Int? = foo as? Int

// 엘비스 연산자를 사용해 널 허용 여부 수정없이 실패한 경우 기본값(0)으로 지정합니다.
val bar2 : Int = foo as? Int ?: 0
```

<br>

<br>

<h3>널 값이 아님을 명시하기 : 非 널 값 보증(!!)</h3>

비 널 값 보증을 사용하면 널 값을 포함할 수 있는 타입을 **널 값을 포함하지 않는 타입으로 변환**하여 사용할 수 있습니다. 보증하려는 항목 뒤에 `!!`을 붙여 사용합니다.

```kotlin
// 값 foo는 널 값을 포함할 수 있는 Foo 타입
val foo: Foo? = ...

// 값 foo는 널 값을 포함하지 않음을 보증
val nonNullFoo : Foo = foo!!
val nonNullFoo : Foo = foo // 에러

// 값 foo가 널값이 아님을 보장하면서 bar() 함수 호출
foo!!.bar()

// 값 foo값 널 값이 아님을 보장하면서 baz 프로퍼티 접근
val myBaz = foo!!.baz
```

<br>

비 널 값 보증을 사용하였으나 실제 객체에 널 값이 들어가 있을 경우, 널 포인터 예외가 발생하므로 **유의하여 사용해야 합니다**.

<br>

<br>

<h3>나중에 초기화되는 변수를 위해 : lateinit 키워드</h3>

클래스의 프로퍼티는 의존성 주입을 사용하거나 설계상 이유로 클래스를 생성한 후 나중에 따로 초기화를 수행하는 경우도 있습니다. 코틀린은 널 값을 허용하지 않는 경우 값을 초기화하도록 강제하고 있지만, **lateinit 키워드**를 사용하면 초기화 없이 변수만 선언할 수 있습니다.

```kotlin
class MyActivity : Activitiy() {
    
    // 나중에 초기화를 수행할 객체로 표시하였으므로 바로 초기화를 하지 않아도 됩니다.
    lateinit var api : Api
    ...
}
```

<br>

비 널 값 보증과 마찬가지로 초기화를 하지 않은 상태로 사용하려 하면 널 포인터 예외가 발생하니 **초기화 작업을 빠뜨리지 않도록 유의**해야 합니다.

<br>

<br>

<h3>자바로 작성된 클래스의 널 처리</h3>

자바로 작성된 클래스는 기본적으로 널 값을 허용하도록 처리되며, 코틀린에서는 이를 **플랫폼 타입**이라 부릅니다. 플랫폼 타입은 **Type!**과 같은 형태로 표시되며 개발자가 직접 사용할 수 없습니다.

```kotlin
val myPlatformType : MyType! = ... // 오류: 플랫폼 타입을 선언할 수 없습니다.
```

<br>

그러나, 플랫폼 타입은 코틀린에서 값 및 변수의 타입을 지정할 때 널을 허용하는 타입과 그렇지 않은 타입에 자유롭게 할당할 수 있습니다.

```kotlin
val person : Person = ... // Person(자바로 작성된 클래스) 객체 생성

val n1 : String = person.name
val n2 : String? = person.name
```

<br>

따라서 널 포인터 예외를 피하기 위해 항상 객체의 널 값 여부를 확인해야하며, 코틀린은 어노테이션을 인식하여 객체의 널 허용 여부를 판단합니다. 어노테이션의 종류는 여러가지이며 그 중 **@Nullable**을 적용하면 다음과 같습니다.

```java
// java
class Person {
    
    @Nullable
    String name;
    
    public String getName() {
        return name;
    }
}
```

```kotlin
// kotlin
val person : Person = ... // Person 객체 생성

// 실패 : 값 n1은 널 값을 허용하지 않습니다.
val n1 : String = person.name

// 성공 : 값 n2는 널 값을 허용합니다.
val n2 : String? = person.name
```



<br><br>  

<h1>자바와는 다른 코틀린의 특징</h1>  

  <br><br><br><br>

<h2>1. 클래스</h2> 

<br>

<h3>데이터 클래스</h3>

자료를 저장하는 클래스를 만드는 과정을 단순하게 하기 위해, 코틀린에서는 데이터 클래스를 제공합니다. 데이터 클래스는 자료를 구성하는 프로퍼티만 선언하면 컴파일러가 `equals()`, `hashCode()`, `toString()` 함수를 자동으로 생성해줍니다.

```kotlin
data class person(val name: String, val address: String)

val john = Person("John Doe", "Somewhere")
val hyun = Person("Taehyun", "USA")

println("${john == hyun}")    // false
println("${john.hashCode()}") // -1126692462
println("$hyun")              // Person(name=Taehyun, address=USA)
```

<br>

<br>

<h3>한정 클래스</h3>

한정 클래스는 enum 클래스를 확장한 개념을 가진 클래스로, enum 클래스와 달리 인스턴스를 여러 개 생성할 수 있습니다. 다음은 MobileApp이라는 한정 클래스와 이를 상속하는 Android, IOS 클래스를 정의한 예를 보여줍니다.

```kotlin
sealed class MobileApp(val os: String) {
    class Android(os: String, val packageName: String) : MobileApp(os)
    class IOS(os: String, val bundleId: String) : MobileApp(os)
}
```

<br>

한정 클래스로 지정하고 else 절을 사용하지 않도록 하면 when 문에서 모든 클래스를 처리했는지 여부를 알 수 있으므로 **새로 추가된 유형에 대한 처리가 누락되는 것을 방지**할 수 있습니다. 

```kotlin
fun whoami(app: MobileApp) = when (app) {
    is MobileApp.Android -> println("${app.os} / ${app.packageName}")
    is MobileApp.IOS -> println("${app.os} / ${app.bundleId}")
    // 모든 경우를 처리했으므로 else를 쓰지 않아도 됩니다.
}
```

 <br>다음 코드는 MobileApp 클래스가 한정 클래스이고, 새로운 유형인 WindowsMobile 클래스가 추가되었을 때 컴파일 에러가 발생하는 예입니다.

```kotlin
// when 문에서 Android, IOS의 경우만 처리하고 새로 추가된 유형은 처리하고 있지 않으므로
// 컴파일 에러가 발생합니다.
fun whoami(app: MobileApp) = when (app) {
    is MobileApp.Android -> println("${app.os} / ${app.packageName}")
    is MobileApp.IOS -> println("${app.os} / ${app.bundleId}")
    // else나 WindosMobile에 대한 처리가 누락되어 있습니다.
}
```

<br>

<br>

<h3>프로퍼티의 사용자 지정 Getter/Setter</h3>

사용자 지정 Getter/Setter를 사용하면 프로퍼티에서 Getter 및 Setter의 구현을 원하는 대로 변경할 수 있습니다. 다음은 프로퍼티를 정의할 때 사용하는 문법을 보여줍니다.

```kotlin
var <propertyName>[: <PropertyType>] [=<property_initializer>]
	[<getter>]
	[<setter>]
```

<br>

다음은 사람에 대한 정보를 표현할 수 있는 클래스에서 **사용자 지정 Getter/Setter를 이용하여** 나이에 따른 성인 여부와 입력된 주소의 앞 10자만 저장하도록 구현한 코드입니다.

```kotlin
class Person(val age: Int, val name: String) {
    
    val adult: Boolean
		get() = age >= 19
    
    // Setter는 읽고 쓰기가 모두 가능한 var에서만 사용가능
    var address: String = "" 
    	set(value) {
        	// 인자로 들어온 문자열의 앞 10자리만 필드에 저장
            field = value.substring(0..9)
    	}
}
```

<br>

<br>

<br>

<br>

<h2>2. 함수</h2>

코틀린의 함수는 자바의 메서드와 동일한 기능을 수행하지만, 표현 형태가 더 자유롭고 자바의 메서드에서는 제공하지 않는 여러 유용한 기능을 갖추고 있습니다.

<br>

<h3>명명된 인자</h3>

메서드의 매개변수가 선언된 순서에 맞춰 인자를 대입해야 하는 자바와 달리, 코틀린에서는 **명명된 인자**를 사용함으로써 함수를 호출할 때 **매개 변수의 순서와 상관없이 인자를 전달**할 수 있습니다.

```kotlin
// 원을 그리는 함수
fun drawCircle(x: Int, y:Int, radius: Int) {
    ...
    println("x = $x | y = $y | radius = $radius")
}

// 명명된 인자를 사용하여 함수 호출
drawCircle(radius = 25, x = 10, y = 5) // x = 10 | y = 5 | radius = 25
```

<br>

<br>

<h3>기본 매개변수</h3>

자바에서는 매개변수에 아무 값이 대입되지 않을 경우 기본값을 지정할 수 없기에 메서드를 별도로 만들어 사용해야했습니다. 하지만 코틀린에서는 함수의 매개변수에 기본값을 지정할 수 있으며, 이때 지정하는 값을 **기본 매개변수**라 부릅니다.

```kotlin
// 반지름의 기본값으로 25를 갖는 함수
fun drawCircle(x: Int, y: Int, radius: Int = 25) {
    ...
}

// 중심축(x,y)이 (10,5)인 원을 그립니다.
// 반지름을 지정하지 않았으므로 반지름은 25가 됩니다.
drawCircle(10,5)
```

<br>

<br>

<h3>단일 표현식 표기</h3>

메서드 내용을 항상 중괄호 `{}`로 감싸야 했던 자바와 달리, 코틀린에서는 unit 타입을 제외한 타입을 반환하는 함수라면 함수의 내용을 **단일 표현식**을 사용하여 정의할 수 있습니다.

```kotlin
fun singleExpressionPractice(): Int {
    return 21 * 23
}

// 단일 표현식 표기를 사용하면 다음과 같이 정의할 수 있습니다.
fun singleExpressionPractice() : Int = 21 * 23

// 단일 표현식 표기를 사용하는 경우, 반환 타입을 생략하는 것도 가능합니다.
fun singleExpressionPractice() = 21 * 23
```

<br>

<br>

<h3>확장 함수</h3>

코틀린에서는 **확장 함수**를 사용하여 상속 없이 기존 클래스에 새로운 함수를 추가할 수 있습니다. 확장함수를 추가할 대상 클래스는 **리시버 타입**이라 부르며, 이 뒤에 점 `.`을 찍고 원하는 함수의 형태를 적는 방식으로 정의합니다.

```kotlin
// String 클래스에 withPostfix() 함수를 추가합니다.
// this를 사용하여 인스턴스에 접근할 수 있습니다.
private fun String.withPostfix(postFix: String) = "$this$postFix"

// this를 사용하여 인스턴스에 접근할 수 있으므로, 앞에서 정의한 확장 함수를 사용할 수 있습니다.
fun String.withBar() = this.withPostfix("Bar")

val foo = "Foo"

// String 클래스에 포함된 함수를 호출하듯이 사용합니다.
val foobar = foo.withBar() // FooBar
```

<br>

확장함수는 엄연히 클래스 외부에서 정의하는 함수이므로 리시버 객체에서는 **클래스 내 public**으로 정의된 프로퍼티나 함수에만 접근할 수 있습니다.

<br>

<br>

<h3>연산자 오버로딩</h3>

코틀린은 사용자 정의 타입에 한해 각 연산자별로 사전 정의된 함수를 재정의하는 방식으로 연산자 오버로딩을 사용할 수 있습니다. 연산자 오버로딩을 위한 함수는 함수 정의에 `operator` 키워드가 추가되며 **기존의 연산자를 재정의 하는 것만 허용**합니다. 

<br>

| 단항 연산자 | 함수       | 이항 연산자 | 함수  | 비교 연산자 | 함수      | 인덱스 연산자 | 함수     |
| ----------- | ---------- | ----------- | ----- | ----------- | --------- | ------------- | -------- |
| +           | unaryPlus  | +           | plus  | >           | compareTo | [ ]           | get      |
| -           | unaryMinus | -           | minus | <           | compareTo | [ ]           | set      |
| !           | not        | *           | times | >=          | compareTo |               |          |
| ++          | inc        | /           | div   | <=          | compareTo | **in 연산자** | **함수** |
| --          | dec        | %           | rem   |             |           | in            | contains |



```kotlin
class Volume(var left: Int, var right: Int) {
    
    // 단항 연산자 '++'를 재정의합니다.
    operator fun inc() : Volume {
        this.left += 1
        this.right += 1
        return this
    }   
}

// 확장 함수를 사용하여 연산자 재정의도 가능합니다.
// 이항 연산자 '-'를 재정의합니다.
operator fun Volume.minus(other: Volume): Volume {
    return Volume(this.left - other.left, this.right - other.right)
}

var volume = Volume(50, 50)
val v1 = volume++ // (51, 51)
val v2 = Volume(30,30) - Volume(20,20) // (10, 10)

```

<br>

이 밖에도 **비교 연산자**, **인덱스 접근 연산자**, **복합 할당 연산자도** 각 연산자에 해당 하는 함수를 위와 같이 재정의하여 사용할 수 있습니다.

<br>

<br>

<h3>중위 표기법 지원</h3>

코틀린에서는 사용자가 정의한 함수를 **중위 표기법**을 사영하여 호출할 수 있으며, 해당 함수는 다음 조건을 만족해야 합니다.

- 함수 선언에 **infix 키워드**를 표기해야 합니다.
- 확장 함수 혹은 멤버 함수이면서, 매개 변수가 하나여야 합니다.

```kotlin
class Volume(var left: Int, var right: Int) {
    
    // 멤버로 선언된 함수에 중위 표기를 지원하도록 합니다.
    infix fun increaseBy(amount: Int) {
        this.left += amount
        this.right += amount
    }
}

// 확장 함수로 선언된 함수에 중위 표기를 지원하도록 합니다.
infix fun Volume.decreaseBy(amount: Int) {
    this.left -= amount
    this.right -= amount
}

val currentVolume = Volume(50,50)

// currentVolume.increaseBy(30)과 동일
currentVolume increaseBy 30  // (80, 80)

// currentVolume.decreaseBy(50)과 동일
currentVolume decreaseBy 50  // (30, 30)
```

<br>

<br>

<br>

<br>

<h2>3. 람다 표현식</h2>

<br>

<h3>자바와 코틀린의 람다 표현식</h3>

람다 표현식은 하나의 함수를 표현할 수 있습니다. 특히 **익명 클래스**를 간결하게 표현할 수 있으므로 매우 유용합니다. 다음은 자바에서 익명 클래스를 사용하여 버튼의 리스너를 설정하는 코드입니다.

```java
// java 7 및 이전
Button button = ... // 버튼 인스턴스
button.setOnClickListener(new View.onClickListener() {
	@Override
    public void onClick(View v) {
        doSomething();
    }
});


// java 8
Button button = ... // 버튼 인스턴스

// 람다 표현식을 사용하여 리스너 선언
button.setOnClickListener((View v) -> doSomething());
// 인자의 타입 생략 가능
button.setOnClickListener(v -> doSomething());
```

<br>

자바 7 및 이전 버전에서는 문법상 한계로 인해 주요 구현부 코드보다 익명 클래스 생성 코드가 더 긴 것을 확인할 수 있으며, 자바 8부터는 익명 클래스 대신 람다 표현식으로 구현하여 간결하게 표현할 수 있습니다. **코틀린에서도 람다 표현식**을 사용할 수 있으며 자바 8의 람다 표현식과 형태가 매우 유사하고, **중괄호`[]`를 사용하여 앞뒤를 묶어준다**는 점이 다릅니다.

```kotlin
//    매개 변수      함수 본체
{ x: Int, y: Int ->  x + y  }
```

```kotlin
val button: Button = ... // 버튼 인스턴스

// 람다 표현식을 사용하여 리스너 선언
button.setOnClickListener({v:View -> doSomething()})
// 인자의 타입 생략 가능
button.setOnClickListener({v -> doSomething()})
```

<br>

코틀린에서는 **하나의 함수**만 호출하는 람다 표현식은 **멤버 참조**를 통해 간략하게 표현할 수 있습니다. 또한 함수뿐만 아니라 **프로퍼티**도 멤버 참조를 지원합니다.

```kotlin
button.setOnClickListener({v -> doSomething(v)}) // 함수 하나만 호출하고 있습니다.
button.setOnClickListener(::doSomething(v))  // 멤버 참조를 사용하여 바로 대입할 수 있습니다.
```

```kotlin
class Person(val name: String, val age: Int) {
    // 성인 여부를 표시하는 프로퍼티
    val adult = age > 19
}

// 전체 사람 목록 중, 성인의 이름만 출력
fun printAdults(people: List<Person>) {
    
    // 필터링 조건을 람다 표현식을 사용하여 대입
    // 단순히 adult 프로퍼티의 값만 반환
    people.filter({person -> person.adult}).forEach{ println("Name = ${it.name}") }
    
    // 멤버 참조를 사용하여 adult 프로퍼티를 바로 대입
    people.filter(Person::adult).forEach{ println("Name = ${it.name}") }
}
```

<br>

<br>

<h3>코틀린 람다 표현식의 유용한 기능</h3>

함수를 호출할 때 대입하는 마지막 인자가 함수 타입이고, 이 인자에 대입하는 함수가 람다 표현식을 사용한다면 이 람다 표현식은 함수의 인자를 대입하는 괄호 외부에 선언할 수 있습니다. 

```kotlin
val dialog = AlertDialog.Builder(this)
		...
		// 함수 타입의 인자를 마지막 인자로 대입하고 있습니다.
		.setPositiveButton("OK"), { dialog, which -> doOnOkay(which) })

		// 함수 타입의 마지막 인자는 괄호 외부에 선언할 수 있습니다.
		.setPositiveButton("Cancel") { dialog, which -> doOnCancel(which) }
		.create()
```

<br>

또한 단 하나의 함수 타입 매개변수를 가질 경우, 인자 대입을 위한 괄호를 생략하고 바로 람다 표현식을 사용할 수 있습니다.

```kotlin
val button: Button = ... // 버튼 인스턴스

// setOnClickListener의 마지막 인자로 함수 타입을 대입하고 있습니다.
button.setOnClickListener({ v -> doSomething()})

// 다른 인자가 없으므로, 괄호 없이 바로 외부에 람다 표현식을 사용할 수 있습니다.
button.setOnClickListener{ v -> doSomething() }
```

<br>

코틀린에서 람다 표현식 내 **매개변수가 하나인 경우** 매개변수 선언을 생략할 수 있으며, 매개변수에 대한 참조가 필요한 경우 `it`을 사용할 수 있습니다. 여러 개의 매개변수를 갖는 람다 표현식에서 **사용하지 않는 매개변수**는 이름 대신 `_`을 사용하여 명시할 수 있습니다.

```kotlin
val button: Button = ... // 버튼 인스턴스

button.setOnClickListener{ v -> doSomethingWithView(v) }
// 매개변수가 하나만 있으므로 선언을 생략하고 it을 대신 사용할 수 있습니다.
button.setOnClickListener{ doSomethingWithView(it) }

val dialog = AlertDialog.Builder(this)
		...
		// 리스너 내에 dialog 매개변수 미사용
		.setPositiveButton("OK"), { dialog, which -> doOnOkay(which) })

		// 사용하지 않는 매개변수에 이름 대신 '_' 사용 가능
		.setPositiveButton("Cancel") { _, which -> doOnCancel(which) }
		.create()
```

<br>

<br>

<h3>인라인 함수</h3>

인라인 함수를 사용하면, 함수의 매개변수로 받는 함수형 인자의 본체를 해당 인자가 사용되는 부분에 그대로 대입하므로 **성능 하락을 방지**할 수 있습니다. 인라인 함수로 선언하려면 함수 선언 앞에 **inline 키워드**를 추가하면 됩니다.

```kotlin
// 인자로 받은 함수를 내부에서 실행하는 함수
inline fun doSomething(body: () -> Unit) {
    println("onPreExcute()")
    body()
    println("onPostExecute()")
}
```

<br>

위와 같이 인라인 함수를 선언하고 ``doSomething { println("do Something") }``을 통해 인라인 함수를 호출하면, 이 구문은 컴파일 과정에서 다음과 같이 변환됩니다.

```kotlin
println("onPreExcute()")
// 인자로 전달된 함수 본체의 내용이 그대로 복사된 것을 확인할 수 있습니다.
println("do Something")
println("onPostExecute()")
```

<br>

인라인 함수의 함수형 매개변수는 별도의 표기가 없을 경우 모두 인라인 처리를 하므로, 인라인 처리를 원치 않는 경우 해당 매개 변수 앞에 **noinLine 키워드**를 추가하면 됩니다.

<br>

<br>

<br>

<br>

<h2>4. 코틀린의 여타 특징</h2>

<br>

<h3>타입 별칭</h3>

코틀린에서는 **타입 별칭**을 사용하여 복잡한 구조로 구성된 타입을 간략하게 표현할 수 있습니다. 타입 별칭은 **typealias**를 사용하여 정의합니다.

```kotlin
// 사람 정보를 저장하는 리스트
typealias PeopleList = List<Person>
// 특정 태그를 가진 사람의 리스트를 포함하는 맵
typealias PeopleInTags = Map<String, Person>

// 인자로 받은 사람에게 메세지를 보내는 함수
fun sendMessage(people: List<Person>) {
    people.forEach { /* 메세지 전송 */ }
}

// 타입 별칭을 이용하여 위 코드와 동일한 역할
fun sendMessage(people: PeopleList) {
    people.forEach { /* 메세지 전송 */ }
}
```

<br>

<br>

<h3>분해 선언</h3>

코틀린에서는 **분해 선언**을 통해 복잡한 구성을 갖는 자료구조에서 각 프로퍼티가 가진 자료의 값을 한번에 여러 개의 값(val) 혹은 변수에 할당할 수 있습니다. 

```kotlin
data class Person(val age: Int, val name: String)

val person : Person = Person(25, "jongwon") // 사람을 표현하는 객체

// 사람 객체에 포함된 필드의 값을 한번에 여러 값에 할당합니다.
val (ageOfPerson, nameOfPerson) = person

println("$ageOfPerson")  // 25
println("$nameOfPerson") // jongwon
```

<br>

분해 선언은 `componentN()`함수가 있는 클래스에서만 사용할 수 있으며, 분해 선언을 기본으로 제공하는 클래스들은 다음과 같습니다.

- 데이터 클래스로 선언된 클래스
- kotlin.Pair
- kotlin.Triple
- kotlin.collections.Map.Entry

<br>

분해 선언은 반복문에서 맵 자료구조를 사용할 때 유용하며, 람다 표현식에서도 이 기능을 사용할 수 있습니다.

```kotlin
val cities: Map<String, String> = ... // 도시 정보

cities.forEach { citiyCode, name -> System.out.println("$cityCode=$name")}
```

<br>

개발자가 작성한 클래스에서 분해 선언 기능을 사용하고 싶다면 해당 클래스 내에 별도로 `componentN()`함수를 프로퍼티의 선언 순서 및 타입에 알맞게 **operator 키워드**를 붙여주어 추가하면 됩니다.

```kotlin
class Person(val age: Int, val name: String) {
    // 첫 번째 프로퍼티의 값 반환
    operator fun component1() = this.age
    
    // 두 번째 프로퍼티의 값 반환
    operator fun component2() = this.name
}

val person: Person = ... 
val (age, name) = person // 분해 선언 사용 가능
```

<br>

<br>