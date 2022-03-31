# Overriding
## 창의적인 상속
 상속은 상위 클래스의 기능을 하위 클래스에게 물려주는 기능임. 그럼 하위 클래스는 상위 클래스 모습 그대로 물려 받아야 할까? 
 만약 이 제약을 벗어나려면 **하위 클래스가 부모 클래스의 기본적인 동작방법을 변경할 수 있어야 한다**. 이런 기능이 바로 **메소드 오버라이딩**이다.
    
 처음 상속을 배울 때 썼던 코드에 몇 가지를 추가해서 다시 보자.
 ```java
 class Calculator {
	int left, right;
	
	public void setOprands(int left, int right) {
		this.left = left;
		this.right = right;
	}
	
	public void sum() {
		System.out.println(this.left + this.right); // 원래는 이게 실행되어야 하는데
	}
	
	public void avg() {
		System.out.println((this.left + this.right) / 2);
	}
}

class SubstractableCalculator extends Calculator {
	// 추가된 부분
	public void sum() { 
		System.out.println("실행 결과는 " + (this.left + this.right) + "입니다");  // 이게 실행됨(하위 클래스의 메소드)
	}
	
	public void substract() {
		System.out.println(this.left + this.right);
	}
}
public class CalculatorDemo {
	public static void main(String[] args) {
		SubstractableCalculator c1 = new SubstractableCalculator();
		c1.setOprands(10,20);
		c1.sum();
		c1.avg();
		c1.substract();
	}

}
```
실행 결과
```
실행 결과는 30입니다.  // 결과가 바뀐 부분. Overriding.
15
-10
```
메소드 `sum`이 `SubstractionableCalculator`에 추가되었음. 실행 결과는 `c1.sum` 이 상위 클래스의 메소드가 아니라 하위 클래스의 메소드 `sum`을 실행하고 있다는 것을 보여줌.
기존의 `Calculator` 클래스가 `sum`이라고 하는 메소드를 가지고 있었는데 이 `Calculator` 클래스를 상속받은 `SubstractableCalculator` 클래스가 부모가 이미 가지고 있는 메소드인
`sum`을 재정의Overriding 하고 있는 것.
**하위 클래스에서 상위 클래스와 동일한 메소드를 정의하면 부모 클래스서부터 받은 기본 동작방법을 변경하는 효과가 있다. - 메소드 오버라이딩**.   
   
## 메소드 오버라이딩의 조건
원래 코드에서는 상위 클래스에서 정의하고 있는 메소드 `avg`의 계산 결과를 화면에 출력하고 있다. 이걸 화면 출력 대신 메소드 바깥쪽으로 리턴하게 하고 싶다면 어떻게 할까?
하위 클래스의 `avg`를 overriding하면 된다.
주의해야 할 점은, overriding 하기 위해선 메소드와 리턴 형식이 같아야 한다는 것이다. 
부모 클래스 `Calculator`의 메소드 `avg` 리턴 타입은 void이다. 이것을 상속한 하위 `SubstractableCalculator` 클래스의 리턴 타입은 int이다. 맞추지 않으면 에러가 발생한다. 
오버라이딩 하려면

* 메소드의 리턴 타입
* 메소드의 이름
* 메소드 매개변수의 개수, 데이터타입, 순서

을 같게 만들어야 한다. 이것을 메소드의 **서명signature**이라 한다. 서명이 다를 시 에러가 발생한다. 에러를 염두하면서 상위 클래스 코드를 변경해 보겠다.

```java
package org.opentutorials.javatutorials.overriding.example1;
 
class Calculator {
    int left, right;
 
    public void setOprands(int left, int right) {
        this.left = left;
        this.right = right;
    }
 
    public void sum() {
        System.out.println(this.left + this.right);
    }
 
    public int avg() { // 부모 메소드의 void 를 int 로 변경
        return ((this.left + this.right) / 2); // print 를 return 으로 변경
    }
}
 
class SubstractionableCalculator extends Calculator {
     
    public void sum() {
        System.out.println("실행 결과는 " +(this.left + this.right)+"입니다.");
    }
     
    public int avg() {  // 변경된 부분
        return ((this.left + this.right) / 2);
    }
     
    public void substract() {
        System.out.println(this.left - this.right);
    }
}
 
public class CalculatorDemo {
    public static void main(String[] args) {
        SubstractionableCalculator c1 = new SubstractionableCalculator();
        c1.setOprands(10, 20);
        c1.sum();
        c1.avg();
        c1.substract();
    }
}
```

상위 클래스와 하위 클래스의 서명이 같기 때문에 메소드 오버라이딩을 할 수 있었다. 그런데 위의 코드를 보면 중복이 발생했다. 
메소드 `avg`의 부모와 자식 클래스가 같은 로직`return ((this.left + this.right) / 2)`을 가지고 있다. 중복은 제거 되어야 한다. 
생성자와 마찬가지로 super를 사용하면 이 문제를 해결 할 수 있다.

```java

...(중략)
    public int avg() { // 부모 클래스의 메소드 avg.
        return ((this.left + this.right) / 2); 
    }
}
class SubstractionableCalculator extends Calculator {
     
    public void sum() {
        System.out.println("실행 결과는 " +(this.left + this.right)+"입니다.");
    }
     
    public int avg() {
    	// return ((this.left + this.right) / 2); 	제거
        return super.avg(); 				// super.avg() 로 변경. 부모 클래스의 메소드 avg를 호출.
    }
     
    public void substract() {
        System.out.println(this.left - this.right);
    }
}
 
public class CalculatorDemo {
    public static void main(String[] args) {
        SubstractionableCalculator c1 = new SubstractionableCalculator();
        c1.setOprands(10, 20);
        c1.sum();
        System.out.println("실행 결과는" + c1.avg()); // 변경된 부분
        c1.substract();
    }
}
```
하위 클래스의 메소드 `avg`에서 상위 클래스의 메소드를 호출하기 위해서 super를 사용하고 있다. 덕분에 코드의 중복을 제거 할 수 있었다.

---
## 정리
* Overriding 은 '재정의' 하는 것이다. 하위 클래스가 상위 클래스의 메소드를 그대로만 사용해야 한다면 너무 제약이 크기에, 하위 클래스가 부모 클래스의 동작방법을 변경할 수 있게 도입된 기능이 메소드 오버라이딩이다.
* 하위 클래스에서 상위 클래스와 동일한 메소드를 정의하면 부모 클래스로부터 물려받은 기본 동작 방법을 변경하는 효과를 갖게 된다. 예외적용은 기본적용에 우선한다는 공학논리에 따라.
* 오버라이딩을 위해서는 메소드의 서명이 일치해야 한다. 서명은 메소드의 이름 / 메소드 매개변수의 숫자와 데이터 타입, 순서 / 메소드의 리턴 타입 이다.
* 하위 클래스의 메소드에서 상위 클래스의 메소드를 호출하기 위해서 super를 사용한다. 이걸로 코드 중복을 줄일 수 있다.
