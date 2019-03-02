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



## 图论算法入门

#### 子图

若一个图的顶点集和边集分别是另一图的顶点集的子集和边集的子集，则称该图为另一图的子图。

换句话说，从一个图里选出一部分顶点和边，只要确保选择的边对应的两个顶点也都被选择，那么所有选出的顶点和边组成的图就是原图的子图。

#### 连通

在无向图中，如果有顶点v到顶点w的路径存在，则称v和w是连通的。若图G中`任意两个顶点是连通`的，则称G为`连通图`，否则称为`非连通图`。

**`极大连通子图`**即`连通分量`

#### FloodFill算法

求解无向图的所有连通分量

算法通过给图中的顶点染色，最终使得同一个连通分量的顶点颜色相同，不同连通分量的顶点颜色不同。

>1. 找到一个没有染色的顶点，将其染成新的颜色color_cnt，如果没有则算法结束
>2. 初始化一个空的队列，并将第一步的顶点插入队列（初始化）
>3. 不断获得队首元素并弹出，将和队首元素相邻的并且没有染色的顶点染为color_cnt，并且入队
>4. 重复执行第一步，直至所有顶点被染色

```cpp
// 使用邻接矩阵实现
#include <stdio.h>
#include <stdlib.h>

#define MAX_N 1000

typedef struct Graph {
    int n;
    int color[MAX_N];
    int mat[MAX_N][MAX_N];
} Graph;

void init_Graph(Graph *g, int input_n) {
    g->n = input_n;
    for (int i = 0; i < g->n; i++) {
        g->color[i] = 0;
        for (int j = 0; j < g->n; j++) {
            g->mat[i][j] = 0;
        }
    }
}

void insert(Graph *g, int x, int y) {
    g->mat[x][y] = 1;
    g->mat[y][x] = 1;
}

void floodfill(Graph *g) {
    int color_cnt = 0;
    int q[MAX_N];
    for (int i = 0; i < g->n; i++) {
        if (g->color[i] == 0) {
            color_cnt++;
            g->color[i] = color_cnt;
            int l = 0, r = 0;
        	q[r++] = i;
            while (l < r) {
                int vertex = q[l++];
                for (int j = 0; j < g->n; j++) {
                    if (g->mat[vertex][j] && g->color[j] == 0) {
                        g->color[j] = color_cnt;
                        q[r++] = j;
                    }
                }
            }
        }
    }
    for (int i = 0; i < g->n; i++) {
        printf("%d %d\n", i, g->color[i]);
    }
}

int main() {
    int n, m;
    scanf("%d %d", &n, &m);
    Graph *g = (Graph *)malloc(sizeof(Graph));
    init_Graph(g, n);
    for (int i = 0; i < m; i++) {
        int a, b;
        scanf("%d %d", &a, &b);
        insert(g, a, b);
    }
    floodfill(g);
    free(g);
    return 0;
}
```

#### 最小生成树

如何从一个带权图中抽出一棵树，使得边权值和最小，这棵树就叫做最小生成树。

#### Prim算法--带权无向图的最小生成树

`使用了贪心的策略` `合并边`

时间复杂度： $O(V^2)$ 

V为图G中顶点总个数，如果加上堆优化，可以把时间复杂度降到O(VlogV+E)，其中E为图G中总边数

**`#define INF 0x3f3f3f3f`**

>原因：可以作为无穷大使用，而且还满足了无穷大加无穷大还是无穷大的需求

小技巧，这个值可以用到memset中

```cpp
int dist[100];
memset(dist, 0x3f, sizeof(dist));
```



算法过程如下：

> 我们定义带权图G的顶点集合为V，接着定义最小生成树的顶点集合为U，初始集合U为空，执行一下操作
>
> 1. 任选一个顶点x，加入集合U，并记录每个顶点到当前最小生成树的最短距离
> 2. 选择一个距离当前最小生成树最近的，且不属于集合U的顶点v，（若有多个，任选其一即可），将顶点v加入集合U，并更新所有与顶点相连的顶点到当前最小生成树的最短距离
> 3. 重复第二步操作，直至集合U等于集合V（即选够n个顶点）

