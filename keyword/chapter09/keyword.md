스터디 질문 내용
워크북 내용중
> API 하나를 모두 완성 후 명세를 하게 되면 프론트엔드 개발자는 해당 API가 완성이 될 때 까지 다른 API의 응답을 모르기 때문에 작업을 멈추게 됩니다. 이런 상황을 최대한 막기 위해 우선적으로 응답 Data의 형태를 알려주어 프론트 개발자도 미리 API 연결 부분을 작업 해둬 최대한 개발을 **병렬적으로** 할 수 있도록 합니다.

라는 부분이 있는데, 지난 플젝 기준으로 API 기능 개발이 전체적으로 끝나고 서버 호스팅을 마친 뒤에야 연결 작업을 진행했었는데, 배포 하기 전에도 미리 Swagger로 공유를 하는지? 그러면 프론트 측에서 스프링 코드를 클론받아서 실행시키고 보면서 작업해야하는건가

### Swagger 기능
- `@Operation` : API에대한 설명을 넣을 수 있다. summary, description으로 설명을 적는다.
- `@ApiResponse` : API의 응답을 담게되며 내부적으로 @ApiResponse로 각각의 응답들을 담게된다.
- `@Parameters` : 프론트엔드에서 넘겨줘야 할 정보를 담으며, path variable, query String 등등 기재할 수 있음


## 키워드 정리
### Spring Data JPA의 Paging
Spring Data JPA는 대용량 데이터를 효율적으로 관리하기 위해 페이징(Paging) 기능을 제공

페이징은 데이터의 특정 범위를 나누어 조회하는 기능으로, 두 가지 대표적인 인터페이스를 제공한다. 

Page
- `Page`는 페이징 처리된 데이터와 함께 전체 데이터에 대한 메타정보를 제공한다 (ex. 전체 페이지 수, 전체 요소 수 등)
- 메타정보를 함께 가져오기 때문에 약간의 추가 쿼리가 실행된다.
```Java
Pageable pageable = PageRequest.of(0, 10); // 페이지 번호와 페이지 크기 지정
Page<MyEntity> page = myEntityRepository.findAll(pageable);

System.out.println("전체 페이지 수: " + page.getTotalPages());
System.out.println("전체 요소 수: " + page.getTotalElements());
System.out.println("현재 페이지 번호: " + page.getNumber());
System.out.println("현재 페이지 데이터: " + page.getContent());

```
- 장점: 
    - 전체 데이터의 크기를 구할 수 있다.
    - 페이지 이동 기능을 구현하기 용이하다.
- 단점:
    - `COUNT`쿼리가 추가적으로 실행된다.

Slice
- `Slice`는 현재 페이지에 대한 데이터와 다음 페이지의 존재 여부만 제공된다.
- 전체 페이지 수나 전체 요소 수를 구하지 않으므로 `COUNT`쿼리가 실행되지 않아 성능상 이점이 있다.
```Java
Pageable pageable = PageRequest.of(0, 10); // 페이지 번호와 페이지 크기 지정
Slice<MyEntity> slice = myEntityRepository.findAll(pageable);

System.out.println("현재 페이지 데이터: " + slice.getContent());
System.out.println("다음 페이지 존재 여부: " + slice.hasNext());

```

- 장점
    - 필요한 데이터만 조회하여 성능이 더 효율적이다
    - 다음 페이지 존재 여부만 확인하면 되는 무한 스크롤(인피니트 스크롤) 구현에 적합하다
- 단점
    - 전체 데이터의 크기를 알 수 없다
### 객체그래프 탐색 처리
Spirng Data JPA는 엔티티를 효율적으로 로드하기 위한 객체 그래프 탐색 전략을 제공한다. 대표적으로 지연로딩과 즉시로딩 전략이다. 

- 지연 로딩
    - 연관된 엔티티를 실제 사용 시점에 로드
    - `@OneToMany`, `@ManyToOne` 관계에서 기본적으로 사용됨
    - 데이터베이스 쿼리가 필요할 떄만 실행되므로 초기 로드 시 성능이 좋음
- 즉시 로딩
    - 연관된 엔티티를 즉시 로드
    - 연관 엔티티를 자주 사용하는 경우 적합
- Fetch Join
    - 객체 그래프를 탐색할 때 JPA의 Fetch Join을 사용하면 N+1문제를 방지할 수 있음
    - 연관된 엔티티를 한번의 쿼리로 가져온다
    