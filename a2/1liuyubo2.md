# 283.移动0

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204055089.png" alt="image-20220210204055089" style="zoom:80%;" />

**解法一**：

时间：o（n）空间 o（n）

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int n = nums.size();
        vector<int> arr(n);
        for(int i = 0, j = 0; i < n; i++)
            if(nums[i] != 0)
                arr[j++] = nums[i];
        nums = arr;
    }
};
```

**解法二**：

时间：o（n）空间 o（1）

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int n = nums.size();
        int j = 0;
        for(int i = 0; i < n; i++)
            if(nums[i] != 0)
                nums[j++] = nums[i];
        for(int i = j; i < n; i++)
            nums[i] = 0;
    }
};
```

swap:

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int n = nums.size();
        for(int i = 0, j = 0; i < n; i++)
            if(nums[i] != 0)
                swap(nums[j++],nums[i]);
    }
};
```

优化：针对没有0元素的数组，或者非0元素较多的数组

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int n = nums.size();
        for(int i = 0, j = 0; i < n; i++)
            if(nums[i] != 0 && i != j)
                swap(nums[j++],nums[i]);
            else if(nums[i] != 0 && i == j)
                j++;
    }
};
```

# 27.移除元素val

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204200544.png" alt="image-20220210204200544" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204218050.png" alt="image-20220210204218050" style="zoom:80%;" />

1.时间：o（n）空间 o（1）

```c
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int n = nums.size();
        int j = 0;
        for(int i = 0; i < n; i++)
            if(nums[i] != val)
                nums[j++] = nums[i];
        return j;
    }
};
```

2.时间：o（n）空间 o（1）

```c++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int n = nums.size();
        int j = 0;
        for(int i = 0; i < n; i++)
            if(nums[i] != val)
                swap(nums[j++], nums[i]);
        return j;
    }
};
```

3.时间：o（n）空间 o（1）

```c++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int n = nums.size();
        int j = 0;
        for(int i = 0; i < n; i++)
            if(nums[i] != val && i != j)
                swap(nums[j++], nums[i]);
            else if(nums[i] != val && j == i)
                j++;
        return j;
    }
};
```

**解法二**：

时间：o（n）空间 o（1）

思路：对于需要保留的元素不需要重新赋值，而是把等于value的元素，逐渐用不需要删除的元素赋值来覆盖掉。**打乱了元素顺序。**

```c++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int i = 0; 
        int j = nums.size() - 1;
        while(i <= j)
            if(nums[i] == val)
                nums[i] = nums[j--];
            else
                i++;
        return i;
    }
};
```

# **26.删除有序数组中重复元素**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204334283.png" alt="image-20220210204334283" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204351383.png" alt="image-20220210204351383" style="zoom:80%;" />

时间：o（n）空间 o（1）

```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int n = nums.size();
        int j = 1;
        for(int i = 1; i < n; i++)
            if(nums[j - 1] != nums[i])
                nums[j++] = nums[i];
        return j;
    }
};
```

# 80.删除有序数组中重复元素Ⅱ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204427741.png" alt="image-20220210204427741" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204443582.png" alt="image-20220210204443582" style="zoom:80%;" />

时间：o（n）空间 o（1）

```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size() <= 2)return nums.size();
        int j = 2;
        for(int i = 2;i < nums.size();i++){
            if(nums[j - 2] != nums[i])
                nums[j++] = nums[i];
        }
        return j;
    }
};
```

拓展：保留n个

```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums,int n) {
        if (nums.size() <= n)return nums.size();
        int j = n;
        for (int i = n; i < nums.size(); i++) {
            if (nums[j - n] != nums[i])
                nums[j++] = nums[i];
        }
        return j;
    }
};
```

有一个很大的问题：何为删除元素？是放在数组末尾吗？

# 75.颜色分类

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204513801.png" alt="image-20220210204513801" style="zoom:80%;" />

解法一

时间复杂度O（n）

空间复杂度O（K）k为数组中要排序的元素个数

```c++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int count[3] = {0};
        for(int i = 0;i < nums.size();i++)
            count[nums[i]]++;
        int index = 0;
        for(int i = 0;i < 3;i++)
            for(int j = 0;j < count[i];j++)
                nums[index++] = i;
    }
};
```

解法二

只需要遍历一遍

时间复杂度O（n）

空间复杂度O（1）

```c++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int lt = -1;
        int gt = nums.size();
        int i = 0;
        while(i < gt)
        {
            if(nums[i] < 1)
                swap(nums[++lt], nums[i++]);
            else if(nums[i] > 1)
                swap(nums[--gt], nums[i]);
            else 
                i++;
        }        
    }
};
```

