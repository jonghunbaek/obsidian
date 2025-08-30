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
복습 풀이: 250805(X), 250816(X), 250823(O), 250830(O)
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

## 2차 풀이
```java
import java.util.*;

class Solution {
    // 0, 1, 3, 5, 6
    // 0, 1, 2, 3, 4
    public int solution(int[] citations) {
        Arrays.sort(citations);
        int result = 0;
        for (int i = 0; i < citations.length; i++) {
            int hIndex = citations.length - i;
            if (citations[i] >= hIndex) {
                result = hIndex;
                break;
            }
        }
        
        return result;
    }
}
```
컨디션 난조로 지문 이해도가 떨어져 또 틀림 

# 3차 풀이
```java
import java.util.*;

class Solution {
    public int solution(int[] citations) {
        Arrays.sort(citations);
        int hIndex = 0;
        for (int i = 0; i < citations.length; i++) {
            int h = citations.length - i;
            if (citations[i] >= h) {
                hIndex = h;
                break;
            }
        }
        return hIndex;
    }
}
```
다시 풀어보니 핵심은 h값을 구할 때, citations\[i] - i로 하던가 citations\[i]하던가 둘 중 하나로 선택할 수 있음
citations\[i]로 할 경우엔, 아래와 같은 예외 케이스가 생길 수 있기 때문에 첫 번째 방식으로 구해줘야 함
```java
[0, 1, 3, 5, 7, 9, 11, 12, 13, 14]
```
위와 같은 입력 값의 경우, 정답은 5가 아닌 6이 됨 그러므로 첫 번째 방식을 써야함

# 4차 풀이
```java
import java.util.*;

class Solution {
    public int solution(int[] citations) {
        Arrays.sort(citations);
        int hIndex = 0;
        for (int i = 0; i < citations.length; i++) {
            int target = citations.length - i;
            if (citations[i] >= target) {
                hIndex = target;
                break;
            }
        }
        
        return hIndex;
    }
}
```