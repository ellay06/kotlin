# 함수

### 기본
fun <T> joinToString(
    collection: Collection<T>,
    separator: String,
    prefix: String,
    postfix: String
): String {
    val result = StringBuilder(prefix)
    for ((index, element) in collection.withIndex()) {
        if (index > 0) result.append(separator)
        result.append(element)
    }
    
    result.append(postfix)
    return result.toString()
}





## 함수
jotinToString(collections, “; “, “(”, “)”)

그래서, 가독성을 위해 호출인자를 넣을 수 있음 (이런 경우, 파라미터 순서 변경 가능)
(단, 자바 함수 호출시에는 쓸 수 없다)
jotinToString(collections, separator = “; “, prefix = “(”, postfix = “)”)

또한 디폴트 값을 넣을 수 있다.
fun <T> joinToString(
    collection: Collection<T>,
    separator: String = “, “,
    prefix: String = “”,
    postfix: String = “”
): String

이때는 호출시 생략 가능
joinToString(list)

*자바에는 디폴트 값이 없으므로 @JvmOverloads를 사용하면 자동으로 오버로딩한 자바 함수를 생성해준다.


## 최상위 함수
클래스에 포함 되지 않는 자바의 유틸성 함수를 선언할때 사용 (java로는 static function)
물론, 최상위에 프로퍼티도 선언 가능


## 확장함수
String에 마지막 문자를 구하는 함수를 추가한다면
fun String.lastChar(): Char = this.get(this.length - 1)
String 은 수신객체타입 이라 하며 this 는 수신 객체라고 함.
*this 생략 가능

사용 : 일반 함수처럼 사용
“코뚫린“.lastChar()
*확장함수는 자바로 변환하면 정적 메소드가 하나 생성된 것뿐이다. 

open class C
class D: C()

fun C.foo() = "c"
fun D.foo() = "d"
fun printFoo(c: C) {
    println(c.foo())
}

printFoo(D())

특징
1. 확장함수는 오버라이딩 불가능
2. 이름이 같은 경우 우선순위
  클래스 함수 > 확장 함수

*널이 가능한 함수를 널이 없도록
fun Any?.toString(): String {
    if (this == null) return "null"
    // after the null check, 'this' is autocast to a non-null type, so the toString() below
    // resolves to the member function of the Any class
    return toString()
}



## 함수 임포트
1. import strings.lastChar            // “코뚫린“.lastChar()
2. import strings.*                // “코뚫린“.lastChar()
3. import string.lastChar as last  // “코뚫린“.last()

3번의 경우, 똑같은 함수명을 가진 클래스들을 사용할때 유용하다.


### 최종
fun <T> Collection<T>.joinToString(
    collection: Collection<T>,
    separator: String = ", ",
    prefix: String = "",
    postfix: String = ""
): String {
    val result = StringBuilder(prefix)
    for ((index, element) in this.withIndex()) {
        if (index > 0) result.append(separator)
        result.append(element)
    }
    
    result.append(postfix)
    return result.toString()
}


## 로컬 함수
함수 내에 함수를 선언
*로컬 함수는 바깥 함수의 변수를 사용할 수 있다.
class User(val id: Int, val name: String, val address: String)

fun User.validateBeforeSave() {
    fun validate(value: String, fieldName: String) {
        if (value.isEmpty()) {
            throw IllegalArgumentException("error $id: empty $fieldName")
        }
    }
    
    validate(name, "Name")
    validate(address, "Address")
}
    

*콜랙션에 제공하는 함수처럼 사용 가능


## 확장 프로퍼티
val StringBulider.lastChar: Char
    get() = get(length - 1)
    set(value: Char) {
        this.setCharAt(length - 1, value)
    }
    
// 사용: StringBuilder("ok").lastChar = '!'
*자바에서 사용한다면 get, set을 프로퍼티 앞에 붙여 함수 호출해야한다.


## 콜렉션
### vararg
가변인자를 가지는 경우에 사용한다. 단, 마지막 파라미터만 가능하고, 한개만 사용 가능하다.
선언 : fun listOf<T>(vararg values: T): List<T> {...}
사용 : listOf("args: ", *args) // *문자를 붙여서 배열 요소임을 표시해줘야 한다.
    
### 중위 함수
infix fun Any.to(other:Any) = Pair(this, other)
일반 함수를 중위 함수로 만들기 위해서는 infix를 함수 선언 앞에 꼭 붙여야한다.

### 정규식
정규식 문법 외에 정말 문자도 넣을수 있다...
