[004. Median of Two Sorted Arrays](https://leetcode.com/problems/Median-of-Two-Sorted-Arrays/)
===

There are two sorted arrays nums1 and nums2 of size m and n respectively. Find the median of the two sorted arrays.
The overall run time complexity should be O(log (m+n)).


中位数(Median)：是指将统计总体当中的各个值按大小顺序排列起来，形成一个数列，

1. 如果值的个数为奇数个，则处于数列中间位置的值就称为中位数；
2. 如果值的个数是偶数，则处于数列中间位置的两个值的平均值就称为中位数。

```java
public double findMedianSortedArrays(int[] A, int[] B) {
        int m = A.length, n = B.length;
        int l = (m + n + 1) / 2;
        int r = (m + n + 2) / 2;
        return (getkth(A, 0, B, 0, l) + getkth(A, 0, B, 0, r)) / 2.0;
    }

public double getkth(int[] A, int aStart, int[] B, int bStart, int k) {
    if (aStart > A.length - 1) return B[bStart + k - 1];            
    if (bStart > B.length - 1) return A[aStart + k - 1];                
    if (k == 1) return Math.min(A[aStart], B[bStart]);

    int aMid = Integer.MAX_VALUE, bMid = Integer.MAX_VALUE;
    if (aStart + k/2 - 1 < A.length) aMid = A[aStart + k/2 - 1]; 
    if (bStart + k/2 - 1 < B.length) bMid = B[bStart + k/2 - 1];        

    if (aMid < bMid) 
        return getkth(A, aStart + k/2, B, bStart,       k - k/2);// Check: aRight + bLeft 
    else 
        return getkth(A, aStart,       B, bStart + k/2, k - k/2);// Check: bRight + aLeft
}
```
