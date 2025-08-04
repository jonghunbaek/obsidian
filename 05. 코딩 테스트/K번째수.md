---
플랫폼: 프로그래머스
문제 이름: K번째수
알고리즘: 정렬
tags:
  - 정렬
date: 2025-08-04
aliases:
  - 정렬
복습 풀이: 250804(O)
---
# 1차 풀이
```java
import java.util.*;

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        List<Integer> results = new ArrayList<>();
        
        for (int[] command : commands) {
            int[] target = Arrays.copyOfRange(array, command[0] - 1, command[1]);
            Arrays.sort(target);
            results.add(target[command[2] - 1]);
        }
        
        return results.stream()
            .mapToInt(Integer::intValue)
            .toArray();
    }
}
```
