## 2.4-------------------5

### 283.移动0

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204055089.png" alt="image-20220210204055089" style="zoom:80%;" />

**解法一**：

时间：o（n）空间 o（n）

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int n = nums.size();
        if(n <= 0) return; 
        vector<int> arr(n,0);
        for(int i = 0,j = 0;i < n;i++)
        {
            if(nums[i])
                arr[j++] = nums[i];
        }
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
        if(n <= 0) return; 
        int j = 0;
        for(int i = 0;i < n;i++)
        {
            if(nums[i])
                nums[j++] = nums[i];
        }
        for(int i = j;i < n;i++)
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
        if(n <= 0) return; 
        int j = 0;
        for(int i = 0;i < n;i++)
        {
            if(nums[i])
                swap(nums[j++],nums[i]);
        }
    }
};
```

优化：针对没有0元素的数组，或者非0元素较多的数组

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int n = nums.size();
        if(n <= 0) return; 
        int j = 0;
        for(int i = 0;i < n;i++)
        {
            if(nums[i] && j != i)
                swap(nums[j++],nums[i]);
            else if(nums[i] && j == i)
                j++;
        }
    }
};
```

### 27.移除元素val

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204200544.png" alt="image-20220210204200544" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204218050.png" alt="image-20220210204218050" style="zoom:80%;" />

**解法一：**时间：o（n）空间 o（n）

**保留了剩余元素的相对顺序。**

```c++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int n = nums.size();
        vector<int> arr(n,val);
        int j = 0;
        for(int i = 0;i < n;i++)
        {
            if(nums[i] != val)
                arr[j++] = nums[i];
        }
        nums = arr;
        return j;
    }
};
```

2.时间：o（n）空间 o（1）

```c
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int i = 0;
        int j = 0;
        int n = nums.size();
        for(int i = 0;i < n;i++)
        {
            if(nums[i] != val)
                nums[j++] = nums[i];
        }
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
        if(n <= 0) return 0;
        int j = 0;
        for(int i = 0;i < n;i++)
        {
            if(nums[i] != val)
                swap(nums[j++],nums[i]);
        }
        return j;
    }
};
```

4.时间：o（n）空间 o（1）

```c++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int n = nums.size();
        if(n <= 0) return 0;
        int j = 0;
        for(int i = 0;i < n;i++)
        {
            if(nums[i] != val && i != j)
                swap(nums[j++],nums[i]);
            else if(nums[i] != val && i == j)
                j++;
        }
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
        {
            if(nums[i] == val)
                    nums[i] = nums[j--];
            else
                i++;
        }
        return i;
    }
};
```

### **26.删除有序数组中重复元素**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204334283.png" alt="image-20220210204334283" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204351383.png" alt="image-20220210204351383" style="zoom:80%;" />

时间：o（n）空间 o（1）

```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size()<=1)return nums.size();
        int j=1;
        for(int i=1;i<nums.size();i++){
            if(nums[j-1]!=nums[i])
                nums[j++]=nums[i];
        }
        return j;
    }
};
```

### 80.删除有序数组中重复元素（每个元素最多保留2个）

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

### 75.颜色分类（计数排序）

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
    void sortColors(vector<int>& arr) {
        int lt = -1;
        int i = 0;
        int gt = arr.size();
        while(i < gt)
        {
            if(arr[i] < 1)
                swap(arr[++lt],arr[i++]);
            else if(arr[i] > 1)
                swap(arr[--gt],arr[i]);
            else 
                i++;
        }
    }
};
```

## 2.5-------------------10

### 88.合并两个有序数组

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204549550.png" alt="image-20220210204549550" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204601690.png" alt="image-20220210204601690" style="zoom:80%;" />

解法一

时间复杂度O（m+n）

空间复杂度O（m+n）

```c++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        vector<int> num;
        int i = 0;
        int j = 0;
        while(i < m && j < n)
        {
            if(nums1[i] < nums2[j]) num.push_back(nums1[i++]);
            else num.push_back(nums2[j++]);
        }
        while(i < m) num.push_back(nums1[i++]);
        while(j < n) num.push_back(nums2[j++]);
        nums1 = num;
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

### 215. 求数组中的第K个最大元素

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204647196.png" alt="image-20220210204647196" style="zoom:80%;" />

利用快速排序。注意此题，第k大元素，索引n-1为第一大的元素，则索引n-k为第k大的元素。即找到（数组排序后）索引为n-k的元素。

- 时间复杂度：O(n)
- 空间复杂度：O(logn)

**加入随机化，可以使得时间复杂度变为O(n)。证明：算法导论9.2。**

```c++
class Solution {
    int partition(vector<int>& nums,int k,int l,int r)
    {
        int j = r;
        int i = l + 1;
        swap(nums[l],nums[rand() % (r - l + 1) + l]);
        while(1)
        {
            while(i <= r && nums[i] < nums[l]) i++;
            while(j >= l + 1 && nums[j] > nums[l]) j--;
            if(i >= j) break;
            swap(nums[i++],nums[j--]);
        }
        swap(nums[l],nums[j]);
        if(k == j) return k;
        else if (k > j) return partition(nums,k,j + 1,r);
        else return partition(nums,k,l,j - 1);
    }
public:
    int findKthLargest(vector<int>& nums, int k) {
        srand(time(nullptr));
        int index =  partition(nums,nums.size() - k,0,nums.size() - 1);
        return nums[index];
    }
};
```

堆方法

```c++
class Solution {
    void shift_down(vector<int>& arr,int n,int i)
    {
        while(2 * i + 1 < n)
        {
            int j = 2 * i + 1;
            if(j + 1 < n && arr[j + 1] > arr[j])
                j = j + 1;
            if(arr[i] > arr[j]) return;
            swap(arr[i], arr[j]);
            i = j;
        }
    }
public:
    int findKthLargest(vector<int>& arr, int k) {
        int n = arr.size();
        for(int i = (n - 2) / 2;i >= 0;i--)
            shift_down(arr, n, i);
        for(int i = n - 1;i >= n - k;i--)
        {
            swap(arr[0], arr[i]);
            shift_down(arr, i, 0);
        }
        return arr[n - k];
    }
};
```

### 167. 两数之和 II - 输入有序数组

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204716128.png" alt="image-20220210204716128" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204737118.png" alt="image-20220210204737118" style="zoom:80%;" />

解法一：暴力。

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& arr, int target) {
        if(arr.size() <= 2) return {1,2};
        for(int i = 0;i < arr.size();i++)
            for(int j = i + 1; j < arr.size();j++)
                if(arr[i] + arr[j] == target)
                    return vector<int>{i + 1,j + 1};
        return vector<int>();
    }
};
```

解法二：

时间复杂度：O(nlogn)

空间复杂度：O(1)

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& arr, int target) {
        int n = arr.size();
        for(int i = 0;i < n - 1;i++)
        {
            int l = i + 1;
            int r = n - 1;
            while(l <= r)
            {
                int mid = l + r >> 1;
                if(target - arr[i] < arr[mid]) 
                    r = mid - 1;
                else if(target - arr[i] > arr[mid])
                    l = mid + 1;
                else
                    return {i + 1,mid + 1};
            }
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
    vector<int> twoSum(vector<int>& arr, int target) {
        int n = arr.size();
        int i = 0;
        int j = n - 1;
        while(i < j)
        {
            if(arr[i] + arr[j] < target) i++;
            else if(arr[i] + arr[j] > target) j--;
            else return {i + 1,j + 1};
        }
        return {};
    }
};
```

### 125. 验证回文串

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
        bool result = true;
        int i = 0;
        int j = s.size() - 1;
        while(i < j)
        {
            while(i < j && !isalnum(s[i])) i++;
            while(j > i && !isalnum(s[j])) j--;
            if(tolower(s[i++]) != tolower(s[j--]))
            {
                result = false;
                break;
            }
        }
        return result;
    }
};
```

### 344.反转字符串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204843561.png" alt="image-20220210204843561" style="zoom:80%;" />

时间复杂度：O(n)

空间复杂度：O(1) 

```c++
class Solution {
public:
    void reverseString(vector<char>& s) {
        for(int i = 0;i < s.size() / 2 ;i++){
            int j = s.size() - 1 - i;
            swap(s[i],s[j]);
        }
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

## 2.6--------------------15

### 345. 反转字符串中的元音字母

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204913994.png" alt="image-20220210204913994" style="zoom:80%;" />

时间复杂度：O(n)

空间复杂度：O(1)

```c++
class Solution {
    bool func(char& ch)
    {
        if(ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u' || ch == 'A' || ch == 'E' || ch == 'I' || ch == 'O' || ch == 'U')
            return true;
        return false;
    }
public:
    string reverseVowels(string s) {
        int i = 0;
        int j = s.size() - 1;
        while(i < j)
        {
            while(i < j && !func(s[i])) i++;
            while(i < j && !func(s[j])) j--;
            swap(s[i++],s[j--]);
        }
        return s;
    }
};
```

### 11. 盛最多水的容器

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210204950851.png" alt="image-20220210204950851" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210205021958.png" alt="image-20220210205021958" style="zoom: 80%;" />

解法一：

时间复杂度：O(N)

空间复杂度：O(1)

```c++
class Solution {
public:
    int maxArea(vector<int>& height) {
        int i=0;
        int j=height.size()-1;
        int max=0;
        while(i < j){
            int area=(j-i)*min(height[i],height[j]);
            max=(max>=area)?max:area;
            
            if(height[i]<=height[j]){
                i++;
            }
            else
                j--;
        }
        return max;
    }
};
```

解法二：

时间复杂度O(n^2)

空间复杂度O(n^2)

```c++
class Solution {
public:
    int maxArea(vector<int>& height) {
        int i=0;
        int n=height.size();
        int j;

        vector<int> area;
        for(i=0;i<=n-2;i++)
            for(j=i+1;j<=n-1;j++)
                area.push_back((j-i)*min(height[i],height[j]));
        int max=area[0];
        for(int i=0;i<=n*(n-1)/2-1;i++){
            if(area[i]>=max)
                max=area[i];
        }
        return max;

        
    }
};
```

### 209长度最小的子数组

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210205110714.png" alt="image-20220210205110714" style="zoom:80%;" />

解法一：

时间复杂度O(n)

空间复杂度O(1)

```c++
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int l=0;
        int r=-1;
        int s=0;
        int n=nums.size();
        int res=n+1;
        while(l<n){
            if(r+1<n&&s<target)
                s+=nums[++r];
            else
                s-=nums[l++];
            if(s>=target)
                res=min(res,r-l+1);
        }
        if(res==nums.size()+1) return 0;
        return res;
    }
};
```

解法二：暴力解法

时间复杂度O(n^2)

空间复杂度O(n)

```c++
class Solution {
public:
    int sum(vector<int>& nums,int k){
        int s=0;
        for(int i=0;i<=k;i++){
            s+=nums[i];
        }
        return s;
    }
    int minSubArrayLen(int target, vector<int>& nums) {
        int n=nums.size();
        int res=n+1;
        vector<int> sums;
        sums.clear();
        for(int i=0;i<n;i++)
            sums.push_back(sum(nums,i));
        for(int i=0;i<n;i++){
            for(int j=i;j<n;j++){
                if(sums[j]-sums[i]+nums[i]>=target){
                    res=min(res,j-i+1);
                }
            }
        }
        if(res==n+1)return 0;
        return res;
    }
};
```

解法三：暴力解法

时间复杂度O(n^3)

空间复杂度O(1)

```c++
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int n=nums.size();
        for(int i=1;i<=n;i++){
            for(int k=0;k<=n-i;k++){
                int s=0;
                for(int j=k;j<=k+i-1;j++){
                    s=s+nums[j];
                }
                if(s>=target)
                    return i;
            }
        }
        return 0;
    }
};
```

### 3. 无重复字符的最长子串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210205148399.png" alt="image-20220210205148399" style="zoom:80%;" />

 时间复杂度：O(N)

空间复杂度：O(∣Σ∣) Σ表示ASCII码的个数（123）

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int i=0;
        int j=-1;
        int freq[256]={0};
        int res=0;
        while(i<s.size()){
            if(j+1<s.size()&&freq[s[j+1]]==0)
                freq[s[++j]]++;
            else
                freq[s[i++]]--;

            res=max(res,j-i+1);
        }
        return res;
    }
};
```

### 438. 找到字符串中所有字母异位词

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210205218992.png" alt="image-20220210205218992" style="zoom:80%;" />

解法二：滑动窗口

```c++
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        vector<int> result;
        vector<int> freqp(128,0);      //保存p的字符信息
        vector<int> win(128,0);        //记录窗口win的字符信息

        if(p.size()>s.size()) return result;    //输入不合法返回空数组
        
        //首先：
        //记录p的字符信息，以及窗口初始位置时(下标为0)的字符信息
        //p的字符信息在之后也是固定不变的
        for(int i=0;i<p.size();i++){
            freqp[p[i]]++;
            win[s[i]]++;
        }
        
        //开始滑动窗口，依次遍历
        for(int i=0;i<=s.size()-p.size();i++){
            //若p和窗口的字符信息相等，记录起始索引i
            if(win==freqp)
                result.push_back(i);
            
            //每滑动一步，删除原来窗口的第一个字符的信息
            //           并将原来窗口最外(右)侧的第一个字符新添加进来，保持窗口长度不变
            win[s[i]]--;
            win[s[i+p.size()]]++;
        }
        return result;
    }
};
```

## 2.7---------------------20

### 76.最小覆盖子串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210205329371.png" alt="image-20220210205329371" style="zoom:80%;" />

```c++
class Solution {
public:
    string minWindow(string s, string t) {
        unordered_map<char,int> ht;
        unordered_map<char,int> hs;
        for(auto x:t)
            ht[x]++;
        int j = 0;
        int cnt = 0;
        string res;
        for(int i=0;i<s.size();i++){
            hs[s[i]]++;
            if(hs[s[i]]<=ht[s[i]]) cnt++;

            while(hs[s[j]]>ht[s[j]]) hs[s[j++]]--;

            if(cnt == t.size()){
                if(res.empty() || res.size() > (i-j+1)){
                    res=s.substr(j,i-j+1);
                }
            }
        }
        return res;
    }
};
```

### 349.两个数组的交集

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220207215445977.png" alt="image-20220207215445977" style="zoom: 80%;" />

时间复杂度：O(n*1)

空间复杂度：O(n) 

```c++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> record(nums1.begin(),nums1.end());
        
        unordered_set<int> resultSet;
        for(int i=0;i<nums2.size();i++)
            if(record.find(nums2[i])!=record.end())
                resultSet.insert(nums2[i]);
        
        return vector<int>(resultSet.begin(),resultSet.end());
    }
};
```

### 350. 两个数组的交集 II

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220207221036215.png" alt="image-20220207221036215" style="zoom: 80%;" />

时间复杂度：O(n*1)

空间复杂度：O(n) 

```c++
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        unordered_map<int,int> record;
        for(auto a:nums1)
            record[a]++;
        vector<int> result;
        for(auto b:nums2){
            if(record[b]-->0)
                result.push_back(b);
        }
        return result;
    }
};
```

### 242.有效的字母异位词

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220207233542502.png" alt="image-20220207233542502" style="zoom:80%;" />

解法一：

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        vector<int> freq(128,0);
        for (char ch : s)
            freq[ch]++;
        for (char ch : t)
            freq[ch]--;
        return freq ==vector<int>(128,0);
    }
};
```

解法二：

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        unordered_map<char, int> maps;
        unordered_map<char, int> mapt;
        for (char ch : s)
            maps[ch]++;
        for (char ch : t)
            mapt[ch]++;
        return maps == mapt;
    }
};
```

### 202.快乐数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220208155236980.png" alt="image-20220208155236980" style="zoom:80%;" />

利用map记录，循环中每个数出现的次数

```c++
class Solution {
public:
    int func(int n){
        int sum=0;
        while(n>0){
            int d=n%10;
            n/=10;
            sum+=d*d;
        }
        return sum;
    }
    bool isHappy(int n) {
        
        unordered_map<int,int> map;
        while(n!=1&&map[n]==0){//一种是因为n==1跳出循环，一种是因为map[n]已经存在开始进入循环							//但是这个n不等于1，也就是循环中没有1
            map[n]++;
            n=func(n);
        }
        return n==1;
    }
};
```

解法二：

利用双指针进行遍历

```c++
class Solution {
public:
    int getNext(int n){
        int sum=0;
        while(n>0){
            int d=n%10;
            n/=10;
            sum+=d*d;
        }
        return sum;
    }
    bool isHappy(int n) {
        int slow=n;
        int fast=n;
        do{
            slow=getNext(slow);
            fast=getNext(fast);
            fast=getNext(fast);
        }while(slow!=fast);
        return slow==1;
    }
};
```

## 2.8-------------------25

### 290. 单词规律

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220208183258904.png" alt="image-20220208183258904" style="zoom:80%;" />

均摊时间复杂度为 O(n + m)

空间复杂度：O(n + m)

```c++
class Solution {
public:
    bool wordPattern(string pattern, string s) {
        unordered_map<string,char> stc;
        unordered_map<char,string> cts;
        int i=0;
        for(auto ch:pattern){
            int j=i;
            if(i>s.size()) return false;
            while(j<s.size()&&(s[j]!=' ')) j++;
            string tmp=s.substr(i,j-i);
            if(stc.count(tmp) && stc[tmp]!=ch)
                return false;
            if(cts.count(ch) && cts[ch]!=tmp)
                return false;
            stc[tmp]=ch;
            cts[ch]=tmp;
            i=j+1;
        }
        return i>=s.size();
    }
};
```

### 205. 同构字符串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210205437495.png" alt="image-20220210205437495" style="zoom:80%;" />

时间复杂度：O(n)，其中 n 为字符串的长度。我们只需同时遍历一遍字符串 s和t 即可。
空间复杂度：O(∣Σ∣) ascii码长度

```c++
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        unordered_map<char,char> s2t;
        unordered_map<char,char> t2s;
        if(s.size()!=t.size()) return false;
        for(int i=0;i<s.size();i++){
            if(s2t.count(s[i])&&s2t[s[i]]!=t[i]||t2s.count(t[i])&&t2s[t[i]]!=s[i])
                return false;
            s2t[s[i]]=t[i];
            t2s[t[i]]=s[i];
        }
        return true;
    }
};
```

### 451.根据字符出现频率排序

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210205526923.png" alt="image-20220210205526923" style="zoom:80%;" />

```c++
bool cmp(pair<char,int> a,pair<char,int> b){
    return a.second>b.second;
}
class Solution {
public:

    int contain(char x,vector<pair<char,int>>& vec){
        for(int i=0;i<vec.size();i++)
            if(vec[i].first == x) return i;
        return -1;
    }
    string frequencySort(string s) {
        vector<pair<char,int>> vec;
        for(auto x:s){
            if(contain(x,vec)!=-1){
                vec[contain(x,vec)].second++;
            }
            else
                vec.emplace_back(x,1);
        }
        sort(vec.begin(),vec.end(),cmp);
        string res;
        for(auto x:vec){
            for(int i=0;i< x.second;i++){
                res += x.first;
            }
        }
        return res;
    }
};
```

### 1.两数之和

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210210028986.png" alt="image-20220210210028986" style="zoom:80%;" />

On   On：

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> map1;
        for(int i = 0;i<nums.size();i++){
            if(map1.count(target - nums[i]))
                return {i,map1[target-nums[i]]};
            map1[nums[i]] = i;
        }
        return {-1,-1};
    }
};
```

### 15.三数之和

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

## 2.9-------------------30

### 18.四数之和

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210210202009.png" alt="image-20220210210202009" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> res;
        if(nums.size()<4) return res;
        sort(nums.begin(),nums.end());
        for(int a=0;a<nums.size();a++){
            if(a>0&&nums[a]==nums[a-1])
                continue;
            for(int b=a+1;b<nums.size();b++){
                if(b>a+1&&nums[b]==nums[b-1])
                    continue;
                int d = nums.size() - 1;
                int target1 = target - nums[a] - nums[b];
                for(int c = b+1;c<nums.size();c++){
                    if(c>b+1&&nums[c]==nums[c-1])
                        continue;
                    while(c<d && nums[d] + nums[c] > target1)
                        d--;
                    if(d==c) break;
                    if(nums[d]+nums[c]==target1)
                        res.push_back({nums[a],nums[b],nums[c],nums[d]});
                }
            }
        }
        return res;
    }
};
```

### 16.最接近的三数之和

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210210244722.png" alt="image-20220210210244722" style="zoom:80%;" />

解法一：

```c++
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        int d = INT_MAX;
        int res = 0;
        sort(nums.begin(),nums.end());
        for(int i=0;i<nums.size();i++){
            for(int sum,j=i+1,k=nums.size()-1;j<k;sum>target?k--:j++){
                sum = nums[i]+nums[j]+nums[k];
                if(sum == target)
                    return target;
                if(abs(sum - target)<d){
                    d=abs(sum - target);
                    res = sum;
                }
            }
        }
        return res;
    }
};
```

### 454.四数相加 Ⅱ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210210321397.png" alt="image-20220210210321397" style="zoom:80%;" />

```c++
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        unordered_map<int,int> map;
        for(auto c:nums3){
            for(auto d:nums4)
                map[c+d]++;
        }
        int res=0;
        for(auto a:nums1){
            for(auto b:nums2)
                if(map.count(-a-b))
                    res+=map[-a-b];
        }
        return res;
    }

};
```

解法：暴力

```c++
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        int count=0;
        for(auto a:nums1){
            for(auto b:nums2){
                for(auto c:nums3){
                    for(auto d:nums4){
                        if(a+b+c+d==0)count++;
                    }
                }
            }
        }
        return count;
    }
};
```

### 49.字母异位词分组

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210210356815.png" alt="image-20220210210356815" style="zoom:80%;" />

时间复杂度：O(n^2)，其中 n是数组 points 的长度。

空间复杂度：O(n)*O*。

为什么把条件判断语句放到循环里边会出错？

```c++
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> res;
        unordered_map<string,vector<string>> m1;
        for(auto s:strs){
            string tmp = s;
            sort(s.begin(),s.end());
            m1[s].push_back(tmp);
        }
        for(auto x:m1){
            res.push_back(x.second);
        }
        return res;
    }
};
```

### 447.回旋镖的数量

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210210457248.png" alt="image-20220210210457248" style="zoom:80%;" />

```c++
class Solution {
public:
    int numberOfBoomerangs(vector<vector<int>>& points) {
        int res = 0;
        for(int i=0;i<points.size();i++){
            unordered_map<int,int> map1;
            for(int j=0;j<points.size();j++){
                map1[(points[i][0]-points[j][0])*(points[i][0]-points[j][0])+(points[i][1]-points[j][1])*(points[i][1]-points[j][1])]++;
            }
            for(auto x:map1){
                res += (x.second)*(x.second-1);
            }
        }
        return res;
    }
};
```

## 2.10------------------35

### 149.直线上最多的点数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210210544541.png" alt="image-20220210210544541" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210210556461.png" alt="image-20220210210556461" style="zoom:80%;" />

```c++
class Solution {
public:
    int maxPoints(vector<vector<int>>& points) {
        if (points.size() <= 2)
            return points.size();
        map<vector<double>, int> map;//k,b - 组合数
        for (int i = 0; i < points.size(); i++){
            for (int j = 0; j!=i && j < points.size(); j++){
                if(points[i][0] == points[j][0])
                    map[vector<double>{double(INT_MAX),double(points[i][0])}]++;
                else
                    map[vector<double>{((double)points[i][1] - (double)points[j][1])/((double)points[i][0] - (double)points[j][0]),((double)points[i][0]*(double)points[j][1]-(double)points[i][1]*(double)points[j][0])/((double)points[i][0]-(double)points[j][0])}]++;
            }
        }
        int res = 0;
        for (auto it = map.begin(); it != map.end(); it++)
            res = max(res, it->second);
        return (1+sqrt(1+8*res))/2;
    }
};
```

### 219.存在重复元素 Ⅱ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210210644397.png" alt="image-20220210210644397" style="zoom:80%;" />

```c++
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        unordered_map<int,int> map;
        for(int i=0;i<nums.size();i++){
            if(map.count(nums[i])&&i-map[nums[i]]<=k)
                return true;
            map[nums[i]]=i;
        }
        return false;
    }
};
```

set

```c++
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        unordered_set<int> record;
        for(int i=0;i<nums.size();i++){
            if(record.find(nums[i])!=record.end())
                return true;
            record.insert(nums[i]);
            if(record.size()==k+1)
                record.erase(nums[i-k]);
        }
        return false;
    }
};
```

### 217.存在重复元素

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210210736348.png" alt="image-20220210210736348" style="zoom:80%;" />```

```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> s1;
        for(auto x:nums)
            s1.insert(x);
        return s1.size()<nums.size();
    }
};
```

```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        for(int i=1;i<nums.size();i++){
            if(nums[i]==nums[i-1])
                return true;
        }
        return false;
    }
};
```

```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> s1;
        for(auto x:nums)
            s1.insert(x);
        return s1.size()<nums.size();
    }
};
```

### 220.存在重复元素 Ⅲ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210210817039.png" alt="image-20220210210817039" style="zoom:80%;" />

问题：1.upper_bound为什么不行，2.桶排序

解法一

```
class Solution {
public:
    bool containsNearbyAlmostDuplicate(vector<int>& nums, int k, int t) {
        set<long long> set;
        for(int i=0;i<nums.size();i++){
            if(set.lower_bound((long long)nums[i]-(long long)t)!=set.end()&&*set.lower_bound((long long)nums[i]-(long long)t)<=(long long)nums[i]+(long long)t)
                return true;

            set.insert(nums[i]);
            if(set.size()==k+1)
                set.erase(nums[i-k]);
        }
        return false;
    }
};
```

### 206.反转链表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210210924642.png" alt="image-20220210210924642" style="zoom:80%;" />

方法一：迭代

```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* pre=nullptr;
        ListNode* cur=head;
        while(cur){
            ListNode* next=cur->next;
            cur->next=pre;
            pre=cur;
            cur=next;
        }
        return pre;
    }
};
```

方法二：递归

```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(!head || !head->next) return head;
        ListNode* newhead = reverseList(head->next);
        head->next->next = head;
        head->next = nullptr;
        return newhead;
    }
};
```

## 2.11------------------40

### 92.反转链表 Ⅱ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214224735863.png" alt="image-20220214224735863" style="zoom:80%;" />

解法一：遍历两边

```c++
class Solution {
    void reverselist(ListNode* node){
        ListNode* pre = nullptr;
        ListNode* cur = node;
        while(cur){
            ListNode* next = cur->next;
            cur->next = pre;
            pre = cur;
            cur = next;
        }
    }
public:
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        //切断链表，单独反转，再接回去
        ListNode* dummy = new ListNode(0,head);

        ListNode* pre = dummy;
        for(int i=0;i<left-1;i++)
            pre = pre->next;
        ListNode* pree = pre;//记录要连回去的左点
        ListNode* leftnode = pre->next;//子链表左节点

        for(int i=0;i<right-left+1;i++)
            pre = pre->next;
        ListNode* rightnode = pre;//子链表右节点
        ListNode* curr = rightnode->next;//记录要连回去的右点

        pree->next = nullptr;//切断
        rightnode->next = nullptr;//切断

        reverselist(leftnode);//反转

        pree->next = rightnode;//重连
        leftnode->next = curr;//重连
        return dummy->next;

    }
};
```

解法二：遍历一遍

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220510181045159.png" alt="image-20220510181045159" style="zoom: 25%;" />

```c++
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        ListNode* dummyNode=new ListNode(-1);
        dummyNode->next=head;

        ListNode* pre=dummyNode;
        for(int i=0;i<left-1;i++)
            pre=pre->next;
        
        ListNode* cur=pre->next;

        for(int i=0;i<right-left;i++){
            ListNode* next=cur->next;
            cur->next=next->next;
            next->next=pre->next;

            pre->next=next;

        }
        return dummyNode->next; 

    }
};
```

### 83.删除有序链表中的重复元素

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214224654757.png" alt="image-20220214224654757" style="zoom:80%;" />

解法一：

时间复杂度：O(n)，其中 n是链表的长度。

空间复杂度：O(1)

```c++
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        if(!head || !head->next) return head;
        ListNode* p = head;
        while(p && p->next){
            if(p->val == p->next->val){
                ListNode* delnode = p->next;
                p->next = p->next->next;
                delete delnode;
            }
            else	
                p=p->next;
        }
        return head;
    }
};
```

### 86.分隔链表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214224450889.png" alt="image-20220214224450889" style="zoom:80%;" />

```c++
class Solution {
public:
    ListNode* partition(ListNode* head, int x) {
        ListNode* small = new ListNode(0);
        ListNode* smallhead = small;
        ListNode* large = new ListNode(0);
        ListNode* largehead = large;
        while(head){
            if(head->val<x){
                small->next = head;
                small = small->next;
            }
            else{
                large->next = head;
                large = large->next;
            }
            head = head->next;
        }

        small->next = largehead->next;
        large->next = nullptr;
        return smallhead->next;
    }
};
```

### 328.奇偶链表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214224400018.png" alt="image-20220214224400018" style="zoom:80%;" />

```c++
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
        if(!head)return head;
        ListNode* evenHead=head->next;
        ListNode* odd = head;
        ListNode* even=evenHead;

        while(even&&even->next){
            odd->next=even->next;
            odd=odd->next;
            even->next=odd->next;
            even=even->next;

        }
        odd->next=evenHead;
        return head;
    }
};
```

### 2.两数相加

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214224305845.png" alt="image-20220214224305845" style="zoom:80%;" />

```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* head = nullptr;
        ListNode* tail = nullptr;
        int cnt = 0;
        while(l1||l2){
            int n1 = l1?l1->val:0;
            int n2 = l2?l2->val:0;
            int sum = n1 + n2 + cnt;
            cnt = sum/10;
            if(!head){
                head = tail = new ListNode(sum%10);
            }else{
                tail->next = new ListNode(sum%10);
                tail = tail->next;
            }
            if(l1) l1=l1->next;
            if(l2) l2=l2->next;
        }
        if(cnt!=0)
            tail->next = new ListNode(cnt);
        return head;
    }
};
```

## 2.12------------------45

### 445.两数相加Ⅱ

```c++
class Solution {
private:
    ListNode* reverseList(ListNode* head){
        ListNode* pre=nullptr;
        ListNode* cur=head;
        while(cur){
            ListNode* next=cur->next;
            cur->next=pre;
            pre=cur;
            cur=next;    
        }
        return pre;
    }
    ListNode* addTwoNumbers1(ListNode* l1, ListNode* l2) {
        ListNode* head=nullptr;
        ListNode* tail=nullptr;
        int carry=0;
        while(l1||l2){
            int n1=l1?l1->val:0;
            int n2=l2?l2->val:0;
            int sum=n1+n2+carry;
            carry=sum/10;
            if(!head)
                head=tail=new ListNode(sum%10);
            else{
                tail->next=new ListNode(sum%10);
                tail=tail->next;
            }
            if(l1)
                l1=l1->next;
            if(l2)
                l2=l2->next;
            if(carry>0)
                tail->next=new ListNode(carry);
        }
        return head;
    }
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* l11=reverseList(l1);
        ListNode* l22=reverseList(l2);
        return reverseList(addTwoNumbers1(l11,l22));
    }
};
```

解法二：

利用栈

```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        stack<int> s1,s2;
        while(l1){
            s1.push(l1->val);
            l1=l1->next;
        }
        while(l2){
            s2.push(l2->val);
            l2=l2->next;
        }
        ListNode* head = nullptr;//指针若不指向对象，一定将其指向空
        int carry=0;
        while(!s1.empty()||!s2.empty()||carry!=0){
            int n1=s1.empty()?0:s1.top();
            int n2=s2.empty()?0:s2.top();
            if(!s1.empty())s1.pop();//若栈为空，pop会导致程序出错
            if(!s2.empty())s2.pop();
            int sum=carry+n1+n2;
            carry=sum/10;
            sum%=10;
            ListNode* cur=new ListNode(sum);
            cur->next=head;
            head=cur;
        }
        return head;
    }
};
```

### 203.移除链表元素

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214224128574.png" alt="image-20220214224128574" style="zoom:80%;" />

解法一，迭代：

```c++
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* dummynode = new ListNode(-1,head);
        ListNode*p = dummynode;

        while(p->next){
            if(p->next->val == val){
                ListNode* del = p->next;
                p->next = p->next->next;
                delete del;
            }
            else{
                p = p->next;
            }
        }
        ListNode* newhead = dummynode->next;
        delete dummynode;
        return newhead;

    }
};
```

解法二，递归

```c++
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        if(!head) return head;
        head->next = removeElements(head->next,val);
        if(head->val!=val) return head;

        ListNode* delnode = head;
        ListNode* newhead = head->next;
        delete delnode;
        return newhead;
    }
};
```

### 82.删除排序链表中的重复元素 II

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214224030661.png" alt="image-20220214224030661" style="zoom:80%;" />

```c++
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* dummt = new ListNode(0,head);
        ListNode* p = dummt;
        while(p->next && p->next->next){
            if(p->next->val == p->next->next->val){
                int x = p->next->val;
                while(p->next && p->next->val==x)//直到next为空，或者不再等于x的时候，跳出循环
                    p->next = p->next->next;
            }
            else
                p=p->next;
        }
        return dummt->next;
    }
};
```

### 21.合并两个有序链表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214223744783.png" alt="image-20220214223744783" style="zoom:80%;" />

迭代：

```c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode* dummy = new ListNode(0);
        ListNode* p = dummy;
        while(list1 && list2){
            if(list1->val<list2->val){
                p->next = list1;
                list1=list1->next;
            }
            else{
                p->next = list2;
                list2=list2->next;
            }
            p=p->next;
        }
        p->next = list2?list2:list1;
        return dummy->next;
    }
};
```

递归:

```c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(!l1) return l2;
        if(!l2) return l1;

        if(l1->val<l2->val) {
            l1->next = mergeTwoLists(l1->next,l2);
            return l1;
        }
        else{
            l2->next = mergeTwoLists(l1,l2->next);
            return l2;
        }
    }
};
```

### 24.两两交换链表中的节点

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214223657493.png" alt="image-20220214223657493" style="zoom:80%;" />

迭代

```c++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* dummyNode=new ListNode(0,head);
        ListNode* p=dummyNode;
        while(p->next!=NULL&&p->next->next!=NULL){
            ListNode* node1=p->next;
            ListNode* node2=node1->next;
            ListNode* next=node2->next;

            node2->next=node1;
            node1->next=next;
            p->next=node2;

            p=node1;
        }
        ListNode* res=dummyNode->next;
        delete dummyNode;
        return res;
    }
};
```

递归：