```cpp
// 初始时所有点距离最小生成树的最短距离为INF（无穷大），从顶点v开始找最小生成树。先将顶点v的距离置为0，接着更新与v相邻的未访问顶点的距离，直至找出n个点。
#include <stdio.h>
#include <stdlib.h>

#define MAX_N 1000

const int INF = 0x3f3f3f3f;

typedef struct Graph {
    int n;
    int visited[MAX_N], dist[MAX_N]; 		// g->visited[i]记录i是否已经加入最小生成树
    int mat[MAX_N][MAX_N]; 					// g->dist[i]记录i点到最小生成树的最短距离
}Graph;

void init(Graph *g, int input_n) {
    g->n = input_n;
    for (int i = 0; i < g->n; i++) {
        for (int j = 0; j < g->n; j++) {
            g->mat[i][j] = INF;
        }
    }
}

void insert(Graph *g, int x, int y, int weight) {
    g->mat[x][y] = weight;
    g->mat[y][x] = weight;
}

int prim(Graph *g, int v) {
    int total_weight = 0;
	for (int i = 0; i < g->n; i++) {
        g->visited[i] = 0;
        g->dist[i] = INF;
    }
    g->dist[v] = 0;
    // 一共需要找n个点
    for (int i = 0; i < g->n; i++) {
    	int min_dist = INF, min_vertex;
    	for (int j = 0; j < g->n; j++) {
            if (!g->visited[j] && g->dist[j] < min_dist) {
                min_dist = g->dist[j];
                min_vertex = j;
            }
        }
        total_weight += min_dist;
        g->visited[min_vertex] = 1; 	// 表示插入到最小生成树中 别忘记写！！！！
        // 更新相邻未插入节点距离最小生成树的距离
        for (int j = 0; j < g->n; j++) {
            if (!g->visited[j] && g->mat[min_vertex][j] < g->dist[j]) {
                g->dist[j] = g->mat[min_vertex][j];
            }
        }
    }
    return total_weight;
}

int main() {
    int n, m;
    scanf("%d %d", &n, &m);
    Graph *g = (Graph *)malloc(sizeof(Graph));
    init(g, n);
    for (int i = 0; i < m; i++) {
        int a, b, c;
        scanf("%d %d %d", &a, &b ,&c);
        insert(g, a, b, c);
    }
    printf("%d\n", prim(g, 0));
    free(g);
    return 0;
}
```

#### 最短路问题

`带权无向图从顶点v出发，到所有顶点的最短路径长度`

时间复杂度：$O(V^2 + E)$

如果利用堆优化，可以将时间复杂度优化为O(VlogV + E)，这是最坏情况下最优的单源最短路算法

不适用于有边权为负数的情况

```cpp
和Prim算法极为相似，都会用到一个visited数组标记是否已经完成计算，以及一个dist数组表示最短路径。不过在Dijstra算法中，dist存储的不是到生成树的最短距离了，而是从源点出发到每个顶点的最短路径
```

```cpp
#include <stdio.h>
#include <stdlib.h>

#define MAX_N 1000

const int INF = 0x3f3f3f3f;

typedef struct Graph {
    int n;
    int visited[MAX_N], dist[MAX_N];
    int mat[MAX_N][MAX_N];
}Graph;

void init(Graph *g, int input_n) {
    g->n = input_n;
    for (int i = 0; i < g->n; ++i) {
        for (int j = 0; j < g->n; j++) {
            g->mat[i][j] = INF;
        }
    }
}

void insert(Graph *g, int x, int y, int weight) {
    g->mat[x][y] = weight;
    g->mat[y][x] = weight;
}

void dijkstra(Graph *g, int v) {
    for (int i = 0; i < g->n; i++) {
        g->visited[i] = 0;
        g->dist[i] = INF;
    }
    g->dist[v] = 0;
    // 循环n次，每次找到从源点出发最短路径最小的未访问的节点，标记位已访问
    // 之后更新和这个顶点相邻的所有顶点的最短路
    for (int i = 0; i < g->n; i++) {
        int min_dist = INF, min_vertex;
        for (int j = 0; j < g->n; j++) {
            if (!g->visited[j] && g->dist[j] < min_dist) {
                min_dist = g->dist[j];
                min_vertex = j;
            }
        }
        g->visited[min_vertex] = 1;
        // 最重要！！松弛操作
    	for (int j = 0; j < g->n; j++) {
            if (!g->visited[j] && min_dist + g->mat[min_vertex][j] < g->dist[j]) {
                g->dist[j] = min_dist + g->mat[min_vertex][j];
            }
        }
    }
}

int main() {
    int n, m;
    scanf("%d %d", &n, &m);
    Graph *g = (Graph *)malloc(sizeof(Graph));
    init(g, n);
    for (int i = 0; i < m; i++) {
        int a, b, c;
        scanf("%d %d %d", &a, &b ,&c);
        insert(g, a, b, c);
    }
    dijkstra(g, 0);
    for (int i = 0; i < n; i++) {
        printf("%d: %d\n", i, g->dist[i]);
    }
    free(g);
    return 0;
}
```
