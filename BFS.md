## BFS

- 广搜往往需要封装一个结构体，记录坐标以及当前步数（为了下一层节点方便统计步数）

- 为这个结构体写一个构造函数方便使用

  **`q.push(node(x, y, d))`**

#### 密码锁

> 自己的方法只能过一半的测试用例，因为没有对已访问过的情况标记处理

bfs一般用于最优化问题，最值问题，题目有三种操作：上滑、下滑、交换。将这三种操作的结果加入队列，直到目标解

不要用string，会TLE

> 答案，使用一个标记数组，开到1000即可，因为最大数字为9999，将密码序列转换为字符串处理。每次都字符串的4位都做变化，然后入队，直到队首元素为目标密码即可

#### :small_red_triangle: 蒜头君回家

有启发性的题目

> 可以开一个三维的vis数组**`int vis[MAX][MAX][2]`**
>
> 其中`vis[x][y][0]`记录bfs搜索拿到钥匙（即到达过'P'点）的过程，之后`vis[x][y][1]`记录从拿到钥匙出发，一直到达终点的过程
>
> 原因如下：因为到达'P'点的过程中，如果只用二维的vis数组，会出现图上的点已经标记过的过程，即到达p之后，不能再向标记过的点走了，即搜到'P'点后bfs过程就结束了
>
> 个人理解，这是把'P'作为终点的结果。而实际上我们在到达'P' 点拿到钥匙后，还要继续去走到终点，因此使用一个三维的vis数组，当`vis[x][y][0]`标记为走过时，`vis[x][y][1]`用来表示从'P'点再继续向终点走的过程
>
> ```cpp
> #include <iostream>
> #include <queue>
> #define MAX 2005
> using namespace std;
> struct node {
>     int x, y, step;
>     int f;
>     node(int x1, int y1, int s1, int flag = 0) : x(x1), y(y1), step(s1), f(flag) {}
>     node() {}
> };
> int vis[MAX][MAX][2] = {0};
> char g[MAX][MAX];
> int n, m, sx, sy;
> int dx[4] = {0, 0, 1, -1};
> int dy[4] = {1, -1, 0, 0};
> int in0(int x, int y) {
>     return x >= 0 && x < n && y >= 0 && y < m && g[x][y] != '#' && !vis[x][y][0];
> }
> int in1(int x, int y) {
>     return x >= 0 && x < n && y >= 0 && y < m && g[x][y] != '#' && !vis[x][y][1];
> }
> int bfs() {
>     queue<node> q;
>     q.push(node(sx, sy, 0));
>     vis[sx][sy][0] = 1;
>     while (!q.empty()) {
>         node temp = q.front();
>         q.pop();
>         if (g[temp.x][temp.y] == 'T' && temp.f == 1) {
>             return temp.step;
>         }
>         for (int i = 0; i < 4; i++) {
>             int xx = temp.x + dx[i];
>             int yy = temp.y + dy[i];
>         	if (in0(xx, yy)) {
>                 // 当没拿到钥匙时走到了终点，不去访问，走其他的点
>                 if (g[xx][yy] == 'T' && temp.f == 0) {
>                     continue;
>                 }
>                 vis[xx][yy][0] = 1;
>                 int flag = 0;
>                 // temp点已经拿到了钥匙，则从temp出发到的点都标记为已经拿到了钥匙
>                 if (g[xx][yy] == 'P' || temp.f) {
>                     flag = 1;
>                 }
>                 q.push(node(xx, yy, temp.step + 1, flag));
>             }
>             // 已经拿到钥匙，继续走的情况
>             if (in1(xx, yy) && temp.f == 1) {
>                 vis[xx][yy][1] = 1;
>                 q.push(node(xx, yy, temp.step + 1, 1));
>             }
>         }
>     }
>     return -1;
> }
> int main() {
>     cin >> n >> m;
>     for (int i = 0; i < n; i++) {
>         for (int j = 0; j < m; j++) {
>             cin >> g[i][j];
>             if (g[i][j] == 'S') sx = i, sy = j;
>         }
>     }
>     cout << bfs() << endl;
>     return 0;
> }
> ```
>
> 

#### 一维跳棋

移动如何实现？

如何记录最短的那条路径？

保存每种状态可使用map

