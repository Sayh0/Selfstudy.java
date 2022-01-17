# 객체 지향 프로그래밍.Object Oriented Programming 

객체지향 프로그램은 객체를 만드는 것. 이 객체들을 조립하여 하나의 프로그램을 만드는 것.
하나의 객체 안에는 그 객체가 가지고 있는 취지/기능을 하는 메소드와 변수가 담겨 있음.
결국 객체는 어떤 추상적인게 아니라 변수와 메소드를 그룹핑한 것.
이렇게 만들어진 객체들을 다른 곳에서 또 사용할 수가 있음. 재활용성.

## 어떻게 쓰는가?

현실의 추상화 중요. 소프트웨어적으로 단순화 시킬수 있는가.
부품화, 은닉화(캡슐화), 인터페이스(연결점). 

### 왜 객체를 쓰는거지?

예를 들어서 계산기 프로그램을 짠다고 생각해보자.

```java
// 목표는 계산기 만들기.left와 right로 sum과 avg를 계산. 
public class Calculator {
	// class 는 Calculator 라고 하는 객체의 설계도를 알려주겠다 라고 하는 것을 컴퓨터에게 알려주는 것.
	/*
	 * 클래스는 연관되어 있는 변수와 메소드의 집합이다.
	 */
	// Calculator 는 23행에서 만든 것.
    int left, right; // 레프트와 라이트 선언.
    
    public void setOprands(int left, int right){
        this.left = left;
    // this. 가 붙으면 그 인스턴스 자신을 의미.
        this.right = right;
    }
      
    public void sum(){
        System.out.println(this.left+this.right);
    }
      
    public void avg(){
        System.out.println((this.left+this.right)/2);
    }
    public static void main(String[] args) {
        
        Calculator c1 = new Calculator(); // Calculator라는 객체를 새로 만들어서 c1이라는 변수에 담음.
        /*
         * new Calculator()는 클래스 Calculator를 구체적인 제품으로 만드는 명령.
         * 이렇게 만들어진 제품을 인스턴스instance라고 부른다.
         */
        // 이때 c1앞에는 Calculator 변수를 담았다는 뜻으로 앞에 붙임.
        // 사용자 임의로 '데이터 타입'을 만들었다고 이해할 것.
        c1.setOprands(10, 20); // setOprands 메소드는 연산의 대상이 될 값. 
        // public void setOprands(int left, int right) 이거임. 매개변수 left right 에는 10과 20이 들어가겠지.
        c1.sum();       
        // 
        c1.avg();       
          
        Calculator c2 = new Calculator();
        c2.setOprands(20, 40);
        c2.sum();       
        c2.avg();
    }
}
```

// 객체는 독립된 하나의 프로그램으로 생각할 것.
// 객체는 메소드와 변수의 집합. 프로그램 안의 프로그램.

변수는 다른 말로 상태State 라고도 표현. 
상태가 다른 객체를 대상으로 메소드를 실행하면 다른 결과가 나옴. ex) c1 sum은 30이 나오고, c2 sum은 60이 나옴.
그럼 메소드를 행동behave라고 할 수 있겠지.
하나의 클래스를 바탕으로 서로 다른 상태를 가진 인스턴스(제품)를 만들면 서로 다른 행동을 하게 할 수 있다.
하나의 클래스가 여러개의 인스턴스가 된다 == 객체지향의 재활용성.
