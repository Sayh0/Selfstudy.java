# Object 클래스
모든 클래스의 조상은 Object 클래스에 대해.<br>

## 상속
자바에서 상속은 필수적이다. 우리가 상속을 쓰던 안 쓰던 기본적인 상속은 하고 있다.
```
package org.opentutorials.javatutorials.progenitor;

class O {
...
}
```
```
package org.opentutorials.javatutorials.progenitor;

class O extends Object {
...
}
```
위 두 코드는 같은 코드이다. 자바에서 모든 클래스는 사실 **Object**를 암시적으로 상속받고 있다. 사실상 모든 클래스의 조상 격인 셈이다.<br>
이유는 모든 클래스가 공통으로 포함하고 있어야 하는 기능을 제공하기 위해서인데, 그게 뭔지 API 문서를 보면 다음과 같다.<br>
<br>
![2123](https://user-images.githubusercontent.com/96712990/160845205-7d848eac-2525-4f7c-8133-8cfed8efc7e9.png)

Object 클래스가 가지고 있는 메소드 목록이다. 자바의 객체는 위의 메소드들을 반드시 가지고 있다소 할 수 있다.
이 중에서 중요하면서 입문 단계에서 이해할 수 있는 API 들을 알아보자.

## toString
**toString**은 객체를 문자로 표현하는 메소드이다. 매일 쓰던 계산기 코드로 알아보자.
```java
class Calculator {
	int left, right;
	
	public void setOprands(int left, int right) {
		this.left = left;
		this.right = right;
	}
	public void sum() {
		System.out.println(this.left + this.right);
	}
	
	public void avg() {
        System.out.println((this.left+this.right)/2);
	}
}
public class CalculatorDemo {
	public static void main(String[] args) {
		Calculator c1 = new Calculator();
		c1.setOprands(10, 20);
		System.out.println(c1);
		
	}

}
```
`System.out.println(c1);`코드를 통해 클래스 `Calculator`의 인스턴스 `c1`을 화면에 출력하고 있다.




