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
```
여기서 left와 right는 인스턴스의 멤버. 인스턴스를 만들어야 사용가능하고, 인스턴스마다 서로 다른 값을 가지고 있기 때문.   
근데 클래스도 멤버를 가질 수 있음. 이게 무슨 소린 고 하면은...
