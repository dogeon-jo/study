# 코딩테스트 스터디 기록

## 문제
보호소에서는 몇 시에 입양이 가장 활발하게 일어나는지 알아보려 합니다.
0시부터 23시까지, 각 시간대별로 입양이 몇 건이나 발생했는지 조회하는 SQL문을 작성해주세요.
이때 결과는 시간대 순으로 정렬해야 합니다.


- 날짜 
-- 2026-04-17

- 링크
-- https://school.programmers.co.kr/learn/courses/30/lessons/59413

## 작성쿼리
```SQL
WITH RECURSIVE TIME_LIST AS (
    SELECT 0 AS HOUR
    UNION ALL
    SELECT HOUR + 1 FROM TIME_LIST WHERE HOUR < 23
)

SELECT
    L.HOUR,
    COUNT(O.ANIMAL_ID) AS COUNT
FROM TIME_LIST L
LEFT JOIN ANIMAL_OUTS O ON L.HOUR = HOUR(O.DATETIME)
GROUP BY L.HOUR
ORDER BY L.HOUR;
```

## 배운점
- WITH RECURSIVE 를 사용해서 하나의 테이블을 생성하고 이를 원래의 테이블과 합칠수 있다는 것을 알게 되었습니다.