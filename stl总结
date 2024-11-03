# C++ STL常用容器完整指南

## 1. 顺序容器

### 1.1 vector（变长数组）
```
特点：
- 连续内存，支持随机访问
- 尾部插入/删除O(1)，中间插入/删除O(n)
- 自动扩容（2倍增长）
- 适合频繁随机访问，较少插入删除的场景

常用操作：
push_back()   // 尾部添加
pop_back()    // 尾部删除
insert()      // 指定位置插入
erase()       // 删除指定位置
size()        // 当前大小
capacity()    // 当前容量
reserve()     // 预分配空间
clear()       // 清空元素

内存结构：
[  |  |  |  |  |  |  |  ]  capacity
[1 |2 |3 |4 |  |  |  |  ]  size = 4
```

### 1.2 deque（双端队列）
```
特点：
- 分段连续内存
- 两端插入/删除O(1)
- 支持随机访问（但比vector慢）
- 适合两端频繁操作的场景

常用操作：
push_back()   // 尾部添加
push_front()  // 头部添加
pop_back()    // 尾部删除
pop_front()   // 头部删除
size()        // 当前大小
clear()       // 清空元素

内存结构：
控制中心
[ptr|ptr|ptr|ptr]  指向多个缓冲区
   ↓   ↓   ↓   ↓
[...][...][...][...]  数据分散存储
```

### 1.3 queue（队列）
```
特点：
- FIFO（先进先出）
- 基于deque实现
- 只能访问队首和队尾元素
- 适合需要FIFO的场景

常用操作：
push()    // 入队
pop()     // 出队
front()   // 访问队首
back()    // 访问队尾
empty()   // 判空
size()    // 大小

示意图：
[1|2|3|4|5] ← push
 ↑     
pop → [2|3|4|5]
```

### 1.4 stack（栈）
```
特点：
- LIFO（后进先出）
- 基于deque实现
- 只能访问栈顶元素
- 适合需要LIFO的场景

常用操作：
push()    // 入栈
pop()     // 出栈
top()     // 访问栈顶
empty()   // 判空
size()    // 大小

示意图：
[4] ← top
[3]
[2]
[1]
```

## 2. 关联容器

### 2.1 set/multiset
```
特点：
set:
- 有序不重复集合
- 基于红黑树实现
- 查找、插入、删除O(logN)
- 适合需要有序且不重复的场景

multiset:
- 有序可重复集合
- 其他特性同set

常用操作：
insert()      // 插入元素
erase()       // 删除元素
find()        // 查找元素
count()       // 统计元素个数
lower_bound() // 第一个大于等于值
upper_bound() // 第一个大于值

内部结构（红黑树）：
    [4]
   /   \
 [2]   [6]
 / \   / \
[1][3][5][7]
```

### 2.2 unordered_set
```
特点：
- 无序不重复集合
- 基于哈希表实现
- 平均O(1)查找、插入、删除
- 适合需要快速查找且不要求有序的场景

常用操作：
insert()   // 插入
erase()    // 删除
find()     // 查找
count()    // 统计个数

内部结构（哈希表）：
[0] → [a|next]
[1] → [b|next] → [f|next]
[2] → [c|next]
[3] 
[4] → [d|next] → [e|next]
```

## 3. 工具类

### 3.1 pair
```
特点：
- 将两个元素组合成一个元素
- 常用于map的键值对、图论中的边等
- 支持比较运算（先比较first，再比较second）

使用方式：
pair<T1, T2> p;
p.first   // 第一个元素
p.second  // 第二个元素
make_pair(a, b)  // 创建pair

示例：
pair<string, int> p("hello", 1);
pair<int, int> edge(1, 2);  // 图的边
```

## 4. 效率对比

### 4.1 时间复杂度
```
操作       vector   deque    set      unordered_set
查找       O(n)     O(n)     O(logn)  O(1)
插入头部   O(n)     O(1)     O(logn)  O(1)
插入尾部   O(1)     O(1)     O(logn)  O(1)
插入中间   O(n)     O(n)     O(logn)  O(1)
删除头部   O(n)     O(1)     O(logn)  O(1)
删除尾部   O(1)     O(1)     O(logn)  O(1)
删除中间   O(n)     O(n)     O(logn)  O(1)
```

### 4.2 使用场景建议

1. 需要高效随机访问：vector
2. 需要频繁在两端操作：deque
3. 需要FIFO：queue
4. 需要LIFO：stack
5. 需要有序集合：set/multiset
6. 需要快速查找且不关心顺序：unordered_set
7. 需要键值对：pair

## 5. 常见陷阱

1. vector扩容导致迭代器失效
```cpp
vector<int> v = {1,2,3};
auto it = v.begin();
v.push_back(4);  // 扩容，it失效
```

2. 边遍历边删除元素
```cpp
// 错误方式
for(auto it = v.begin(); it != v.end(); ++it) {
    if(*it == 1) v.erase(it);  // 迭代器失效
}

// 正确方式
for(auto it = v.begin(); it != v.end();) {
    if(*it == 1) it = v.erase(it);
    else ++it;
}
```

3. 访问空容器
```cpp
vector<int> v;
v[0] = 1;     // 未定义行为
v.front();    // 未定义行为
```

## 6. 使用建议

1. 优先使用vector
   - 除非有特殊需求，vector是最常用和最高效的容器

2. 需要在两端操作时使用deque
   - 比vector在首部操作更高效

3. 需要集合操作时：
   - 要求有序：使用set
   - 不要求有序：使用unordered_set
   - 要求重复：使用multiset

4. pair的使用：
   - 优先使用make_pair创建
   - 考虑使用tie进行解包

5. 容器选择准则：
   - 是否需要随机访问
   - 是否需要频繁插入/删除
   - 是否需要有序性
   - 是否允许重复元素
