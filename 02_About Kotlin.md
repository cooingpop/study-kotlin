<br><br>

<h1>코틀린 표준 라이브러리</h1>  

  <br><br><br><br>

<h2>1. 조건 확인 함수</h2> 

<br>

<h3>특정 값의 일치 여부 확인 : check, require</h3>

 `check()`함수와 `require()` 함수 모두 인자로 받은 표현식이 참이 아닌 경우 각각 **IllegalStateException**과 **IllegaArgumentException**을 발생시킵니다. 

```kotlin
fun showMessage(isPrepared: Boolean, message: String) {
    // 인자로 받은 isPrepared의 값이 true가 아니라면 IllegalStateException을 발생
    check(isPrepared)
    
    // 인자로 받은 message 문자열의 길이가 10이상이 아니라면
    // IllegalArgumentException을 발생
    require(message.length > 10)
}
```

<br>

두 함수 모두 추가적으로 조건이 일치하지 않았을 경우 **수행할 작업을 함께 지정**할 수 있는 형태도 지원합니다.

- fun check (value: Boolean, lazyMessage: () -> Any)

  인자로 받은 value 값이 참이 아니라면 **IllegalStateException**을 발생시키며, 이 때 **lazyMessage**로 넘겨진 함수를 함께 실행합니다.

- fun require (value: Boolean, lazyMessage: () -> Any)

  인자로 받은 value 값이 참이 아니라면 **IllegalArgumentException**을 발생시키며, 이 때 **lazyMessage**로 넘겨진 함수를 함께 실행합니다.

<br>

이 외에도, `checkNotNull()`함수와 `requireNotNull()`함수를 사용하면 **특정 값의 널 여부를 확인**하고 **널이 아닌 값을 반환** 받을 수 있습니다.

```kotlin
fun showMessage(isPrepared: Boolean, message: String?) {
    check(isPrepared)
   
    // 인자로 받은 message 값이 널인 경우 IllegalArgumentException 발생
    // 널이 아닌 경우, msg에 값을 할당
    val msg = requireNotNull(message)
    require(message.length > 10)
}
```

<br>

<br>

<h3>명시적으로 실행 중단하기: error, TODO</h3>

정상적으로 프로그램이 실행될 때 **호출될 가능성이 없는 영역에 진입**하게 되는 경우, `error()`함수를 통해 임의로 예외를 발생시켜 프로그램의 실행을 막을 수 있습니다.

```kotlin
fun showMessage(isPrepared: Boolean, message: String) {
    
    // 인자로 받은 값 isPrepared가 거짓일 경우
    // IllegalStateException: Not prepared yet 예외가 발생합니다.
    if(!isPrepared){
        error("Not prepared yet")
    }
    println(message)
}
```

<br>

이 이외에도 **다른 부분의 작업이 완료되어야 구현이 가능한 부분**이 있는 경우, 보통 주석을 사용하여 추가 작업이 필요함을 표시한 경우가 많습니다. 하지만 간혹 이러한 주석들을 미처 확인하지 못하고 그냥 두어 버그가 발생하기도 하는데, 코틀린에서는 이를 방지하기 위해 `TODO()` 함수를 제공합니다.

```kotlin

```

<br>

<br>

<br>

<br>

<h2>2. 컬렉션 생성 함수</h2>

<br>

<h3>배열</h3>

**특정 원소를 담고 있는 배열**을 생성하려면 `arrayOf()`함수를 사용합니다. **빈 배열**을 생성하고 싶은 경우`emptyArrayOf()`함수를 대신 사용할 수 있습니다. **널 값을 포함할 수 있는 배열**을 생성하고 싶은 경우에는 `arrayOfNulls()`함수를 사용하여 널로 초기화 된 배열을 생성한 후에 값을 따로 채워넣을 수 있습니다.

```kotlin
// 인자로 전달된 문자열을 포함하는 배열을 생성
// 배열의 타입은 인자를 통해 추론되므로 생략 가능
val cities = arrayOf("Seoul", "Tokyo", "San Francisco")

// String 타입의 빈 배열을 생성
// 전달되는 인자가 없어 타입 추론이 불가하므로 함수 호출 시 타입 지정
val emptyStringArray = emptyArray<String>()

// 크기가 3이고 넓 값을 포함할 수 있는 배열 생성
// 전달되는 인자가 없어 타입 추론이 불가하므로 함수 호출 시 타입 지정
val nullStoreAbleArray = arrayOfNulls<String>(3)
```

