# Java Language Tutorials
- https://dev.java/learn/

## Java Language Basics
- Getting to know the basics of the Java language.

### Creating Variables and Naming Them
- Rules to name variables.

**Variables**
1. 인스턴스 변수 (Non-Static Fields)
- 객체는 자신의 상태를 **"non-static fields"** 에 저장한다
  - 즉, 필드 정의 시에 `static` 키워드를 사용하지 않는다  
- non-static 필드는 인스턴스 변수라고도 불린다
  - 각 필드 값이 **각 클래스 인스턴스 (객체) 에 유니크하게 존재**한다

2. 클래스 변수 (Static Fields)
- 클래스 변수는 `static` 과 함께 정의된 필드를 의미한다
  - 클래스가 얼마나 많은 인스턴스를 보유하기 있는지와 관계없이, 항상 하나의 정적 (static) 변수만 존재한다
  - 만약 정적 변수의 값이 바뀔 일이 없다면, `final` 키워드를 함께 사용할 수 있다

3. 지역 변수 
- 객체의 상태를 필드에 저장하는 것처럼, **메서드의 일시적인 상태를 지역 변수에 저장**할 수 있다
- 정적 변수와 달리, 지역 변수를 생성하는 것은 키워드가 아니라 변수의 선언 위치이다
  - 메서드 내부에 존재하는지 여부에 의해 결정된다
  - 메서드 내부에서만 사용 가능하며, 메서드 밖에서는 접근 불가능하다

4. 파라미터
- 파라미터는 항상 "필드" 가 아닌 "변수" 로 분류된다

**Naming Variables**
- 변수 이름은 case-sensitive 하다
- 축약어를 사용하는 것은 코드를 이해하기 어렵게 만드므로, 지양한다
- 카멜 케이스를 사용하라

### Creating Primitive Type Variables in Your Programs
- 자바는 정적 타입 언어이므로, 변수가 사용되기 전에 변수의 이름과 타입이 선언되어야 한다.
- 변수 타입은, 해당 변수가 어떤 값을 갖고 있으며 어떤 연산을 수행할지 결정한다
- 지역 변수는 필드 값과 다르게, 컴파일러로부터 기본 값 (default value) 를 할당받지 않는다

**Primitive Types**
- 클래스로부터 생성된 객체가 아니므로, `new` 키워드 없이 변수 초기화가 가능하#
1. `byte` - 8-bit signed integer
2. `short` - 16-bit signed integer
3. `int` - 32-bit signed integer (default)
4. `long` - 64-bit singed integer
5. `float` - 32-bit floating point, 정확한 값이 필요할 때는 사용하면 안된다 (`BigDeciamal` 사용 권장)
6. `double` - 64-bit floating point (default), 정확한 값이 필요할 때는 사용하면 안된다 (`BigDecimal` 사용 권장)
7. `boolean` - `true` 혹은 `false` 의 ` bit 정보
8. `char` - 16-bit 유니코드 캐릭터

### Creating Arrays in Your Programs
- `array` 는 **지정된 길이와 타입의 변수들을 저장**하고 있는 컨테이너 객체이다
  - array 의 길이는 생성 당시에 지정된다
  - 한 번 생성되면, 길이는 고정되어 있다
  - `java.util.Arrays` 클래스는 `array` 조작을 위한 메서드들을 제공한다
```java
class ArrayDemo {
  public static void main(String[] args) {
    // declares an array of integers
    int[] anArray;
    
    // allocated memory for 10 integers
    anArray = new int[10];
    
    // initialize first element
    anArray[0] = 100;
  }
}
```

**Declaring a Variable to Refer to an Array**
```java
// declares an array of integers
int[] anArray;
```
- `array` 선언 시에는 타입과 이름을 포함해야 햔다
- 변수 선언이 `array` 를 생성하지는 않는다

**Creating, Initializing, and Accessing an Array**
```java
// create an array of integers
anArray = new int[10];
```
- `new` 연산자로 `array` 를 생성할 수 있다
```java
int[] anArray = {
        100, 200, 300
};
```
- 다음과 같이, 한 번에 선언과 초기화가 가능하다
```java
String[][] names = {
        {"Mr. ", "Mrs. ", "Ms. "},
        {"Smith", "Jones"}
};
```
- 자바에서 다차원 배열은 element 로 배열을 갖는, 배열이므로 각 row 들은 서로 다른 길이의 배열을 갖을 수 있다

### Branching with Switch Expressions
- Java SE 14 에서는, `switch` 표현식의 사용이 가능하다
- `switch` 블록을 하나의 블록으로 간주하므로, 해당 `case` 에서만 유효한 변수의 선언이 가능하다
```java
String quarterLabel =
    switch (quarter) {
        case 0 -> {
            System.out.println("Q1 - Winter");
            yield "Q1 - Winter"
        };
        default -> "Unknown quarter";
    }
```
