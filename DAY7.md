## 1.Leetcode 242.有效的字母异位词
1.理解==红黑树==和==哈希==的区别 

2.理解==stl==库中哈希的几个容器

集合：std::set std::multiset std::unordered_set 
映射：std::map std::multimap std::unordered_map
理解哪两个是==无序==的？-> 搞清楚红黑树 和 哈希表之后就很容易得出 底层为==红黑树的为有==序  底层为==哈希表==的std::unordered_map std::unordered_set 是==无序==的
其次记住 std::multiset  std::multimap  的key值可以==重复==！

3.思考为什么使用==哈希表== 用其他方法是不是也可以 ，但是时间复杂度？

4.唯一算是难点的一步为把==字符转换成整数==存储为==key==值。

5.其他的就基本思考下就能做出
```cpp
	bool isAnagram(string s, string t) {
        int index = 0;
        int ssize = s.size();
        int tsize = t.size();
        if(ssize != tsize) return false;
        int hash[26] = {0};
        while(ssize--){
            int i = s[index++] - 'a';
            hash[i]++;
        }
        index = 0;
        while(tsize--){
            int i = t[index++] - 'a';
            hash[i]--;
            if(hash[i] < 0) return false;
        }
        return true;
    }
```

-----------------------

## 2.Leetcode 349.两个数组的交集
1.本题考察的主要是对==stl==容器的用法
unordered_set容器是==无序非重复==的 在此题中的用法为==去重==

2.寻找==交集==
考察==find==用法

3.总结：难度不大 主要熟悉stl容器和哈希
```cpp
	vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> res;
        unordered_set<int> nums1Set(nums1.begin(),nums1.end());
        for(int num:nums2){
            if(nums1Set.find(num) != nums1Set.end()){
                res.insert(num);
            }
        }
        return vector<int>(res.begin(),res.end());
    }
 ```