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
>  vector<vector<int> > res(1);
>  sort(S.begin(), S.end());
>  for (int i = 0; i < S.size(); ++i) {
>      int size = res.size();
>      for (int j = 0; j < size; ++j) {
>          res.push_back(res[j]);
>          res.back().push_back(S[i]);
>      }
>  }
>  return res;
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

#### 37 数独 :boom:

> 坐标(i, j)所在的宫为(i / 3) * 3 + (j / 3);
>
> 对于每个需要填数字的格子带入1到9，每代入一个数字都判定其是否合法，如果合法就继续下一次递归，结束时把数字设回'.'，判断新加入的数字是否合法时，只需要判定当前数字是否合法，不需要判定这个数组是否为数独数组，因为之前加进的数字都是合法的，这样可以使程序更加高效一些

**回顾时再做一遍**

- 本题目与其他dfs题目不同之处
  - dfs函数返回值为bool

本题目中要求最后将给的数独矩阵填充答案，因此当填完最后一个数字并且合法时，直接返回true，即不再进行回溯（若回溯会将已经填充的数字删除）

#### 131 回文划分 :triangular_flag_on_post:

> dfs

本题目中要注意c++中`substr`和`substring`两个函数区别

```cpp
// 功能相似，参数不同
substr ：返回一个从指定位置开始的指定长度的子字符串
substring ：返回位于 String 对象中指定位置的子字符串。
string s = "abcde";
s.substr(start, length);		// 从start开始长度为length
s.substring(start, end);		// 左闭右开（即不包含end）
```