<br>

자바의 원시 타입을 포함하는 배열은 코틀린의 배열과 다른 타입으로 취급되므로, 각 타입에 맞는 함수를 사용해야 합니다.

| Java                                                         | Kotlin                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| boolean[ ]                                                   | fun booleanArrayOf(vararg elements: Boolean): BooleanArray   |
| byte[ ]                                                      | fun byteArrayOf(vararg elements: Byte): ByteArray            |
| char[ ]                                                      | fun charArrayOf(vararg elements: Char): CharArray            |
| double[ ]                                                    | fun doubleArrayOf(vararg elements: Double): DoubleArray      |
| float[ ]                                                     | fun floatArrayOf(vararg elements: Float): FloatArray         |
| int[ ]                                                       | fun intArrayOf(vararg elements: Int): IntArray               |
| long[ ]                                                      | fun longArrayOf(vararg elements: Long): LongArray            |
| short[ ]                                                     | fun shortArrayOf(vararg elements: Short): ShortArray         |
| // 문자열을 포함하는 배열 생성<br />char[] chars = new char[] {'a', 'b', 'c', 'd', 'e'};<br /><br />// 정수를 포함하는 배열 생성<br />int[] numbers = new int[] {1, 2, 3, 4, 5}; | // 자바의 원시 타입 char를 포함하는 배열 생성<br />var chars = charArrayOf('a', 'b', 'c', 'd', 'e')<br /><br />// 자바의 원시 타입 int를 포함하는 배열 생성<br />var numbers = intArrayOf(1, 2, 3, 4, 5) |

<br>

<br>

<h3>리스트</h3>

포함하는 요소를 읽을 수만 있고 수정할 수 없는 **읽기 전용 리스트**는 `listOf()`함수를 사용하여 생성할 수 있습니다. 인자로 받는 값 중, 널 값은 무시하고 **널이 아닌 값으로만 리스트를 구성**하고 싶은 경우 `listOfNotNull()`함수를 사용합니다. 리스트에 포함된 요소를 **수정할 수 있는 리스트**는 `mutableListOf()`함수를 사용하여 생성합니다.

```kotlin
val foods: List<String> = listOf("라면", "갈비", "밥")

// 널 값이 아닌 인자가 아무것도 없으므로, 빈 리스트가 생성
val listOfCountries = listOfNotNull(null)

// 널 값인 인자는 무시하므로, "Seoul", "Tokyo"만을 요소로 갖는 리스트 생성
val listOfCities = listOfNotNull("Seoul", null, "Tokyo", null)

val foods = mutableListOf("라면", "갈비", "밥")
foods.add("초밥")      // [라면, 갈비, 밥, 초밥]
foods.removeAt(0)     //  [갈비, 밥, 초밥]
```

<br>

안드로이드 앱 개발 시 자주사용하는 ArrayList 또한 코틀린에서 `arrayListOf`를 사용하여 쉽게 생성할 수 있습니다.

<br>

<br>

<h3>맵</h3>

포함하는 요소를 읽을 수만 있고, **수정할 수 없는 읽기 전용** 맵은 `mapOf()`함수를 사용합니다. 리스트와 유사하게, 맵이 포함하고 있는 요소를 **수정할 수 있는 맵**은 `mutableMapOf()`함수로 생성할 수 있습니다. 위의 두 함수는 맵에 들어갈 요소를 모두 **Pair 형태**로 받는데, Pair를 만들 때 `to()`를 사용하면 이를 **직관적으로 표현**할 수 있습니다.

```kotlin
// Pair를 직접 사용하는 예
val cities1 = mapOf(Pair("SEO", "Seoul"), Pair("TOK", "Tokyo"))

// to() 함수를 사용하여 Pair를 직관적으로 표현한 예
val cities2 = mapOf("SEO" to "Seoul", "TOK" to "Tokyo")
```