```c++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if(!head||!head->next) return head;
        ListNode* newhead = head->next;
        head->next = swapPairs(newhead->next);
        newhead->next = head;
        return newhead;
    }
};
```

## 2.13-----------------50

### 25.K 个一组翻转链表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214223603796.png" alt="image-20220214223603796" style="zoom:80%;" />

```c++
class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode* p = head;
        int count = 0;
        while(p){
            p = p->next;
            count++;
        }
        int n = count / k;
        ListNode* dummy = new ListNode(-1,head);
        p = dummy;
        for(int i=0;i<n;i++){
            ListNode* cur = p->next;
            for(int i=0;i<k-1;i++){
                ListNode* next = cur->next;
                cur->next = next->next;
                next->next = p->next;
                p->next = next;
            }
            p = cur;
        }
        return dummy->next;
    }
};
```

### 147.对链表进行插入排序

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214223305615.png" alt="image-20220214223305615" style="zoom:80%;" />

```c++
class Solution {
public:
    ListNode* insertionSortList(ListNode* head) {
        if(!head || !head->next) return head;
        ListNode* dummynode = new ListNode(0,head);
        ListNode* lastsorted = head;
        ListNode* cur = head->next;
        while(cur!=nullptr){
            if(cur->val < lastsorted->val){
                ListNode* p = dummynode;
                while(p->next && p->next->val<=cur->val)
                    p = p->next;
                
                lastsorted->next = cur->next;
                cur->next = p->next;
                p->next = cur;
            }
            else
                lastsorted=lastsorted->next;
            cur = lastsorted->next;
        }
        return dummynode->next;
    }
};
```

### 148.排序链表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214223215980.png" alt="image-20220214223215980" style="zoom:80%;" />

```c++
class Solution {
    ListNode* merge(ListNode* a,ListNode* b){
        ListNode* dummy = new ListNode(0);
        ListNode* dumnode = dummy;
        while(a&&b){
            if(a->val<b->val){
                dummy->next = a;
                a=a->next;
            }
            else{
                dummy->next = b;
                b=b->next;
            }
            dummy=dummy->next;
        }
        dummy->next=a?a:b;

        return dumnode->next;
    }
    ListNode* merge_sort(ListNode* head,ListNode* tail){
        if(head == tail){
            tail->next = nullptr;
            return tail;
        }
        ListNode* a = head;
        ListNode* b = head;
        while(b->next && b->next->next){
            a=a->next;
            b=b->next->next;
        }
        ListNode* right = merge_sort(a->next,tail);
        a->next = nullptr;
        ListNode* left = merge_sort(head,a);
        return merge(left,right); 
    }
public:
    ListNode* sortList(ListNode* head) {
        if(!head||!head->next) return head;
        ListNode* tail = head;
        while(tail->next){
            tail = tail->next;
        }
        return merge_sort(head,tail);
    }
};
```

### 237.删除链表中的节点

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214222934955.png" alt="image-20220214222934955" style="zoom:80%;" />

```c++
class Solution {
public:
    void deleteNode(ListNode* node) {
        if(!node)return;
        if(!node->next){
            delete node;
            node=NULL;
            return;
        }
        node->val=node->next->val;
        ListNode* delNode=node->next;
        node->next=delNode->next;
        delete delNode;

        return;
    }
};
```

### 19.删除链表的倒数第 N 个结点

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214222839447.png" alt="image-20220214222839447" style="zoom:80%;" />

只遍历一遍

```c++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dhead = new ListNode(0,head);
        ListNode* s = dhead;
        ListNode* f = dhead;
        for(int i=0;i<n+1;i++)
            f=f->next;
        while(f){
            s=s->next;
            f=f->next;
        }
        ListNode* del = s->next;
        s->next = s->next->next;
        delete del;
        return dhead->next;
    }
};
```

遍历两遍

```c++
class Solution {
public:
    int getListLength(ListNode* head){
        int l=0;
        while(head){
            l++;
            head=head->next;
        }
        return l;
    }
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        
        ListNode* dummyNode=new ListNode(0,head);
        ListNode* p=dummyNode;
        int l=getListLength(head);
        for(int i=0;i<l-n;i++)
            p=p->next;
        
        p->next=p->next->next;
        ListNode* result=dummyNode->next;
        delete dummyNode;
        return result;
        
    }
};
```

利用栈

```c++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummyNode=new ListNode(0,head);
        ListNode* p=dummyNode;
        stack<ListNode*> s;
        while(p){
            s.push(p);
            p=p->next;
        }
        for(int i=0;i<n;i++){
            s.pop();
        }
        ListNode* pre=s.top();
        pre->next=pre->next->next;
        ListNode* result=dummyNode->next;
        delete dummyNode;
        return result;
        
    }
};
```

## 2.14--------------56

### 61.旋转链表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214222738565.png" alt="image-20220214222738565" style="zoom:80%;" />

时间复杂度：O(n)

空间复杂度：O(1)

```c++
class Solution {
public:
    ListNode* rotateRight(ListNode* head, int k) {
        if(!head||!head->next||k==0) return head;
        ListNode* p = head;
        int n = 0;
        while(p->next){
            p=p->next;
            n++;
        }
        k=k%(n+1);
        if(k==0) return head;
        ListNode* tail = p;
        p=head;
        for(int i=0;i<(n+1-k)-1;i++){
            p=p->next;
        }
        ListNode* newhead = p->next;
        p->next = nullptr;
        tail->next = head;
        return newhead;
    }
};
```

### 143.重排链表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214222436291.png" alt="image-20220214222436291" style="zoom:80%;" />

```c++
class Solution {
    ListNode* reverse(ListNode* head){
        if(!head||!head->next) return head;
        ListNode* newhead = reverse(head->next);
        head->next->next = head;
        head->next = nullptr;
        return newhead;
    }
public:
    ListNode* mid(ListNode* head){
        ListNode* dhead = new ListNode(0,head);
        ListNode* s = dhead;
        ListNode* f = dhead;
        while(f->next&&f->next->next){
            s=s->next;
            f=f->next->next;
        }
        return s;
    }
    ListNode* merge(ListNode* l1,ListNode* l2){
        ListNode* res = new ListNode(0);
        ListNode* p = res;
        while(l1&&l2){
            res->next = l1;
            l1=l1->next;
            res = res->next;
            res->next = l2;
            l2=l2->next;
            res = res->next;
        }
        return p->next;
    }
    void reorderList(ListNode* head) {
        if(!head||!head->next) return;
        ListNode* midnode = mid(head);
        ListNode* node2 = reverse(midnode->next);
        midnode->next = nullptr;
        ListNode* res = merge(head,node2);
    }
};
```

### 234.判断是否为回文链表

解法二：递归

```c++
class Solution {
    ListNode* frontPointer;
public:
    bool recursivelyCheck(ListNode* currentNode) {
        if (currentNode != nullptr) {
            if (!recursivelyCheck(currentNode->next)) {
                return false;
            }
            if (currentNode->val != frontPointer->val) {
                return false;
            }
            frontPointer = frontPointer->next;
        }
        return true;
    }

    bool isPalindrome(ListNode* head) {
        frontPointer = head;
        return recursivelyCheck(head);
    }
};
```

解法三：快慢指针 O(n)  O(1)

```c++
class Solution {
    ListNode* reverse(ListNode* head){
        ListNode* pre = nullptr;
        ListNode* cur = head;
        while(cur){
            ListNode* next = cur->next;

            cur->next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }
    ListNode* mid(ListNode* head){
        ListNode* s=head;
        ListNode* f=head;
        while(f->next&&f->next->next){
            s=s->next;
            f=f->next->next;
        }
        return s;
    }
public:
    bool isPalindrome(ListNode* head) {
        ListNode* midnode = mid(head);
        ListNode* node2 = reverse(midnode->next);
        midnode->next = nullptr;
        ListNode* a = head;
        ListNode* b = node2;
        while(a && b){
            if(a->val!=b->val)
                return false;
            a=a->next;
            b=b->next;
        }
        ListNode* node3 = reverse(node2);
        midnode->next = node3;
        return true;
    }
};
```

### 20.有效的括号

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220215092047228.png" alt="image-20220215092047228" style="zoom:80%;" />

时间复杂度：O(n)

空间复杂度：O(∣Σ∣)

```c++
class Solution {
    bool f(char x){
        if(x=='['||x=='{'||x=='(')
            return true;
        return false;
    }
public:
    bool isValid(string s) {
        stack<char> s1;
        for(auto x:s){
            if(f(x)) s1.push(x);
            else{
                if(s1.empty()) return false;
                int ch = s1.top();
                if(!s1.empty())s1.pop();

                char match;
                if(x == '}') match = '{';
                else if(x == ']') match = '[';
                else if(x == ')') match = '(';
                else return false;

                if(match!=ch) return false;
            }
        }
        if(!s1.empty()) return false;
        return true;
    }
};
```

### 150.逆波兰表达式求值

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220215162115528.png" alt="image-20220215162115528" style="zoom:80%;" />

时间复杂度：O(n)

空间复杂度：O(n)

```c++
class Solution {
    bool f(string s){
        if(s=="/"||s=="-"||s=="+"||s=="*")
            return true;
        return false;
    }
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> stk;
        int sum = 0;
        for(auto x:tokens){
            if(f(x)){
                int a = stk.top();
                stk.pop();
                int b = stk.top();
                stk.pop();
                if(x=="/") sum = b/a;
                else if(x=="-") sum=b-a;
                else if(x=="+") sum=b+a;
                else sum = b*a;
                stk.push(sum);
            }
            else{
                stk.push(stoi(x));
            }
        }
        return stk.top();
    }
};
```

### 71.简化路径

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220215210922240.png" alt="image-20220215210922240" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220215210935949.png" alt="image-20220215210935949" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220511152406374.png" alt="image-20220511152406374" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<string> split(string s,char c){
        vector<string> res;
        string t;
        for(auto x:s){
            if(x==c){
                res.push_back(t);
                t.clear();
            }
            else
                t+=x;
        }
        res.push_back(t);
        return res;
    }
    string simplifyPath(string path) {
        vector<string> names = split(path,'/');
        vector<string> stack;
        for(auto x:names){
            if(x==""||x==".")
                continue;
            else if(x==".."){
                if(stack.empty()) continue;
                else stack.pop_back();
            }
            else    
                stack.push_back(x);
        }
        string res;
        if(stack.size()==0) return "/";
        for(auto x:stack)
            res+="/"+x;
        return res;
    }
};
```

## 2.15---------------63

### 144.二叉树的前序遍历

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220216185126517.png" alt="image-20220216185126517" style="zoom:80%;" />

解法一：

```c++
class Solution {
public:
    void preorder(TreeNode* root,vector<int>& vec){
        if(!root)return;
        vec.push_back(root->val);
        preorder(root->left,vec);
        preorder(root->right,vec);
    }
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> vec;
        preorder(root,vec);
        return vec;
    }
};
```

解法三：迭代

```c++
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> res;
        if(!root) return res;
        stack<TreeNode*> stk;
        TreeNode* node= root;
        while(!stk.empty() || node){
            while(node){
                res.push_back(node->val);
                stk.push(node);
                node=node->left;
            }
            node = stk.top();
            stk.pop();
            node = node->right;
        }
        return res;
    }
};
```

```c++
class Solution {
    struct Com{
        TreeNode* node;
        int c = 0;//0表示访问，1表示打印
        Com(int c0,TreeNode* Node):c(c0),node(Node){}
    };
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> res;
        if(!root) return res;
        stack<Com> stk;
        stk.push(Com(0,root));
        while(!stk.empty()){
            Com com = stk.top();
            stk.pop();
            if(com.c == 1) 
                res.push_back(com.node->val);
            else{
                if(com.node->right)stk.emplace(0,com.node->right);
                if(com.node->left) stk.emplace(0,com.node->left); 
                stk.push(Com(1,com.node));  
            }
        }
        return res;
    }
};
```

解法四：Morris 遍历

### 94.二叉树的中序遍历

```c++
class Solution {
public:
    void inorder(TreeNode* node,vector<int>& vec){
        if(!node)return;
        inorder(node->left,vec);
        vec.push_back(node->val);
        inorder(node->right,vec);
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> vec;
        inorder(root,vec);
        return vec;
    }
};
```

```c++
class Solution {
    struct Com{
        TreeNode* node;
        int c = 0;//0表示访问，1表示打印
        Com(int c0,TreeNode* Node):c(c0),node(Node){}
    };
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        if(!root) return res;
        stack<Com> stk;
        stk.push(Com(0,root));
        while(!stk.empty()){
            Com com = stk.top();
            stk.pop();
            if(com.c == 1) 
                res.push_back(com.node->val);
            else{
                if(com.node->right)stk.emplace(0,com.node->right);
                stk.push(Com(1,com.node));
                if(com.node->left) stk.emplace(0,com.node->left);    
            }
        }
        return res;
    }
};
```

### 145.二叉树的后序遍历

```c++
class Solution {
public:
    void postorder(TreeNode* node,vector<int>& vec){
        if(!node) return;
        postorder(node->left,vec);
        postorder(node->right,vec);
        vec.push_back(node->val);
    }
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> vec;
        postorder(root,vec);
        return vec;
    }
};
```

```c++
class Solution {
    struct Com{
        TreeNode* node;
        int c = 0;//0表示访问，1表示打印
        Com(int c0,TreeNode* Node):c(c0),node(Node){}
    };
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;
        if(!root) return res;
        stack<Com> stk;
        stk.push(Com(0,root));
        while(!stk.empty()){
            Com com = stk.top();
            stk.pop();
            if(com.c == 1) 
                res.push_back(com.node->val);
            else{
                stk.push(Com(1,com.node));
                if(com.node->right)stk.emplace(0,com.node->right);
                if(com.node->left) stk.emplace(0,com.node->left);    
            }
        }
        return res;
    }
};
```

### 341.扁平化嵌套列表迭代器（）

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220511185151923.png" alt="image-20220511185151923" style="zoom:80%;" />

```c++
class NestedIterator {
    vector<int> res;
    vector<int>::iterator it;
    void dfs(vector<NestedInteger> &nestedList){
        for(auto x:nestedList){
            if(x.isInteger())
                res.push_back(x.getInteger());
            else
                dfs(x.getList());
        }
    }
public:
    NestedIterator(vector<NestedInteger> &nestedList) {
        dfs(nestedList);
        it = res.begin();
    }
    
    int next() {
        return *(it++);
    }
    
    bool hasNext() {
        return it!=res.end();
    }
};
```

### 102.二叉树的层序遍历

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220217164356690.png" alt="image-20220217164356690" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if(!root) return res;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()){
            int sz = q.size();
            vector<int> cur;
            for(int i=0;i<sz;i++){
                TreeNode* node = q.front();
                q.pop();
                cur.push_back(node->val);
                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);
            }
            res.push_back(cur);
        }
        return res;
    }
};
```

### 107.二叉树的层序遍历 Ⅱ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220217185328532.png" alt="image-20220217185328532" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int>> vec;
        if(!root) return vec;
        queue<pair<TreeNode*,int>> q;
        q.push(make_pair(root,0));
        while(!q.empty()){
            TreeNode* node=q.front().first;
            int level=q.front().second;
            q.pop();
            if(level==vec.size())
                vec.push_back(vector<int>());
            vec[level].push_back(node->val);
            if(node->left)
                q.push(make_pair(node->left,level+1));
            if(node->right)
                q.push(make_pair(node->right,level+1));
        }
        reverse(vec.begin(),vec.end());
        return vec;
    }
};
```

### 103.二叉树的锯齿形层序遍历

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220217185458121.png" alt="image-20220217185458121" style="zoom: 80%;" />

```c++
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if(!root) return res;
        deque<TreeNode*> q;
        q.push_front(root);
        int cnt = 0;
        while(!q.empty()){
            int n = q.size();
            vector<int> cur;
            if(cnt%2==0){
                for(int i=0;i<n;i++){
                    TreeNode* node = q.front();
                    q.pop_front();
                    cur.push_back(node->val);
                    if(node->left) q.push_back(node->left);
                    if(node->right) q.push_back(node->right);
                }
            }
            else{
                for(int i=0;i<n;i++){
                    TreeNode* node = q.back();
                    q.pop_back();
                    cur.push_back(node->val);
                    if(node->right) q.push_front(node->right);
                    if(node->left) q.push_front(node->left);
                }
            }
            cnt++;
            res.push_back(cur);
        }
        return res;
    }
};
```

## 2.16-----------------68

### 199.二叉树的右视图

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220511200112299.png" alt="image-20220511200112299" style="zoom:80%;" />

DFS递归

```c++
class Solution {
public:
    vector<int> ans;
    int depth=0;
    void dfs(TreeNode* root){
        if(!root)
            return;
        ++depth;
        if(ans.size()<depth)
            ans.emplace_back(root->val);
        dfs(root->right);
        dfs(root->left);
        --depth;
    }
    vector<int> rightSideView(TreeNode* root) {
        dfs(root);
        return ans;
    }
};
```

第二种递归

```c++
class Solution {
    vector<int> res;
    void dfs(TreeNode* node,int depth){
        if(!node) return;
        if(res.size()==depth)
            res.push_back(node->val);
        depth++;
        dfs(node->right,depth);
        dfs(node->left,depth);
    }
public:
    vector<int> rightSideView(TreeNode* root) {
        dfs(root,0);
        return res;
    }
};
```

迭代：层序遍历，依次加入每一层的最后一个元素

```c++
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        vector<int> res;
        if(!root) return res;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()){
            int size = q.size();
            vector<int> cur;
            for(int i=0;i<size;i++){
                TreeNode* node = q.front();
                q.pop();
                cur.push_back(node->val);
                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);
            }
            res.push_back(cur.back());
        }
        return res;
    }
};
```

### 279.完全平方数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218090951739.png" alt="image-20220218090951739" style="zoom:80%;" />

解法一：BFS

```c++
class Solution {
public:
    int numSquares(int n) {
        queue<pair<int,int>> q;
        q.push(make_pair(n,0));

        vector<bool> visited(n+1,false);
        visited[n]=true;
        while(!q.empty()){
            int num=q.front().first;
            int distance=q.front().second;
            q.pop();
            for(int i=1;;i++){
                int a=num-i*i;
                if(a<0)break;
                if(a==0)return distance+1;
                if(!visited[a]){
                    q.push(make_pair(num-i*i,distance+1));
                    visited[a]=true;
                }
            }
        }
        throw invalid_argument("error");
    }
};
```

解法二：动态规划

```c++
class Solution {
public:
    int numSquares(int n) {
        vector<int> f(n + 1);
        for (int i = 1; i <= n; i++) {
            int minn = INT_MAX;
            for (int j = 1; j * j <= i; j++) {
                minn = min(minn, f[i - j * j]);
            }
            f[i] = minn + 1;
        }
        return f[n];
    }
};
```

解法三：四平方和定理

```c++
class Solution {
public:
    // 判断是否为完全平方数
    bool isPerfectSquare(int x) {
        int y = sqrt(x);
        return y * y == x;
    }

    // 判断是否能表示为 4^k*(8m+7)
    bool checkAnswer4(int x) {
        while (x % 4 == 0) {
            x /= 4;
        }
        return x % 8 == 7;
    }

    int numSquares(int n) {
        if (isPerfectSquare(n)) {
            return 1;
        }
        if (checkAnswer4(n)) {
            return 4;
        }
        for (int i = 1; i * i <= n; i++) {
            int j = n - i * i;
            if (isPerfectSquare(j)) {
                return 2;
            }
        }
        return 3;
    }
};
```

### 127.单词接龙

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218101552780.png" alt="image-20220218101552780" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218101602996.png" alt="image-20220218101602996" style="zoom:80%;" />

### 126.单词接龙Ⅱ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218101635956.png" alt="image-20220218101635956" style="zoom:80%;" />

```c++
class Solution {
    vector<vector<string>> res;
public:
    vector<vector<string>> findLadders(string beginWord, string endWord, vector<string>& wordList) {
        if(wordList.size()<=0) return res;
        unordered_map<string,int> map1;
        wordList.push_back(beginWord);
        for(int i=0;i<wordList.size();i++){
            map1[wordList[i]] = i;
        }

        for(auto x:map1){
            cout<<x.first<<' '<<x.second<<endl;
        }

        int begin_index = map1[beginWord];
        int end_index = map1[endWord];

        vector<vector<int>> g(wordList.size());

        for(int k=0;k<wordList.size();k++){
            for(int i=0;i<wordList[k].size();i++){
                string word = wordList[k];
                for(int j=97;j<=122;j++){
                    if(j!=int(word[i])){
                        word[i] = char(j);
                        if(map1.count(word) && word!=wordList[k]){
                            g[map1[wordList[k]]].push_back(map1[word]);
                        }
                    }
                }
            }
        }















        return res;
    }
};
```

### 347. 前 K 个高频元素

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218101838761.png" alt="image-20220218101838761" style="zoom:80%;" />

时间复杂度：O(Nlogk)
空间复杂度：O(N)

```c++
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        vector<int> res;
        unordered_map<int,int> map1;
        for(auto x:nums)
            map1[x]++;
        priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>> pq;

        for(auto it = map1.begin();it!=map1.end();it++){
            if(pq.size()==k){
                if(it->second > pq.top().first){
                    pq.pop();
                    pq.emplace(it->second,it->first);
                }
            }
            else
                pq.emplace(it->second,it->first);
        }
        while(!pq.empty()){
            res.push_back(pq.top().second);
            pq.pop();
        }
        return res;
    }
};
```

超时做法

```c++
bool cmp(pair<int,int> a,pair<int,int> b){
    return a.second>b.second;
}
int contain(int x,vector<pair<int,int>> vec){
    for(int i=0;i<vec.size();i++){
        if(vec[i].first==x)
            return i;
    }
    return -1;
}
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        vector<int> res;
        vector<pair<int,int>> map;
        for(auto x:nums){
            if(contain(x,map)==-1)
                map.emplace_back(x,1);
            else
                map[contain(x,map)].second++;
        }
        sort(map.begin(),map.end(),cmp);
        for(int i=0;i<k;i++){
            res.push_back(map[i].first);
        }
        return res;
    }
};
```

## 2.17-----------------73

### 23.合并K个升序链表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218101947398.png" alt="image-20220218101947398" style="zoom:80%;" />

解法一：优先队列

```c++
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<int,vector<int>,greater<int>> pq;
        for(int i=0;i<lists.size();i++){
            while(lists[i]){
                pq.push(lists[i]->val);
                lists[i]=lists[i]->next;
            }
        }
        vector<int> vec;
        while(!pq.empty()){
            vec.push_back(pq.top());
            pq.pop();
        }
        if(vec.size()==0)return nullptr;
        ListNode* head=new ListNode(vec[0],nullptr);
        ListNode* p= head;
        for(int i=1;i<vec.size();i++){
            p->next=new ListNode(vec[i],nullptr);
            p=p->next;
        }
        return head;
    } 
};
```

解法二：顺序合并

```c++
class Solution {
    ListNode* merge(ListNode* a,ListNode* b){
        ListNode* dummy = new ListNode(0);
        ListNode* p =dummy;
        while(a&&b){
            if(a->val<b->val){
                p->next = a;
                a=a->next;
            }
            else{
                p->next = b;
                b=b->next;
            }
            p=p->next;
        }
        p->next=a?a:b;
        return dummy->next;
    }
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if(lists.size()==0) return nullptr;
        while(lists.size()>1){
            ListNode* a = lists[lists.size()-1];
            ListNode* b = lists[lists.size()-2];
            lists.pop_back();
            lists.pop_back();
            ListNode* c = merge(a,b);
            lists.push_back(c);
        }
        return lists[0];
    }
};
```

解法三：分治合并

```c++
class Solution {
    ListNode* merge(ListNode* a,ListNode* b){
        ListNode* dummy = new ListNode(0);
        ListNode* p =dummy;
        while(a&&b){
            if(a->val<b->val){
                p->next = a;
                a=a->next;
            }
            else{
                p->next = b;
                b=b->next;
            }
            p=p->next;
        }
        p->next=a?a:b;
        return dummy->next;
    }
    ListNode* merge_sort(vector<ListNode*>& lists,int l,int r){
        if(l==r)return lists[l];
        if(l>r) return nullptr;
        int mid = (l+r)/2;
        return merge(merge_sort(lists,l,mid),merge_sort(lists,mid+1,r));
    }
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        return merge_sort(lists,0,lists.size()-1);
    }
};
```

### 104.二叉树的最大深度

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218102025838.png" alt="image-20220218102025838" style="zoom:80%;" />

深度优先搜索：递归

```c++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(!root)return 0;
        return max(maxDepth(root->left),maxDepth(root->right))+1;
    }
};
```

广度优先搜索：迭代

```c++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        int res = 0;
        if(!root) return res;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()){
            res++;
            int size = q.size();
            for(int i=0;i<size;i++){
                TreeNode* node = q.front();
                q.pop();
                if(node->left) q.push(node->left);
                if(node->right)q.push(node->right);
            }
        }
        return res;
    }
};
```

### 111.二叉树的最小深度

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218102103730.png" alt="image-20220218102103730" style="zoom:80%;" />

深度优先搜索：

```c++
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(!root) return 0;
        if(!root->left) return minDepth(root->right)+1;
        if(!root->right) return minDepth(root->left)+1;
        return min(minDepth(root->left),minDepth(root->right))+1;
    }
};
```

广度优先搜索：

```c++
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(!root) return 0;
        queue<pair<TreeNode*,int>> q;
        q.emplace(root,1);
        while(!q.empty()){
            int size = q.size();
            for(int i=0;i<q.size();i++){
                TreeNode* node = q.front().first;
                int res = q.front().second;
                q.pop();
                if(!node->left && !node->right)
                    return res;
                if(node->left) q.emplace(node->left,res+1);
                if(node->right)q.emplace(node->right,res+1);
            }
        }
        return -1;
    }
};
```

### 226.翻转二叉树

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218102140684.png" alt="image-20220218102140684" style="zoom:80%;" />

递归：

```c++
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(!root) return root;
        TreeNode* tmp = root->left;
        root->left = invertTree(root->right);
        root->right = invertTree(tmp);
        return root;
    }
};
```

### 100.相同的树

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218102222893.png" alt="image-20220218102222893" style="zoom:80%;" />

深度优先遍历：递归

```c++
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if(!p&&!q) return true;
        if(!p||!q) return false;
        if(q->val!=p->val) return false;
        return isSameTree(p->left,q->left) && isSameTree(p->right,q->right);
    }
};
```

广度优先遍历：迭代

```c++
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if(!p&&!q) return true;
        if(!p||!q) return false;
        queue<TreeNode*> qq;
        qq.push(q);
        queue<TreeNode*> pp;
        pp.push(p);
        while(!qq.empty()&&!pp.empty()){
            int sizeq = qq.size();
            int sizep = pp.size();
            if(sizep!=sizeq) return false;
            for(int i=0;i<sizeq;i++){
                TreeNode* nq = qq.front();
                TreeNode* np = pp.front();
                qq.pop();
                pp.pop();
                if(nq->val!=np->val) return false;
                if(nq->left==nullptr^np->left==nullptr) return false;
                if(nq->right==nullptr^np->right==nullptr) return false;
                if(nq->left)qq.push(nq->left);
                if(nq->right)qq.push(nq->right);
                if(np->left)pp.push(np->left);
                if(np->right)pp.push(np->right);
            }
        }
        return true;
    }
};
```

## 2.18------------------82

### 101.对称二叉树

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218102310111.png" alt="image-20220218102310111" style="zoom:80%;" />

DFS 递归

```c++
class Solution {
    bool check(TreeNode* q,TreeNode* p){
        if(!p&&!q) return true;
        if(!p||!q) return false;
        return q->val==p->val&&check(q->left,p->right)&&check(q->right,p->left);
    }
public:
    bool isSymmetric(TreeNode* root) {
        return check(root,root);
    }
};
```

BFS 迭代

```c++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        queue<TreeNode*> q;
        q.push(root);
        q.push(root);
        while(!q.empty()){
            TreeNode* node1=q.front();
            q.pop();
            TreeNode* node2=q.front();
            q.pop();
            if(node1==nullptr&&node2==nullptr) continue;
            if(node1==nullptr || node2==nullptr) return false;
            if(node1->val!=node2->val) return false;
            q.push(node1->left);
            q.push(node2->right);
            q.push(node1->right);
            q.push(node2->left);
        }
        return true;
    }
};
```

### 222.完全二叉树的节点个数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218102344421.png" alt="image-20220218102344421" style="zoom:80%;" />

解法一：遍历所有节点（适用于任何二叉树）

```c++
class Solution {
public:
    int countNodes(TreeNode* root) {
        if(!root) return 0;
        return countNodes(root->left)+countNodes(root->right)+1;
    }
};
```

解法二：完全二叉树的左停靠性质

```c++
class Solution {
public:
    int countLevels(TreeNode* node){
        int levels = 0;
        while(node){
            levels++;
            node=node->left;
        }
        return levels;
    }
    int countNodes(TreeNode* root) {
        if(!root) return 0;
        int r_level = countLevels(root->right);
        int l_level = countLevels(root->left);
        if(r_level==l_level)
            return countNodes(root->right)+pow(2,l_level)-1+1;
        else
            return countNodes(root->left)+pow(2,r_level)-1+1;
    }
};
```

解法三：二分查找

### 110.平衡二叉树

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218102420770.png" alt="image-20220218102420770" style="zoom:80%;" />

递归：

```c++
class Solution {
public:
    int depth(TreeNode* node){
        if(!node) return 0;
        return max(depth(node->left),depth(node->right))+1;
    }
    bool isBalanced(TreeNode* root) {
        if(!root) return true;
        return abs(depth(root->left)-depth(root->right))<=1&&isBalanced(root->left)&&isBalanced(root->right);
    }
};
```

### 112.路径总和			根到叶子

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218102459821.png" alt="image-20220218102459821" style="zoom:80%;" />

解法一：递归：

时间复杂度：O(N)

空间复杂度：O(H)H为树的高度。

```c++
class Solution {
public:
    bool hasPathSum(TreeNode* root, int targetSum) {
       if(!root) return false;
       if(!root->left&&!root->right) return root->val==targetSum;
       return hasPathSum(root->left,targetSum-root->val)||hasPathSum(root->right,targetSum-root->val);  
    }
};
```

解法二：广度优先搜索：

```c++
class Solution {
public:
    bool hasPathSum(TreeNode* root, int targetSum) {
        if(!root) return false;
        queue<TreeNode*> q;
        queue<int> q2;
        q.push(root);
        q2.push(root->val);
        while(!q.empty()){
            TreeNode* node = q.front();
            q.pop();
            int tmp = q2.front();
            q2.pop();
            if(!node->left&&!node->right){
                if(targetSum==tmp) return true;
                continue;
            }
            if(node->left){
                q.push(node->left);
                q2.push(node->left->val+tmp);
            }
            if(node->right){
                q.push(node->right);
                q2.push(node->right->val+tmp);
            }
        }
        return false;
    }
};
```

### 404.左子叶之和

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218102600907.png" alt="image-20220218102600907" style="zoom:80%;" />

广度优先搜索：

```c++
class Solution {
public:
    bool isleaf(TreeNode* node){
        return node && !node->left && !node->right;
    }
    int sumOfLeftLeaves(TreeNode* root) {
        if(!root) return 0;
        queue<TreeNode*> q;
        int sum = 0;
        q.push(root);
        while(!q.empty()){
            TreeNode* node = q.front();
            q.pop();
            if(node->left){
                if(isleaf(node->left))
                    sum+=node->left->val;
                else
                    q.push(node->left);
            }
            if(node->right)q.push(node->right);
        }
        return sum;
    }
};
```

深度优先搜索：

```c++
class Solution {
public:
    bool isleaf(TreeNode* node){
        return node && !node->left && !node->right;
    }
    int dfs(TreeNode* node){
        int sum = 0;
        if(!node) return sum;
        sum += isleaf(node->left)?node->left->val:dfs(node->left);
        sum += dfs(node->right);
        return sum;
    }
    int sumOfLeftLeaves(TreeNode* root) {
        return root?dfs(root):0;
    }
};
```

### 257.二叉树的所有路径

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218102645463.png" alt="image-20220218102645463" style="zoom:80%;" />

深度优先搜索：

```c++
class Solution {
public:
    void dfs(TreeNode* node,string path,vector<string>& res){
        if(!node) return;
        path += to_string(node->val);
        if(!node->left&&!node->right)
            res.push_back(path);
        else{
            path+="->";
            dfs(node->left,path,res);
            dfs(node->right,path,res);
        }
    }
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> res;
        dfs(root,"",res);
        return res;
    }
};
```

广度优先搜索：

```c++
class Solution {
public:
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> res;
        if(!root) return res;
        queue<TreeNode*> q;
        queue<string> q2;
        q.push(root);
        q2.push(to_string(root->val));
        while(!q.empty()){
            TreeNode* node = q.front();
            string path = q2.front();
            q.pop();
            q2.pop();
            if(!node->left&&!node->right){
                res.push_back(path);
            }
            else{
                if(node->left){
                    q.push(node->left);
                    q2.push(path+"->"+to_string(node->left->val));
                }
                if(node->right){
                    q.push(node->right);
                    q2.push(path+"->"+to_string(node->right->val));
                }
            }
        }
        return res;
    }
};
```

### 113.路径总和 II

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218102726722.png" alt="image-20220218102726722" style="zoom:80%;" />

深度优先搜索：递归1

```c++
class Solution {
    void dfs(vector<vector<int>>& res,TreeNode* node,int targetSum,vector<int> cur){
        if(!node) return;
        targetSum -= node->val;
        cur.push_back(node->val);
        if(!node->left&&!node->right&&targetSum==0){
            res.push_back(cur);
            return;    
        }
        dfs(res,node->left,targetSum,cur);
        dfs(res,node->right,targetSum,cur);
    }
public:
    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
        vector<vector<int>> res;
        vector<int> cur;
        dfs(res,root,targetSum,cur);
        return res;
    }
};
```

递归2

```c++
class Solution {
    vector<vector<int>> res;
    vector<int> cur;
    void dfs(TreeNode* node,int targetSum){
        if(!node) return;
        targetSum -= node->val;
        cur.push_back(node->val);
        if(!node->left&&!node->right&&targetSum==0){
            res.push_back(cur); 
            //此处写return会出错是为什么请注意
        }
        dfs(node->left,targetSum);
        dfs(node->right,targetSum);
        cur.pop_back();
    }
public:
    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
        dfs(root,targetSum);
        return res;
    }
};
```

广度优先搜索：

```c++
class Solution {
    vector<vector<int>> res;
    unordered_map<TreeNode*,TreeNode*> parent;
public:
    void getpath(TreeNode* node){
        vector<int> vec;
        while(1){
            vec.push_back(node->val);
            if(!parent.count(node)) break;
            node=parent[node];
        }
        reverse(vec.begin(),vec.end());
        res.push_back(vec);
    }
    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
        if(!root) return res;
        queue<TreeNode*> q1;
        queue<int> q2;
        q1.push(root);
        q2.push(0);
        while(!q1.empty()){
            TreeNode* node = q1.front();
            q1.pop();
            int sum = q2.front()+node->val;
            q2.pop();
            
            if(!node->left&&!node->right){
                if(sum==targetSum){
                    getpath(node);
                    continue;
                }
            }
            if(node->left){
                parent[node->left]=node;
                q1.push(node->left);
                q2.push(sum);
            }
            if(node->right){
                parent[node->right]=node;
                q1.push(node->right);
                q2.push(+sum);
            }
        }
        return res;
    }
};
```

### 129.求根节点到叶节点数字之和

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218102802768.png" alt="image-20220218102802768" style="zoom:80%;" />

深度优先搜索：

```c++
class Solution {
    int res=0;
    int dfs(TreeNode* node,int sum){
        if(!node) return 0;
        sum =sum*10+node->val;
        if(!node->left&&!node->right) return sum;
        return dfs(node->left,sum)+dfs(node->right,sum);
    }
public:
    int sumNumbers(TreeNode* root) {
        return dfs(root,0);
    }
};
```

递归二

```c++
class Solution {
    int res=0;
    int dfs(TreeNode* node,int sum){
        if(!node) return 0;
        sum =sum*10+node->val;
        if(!node->left&&!node->right)
            res+=sum;
        dfs(node->left,sum);
        dfs(node->right,sum);
        return 0;//代码不会运行到这句，
                    //因为一定会运行到第一句，叶子结点的孩子为空的时候
                    //将结果sum加入res 
                    //并执行第一行return 0
    }
public:
    int sumNumbers(TreeNode* root) {
        dfs(root,0);
        return res;
    }
};
```

广度优先搜索：

```c++
class Solution {
public:
    int sumNumbers(TreeNode* root) {
        if(!root) return 0;
        queue<TreeNode*> q;
        q.push(root);
        queue<int> q2;
        q2.push(0);
        int res = 0;
        while(!q.empty()){
            TreeNode* node = q.front();
            q.pop();
            int cur = q2.front()*10+node->val;
            q2.pop();
            if(!node->left&&!node->right){
                res+=cur;
                continue;
            }
            if(node->left){
                q.push(node->left);
                q2.push(cur);
            }
            if(node->right){
                q.push(node->right);
                q2.push(cur);
            }
        }
        return res;
    }
};
```

### 437.路径总和Ⅲ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218102907452.png" alt="image-20220218102907452" style="zoom:80%;" />

深度优先搜索：

```c++
class Solution {
    int findpath(TreeNode* node,long targetSum){
        if(!node) return 0;
        int res = 0;
        targetSum = targetSum-node->val;
        if(targetSum == 0)
            res++;
        res+=findpath(node->left,targetSum);
        res+=findpath(node->right,targetSum);
        return res;
    }
public:
    int pathSum(TreeNode* root, int targetSum) {
        if(!root) return 0;
        int res = findpath(root,targetSum);

        res+=pathSum(root->left,targetSum);
        res+=pathSum(root->right,targetSum);
        return res;
    }
};
```

前缀和：

```c++
class Solution {
    unordered_map<long long,int> pre;
    int dfs(TreeNode* node,long long cur,int targetSum){
        if(!node) return 0;
        cur += node->val;
        
        int res = 0;
        if(pre.count(cur-targetSum)){
            res = pre[cur-targetSum];
        }
        pre[cur]++;
        res+=dfs(node->left,cur,targetSum);
        res+=dfs(node->right,cur,targetSum);
        pre[cur]--;
        return res;
    }
public:
    int pathSum(TreeNode* root, int targetSum) {
        pre[0] = 1;
        return dfs(root,0,targetSum);
    }
};
```

## 2.20-----------------87

### 235.二叉搜索树的最近公共祖先

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218103216650.png" alt="image-20220218103216650" style="zoom:80%;" />

一次遍历：

```c++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(!root) return root;
        TreeNode* res = root;
        while(res){
            if(res->val<p->val&&res->val<q->val)
                res=res->right;
            else if(res->val>p->val&&res->val>q->val)
                res=res->left;
            else
                return res;
        }
        return nullptr;
    }
};
```

**适用于所有树，寻找最近公共祖先**

```c++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(!root) return root;
        
        if(p==root)return p;
        if(q==root)return q;

        TreeNode* left = lowestCommonAncestor(root->left,p,q);
        TreeNode* right = lowestCommonAncestor(root->right,p,q);

        if(!left) return right;
        if(!right) return left;
        return root;
    }
};
```

### 98.验证二叉搜索树

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218103257657.png" alt="image-20220218103257657" style="zoom:80%;" />

递归：

```c++
class Solution {
public:
    bool helper(TreeNode* node,long long lower,long long upper){
        if(!node) return true;
        if(node->val<=lower||node->val>=upper)
            return false;
        return helper(node->left,lower,node->val)&&helper(node->right,node->val,upper);
    }
    bool isValidBST(TreeNode* root) {
        return helper(root,LONG_MIN,LONG_MAX);
    }
};
```

中序遍历：

### 450. 删除二叉搜索树中的节点

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218103358358.png" alt="image-20220218103358358" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218103414906.png" alt="image-20220218103414906" style="zoom:80%;" />

```c++
class Solution {
    TreeNode* min_node(TreeNode* node){
        while(node->left){
            node=node->left;
        }
        return node;
    }
    TreeNode* delete_min(TreeNode* node){
        if(!node->left){
            TreeNode* newnode = node->right;
            delete node;
            return newnode;
        }
        node->left = delete_min(node->left);
        return node;
    }
public:
    TreeNode* deleteNode(TreeNode* root, int key) {
        if(!root) return root;
        if(key>root->val){
            root->right=deleteNode(root->right,key);
            return root;
        }
        else if(key<root->val){
            root->left=deleteNode(root->left,key);
            return root;
        }
        else{//if(root->val == key
            if(!root->left&&!root->right){
                delete root;
                return nullptr;
            }
            else if(root->left&&!root->right){
                TreeNode* newroot = root->left;
                delete root;
                return newroot;
            }
            else if(root->right&&!root->left){
                TreeNode* newroot = root->right;
                delete root;
                return newroot;
            }
            else {
                TreeNode* newnode = new TreeNode(min_node(root->right)->val,min_node(root->right)->left,min_node(root->right)->right);
                newnode->right = delete_min(root->right);
                newnode->left = root->left;
                delete root;
                return newnode;
            }
        }
    }
};
```

### 108. 将有序数组转换为二叉搜索树

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218103447962.png" alt="image-20220218103447962" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218103503663.png" alt="image-20220218103503663" style="zoom:80%;" />

中序遍历，递归：

```c++
class Solution {
public:
    TreeNode* helper(vector<int>& nums,int l,int r){
        if(l>r) return nullptr;
        int mid = (l+r)/2;
        TreeNode* node = new TreeNode(nums[mid]);
        node->left = helper(nums,l,mid-1);
        node->right = helper(nums,mid+1,r);
        return node;
    }
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return helper(nums,0,nums.size()-1);
    }
};
```

### 230. 二叉搜索树中第K小的元素

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218103541860.png" alt="image-20220218103541860" style="zoom:80%;" />

解法一：中序遍历：

```c++
class Solution {
public:
    vector<int> nums;
    void dfs(TreeNode* node){
        if(node->left)
            dfs(node->left);
        nums.push_back(node->val);
        if(node->right)
            dfs(node->right);
    }
    int kthSmallest(TreeNode* root, int k) {
        dfs(root);
        return nums[k-1];
    }
};
```

递归

```c++
class Solution {
    int res;
    int k1;
    void dfs(TreeNode* node){
        if(!node) return;
        dfs(node->left);
        k1--;
        if(k1==0) res = node->val;
        dfs(node->right);
    }
public:
    int kthSmallest(TreeNode* root, int k) {
        k1 = k;
        dfs(root);
        return res;
    }
};
```

解法二：记录子树的节点个数：

解法三：平衡二叉搜索树：

## 2.21---------------92

### 236. 二叉树的最近公共祖先

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218103620120.png" alt="image-20220218103620120" style="zoom:80%;" />

二叉树的最近公共祖先。

```c++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(!root) return root;
        if(root==q||root==p) return root;
        
        TreeNode* left=lowestCommonAncestor(root->left,p,q);
        TreeNode* right=lowestCommonAncestor(root->right,p,q);

        if(!left)return right;
        if(!right) return left;
        return root;
    }
};
```

### 17. 电话号码的字母组合

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218103725473.png" alt="image-20220218103725473" style="zoom:80%;" />

```c++
class Solution {
    unordered_map<char,string> map;
    vector<string> res;
    void dfs(string& digits,int index,string cur){
        if(index==digits.size()){
            res.push_back(cur);
            return;
        }
        for(int i=0;i<map[digits[index]].size();i++){
            cur += map[digits[index]][i];
            dfs(digits,index+1,cur);
            cur.pop_back();
        }
    }
public:
    vector<string> letterCombinations(string digits) {
        if(digits.size()==0) return res;
        map['2'] = "abc";
        map['3'] = "def";
        map['4'] = "ghi";
        map['5'] = "jkl";
        map['6'] = "mno";
        map['7'] = "pqrs";
        map['8'] = "tuv";
        map['9'] = "wxyz";
        dfs(digits,0,"");
        return res;
    }
};
```

### 93. 复原 IP 地址

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218103826901.png" alt="image-20220218103826901" style="zoom:80%;" />

```c++
class Solution {
    vector<string> res;
    vector<int> vec;
    void dfs(string& s,int k,int i){
        if(k==4){
            if(i==s.size()){
                string t;
                for(auto x:vec)
                    t+=to_string(x)+".";
                t.pop_back();
                cout<<t<<' ';
                res.push_back(t);
            }
            return;
        }

        if(i==s.size()) return;

        if(s[i]=='0'){
            vec[k]=0;
            dfs(s,k+1,i+1);
        }

        int num = 0;
        for(int j=i;j<s.size();j++){
            num = num*10 + (s[j]-'0');
            if(num>0&&num<=255){
                vec[k]=num;
                dfs(s,k+1,j+1);
            }
            else{
                break;
            }
        }
    }
public:
    vector<string> restoreIpAddresses(string s) {
        vec.resize(4);
        dfs(s,0,0);
        return res;
    }
};
```

### 131.分割回文串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218103920035.png" alt="image-20220218103920035" style="zoom:80%;" />

```c++
class Solution {
    bool f(string s){
        string t = s;
        reverse(s.begin(),s.end());
        return t==s;
    }
    vector<vector<string>> res;
    vector<string> cur;
    void dfs(string& s,int i){
        if(i==s.size()){
            res.push_back(cur);
            return;
        }
        for(int j=i;j<s.size();j++){
            if(f(s.substr(i,j-i+1))){
                cur.push_back(s.substr(i,j-i+1));
                dfs(s,j+1);
                cur.pop_back();
            }
        }
    }
public:
    vector<vector<string>> partition(string s) {
        dfs(s,0);
        return res;
    }
};
```

一个记忆化判断字符串为回文的方法

```c++
//					f[i][j] 表示s[i..j]为回文串
    string s = "aabbaabbaa";
    int n = s.size();
    vector<vector<bool>> f(s.size(), vector<bool>(s.size(), true));
    for (int i = n - 1; i >= 0; --i) {
        for (int j = i + 1; j < n; ++j) {
            f[i][j] = (s[i] == s[j]) && f[i + 1][j - 1];
        }
    }
    cout << f[4][5] << endl;
