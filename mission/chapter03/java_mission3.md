# Chapter3. 추가 미션_generic&wild card, wrapper class, optional

# Generic

- 정의 : 클래스나 메서드에서 사용할 데이터 타입을 일반화할 수 있는 기능으로, 컴파일 시점에 타입 체크를 수행하도록 하여 타입 안전성을 높여준다.

```sql
List<String> list = new ArrayList<>();
list.add("Hello");
String value = list.get(0); // 타입 캐스팅 불필요
```

- 장점: **컴파일러가 타입을 체크**해주기 때문에, **실행 시점에서 발생할 수 있는 타입 에러를 줄일 수 있다**.

### Wild Card

- 정의: 제네릭에서 타입의 불확실성을 표현하기 위해 사용되는 기호 `?`, 메서드에서 **제네릭 타입 파라미터의 범위를 유연하게 지정**할 때 사용
- 종류:
    - 무제한 `<?>`: 어떤 타입이든 받을 수 있다
    - 상한 제한 `<? extends Type>`: 특정 클래스 또는 그 **하위 타입** 허용
    - 하한 제한 : `<? super Type>`:  특정 클래스 또는 그 **상위 타입** 허용

```java
List<? extends Number> numbers = new ArrayList<Integer>(); // Integer나 Double 등 Number의 하위 타입 허용
List<? super Integer> integers = new ArrayList<Number>(); // Integer나 Number의 상위 타입 허용
```

# Wrapper Class

- 정의: 래퍼 클래스는 **기본 데이터 타입을 객체로 다루기 위해** 제공되는 클래스,
기본 타입인 int, double 등은 객체로서 메소드 호출이 불가능하므로 이를 래퍼클래스로 감싸서 사용
- 기본 타입과 대응 되는 래퍼 클래스 :
    - `int` → `Integer`
    - `double` → `Double`
    - `boolean` → `Boolean`

```java
Integer num = 10; // int 값을 Integer 객체로 감싸는 경우
int value = num;  // Integer 객체에서 int 값 추출하는 경우
```

- 장점: 객체만 다뤄야 하는 상황에서 기본 타입을 객체로서 사용할 수 있다.

# Optional

- 정의: `null`값 대신, 존재할 수도 있고 존재하지 않을 수도 있도록 하는 값으로 사용 한다. 
(주로 `null`로 인한 `NullPointerException`을 방지하기 위해 사용)
- 장점: `null` 값 체크를 명시적으로 할 수 있어 코드 가독성을 높이고, `null`로 인해 발생하는 에러를 예방할 수 있다.

```java
Optional<String> optionalValue = Optional.of("Hello");
optionalValue.ifPresent(System.out::println); // 값이 존재하면 출력

Optional<String> emptyValue = Optional.empty();
String defaultValue = emptyValue.orElse("Default Value"); // 값이 없으면 대체 값을 사용
```