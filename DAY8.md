## （1.）Leetcode 202.快乐树
1.思考为什么要使用**哈希**？
	&nbsp;&nbsp;当要**判断一个元素是否出现在集合中**，考虑使用哈希
2.**无限循环，求和过程中，sum会重复出现**
3.**各个位**上取数操作
```cpp
while(n){
            sum += (n % 10) * (n % 10);
            n /= 10;
        }
```
4.key value一样 用set就行
```cpp
	int getSum(int n){
        int sum = 0;
        while(n){
            sum += (n % 10) * (n % 10);
            n /= 10;
        }
        return sum;
    }

    bool isHappy(int n) {
        unordered_set<int> set;
        while(1){
            int sum = getSum(n);
            if(sum == 1){
                return true;
            }
            if(set.find(sum) !=  set.end()){
                return false;
            }else{
                set.insert(sum);
            }
            n = sum;
        }
    }
```

------------------

## 2.Leetcode算法劝退题 两数之和
1.很容易想到的是暴力求解 两层for 时间复杂度**n²**
2.**思考为什么要用哈希？**
&nbsp;&nbsp;正常思路是两个数相加然后和target对比是不是相同
&nbsp;&nbsp;但是如果换种思路：==target - 当前的值==  去哈希表中寻找有没有对应的值,这样明显会更方便
3.使用==map 存放key和value==
4.总结
&nbsp;&nbsp;个人认为这题最主要是**第2点**，想到这点，用时间复杂度更低的算法就不难了。
```cpp
vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> map;
        for(int i = 0; i < nums.size(); i++){
            auto it = map.find(target-nums[i]);
            if(it != map.end()){
                return {it->second,i};
            }
            map.insert(pair<int,int>(nums[i],i));
        }
        return {};
    }
```
----------------------

## 3.Leetcode 454.四数相加Ⅱ
**1.此题难点在于思考如何找到满足条件的方法**
&nbsp;&nbsp;正常思路是for循环 但是大概率时间复杂度过高 通不过
&nbsp;&nbsp;结合前两题的思路 就可以得出结论 我们可以**两两计算两个数组 **
&nbsp;&nbsp;然后**再在哈希表中查找是否有相反数 **， 那么就得出，我们要在数组中判断是否有这个元素出现，那么就可以知道要使用* *哈希**了
2.知道思路之后 其他的就是有手就行了
```cpp
int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        unordered_map<int,int> map;
        for(int a:nums1){
            for(int b:nums2){
                map[a+b]++;
            }
        }
        int count = 0;

        for(int c:nums3){
            for(int d : nums4){
                if(map.find(0-(c+d)) != map.end()){
                    count += map[0-(c+d)];
                }
            }
        }

        return count;
    }
  ```
-----------------------