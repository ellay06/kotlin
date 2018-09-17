# 함수
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
:disappointed: String

이때는 호출시 생략 가능
joinToString(list)

*자바에는 디폴트 값이 없으므로 @JvmOverloads를 사용하면 자동으로 오버로딩한 자바 함수를 생성해준다.


최상위 함수
클래스에 포함 되지 않는 자바의 유틸성 함수를 선언할때 사용 (java로는 static function)
물론, 최상위에 프로퍼티도 선언 가능


확장함수
String에 마지막 문자를 구하는 함수를 추가한다면
fun String.lastChar(): Char = this.get(this.length - 1)
String 은 수신객체타입 이라 하며 this 는 수신 객체라고 함.
*this 생략 가능

사용 : 일반 함수처럼 사용
“코뚫린“.lastChar()


함수 임포트
1. import strings.lastChar            // “코뚫린“.lastChar()
2. import strings.*                // “코뚫린“.lastChar()
3. import string.lastChar as last  // “코뚫린“.last()

3번의 경우, 똑같은 함수명을 가진 클래스들을 사용할때 유용하다.

확장함수는 자바로 변환하면 정적 메소드가 하나 생성된 것뿐이다.

