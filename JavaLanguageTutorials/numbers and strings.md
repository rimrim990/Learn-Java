# Java Language Tutorials
- https://dev.java/learn/

## Numbers and Strings
- Understanding numbers, characters and strings of characters.

### Numbers
- java.lang 패키지, `Number` 클래스
- 자바에는 원시 타입에 대한 `wrapper` 클래스가 존재하는데, 숫자와 관련된 `wrapper` 클래스는 추상 클래스인 `Number` 의 자식 클래스들이다
- `xxxValue()` 메서드는 `Number` 객체의 값을 원시 타입으로 변환하여 변환한다
- `compareTo()` 메서드는 `Number` 객체를 매개변수 값과 비교한다

### Characters
- 하나의 문자 값을 저장할 때는 원시 타입 중 하나인 `char` 타입을 사용할 수 있다
```java
char ch = 'a';
// Unicode for uppercase Greek omega character
char uniChar = '\u03A9';
// an array of chars
char[] charArray = { 'a', 'b', 'c', 'd', 'e'};
```
- 원시 타입인 `char` 의 wrapper 클래스인 `Character` 가 존재한다
  - `Character` 인스턴스는 불변 객체이므로, 한 번 생성되면 값을 변경할 수 없다
```java
Character ch = new Character('a');
```
- 자바 컴파일러는 원시 타입 `char` 와 `Character` 클래스 간에 `autoboxing` 과 `unboxing` 을 지원한다

### Strings
- 문자들의 시퀀스를 문자열이라고 한다
- 자바에서 문자열은 객체이다
```java
String greeting = "Hello world!";
```
- "Hello world" 는 문자열 리터럴이다
  - 코드 상에 문자열 리터럴이 등장하면, 컴파일러는 해당 리터럴을 값으로 하는 `String` 객체를 생성한다
  - `String` 인스턴스는 불변 객체이므로, 한 번 생성되면 값을 변경할 수 없다
  - `String` 은 불변 객체이므로, `String` 을 조작하는 메서드들은 연산 결과에 해당하는 새로운 `String` 인스턴스를 생성하여 반환한다

### String Builders
- `String` 객체는 `StringBuilder` 객체와 유사하지만, 값의 변경이 가능하다
- `StringBuilder` 객체는 내부적으로 가변 길이의 문자 배열처럼 다루어진다
  - 특정 시점에 메서드 호출로 인해 배열의 길이와 내용이 변경된다
- `StringBuiler` 의 사용이 코드를 간결하게 하거나 성능 상의 이점을 내지 않는 이상, `String` 사용을 권장한다
  - 자바 SE 9 전에는 문자열 더할 때 `StringBuilder` 의 사용이 더 효율적이었지만, 자바 SE 9 이후에는 `String` 더하는 연산이 최적화되어 `StringBuilder` 보다 더 효율적이다
- `StringBuilder` 도 `String` 과 마찬가지로 객체 내부에 존재하는 문자 시퀀스의 길이를 나타내는 메서드인 `length()` 가 존재한다
- `String` 과 다르게, 문자열을 위해 할당된 공간의 크기를 반환하는 `capacity()` 메서드가 존재한다
  - 항상 `length` 보다 크거나 같으며, 추가적인 공간이 필요하면 자동으로 확장된다
```java
// creates empty builder, capacity 16
StringBuilder sb = new StringBuilder();
// adds 9 character string at beginning
sb.append("Greetings");
```
- 길이가 9이고, 용량 (capacity) 가 16인 string builder 를 생성한다
- `StringBuilder` 와 동일하면서 `thread-safe` 한 `StringBuffer` 클래스도 존재한다
  - `thread-safe` 가 중요하지 않다면 속도 상의 이유로 사용하지 말아야 한다

### Autoboxing and Unboxing
- `Autoboxing` 은 자바 컴파일러가 원시 타입을 대응되는 객체 wrapper 클래스로 자동 변환시켜주는 것을 의미한다
- ex. `int` -> `Integer`, `double` -> `Double`
```java
List<Integer> ints = new ArrayList<>();
for (int i=1; i < 50; i += 2) 
    ints.add(i);
```
- 리스트에 `Integer` 객체가 아닌 원시 타입의 `int` 를 추가했지만, 컴파일 에러가 발생하지 않는다
  - 컴파일러에 의해 자동으로 `Integer` 객체로 변환된다 (`autoboxing`)