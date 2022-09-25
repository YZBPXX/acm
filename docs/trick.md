- 解除输入流绑定
```c++
ios::sync_with_stdio(0);
cin.tie(0);
cout.tie(0);
```
- 二进制相关 内置
    - 返回最高位是第几位（从1开始) `(32-builtin_clz(n))`
```c++
/*
他们本来的类型都是unsigned int
改成usigned long 加l 例__builtin_clzl
改成usigned long long 加ll 例__builtin_clzll

__builtin_popcount(n) ：n的二进制中1的个数
__builtin_clz(n)：返回n前0的个数 count leading zeros 
__builtin_ctz(n)：返回n后的0的个数
__builtin_ffs(n)：返回n的最后一位1的是从后向前第几位, 相当于__builtin_ctz(n)+1

example:
    // 00...1010
    cout<<__builtin_ffs(10)<<endl;
    cout<<__builtin_clz(10)<<endl;
    cout<<__builtin_ctz(10)<<endl;
out :
2
28
1
*/ 
```

- 获得某类型最大值climits头文件
```
LLONG_MAX
INT_MAX
FLOAT_MAX
```

- 二分查找 algorithm
    - `while (l<=r)` 注意取等号，返回l，这样最后一次判断是否满足条件
        - 如果写`l<=r' 则r=mid-1,并且l=mid-1； 否则必然造成死循环
    - lower_bound(a,a+n,key) , 返回第一个大于等于key的指针
        - 相当于条件`if(a[i]>=key) r=mid-1` 
    - upper_bound(a,a+n,key) , 返回第一个大于key的指针
        - 相当于条件`if(a[i]>key) r=mid-1` 
    - 因为a是数组，所以通过`lower_bound(a,a+n,key)-a` 可以获得索引

- 取整 cmath
    - ceil(), 正无穷大方向取整
    - floor(), 负无穷大方向取整
    - trunc()  零向取整
    - round() 四舍五入
- 从c开始每次加减b返回第一个大于a的整数ans = c+((a-c)/b)b + b;
    - 主要理解`d+(d/b)*b` 小于等于d 无论正负
    - 向0取整

- 链表
    - 对于字典树如果没法使用vector来模拟，应为要嵌套很多层，每层还得同时生成n个几点(如果只是单纯的push，没办法区别第几个，所以要同时全部生成)，如果使用链表可以在需要的时候在生成
    - 语法规则

* struct TreeNode {
*     int val;
*     TreeNode *left;
*     TreeNode *right;
*     TreeNode() : val(0), left(nullptr), right(nullptr) {} // 初始化 参数列表
*     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {} //重构
*     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
* };
