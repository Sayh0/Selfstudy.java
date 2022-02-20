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