```

### 46.全排列

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218103955636.png" alt="image-20220218103955636" style="zoom:80%;" />

```c++
class Solution {
    vector<vector<int>> res;
    vector<bool> vis;
    vector<int> cur;
    void dfs(vector<int>& nums,int index){
        if(cur.size()==nums.size()){
            res.push_back(cur);
            return;
        }
        for(int i=0;i<nums.size();i++){
            if(!vis[i]){
                cur.push_back(nums[i]);
                vis[i] = true;
                dfs(nums,index+1);
                cur.pop_back();
                vis[i] = false;
            }
        }
    }
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vis.assign(nums.size(),false);
        dfs(nums,0);
        return res;
    }
};
```

递归二

```c++
class Solution {
    vector<vector<int>> res;
    vector<bool> vis;
    vector<int> cur;
    void dfs(vector<int>& nums,int i){
        if(i==nums.size()){
            res.push_back(cur);
            return;
        }
        for(int j=0;j<nums.size();j++){
            if(!vis[j]){
                cur.push_back(nums[j]);
                vis[j] = true;
                dfs(nums,i+1);
                cur.pop_back();
                vis[j] = false;
            }
        }
    }
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vis.assign(nums.size(),false);
        dfs(nums,0);
        return res;
    }
};
```

## 2.22-----------------97

### 47.全排列Ⅱ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104026369.png" alt="image-20220218104026369" style="zoom:80%;" />

```c++
class Solution {
    void dfs(vector<vector<int>>& res,vector<int>& nums,vector<int> cur,int index,vector<bool>& vis){
        if(index==nums.size()){
            res.push_back(cur);
            return;
        }
        for(int i=0;i<nums.size();i++){
            if(vis[i] || i>0&&nums[i]==nums[i-1]&&!vis[i-1])
                continue;
            cur.push_back(nums[i]);
            vis[i]=1;
            dfs(res,nums,cur,index+1,vis);
            vis[i]=0;
            cur.pop_back();
        }
    }
public:
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> cur;
        vector<bool> vis(nums.size(),false);
        sort(nums.begin(),nums.end());
        dfs(res,nums,cur,0,vis);
        return res;
    }
};
```

### 77.组合

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104057464.png" alt="image-20220218104057464" style="zoom:80%;" />

```c++
class Solution {
    vector<vector<int>> res;
    void dfs(int n,int k,int begin,vector<int> p){
        if(p.size()==k){
            res.push_back(p);
            return;
        }
      //for(int i=begin;i<=n;i++)
      //优化：剩余可选必须大于等于空位
      //(n-i+1) >= k-c.size()
      //i<=n+1-k+p.size()
        for(int i=begin;i<=n+1-k+p.size();i++){
            p.push_back(i);
            dfs(n,k,i+1,p);
            p.pop_back();
        }
    }
public:
    vector<vector<int>> combine(int n, int k) {
        vector<int> p;
        dfs(n,k,1,p);
        return res;
    }
};
```

### 39.组合总和

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104144475.png" alt="image-20220218104144475" style="zoom:80%;" />

```c++
class Solution {
    void dfs(vector<vector<int>>& res,vector<int> cur,vector<int>& candidates,int target,int index){
        if(index==candidates.size())
            return;
        if(target==0){
            res.push_back(cur);
            return;
        }
        dfs(res,cur,candidates,target,index+1);//跳过index处的元素找下一个
        if(target-candidates[index]>=0){
            cur.push_back(candidates[index]);
            dfs(res,cur,candidates,target-candidates[index],index);//重复找index中的元素
            cur.pop_back();
        }
    }
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> res;
        vector<int> cur;
        dfs(res,cur,candidates,target,0);
        return res;
    }
};
```

### 40.组合总和Ⅱ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104231333.png" alt="image-20220218104231333" style="zoom:80%;" />

```c++
class Solution {
    void dfs(vector<vector<int>>& res,vector<int> cur,vector<int>& candidates,int target,int index){
        if(target==0){
            res.push_back(cur);
            return;
        }

        for(int i=index;i<candidates.size();i++){
            if(i>index&&candidates[i]==candidates[i-1])
                continue;
            if(target-candidates[index]>=0){
                cur.push_back(candidates[i]);
                dfs(res,cur,candidates,target-candidates[i],i+1);
                cur.pop_back();
            }
        }
    }
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        vector<vector<int>> res;
        vector<int> cur;
        sort(candidates.begin(),candidates.end());
        dfs(res,cur,candidates,target,0);
        return res;
    }
};
```

### 216.组合总和Ⅲ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104252289.png" alt="image-20220218104252289" style="zoom:80%;" />

```c++
class Solution {
    vector<vector<int>> res;
    void dfs(int k,int n,vector<int> p,int begin){
        if(p.size()==k){
            if(n==0)
                res.push_back(p);
            return;
        }       
        for(int i=begin;i<=9;i++){
            p.push_back(i);
            dfs(k,n-i,p,i+1);
            p.pop_back();
        }
    }
public:
    vector<vector<int>> combinationSum3(int k, int n) {
        vector<int> p;
        dfs(k,n,p,1);
        return res;
    }
};
```

## 2.23-------------------102

### 78.子集

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104326542.png" alt="image-20220218104326542" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        int n = nums.size();
        vector<vector<int>> res;
        for(int mask = 0;mask<(1<<n);mask++){
            vector<int> t;
            for(int i=0;i<n;i++){
                if(mask&(1<<i))t.push_back(nums[i]);
            }
            res.push_back(t);
        }
        return res;
    }
};
```

迭代

```c++
class Solution {
    vector<vector<int>> res;
    void dfs(vector<int>& nums,vector<int> p,int index){
        if(index==nums.size()){
            res.push_back(p);
            return;
        }
        dfs(nums,p,index+1);//直接跳过

        p.push_back(nums[index]);//不跳过
        dfs(nums,p,index+1);
        p.pop_back();

    }
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<int> p;
        dfs(nums,p,0);
        return res;
    }
};
```

### 90.子集Ⅱ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104354563.png" alt="image-20220218104354563" style="zoom:80%;" />

```c++
class Solution {
    vector<vector<int>> res;
    void dfs(vector<int>& nums,int index,vector<int> p){
        res.push_back(p);
        if(index>=nums.size())return;
        for(int i=index;i<nums.size();i++){
            if(i>index&&nums[i]==nums[i-1])continue;
            p.push_back(nums[i]);
            dfs(nums,i+1,p);
            p.pop_back();
        }
    }
public:
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        vector<int> p;
        sort(nums.begin(),nums.end());
        dfs(nums,0,p);
        return res;
    }
};
```

### 401.二进制手表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104445298.png" alt="image-20220218104445298" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104453781.png" alt="image-20220218104453781" style="zoom:50%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104506370.png" alt="image-20220218104506370" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<string> readBinaryWatch(int turnedOn) {
        vector<string> res;
        for(int i=0;i<12;i++){
            for(int j=0;j<60;j++){
                if(bitset<6>(i).count()+bitset<6>(j).count()==turnedOn){
                    res.push_back(to_string(i)+":"+(j<10?"0":"")+to_string(j));
                }
            }
        }
        return res;
    }
};
```

### 79.单词搜索

​	<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104538906.png" alt="image-20220218104538906" style="zoom:80%;" />

```c++
class Solution {
    int m;
    int n;
    int d[4][2]={{1,0},{-1,0},{0,1},{0,-1}};
    vector<vector<bool>> vis;
    bool inarea(int i,int j){
        return (i>=0&&i<m)&&(j>=0&&j<n);
    }
    bool dfs(vector<vector<char>>& board,string& word,int index,int i,int j){
        if(index==word.size()-1){
            return board[i][j]==word[index];
        }
        if(board[i][j]==word[index]){
            vis[i][j]=true;
            
            for(int k=0;k<4;k++){
                int x1=i+d[k][0];
                int y1=j+d[k][1];
                if(inarea(x1,y1)&&!vis[x1][y1]&&dfs(board,word,index+1,x1,y1))
                    return true;
            }
            vis[i][j]=false;
        }
        return false;
    }
public:
    bool exist(vector<vector<char>>& board, string word) {
        m=board.size();
        if(m==0) return false;
        n=board[0].size();
        vis = vector<vector<bool>>(m,vector<bool>(n,false));
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(dfs(board,word,0,i,j)) 
                    return true;
            }
        }
        return false;
    }
};
```

### 200.岛屿数量

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104610175.png" alt="image-20220218104610175" style="zoom:80%;" />

```c++
class Solution {
    int m,n;
    int d[4][2]={{1,0},{-1,0},{0,1},{0,-1}};	
    vector<vector<bool>> vis;
    void dfs(vector<vector<char>>& grid,int i,int j){
        vis[i][j] = true;
        for(int k=0;k<4;k++){
            int x=i+d[k][0];
            int y=j+d[k][1];
            if(x>=0&&x<m&&y>=0&&y<n&&grid[x][y]=='1'&&!vis[x][y])
                dfs(grid,x,y);
        }
    }
public:
    int numIslands(vector<vector<char>>& grid) {
        m = grid.size();
        n = grid[0].size();
        int res = 0;
        vis = vector<vector<bool>>(m,vector<bool>(n,false));
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(grid[i][j]=='1'&&!vis[i][j]){
                    res++;
                    dfs(grid,i,j);
                }
            }
        }
        return res;
    }
};
```

## 2.24-------------------107

### 130.被围绕的区域

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104644711.png" alt="image-20220218104644711" style="zoom:80%;" />

```c++
class Solution {
    int m,n;
    void dfs(vector<vector<char>>& board,int i,int j){
        if(i<0||i>=m||j<0||j>=n||board[i][j]!='O')
            return;
        board[i][j]='a';
        dfs(board,i-1,j);
        dfs(board,i+1,j);
        dfs(board,i,j-1);
        dfs(board,i,j+1);
    }
public:
    void solve(vector<vector<char>>& board) {
        m=board.size();
        n=board[0].size();
        for(int j=0;j<n;j++){
            dfs(board,0,j);
            dfs(board,m-1,j);
        }
        for(int i=0;i<m;i++){
            dfs(board,i,0);
            dfs(board,i,n-1);
        }

        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(board[i][j]=='a')
                    board[i][j]='O';
                else if(board[i][j]=='O')
                    board[i][j]='X';
            }
        }
    }
};
```

### 417.太平洋大西洋水流问题

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104725387.png" alt="image-20220218104725387" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104735577.png" alt="image-20220218104735577" style="zoom: 33%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104753822.png" alt="image-20220218104753822" style="zoom:80%;" />

```c++
class Solution {
    int m,n;
    int d[4][2]={{1,0},{-1,0},{0,1},{0,-1}};
    vector<vector<int>> res;
    void dfs(vector<vector<bool>>& o,vector<vector<int>>& heights,int i,int j){
        if(o[i][j]) return;
        o[i][j] = true;
        for(int k=0;k<4;k++){
            int x=i+d[k][0];
            int y=j+d[k][1];
            if(x>=0&&x<m&&y>=0&&y<n&&heights[x][y]>=heights[i][j])
                dfs(o,heights,x,y);
        }
    }
public:
    vector<vector<int>> pacificAtlantic(vector<vector<int>>& heights) {
        m=heights.size();
        n=heights[0].size();
        vector<vector<bool>> o1(m,vector<bool>(n,false));
        vector<vector<bool>> o2(m,vector<bool>(n,false));

        for(int i=0;i<m;i++){
            dfs(o1,heights,i,0);
        }
        for(int j=1;j<n;j++){
            dfs(o1,heights,0,j);
        }
        for(int i=0;i<m;i++){
            dfs(o2,heights,i,n-1);
        }
        for(int j=0;j<n-1;j++){
            dfs(o2,heights,m-1,j);
        }
        cout<<"dad"<<endl;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(o1[i][j]&&o2[i][j])
                    res.push_back({i,j});
            }
        }
        return res;
    }
};
```

### 51.N皇后

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218104828650.png" alt="image-20220218104828650" style="zoom: 80%;" />



```c++
class Solution {
    vector<vector<string>> res;
    int n;
    vector<bool> col;
    vector<bool> dia1;
    vector<bool> dia2;
    void dfs(int index,vector<int>& p){
        if(index==n){
            res.push_back(transfer(p));
            return;
        }
        for(int i=0;i<n;i++)
            if(!col[i]&&!dia1[index+i]&&!dia2[index-i+n-1]){
                p.push_back(i);
                col[i]=true;
                dia1[index+i]=true;
                dia2[index-i+n-1]=true;
                dfs(index+1,p);
                col[i]=false;
                dia1[index+i]=false;
                dia2[index-i+n-1]=false;
                p.pop_back();
            }
        return;
    }
    vector<string> transfer(vector<int>& row){
        vector<string> res(row.size(),string(row.size(),'.'));
        for(int i=0;i<row.size();i++)
            res[i][row[i]]='Q';
        return res;
    }
public:
    vector<vector<string>> solveNQueens(int n) {
        this->n=n;
        res.clear();
        col=vector<bool>(n,false);
        dia1=vector<bool>(2*n-1,false);
        dia2=vector<bool>(2*n-1,false);
        vector<int> p;
        dfs(0,p);
        return res;
    }
};
```

### 52.

### 37.

## 2.25--------------112

### 70.爬楼梯

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218105049170.png" alt="image-20220218105049170" style="zoom:80%;" />

动态规划：

```c++
class Solution {
public:
    int climbStairs(int n) {
        int a=0,b=0,c=1;
        for(int i=1;i<=n;i++){
            a=b;
            b=c;
            c=a+b;
        }
        return c;
    }
};
```

```c++
class Solution {
public:
    int climbStairs(int n) {
        vector<int> vec(n+1,-1);
        vec[0]=1;
        vec[1]=1;
        for(int i=2;i<=n;i++){
            vec[i]=vec[i-1]+vec[i-2];
        }
        return vec[n];
    }
};
```

矩阵快速幂：

通项公式：

### 120.三角形最小路径和

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218105114591.png" alt="image-20220218105114591" style="zoom:80%;" />

### 64.

### 343.整数拆分

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218105228678.png" alt="image-20220218105228678" style="zoom:80%;" />

动态规划：

```c++
class Solution {
public:
    int integerBreak(int n) {
        vector<int> dp(n+1);
        for(int i=2;i<=n;i++)
            for(int j=1;j<i;j++)
                dp[i]=max(max(dp[i],j*(i-j)),j*dp[i-j]);
        return dp[n];
    }
};
```

### 279.完全平方数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218105338799.png" alt="image-20220218105338799" style="zoom:80%;" />

## 2.26---------------117

### 91.解码方法

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218105406768.png" alt="image-20220218105406768" style="zoom:80%;" />

### 62.不同路径

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218105438416.png" alt="image-20220218105438416" style="zoom:80%;" />

### 63.不同路径Ⅱ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218105509465.png" alt="image-20220218105509465" style="zoom:80%;" />

### 198.打家劫舍

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218105552231.png" alt="image-20220218105552231" style="zoom:80%;" />

记忆化搜索：

```c++
class Solution {
private:
    vector<int> vec;
    //考虑抢劫nums[index....nums.size()-1]的房子
    int tryRob(vector<int>& nums,int index){
        if(index>=nums.size())return 0;

        if(vec[index]!=-1)return vec[index];
        int res=0;
        for(int i=index;i<nums.size();i++)
            res=max(res,nums[i]+tryRob(nums,i+2));
        
        vec[index]=res;
        return res;
    }
public:
    int rob(vector<int>& nums) {
        vec=vector<int>(nums.size(),-1);
        return tryRob(nums,0);//最初从第0个房子开始偷
    }
};
```

动态规划：

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        int n=nums.size();
        if(n==0)return 0;

        vector<int> vec(n,-1);
        vec[n-1]=nums[n-1];
        for(int i=n-2;i>=0;i--){
            for(int j=i;j<n;j++)
                vec[i]=max(vec[i],nums[j]+(j+2<n?vec[j+2]:0));
        }
        return vec[0];
    }
};
```

### 213.打家劫舍Ⅱ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218105622167.png" alt="image-20220218105622167" style="zoom:80%;" />

## 2.27---------------122

### 337.打家劫舍Ⅲ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218105646048.png" alt="image-20220218105646048" style="zoom:80%;" />

### 309.最佳买卖股票时机含冷冻期

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218105712985.png" alt="image-20220218105712985" style="zoom:80%;" />

### 416.分割等和子集

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218105802485.png" alt="image-20220218105802485" style="zoom:80%;" />

动态规划：

```c++
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum=0;
        int n=nums.size();
        for(int i=0;i<n;i++){
            sum+=nums[i];
        }
        if(sum%2)return false;

        int C=sum/2;
        vector<bool> vec(C+1,false);

        for(int i=0;i<=C;i++)
            vec[i]=(nums[0]==i);

        for(int i=1;i<n;i++)
            for(int j=C;j>=nums[i];j--)
                vec[j]=vec[j]||vec[j-nums[i]];

        return vec[C];            
    }
};
```

### 322.

### 377.组合总和Ⅳ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218105908513.png" alt="image-20220218105908513" style="zoom:80%;" />

## 2.28----------------127

### 474.一和零

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218105934916.png" alt="image-20220218105934916" style="zoom:80%;" />

### 139.单词拆分

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218110000956.png" alt="image-20220218110000956" style="zoom:80%;" />

### 494.目标和

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218110026271.png" alt="image-20220218110026271" style="zoom:80%;" />

### 300.最长递增子序列

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218110054106.png" alt="image-20220218110054106" style="zoom:80%;" />

动态规划：

```c++
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n=nums.size();
        if(n==0)return 0;
        //vec[i]表示以数字i为结尾的最长上升子序列的长度
        vector<int> vec(n,1);
        for(int i=1;i<n;i++){
            for(int j=0;j<i;j++)
                if(nums[j]<nums[i])
                    vec[i]=max(vec[i],1+vec[j]);
        }
        for(int i=0;i<n;i++)
            if(vec[i]>vec[0])
                vec[0]=vec[i];
        return vec[0];
    }
};
```

### 376.摆动序列

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218110120009.png" alt="image-20220218110120009" style="zoom:80%;" />

## 3.1---------------130

### 455.分发饼干

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218110151723.png" alt="image-20220218110151723" style="zoom:80%;" />

```c++
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(),g.end(),greater<int>());
        sort(s.begin(),s.end(),greater<int>());

        int si=0,gi=0;
        int res=0;
        while(gi<g.size()&&si<s.size()){
            if(s[si]>=g[gi]){
                res++;
                si++;
                gi++;
            }
            else
                gi++;
        }
        return res;
    }
};
```

### 392.判断子序列

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218110218282.png" alt="image-20220218110218282" style="zoom:80%;" />

### 252.会议室

```c++
bool cmp(vector<int> a,vector<int> b){
    if(a[0]!=b[0])return a[0]<b[0];
    return a[1]<b[1];
}
class Solution {
public:
    bool canAttendMeetings(vector<vector<int>>& intervals) {
        sort(intervals.begin(),intervals.end());
        for(int i=1;i<intervals.size();i++){
            if(intervals[i][0]<intervals[i-1][1])
                return false;
        }
        return true;
    }
};
```

### 253.会议室Ⅱ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502084833209.png" alt="image-20220502084833209" style="zoom:80%;" />

```c++
class Solution {
public:
    int minMeetingRooms(vector<vector<int>>& intervals) {
        map<int,int> map1;
        for(auto x:intervals){
            map1[x[0]]++;
            map1[x[1]]--;
        }
        int res = 0;
        int sum = 0;
        for(auto i:map1){
            sum+=i.second;
            res = max(res,sum);
        }
        return res;
    }
};
```

### 435.无重叠区间

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218110249656.png" alt="image-20220218110249656" style="zoom:80%;" />

动态规划

```

```

### 876.链表的中间结点

第一种对于偶数个节点的链表来说，找的是中间两数的前一个，第二中找的是中间两数的后一个

```c++
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* s = head;
        ListNode* f = head;
        while(f->next&&f->next->next){
            s=s->next;
            f=f->next->next;
        }
        return s;
    }
};
```

```c++
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* s = head;
        ListNode* f = head;
        while(f->next){
            s=s->next;
            f=f->next;
            if(f->next)
                f=f->next;
        }
        return s;
    }
};
```

## 华为机试

### 1. 字符串最后一个单词的长度

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214180711177.png" alt="image-20220214180711177" style="zoom:80%;" />

```c++
#include <string>
#include <iostream>
#include <vector>
using namespace std;
int main(){
    string s;
    vector<char> vec;
    getline(cin,s);
    for(int i=0;i<s.size();i++){
        vec.push_back(s[i]);
        if(s[i]==' ')
            vec.clear();
    }
    cout<<vec.size();
    return 0;
}
```

### 2.计算某字符出现次数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214175311967.png" alt="image-20220214175311967" style="zoom:80%;" />

数组可以用map来代替。

```c++
#include <iostream>
#include <string>
using namespace std;
int main()
{
    string s;
    char ch;
    getline(cin, s);
    cin >> ch;

    int count = 0;
    for(auto x:s) if(tolower(x) == tolower(ch)) count++;
    cout << count << endl;
}
```

### 3.明明的随机数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220214204239240.png" alt="image-20220214204239240" style="zoom:80%;" />

```
 输入        3
            2
            2
            1
            11
            10
            20
            40
            32
            67
            40
            20
            89
            300
            400
            15
输出：
1
2
10
15
20
32
40
67
89
300
400
```

```c++
#include <iostream>
#include <set>
#include <vector>
using namespace std;
int main(){
    int N;
    while(cin>>N){
        int a[1001]={0};
        int n;
        while(N--){
            cin>>n;
            a[n]=1;
        }
        for(int i=0;i<1001;i++)
            if(a[i])
                cout<<i<<endl;
    }
    return 0;
}
```

### 4.字符串分隔

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220215221444796.png" alt="image-20220215221444796" style="zoom:80%;" />

```c++
#include <iostream>
using namespace std;
int main(){
    string s;
    while(cin>>s){
        if(s.size()<=8){
            cout<<s;
            for(int i=0;i<8-s.size();i++)
                cout<<'0';
            cout<<endl;
        }
        else{
            int a=s.size()/8;
            int b=s.size()%8;
            for(int i=0;i<8*a;i=i+8)
                cout<<s[i]<<s[i+1]<<s[i+2]<<s[i+3]<<s[i+4]<<s[i+5]<<s[i+6]<<s[i+7]<<endl;
            for(int i=0;i<b;i++)
                cout<<s[8*a+i];
            if(b){
            for(int i=0;i<8-b;i++)
                cout<<'0';
            cout<<endl;}
        }
    }
    return 0;
}
```

### 5.进制转换

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220215232225754.png" alt="image-20220215232225754" style="zoom:80%;" />

解法一：

```c++
#include<iostream>
#include<string>
using namespace std;
  
int main(){
    string str;
    while(cin>>str){
        cout << stoi(str,0,16) << endl;
    }
}
```

解法二：