# 88.合并两个有序数组

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204549550.png" alt="image-20220210204549550" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204601690.png" alt="image-20220210204601690" style="zoom:80%;" />

解法一

时间复杂度O（m+n）

空间复杂度O（m+n）

```c++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = 0;
        int j = 0;
        int k = 0;
        int t[m + n];
        while(i < m && j < n)
        {
            if(nums1[i] < nums2[j]) t[k++] = nums1[i++];
            else t[k++] = nums2[j++];
        }
        while(i < m) t[k++] = nums1[i++];
        while(j < n) t[k++] = nums2[j++];
        while(k--) nums1[k] = t[k];
    }
};
```

解法二

时间复杂度O（m+n）

空间复杂度O（1）直接对nums1赋值，不需要另辟空间

```c++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = m - 1;
        int j = n - 1;
        int k = m + n - 1;
        while(i >= 0 && j >= 0)
        {
            if(nums1[i] > nums2[j]) nums1[k--] = nums1[i--];
            else nums1[k--] = nums2[j--];
        }
        while(i >= 0) nums1[k--] = nums1[i--];
        while(j >= 0) nums1[k--] = nums2[j--];
    }
};
```

# 215. 求数组中的第K个最大元素

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204647196.png" alt="image-20220210204647196" style="zoom:80%;" />

利用快速排序。注意此题，第k大元素，索引n-1为第一大的元素，则索引n-k为第k大的元素。即找到（数组排序后）索引为n-k的元素。

- 时间复杂度：O(n)
- 空间复杂度：O(logn)

**加入随机化，可以使得时间复杂度变为O(n)。证明：算法导论9.2。**

快排1超时

```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        return quick_sort(nums, 0, nums.size() - 1, nums.size() - k);
    }
    int quick_sort(vector<int>& a, int l, int r, int k)
    {
        swap(a[l], a[rand() % (r - l + 1) + l]);
        int j = l;
        for(int i = l + 1; i <= r; i++)
            if(a[i] < a[l])
                swap(a[++j], a[i]);
        swap(a[l], a[j]);
        if(k < j) return quick_sort(a, l, j - 1, k);
        else if (k > j) return quick_sort(a, j + 1, r, k);
        else return a[k];
    }
};
```

快排2

```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        return quick_sort(nums, 0, nums.size() - 1, nums.size() - k);
    }
    int quick_sort(vector<int>& a, int l, int r, int k)
    {
        swap(a[l], a[rand() % (r - l + 1) + l]);
        int i = l + 1;
        int j = r;
        while(1)
        {
            while(i <= r && a[i] < a[l]) i++;
            while(j >= l + 1 && a[j] > a[l]) j--;
            if(i > j) break;
            swap(a[i++], a[j--]);
        }
        swap(a[l], a[j]);
        if(k < j) return quick_sort(a, l, j - 1, k);
        else if (k > j) return quick_sort(a, j + 1, r, k);
        else return a[k];
    }
};
```

快排3

```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        return quick_sort(nums, 0, nums.size() - 1, nums.size() - k);
    }
    int quick_sort(vector<int>& a, int l, int r, int k)
    {
        int lt = l;
        int gt = r + 1;
        int i = l + 1;
        while(i < gt)
        {
            if(a[i] < a[l])
                swap(a[++lt], a[i++]);
            else if(a[i] > a[l])
                swap(a[--gt], a[i]);
            else
                i++;
        }
        swap(a[l], a[lt]);
        if(k < lt) return quick_sort(a, l, lt - 1, k);
        else if (k >= gt) return quick_sort(a, gt, r, k);
        else return a[k];
    }
};
```

堆方法

```c++
class Solution {
    void shift_down(vector<int>& a, int n, int i)
    {
        while(2 * i + 1 < n)
        {
            int j = 2 * i + 1;
            if(j + 1 < n && a[j + 1] > a[j])
                j++;
            if(a[i] > a[j]) return;
            swap(a[i], a[j]);
            i = j;
        }
    }
public:
    int findKthLargest(vector<int>& nums, int k) {
        int n = nums.size();
        for(int i = n / 2 - 1; i >= 0; i--)
            shift_down(nums, n, i);
        for(int i = n - 1; i >= 0; i--)
        {
            if(i == n - k) return nums[0];
            swap(nums[0], nums[i]);
            shift_down(nums, i, 0);
        }
        return nums[n - k];
    }
};
```

# 167. 两数之和 II - 输入有序数组

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204716128.png" alt="image-20220210204716128" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204737118.png" alt="image-20220210204737118" style="zoom:80%;" />

