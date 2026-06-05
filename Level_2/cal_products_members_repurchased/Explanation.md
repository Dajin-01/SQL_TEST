# 재구매가 일어난 상품과 회원 리스트 구하기

## 문제 설명

ONLINE_SALE 테이블에서 동일한 회원이 동일한 상품을 재구매한 데이터를 구하여, 
재구매한 회원 ID와 재구매한 상품 ID를 출력하는 SQL문을 작성해주세요. 
결과는 회원 ID를 기준으로 오름차순 정렬해주시고 회원 ID가 같다면 상품 ID를 기준으로 내림차순 정렬해주세요.

---

## 테이블 구조

| Column name | Type | Nullable | 설명 |
|---|---|---|---|
| ONLINE_SALE_ID | INTEGER | FALSE | 온라인 상품 판매 ID |
| USER_ID | INTEGER | FALSE | 회원 ID |
| PRODUCT_ID | INTEGER | FALSE | 상품 ID |
| SALES_AMOUNT | INTEGER | FALSE | 판매량 |
| SALES_DATE | DATE | FALSE | 판매일 |

---

## 문제 조건

- 동일한 회원이 동일한 상품을 재구매한 데이터 조회
- `USER_ID`, `PRODUCT_ID`를 기준으로 그룹화
- 같은 조합의 데이터가 2개 이상인 경우만 출력
- 결과는 회원 ID 기준 오름차순 정렬
- 회원 ID가 같다면 상품 ID 기준 내림차순 정렬

---

## 풀이 설명

`USER_ID`와 `PRODUCT_ID`를 기준으로 `GROUP BY`를 사용해  
회원별, 상품별 구매 기록을 하나의 그룹으로 묶습니다.

그다음 `HAVING COUNT(*) >= 2` 조건을 사용해  
같은 회원이 같은 상품을 2번 이상 구매한 경우만 필터링합니다.

마지막으로 `ORDER BY USER_ID ASC, PRODUCT_ID DESC`를 사용해  
회원 ID는 오름차순, 상품 ID는 내림차순으로 정렬합니다.

## 정답 코드

```sql
SELECT 
    USER_ID,
    PRODUCT_ID
FROM ONLINE_SALE
GROUP BY USER_ID, PRODUCT_ID
HAVING COUNT(*) >= 2
ORDER BY USER_ID ASC, PRODUCT_ID DESC;
