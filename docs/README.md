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
 
[1658](https://codeforces.com/contest/1658/problem/B)
----
- p是一组排列, 要使得$gcd(p_1\times 1,p_2\times 2,...,p_n\times n)>1$， 问有几种排列满足要求
