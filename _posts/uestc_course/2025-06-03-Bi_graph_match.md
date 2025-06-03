---
layout:     post
title:      "二分图匹配问题.25"
subtitle:   " \"algorithm learning\""
date:       2025-06-03 13:00:00
author:     "LanZinYtt"
header-img: "img/in-post/Bi-graph_match/BiGraph_match_header.jpg"
catalog: true
tags:
    - Algorithm Basic
---

<p id = "build"></p>

>本专题着重分析二分图匹配算法，图源参考[OiWiki](https://oi-wiki.org/graph/graph-matching/bigraph-match)

# 二分图匹配问题

## 二分图

- 定义：节点由两个集合组成，且两个集合内部没有边的图
![二分图示例](/img/in-post/Bi-graph_match/bi-graph.svg)
- 性质：
    - 不存在长度为奇数的环
    - 如果用黑白交叉染色节点，二分图中每一条边的两边一定是一黑一白
- 判定：无向图G=<V,E>为偶图(二分图)的充要条件是G的所有回路的长度均为偶数。
    - 对于这样的充要条件，我们可以取它的逆否命题来高效得证明，下列我们使用DFS遍历来判断
   
    ```cpp
   
        class BiGraph{
        private:
            vector<vector<int>> graph;  //邻接表
            vector<int> depth;
            vector<bool> visited;
            int n;  //节点数

            bool dfs(int u,int p,int d){
                visited[u]=true;
                depth[u]=d;
                for(int v:graph[u]){
                    if(v==p)continue;   //避免回头
                    if(!visited[v]){
                        if(dfs(v,u,d+1))return true;
                    }else{
                        if((d-depth[v]+1)%2==1)return true;//形成奇数回路
                    }
                }
                return false; 
            }
        public:
            BiGraph(...){...}
            
            bool is_BiGraph(){
                visited.assign(n,false);
                depth.assign(n,-1);
                for(int i=0;i<n;i++){
                    if(!visited[i]){
                        if(dfs(i,-1,0))return false;
                    }
                }
                return true; //是二分图
            }
        }
   
    ```

## 二分图匹配问题

### 最大匹配
- **增广路算法**(O(nm))
   - 增广路算法的思想来源于这样一种情况：当存在从一个未匹配点开始，以另一个未匹配点结束的通路，且路径上的边交替为非匹配边和匹配边，那么，将路径上的各个边非匹配和匹配性质调换，可以使得匹配边数加一。
   - 不断地进行增广路检测，即可找到最大匹配。
   - 这点我们可以使用dfs进行检测与更新。
   - 我们试着对这个想法进行优化，让它更易于编写：不难发现增广路长度一定是奇数，并且路径匹配边和非匹配边在同一次遍历中方向是相同的，于是我们可以给二分图**定向**为有向图，可以更容易的进行dfs。
   
    ```cpp

    struct augment_path{
        vector<set<int>> g;
        vector<int> pa,pb,vis;
        int n,m,dfn,res;
        augment_path(int _n,int _m):n(_n),m(_m){
            assert(0<=n && 0<=m);
            pa.assign(n,-1);
            pb.assign(m,-1);
            vis.assign(n,-1);
            g.resize(n);
            res=0;
            dfn=0;
        }
        void add(int u,int to){
            assert(0<=u && u<n && 0<=to && to<m);   //断言
            g[u].insert(to);
        }
        bool dfs(int v){
            vis[v]=dfn;
            for(int u:g[v]){
                if(pb[u]==-1){
                    pb[u]=v;
                    pa[v]=u;
                    return true;
                }
            }
            for(int u:g[v]){
                if(vis[pb[u]]!=dfn && dfs(pb[u])){
                    pa[v]=u;
                    pb[u]=v;
                    return true;
                }
            }
            return false;
        }
        int solve(){
            while (true){
                dfn++;  //表示轮数
                int cnt=0;
                for(int i=0;i<n;i++){
                    if(pa[i]==-1 && dfs(i)){
                        cnt++;
                    }
                }
                if(cnt==0){
                    break;
                }
                res+=cnt;
            }
            return res;
        }
    };

    ```
- **最小点覆盖**

    - 定义：在二分图中选出最少的点，满足每条边至少有一个端点被选。
    - 可以证明，在二分图中，最小点覆盖=最大匹配
    - 证明:容易想到，在最大匹配中若有k条边，要覆盖这k条边，起码要有k个点，有最小点覆盖≥最大匹配，这点是显然的。然而为什么可以直接相等，并不好想，但是我们可以构造一个点覆盖。对于左侧集合A与右侧集合B，设用DFS可达的左侧点集合为S，右侧点集合为T，(A-S) ∪ T，对于连接S和T的边(被T覆盖)、对于连接S和(B-T)的边(不存在)、对于连接A-S和T的边(被A-S中覆盖)、对于连接A-S和B-T的边(被A-S覆盖)，容易观察知这个点覆盖的大小等于最大匹配。[König定理]
- 这里最大匹配实际上也可以转为网络流问题，但鄙人网络流了解不多，可以前往[OiWiki](https://oi-wiki.org/graph/flow/max-flow/#dinic-%E7%AE%97%E6%B3%95)查阅

### 最大权匹配

- [**匈牙利算法**(Hungarian Algorithm)](https://oi-wiki.org/graph/graph-matching/bigraph-weight-match/)
    - 这个算法的逻辑相当复杂，对于想要深究的同学非常建议读一下[原论文](https://onlinelibrary.wiley.com/doi/abs/10.1002/nav.3800020109)。另外，这里还有一个比较有意思的网站直接[演示匈牙利算法的计算过程](https://www.hungarianalgorithm.com/hungarianalgorithm.php)，在此我只做部分我对原理的理解。
    - 关键概念:
        - 顶标：给每个顶点分配数值标签，左侧顶点标签`lx[i]`，右侧顶点标签`ly[j]`
        - 可行顶标：满足`lx[i] + ly[j] ≥ w[i][j]`对所有边成立
        - 相等子图：只包含满足`lx[i] + ly[j] = w[i][j]`的边的子图
        - 
    - 原理解析：
        - 必须要说明的是，匈牙利匹配需要偶图两个集合中点数相等，因此我们将不存在的边补0，然后再进行算法流程即可，我们这里以代码中常用的顶标形式举例。
        - 首先我们证明一个前置定理一：对于某组可行顶标，如果其相等子图存在完全匹配，那么，该匹配就是原二分图的最大权完全匹配
        - 不难证明，对于任何匹配，其权重小于所有顶标和，而如果存在一组匹配使得在相等子图中是完全匹配，则满足上界取等
        - 我们可以先对原图初始化一组可行顶标，例如$lx(i) = \max_{1\leq j\leq n} \{ w(i, j)\},\, ly(i) = 0$
        - 然后选一个未匹配点，如同最大匹配一样求增广路。找到增广路就增广，否则，会得到一个交错树，则需要回溯或者结束当轮搜索。
        - 令 S，T 表示二分图左边右边在交错树中的点，S'，T' 表示不在交错树中的点。
        - 在相等子图中：
            - S-T' 的边不存在，否则交错树会增长。
            - S'-T 一定是非匹配边，否则他就属于 S。
        - 假设给 S 中的顶标 -a，给 T 中的顶标 +a，可以发现
            - S-T 边依然存在相等子图中。
            - S'-T' 没变化。
            - S-T' 中的 lx + ly 有所减少，可能加入相等子图。
            - S'-T 中的 lx + ly 会增加，所以不可能加入相等子图。
        - 未来最小化顶标调整的幅度，同时确保至少有一条新边能进入相等子图，a得是 S-T'当中最小的边权
        $a =\min\{ lx(u) + ly(v) - w(u,v) | u\in{S} , v\in{T'}\}$
        - 当一条新的边 (u,v) 加入相等子图后有两种情况
            - v 是未匹配点，则找到增广路
            - v 和 S' 中的点已经匹配
        - 这样至多修改 n 次顶标后，就可以找到增广路。
        - 这样得到的相等子图中的完全匹配，根据定理一可以得知它就算最大权完全匹配。
    - 以上是顶标形式的逻辑，[矩阵形式](https://zhuanlan.zhihu.com/p/677501913)实质上是等价的，目的都是为了让更多的边进入相等子图中。
    - 代码实现(这里用的是简短的，而且效率不算很高的，如果想要更实用的板子可以参考[OiWiki](https://oi-wiki.org/graph/graph-matching/bigraph-weight-match/))：

    ```cpp
    
        struct KM {
            int n;
            vector<vector<int>> w;
            vector<int> lx, ly, match;
            vector<bool> vx, vy;
            vector<int> slack;

            KM(int n) : n(n), w(n, vector<int>(n, 0)), 
                    lx(n), ly(n), match(n, -1), 
                    vx(n), vy(n), slack(n) {}
            
            bool dfs(int u) {
                vx[u] = true;
                for (int v = 0; v < n; v++) {
                    if (vy[v]) continue;
                    int d = lx[u] + ly[v] - w[u][v];
                    if (d == 0) {
                        vy[v] = true;
                        if (match[v] == -1 || dfs(match[v])) {
                            match[v] = u;
                            return true;
                        }
                    } else if (slack[v] > d) {
                        slack[v] = d;
                    }
                }
                return false;
            }
            
            int solve() {
                // 初始化顶标
                for (int i = 0; i < n; i++)
                    lx[i] = *max_element(w[i].begin(), w[i].end());
                    
                for (int i = 0; i < n; i++) {
                    fill(slack.begin(), slack.end(), INT_MAX);
                    while (true) {
                        fill(vx.begin(), vx.end(), false);
                        fill(vy.begin(), vy.end(), false);
                        if (dfs(i)) break;
                        
                        // 调整顶标
                        int d = *min_element(slack.begin(), slack.end());
                        for (int j = 0; j < n; j++) {
                            if (vx[j]) lx[j] -= d;
                            if (vy[j]) ly[j] += d;
                            else slack[j] -= d;
                        }
                        fill(slack.begin(), slack.end(), INT_MAX);
                    }
                }
                
                int res = 0;
                for (int i = 0; i < n; i++)
                    if (match[i] != -1 && w[match[i]][i] > 0) // 只统计实际存在的边
                        res += w[match[i]][i];
                return res;
            }
        };
    
    ```

样题：[CDOJ徽章商店(最小覆盖)[可能未公开]](https://cdoj.site/d/presummer_training_2025/p/P1085?tid=6817867c385b3643f32598b3)、[UOJ80(最大权匹配)](https://uoj.ac/problem/80)

至此，希望你能理解二分图中的各个概念😘