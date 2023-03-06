# Java Language Tutorials
- https://dev.java/learn/

## Classes and Objects
- Defining your own classes, declaring member variables, methods, and constructors.

### Creating Classes
```java
private class MyClass extends MySuperClass implements YourInterface {
    // field, constructor, and method declarations
}
```

**클래스 정의 요소**
1. 접근 제어자 - `public`, `private` (중첩 클래스에만 적용 가능하다)
2. 클래스 이름 (컨벤션에 의해 대문자로 시작해야 한다)
3. 부모 클래스의 이름 (최대 하나의 부모 클래스만 상속 가능하다)
4. 구현하는 인터페이스 리스트 (여러 개 구현 가능하다)
5. 클래스 바디 

**Controlling who has Access to a Member**
- 접근 제어자는 어떤 외부 클래스가 해당 클래스의 멤버 필드에 접근 가능한지 나타낸다
- ex. `public` (모든 클래스에서 접근 가능), `private` (해당 클래스 내부에서만 접근 가능)
- 캡슐화를 위해 필드를 `private` 로 선언하는 것이 일반적이다

**Naming Convention**
- 클래스 이름은 대문자로 시작해야 한다
- 메서드 이름은 동사로 시작해야 한

### Defining Methods
```java
public double calculateAnswer(double wingSpan, int numberOfEngines) {
    // do the calculation here
}
```

**메서드 정의 요소**
- **메서드 이름**과 **파라미터 타입**이 메서드 시그니처를 구성한다
1. 접근 제어자 - `public`, `private` 등
2. 반환 타입
3. 메서드 이름
4. 파라미터 리스트
5. 예외 리스트
6. 메서드 바디

**Overloading Methods**
- 자바는 메서드 오버로딩을 지원하며, 메서드 시그니처로 메서드를 구별한다
  - 따라서 동일한 클래스 내부에서도, **이름은 동일하지만 파라미터 타입이 다른 메서드의 선언**이 가능하다
- 반환값은 메서드 시그니처에 포함되지 않으므로, 반환 값만 다른 메서드의 선언은 불가능하다
```java
public class DataArtist {
    public void draw(String s) {
       // ...
    }
    public void draw(int i) {
        // ...
    }
}
```

### Providing Constructors for your Classes
- 생성자 (constructor) 는 클래스로부터 인스터스를 생성할 때 호출된다
- 반환 값이 없으며 클래스 이름과 동일한 이름을 사용하는 메서드와 같다
```java
// Bicycle 생성자
public Bicycle(int startCadence, int startSpeed) {
    cadence = startCadence;
    speed = startSpeed;
}

// Bicycle 생성자 호출
Bicycle = myBike = new Bicycle(30, 0);
```
- `new Bicycle(30, 0)` 코드는 객체 생성을 위한 메모리 공간을 할당받고, 필드 값을 초기화한다
- 자바는 매개변수의 수와 타입으로 생성자를 구분한다
- 생성자를 정의하지 않으면, 컴파일러에 의해 매개변수가 없는 기본 생성자가 생성된다
  - 기본 생성자는 부모 클래스의 기본 생성자를 호출한다
  - 상속받는 부모 클래스가 존재하지 않는다면, 암묵적으로 `Object` 를 부모 클래스로 갖는다
  - 부모 클래스에 기본 생성자가 존재하지 않으면 컴파일 에러가 발생한다

### Calling Methods and Constructors
**Arbitrary Number of Arguments**
- 메서드에 특정 타입의 데이터가 얼마나 들어오는지 모를 때, `varargs` 를 사용할 수 있다
- `varargs` 는 내부적으로 `array` 를 직접 생성하는 것과 동일하다
  - `array` 처럼 사용하면 된다
```java
public Polygon polygonFrom(Point ... corners) {
    double squareOfSide1 = corners[1].x - corners[0].x;    
}
```

**Passing Reference Data Type Arguments**
- 객체와 같은 참조 타입의 파라미터도 원시 타입과 같이 메서드에 값이 넘어간다
  - 메서드가 반환됐을 때, 참조 타입은 이전과 동일한 메모리 주소를 참조하고 있다
  - 그러나, 객체의 필드 값은 변할 수 있다
```java
public void moveCircle(Circle circle, int deltaX, deltaY) {
    // code to move origin of circle to x+deltaX, y+deltaY
    circle.setX(circle.getX() + deltaX);
    circle.setY(circle.getY() + deltaY);
    
    // code to assign a new reference to circle
    circle = new Circle(0, 0);       
}
```
- `moveCircle` 에 의해 변화된 `x` 와 `y` 필드 값은, 메서드가 종료되어도 지속된다
- `circle` 은 새로운 `Circle` 객체의 참조하게 되는데, 메서드가 종료하면 `circle` 변수는 동일한 객체를 가리키고 있다.
  - 이는 객체에 대한 참조가 값으로 넘어갔기 때문이다. 

### More on Classes

