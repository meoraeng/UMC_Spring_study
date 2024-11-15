## 어노테이션 정리
- `@Getter`: 클래스의 모든 필드에 getter 메소드 자동 생성
- `@AllArgsConstructor`: 모든 필드를 파라미터로 받는 생성자 자동으로 생성
- `@JsonPropertyOrder`: JSON 직렬화 시 필드의 출력 순서를 지정
- `@JsonInclude(JsonInclude.Include.NOT_NULL)`: null인 필드를 JSON에 포함하지 않도록 한다 


### Builder
builder(): (복습)빌더패턴 구현 메서드, 클래스에 대한 빌더 인스턴스를 반환하여 유연하게 객체를 생성할 수 있게 한다.
반환된 빌더 객체를 사용해 필요한 필드를 지정할 수 있고 각 필드를 설정하는 메서드는 빌더 객체 자체를 반환하여, 메서드 체이닝 방식으로 필드 설정 후 build()메서드를 호출하여, 설정된 필드들로 객체를 생성

우리가 만드는 인스턴스는 모두 빌더 패턴을 쓴다고 생각하면 편하다.


## 키워드 정리
`public static class`를 쓰는 이유는 다음과 같다.
> DTO는 수많은 곳에서 사용되기 때문에, static class로 만들면 매번 class파일을 만들 필요 없이 범용적으로 DTO를 사용 가능

