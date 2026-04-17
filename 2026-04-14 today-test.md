# 코딩테스트 스터디 기록

## 문제
7월 아이스크림 총 주문량과 상반기의 아이스크림 총 주문량을 더한 값이 큰 순서대로 상위 3개의 맛을 조회하는 SQL 문을 작성해주세요.

- 날짜 
-- 2026-04-14

- 링크
-- https://school.programmers.co.kr/learn/courses/30/lessons/133027

## 작성쿼리
```SQL
SELECT
    H.FLAVOR
FROM FIRST_HALF H
JOIN (SELECT FLAVOR,SUM(TOTAL_ORDER) AS TOTAL_ORDER FROM JULY GROUP BY FLAVOR) J ON J.FLAVOR = H.FLAVOR
ORDER BY (H.TOTAL_ORDER + J.TOTAL_ORDER) DESC
LIMIT 3;
```

## 배운점
- Join문에서도 서브 커리를 사용하여 한개의 테이블을 가지고 합칠 수 있다는 것을 배웠습니다.