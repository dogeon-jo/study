# 코딩테스트 스터디 기록

## 문제
데이터 분석 팀에서는 우유(Milk)와 요거트(Yogurt)를 동시에 구입한 장바구니가 있는지 알아보려 합니다.
우유와 요거트를 동시에 구입한 장바구니의 아이디를 조회하는 SQL 문을 작성해주세요. 이때 결과는 장바구니의 아이디 순으로 나와야 합니다.

- 날짜 
-- 2026-04-13

- 링크
-- https://school.programmers.co.kr/learn/courses/30/lessons/62284

## 작성쿼리
```SQL
SELECT
    CART_ID
FROM CART_PRODUCTS
WHERE CART_ID IN (SELECT CART_ID FROM CART_PRODUCTS WHERE NAME = 'Milk')
AND NAME = 'Yogurt'
ORDER BY CART_ID ASC;
```

## 배운점
- 서브쿼리를 사용해서 WHERE절에 2가지 조건을 넣을 수 있다는 것을 배웠습니다.