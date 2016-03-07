001.Two_Sum (Medium)

链接：

题目：https://oj.leetcode.com/problems/two-sum/
代码(github)：https://github.com/illuz/leetcode

题意：

一个数组中两个位置上的数的和恰为 target，求这两个位置。

分析：

暴力找过去复杂度是 O(n^2)，会 TLE。

可以先排序再用双指针向中间夹逼，复杂度 O(nlogn)。
可以用 Map 记录出现的数，只要判断有没有和当前的数凑成 target 的数，再找出来就行，复杂度 O(nlogn) 而不是 O(n) ，因为 Map 也要复杂度的。
在 2 中的 Map 复杂度可以用数组来弥补，时间复杂度是 O(n) ，不过空间复杂度是 O(MAXN)。
代码：

方法一：双指针
```c++
class Solution {
    public:
        vector<int> twoSum(vector<int> &numbers, int target) {
            int sz = numbers.size();
            int left = 0, right = sz - 1, sum = 0;

            vector<int> sorted (numbers);
            std::sort(sorted.begin(), sorted.end());

            vector<int> index;
            while (left < right) {
                sum = sorted[left] + sorted[right];
                if (sum == target) {
                    // find the answer
                    for (int i = 0; i < sz; i++) {
                        if (numbers[i] == sorted[left])
                            index.push_back(i + 1);
                        else if (numbers[i] == sorted[right])
                            index.push_back(i + 1);
                        if (index.size() == 2)
                            return index;
                    }
                } else if (sum > target) {
                    right--;
                } else {
                    left++;
                }
            }
            // Program never go here, because
            // "each input would have exactly one solution"
        }
};
```

Java:

```java
public class Solution {

    static class Pair implements Comparable<Pair> {
        int value, index;
        public Pair(int v, int id) {
            value = v;
            index = id;
        }

        @Override
        public int compareTo(Pair b) {
            return this.value - b.value;
        }
    }

    public static int[] twoSum(int[] numbers, int target) {
        int[] res = new int[2];
        Pair[] pairs = new Pair[numbers.length];

        // get pairs and sort
        for (int i = 0; i < numbers.length; ++i) {
            pairs[i] = new Pair(numbers[i], i + 1);
        }
        Arrays.sort(pairs);

        // two points
        int left = 0, right = numbers.length - 1, sum = 0;
        while (left < right) {
            sum = pairs[left].value + pairs[right].value;
            if (sum == target) {
                res[0] = pairs[left].index;
                res[1] = pairs[right].index;
                if (res[0] > res[1]) {
                    // swap them
                    res[0] ^= res[1];
                    res[1] ^= res[0];
                    res[0] ^= res[1];
                }
                break;
            } else if (sum > target) {
                --right;
            } else {
                ++left;
            }
        }

        return res;
    }
}
```

Python:

```python
class Solution:
    # @return a tuple, (index1, index2)
    def twoSum(self, num, target):
        # sort
        sorted_num = sorted(num)

        # two points
        left = 0
        right = len(num) - 1
        res = []
        while (left < right):
            sum = sorted_num[left] + sorted_num[right]
            if sum == target:
                # find out index
                break;
            elif sum > target:
                right -= 1
            else:
                left += 1

        if left == right:
            return -1, -1
        else:
            pos1 = num.index(sorted_num[left]) + 1
            pos2 = num.index(sorted_num[right]) + 1
            if pos1 == pos2:    # find again
                pos2 = num[pos1:].index(sorted_num[right]) + pos1 + 1

            return min(pos1, pos2), max(pos1, pos2)
```