```c++
#include <iostream>
#include <cassert>
#include <cmath>
using namespace std;
int func(char ch){
    switch(ch){
        case '0':return 0;
        case '1':return 1;
        case '2':return 2;
        case '3':return 3;
        case '4':return 4;
        case '5':return 5;
        case '6':return 6;
        case '7':return 7;
        case '8':return 8;
        case '9':return 9;
        case 'A':return 10;
        case 'B':return 11;
        case 'C':return 12;
        case 'D':return 13;
        case 'E':return 14;
        case 'F':return 15;
    }
    return 0;
}
int main(){
    string s;
    while(cin>>s){
        assert(s[0]=='0'&&s[1]=='x');
        int sum=0;
        for(int i=2;i<s.size();i++)
            sum+=func(s[i])*pow(16,s.size()-i-1);
        cout<<sum<<endl;       
    }
    return 0;
}
```

### 6.质数因子

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220217105029766.png" alt="image-20220217105029766" style="zoom:80%;" />

```c++
#include <iostream>
using namespace std;
int main() {
    int n;
    cin>>n;
    for(int i=2;i*i<=n;i++){
        if(n%i==0){
            cout<<i<<" ";
            n/=i;
            i=1;
        }
    }
    cout<<n<<" ";
    return 0;
}
```

### 7.取近似值

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220215215408299.png" alt="image-20220215215408299" style="zoom:80%;" />

```c++
#include <iostream>
using namespace std;
int main(){
    double a;
    cin>>a;
    if(a-int(a)<0.5)
        cout<<int(a);
    else
        cout<<int(a)+1;
    return 0;
}
```

### 8.**合并表记录**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218221400657.png" alt="image-20220218221400657" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218221418882.png" alt="image-20220218221418882" style="zoom:80%;" />

```c++
#include <iostream>
#include <map>
using namespace std;
int main()
{
    map<int, int> m;
    int n; cin >> n;
    while(n--)
    {
        int key, value;
        cin >> key >> value;
        m[key] += value;
    }
    for(auto x : m) cout << x.first << ' ' << x.second << endl;
}
```

### 9.提取不重复的整数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220219000816656.png" alt="image-20220219000816656" style="zoom:80%;" />

```c++
#include <iostream>
#include <string>
#include <unordered_set>
#include <algorithm>
using namespace std;
int main(){
    int n;
    cin>>n;
    string res;
    unordered_set<char> set;
    string s= to_string(n);
    reverse(s.begin(),s.end());
    for(char a:s){
        if(set.count(a))
            continue;
        set.insert(a);
        res+=a;
    }
    cout<<stoi(res);  
}
```

### 10.字符个数统计

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220219103153314.png" alt="image-20220219103153314" style="zoom:80%;" />

```c++
#include <iostream>
#include <string>
#include <unordered_set>
using namespace std;
int main(){
    string s;
    cin>>s;
    unordered_set<char> set;
    for(char ch:s)
        set.insert(ch);
    cout<<set.size();
    return 0;
}
```

### 11.数字颠倒

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220219103906818.png" alt="image-20220219103906818" style="zoom:80%;" />

```c++
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;
int main(){
    int n;
    cin>>n;
    string s=to_string(n);
    reverse(s.begin(),s.end());
    cout<<s;
}
```

```c++
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;
int main(){
    int n;
    cin>>n;
    if(n==0)cout<<n;
    while(n){
        cout<<n%10;
        n/=10;
    }
}
```

### 12.反转字符串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220219124330349.png" alt="image-20220219124330349" style="zoom: 80%;" />

```c++
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;
int main(){
    string s;
    cin>>s;
    reverse(s.begin(),s.end());
    cout<<s;
}
```

```c++
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;
int main(){
    string s;
    cin>>s;
    for(int i=0;i<=(s.size()-1)/2;i++)
        swap(s[i],s[s.size()-i-1]);
    cout<<s;
}
```

### 13.句子逆序

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220219130353658.png" alt="image-20220219130353658" style="zoom:80%;" />

```c++
#include <iostream>
#include <string>
using namespace std;
int main() 
{
    string s;
    string res = "";
    while(cin >> s)
        res = s + " " + res;
    res.resize(res.size() - 1);
    cout << res;
}
```

### 14.字符串排序

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220219130929681.png" alt="image-20220219130929681" style="zoom:80%;" />

```c++
#include <string>
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
int main(){
    int n;
    cin>>n;
    string s;
    vector<string> vec;
    while(cin>>s){
        vec.push_back(s);
    }
    sort(vec.begin(),vec.end());
    for(auto s:vec)
        cout<<s<<endl;
}
```

### 15.求int型正整数在内存中存储时1的个数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220219134616065.png" alt="image-20220219134616065" style="zoom:80%;" />

```c++
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;
int main(){
    int n;
    cin>>n;
    vector<int> vec;
    while(n){
        vec.push_back(n%2);
        n/=2;
    }
    int count=0;
    for(auto a:vec)
        if(a)
            count++;
    cout<<count;
}
```

### 16.购物单

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505205826752.png" alt="image-20220505205826752" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505205848350.png" alt="image-20220505205848350" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505205904987.png" alt="image-20220505205904987" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    vector<vector<int>> p(60,vector<int>(3,0));//物品价格
    vector<vector<int>> v(60,vector<int>(3,0));//重要度（价值）
    
    int N,m;
    cin>>N>>m;
    int a,b,c;
    for(int i = 1;i <= m;i++){
        int a,b,c;
        cin>>a>>b>>c;
        if(c == 0){
            p[i][0] = a;
            v[i][0] = b*a;
        }
        else{
            if(p[c][1] == 0){
                p[c][1] = a;
                v[c][1] = b*a;
            }
            else{
                p[c][2] = a;
                v[c][2] = b*a;
            }
        }
    }
    vector<vector<int>> dp(m + 1,vector<int>(N + 1,0));
    for(int i=1;i <= m;i++){
        for(int j=0;j<=N;j++){
            int a = p[i][0], b = v[i][0];
            int c = p[i][1], d = v[i][1];
            int e = p[i][2], f = v[i][2];
            dp[i][j] = j >= a ? max(dp[i-1][j-a] + b, dp[i-1][j]) : dp[i-1][j];
            dp[i][j] = j >= (a+c) ? max(dp[i-1][j-a-c] + b + d, dp[i][j]) : dp[i][j];
            dp[i][j] = j >= (a+e) ? max(dp[i-1][j-a-e] + b + f, dp[i][j]) : dp[i][j];
            dp[i][j] = j >= (a+c+e) ? max(dp[i-1][j-a-c-e] + b + d + f, dp[i][j]) : dp[i][j]; 
        }
    }
    cout<<dp[m][N];
}
```

### 18.**识别有效的IP地址和掩码并进行分类统计**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505205942967.png" alt="image-20220505205942967" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210009364.png" alt="image-20220505210009364" style="zoom:80%;" />

```
```



### 17.坐标移动

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220416124119129.png" alt="image-20220416124119129" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220416124130230.png" alt="image-20220416124130230" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
//判断字符串是否合法
bool f1(string s){
    if(s.size()<=1 || s.size()>3)return false;
    if(s.size()==3&&(s[0]=='A'||s[0]=='W'||s[0]=='S'||s[0]=='D')&& isdigit(s[1])&&isdigit(s[2]))
       return true;
    if(s.size()==2&&(s[0]=='A'||s[0]=='W'||s[0]=='S'||s[0]=='D')&& isdigit(s[1]))
       return true;
    return false;
}
int main(){
    string s;
    int a[2]={0,0};
    while(getline(cin,s)){
        string t;
        vector<string> vec;
        for(auto c:s){
            if(c!=';'){
                t+=c;
            }
            else{
                if(f1(t))
                    vec.push_back(t);
                t.clear();
            }
        }
        for(auto s:vec){
            if(s[0]=='A')
                a[0]-=stoi(s.substr(1));
            else if(s[0]=='S')
                a[1]-=stoi(s.substr(1));
            else if(s[0]=='D')
                a[0]+=stoi(s.substr(1));
            else if(s[0]=='W')
                a[1]+=stoi(s.substr(1));
        }
        cout<<a[0]<<','<<a[1]<<endl;
    }
}
```

### 19.简单错误记录

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210036199.png" alt="image-20220505210036199" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210102520.png" alt="image-20220505210102520" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int contain(string s,int t,vector<pair<pair<string,int>,int>> vec){
    for(int i = 0;i < vec.size(); i++)
        if(vec[i].first.first == s && vec[i].first.second == t) return i;
    return -1;
}
int main(){
    vector<pair<pair<string,int>,int>> vec;
    string s;
    while(getline(cin,s)){
        string t;
        string tmp;
        for(auto c:s){
            if(c!=' ' && c!='\\')
                t += c;
            else if(c == '\\')
                t.clear();
            else if(c == ' ' && t != "" ){
                tmp = t;
                t.clear();
            }
        }
        if(tmp.size() > 16)
            tmp = tmp.substr(tmp.size() - 16);
        if(contain(tmp,stoi(t),vec) == -1)
            vec.emplace_back(make_pair(tmp,stoi(t)),1);
        else
            vec[contain(tmp,stoi(t),vec)].second++;
        
    }
    for(int i = max(0,(int)vec.size() - 8);i <= vec.size() - 1 ; i++){
        cout<<vec[i].first.first<<' '<<vec[i].first.second<<' '<<vec[i].second<<endl;
    }
}
```





### 20.密码验证合格程序

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220416154052344.png" alt="image-20220416154052344" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int contain1(string s){
    for(auto c:s)
        if(c>=48&&c<=57)
            return 1;
    return 0;
}
int contain2(string s){
    for(auto c:s)
        if(c>=65&&c<=90)
            return 1;
    return 0;
}
int contain3(string s){
    for(auto c:s)
        if(c>=97&&c<=122)
            return 1;
    return 0;
}
int contain4(string s){
    for(auto c:s)
        if(ispunct(c))
            return 1;
    return 0;
}
bool f1(string s){
    unordered_map<string,int> map;
    for(int size=3;size<=s.size();size++){
        for(int i=0;i<=s.size()-size;i++){
            string t = s.substr(i,size);
            if(map.count(t))
                map[t]++;
            else
                map.insert(make_pair(t,1));
        }
    }
    for(auto it=map.begin();it!=map.end();it++){
        if((*it).second>1)
            return false;
    }
    return true;
}
bool f(string s){
    if(s.size()<=8) return false;
    if(contain1(s)+contain2(s)+contain3(s)+contain4(s)<=2) return false;
    if(!f1(s)) return false;
    
    return true;
}
int main(){
    string s;
    while(cin>>s){
        if(f(s))
            cout<<"OK"<<endl;
        else
            cout<<"NG"<<endl;
    }
}
```









### 21.简单密码

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220227162529314.png" alt="image-20220227162529314" style="zoom:80%;" />

```c++
#include <iostream>
#include <string>
using namespace std;
void func(char& ch){
    if(ch=='a'||ch=='b'||ch=='c') ch= '2';
    if(ch=='d'||ch=='e'||ch=='f') ch= '3';
    if(ch=='g'||ch=='h'||ch=='i') ch= '4';
    if(ch=='j'||ch=='k'||ch=='l') ch= '5';
    if(ch=='m'||ch=='n'||ch=='o') ch= '6';
    if(ch=='p'||ch=='r'||ch=='q'||ch=='s') ch= '7';
    if(ch=='t'||ch=='u'||ch=='v') ch= '8';
    if(ch=='w'||ch=='x'||ch=='y'||ch=='z') ch= '9';
    if(ch>=65&&ch<90)ch= tolower(ch)+1;
    if(ch==90)ch='a';
}
int main(){
    string s;
    while(cin>>s){
        for(int i=0;i<s.size();i++)
            func(s[i]);
        cout<<s<<endl;
    }
    return 0;
}
```





### 22.汽水瓶

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220227165159446.png" alt="image-20220227165159446" style="zoom:80%;" />

```c++
#include <iostream>
#include <vector>
using namespace std;
int func(int x){
    int n=0;
    while(x>=2){
        n+=x/3;
        x=x/3+x%3;
        if(x==2){
            n++;
            break;
        }
    }
    return n;
}
int main(){
    vector<int> vec;
    int x;
    while(cin>>x){
        if(x==0)break;
        vec.push_back(x);
    }
    for(auto a:vec)
        cout<<func(a)<<endl;
}
```

```c++
#include <iostream>
#include <vector>
using namespace std;
int main(){
    int x;
    while(cin>>x){
        int n=0;
        if(x==0)break;
        while(x>=2){
            n+=x/3;
            x=x/3+x%3;
            if(x==2){
                n++;
                break;
            }
        }
        cout<<n<<endl;
    }
}
```

### 23.删除字符串中出现次数最少的字符

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220227170529257.png" alt="image-20220227170529257" style="zoom:80%;" />

```c++
#include <iostream>
using namespace std;
int main(){
    string s;
    while(cin>>s){
        int map[128]={};
        for(auto ch:s)                            //统计字符频率
            map[ch]++;
        int freq=INT8_MAX;
        for(int i=0;i<128;i++)                    //记录最小频率
            if(map[i]!=0&&map[i]<freq)
                freq=map[i];
        for(int i=0;i<s.size();i++){
            if(map[s[i]]==freq)continue;          //若某字符出现次数等于最小频率
            cout<<s[i];                            //则将其跳过不输出
        }
        cout<<endl;
    }
}
```

### 24.合唱队

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210138252.png" alt="image-20220505210138252" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210152634.png" alt="image-20220505210152634" style="zoom:80%;" />

瞎写的居然过了，我都不知道为啥，打算求

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n;
    cin>>n;
    vector<int> nums;
    for(int i=0;i<n;i++){
        int a;
        cin>>a;
        nums.push_back(a);
    }
    vector<int> f(n,1);
    
    for(int i=1;i<n;i++){
        for(int j=0;j<i;j++){
            if(nums[i]>nums[j]) f[i] = max(f[i],1+f[j]);            
        }
    }
    
    for(int i=1;i<n;i++){
        for(int j=0;j<i;j++){
            if(nums[i]<nums[j]) f[i] = max(f[i],1+f[j]);            
        }
    }

    int res = 0;
    for(int i=0;i<n;i++)
        res = max(res,f[i]);
    cout<<n-res<<endl;
}
```

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n;
    cin>>n;
    vector<int> nums;
    for(int i=0;i<n;i++){
        int a;
        cin>>a;
        nums.push_back(a);
    }
    vector<int> f(n,1);
    vector<int> g(n,1);
    //求从左向右看的最长上升子序列
    for(int i=1;i<n;i++){
        for(int j=0;j<i;j++){
            if(nums[i]>nums[j]) f[i] = max(f[i],1+f[j]);            
        }
    }
    //求从右向左看的最长上升子序列
    for(int i=n-2;i>=0;i--){
        for(int j=n-2;j>i;j--){
            if(nums[i]>nums[j]) g[i] = max(g[i],1+g[j]);            
        }
    }

    int res = 0;
    for(int i=0;i<n;i++)
        res = max(res,f[i] + g[i] - 1);
    cout<<n-res<<endl;
}
```



### 25.数据分类处理

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210230404.png" alt="image-20220505210230404" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210248411.png" alt="image-20220505210248411" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210302155.png" alt="image-20220505210302155" style="zoom:80%;" />

```
```

### 26.字符串排序

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210637423.png" alt="image-20220505210637423" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
bool cmp(pair<char,int> a,pair<char,int> b){
    char cha = tolower(a.first);
    char chb = tolower(b.first);
    if(cha == chb)
        return a.second < b.second;
    return cha < chb;
}
int main(){
    string s;
    while(getline(cin,s)){
        vector<pair<char,int>> vec;
        for(int i = 0;i<s.size();++i)
            vec.emplace_back(s[i],i);
        vector<pair<char,int>> vec2(vec.begin(),vec.end());
        string t;
        sort(vec.begin(),vec.end(),cmp);
        for(int i=0;i<vec.size();i++)
            if(isalpha(vec[i].first)) t+=vec[i].first;
        int j = 0;
        for(int i=0;i<vec2.size();i++)
            if(isalpha(vec2[i].first)) {
                vec2[i].first = t[j];
                j++;
            }
        for(auto x:vec2)
            cout<<x.first;
    }

}
```

### 27.查找兄弟单词

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210710886.png" alt="image-20220505210710886" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210724235.png" alt="image-20220505210724235" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
#include <string> 
#include <algorithm>
using namespace std;
bool f(string s,string t){
    if(s!=t){
        sort(s.begin(),s.end());
        sort(t.begin(),t.end());
        if(s==t) return true;
    }
    return false;
}
int main(){
    int n;
    cin>>n;
    vector<string> vec;
    for(int i=0;i<n;i++){
        string t;
        cin>>t;
        vec.push_back(t);
    }
    string s;
    cin>>s;
    int k;
    cin>>k;
    vector<string> res;
    for(int i=0;i < vec.size();i++){
        if(f(s,vec[i])){
            res.push_back(vec[i]);
        }
    }
    if(res.size() == 0)cout<<0<<endl;
    else{
    cout<<res.size()<<endl;
    sort(res.begin(),res.end());
    if(k-1>=0 && k-1 <=res.size() - 1)
        cout<<res[k-1]<<endl;
    }
}
```

### 28.素数伴侣

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210800284.png" alt="image-20220505210800284" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210813259.png" alt="image-20220505210813259" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
vector<int> even;
vector<int> odd;
bool isprime(int num){
    for(int i = 2; i * i <= num; i++){ //遍历到根号num
        if(num % i == 0) //检查有无余数
            return false;
    }
    return true;
}
bool find(int num,vector<int>& even,vector<bool>& used,vector<int>& match){
    for(int i=0;i<even.size();i++){
        if(isprime(num + even[i]) && !used[i]){
            used[i] = true;
            if(match[i] == 0 || find(match[i],even,used,match)){
                match[i] = num;
                return true;
            }
        }
    }
    return false;
}
int main(){
    int n;
    cin>>n;
    for(int i = 0;i < n;i++){
        int a;
        cin >> a;
        if(a%2 == 0)
            even.push_back(a);
        else
            odd.push_back(a);
    }
    int count = 0;
    //记录每个偶数配对的是 哪一个奇数
    vector<int> match(even.size(),0);
    for(int i=0;i<odd.size();i++){
        vector<bool> used(even.size(),false);
        if(find(odd[i],even,used,match))
            count++;
    }
    
    cout<<count;
    
}
```

### 29.字符串加解密

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210853782.png" alt="image-20220505210853782" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
#include <string> 
#include <algorithm>
using namespace std;
int main(){
    string s;
    string t;
    while(getline(cin,s)&&getline(cin,t)){
        for(auto& c:s){
            if(c=='9')c='0';
            else if(c=='z') c='A';
            else if(c=='Z') c='a';
            else if(isdigit(c)) c = char(int(c) + 1);
            else if(islower(c)) c = toupper(char(int(c) + 1));
            else if(isupper(c)) c = tolower(char(int(c) + 1));
        }
        for(auto& c:t){
            if(c=='0')c='9';
            else if(c=='a') c='Z';
            else if(c=='A') c='z';
            else if(isdigit(c)) c = char(int(c) + -1);
            else if(islower(c)) c = toupper(char(int(c) - 1));
            else if(isupper(c)) c = tolower(char(int(c) - 1));
        }
        cout<<s<<endl;
        cout<<t<<endl;
    }
}
```

### 30.字符串合并处理

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210937276.png" alt="image-20220505210937276" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505210952162.png" alt="image-20220505210952162" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
void f(string& s){
    for(auto& c:s){
        if(c == '1')
            c = '8';
        else if(c == '2')
            c = '4';
        else if(c == '3')
            c = 'C';
        else if(c == '4')
            c = '2';
        else if(c == '5')
            c = 'A';
        else if(c == '7')
            c = 'E';
        else if(c == '8')
            c = '1';
        else if(tolower(c) == 'a')
            c = '5';
        else if(tolower(c) == 'b')
            c = 'D';
        else if(tolower(c) == 'c')
            c = '3';
        else if(tolower(c) == 'd')
            c = 'B';
        else if(tolower(c) == 'e')
            c = '7';  
        else if(tolower(c) == 'f')
            c = 'F';   
    }
}
int main(){
    string a;
    string b;
    cin >> a;
    cin >> b;
    
    string s = a + b;
    
    string s1;
    string s2;
    
    for(int i = 0;i < s.size();i++){
        if(i % 2 == 0)s1 += s[i];
        else s2 += s[i];
    }
    sort(s1.begin(),s1.end());
    sort(s2.begin(),s2.end());
    int n = s.size();
    s.clear();
    for(int i = 0;i < n;i++){
        if(i % 2 == 0)s += s1[i / 2];
        else s += s2[i / 2];
    }
    f(s);
    
    cout << s <<endl;
    
}
```





### 31.单词倒排

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220227172441758.png" alt="image-20220227172441758" style="zoom:80%;" />

```c++
#include <iostream>
#include <string>
#include <vector>
using namespace std;
int main(){
    string s;
    while(getline(cin,s)){
        string t;
        vector<string> vec;
        for(int i=0;i<s.size();i++){
            if(isalpha(s[i]))
                t+=s[i];
            else{
                vec.push_back(t);
                t="";
                }
        }
        vec.push_back(t);
        for(int i=vec.size()-1;i>=0;i--)
            cout<<vec[i]<<' ';
        cout<<endl;
    }
}
```

### 33.**整数与IP地址间的转换**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505211119784.png" alt="image-20220505211119784" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505211133563.png" alt="image-20220505211133563" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
unsigned long long  ip_to_in(string s){
    string t;
    vector<int> res; 
    for(auto c:s){
        if(c!='.')
            t+=c;
        else{
            res.push_back(stoi(t));
            t.clear();
        }
    }
    res.push_back(stoll(t));
    long long sum = 0;
    for(int i=0;i<res.size();i++)
        sum+=res[i]*pow(256,3-i);
    return sum;
}
string int_to_ip(long long n) {
	string s;
	s += to_string((n >> 24) & 0xff);
	s += ".";
	s += to_string((n >> 16) & 0xff);
	s += ".";
	s += to_string((n >> 8) & 0xff);
	s += ".";
	s += to_string((n) & 0xff);
	return s;
}
int main(){
    string s;
    cin>>s;
    long long n;
    cin>>n;
    cout<<ip_to_in(s)<<endl;
    cout<<int_to_ip(n)<<endl;
    
}
```

### 34.图片整理

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220222124204017.png" alt="image-20220222124204017" style="zoom:80%;" />

```c++
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;
int main(){
    string s;
    while(cin>>s){
        sort(s.begin(),s.end());
        cout<<s<<endl;
    }
}
```

### 35.蛇形矩阵

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220222215829663.png" alt="image-20220222215829663" style="zoom:80%;" />

```c++
#include <iostream>
using namespace std;
int main(){
    int n;
    while(cin>>n){
        for(int i=1;i<=n;i++){
            for(int j=1;j<=n-i+1;j++){
                cout<<(j+i-1)*(j+i)/2-(i-1)<<' ';
            }
            cout<<endl;
        }
    }
}
```

### 36.字符串加密

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505211214315.png" alt="image-20220505211214315" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
bool contain(char c,vector<char> vec){
    for(auto x:vec)
        if(c==x) return true;
    return false;
}
int main(){
    string t;
    string s;
    cin>>t>>s;
    vector<char> vec;
    for(auto x:t)
        if(!contain(x,vec)) vec.push_back(x);
    
    for(int i=0;i<26;i++){
        if(!contain(char(i+97),vec)) vec.push_back(char(i+97));
    }
    
    for(auto& c:s)
        c=vec[int(c)-97]; 
    cout<<s<<endl;
    
}
```

### 37.统计每个月兔子的总数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220227174242779.png" alt="image-20220227174242779" style="zoom:80%;" />

```c++
#include <iostream>
using namespace std;
int func(int n){
    if(n==1)return 1;
    if(n==2)return 1;
    return func(n-1)+func(n-2);
}
int main(){
    int n;
    while(cin>>n){
        cout<<func(n)<<endl;
    }
}
```

```c++
#include <iostream>
#include <vector>
using namespace std;
int func(int n){
    vector<int> vec(n+1,-1);
    vec[0]=1;
    vec[1]=1;
    for(int i=2;i<vec.size();i++)
        vec[i]=vec[i-1]+vec[i-2];
    return vec[n];
}
int main(){
    int n;
    while(cin>>n){
        cout<<func(n-1)<<endl;
    }
}
```

### 38.**求小球落地5次后所经历的路程和第5次反弹的高度**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505211251027.png" alt="image-20220505211251027" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n;
    cin>>n;
    double sum = 0;
    double h = n;
    for(int i=0;i<5;i++){
        sum += h;
        h /= double(2);
        if(i==4)break;
        sum += h;
    }
    cout<<fixed<<setprecision(6)<<sum<<endl;
    cout<<fixed<<setprecision(6)<<h<<endl; 
}
```

### 39.**判断两个IP是否属于同一子网**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505211332803.png" alt="image-20220505211332803" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505211353997.png" alt="image-20220505211353997" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505211412084.png" alt="image-20220505211412084" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
//ip to int
long long ip_to_int(string s){
    vector<int> vec;
    string t;
    for(auto x:s){
        if(x!='.')
            t+=x;
        else{
            vec.push_back(stoi(t));
            t.clear();
        }
    }
    vec.push_back(stoi(t));
    long long sum = 0;
    for(int i = 0;i<vec.size();i++)
        sum += vec[i]*pow(256,3-i);
    return sum;
}
//判断子网掩码是否合法
bool f2(string s){
    vector<int> vec;
    string t;
    for(auto x:s){
        if(x!='.')
            t+=x;
        else{
            vec.push_back(stoi(t));
            t.clear();
        }
    }
    vec.push_back(stoi(t));
    if(vec.size() != 4) return false;
    for(auto x:vec)
        if(x<0 || x>255) return false;
    
    unsigned int sum = 0;
    for(int i = 0;i<vec.size();i++)
        sum += vec[i]*pow(256,3-i);
    
    string bits = bitset<32>(sum).to_string();
    int flag = 0;
    for(int i = 0;i<bits.size()-1;i++)
        if(bits[i] != bits[i+1]) flag++;
    if(flag > 1) return false;
    
    return true;
} 
//判断是否合法
bool f1(string s){
    vector<int> vec;
    string t;
    for(auto x:s){
        if(x!='.')
            t+=x;
        else{
            vec.push_back(stoi(t));
            t.clear();
        }
    }
    vec.push_back(stoi(t));
    if(vec.size() != 4) return false;
    for(auto x:vec)
        if(x<0 || x>255) return false;
    return true;
}
int main(){
    string s;
    string s1;
    string s2;
    cin>>s>>s1>>s2;
    //判断是否合法
    //转换为整数
    
    if(!f1(s1) || !f1(s2) || !f2(s))
        cout<<1<<endl;
    else if((ip_to_int(s2) & ip_to_int(s)) == (ip_to_int(s1) & ip_to_int(s)) ){
        cout<<0<<endl;
    }
    else{
        cout<<2<<endl;
    }
}
```

### 40.统计字符

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220227174710659.png" alt="image-20220227174710659" style="zoom:80%;" />

```c++
#include <iostream>
#include <string>
using namespace std;
int main(){
    string s;
    while(getline(cin,s)){
        int a=0,b=0,c=0,d=0;
        for(char ch:s){
            if(isalpha(ch))
                a++;
            else if(ch==' ')
                b++;
            else if(isdigit(ch))
                c++;
            else
                d++;
        }
        cout<<a<<endl<<b<<endl<<c<<endl<<d<<endl;
    }
}
```

### 41.称砝码

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505211451052.png" alt="image-20220505211451052" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n;
    cin>>n;
    vector<int> w;
    vector<int> nums;
    for(int i=0;i<n;i++){
        int a;
        cin>>a;
        w.push_back(a);
    }
    int max = 0;
    for(int i=0;i<n;i++){
        int a;
        cin>>a;
        max+=w[i]*a;
        nums.push_back(a);
    }
    vector<bool> dp(max+1,false);
    dp[0] = true;
    for(int i=0;i<n;i++){
        for(int j=0;j<nums[i];j++){
            for(int k=max;k>=w[i];k--)
                if(dp[k-w[i]]==1)dp[k] = 1;
        }
    }
    int res = 0;
    for(int i=0;i<dp.size();i++)
        if(dp[i]==1) res++;
    cout<<res<<endl;
}
```

### 42.学英语

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505211518333.png" alt="image-20220505211518333" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505211529131.png" alt="image-20220505211529131" style="zoom: 80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
vector<string> ones = {"zero","one","two","three","four","five","six","seven","eight","nine"};
vector<string> twos = {"ten","eleven","twelve","thirteen","fourteen","fifteen","sixteen","seventeen","eighteen","nineteen"};
vector<string> twenties = {"zero","ten","twenty","thirty","forty","fifty","sixty","seventy","eighty","ninety"};
vector<string> hundreds = {"hundred","thousand","million","billion"};
int ihundreds[] = { (int)1e2, (int)1e3, (int)1e6, (int)1e9, (int)1e12 };
string f(long long n){
    if(n<=9) return ones[n];
    else if(n<=19) return twos[n%10];
    else if(n<100) return twenties[n/10] + (n%10==0?"":" "+ones[n%10]);
    else {
        for(int i=0;i<4;i++){
            if(n<ihundreds[i+1])
                return f(n/ihundreds[i]) + " " + hundreds[i] + 
                (n%ihundreds[i]?(i?" ":" and ") + f(n%ihundreds[i]):""); 
        }
    }
    return "";
}
int main(){
    long long n ;
    cin>>n;
    cout<<f(n)<<endl;
}
```

### 43.迷宫问题

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505211606552.png" alt="image-20220505211606552" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505211638459.png" alt="image-20220505211638459" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505211650146.png" alt="image-20220505211650146" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
vector<vector<int>> res;
int m,n;
vector<vector<int>> vec;
vector<vector<int>> res1;
void dfs(int x,int y){
    if(x<0||y<0||x>=m||y>=n||vec[x][y]==1) return;
    vec[x][y] = 1;
    res.push_back({x,y});
    if(x == m-1 && y == n-1){
        res1 = res;
        return;
    }

    dfs(x+1,y); 
    dfs(x-1,y);
    dfs(x,y+1);
    dfs(x,y-1);
    vec[x][y] = 0;
    res.pop_back();

}
int main(){
    cin>>m>>n;
    vec = vector<vector<int>>(m,vector<int>(n,0));
    for(int i=0;i<m;i++){
        for(int j=0;j<n;j++){ 
            int a;
            cin>>a;
            vec[i][j] = a;
        }
    }
    dfs(0,0);
    for(auto x:res1){
        cout<<'('<<x[0]<<','<<x[1]<<')'<<endl;
    }
    
}
```

### 44.Sudoku

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505211802924.png" alt="image-20220505211802924" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
vector<vector<int>> vec(9,vector<int>(9,0));
bool flag = false;
bool check(int n){
    int a = n/9;
    int b = n%9;
   
    for(int i=0;i<9;i++)
        if(i != a && vec[i][b] == vec[a][b]) return false;
    for(int j=0;j<9;j++)
        if(j != b && vec[a][j] == vec[a][b]) return false;
    for(int i=(a/3)*3;i<(a/3)*3+3;i++){
        for(int j=(b/3)*3;j<(b/3)*3+3;j++){
            if((i!=a || j!=b) &&(vec[i][j] == vec[a][b]))
                return false;
        }
    }
    return true;
}
void dfs(int n){
    if(n==81){
        for(auto x:vec){
            for(auto y:x){
                cout<<y<<' ';
            }
            cout<<endl;
        }
        flag = true;
        return;
    }
    int i = n/9;
    int j = n%9;
    
    if(vec[i][j] == 0){
        for(int k=1;k<=9;k++){
            vec[i][j] = k;
            if(check(n)){
                dfs(n+1);
                if(flag) return;
                vec[i][j] = 0;
            }
        }
        vec[i][j] = 0;
    }
    else{
        dfs(n+1);
    }
}

int main(){
    for(int i=0;i<9;i++){
        for(int j=0;j<9;j++){
            cin>>vec[i][j];
        }
    }
    dfs(0);
}
```

### 45.名字的漂亮度

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505211853954.png" alt="image-20220505211853954" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int contain(char c,vector<pair<char,int>> vec){
    for(int i=0;i<vec.size();i++)
        if(vec[i].first == c) return i;
    return -1;
}
bool cmp(pair<char,int> a,pair<char,int> b){
    return a.second> b.second;
}
int f(string s){
    vector<pair<char,int>> vec;
    for(auto c:s)
        if(contain(c,vec)!=-1)
            vec[contain(c,vec)].second++;
        else
            vec.emplace_back(c,1);
    sort(vec.begin(),vec.end(),cmp);
    unordered_map<char,int> map1;
    int i = 26;
    for(auto x:vec){
        map1[x.first]=i;
        i--;
    }
    
    int sum = 0;
    for(auto c:s)
        sum+=map1[c];
    return sum;
}
int main(){
    int n;
    cin>>n;
    vector<string> vec;
    string s;
    for(int i=0;i<n;i++){
        cin>>s;
        vec.push_back(s);
    }
    for(auto x:vec)
        cout<<f(x)<<endl;
}
```

### 46.截取字符串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220219203204775.png" alt="image-20220219203204775" style="zoom:80%;" />

```c++
#include <iostream>
#include <string>
using namespace std;
int main(){
    string s;
    int k;
    while(cin>>s){
        cin>>k;
        for(int i=0;i<k;i++)
            cout<<s[i];
        cout<<endl;
    }
}
```

```c++
#include <iostream>
#include <string>
using namespace std;
int main(){
    string s;
    int k;
    while(cin>>s>>k){
        cout<<s.substr(0,k)<<endl;
    }
}
```

### 48. **从单向链表中删除指定值的节点**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505212000788.png" alt="image-20220505212000788" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505212015749.png" alt="image-20220505212015749" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505212029254.png" alt="image-20220505212029254" style="zoom:80%;" />

```
```

