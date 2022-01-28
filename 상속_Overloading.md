# Overloading
같은 이름이지만 서로 다른 매개변수의 형식을 가지고 있는 메소드를 여러개 정의할 수 있는 방법. 무슨 소리냐면...   


계산기 코드에서 우리의 계산기는 2개의 값(left, right)으로만 연산을 수행할 수 있다. 이걸 3개로 늘리려면 어떻게 해야 할까? 우선 입력값을 늘리기 위해 코드를 수정한다.
```java
c1.setOprands(10, 20, 30);
```
```java
public void setOprands(int left, int right, int third){
    this.left = left;
    this.right = right;
    this.third = third;
}
``` 
다만 이를 위해 기존의 setOprands 메소드를 수정한다면 2개의 입력값을 받을 수 없게 될 것이다.(2개 받는 메소드를 3개로 수정했으니). 메소드의 이름을 변경해서 또 만들수도 있지만 그렇게 되면 
매개변수 수에 따라 메소드를 한도 끝도 없이 만들수도 없는 노릇. 어떻게 할까? 이렇게 한다.
```java
 class Calculator{
    int left, right;
    int third = 0; // 수정된 부분
      
    public void setOprands(int left, int right){
        System.out.println("setOprands(int left, int right)"); // 수정된 부분
        this.left = left;
        this.right = right;
    }
     
    public void setOprands(int left, int right, int third){ //수정된 부분
        System.out.println("setOprands(int left, int right, int third)");
        this.left = left;
        this.right = right;
        this.third = third;
    }
     
    public void sum(){
        System.out.println(this.left+this.right+this.third); // +this.third
    }
      
    public void avg(){
        System.out.println((this.left+this.right+this.third)/3); // +this.third
    }
}
  
public class CalculatorDemo {
      
    public static void main(String[] args) {
          
        Calculator c1 = new Calculator();
        c1.setOprands(10, 20);
        c1.sum();       
        c1.avg();
        c1.setOprands(10, 20, 30); // 수정된 부분
        c1.sum();       
        c1.avg();
         
    }
  
}
```
실행 결과
```
etOprands(int left, int right)
30
15
setOprands(int left, int right, int third)
60
30
```
```
c1.setOprands(10,20);
```
이 코드의 실행 결과는 화면에 `setOprands(int left, int right)` 메시지를 출력한다. 
```
c1.setOprands(10, 20, 30);
```
이 코드의 실행 결과는 화면에 `setOprands(int left, int right, int third)` 메시지를 출력한다. 


매개변수의 숫자에 따라서 같은 이름의, 서로 다른 메소드를 호출하고 있다는 것을 알 수 있다. 
이렇게 이름은 같지만 시그니처는 다른 메소드를 중복으로 선언 할 수 있는 방법을 메소드 **오버로딩**(overloading)이라고 한다.
