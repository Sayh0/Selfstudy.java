# 초기화와 생성자
**초기화**는 어떤 일을 시작하기 전 준비를 하는 것이라고 생각하면 됨. **생성자**는 그런 초기화를 객체 단위에서 할 수 있도록 도와주는 것.   
이해를 돕기 위해 이전에 썼던 계산기 코드를 다시 보자.
```java
public class Calculator {

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
원래 코드에서 로직은 이러하다.
```java
Calculator c1 = new Calculator(); // Calculator 라는 class를 new 를 통해 선언해서 인스턴스화 시키고, 이것을 c1이라는 변수에 담은 것.
c1.setOprands(10, 20); // 이 절차를 항상 먼저 수행해야 함.
c1.sum();       
c1.avg();  
```
메소드 setOprands의 값으로 10, 20 을 지정함. 이 값들은 객체 내부에서 인스턴스 변수 left, right 의 값으로 설정되어서 유지된다. 
이 객체를 이용하기 위해선 기억해야 할 것은, 메소드 setOprands를 호출하기 전에 sum과 svg를 먼저 호출했다면 원하는 결과와 다른 값이 나오기에, 항상 setOrpands를 먼저 호출해야 한다는 것이다.
```java
Calculator c1 = new Calculator(); 
c1.sum();       
c1.avg(); 
// setOrpands로 초기화를 하지 않았기 때문에 예상하는 값과 다른 결과가 나올 것이다.
```
 객체 Calculator를 사용하기 위해서 사용자는 메소드 sum을 호출하기 전에 setOprands를 호출해야 한다는 것을 기억하고 있어야 한다. 이러한 절차는 불편하고, 오류발생 확률 높임. 
 어떻게 이런 불편을 줄여볼까 해서 나온 것이 **생성자**Constructor.

## 생성자
인스턴스가 생성될 때, left와 right 값을 입력하도록 강제한다면? 원래 코드를 살짝 바꿔보자.
```java
class Calculator {
    int left, right;
 
    public Calculator(int left, int right) { // 수정된 내용. 클래스 이름과 똑같은 메소드가 등장
        this.left = left;
        this.right = right; 
    }
 
    public void sum() {
        System.out.println(this.left + this.right);
    }
    
 
    public void avg() {
        System.out.println((this.left + this.right) / 2);
    }
}
 
public class CalculatorDemo1 {
 
    public static void main(String[] args) {
 
        Calculator c1 = new Calculator(10, 20);
        c1.sum();
        c1.avg();
 
        Calculator c2 = new Calculator(20, 40);
        c2.sum();
        c2.avg();
    }
 
}
```java
    public Calculator(int left, int right) { 
        this.left = left;
        this.right = right; 
    }
```
위와 같은 내용이 추가되었는데, 이것이 바로 생성자. 이름처럼 객체를 생성할 때 호출됨.   
Caculator 라는 클래스에 **똑같은 이름의 Calculator 라는 메소드**가 선언됨. 이 메소드에는 파라미터가 left, right 값을 받게 되어있고, 전역변수의 값을 세팅하는 SetOprands 가 하는 역할을 Calculator 메소드가 하고 있는 상황. 이 메소드를 **생성자**Constructor라고 부른다. 생성자의 역할은 클래스가 생성될 때 자동으로 똑같은 이름을 가진 생성자가 실행되도록 약속되어 있음(가장 우선순위로). 그러니까 클래스와 같은 이름을 가진 메소드를 정의해서 거기에 로직을 채워넣게 되면 이건 제일 먼저 실행된다.-초기화 역할-. 
```jav
        Calculator c1 = new Calculator(10, 20);
        c1.sum();
```
부분에서 생성자를 이용해 객체를 생성. 생성자 덕분에 Calculator 객체 사용을 위해 사실상 left,right 값 설정 과정을 객체 생성 과정에서 강제할 수 있게됨. 사실 객체를 생성할 때 Calculator는 클래스가 아니라 클래스의 생성자라고 보는 게 맞다. 옆에 10,20이라는 인자까지 달려 있으니 더더욱.

## 생성자의 특징
* 개발자가 숙지하고 있어야 될 부분을 줄여줌   
알아서 먼저 실행되서 초기화 해주니까.
* 생성자 이름은 클래스 이름과 동일.   
약속입니다. 자바에서 클래스 이름과 동일한 메소드를 생성자로 쓰기로 약속했으니까.
* 값을 반환하지 않음   
**생성자는 인스턴스를 생성하는 특수한 메소드**. 그런데 반환 값이 있으면 이상한 객체가 생성될 것. 반환값 필요한 작업에선 생성자 만들지도 않음. 또한 반환값 없기 때문에 return도 안 쓰고, 메소드 정의에 포함되지도 않음.