### 50.四则运算

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505212108109.png" alt="image-20220505212108109" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int compute(string& s,int l,int r){
    char op = '+';
    int num = 0;
    vector<int> res;
    for(int i=l;i<=r;i++){
        if(isdigit(s[i]))
            num = num*10 + (s[i]-'0');
        if(s[i] == '(' || s[i] == '[' || s[i] == '{'){
            int cnt = 0;
            int j = i;
            while(j<=r){
                if(s[j] == '(' || s[j] == '[' || s[j] == '{')
                    cnt++;
                else if(s[j] == ')' || s[j] == ']' || s[j] == '}'){
                    cnt--;
                    if(cnt == 0)break;
                }
                j++;
            }
            num = compute(s,i+1,j-1);
            i = j + 1;
        }
        if(!isdigit(s[i]) || i == r){
            switch(op){ //根据运算符开始计算
                case '+': res.push_back(num); break; //加减法加入到末尾
                case '-': res.push_back(-num); break;
                case '*': res.back() *= num; break; //乘除法与末尾计算
                case '/': res.back() /= num; break;
            }
            op = s[i];
            num = 0;
        }
    }
    int t = 0;
    for(auto x:res)
        t+=x;
    return t;
}
int main(){
    string s;
    while(getline(cin,s)){
        cout<<compute(s,0,s.size()-1)<<endl;
    }
}
```

### 51.输出单向链表中倒数第k个结点

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220409164437343.png" alt="image-20220409164437343" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
struct ListNode
{
    int Key;
    ListNode* Next;
    ListNode(int key){Key = key;Next = nullptr;}
    ListNode(int key,ListNode* next){Key = key;Next = next;}
};
int main(){
    int n;
    while(cin>>n){
        vector<int> vec(n,0);
        int n0 = n;
        while(n>0)
        {
            int a;
            cin>>a;
            vec[vec.size()-n] = a;
            n--;
        }
        ListNode* head = new ListNode(vec[0]);
        ListNode* p = head;
        for(int i=1;i<n0;i++)
        {
            p->Next = new ListNode(vec[i]);
            p = p->Next;
        }
        p = head;
        int k;
        cin >> k;
        for(int i =0;i < n0-k ;++i)
        {
            p = p->Next;
        }
        cout<<p->Key<<endl;
    }
}
```

### 52.**计算字符串的编辑距离**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505212147890.png" alt="image-20220505212147890" style="zoom:80%;" />

```
```

### 53.杨辉三角的变形

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505212556187.png" alt="image-20220505212556187" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505212609706.png" alt="image-20220505212609706" style="zoom:80%;" />

```
```

### 54.表达式求值

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505212636976.png" alt="image-20220505212636976" style="zoom:80%;" />

````c++
#include <bits/stdc++.h>
using namespace std;
int compute(string& s,int l,int r){
    char op = '+';
    int num = 0;
    vector<int> res;
    for(int i=l;i<=r;i++){
        if(isdigit(s[i]))
            num = num*10 + (s[i]-'0');
        if(s[i] == '('){
            int cnt = 0;
            int j = i;
            while(j<=r){
                if(s[j]=='(')
                    cnt++;
                else if(s[j]==')'){
                    cnt--;
                    if(cnt == 0)break;
                }
                j++;
            }
            num = compute(s,i+1,j-1);
            i = j + 1;
        }
        if(!isdigit(s[i]) || i == r){
            switch(op){ //根据运算符开始计算
                case '+': res.push_back(num); break; //加减法加入到末尾
                case '-': res.push_back(-num); break;
                case '*': res.back() *= num; break; //乘除法与末尾计算
                case '/': res.back() /= num; break;
            }
            op = s[i];
            num = 0;
        }
    }
    int t = 0;
    for(auto x:res)
        t+=x;
    return t;
}
int main(){
    string s;
    while(getline(cin,s)){
        cout<<compute(s,0,s.size()-1)<<endl;
    }
}
````

### 55.挑7

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220507205708448.png" alt="image-20220507205708448" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n;
    cin>>n;
    vector<int> res;
    for(int i=1;i<=n;i++){
        if(i%7==0 || to_string(i).find('7') < n )
            res.push_back(i);
    }
    cout<<res.size()<<endl;
}
```

### 56.完全数计算

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505105826956.png" alt="image-20220505105826956" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n;
    cin>>n;
    vector<int> res;
    for(int i=2;i<=n;i++){
        vector<int> vec;
        for(int j=1;j<=i/2;j++){
            if(i%j==0)vec.push_back(j);
        }
        int sum = 0;
        for(auto x:vec)
            sum += x;
        if(sum==i)
            res.push_back(i);
    }
    cout<<res.size()<<endl;
}
```

### 57.高精度整数加法

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    string s;
    string t;
    cin>>s;
    cin>>t;
    int sn = s.size();
    int tn = t.size();
    if(sn>tn){
        for(int i=0;i<sn-tn;i++)
            t = "0" + t;
    }
    else if(tn>sn){
        for(int i=0;i<tn-sn;i++)
            s = "0" + s;
    }
    int cnt = 0;
    int num = 0;
    string res;
    for(int i=s.size() - 1;i>=0;i--){
        num = cnt + stoi(to_string(int(s[i]) - 48)) + stoi(to_string(int(t[i]) - 48));
        cnt = num - 10;
        if(cnt < 0){
            res = to_string(num) + res;
            cnt = 0;
        }
        else{
            res = to_string(num - 10) + res;
            cnt = 1;
        }
    }
    if(cnt!=0)
        res = '1' + res;
    cout<<res<<endl;
}
```

### 58.输入n个整数，输出其中最小的k个

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220219204052522.png" alt="image-20220219204052522" style="zoom:80%;" />

```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
int main(){
    int n,k;
    vector<int> vec;
    while(cin>>n>>k){
        for(int i=0;i<n;i++){
            int a;
            cin>>a;
            vec.push_back(a);
        }
        sort(vec.begin(),vec.end());
        for(int i=0;i<k;i++)
            cout<<vec[i]<<' ';
        cout<<endl;
        vec.clear();
    }
    
}
```

### 59.**找出字符串中第一个只出现一次的字符**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220507184914591.png" alt="image-20220507184914591" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int contain(char c,vector<pair<char,int>> v){
    for(int i=0;i<v.size();i++){
        if(v[i].first == c) return i;
    }
    return -1;
}
int main(){
    string s;
    cin>>s;
    vector<pair<char,int>> v;
    for(auto x:s){
        if(contain(x,v) != -1)
            v[contain(x,v)].second++;
        else
            v.emplace_back(x,1);
    }
    int i = 0;
    for(i;i<v.size();i++)
        if(v[i].second == 1){
            cout<<v[i].first;
            break;
        }
    if(i == v.size())
        cout<< -1 <<endl;
}
```

### 101.输入整型数组和排序标识，对其元素按照升序或降序进行排序

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220219204640895.png" alt="image-20220219204640895" style="zoom:80%;" />

```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
int main(){
    int n,a;
    vector<int> vec;
    while(cin>>n){
        for(int i=0;i<n;i++){
            int a;
            cin>>a;
            vec.push_back(a);
        }
        sort(vec.begin(),vec.end());
        cin>>a;
        if(a)
            reverse(vec.begin(),vec.end());
        for(auto a:vec)
            cout<<a<<' ';
    }
}
```











### 60.查找组成一个偶数最接近的两个素数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505110546256.png" alt="image-20220505110546256" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
bool f(int x){
    if(x==1)return false;
    int count = 0;
    for(int i=2;i<=x/2;i++){
        if(x%i==0) count++;
    }
    return count==0;
}
int main(){
    int n;
    cin>>n;
    int i;
    for(i=n/2;i>1;i--){
        if(f(i) && f(n-i))break;
    }
    cout<<i<<endl;
    cout<<(n-i)<<endl;
}
```

### 61.放苹果

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505215557382.png" alt="image-20220505215557382" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int f(int m,int n){
    if(m<0||n<0) 
        return 0;
    if(m == 1 || n == 1)
        return 1;
    return f(m,n-1) + f(m - n,n);
}
int main(){
    int m,n;
    cin>>m>>n;
    cout<<f(m,n)<<endl;
}
```

### 62.二进制中1的个数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505111459080.png" alt="image-20220505111459080" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n;
    while(cin>>n){
        int count = 0;
        while(n!=0){
            n&=(n-1);
            count++;
        }
        cout<<count<<endl;
    }
}
```

### 63.DNA序列

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505215508228.png" alt="image-20220505215508228" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505215518101.png" alt="image-20220505215518101" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int f(string s){
    int cnt = 0;
    for(auto x:s)
        if(x=='C'||x=='G')cnt++;
    return cnt;
}
int main(){
    string s;
    int n;
    cin>>s;
    cin>>n;
    int index = 0;
    int maxv = 0;
    for(int i=0;i+n<s.size();i++){
        if(f(s.substr(i,n)) > maxv){
            maxv = f(s.substr(i,n));
            index = i;
        }
    }
    cout<<s.substr(index,n);
}
```

### 64.**MP3光标位置**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505215414935.png" alt="image-20220505215414935" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505215431538.png" alt="image-20220505215431538" style="zoom:80%;" />

```
```



### 65.**查找两个字符串a,b中的最长公共子串**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505215334425.png" alt="image-20220505215334425" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    string s;
    string t;
    cin>>s>>t;
    if(s.size()>t.size())
        swap(s,t);
    int m = s.size();
    int n = t.size();
    vector<vector<int>> dp(m+1,vector<int>(n+1,0));
    int maxl = 0;
    int end = 0;
    for(int i = 1;i <= m;i++){
        for(int j = 1;j <=n ;j++){
            if(s[i-1] == t[j-1])dp[i][j] = dp[i-1][j-1] + 1;
            if(dp[i][j] > maxl){
                maxl = dp[i][j];
                end = i - 1;
            }
        }
    }
    cout<<s.substr(end-maxl+1,maxl); 
}
```







### 66.配置文件恢复

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505215220769.png" alt="image-20220505215220769" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505215243595.png" alt="image-20220505215243595" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505215300697.png" alt="image-20220505215300697" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
string a1 = "reset";
string a2 = "reset what";
string b1 = "reset board";
string b2 = "board fault";
string c1 = "board add";
string c2 = "where to add";
string d1 = "board delete";
string d2 = "no board at all";
string e1 = "reboot backplane";
string e2 = "impossible";
string f1 = "backplane abort";
string f2 = "install first";
bool f(vector<string> a,vector<string> b){
    for(int i=0;i<a.size();i++){
        for(int j=0;j<a[i].size();j++){
            if(a[i][j]!=b[i][j])
                return false;
        }
    }
    return true;
}
int main(){
    unordered_map<string,vector<string>> map1;
    map1[a1] = {"reset"};
    map1[b1] = {"reset","board"};
    map1[c1] = {"board", "add"};
    map1[d1] = {"board","delete"};
    map1[e1] = {"reboot", "backplane"};
    map1[f1] = {"backplane","abort"};
    unordered_map<string,string> map2;
    map2[a1] = a2;
    map2[b1] = b2;
    map2[c1] = c2;
    map2[d1] = d2;
    map2[e1] = e2;
    map2[f1] = f2;
    string s;
    while(getline(cin,s)){
        vector<string> vec;
        string t;
        for(auto x:s){
            if(x!=' ')
                t += x;
            else{
                if(t.size()>0){
                    vec.push_back(t);
                    t.clear();
                }
            }
        }
        if(t.size()>0){
            vec.push_back(t);
            t.clear();
        }
        //先判断size是否相等，若不等返回false
        //再判断是否为前缀，若不是返回false
        //返回匹配的个数 若等于一则成功，否则返回false
        vector<string> res;
        for(auto it=map1.begin();it!=map1.end();it++){
            if(vec.size() == (*it).second.size() ){
                if(f(vec,(*it).second))
                    res.push_back(map2[(*it).first]);
            }
        }
        if(res.size() != 1)
            cout<<"unknown command"<<endl;
        else{
            cout<<res[0]<<endl;
        }
        
    }
}
```





### 67.**24点游戏算法**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505215151759.png" alt="image-20220505215151759" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
bool f(vector<double>& v){
    if(v.size() == 1) return abs(v[0]-24)<1e-10;
    for(double num:v){
        double a = v[0];
        v.erase(v.begin());
        for(double num:v){
            double b = v[0];
            v.erase(v.begin());
            for(double n:{a+b,a-b,a*b}){
                v.push_back(n);
                if(f(v)) return true;
                v.pop_back();
            }
            if(b!=0){
                v.push_back(a/b);
                if(f(v)) return true;
                v.pop_back();
            }
            v.push_back(b);
        }
        v.push_back(a);
    }
    return false;
}
int main(){
    vector<double> vec(4,0);
    for(int i=0;i<4;i++){
        double a;
        cin>>a;
        vec[i] = double(a);
    }
    if(f(vec)) cout<<"true"<<endl;
    else cout<<"false"<<endl;
}
```

### 68.成绩排序

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505215057668.png" alt="image-20220505215057668" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505215112258.png" alt="image-20220505215112258" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
bool cmp1(pair<pair<string,int>,int> a,pair<pair<string,int>,int> b){
    if(a.first.second == b.first.second)
        return a.second < b.second;
    return a.first.second > b.first.second;
}
bool cmp2(pair<pair<string,int>,int> a,pair<pair<string,int>,int> b){
    if(a.first.second == b.first.second)
        return a.second < b.second;
    return a.first.second < b.first.second;
}
int main(){
    int n;
    cin>>n;
    int f;
    cin>>f;
    vector<pair<pair<string,int>,int>> vec;
    for(int i=0;i<n;i++){
        string s;
        cin>>s;
        int n;
        cin>>n;
        vec.emplace_back(make_pair(s,n),i);
    }
    if(f == 0)
        sort(vec.begin(),vec.end(),cmp1);
    else 
        sort(vec.begin(),vec.end(),cmp2);
    for(auto x:vec)
        cout<<x.first.first<<' '<<x.first.second<<endl;
}
```

### 69.**矩阵乘法**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505215001190.png" alt="image-20220505215001190" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505215022869.png" alt="image-20220505215022869" style="zoom: 80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
vector<vector<int>> a;
vector<vector<int>> b;
int x,y,z;
int main(){
    cin>>x>>y>>z;
    for(int i=0;i<x;i++){
        a.push_back({});
        for(int j=0;j<y;j++){
            int t;cin>>t;a[i].push_back(t);
        }
    }
    for(int i=0;i<y;i++){
        b.push_back({});
        for(int j=0;j<z;j++){
            int t;cin>>t;b[i].push_back(t);
        }
    }
    vector<vector<int>> res(x,vector<int>(z,0));
    for(int i=0;i<x;i++){
        for(int j=0;j<z;j++){
            for(int k=0;k< y;k++)
            res[i][j] += a[i][k] * b[k][j];
        }
    }
    for(auto x:res){
        for(auto y:x){
            cout<<y<<' ';
        }
        cout<<endl;
    }
}
```

### 70.矩阵乘法计算量估算

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505214933604.png" alt="image-20220505214933604" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
unordered_map<char,vector<int>> map1;
stack<vector<int>> stk;
int main(){
    int n;
    cin>>n;
    vector<vector<int>> vec(n,vector<int>(2,0));
    for(int i=0;i<n;i++){
        cin>>vec[i][0];
        cin>>vec[i][1];
    }
    string s;
    cin>>s;
    int i = 0;
    for(auto x:s)
        if(isalpha(x)){
            map1[x] = vec[i];
            i++;
        }
    int res = 0;
    for(int i=0;i<s.size();i++){
        if(s[i] == ')'){
            auto x = stk.top();
            stk.pop();
            auto y = stk.top();
            stk.pop();
            res += x[0] * x[1] * y[0];
            auto xxx = {y[0],x[1]};
            stk.push(xxx); 
        }
        else if(isalpha(s[i])){
            stk.push(map1[s[i]]);
        }
    }
    cout<<res<<endl;
   
}
```

### 71.字符串通配符

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505214658631.png" alt="image-20220505214658631" style="zoom:80%;" />



<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505214712559.png" alt="image-20220505214712559" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
bool isMatch(string s,string p){
    int sn = s.size();
    int pn = p.size();
    vector<vector<bool>> dp(sn+1,vector<bool>(pn+1,false));
    //dp[i][j]表示s的前i个字符和p的前j个字符是否匹配。
    dp[0][0] = true;
    //如果p.size() == 0 s.size() > 0 肯定不匹配
    //dp[j][0] = false
    //如果s.size() == 0 p.size() > 0 肯定不匹配，只能是p全为*
    for(int j=1;j<=pn;j++)
        if(p[j-1] == '*') dp[0][j] = dp[0][j-1];
    //
    for(int i=1;i<=sn;i++){
        for(int j=1;j<=pn;j++){
            if(p[j-1] == '*')
                dp[i][j] = dp[i][j-1] || dp[i-1][j];// ab和ab*  abc 和 a*
            else{
                if(tolower(s[i-1]) == tolower(p[j-1]))
                    dp[i][j] = dp[i-1][j-1];
                else if(p[j-1] == '?' &&( isalnum(s[i-1]) || s[i-1]=='.' ))
                    dp[i][j] = dp[i-1][j-1];
            }
        }
    }
    return dp[sn][pn];
}
int main(){
    string s;
    string p;
    cin>>p;
    cin>>s;
    if(isMatch(s,p))cout<<"true"<<endl;
    else cout<<"false"<<endl;
}
```

### 72.百钱买百鸡问题

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505115038505.png" alt="image-20220505115038505" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int x,y,z;
    for(x=0;5*x<=100;x++){
        for(y=0;3*y<=100;y++){
            if((100-x-y)%3==0 && 5*x+3*y+(100-x-y)/3 == 100)
                    cout<<x<<' '<<y<<' '<<100-x-y<<endl;
        }
    }
}
```

### 73.**计算日期到天数转换**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505214548878.png" alt="image-20220505214548878" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int a,b,c;
    string s;
    while(getline(cin,s)){
        string t;
        int cnt = 0;
        for(auto c:s){
            if(c!=' ')
                t+=c;
            else{
                if(cnt == 0){
                    a = stoi(t);
                    t.clear();
                }
                if(cnt == 1){
                    b = stoi(t);
                    t.clear();
                }
                cnt++;
            }
        }
        c = stoi(t);
        int res = 0;
        if((a%100!=0&&a%4==0)||(a%400==0)){
            for(int i=1;i<=b - 1;i++){
				if (i == 1)res += 31;
				else if (i == 2)res += 29;
				else if (i == 3)res += 31;
				else if (i == 4)res += 30;
				else if (i == 5)res += 31;
				else if (i == 6)res += 30;
				else if (i == 7)res += 31;
				else if (i == 8)res += 31;
				else if (i == 9)res += 30;
				else if (i == 10)res += 31;
				else if (i == 11)res += 30;
				else if (i == 12)res += 31;
            }
            res+=c;
        }
        else{
            for(int i=1;i<=b - 1;i++){
				if (i == 1)res += 31;
				else if (i == 2)res += 28;
				else if (i == 3)res += 31;
				else if (i == 4)res += 30;
				else if (i == 5)res += 31;
				else if (i == 6)res += 30;
				else if (i == 7)res += 31;
				else if (i == 8)res += 31;
				else if (i == 9)res += 30;
				else if (i == 10)res += 31;
				else if (i == 11)res += 30;
				else if (i == 12)res += 31;
            }
            res+=c;
        }
        
        cout<<res;      
    }
}
```

### 74.参数解析

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505214504803.png" alt="image-20220505214504803" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505214518561.png" alt="image-20220505214518561" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
vector<string> res;
void f1(string& s){
    for(int i=0;i<s.size();i++)
        if(s[i]=='"')s.erase(i,1);
}
void f(string s){
    string t;
    for(int i=0;i<s.size();i++){
        if(s[i]=='"'){
            i++;
            while(s[i]!='"'){
                t+=s[i];
                i++;
            }
            res.push_back(t);
            t.clear();
            i++;
        }
        else if(s[i] != ' '){
            t+=s[i];
        }
        else if(s[i] == ' '){
            if(t.size()>0){
                res.push_back(t);
                t.clear();
            }
        }
    }
    if(t.size() > 0){
        res.push_back(t);
        t.clear();
    }
    cout<<res.size()<<endl;
    for(auto& x:res){
        f1(x);
        cout<<x<<endl;
    }
}
int main(){
    string s;
    getline(cin,s);
    f(s);
}
```



### 75.公共子串计算

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505214421111.png" alt="image-20220505214421111" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int f(string s,string t){
    int m = s.size();
    int n = t.size();
    vector<vector<int>> dp(m+1,vector<int>(n+1,0));
    //dp[i][j]表示s的前i个字符和t的前j个字符 的最长公共子串的长度
    int maxlen = 0;
    for(int i=1;i<=m;i++){
        for(int j = 1;j <= n;j++){
            if(s[i-1]==t[j-1])
                dp[i][j] = dp[i-1][j-1] + 1;
            maxlen = max(maxlen,dp[i][j]);
        }
    }
    return maxlen;
}
int main(){
    string s;
    string t;
    cin>>s;
    cin>>t;
    cout<<f(s,t);
}
```





### 76.尼科彻斯定理

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505113202970.png" alt="image-20220505113202970" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n;
    cin>>n;
    int s = pow(n,3);
    int t = s/n;
    if(n%2==0){
        for(int i=1;i<=n;i++){
            if(i==n) cout<<(t-2*(n/2)+1)+2*(i-1);
            else cout<<(t-2*(n/2)+1)+2*(i-1)<<"+";
        }
    }
    else{
        for(int i=1;i<=n;i++){
            if(i==n)cout<<(t-2*(n/2))+2*(i-1);
            else cout<<(t-2*(n/2))+2*(i-1)<<"+";
        }
    }
}
```



### 77.火车进站

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505214329646.png" alt="image-20220505214329646" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505214340651.png" alt="image-20220505214340651" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
vector<int> in;
vector<int> out;
stack<int> stk;
vector<vector<int>> res;
void dfs(int i){
    if(out.size() == in.size()){
        res.push_back(out);
        return;
    }
    //进站
    if(i<in.size()){
        stk.push(in[i]);
        dfs(i+1);
        stk.pop();
    }
    //出站
    if(!stk.empty()){
        out.push_back(stk.top());
        stk.pop();
        dfs(i);
        stk.push(out.back());
        out.pop_back();
    }
}
int main(){
    int n;
    cin>>n;
    for(int i=0;i<n;i++){
        int a;
        cin>>a;
        in.push_back(a);
    }
    dfs(0);
    sort(res.begin(),res.end());
    for(auto x:res){
        fr(auto y:x){
            cout<<y<<' ';
        }
        cout<<endl;
    }
}
```

### 80.整型数组合并

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505112049080.png" alt="image-20220505112049080" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n,m;
    int a;
    set<int> set1;
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>a;
        set1.insert(a);
    }
    cin>>m;
    for(int i=0;i<m;i++){
        cin>>a;
        set1.insert(a);
    }
    for(auto it=set1.begin();it!=set1.end();it++){
        cout<<(*it);       
    }
    
}
```

### 81.字符串字符匹配

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505214244742.png" alt="image-20220505214244742" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
bool f(string& s,string& t){
    set<char> set1;
    set<char> set2;
    for(auto c:s)
        set1.insert(c);
    for(auto c:t)
        set2.insert(c);
    for(auto c:set1)
        if(!set2.count(c)) return false;
    return true;
}
int main(){
    string s1,s2;
    cin>>s1>>s2;
    if(f(s1,s2))cout<<"true"<<endl;
    else cout<<"false"<<endl;
}
```

### 82.**将真分数分解为埃及分数**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505214132225.png" alt="image-20220505214132225" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220507105938706.png" alt="image-20220507105938706" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
vector<string> res;
void f(long long a,long long b){
    if(b % a==0) {
        res.push_back(to_string(1)+"/"+to_string(b/a));
        return;
    }
    
    int p = b/a;
    int r = b%a;
    
    res.push_back(to_string(1)+"/"+to_string(p + 1));
    a = a - r;
    b = b * (p+1);
    f(a,b);
}
int main(){
    string s;
    while(cin>>s){
        res.clear();
        int index = s.find('/');
        long long a = stoi(s.substr(0,index));
        long long b = stoi(s.substr(index + 1));
        f(a,b);
        for(int i=0;i<res.size();i++){
            if(i==res.size()-1)
                cout<<res[i];
            else
                cout<<res[i]<<"+";
        }
    }
}
```

### 83.二维数组操作

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505214009425.png" alt="image-20220505214009425" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505214026765.png" alt="image-20220505214026765" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505214045811.png" alt="image-20220505214045811" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505214101002.png" alt="image-20220505214101002" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int m,n;
    while(cin>>m>>n){
        if(m>=1&&m<=9&&n>=1&&n<=9)cout<< 0 <<endl;
        else cout<< -1 <<endl;
        
        int x1,y1,x2,y2;
        cin>>x1>>y1>>x2>>y2;
        if(x1>=0 && x1<m && x2>=0 && x2<m &&
           y1>=0 && y1<n && y2>=0 && y2<n)cout<< 0 <<endl;
        else cout<< -1 <<endl;
        
        int d1;
        cin>>d1;
        if(d1 < 0|| d1 >= m  || m == 9)cout<< -1 <<endl;
        else cout<< 0 <<endl;
        
        int d2;
        cin>>d2;
        if(d2 < 0|| d2 >= n  || n == 9)cout<< -1 <<endl;
        else cout<< 0 <<endl;
        
        int x3,y3;
        cin>>x3>>y3;
        if(x3 < 0 || x3 >=m || y3 < 0 || y3 >= n)cout<< -1 <<endl;
        else cout<< 0 <<endl;
    }
}
```

### 84.**统计大写字母个数**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213850994.png" alt="image-20220505213850994" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    string s;
    getline(cin,s);
    int cnt = 0;
    for(auto c:s)
        if(isupper(c)) cnt++;
    cout<<cnt;
}
```

### 85.**最长回文子串**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213823596.png" alt="image-20220505213823596" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
string add(string& s) {
    string t = s;
    s.clear();
    s += '*';
    for (int i = 0; i < t.size(); i++) {
        s += t[i];
        s += "*";
    }
    return s;
}   
vector<int> manacher(vector<int>& p, string& s) {
    p.resize(s.size());
    int max_r = 0, mid = 0;
    for (int i = 0; i < s.size(); i++) {
        if (i < max_r)
            p[i] = min(p[2 * mid - i], max_r - i);
        else
            p[i] = 1;
        while (i + p[i] < s.size() && i - p[i] >= 0 && s[i + p[i]] == s[i - p[i]])
            p[i]++;
        if (i + p[i] > max_r) {
            max_r = i + p[i];
            mid = i;
        }   
    }
    return p;
}
int longestPalindrome(string s) {
    string t = s;
    s = add(s);
    vector<int> p;
    p = manacher(p,s);//p[i]是处理后的字符串的索引i位置对应的回文半径
    int index = 0;
    int max = INT_MIN;
    for(int i=0;i<p.size();i++){
        if(p[i]>max)
            max = p[i],index = i;
    }
    return max - 1;
}
int main(){
    string s;
    cin>>s;
    cout<<longestPalindrome(s)<<endl;
}
```

### 86.求最大连续bits数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220504122422455.png" alt="image-20220504122422455" style="zoom:80%;" />

位运算

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n;
    cin>>n;
    int cnt = 0;
    while(n!=0){
        n = (n & n<<1);
        cnt++;
    }
    cout<<cnt;
}
```

除法

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n;
    cin>>n;
    int count = 0;
    int maxcount = 0;
    while(n!=0){
        if(n%2==1)count++;
        else{
            maxcount=max(maxcount,count);
            count=0;
        }
        n/=2;
    }
    maxcount=max(maxcount,count);
    cout<<maxcount<<endl;
}
```



### 88.**扑克牌大小**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213710426.png" alt="image-20220505213710426" style="zoom: 80%;" />

```

```

### 87.密码强度等级

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220504120751550.png" alt="image-20220504120751550" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220504120807219.png" alt="image-20220504120807219" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220504120825705.png" alt="image-20220504120825705" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
bool is_fuhao(char c){
    int nc = int(c);
    if((nc<=0x2f && nc>=0x21)||
      (nc<=0x40 && nc>=0x3a)||
      (nc<=0x60 && nc>=0x5b)||
      (nc<=0x7e && nc>=0x7b))
        return true;
    return false;
}
int f1(string s){
    int n = s.size();
    if(n<=4)return 5;
    if(n<=7&&n>=5)return 10;
    if(n>=8)return 25;
    return 0;
}
int f2(string s){
    int count1=0;
    for(auto c:s)
        if(isalpha(c))count1++;
    int count2=0;
    for(auto c:s)
        if(islower(c))count2++;
    int count3=0;
    for(auto c:s)
        if(isupper(c))count3++;
    if(count1==0)return 0;
    if(count1==count2) return 10;
    if(count1==count3) return 10;
    return 20;
}
int f3(string s){
    int count=0;
    for(auto c:s)
        if(isdigit(c))count++;
    if(count==0)return 0;
    return count==1?10:20;
}
int f4(string s){
    int count=0;
    for(auto c:s)
        if(is_fuhao(c))count++;
    if(count==0) return 0;
    if(count==1) return 10;
    return 25;
}
int f5(string s){
    if(f2(s)==10 && f3(s)>0 && f4(s)==0)return 2;
    if(f2(s)==10 && f3(s)>0 && f4(s)>0)return 3;
    if(f2(s)==20 && f3(s)>0 && f4(s)>0)return 5;
    return 0;
}
int main(){
    string s;
    getline(cin,s);
    int f = f1(s)+f2(s)+f3(s)+f4(s)+f5(s);
    if(f>=90)cout<<"VERY_SECURE"<<endl;
    else if(f>=80)cout<<"SECURE"<<endl;
    else if(f>=70)cout<<"VERY_STRONG"<<endl;
    else if(f>=60)cout<<"STRONG"<<endl;
    else if(f>=50)cout<<"AVERAGE"<<endl;
    else if(f>=25)cout<<"WEAK"<<endl;
    else if(f>=0)cout<<"VERY_WEAK"<<endl;
    
}
```

### 89.24点运算

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213601830.png" alt="image-20220505213601830" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213626734.png" alt="image-20220505213626734" style="zoom:80%;" />

```
```



### 90.合法IP

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213523340.png" alt="image-20220505213523340" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std; 
bool f(vector<string> res){
    
    if(res.size()!=4) return false;
        
    for(auto x:res){
        for(int i = 0;i<x.size();i++){
            if(!isdigit(x[i]))
                return false;
            if(x.size()>1 && i==0 && x[i] == '0')
                return false;
        }
    }
    for(auto x:res)
        if(stoi(x)<0||stoi(x)>255) return false;
    
    return true;
}
int main(){
    string s;
    cin>>s;
    vector<string> res;
    string t;
    for(auto x:s){
        if(x!='.'){
            t+=x;
        }
        else{
            if(t.size()!=0){
                res.push_back(t);
                t.clear();
            }
        }
    }
    if(t.size()!=0){
        res.push_back(t);
        t.clear();
    }
 
    
    if(!f(res)) cout<<"NO"<<endl;
    else cout<<"YES"<<endl;
    
}
```

### 91.走方格的方案数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220504112739187.png" alt="image-20220504112739187" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int m,n;
    cin>>m>>n;
    vector<vector<int>> dp(m+1,vector<int>(n+1,0));
    for(int i=0;i<=m;i++)
        dp[i][0]=1;
    for(int j=0;j<=n;j++)
        dp[0][j]=1;
    for(int i=1;i<=m;i++){
        for(int j=1;j<=n;j++)
            dp[i][j]=dp[i-1][j]+dp[i][j-1];
    }
    cout<<dp[m][n];
}
```

### 92.**在字符串中找出连续最长的数字串**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213502966.png" alt="image-20220505213502966" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    string s;
    cin>>s;
    vector<string> res;
    int max_len = 0;
    string t;
    for(int i=0;i<s.size();i++){
        if(isdigit(s[i]))
            t+=s[i];
        else if(!isdigit(s[i]) && t.size()>0){
            res.push_back(t);
            if(t.size()>max_len){
                max_len = max(max_len,(int)t.size());
            }
            t.clear();
        }
    }
    if(t.size()>0)
        res.push_back(t);
    max_len = max(max_len,(int)t.size());
    
    for(int i=0;i<res.size();i++){
        if(res[i].size() == max_len)
            cout<<res[i];
    }
    cout<<','<<max_len<<endl;
}
```

### 93.数组分组

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213423062.png" alt="image-20220505213423062" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213433774.png" alt="image-20220505213433774" style="zoom:80%;" />

```
```













### 94.计票统计

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220504111535593.png" alt="image-20220504111535593" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int contain(string s,vector<pair<string,int>> a){
    int index=-1;
    for(int i=0;i<a.size();i++)
        if(a[i].first==s)
            index=i;
    return index;
}
int main(){
    string s;
    int n,m;
    vector<pair<string,int>> a;
    vector<string> b;
    for(int i=0;i<4;i++){
        getline(cin,s);
        if(i==0)n=stoi(s);
        if(i==1){
            string t;
            for(auto c:s){
                if(isalpha(c))
                    t+=c;
                else{
                    a.emplace_back(t,0);
                    t.clear();
                }
            }
            a.emplace_back(t,0);
        }
        if(i==2)m=stoi(s);
        if(i==3){
            string t;
            for(auto c:s){
                if(isalpha(c))
                    t+=c;
                else{
                    b.push_back(t);
                    t.clear();
                }
            }
            b.push_back(t);
        }
    }
    int count=0;
    for(int i=0;i<b.size();i++){
        if(contain(b[i],a)>=0){
            a[contain(b[i],a)].second++;
            count++;
        }
    }
    for(auto x:a)
        cout<<x.first<<" : "<<x.second<<endl;
    cout<<"Invalid : "<<m-count<<endl;
     
}
```

### 95.人民币转换

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213343681.png" alt="image-20220505213343681" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213353163.png" alt="image-20220505213353163" style="zoom:80%;" />

```

```

### 96.表示数字

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220504105139147.png" alt="image-20220504105139147" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    string s;
    getline(cin,s);
    for(int i=0;i<s.size();i++){
        if(isdigit(s[i])){
            s.insert(i,"*");
            i++;
            while(isdigit(s[i]))
                i++;
            s.insert(i,"*");
        }
    }
    cout<<s<<endl;
}
```

### 97.记负均正

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220504103638133.png" alt="image-20220504103638133" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n;
    cin>>n;
    double result = 0;
    int count = 0;
    int cnt = 0;
    for(int i=0;i<n;i++){
        int x;
        cin>>x;
        if(x<0)count++;
        if(x>0){
            cnt++;
            result+=x;
        }
    }
    cout<<count<<' ';
    if(cnt>0)
        cout<<fixed<<setprecision(1)<<(result/cnt)<<endl;
    else
        cout<<fixed<<setprecision(1)<<double(0)<<endl;
}
```

### **98.** **自动售货系统**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213005555.png" alt="image-20220505213005555" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213018685.png" alt="image-20220505213018685" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213035421.png" alt="image-20220505213035421" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213053676.png" alt="image-20220505213053676" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213112702.png" alt="image-20220505213112702" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213131072.png" alt="image-20220505213131072" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213150291.png" alt="image-20220505213150291" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505213202828.png" alt="image-20220505213202828" style="zoom:80%;" />

```

```

### 99.自守数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220504102742748.png" alt="image-20220504102742748" style="zoom:80%;" />