解法一：暴力。

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& a, int target) {
        int n = a.size();
        for(int i = 0; i < n; i++)
            for(int j = i + 1; j < n; j++)
                if(a[i] + a[j] == target) 
                    return {i + 1, j + 1};
        return {};
    }
};
```

解法二：

时间复杂度：O(nlogn)

空间复杂度：O(1)

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& a, int target) {
        int n = a.size();
        for(int i = 0; i < n; i++)
        {
            int l = i + 1, r = n - 1;
            while(l < r)
            {
                int mid = l + r >> 1;
                if(a[mid] >= target - a[i]) r = mid;
                else l = mid + 1;
            }
            if(a[l] == target - a[i]) return {i + 1, l + 1};
        }
        return {};
    }
};
```

解法三：

时间复杂度：O(n)

空间复杂度：O(1)

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& a, int target) {
        int n = a.size();
        int i = 0, j = n - 1;
        while(i < j)
        {
            if(a[i] + a[j] < target) i++;
            else if(a[i] + a[j] > target) j--;
            else return {i + 1, j + 1};
        }
        return {};
    }
};
```

# 125. 验证回文串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204807362.png" alt="image-20220210204807362" style="zoom:80%;" />

解法一：

时间复杂度：O(|s|)

空间复杂度：O(1) 无需开辟额外空间

```c++
class Solution {
public:
    bool isPalindrome(string s) {
        int n = s.size();
        int j = 0;
        for(int i = 0;i < s.size();i++)
            if(isalnum(s[i]))
                swap(s[j++],s[i]);
        s.resize(j);
        bool result = true;
        for(int i = 0;i < s.size() / 2;i++)
            if(tolower(s[i]) != tolower(s[s.size() - 1 - i]))
            {
                result = false;
                break;
            }
        return result;
    }
};
```

解法二：原地操作

时间复杂度：O(|s|)

空间复杂度：O(1) 

```c++
class Solution {
public:
    bool isPalindrome(string s) {
        int n = s.size();
        int i = 0, j = n - 1;
        while(i < j)
        {
            while(i < j && !isalnum(s[i])) i++;
            while(i < j && !isalnum(s[j])) j--;
            if(tolower(s[i]) != tolower(s[j])) return false;
            i++;
            j--;
        }
        return true;
    }
};
```

# 344.反转字符串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204843561.png" alt="image-20220210204843561" style="zoom:80%;" />

时间复杂度：O(n)

空间复杂度：O(1) 

```c++
class Solution {
public:
    void reverseString(vector<char>& s) {
        for(int i = 0;i < s.size() / 2 ;i++)
            swap(s[i],s[s.size() - 1 - i]);
    }
};
```

```c++
class Solution {
public:
    void reverseString(vector<char>& s) {
        int i = 0;
        int j = s.size() - 1;
        while(i < j)
            swap(s[i++],s[j--]);
    }
};
```

# 345. 反转字符串中的元音字母

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204913994.png" alt="image-20220210204913994" style="zoom:80%;" />

时间复杂度：O(n)

空间复杂度：O(1)

```c++
class Solution {
    bool f(char& c)
    {
        return (c == 'a') || (c == 'e') || (c == 'i') || (c == 'o') || (c == 'u') || (c == 'A') || (c == 'E') || (c == 'I') || (c == 'O') || (c == 'U');
    }
public:
    string reverseVowels(string s) {
        int i = 0, j = s.size() - 1;
        while(i < j)
        {
            while(i < j && !f(s[i])) i++;
            while(i < j && !f(s[j])) j--;
            swap(s[i++], s[j--]);
        }
        return s;
    }
};
```

# 11.盛最多水的容器

给定一个长度为 `n` 的整数数组 `height` 。有 `n` 条垂线，第 `i` 条线的两个端点是 `(i, 0)` 和 `(i, height[i])` 。

找出其中的两条线，使得它们与 `x` 轴共同构成的容器可以容纳最多的水。

返回容器可以储存的最大水量。

**说明：**你不能倾斜容器。

**示例 1：**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204950851.png" alt="image-20220210204950851" style="zoom:80%;" />

```
输入：[1,8,6,2,5,4,8,3,7]
输出：49 
解释：图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。
```

**示例 2：**

```
输入：height = [1,1]
输出：1
```

**提示：**

- `n == height.length`
- `2 <= n <= 105`
- `0 <= height[i] <= 104`

暴力

```c++
class Solution {
public:
    int maxArea(vector<int>& h) {
        int n = h.size();
        int res = 0;
        for(int i = 0; i < n; i++)
            for(int j = i + 1; j < n; j++)
                res = max(res, min(h[i], h[j]) * (j - i));
        return res;
    }
};
```

```c++
class Solution {
public:
    int maxArea(vector<int>& h) {
        int i = 0, j = h.size() - 1;
        int res = 0;
        while(i < j)
        {
            res = max(res, min(h[i], h[j]) * (j - i));
            if(h[i] < h[j]) i++;
            else j--;
        }
        return res;
    }
};
```

# 209.长度最小的子数组

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210205110714.png" alt="image-20220210205110714" style="zoom:80%;" />

暴力

```c++
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int n = nums.size();
        for(int size = 1; size <= n; size++)
            for(int i = 0; i + size - 1 < n; i++)
            {
                int sum = 0;
                for(int j = i + size - 1; j >= i; j--)
                    sum += nums[j];
                if(sum >= target) return size;
            } 
        return 0;
    }
};
```

双指针

```c++
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int n = nums.size();
        int sum = 0, len = INT_MAX;
        for(int i = 0, j = 0; i < n; i++)
        {
            sum += nums[i];
            while(sum - nums[j] >= target) sum -= nums[j++];
            if(sum >= target) len = min(len, i - j + 1);
        }
        return len == INT_MAX ? 0 : len;
    }
};
```

# 3. 无重复字符的最长子串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210205148399.png" alt="image-20220210205148399" style="zoom:80%;" />

 时间复杂度：O(N)

空间复杂度：O(∣Σ∣) Σ表示ASCII码的个数（123）

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int n = s.size();
        int i = 0, j = -1;
        int hash[128] = {0};
        int res = 0;
        while(i < n)
        {
            if(j + 1 < n && !hash[s[j + 1]])
                hash[s[++j]]++;
            else 
                hash[s[i++]]--;
            res = max(res, j - i + 1);
        }
        return res;
    }
};
```

