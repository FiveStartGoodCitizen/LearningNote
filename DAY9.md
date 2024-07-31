## 1.Leetcode 383.赎金信
1.仔细看题目真的很重要
“magazine 中的每个字符只能在 ransomNote 中使用一次。”
仔细看示例 不然就会把这道简单题思考成中等。
2.知道怎么把==字符转换成整数==
3.有手
```cpp
	bool canConstruct(string ransomNote, string magazine) {
        unordered_map<int,int> map;
        if(ransomNote.size() > magazine.size()) return false;
        for(int i = 0; i < magazine.size();i++){
            map[magazine[i] - 'a']++;
        }
        for(int j = 0; j < ransomNote.size(); j++){
            map[ransomNote[j] - 'a']--;
            if(map[ransomNote[j] - 'a'] < 0) return false;
        }
        return true;
    }
```
4.后来看题解 直接用==数组==更方便点
用==map的话还要维护红黑树，非常耗时在数据量大的情况下。==

--------------------

## 2.Leetcode 15.三数之和 ==中等==
1.本题思考的难点在于如何思考==去重==操作，由于原来的数组是==无序==的，**思考去重会更复杂**，因此首先需要==排序==。
```cpp
        sort(nums.begin(),nums.end());
```
2.**三数之和为0 举例 三数为a b c**
总体的思考路线和之前的哈希法一样== c = 0-(a + b);==
3.**对于a b c的去重才是本题的关键**
==a的去重逻辑：==
**a是第一个循环 固定不动的 如果判断a==a-1的话 数组可能越界 因此需要添加条件**
**其次是判断是使用a == a-1还是 a == a+1，如果是后者，那么{-1,-1,2}比如这种情况 直接就pass了，那么结果就收集不到。**
==b的去重逻辑：==
**b的去重逻辑和a类似 但是由于初始化的值是有a决定的 因此需要多考虑一点**
==c的去重逻辑：==
**找到c后 直接erase就行**
4.总结：
哈希的思路还可以 但是去重真的很难顶 ，其次可以使用==双指针==， 在难度上会比哈希简单点。

==哈希：==
```cpp
	vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        sort(nums.begin(),nums.end());
        for(int i = 0; i < nums.size();i++){
            if(nums[i] > 0){
                break;
            }
            if(i > 0 && nums[i] == nums[i-1]){
                continue;
            }
            unordered_set<int> set;
            for(int j = i + 1; j < nums.size();j++){
                if(j > i + 2 && nums[j] == nums[j-1] && nums[j - 1] == nums[j - 2])continue;
                int c = 0 - (nums[i] + nums[j]);
                if(set.find(c) != set.end()){
                    res.push_back({nums[i],nums[j],c});
                    set.erase(c);
                }else{
                    set.insert(nums[j]);
                }
            }
        }
        return res;
    }
```

==双指针：==
```cpp
	vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        sort(nums.begin(),nums.end());
        for(int i = 0; i < nums.size(); i++){
            if(nums[i] > 0) return res;
            if(i > 0 && nums[i] == nums[i - 1])continue;
            int left = i + 1;
            int right = nums.size() - 1;
            while(right > left){
                if(nums[i] + nums[right] + nums[left] > 0) right--;
                else if(nums[i] + nums[right] + nums[left] < 0) left++;
                else{
                    res.push_back(vector<int>{nums[i],nums[right],nums[left]});
                    while(right > left && nums[right] == nums[right-1]) right--;
                    while(right > left && nums[left] == nums[left+1]) left++;
                    right--;
                    left++;
                    };            
            }
        }
        return res;
    }
```

------------------

## 3.Leetcode 18.四数之和 中等
1.**本题和三数之和是一个思路 但是哈希贼难没d出来 用的双指针**
2.**还是需要left和right指针 三数之和中固定的数到此题就只要把==前2个数相当成一个整体==就可以了 其他的思路一摸一样**
```cpp
	vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> res;
        sort(nums.begin(),nums.end());
        for(int i = 0; i < nums.size();i++){
            if(nums[i] > target && target >= 0) break;
            if(i> 0 && nums[i] == nums[i-1])continue;
            for(int j = i+1; j < nums.size();j++){
                if(nums[i] + nums[j] > target && nums[i] + nums[j] >= 0)break;
                if(j > i+1&& nums[j] == nums[j - 1])continue;
                int left = j + 1;
                int right = nums.size() -1;
                while(right > left){
                    if((long)nums[i] + nums[j] + nums[left] + nums[right] > target) right--;
                    else if((long)nums[i] + nums[j] + nums[left] + nums[right] < target) left++;
                    else{
                        res.push_back(vector<int>{nums[i],nums[j],nums[left],nums[right]});
                        while(right>left && nums[right] == nums[right-1]) right--;
                        while(right>left && nums[left] == nums[left + 1]) left++;
                        right--;
                        left++;
                    }
                }
            }
        }
        return res;
    }
```
----------------------