```
#include <bits/stdc++.h>
using namespace std;
bool f(int n){
    int m = n*n;
    string a=to_string(n);
    reverse(a.begin(),a.end());
    string b=to_string(m);
    string res;
    for(int i=b.size()-1;i>=0;i--){
        res+=b[i];
        if(res==a)return true;
    }
    return false;
}
int main(){
    int n;
    cin>>n;
    vector<int> res;
    for(int i=0;i<=n;i++){
        if(f(i)) res.push_back(i);
    }
    cout<<res.size()<<endl;
}
```

### 100.等差数列

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n;
    cin>>n;
    int a=2;
    int sum = 0;
    for(int i=0;i<n;i++){
        sum+=a;
        a+=3;
    }
    cout<<sum;
}
```

### 102.字符统计

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220504093958796.png" alt="image-20220504093958796" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
bool cmp(vector<int>& a,vector<int>& b){
    if(a[1]==b[1])return a[0]<b[0];
    else return a[1]>b[1];
}
int main(){
    string s;
    cin>>s;
    unordered_map<char,int> map;
    for(int i=0;i<s.size();i++){
        map[s[i]]++;
    }
    vector<vector<int>> vec;
    for(auto it=map.begin();it!=map.end();it++){
        vec.push_back({(*it).first,(*it).second});
    }
    sort(vec.begin(),vec.end(),cmp);
    string res;
    for(int i=0;i<vec.size();i++)
        res+=vec[i][0];
    cout<<res;
}
```

### 103.**Redraiment的走法**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220507103211787.png" alt="image-20220507103211787" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int f(vector<int> nums){
    int res = 0;
    vector<int> dp(nums.size(),1);
    for(int i=0;i<nums.size();i++){
        for(int j=0;j<i;j++){
            if(nums[i] > nums[j]){
                dp[i] = max(dp[i],1+dp[j]);
            }
            res = max(res,dp[i]);
        }
    } 
    return res;
}
int main(){
    int n;
    cin>>n;
    vector<int> res(n);
    for(int i=0;i<n;i++)
        cin>>res[i];
    cout<<f(res)<<endl; 
}
```



### 105.**记负均正II**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505212903762.png" alt="image-20220505212903762" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505212913932.png" alt="image-20220505212913932" style="zoom:80%;" />

```
```



### 107.求解立方根

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505212825169.png" alt="image-20220505212825169" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std; 
double f1(double x){
    return x*x*x;
}
double f(double x){
    double l;
    double r; 
    for(int i=0;i<10;i++){
        if(x>=pow(i,3) && x<=pow(i+1,3)){
            l=i;
            r=i+1;
            break;
        }
    }
    double mid = (l+r)/2;
    while(abs(f1(mid) - x) > 0.001){
        mid = (l+r)/2;
        if(f1(mid) - x < 0)
            l=mid;
        else
            r=mid;
    }
    return l;
}
int main(){
    double n;
    cin>>n;
    int flag = 1;
    if(n>=0)
        flag = 1;
    else
        flag = -1;
    cout<<fixed<<setprecision(1)<<flag*f(abs(n))<<endl;
}
```

### 106.字符逆序

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220504085540479.png" alt="image-20220504085540479" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    string s;
    getline(cin,s);
    //reverse(s.begin(),s.end());
    for(int i=0;i<s.size()/2;i++){
        swap(s[i],s[s.size()-1-i]);
    }
    cout<<s<<endl;
}
```

### 108.求最小公倍数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220504084928297.png" alt="image-20220504084928297" style="zoom:80%;" />

辗转相除法<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220504085016993.png" alt="image-20220504085016993" style="zoom:67%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    int a,b;
    cin>>a>>b;
    int s=a*b;
    int tmp;
    while(b!=0){
        tmp = a%b;
        a=b;
        b=tmp;
    }
    cout<<(s)/(a)<<endl;//积除以最大公约数，就是最小公倍数
}
```













































6008.统计包含给定前缀的字符串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220227112505134.png" alt="image-20220227112505134" style="zoom: 67%;" />

```c++
class Solution {
private:
    bool func(string a,string b){
        for(int i=0;i<b.size();i++)
            if(a[i]!=b[i])
                return false;
        return true;
    }
public:
    int prefixCount(vector<string>& words, string pref) {
        int cnt=0;
        for(int i=0;i<words.size();i++){
            if(words[i].size()<pref.size())
                continue;
            cnt+=func(words[i],pref);
        }
        return cnt;
    }
};
```

### 

![img](https://img-blog.csdnimg.cn/20190920145904368.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25laTUwNDI5MzczNg==,size_16,color_FFFFFF,t_70)

![image-20220308123309393](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220308123309393.png)

华为机试

### 1.

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220408202233425.png" alt="image-20220408202233425" style="zoom:80%;" />

```c++
#include <vector>
#include <string>
#include <iomanip>
int main()
{
    string s;
    vector<int> vec;
    while(getline(cin,s)){
        string t;
        for(auto c:s){
            if(c!=' ')
               t+=c;
            else
            {
                vec.push_back(t.size());
                t.clear();
            }
        }
        vec.push_back(t.size());
    }
    double res = 0;
    for(auto i:vec)
        res = res + i;
    res = res /double(vec.size());
    cout<<fixed<<setprecision(2)<< res <<endl;
    return 0;
}
```

2.

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220408203855417.png" alt="image-20220408203855417" style="zoom:80%;" />

```c
#include <bits/stdc++.h>
using namespace std;
int main()
{
    string s;
    while(getline(cin,s)){
        for(auto &c:s){
            if(c=='a'||c=='A'||c=='e'||c=='E'||
              c=='i'||c=='I'||c=='o'||c=='O'||
              c=='u'||c=='U')
                c = toupper(c);
            else if(c==' ')
                continue;
            else    
                c = tolower(c);
        }
        cout<<s<<endl;
    }
    return 0;
}
```

3.

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220408205029660.png" alt="image-20220408205029660" style="zoom:80%;" />

```c++
#include <bits/stdc++.h>
using namespace std;
long long  func(long long  n){
    if(n==1)return 1;
    return n*func(n-1);
}
int main()
{
    string s;
    while(getline(cin,s)){
        vector<char> map(128,0);
        vector<int> vec;
        for(auto c:s)
            map[c]++;
        for(auto i:map){
            if(i>1)
                vec.push_back(i);
        }
        long long sum = 1;
        for(auto i:vec)
            sum*=func(i);
        cout<<(func(s.size())/sum)<<endl;
    }
    return 0;
}
```

# 力扣hot100

### 4.[寻找两个正序数组的中位数]

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220428185840252.png" alt="image-20220428185840252" style="zoom:80%;" />

1.二分法：复杂度O(log (m+n))

```c
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int total_size = nums1.size() + nums2.size();
        if(total_size % 2 == 0){
            int left = find(nums1,0,nums2,0,total_size / 2);
            int right = find(nums1,0,nums2,0,total_size / 2 + 1);
            return (left + right)/2.0;
        }
        else{
            return find(nums1,0,nums2,0,total_size / 2 +1);
        }
    }
    int find(vector<int>& nums1,int i,vector<int>& nums2,int j,int k)
    {	//交换两数组，nums1是短的那个
        if(nums1.size() - i > nums2.size() - j) return find(nums2,j,nums1,i,k);
        if(k == 1)//边界处理
        {
            if(nums1.size() == i) return nums2[j];
            else return min(nums1[i],nums2[j]);
        }
        if(nums1.size() == i) return nums2[j + k - 1];
        int si = min(i + k / 2,(int)nums1.size());//越界处理
        int sj = j + k - k / 2;
        if(nums1[si - 1] > nums2[sj - 1]){
            return find(nums1,i,nums2,sj,k - (sj - j));
        }
        else
            return find(nums1,si,nums2,j,k - (si - i));
    }
};
```

分割数组：O(log min(m , n))

### 5. 最长回文子串

1.超时解法

```c++
class Solution {
public:
    bool func(string& s)
    {
        for(int i=0;i<s.size()/2;i++)
        {
            if(s[i]!=s[s.size()-1-i])
                return false;
        }
        return true;
    }
    string longestPalindrome(string s) {
        string t;
        for(int l = s.size();l >= 1;l--)
        {
            for(int i = 0;i <= s.size()- l;i++)
            {
                t = s.substr(i,l);
                if(func(t)) return t;
                t.clear();
            }
        }
        return "";
    }
};
```

2.动态规划

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220429122417037.png" alt="image-20220429122417037" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220429122436511.png" alt="image-20220429122436511" style="zoom:80%;" />

```c
class Solution {
public:
    string longestPalindrome(string s) {
        int n = s.size();
        vector<vector<int>> dp(n,vector<int>(n,false));
        int begin = 0;
        int maxlen = 1;
        for(int i = 0;i < n;i++)
            dp[i][i] = true;
        for(int l = 2;l <= n;l++){
            for(int i = 0;i < n;i++){
                int j = i + l - 1;
                if(j >= n) break;
                if(s[i] != s[j])
                    dp[i][j] = false;
                else{
                    if(j - i + 1 <=2){
                        dp[i][j] = true;
                    }
                    else
                        dp[i][j] = dp[i+1][j-1];
                }

                if(dp[i][j] && j - i + 1 > maxlen){
                    maxlen = j - i + 1;
                    begin = i;
                }
            }
        }
        return s.substr(begin,maxlen);
    }
};
```

3.中心扩展算法

```c
class Solution {
public:
    pair<int,int> expand(string& s,int l,int r){
        while(l >= 0 && r < s.size() && s[l] == s[r]){
            --l;
            ++r;
        }
        return make_pair(l+1,r-1);
    }
    string longestPalindrome(string s) {
        int end = 0;
        int start = 0;
        for(int i = 0;i < s.size();i++){
            auto [left1,right1] = expand(s,i,i);		//奇数长度子串
            auto [left2,right2] = expand(s,i,i+1);		//偶数长度子串
            if(right1 - left1 > end - start){
                start = left1;
                end = right1;
            }
            if(right2 - left2 > end - start){
                end = right2;
                start = left2;
            }
        }
        return s.substr(start,end - start + 1);
    }
};
```

4.Manacher 算法

```c++
class Solution {
    string add(string& s) {
        string t = s;
        s.clear();
        s += '*';
        for (int i = 0; i < t.size(); i++) {
            s += t[i];
            s += "*";
		}
	return s;
    }   
    vector<int> manacher(vector<int>& p, string& s) {
        p.resize(s.size());
        int max_r = 0, mid = 0;
        for (int i = 0; i < s.size(); i++) {
            if (i < max_r)
                p[i] = min(p[2 * mid - i], max_r - i);
            else
                p[i] = 1;
            while (i + p[i] < s.size() && i - p[i] >= 0 && s[i + p[i]] == s[i - p[i]])
                p[i]++;
            if (i + p[i] > max_r) {
                max_r = i + p[i];
                mid = i;
            }   
        }
	return p;
    }
public:
    string longestPalindrome(string s) {
        string t = s;
        s = add(s);
        vector<int> p;
        p = manacher(p,s);//p[i]是处理后的字符串的索引i位置对应的回文半径
        int index = 0;
        int max = INT_MIN;
        for(int i=0;i<p.size();i++){
            if(p[i]>max)
                max = p[i],index = i;
        }
        if(index%2==0)
            return t.substr((index-1)/2 - (p[index] - 1) / 2  + 1,p[index] - 1);
        return t.substr((index-1)/2 - (p[index] - 1) / 2,p[index] - 1);
    }
};
```

### 647.回文子串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220503091357846.png" alt="image-20220503091357846" style="zoom:80%;" />

```c++
class Solution {//中心扩展算法
public:
    int countSubstrings(string s) {
        int n = s.size();
        int count=0;
        for(int i=0;i<2*n-1;i++){
            int l = i/2;
            int r = i/2 + i%2;
            while(l>=0 && r<n && s[l]==s[r]){
                l--;
                r++;
                count++;
            }
        }
        return count;
    }
};
```

### 22. 括号生成

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220429161513538.png" alt="image-20220429161513538" style="zoom:80%;" />

回溯法：

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220429161537151.png" alt="image-20220429161537151" style="zoom:80%;" />

```c++
class Solution {
    vector<string> res;
    void dfs(int n,int l,int r,string t){
        if(l+r==2*n){
            res.push_back(t);
            return;
        }
        if(l<n){
            t.push_back('(');
            dfs(n,l+1,r,t);
            t.pop_back();
        }
        if(r<l){
            t.push_back(')');
            dfs(n,l,r+1,t);
            t.pop_back();
        }
    }
public:
    vector<string> generateParenthesis(int n) {
        dfs(n,0,0,"");
        return res;
    }
};
```

### 28.实现 strStr()

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220505215650749.png" alt="image-20220505215650749" style="zoom:80%;" />

```c++
class Solution {
    vector<int> res;
    vector<int> pi_table(string p, vector<int>& pi) {//求pi数组
        pi.resize(p.size());
        pi[0] = 0;
        int len = 0;// p[0....i-1]中的最长公共真前后缀长度，初始值为0
        int i = 1;	// 当前判断的 p[i]
        while (i < p.size()) {
            if (p[i] == p[len]) {
                len++;
                pi[i] = len;
                i++;
            }
            else {//不相等的话
                if (len >= 1)
                    len = pi[len - 1];
                else {//len = 0
                    pi[i] = 0;
                    i++;
                }
            }
        }
        pi.pop_back();
        pi.insert(pi.begin(), -1);
        return pi;
    }
public:
    int strStr(string s, string p) {
        vector<int> pi;
        pi = pi_table(p, pi);
        int i = 0;
        int j = 0;
        while (i < s.size()) {
            if (p[j] == s[i]) {
                if (j == p.size() - 1) {
                    res.push_back(i - j);
                    j = pi[j];
                    if (j == -1) {
                        i++;
                        j++;
                    }
                    continue;
                }
                i++;
                j++;
            }
            else {
                j = pi[j];
                if (j == -1) {
                    i++; 
                    j++;
                }
            }
        }
        if(res.size()==0) return -1;
        return res[0];
    }
};
```

### 31. 下一个排列

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220507214620248.png" alt="image-20220507214620248" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220429163214492.png" alt="image-20220429163214492" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220429163225954.png" alt="image-20220429163225954" style="zoom:80%;" />

```c++
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int n = nums.size();
        int i = n - 2;
        while(i >= 0 && nums[i] >= nums[i+1])
            i--;
        if(i >= 0){
            int j = n - 1;
            while(j >=0 && nums[i] >= nums[j])
                j--;
            swap(nums[i],nums[j]);
        }
        reverse(nums.begin()+i+1,nums.end());
    }
};
```

### 32.最长有效括号

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220429171621523.png" alt="image-20220429171621523" style="zoom:80%;" />

1.动态规划

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220429171537112.png" alt="image-20220429171537112" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220429171559716.png" alt="image-20220429171559716" style="zoom:80%;" />

```c++
class Solution {
public:
    int longestValidParentheses(string s) {
        vector<int> dp(s.size(),0);
        int maxlen = 0;
        for(int i=1;i<s.size();i++){
            if(s[i]==')'){
                if(s[i-1]=='(')
                    dp[i]=(i>=2?dp[i-2]:0)+2;
                else if(s[i-1]==')'&&i-1-dp[i-1]>=0&&s[i-1-dp[i-1]]=='(')
                    dp[i]=dp[i-1]+2+(i-2-dp[i-1]>=0?dp[i-1-dp[i-1]-1]:0);
            }
            maxlen = max(maxlen,dp[i]);
        }
        return maxlen;
    }
};
```

2.栈

3.双计数

### 33. 搜索旋转排序数组

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220429174221996.png" alt="image-20220429174221996" style="zoom:80%;" />

```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int l = 0;
        int r = nums.size()-1;
        while(l<=r){
            int mid = (l+r)/2;
            if(nums[mid]==target) return mid;
            else if(nums[0]<=nums[mid]){
                if(target>=nums[0]&&target<nums[mid])
                    r=mid-1;
                else    
                    l=mid+1;
            }
            else{
                if(target>nums[mid]&&target<=nums[nums.size()-1])
                    l=mid+1;
                else    
                    r=mid-1;
            }
        }
        return -1;
    }
};
```

### 34. 在排序数组中查找元素的第一个和最后一个位置]

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220429181927846.png" alt="image-20220429181927846" style="zoom:80%;" />

二分搜索

```c++
class Solution {
public:
    int floor(vector<int>& nums,int target){
        int n = nums.size();
        int l = -1;
        int r = n - 1;
        while(l < r){
            int mid = l + (r - l + 1)/2;
            if(nums[mid] >= target)
                r = mid - 1;
            else
                l = mid;
        }
        if(l+1 >=0&& l+1 <n &&nums[l + 1] == target)
            return l+1;
        //return l;不存在的时候返回前一个值的最后一个元素
        return -1;
    }
    int ceil(vector<int>& nums,int target){
        int n = nums.size();
        int l = 0;
        int r = n;
        while(l < r){
            int mid = l + (r - l - 1)/2;
            if(nums[mid] <= target)
                l = mid+ 1;
            else    
                r = mid;
        }
        if(r-1<n && r-1>=0 &&nums[r-1]==target)
            return r-1;
        //return r;不存在的时候ceil返回后一个值的第一个元素
        return -1;
    }
    vector<int> searchRange(vector<int>& nums, int target) {
        return {floor(nums,target),ceil(nums,target)};
    }
};
```

### 42.接雨水

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430092658072.png" alt="image-20220430092658072" style="zoom:80%;" />

1.动态规划

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430092644992.png" alt="image-20220430092644992" style="zoom:80%;" />

```c++
class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size();
        vector<int> leftmax(n);
        vector<int> rightmax(n);

        leftmax[0]=height[0];
        for(int i=1;i<=n-1;i++)
            leftmax[i]=max(height[i],leftmax[i-1]);
        rightmax[n-1]=height[n-1];
        for(int i=n-2;i>=0;i--)
            rightmax[i]=max(rightmax[i+1],height[i]);
        int res = 0;
        for(int i=0;i<n;i++)
            res+=min(leftmax[i],rightmax[i])-height[i];
        return res;
    }
};
```

2.栈

3.双指针

### 48.旋转矩阵

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430151255038.png" alt="image-20220430151255038" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430151326608.png" alt="image-20220430151326608" style="zoom:80%;" />

```c++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        for(int i=0;i<n/2;i++){
            for(int j=0;j<(n+1)/2;j++){
                int tmp = matrix[i][j];
                matrix[i][j]=matrix[n-1-j][i];
                matrix[n-1-j][i]=matrix[n-1-i][n-1-j];
                matrix[n-1-i][n-1-j]=matrix[j][n-1-i];
                matrix[j][n-1-i]=tmp;
            }
        }
    }
};
```

### 55.跳跃游戏

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430153438422.png" alt="image-20220430153438422" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430153500981.png" alt="image-20220430153500981" style="zoom:80%;" />

```c++
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int maxpos = 0;
        for(int i=0;i<nums.size();i++){
            if(i<=maxpos)
                maxpos = max(maxpos,i+nums[i]);
            if(maxpos>=nums.size()-1) return true;
        }
        return false;
    }
};
```

### 45.跳跃游戏Ⅱ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220503094408270.png" alt="image-20220503094408270" style="zoom:80%;" />

```c++
class Solution {
public:
    int jump(vector<int>& nums) {
        int end = 0;
        int max_pos = 0;
        int count=0;
        for(int i=0;i<nums.size()-1;i++){
            max_pos=max(max_pos,nums[i]+i);//(找到范围内能跳的最远的距离)
            if(i==end){//跳
                end=max_pos;
                count++;
            }
        }
        return count;
    }
};
```

### 56.合并区间

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430155704664.png" alt="image-20220430155704664" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430155730994.png" alt="image-20220430155730994" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(),intervals.end());
        vector<vector<int>> res;
        for(int i=0;i<intervals.size();){
            int t = intervals[i][1];
            int j = i+1;
            while(j<intervals.size()&&intervals[j][0]<=t){
                t = max(t,intervals[j][1]);
                j++;
            }
            res.push_back({intervals[i][0],t});
            i = j;
        }
        return res;
    }
};
```

### 62.不同路径

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430163151804.png" alt="image-20220430163151804" style="zoom:80%;" />

```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m,vector<int>(n,0));
        for(int i=0;i<m;i++)
            dp[i][0]=1;
        for(int j=0;j<n;j++)
            dp[0][j]=1;
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
};
```

### 64.最小路径和

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430163804916.png" alt="image-20220430163804916" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430163839102.png" alt="image-20220430163839102" style="zoom:80%;" />

```c++
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        if(grid.size()==0)
            return 0;
        int m = grid.size();
        int n = grid[0].size();

        vector<vector<int>> dp(m,vector<int>(n,0));
        dp[0][0] = grid[0][0];
        for(int i=1;i<m;i++)
            dp[i][0] = dp[i-1][0] + grid[i][0];
        for(int j=1;j<n;j++)
            dp[0][j] = dp[0][j-1] + grid[0][j];

        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                dp[i][j] = min(dp[i-1][j],dp[i][j-1]) + grid[i][j];
            }
        }
        return dp[m-1][n-1];
    }
};
```

### 72.编辑距离

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430170137765.png" alt="image-20220430170137765" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430170201541.png" alt="image-20220430170201541" style="zoom:80%;" />

```c++
class Solution {
public:
    int minDistance(string word1, string word2) {
        int m = word1.size();
        int n = word2.size();
        vector<vector<int>> dp(m+1,vector<int>(n+1,0));
        if(m*n==0) return m + n;
        for(int i=0;i<=m;i++)
            dp[i][0]=i;
        for(int j=0;j<=n;j++)
            dp[0][j]=j;
        for(int i=1;i<=m;i++){
            for(int j=1;j<=n;j++){
                if(word2[j-1]==word1[i-1]){//dp[i][j] 对应字符串的索引word1[i-1]  word[j-1]
                    dp[i][j] = dp[i-1][j-1];
                    continue;
                }
                dp[i][j] = min(dp[i-1][j-1],min(dp[i-1][j],dp[i][j-1]))+1;
            }
        }
        return dp[m][n];
    }  
};
```

### 84.柱状图中的最大矩形

单调栈

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430180921873.png" alt="image-20220430180921873" style="zoom:80%;" />

```c++
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        stack<int> stk;
        heights.insert(heights.begin(),0);
        heights.push_back(0);
        int maxval = 0;
        for(int i=0;i<heights.size();i++){
            while(!stk.empty() && heights[i] < heights[stk.top()]){
                int tmp = stk.top();
                stk.pop();
                int width = i - stk.top() - 1;
                maxval = max(maxval,width*heights[tmp]);
            }
            stk.push(i);
        }
        heights.pop_back();
        heights.erase(heights.begin());
        return maxval;
    }
};
```

### 85.最大矩形

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430201740689.png" alt="image-20220430201740689" style="zoom:80%;" />

```c++
class Solution {
public:
    int largestRectangleArea(vector<int> heights) {
        stack<int> stk;
        heights.insert(heights.begin(),0);
        heights.push_back(0);
        int maxval = 0;
        for(int i=0;i<heights.size();i++){
            while(!stk.empty() && heights[i] < heights[stk.top()]){
                int tmp = stk.top();
                stk.pop();
                int width = i - stk.top() - 1;
                maxval = max(maxval,width*heights[tmp]);
            }
            stk.push(i);
        }
        return maxval;
    }
    int maximalRectangle(vector<vector<char>>& matrix) {
        int m = matrix.size();
        if(m == 0) return 0;
        int n = matrix[0].size();

        int maxval = 0;
        vector<int> heights(n,0);
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j] == '1')
                    heights[j]++;
                else
                    heights[j] = 0;
            }
            maxval = max(maxval,largestRectangleArea(heights));
        }
        return maxval;
    }
};
```

### 96.不同的二分搜索树

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430210238447.png" alt="image-20220430210238447" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430210148563.png" alt="image-20220430210148563" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430210158665.png" alt="image-20220430210158665" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220430210210683.png" alt="image-20220430210210683" style="zoom:80%;" />

```c++
class Solution {
public:
    int numTrees(int n) {
        vector<int> g(n+1,0);
        g[0] = 1;
        g[1] = 1;
        for(int i=2;i<=n;i++){
            for(int j=1;j<=i;j++)
                g[i] += g[j-1]*g[i-j];
        }
        return g[n];
    }
};
```

### 114.二叉树展开为链表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220501085218192.png" alt="image-20220501085218192" style="zoom:80%;" />

额外空间

```c++
class Solution {
public:
    void flatten(TreeNode* root) {
        vector<TreeNode*> res;
        preorder(root,res);
        int n = res.size();
        for(int i = 0;i<n-1;i++){
            res[i]->right = res[i+1];
            res[i]->left = nullptr;
        }
    }
    void preorder(TreeNode* node,vector<TreeNode*>& res){
        if(node){
            res.push_back(node);
            preorder(node->left,res);
            preorder(node->right,res);
        }
    }
};
```

不需要额外空间

```c
class Solution {
public:
    void flatten(TreeNode* root) {
        TreeNode* cur = root;
        while(cur){
            if(cur->left){
                TreeNode* next = cur->left;
                TreeNode* predecessor = next;
                while(predecessor->right){
                    predecessor = predecessor->right;
                }
                predecessor->right = cur->right;
                cur->left = nullptr;
                cur->right = next;
            }
            cur = cur->right;
        }
    }
};
```

### 124.二叉树中的最大路径和

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220501090328444.png" alt="image-20220501090328444" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220501090342909.png" alt="image-20220501090342909" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220501090359926.png" alt="image-20220501090359926" style="zoom:80%;" />

```c++
class Solution {
    int max_sum = INT_MIN;
public:
    //max_gain函数的作用是得到从该节点出发，到叶子节点的最大节点值之和
    int max_gain(TreeNode* node){
        if(!node)
            return 0;
        
        int leftgain = max(0,max_gain(node->left));
        int rightgain = max(0,max_gain(node->right));

        int val = node->val + leftgain + rightgain;

        max_sum = max(max_sum,val);

        return node->val + max(leftgain,rightgain);
    }
    int maxPathSum(TreeNode* root) {
        max_gain(root);
        return max_sum;
    }
};
```

### 128.最长连续序列

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220501095048281.png" alt="image-20220501095048281" style="zoom:80%;" />

o(n)		**unordered_set是哦o(1)级别的，set是o(logn)**

```c++
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        if(nums.size()<2)return nums.size();
        unordered_set<int> set1;
        for(auto i:nums)
            set1.insert(i);
        int max_length = 1;
        for(auto it=set1.begin();it!=set1.end();it++){
            if(!set1.count((*it)-1)){
                int num = (*it);
                int length = 1;

                while(set1.count(num+1)){
                    length++;
                    num++;
                }
                max_length = max(max_length,length);
            }
        }
        return max_length;
    }
};
```

o(logn)

```c++
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        if (nums.size() < 2)return nums.size();
        set<int> set1;
        for (auto i : nums)
            set1.insert(i);
        int res = 1;
        int l = 1;
        vector<int> vec;
        for (auto it = set1.begin(); it != set1.end(); it++)
            vec.push_back((*it));
        cout << endl;
        int i = 0;
        int j = 1;
        while (i < vec.size() - 1) {
            if (vec[j] - vec[i] == 1) {
                l++;
                cout << "l " << l << endl;
            }
            else if (vec[j] - vec[i] > 1) {
                res = max(l, res);
                l = 1;
            }
            i++;
            j++;
        }
        res = max(l,res);
        return res;
    }
};
```

### 139.单词拆分

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220501110027583.png" alt="image-20220501110027583" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220501105939069.png" alt="image-20220501105939069" style="zoom:80%;" />

定义 dp[i] 表示字符串 s 前 i 个字符组成的字符串 s[0..i-1] 是否能被空格拆分成若干个字典中出现的单词

```c++
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string> set1;
        for(int i=0;i<wordDict.size();i++)
            set1.insert(wordDict[i]);
        vector<bool> dp(s.size()+1,false);
        dp[0] = true;
        for(int i=1;i<=s.size();i++){
            for(int j=0;j<i;j++){
                if(dp[j] && set1.count(s.substr(j,i-j))){
                    dp[i] = true;
                    break;    
                }
            }
        }
        return dp[s.size()];
    }
};
```

### 141.环形链表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220501110315560.png" alt="image-20220501110315560" style="zoom:80%;" />

O(N)	O(N)

```c++
class Solution {
public:
    bool hasCycle(ListNode *head) {
        unordered_set<ListNode*> set1;
        while(head){
            set1.insert(head);
            if(set1.count(head->next))
                return true;
            head = head->next;
        }
        return false;
    }
};
```

O(N)	O(1)快慢指针

```c++
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if(!head || !head->next)
            return false;
        ListNode* s = head;
        ListNode* f = head->next;
        while(s != f){
            if(!f || !f->next)
                return false;
            s=s->next;
            f=f->next->next;
        }
        return true;
    }
};
```

### 142.环形链表Ⅱ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220501111358817.png" alt="image-20220501111358817" style="zoom:80%;" />

```c++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
       ListNode* p = head;
       unordered_set<ListNode*> set1;
       while(p){
            set1.insert(p);
            if(set1.count(p->next))
                return p->next;
            p = p->next;
       } 
       return nullptr;
    }
};
```

o(n)		o(1)

```c++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* slow = head;
        ListNode* fast = head;
        while(fast){
            if(!fast->next)
                return nullptr;
            slow=slow->next;
            fast=fast->next->next;
            if(slow == fast){
                ListNode* p=head;
                while(p!=slow){
                    p=p->next;
                    slow=slow->next;
                }
                return p;
            }
        }
        return nullptr;
    }
};
```

### 146.LRU缓存

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220501120649484.png" alt="image-20220501120649484" style="zoom:80%;" />

```c++
struct dLinkNode{
    int key,val;
    dLinkNode* prev;
    dLinkNode* next;
    dLinkNode():key(0),val(0),prev(nullptr),next(nullptr){}
    dLinkNode(int k,int v):key(k),val(v),prev(nullptr),next(nullptr){}
};
class LRUCache {
    unordered_map<int,dLinkNode*> cache;
    dLinkNode* head;
    dLinkNode* tail;
    int size;
    int capacity;
public:
    LRUCache(int capacity) {
        //创建虚拟节点
        head = new dLinkNode();
        tail = new dLinkNode();
        head->next = tail;
        tail->prev = head;
        this->capacity = capacity;
        size = 0;
    }
    
    int get(int key) {
        if(!cache.count(key))
            return -1;              //不存在返回-1
        dLinkNode* node = cache[key];//存在通过哈希表定位，将其移到头部，然后返回其val
        moveToHead(node);
        return node->val;
    }
    
    void put(int key, int value) {
        if(!cache.count(key)){
            dLinkNode* node = new dLinkNode(key,value);
            cache[key]=node;
            addToHead(node);
            size++;
            if(size > capacity){
                dLinkNode* delete_node = removeTail();
                cache.erase(delete_node->key);
                delete delete_node;
                size--;
            }
        }
        else{//存在通过哈希表定位，然后修改其val，并移到头部
            dLinkNode* node = cache[key];
            node->val = value;
            moveToHead(node);
        }
    }
    //添加node到头部
    void addToHead(dLinkNode* node){
        node->prev = head;
        node->next = head->next;
        head->next->prev = node;
        head->next = node;
    }
    //移除node
    void removeNode(dLinkNode* node){
        node->prev->next = node->next;
        node->next->prev = node->prev;
    }
    //移动到头部
    void moveToHead(dLinkNode* node){
        removeNode(node);
        addToHead(node);
    }
    //删除尾节点，将其并返回
    dLinkNode* removeTail(){
        dLinkNode* node = tail->prev;
        removeNode(node);
        return node;
    }

};
```

### 152.乘积的最大子数组

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220501162523960.png" alt="image-20220501162523960" style="zoom:80%;" />

```c
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        vector<int> maxf(nums),minf(nums);
        for(int i=1;i<nums.size();i++){
            maxf[i] = max(maxf[i-1]*nums[i],max(minf[i-1]*nums[i],nums[i]));
            minf[i] = min(maxf[i-1]*nums[i],min(minf[i-1]*nums[i],nums[i]));
        }
        return *max_element(maxf.begin(),maxf.end());
    }
};
```

### 207.课程表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220501163325119.png" alt="image-20220501163325119" style="zoom:80%;" />

DFS

```c++

```

BFS

```c++
class Solution {
    vector<vector<int>> edges;      //存储有向图的边
    vector<int> indeg;      //存储入度
    vector<int> res;        //存储答案
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        edges.resize(numCourses);
        indeg.resize(numCourses);
        for(auto p:prerequisites){
            edges[p[1]].push_back(p[0]);//构建邻接表
            indeg[p[0]]++;              //计算每个节点的入度
        }

        queue<int> q;//将入度为0的课程放入，入度为0表示，先修课程为0
        for(int i=0;i<numCourses;i++){
            if(indeg[i] == 0)
                q.push(i);
        }

        while(!q.empty()){
            int u = q.front();
            q.pop();
            res.push_back(u);

            for(int v:edges[u]){//u学了之后，它指向的课程的入度减1，若减到0，则可以学了，放入队列
                indeg[v]--;
                if(indeg[v]==0)
                    q.push(v);
            }
        }
        if(res.size() == numCourses)
            return true;
        return false;
    }
};
```

### 208.实现前缀树

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220501182455405.png" alt="image-20220501182455405" style="zoom:80%;" />

```c++
class Trie {
    vector<Trie*> children;
    bool isEnd = false;
	//是否有prefix字符串
    Trie* searchPrefix(string prefix){
        Trie* node = this;
        for(char ch:prefix){
            ch -= 'a';
            if(node->children[ch] == nullptr)
                return nullptr;
            node = node->children[ch];
        }
        return node;
    }
public:
    Trie():children(26),isEnd(false){}
    
