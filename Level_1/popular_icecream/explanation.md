# 상반기 아이스크림 총주문량 정렬하기

## 문제 설명

`FIRST_HALF` 테이블은 아이스크림 가게의 상반기 주문 정보를 담고 있는 테이블입니다.

이 문제는 상반기에 판매된 아이스크림의 맛을 조회하되,  
총주문량이 많은 순서대로 정렬하고, 총주문량이 같은 경우에는 출하 번호가 작은 순서대로 정렬하는 문제입니다.

---

## 테이블 구조

| 컬럼명 | 타입 | NULL 허용 | 설명 |
|---|---|---|---|
| SHIPMENT_ID | INT | FALSE | 출하 번호 |
| FLAVOR | VARCHAR | FALSE | 아이스크림 맛 |
| TOTAL_ORDER | INT | FALSE | 상반기 총주문량 |

---

## 문제 조건

- 조회할 컬럼은 아이스크림 맛인 `FLAVOR`
- 총주문량 `TOTAL_ORDER`를 기준으로 내림차순 정렬
- 총주문량이 같은 경우 `SHIPMENT_ID`를 기준으로 오름차순 정렬

---

## 풀이 설명

`FIRST_HALF` 테이블에서 아이스크림 맛인 `FLAVOR`만 조회합니다.

```sql
SELECT FLAVOR
FROM FIRST_HALF
```

이후 `ORDER BY`를 사용해 정렬합니다.

```sql
ORDER BY TOTAL_ORDER DESC, SHIPMENT_ID ASC;
```

- `TOTAL_ORDER DESC` : 총주문량이 많은 순서대로 정렬
- `SHIPMENT_ID ASC` : 총주문량이 같으면 출하 번호가 작은 순서대로 정렬

따라서 최종 SQL은 다음과 같습니다.

```sql
SELECT FLAVOR
FROM FIRST_HALF
ORDER BY TOTAL_ORDER DESC, SHIPMENT_ID ASC;
```
