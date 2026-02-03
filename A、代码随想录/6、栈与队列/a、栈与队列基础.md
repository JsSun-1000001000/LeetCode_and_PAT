
栈有多种底层实现，并且可以指定
`std::stack<int, std::vector<int>> third;`
`std::stack<int, std::list<int>> third;`

STL队列、栈都是不归类为容器的，归类为容器适配器