# 코딩테스트 스터디 기록

## 문제
CAR_RENTAL_COMPANY_CAR 테이블과 CAR_RENTAL_COMPANY_RENTAL_HISTORY 테이블과 CAR_RENTAL_COMPANY_DISCOUNT_PLAN 테이블에서 자동차 종류가 
'트럭'인 자동차의 대여 기록에 대해서 대여 기록 별로 대여 금액(컬럼명: FEE)을 구하여 대여 기록 ID와 대여 금액 리스트를 출력하는 SQL문을 작성해주세요. 
결과는 대여 금액을 기준으로 내림차순 정렬하고, 대여 금액이 같은 경우 대여 기록 ID를 기준으로 내림차순 정렬해주세요.

- 날짜 
-- 2026-04-19

- 링크
-- https://school.programmers.co.kr/learn/courses/30/lessons/59045

## 작성쿼리
```SQL
SELECT
    H.HISTORY_ID,
    ROUND(C.DAILY_FEE * (DATEDIFF(H.END_DATE, H.START_DATE) + 1) * (100 - IFNULL(P.DISCOUNT_RATE, 0)) / 100) AS FEE
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY H
JOIN CAR_RENTAL_COMPANY_CAR C ON H.CAR_ID = C.CAR_ID
LEFT JOIN CAR_RENTAL_COMPANY_DISCOUNT_PLAN P
    ON P.CAR_TYPE = C.CAR_TYPE
    AND P.DURATION_TYPE = (
        CASE 
            WHEN DATEDIFF(H.END_DATE, H.START_DATE) + 1 >= 90 THEN '90일 이상'
            WHEN DATEDIFF(H.END_DATE, H.START_DATE) + 1 >= 30 THEN '30일 이상'
            WHEN DATEDIFF(H.END_DATE, H.START_DATE) + 1 >= 7 THEN '7일 이상'
            ELSE NULL 
        END
    )
WHERE C.CAR_TYPE = '트럭'
ORDER BY FEE DESC, H.HISTORY_ID DESC;
```

## 배운점
- LEFT JOIN에서 WHERE 절은 기준 테이블의 컬럼을 사용해서 데이터 누락을 방지하고, DATEDIFF 와 CASE 문으로 새로운 걸럼을 만들수 있다는 것을 배웠습니다.