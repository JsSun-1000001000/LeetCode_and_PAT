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

## [707. 设计链表 - 力扣（LeetCode）](https://leetcode.cn/problems/design-linked-list/)
```cpp
class MyLinkedList {

public:

    struct listnode{

        int val;

        listnode* next;

        listnode(int x):val(x),next(nullptr){}

    };

  

    MyLinkedList() {

        //定义一个虚拟头节点

        dummyhead = new listnode(0);

        size = 0;

    }

    int get(int index) {

        if(index < 0 || index > size-1){

            return -1;

        }

        listnode* cur = dummyhead->next;

        while(index--){

            cur = cur->next;

        }

        return cur->val;

    }

    void addAtHead(int val) {

        listnode* newnode = new listnode(val);

        newnode->next = dummyhead->next;

        dummyhead->next = newnode;

        size++;

    }

    void addAtTail(int val) {

        listnode* newnode = new listnode(val);

        listnode* cur = dummyhead;

        while(cur->next != nullptr){

            cur = cur->next;

        }

        cur->next = newnode;

        size++;

    }

    void addAtIndex(int index, int val) {

        //先遍历后插入

        if(index < 0){

            index = 0;

        }

        if(index > size){

            return;

        }

        listnode* cur = dummyhead;

        listnode* newnode = new listnode(val);

        while(index--){

            cur = cur->next;

        }

        newnode->next = cur->next;

        cur->next = newnode;

        size++;

    }

    void deleteAtIndex(int index) {

        if(index < 0 || index > size-1){

            return;

        }

        listnode* cur = dummyhead;

        while(index--){

            cur = cur->next;

        }

        listnode* tmp = cur->next;

        cur->next = cur->next->next;

        delete tmp;

        size--;

    }

    void printLinkedList() {

        listnode* cur = dummyhead;

        while (cur->next != nullptr) {

            cout << cur->next->val << " ";

            cur = cur->next;

        }

        cout << endl;

    }

    private:

    int size;

    listnode* dummyhead;

};

  

/**

 * Your MyLinkedList object will be instantiated and called as such:

 * MyLinkedList* obj = new MyLinkedList();

 * int param_1 = obj->get(index);

 * obj->addAtHead(val);

 * obj->addAtTail(val);

 * obj->addAtIndex(index,val);

 * obj->deleteAtIndex(index);

 */
```