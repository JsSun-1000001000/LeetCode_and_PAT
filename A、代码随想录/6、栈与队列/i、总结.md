1. C++中stack，queue 是容器么？
	- 不是，stack、queue是容器适配器，底层可以使用不同的容器
	- 默认是deque，deque是不连续的
2. 我们使用的stack，queue是属于那个版本的STL？
	- SGI
	- （一共有三个普遍的stl版本，hp、pjplauger、sgi）
3. 我们使用的STL中stack，queue是如何实现的？
	- deque
4. stack，queue 提供迭代器来遍历空间么？
	- 不提供