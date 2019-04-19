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

<!--more-->

#### 贪心思想

Leetcode[435. Non-overlapping Intervals (Medium)](https://leetcode.com/problems/non-overlapping-intervals/description/)

> 先计算最多能组成的不重叠区间数，然后用区间总个数减去不重叠区间的个数
>
> 每次选择中区间的结尾最为重要，选择的区间结尾越小，留给后面区间的空间越大，则能选择的个数也越多，因此按区间的结尾小的在前进行排序，`每次选择结尾最小，并且和前一个区间不重叠的区间`

Leetcode[452. Minimum Number of Arrows to Burst Balloons (Medium)](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/)

> 也是计算不重叠的区间个数

> 比自己的思路简单的做法：按区间右端点排序，记录第一个区间的右端点为end，cnt为1；之后从第2个区间开始遍历所有区间，如果该区间的左端点比end大，则cnt++，同时更新end为该区间的右端点

:question:比较cmp函数要声明在类外（即静态的），为何

**Leetcode**[406. Queue Reconstruction by Height(Medium)](https://leetcode.com/problems/queue-reconstruction-by-height/description/)

>  为了使插入操作不影响后续的操作，身高较高的学生应该先做插入操作，否则身高较小的学生原先正确插入的第 k 个位置可能会变成第 k+1 个位置。

**Leetcode**[665. Non-decreasing Array (Easy)](https://leetcode.com/problems/non-decreasing-array/description/)修改一个数成为非递减数组

> 在出现 nums[i] < nums[i - 1] 时，需要考虑的是应该修改数组的哪个数，使得本次修改能使 i 之前的数组成为非递减数组，并且 **不影响后续的操作** 。优先考虑令 nums[i - 1] = nums[i]，因为如果修改 nums[i] = nums[i - 1] 的话，那么 nums[i] 这个数会变大，就有可能比 nums[i + 1] 大，从而影响了后续操作。还有一个比较特别的情况就是 nums[i] < nums[i - 2]，只修改 nums[i - 1] = nums[i] 不能使数组成为非递减数组，只能修改 nums[i] = nums[i - 1]。

**Leetcode**[122. Best Time to Buy and Sell Stock II (Easy)](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/)

#### 二分查找

`mid = head + (tail - head)  / 2`; 可防止两数相加时溢出

**Leetcode**[34. Search for a Range (Medium)](https://leetcode.com/problems/search-for-a-range/description/) 查找区间

前0后1问题，注意初始时设置`head = 0, tail = nums.size()（可能有全0的情况发生）`

先查找第一个大于等于target的数的位置作为first，再查找第一个大于target的数的位置减1作为last

注意边界条件的判断！