**Returning a Class for Interface**
- 메서드 정의 시 반환 타입에 클래스 명을 사용한다면, 반환되는 객체 타입은 반드시 반환 타입과 일치하거나 해당 타입의 자식 클래스이어야 한다
- 반환 타입이 인터페이스일 경우, 반횐되는 객체는 반드시 해당 인터페이스를 구현해야 한다
```java
public Number returnANumber() {
    // ...
}
```
- 다음의 메서드는 `ImaginaryNumber` 는 반환 가능하지만, `Object` 는 반환할 수 없다
  - 해당 메서드를 `ImaginaryNumber` 를 반환타입으로 갖도록 오버라이드 할 수 있다

**Using the this Keyword**
- 인스턴스 메서드와 생성자에서 사용된 `this` 는, 해당 객체를 가리킨다
- 주로 필드 값이 메서드나 생성자 변수에 의해 가려질 경우, `this` 키워드를 사용한다
```java
public class Point {
    public int x = 0;
    public int y = 0;
    
    // constructor
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```
- 생성자 내부에서 다른 생성자를 호출 시에 `this` 키워드를 사용할 수 있다
```java
public class Rectangle {
    private int x, y;
    
    public Rectangle() {
        this(0, 0);
    }
    
    public Rectable(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

**Controlling Access to Members of a Class**
- 접근 지정자 (access level modifiers) 는 다른 클래스가 해당 클래스 내부 필드에 접근하거나, 메서드를 호출할 수 있는지 결정한다
- 클래스 - `public`, `default`
- 필드 - `public`, `private`, `protected`, `default`
- 최대한 한정적인 접근 지정자를 사용하는 것이 에러나 오사용을 예방할 수 있다
  - 특별한 이유가 없으면 `private` 사용을 권장한다

**Understanding Class Members**
- `static` 키워드를 사용하여 생성된 클래스 변수는, 모든 클래스 인스턴스는 **클래스 변수를 공유한다**
  - 객체가 아닌 클래스와 연관된 변수이다 
  - 클래스 변수는 고정된 메모리 공간에 존재한다
- 어떠한 인스턴스도 클래스 변수를 조작할 수 있으며, 인스턴스 생성 없이도 값을 변화시킬 수 있다
```java
public class Bicycle {
    // add an instance variable for the object ID
    private int id;
    
    // add a class variable for the number of Bicycle objects instantiated
    private static int numberOfBicycles = 0;
}

Bicycle.numberOfBicycles
```

- 클래스 변수뿐만 아니라, `static` 으로 선언된 클래스 메서드도 존재할 수 있다
  - 마찬가지로, 인스턴스 생성 없이 사용 가능하다
  - 일반적으로, static 필드 접근을 위해 사용된다
- 클래스 메서드는 인스턴스 변수나 메서드에 접근할 수 없다
- 클래스 메서드는 `this` 키워드를 사용할 수 없다 (가라킬 인스턴스가 없기 때문)

- `static` 과 `final` 을 조합하여 상수 선언이 가능하다
```java
static final double PI = 3.12159;
```
- `final` 로 선언되었으므로, 재할당이 불가능하다
  - `final` 이 메서드에 사용되면, 오버라이딩이 불가능하다

**Initializing Fields**
- 정적 할당 블록을 통해 정적 필드에 값을 할당할 수 있다

### Nested Classes
- 자바에서는 클래스 내부에 다른 클래스를 정의할 수 있다 (nested class)
```java
class OuterClass {
    class InnerClass {
    }
    
    static class StaticNestedClass {
    }
}
```
- 중첩 클래스는 외부 클래스의 멤버이다
  - 멤버 이므로, `private`, `public`, `protected`, `default` 레벨의 접근 제어가 선언이 가능하다
- 중첩 클래스에는 `non-static` 한 이너 클래스와 `static` 한 클래스가 존재한다
  - 이너 클래스는 `private` 하게 선언되더라도, 외부 클래스에 존재하는 모든 멤버들에서 접근가능하다
  - `static` 중첩 클래스는 외부 클래스의 멤버들에서 접근이 불가능하다

**Why Use Nested Classes?**
1. 한 곳에서만 사용되는 클래스를 논리적으로 그룹핑할 수 있다
- 생성될 클래스가 특정 클래스에서만 사용된다면, 해당 클래스 내부에 클래스를 생성하여 두 가지를 묶어서 관리하는 것이 유용할 것이다
2. 캡슐화가 가능하다
- 클래스 A 의 모든 멤버들이 클래스 B 에 의해서만 사용된다면, 클래스 A 에 B 를 생성하면 A 의 모든 멤버들은 `private` 레벨로 선언 가능하다
- 또한 클래스 B 를 외부 접근으로부터 숨길 수 있다
3. 가독성이 좋아지고 유지보수가 간편해진다

**이너 클래스**
- 인스턴스 메서드와 변수처럼 이너 클래스도 클래스 인스턴스와 연관되며, 인스턴스 메서드와 필드에 접근 가능하다
  - 인스턴스와 연관되어 있으므로, 정적 멤버의 선언이 불가능하다
```java
class OuterClass {
    class InnerClass {
    }
}

