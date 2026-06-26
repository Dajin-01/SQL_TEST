# SQL 문제 풀이 - 희귀도 LEGEND 아이템 가격 총합 구하기

## 문제 설명

`ITEM_INFO` 테이블에서 희귀도가 `LEGEND`인 아이템들의 가격 총합을 구하는 문제입니다.

조회 결과의 컬럼명은 반드시 `TOTAL_PRICE`로 지정해야 합니다.

---

## 테이블 구조

| Column name | Type       | Nullable | 설명      |
| ----------- | ---------- | -------- | ------- |
| ITEM_ID     | INTEGER    | FALSE    | 아이템 ID  |
| ITEM_NAME   | VARCHAR(N) | FALSE    | 아이템 명   |
| RARITY      | VARCHAR(N) | FALSE    | 아이템 희귀도 |
| PRICE       | INTEGER    | FALSE    | 아이템 가격  |

---

## 문제 조건

* `ITEM_INFO` 테이블에서 데이터를 조회
* 희귀도(`RARITY`)가 `LEGEND`인 아이템만 필터링
* 해당 아이템들의 가격(`PRICE`)을 모두 합산
* 결과 컬럼명은 `TOTAL_PRICE`로 지정

---

## 풀이 설명

이 문제는 **WHERE 조건절과 SUM 집계 함수를 사용하는 문제**입니다.

먼저 `WHERE`절을 사용해 희귀도가 `LEGEND`인 아이템만 필터링합니다.

```sql
WHERE RARITY = 'LEGEND'
```

그다음 `SUM(PRICE)`를 사용해 조건에 해당하는 아이템들의 가격을 모두 더합니다.

```sql
SUM(PRICE)
```

마지막으로 문제에서 요구한 컬럼명인 `TOTAL_PRICE`를 지정하기 위해 `AS`를 사용합니다.

```sql
SUM(PRICE) AS TOTAL_PRICE
```

---

## 정답 코드

```sql
SELECT 
    SUM(PRICE) AS TOTAL_PRICE
FROM ITEM_INFO
WHERE RARITY = 'LEGEND';
```

---

## 핵심 개념 정리

| SQL 문법                    | 역할                        |
| ------------------------- | ------------------------- |
| `WHERE RARITY = 'LEGEND'` | 희귀도가 `LEGEND`인 아이템만 필터링   |
| `SUM(PRICE)`              | 조건에 맞는 아이템 가격의 총합 계산      |
| `AS TOTAL_PRICE`          | 결과 컬럼명을 `TOTAL_PRICE`로 지정 |

---

## 정리

이 문제의 핵심은 **조건에 맞는 행만 먼저 필터링한 뒤, 가격을 합산하는 것**입니다.

따라서 `WHERE`절로 `RARITY = 'LEGEND'` 조건을 걸고,
`SUM(PRICE)`를 사용해 가격 총합을 구하면 됩니다.
