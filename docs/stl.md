priority_queue
----
- 定义int形从大到小(默认从小到大）的优先队列priority_queue(int, vector<int>,greater<int>) a
- 查询 top()
- 添加 push()
- 删除 pop()
set
----
- 复制一个集合:set<int>s1(s2)
- set.erase() 参数可以是迭代器也可以是数值
- set.insert()
- 二分查找auto pos = upper_bound(key) 返回迭代器

vector
----
- 初始化时需要制定大小，才能通过索引赋值，否则只能push_back()
- 添加 push_back()
- 删除 
    - pop_back()
    - erase(const_iterator pos)
- 插入 insert(const_iterator pos, a) 原来的元素向后
- 清空 clear()
