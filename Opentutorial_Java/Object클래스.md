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
**toString**은 객체를 문자화, 문자로 표현하는 메소드이다. 매일 쓰던 계산기 코드로 알아보자.
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
`System.out.println(c1);`코드를 통해 클래스 `Calculator`의 인스턴스 `c1`을 화면에 출력하고 있다.<br>
결과는 이러하다.
```
org.opentutorials.javatutorials.progenitor.Calculator@1bc6a36e
```
이것은 인스턴스 `c1`이 클래스 `Calculator`의 인스턴스라는 의미이다. @ 뒤의 내용은 인스턴스에 대한 고유 식별 주소값 정도로 이해하자.<br>
위의 정보도 유용하지만, 클래스 설계자의 필요에 따라서 toString의 결과를 더욱 유용하게 만들 수 있다. 
예를 들어 계산기 인스턴스의 left, right 값을 알 수 있다면 개발이 좀 더 수월해 질 것이다.
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
     
    public String toString(){ //변경점.
        return "left : " + this.left + ", right : "+ this.right;
    }
}
  
public class CalculatorDemo {
      
    public static void main(String[] args) {
          
        Calculator c1 = new Calculator();
        c1.setOprands(10, 20);
        System.out.println(c1);
        System.out.println(c1.toString());
    }
  
}
```
```
left : 10, right : 20
left : 10, right : 20
```
클래스 `Calculator`에 toString 을 재정의(Overriding)했다. 그리고 인스턴스를 `System.out.println`의 인자로 전달하니
toString을 명시적으로 호출하지 않아도 동일한 효과를 보인다. toString 메소드는 자바에서 특별히 취급하는 메소드다. 
**toString을 직접 호출하지 않아도 어떤 객체를 System.out.print로 호출하면 자동으로 toString이 호출되도록 약속되어 있다**. 
이를 통해 우리는 인스턴스(여기서는 `c1`)의 상태를 쉽게 파악할 수 있게 되었다.



