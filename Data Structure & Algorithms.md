### 数据结构
- 数组
	- 定义 一组连续的内存空间存储同类型的数据
	- 时间复杂度
		- 查找 $O(1)$
		- 插入和删除 $O(n)$
- 链表
	- 定义 元素以node形式存储，包含数据和指向其他node的指针
	- 分类
		- 单链表 只能单向访问的链表
		- 双向链表 可以双向访问的链表
		- 循环链表 首尾相接后的单链表
	- 时间复杂度
		- 查找 $O(n)$
		- 插入和删除 $O(1)$
- 栈
	- 定义 LIFO的数据结构
	- 时间复杂度
		- `push` $O(1)$
		- `pop` $O(1)$
		- `peek` $O(1)$
- 队列
	- 定义 FIFO的数据结构
	- 分类
		- Deque双端队列 可以在两端插入和删除元素
	- 时间复杂度
		- `enqueue` $O(1)$
		- `dequeue` $O(1)$
- 哈希表
	- 定义 通过hash函数（将任意大小数据映射到固定大小整数的数学函数）将key映射到array index
	- 时间复杂度 理想情况下查找、插入、删除均$O(1)$ 但可能出现冲突
	- 冲突解决方法
		- 开放地址法 发生冲突时寻找下一个可用位置解决冲突
			- 线性探测 线性步长向后寻找
			- 二次探测 平方递增的步长向后查找
			- 双重哈希 使用另一个哈希函数来确定步长
		- 链地址法 将同一个索引地址的元素以链表的形式存储
- 树
	- 定义 分层数据结构，由node组成，除root node外每个node有一个parent node和若干个child node
	- 常见二叉树
		- 完全二叉树
		- 满二叉树
		- 二叉搜索树（BST）
	- 常见操作 （以BST为例）
		- 插入 平均$O(\log n)$ 最坏$O(n)$
		- 删除 平均$O(\log n)$ 最坏$O(n)$
		- 查找 平均$O(\log n)$ 最坏$O(n)$
		- 遍历操作 见后文搜索算法
- 堆
	- 定义 特殊的完全二叉树
	- 分类
		- 最大堆
		- 最小堆
	- 常见操作
		- 插入和删除 时间复杂度$O(\log n)$
- 字典树
	- 定义 特殊的树，每个node代表一个字符，路径代表字符串
### 算法
- 排序算法
	- 冒泡排序
		- 工作原理 重复遍历，交换相邻逆序，一次遍历只能排序一个最大元素
		- 稳定性 稳定
		- 时间复杂度 $O(n) \quad O(n^2) \quad O(n^2)$
		- 空间复杂度 $O(1)$
		- 使用场景 教学示例
	- 插入排序
		- 工作原理 分为已排序和未排序两部分，一次取出一个未排序元素插入
		- 稳定性 稳定
		- 时间复杂度 $O(n) \quad O(n^2) \quad O(n^2)$
		- 空间复杂度 $O(1)$
		- 使用场景 基本有序时
	- 选择排序
		- 工作原理 直接选取最大（最小）元素的插入排序
		- 稳定性 不稳定
		- 时间复杂度 $O(n^2) \quad O(n^2) \quad O(n^2)$
		- 空间复杂度
		- 使用场景 需要易于实现的时候
	- 希尔排序
		- 工作原理 slice过后分别使用插入排序
		- 稳定性 不稳定
		- 时间复杂度 $O(n) \quad O(n^2) \quad O(n\log n)$
		- 空间复杂度 $O(1)$
		- 使用场景 大规模数据
	- 归并排序
		- 工作原理 分治算法递归排序，分割点选取中点
		- 稳定性 稳定
		- 时间复杂度 $O(n\log n) \quad O(n\log n) \quad O(n\log n)$
		- 空间复杂度 $O(n)$
		- 使用场景 大规模数据处理，尤其是链表
		- 基准元素的选择 默认选取“位置中位数”的元素进行分割
	- 快速排序
		- 工作原理 分治算法递归排序，分割点选取基于基准元素
		- 稳定性 不稳定
		- 时间复杂度 $O(n^2) \quad O(n\log n) \quad O(n\log n)$
		- 空间复杂度 $O(\log n)$
		- 使用场景 时间效率要求高，尤其是数组
		- 基准元素的选择 目标是选取“数值中位数”的元素进行分割
			- 固定选择 固定选第一个或最后一个
			- 随机选择 随机选择一个
			- 中位数 取数组中位数，时间复杂度变成$O(n\log n)$
			- 三数取中法 第一个、中间、最后一个的中位数
			- 随机化三数取中法 随机取三个，再取中位数
	- 桶排序
		- 工作原理 按照数据范围切片后排序
		- 稳定性 依据桶内排序算法确定
		- 时间复杂度 $?? \quad O(n^2) \quad O(n+k)$
		- 空间复杂度 $O(n+k)$
		- 使用场景 数据分布均匀且范围已知，浮点数或范围较大整数
	- 基数排序
		- 工作原理 非比较排序算法，根据数位排序
		- 稳定性 稳定
		- 时间复杂度 $O(d * (n + k))$
		- 空间复杂度 $O(n+k)$
		- 使用场景 整数和字符串
	- 计数排序
		- 工作原理 非比较排序算法，遍历范围内所有数，计数然后输出
		- 稳定性 稳定
		- 时间复杂度 $O(n + k)$
		- 空间复杂度 $O(k)$
		- 使用场景 范围小且为整数
	- 堆排序
		- 工作原理 用min heap依次pop
		- 稳定性 不稳定
		- 时间复杂度 $O(n\log n)$
		- 空间复杂度 $O(1)$
		- 使用场景 大规模要求空间复杂度
- 二叉树的搜索算法
	- DFS
		- 前序遍历
			- root -> left child tree -> right child tree
			- 生成树的副本或构造表达式树的前缀表达式
		- 中序遍历
			- left child tree -> root -> right child tree
			- 适用于二叉搜索树BST用于从小到大遍历
		- 后序遍历
			- left child tree -> right child tree -> root
			- 删除树中所有节点或构造表达式树的后缀表达式
		- 层序遍历 #todo 
	- BFS
		- 使用queue的FIFO性质实现
- 贪心 选取目前的最优解 容易选取到局部最优解而非全局最优解
	- A* 算法 考虑到路径代价改良后的贪心算法
		- 将起点加入open list
		- 从open list中选取总估计代价（起点到当前节点的实际代价+当前节点到目标节点的估计代价）最小的
		- 将其所有不在closed list中的相邻节点加入open list
		- 将其从open list移入closed list
- 动态规划 递归但是存储，再用就查表
- 递归 和 分治
	- 递归 划分为相同性质的子问题 需要选取结束条件并实现自我调用
	- 分治 slice为若干个子问题再求解



#todo 
1. **堆与优先队列**（2小时）
   - 理解堆的概念，尤其是二叉堆。
   - 掌握优先队列的实现和应用，如任务调度。

2. **图论基础**（3小时）
   - 学习图的表示方法（邻接矩阵、邻接表）。
   - 理解图的基本概念，如顶点、边、连通图等。
   - 掌握深度优先搜索（DFS）和广度优先搜索（BFS）。

3. **字典树（Trie）与并查集**（2小时）
   - 学习字典树的构建和查找操作，理解其应用于字符串查找的问题。
   - 掌握并查集的基本操作及其在解决连通性问题中的应用。
