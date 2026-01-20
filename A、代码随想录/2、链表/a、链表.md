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

```cpp
class solution{
public:
	listnode* remove(listnode* head, int val){
		listnode* dummyhead = new listnode(0);
		dummyhead->next = head;
		listnode* cur = dummyhead;
		while(cur->next != NULL){
			if(cur->next->val == val){
				listnode* tmp = cur->next;
				cur->next = cur->next->next;
				delete tmp;
			}
			else{
				cur = cur->next;
			}
		}
		head = dummyhead->next;
		delete dummyhead;
		return head;
	}
}
```

递归的思路移除元素
```cpp
class solution{
public:
	listnode* remove(listnode* head, int val){
		if(head == nullptr){
			return nullptr;
		}
		if(head->val == val){
			listnode* newhead = remove(head->next,val);
			delete head;
			return newhead;
		}
		else{
			head->next = remove(head->next, val);
			return head;
		}
	}
}
```
