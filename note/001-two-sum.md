[001.Two_Sum (Medium)](https://leetcode.com/problems/Two-Sum/)
===

链接：https://oj.leetcode.com/problems/two-sum/

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution.

Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
UPDATE (2016/2/13):
The return format had been changed to zero-based indices. Please read the above updated description carefully.

题意：

一个数组中两个位置上的数的和恰为 target，求这两个位置。

```

```java
public class Solution {
    
    public int[] twoSum(int[] nums, int target) {
    int[] result = null;
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    result = new int[]{i, j};
                    break;
                }
            }
        }
        return result;
    }
}
```

Better answer:

```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = null;
        Map<Integer, Integer> indexMap = new HashMap<>();
        for (int i = 0; i < nums.length; ++i) {
            Integer index = indexMap.get(target - nums[i]);
            if (index == null) {
                indexMap.put(nums[i], i);
            } else {
                result = new int[] {index, i};
                break;
            }
        }
        return result;
    }
}
```
