# 容器（Container）的使用体会
![accessing_of_containers](accessing_elements_in_a_container.png)


0、vector 扩充存储的方式是指数增加分配空间，并且把自己分配的节点位置。

1、关于 array，荷兰国旗问题，调用 array 和调用 C-style 数组的效果是一样的。

2、list 的是双向链表，每个节点包含指向前一个节点和下一个节点的指针，forward_list 是指包含指向下个节点的指针的链表，和数据结构课程上学到的一样。list 执行 merge，参数list会清零，合并的 list 大小是排好队的；unique函数会删掉所有重复元素。他们overlie vector（在vector上实现）。

3、deque 是双端队列，和 vector 不同的是它存储的元素不在连续存储位置，比 vector 复杂，在需要处理相对长度大的队列，增加长度更有效率。可以用索引（index）来操作元素，当使用指针指向某个节点时，使用指针增量访问元素会导致未定义的行为。

```c++
deque<int> d {1, 2, 3, 4};
d.push_front(5);
int* i = &d[0];

cout << *(i + 2 )  << endl;   //undefined behavior
```

14、queue 是“覆盖deque的适配器容器”（或者 翻译为在 deque 基础上实现），具有先进先出（FIFO）特性；stack 也是覆盖 deque 的适配器容器，后进先出（LIFO）；priority queue还有一种例外的常规队列，第一个元素是容器内的最大元素（由对排序规范严格执行得到的结果）。元素可以在任何时刻插入，但是只有最大堆元素能被重新读取。同样 overlie vector（在vector上实现）。

![](./img/types_of_maps.png)

5、map 是关联容器，存储成对出现的元素,有四种 map，都靠 key 访问，而不是指针，ordered 指的是基于 key 排序，定制的排序可以在创建 map 时传递给构造函数，mapped 说明一个key和一个value对应，没有value的时候，可能用 NULL 表示一个值， 使用 hashing方法便于读取元素，dynamic 动态分配内存，不存在一个固定的size。map容器在根据key访问每个元素一般比 unordered_map 效率低/速度慢，但它允许使用基于顺序的直接索引应用在子集上。map 要求独立的 key，插入已经存在的 key 的时候，可能会覆盖掉已经存在的 key 或者被拒绝插入到 map，这取决于插入算法的具体写法（用[]，不用 insert 函数）。multimap 就像 regular map，允许使用等价的 keys，不产生异常信息；multimap 不包括[]()，使用 multimap::find() 来找到 key；一个 key 对应多个 value，仍可以使用索引，find() 返回第一个，并且这些值是排过序的。inert 函数返回 pair，map 的索引和 key 是否存在于 map 中[iterator itr, boolen inserted]。

6、sets 是非重复元素的集合，元素按照 key 存储，像 map，而不是索引 index，key 就是value，元素插入后不能更改，只能读取或者移除。multimap 允许存在相同 key，它们都有排序和非排序版本。

