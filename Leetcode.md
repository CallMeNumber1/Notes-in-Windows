## Leetcode

#### 排序

**Kth Element 问题**

题目描述：找到第k大的元素

1. 排序。时间复杂度$O(NlogN)$，空间复杂度$O(1)$

2. 堆排序。时间复杂度$O(NlogK)$，空间复杂度$O(K)$

   维护一个最多有k个元素的小顶堆（最后队列里剩下的是最大的k个元素）

3. 快速选择

   使用快速排序的partition()实现

TopK Elements 问题

#### 贪心思想

Leetcode[435. Non-overlapping Intervals (Medium)](https://leetcode.com/problems/non-overlapping-intervals/description/)

先计算最多能组成的不重叠区间数，然后用区间总个数减去不重叠区间的个数

每次选择中区间的结尾最为重要，选择的区间结尾越小，留给后面区间的空间越大，则能选择的个数也越多，因此按区间的结尾小的在前进行排序，`每次选择结尾最小，并且和前一个区间不重叠的区间`

Leetcode[452. Minimum Number of Arrows to Burst Balloons (Medium)](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/)

也是计算不重叠的区间个数

> 比自己的思路简单的做法：按区间右端点排序，记录第一个区间的右端点为end，cnt为1；之后从第2个区间开始遍历所有区间，如果该区间的左端点比end大，则cnt++，同时更新end为该区间的右端点

:question:比较cmp函数要声明在类外（即静态的），为何

**Leetcode**[406. Queue Reconstruction by Height(Medium)](https://leetcode.com/problems/queue-reconstruction-by-height/description/)

为了使插入操作不影响后续的操作，身高较高的学生应该先做插入操作，否则身高较小的学生原先正确插入的第 k 个位置可能会变成第 k+1 个位置。