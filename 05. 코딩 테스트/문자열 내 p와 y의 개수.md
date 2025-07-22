---
플랫폼: 프로그래머스
문제 이름: 문자열 내 p와 y의 개수
알고리즘: 문자열
tags:
  - 문자열
date: 2025-07-22
aliases:
  - 문자열
복습 풀이: 250722(O)
---
# 1차 풀이
```java
class Solution {
    boolean solution(String s) {
        String value = s.toLowerCase();
        int pCount = 0;
        int yCount = 0;
        for (char c : value.toCharArray()) {
            if (c == 'p') {
                pCount++;
            } else if (c == 'y') {
                yCount++;
            }
        }
        
        return pCount == yCount;
    }
}
```

```java
public class Solution {
    boolean solution(String s) {
        s = s.toLowerCase();

        int ps = s.length() - s.replace("p", "").length();
        int ys = s.length() - s.replace("y", "").length();
        return ps == ys;
    }
}
```

쉬운 문제이지만 p, y 개수를 세는 방식에서 다른 풀이와 차이가 있음. 두 번째 풀이와 같은 방식을 기억할것