1. 写sort时可以写函数作为cmp，写priority_queue<int,vector<int>,cmp> 时cmp为结构体
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
2. 返回vector最大值和下标 index = max_element(a.begin(),a.end())-a.begin()
    - 同时elelment 也能定义比较规则，如在找到第二维最大的那一行
```
bool cmp(const vector<int> &a,const vector<int>&b){
   return a[1]<b[1];
}
cout<<max_element(a.begin(),a.end(),cmp)-a.begin()<<endl;
```

