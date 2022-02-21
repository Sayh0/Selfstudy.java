## 멤버
클래스는 설계도, 인스턴스는 제품이라고 했다. 인스턴스들은 인스턴스에 들어가 있는 변수의 값에 따라 상태가 달라지므로 그걸로 서로를 구분한다. 
그 상태에 따라 행위를 하면(메소드를 실행하면) 그 상태에 따라 다른 결과를 리턴한다.<br><br>
그럼 멤버는 뭘까? 멤버는 구성원이라는 뜻이다. 객체의 구성원은 아래와 같다(객체는 변수와 메소드의 집합이다라는 것은 계속 강조를 하고 있다).
* 변수
* 메소드
클래스를 구체적인 제품인 인스턴스로 만들게 되면 인스턴스 안에는 클래스에서 정의된 변수와 메소드가 존재한다. 그러한 것들이 인스턴스 안의 멤버이다.
무슨 소리인지 모르니 코드로 이해해보자.
```java
class Calculator{
    int left, right;
      
    public void setOprands(int left, int right){
        this.left = left;
        this.right = right;
    }
      
    public void sum(){
        System.out.println(this.left+this.right);
    }
      
    public void avg(){
        System.out.println((this.left+this.right)/2);
    }
}
  
public class CalculatorDemo4 {
      
    public static void main(String[] args) {
          
        Calculator c1 = new Calculator();
        c1.setOprands(10, 20);
        c1.sum();       
        c1.avg();       
          
        Calculator c2 = new Calculator();
        c2.setOprands(20, 40);
        c2.sum();       
        c2.avg();
    }
  
}
```
여기서 쓰인 인스턴스 변수 left를 보면, left의 값은 각 인스턴스마다 다르다. 인스턴스 변수 c1의 left 값은 10, c2의 값은 20이다. 
인스턴스의 상태인 변수의 값이 인스턴스마다 다른 값을 가질 수 있다는 건 클래스 하나로 여러 인스턴스를 만들수 있다는 좋은 기능이다.
근데 만약에 모든 인스턴스가 같은 값을 공유하게 하고 싶으면? 예를 들어 우리 계산기에서 특정 값(ex)원주율)을 사용자에게 제공하고 싶을 때. 
원주율 값은 3.14 상수이므로 각각 인스턴스마다 별도로 원주율 값을 가져야 할 이유가 없다. 이 때 변수를 클래스 멤버로 만들면 된다. 이렇게.
```java
class Caculator {
    static double PI = 3.14; // << 추가
    int left, right;
    
    public void setOprands(int left, int right) {
...
```
변수 PI 앞에 static 이 붙었다. **static을 멤버(변수 메소드) 앞에 붙이면 클래스의 멤버, 그러니까 클래스 소속의 변수가 된다.** 
이제 만들었으니 어떻게 쓰는 지 알아보자.
클래스 변수에 접근하는 방법은,
```
System.out.println(c1.PI); // 인스턴스를 통해 PI에 접근.
System.out.println(Calculator.PI); // 클래스를 통해 PI에 접근.
```
이 중 두번째 방법은 객체 Calculator.java의 다른 기능(sum,avg)은 필요없고, 원주율만 필요할 때 클래스에 직접 접근하기 때문에 인스턴스를 생성할 필요가 없어진다.<br><br>

클래스 변수는 변수의 변경사항을 모든 인스턴스애서 공유해야 할 때도 사용한다. 이를테면, 연산을 할 때 언제나 특별한 값을 포함시켜야 할 때.
```java
class Calculator2 {
	static double PI = 3.14;
	static int base = 0; //클래스 변수인 base 가 추가되었음.
	int left, right;
	
	public void setOprands(int left, int right) {
		this.left = left;
		this.right = right;
	}
	
	public void sum() {
		System.out.println(this.left + this.right + base); //더하기에 base 값 포함
	}
	
	public void avg() {
		System.out.println((this.left + this.right + base)/2);//평균에 base 값 포함	
	}
}

public class CalculatorDemo2 {
	
	public static void main(String[] args) {
		
		Calculator2 c1 = new Calculator2();
		c1.setOprands(10, 20);
		c1.sum(); //30 출력
		
		Calculator2 c2 = new Calculator2();
		c2.setOprands(20, 40);
		c2.sum(); // 60 출력
		
		Calculator2.base = 10; // 클래스 변수 base의 값을 10으로 변경
		
		c1.sum(); // 40 출력
		c2.sum(); // 70 출력
	}
	
}
```
`Calculator2.base = 10;`로 클래스 변수 base의 값을 10으로 변경하면 모든 인스턴스의 base 값이 일제히 변경되어 결과가 다르게 나온다.<br><br>
클래스 변수의 용도를 정리하면 다음과 같다.
* 인스턴스에 따라 변하지 않는 값이 필요할 때 (후에 배울 final이 좀 더 유용하긴 하지만 아직 안 배웠으니 패스)
* 인스턴스를 생성할 필요가 없는 값을 클래스에 저장하고 싶을 때.
* 값의 변경 사항을 모든 인스턴스가 공유해야 할 때.

