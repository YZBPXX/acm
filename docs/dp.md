### 基本概念
维基百科：
>动态规划在寻找有很多重叠子问题的情况的最佳解时有效。它将问题重新组合成子问题。为了避免多次解决这些子问题，它们的结果都逐渐被计算并被储存，从简单的问题直到整个问题都被解决。因此，动态规划储存递迴时的结果，因而不会在解决同样的问题时花费时间。动态规划只能应用于有最佳子结构的问题。最佳子结构的意思是局部最佳解能决定全域最佳解（对有些问题这个要求并不能完全满足，故有时需要引入一定的近似）。简单地说，问题能够分解成子问题来解决。

个人理解： 很多时候我们求的问题都是由若干个子问题互相嵌套的，如果我们用动态规划的思想来考虑可以重新划分为若干个子问题，并逐步求解

#### 题目
[题集](https://zhuanlan.zhihu.com/p/126546914)
- [最长递增子序列](http://acm.hdu.edu.cn/showproblem.php?pid=1257)
	- $dp[i]=a[i]>a[top]?dp[i-1]+1:dp[i-1]$
- [最长公共子序列](https://leetcode-cn.com/problems/longest-common-subsequence/)
	- $dp[i][j]\begin{cases}
		0 i==0||j==0\\
		dp[i-1][j-1] &s_1[i]==s_2[j]\\
		max(dp[i-1][j],dp[i][j-1]), &s_1[i]!=s_2[j]\\
	\end{cases}$
- [鸡蛋掉落](https://leetcode-cn.com/problems/super-egg-drop/)
	- $dp[n][k]=max(dp[x-1][k-1],dp[n-x][k])+1, n为层数，k为鸡蛋数$
- [三角形最小路径和](http://acm.hdu.edu.cn/showproblem.php?pid=2084)
	- $dp[n][i]=max(dp[n-1][i-1],dp[n-1][i])+a[n][i], n为第几层，i为第几个数，注意取之范围$
- [最大子串和](http://acm.hdu.edu.cn/showproblem.php?pid=1003)
	- $dp[i]\begin{cases}
		dp[i-1]+a[i] &dp[i-1]>=0
		a[i] &dp[i-1]<0
	\end{cases}, dp[i]一i结尾最大的子串和$
- [最大子串积](https://leetcode-cn.com/submissions/detail/128613292/)
	- $\begin{cases}
		dp1[i]=dp1[i-1]*a[i] &a[i]>0\\
		dp1[i]=dp2[i-1]*a[i] &a[i]<0
	\end{cases}, dp1[i]是i结尾最大的正子串积,dp2[i]是i结尾的最大负子串积$
		- 注意需要维护
