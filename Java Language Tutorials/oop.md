# Java Language Tutorials
- https://dev.java/learn/

## Objects, Classes, Interfaces, Packages, and Inheritance
- Introducing the object oriented programming.

### What is an Object ?
- 객체 (object) 는 연관된 상태와 동작을 갖는 소프트웨어 집합이다

**객체의 공통된 특징**
1. 상태
- ex. 강아지는 이름, 색깔, 품종 등의 상태를 갖는다
2. 동작
- ex. 강아지는 짖기, 꼬리 흔들기 등의 동작을 수행한다

**객체의 구성 요소**
1. 필드 (변수)
- 객체의 상태 
2. 메서드 (함수)
- 객체의 동작 
- 메서드는 객체의 내부 필드 값에 대해 동작한다
- oop 의 기본 규칙인 데이터 캡슐화를 구현하기 위해서는, 객체 내부 상태는 노출시키지 않고 모든 상호작용이 메서드를 통해서만 이루어져야 한다

**객체 생성의 이점**
- modularity: 서로 다른 객체의 코드가 독립적으로 유지 가능
- information-hiding: 객체 메소드를 통해서만 상호작용이 가능하므로, 내부 구현은 숨길 수 있다
- code re-use
- pluggability and debugging ease: 하나의 객체에 문제가 발생하면, 전체 코드가 아닌 해당 객체만 대체하면 된다

### What is Class ?
- 클래스는 객체 (object) 를 생성하기 위한 blueprint 이다
```java
class Bicycle {
    // 객체 상태 (object's state)
    int speed = 0;
    int gear = 1;
    
    // 객체 동작 (objects' method) -> 외부와의 상호작용 정의
    void changeGear(int newValue) {
        gear = newValue;
    }
    
    void speedUp(int increment) {
        speed = speed + increment;
    }
}
```
- 예시에 정의된 `Bicycle` 클래스는 `main` 메서드를 포함하고 있지 않는다
  - 어플리케이션 내부에서 사용하기 위한 용도로 정의되었기 때문이다
  - 어플리케이션 내부의 다른 클래스에서 `Bicycle` 클래스의 인스턴스를 생성하여 사용할 것이다
```java
class BicycleDemo {
  public static void main(String[] args) {
    // Create two different Bicycle objects
    Bicycle bike1 = new Bicycle();
    Bicycle bike2 = new Bicycle();
    
    // Invoke methods on those objects
    bike1.speedUp(10);
    bike2.changeGear(2);
  }
}
```

### What is Inheritance ?
- 서로 다른 객체라 하더라도, 일정 부분의 공통점을 갖고 있는 경우가 있다
- ex. 산악 자전거와 일반 자전거는 모드 자전거의 특성을 보유하고 있다 (속도, 기어 등)
- 객체 지향 프로그래밍에서는 공통적으로 사용되는 상태와 동작을 다른 클래스로부터 `상속 (inherit)` 받을 수 있다
- ex. `Bicycle` 클래스를 상속받아 `MountainBike` 와 `RoadBike` 클래스를 생성한다
- 자바에서는 **하나의 클래스만 (direct superclass) 상속받을 수 있으며**, 부모 클래스는 무한한 자식 클래스를 생성할 수 있다
```java
class MountainBike extends Bicycle {
    // new fields and methods defining a mountain bike would go here
}
```
- `MountainBike` 는 `Bicycle` 의 모든 필드와 메서드를 보유하게 되며, 추가적으로 `MountainBike` 고유의 특성도 가질 수 있다

### What is Interface ?
- 객체 (object) 는 메서드를 통해 외부와의 상호작용을 정의한다
- 즉, 메서드는 외부 세계에 대한 오브젝트의 인터페이스를 형성한다
- ex. 리모컨 버튼
- 일반적으로, 인터페이스는 연관된 메서드의 (with empty bodies) 그룹이다
```java
interface Bicycle {
    void changeGear(int newValue);
    
    void speedUp(int increment);
}
```
- 인터페이스를 구현하기 위해서는, `implements` 키워드를 사용하여 새로운 클래스를 정의해야 한다
```java
class ACMEBicycle implements Bicycle {
    int speed = 0;
    int gear = 1;
    
    // The compiler will now require that methods changeGear and speedUp all be implemented.
    // Compiler will fail if those methods are missing from this class.
    void changeGear(int newValue) {
        gear = newValue;
    }
    
    void speedUp(int increment) {
        speed = speed + increment;
    }
}
```
- 인터페이스는 클래스와 외부 세계 사이의 `계약` 과 같다
  - 인터페이스에 기재된 기능은 반드시 제공될 것이다 
  - 이는 빌드 시에 컴파일러가 구현 여부를 체크한다 
- `ACMEBicycle` 이 컴파일되기 위해서는 구현된 메서드가 `public` 이어야 한다

### What is a Package ?
- 패키지는 연관된 클래스와 인터페이스의 집합을 생성하는 **네임스페이스**이다
- 개념적으로는 컴퓨터 내에 존재하는 서로 다른 폴더와 유사하다
- 자바에서는 수백, 수천 개의 서로 다른 클래스가 존재하므로, 연관된 클래스들을 패키지로 묶어 관리하는 것이 합리적이다