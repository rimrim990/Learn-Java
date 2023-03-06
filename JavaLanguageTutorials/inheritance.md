# Java Language Tutorials
- https://dev.java/learn/

## Inheritance
- Leveraging inheritance in Java applications
- oop 는 공통적으로 사용되는 상태와 동작을 다른 클래스로부터 상속받을 수 있도록 허용한

### Inheritance
- `Object` 를 제외한 모든 클래스는 하나의 부모 클래스를 갖고 있다
- 명시된 부모 클래스가 없는 모든 클래스들은, 암묵적으로 `Object` 클래스를 상속 받는다
  - 모든 클래스의 최고 조상 클래스는 `Object` 이다
- 상속을 통해 기존 클래스에 존재하는 필드와 메서드 들을 재활용 할 수 있다
  - 새로 작성하거나 디버깅 할 필요가 없다 !
- 자식 클래스는 부모 클래스의 모든 멤버 (필드, 메서드, 중첩 클래스) 들을 상속 받는다
  - 생성자는 멤버가 아니므로 상속받지 않지만, 부모 클래스의 생성자는 자식 클래스의 생성자에서 호출될 수 있다

**What You Can Do in a Subclass**
- 자식 클래스는 부모의 모든 `public` 과 `protected` 레벨의 멤버를 상속받는다
  - 자식 클래스와 부모 클래스와 동일한 패키지에 존재하는지 여부와 관계없이, 모든 패키지 프라이빗한 멤버들을 상속받는다
  - 상속받은 멤버를 그대로 사용하거나, 대체하거나, 숨기거나 새로운 멤버에 제공할 수 있다

**Private Members in a Superclass**
- 자식 클래스는 부모 클래스의 `private` 멤버는 상속받지 않는다
- 그러나 `private` 필드에 접근하는 `public` 혹은 `protected` 레벨의 메서드가 존재하는 이를 사용할 수 있다
- 중첩 클래스 또한 모든 `private` 멤버에 접근할 수 있다

**Casting Objects**
```java
Object obj = new MountainBike();
MountainBike myBike = (MountainBike) obj;
```
- 암묵적인 타입 캐스팅이 발생하여 컴파일 에러가 발생하지 않는다

**Multiple Inheritance of State, Implementation, and Type**
- 클래스는 필드를 갖을 수 있지만, 인터페이스는 불가능하다
- 클래스는 인스턴스를 생성할 수 있지만, 인터페이스는 불가능하다
- 자바에서 클래스의 다중 상속을 지원하지 않는 이유 중 하나는, 동일한 상태에 대해 여러 번 상속받는 상황을 방지하지 위해서다
  - 인터페이스는 필드가 없으므로 다중 상속이 가능하다 

**Overriding and Hiding Methods**
- 자식 클래스 인스턴스에 부모 클래스와 동일한 시그니처와 반환 타입을 갖는 메서드를 재정의 할 수 있다 (오버라이딩)
- `@Override` 어노테이션을 사용하여 컴파일러에 의한 검증이 가능하다

**Static Methods**
- 자식 클래스에서 부모 클래스에 존재하는 정적 메서드와 동일한 시그니처를 갖는 정적 메서드를 정의하면, 부모 클래스의 메서드는 가려진다
```java
public class Cat extends Animal {
    public static void testClassMethod() {
    }
    
    public void testInstanceMethod() {
    }

    public static void main(String[] args) {
        Cat myCat = new Cat();
        Animal myAnimal = myCat;
        // Animal
        Animal.testClassMethod();
        // Cat
        myAnimal.testInstanceMethod();
    }
}
```
- `Cat` 클래스는 `Animal` 의 인스턴스 메서드를 오버라이드하고, 정적 메서드를 가리고 있다
- 오버라이딩된 인스턴스 메서드는 호출 시 자식 클래스의 메서드를 호출한다
- 가려진 정적 메서드는 어느 클래스에서 호출되는지에 따라 실행되는 메서드가 다르가

### Methods From the Object Class
**The equals() Method**
- `equals()` 메서드는 두 객체의 동등성을 비교한다
- `Object` 클래스에 정의된 `equals` 메서드는 `==` 연산자로 두 객체의 동등성을 비교한다
  - 원시 타입에서는 정상적으로 동작한다
  - 그러나 객체 타입에서는, 객체의 참조가 동일한지 검사한다. 즉, 완전히 동일한 객체인지 비교하게 된다

**The hashCode() Method**
- `hashCode()` 는 객체의 해시 코드를 반환한다
  - 해시 코드는 해싱 알고리즘에 의해 생성된 정수 값이다
- 정의에 의해, 두 객체가 동일하면 해시 코드도 동일해야 한다
  - 따라서 `equals()` 메서드를 오버라이딩한다면, `hashCode` 도 오버라이딩해야 한다

**The finalize()**
- 객체가 더이상 사용되지 않을 때 `finalize()` 메서드를 호출할 수 있다
- `finalize()` 메서드는 시스템에서 자동으로 호출되지만, 언제 호출되는지는 알 수 없다
  - 따라서 클린업을 위해 `finalize()` 를 사용하는 것은 적절하지 않다

### Abstract Methods and Classes
- 추상 클래스는 `abstract` 키워드와 함께 선언된 클래스이다
  - 추상 메서드를 포함할 수 있다
  - 추상 메서드는 선언만 있고 구현이 없는 메서드이다 
  - 인스턴스를 생성할 수 없지만, 상속될 수 있다
  - 자식 클래스에서는 반드시 추상 메서드를 구현해야 한다

**Abstract Classes Compared to Interfaces**
- 추상 클래스와 인터페이스는 유사하다
  - 인스턴스를 생성할 수 없다
  - 추상 메서드를 포함할 수 있다
- 그러나 추상 클래스에서는 `static` 이나 `final` 이 아닌 필드를 선언할 수 있으며, `public`, `protected`, `private` 메서드를 정의할 수 있다
- 인터페이스에서는 모든 필드가 기본적으로 `public`, `static`, `final` 이며, 모든 메서드가 `public` 이다
- 추상 클래스는 클래스이므로 하나만 상속받을 수 있지만, 인터페이스는 제한 없이 상속받을 수 있다