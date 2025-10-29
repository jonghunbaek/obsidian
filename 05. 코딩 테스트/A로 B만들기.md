---
플랫폼: 프로그래머스
문제 이름: A로 B만들기
알고리즘: 해시
tags:
  - 해시
date: 2025-08-21
aliases:
  - 해시
복습 풀이: 250821(O), 250824(O), 251029()
---
# 1차 풀이
```java
class Solution {
    public int solution(String before, String after) {
        Map<Character, Integer> map = new HashMap<>();
        for (char c : before.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
        
        for (char c : after.toCharArray()) {
            if (!map.containsKey(c)) {
                return 0;
            }
            
            int value = map.get(c) - 1;
            if (value < 0) {
                return 0;
            }
            
            map.put(c, value);
        }
        
        return map.values().stream()
            .filter(val -> val > 0)
            .findAny()
            .isPresent() ? 0 : 1;
    }
}
```

```java
public class Solution {
    private static Map<Character, Integer> toMap(String word) {
        Map<Character, Integer> map = new HashMap<>();
        for (char c : word.toCharArray()) {
            map.putIfAbsent(c, 0);
            map.put(c, map.get(c) + 1);
        }
        return map;
    }

    public int solution(String before, String after) {
        return toMap(before).equals(toMap(after)) ? 1 : 0;
    }
}

class Solution {
    public int solution(String before, String after) {
        char[] a = before.toCharArray();
        char[] b = after.toCharArray();
        Arrays.sort(a);
        Arrays.sort(b);

        return new String(a).equals(new String(b)) ? 1 :0;
    }
}
```
더 간단하게 풀 수 있는 다양한 아이디어가 존재함