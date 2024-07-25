## 1.Leetcode 24.两两交换链表中的节点 ==中等==
&nbsp;&nbsp;1.一定要==画图 ==
&nbsp;&nbsp;2.使用==虚拟头节点==
&nbsp;&nbsp;3.考虑==终止条件== 链表中的节点数量是==奇数==还是==偶数==
```cpp
	while(cur->next != nullptr && cur->next->next != nullptr)
```
&nbsp;&nbsp;4.==记录临时节点== 在交换节点时  我们其实要操作==3个节点==
&nbsp;&nbsp;cur节点 cur->next 和cur->next->next->next 
&nbsp;&nbsp;总结：链表还是一个==模拟==的过程 基本上都要使用虚拟头节点 需要记录节点 创建临时节点
&nbsp;&nbsp;剩下的就是画图和观察终止条件

-----------------
## 2.Leetcode 19.删除链表的倒数第N个节点 ==中等==
==错误示范== 
187 / 208 个通过的测试用例
```cpp
 ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummy = new ListNode(0);
        dummy->next = head;
        ListNode* cur = dummy;
        ListNode* tmp = cur;
        if(head != nullptr && head->next == nullptr)return NULL;//没必要判断 后面循环中就处理了
        while(n--){
            tmp = tmp->next;
        }
//缺少一步 tmp需要再走一步 需要让cur指向要删除的上一个节点
        ListNode* res = cur;
        while(cur != nullptr){//条件错误 应该是tmp != nullptr 如果是cur的话 tmp就栈溢出了
            cur = cur->next;
            if(tmp != NULL)tmp = tmp->next;
            if(tmp != NULL && tmp->next == NULL){
                ListNode *tmp1 = cur->next->next;
                cur->next = tmp1;
                break;
            }
        }
        return res->next;
}
```
==正确方法==
```cpp
ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummy = new ListNode(0);
        dummy->next = head;
        ListNode* fast = dummy;
        ListNode* slow = dummy;
        while(n-- && fast != NULL){
            fast = fast->next;
        }
        fast = fast->next;
        while(fast != NULL){
            slow = slow->next;
            fast = fast->next;
        }
        slow->next = slow->next->next;
        return dummy->next;
    }
```
&nbsp;&nbsp;1.使用==双指针==  快指针比慢指针快n+1 因为要删除指定节点的话 慢指针就要在此节点前面一位
&nbsp;&nbsp;2.使用==虚拟头节点==
&nbsp;&nbsp;3.一定要==画图==！ 我做这题的时候感觉挺简单的 直接上手做了 导致一些条件没考虑到 一定要画图！！！！