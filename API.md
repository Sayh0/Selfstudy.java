# API와 API 문서
## 기본 패키지와 사용자 정의 로직
```java
System.out.println(1);
```
여태 써오던 이건 대체 어떻게 동작하는 것일까? 문법적으로 살펴보면, println은 메소이다. 
메소드 앞의 System.out은 뭘까? System은 클래스이고, out은 그 클래스의 필드(변수)이다.
이 필드가 메소드를 가지고 있는 것은 이것 역시 객체라는 것을 알 수 있다. 
그리고 System을 인스턴스화 한적이 없음에도 불구하고, out에 접근할 수 있는건 out이 static하기 때문이라는 것도 예상할 수 있다.<br>
그럼  이 System이란 클래스가 어디서 왔는 지 알아보자.
```java
public class LibraryDemo1 {
    public static void main(String[] args) {
        System.out.println(1);
    }

```
이 코드는 아래 나올 코드와 같다.
```java
import java.lang.*; // 추가된 부분.
public class LibraryDemo1 {
    public static void main(String[] args) {
        System.out.println(1);
    }
```
`import java.lang.*`에서 패키지 java.lang은 자바 프로그래밍을 하기 위한 필수적 클래스들을 모아 둔 패키지이다.
따라서 사용자 편의를 위해 자동으로 로딩을 하고 있는 것이다. 클래스 System은 바로 이 java.lang의 소속이다.
결국 자바 애플리케이션을 만드는 것은 자바에서 제공하는 패키지들을 부품으로 조립하여 사용자 정의 로직을 만드는 과정이라고 할 수 있다.

## API
**API**란 자바 시스템을 제어하기 위해서 자바에서 제공하는 명령어들을 의미한다. Java SE(JDK)를 설치하면 자바 시스템을 제어하기 위한 API를 제공한다.
자바 개발자들은 자바에서 제공한 API를 이용해서 자바 애플리케이션을 만들게 된다. 패키지 `java.lang.*`의 클래스들도 자바에서 제공하는 API 중의 하나라고 할 수 있다.
