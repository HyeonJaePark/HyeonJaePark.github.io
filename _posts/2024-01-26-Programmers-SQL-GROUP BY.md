---
title: 프로그래머스 SQL 문제 답지 - GROUP BY
author: HyeonJaePark
date: 2024-01-26
categories: [Problem Solving, 프로그래머스 SQL]
tags: [MYSQL, 프로그래머스 SQL]
math: true
mermaid: true
render_with_liquid: false
---

{::options parse_block_html="true" /}

본 게시물에서는 [프로그래머스 SQL 고득점 Kit GROUP BY](https://school.programmers.co.kr/learn/courses/30/parts/17044){:target="_blank"} 카테고리 문제의 MYSQL 쿼리를 다루고 있습니다.

## 즐겨찾기가 가장 많은 식당 정보 출력하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT
    ri.food_type,
    ri.rest_id,
    ri.rest_name,
    ri.favorites
FROM rest_info ri
JOIN 
    (
        SELECT 
            food_type,
            MAX(favorites) AS favorites
        FROM rest_info
        GROUP BY food_type
    ) fr
ON ri.food_type = fr.food_type
WHERE ri.favorites = fr.favorites
ORDER BY ri.food_type DESC;
```
</details>

## 조건에 맞는 사용자와 총 거래금액 조회하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT 
    u.user_id, 
    u.nickname, 
    SUM(price) AS total_sales
FROM used_goods_board b
JOIN used_goods_user u
ON b.writer_id = u.user_id
WHERE b.status = "DONE"
GROUP BY b.writer_id
HAVING SUM(price) >= 700000
ORDER BY total_sales;
```
</details>

## 저자 별 카테고리 별 매출액 집계하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT
    author_id,
    author_name,
    category,
    SUM(sales * price) AS total_sales
FROM book_sales bs
JOIN (
    SELECT 
        b.*, 
        a.author_name
    FROM book b
    JOIN author a
    ON b.author_id = a.author_id
) x
on bs.book_id = x.book_id
WHERE LEFT(bs.sales_date, 7) = "2022-01"
GROUP BY author_id, category
ORDER BY author_id, category DESC;
```
</details>

## 카테고리 별 도서 판매량 집계하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT 
    category,
    SUM(sales) AS total_sales
FROM book b
JOIN book_sales bs
ON b.book_id = bs.book_id
WHERE LEFT(bs.sales_date, 7) = "2022-01"
GROUP BY category
ORDER BY category;
```
</details>

## 자동차 대여 기록에서 대여중 / 대여 가능 여부 구분하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT
    DISTINCT c.car_id,
    IF(ISNULL(rented.car_id), "대여 가능", "대여중") AS availability
FROM car_rental_company_rental_history c
LEFT JOIN (
    SELECT car_id
    FROM car_rental_company_rental_history
    WHERE "2022-10-16" BETWEEN start_date AND end_date
    GROUP BY car_id
) rented
ON c.car_id = rented.car_id
ORDER BY c.car_id DESC;
```
</details>

## 진료과별 총 예약 횟수 출력하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT
    MCDP_CD AS "진료과코드",
    COUNT(DISTINCT PT_NO) AS "5월예약건수"
FROM appointment
WHERE LEFT(APNT_YMD, 7) = "2022-05"
GROUP BY MCDP_CD
ORDER BY 5월예약건수, 진료과코드;
```
</details>

## 자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT
    car_type,
    COUNT(car_id) AS cars
FROM car_rental_company_car
WHERE OPTIONS REGEXP "통풍시트|열선시트|가죽시트"
GROUP BY car_type
ORDER BY car_type
```
</details>

## 대여 횟수가 많은 자동차들의 월별 대여 횟수 구하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT
    MONTH(c.start_date) AS month,
    c.car_id,
    COUNT(*) AS records
FROM car_rental_company_rental_history c
JOIN (
    SELECT car_id
    FROM car_rental_company_rental_history
    WHERE (start_date BETWEEN DATE('2022-08-01') AND DATE('2022-11-01'))
    GROUP BY car_id
    HAVING COUNT(*) >= 5
) x
ON c.car_id = x.car_id
WHERE (start_date BETWEEN DATE('2022-08-01') AND DATE('2022-11-01'))
GROUP BY c.car_id, MONTH(c.start_date)
HAVING COUNT(*) > 0
ORDER BY month, c.car_id DESC;
```
</details>

## 성분으로 구분한 아이스크림 총 주문량

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT
    ii.ingredient_type,
    SUM(fh.total_order) AS total_order
FROM first_half fh
JOIN icecream_info ii
ON fh.flavor = ii.flavor
GROUP BY ii.ingredient_type
ORDER BY total_order;
```
</details>

## 식품분류별 가장 비싼 식품의 정보 조회하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT
    category,
    max_price,
    product_name
FROM (
    SELECT
        category,
        price AS max_price,
        product_name,
        ROW_NUMBER() OVER (PARTITION BY category ORDER BY price DESC) AS rn
    FROM food_product
    WHERE category IN ('과자', '국', '김치', '식용유')
) X
WHERE X.rn = 1
ORDER BY max_price DESC;
```
</details>

## 고양이와 개는 몇 마리 있을까

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT 
    animal_type, 
    COUNT(ANIMAL_TYPE) AS ani_count
FROM animal_ins
GROUP BY animal_type
ORDER BY animal_type ASC;
```
</details>

## 동명 동물 수 찾기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT 
    name, 
    COUNT(NAME) AS name_count
FROM animal_ins
GROUP BY name
HAVING COUNT(name) > 1
ORDER BY name;
```
</details>

## 년, 월, 성별 별 상품 구매 회원 수 구하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT
    YEAR(sales_date) AS year,
    MONTH(sales_date) AS month,
    gender,
    COUNT(DISTINCT s.user_id) AS users
FROM online_sale s
LEFT JOIN user_info u
ON s.user_id = u.user_id
WHERE u.gender IS NOT NULL
GROUP BY YEAR(sales_date), MONTH(sales_date), gender
ORDER BY YEAR(sales_date), MONTH(sales_date), gender;
```
</details>

## 입양 시각 구하기(1)

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT 
    HOUR(datetime), 
    COUNT(1)
FROM animal_outs
WHERE 9 <= HOUR(datetime) AND 
HOUR(datetime) < 20
GROUP BY 1
ORDER BY 1;
```
</details>

## 입양 시각 구하기(2)

<details><summary markdown="span">접기/펼치기</summary>
```sql
SET @hour := -1;

SELECT
    (@hour := @hour + 1) AS hour,
    (
        SELECT COUNT(1)
        FROM animal_outs
        WHERE HOUR(datetime) = @hour
    ) AS COUNT
FROM animal_outs
WHERE @hour < 23;
```
</details>

## 가격대 별 상품 개수 구하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT
    (price_group * 10000) AS price_group,
    COUNT(product_id) AS products
FROM (
    SELECT
        *,
        FLOOR((price / 10000)) as price_group
    FROM product
) X
GROUP BY price_group
ORDER BY price_group;
```
</details>

{::options parse_block_html="false" /}
