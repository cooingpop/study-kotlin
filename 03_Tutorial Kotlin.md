<br><br>  

<h1>Android Kotlin 정리</h1>  

  <br><br><br><br>  
  
<h2>1. Android Studio 설정</h2> 

책에서는 Android Studio 설치 방법부터 자세하게 설명하지만 이는 타 블로그에서도 쉽게 찾을 수 있으므로 생략하고 Android Studio 설치 후 설정하면 유용한 **인코딩 설정**과 **패키지 자동 삭제**만 소개합니다.
<br/>
- **인코딩 설정**
  <br><br>
  Windows는 EUC-KR 계열 인코딩을 기본으로 사용하기 때문에 한글로 작성된 문장들이 깨져 보일 수 있습니다. 이를 위해 UTF-8로 변환합니다.
  <br><br>
  ​	
    1. Settings(Ctrl+Alt+S) → Editor → File Encodings
  <br><br>
  ![](https://i.imgur.com/bNDObwC.png)
  <br><br>

    2. Global Encoding, Project Encoding을 모두 UTF-8로 설정합니다.

<br><br>
- **패키지 자동 삭제**

  <br>기본 설정으로 패키지가 자동 import가 되지만 API 제거 시 import문을 자동으로 정리해주면 코드가 더 깔끔하게 유지 될 수 있습니다.

  <br>

   1. Settings(Ctrl+Alt+S) → Editor → General → Auto Import
      <br><br>
      ![](https://i.imgur.com/lRFUVhE.png)
      <br><br>

   2. **Add unambiguous import on the fly**와 **Optimize imports on the fly**를 모두 체크하여 반영합니다.
      <br><br><br><br><br>

<h2>2. 기기와 에뮬레이터 준비</h2>  

1장과 동일하게 Android 기기, 에뮬레이터를 실행하는 기본적인 내용은 생략하고 **Android Kotlin 프로젝트 생성 시 필요한 설정**과 에뮬레이터 실행 시 유용한 **한국어 설정**만 소개하도록 하겠습니다.
<br><br>
- **Android Kotlin 프로젝트 생성**
  <br><br>![](https://i.imgur.com/02AHV5Y.png)
  <br><br>
  프로젝트 생성 방법은 Java로 프로젝트를 생성하는 것과 대부분 동일하나 **Include Kotlin support**를 체크해주어야 합니다.
  <br><br><br>
- **에뮬레이터 한국어 설정**<br><br>에뮬레이터가 제공하는 기본 언어는 영어이므로 한국어로 설정하려면 다음의 순서를 따릅니다.![](https://i.imgur.com/bcw66UW.png)
  <br><br>
  Setting 앱 실행 → 제일 하단의 System → Language &input → Add a language → 한국어 → 대한민국 클릭 후 우측의 이동 아이콘을 드래그하여 **가장 위로 오도록** 이동합니다.
  <br><br><br><br><br>
<h2>3. Kotlin</h2>

<h3> REPL & Scratch</h3>

- Android Studio에서 제공하는 코드를 한 줄씩 실행하는 셸인 **REPL**을 사용하면 새로운 언어를 배울 때 직관적으로 실행시킬 수 있기 때문에 유용합니다.
  <br><br>![](https://i.imgur.com/n2jz1FX.png)<br>Tools → Kotlin → Kotlin REPL을 클릭하면 창이 표시되고 코드작성 후 **Ctrl + Enter**를 누르면 하단에 결과가 표시됩니다.<br>
  <br><br><br>
- REPL은 한 줄 단위 코드로 코드를 실행할 때는 편리하지만 복잡한 코드 테스트 때는 불편합니다. 이런 경우에는 **Scratch**를 사용합니다.
  <br><br>![](https://i.imgur.com/4AwhWCb.png)![](https://i.imgur.com/fnVYmzW.png)<br><br>
  File → New → Scratch File을 클릭하면 언어를 선택하는 창이 표시되고 **Kotlin**을 선택합니다. 에디터 창에 **scratch.kts** 파일이 열리면 여기서 자유롭게 Kotlin 코딩을 연습할 수 있습니다.
  <br><br><br><br>

<h3> Kotlin 문법</h3>

<h4>1. 기본 구문</h4>  

- **변수와 상수**
  <br><br>Kotlin에서 변수는 **var**로 상수는 **val**로 선언합니다. val은 자바의 **final** 키워드와 동일합니다.<br>

  ```kotlin
  var a:Int = 10 //var 변수명: 자료형 = 값
  val b:Int = 10 //var 상수명: 자료형 = 값  
  ```
  Kotlin은 자료형을 지정하지 않아도 추론하기 때문에 **생략할 수 있습니다.**<br>

  ```kotlin
  var a = 10 // 변수 var a:Int  
  val b = 10 // 상수 var b:Int (재할당 불가)
  ```
  <br><br>


- **함수**
  <br><br>
  함수를 선언하는 방법은 다음과 같습니다.
  <br>`fun 함수명(인수1: 자료형, 인수2: 자료형 … ): 반환자료형`<br><br>
  Kotlin에서 반환값이 없을 때 **Unit**형을 사용하며 이는 **Java의 void**에 대응합니다. 반환 값이 Unit인 경우에는 생략할 수 있습니다.<br>

  ```kotlin
  fun printKotlin(): Unit {
     println("hello kotlin!")
  }
  
  fun printKotlin() {     // 반환자료형 Unit 생략
     println("hello kotlin!")
  }
  ```
  <br><br><br>

<h4>2. 기본 자료형</h4>  

- **숫자형**<br><br>
  코틀린의 기본 자료형은 모두 객체입니다. Java가 프리미티브 자료형(int, double 등)과 객체 자료형으로 분류되는 것과는 다릅니다.<br><br>
  코틀린에서 숫자를 표현하는 자료형은 다음과 같으며 코틀린 컴파일러는 자료형을 추론합니다.



  - **Double** : 64비트 부동소수점  
  - **Float** : 32비트 부동 소수점  
  - **Long** : 64비트 정수  
  - **Int** : 32비트 정수  
  - **Short** : 16비트 정수

<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![](https://i.imgur.com/LKScuDe.png)<br><br><br>

- **문자형**
  <br><br>
  Kotlin에서 문자를 나타내는 자료형은 다음과 같이 두가지 이며 Char가 숫자형이 아니라는 점이 Java와 다릅니다.<br>

  	String : 문자열
  	Char : 하나의 문자
  <br>여러 줄에 걸쳐 문자열을 표현할 때는 큰따옴표 3개를 리터럴로 사용합니다.<br>

  ```kotlin
  val str = """오늘은
  	  날씨가 좋습니다.
  	  빨래를 합시다.
  	  """
  ```
  <br>문자열 비교는 ==을 사용하며 Java의 equls() 메서드와 대응합니다. **Java에서 == 를 오브젝트 비교** 시에 사용하는데 **Kotlin에서는 오브젝트 비교 시에는** `===` 을 사용합니다.<br>

  ```kotlin
  var str = "hello"
  if (str == "hello") {
  	 println("안녕하세요")
  } else {
    	 println("안녕 못 해요")
  }
  ```
  <br>

  문자열 템플릿 기능을 사용하면 `+` 기호로 문자열을 연결할 수 있고 `$ `기호를 사용해서 문자열 리터럴 내부에 변수를 쉽게 포함할 수 있습니다.<br>

  ```kotlin
  val str = "반갑"
  println(str + "습니다")          // Java와 동일
  
  // Kotlin
  println("$str 하세요")           안녕 하세요
  println("${str}하세요")          안녕하세요
  ```

  <br>

  <br>

- **배열**

   

  배열은 **Array**라는 별도의 타입으로 표현하며 `arrayOf( )` 메서드를 사용하여 생성과 초기화를 함께 수행합니다. 자료형을 유추할 수 있을 때는 이를 생략할 수 있으며 배열 요소에 접근하는 것은 `[ ]`를 이용합니다.

  ```kotlin
  val numbers:Array<Int> = arrayOf(1,2,3,4,5)
  val numbers2 = arrayOf(1,2,3,4,5)  // 자료형 생략
  numbers[0] = 5    // [5,2,3,4,5]
  ```

  <br><br>

  <br>

<h4>3. 제어문</h4>
  제어문은 크게 **if, when, for, while**이 있으며 if와 while의 경우 Java와 거의 동일하므로 여기서는 when과 for에 대해서만 다루도록 하겠습니다.

 

- **when**

  `when`은 Java의 **switch**에 해당합니다. 콤마와 in 연산자를 이용해 값의 범위를 자유롭게 지정할 수 있습니다.

  ```kotlin
  val x = 1
  
  when(x) {
      1 -> println("x==1")						// 값 하나인 경우
      2,3 -> println("x==2 or x==3")				// 여러 값은 콤마로 지정
      in 4..7 -> println("4부터 7사이")			 // in 연산자로 범위 지정
      !in 8..10 -> println("8부터 10사이가 아님")
      else -> {									// 나머지
          println("x는 1이나 2가 아님")
      }
  }
  ```

  <br>

  <br>

- **for**

  for문은 Java의 foreacn문과 비슷하며 `..` 연산자, `in` 키워드, `downTo` 키워드, `step` 키워드로 배열이나 컬렉션을 순회할 수 있습니다. 

  ```kotlin
  var numbers = arrayOf(1,2,3,4,5)
  
  for(num in numbers){
      println(num)   // 1; 2; 3; 4; 5
  }
  
  // 1~3까지 출력
  for(i in 1..3){
      println(i)     // 1; 2; 3; 
  }
  
  // 0~10까지 2씩 증가하며 출력
  for(i in 0..10 step 2){
      println(i)     // 2; 4; 6; 8; 10;
  }
  
  // 10부터 0까지 2씩 감소하며 출력
  for(i in 10 downTo 0 step 2){
      println(i)     // 10; 8; 6; 4; 2;
  }
  ```

  <br>

  <br>
  <br>

<h4>4. 클래스</h4>

- **클래스 선언**

  Java에서는 new 키워드로 객체를 생성하지만 Kotlin은 new 키워드를 사용하지 않습니다. 또한  Java는 변수를 선언만 해도 null이나 0으로 초기화해주었지만 Kotlin에서는  **반드시 초기화를 직접 해주어야 합니다.**

  ```kotlin
  // 클래스 선언
  class Shape {
  	var x:Int = 0
  	var y:Int = 0
  	var width:Int = 0
  	var height:Int = 0
  }
  
  // 인스턴스 생성
  val shape = Shape()
  ```

  <br>

  <br>

- **생성자**

  생성자는 `constructor` 키워드를 사용하여 표현하고 클래스명 옆에 선언한 생성자를 **기본생성자**라고 합니다. 기본생성자의 경우 constructor 키워드를 붙이지 않고도 표현할 수 있습니다.

  ```kotlin
  class Shape constructor(x:Int, y:Int) {
  	var x:Int = x
  	var y:Int = y
  	var width:Int = 0
  	var height:Int = 0
  }
  
  // 위의 코드와 동일
  class Shape(x:Int, y:Int) {
  	var x:Int = x
  	var y:Int = y
  	var width:Int = 0
  	var height:Int = 0
  }
  ```

  <br>

  기본 생성자 이외에도 다른 생성자들을 만들기 위해서는 constructor 키워드를 사용하여 체인형식으로 메서드처럼 선언합니다.

  ```kotlin
  class Shape(x:Int, y:Int) {
  	var x:Int = x
  	var y:Int = y
  	var width:Int = 0
  	var height:Int = 0
  	
  	// 체인형식 - 내가 만든 기본생성자를 호출
  	constructor(x: Int, y: Int, width: int, height: Int) : this(x,y) {
          this.width = width
          this.height = height
  	}
  }
  ```

  <br>

  Kotlin에서는 생성자 이외에도 init 블록에 작성한 코드가 클래스를 인스턴스화할 때 가장 먼저 초기화됩니다.

  ```kotlin
  class Shape(x: Int, y: Int) {
      var x: Int = x
      var y: Int = y
      var width: Int = 0
      var height: Int = 0
  
      init {
          println("생성자 호출")
      }
  
      constructor(x: Int, y: Int, width: Int, height: Int) : this(x, y) {
          this.width = width
          this.height = height
      }
  }
  ```

  <br>

  <br>

- **프로퍼티**

  클래스의 속성을 사용할 때는 멤버에 직접 접근하며 이를 **프로퍼티**라고 합니다. Java와 다르게 private 접근지정자로 은닉화된 멤버 변수에도 게터/세터 메서드 없이 프로퍼티로 대체할 수 있습니다.

  ```kotlin
  // 클래스 선언
  class Person(var name:String) {
      
  }
  
  // 인스턴스 생성
  val person = Person("멋쟁이")
  person.name = "키다리"   // 쓰기
  println(person.name)    // 읽기
  ```

  <br>

  <br>

- **접근 제한자**

  변수나 함수를 공개하는데 사용하는 키워드입니다. Kotlin에서 사용되는 접근 제한자는 Java와 거의 동일하며 다음과 같습니다.

   

  - **public** (생략 가능) : 전체 공개이며 아무것도 쓰지 않으면 기본적으로 public입니다.

  - **private** : 현재 파일 내부에서만 사용할 수 있습니다.

  - **internal** : 같은 모듈 내에서만 사용할 수 있습니다.

  - **protected** : 상속받은 클래스에서 사용할 수 있습니다.


  ```kotlin
class A {
    val a = 1	// public
    private val b =2
    protected val c = 3
    internal val d = 4
}
  ```

  <br>

  <br>

- **클래스의 상속**

  Kotlin에서의 클래스는 기본적으로 상속이 금지되므로 상속이 가능하게 하려면 `open` 키워드를 클래스 선언 앞에 추가합니다.

  ```kotlin
  open class Animal {
      
  }
  
  class Dog : Animal() {
      
  }
  ```

  만약 상속받을 클래스가 생성자를 가지고 있다면 다음과 같이 상속받을 수 있습니다.

  ```kotlin
  open class Animal(val name: String) {
      
  }
  
  class Dog(name: String) : Animal(name) {
      
  }
  ```

  <br>

  <br>

- **내부 클래스**

  내부 클래스 선언에는 `inner` 키워드를 사용합니다. 내부 클래스는 외부 클래스에 대한 참조를 가지고 있으므로 아래 코드에서 inner 키워드가 없다면 a를 변경할 수 없습니다.

  ```kotlin
  class OutClass {
      var a = 10
      
      // 내부 클래스
      inner class OuterClass2 {
          fun something() {
              a = 20  // inner 키워드로 인해 접근 가능
          }
      }
  }
  ```

  <br>

  <br>

- **추상 클래스**

  추상 클래스는 미구현 메서드가 포함된 클래스를 말합니다. Java와 거의 동일하며 클래스와 미구현 메서드 앞에 `abstract` 키워드를 붙입니다. 추상 클래스는 직접 인스턴스화할 수 없고 다른 클래스가 상속하여 미구현 메서드를 구현해야합니다.

  ```kotlin
  abstract class A {
      abstract fun func()
      
      fun func2() {
          
      }
  }
  
  class B: A() {
      override fun func() {
          println("hello")
      }
  }
  
  var a = A()  // 에러
  var b = B()  // hello
  ```

  <br>

  <br>

  <br>

<h4>5. 인터페이스</h4>

**인터페이스**는 미구현 메서드를 포함하여 클래스에서 이를 구현합니다. 추상클래스와 비슷하지만 클래스가 단일 상속만 되는 반면 인터페이스는 **다중 구현**이 가능합니다. OnClickListener처럼 주로 클래스에 동일한 속성을 부여해 같은 메서드라도 다른 행동을 할 수 있게 하는데 사용합니다. 사용법은 Java와 거의 동일합니다.

<br>

- **인터페이스의 선언**

  인터페이스에 추상 메서드를 포함할 수 있으며 abstract 키워드를 생략할 수 있습니다.

  ```kotlin
  interface Runnable {
      fun run()
  }
  ```

  인터페이스는 구현이 없는 메서드뿐만 아니라 구현된 메서드도 포함할 수 있습니다.

  ```kotlin
  interface Runnable{
      fun run()
      
      fun fastRun() = println("빨리 달린다")
  }
  ```

  <br>

  <br>

- **인터페이스의 구현**

  인터페이스를 구현할 때는 인터페이스 이름을 콜론(:) 뒤에 나열합니다. 그리고 미구현 메서드를 작성하는데 이때 `override` 키워드 메서드 앞에 추가합니다.

  ```kotlin
  class Human : Runnable {
      override fun run() {
          println("달린다")
      }
  }
  ```

  <br><br>

- **상속과 인터페이스를 함께 구현**

  상속과 인터페이스를 함께 구현할 수 있습니다. 상속은 하나의 클래스만 상속하는 반면 인터페이스는 콤마로 구분하여 여러 인터페이스를 동시에 구현할 수 있습니다.

  ```kotlin
  open class Animal {
      
  }
  
  interface Runnable {
      fun run()
      
      fun fastRun() = println("빨리 달린다")
  }
  
  interface Eatable {
      fun eat()
  }
  
  class Dog : Animal(), Runnable, Eatable {
      override fun eat() {
          println("먹는다")
      }
      
      override fun run() {
          println("달린다")
      }
  }
  
  val dog = Dog()
  dog.run()
  dog.eat()
  ```

  <br>

  <br>

  <br>

<h4>6. null 가능성</h4>

Kotlin은 기본적으로 객체를 불변으로 보고 null값을 허용하지 않습니다. null값을 허용하려면 별도의 연산자가 필요하고 허용을 했더라도 별도의 연산자들을 사용하여 안전하게 호출해야 합니다.

<br>

- **null 허용?**

  Kotlin은 기본적으로 null값을 허용하지 않기 때문에 모든 객체는 생성과 동시에 값을 대입하여 **초기화해야** 합니다. Kotlin에서 null값을 허용하려면 자료형의 오른쪽에 **? 기호**를 붙여주면 됩니다.

  ```kotlin
  val a: String         // 에러 : 반드시 초기화 해야 함
  val a: String = null  // 에러 : Kotlin은 기본적으로 null 허용하지 않음
  val a: String? = null // OK
  ```

  <br>

  <br>

- **lateinit 키워드로 늦은 초기화**

  Android를 개발할 때 초기화를 나중에 해야할 경우가 있는데, 이 때 `lateinit` **키워드**를 변수 선언 앞에 추가하면 됩니다. lateinit을 사용 시 초기화를 잊지 않도록 주의해야 합니다.

  ```kotlin
  lateinit var a: String    // OK
  
  a = "hello"
  println(a)   //hello
  ```

  - var 변수에서만 사용합니다.
  - null값으로 초기화할 수 없습니다.
  - 초기화 전에는 변수를 사용할 수 없습니다.
  - Int, Long, Double, Float에서는 사용할 수 없습니다.

  <br>

  <br>

- **lazy로 늦은 초기화**

  lateinit이 var로 선언한 변수의 늦은 초기화라면 lazy는 값을 **변경할 수 없는 val**을 사용할 수 있습니다. val 선언 뒤에 by lazy 블록에 초기화에 필요한 코드를 작성합니다. 마지막 줄에는 초기화할 값을 작성합니다. **str이 처음 호출될 때** 초기화 블록의 코드가 실행됩니다.

  ```kotlin
  val str: String by lazy {
      println("초기화")
      "hello"
  }
  
  println(str)    // 초기화; hello
  println(str)    // hello
  ```

  - val에서만 사용합니다.

  <br>

  <br>

- **null값이 아님을 보증(!!)**

  변수 뒤에 `!!`를 추가하면 **null값이 아님을 보증**하게 됩니다. 다음과 같이 null값이 허용되는 name 변수의 경우 String? 타입이기 때문에 String 타입으로 변환하려면 !!를 붙여서 null값이 아님을 보증해야 합니다.

  ```kotlin
  val name: String? = "피노키오"
  
  val name2: String = name    // 에러
  val name3: String? = name   // OK
  val name4: String = name!!  // OK
  ```

  <br><br>

- **안전한 호출**

  메서드 호출 시 점(.) 연산자 대신 `?. `연산자를 사용하면 **null값이 아닌 경우**에만 호출됩니다.

  ```kotlin
  val str: String? = null
  
  var upperCase = if (str!=null) str else null  // null
  upperCase = str?.toUpperCase  // null
  ```

  <br>

  <br>

- **엘비스 연산자(?:)**

  안전한 호출 시 null이 아닌 기본값을 반환하고 싶을 때는 **엘비스 연산자**를 함께 사용합니다. 

  ```kotlin
  val str: String?=null
  
  var upperCase = if(str!=null) str else null    // null
  upperCase = str?.toUpperCase ?: "초기화하시오"   // 초기화하시오
  ```

  <br>

  <br>

  <br>

<h4>7. 컬렉션</h4>

컬렉션은 개발에 유용한 자료구조를 말하며 안드로이드 개발에서는 리스트나 맵이 자주 사용됩니다.

<br>

- **리스트**

  요소를 변경할 수 없는 읽기 전용 리스트는 `lisfOf( )` 메서드로 작성할 수 있습니다.

  ```kotlin
  val foods: List<String> = listOf("라면", "갈비", "밥")
  ```

  요소를 변경하는 리스트를 작성할 때는 `mutableListOf( )` 메서드를 사용합니다. Java와 다르게 특정 요소에 접근할 때 [ ] 로 접근할 수 있습니다.

  ```kotlin
  val foods = mutableListOf("라면", "갈비", "밥")
  
  foods.add("초밥")      // [라면, 갈비, 밥, 초밥]
  foods.removeAt(0)     //  [갈비, 밥, 초밥]
  foods[1] = "부대찌개"   // [갈비, 부대찌개, 초밥]
  ```

  <br>

  <br>

- **맵**

  맵은 키(key)와 값(value)의 쌍으로 이루어진 키가 중복될 수 없는 자료구조입니다. 리스트와 마찬가지로 `mapOf( )` 메서드로 읽기 전용 맵을 만들 수 있고, `mutableMapOf( )` 메서드로 수정 가능한 맵을 만들 수 있습니다.

  ```kotlin
  // 읽기 전용 맵
  val map = mapOf("a" to 1, "b" to 2, "c" to 3)
  
  // 변경 가능한 맵
  val citiesMap = mutableMapOf("한국" to "서울", "일본" to "동경", "중국" to "북경")
  
  // 요소에 덮어쓰기
  citiesMap["한국"] = "서울특별시"
  // 추가
  citiesMap["미국"] = "워싱턴"
  
  // 맵의 키와 값 탐색
  for((key,value) in map) {
      println("$key -> $value")
  }
  ```

  <br>

  <br>

- **집합**

  집합은 중복되지 않는 요소들로 구성된 자료구조입니다. `setOf( )` 메서드로 읽기 전용 집합을, `mutableSetOf( )` 메서드로 수정 가능한 집합을 생성합니다.

  ```kotlin
  // 읽기 전용 집합
  val citySet = setOf("서울", "수원", "부산")
  
  // 수정 가능한 집합
  val citySet2 = mutableSetOf("서울", "수원", "부산")
  citySet2.add("안양")        // [서울, 수원, 부산, 안양]
  citySet2.remove("수원")     // [서울, 부산, 안양]
  ```

  <br>

  <br>

  <br>

<h4>8. 람다식</h4>

람다식은 하나의 함수를 표현하는 방법으로 익명 클래스나 익명 함수를 간결하게 표현할 수 있어 매우 유용합니다. 아래와 같이 반환 자료형을 생략하고 블록과 return을 생략할 수 있습니다.

```kotlin
fun add(x: Int, y: Int): Int {
    return x + y
}

//위의 코드와 동일
fun add(x: Int, y: Int) = x + y
var add = {x: Int, y:Int -> x + y}  // {인수1: 타입1, 인수2: 타입2 -> 본문}
```

<br>

<br>

<br>

<h4>기타 기능</h4>

- **확장 함수**

  Kotlin은 확장 함수 기능을 사용하여 쉽게 기존 클래스에 함수를 추가할 수 있습니다. 확장 함수를 **추가할 클래스에 점을 찍고** 함수 이름을 작성합니다.

  ```kotlin
  fun Int.isEven() = this % 2 == 0
  
  val a = 5
  val b = 6
  
  println(a.isEven())   // false
  println(b.isEven())   // true
  ```

  <br>

  <br>

- **형변환**

  숫자형 자료끼리는 `to자료형( )` 메서드를 사용하여 형변환이 가능합니다.

  ```kotlin
  val a = 10L
  val b = 20
  
  val c = a.toInt()    // Long → Int 
  val d = b.toDouble() // Int → Double
  val e = a.toString() // Long → String
  ```

  숫자 형태의 문자열을 숫자로 바꿀 때는 Java와 동일하게 `Integer.parseInt( )` 메서드를 사용합니다.

  ```kotlin
  val intStr = "10"
  val str = Integer.parseInt(intStr)
  ```

  일반 클래스 간에 형변환을 하려면 `as` 키워드를 사용합니다.

  ```kotlin
  open class Animal
  
  class Dog : Animal()
  
  val dog = Dog()
  
  val animal = dog as Animal  // Dog → Animal형으로 변환
  ```

  <br>

  <br>

- **형 체크**

  `is` 키워드 사용하여 형을 체크할 수 있으며 이는 Java의 instanceOf에 해당합니다.

  ```kotlin
  val str = "hello"
  
  if(str is String) {
      println("This is String")
  }
  ```

  <br>

  <br>

- **고차 함수**

  Kotlin에서는 함수의 인수로 함수를 전달하거나 함수를 반환할 수 있습니다.

  ```kotlin
  // 인수 : 숫자, 숫자, 하나의 숫자를 인수로 하는 반환값이 없는 함수
  // callback에 x와 y의 합을 전달하면 callback은 하나의 숫자를 받고 반환이 없는 함수
  fun add(x: Int, y: Int, callback: (sum: Int) -> Unit){
      callback(x + y)
  }
  
  // 함수는 { }로 감싸고 내부에서는 반환값을 it으로 접근 가능
  add(5,3 { println(it)})   // 8
  ```

  <br>

  <br>

- **동반 객체**

  Kotlin에는 Java의 static 이 없습니다. Kotlin에서는 Java 의 static 함수와 같이 인스턴스 생성 없이 해당 클래스의 함수나 프로퍼티를 참조하기 위해서 사용하는 키워드가 `companion` 키워드입니다. `companion` 은 `object`와 함께 쓰입니다.

  ```kotlin
  class Fragment {
      companion object {
          fun newInstance() : Fragment {
              println("생성")
          }
      }
  }
  
  val fragment = Fragment.newInstance()
  ```

  <br>

  <br>

- **let ( ) 함수**

  `let ( )` 함수는 블록에 자기 자신을 인수로 전달하고 수행된 결과를 반환합니다. 인수로 전달한 객체는 it으로 참조합니다.

  ```kotlin
  // fun <T,R> T.let(block: (T) -> R): R
  var result = str?.let{
      Integer.parseInt(it)
  }
  ```

  <br>

  <br>

- **with ( ) 함수**

  `with ( )` 함수는 인수로 객체를 받고 블록에 리시버 객체로 전달합니다. 그리고 수행된 결과를 반환하며 리시버 객체로 전달된 객체는 this로 접근이 가능합니다.

  ```kotlin
  // fun <T,R> with(receiver: T, block T.() -> R): R
  with(str){
      println(toUpperCase())
  }
  ```

  <br>

  <br>

- **apply ( ) 함수**

  `apply ( )` 함수는 블록에 객체 자신이 리시버 객체로 전달되고 이 객체가 반환됩니다.

  ```kotlin
  // fun <T> T.apply(block: T.() -> Unit): T
  val result = car?.apply {
      car.setColor(Color.RED)
      car.setPrice(1000)
  }
  ```

  <br>

  <br>

- **run( ) 함수**

  1. 익명 함수 처럼 사용하는 경우 블록의 결과를 반환합니다.

     ```kotlin
     // fun <R> run(block: () -> R): R
     val avg = run {
         val korean = 100
         val english = 100
         val math = 50
         
         (korean + english + math) / 3.0
     }
     ```

  2. 객체에서 호출하는 경우 객체를 블록의 리시버 객체로 전달하고 블록의 결과를 반환합니다.

     ```kotlin
     // fun <T,R> T.run(block: T.() -> R): R
     str?.run{
         println(toUpperCase())
     }
     ```

     <br>

     <br>

     <br>

     <br>

     <br>

<h2>4. Kotlin 예제 - 비만도 계산기</h2>

 책에서는 레이아웃을 Design을 통해 구현하였지만 저는 Text를 통해 구현하였습니다. 앞으로의 모든 예제에서는 **UI 및 기능 명세만 정의**하고 공부를 위해 직접 구현해보시길 바랍니다. 구현에 필요한 **문법에 관해서는 아래에 정리**하였으며 어려움이 생길 경우에는 [BmiCalculator 소스코드](https://github.com/cj1ne/android-kotlin-tutorial/tree/master/%EC%98%A4%EC%A4%80%EC%84%9D%EC%9D%98%20%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C%20%EC%83%9D%EC%A1%B4%EC%BD%94%EB%94%A9%20%EC%BD%94%ED%8B%80%EB%A6%B0%ED%8E%B8%20%EC%A0%95%EB%A6%AC/04_Kotlin%EC%98%88%EC%A0%9C-%EB%B9%84%EB%A7%8C%EB%8F%84%EA%B3%84%EC%82%B0%EA%B8%B0)를 참고하시길 바랍니다.

<br>

<h3>UI 및 기능 명세</h3>

​    ![](https://i.imgur.com/1Si3Es7.png)           ![](https://i.imgur.com/RrZWa0e.png)

<br>

<h4>UI 명세</h4>

1. **메인화면**

   - 키 입력 (EditText)

     - **상단, 좌우 여백**  : 16

     - **ID** : heightEditText

     - **hint** : 키

       <br>

   - 몸무게 입력 (EditText)

     - **상단, 좌우 여백**  : 16
     - **ID** : weightEditText
     - **hint** : 몸무게 

     <br>

   - 결과 버튼 (Button)

     - **상단, 우측 여백**  : 16
     - **ID** : resultButton
     - **text** : 결과

     <br><br>

2. **결과화면**

   - 결과 문장 (TextView)

     - **상단 여백** : 130
     - **좌우 여백** : 16
     - **ID** : resultTextView

     <br>

   - 결과 이미지 (ImageView)

     - **가로** : 100
     - **세로** : 100
     - **ID** : imageView
     - **이미지 경로** : BMI에 따라 표정이 다른 이미지 경로로 설정

<br>

<br>

<h4>기능 명세</h4>

- 키와 몸무게를 입력하고 결과 버튼을 누르면 다른 홤녀에서 비만도 결과를 문자와 그림으로 보여줍니다.

- 마지막에 입력했던 키와 몸무게는 자동으로 저장됩니다. (SharedPreference)

- BMI 계산식은 다음과 같습니다.

  ```kotlin
  val bmi = weight / Math.pow(height / 100.0, 2.0)
  ```

<br>

<br>

<br>

<h3>Anko common 라이브러리 사용 준비</h3>

1. 프로젝트 창에서 **build.gradle (Module: app)** 파일을 엽니다.

2. dependencies 항목에 Anko 라이브러리를 추가합니다.

   ```kotlin
   dependencies{
       implementation "org.jetbrains.anko:anko:$anko_version"
   }
   ```

3. 프로젝트 창에서 **build.gradle (Project: ~)** 파일을 엽니다.

4. buildscript 블록에 Anko 라이브러리 버전을 변수에 지정합니다.

   ```kotlin
   ext.anko_version = '0.10.5'
   ```

   <br>![](https://i.imgur.com/kWT6fin.png)

5. `Sync Now`를 클릭하여 싱크합니다.

<br>

<br>

<br>

<h3>버튼 클릭 이벤트 리스너</h3>

xml 파일에서 버튼의 id가  `android:id="@+id/resultButton"`와 같이 설정되어 있다면 버튼 클릭 이벤트 리스너는 다음과 같이 설정할 수 있습니다. Java에 비해 코드가 간결해진 것을 확인할 수 있습니다.

```kotlin
resultButton.setOnClickListener{
    // 버튼이 클릭되면 할 일을 작성하는 부분
}
```

<br>

<br>

<br>

<h3>액티비티 전환</h3>

액티비티를 전환은 다음과 같이 수행할 수 있습니다. 현재 액티비티는 MainActivity이고  ResultActivity로 이동하는 것을 가정하겠습니다.

```kotlin
// Intent(현재 액티비티, 전환할 액티비티)

var intent = Intent(this, ResultActivity::class.java)
startActivity(intent)
```

<br>

하지만 자주 사용하는 코드 치고는 타이핑양이 적지 않습니다. 이 부분을 Anko 라이브러리를 사용하면 다음과 같이 간단하게 작성할 수 있습니다.

```kotlin
startActivity<ResultActivity>()
```

<br>

<br>

<br>

<h3>이전 화면으로 돌아가는 업 네비게이션</h3>

다른 화면으로 이동 후, 뒤로 가기를 눌러 이전 화면으로 이동할 수 있습니다. 하지만 화면상으로는 이전 액티비티와의 상관관계를 알 수 있는 어떠한 표시도 없는데 이럴 경우 **업 네비게이션**을 설정하여 상단 툴바에 뒤로가기 아이콘을 표시할 수 있습니다.

<br>

1. 프로젝트 창에서 **AndroidManifest.xml** 파일을 엽니다.

2. 두 번째 액티비티에 **parentActivityName** 속성을 추가합니다.

   ```kotlin
   // 부모 액티비티 지정
   <activity 
       android:name=".ResultActivity"	// 현재 액티비티
       android:parentActivityName=".MainActivity">  // 이전 액티비티(부모)
   </activity>
   ```

<br>

<br>

<br>

<h3>인텐트에 데이터 담기</h3>

인텐트는 데이터를 담아서 다른 액티비티에 전달하는 역할도 수행하며 코드는 다음과 같습니다.

```kotlin
var intent = Intent(this, ResultActivity::class.java)

// intent.putExtra(키, 값)
intent.putExtra("weight", weightEditText.text.toString())
intent.putExtra("height", heightEditText.text.toString())
startActivity(intent)
```

Anko를 적용하면 좀 더 간단히 작성할 수 있습니다.

```kotlin
startActivity<ResultActivity>(
      "weight" to weightEditText.text.toString(),
      "height" to heightEditText.text.toString()
)
```

<br>

<br>

<br>

<h3>인텐트에서 데이터 꺼내기</h3>

인텐트에서 데이터를 꺼내려면 `get~~Extra()` 메서드를 사용합니다. 전달받은 데이터가 문자열인 경우 `getStringExtra( )` 메서드를 사용합니다.

```kotlin
// intent.get~~Extra("키")
val height = intent.getStringExtra("height").toInt()
val weight = intent.getStringExtra("weight").toInt()
```

<br>

<br>

<br>

<h3>토스트</h3>

Java에서 사용하던 토스트 코드도 Kotlin에서 다음과 같이 사용이 가능합니다.

```kotlin
Toast.makeText(this, "$bmi", Toast.LENGTH_SHORT).show()
```

그러나 Anko를 적용하면 다음과 같이 줄일 수 있습니다.

```
toast("$bmi")
```

<br>

<br>

<br>

<h3>SharedPreference로 데이터 저장 및 불러오기</h3>

<br>

<h4>데이터 저장하기</h4>

```kotlin
private fun saveData(height: Int, weight: Int)
{
    val pref = PreferenceManager.getDefaultSharedPreferences(this) // (1)
    va  editor = pref.edit()               // (2)
        
    editor.putInt("KEY_HEIGHT", height)    // (3)
            .putInt("KEY_WEIGHT", weight)
            .apply()                       // (4)
}
```

1. PreferenceManager를 사용해 Preference 객체를 얻습니다.
2. Preference 객체의 Editor 객체를 얻습니다. 이 객체를 사용해 데이터를 담을 수 있습니다.
3. Editor 객체에 `putㅁㅁ` 메서드를 사용하여 키와 값 형태의 쌍으로 데이터를 저장합니다.
4. 설정된 내용을 반영합니다.

<br>

<br>

<h4>데이터 불러오기</h4>

```kotlin
private fun loadData()
{
    val pref = PreferenceManager.getDefaultSharedPreferences(this)  // (1)
    val height =pref.getInt("KEY_HEIGHT", 0)        // (2)
    val weight =pref.getInt("KEY_WEIGHT", 0)

    if(height != 0 && weight != 0) {                
        heightEditText.setText(height.toString())   
        weightEditText.setText(weight.toString())
    }
}
```

1. Preference 객체를 얻습니다.
2. `getㅁㅁ` 메서드를 사용하여 저장된 값을 불러옵니다. 두 번째 인자는 저장된 값이 없을 때 반환할 값을 의미합니다.

<br>

<br>

<br>

<br>

<br>

<h2>5. Kotlin 예제 - 스톱워치</h2>

 책에서는 레이아웃을 Design을 통해 구현하였지만 여기에서는 Text를 통해 구현하였습니다. 예제에서는 **UI 및 기능 명세만 정의**하고 공부를 위해 직접 구현해보시길 바랍니다.  **구현에 필요한 내용은 아래에 정리**하였으며 어려움이 생길 경우에는 [StopWatch 소스코드](https://github.com/cj1ne/android-kotlin-tutorial/tree/master/%EC%98%A4%EC%A4%80%EC%84%9D%EC%9D%98%20%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C%20%EC%83%9D%EC%A1%B4%EC%BD%94%EB%94%A9%20%EC%BD%94%ED%8B%80%EB%A6%B0%ED%8E%B8%20%EC%A0%95%EB%A6%AC/05_Kotlin%EC%98%88%EC%A0%9C-%EC%8A%A4%ED%86%B1%EC%9B%8C%EC%B9%98)를 참고하시길 바랍니다.

<br>

<h3>UI 및 기능 명세</h3>

![](https://i.imgur.com/yLFqW2B.png)![](https://i.imgur.com/fKrudXa.png)

<br>

<h4>UI 명세</h4>

**메인화면**

1. 초 second 표시 (TextView)

   - **ID** : secTextView
   - **textAppearance** : AppCompat.Large
   - **textSize** : 100sp 

   <br>

2. 밀리 초 milli second 표시 (TextView)

   - **ID** : milliTextView
   - **textAppearance** : AppCompat.Large
   - **textSize** : 22sp

   <br>

3. 랩 타임 표시 (ScrollView)

   - **ID** : labLayout (ScrollView 내부의 LinearLayout의 ID)

   <br>

4. 초기화버튼 (FloatingActionButton)

   - **ID** : resetFab
   - **src** : ic_refresh_black_24dp
   - **backgroundTint** : colorAccent
   - **tint** : color/white
   - **왼쪽, 아래 여백** : 16

   <br>

5. 시작, 일시정지 버튼 (FloatingActionButton)

   - **ID** : playFab

   - **src** : ic_play_arrow_black_24dp(default), ic_pause_24dp

     *타이머 시작 시 일시정지 이미지로 바뀌고, 일시 정지 시 시작 이미지로 전환*

   - **backgroundTint** : colorPrimary

   - **아래 여백** : 16 

   - **tint** : color/white

   <br>

6. 랩 타임 기록 버튼 (Button)

   - **ID** : labButton
   - **textSize** : 랩 타임
   - **오른쪽, 아래 여백** : 16

   <br>

<br>

<br>

<h4>기능 명세</h4>

- 타이머를 시작, 일시정지하고 초기화할 수 있습니다.
- 타이머의 시간은 0.01초 단위로 변경되어 나타납니다.
- 타이머 실행 중에 랩 타임을 측정하여 표시할 수 있으며 최근의 랩 타임이 ScrollView 맨 위에 나타납니다.
- 타이머 초기화 시 랩 타임 정보가 사라지며 타이머 시간도 0으로 초기화됩니다.

<br>

<br>

<br>

<h3>Floating Action Button 생성</h3>



![](https://i.imgur.com/8I6gkJa.png)

<br>

이번 예제에서 초기화, 시작, 일시정지 버튼은 FAB를 사용하기 때문에 이를 사용하기 위해 Palette 창에서 Button 카테고리의 FloatingActionButton을 찾습니다. FAB는 기본 제공되는 컴포넌트가 아니기 때문에 다운로드를 받아야합니다. 빨간 네모 박스안에 있는 아이콘을 클릭하면 잠시 후 자동으로 deisgn 라이브러리를 추가하고 싱크합니다.

<br>

<br>

<h3>벡터 드로어블 하위 호환 설정</h3>

**FloatingActionButton** 버튼의 배경에 벡터 이미지를 사용합니다. 안드로이드 5.0 미만의 기기에서도 벡터 이미지가 잘 표시되도록 모듈 수준의 gradle 파일에 다음 코드를 추가합니다.

```kotlin
defaultConfig{
    vectorDrawables.useSupportLibrary = true
}
```

<br>

<br>

<h3>벡터 이미지 준비</h3>

이 예제에서 사용할 시작, 일시정지, 초기화 버튼에 총 3가지 이미지가 필요합니다. 먼저 다음의 순서를 통해 Asset Studio를 실행합니다.

```
프로젝트 창 res 폴더에서 마우스 우클릭 → New → Vector Asset
```

![](https://i.imgur.com/DeAQVdi.png)

<br>

Asset Studio에서 **Clip Art**를 클릭한 후에 `pause`, `play arrow`, `refresh`를 각각 검색한 후에 Next, Finish 버튼을 순서대로 클릭하여 벡터 이미지를 추가합니다. 추가한 이미지는 FloatingActionButton의 **src** 속성을 이용하여 버튼 이미지로 사용할 수 있습니다.

<br>

<br>

<h3>랩 타임을 표시하는 ScrollView</h3>

![](https://i.imgur.com/H4rHSJD.png) ![](https://i.imgur.com/baeJ1nB.png)

<br>

이 예제에서 랩 타임 버튼을 누를 때마다 타임 랩이 누적되어 **ScrollView**에 나타납니다. ScrollView는 자식을 하나만 가지는 특수한 뷰이며, 우리가 실제로 타임 랩을 추가할 곳은 ScrollView가 아니라 ScrollView 내부의 **LinearLayout**입니다. 따라서 위처럼 ScrollView 내부에 LinearLayout을 배치하고 여기에 ID를 작성합니다. 

<br>

<br>

<h3>타이머 구현</h3>

<h4>타이머 시작</h4>

```kotlin
private var time = 0  // 시간을 계산하는 변수
private var timeTask: Timer? = null // null을 허용하는 Timer

private fun start() {
    playFab.setImageResource(R.drawable.ic_pause_black_24dp)

    timerTask = timer(period=10){ // 0.01초마다 수행 (ms 단위)
        time++
        var sec = time / 100
        var milli = time % 100

        runOnUiThread({
            secTextView.text="$sec"
            milliTextView.text="$milli"
        })
    }
}
```

타이머가 시작되면 시작 버튼의 이미지를 일시정지 이미지로 변경하고 0.01초마다 시간을 1(0.01s) 증가시킵니다. 나중에 timer를 취소하기 위해 Timer 객체를 변수에 저장해둘 필요가 있습니다. 또한 timer는 워커 스레드에서 동작하여 UI 조작이 불가능하므로  변경된 시간을 **runOnUiThread**로 감싸서 UI조작이 가능하도록 합니다.

<br>

<h4>타이머 일시정지</h4>

```kotlin
private fun pause(){
        playFab.setImageResource(R.drawable.ic_play_arrow_black_24dp)

        timerTask?.cancel()
    }
```

타이머 시작과 반대로 버튼이 눌리면 버튼의 이미지를 시작버튼의 이미지로 변경하고, 실행 중인 타이머가 있다면 타이머를 취소합니다.

<br>

<h4>타이머 초기화</h4>

```kotlin
private fun reset(){~~
    timerTask?.cancel()

    // 모든 변수 초기화
    time = 0
    isRunning = false
    playFab.setImageResource(R.drawable.ic_play_arrow_black_24dp)
    secTextView.text="0"
    milliTextView.text="00"

    // 모든 랩타임 제거
    labLayout.removeAllViews()
    lap = 1
}
```

실행 중인 타이머가 있다면 취소하고 모든 변수와 화면에 표시되는 모든 것을 초기화합니다.

<br>

<br>

<h3>동적으로 LinearLayout에 뷰 추가</h3>

ScrollView 내부에 있는 LinearLayout에 타임 랩을 추가 하기 위해 다음과 같이 코드를 작성합니다. 이 때 새롭게 생성된 타임 랩이 항상 ScrollView의 제일 위에 올 수 있도록 `addView( )`메서드의 **두 번째 인자**에 0을 추가합니다.

```kotlin
val textView = TextView(this)
textView.text = "LAB : ${lapTime/100}.${lapTime%100}"
lapLayout.addView(textView, 0)
```

<br>

<br>

<br>

<br>

<br>

<h2>6. Kotlin 예제 - 웹 브라우저</h2>

 책에서는 레이아웃을 Design을 통해 구현하였지만 여기에서는 Text를 통해 구현하였습니다. 예제에서는 **UI 및 기능 명세만 정의**하고 공부를 위해 직접 구현해보시길 바랍니다.  **구현에 필요한 내용은 아래에 정리**하였으며 어려움이 생길 경우에는 [WebBrowser 소스코드](https://github.com/cj1ne/android-kotlin-tutorial/tree/master/%EC%98%A4%EC%A4%80%EC%84%9D%EC%9D%98%20%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C%20%EC%83%9D%EC%A1%B4%EC%BD%94%EB%94%A9%20%EC%BD%94%ED%8B%80%EB%A6%B0%ED%8E%B8%20%EC%A0%95%EB%A6%AC/06_Kotlin%EC%98%88%EC%A0%9C-%EC%9B%B9%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80)를 참고하시길 바랍니다.

<br>

<h3>UI 및 기능 명세</h3>

![](https://i.imgur.com/Olg4Jk8.png)![](https://i.imgur.com/fQdJ663.png)

<br>

<h4>UI 명세</h4>

**메인화면**

1. URL 입력  (EditText)

   - **ID** : urlEditText
   - **textAppearance** : AppCompat.Large
   - **상단, 좌우 여백** : 8dp
   - **hint** : http://
   - **imeOption** : actionSearch (키보드 내 검색 아이콘 사용 설정)
   - **inputType** : textUri 

   <br>

2. 웹뷰 (WebView)

   - **ID** : webView

   <br>

<br>

<br>

<h4>기능 명세</h4>

<br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![](https://i.imgur.com/FAR16qO.png)&nbsp;![](https://i.imgur.com/wOZ1Rfp.png)&nbsp;![](https://i.imgur.com/64PAWlv.png)

<br>

1. URL 입력창(EditText)의 주소로 검색 아이콘을 클릭 시 웹 페이지를 탐색합니다.

2. 홈 메뉴를 클릭하면 첫 페이지로 돌아옵니다.

3. 스마트폰의 뒤로 가기 버튼 클릭 시 최초 페이지까지 **페이지를 역행**합니다.

   <br>

   ![](https://i.imgur.com/0ZJGG8J.png)&nbsp;![](https://i.imgur.com/llzKJA4.png)&nbsp;![](https://i.imgur.com/XshZuXk.png)

   <br>

4. 옵션의 검색 사이트 아이템을 클릭하는 경우 **해당 사이트로 연결**합니다.

5. 옵션의 개발자 정보 아이템을 클릭하는 경우 개발자에게 **전화, 문자, 이메일**을 보낼 수 있습니다.

6. 웹뷰를 지속해서 누른 경우 **컨텍스트 메뉴**가 나타나며 현재 페이지를 공유하거나 기본 브라우저에서 열 수 있습니다.<br>

<br>

<br>

<h3>인터넷 권한 설정</h3>

안드로이드에서는 특정 권한이 필요한 동작을 할 때는 **권한을 추가해야**하며, 웹 뷰에 웹 페이지를 표시하려면 인터넷이 필요하므로 인터넷 사용 권한을 추가합니다. 프로젝트에서 **AndroidManifest.xml**파일을 열고 다음과 같이 권한을 추가합니다.

```kotlin
<manifest...>
	...
	  <uses-permission android:name="android.permission.INTERNET"/>
	...
</manifest>
```

<br>

<br>

<h3>웹뷰 기본 설정</h3>

```kotlin
webView.apply {
    settings.javaScriptEnabled = true
    webViewClient = WebViewClient()
}

webView.loadUrl("https://www.google.com")
```

웹뷰를 사용할 때 항상 기본으로 **javaScriptEnabled 기능 활성**과 **WebViewClient 클래스를 지정**을 해야 합니다. 그렇지 않으면 자바스크립트 기능이 작동하지 않거나 웹뷰에 페이지가 표시되지 않고 자체 웹 브라우저가 동작할 수 있습니다. `loadUrl()` 를 사용하여 Url을 전달하면 웹뷰에 페이지가 로딩됩니다.

<br>

<br>

<h3>키보드의 검색 버튼 동작 정의</h3>

```kotlin
urlEditText.setOnEditorActionListener { _, actionId, _ -> // (1)
    if (actionId == EditorInfo.IME_ACTION_SEARCH) {       // (2)
        webView.loadUrl(urlEditText.text.toString())      // (3)
        true
    } else {
        false
    }
}
```

1. EditText의 **setOnEditorActionListener**는 EditText가 선택되고 글자가 입력될 때마다 호출됩니다. 인자로는 반응한 뷰, 액션 ID, 이벤트 세 가지며, 사용하지 않는 인자는 _로 대치할 수 있습니다.
2. actionId값은 상수로 정의된 값 중에 검색 버튼에 해당하는 상수와 비교하여 검색 버튼이 눌렸는지 확인합니다.
3. 검색 창에 입력한 주소를 웹뷰에 로딩하고 true를 반환하여 이벤트를 종료합니다.

<br><br>

<h3>뒤로가기 동작 재정의</h3>

```kotlin
override fun onBackPressed() {
    if(webView.canGoBack()){
        webView.goBack()
    } else {
        super.onBackPressed()
    }
}
```

액티비티에서 뒤로가기 키를 눌렀을 때 이벤트를 감지하고 재정의하려면 `onBackPressed()` 메서드를 **오버라이드**합니다. 위의 코드는 웹뷰가 이전 페이지로 갈 수 있다면 이전 페이지로 이동하고, 그렇지 않은 경우 원래 뒤로가기 키의 동작을 수행합니다.

<br><br>

<h3>옵션 메뉴 사용하기</h3>

<h4>1. 메뉴 리소스 파일 작성</h4>

menu 디렉터리를 우클릭 한 상태에서 `New → Android Resource Directory`를 클릭합니다.

![](https://i.imgur.com/P5jy4Uj.png)

Resource type을 **menu**로 선택하고 **OK**를 클릭합니다. 프로젝트 창을 보면 res 폴더 아래에 menu 디렉터리가 생성된 것을 확인할 수 있습니다.

<br>

![](https://i.imgur.com/DhuhD7B.png)

그 다음으로는 menu 디렉터리에서 마우스 우클릭 후 `New → Menu resource file`을 선택합니다. Source set과 File name에 **main**을 입력하고 **OK**를 클릭합니다. 그 다음 이전 예제에서다 다뤘던 [Asset Studio](https://github.com/cj1ne/android-kotlin-tutorial/blob/master/%EC%98%A4%EC%A4%80%EC%84%9D%EC%9D%98%20%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C%20%EC%83%9D%EC%A1%B4%EC%BD%94%EB%94%A9%20%EC%BD%94%ED%8B%80%EB%A6%B0%ED%8E%B8%20%EC%A0%95%EB%A6%AC/05_Kotlin%EC%98%88%EC%A0%9C-%EC%8A%A4%ED%86%B1%EC%9B%8C%EC%B9%98.md#%EB%B2%A1%ED%84%B0-%EC%9D%B4%EB%AF%B8%EC%A7%80-%EC%A4%80%EB%B9%84)에서 **home**을 검색하여 벡터 이미지를 추가합니다. 

<br>

<h4>2. 메뉴 작성</h4>

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto">

<item android:title="검색 사이트">
    <menu>
        <item
            android:id="@+id/action_naver"
            android:title="네이버" />
        <item
            android:id="@+id/action_google"
            android:title="구글" />
        <item
            android:id="@+id/action_daum"
            android:title="다음" />
    </menu>
</item>
<item android:title="개발자 정보" >
    <menu >
        <item
            android:id="@+id/action_call"
            android:title="전화하기" />
        <item
            android:id="@+id/action_send_text"
            android:title="문자 보내기" />
        <item
            android:id="@+id/action_email"
            android:title="이메일 보내기" />
    </menu>
</item>
<item
    android:id="@+id/action_home"
    android:icon="@drawable/ic_home_black_24dp"
    android:title="Home"
    app:showAsAction="ifRoom" />
</menu>
```

앞서 생성한 **main.xml** 파일에 메뉴를 구성하기 위해서 위와 같이 코드를 작성합니다. 기능 명세 4), 5) 항목의 사진과 같이 **검색사이트**와 **개발자정보** **메뉴에** 각각 [네이버, 구글, 다음]과 [전화하기, 문자 보내기, 이메일 보내기]  아이템이 추가되도록 한 것 입니다.  마지막 아이템은 기능 명세 2) 를 만들기 위한 것이며 **ifRoom** 속성은 공간에 여유가 있을 때 아이콘을 노출시키는 것을 의미합니다.

<br>

<h4>3. 옵션 메뉴 액티비티에 표시하기</h4>

액티비티에서 다음과 같이 `onCreateOptionsMenu( )` 메서드를 오버라이드하여 메뉴 리소스 파일을 지정하면 메뉴가 표시됩니다.

```kotlin
override fun onCreateOptionsMenu(menu: Menu?): Boolean {
    menuInflater.inflate(R.menu.main, menu)
    return true
}
```

<br>

<h4>4. 옵션 메뉴 클릭 이벤트 처리</h4>

옵션 메뉴를 선택했을 때의 이벤트를 처리하려면 다음과 같이 `onOptionsItemSelected( ) 메서드`를 오버라이드하여 메뉴 아이템의 ID로 구분해 처리합니다.

```kotlin
override fun onOptionsItemSelected(item: MenuItem?): Boolean {
    when(item?.itemId) {
        R.id.action_google, R.id.action_home -> {
            webView.loadUrl("https://www.google.com")
            return true
        }
        R.id.action_naver -> {
            webView.loadUrl("https://m.naver.com")
            return true
        }
        R.id.action_daum -> {
            webView.loadUrl("https://m.daum.net")
            return true
        }
        R.id.action_call -> {
            // 전화 걸기
            return true
        }
        R.id.action_send_text -> {
            // 문자 전송
            return true
        }
        R.id.action_email -> {
            // 이메일 전송
            return true
        }
    }
    return super.onOptionsItemSelected(item)
}
```

<br>

<br>

<h3>컨텍스트 메뉴 사용하기</h3>

<h4>1. 컨텍스트 메뉴 리소스 파일 생성 및 작성</h4>

특정 뷰를 길게 클릭하면 메뉴가 표시되는 **컨텍스트 메뉴**의 리소스 파일 생성 및 작성 과정은 앞서 살펴 본 옵션 메뉴와 거의 동일합니다.

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/action_share"
        android:title="페이지 공유">
    </item>
    <item
    android:id="@+id/action_browser"
    android:title="기존 브라우저에서 열기">
    </item>
</menu>
```

menu 디렉터리에서 마우스 우클릭 후 `New → Menu resource file`을 선택합니다. File name에 **context**을 입력하고 **OK**를 클릭합니다. XML 파일이 생성되면 기능 명세 6) 과 같이 메뉴를 구성하기 위해 위의 코드를 입력합니다.

<br>

<h4>2. 컨텍스트 메뉴 등록하기</h4>

액티비티에서 다음과 같이 `onCreateContextMenu( )` 메서드를 오버라이드하여 메뉴 리소스 파일을 지정하면 메뉴가 표시됩니다. 옵션 메뉴의 `onCreaeteOptionsMenu( )` 메서드와 메서드 이름에 약간의 차이가 있습니다.

```kotlin
override fun onCreateContextMenu(menu: ContextMenu?, v: View?, menuInfo: ContextMenu.ContextMenuInfo?) {
    super.onCreateContextMenu(menu, v, menuInfo)
    menuInflater.inflate(R.menu.context, menu)
}
```

그 다음 **컨테스트 메뉴가 표시될 대상 뷰를 지정**해야합니다. 이 예제에서 액티비티가 main 액티비티밖에 존재하지 않으므로 MainActivity.kt 파일의 onCreate() 메서드에 다음과 같은 코드를 추가합니다.

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)
    
    ...
    ...
    // 컨텍스트 메뉴 등록
    registerForContextMenu(webView)
}
```

<br>

<h4>3. 컨텍스트 메뉴 클릭 이벤트 처리</h4>

옵션 메뉴의 클릭 이벤트 처리와 동일하게 `onCotextItemSelected( )`메서드를 오버라이드하여 메뉴 아이템의 ID로 구분해 처리합니다.

```kotlin
override fun onContextItemSelected(item: MenuItem?): Boolean {
    when(item?.itemId)
    {
        R.id.action_share -> {
            // 페이지 공유
            share(webView.url)
            return true
        }
        R.id.action_browser -> {
            // 기존 웹 브라우저에서 열기
            browse(webView.url)
            return true
        }
    }
    return super.onContextItemSelected(item)
}
```

<br>

<br>

<h3>암시적 인텐트</h3>

안드로이드에는 미리 정의된 인텐트들이 있고 이를 **암시적 인텐트**라고 합니다. 다음은 웹 브라우저에서 해당 url의 페이지를 여는 코드이며, 암시적 인텐트는 대부분 이러한 형태를 하고 있습니다.

```kotlin
var intent = Intent(Intent.ACTION_VIEW)
intent.data = Uri.parse("https://www.google.co.kr")
if (intent.resolveActivity(packageManager) != null) {
    startActivity(intent)
}
```

<br>

그러나, Anko 라이브러리를 사용하면 복잡한 암시적 인텐트 사용 코드를 **획기적으로 줄일 수 있으며** Anko에서 지원하는 암시적 인텐트 기능은 다음과 같습니다.

| 종류                 | 코드                                        |
| -------------------- | ------------------------------------------- |
| 전화 걸기            | makeCall(전화 번호) - 별도의 권한 추가 필요 |
| 문자 보내기          | sendSMS(전화번호, 보낼 문자)                |
| 웹 브라우저에서 열기 | browse(url)                                 |
| 문자열 공유          | share(문자열, [제목])                       |
| 이메일 보내기        | email(받는 메일 주소, 제목, 내용)           |

<br>
