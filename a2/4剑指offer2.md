# 03.数组中重复的数字

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220304212958456.png" alt="image-20220304212958456" style="zoom:80%;" />

1.哈希存 数字出现次数，大于1则返回

```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        vector<int> count(nums.size(), 0);
        for(auto x:nums) 
            if(count[x]++) return x;
        return -1;
    }
};
```

On时间，空间O1

```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        int i = 0;
        int n = nums.size();
        while(1)
        {
            while(i < n && nums[i] == i) i++;
            if(i == n) break;//数组不存在重复数字
            if(nums[i] == nums[nums[i]]) return nums[i];
            swap(nums[i],nums[nums[i]]);
        }
        return -1;
    }
};
```