<br>

<br>

<h3>집합</h3>

집합(set)은 중복되지 않는 요소들로 구성된 자료 구조입니다. **읽기 전용** 집합은 `setOf()`함수를 사용하여 생성할 수 있으며, 포함하고 있는 요소를 **수정할 수 있는** 집합은 `mutableSetOf()`함수로 생성할 수 있습니다.

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

<br>

<h2>3. 스트림 함수</h2>

<br>

<h3>변환</h3>

`map()`함수는 컬렉션 내 인자를 다른 값 혹은 타입으로 변환할 때 사용됩니다. 

```kotlin
val cities = listOf("Seoul", "Tokyo", "Washington")

// 도시 이름을 대문자로 변환
cities.map{ city -> city.toUpperCase() }.forEach { println(it) }
// SEOUL
// TOKYO
// WASHINGTON

// 도시 이름을 받아, 각 이름의 문자열 길이로 변환
cities.map{ city -> city.length }.forEach { println(it) }
// 5
// 5
// 13
```

<br>

`maxIndexed()` 함수를 사용하면 컬렉션 내 포함된 인자의 인덱스 값을 변환 함수 내에서 사용할 수 있습니다. `mapNotNull()`은 컬렉션 내 각 인자를 변환함과 동시에, 널 값인 경우 이를 무시합니다.

```kotlin
// 0부터 10까지 정수를 포함하는 범위
val numbers = 0..10

// 변환 함수에서 각 인자와 인덱스를 곱한 값을 반환
numbers.mapIndexed{ idx, number -> idx * number}.forEach{ print("$it ")}
// 0 1 4 9 16 25 36 49 64 81 100

val cities = listOf("Seoul", "Tokyo", "Washington")

// 도시 이름의 길이가 5 이하일 경우에만 반환하고, 그렇지 않은 경우 널 반환
cities.mapNotNull{ city -> if(city.length <= 5) city else null }.forEach{ println(it)}
// Seoul
// Tokyo
```

<br>

`flapMap()`함수는 `map()`함수와 달리 변환 함수의 반환형이 **Iterable**입니다. 따라서 하나의 인자에서 여러 개의 인자로 매핑이 필요한 경우 사용합니다. 그리고 `groupBy()`함수는 **컬렉션 내 인자들을 지정한 기준에 따라 분류**하며, 각 인자들의 리스트를 포함하는 맵 형태로 결과를 반환합니다.

```kotlin
val numbers = 1..6

// 1부터 시작하여 각 인자를 끝으로 하는 범위를 반환
numbers.flatMap{ number -> 1..number }.forEach{ print("$it ")}
// 1 1 2 1 2 3 1 2 3 4 1 2 3 4 5 1 2 3 4 5 6

val cities = listOf("Seoul", "Tokyo", "Washington")

// 도시 이름의 길이가 5 이하일 경우에만 반환하고, 그렇지 않은 경우 널 반환
cities.groupBy { city -> if (city.length <= 5) "A" else "B" }
		.forEach{ key, cities -> println("key=$key cities=$cities") }
// key=A cities=[Seoul, Tokyo]
// key=B cities=[Washington]
```

<br>

<br>

<h3>필터</h3>

`filter()`함수는 컬렉션 내 인자들 중 주어진 조건과 일치하는 인자만 걸러주는 역할을 합니다.

```kotlin

```

<br>

`take()`함수는 **앞에서부터** 인자로 받은 개수만큼만을 인자로 갖는 리스트를 반환합니다. `takeLst()`함수는 take() 함수와 반대로 **뒤에서부터** 이 함수의 인자로 받은 개수만큼만을 인자로 갖는 리스트를 반환하고, `takeWhile()`함수는 첫 번째 인자부터 시작하여 **주어진 조건을 만족하는 인자까지를 포함**하는 리스트를 반환합니다. 