## 클래스 메소드
클래스 변수가 있으면 클래스 메소드도 있겠지. 예제 Calculator 에서는 인스턴스 변수 left와 right로 합계와 평균을 구한다. 
굳이 인스턴스가 항상 left, right 값을 유지해야 할까? 노노. 합계나 평균을 구할 때마다 좌항과 우항의 값을 주는 방식으로 계산할 수도 있다. 아래를 보자.
```java
class Calculator3 {
	
	public static void sum(int left, int right) {
		System.out.println(left + right);
	}
	
	public static void avg(int left, int right) {
		System.out.println((left+right)/2);
	}
	
}
public class CalculatorDemo3 {
	
	public static void main(String[] args) {
		Calculator3.sum(10, 20);
		Calculator3.avg(10, 20);
		
		Calculator3.sum(20, 40);
		Calculator3.avg(20, 40);
	}

}
```
원래는 Calculator라는 클래스를 구체화시킨 인스턴스를 만들어서(`Calculator c1 = new Calculator();`이런 식으로) 진행했다.
근데 이번 예제는 인스턴스가 드러나지 않는다. 그냥 `Calculator3.sum(10, 20);`처럼 클래스에 직접 접근에서 sum과 avg를 호출하고 있는 것이다.
Calculator3가 어떻게 구현되어 있는가 살펴보면,
```
class Calculator3 {
	
	public static void sum(int left, int right) {
		System.out.println(left + right);
	}
...
```
sum이라는 메소드에 static이라는 키워드를 달면 클래스 소속의 메소드가 된다. 그 메소드의 인자값으로 left, right값을 주고 그 계산값을 print로 화면에 출력하고 있다.
클래스에 직접 접근해서 실행할 수 있게 되는 것이다. 만약 메소드가 인스턴스 변수를 참조하지 않는다면, **클래스 메소드를 사용해서 불필요한 인스턴스 생성을 막을 수 있다.**

## 클래스 메소드2
클래스와 인스턴스의 차이를 알아보기 위해 오류가 있는 코드를 보기로 하자. 보기 전에 몇가지 원칙을 기억하고 예제를 보면 이해가 더 쉽다.<br>
**1. 인스턴스 메소드는 클래스 멤버에 접근할 수 있다.**
**2. 클래스 메소드는 인스턴스 멤버에 접근할 수 없다.**<br>
인스턴스 변수는 인스턴스가 만들어지면서 생성되는데, 클래스 메소드는 인스턴스가 생성되기 전에 **먼저** 만들어진다. 
따라서 클래스 메소드가 인스턴스 멤버에 접근하는 건 존재하지 않는 변수에 접근하는 것이기 때문에 불가능하다. 코드를 보자.
```java
class C1 {
	static int static_variable = 1; // 클래스 변수
	int instance_variable = 2; // 인스턴스 변수
	static void static_static() { // 클래스 메소드가 클래스 변수를 호출.
		System.out.println(static_variable);
	}
	static void static_instance() { // 클래스 메소드가 인스턴스 변수를 호출.
		System.out.println(instance_variable); // 오류. 클래스 메소드에선 인스턴스 변수에 접근 불가
	}
	void instance_static() {
		System.out.println(static_variable);	
	}
	void instance_instance() {
		System.out.println(instance_variable);
	} // 인스턴스 메소드에선 클래스 메소드에 접근 가능.
}
public class ClassMemberDemo {
	public static void main(String[] args) {
		C1 c = new C1(); // C1이라는 클래스를 c라는 인스턴스에 담음.
		c.static_static(); // 인스턴스 메소드에서 클래스 변수에 접근.
		c.static_instance(); // 실패! 클래스 메소드에서 인스턴스 변수에 접근 불가.
		c.instance_static(); // 인스턴스 변수에서 클래스 변수에 접근.
		c.instance_instance(); // 인스턴스 메소드에서 인스턴스 변수에 접근.
		C1.static_static(); // 클래스를 통해서 직접 클래스 메소드에 접근.
		C1.static_instance(); // 실패! 클래스 메소드에서 인스턴스 변수에 접근 불가.
		C1.instance_static(); // 실패! 클래스를 통해서 인스턴스 메소드는 접속 불가.
		C1.instance_instance(); // 실패! 클래스를 통해 인스턴스 변수에도 접속 불가.
	}

}
```
인스턴스 변수와 클래스 변수는 아래와 같이 부르기도 한다.<br>

* 인스턴스 변수 -> Non-Static Field
* 클래스 변수 -> Static Field<br>

필드(field)라는 것은 클래스 전역에서 접근 할 수 있는 변수를 의미하는데, 이에 대한 자세한 내용은 유효범위에서 다룬다.
