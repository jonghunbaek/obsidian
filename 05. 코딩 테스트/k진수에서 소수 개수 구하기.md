---
플랫폼: 프로그래머스
문제 이름: k진수에서 소수 개수 구하기
알고리즘: 문자열
tags:
  - 문자열
date: 2025-11-18
aliases:
  - 문자열
복습 풀이: 251118(O)
---
# 1차 풀이
```java
// 1. 문자열 문제
// 2. n을 k진수로 변환
// 3. 문자열을 0으로 split
// 4. split 배열을 순회하며, 소수 여부를 판단

class Solution {
    public int solution(int n, int k) {
        String target = Integer.toString(n, k);
        String[] split = target.split("0+");
        int count = 0;
        for (String s : split) {
            if (isPrime(Long.parseLong(s))) count++;
        }
        
        return count;
    }
    
    private boolean isPrime(long target) {
        if (target <= 1) return false;
        
        for (int i = 2; i <= Math.sqrt(target); i++) {
            if (target % i == 0) return false;
        }
        
        return true;
    }
}
```
풀이 자체는 어렵지 않았으며, 약 15분정도 소요됨
다만, 테케가 없었다면 쉽게 정답을 맞추지 못했을 것으로 보임
- 0을 기준으로 분리 시, 0이 연속된 경우 빈 값으로 숫자를 변환해 에러가 발생
- isPrime에 최초엔 int타입으로 인자를 전달했으나 계속 런타임 에러가 발생해 long 타입으로 변경
	- 기본 테케는 통과했으나 채점시 2개의 테케에서 런타임 에러가 발생해 해당 부분이 원인일 것이라 판단
