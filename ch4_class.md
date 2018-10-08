#Class

##인터페이스
1. 정의
interface Clickable {
  fun click()
}
//인터페이스에는 추상 메소드와 구현된 메소드를 포함할 수 있다.

2. 클래스에 구현
{클래스}:{인터페이스}, {인터페이스} , ..., {인터페이스}
//자바에서는 인터페이스는 implement, 클래스는 extends를 사용하지만 코틀린에서는 :를 사용한다(클래스, 인터페이스 순서는 중요하지 않다.)

3. 인터페이스에 포함된 구현 메소드 
interface Clickable {
  fun click()                       // 추상 메소드
  fun showOff() = println("click")  // 구현된 메소드 : 이 메소드를 사용할 수 있고, override를 통한 재정의도 가능하다.
}

4. 상속한 인터페이스의 메소드 구현 호출
interface Focusable {
  fun setFocus(b: Boolean) = println("focus: ${if (b) "got" else "lost"}.")
  fun showOff() = println("fucusable")
}

class Button: Clickable, Focusable {
  override fun click() = println("clicked") //재정의
  override fun showOff() {
    super<Clickable>.showOff()
    super<Focusable>.showOff()
  }
}
// "<{인터페이스}>" 꺽쇠 안에 호출할 인터페이스 타입을 쓴다.


