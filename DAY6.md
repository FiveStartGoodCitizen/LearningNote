## 1.Leetcode 链表相交
1.==画图==
2.注意==是指针相同== ==不是值相同==
3.思考要==从什么位置开始循环== 不难写出
```cpp
			int lena = 0 ,lenb = 0;
			        while(cura != NULL){
			            lena++;
			            cura = cura->next;
			        }
			        while(curb != NULL){
			            lenb++;
			            curb = curb->next;
			        }
 ```
剩下的就交给手
4.总结：考察的还是==模拟和逻辑==，具体的细节其实不多

------------------------
## 2.Leetcode 142.环形链表Ⅱ 中等
1.==画图==
2.判断是否有环 双指针法 
```cpp
		fast = fast->next->next;
            slow = slow->next;
```
3.思考如何找到环==开始=的=节点
这点有点困难 可以用数学的方法分析比较有意思 但是自己想出来难度挺大 具体看代码随想录分析
```cpp
			if(fast == slow){
                ListNode* index1 = fast;
                ListNode* index2 = head;
                while(index1 != index2){
                    index1 = index1->next;
                    index2 = index2->next;
                }
                return index2;
            }
```
或者可以直接==哈希==解决 自己可以试试