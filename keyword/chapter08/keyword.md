### 내용 정리

- converter: 타입 변환, 데이터 바인딩, 서비스 계층에서 DTO와 엔티티간 변환을 위해 활용

- collect 메서드 : Java Stream 종료 연산중 하나
    - 스트림의 모든 요소를 특정 컬렉션 형태로 수집할떄 사용(ex.`List`)
- `Collectors.toList()`:
    - Collectors 클래스의 static method
    - 스트림의 요소를 List로 수집하는데 사용
    - 변환된 객체들을 새로운 `List<type>`로 모은다.
- `stream()`: Java컬렉션(ex.`List`)에 사용할 수 있는 메서드로, 해당 컬렉션의 데이터를 기반으로 Stream 객체를 생성한다
    - 단순히 데이터를 담고있는 컨테이너가 아니라, 데이터 처리 파이프라인을 설정하는 도구
    - 스트림 내부에 데이터가 직접 저장되지 않음, 컬렉션의 데이터가 스트림 파이프라인을 통해 필터링, 변환, 수집
    - 데이터를 간결하고 효율적으로 처리할 수 있음
- `@Transactional`: 스프링에서 데이터베이스 트랜잭션을 관리하기 위한 설정을 제공한다. 여러 데이터베이스 작업을 하나의 논리적 단위로 처리하기 위해 사용된다.
    - 트랜잭션 시작과 종료를 관리한다.
    - 예외 발생 시 롤백한다
    - 트랜잭션 간의 격리 수준을 설정할 수 있다

- Swagger 세팅
    - `@Configuration` 어노테이션(설정 클래스 명시)과 `@Bean`어노테이션(구성객체 반환) 사용
    - `new Info()` : Swagger UI 상단에 표시될 API 제목, 설명, 버전 정의
    - `SecurityRequirement`: API요청에 보안 요구사항 정의 - 이번엔 JWT 인증 토큰을 API요청시 헤더에 포함하도록 함
    - `Component` 객체: Swagger 문서에서 사용할 다양한 보안 구성 및 재사용 가능한 객체 정의 -> JWT 인증 스키마 설정(타입, 스키마, 포맷)
    - `OpenAPI`객체 : Swagger 전체 구성을 정의
        - `addServersItem`: 기본 URL 설정
        - `addSecurityItem`: API가 요구하는 보안 설정을 추가. JWT 토큰 인증을 요구하도록 설정.
        - `components`: 위에서 정의한 보안스키마와 기타 재사용 가능한 설정들을 포함


### 키워드 정리

### Java의 Exception 종류들
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

### @Valid
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