---
title: 프로그래머스 PS 가장 많이 받은 선물
author: HyeonJaePark
date: 2024-01-27
categories: [Problem Solving, 2024 카카오 인턴쉽, Programmers PS]
tags: [코딩테스트, 프로그래머스 PS, 2024 Kakao Internship, 2024 카카오 코테]
math: true
mermaid: true
render_with_liquid: false
---

2024 카카오 인턴쉽 코딩테스트 1번 문항 [가장 많이 받은 선물](https://school.programmers.co.kr/learn/courses/30/lessons/258712#qna){:target="_blank"} 을 다루고 있습니다.  


```java
import java.util.*;

class Solution {
    public int solution(String[] friends, String[] gifts) {
        int answer = 0;
        
        Map<String, Integer> giftScore = new HashMap<>();
        Map<String, Map<String, Integer>> history = new HashMap<>();
        Map<String, Integer> results = new HashMap<>();
        
        for (String friend : friends) {
            giftScore.put(friend, 0);
            history.put(friend, new HashMap<>());
            results.put(friend, 0);
        }

        for (String giver : friends) {
            Map<String, Integer> giverToReceiverMap = history.get(giver);

            for (String receiver : friends) {
                if (giver.equals(receiver)) continue;
                giverToReceiverMap.put(receiver, 0);
            }
        }
        
        for (String gift : gifts) {
            String[] tokens = gift.split(" ");
            String giver = tokens[0];
            String receiver = tokens[1];

            // Update giftScore
            giftScore.put(giver, giftScore.get(giver) + 1);
            giftScore.put(receiver, giftScore.get(receiver) - 1);

            // Update history
            Map<String, Integer> giverToReceiverMap = history.get(giver);
            giverToReceiverMap.put(receiver, giverToReceiverMap.get(receiver) + 1);
        }

        for (int i = 0; i < friends.length - 1; i++) {
            String giver = friends[i];
            Map<String, Integer> giverToReceiverMap = history.get(giver);

            for (int j = i + 1; j < friends.length; j++) {
                String receiver = friends[j];
                Map<String, Integer> receiverToGiverMap = history.get(receiver);

                int giverToReceiverCount = giverToReceiverMap.get(receiver);
                int receiverToGiverCount = receiverToGiverMap.get(giver);

                if (giverToReceiverCount == receiverToGiverCount) {
                    int giverGiftScore = giftScore.get(giver);
                    int receiverGiftScore = giftScore.get(receiver);

                    if (giverGiftScore > receiverGiftScore) {
                        results.put(giver, results.get(giver) + 1);
                    }
                    else if (giverGiftScore < receiverGiftScore) {
                        results.put(receiver, results.get(receiver) + 1);
                    }
                }
                else if (giverToReceiverCount > receiverToGiverCount) {
                    results.put(giver, results.get(giver) + 1);
                }
                else if (giverToReceiverCount < receiverToGiverCount) {
                    results.put(receiver, results.get(receiver) + 1);
                }
            }
        }

        for (int giftCount : results.values()) {
            answer = Math.max(answer, giftCount);
        }
        
        return answer;
    }
}
```

Map 자료구조를 사용해서 풀 수 있습니다. 특별한 알고리즘 없이 문제의 조건을 그대로 구현하면 됩니다.  
파이썬의 경우 Dictionary를 사용하면 풀 수 있습니다.  