```kotlin
val cities = listOf("Seoul", "Tokyo", "Mountain View", "NYC", "Singapore")

// 첫 번째 인자로부터 하나의 인자만 포함
cities.take(1).forEach { println(it) } // Seoul

// 마지막 인자로부터 두 개의 인자만 포함
cities.takeLast(2).forEach { print("$it ")} // NYC Singapore

// 문자열의 길이가 5 이하인 조건을 만족할 때까지 해당 항목 반환
cities.takeWhile { city -> city.length <= 5 }.forEach{ print("$it ") } // Seoul Tokyo

// 뒤에서부터 시작하여, 문자열의 길이가 13미만인 조건을 만족할 때까지 해당 항목 반환
cities.takeLastWhile { city -> city.length < 13 }.forEach{ print("$it ") } 
// NYC Singapore 
```

<br>

`drop()`함수는 take() 함수와 역할을 하며, **조건을 만족하는 항목을 컬렉션에서 제외한 결과를 반환**합니다. take() 함수와 유사하게 `dropLast()`, `drowWhile()`, `dropLastWhile()`함수를 지원합니다.

```kotlin
val cities = listOf("Seoul", "Tokyo", "Mountain View", "NYC", "Singapore")

// 첫 번째 인자로부터 하나의 인자 제외
cities.drop(1).forEach { print("$it ") } // Tokyo Mountain View NYC Singapore

// 마지막 인자로부터 두 개의 인자 제외
cities.dropLast(2).forEach { print("$it ")} // Seoul Tokyo Mountain View

// 문자열의 길이가 5 이하인 조건을 만족할 때까지 해당 항목 제외
cities.dropWhile { city -> city.length <= 5 }.forEach{ print("$it ") } 
// Mountain View NYC Singapore

// 뒤에서부터 시작하여, 문자열의 길이가 13미만인 조건을 만족할 때까지 해당 항목 제외
cities.dropLastWhile { city -> city.length < 13 }.forEach{ print("$it ") } 
// Seoul Tokyo Mountain View 
```

<br>

`first()`함수는 단순히 리스트 내에서 **첫 번째에 위치하는 인자를 반환**하는 것 뿐만 아니라 특정 조건을 만족하는 첫 번째 인자를 반환하도록 구성할 수 있습니다. 조건을 만족하는 인자가 없는 경우 예외를 발생시키며, `firstOfNull()`함수를 사용하면 예외 대신 널 값을 반환하도록 할 수 있습니다. `last()`함수는 first() 함수와 반대의 역할을 수행합니다.

```kotlin
val cities = listOf("Seoul", "Tokyo", "Mountain View", "NYC", "Singapore")

// 첫 번째 인자 반환
println(cities.first()) // Seoul

// 마지막 인자 반환
println(cities.last()) // Singapore

// 문자열 길이가 5 이상인 첫 번째 인자 반환
println(cities.first { city -> city.length >5 }) // Mountain View

try{
    // 조건을 만족하는 마지막 인자 반환, 없을 경우 예외 발생
    cities.last{ city -> city.isEmpty() }
} catch (e: NoSuchElementException) {
    println("Not found")
}
// Not found

// 조건을 만족하는 첫 번째 인자를 반환, 없을 경우 널 반환
println(cities.firstOrNull{ city -> city.isEmpty() }) // null
```

<br>

`distinct()`함수는 컬렉션 내에 포함된 항목 중 중복된 항목을 걸러낸 결과를 반환합니다. `distinctBy()`함수를 사용하면 비교에 사용할 키 값을 직접 설정할 수 있습니다.

```kotlin
val cities = listOf("Seoul", "Tokyo", "Mountain View", "Seoul", "Tokyo")

// 도시 목록 중 중복된 항목 제거
cities.distinct().forEach{println(it)} // Seoul Tokyo Mountain View

// 도시 이름의 길이를 기준으로 중복된 항목 판단
cities.distinctBy { city -> city.length }.forEach{ println(it) } // Seoul Mountain View
```

<br>

<br>

<h3>조합 및 합계</h3>

`zip()`함수는 **두 컬랙션 내의 자료들을 조합하여 새로운 자료를 만들 때 사용**합니다. 두 컬렉션 간 자료의 개수가 다른 경우, 반환되는 컬렉션의 자료 수는 더 적은 쪽을 따라갑니다.

