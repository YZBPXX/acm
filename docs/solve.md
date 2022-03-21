1634
----
> 注意考虑方向，排除某些不可能的情况，考虑剩下的情况是否满足要求

分析：平均数为整数则相邻之间奇偶性相同，也就是说奇数和偶数个数不能差1只能相同，也就得到了$n\times k$为偶数，考虑连续奇偶性相同的数是否所有满足条件，任意i-j 之间的和为
$$\frac{(a+(j-i)*2+a)(j-i+1)}{2}\times\frac{1}{j-i+1}=a+j-i$$
故证明均值都是整数

1352B
----
- 偶数可以由若干个2组成、奇数可以由若干个1组成,所以不管偶数（奇数）如何组成都可以用一个偶数数，n-1写2 表示. 奇数则可以用一个奇数和n-1个1表示(将其他不为1的奇数提取2k加到第一个数 两个还是奇数）. 所以问题变成了n能不能由k-1个1外加一个奇数，或k-1个2外加一个偶数表示.
- 所以直接n-k+1 如果是奇数则可以，或则n-(k-1)*2 是偶数就可以 否则不行

1646C
----
> **这种题型可以设置成一个参数x范围比较小，另一个参数y范围随意，已知函数f(x,y)，求x,y的组合**
> 注意到一个点，如果贪心解决不了，可以考虑两种解发，1 遍历所有情况，2 求局部最优解(dp)
> 解法1中遍历所有情况需要花销$2^n$ （因为用二进制表示该情况有无，m种状态则$m^n$）， 遍历完后查找最优解也为$m^n$ 时间复杂度为$\log(m^n)$ , 参考以下代码 怎么写这种迭代
> 解法2中 遍历不同的状态需要m 需要n次遍历  故时间复杂度为O(mn)
- 一个数肯定能由若干个2的幂表示, 所以肯定有解，比较如果用阶层表示会减少多少个2的幂项
- 问题 若是直接减小于n的最大阶层，则可能破坏结构减少过多2的幂项，而判定是否会破坏结构又需要在上次减去的操作后在考虑要不要减去某个阶层，类似于背包问题 直接放最大的会怎么样
- 遍历所有阶层组合的情况(注意这种写法），以背包问题为例
```c++
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;
int main(){
    int t;
    cin>>t;
    while(t--){
       int n,key;
       cin>>n>>key;
       int w[100],v[100];
       for(int i=0;i<n;i++){
           cin>>w[i];
       }
       for(int i=0;i<n;i++){
           cin>>v[i];
       }
       long long s=1<<n;
       vector<pair<long long,long long>>C(s);//大小为2^n 因为有2^n种情况
       C[0]={ 0,0 };
       for(long long i=1;i<s;i++){
            int mask=63-__builtin_clzll(i);//mask 代表第几个// count leading zeros
           // 将全部需要信息保存起来
           C[i].first=C[i-(1<<(mask))].first+w[mask];
           C[i].second=C[i-(1<<(mask))].second+v[mask];
       }
       long long  ans=0;
       利用保存的信息一次查找
       for(auto i: C){
           if(i.first<=key){
               ans=max(ans,i.second);
           }
       }
       cout<<ans;
    }
}
```

```c++
    /*
     __builtin_popcount(n) ：n的二进制中1的个数
    __builtin_ffs(n)：返回n的最后一位1的是从后向前第几位
    __builtin_clz(n)：返回n前0的个数
    __builtin_ctz(n)：返回n后的0的个数
    他们本来的类型都是unsigned int
    改成usigned long 加l 例__builtin_clzl
    改成usigned long long 加ll 例__builtin_clzll
    */ 
#include<iostream>
#include<utility>
#include<vector>
#include<cmath>
#include <algorithm>
using namespace std;
long long MAX=1e14+11;
int main(){
    int t;
    cin>>t;
    while(t--){
        long long  n;
        cin>>n;
        vector<long long>facts;
        long long  fact=1,i=1;
        while(fact<MAX){
           facts.push_back(fact);
           i++;
           fact*=i;
        }
        vector<pair<long long, long long>>f(1<<facts.size());// facts 每项代表每位 所有应该有facts 这个大小
        f.push_back(make_pair(0,0));
        long long  s=facts.size();
        long long r=1;
        for(long long  i=1; i<(r<<s); i++){
            long long  mask=63-__builtin_clzll(i);
            f[i].first=f[i-(1<<(mask))].first+facts[mask];
            f[i].second=__builtin_popcountll(i);
        }
        long long res = __builtin_popcountll(n);
        for(auto i : f){
            if(i.first<=n){
                res = min(res, __builtin_popcountll(n-i.first)+i.second);
            }
        }
        cout<<res<<endl;
    }
}
```
1630A
----
- 考虑入k!=n-1 则 k&n-1=k,~(k)&0=0,其余的x只需要x&~x=0
- 如果k==n-1 思考如何改变小批量的数，得到k的同时其余数满足x&!x=0

1614C
-----
- 分析：求异或，考虑每一位对答案的贡献，例如在某个区间[l,r]中,考虑第i位的影响，将第i位为0的放在一在A集合里，第i位为1的放在B集合里(通过整区间的异或结果判断该位是否至少有一个），如果B不为空,从B里任选奇数个项和A中任意组合构成答案中第i位的所有组合count，而第i位值位$2^{i-1}$, 对结果的共享为$count\times2^{i-1}$, 若果B为空则为0,第i位不产生影响。故$ans=\sum\limits_{i=1}^{若至少存在一个整数，第i为1}count\times 2^{i-1}=count\times k$ k为所有整数求异或; 由count等于以下. 所以$ans=2^{n-1}\times k$
$$
count=2^count_A\times \sum\limits_{i=0}C_{count_B}^{2i+1}=2^{count_A+count_B-1}=2^{r-l-1}
$$

[1562C](https://codeforces.com/contest/1562/problem/C)
----
- 要使得两个乘数关系：如果有0 去掉0即可（判断0在左边还是右边），如果没0全1则移动一个单位即可

[牛客挑战赛58B](https://ac.nowcoder.com/acm/contest/11198/B)
----
> 对于位运算、首先应该想到按位来求对结果的共享
- 考虑每个一位对结果的影响（要想$a\leq b$那肯定是某一位大于它，所以枚举每一位的情况，总共m位）
    - 等式左边第i位为1(($2^{n}-1$),等式右边第i位为0($2^{n-1}$)，
    - 两边中下标在[1,i-1]随便填($(2^2n)^{i-1}$) 
    - 两边中下标在[i+1,m]要求两边一样,而要使两边一样, 左边可以随便填，右边最后一个唯一保证一致($(2^n)^{m-i}\times ((2^{n-1})^{m-i})$,  相乘有$(2^{2n-1})^{m-i}$
        - 注意还有全部相等的情况: 根据上诉分析，无论左边怎么选，右边都有$(2^n-1)^m$种情况等于左边，而左边有$2^n^m$种情况, 相乘得$(2^{2n-1})^m$
    - 所以总共有:
$$
(2^{2n-1})^m + \sum\limits_{1}^{m} (2^{2n-1})^{m-i} (2^2n)^{i-1} (2^{n}-1) 2^{n-1}
$$

[1654C](https://codeforces.com/contest/1654/problem/C)
----
> 这个题只有两种考虑方法，要么从结果往上推是否能得到答案，要么从答案往下推结果是否满足
- 分析： 
    - 如果从下往上推，应该依次合并差值不超过1的两个数，但是对于最小值x有两种情况，要么y=x+x,要么y=x+x+1; 没有什么好的方法决定哪个 例如2 2 3 3。1 1 2 选择方法不一样
    - 如果从上往下推，假设可以推出那么第一个必然是总和sum，每次将sum分裂 , 如果等于$\max{a_i}$最大值则停止分裂，并删除$max{a_i}$, 重复上个步骤直到sum分裂成多个1，且不能和$a_i$匹配，则停止


[1542B](https://codeforces.com/problemset/problem/1542/B)
----
- 分析：集合S中的元素可以表示为: $a^i + a^jb + kb$
    - 如果n在S中那么s就满足上面式子即: $n = a^i + a^jb + kb$  ,可转化为一下两种等式
        - $n = a^i + a^jb + kb mod a$ -> $n mod a = kb mod a$ 需要遍历kb<n 的所有情况
        -  $n = a^i + a^jb + kb mod b$ -> $n mod b = a^i mod b$ 需要遍历a^i 小于n的所有情况
    - 因为a^i更容易收敛，所以选择第二种情况(**注意a=1**）

[1487C](https://codeforces.com/problemset/problem/1487/C)
----
- 总共有$\frac{(n-1)n}{2}$ 场比赛，
    - 当n为奇数的时候每个队伍刚好可以获得$\frac{n-1}{2}$场比赛的胜利， 所以需要构造每个队伍刚好获胜$k = \frac{n-1}{2}$,可以构造一个圈，每个队伍将会赢得前面k个队伍，剩余的队伍都输了
    - 当n为偶数, 因为得分$\frac{3n(n-1)}{2n}$不可能是整数，所以需要构建平局~通常可以考虑变化为前面一种解决方案的状况~ , 使得分数恰好能被整数, 即$\frac{3n(n-1)}{2n} - t = 0 mod n$ ，求的$t=\frac{n}{2}$, 所以构造$\frac{n}{2}$场平局，还是构造一个圈每个元素与圈的对立面达成平手，其余胜负各一半
