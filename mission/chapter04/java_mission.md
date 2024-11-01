# Stream API

Stream API는 데이터를 추상화하고 처리하는데 자주 사용되는 함수들을 정의해둔 것이다. (추상화라는 것은 데이터의 종류에 상관 없이 같은 방식으로 데이터를 처리할 수 있다는 것을 의미) -> 재사용성 증가

Stream은 컬렉션(List, Set 등) 또는 배열에 저장된 데이터를 추상화한 연산 흐름으로, 이를 통해 필터링, 매핑, 정렬 등의 다양한 작업을 간결하게 수행할 수 있다.

코드의 가독성을 좋게 만들 수 있고, 병렬 처리를 쉽게 할 수 있다.

### 문제풀이
1부터 10까지 다루는 정수 배열을 문제의 조건에 맞춰 다루는 코드를 작성해보았다.
사용되는 기능들은 대표적으로
- `toArray`: 스트림의 요소들을 배열로 수집해 반환, 스트림 연산 결과를 배열 형태로 쉽게 변환 가능
- `rangeClosed`: 특정 범위의 숫자들을 포함하는 intStream을 생성하는 메서드
- `filter`: 스트림의 각 요소에 조건을 적용해 조건을 만족하는 요소만 걸러냄
- `mapTo...`: 스트림의 각 요소를 다른 타입으로 변환하는 연산을 수행
```
import java.util.Arrays;
import java.util.stream.IntStream;

public class StreamExample {

    public static void main(String[] args) {
        // 1부터 10까지 있는 정수 배열 생성
        int[] numbers = IntStream.rangeClosed(1, 10).toArray();

        // 배열을 스트림으로 만들어 요소를 모두 2배로 만든 배열 반환 후 비교
        int[] doubledNumbers = Arrays.stream(numbers).map(n -> n * 2).toArray();
        System.out.println("원본 배열: " + Arrays.toString(numbers));
        System.out.println("2배로 만든 배열: " + Arrays.toString(doubledNumbers));

        // 배열 중 짝수만 "숫자 + is even number"로 변환하여 문자열 배열 생성 후 출력
        String[] evenNumbersStrings = Arrays.stream(numbers)
                .filter(n -> n % 2 == 0)
                .mapToObj(n -> n + " is even number")
                .toArray(String[]::new);
        System.out.println("짝수 변환 배열: " + Arrays.toString(evenNumbersStrings));
    }
}
```
실행결과
```
/Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home/bin/java -javaagent:/Users/k.seonwoo/Applications/IntelliJ IDEA Community Edition.app/Contents/lib/idea_rt.jar=61984:/Users/k.seonwoo/Applications/IntelliJ IDEA Community Edition.app/Contents/bin -Dfile.encoding=UTF-8 -classpath /Users/k.seonwoo/Downloads/java_practice/out/production/java_practice StreamExample
원본 배열: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
2배로 만든 배열: [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
짝수 변환 배열: [2 is even number, 4 is even number, 6 is even number, 8 is even number, 10 is even number]
```





# 함수 인터페이스
함수형 인터페이스는 추상메서드가 1개만 정의된 인터페이스를 통칭하여 일컫는다. 이 인터페이스 형태의 목적은 자바에서 람다 표현식을 이용해 함수형 프로그래밍을 구현하는 것이다.

여기서, 함수는 리턴값이 있을수도 있고 없을 수도 있다. 매개변수가 1개일수도, 2개일수도, 없을수도 있다. 이렇게 다양한 함수의 형태에 대해 미리 만들어져 있는 함수형 인터페이스를 사용할 수 있다. 이것을 함수형 인터페이스 표준 API라고 한다.

함수적 인터페이스 표준 API는 `java.util.function` 패키지로 제공된다.

함수적 인터페이스 종류로는 Consumer, Supplier, Function, Operator, Predicate가 있다. 각 함수의 형태와 목적에 따라 붙여진 이름이다.
(메서드 형태, 매개변수, 반환값 등)


### 문제풀이


```
import java.util.function.Function;

public class FunctionExamples {

    public static void main(String[] args) {
        // 1. 익명 클래스 정의 -> Function<T, R> 사용 Integer->String으로 변환
        Function<Integer, String> functionAnonymous = new Function<Integer, String>() {
            @Override
            public String apply(Integer i) {
                return String.valueOf(i);
            }
        };
        
        // 2. 클래스를 상속받아 구현
        class MyFunction implements Function<Integer, String> {
            @Override
            public String apply(Integer i) {
                return String.valueOf(i);
            }
        }
        Function<Integer, String> functionClass = new MyFunction();
        
        // 3. 람다식으로 정의
        Function<Integer, String> functionLambda = i -> String.valueOf(i);
        
        // 4. 메서드 참조로 정의 (String.valueOf 메서드 사용)
        Function<Integer, String> functionMethodReference = String::valueOf;

        // 각 함수로 정수 변환 후 출력
        System.out.println("익명 클래스 결과: " + functionAnonymous.apply(123)); // +연산자로 스트링 값끼리 출력
        System.out.println("클래스 상속 결과: " + functionClass.apply(456));
        System.out.println("람다식 결과: " + functionLambda.apply(789));
        System.out.println("메서드 참조 결과: " + functionMethodReference.apply(101));
    }
}

```
실행결과
```
/Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home/bin/java -javaagent:/Users/k.seonwoo/Applications/IntelliJ IDEA Community Edition.app/Contents/lib/idea_rt.jar=61456:/Users/k.seonwoo/Applications/IntelliJ IDEA Community Edition.app/Contents/bin -Dfile.encoding=UTF-8 -classpath /Users/k.seonwoo/Downloads/java_practice/out/production/java_practice FunctionExamples
익명 클래스 결과: 123
클래스 상속 결과: 456
람다식 결과: 789
메서드 참조 결과: 101

종료 코드 0(으)로 완료된 프로세스

```

