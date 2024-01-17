---
title: 프로그래머스 SQL 문제 답지
author: HyeonJaePark
date: 2024-01-17
categories: [Problem Solving, 프로그래머스 SQL]
tags: [MYSQL, 프로그래머스 SQL]
math: true
mermaid: true
render_with_liquid: false
---

{::options parse_block_html="true" /}

본 게시물에서는 프로그래머스 SQL 문제의 MYSQL 쿼리를 다루고 있습니다.

## 12세 이하인 여자 환자 목록 출력하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT PT_NAME, PT_NO, GEND_CD, AGE, IFNULL(TLNO, "NONE") AS TLNO
FROM PATIENT
WHERE AGE <= 12 AND GEND_CD = 'W'
ORDER BY AGE DESC, PT_NAME;
```
</details>

## 3월에 태어난 여성 회원 목록 출력하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT MEMBER_ID, MEMBER_NAME, GENDER, DATE_FORMAT(DATE_OF_BIRTH, "%Y-%m-%d") AS DATE_OF_BIRTH
FROM MEMBER_PROFILE
WHERE MONTH(DATE_OF_BIRTH) = 3 AND GENDER = 'W' AND TLNO IS NOT NULL
ORDER BY MEMBER_ID;
```
</details>

## 흉부외과 또는 일반외과 의사 목록 출력하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT DR_NAME, DR_ID, MCDP_CD, DATE_FORMAT(HIRE_YMD, "%Y-%m-%d") AS HIRE_YMD
FROM DOCTOR
WHERE MCDP_CD IN ("CS", "GS")
ORDER BY HIRE_YMD DESC, DR_NAME;
```
</details>

## 서울에 위치한 식당 목록 출력하기

<details><summary markdown="span">접기/펼치기</summary>
```sql
SELECT RI.REST_ID, REST_NAME, FOOD_TYPE, FAVORITES, ADDRESS, ROUND(AVG(REVIEW_SCORE), 2) AS REVIEW_SCORE
FROM REST_INFO RI
JOIN REST_REVIEW RV
ON RI.REST_ID = RV.REST_ID
WHERE LEFT(ADDRESS, 2) = "서울"
GROUP BY RI.REST_ID
ORDER BY REVIEW_SCORE DESC, FAVORITES DESC;
```
</details>

{::options parse_block_html="false" /}
