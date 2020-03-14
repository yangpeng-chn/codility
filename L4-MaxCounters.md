[Problem](https://app.codility.com/programmers/lessons/4-counting_elements/max_counters/)

## Solution 1 - `O(M*N), O(1)`

Update each value when `A[K] == N + 1`.

+ Task Score: 77%
+ Correctness: 100%
+ Performance: 60%

```c++
vector<int> solution(int N, vector<int> &A) {
    vector<int>res(N);
    int maxValue = 0;
    for (auto num : A) {
        if (num == N + 1) {
            res.assign(N, maxValue);
        } else {
            res[num-1]++;
            maxValue = max(maxValue, res[num-1]);
        }
    }
    return res;
}
```

## Solution 2 - `O(M+N), O(1)`

+ Task Score: 100%
+ Correctness: 100%
+ Performance: 100%

As N and M are integers within the range [1..100,000], we need a solution with `O(n)` or `O(n log n)`.
Define two max values:

1. maxValue is the maxValue after each operation
2. maxV is the value that should be applied to each element

+ When A[K] != N + 1, we need to update the `res[X]` with `max(res[num-1] + 1, maxV + 1);`
+ The final `for` loop is used to update the counters if the last operation is to update all the counters.

```c++
vector<int> solution(int N, vector<int> &A) {
    vector<int>res(N);
    int maxValue = 0;
    int maxV = 0;
    for (auto num : A) {
        if (num == N + 1) {
            maxV = maxValue;
        } else {
            res[num-1] = max(res[num-1] + 1, maxV + 1);
            maxValue = max(maxValue, res[num-1]);
        }
    }
    for (auto & num : res) 
        num = max(num, maxV);
    return res;
}
```
