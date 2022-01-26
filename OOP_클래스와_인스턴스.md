# 클래스 멤버와 인스턴스 멤버

멤버 Member. 말 그대로 구성원이라는 뜻.   
객체의 구성원은 변수와 메소드이다.   

복습을 해보자.
```java
package org.opentutorials.javatutorials.object;
 
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

   
㉡ c1이라고 하는 변수 안에는 우리가 생성한 객체가 들어 있다. 거기에 setOprand\*라는 메소드를 사용한다. 10과 20을 이 메소드의 인자값으로 전달한다. 지금 단계에선 setOrpand가 어떻게 동작하는 진 모르지만, 어쨌든 c1이라는 객체
*oprand 피연산자 ; 컴퓨터에서 오퍼랜드, 즉 피연산자는 처리될 데이터 그 자체 또는 데이터를 지정하는 컴퓨터 명령어의 일부를 의미한다. 원래 컴퓨터 명령어는 덧셈, 뺄셈 등, 연산을 나타내고, 오퍼랜드는 그 연산의 대상이 되는 것이다.*

left와 right는 인스턴스의 멤버. 인스턴스를 만들어야 사용가능하고, 인스턴스마다 서로 다른 값을 가지고 있기 때문.   
근데 클래스도 멤버를 가질 수 있음. 이게 무슨 소린 고 하면은...