# 438. 找到字符串中所有字母异位词

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210205218992.png" alt="image-20220210205218992" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        vector<int> ph(128, 0);
        vector<int> h(128, 0);
        int sn = s.size(), pn = p.size();
        for(auto& c : p) ph[c]++;
        int i = 0, j = 0;
        vector<int> res;
        for(j = 0; j < pn && j < sn; j++)
            h[s[j]]++;
        if(h == ph) res.push_back(i);
        while(j < sn) {
            h[s[j++]]++;
            h[s[i++]]--;
            if(h == ph) res.push_back(i);
        }
        return res;
    }
};
```

# 76.最小覆盖子串

![image-20240113224830541](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240113224830541.png)

```c++
class Solution {
public:
    string minWindow(string s, string t) {
        int ht[128] = {0};
        int h[128] = {0};
        for(auto& c : t) ht[c]++;
        string res;
        for(int i = 0, j = 0, cnt = 0; i < s.size(); i++) {
            h[s[i]]++;
            if(h[s[i]] <= ht[s[i]]) cnt++;
            while(h[s[j]] > ht[s[j]]) h[s[j++]]--;
            if(cnt == t.size() && (res == "" || res.size() > (i - j + 1)))
                res = s.substr(j, i - j + 1);
        }
        return res;
    }
};
```

# 349.两个数组的交集

![image-20240113225843260](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240113225843260.png)

```c++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> s;
        vector<int> res;
        for(auto& x : nums1) s.insert(x);
        for(auto& x : nums2) 
            if(s.count(x)) {
                res.push_back(x);
                s.erase(x);
            }
        return res;
    }
};
```









# 150.逆波兰表达式求值

![image-20230907184649800](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230907184649800.png)

```c++
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> stk;
        for(auto s : tokens)
        {
            if((!(isdigit(s[0])) && isdigit(s[1])) || isdigit(s[0]))
                stk.push(stoi(s));
            else
            {
                int a = stk.top(); stk.pop();
                int b = stk.top(); stk.pop();
                switch (s[0])
                {
                    case '+' : stk.push(b + a);break;
                    case '-' : stk.push(b - a);break;
                    case '*' : stk.push(b * a);break;
                    case '/' : stk.push(b / a);break;
                }
            }
        }
        return stk.top();
    }
};
```

# 15.三数之和

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210210112563.png" alt="image-20220210210112563" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        vector<vector<int>> res;
        int n = nums.size();
        // if(nums.size() < 3 || nums[0] > 0 || nums[n - 1] < 0)
        //     return res;
        // if(!nums[0] && !nums[n - 1])
        //     return {{0, 0, 0}};
        for(int i = 0; i < n - 2; i++ ) {
            if(i > 0 && nums[i] == nums[i - 1]) continue;
            int j = i + 1;
            int k = n - 1;
            while(j < k) {
                int t = nums[i] + nums[j] + nums[k];
                if(t < 0) j++;
                else if(t > 0) k--;
               	else {
                    res.push_back({nums[i], nums[j], nums[k]});
                    j++;
                    k--;
                    while(j < k && nums[j] == nums[j - 1]) j++;
                    while(j < k && nums[k] == nums[k + 1]) k--;
                }
            }
        }
        return res;
    }
};
```

