---
title: 프로그래머스 SQL 문제 답지 - IS NULL
author: HyeonJaePark
date: 2024-01-23
categories: [Problem Solving, 프로그래머스 SQL]
tags: [MYSQL, 프로그래머스 SQL]
math: true
mermaid: true
render_with_liquid: false
---

{::options parse_block_html="true" /}

본 게시물에서는 [프로그래머스 SQL 고득점 Kit IS NULL](https://school.programmers.co.kr/learn/courses/30/parts/17045){:target="_blank"} 카테고리 문제의 MYSQL 쿼리를 다루고 있습니다.

## 경기도에 위치한 식품창고 목록 출력하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT
    warehouse_id,
    warehouse_name,
    address,
    IFNULL(freezer_yn, "N") AS freezer_yn
FROM food_warehouse
WHERE LEFT(address, 2) = "경기"
ORDER BY warehouse_id;
```
</details>

## 이름이 없는 동물의 아이디

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT animal_id
FROM animal_ins
WHERE name IS NULL;
```
</details>

## 이름이 있는 동물의 아이디

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT animal_id
FROM animal_ins
WHERE name IS NOT NULL;
```
</details>

## NULL 처리하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT animal_type, IFNULL(anme, 'No name'), sex_upon_intake
FROM animal_ins
ORDER BY animal_id;
```
</details>

## 나이 정보가 없는 회원 수 구하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT COUNT(*) AS users
FROM user_info
WHERE age IS NULL;
```
</details>

{::options parse_block_html="false" /}
