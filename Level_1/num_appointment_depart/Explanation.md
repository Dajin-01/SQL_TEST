# 진료과별 총 예약 횟수 출력하기

## 문제 설명

`DOCTOR` 테이블에서 진료과가 흉부외과(`CS`)이거나 일반외과(`GS`)인 의사의 정보를 조회하는 문제입니다.

조회할 컬럼은 의사 이름, 의사 ID, 진료과 코드, 고용일자이며,  
결과는 고용일자를 기준으로 내림차순 정렬해야 합니다.

고용일자가 같은 경우에는 의사 이름을 기준으로 오름차순 정렬합니다.

---

## 테이블 구조

| Column name | Type | Nullable | 설명 |
|---|---|---|---|
| DR_NAME | VARCHAR(20) | FALSE | 의사 이름 |
| DR_ID | VARCHAR(10) | FALSE | 의사 ID |
| LCNS_NO | VARCHAR(30) | FALSE | 면허 번호 |
| HIRE_YMD | DATE | FALSE | 고용일자 |
| MCDP_CD | VARCHAR(6) | TRUE | 진료과 코드 |
| TLNO | VARCHAR(50) | TRUE | 전화번호 |

---

## 문제 조건

- 진료과 코드가 `CS` 또는 `GS`인 의사만 조회
- 출력 컬럼은 `DR_NAME`, `DR_ID`, `MCDP_CD`, `HIRE_YMD`
- 고용일자는 `YYYY-MM-DD` 형식으로 출력
- 결과는 고용일자 기준 내림차순 정렬
- 고용일자가 같다면 의사 이름 기준 오름차순 정렬

---

## 풀이 설명

`WHERE MCDP_CD = 'CS' OR MCDP_CD = 'GS'` 조건을 사용해  
진료과가 흉부외과 또는 일반외과인 의사만 필터링합니다.

고용일자는 문제 예시와 동일한 형식으로 출력해야 하므로  
`DATE_FORMAT(HIRE_YMD, '%Y-%m-%d')`를 사용합니다.

마지막으로 `ORDER BY HIRE_YMD DESC, DR_NAME ASC`를 사용해  
고용일자는 최신순으로 정렬하고, 고용일자가 같을 경우 의사 이름을 오름차순으로 정렬합니다.

## 정답 코드

```sql
SELECT 
    DR_NAME,
    DR_ID,
    MCDP_CD,
    DATE_FORMAT(HIRE_YMD, '%Y-%m-%d') AS HIRE_YMD
FROM DOCTOR
WHERE MCDP_CD = 'CS'
   OR MCDP_CD = 'GS'
ORDER BY HIRE_YMD DESC, DR_NAME ASC;
