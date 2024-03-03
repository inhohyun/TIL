# 순열 vs 조합 vs 부분 집합  코드 정리

## 코드 비교
순열, 조합은 재귀 안에 for문을 사용해 원하는 경우의 수를 구하는 방식으로 구현된다.

다만 조합은 start 부분을 지정해주어 그 동안 고르지 않은 다음 값을 고려한다.

부분집합은 선택, 비선택의 구조로 2번 재귀를 구현하는 방식으로 구현된다.
### 순열, 중복 순열
```
    // 순열
    private static void permutation(int cnt) {
        if (cnt == N) {
            System.out.println(Arrays.toString(arr));
            return;
        }
        
        for (int i = 0; i < N; i++) {
            if (!visited[i]) {
                visited[i] = true;
                arr[cnt] = i;
                permutation(cnt+1);
                visited[i] = false;
            }
        }
    }
    // 중복 순열
    private static void permutation_With_Repetition(int cnt) {
        if (cnt == N) {
            System.out.println(Arrays.toString(arr));
            return;
        }
        for (int i = 0; i < N; i++) {
            arr[cnt] = i;
            permutation_With_Repetition(cnt+1);    
        }
    }

```

### 조합
```
    private static void combination(int cnt, int start) {
        if (cnt == N) {
            System.out.println(Arrays.toString(arr));
            return;
        }
        for (int i = start; i < 5; i++) {
            arr[cnt] = i;
            combination(cnt+1, i+1);
        }
        
    }
    
    private static void combination_With_Repetition(int cnt, int start) {
        if (cnt == N) {
            System.out.println(Arrays.toString(arr));
            return;
        }
        for (int i = start; i < 5; i++) {
            arr[cnt] = i;
            combination_With_Repetition(cnt+1, i);
        }
    }

```
### 부분 집합
```
    private static void PowerSet(int cnt, int select) {
        if (cnt == N) {
            for (int i = 0; i < 5; i++) {
                if ((select & 1 << i) != 0) {
                    System.out.print(i + ", ");
                }
            }
            System.out.println();
            return;
        }
        PowerSet(cnt+1, select | 1 << cnt);    
        PowerSet(cnt+1, select);
            
    }

```