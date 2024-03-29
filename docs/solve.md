[1634](https://codeforces.com/contest/1634/problem/C)
----
>  从大方向考虑要判断是否能被整除，那么字串的和就必须有通式，故而想到了等差数列和等比数列

分析：平均数为整数则每行相邻之间奇偶性相同，如果每行个数k>1 那么总数$a\times k$ 必须是偶数, 否则不能满足前面那个条件。考虑连续奇偶性相同的数是否所有满足条件(只有这个方向才能用通式表达，进而用数学公式证明），任意i-j 之间的和为
$$\frac{(a+(j-i)*2+a)(j-i+1)}{2}\times\frac{1}{j-i+1}=a+j-i$$
故证明均值都是整数

[1352B](https://codeforces.com/contest/1352/problem/B)
----
- 偶数可以由若干个2组成、奇数可以由若干个1组成,所以不管偶数（奇数）如何组成都可以用一个偶数数，n-1写2 表示. 奇数则可以用一个奇数和n-1个1表示(将其他不为1的奇数提取2k加到第一个数 两个还是奇数）. 所以问题变成了n能不能由k-1个1外加一个奇数，或k-1个2外加一个偶数表示.
- 所以直接n-k+1 如果是奇数则可以，或则n-(k-1)*2 是偶数就可以 否则不行

[1646C](https://codeforces.com/contest/1646/problem/C)
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
#include<cmath>
using namespace std;
typedef long long ll;
static ll facts(ll x){
    ll sum=1;
    for(int i=2;i<=x;i++){
       sum*=i; 
    }
    return sum;
}
int main(){
    ios::sync_with_stdio(0);cin.tie(0);cout.tie(0);
    int t;
    cin>>t;
    ll  a[1<<15]={ 0 };
    for(ll  i=1;i<=(1<<15);i++){
        ll mask=(31-__builtin_clz(i));
        a[i]=a[i^(1<<mask)]+facts(mask+1);
    }
    while(t--){
        ll n;
        cin>>n;
        int cnt=100;
        for(int i=0;i<=(1<<15);i++){
           if(a[i]<=n){
              cnt=min(__builtin_popcountll(i)+__builtin_popcountll(n-a[i]),cnt);
           }
           else {
               break;
           }
        }
        cout<<cnt<<endl;
    }
}
```
[1630A](https://codeforces.com/contest/1630/problem/A)
----
- 考虑入k!=n-1 则 k&n-1=k,~(k)&0=0,其余的x只需要x&~x=0
- 如果k==n-1 思考如何改变小批量的数，得到k的同时其余数满足x&!x=0

[1614C](https://codeforces.com/contest/1614/problem/C)
-----
> 对于任意种组合类问题，需要判断出哪些组合是有用的，找出有用的组合
> 子序列的异或，异或满足结合律，所以相当于所有组合求异或, 然后求和

- 分析：求异或，考虑每一位对答案的贡献，考虑第i位的贡献，要使第i位为1，只需要前n-1个任意取，留一个1根据前面的结果确定取不取, 使得结果为1，即可。此时有$2^{n-1}$ 种情况
    - 而已知的或结果，即可知第i位是否至少有一个1
$$
ans = 2^{n-1} \times \sum\limits_{i=0,第i位存在}^{} 2^i = 2^{n-1}sum 
$$

[1562C](https://codeforces.com/contest/1562/problem/C)
----
- 要使得两个为倍数关系：如果有0 去掉0即可（判断0在左边还是右边），如果没0, 说明全1，此时让他们为1倍即可

[牛客挑战赛58B](https://ac.nowcoder.com/acm/contest/11198/B)
----
> 对于位运算、首先应该想到按位来求对结果的贡献
> 对于a \le b 暴力求解的办法是遍历每个位大小关系
> 对于n个数的异或运算，要使结果为m，只需要确定最后一个数
- 考虑每个一位对结果的影响（要想$a\leq b$那肯定是某一位大于它，所以枚举每一位的情况，总共m位）
    - 等式左边第i位为1(($2^{n}-1$),等式右边第i位为0($2^{n-1}$)，
    - 两边中下标在[1,i-1]随便填($(2^{2n})^{i-1}$) 
    - 两边中下标在[i+1,m]要求两边一样,而要使两边一样, 左边可以随便填，右边最后一个唯一保证一致($(2^n)^{m-i}\times ((2^{n-1})^{m-i})$,  相乘有$(2^{2n-1})^{m-i}$
        - 注意还有全部相等的情况: 根据上诉分析，无论左边怎么选，右边都有$(2^{n-1})^m$种情况等于左边，而左边有$2^n^m$种情况, 相乘得$(2^{2n-1})^m$
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


[1487C](https://codeforces.com/problemset/problem/1487/C)
----
> 逆序对应该两两对答案的贡献
- 考虑两两变化后的逆序对对答案的影响: 变化前有 x ... y ... y ... x (或则x ... y ...x)此时(x,y) 的逆序对有2个，变化后要么相对位置不变，要么变成，y ... x ... x ... y 此时(x,y)的逆序对还是两个, 也就是说对称部分不管怎么转换两两间的逆序对还是不变(可以证明如果改动非对称部分逆序对一定会变多），所以要求最大字典序，只需要在对称位置降序排列即可

[1567C](https://codeforces.com/problemset/problem/1657/C)
----
> 如果只有两种字符，那么判断最短回文前缀回很方便

首先想到分别进行两种普通的括号匹配和回文判定
- 但回文串的判定比较麻烦，需要先用马拉车预处理才能达到O(n)
可以注意到这只有两种字符, 肯定有取巧的地方
- 考虑第一个字符是'(' 的情况，那么无论下一个是什么，都能删除, 
- 当第一个是')'时，找下一个')'，因为中间全是'(' 所以只要能找到就肯定是回文串

[1567C](https://codeforces.com/problemset/problem/1657/C)
----
> 注意以后写构造题，即使有想法，但是想法很复杂没必要写，参考答案好些
> 从题目给的线索$3n\times m$肯定与算法有关，而目标是每个坐标都为0，有$n\times m $个目标，考虑是否意味着3次操作可以使一个目标完成

- 根据题目要求，一个位置翻转奇数次得到相反的值，偶数次得到相同的值，通过这个规律可以通过3个此翻转一个位置改变其余不变

[1658](https://codeforces.com/contest/1658/problem/B)
----
- 很容易发现奇数位放偶数，偶数位放奇数肯定满足要求，此时gcd=2. 
- 进一步考虑gcd>2 的情况，加入gcd=k>2, 那么n个数里面最多有$2\floor{\frac{n}{k}}$个数的最大公约数为k，而$2\floor{\frac{n}{k}} < n$ 所以k>2 时不可能有n个的最大公约数为k
    - 同时可以证明k==2，n&1==1，时也不可能有n个数最大公约数为k

[1660C](https://codeforces.com/contest/1660/problem/C)
> 正向思考删除那个字符很难通过前段决定；如aaaba, aaabb; 需要全局信息才能决定
> 如果考虑逆问题求偶数个相同的序列则可以通过局部信息确定最优解（贪心）
- 删除后的字符相邻都是偶数个相同的，那么最少删除某些字符，等价于尽可能找出最多相邻相同的是偶数的子序列出来，而每个偶数子序列又是两两一组的；贪心的考虑一组字符a...a; ...中为不同的字符，那么删除..., 肯定是最优的选择


[1651C](https://codeforces.com/contest/1651/problem/C)
----
> 注意思考如果if语句过于复杂 能不能用否命题简化

- 考虑坏了某一台会对全局网络有什么影响
    - 如果该台不是接通点，那么左右无法通信
    - 如果该台是接通点，左右无法通信，且少一条接通线
- 考虑最坏情况该台是接通点：
    - 如果该台是最左接通点，且左边还有电脑，那么无解，肯定无法接通
    - 如果该台是最右接通点，且右边还有电脑，那么无解，肯定无法接通
    - 如果该台两种都不是，那么两侧可以通过两侧接通点接通
    - 所以最左接通点左边没有电脑也就是必须是左边（右边，另一排同理)。只需要连接线包含四个角点即可
- 考虑连接四个角点，如何使得最小
    - 角点间可能互连，也可能不互连，不能通过每个角点的最优边判定
    - 四个点数据并不算大，如何暴力求解？
    - 暴力即遍历角点间互连与不互连的情况，

[1649C](https://codeforces.com/contest/1651/problem/C)
----
> 数学计算的题 实在太难了～～
- 对于某个数字有k个那么两两间的计算公式为
$$
sum_{i=0}^{k-1} \sum_{j=i+1}^{k-1} |r_i - r_j| + |c_i - c_j| = \left(\sum_{i=0}^{k-1} \sum_{j=i+1}^{k-1} |r_i - r_j|\right) + \left(\sum_{i=0}^{k-1} \sum_{j=i+1}^{k-1} |c_i - c_j|\right)
$$
- 以第一部分为例，如果按大到小排序，去掉绝对值有
$$
\sum_{i=0}^{k-1} \sum_{j=i+1}^{k-1} |r_i - r_j| = \sum_{i=0}^{k-1} \sum_{j=i+1}^{k-1} s_j - s_i = \left(\sum_{i=0}^{k-1} \sum_{j=i+1}^{k-1} s_j\right) + \left(\sum_{i=0}^{k-1} \sum_{j=i+1}^{k-1} -s_i\right)
$$
- 而此时可以将两个求和符号化为一个, 于是得到了一个$O(k)$时间复杂度的算法
$$
\sum_{j=0}^{k-1} js_j + \sum_{i=0}^{k-1} -(k-1-i)s_i = \sum_{i=0}^{k-1} (2i+1-k)s_i
$$

[1661C](https://codeforces.com/contest/1661/problem/C)
----
- 首先可以判断最少次数使其相等时的数字不会超过其中最大值的太多~这步就算不证明也能用，大概遍历多少就行了~
- 假设目标值是mx，
    - 那么每个数字与目标值差值为奇数的必须要加一，此时操作次数为$cnt = 2\times x$, 剩下$res = sum - 3\times x$ , 如果res为负则说明最后一个是1，cnt--
    - 此时考虑偶数res 如何分配的问题；此时我们想让它尽快收敛，贪心的想只能1、2、1、2 .... , 也就是以3为周期此时$cnt2 = 2(res/3)+res%3$


[1419D2](https://codeforces.com/contest/1419/problem/D2)
----
- 答案的范围是0-n， 思考给定一个k如何判断是否符合条件, 
- 提取的k个数必然是最小的k个数(~证明~)
- 那么数据就分成了两个几个A,B分别表示选定的集合，不在选定的数的集合(坑1，Ai不一定小于Bi，有可能等于,选择的时候需要判断，不能直接选择)
    - 进行组合时，贪心的考虑将最小的A匹配最小的B且满足Ai严格小于Bi的数Bi
        - 任意一方匹配完只需要将剩下每匹配的按大到小输出(坑2: 如果从小到大不是最优的)
    - 因为以上是最优的组合方式，所以最后遍历是否满足条件
    

[1400C](https://codeforces.com/problemset/problem/1400/C)
----
> 注意题目思考方向，如果可以确定某些东西则确定然后思考（贪心）
- 如果s[i]=0 那么可以确定$w_i$两边必须为0
- 注意这个时候已经没有必要产生0了，也就是说w就这么多0，只需要判断是否会产生冲突即可

[1659C](https://codeforces.com/problemset/problem/1459/C)
----
- 思考: 如果某次需要移动到$x_i$ 那么之前的操作都需要移动到怪物的前一个位置再进行消灭
    - 因为总的移动开销不变，而消灭的开销减少了
- 那么问题转化为确定最后一个移动的位置，使得开销最小, 根据前面的思考得到
$$
cost = ax_i + bx_1 + \sum\limits_{2}^{j=i}b(x_j-x_{j-1}) + \sum\limits_{j=i+1}^{j=n}(b(x_j-x_i) \\
cost = ax_i + \sum\limits_{j=1}^{j=n}bx_j - \sum\limits_{j=1}^{j=i-1}bx_j -b(n-i)x_i
$$
- 注意$\sum\limits_{j=1}^{j=i-1}bx_j$ 是可以迭代的，所以时间复杂度为O(n)

[1668C](https://codeforces.com/problemset/problem/1668/C)
----
> 虽然做出来了，但最近这类的问题遇到倒多了还是总结以下
-  这类问题初看需要考虑的点很多，比如首先尽量乘1倍，如果遇到1倍不符合的，比较是将前面变小为当前这个乘1倍就满足，还是将当前这个数乘多倍
- 但是换个角度看：确定0的位置，0两边的情况是可以唯一确定的，只能乘越来越多倍, 而不需要改边前面的已经得到的数(因为需要改变的化0就换位置了，就变成了下一次的遍历). 而0的位置由是可以遍历的。所以暴力比较即可

[2392](https://leetcode.cn/problems/build-a-matrix-with-conditions/)
---
- ans[sort1[key]][sort2[key]]=key

[2389](https://leetcode.cn/problems/longest-subsequence-with-limited-sum/)
----
- 求子序列只有相对位置，求和与位置无关所以可以将其排序

## [164](https://leetcode.cn/problems/maximum-gap/)
- 将区间划分成n-1个(不管怎么划分最大的元素都在第n个区间), 此时有n-1个区间，n-1个数字（最大的数不再），将数字放入所属区间，有一下三种情况
    1. 刚好放满，此时每个区间都有且仅有一个，这个时候所有间隔都是相邻区间内元素的间隔，所以最大间隔也是相邻区间元素间隔
    2. 没放满，存在空区间，那么同一个区间内的元素不可能构成最小间隔（左右两端有最值封住）
- 所以不管怎么样，最大间隔都在相邻区间求的（除去空区间后相邻）; 其实只要区间个数大于n-1就行了
- 注意代码实现还有些问题，虽然最大值放在第n区间但是求除法的时候除非整除 否则在n-1区间, 可以选择加个1e-9进行调整
[6169](https://leetcode.cn/problems/longest-nice-subarray/)
- 注意这种回溯算法代码怎么写
```
int longestNiceSubarray(vector<int>& nums) {
        int n=nums.size();
        int or_=nums[0];
        int ans=1;
        int pre=0,next=1;

        while(next<n){

            if((or_&nums[next])==0){

                or_|=nums[next];
                ans=max(ans,next-pre+1);
                next++;
            }
            else{
                while((or_&nums[next])!=0){
                    or_^=nums[pre];
                    pre++;
                }
                or_|=nums[next];
                next++;
            }

        }
        return ans;
    }
```
## [6168](https://leetcode.cn/problems/number-of-ways-to-reach-a-position-after-exactly-k-steps/)
- 明显可以想出：当前位置的值 = 前一个位置少一步的值 + 后一个位置少一步的值 - 当时想着第一轮遍历位置，但是又觉得后一个位置需要前一个位置提供信息才可行，所以就卡住了；仔细一想，后一个位置需要的是前一个位置上一轮的信息
- 其实根据方程: dp[stride][pos]=dp[stride-1][pos-1]+dp[stride-1][pos+1]
                dp[pos][stride]=dp[pos-1][stride-1]+dp[pos+1][stride-1]
- 可以看出，只有stride才能迭代出来, 迭代一轮pos所有情况都会遍历

## [lc2406](https://leetcode.cn/problems/divide-intervals-into-minimum-number-of-groups/)
- 左区间加一，右区间减一。前缀和统计，维护最大值
- 注意加减分开统计，否则出现(1,1)这种情况，不能正确统计

## [lc2407](https://leetcode.cn/problems/longest-increasing-subsequence-ii/)
首先考虑最朴素的做法
- $dp[i][j]=max{dp[i-1][j-z]},z=1,2,3,...,k$
- 滚动数组优化掉第一纬，此时$dp[j]=max{dp[j-z]),z=1,2,3,...k$
- 此时转化为一个区间查询问题，查询n次，每次需要logk,也就是O(nlogn)

## [lc2412](https://leetcode.cn/problems/minimum-money-required-before-transactions/)
- 对于每一笔交易来说，最差的情况就是前面都是亏钱，然后就轮到这笔交易。而总的最差情况就是这些最差情况中的一个。
    - 因此可以保存每比交易亏钱总和，然后遍历每次交易，比较出最大损失
