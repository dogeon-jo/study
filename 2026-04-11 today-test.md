# 코딩테스트 스터디 기록

## 문제
PATIENT, DOCTOR 그리고 APPOINTMENT 테이블에서 2022년 4월 13일 취소되지 않은 흉부외과(CS) 진료 예약 내역을 조회하는 SQL문을 작성해주세요.
진료예약번호, 환자이름, 환자번호, 진료과코드, 의사이름, 진료예약일시 항목이 출력되도록 작성해주세요. 결과는 진료예약일시를 기준으로 오름차순 정렬해주세요.

- 날짜
-- 2026-04-11

- 링크
-- https://school.programmers.co.kr/learn/courses/30/lessons/132204

## 작성쿼리
```SQL
SELECT
    A.APNT_NO,
    P.PT_NAME,
    P.PT_NO,
    A.MCDP_CD,
    D.DR_NAME,
    A.APNT_YMD
FROM APPOINTMENT A                      -- 3개의 PATIENT, DOCTOR 그리고 APPOINTMENT 3개의 테이블을 하나로 합칠수있는 공통된 컬럼을 가지고 있기 때문에 중심된 테이블로 지정
JOIN PATIENT P ON A.PT_NO = P.PT_NO     -- 그룹인 PATIENT, APPOINTMENT를 각각 연결 해주기 위해 AS를 생략 했지만 AS를 사용하여 별칭을 정해주고 연결
JOIN DOCTOR D ON A.MDDR_ID = D.DR_ID    -- 그룹인 DOCTOR, APPOINTMENT를 각각 연결 해주기 위해 AS를 생략 했지만 AS를 사용하여 별칭을 정해주고 연결
WHERE A.APNT_YMD LIKE '2022-04-13%'     -- 2022년 4월 13일 데이터만을 필요로 하지만 APNT_YMD 컬럼에 시간또한 포함이 되어있기 때문에 `%`를 사용해서 시간또한 포함되게 사용
    AND A.APNT_CNCL_YN = 'N'            -- 예약이 취소되지 않은 데이터를 추출
    AND D.MCDP_CD ='CS'                 -- MCDP_CD가 CS인 데이터만 추출
ORDER BY A.APNT_YMD ASC;                -- 진료예약일시를 기준으로 오름차순진행
```

## 배운점
- 3개지의 테이블을 조인하여 복잡한 필터링 조건을 적용하여 유요한 예약 데이터를 추출하는 방법을 배웠습니다.