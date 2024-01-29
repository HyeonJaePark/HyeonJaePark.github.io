---
title: 프로그래머스 PS 데이터 분석
author: HyeonJaePark
date: 2024-01-29
categories: [Problem Solving, Programmers PS]
tags: [코딩테스트, 프로그래머스 PS, 정렬]
math: true
mermaid: true
render_with_liquid: false
---

PCCE 기출문제인 [데이터 분석](https://school.programmers.co.kr/learn/courses/30/lessons/250121){:target="_blank"} 을 다루고 있습니다.  

## Solution 1 using stream, filter
```java
import java.util.*;

class Solution {
    public int convertStringToInt(String token) {
        switch (token) {
            case "code":
                return 0;
            case "date":
                return 1;
            case "maximum":
                return 2;
            case "remain":
                return 3;
            default:
                return -1;
        }
    }

    public int[][] solution(int[][] data, String ext, int val_ext, String sort_by) {
        final int finalExtByIdx = convertStringToInt(ext);
        final int finalSortByIdx = convertStringToInt(sort_by);

        Arrays.sort(data, Comparator.comparingInt(arr -> arr[finalSortByIdx]));

        int[][] answer = Arrays.stream(data)
                .filter(row -> row[finalExtByIdx] <= val_ext)
                .toArray(int[][]::new);

        return answer;
    }
}
```


## Solution 2 using for-loop
```java
import java.util.*;

class Solution {
    public int convertStringToInt(String token) {
        switch (token) {
            case "code":
                return 0;
            case "date":
                return 1;
            case "maximum":
                return 2;
            case "remain":
                return 3;
            default:
                return -1;
        }
    }

    public int[][] solution(int[][] data, String ext, int val_ext, String sort_by) {
        final int finalExtByIdx = convertStringToInt(ext);
        final int finalSortByIdx = convertStringToInt(sort_by);

        Arrays.sort(data, Comparator.comparingInt(arr -> arr[finalSortByIdx]));

        List<int[]> filteredData = new ArrayList<>();
        for (int[] row: data) {
            if (row[finalExtByIdx] <= val_ext) {
                filteredData.add(row);
            }
        }

        int[][] answer = new int[filteredData.size()][];
        for (int i = 0; i < filteredData.size(); i++) {
            answer[i] = filteredData.get(i);
        }

        return answer;
    }
}
```

배열과 정렬을 통해서 문제를 해결했습니다.  
배열에 data를 저장하고 ext와 sort_by 문자열을 해당되는 배열 인덱스로 변환하여 정렬하여 풀었습니다.   
첫번째 코드의 경우, stream과 filter를 사용해서 코드를 간결하게 표현했습니다.  
두번째 코드의 경우, for-loop를 사용했습니다.  
stream과 filter 내부의 연산이 간단하여 for-loop보다는 시간이 조금 더 걸리지만 문제를 풀 수 있습니다.  
