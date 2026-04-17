# 코딩테스트 스터디 기록

## 문제
MEMBER_PROFILE와 REST_REVIEW 테이블에서 리뷰를 가장 많이 작성한 회원의 리뷰들을 조회하는 SQL문을 작성해주세요.
회원 이름, 리뷰 텍스트, 리뷰 작성일이 출력되도록 작성해주시고, 결과는 리뷰 작성일을 기준으로 오름차순, 리뷰 작성일이 같다면 리뷰 텍스트를 기준으로 오름차순 정렬해주세요.

- 날짜 
-- 2026-04-15

- 링크
-- https://school.programmers.co.kr/learn/courses/30/lessons/131124

## 작성쿼리
```SQL
SELECT
    P.MEMBER_NAME,
    R.REVIEW_TEXT,
    DATE_FORMAT(R.REVIEW_DATE, '%Y-%m-%d') AS REVIEW_DATE
FROM MEMBER_PROFILE P
JOIN REST_REVIEW R ON P.MEMBER_ID = R.MEMBER_ID
WHERE P.MEMBER_ID = (SELECT MEMBER_ID FROM REST_REVIEW GROUP BY MEMBER_ID ORDER BY COUNT(*) DESC LIMIT 1)
ORDER BY R.REVIEW_DATE ASC, R.REVIEW_TEXT ASC;
```

## 배운점
- WHERE절에서 ORDER BY 에서 COUNT(*)를 사용이 가능하다는 것을 배웠습니다.