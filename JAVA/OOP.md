https://www.baeldung.com/java-oop,
https://www.geeksforgeeks.org/object-oriented-programming-oops-concept-in-java,
https://gmlwjd9405.github.io/2018/07/05/oop-features.html
# 자바에서의 객체-지향 프로그래밍 개념은 클래스(classes), 객체(objects), 추상화(abstraction), 캡슐화(encapsulation), 상속(inheritance), 다형성(polymorphism)이 있다.

## 클래스(Classes)
클래스는 객체 생성을 위한 템플릿(설계도, 청사진)입니다. 하나의 클래스는 일반적으로 멤버 필드(variable, property), 멤버 메서드, 생성자 메서드를 포함합니다.

클래스에서 객체를 생성하기 위해 생성자를 사용합니다. 생성자는 한개 이상이 될 수 있습니다.

추가 설명 : https://www.baeldung.com/java-classes-objects#classes

## 객체(Objects)
객체는 클래스로부터 생성되고 클래스의 인스턴스라 부릅니다. 또한 생성자를 사용하여 객체를 생성합니다.

## 추상화(Abstraction)
추상화는 구현의 복잡성을 숨기고 더 단순한 인터페이스를 노출하는 것입니다.

우리가 사용하는 일반적인 컴퓨터를 생각하면, 컴퓨터와 상호작용하는데 가장 필수적인 외부 인터페이스(USB, HDMI, 무선랜, 블루투스 등)만 볼 수 있고,
그것을 구성하는 내부 칩과 회로는 숨겨져 있습니다.

객체 지향 프로그래밍(OOP)에서 추상화는 프로그램의 복잡한 구현 세부 사항을 숨기고 구현을 사용하는 데 필요한 API만 노출시키는 것을 의미합니다.
자바에서는 인터페이스와 추상 클래스를 사용하여 추상화를 달성합니다.

컴퓨터 과학에서의 추상화랑 OOP에서의 추상화의 차이점
API란 : https://yozm.wishket.com/magazine/detail/727/
추가 설명 : https://www.baeldung.com/java-interfaces, https://www.baeldung.com/java-abstract-class, https://www.baeldung.com/java-interface-vs-abstract-class

* 추상화에서 인터페이스, 추상 클래스 의미가 나옴

# 캡슐화(Encapsulation)
캡슐화는 API의 소비자로부터 객체의 상태나 내부 표현을 숨기고 읽기/쓰기 액세스를 위해 객체에 바인딩된 공개적으로 접근 가능한 메서드를 제공하는 것입니다.
이를 통해 특정 정보를 숨기고 내부 구현에 대한 액세스를 제어할 수 있습니다.

예를 들어, 클래스의 멤버 필드는 다른 클래스로부터 숨겨져 있으며, 멤버 메서드를 사용하여 접근할 수 있습니다.
이를 위한 한 가지 방법은 공용(public) 멤버 메서드를 사용하여 모든 데이터 필드를 비공개(private)로 설정하고 접근할 수 있도록 하는 것입니다.
이런 접근을 제한하게 하는 기능을 접근 제어자라 합니다.

추가 설명 : https://www.baeldung.com/java-access-modifiers
* 캡슐화에서 접근 제어자, setter/getter 의미가 나옴

# 상속(Inheritance)
상속은 한 클래스가 클래스를 상속함으로써 상속 받은 클래스가 상속한 클래스로부터 모든 속성을 획득할 수 있도록 하는 메커니즘입니다.
상속받은 클래스를 자식(child) 클래스, 서브(sub) 클래스 상속한 클래스를 부모(parent) 클래스, 슈퍼(super) 클래스라 부릅니다.

자바에서는 상위 클래스를 확장하여 이 작업을 수행합니다. 따라서 하위 클래스는 상위 클래스로부터 다음과 같은 모든 속성을 가져옵니다.
```java
public class Car extends Vehicle { 
    //...
}
```
Car 클래스가 Vehicle 클래스를 extend 할 때, IS-A 관계를 형성합니다. "자동차는 차량이다"(The Car IS-A Vehicle).
따라서 Car는 Vehicle의 모든 특성을 갖고 있습니다.