```kotlin
val cityCodes = listOf("SEO", "TOK", "MTV", "NYC")
val cityNames = listOf("Seoul", "Tokyo", "Mountain View")

// 단순히 zip 함수를 호출하는 경우, Pair 형태로 조합
cityCodes.zip(cityNames).forEach { pair -> println("${pair.first}:${pair.second}")}
//SEO:Seoul
//TOK:Tokyo
//MTV:Mountain View

// 조합할 자료의 타입을 지정하면 해당 형태로 변환
cityCodes.zip(cityNames){ code, name -> "$code ($name)"}.forEach { println(it) }
//SEO (Seoul)
//TOK (Tokyo)
//MTV (Mountain View)
```

<br>

`joinToString()`함수는 컬렉션 내 자료를 **문자열 형태로 변환함과 동시에, 하나의 문자열로 생성**합니다. 컬렉션 내 자료를 직렬화할 때 유용하게 사용할 수 있습니다.

```kotlin
val cities = listOf("Seoul", "Tokyo", "Mountain View", "NYC", "Singapore")

// 기본 설정값을 사용하여 문자열 형태로 조합
println(cities.joinToString()) // Seoul, Tokyo, Mountain View, NYC, Singapore

// 구분자로 다른 문자를 사용하도록 설정
println(cities.joinToString(separator = "|")) 
// Seoul|Tokyo|Mountain View|NYC|Singapore
```

<br>

`count()`함수는 **컬렉션 내 포함된 자료의 개수를 반환**할뿐만 아니라 별도의 조건식을 추가할 수 있습니다.

```kotlin
val cities = listOf("Seoul", "Tokyo", "Mountain View", "NYC", "Singapore")

// 컬렉션 내 포함된 모든 자료의 개수 반환
println(cities.count())  // 5

// 컬렉션 내 길이가 5 이하인 자료의 개수 반환
println(cities.count { city -> city.length <= 5}) // 3
```

<br>

`reduce()` 함수는 컬렉션 내 자료들을 첫 번째 자료부터 **모두 합쳐 하나의 값으로 만들어주는 역할**을 수행합니다. `reduceRight()`함수는 동일한 작업을 마지막 자료부터 시작합니다.

```kotlin
val cities = listOf("Seoul", "Tokyo", "Mountain View", "NYC", "Singapore")

// acc에는 지금까지 조합된 결과가, s에는 새로 조합할 자료가 들어갑니다.
println(cities.reduce{acc, s -> "$acc, $s"}) 
// Seoul, Tokyo, Mountain View, NYC, Singapore

// reduceRight 함수는 마지막 인자부터 조합합니다.
println(cities.reduceRight{s, acc -> "$acc, $s"})
// Singapore, NYC, Mountain View, Tokyo, Seoul
```

<br>

`fold()`함수는 reduce() 함수와 거의 동일하나, **초깃값을 지정**할 수 있습니다. reduce() 함수와 마찬가지로 `foldRight()`함수를 제공합니다.

```kotlin

```

<br>

<br>

<h3>기타</h3>

`any()`함수는 컬렉션 내 **자료가 하나라도 존재하는 지에 따라 true, false를 반환**합니다. `none()`함수는 any() 함수의 반대 작업을 하며, 두 함수 모두 인자로 조건식을 전달할 수 있습니다.

```kotlin
val cities = listOf("Seoul", "Tokyo", "Mountain View", "NYC", "Singapore")

// 리스트 내 자료가 존재하는지 확인
println(cities.any())  // true

// 빈 문자열을 가진 자료가 존재하지 않는지 확인
println(cities.none { city -> city.isEmpty() })  // true
```

<br>`max()`, `min()`, `average()` 함수는 숫자 타입의 자료를 갖는 컬렉션에서 각각 **최대값**, **최소값**, **평균**을 반환합니다.

```kotlin
val numbers = listOf(4, 2, 5, 3, 2, 0, 8)

println(numbers.max())     // 8
println(numbers.min())     // 0
println(numbers.average()) // 3.4285714285714284
```

<br>

<br>

<br>

<br>

<h2>4. 범위 지정 함수</h2>

<br>

<h3>let() 함수</h3>

`let()`함수는 이 함수를 호출한 **객체를 이어지는 함수 블록의 인자로 전달**하고 블록 함수의 결과를 반한합니다. let() 함수를 사용하면 불필요한 변수 선언을 방지할 수 있습니다.

