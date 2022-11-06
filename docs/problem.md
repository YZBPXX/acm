[1634](https://codeforces.com/contest/1634/problem/C)
----
题意：将 1 到 $n\times k$的正整数排成 n 行 k 列，使得每一行 k 个数所有子串的平均数都为整数。

[1352B](https://codeforces.com/problemset/problem/1352/B)
----
题意：将n表示成k个偶数或奇数表示且为正整数

[1646C](https://codeforces.com/problemset/problem/1646/C)
----
题意：将n 表示成2的幂和阶层和，要求项数最少

[1630A](https://codeforces.com/contest/1630/problem/A)
----
- 题意：给你一个n,且n是2的幂，让你将0~n-1这n个数配对, 使得
$$
\sum\limits_{i=1,j=1}^{\frac{n}{2}}a_i&a_j=k
$$

[1614C](https://codeforces.com/problemset/problem/1614/C)
----
- 题意：有一段序列${a_i}$,已知m段子序列在原序列的起始位置，结束位置，以及该段的或，求原序列的所有子序列的异或总和

[1562C](https://codeforces.com/contest/1562/problem/C)
----
- 题意：有一段01串s, 其中a, b，是s中长度不小于一半的子串
    - 求a, b. 使得a和b转化为十进制是倍数关系

[牛客挑战赛58B](https://ac.nowcoder.com/acm/contest/11198/B)
----
- 题意：给定n，m,$a_i,b_i \in [0,2^m)$ 求多少序列满足下式
$$
a_1|a_2|a_i|...|a_n \leq b_1 \oplus b_2 \oplus b_i \oplus ... \oplus b_n
$$

[1654C](https://codeforces.com/contest/1654/problem/C)
----
- 题意：有n个数，这n个数判断这n个数是否是某个数通过不断处2得到的（如果是奇数则一个数向上取整，一个数向下取整）
- 例子如4 -> 2, 2 -> 1, 1, 2. 所以2，2和1，1，2 都满足条件,而2，8不可能是某个数除2得到

[1542B](https://codeforces.com/problemset/problem/1542/B)
----
- 题意：以知a, b和集合S(第一个元素是1），在S中如果存在x，那么ax,x+b 也存在

[1487C](https://codeforces.com/problemset/problem/1487/C)
----
> 写了一个多小时 写C题还是很吃力～～～ 但起码还是写出来了
- 有n个队伍，每两个队伍之间会有一场比赛，并有一下规则, 求每个队伍间的胜负情况使得每个队伍积分相同的情况下，平局次数最少
    - 比赛输了不扣积分
    - 赢了奖励3点积分
    - 平局1点积分

[1487C](https://codeforces.com/problemset/problem/1487/C)
----
- 给一个从1到n的数并且从第k位开始依次下降:  求一个k长的排列映射p[a[i]]=b[i]，使得b的逆序对和a的逆序对相同
     - 例如n=6, k=4: 1, 2, 3, 4, 3, 2 

[1567C](https://codeforces.com/problemset/problem/1657/C)
----
- 给一个字符串由'('、')' 两种括号构成，每次可以进行一下操作
    - 删除最短的回文前缀
    - 删除最短的配对括号前缀

[1440C1](https://codeforces.com/problemset/problem/1440/C1)
----
- 给一个由0，1组成的表, 有一下操作
    - 每次可以选择一个$2\times 2$的格子中其中的3位将其翻转
- 目标是通过操作让这个表全为0，输出每次翻转的三个点坐标, 要求翻转次数不超过$3n\times m$
 
[1658B](https://codeforces.com/contest/1658/problem/B)
----
- p是一组排列, 要使得$gcd(p_1\times 1,p_2\times 2,...,p_n\times n)>1$， 问有几种排列满足要求


[1660C](https://codeforces.com/contest/1660/problem/C)
----
- 有一个s串，尽可能少的删除串中某些字符，使得串中相临相同的字母有偶数个
    - 例如：aabab, 删除a aabb
    - 例如：aba， 删除b 后a

[1651C](https://codeforces.com/contest/1651/problem/C)
----
- 有两排电脑，相邻电脑有网线接通，两排之间没有网线接通, 两排接网线的代价为$|a_i-b_j|
    - 如果接网线在成本最少的情况下使得坏任意一台电脑，剩下的电脑都能通信

[1649C](https://codeforces.com/contest/1651/problem/C)
----
- 有一个矩阵，计算矩阵里元素相等的两两间的曼哈顿距离，并输出总和
    - 要求时间复杂度为$O(n\times m)$

[1661C](https://codeforces.com/contest/1661/problem/C)
----
- 有n个正整数，可以选择一个数字进行以下操作
    - 加一(如果是第一次或上一次加操作是加二）
    - 加二(如果上一次加操作是加一）
    - 不操作
- 问最少多少次使得n个数字相等
- 例子1,2,4; 可以选择第一个加1，第二个加2，然后什么都不做，在加二

[1419D2](https://codeforces.com/contest/1419/problem/D2)
----
- 有一个数组$a_i$, 如果$a_{i-1}\le ai \le a_{i+1}$, 则提取a[i]，
    - 重新排序使得提取的数最多

[1400C](https://codeforces.com/problemset/problem/1400/C)
- 有一个串w，有间距x. 并且有串s满足
    - 如果$w_{i-x}==1 or w_{i+x}==1 $ 则$s_i=1$
    - 否则$s_i=0$
- 现在有串s，和间距x，求w，如果不存在输出-1

```
input 
3
101110
2
01
1
110
1

output

111011
10
-1
```

[1659C](https://codeforces.com/problemset/problem/1459/C)
----
- 给定一个数组x 表示每个怪物离初始位置距离（依次递增），从左到右可以进行以下操作
    - 从当前位置$x_i$移动到已经消灭了的怪物位置$x_j$；代价$cos=a\times (x_j -  x_i)$
    - 从当前位置$x_i$消灭最近的未被消灭的怪物$x_j$；代价$cos=b\times (x_j -  x_i)$
- 如何使得代价最小而消灭所有的怪物

[1668C](https://codeforces.com/problemset/problem/1668/C)
----
- 有一个数组a（给定其值），和一个数组b初始为0
    - 可以进行$b_i=k_i\times a_i$, k为任意数
- 问如果要使b成递增序列，$\sum\limits_{i=1}^{n}$abs(ki) 最少为多少

[2392](https://leetcode.cn/problems/build-a-matrix-with-conditions/)
----
- 已知两个有序序列里面都是1-k的整数，分别是1-k从上到下，从左到有的顺序，将这k个数字插入到$k\times k$的矩阵中，使得他们从上到下，从左到右顺序一致，

## [2389](https://leetcode.cn/problems/longest-subsequence-with-limited-sum/)
- 求一个序列中的子序列和不超过k的最长长度，

## [164](https://leetcode.cn/problems/maximum-gap/)
- 求一个序列中在坐标轴的最大间隔, 要求O(n)
## [6169](https://leetcode.cn/problems/longest-nice-subarray/)
- 求数组中最长连续与的子数组长度
## [6168](https://leetcode.cn/problems/number-of-ways-to-reach-a-position-after-exactly-k-steps/)
- 从a到b每次可以向前或者向后移动1步，给你k步问有多少种方法到达
## [lc2406](https://leetcode.cn/problems/divide-intervals-into-minimum-number-of-groups/)
- 给你n个区间求区间最大重叠个数
## [lc2407](https://leetcode.cn/problems/longest-increasing-subsequence-ii/)
- 求最长递增子序列，最大间隔不超过k
## [lc2412](https://leetcode.cn/problems/minimum-money-required-before-transactions/)
- 有n件商品，每件商品花销和返利为[cost,back]，cost表示第i个商品花销，back表示反利；问任意顺序选择n减商品，花销最大是多少
```
输入：transactions = [[2,1],[5,0],[4,2]]
输出：10
解释：
刚开始 money = 10 ，交易可以以任意顺序进行。
可以证明如果 money < 10 ，那么某些交易无法进行。
```

## [318B](https://leetcode.cn/problems/maximum-sum-of-distinct-subarrays-with-length-k/)
    问题：求子数组中长度正好为k，且元素不重复，的最大和。
    分析：按题目要求模拟求每个子数组，从j开始，
        - 如果第i个位置没有重复元素，计算最大和，跟新
        - 当在第i个位置出现重复元素的时候需要回溯，
            - 回溯到第一个位置，朴素的方法
            - 容易想到回溯到重复点的位置pos后一个元素pos+1，才是有效的回溯，所以需要额外维护一个位置数组vis。这个时候如果从i开始重新计算vis，时间复杂度还是很大；
                - 我们已经计算过从j到i的vis了，很自然想到能否通过之前的计算来避免重新计算vis；显然vis并不需要更改，之前的记录的重复元素下标x小于pos+1计无效即可。
