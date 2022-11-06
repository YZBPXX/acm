## 思维题
问题：![di-co](../img/di-co.png)
- 显然直接缩小规模，是不满足分治策略的（要求子问题形式上与父问题一直）
- 通过对子问题修改，添加特殊方格可以达到一致的效果
## 点分治
    其实就是树上的结点分治，每次求出该点的贡献，然后用同样的策略求子树的贡献
    对于求结点的贡献，也就是该点必须参与到答案中。由两部分组成：左子树、右子树中到根结点的路径的贡献；合并两个子树的贡献，点分治主要考虑的是
    1. 如何将左右子树的贡献求出
    2. 如何将求出的贡献和并
    而模版部分则是：
    1. 如何求树的重心（定理：重心的最大子树结点不超过n/2，进而最大递归深度为log n)：
        - 定义：该结点的最大子树与其他结点的最大子树比结点最小(dp)。例如一条链：1，2，3，4，5；3的最大子树最小
        - 通过dfs可以求出子树结点个数;
            - 换个角度就是树形dp(树的dp似乎不存在回溯问题，也就不需要反向求解去除重复子问题)；$dp[i]=max(dp[i])$dp[i]表示i结点的最大子树
     ```c++
     int cnt_total[N],max_node[N];//cnt_totale and weight, weight mean max sontree
     int n=node_total,mi=INF,ans;//mi=min max cnt_totale, ans=重心
     void dfs(int now,int parent)
     {
         cnt_total[now]=1;//最大结点数包括本身
         max_node[now]=0;
         // e是临街表
         for(int i=0;i<e[now].cnt_totale();i++)
         {
             int to=e[now][i];
             if(to==parent) continue;//如果子树是父节点退出
             dfs(to,now);
             cnt_total[now]+=cnt_total[to];//父节点也是一颗子树，cnt=总树-其他子结点数量
             max_node[now]=max(wgt[now],cnt_total[to]);//wgt 保存该结点最大子树
         }
         max_node[now]=max(wgt[now],n-cnt_total[now]);//比较父结点
         if(max_node[now]<mi) mi=wgt[now],ans=now;//跟新最优值
     }
     ```
    思考部分
    1. 因为子结点包括父结点，所以起码有3个子结点，要统计组合答案的时候需要是不同子结点上的
    2. 如果已经有各个结点到根结点的信息了，如果进行枚举则需要花O(n^2)，可以将结果排序，或者进行其他处理(直接判断k-key[i]是否出现过) 