    void insert(string word) {
        Trie* node = this;//根节点
        for(char ch:word){
            ch -= 'a';
            if(node->children[ch] == nullptr){
                node->children[ch] = new Trie(); 
            }
            node = node->children[ch];
        }
        node->isEnd = true;
    }
    //是否有word字符串
    bool search(string word) {
        Trie* node = this->searchPrefix(word);
        return node!=nullptr && node->isEnd;
    }
    //是否有prefix的前缀
    bool startsWith(string prefix) {
        return this->searchPrefix(prefix)!=nullptr;
    }
};
```

### 221.最大正方形

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502083251775.png" alt="image-20220502083251775" style="zoom:80%;" />

我们用 dp(i,j) 表示以 (i, j)为右下角，且只包含 1 的正方形的边长最大值。

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502083351688.png" alt="image-20220502083351688" style="zoom:80%;" />

```c++
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        if(matrix.size()==0||matrix[0].size()==0)
            return 0;
        int m = matrix.size();
        int n = matrix[0].size();
        int maxside = 0;
        vector<vector<int>> dp(m,vector<int>(n,0));
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j] == '1'){
                    if(i==0 || j==0)
                        dp[i][j] = 1;
                    else
                        dp[i][j] = min(dp[i-1][j],min(dp[i][j-1],dp[i-1][j-1])) + 1;
                }
                maxside = max(maxside,dp[i][j]);
            }
        }
        return maxside*maxside;
    }
};
```

### 287.寻找重复数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502091618601.png" alt="image-20220502091618601" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502091635793.png" alt="image-20220502091635793" style="zoom:80%;" />

```c++
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int n = nums.size();
        int l=1;
        int r=n-1;
        int res=0;
        while(l <= r){
            int mid = (l+r)/2;
            int cnt = 0;
            for(auto x:nums){
                if(x<=mid) cnt++;
            }
            if(cnt<=mid)
                l = mid+1;
            else{
                r = mid-1;
                res=mid;
            }
            //核心思想：找到第一个cnt大于mid的mid就是重复的数字
        }
        return res;
    }
};
```

快慢指针:大小为n的数组，里面的值都在[1,n-1]之间。那么其值也是下标。

```c++
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow = 0;
        int fast = 0;
        do{
            slow = nums[slow];			//slow每次跳一次
            fast = nums[nums[fast]];	//fast每次跳两次
        }while(slow!=fast);
        slow = 0;
        while(slow!=fast){
            slow=nums[slow];
            fast=nums[fast];
        }
        return fast;
    }
};
```

### 301.删除无效的括号

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502111407969.png" alt="image-20220502111407969" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502111427125.png" alt="image-20220502111427125" style="zoom:80%;" />

```c++
class Solution {
    unordered_set<string> res;
    //cnt表示，索引i之前的左右括号的累加值，累加规则为，加入一个左括号，cnt++，加入一个右括号，cnt--
    //cnt初始化为0，因为此时字符串还为空
    //只有当 cnt == 0 的时候才是一个合法的字符串
    void dfs(string& s,string t,int l,int r,int i,int cnt){
        if(i==s.size()){
            if(cnt == 0) res.insert(t);
            return;
        }
        if(s[i]=='('){
            if(l>0) dfs(s,t,l-1,r,i+1,cnt); //删除左括号
            dfs(s,t+'(',l,r,i+1,cnt+1);     //不需要删除，直接加入。
        }
        else if(s[i]==')'){
            //删除右括号
            if(r>0) dfs(s,t,l,r-1,i+1,cnt); 
            //也可以选择不删除，因为cnt>0,说明前面左括号多余，需要用右括号抵消
            if(cnt>0) dfs(s,t+')',l,r,i+1,cnt-1);
        }
        else 
            dfs(s,t+s[i],l,r,i+1,cnt);
    }
public:
    vector<string> removeInvalidParentheses(string s) {
        int l=0;//l 和 r表示 应当删除的 不合法的左右括号的个数，
        int r=0;
        for(auto c:s){
            if(c=='(') l++;
            else if(c==')'){
                if(l<=0)r++;
                else l--;
            }
        }
        dfs(s,"",l,r,0,0);
        vector<string> vec(res.begin(),res.end());
        return vec;
    }
};
```

### 309.最佳买卖股票时机含冷冻期

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502113510559.png" alt="image-20220502113510559" style="zoom:80%;" />

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n=prices.size();
        vector<vector<int>> dp(n,vector<int>(3,0));
        //初始化1.可以买股票，此时收益为-prices[0]
        //	   2.第一天不可能卖股票
        //	   3.可以什么都不做
        dp[0]={-prices[0],0,0};
        for(int i=1;i<n;i++){
            //持有股票的状态，可以是之前就已经持有了买的，也可以是今天买的。
            dp[i][0] = max(dp[i-1][0],dp[i-1][2]-prices[i]);
            //冷冻期，刚卖完股票的状态，直接加上卖出价格即可
            dp[i][1] = dp[i-1][0]+prices[i];
            //既不是冷冻也不持有股票，什么事情也不做，延续i-1中[1][2]的状态即可
            dp[i][2] = max(dp[i-1][1],dp[i-1][2]);
        }
        return max(dp[n-1][0],max(dp[n-1][1],dp[n-1][2]));
    }
};
```

### 312.戳气球

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502121650265.png" alt="image-20220502121650265" style="zoom:80%;" />

记忆化搜索

```c++
class Solution {
    vector<vector<int>> res;
    int dfs(vector<int>& nums,int l,int r){
        if(l>=r-1) return 0;
        if(res[l][r]!=-1)
            return res[l][r];
        for(int i=l+1;i<=r-1;i++){
            res[l][r] = max(res[l][r],nums[l]*nums[i]*nums[r]+dfs(nums,l,i)+dfs(nums,i,r));
        }
        return res[l][r];
    }
public:
    int maxCoins(vector<int>& nums) {
        nums.insert(nums.begin(),1);
        nums.push_back(1);
        res.assign(nums.size(),vector<int>(nums.size(),-1));
        return dfs(nums,0,nums.size()-1);
    }
};
```

动态规划：

### 322.零钱兑换

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220218105832859.png" alt="image-20220218105832859" style="zoom:80%;" />

动态规划

```c++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        //dp[i]，表示装满容量为i的时候，需要最少硬币的个数
        vector<int> dp(amount+1,0);
        dp[0] = 0;
        for(int j=1;j<=amount;j++){
            dp[j] = amount+1;
            for(int i=0;i<coins.size();i++)
                if(j>=coins[i])
                    //遍历所有的硬币，看哪一个放到最后，可以使得最终结果最小。
                    dp[j] = min(dp[j],dp[j-coins[i]]+1);
        }
        return dp[amount]==(amount+1)?-1:dp[amount];
    }
};
```

记忆化搜索

### 337.打家劫舍Ⅲ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502141138525.png" alt="image-20220502141138525" style="zoom:80%;" />

```c++
class Solution {
    unordered_map<TreeNode*,int> f,g;
    void dfs(TreeNode* node){
        if(!node) return;
        dfs(node->left);
        dfs(node->right);
        f[node] = node->val+g[node->left]+g[node->right];
        g[node] = max(f[node->left],g[node->left])+max(f[node->right],g[node->right]);
    }
public:
    int rob(TreeNode* root) {
        dfs(root);
        return max(f[root],g[root]);
    }
};
```

### 338.比特位计数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502141255849.png" alt="image-20220502141255849" style="zoom:80%;" />

通用解法o(nlogn)

```c++
class Solution {
    int func(int x){
        int sum = 0;
        while(x){
            sum += x%2;
            x/=2;
        }
        return sum;
    }
public:
    vector<int> countBits(int n) {
        vector<int> res(n+1,0);
        for(int i=0;i<=n;i++){
            res[i] = func(i);
            //res[i] = bitset<32>(i).count();
        }
        return res;
    }
};
```

动态规划

```c++
class Solution {
public:
    vector<int> countBits(int n) {
        vector<int> res(n+1);
        for(int i=1;i<=n;i++){
            res[i]=res[i&(i-1)]+1;
        }
        return res;
    }
};
```

### 394.字符串解码

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502143545903.png" alt="image-20220502143545903" style="zoom:80%;" />

```c++
class Solution {
public:
    string decodeString(string s) {
        int i = 0;
        int n = s.size();
        string res;
        stack<pair<int,string>> stk;
        int num = 0;
        for(int i=0;i<n;i++){
            if(isdigit(s[i])){
                num = num*10+int(s[i]-'0');
            }
            else if(s[i]=='['){
                stk.emplace(num,res);
                num=0;
                res="";
            }
            else if(s[i]==']'){
                int a = stk.top().first;
                string b = stk.top().second;
                stk.pop();
                for(int i=0;i<a;i++)b+=res;
                res=b;
            }
            else
                res+=s[i];
        }
        return res;
    }
};
```

递归

### 399.除法求值

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502151929274.png" alt="image-20220502151929274" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<double> calcEquation(vector<vector<string>>& equations, vector<double>& values, vector<vector<string>>& queries) {
        //首先将出现的单个字符变量，一一映射为数字0....count-1
        int count=0;
        unordered_map<string,int> map1;
        for(int i=0;i<values.size();i++){
            if(!map1.count(equations[i][0])) map1[equations[i][0]]=count++;
            if(!map1.count(equations[i][1])) map1[equations[i][1]]=count++;
        }
        //构建邻接表
        vector<vector<pair<int,double>>> edges(count);
        for(int i=0;i<values.size();i++){
            int a = map1[equations[i][0]];
            int b = map1[equations[i][1]];
            edges[a].emplace_back(b,values[i]);
            edges[b].emplace_back(a,1/values[i]);
        }
        vector<double> res;
        for(auto& x:queries){
            double result=-1.0;
            //当queries中的组合，的两个字符都存在的时候才进行操作，否则为-1
            if(map1.count(x[0]) && map1.count(x[1])){
                int a=map1[x[0]];
                int b=map1[x[1]];
                if(a==b) result=1.0;
                //若两字符都不存在，且不等
                else{
                    queue<int> points;
                    points.push(a);
                    vector<double> vec(count,-1.0);
                    vec[a]=1.0;

                    while(!points.empty()&&vec[b]<0){
                        int tmp=points.front();
                        points.pop();

                        for(auto p:edges[tmp]){
                            if(vec[p.first]<0){
                                vec[p.first]=vec[tmp]*p.second;
                                points.push(p.first);
                            }
                        }
                    }
                    result=vec[b];
                }
            }
            res.push_back(result);
        }
        return res;
    }
};
```

### 406.根据身高重建队列

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502154604354.png" alt="image-20220502154604354" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502155041065.png" alt="image-20220502155041065" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502155055214.png" alt="image-20220502155055214" style="zoom:80%;" />

```c++
bool cmp(vector<int> a,vector<int> b){
    return a[0]>b[0]||(a[0]==b[0]&&a[1]<b[1]);
}
class Solution {
public:
    vector<vector<int>> reconstructQueue(vector<vector<int>>& people) {
        sort(people.begin(),people.end(),cmp);
        vector<vector<int>> res;
        for(auto p:people){
            res.insert(res.begin()+p[1],p);
        }
        return res;
    }
};
```

### 448.找到所有数组中消失的数字

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220517095738200.png" alt="image-20220517095738200" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502160713331.png" alt="image-20220502160713331" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        vector<int> res;
        for(auto& x:nums){
            int y = (x-1)%nums.size();
            nums[y]+=nums.size();
        }
        for(int i = 0;i<nums.size();i++){
            if(nums[i]<=nums.size())
                res.push_back(i+1);
        }
        return res;
    }
};
```

### 494.目标和

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502161450022.png" alt="image-20220502161450022" style="zoom:80%;" />

回溯法：

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502161505457.png" alt="image-20220502161505457" style="zoom:80%;" />

```c++
class Solution {
    int count=0;
    void dfs(vector<int>& nums,int target,int index,int sum){
        if(index == nums.size()){
            if(sum==target)count++;
        }
        else{
            dfs(nums,target,index+1,sum+nums[index]);
            dfs(nums,target,index+1,sum-nums[index]);
        }
    }
public:
    int findTargetSumWays(vector<int>& nums, int target) {
        dfs(nums,target,0,0);
        return count;
    }
};
```

动态规划

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502170816449.png" alt="image-20220502170816449" style="zoom:80%;" />

```c++
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int target) {
        int sum = 0;
        for(auto x:nums)
            sum+=x;
        if((sum-target)%2==1||sum-target<0) return 0;
        int c = (sum-target)/2;
        int n = nums.size();
        //dp[i][j] //0..i,选出和为j的数字的，方案个数
        vector<vector<int>> dp(n+1,vector<int>(c+1,0));

        dp[0][0]=1;
        
        for(int i=1;i<=n;i++){
            for(int j=0;j<=c;j++){
                dp[i][j] = dp[i-1][j];
                if(j>=nums[i-1]) dp[i][j]+=dp[i-1][j-nums[i-1]];
            }
        }

        return dp[n][c];
    }
};
```

### 538.把二叉搜索树转换为累加树

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502171452975.png" alt="image-20220502171452975" style="zoom:80%;" />

```c++
class Solution {
    int sum = 0;
    void dfs(TreeNode* node){
        if(!node) return;
        dfs(node->right);
        sum += node->val;
        node->val = sum;
        dfs(node->left);
    }
public:
    TreeNode* convertBST(TreeNode* root) {
        dfs(root);
        return root;
    }
};
```

Morris遍历

```
```

### 543.二叉树的直径

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220516213220258.png" alt="image-20220516213220258" style="zoom:80%;" />

```c++
class Solution {
    int res = 0;
    int depth(TreeNode* node){
        if(!node) return 0;
        int left = depth(node->left);
        int right = depth(node->right);
        res = max(res,left+right);
        return max(left,right) + 1;
    }//半径就等于，左子树最大深度，加上右子树最大深度
public:
    int diameterOfBinaryTree(TreeNode* root) {
        cout<<depth(root);

        return res;
    }
};
```

### 560.和为k的连续子数组

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502174313081.png" alt="image-20220502174313081" style="zoom:80%;" />

o(n^2)

```c++
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int count = 0;
        for (int i = 0; i < nums.size(); ++i) {
            int sum = 0;
            for (int j = i; j >= 0; --j) {
                sum += nums[j];
                if (sum == k) {
                    count++;
                }
            }
        }
        return count;
    }
};
```

前缀和o(n)

```c++
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int pre = 0;
        int count = 0;
        unordered_map<int,int> map1;
        map1[0]=1;
        for(int i=0;i<nums.size();i++){
            pre+=nums[i];
            if(map1.count(pre-k))
                count+=map1[pre-k];
            map1[pre]++;
        }
        return count;
    }
};
```

### 581.最短无序连续子数组

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502183057249.png" alt="image-20220502183057249" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220502183116452.png" alt="image-20220502183116452" style="zoom:67%;" />

```c++
class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        int minv = INT_MAX;
        int maxv = INT_MIN;
        int right = -1;
        int left = -1;
        int n = nums.size();
        for(int i=0;i<n;i++){
            if(nums[i]>=maxv)
                maxv=nums[i];
            else
                right=i;
            if(nums[n-1-i]<=minv)
                minv=nums[n-1-i];
            else    
                left=n-1-i;
        }
        return right==-1?0:(right-left+1);
    }
};
```

### 617.合并二叉树

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220503084114181.png" alt="image-20220503084114181" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220503084135446.png" alt="image-20220503084135446" style="zoom:80%;" />

```c++
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        if(!root1&&!root2) return nullptr;
        if(!root1) return root2;
        if(!root2) return root1;

        root1->val+=root2->val;
        root1->left = mergeTrees(root1->left,root2->left);
        root1->right = mergeTrees(root1->right,root2->right);
        return root1;
    }
};
```

迭代：

### 621.任务调度器

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220503090058307.png" alt="image-20220503090058307" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220503090317666.png" alt="image-20220503090317666" style="zoom:80%;" />

```c++
bool cmp(int a,int b){
    return a>b;
}
class Solution {
public:
    int leastInterval(vector<char>& tasks, int n) {
        vector<int> vec(26,0);
        for(auto x:tasks)
            vec[x-'A']++;
        sort(vec.begin(),vec.end(),cmp);
        int count = 0;
        for(auto x:vec)
            if(x==vec[0]) count++;
        return max((int)tasks.size(),(vec[0]-1)*(n+1)+count);
    }
};
```

### 739.每日温度

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220503093039232.png" alt="image-20220503093039232" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        int n = temperatures.size();
        vector<int> res(n,0);
        stack<int> s;
        for(int i=0;i<n;i++){
            while(!s.empty()&&temperatures[i]>temperatures[s.top()]){
                res[s.top()] = i - s.top();
                s.pop();
            }
            s.push(i);
        }
        return res;
    }
};
```

## 剑指offer

### 03.数组中重复的数字

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220304212958456.png" alt="image-20220304212958456" style="zoom:80%;" />

解法二：时间复杂度 O(N),空间复杂度 O(1)

```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        int i=0;
        while(i<nums.size()){
            if(nums[i]==i){
                i++;
                continue;
            }
            if(nums[i]==nums[nums[i]])return nums[i];
            swap(nums[i],nums[nums[i]]);
        }
        return -1;
    }
};
```

### 04.二维数组中的查找

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220304214816298.png" alt="image-20220304214816298" style="zoom:80%;" />

解法一：时间复杂度 O(N*M	),空间复杂度 O(1)

```c++
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        for(int i=0;i<matrix.size();i++)
            for(int j=0;j<matrix[i].size();j++)
                if(matrix[i][j]==target)
                    return true;
        return false;
    }
};
```

解法二：时间复杂度 O(N+M),空间复杂度 O(1)

```c++
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        if(matrix.size()==0)return false;
        int i=0,j=matrix[0].size()-1;
        while(j>=0&&i<matrix.size()){
            if(matrix[i][j]==target) return true;
            else if(matrix[i][j]>target)j--;
            else i++;
        }
        return false;
    }
};
```

或者

```c++
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        int j=0,i=matrix.size()-1;
        while(i>=0&&j<matrix[0].size()){
            if(matrix[i][j]==target) return true;
            else if(matrix[i][j]>target)i--;
            else j++;
        }
        return false;
    }
};
```

### 05.替换空格

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220307084510229.png" alt="image-20220307084510229" style="zoom:80%;" />

1.原地:时间复杂度 O(N),空间复杂度 O(1)

```c++
class Solution {
public:
    string replaceSpace(string s) {
        int len = s.size();
        for(int i = 0;i < len;i++)
            if(s[i] ==' ') s+="  ";
        int i = s.size()-1;
        for(int j=len-1;j>=0;j--){
            if(s[j]==' '){
                s[i--] = '0';
                s[i--] = '2';
                s[i--] = '%';
            }
            else
                s[i--] = s[j];
        }
        return s;
    }
};
```

### 06.从尾到头打印链表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220307085156058.png" alt="image-20220307085156058" style="zoom:80%;" />

2.递归:时间复杂度 O(N),空间复杂度 O(N)

```c++
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        if(!head)return {};
        vector<int> res=reversePrint(head->next);
        res.push_back(head->val);
        return res;
    }
};
```

### 07.重建二叉树			

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220307095754790.png" alt="image-20220307095754790" style="zoom:80%;" />

1.递归：时间复杂度 O(N),空间复杂度 O(N)，改进：把数组复制一份，不用每次都调用，节省空间

```c++
class Solution {
    vector<int> p;
    unordered_map<int,int> map;
    TreeNode* dfs(int pre_root,int in_left,int in_right){
        if(in_left>in_right) return nullptr;
        int in_root = map[p[pre_root]];
        TreeNode* node = new TreeNode(p[pre_root]);
        node->left = dfs(pre_root+1,in_left,in_root-1);
        node->right = dfs(pre_root+in_root-in_left+1,in_root+1,in_right);
        return node;
    }
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        p = preorder;
        for(int i=0;i<inorder.size();i++)
            map[inorder[i]] = i;
        return dfs(0,0,inorder.size()-1);
    }
};
```

2.迭代:时间复杂度 O(N),空间复杂度 O(N)

```c++
class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        if(preorder.size()==0)return nullptr;
        stack<TreeNode*> stk;
        TreeNode* root=new TreeNode(preorder[0]);
        stk.push(root);
        int index=0;
        for(int i=1;i<preorder.size();i++){
            int preorderval=preorder[i];
            TreeNode* node=stk.top();
            if(node->val!=inorder[index]){
                node->left=new TreeNode(preorderval);
                stk.push(node->left);
            }
            else{
                while(!stk.empty()&&stk.top()->val==inorder[index]){
                    node=stk.top();
                    stk.pop();
                    index++;
                }
                node->right=new TreeNode(preorderval);
                stk.push(node->right);
            }
        }
        return root;
    }
};
```

### 09. 用两个栈实现队列

时间复杂度：对于插入和删除操作，时间复杂度均为 O(1)O(1)。插入不多说，对于删除操作，虽然看起来是 O(n)O(n) 的时间复杂度，但是仔细考虑下每个元素只会「至多被插入和弹出 stack2 一次」，因此均摊下来每个元素被删除的时间复杂度仍为 O(1)O(1)。

空间复杂度：O(n)

```c++
class CQueue {
    stack<int> s1;
    stack<int> s2;
public:
    CQueue() {

    }
    
    void appendTail(int value) {
        s1.push(value);
    }
    
    int deleteHead() {
        if(s2.empty()){
            while(!s1.empty()){
                s2.push(s1.top());
                s1.pop();
            }
        }
        if(s2.empty())
            return -1;
        else{
            int res = s2.top();
            s2.pop();
            return res;
        }
    }
};

```

### 10.斐波那契数列

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220308085109669.png" alt="image-20220308085109669" style="zoom:80%;" />

```c++
class Solution {
    int f(int n){
        if(n<2) return n;
        return f(n-1)+f(n-2);
    }
public:
    int fib(int n) {
        return f(n);
    }
};
```

滚动数：时间复杂度：O(n)   空间复杂度：O(1)

```c++
class Solution {
public:
    int fib(int n) {
        if(n<2) return n;
        int a=0,b=0,c=1;
        for(int i=1;i < n;i++){
            a=b;
            b=c;
            c=a+b;
        }
        return c;
    }
};
```

矩阵快速幂：时间复杂度：O(logn)   空间复杂度：O(1)

```c++
class Solution {
public:
    int fib(int n) {
        if(n<2) return n;
        vector<vector<int>> t = {{1,1},{1,0}};
        vector<vector<int>> res = mpow(t,n-1);
        return res[0][0];
    }
    vector<vector<int>> mpow(vector<vector<int>> m,int n){
        vector<vector<int>> res = {{1,0},{0,1}};
        while(n){
            if(n&1)
                res = mul(res,m);
            n>>=1;
            m=mul(m,m);
        }
        return res;
    }
    vector<vector<int>> mul(vector<vector<int>> a,vector<vector<int>> b){
        vector<vector<int>> c = {{0,0},{0,0}};
        int x = a.size();
        int y = a[0].size();
        int z = b[0].size();
        for(int i=0;i<y;i++){
            for(int j=0;j<z;j++){
                for(int k=0;k<y;k++){
                    c[i][j]+=a[i][k]*b[k][j];
                }
            }
        }
        return c;
    }
};
```

通项公式：

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220516190510889.png" alt="image-20220516190510889" style="zoom: 80%;" />

### 11.旋转数组的最小数字

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220308101628257.png" alt="image-20220308101628257" style="zoom:80%;" />

二分查找：O(logn)，边界条件非常关键，是mid 还是mid+1决定了循环能否结束。

```c++
class Solution {
public:
    int minArray(vector<int>& numbers) {
        int i = 0;
        int j =numbers.size()-1;
        while(i<j){
            int mid = (i+j)/2;
            if(numbers[mid]<numbers[j])
                j=mid;
            else if(numbers[mid]>numbers[j])
                i=mid+1;
            else
                j--;
        }
        return numbers[i];
    }
};
```

### 12.矩阵中的路径

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220308111847739.png" alt="image-20220308111847739" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220308111917391.png" alt="image-20220308111917391" style="zoom:80%;" />

```c++
class Solution {
    int m,n;
    bool dfs(vector<vector<char>>& board,int index,int i,int j,string word){
        if(i<0||i>=m||j<0||j>=n||board[i][j]!=word[index])return false;
        if(index == word.size()-1) return true;
        board[i][j] = '\0';
        bool res = dfs(board,index+1,i,j+1,word)||dfs(board,index+1,i-1,j,word)||
                dfs(board,index+1,i+1,j,word)||dfs(board,index+1,i,j-1,word);
        board[i][j] = word[index];
        return res;
    }
public:
    bool exist(vector<vector<char>>& board, string word) {
        m = board.size();
        if(m==0) return false;
        n = board[0].size();
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(dfs(board,0,i,j,word)) return true;
            }
        }
        return false;
    }
};
```

### 13.机器人的运动范围

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220309090522694.png" alt="image-20220309090522694" style="zoom:80%;" />

广度优先搜索：时间复杂度：O(mn)，其中 m 为方格的行数，n 为方格的列数。考虑所有格子都能进入，那么搜索的时候一个格子最多会被访问的次数为常数，所以时间复杂度为 O(2mn)=O(mn)。

空间复杂度：O(mn)，其中 m 为方格的行数，n 为方格的列数。搜索的时候需要一个大小为 O(mn) 的标记结构用来标记每个格子是否被走过。

```c++
class Solution {
private:
    int d[4][2]={{-1,0},{0,1},{1,0},{0,-1}};

    int get(int x){
        int res=0;
        while(x){
            res+=x%10;
            x/=10;
        }
        return res;
    }
public:
    int movingCount(int m, int n, int k) {
        if(k==0)return 1;
        queue<pair<int,int>> q;
        vector<vector<bool>> visited(m,vector<bool>(n,false));
        q.push(make_pair(0,0));
        visited[0][0]=true;
        int result=1;
        while(!q.empty()){
            auto [x,y]=q.front();
            q.pop();
            for(int i=0;i<4;i++){
                int x1=x+d[i][0];
                int y1=y+d[i][1];
                if(x1<0||x1>=m||y1<0||y1>=n||visited[x1][y1]||get(x1)+get(y1)>k)continue;
                q.push(make_pair(x1,y1));
                visited[x1][y1]=true;
                result++;
            }
        }
        return result;
    }
};
```

深度优先搜索：时间复杂度 O(MN)： 最差情况下，机器人遍历矩阵所有单元格，此时时间复杂度为 O(MN) 。
空间复杂度 O(MN)： 最差情况下，Set visited 内存储矩阵所有单元格的索引，使用 O(MN)O(MN) 的额外空间。

```c++
class Solution {
    int k;
    int m,n;
    vector<vector<bool>> vis;
    int dfs(int i,int j){
        if(i<0||i>=m||j<0||j>=n||vis[i][j]||get(i)+get(j)>k) return 0;
        vis[i][j] = true;
        return 1+dfs(i-1,j)+dfs(i+1,j)+dfs(i,j-1)+dfs(i,j+1);
    }
    int get(int x){
        int res = 0;
        while(x){
            res+=x%10;
            x/=10;
        }
        return res;
    }
public:
    int movingCount(int m, int n, int k) {
        vis = vector<vector<bool>>(m,vector<bool>(n,false));
        this->m=m;
        this->n=n;
        this->k=k;
        return dfs(0,0);
    }
};
```

### 14.剪绳子

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220309093956901.png" alt="image-20220309093956901" style="zoom:80%;" />

动态规划:时间复杂度：O(n ^ 2) 空间复杂度：O(n)

```c++
class Solution {
public:
    int cuttingRope(int n) {
        vector<int> f(n+1);
        for(int i=0;i<=n;i++){
            for(int j=0;j<i;j++){
                f[i]=max(f[i],max(j*f[i-j],j*(i-j)));
            }
        }
        return f[n];
    }
};
```

### 14剪绳子Ⅱ

数学推导最优解

```c++
class Solution {
public:
    int cuttingRope(int n) {
        if(n<=3)return n-1;
        long long res=1;
        while(n>4){
            res=res*3%1000000007;
            n-=3;
        }
        return res*n%1000000007;    //剩0不需要分了//余1就是1与
    }
};
```

### 15. 二进制中1的个数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220309101154167.png" alt="image-20220309101154167" style="zoom:80%;" />

遍历：时间复杂度O(n)

```c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int cnt=0;
        while(n){
            cnt+=n%2;
            n/=2;
        }   
        return cnt;
    }
};
```

位运算优化：n&n-1这个运算将n中的最低位的1消除。时间复杂度O(logn)

```c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int cnt=0;
        while(n){
            n&=(n-1);
            cnt++;
        }   
        return cnt;
    }
};
```

### 16.数值的整数次方

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220309103727736.png" alt="image-20220309103727736" style="zoom:80%;" />

快速幂

```c++
class Solution {
public:
    double myPow(double x, int n) {
        long m=n;
        if(m<0){
            x=1/x;
            m=-m;
        }
        double res=1;
        while(m){
            if(m&1)res*=x;
            m>>=1;
            x*=x;
        }
        return res;
    }
};
```

### 17.打印从1到最大的n位数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220310214313440.png" alt="image-20220310214313440" style="zoom:80%;" />

```c++
class Solution {
    vector<string> res;
    string s="0123456789";
    string cur;
    void dfs(int index,int len){
        if(index==len){
            res.push_back(cur);
            return;
        }
        int start = index==0?1:0;
        for(int i=start;i<10;i++){
            cur.push_back(s[i]);
            dfs(index+1,len);
            cur.pop_back();
        }
    }
public:
    vector<int> printNumbers(int n) {
        for(int i=1;i<=n;i++)
            dfs(0,i);
        vector<int> vec;
        for(auto x:res)
            vec.push_back(stoi(x));
        return vec;
    }
};
```

### 19.正则表达式匹配

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220402125704050.png" alt="image-20220402125704050" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220402125725158.png" alt="image-20220402125725158" style="zoom:80%;" />

```c++
class Solution {
public:
    bool isMatch(string s, string p) {
        int sn = s.size();
        int pn = p.size();
        vector<vector<bool>> dp(sn+1,vector<bool>(pn+1,false));
        //特殊情况:1.s和p都为空的时候 可以匹配
        //        2. p为空 s不为空 都为false
        dp[0][0] = true;
        //        3. s为空 p可以不为空
        //          此时做处理：
        for(int j = 1;j <= pn; ++j){
            if(p[j-1]=='*' && dp[0][j-2] == true)
                dp[0][j] = true;
        }

        for(int i = 1;i <= sn; ++i){
            for(int j = 1;j <= pn;j++){
                if(s[i-1] == p[j-1] || p[j-1] == '.')
                    dp[i][j] = dp[i-1][j-1];
                else if(p[j-1] == '*'){
                    if(p[j-2] != s[i-1] && p[j-2] != '.')
                        dp[i][j] = dp[i][j-2];
                    else
                        dp[i][j] = dp[i][j-2] || dp[i][j-1] || dp[i-1][j];
                }
            }
        }
        return dp[sn][pn];
    }
};
```

### 20.表示数值的字符串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220311182237723.png" alt="image-20220311182237723" style="zoom:80%;" />

```c++
class Solution {
    bool isin(string s,int& i){
        if(s[i]=='+'||s[i]=='-')
            i++;
        return isunin(s,i);
    }
    bool isunin(string s,int& i){
        int p = i;
        while(i<s.size()&&isdigit(s[i]))
            i++;
        return i>p;
    }
public:
    bool isNumber(string s) {
        int i = 0;
        int n = s.size();
        if(n == 0) return false;
        while(s[i]==' ')
            i++;
        bool res = isin(s,i);
        if(s[i]=='.'){
            i++;
            res = isunin(s,i) || res;
        }
        if(s[i]=='e'||s[i]=='E'){
            i++;
            res = isin(s,i) && res;
        }
        while(s[i]==' ') i++;
        return res && i==s.size();
    }
};
```

### 21.调整数组顺序使奇数位于偶数前面

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220311183359044.png" alt="image-20220311183359044" style="zoom:80%;" />

时间复杂度O(n)，空间复杂度O(1)

```c++
class Solution {
public:
    vector<int> exchange(vector<int>& nums) {
        int i=0,j=nums.size()-1;
        while(i<j){
            if(nums[i]%2==1){
                i++;
                continue;
            }
            if(nums[j]%2==0){
                j--;
                continue;
            }
            swap(nums[i],nums[j]);
            i++;
            j--;
        }
        return nums;
    }
};
```

### 26.树的子结构

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220312085602686.png" alt="image-20220312085602686" style="zoom:80%;" />



<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220312085530721.png" alt="image-20220312085530721" style="zoom:80%;" />

递归

```c++
class Solution {
private:
    bool dfs(TreeNode* A,TreeNode* B){
        if(!B)return true;
        if(!A)return false;
        if(A->val!=B->val)return false;
        return dfs(A->left,B->left)&&dfs(A->right,B->right);
    }
public:
    bool isSubStructure(TreeNode* A, TreeNode* B) {
        if(!A||!B)return false;
        return dfs(A,B)||isSubStructure(A->left,B)||isSubStructure(A->right,B);
    }
};
```

### 29.顺时针打印矩阵

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220312101057388.png" alt="image-20220312101057388" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220312101226965.png" alt="image-20220312101226965" style="zoom:80%;" />

```c++
class Solution {
private:
    int d[4][2]={{0,1},{1,0},{0,-1},{-1,0}};
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if(matrix.size()==0)return {};
        int rows=matrix.size();
        int columns=matrix[0].size();

        vector<vector<bool>> visited(rows,vector<bool>(columns,false));
        int total=rows*columns;
        vector<int> res(total);

        int row=0,column=0;
        int directionIndex=0;
        for(int i=0;i<total;i++){
            res[i]=matrix[row][column];
            visited[row][column]=true;

            int nextrow=row+d[directionIndex][0];
            int nextcolumn=column+d[directionIndex][1];
            if(nextrow<0||nextrow>=rows||nextcolumn<0||nextcolumn>=columns||visited[nextrow][nextcolumn])
            directionIndex=(directionIndex+1)%4;

            row+=d[directionIndex][0];
            column+=d[directionIndex][1];
        }
        return res;
    }
};
```

按照层模拟

```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if(matrix.size()==0)return {};
        int rows=matrix.size();
        int columns=matrix[0].size();

        vector<int> res;
        int left=0,right=columns-1,top=0,bottom=rows-1;
        while(left<=right&&top<=bottom){
            for(int i=left;i<=right;i++)
                res.push_back(matrix[top][i]);
            for(int i=top+1;i<=bottom;i++)
                res.push_back(matrix[i][right]);
            if(left<right&&top<bottom){
                for(int i=right-1;i>left;i--)
                    res.push_back(matrix[bottom][i]);
                for(int i=bottom;i>top;i--)
                    res.push_back(matrix[i][left]);
            }
            left++;
            right--;
            top++;
            bottom--;
        }
        return res;
    }
};
```

### 30.包含min的栈

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220402175412840.png" alt="image-20220402175412840" style="zoom:80%;" />

```c++
class MinStack {
private:
    stack<int> stk;
    stack<int> min_stk;
public:
    /** initialize your data structure here. */
    MinStack() {
        min_stk.push(INT_MAX);
    }
    
    void push(int x) {
        stk.push(x);
        min_stk.push(std::min(x,min_stk.top()));
    }
    
    void pop() {
        stk.pop();
        min_stk.pop();
    }
    
    int top() {
        return stk.top();
    }
    
