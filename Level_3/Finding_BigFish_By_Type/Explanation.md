# [SQL] 물고기 종류별 가장 큰 물고기 조회

## 문제 설명

`FISH_INFO` 테이블에는 잡은 물고기의 정보가 저장되어 있고,
`FISH_NAME_INFO` 테이블에는 물고기 종류별 이름 정보가 저장되어 있다.

이 문제는 **물고기 종류별로 가장 큰 물고기 1마리의 ID, 물고기 이름, 길이**를 조회하는 문제이다.

출력해야 하는 컬럼은 다음과 같다.

| 컬럼명       | 설명     |
| --------- | ------ |
| ID        | 물고기 ID |
| FISH_NAME | 물고기 이름 |
| LENGTH    | 물고기 길이 |

결과는 `ID`를 기준으로 오름차순 정렬해야 한다.

---

## 테이블 구조

### FISH_INFO

| Column name | Type    | Nullable | 설명         |
| ----------- | ------- | -------- | ---------- |
| ID          | INTEGER | FALSE    | 잡은 물고기의 ID |
| FISH_TYPE   | INTEGER | FALSE    | 물고기의 종류    |
| LENGTH      | FLOAT   | TRUE     | 물고기의 길이    |
| TIME        | DATE    | FALSE    | 물고기를 잡은 날짜 |

### FISH_NAME_INFO

| Column name | Type    | Nullable | 설명      |
| ----------- | ------- | -------- | ------- |
| FISH_TYPE   | INTEGER | FALSE    | 물고기의 종류 |
| FISH_NAME   | VARCHAR | FALSE    | 물고기의 이름 |

---

## 문제 조건

* 물고기 종류별로 가장 큰 물고기를 조회한다.
* `ID`, `FISH_NAME`, `LENGTH`를 출력한다.
* `FISH_INFO`와 `FISH_NAME_INFO`를 `FISH_TYPE` 기준으로 연결한다.
* 결과는 `ID` 기준 오름차순 정렬한다.
* 물고기 종류별 가장 큰 물고기는 1마리만 존재한다.
* 10cm 이하의 물고기가 가장 큰 경우는 없으므로, 최대 길이는 `NULL`이 아니다.

---

## 풀이 설명

먼저 `FISH_INFO` 테이블에서 `FISH_TYPE`별 최대 길이를 구한다.

```sql
SELECT 
    FISH_TYPE,
    MAX(LENGTH) AS MAX_LENGTH
FROM FISH_INFO
GROUP BY FISH_TYPE
```

이 결과는 물고기 종류별 가장 긴 길이만 가지고 있으므로,
해당 길이를 가진 실제 물고기의 `ID`를 찾기 위해 원본 테이블인 `FISH_INFO`와 다시 `JOIN`한다.

```sql
ON F.FISH_TYPE = M.FISH_TYPE
AND F.LENGTH = M.MAX_LENGTH
```

그다음 `FISH_NAME_INFO` 테이블과 `FISH_TYPE` 기준으로 연결하여 물고기 이름을 가져온다.

마지막으로 문제 조건에 따라 `ID` 기준 오름차순으로 정렬한다.

---

## 정답 코드

```sql
SELECT
    F.ID,
    N.FISH_NAME,
    F.LENGTH
FROM FISH_INFO F
JOIN (
    SELECT 
        FISH_TYPE,
        MAX(LENGTH) AS MAX_LENGTH
    FROM FISH_INFO
    GROUP BY FISH_TYPE
) M
    ON F.FISH_TYPE = M.FISH_TYPE
   AND F.LENGTH = M.MAX_LENGTH
JOIN FISH_NAME_INFO N
    ON F.FISH_TYPE = N.FISH_TYPE
ORDER BY F.ID ASC;
```

---

## 핵심 개념 정리

| SQL 문법               | 역할                            |
| -------------------- | ----------------------------- |
| `GROUP BY FISH_TYPE` | 물고기 종류별로 그룹화                  |
| `MAX(LENGTH)`        | 각 물고기 종류에서 가장 긴 길이 계산         |
| 서브쿼리                 | 종류별 최대 길이 결과를 임시 테이블처럼 사용     |
| `JOIN`               | 최대 길이를 가진 실제 물고기 정보와 이름 정보 연결 |
| `ORDER BY F.ID ASC`  | 물고기 ID 기준 오름차순 정렬             |

---

## 주의할 점

아래와 같이 작성하면 정확한 정답이 되기 어렵다.

```sql
SELECT 
    ID,
    FISH_TYPE,
    MAX(LENGTH)
FROM FISH_INFO
GROUP BY FISH_TYPE;
```

이 쿼리는 `FISH_TYPE`별 최대 길이는 구할 수 있지만,
그 최대 길이를 가진 물고기의 정확한 `ID`를 안정적으로 가져오지 못한다.

따라서 먼저 종류별 최대 길이를 구한 뒤,
그 최대 길이와 일치하는 원본 데이터를 다시 찾아야 한다.

---

## 정리

이 문제의 핵심은 **물고기 종류별 최대 길이를 구한 뒤, 그 최대 길이를 가진 실제 물고기 행을 다시 찾는 것**이다.

따라서 `GROUP BY`와 `MAX()`로 종류별 최대 길이를 구하고,
그 결과를 `FISH_INFO`와 다시 `JOIN`하여 물고기 ID를 가져온 뒤,
`FISH_NAME_INFO`와 연결해 물고기 이름을 출력하면 된다.
