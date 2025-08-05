---
플랫폼: 프로그래머스
문제 이름: H-Index
알고리즘: 정렬, 구현
tags:
  - 정렬
  - 구현
date: 2025-08-05
aliases:
  - 정렬
복습 풀이: 250805()
---
# 1차 풀이
```java
class Solution {
	public int solution(int[] citations) {  
	    Arrays.sort(citations);  
	    int result = -1;  
	    int hIndex = 0;  
	    int index = 0;  
	    while (index < citations.length) {  
	        hIndex = citations[index];  
	        int rightLength = citations.length - index;  
	        if (hIndex <= rightLength) { // h번 이상 인용된 논문이 h개 이상이고, 나머지 논문이 h번 이하 인용된 경우  
	            result = Math.max(result, hIndex);  
	        }  
	  
	        index++;  
	    }  
	  
	    return result;  
	}
}
```
```java
class Solution {
    public int solution(int[] citations) {
        Arrays.sort(citations);
        int answer = 0;
        for (int i = 0; i < citations.length; i++) {
            int h = citations.length - i;
            if (citations[i] >= h) {
                answer = h;
                break;
            }
        }
        
        return answer;
    }
}
```
반례를 찾지 못해 결국 정답을 다시 봐야했음
아무래도 문제의 조건을 정확히 이해하지 못한 것이 패착인듯함
h번 이상 인용된 논문이 h편 이상이라는 조건에서 'h번 이상'을 citations의 원소로만 한정한 것이 문제였음

