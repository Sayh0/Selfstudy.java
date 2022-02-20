# 클래스와 인스턴스

## 클래스
```java
class Calculator {
```
클래스는 연관되어 있는 변수와 메소드의 집합. 또는 Calculator 라고 하는 객체의 설계도를 알려주겠다 라고 하는 것을 컴퓨터에게 알려준다고 생각하기. 설계도 안에는 변수들과 메소드가 들어가 있음.

## 인스턴스
```java
Calculator c1 = new Calculator();
```
클래스는 설계도지만 클래스를 정의하는 것 자체로는 부족. 설계도를 구체적인 제품으로 만들어야 함. 그 때 사용하는 키워드가 **new**. new Calculator()은 클래스 Calculator를 구체적인 제품으로 만드는 명령. new 연산자 뒤에는 생성자가 온다. 생성자는 클래스() 형태를 가지고 있음.
**클래스는 설계도이고, 인스턴스는 이걸로 만든 제품이다**. 클래스는 자동차 설계도이고, 인스턴스는 이걸로 찍은 자동차들임.   
위의 코드는 new를 이용해서 만든 인스턴스를 변수 c1에 담은 상태.  c1에 인스턴스를 담은 이유는 c1을 통해서 인스턴스를 제어하기 때문. c1 앞에 Caculator는 데이터 타입을 의미.

// 객체는 독립된 하나의 프로그램으로 생각할 것.   
// 객체는 메소드와 변수의 집합. 프로그램 안의 프로그램.   

변수는 다른 말로 상태State 라고도 표현.    
상태가 다른 객체를 대상으로 메소드를 실행하면 다른 결과가 나옴. ex) c1 sum은 30이 나오고, c2 sum은 60이 나옴.   
그럼 메소드를 행동behave이라고 할 수 있겠지.   
하나의 클래스를 바탕으로 서로 다른 상태를 가진 인스턴스(제품)를 만들면 서로 다른 행동을 하게 할 수 있다.   
하나의 클래스가 여러개의 인스턴스가 된다 == 객체지향의 재활용성.
   
   
```java

class Calculator{ // ㉢
    int left, right; // ㉣
      
    public void setOprands(int left, int right){ //㉤ 
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
우선 이 객체는 left와 right를 받아서 sum과 avg를 수행하는 기능을 가진다라는 것을 이해해야 한다. 그 기능을 하는 부분이 아래 부분.
```java
    public static void main(String[] args) {
          
        Calculator c1 = new Calculator(); // ㉠
        c1.setOprands(10, 20); // ㉡
        c1.sum();       
        c1.avg();       
          
        Calculator c2 = new Calculator();
        c2.setOprands(20, 40);
        c2.sum();       
        c2.avg();
```
```java
Calculator c1 = new Calculator();
```
㉠ 우리는 Caculator 라는 객체를 새로 만들었다. ()가 붙어서 메소드처럼 보일 수 있지만, 앞에 new가 붙어 있으니 메소드는 아니다. 이것을 객체라고 하자. 그리고 새로 만들었으니까 new 를 붙였다고 생각하자. 새로 만든 객체를 c1 이라는 변수에 담는다. 그 변수는 Caculator 라는 변수를 새로 담을 수 있는 타입이라는 뜻에서 앞에 Caculator를 붙인다.   
**new Calculator()은 클래스 Calculator를 구체적인 제품으로 만드는 명령이다. 이렇게 만들어진 구체적인 제품을 인스턴스(instance)라고 부른다. 클래스가 설계도이고, 인스턴스는 제품이다**   
변수 c1의 데이터 타입이 Calculator라는 건, 클래스를 만드는 건 사용자 정의 데이터 타입을 만드는 것과 같은 의미. 사용자 정의 타입이 뭔지는 차차 알기로 하고, 지금은 클래스를 인스턴스화(제품처럼 쓰기) 할 때는 변수에 담아야 한다는 것과 이 때 사용하는 변수의 데이터 타입은 그 클래스가 된다는 것만 기억하자.

   
㉡ c1이라고 하는 변수 안에는 우리가 생성한 객체가 들어 있다. 거기에 setOprands\*라는 메소드를 사용한다. 10과 20을 이 메소드의 인자값으로 전달한다. 지금 단계에선 setOrpands가 어떻게 동작하는 진 모르지만, 어쨌든 c1이라는 객체에 sum이라고 하는 메소드를 호출하면 ()안에 입력값을 주지 않아도 출력값이 나온다. 각각의 메소드들의 역할에 의해.
*oprand 피연산자 ; 컴퓨터에서 오퍼랜드, 즉 피연산자는 처리될 데이터 그 자체 또는 데이터를 지정하는 컴퓨터 명령어의 일부를 의미한다. 원래 컴퓨터 명령어는 덧셈, 뺄셈 등, 연산을 나타내고, 오퍼랜드는 그 연산의 대상이 되는 것이다.*
   
   
㉢ ㄱ과 ㄴ에서 어떤 객체(Calculator)를 생성해서 변수(c1)에 담았다. 그러한 것을 인스턴스-구체적인 객체-라고 부르기로 했다. 그럼 그 구체적인 객체를 만들기 위해선 그 객체가 어떤 모습인지, 어떤 메소드와 변수로 이루어져 있는지를 알려주는 설계도가 있어야 함. 그게 바로 ㄷ 부분이다. Caculator 앞에 class 라는 키워드는 '지금부터 Calculator 라고하는 객체의 설계도를 알려주겠다' 라고 컴퓨터에게 통보하는 키워드. Calculator는 new 를 통해 만든 ㄱ 부분임. 우리가 new 를 통해서 실제 생성한 것의 설계도가 ㄷ 부분인 것.   
   
   
설계도에서는 left, right 변수를 선언하고, setOrprands 가 드디어 등장한다. 다른건 알겠는데, "this." 는 뭘까? this.left는 인스턴스를 가리킨다. . ㄹ부분. calculator 클래스를 정의할 때 선언했던 그 left. 우측의 그냥 left는 ㅁ 부분이다. 매개변수. 따라서 left에 10이 담기게 되고 class 전역에서 left는 10으로 사용한다. 그 10으로 sum과 avg 수행하게 되는 것.
