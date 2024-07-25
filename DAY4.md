## 1.Leetcode 707.设计链表 中等？？？？
有手就行 使用==虚拟头节点==更好实现
```cpp
	NodeList* dummpyHead;
	newNode->next = dummpyHead->next;
	dummpyHead->next = newNode;
```
理解链表就行 处理好之后记得把==节点指向next ==并==记录新的size==就行

## 2.Leetcode 206.反转链表
1.思路： 将==头节点指向nullptr== 再把==next节点指到cur节点==
2.记得使用==临时节点记录next节点==
3.注意要返回哪个链表 ==return pre;==
剩下的就是有手就行 