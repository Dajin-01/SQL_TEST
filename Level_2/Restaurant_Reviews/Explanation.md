# 조건에 맞는 회원수 구하기

## 문제 설명

`MEMBER_PROFILE` 테이블에서 생일이 3월인 여성 회원의 정보를 조회하는 문제입니다.

단, 전화번호가 `NULL`인 회원은 출력 대상에서 제외해야 하며,  
결과는 `회원 ID`를 기준으로 오름차순 정렬해야 합니다.

---

## 테이블 구조

| Column name | Type | Nullable | 설명 |
|---|---|---|---|
| MEMBER_ID | VARCHAR(100) | FALSE | 회원 ID |
| MEMBER_NAME | VARCHAR(50) | FALSE | 회원 이름 |
| TLNO | VARCHAR(50) | TRUE | 회원 연락처 |
| GENDER | VARCHAR(1) | TRUE | 성별 |
| DATE_OF_BIRTH | DATE | TRUE | 생년월일 |

---

## 문제 조건

- 성별이 여성인 회원만 조회
- 생일이 3월인 회원만 조회
- 전화번호가 `NULL`인 회원은 제외
- 결과는 회원 ID 기준 오름차순 정렬
- 생년월일은 `YYYY-MM-DD` 형식으로 출력
- 출력 컬럼은 `MEMBER_ID`, `MEMBER_NAME`, `GENDER`, `DATE_OF_BIRTH`

---

## 풀이 설명

`WHERE GENDER = 'W'` 조건으로 여성 회원만 필터링합니다.

생일이 3월인 회원을 찾기 위해 `MONTH(DATE_OF_BIRTH) = 3` 조건을 사용하고,  
전화번호가 없는 회원은 제외해야 하므로 `TLNO IS NOT NULL` 조건을 추가합니다.

또한 문제에서 요구한 날짜 형식과 동일하게 출력하기 위해  
`DATE_FORMAT(DATE_OF_BIRTH, '%Y-%m-%d')`를 사용합니다.

마지막으로 결과는 `ORDER BY MEMBER_ID ASC`를 사용해 회원 ID 기준 오름차순으로 정렬합니다.

## 정답 코드

```sql
SELECT 
    MEMBER_ID,
    MEMBER_NAME,
    GENDER,
    DATE_FORMAT(DATE_OF_BIRTH, '%Y-%m-%d') AS DATE_OF_BIRTH
FROM MEMBER_PROFILE
WHERE GENDER = 'W'
  AND TLNO IS NOT NULL
  AND MONTH(DATE_OF_BIRTH) = 3
ORDER BY MEMBER_ID ASC;