    int min() {
        return min_stk.top();
    }
};
```

### 31.栈的压入弹出序列

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220313085214718.png" alt="image-20220313085214718" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220313085255158.png" alt="image-20220313085255158" style="zoom:80%;" />

```c++
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        stack<int> stk;
        int i=0;
        for(auto num:pushed){
            stk.push(num);
            while(!stk.empty()&&stk.top()==popped[i]){
                stk.pop();
                i++;
            }
        }
        return stk.empty();
    }
};
```

### 31.打印二叉树

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220324114738709.png" alt="image-20220324114738709" style="zoom:80%;" />

层序遍历：广度优先搜索

```c++
class Solution {
public:
    vector<int> levelOrder(TreeNode* root) {
        if(root==nullptr)return {};
        vector<int> res;
        queue<TreeNode*> q;
        q.push(root);

        while(!q.empty()){
            int size=q.size();
            for(int i=0;i<size;i++){
                TreeNode* node=q.front();
                q.pop();
                res.push_back(node->val);
                if(node->left)q.push(node->left);
                if(node->right)q.push(node->right);
            }
        }
        return res;
    }
};
```

层序遍历：深度优先搜索

### 32 - II. 从上到下打印二叉树 II

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220313091243678.png" alt="image-20220313091243678" style="zoom:80%;" />

广度优先搜索

```c++
    class Solution {
    public:
        vector<vector<int>> levelOrder(TreeNode* root) {
            if(!root)return {};
            vector<vector<int>> res;
            queue<TreeNode*> q;
            q.push(root);
            while(!q.empty()){
                vector<int> row;
                int size = q.size();
                for(int i=0;i<size;i++){
                    if(q.front()->left)q.push(q.front()->left);
                    if(q.front()->right)q.push(q.front()->right);
                    row.push_back(q.front()->val);
                    q.pop();    
                }
                res.push_back(row);
            }
            return res;
        }
    };
```

深度优先搜索（递归）

```c++
class Solution {
private:
    vector<vector<int>> res;
    void dfs(int depth,TreeNode* node){
        if(!node) return ;
        if(res.size()==depth)
            res.push_back(vector<int>());
        
        res[depth].push_back(node->val);
        dfs(depth+1,node->left);
        dfs(depth+1,node->right);
    }
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        dfs(0,root);
        return res;
    }
};
```

### 33.二叉搜索树的后序遍历序列

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220314082948636.png" alt="image-20220314082948636" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220314083002644.png" alt="image-20220314083002644" style="zoom:80%;" />

递归分治

```c++
class Solution {
private:
    bool recur(vector<int>& postorder,int i,int j){
        if(i>=j)return true;
        int p=i;
        while(postorder[p]<postorder[j])p++;
        int m=p;
        while(postorder[p]>postorder[j])p++;
        return p==j&&recur(postorder,i,m-1)&&recur(postorder,m,j-1);
    }
public:
    bool verifyPostorder(vector<int>& postorder) {
        return recur(postorder,0,postorder.size()-1);
    }
};
```

#### 辅助单调栈(真的看不懂的方法)

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220314083049252.png" alt="image-20220314083049252" style="zoom:80%;" />

```c++
class Solution {
public:
    bool verifyPostorder(vector<int>& postorder) {
        stack<int> stk;
        int root = 2147483647;
        for(int i = postorder.size() - 1 ; i >= 0 ; i--)
        {
            if(postorder[i] > root) return false;
            while(!stk.empty() && stk.top() > postorder[i])
            {
                root = stk.top();
                stk.pop();
            }
            stk.push(postorder[i]);
        }
        return true;
    }
}
```

### 35.复杂链表的复制

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220320123650381.png" alt="image-20220320123650381" style="zoom:80%;" />

回溯，哈希表:

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220323170209462.png" alt="image-20220323170209462" style="zoom:80%;" />

```c++
class Solution {
    unordered_map<Node*,Node*> oldNode_newNode;
public:
    Node* copyRandomList(Node* head) {
        if(!head) return nullptr;
        
        if(!oldNode_newNode.count(head)){
            Node* newNode = new Node(head->val);
            oldNode_newNode[head]=newNode;
            newNode->next=copyRandomList(head->next);
            newNode->random=copyRandomList(head->random);
        }
        return oldNode_newNode[head];
    }
};
```

迭代+节点拆分：

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220323172600675.png" alt="image-20220323172600675" style="zoom:80%;" />

```c++
class Solution {
public:
    Node* copyRandomList(Node* head) {
        Node* p = head;
        if(!p) return head;
        for(p;p!=nullptr;p=p->next->next){
            Node* newnode = new Node(p->val);
            newnode->next = p->next;
            p->next = newnode;
        }
        
        p = head;
        for(p;p!=nullptr;p=p->next->next){
            Node* p2 = p->next;
            p2->random = p->random==nullptr?nullptr:p->random->next;
        }
        
        Node* newhead = head->next;
        p = head;
        for(p;p!=nullptr;p=p->next){
            Node* p2 = p->next;
            p->next = p->next->next;
            p2->next = p2->next==nullptr?nullptr:p2->next->next;
        }
        return newhead;
    }
};
```

### 36.二叉搜索树与双向链表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220323174953630.png" alt="image-20220323174953630" style="zoom:80%;" />



<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220323175001362.png" alt="image-20220323175001362" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220323175118458.png" alt="image-20220323175118458" style="zoom:80%;" />

```c++
class Solution {
    Node* tail;
    Node* head;
    void dfs(Node* node){
        if(!node) return;
        dfs(node->left);
        if(tail==nullptr)
            head = node;
        else    
            tail->right = node;
        node->left = tail;
        tail = node;
        dfs(node->right);
    }
public:
    Node* treeToDoublyList(Node* root) {
        if(!root) return nullptr;
        dfs(root);
        head->left = tail;
        tail->right = head;
        return head;
    }
};
```

### 37.序列化二叉树和反序列化二叉树

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220324085950752.png" alt="image-20220324085950752" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220324090038260.png" alt="image-20220324090038260" style="zoom: 80%;" />

```c++
class Codec {
public:

    // 将二叉树前序遍历成字符串：例如"1,2,3,null,null,4,5,"
    void dfs(TreeNode* node,string& s){
        if(!node) {
            s+="null,";
            return;
        }
        s+=to_string(node->val)+",";
        dfs(node->left,s);
        dfs(node->right,s);
    }
    string serialize(TreeNode* root) {
        string res;
        dfs(root,res);
        cout<<res;
        return res;
    }
    TreeNode* dfs1(list<string>& l){
        if(l.front()=="null"){
            l.erase(l.begin());
            return nullptr;
        }
        TreeNode* node = new TreeNode(stoi(l.front()));
        l.erase(l.begin());
        node->left = dfs1(l);
        node->right = dfs1(l);
        return node;
    }
    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        list<string> l;
        string t;
        for(auto x:data){
            if(x!=','){
                t+=x;
            }
            else {
                if(t.size()!=0){
                    l.push_back(t);
                    t.clear();
                }
            }
        }
        if(t.size()!=0){
            l.push_back(t);
            t.clear();
        }
        return dfs1(l);
    }
};
```

### 38.字符串的排列

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220324092542993.png" alt="image-20220324092542993" style="zoom: 80%;" />

**1.回溯法：**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220324092604202.png" alt="image-20220324092604202" style="zoom:80%;" />

```c++
class Solution {
    vector<bool> vis;
    vector<string> res;
    void dfs(string& s,int index,string t){
        if(index==s.size()){
            res.push_back(t);
            return;
        }
        for(int i=0;i<s.size();i++){
            if(vis[i] || (i>0&&s[i]==s[i-1]&&!vis[i-1]))
                continue;
            
            t+=s[i];
            vis[i]=true;
            dfs(s,index+1,t);
            t.pop_back();
            vis[i]=false;
        }
    }
public:
    vector<string> permutation(string s) {
        vis = vector<bool>(s.size(),false);
        int n = s.size();
        sort(s.begin(),s.end());
        dfs(s,0,"");
        return res;
    }
};
```

**2.下一个排列：**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220324093610305.png" alt="image-20220324093610305" style="zoom:80%;" />

```c++
class Solution {
    bool next(string& s){
        int n = s.size();
        int i = n - 2;
        while(i>=0&&s[i]>=s[i+1])
            i--;
        if(i<0) return false;
        int j = n - 1;
        while(j>=0&&s[i]>=s[j])
            j--;
        swap(s[i],s[j]);
        reverse(s.begin()+i+1,s.end());
        return true;
    }
public:
    vector<string> permutation(string s) {
        sort(s.begin(),s.end());
        vector<string> res;
        do{
            res.push_back(s);
        }while(next(s));
        return res;
    }
};
```

### 39. 数组中出现次数超过一半的数字

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220324094404281.png" alt="image-20220324094404281" style="zoom:80%;" />

**1.哈希表**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220324094523019.png" alt="image-20220324094523019" style="zoom:80%;" />

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        unordered_map<int,int> map;
        for(auto& i:nums){
            if(map.count(i))
                map[i]++;
            else
                map[i]=1;
        }
        for(auto it=map.begin();it!=map.end();it++){
            if((*it).second>nums.size()/2)
                return (*it).first;
        }
        return 0;
    }
};
```

**2.排序**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220324094644979.png" alt="image-20220324094644979" style="zoom:80%;" />

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        return nums[nums.size()/2];
    }
};
```

**3.随机找一个索引**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220324095056004.png" alt="image-20220324095056004" style="zoom:80%;" />

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        while(true){
            int count=0;
            int index=rand()%nums.size();
            for(auto& i:nums){
                if(i==nums[index])
                    count++;
            }
            if(count>nums.size()/2){
                return nums[index];
            }
        }
        return 0;
    }
};
```

**4.分治**



**5.投票法**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220324111324683.png" alt="image-20220324111324683" style="zoom:80%;" />

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int t=-1;
        int count=0;
        for(auto& a:nums){
            if(t==a){
                count++;
            }
            else{
                count--;
                if(count<0){
                    t=a;
                    count=1;
                }
            }
        }
        return t;
    }
};
```

### 40.最小的k个数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220324112320960.png" alt="image-20220324112320960" style="zoom:80%;" />

**1.维护k个元素的最大堆**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220324112308523.png" alt="image-20220324112308523" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        priority_queue<int> q;
        vector<int> res;
        if(k==0)return res;
        for(int i=0;i<k;i++)
            q.push(arr[i]);
        for(int i=k;i<arr.size();i++){
            if(q.top()>arr[i]){
                q.pop();
                q.push(arr[i]);
            }
        }
        for(int i=0;i<k;i++){
            res.push_back(q.top());
            q.pop();
        }
        return res;
    }
};
```

**2.快速排序**

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220324114204304.png" alt="image-20220324114204304" style="zoom:80%;" />

```c++
class Solution {
    vector<int> res;
    int k;
    int partition(vector<int>& arr,int l,int r){
        swap(arr[l],arr[rand()%(r-l+1)+l]);
        int j=l;
        for(int i=l+1;i<=r;i++){
            if(arr[i]<arr[l])
                swap(arr[++j],arr[i]);
        }
        swap(arr[l],arr[j]);
        return j;
    }
    void quick_s(vector<int>& arr,int l,int r){
        if(l>r) return;
        int p = partition(arr,l,r);
        if(p<=k-1) res.push_back(arr[p]);
        quick_s(arr,l,p-1);
        quick_s(arr,p+1,r);
    }
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        this->k=k;
        srand(time(0));
        quick_s(arr,0,arr.size()-1);
        for(auto x:arr)
            cout<<x<<' ';
        return res;
    }
};
```

### 41.数据流中的中位数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220325083743674.png" alt="image-20220325083743674" style="zoom: 80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220325083840753.png" alt="image-20220325083840753" style="zoom:80%;" />

```c++
class MedianFinder {
    priority_queue<double,vector<double>,less<double>> p1;
    priority_queue<double,vector<double>,greater<double>> p2;
public:
    /** initialize your data structure here. */
    MedianFinder() {

    }
    
    void addNum(int num) {
        if(p2.size()>=p1.size()){
            p2.push(double(num));
            p1.push(p2.top());
            p2.pop();
        }
        else{
            p1.push(double(num));
            p2.push(p1.top());
            p1.pop();
        }
    }
    
    double findMedian() {
        if(p1.size()==p2.size())
            return (p1.top()+p2.top())/2;
        else if(p1.size()>p2.size())
            return p1.top();
        else 
            return p2.top();
    }
};
```

### 42.连续子数组的最大和

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220325084526750.png" alt="image-20220325084526750" style="zoom:80%;" />

1.动态规划

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        vector<int> res(nums.size(),0);
        res[0] = nums[0];
        for(int i=1;i<nums.size();i++){
            res[i] = max(nums[i],res[i-1]+nums[i]);
        }
        int t = res[0];
        for(auto x:res)
            t = max(t,x);
        return t;
    }
};
```

2.滚动数组

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220325084917950.png" alt="image-20220325084917950" style="zoom:80%;" />

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        if(nums.size()==0)return 0;
        int t=nums[0];
        int res=nums[0];
        for(int i=1;i<nums.size();i++){
            t=max(nums[i],t+nums[i]);
            res=max(res,t);
        }
        return res;
    }
};
```

3.分治

### 43.1～n 整数中 1 出现的次数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220325093801073.png" alt="image-20220325093801073" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220325093751556.png" alt="image-20220325093751556" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220325093740421.png" alt="image-20220325093740421" style="zoom:80%;" />

```c++
class Solution {
public:
    int countDigitOne(int n) {
        long long k = 1;
        long long res = 0;
        while(n >= k){
            res += (n/(k*10))*k+min(k,max(0LL,n%(k*10)-k+1));
            k*=10;
        }
        return res;
    }
};
```

### 44.数字序列中某一位的数字

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220325101814700.png" alt="image-20220325101814700" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220325101824961.png" alt="image-20220325101824961" style="zoom:80%;" />

```c++
class Solution {
public:
    int findNthDigit(long long n) {
        for(int i=1;;i++){
            if(n<i*pow(10,i)) return to_string(n/i)[n%i]-'0';
            n+=pow(10,i);
        }
        return -1;
    }
};
```

### 45.把数组排成最小的数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220325113730054.png" alt="image-20220325113730054" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220325113804021.png" alt="image-20220325113804021" style="zoom: 80%;" />

```c++
bool cmp(string a,string b){
    return a+b<b+a;
}
class Solution {
public:
    string minNumber(vector<int>& nums) {
        string res;
        vector<string> v;
        for(auto x:nums)
            v.push_back(to_string(x));

        sort(v.begin(),v.end(),cmp);
        for(auto x:v)
            res+=x;
        return res;
    }
};
```

### 46. 把数字翻译成字符串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220325124806164.png" alt="image-20220325124806164" style="zoom:80%;" />

滚动数组

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220325124923176.png" alt="image-20220325124923176" style="zoom:80%;" />

```c++
class Solution {
public:
    int translateNum(int num) {
        string s = to_string(num);
        int a=0,b=0,c=1;
        for(int i=0;i<s.size();i++){
            a=b;
            b=c;
            c=0;
            c+=b;
            if(i==0)continue;
            auto pre = stoi(s.substr(i-1,2));
            if(pre>=10&&pre<=25)
                c+=a;
        }
        return c;
    }
};
```

### 47.礼物的最大价值

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326084104061.png" alt="image-20220326084104061" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326084131010.png" alt="image-20220326084131010" style="zoom:80%;" />

```c++
class Solution {
public:
    int maxValue(vector<vector<int>>& grid) {
        int m=grid.size();
        int n=grid[0].size();

        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(i==0&&j==0)continue;
                else if(i==0&&j!=0)grid[i][j]+=grid[i][j-1];
                else if(i!=0&&j==0)grid[i][j]+=grid[i-1][j];
                else grid[i][j]+=max(grid[i][j-1],grid[i-1][j]);
            }
        }
        return grid[m-1][n-1];
    }
};
```

```c++
vector<vector<int>> p;
class Solution {
public:
	int res = INT_MIN;
	int maxValue(vector<vector<int>>& grid) {
		vector<vector<int>> v;
		dfs(grid, 0, 0, 0, v);
		return res;
	}
	void dfs(vector<vector<int>>& grid, int i, int j, int cnt, vector<vector<int>> v) {
		if (i < 0 || j < 0 || i >= grid.size() || j >= grid[0].size()) {
			return;
		}
		if (i == grid.size() - 1 && j == grid[0].size() - 1) {
			cnt += grid[i][j];
			if (cnt > res) {
				p = v;
				p.push_back({ i,j });
				res = cnt;
			}
			return;
		}
		cnt += grid[i][j];
		v.push_back({ i,j });
		dfs(grid, i, j + 1, cnt, v);
		dfs(grid, i + 1, j, cnt, v);
	}
};
```



### 48.最长不含重复字符的子字符串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326092605599.png" alt="image-20220326092605599" style="zoom:80%;" />

动态规划：

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char,int> map;
        int res=0;
        int tmp=0;
        for(int j=0;j<s.size();j++){
            if(!map.count(s[j])){
                tmp++;
            }
            else{
                int i=map[s[j]];
                if(j-i>tmp){
                    tmp++;
                }
                else{
                    tmp=j-i;
                }
            }
            map[s[j]]=j;
            res=max(res,tmp);
        }
        return res;
    }
};
```

双指针

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int f[128]={0};
        int max_len = 0;
        int l=0;
        int r=-1;
        while(l<s.size()){
            if(r+1<s.size()&&f[s[r+1]]==0)
                f[s[++r]]++;
            else
                f[s[l++]]--;
            max_len=max(max_len,r-l+1); 
        }
        return max_len;
    }
};
```

线性遍历

### 49.丑数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326094946655.png" alt="image-20220326094946655" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326094924431.png" alt="image-20220326094924431" style="zoom:80%;" />

动态规划

```c++
class Solution {
public:
    int nthUglyNumber(int n) {
        vector<int> f(n);
        f[0]=1;
        int p2=0;
        int p3=0;
        int p5=0;
        for(int i=1;i<n;i++){
            f[i]=min(f[p2]*2,min(f[p3]*3,f[p5]*5));
            if(f[i]==f[p2]*2) p2++;
            if(f[i]==f[p3]*3) p3++;
            if(f[i]==f[p5]*5) p5++;
        }
        return f[n-1];
    }
};
```

### 50.第一个只出现一次的字符

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326100345736.png" alt="image-20220326100345736" style="zoom:80%;" />

哈希表

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326100408417.png" alt="image-20220326100408417" style="zoom:80%;" />

```c++
class Solution {
public:
    char firstUniqChar(string s) {
        int n=s.size();
        unordered_map<char,int> map;
        for(int i=0;i<n;i++){
            if(map.count(s[i]))
                map[s[i]]++;
            else
                map[s[i]]=1;
        }
        for(auto ch:s){
            if(map[ch]==1)
                return ch;
        }
        return ' ';
    }
};
```

队列

### 51.求逆序对个数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326110022733.png" alt="image-20220326110022733" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326110036052.png" alt="image-20220326110036052" style="zoom:80%;" />

```c++
class Solution {
    int merge(vector<int>& nums,int l,int mid,int r){
        vector<int> t(r-l+1,0);
        for(int i=l;i<=r;i++)
            t[i-l]=nums[i];
        int res = 0;
        int i=l,j=mid+1;
        for(int k=l;k<=r;k++){
            if(i>mid){
                nums[k]=t[j-l];
                j++;
            }
            else if(j>r){
                nums[k]=t[i-l];
                i++;
            }
            else if(t[i-l]<=t[j-l]){
                nums[k]=t[i-l];
                i++;
            }
            else {
                nums[k]=t[j-l];
                j++;
                res+=mid-i+1;
            }
        }
        return res;
    }
    int merge_sort(vector<int>& nums,int l,int r){
        if(l>=r) return 0;
        int mid = (l+r)/2;        
        return merge_sort(nums,l,mid)+merge_sort(nums,mid+1,r)+merge(nums,l,mid,r);
    }
public:
    int reversePairs(vector<int>& nums) {
        return merge_sort(nums,0,nums.size()-1);
    }
};
```

### 52. 两个链表的第一个公共节点

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326111253945.png" alt="image-20220326111253945" style="zoom:80%;" />

双指针：

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326111326415.png" alt="image-20220326111326415" style="zoom:80%;" />

```c++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* a=headA;
        ListNode* b=headB;
        while(a!=b){
            a=(a==nullptr?headB:a->next);
            b=(b==nullptr?headA:b->next);
        }
        return b;
    }
};
```

哈希集合：

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326111419943.png" alt="image-20220326111419943" style="zoom:80%;" />

```c++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        unordered_set<ListNode*> set;
        ListNode* p=headA;
        while(p){
            set.insert(p);
            p=p->next;
        }
        p=headB;
        while(p){
            if(set.count(p))
                return p;
            p=p->next;
        }
        return nullptr;
    }
};
```

### 53.在排序数组中查找数字 I

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326113544270.png" alt="image-20220326113544270" style="zoom:80%;" />

二分查找：

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326113633708.png" alt="image-20220326113633708" style="zoom:80%;" />

```c++
class Solution {
    int floor(vector<int>& nums,int target){
        int n = nums.size();
        int l=-1;
        int r = n-1;
        while(l<r){
            int mid = (l+r+1)/2;
            if(nums[mid]>=target)
                r=mid-1;
            else
                l=mid;
        }
        if(l+1>=0&&l+1<n&&nums[l+1]==target)
            return l+1;
        return l;
    }
    int ceil(vector<int>& nums,int target){
        int n = nums.size();
        int l=0;
        int r = n;
        while(l<r){
            int mid = (l+r-1)/2;
            if(nums[mid]<=target)
                l=mid+1;
            else
                r=mid;
        }
        if(r-1>=0&&r-1<n&&nums[r-1]==target)
            return r-1;
        return r;
    }
public:
    int search(vector<int>& nums, int target) {
        int r=ceil(nums,target);
        int l=floor(nums,target);
        cout<<l<<"       "<<r<<endl;
        if(l==-1) return 0;
        if(nums[l]==target)return r-l+1;
        return 0;

    }
};
```

### 53.0～n-1中缺失的数字

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326115109102.png" alt="image-20220326115109102" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220326115122494.png" alt="image-20220326115122494" style="zoom:80%;" />

二分法

```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int i=0,j=nums.size()-1;
        while(i<=j){
            int m=(i+j)/2;
            if(nums[m]==m)i=m+1;
            else j=m-1;
        }
        return i;
    }
};
```

### 54.二叉搜索树的第k大节点

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220327085224964.png" alt="image-20220327085224964" style="zoom:80%;" />

1.递归

```c++
class Solution {
    int k1;
    int res;
    void dfs(TreeNode* node){
        if(!node) return;
        dfs(node->right);
        if(--k1==0) res = node->val;
        dfs(node->left);
    }
public:
    int kthLargest(TreeNode* root, int k) {
        k1=k;
        dfs(root);
        return res;
    }
};
```

2.vector存储

```c++
class Solution {
private:
    vector<int> res;
    void dfs(TreeNode* Node){
        if(Node==nullptr) return; 
        dfs(Node->right);
        if(Node)res.push_back(Node->val);
        dfs(Node->left);
    }
public:
    int kthLargest(TreeNode* root, int k) {
        dfs(root);
        return res[k-1];
    }
};
```

3.栈 迭代

### 55.二叉树的深度 I

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220327092149878.png" alt="image-20220327092149878" style="zoom:80%;" />

bfs

```c++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(!root)return 0;
        queue<TreeNode*> q;
        q.push(root);
        int res=0;
        while(!q.empty()){
            int size=q.size();
            for(int i=0;i<size;i++){
                TreeNode* node=q.front();
                q.pop();
                if(node->left)q.push(node->left);
                if(node->right)q.push(node->right);
            }
            res++;
        }
        return res;
    }
};
```

递归

```c++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(!root)return 0;
        return max(maxDepth(root->left),+maxDepth(root->right))+1;
    }
};
```

前中后序

### 55.平衡二叉树 Ⅱ

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220327093153222.png" alt="image-20220327093153222" style="zoom:80%;" />

从上往下递归

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220327093310387.png" alt="image-20220327093310387" style="zoom:80%;" />

```c++
class Solution {
    int height(TreeNode* node){
        if(!node)return 0;
        return max(height(node->left),height(node->right))+1;
    }
public:
    bool isBalanced(TreeNode* root) {
        if(!root) return true;
        return abs(height(root->left)-height(root->right))<=1 && isBalanced(root->left) 
                && isBalanced(root->right);
    }
};
```

从下往上递归(复杂度更小)

```c++
class Solution {
    int recur(TreeNode* node){
        if(!node) return 0;
        int left = recur(node->left);
        int right = recur(node->right);
        if(left==-1||right==-1)
            return -1;
        if(abs(left-right)<=1)
            return max(left,right)+1;
        else 
            return -1;
    }
public:
    bool isBalanced(TreeNode* root) {
        return recur(root)!=-1;
    }
};
```

### 56.数组中数字出现的次数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220328094524455.png" alt="image-20220328094524455" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<int> singleNumbers(vector<int>& nums) {
        int x=0,y=0,n=0,m=1;
        for(auto i:nums)
            n^=i;
        while((n&m)==0)
            m<<=1;
        for(auto i:nums){
            if(i&m) x^=i;
            else    y^=i;
        }
        return vector<int>{x,y};
    }
};
```

### 56.数组中数字出现的次数 II

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220329084003555.png" alt="image-20220329084003555" style="zoom:80%;" />

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int a=0,b=0;
        for(int i=0;i<nums.size();i++){
            a=a^nums[i] & ~b;
            b=b^nums[i] & ~a;
        }
        return a;
    }
};
```

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        vector<int> vec(31,0);
        for(int i=0;i<31;i++){
            for(auto x:nums){
                vec[i] += bitset<31>(x)[i];
            }
            vec[i]=vec[i]%3;
        }
        for(auto x:vec)
            cout<<x<<"   ";
        int res = 0;
        for(int i=0;i<31;i++)
            res+=vec[i]*pow(2,i);
        return res;
    }
};
```



### 57. 和为s的两个数字

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220329090710521.png" alt="image-20220329090710521" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n = nums.size();
        int i = 0;
        int j = n-1;
        while(i<j){
            if(nums[i]+nums[j]==target)
                return {nums[i],nums[j]};
            else if(nums[i]+nums[j]>target)
                j--;
            else
                i++;
        }
        return {-1,-1};
    }
};
```

### 57.和为s的连续正数序列

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220329091839363.png" alt="image-20220329091839363" style="zoom:80%;" />

双指针

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220329093556092.png" alt="image-20220329093556092" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<vector<int>> findContinuousSequence(int target) {
        vector<vector<int>> res;
        int l=1,r=2;
        while(l<=target/2){
            int sum = (l+r)*(r-l+1)/2;
            if(sum == target){
                vector<int> vec;
                for(int i=l;i<=r;i++)
                    vec.push_back(i);
                res.push_back(vec);
                r++;
            }
            else if(sum < target)
                r++;
            else
                l++;
        }
        return res;
    }
};
```

### 58.翻转单词顺序

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220329101411609.png" alt="image-20220329101411609" style="zoom:80%;" />

```c++
class Solution {
public:
    string reverseWords(string s) {
        int n = s.size();
        if(n==0) return s;
        string res;
        int r = n-1;
        while(r>=0){
            while(r>=0&&s[r]==' ')r--;
            if(r<0) break;
            int l = r;
            while(l>=0&&s[l]!=' ')l--;
            res+=s.substr(l+1,r-l)+" ";
            r=l;
        }
        if(res.size()!=0) res.pop_back();
        return res;
    }
};
```

### 58.Ⅱ左旋转字符串

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220329102323597.png" alt="image-20220329102323597" style="zoom:80%;" />

空间复杂度n

```c++
class Solution {
public:
    string reverseLeftWords(string s, int n) {
        string t = s;
        for(int i=0;i<s.size();i++)
            t[(i+s.size()-n)%(s.size())]=s[i];
        return t;
    }
};
```

空间复杂度1；

```c++
class Solution {
public:
    string reverseLeftWords(string s, int n) {
        reverse(s.begin(),s.begin()+n);
        reverse(s.begin()+n,s.end());
        reverse(s.begin(),s.end());
        return s;
    }
};
```

### 59.Ⅰ滑动窗口的最大值

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220329114403413.png" alt="image-20220329114403413" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220329114420389.png" alt="image-20220329114420389" style="zoom:80%;" />

核心思想，维护一个单调递减的双端队列，队首的索引是最大值，注意判断队首是不是还在区间之内。

```c++
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        if(nums.size()==0) return nums;
        deque<int> q;
        for(int i=0;i<k;i++){
            while(!q.empty()&&nums[i]>=nums[q.back()])
                q.pop_back();
            q.push_back(i);
        }
        vector<int> res = {nums[q.front()]};
        for(int i=k;i<nums.size();i++){
            while(!q.empty()&&nums[i]>=nums[q.back()])
                q.pop_back();
            q.push_back(i);
            while(q.front()<=i-k)
                q.pop_front();
            res.push_back(nums[q.front()]);
        }
        return res;
    }
};
```

### 59.Ⅱ队列的最大值

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220401090117678.png" alt="image-20220401090117678" style="zoom:80%;" />

**维护一个单调的双端队列**，来保存队列的最大值，注意“队列”是只能一端进一端出的。

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220401090144850.png" alt="image-20220401090144850" style="zoom:80%;" />

```c++
class MaxQueue {
    deque<int> d;
    queue<int> q;
public:
    MaxQueue() {

    }
    
    int max_value() {
        if(d.empty()) return -1;
        return d.front();
    }
    
    void push_back(int value) {
        while(!d.empty()&&value>d.back())
            d.pop_back();
        d.push_back(value);
        q.push(value);
    }
    
    int pop_front() {
        if(q.empty()) return -1;
        int res = q.front();
        if(d.front()==res)
            d.pop_front();
        q.pop();
        return res;
    }
};
```

### 60. n个骰子的点数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220401092444192.png" alt="image-20220401092444192" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220401092541998.png" alt="image-20220401092541998" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220401092527065.png" alt="image-20220401092527065" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220401092554664.png" alt="image-20220401092554664" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<double> dicesProbability(int n) {
        vector<double> dp(6,1.0/6.0);
        for(int i=2;i<=n;i++){
            vector<double> t(6*i-i+1,0);
            for(int k=0;k<6;k++){
                for(int j=0;j<dp.size();j++){
                    t[j+k]+=dp[j]/6.0;
                }
            }
            dp=t;
        }
        return dp;
    }
};
```

### 61.扑克牌中的顺子

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220401094951523.png" alt="image-20220401094951523" style="zoom:80%;" />

```c++
class Solution {
public:
    bool isStraight(vector<int>& nums) {
        int maxv = INT_MIN;
        int minv = INT_MAX;
        unordered_set<int> s1;
        for(auto x:nums){
            if(x==0)continue;
            if(s1.count(x)) return false;
            s1.insert(x);
            maxv = max(maxv,x);
            minv = min(minv,x);
            if(maxv-minv>4) return false;
        }
        return true;
    }
};
```

### 62.圆圈中最后剩下的数字

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220401105406964.png" alt="image-20220401105406964" style="zoom:80%;" />

```c++
class Solution {
public:
    int f(int n,int m){
        if(n==1)return 0;
        return (f(n-1,m)+m)%n;
    }
    int lastRemaining(int n, int m) {
        return f(n,m);
    }
}
```

```c++
class Solution {
public:
    int lastRemaining(int n, int m) {
        int f=0;		//n==1的时候 f==0
        for(int i=2;i<=n;i++){
            f=(f+m)%i;
        }
        return f;		//f是最终留下哪个数字
    }
};
```

### 63.股票的最大利润

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220401124554955.png" alt="image-20220401124554955" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220401124633454.png" alt="image-20220401124633454" style="zoom:80%;" />

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int p = 0;
        int minv = INT_MAX;
        for(auto x:prices){
            minv = min(minv,x);
            p = max(p,x-minv);
        }
        return p;
    }
};
```

### 64.求1 + 2 + 3 + ... + n

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220402172807490.png" style="zoom:80%;" />

逻辑符短路：

```c++
class Solution {
public:
    int sumNums(int n) {
        n && (n += sumNums(n-1));
        return n;
    }
};
```

### 65.不用加减乘除做加法

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220401122725647.png" alt="image-20220401122725647" style="zoom:80%;" />

```c++
class Solution {
public:
    int add(int a, int b) {
        while(b!=0){							//进位是与运算的结果左移一位
            int c=(unsigned int)(a&b)<<1;		//本位和是异或运算的结果
            a=a^b;
            b=c;
        }
        return a;
    }
};
```

### 66. 构建乘积数组

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220330092608981.png" alt="image-20220330092608981" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220330092628059.png" alt="image-20220330092628059" style="zoom:80%;" />

```c++
class Solution {
public:
    vector<int> constructArr(vector<int>& a) {
        int n=a.size();
        if(n==0)return a;
        vector<int> b(n,1);
        for(int i=1;i<n;i++){
            b[i]=b[i-1]*a[i-1];
        }
        int tmp=1;
        for(int i=n-2;i>=0;i--){
            tmp=tmp*a[i+1];
            b[i]=b[i]*tmp;
        }
        return b;
    }
};
```

### 67.把字符串转换成整数

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220330085238678.png" alt="image-20220330085238678" style="zoom:80%;" />

```c++
class Solution {
public:
    int strToInt(string str) {
        int res=0;
        int flag=1;
        int i=0;
        while(str[i]==' ')i++;
        if(str[i]=='-')flag=-1;
        if(str[i]=='-'||str[i]=='+')i++;
        for(;i<str.size()&&isdigit(str[i]);i++){
            if(res==INT_MAX/10 && int(str[i]-'0')>7)return flag==1?INT_MAX:INT_MIN;
            if(res>INT_MAX/10)return flag==1?INT_MAX:INT_MIN;
            res=res*10+int(str[i]-'0');  
        }
        return flag*res;
    }
};
```

## 力扣

### 679.24点游戏

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220507163337775.png" alt="image-20220507163337775" style="zoom:80%;" />

```c++
class Solution {
public:
    bool judgePoint24(vector<int>& cards) {
        vector<double> vec;
        for(auto x:cards)
            vec.push_back(double(x));
        return helper(vec);
    }
    bool helper(vector<double>& vec){
        if(vec.size() == 1) return abs(vec[0] - 24) < 1e-6;
        for(double num:vec){
            double a = vec[0];
            vec.erase(vec.begin());
            for(double num:vec){
                auto b = vec[0];
                vec.erase(vec.begin());
                for(auto n:{a+b,a-b,a*b}){
                    vec.push_back(n);
                    if(helper(vec)) return true;
                    vec.pop_back();
                }
                if(b!=0){
                    vec.push_back(a/b);
                    if(helper(vec)) return true;
                    vec.pop_back();
                }
                vec.push_back(b);
            }
            vec.push_back(a);
        }
        return false;
    }
};
```

