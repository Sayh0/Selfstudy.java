# 추상

**Abstract**-한국어로는 추상-라는 것은 상속을 강제하는 일종의 규제 라고 이해할 것. 왜 '추상'이지? 에 대한 답은 좀 나중에 알아보고, 우선
클래스나 메소드를 사용하기 위해선 **반드시 상속해서 사용하도록 강제하는 것**이 abstract고 이해하자.

## 추상 메소드
추상 메소드랑 **메소드의 시그니처만이 정의되어 있고 나머진 비어있는 메소드**를 의미.   
* *시그니처(서명) : 메소드의 이름 / 메소드 매개변수의 숫자, 데이터타입, 순서 / 메소드의 리턴 타입*


우선 코드를 보자
```java
abstract class A {
	public abstract int b(); //메소드 b에는 구체적인 로직을 담고 있는 본체가 없다.
	public abstract int c() {
	System.out.println("Hello") // 에러.
	} 
	public void d() {
		System.out.println("world");
	}
}
public class AbstractDemo {

	public static void main(String[] args) {
		a abj = new A; //오류

	}

}
```
위 코드는 에러가 발생함. 하지만 에러가 왜 발생하는지 알아보기 전에, 추상 메소드가 뭔지부터 알아보자.
메소드 b의 선언 부분에는 abstract 키워드가 등장하고 있음. 
무슨 뜻인가면 : 메소드 b의 메소드 시그니처만 정의되어 있고 메소드의 구체적 구현은 하위 클래스에서 오버라이딩 하라는 뜻.
이렇게 내용이 비어 있는 메소드를 **추상 메소드**라고 한다. 
추상 메소드를 하나라도 포함하고 있는 클래스는 추상 클래스가 되고, 자연스럽게 클래스의 이름 앞에 abstract가 붙는다.   
   
에러의 원인을 찾아보면, `public abstract int c()`는 로직 `{ {System.out.println("Hello")}`가 존재하는데 
추상 메소드의 abstract를 사용하고 있기 때문에 에러가 발생하는 것이다.<br>
또한 추상 클래스 A 내부의 `public int d(){System.out.println("world");}` 처럼 추상 클래스에는 추상 메소드가 아닌 메소드도 존재할 수 있다.<br>
하지만 `A obj = new A()`와 같이 추상 클래스 A를 인스턴스화 하면 오류가 발생한다.
추상 클래스는 구체적인 메소드 내용이 존재하지 않으니 인스턴스화 시켜서 사용할 수가 없기 때문이다.
그럼 어떻게 하면 클래스 A를 써먹을 수 있을까? 애초에 이걸 왜 쓰는 걸까?<br>

---
## 추상 클래스의 상속
문제 해결을 위해선 클래스 A를 상속한 하위 클래스를 만들고, 추상 메소드를 오버라이드해서 내용이 있는 메소드를 만들어야 한다.
아래 코드를 보자.
```java
abstract class A {
	public abstract int b(); 
	public void d() {
		System.out.println("world");
	}
}
class B extends A { // 클래스 A를 상속한 하위 클래스 B
	public int b() {return 1;}
}
public class AbstractDemo {
	public static void main(String[] args) {
		B obj = new B(); //차이
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
추상 클래스는 상속을 강제하기 위한 것이다. 보통은 큰 프로젝트에서 이런 식의 코드를 작성한다.
부모 클래스에는 메소드의 시그니처만 정의해놓고, 그 메소드의 실제 동작 방법은 이 메소드를 상속받은 하위 클래스의 책임으로 위임한다.<br>
쓰던 계산기 코드에 추상 클래스 개념을 추가해 보자.
```java
abstract class Calculator{
	int left, right;
	public void setOprands(int left, int right) {
		this.left = left;
		this.right = right;
	}
	int _sum() {
		return this.left + this.right; // 공통사용할 덧셈 로직
	}
	int _avg() {
		return (this.left+this.right) / 2); // 공통사용할 평균 로직
	}
	public abstract void sum(); // 사용자가 디자인하는 부분은 abstract 선언.
	public abstract void avg();
	public void run() { //run 메소드로 sum avg 한번에 실행. run 에서는 뭐가 동작하는지만 정해둠. 자세한건 하위 클래스에서 정하게.
		sum();
		avg();
	}
}
class CalculatorDecoPlus extends Calculator {
	public void sum() { // 상속이 강제된 sum을 호출해서 상속시킴.
		System.out.println("+ sum : "+ _sum()); // 공통 사용하는 sum 로직 활용
	}
	public void avg() {
		System.out.println("+ avg : "+ _avg()); // 공통 사용하는 avg 로직 활용
	}
}
class CalculatorDecoMinus extends Calculator {
    public void sum(){ // 활용이 달라졌기에 다시 sum 불러서 상속.
        System.out.println("- sum :"+ _sum());
    }
    public void avg(){
        System.out.println("- avg :" + _avg());
    }
} 
public class CalculatorDemo {
	public static void main(String[] args) {
		CalculatorDecoPlus c1 = new CalculatorDecoPlus();
		c1.setOprands(10,20);
		c1.run();
		
		CalculatorDecoMinus c2 = new CalculatorDecoMinus();
		c2.setOprands(10,20);
		c2.run();
	}
}
```
```
+ sum : 30
+ avg : 15
- sum :30
- avg :15
```
위 코드는 sum을 실행하고 avg를 실행하는 절차를 메소드 run을 통해 간단하게 한 번에 실행시키는 코드이다.
그런데 경우에 따라 합계와 평균을 화면에 출력하는 모습이 달라야 한다면?
**상황에 따라 동작 방법이 달라질 때 추상 메소드를 활용한다.** 달라지는 메소드(여기서는 sum,avg)는 추상 메소드로 만들어 하위 클래스에서 구현하도록 하고,
모든 클래스의 공통분모(여기서는 setOprands, run)는 상위 클래스에 둔다. 이렇게 하면 코드의 중복을 피하고, 유지보수의 용이성을 꾀할 수 있다.
