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