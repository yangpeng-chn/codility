[Problem](https://app.codility.com/programmers/lessons/4-counting_elements/missing_integer/)

## Solution 1 - `O(N), O(N)`

Use an extra array to record if the positive numbers appear or not.

+ Task Score: 100%
+ Correctness: 100%
+ Performance: 100%

```c++
int solution(vector<int> &A) {
    int n = (int)A.size();
    vector<bool>t(n, false);
    for (int i = 0; i < n; i++) {
        if (A[i] >= 1 && A[i] <= n) {
            t[A[i] - 1] = true;
        }
    }
    for (int i = 0; i < n; i++) {
        if (!t[i]) return i + 1;
    }
    return n + 1;
}
```

## Solution 2 - `O(N), O(1)`

+ Task Score: 100%
+ Correctness: 100%
+ Performance: 100%

Similar logic with solution 1, but without extra space.

1. Change original array to put A[i] on A[A[i] - 1], i.e. 1:A[0], 2:A[1]
2. Only care about the numbers >=1 and <=n, i.e. if n = 4 => 1,2,3,4

We can not replace `nums[nums[i] - 1] != nums[i])` with `nums[i] != i + 1`, e.g. [1,1]

```
3 4 -1 1
n = 4
i = 0, A[3-1] != A[0] => -1 4 3 1 (put 3 at correct position)
i = 1, A[4-1] != A[1] => -1 1 3 4 (put 4 at correct position)
       A[1-1] != A[1] => 1 -1 3 4 (put 1 at correct position)
i = 2, A[3-1] == A[2] => do nothing
i = 3, A[4-1] == A[3] => do nothing
-1 != 1+1, return 2
if n == 0, return 1
```

```c++
int solution(vector<int> &A) {
    int n = (int)A.size();
    for (int i = 0; i < n; i++) {
        while (A[i] >= 1 && A[i] <= n && A[A[i] - 1] != A[i]) {
            swap(A[i], A[A[i] - 1]);
        }
    }
    for (int i = 0; i < n; i++) {
        if (A[i] != i + 1) return i + 1;
    }
    return n + 1;
}
```