# 코딩테스트 스터디 기록

## 문제
보호소에서 중성화 수술을 거친 동물 정보를 알아보려 합니다.
보호소에 들어올 당시에는 중성화1되지 않았지만, 보호소를 나갈 당시에는 중성화된 동물의 아이디와 생물 종, 이름을 조회하는 아이디 순으로 조회하는 SQL 문을 작성해주세요.
- 날짜 
-- 2026-04-18

- 링크
-- https://school.programmers.co.kr/learn/courses/30/lessons/59045

## 작성쿼리
```SQL
SELECT
    I.ANIMAL_ID,
    I.ANIMAL_TYPE,
    I.NAME
FROM ANIMAL_INS I
JOIN ANIMAL_OUTS O ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE I.SEX_UPON_INTAKE LIKE 'Intact%'
    AND (O.SEX_UPON_OUTCOME LIKE 'Spayed%' OR O.SEX_UPON_OUTCOME LIKE 'Neutered%');
```

## 배운점
- WHERE절에서 LIKE연산자를 활용해 특정 상태변화라는 필터링하는 법을 배웠습니다.