OuterClass outerObj = new OuterClass();
OuterClass.InnerClass  innerObj = outerObj.new InnerClass();
```
- `InnterClass` 의 인스턴스는 `OuterClass` 인스턴스 내부에서만 존재 가능하며, `OuterClass` 의 메서드와 필드에 접근 가능하다
  - 이너 클래스의 인스턴스를 생성하기 이전에 반드시 외부 클래스의 인스턴스를 생성해야 한다
- 이너 클래스는 로컬 클래스와 익명 클래스가 존재한다

**Static Nested Classes**
- 클래스 메서드와 필드처럼, 정적 중첩 클래스도 외부 클래스와 연관된다
- 정적 클래스 메서드처럼, 정적 중첩 클래스는 외부 클래스에 정의된 인스턴스 변수나 메서드에 직접 접근할 수 없다
  - 객체 참조를 통해 접근 가능하다
```java
// OuterClass.java

public class OuterClass {
    String outerField = "Outer field";
    static String staticOuterField = "Stitac Outer field";
    
    class InnerClass {
        void accessMembers() {
          System.out.println(outerField);
          System.out.println(staticOuterField);
        }
    }
    
    static class StaticNestedClass {
        void accessMembers(OuterClass outer) {
            // Compiler error: Cannot make a static reference to the non-static field outerField
            //System.out.println(outer.outerField);
            System.out.println(outer.outerField);
            System.out.println(staticOuterField);
        }
    }
}
```

**Inner Class Example**
```java
public class DataStructure {
    // Create an array
  private final static int SIZE = 15;
  private int[] arrayOfInts = new int[SIZE];
  
  public DataStructure() {
      // fill the array with ascending integer values
    for (int i=0; i<SIZE; i++) {
        arrayOfInts[i] = i;
    }
  }
  
  public void printEven() {
      // Print out values of even indices of the array
    DataStructureIterator iterator = this.new EvemIterator();
    while (iterator.hasNext()) {
      System.out.println(iterator.next() + " ");
    }
    System.out.println();
  }
  
  interface DataStructureIterator extends java.util.Iterator<Integer> { }
  
  // Inner class implements the DataStructureIterator interface,
  // which extends the Iterator<Integer> interface
  private class EvenInteger implements DataStructureIterator {
      public Integer next() {
          // Record a value of an even index of array
        Integer retValue = Integer.valueOf(arrayOfInts[nextIndex]);
        
        // Get the next even element
        nextIndex += 2;
        return retValue;
      }
  }
}
```
- `EvenIterator` 클래스는 `DataStructure` 객체의 멤버 변수인 `arrayOfInts`를 직접적으로 참조하고 있다
- 이너 클래스에는 로컬 클래스와 익명 클래스가 존재하는데, 메소드 이름 없이 바디만 정의하면 익명 클래스로 선언된다

**Local Classes**
- 블락 안에 선언된 클래스를 로컬 클래스라고 지칭한다
  - 메서드 바디, 반복문, if 문 내부에 로컬 클래스를 정의할 수 있다
- 이너 클래스에서 접근하는 지역 변수는 `final` 이거나 선언 후 값이 변경되지 않아야 한다
- Java SE 8 부터 메서드 내부에 선언된 로컬 클래스는 메서드 파라미터에 접근 가능하다
- 로컬 클래스는 정적 멤버의 선언이 불가능하다는 점에서 이너 클래스와 유사하다
  - 로컬 클래스는 외부 블록의 인스턴스 멤버에 접근하므로 `non-static` 이다
- 인터페이스는 블락 내부에 선언이 불가능하다
  - 인터페이스는 `static` 하다
```java
// Compile Error !
public void greetInEnglish() {
    interface HelloThere {
        public void greet();
    }
    class EnglishHelloThere implements HelloThere {
        public void greet() {
        }
    }
}
```
- `static final` 변수는 선언 가능하다

**Anonymous Classes**
- 익명 클래스는 코드를 더 간결하게 만들어준다
  - 클래스의 선언와 인스턴스 생성이 동시에 가능해진다
- 이름이 없다는 점을 제외하면 로컬 클래스와 동일하다
  - 로컬 클래스가 단 한 번만 필요하다면, 익명 클래스를 사용하라
  - 로컬 클래스는 클래스 선언인데 반해, 익명 클래스는 표현식이므로 다른 표현식에서 정의 가능하다
```java
public class HelloWorldAnonymousClasses {
    interface HelloWorld {
        public void greet();
        public void greetSomeone(String someone);
    }
    
    public void sayHello() {
        class EnglishGreeting implements HelloWorld {
            
        }
        
        HelloWorld englishGreeting = new EnglishGreeting();
        HelloWorld frenchGreeting = new HelloWorld() {
            public void greet() {}
            public void greetSome(String someone) {}
        };
    }
}
```
- 익명 클래스는 외부 클래 멤버에 접근 가능하다
- 익명 클래스는 `final` 이거나 잠재적으로 `final` 인 지역 변수에만 접근 가능하다
- 정적 초기화 블록이나 인터페이스 멤버의 선언이 불가능하다
- 상수인 정적 멤버를 선언할 수 있다

