priority_queue
----
- 定义int形从大到小(默认从小到大）的优先队列priority_queue<int, vector<int>,greater<int>> a
- 查询 top()
- 添加 push()
- 删除 pop()
set
----
- 复制一个集合:set<int>s1(s2)
- set.erase() 参数可以是迭代器也可以是数值
- set.insert()
- 二分查找auto pos = upper_bound(key) 返回迭代器
string
----
- 读取数字 string s=to_string(num);
- 转化为数字 int n=stoi(s)
vector
----
- ⚠️
    - 一旦处事化大小 就别用push_back()
- 初始化时需要制定大小，才能通过索引赋值，否则只能push_back()
- 添加 push_back(),emplace_back()
- 删除 
    - pop_back()
    - erase(const_iterator pos)
- 插入 insert(const_iterator pos, a) 原来的元素向后
- 大小 x.size()
- 对vector排序 sort(x.begin(),x.end())
- 截断 vector<int>y(x.begin()+1,x.end())
- 初始化大小和初值 vector<vector<int>> x(50,vector<int>(50,0))
- 清空 clear()
    - x.clear() 只是将size变成0 此时还可以通过x[1] 访问元素，但是x.push_back(a) 会将其覆盖
- 查找最大值: `mx = *max_element(nums.begin(), nums.end())`
- 二分: `int index=lower_bound(ans.begin(),ans.end(),key)-ans.begin()`
    - upper_bound() 返回第一个大于key的
    - lower_bound() 返回第一个大于等于key的
- 反转 reverse(x.begin(),x.end()); 结果保存在x里
- max.resize(n,element=0)

自定义比较
----
- 写sort时可以写函数作为cmp
- 写priority_queue<int,vector<int>,cmp> 时cmp必须为结构体
- 同时返回true 一位置交换a，b的位置，所以返回条件相当于b是你想要的元素
```
struct cmp{
  bool operator ()(const pair<long long,long long>  & a, const pair<long long,long long>  & b)
      {
          if(a.first!=b.first) return a.first>b.first;
          else return a.second>b.second;
      }
 };
```
- 返回vector最大值和下标 index = max_element(a.begin(),a.end())-a.begin()
    - 同时elelment 也能定义比较规则，如在找到第二维最大的那一行
```
bool cmp(const vector<int> &a,const vector<int>&b){
   return a[1]<b[1];
}
cout<<max_element(a.begin(),a.end(),cmp)-a.begin()<<endl;
```

