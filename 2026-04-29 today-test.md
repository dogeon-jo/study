# 코딩테스트 스터디 기록

## 문제
자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴해주세요. 예를들어 n이 12345이면 [5,4,3,2,1]을 리턴합니다.

- 날짜 
-- 2026-04-28

- 링크
-- https://school.programmers.co.kr/learn/courses/30/lessons/12932

## 작성쿼리
```PYTHON
def solution(n):
    answer = [int(i) for i in str(n)][::-1]
    return answer
```

## 배운점
- [::-1]을 사용해서 역배역을 한다는 것을 배웠습니다