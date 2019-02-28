## DFS

#### 77 组合

> 对于组合问题的dfs过程，与全排列不同。
>
> dfs时不再是从数组的0号位置开始遍历所有元素，而是从上一个元素所在的位置`last+1`处开始搜索。

#### 39 组合求和

- 本题数组中每个元素可使用多次

同77的求解方式相似

#### 40  含有相同元素的组合求和

- 本题数组中每个元素只能用一次，但可能含有重复元素

- **去除重复的常用剪枝技巧如下：** :small_red_triangle:

> 注意和`有重复元素的全排列`问题的区别，两题较为相似
>
> 排序后，dfs即可，注意dfs中从上一个元素所在的位置last开始搜索
>
> **`if (i > 0 && nums[i] == nums[i - 1] && !vis[i - 1]) continue;`**
>
> **同样，要加上此步剪枝来避免重复（因为含有重复元素）**

#### 216 1-9数字的组合求和

同39题相似，较简单

#### 78 Subsets子集合

> 1.dfs
>
> 原集合中每一个数字只有两种状态，要么存在，要么不存在

> 2.非递归
>
> 我们可以一位一位的网上叠加，比如对于题目中给的例子[1,2,3]来说，最开始是空集，那么我们现在要处理1，就在空集上加1，为[1]，现在我们有两个子集：[]和[1]，下面我们来处理2，我们在之前的子集基础上，每个都加个2，可以分别得到[2]，[1, 2]，那么现在所有的子集合为[], [1], [2], [1, 2]，同理处理3的情况可得[3], [1, 3], [2, 3], [1, 2, 3], 再加上之前的子集就是所有的子集合了
>
> ```cpp
> vector<vector<int> > subsets(vector<int> &S) {
>     vector<vector<int> > res(1);
>     sort(S.begin(), S.end());
>     for (int i = 0; i < S.size(); ++i) {
>         int size = res.size();
>         for (int j = 0; j < size; ++j) {
>             res.push_back(res[j]);
>             res.back().push_back(S[i]);
>         }
>     }
>     return res;
> }
> ```

#### 90 Subsets II

排序后，使用**`if (i > 0 && nums[i] == nums[i - 1] && !vis[i - 1]) continue;`**进行剪枝即可

本题注意要先**`排序`**

#### 51 n皇后问题

```cpp
class Solution {
public:
    vector<vector<string>> ans;
    vector<vector<string>> solveNQueens(int n) {
        vector<string> out(n, string(n, '.'));
        vector<int> pos(n, -1);
        solve(pos, n, 0);
        return ans;
    }
    // k代表当前放置第k个皇后(即到了第k行)
    void solve(vector<int>& pos, int n, int k) {
        if (k >= n) {
            vector<string> out(n, string(n, '.'));
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    if (j == pos[i]) out[i][j] = 'Q';
                    else out[i][j] = '.';
                }
            }
            ans.push_back(out);
            return ;
        }
        // 尝试每一列
        for (int i = 0; i < n; i++) {
            pos[k] = i;
            if (isValid(pos, k)) {
                solve(pos, n, k + 1);
                pos[k] = -1;
            }
            pos[k] = -1;
        }
        return ;
    }
    bool isValid(vector<int>& pos, int k) {
        for (int i = 0; i < k; i++) {
            if (pos[i] == pos[k]) return false;
            if (abs(i - k) == abs(pos[i] - pos[k])) return false;
        }
        return true;
    }
};
```



## 图论算法入门

#### 子图

若一个图的顶点集和边集分别是另一图的顶点集的子集和边集的子集，则称该图为另一图的子图。

换句话说，从一个图里选出一部分顶点和边，只要确保选择的边对应的两个顶点也都被选择，那么所有选出的顶点和边组成的图就是原图的子图。

#### 连通

