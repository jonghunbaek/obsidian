---
플랫폼: 프로그래머스
알고리즘: 구현, 완전탐색
tags:
  - 구현
  - 완전탐색
date: 2026-02-13
복습 풀이: 260213(O), 260216(O), 260226(O)
---
# 1차 풀이
```java
import java.util.*;

class Solution {
    public int solution(int n) {
        boolean[] isPrime = new boolean[n + 1];
        Arrays.fill(isPrime, true);
        isPrime[0] = false;
        isPrime[1] = false;
        
        for (int i = 2; i * i <= n; i++) {
            if (!isPrime[i]) continue;
            for (int j = i + i; j <= n; j += i) {
                isPrime[j] = false;
            }
        }
        
        int count = 0;
        for (int i = 0; i < isPrime.length; i++) {
            if (isPrime[i]) count++;
        }
        return count;
    }
}
```
- 연관 문제 [[소수 찾기]]를 풀어 차이점 확실히 인지하기

# 2차 풀이
```java
import java.util.*;

class Solution {
    public int solution(int n) {
        boolean[] isPrime = new boolean[n + 1];
        Arrays.fill(isPrime, true);
        isPrime[0] = false;
        isPrime[1] = false;
        for (int i = 2; i * i <= isPrime.length; i++) {
            for (int j = i + i; j < isPrime.length; j += i) {
                isPrime[j] = false;
            }
        }
        
        int answer = 0;
        for (int i = 0; i < isPrime.length; i++) {
            if (isPrime[i]) answer++;
        }
        return answer;
    }
}
```

# 3차 풀이
```java
import java.util.*;

class Solution {
    public int solution(int n) {
        boolean[] isPrime = new boolean[n + 1];
        Arrays.fill(isPrime, true);
        isPrime[0] = false;
        isPrime[1] = false;
        for(int i = 2; i * i <= n; i++) {
            for (int j = i + i; j <= n; j += i) {
                isPrime[j] = false;
            }
        }
        
        int answer = 0;
        for (int i = 1; i <= n; i++) {
            if (isPrime[i]) answer++;
        }
        
        return answer;
    }
}
```