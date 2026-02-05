栈提供push 和 pop 等等接口，所有元素必须符合先进后出规则，所以栈不提供走访功能，也不提供迭代器(iterator)。 不像是set 或者map 提供迭代器iterator来遍历所有元素。

**栈是以底层容器完成其所有的工作，对外提供统一的接口，底层容器是可插拔的（也就是说我们可以控制使用哪种容器来实现栈的功能）。**

栈有多种底层实现，并且可以指定
`std::stack<int, std::vector<int>> third;`
`std::stack<int, std::list<int>> third;`

STL队列、栈都是不归类为容器的，归类为容器适配器