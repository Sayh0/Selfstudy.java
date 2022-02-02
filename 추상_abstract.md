# 추상

abstract. 한국어로는 추상. abstract라는 것은 상속을 강제하는 일종의 규제 라고 이해할 것. 
클래스나 메소드를 사용하기 위해선 반드시 상속해서 사용하도록 강제하는 것이 abstract.   

## 추상 메소드
추상 메소드랑 **메소드의 시그니처만이 정의되어 있고 나머진 비어있는 메소드**를 의미.   
* *시그니처(서명) : 메소드의 이름 / 메소드 매개변수의 숫자, 데이터타입, 순서 / 메소드의 리턴 타입*


우선 코드를 보자
```java
abstract class A {
	public abstract int b();
	public void d() {
		System.out.println("world");
	}
}
public class AbstractDemo {

	public static void main(String[] args) {
		a abj = new A;

	}

}
```
위 코드는 에러가 발생함. 에러가 왜 발생하는지 알아보기 전에, 추상 메소드가 뭔지부터 알아보자.
메소드 b의 선언 부분에는 abstract 키워드가 등장하고 있음. 
무슨 뜻인가면 : 메소드 b의 메소드 시그니처만 정의되어 있고 메소드의 구체적 구현은 하위 클래스에서 오버라이딩해라~   
이렇게 내용이 비어 있는 메소드를 **추상 메소드**라고 한다. 추상메소드를 하나라도 포함하고 있는 클래스는 추상 클래스가 되고, 자연스럽게
클래스의 이름 앞에 abstract가 붙는다.   
   
그럼 에러는 왜 뱉는가? 하면은,
```java
abstract class A{
    public abstract int b();
}
```
본체인 `System.out.println("Hello")`가 존재하는데 추상 메소드를 의미하는 abstract를 사용하고 있기 때문.
```java
public abstract int c(){System.out.println("Hello")}
```
```java
public int d(){
    System.out.println("world");
}
```
아래와 같이 추상 클래스 A를 인스턴스화 하면 오류가 발생함. 
추상 클래스는 구체적인 메소드 내용이 존재하기 않으니 인스턴스화 시켜서 사용할 수가 없기 때문이다.
그럼 어떻게 하면 클래스 A를 써먹을 수 있을까? 애초에 이딴걸 왜 쓰는 걸까?


---
## 추상 클래스의 상속
문제 해결을 위해선 클래스 A를 상속한 하위 클래스를 만들고, 추상 메소드를 오버라이드해서 내용있는 메소드를 만들어야 한다.
아래 코드를 보자.
```java
abstract class A {
	public abstract int b();
	public void d() {
		System.out.println("world");
	}
}
class B extends A {
	public int b() {return 1;}
}
public class AbstractDemo {
	public static void main(String[] args) {
		B obj = new B();
		System.out.println(obj.b());
	}

}
```
차이점은 아래와 같다.
```java
class B extends A{
    public int b(){return 1;}
}
public class AbstractDemo {
    public static void main(String[] args) {
        B obj = new B();
        System.out.println(obj.b());
```
클래스 B는 클래스 A를 상속했고, 그리고 클래스 A의 추상 메소드인 메소드 b를 오버라이딩 중이다. 그 결과 클래스 A를 사용할 수 있다.

---
## 추상 클래스를 사용하는 이유 

