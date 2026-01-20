### 定义
```cpp
struct listNode{
	int value;
	listNode* next;
	listNode(int x):value(x),next(NULL){}
}
```
要写构造

### 删除操作

移除头节点和其他节点的操作方式是不一样的，用**虚拟头节点**来统一移除节点的方法

