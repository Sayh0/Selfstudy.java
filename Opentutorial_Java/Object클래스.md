# Object 클래스
모든 클래스의 조상은 Object 클래스에 대해.<br>

## 상속
자바에서 상속은 필수적이다. 우리가 상속을 쓰던 안 쓰던 기본적인 상속은 하고 있다.
```
package org.opentutorials.javatutorials.progenitor;

class O {
...
}
```
```
package org.opentutorials.javatutorials.progenitor;

class O extends Object {
...
}
```
위 두 코드는 같은 코드이다. 자바에서 모든 클래스는 사실 **Object**를 암시적으로 상속받고 있다. 사실상 모든 클래스의 조상 격인 셈이다.<br>
이유는 모든 클래스가 공통으로 포함하고 있어야 하는 기능을 제공하기 위해서인데, 그게 뭔지 API 문서를 보면 다음과 같다.<br>
메소드 목록을 살펴보자.