왜 상속이 필요한지 질문 할 수 있습니다. 이에 답하기 위해 자동차, 버스, 트램, 트럭 등 다양한 종류의 차량을 제조하는 차량 제조업체를 생각해봅시다.
작업을 쉽게 하기 위해 모든 차량 유형의 공통 기능과 속성을 모듈(자바의 경우 클래스)로 번들(묶음)할 수 있습니다.
또한 개별 유형이 다음과 같은 속성을 상속하고 재사용하도록 할 수 있습니다.
```java
public class Vehicle {
    private int wheels;
    private String model;
    public void start() {
        // 차량 시동을 겁니다.
    }
    
    public void stop() {
        // 차량 시동을 끕니다.
    }
    
    public void honk() { 
        // 경적을 울립니다. (produces a default honk)
    }

}
```
Vehicle 타입 Car는 부모 클래스(Vehicle 클래스)로부터 상속 받았습니다.
```java
public class Car extends Vehicle {
    private int numberOfGears; // 기어의 개수

    public void openDoors() {
        // 문을 엽니다.
    }
}
```
자바는 단일 상속 및 다단계 상속을 지원합니다. 즉. 클래스는 두 개 이상의 클래에서 직접 확장할 수 없지만 계층을 사용할 수 있습니다.
```java
public class ArmoredCar extends Car {
    private boolean bulletProofWindows; // 방탄창문 유무
    
    public void remoteStartCar() {
        // 원격 제어로 시동을 걸 수 있습니다.
    }
}
```
여기서, ArmoredCar는 Car를  확장(extend)하고 Car는 Vehicle을 확장(extend)합니다. 따라서 ArmoredCar는 Car와 Vehicle로 부터 모든 특성을 물려받습니다.

하위 클래스가 상위 클래스에서 상속받는 동안 상위 클래스의 메서드 구현을 재정의할 수도 있습니다. 이를 메서드 재정의(Overriding)라고 합니다.

위의 Vehicle 클래스 예제에는 honk() 메서드가 있습니다. Vehicle 클래스를 확장(extend)하는 Car 클래스는 이 메서드를 재정의하고 honk() 메서드를 원하는 방식으로 구현할 수 있습니다.
```java
public class Car extends Vehicle {  
    //...

    @Override
    public void honk() { 
        // 특유의 차 경적을 울립니다. (produces car-specific honk)
    }
 }
```
다음 장에서 설명하는 것처럼 이것을 런타임 다형성(runtime polymorphism)이라고도 합니다.

추가 설명 : https://www.baeldung.com/java-inheritance, https://www.baeldung.com/java-inheritance-composition

## 다형성(Polymorphism)
다형성은 입력 유형에 따라 데이터를 다르게 처리하는 OOP 언어의 능력입니다.
자바에서 다형성은 서로 다른 메서드 특징을 가지고 다른 기능을 수행하는 메서드가 동일한 이름을 가지게 할 수 있습니다.
```java
public class TextFile extends GenericFile {
    //...
 
    public String read() {
        return this.getContent()
          .toString();
    }
 
    public String read(int limit) {
        return this.getContent()
          .toString()
          .substring(0, limit);
    }
 
    public String read(int start, int stop) {
        return this.getContent()
          .toString()
          .substring(start, stop);
    }
}
```
이 예제에서, 메서드 read() 가 각자 다른 기능을 가진 세 가지 다른 형태를 가지고 있음을 알 수 있습니다.
이러한 유형의 다형성은 정적 또는 컴파일 시간 다형성이며 메서드 오버로드(overloading)라 부릅니다.

런타임 또는 동적 다형성도 있으며, 자식 클래스가 부모 메서드를 재정의합니다. 즉 오버라이드(overriding)라 부릅니다.
```java
public class GenericFile {
    private String name;
 
    //...
 
    public String getFileInfo() {
        return "Generic File Impl";
    }
}
```
하위 클래스는 GenericFile 클래스를 확장하고 getFileInfo() 메서드를 재정의할 수 있습니다.
```java
public class ImageFile extends GenericFile {
    private int height;
    private int width;
 
    //... getters and setters
     
    public String getFileInfo() {
        return "Image File Impl";
    }
}
```

## 결론
자바를 사용한 OOP의 기본적인 개념에 대해 배워봤습니다.
