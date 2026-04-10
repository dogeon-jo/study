# 2022년 1월의 도서 판매 데이터를 기준으로 저자 별, 카테고리 별 매출액(TOTAL_SALES = 판매량 * 판매가) 을 구하여, 저자 ID(AUTHOR_ID), 저자명(AUTHOR_NAME), 카테고리(CATEGORY), 매출액(SALES) 리스트를 출력하는 SQL문을 작성해주세요.
# 결과는 저자 ID를 오름차순으로, 저자 ID가 같다면 카테고리를 내림차순 정렬해주세요.

SELECT
    A.AUTHOR_ID,                                
    A.AUTHOR_NAME,
    B.CATEGORY,
    SUM(B.PRICE * S.SALES) AS TOTAL_SALES       # 개수와 가격을 곱하여 합을 구함
FROM BOOK B                                     # 3개의 DB 도서 정보(BOOK), 저자정보(AUTHOR), 판매정보(BOOK_SALES) 중에서 도서정보의 DB가 공통된 컬럼을 가지고 있기 때문에 중심으로 잡았습니다.
JOIN AUTHOR A ON B.AUTHOR_ID = A.AUTHOR_ID      # 그룹인 도서 정보(BOOK), 저자정보(AUTHOR)를 각각 연결 해주기 위해 AS를 생략 했지만 AS를 사용하여 별칭을 정해주고 연결
JOIN BOOK_SALES S ON B.BOOK_ID = S.BOOK_ID
WHERE S.SALES_DATE LIKE '2022-01%'              # 2022년 1월의 정보만을 원하고 있기 때문에 WHERE을 사용해서 2022년 데이터 필터링
GROUP BY A.AUTHOR_ID, A.AUTHOR_NAME, B.CATEGORY # 따로 컬럼명을 작성한 컬럼을 제외하고 나머지를 그룹화하는 것이 안전하기 때문에 TOTAL_SALES를 제외한 나머지 컬럼을 그룹화
ORDER BY A.AUTHOR_ID ASC, B.CATEGORY DESC;      # 저자ID를 오름차순(ASC), 카테고리를 내림차순(DESC)

