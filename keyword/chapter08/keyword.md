내용 정리

- converter: 타입 변환, 데이터 바인딩, 서비스 계층에서 DTO와 엔티티간 변환을 위해 활용



Java의 Exception 종류들
1. Checked Exception
컴파일 시점에 반드시 처리해야 하는 예외로, try-catch 또는 throws를 통해 예외 처리가 강제
데이터베이스 작업이나 파일 입출력 시 자주 발생
예시: IOException, SQLException.
2. Unchecked Exception
런타임 시점에 발생하며, 처리하지 않아도 컴파일은 정상적으로 된다.
주로 프로그래밍 실수로 인해 발생하며, Null 처리와 같은 상황에서 자주 나타난다.
예시: NullPointerException, IndexOutOfBoundsException.
3. Error
시스템 레벨에서 발생하는 문제로, 일반적으로 개발자가 처리할 수 없는 경우이며
메모리 부족이나 스택 오버플로와 같은 상황에서 발생한다.
예시: OutOfMemoryError, StackOverflowError.
4. Custom Exception
애플리케이션 로직에 따라 개발자가 정의한 예외 클래스
Exception이나 RuntimeException을 상속받아 구현하며, 특정 상황을 명확하게 처리 가능
@Valid
1. @Valid의 역할
@Valid는 스프링에서 객체의 유효성을 검증하기 위해 사용하는 어노테이션
입력 데이터가 유효한지 자동으로 확인하며, 주로 Controller에서 요청 데이터 검증에 사용된다
2. 유효성 검증 기본 원리
@Valid는 Bean Validation API(JSR 380)를 기반으로 동작한다
유효성 규칙이 위반되면 예외(MethodArgumentNotValidException)가 발생한다
3. 주요 유효성 검증 어노테이션
@NotNull, @Size, @Pattern, @Email, @Min, @Max 등을 사용하여 필드 조건을 명시한다
4. Custom Validation
@Constraint와 ConstraintValidator를 사용하여 커스텀 검증 규칙을 구현할 수 있다.