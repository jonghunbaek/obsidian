---
플랫폼: 프로그래머스
문제 이름: 사칙연산
알고리즘: dp
tags:
  - dp
date: 2025-08-27
aliases:
  - dp
복습 풀이: 250827(X)
---
# 1차 풀이
```java
import java.util.*;

class Solution {
    public int solution(String arr[]) {
        // 숫자와 연산자 분리
        ArrayList<Integer> nums = new ArrayList<>();
        ArrayList<String> ops = new ArrayList<>();

        for (int i = 0; i < arr.length; i++) {
            if (i % 2 == 0) {
                nums.add(Integer.parseInt(arr[i]));
            } else {
                ops.add(arr[i]);
            }
        }

        int n = nums.size();
        
        // DP 테이블 초기화
        // maxDp[i][j]: i번째 숫자부터 j번째 숫자까지의 연산 결과 중 최댓값
        // minDp[i][j]: i번째 숫자부터 j번째 숫자까지의 연산 결과 중 최솟값
        int[][] maxDp = new int[n][n];
        int[][] minDp = new int[n][n];

        for (int i = 0; i < n; i++) {
            Arrays.fill(maxDp[i], Integer.MIN_VALUE);
            Arrays.fill(minDp[i], Integer.MAX_VALUE);
            // 자기 자신으로 초기화 (구간 길이가 1일 때)
            maxDp[i][i] = nums.get(i);
            minDp[i][i] = nums.get(i);
        }

        // DP 테이블 채우기
        // d: 계산할 구간의 길이 (숫자 개수 기준)
        for (int d = 1; d < n; d++) {
            // i: 구간의 시작 인덱스
            for (int i = 0; i < n - d; i++) {
                // j: 구간의 끝 인덱스
                int j = i + d;
                // k: 연산자 위치 (구간을 나누는 기준)
                for (int k = i; k < j; k++) {
                    String op = ops.get(k);

                    if (op.equals("+")) {
                        // '+' 연산일 경우
                        // 최댓값 = (왼쪽 최댓값) + (오른쪽 최댓값)
                        // 최솟값 = (왼쪽 최솟값) + (오른쪽 최솟값)
                        int currentMax = maxDp[i][k] + maxDp[k + 1][j];
                        int currentMin = minDp[i][k] + minDp[k + 1][j];
                        
                        maxDp[i][j] = Math.max(maxDp[i][j], currentMax);
                        minDp[i][j] = Math.min(minDp[i][j], currentMin);
                    } else { // '-' 연산일 경우
                        // 최댓값 = (왼쪽 최댓값) - (오른쪽 최솟값)
                        // 최솟값 = (왼쪽 최솟값) - (오른쪽 최댓값)
                        int currentMax = maxDp[i][k] - minDp[k + 1][j];
                        int currentMin = minDp[i][k] - maxDp[k + 1][j];
                        
                        maxDp[i][j] = Math.max(maxDp[i][j], currentMax);
                        minDp[i][j] = Math.min(minDp[i][j], currentMin);
                    }
                }
            }
        }
        
        // 최종 결과 반환 (0번째부터 마지막 숫자까지의 최댓값)
        return maxDp[0][n - 1];
    }
}
```

```java
public class Solution {
    private interface IntComparator extends Comparator<Integer> {
    }

    private static final IntComparator[] COMP = {
            (a, b) -> Integer.compare(a, b),
            (a, b) -> Integer.compare(b, a),
    };

    private static final int[] INIT = {
            Integer.MIN_VALUE,
            Integer.MAX_VALUE,
    };

    private final int[][][] mem = new int[202][202][2];

    private int compute(int start, int end, int type, String[] arr) {
        if (mem[start][end][type] != Integer.MIN_VALUE) {
            return mem[start][end][type];
        }
        if (end - start == 1) return Integer.parseInt(arr[start]);

        int result = INIT[type];
        for (int i = start + 1; i < end; i += 2) {
            int l = compute(start, i, type, arr);
            int v;
            if (arr[i].equals("+")) {
                int r = compute(i + 1, end, type, arr);
                v = l + r;
            } else {
                int r = compute(i + 1, end, 1 - type, arr);
                v = l - r;
            }

            if (COMP[type].compare(v, result) > 0) result = v;
        }
        return mem[start][end][type] = result;
    }

    public int solution(String[] arr) {
        for (int[][] m : mem) {
            for (int[] row : m) {
                Arrays.fill(row, Integer.MIN_VALUE);
            }
        }

        return compute(0, arr.length, 0, arr);
    }
}
```
전혀 감을 잡지 못하겠음
여러번 반복적으로 읽어보며 풀어보기