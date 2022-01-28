# Overriding
 상속은 상위 클래스의 기능을 하위 클래스에게 물려주는 기능임. 그럼 하위 클래스는 상위 클래스 모습 그대로 물려 받아야 할까? 
 만약 이 제약을 벗어나려면 하위 클래스가 부모 클래스의 기본적인 동작방법을 변경할 수 있어야 한다. 이런 기능이 바로 **메소드 오버라이딩**이다.
    
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
	
	public void sum() {                                                         // 추가된 부분
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
실행 결과는 30입니다.  // 결과가 바뀐 부분
15
-10
```
메소드 sum이 SubstractionableCalculator에 추가되었음. 실행 결과는 c1.sum 이 상위 클래스의 메소드가 아니라 하위 클래스의 메소드 sum을 실행하고 있다는 것을 보여줌.
하위 클래스에서 상위 클래스와 동일한 메소드를 정의하면 부모 클래스서부터 받은 기본 동작방법을 변경하는 효과가 있다. 이게 메소드 오버라이딩.   
   
## 메소드 오버라이딩의 조건



 
