---
title: 프로그래머스 SQL 문제 답지 - SUM, MAX, MIN
author: HyeonJaePark
date: 2024-01-23
categories: [Problem Solving, 프로그래머스 SQL]
tags: [MYSQL, 프로그래머스 SQL]
math: true
mermaid: true
render_with_liquid: false
---

{::options parse_block_html="true" /}

본 게시물에서는 [프로그래머스 SQL 고득점 Kit SUM, MAX, MIN](https://school.programmers.co.kr/learn/courses/30/parts/17043){:target="_blank"} 카테고리 문제의 MYSQL 쿼리를 다루고 있습니다.

## 가격이 제일 비싼 식품의 정보 출력하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT *
FROM food_product
ORDER BY price DESC
LIMIT 1;
```
</details>

## 가장 비싼 상품 구하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT price AS max_price
FROM product
ORDER BY price DESC
LIMIT 1;
```
</details>

## 최댓값 구하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT MAX(datetime)
FROM animal_ins;
```
</details>

## 최솟값 구하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT MIN(datetime)
FROM animal_ins;
```
</details>

## 동물 수 구하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT COUNT(DISTINCT animal_id)
FROM animal_ins;
```
</details>

## 중복 제거하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT COUNT(DISTINCT name)
FROM animal_ins
WHERE name IS NOT NULL;
```
</details>

{::options parse_block_html="false" /}