```kotlin
// 단말기 환경에 맞게 패딩 값을 계산
val padding = TypedValue.applyDimension(TypedValue.COMPLEX_UNIT_DIP, 16f, resource.displaymetrics).toInt()

// 패딩 값 설정
setPadding(padding, 0, padding, 0)
```

<br>

위의 코드의 경우 `let()`함수를 사용하면 아래와 같이 padding 변수 선언 없이 계산된 값을 함수의 인자로 전달할 수 있습니다.

```kotlin
TypedValue.applyDimension(TypedValue.COMPLEX_UNIT_DIP, 16f, resource.displaymetrics).toInt().let {
	// 계산된 값을 인자로 받으므로, 함수에 바로 대입
	setPadding(it, 0, it, 0)   
}
```

<br>

<br>

<h3>apply() 함수</h3>

`apply()`함수는 **이 함수를 호출한 객체**를, 이어지는 **함수 블록의 리시버로 전달**하며, 함수를 호출한 객체를 반환합니다.

```kotlin
val params = LinearLayout.LayoutParams(0, LinearLayout.LayoutParams.WRAP_CONTENT)
params.gravity = Gravity.CENTER_HORIZONTAL
params.weight = 1f
params.topMargin = 100
params.bottomMargin = 100
```

<br>

위의 코드는 속성을 변경하기 위해 객체 이름을 계속해서 호출하고 있지만, `apply()`함수를 사용하면 다음과 같이 **객체 이름 없이 직접 해당 객체 내부의 속성에 접근**할 수 있습니다.

```kotlin
val params = LinearLayout.LayoutParams(0, LinearLayout.LayoutParams.WRAP_CONTENT).apply {
    gravity = Gravity.CENTER_HORIZONTAL
    weight = 1f
    topMargin = 100
    bottomMargin = 100  
}
```

<br>

<br>

<h3>with() 함수</h3>

`with()`함수는 **인자로 받은 객체**를 이어지는 **함수 블록의 리시버**로 전달합니다. 이 함수에서 사용할 객체를 **매개변수**를 통해 전달받으므로 널 값이 아닌 것으로 확인된 객체에 이 함수를 사용하는것이 권장됩니다.

```kotlin
fun manipulateView(messageView: TextView) {
    
    // 인자로 받은 messageView의 여러 속성을 변경
    with(messageView) {
        text = "Hello, World"
        gravity = Gravity.CENTER_HORIZONTAL
    }
}
```

<br>

<br>

<h3>run() 함수</h3>

`run()`함수는 **1) 인자가 없는 익명 함수처럼 사용하는 형태**와 **2) 객체에서 호출하는 형태**를 제공합니다. 

1. 익명 함수처럼 사용하는 경우 **블록의 결과를 반환**하며, 복잡한 계산을 위해 여러 임시 변수가 필요할 때 유용하게 사용할 수 있습니다.

   ```kotlin
   val padding = run {
       // 이 블록의 내부에서 선언하는 값들은 외부에 노출되지 않습니다.
       val defaultPadding = TypedValue.applyDimension(...)
       val extraPadding = TypedValue.applyDimension(...)
       
       // 계산된 값 반환
       defaultPadding + extraPadding
   }
   ```

   <br>

2. 객체에서 호출하는 경우 **with() 함수와 유사한 목적**(객체를 리시버 객체로 전달하고 결과를 반환)으로 사용할 수 있고 `run()`함수는 안전한 호출을 사용할 수 있으므로 **널 값일 수 있는 객체의 속성이나 함수에 연속적으로 접근**할 때 유용합니다.

   ```kotlin
   override fun onCreate(savedInstanceState: Bundle?) {
       super.onCreate(savedInstanceSate)
       
       // 액티비티 생성 시, 기존에 저장된 값이 있는 경우 UI 복원 수행
       savedInstaceState?.run {
           // Bundle 내 저장된 값 추출
           val selection = getInt("last_selection")
           val text = getString("last_text")
           
           // UI 복원 수행
           ...
       }
   }
   ```

<br>

<br>