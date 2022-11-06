# 常用技巧
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
    - `lower_bound(a,a+n,key)` , 返回第一个大于等于key的指针
        - 相当于条件`if(a[i]>=key) r=mid-1` 
    - `upper_bound(a,a+n,key)` , 返回第一个大于key的指针
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
    - 对于字典树如果没法使用vector来模拟，因为要嵌套很多层，每层还得同时生成n个几点(如果只是单纯的push，没办法区别第几个，所以要同时全部生成)，如果使用链表可以在需要的时候在生成
    - 语法规则
```c++
 struct TreeNode {
     int val;
     TreeNode *left;
     TreeNode *right;
     TreeNode() : val(0), left(nullptr), right(nullptr) {} // 初始化 参数列表
     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {} //重构
     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 };
```
# stl

priority\_queue
--
- 定义int形从大到小(默认从小到大）的优先队列`priority_queue<int, vector<int>,greater<int>> a`
- 查询 top()
- 添加 push()
- 删除 pop()
set
--
- 复制一个集合`set<int>s1(s2)`
- `set.erase()` 参数可以是迭代器也可以是数值
- `set.insert()`
- 二分查找`auto pos = upper_bound(key)` 返回迭代器
string
--
- 读取数字 `string s=to_string(num),<algorithm>`
- 转化为数字 `int n=stoi(s),<string>`
vector
--
- 添加 `push_back()`
- 删除 
    - `pop_back()`
    - `erase(const_iterator pos)`
- 插入 `insert(const_iterator pos, a)` 原来的元素向后
- 返回长度 `x.size()`
- 对vector排序 `sort(x.begin(),x.end())`
- 截断 `vector<int>y(x.begin()+1,x.end())`
- 初始化大小和初值 `vector<vector<int>> x(50,vector<int>(50,0))`
- 清空 `x.clear()` 只是将size变成0 此时还可以通过x[1] 访问元素，但是`x.push_back(a)` 会将其覆盖
- 查找最大值: `mx = *max_element(nums.begin(), nums.end())`
- 二分: `int index=lower_bound(ans.begin(),ans.end(),key)-ans.begin()`
    - `upper_bound()` 返回第一个大于key的
    - `lower_bound()` 返回第一个大于等于key的
- 反转 `reverse(x.begin(),x.end())`

自定义比较
--
- 写`sort(s,s+n,cmp)`时可以写函数作为cmp, 写`priority_queue<int,vector<int>,cmp>` 时cmp必须为结构体
```
//从小到大的顺序
struct cmp{
  bool operator ()(const pair<long long,long long>  & a, const pair<long long,long long>  & b)
      {
          if(a.first!=b.first) return a.first<b.first;
          else return a.second<b.second;
      }
 };
```
- 返回vector最大值和下标 `index = max_element(a.begin(),a.end())-a.begin()`
    - 同时elelment 也能定义比较规则，如在找到第二维最大的那一行
```
    bool cmp(const vector<int> &a,const vector<int>&b){
       return a[1]<b[1];
    }
    cout<<max_element(a.begin(),a.end(),cmp)-a.begin()<<endl;
```
