---
title: 프로그래머스 PS 이웃한 칸
author: HyeonJaePark
date: 2024-01-30
categories: [Problem Solving, Programmers PS]
tags: [코딩테스트, 프로그래머스 PS]
math: true
mermaid: true
render_with_liquid: false
---

PCCE 기출문제인 [이웃한 칸](https://school.programmers.co.kr/learn/courses/30/lessons/250125){:target="_blank"} 을 다루고 있습니다.  

```java
import java.util.*;

class Solution {
    public int solution(String[][] board, int h, int w) {
        int[] dxs = {0, 0, -1, 1};
        int[] dys = {-1, 1, 0, 0};
        
        int answer = 0;
        String color = board[h][w];
        int n = board.length;

        for (int i = 0; i < 4; i++) {
            int ch = h + dxs[i];
            int cw = w + dys[i];

            if (0 <= ch && ch < n && 0 <= cw && cw < n) {
                if (board[ch][cw].equals(color)) answer++;
            }
        }

        return answer;
    }
}
```

BFS나 DFS에서 자주 쓰이는 알고리즘입니다.  
본 문제에서는 인접한 3개의 칸만 확인하지만 문제를 확장하면 BFS, DFS 문제가 될 수 있습니다.  
