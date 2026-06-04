# 자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기

## 문제 설명

`CAR_RENTAL_COMPANY_CAR` 테이블에서 자동차 종류가 `SUV`인 자동차들의 평균 일일 대여 요금을 출력하는 문제입니다.

평균 일일 대여 요금은 **소수 첫 번째 자리에서 반올림**해야 하며, 결과 컬럼명은 `AVERAGE_FEE`로 지정해야 합니다.

---

## 테이블 구조

| Column name | Type | Nullable | 설명 |
|---|---|---|---|
| CAR_ID | INTEGER | FALSE | 자동차 ID |
| CAR_TYPE | VARCHAR(255) | FALSE | 자동차 종류 |
| DAILY_FEE | INTEGER | FALSE | 일일 대여 요금 |
| OPTIONS | VARCHAR(255) | FALSE | 자동차 옵션 리스트 |

---

## 문제 조건

- 자동차 종류가 `SUV`인 데이터만 조회
- `DAILY_FEE`의 평균값 계산
- 평균값은 소수 첫 번째 자리에서 반올림
- 컬럼명은 `AVERAGE_FEE`로 지정

---


