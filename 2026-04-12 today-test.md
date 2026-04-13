# 코딩테스트 스터디 기록

## 문제
REST_INFO와 REST_REVIEW 테이블에서 서울에 위치한 식당들의 식당 ID, 식당 이름, 음식 종류, 즐겨찾기수, 주소, 리뷰 평균 점수를 조회하는 SQL문을 작성해주세요.
이때 리뷰 평균점수는 소수점 세 번째 자리에서 반올림 해주시고 결과는 평균점수를 기준으로 내림차순 정렬해주시고, 평균점수가 같다면 즐겨찾기수를 기준으로 내림차순 정렬해주세요.

- 날짜 
-- 2026-04-12

- 링크
-- https://school.programmers.co.kr/learn/courses/30/lessons/131118

## 작성쿼리
```SQL
SELECT
    I.REST_ID,
    I.REST_NAME,
    I.FOOD_TYPE,
    I.FAVORITES,
    I.ADDRESS,
    ROUND(AVG(R.REVIEW_SCORE),2) AS SCORE   -- 리뷰평균점수를 구하고 소수점 3번째 자리에서 반올림을 해야되므로 ROUND(,2)를 사용해서 반올림
FROM REST_INFO I
JOIN REST_REVIEW R ON I.REST_ID = R.REST_ID -- REST_INFO와 REST_INFO에 있는 내용을 함께 보기위해서 조인
WHERE I.ADDRESS LIKE '서울%'    -- 서울에 위치한 식당을 선택
GROUP BY 
    I.REST_ID,
    I.REST_NAME,
    I.FOOD_TYPE,
    I.FAVORITES,
    I.ADDRESS
ORDER BY SCORE DESC, I.FAVORITES DESC;  -- 평균점수를 내림차순, 같다면 즐겨찾기수를 기준으로 내림차순
```

## 배운점
- 특정 지역을 필터링 및 다중 정렬을 통해 사용자 요구에 맞는 데이터 가공 방법을 배웠습니다.