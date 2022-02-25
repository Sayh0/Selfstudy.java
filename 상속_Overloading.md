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
다만 이를 위해 기존의 setOprands 메소드를 수정한다면 2개의 입력값을 받을 수 없게 될 것이다.(2개 받는 메소드를 3개로 수정했으니). 
메소드의 이름을 변경해서 또 만들수도 있지만 그렇게 되면 매개변수 수에 따라 메소드를 한도 끝도 없이 만들수도 없는 노릇. 어떻게 할까?
```java
 class Calculator{
    int left, right;
    int third = 0; // 수정된 부분. 전역변수 추가.
      
    public void setOprands(int left, int right){
        System.out.println("setOprands(int left, int right)"); // 수정된 부분. 매개변수 두개의 메소드라는 뜻의 프린트 출력용.
        this.left = left;
        this.right = right;
    }
     
    public void setOprands(int left, int right, int third){ //수정된 부분. 매개변수 3개용 메소드 오버로딩.
        System.out.println("setOprands(int left, int right, int third)");
        this.left = left;
        this.right = right;
        this.third = third; // 세번째 매개변수를 전역변수로
    }
     
    public void sum(){
        System.out.println(this.left+this.right+this.third); // +this.third 추가
    }
      
    public void avg(){
        System.out.println((this.left+this.right+this.third)/3); // +this.third 추가.
    }
}
  
public class CalculatorDemo {
      
    public static void main(String[] args) {
          
        Calculator c1 = new Calculator();
        c1.setOprands(10, 20);
        c1.sum();       
        c1.avg();
        c1.setOprands(10, 20, 30); // 수정된 부분. 세개의 인자 전달하는 메소드
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

setOprands라는 같은 이름을 쓰는 메소드가 여러 개 있지만 충돌이 일어나지 않는다. 매개변수의 숫자가 다르기 때문에 자동으로 서로 다른 것으로 자바가 인식해준다.
매개변수의 숫자에 따라서 같은 이름의, 서로 다른 메소드를 호출하고 있다는 것을 알 수 있다. 
이렇게 이름은 같지만 시그니처는 다른 메소드를 중복으로 선언 할 수 있는 방법을 메소드 **오버로딩**(overloading)이라고 한다.
추가하자면, 위 코드에서 `setOprands` 메소드의 매개변수가 3개던 2개이던 안의
```
    this.left = left;
    this.right = right;
```
부분은 동일하다(중복). 중복을 제거하려면 어떻게 할까? this.를 활용하면 된다. this.는 자기 자신을 의미하는 변수이니까, 
```
    this.setOrpands(left, right);
```
로 바꾸면 된다. (`System.out.println("setOprands(int left, int right)")` 부분은 여기선 어떤 메소드가 쓰였는지 쉽게 알아보기 넣은 거니까 없애도 상관없다)<br><br>

## Overloading의 규칙
결론적으로, 메소드 오버로딩은 매개변수를 사용한다. 즉, 매개변수가 다르면 이름이 같아도 서로 다른 메소드가 되는 셈이다.
반면에 매개변수는 같지만 리턴 타입이 다르면 에러가 발생한다.
```java
public class OverloadingDemo {
    void A () {System.out.println("void A()");
    }
    void A (int arg1) {System.out.println("void A (int arg1)");
    }
    void A (String arg1) {System.out.println("void A (String arg1)");
    }
    int A () {System.out.println("void A()"); // 오류 : 같은 이름, 같은 매개변수 갯수의 메소드 (첫번째)가 있지만 리턴값이 서로 달라서 오버로딩 불가. 
    }
    public static void main(String[] args) {
        OverloadingDemo od = new OverloadingDemo();
        od.A(); // 첫번째 매개변수가 없는 메소드 호출
        od.A(1); // 두번째 int 데이터타입 매개변수 있는 메소드 호출
        od.A("coding everyday"); // 세번째 문자열 데이터타입 매개변수 메소드 호출
    }
}
```
`void A ()`와 `void A (int arg1)`는 매개변수 갯수가 다르다. `void A (int arg1)`와 `void A (String arg1)`는 갯수는 같지만 데이터 타입이 다르다. 이런 경우는 오버로딩이 가능하다.
메소드를 호출할 때 전달되는 인자의 데이터 타입에 따라서 어떤 메소드를 호출할지를 자바가 판단할 수 있기 때문이다. 
하지만 메소드의 반환값은 [메소드를 사용하는 단계]에서 알려줄 수 있는 정보가 아니라 [메소드 사용 후 반환 결과]이기 때문에 
호출하는 시점에서 전달되지 않는 정보가 아니고, 호출 시점에서 자바가 판단할 수 없으니 오버로딩이 될 수 없다.
비슷하게, 매개변수의 이름을 달리해도 메소드 오버라이딩이 불가능하다. 매개변수의 이름은 메소드 내부에서 사용되는 것이기에 호출 단계에서는 매개변수의 이름이 뭐든 상관않기 때문이다. 
<br><br>

## 상속과 오버로딩
상속 관계에서도 오버로딩을 사용할 수 있다.
```java
public class OverloadingDemo2 extends OverloadingDemo {
    void A (String arg1, String arg2){System.out.println("sub class : void A (String arg1, String arg2)");}
    void A (){System.out.println("sub class : void A ()");}
    public static void main(String[] args) {
        OverloadingDemo2 od = new OverloadingDemo2();
        od.A();
        od.A(1);
        od.A("coding everyday");
        od.A("coding everyday", "coding everyday"); 
    }
}
```
결과
```
sub class : void A ()
void A (int arg1)
void A (String arg1)
sub class : void A (String arg1, String arg2)
```
클래스 `OverloadingDemo2`는 `OverloadingDemo`를 상속받고 있다. 
`OverloadingDemo2`에서 정의 된 메소드 `void A (String arg1, String arg2)`는 문자열 데이터 타입의 매개변수 2개를 가지고 있다.
이러한 형태의 변수는 부모 클래스에선 정의되있지 않으니, 자동으로 메소드 오버로딩이 이루어진다.
반면 `void A ()` 메소드는 매개변수가 없다. 부모 클래스에도 매개변수 없는 가 존재한다. 
이 둘은 매개변수 형태가 같기 때문에 오버로딩이 아니라 **오버라이딩**Overriding이다.

### 오버로딩? 오버라이딩?
메소드 오버로딩은 같은 이름 다른 메소드에 의해서 여러 개의 같은 이름의 메소드들을 정의할 수 있는 것.
오버라이딩은 부모 클래스가 있고 자식이 있을때 부모 클래스에 있는 메소드를 메소드의 이름, 매개변수의 형식, 리턴타입이 동일(=시그니처가 동일)한 메소드를
자식 클래스에서 정의하는 걸 통해서 부모 클래스에 있는 메소드를 상속받지 않고 자식 클래스에서 다시 새롭게 변경하고자 할떄 사용하는 개념.
