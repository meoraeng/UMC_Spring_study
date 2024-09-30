# 머랭 5주차 미션 인증

![2차](./images/Untitled.png)

2차

1. 4주차 때 설계한 데이터베이스를 토대로 아래의 화면에 대한 쿼리를 작성

![내가 진행중, 진행 완료한 미션 모아서 보는 쿼리(페이징 포함)](./images/Untitled%201.png)

내가 진행중, 진행 완료한 미션 모아서 보는 쿼리(페이징 포함)

```sql
SELECT mm.*
FROM member_mission AS mm
JOIN mission AS m ON mm.mission_id = m.id
WHERE mm.member_id = '유저 ID'
  AND (mm.status = 'in progress' OR mm.status = 'success')
ORDER BY mm.status DESC
LIMIT 10 OFFSET 0;
```

테이블에서 특정 사용자의 데이터를 반환하는 쿼리, Offset based 페이징 적용

![리뷰 조회 및 해당 리뷰에 댓글 다는 쿼리](./images/Untitled%202.png)

리뷰 조회 및 해당 리뷰에 댓글 다는 쿼리

```sql
SELECT r.*, m.name AS member_name, s.name AS store_name
FROM review AS r
JOIN member AS m ON r.member_id = m.id
JOIN store AS s ON r.store_id = s.id
WHERE r.store_id = '가게 ID'
ORDER BY r.created_at DESC;

```

특정 가게에 대한 리뷰 또는 특정 유저의 리뷰를 조회

```sql
UPDATE review
SET content = CONCAT(content, '\n댓글 내용: 추가적인 댓글입니다.')
WHERE id = '리뷰 ID';
```

![홈 화면 쿼리
(현재 선택 된 지역에서 도전이 가능한 미션 목록, 페이징 포함)](./images/Untitled%203.png)

홈 화면 쿼리
(현재 선택 된 지역에서 도전이 가능한 미션 목록, 페이징 포함)

```sql
SELECT m.id, m.name, m.mission_spec, m.reward, 
       COUNT(mm.id) AS completed_missions_count
FROM mission AS m
LEFT JOIN store AS s ON m.store_id = s.id
LEFT JOIN region AS r ON s.region_id = r.id
LEFT JOIN member_mission AS mm ON mm.mission_id = m.id AND mm.status = '완료'
WHERE r.id = '지역 ID'
GROUP BY m.id, m.name, m.mission_spec, m.reward
ORDER BY m.created_at DESC;
```

- JOIN → 미션, 상점, 지역, 그리고 멤버 미션을 연결하여 정보에 접근
- 지역 id 기준으로 지역 조회
- COUNT로 완료된 미션 갯수 카운트하여 홈화면에 출력

![마이 페이지 화면 쿼리](./images/Untitled%204.png)

마이 페이지 화면 쿼리

```sql
SELECT name, email, phone_number FROM member WHERE id = '유저 ID'
```