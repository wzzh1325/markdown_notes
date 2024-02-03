<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220419171143560.png" alt="image-20220419171143560" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220419171209075.png" alt="image-20220419171209075" style="zoom:80%;" />

# 0-1背包问题

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220419114458999.png" alt="image-20220419114458999" style="zoom: 50%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220419114640487.png" alt="image-20220419114640487" style="zoom: 50%;" />

贪心算法得不到全局最优解。

比如如下例子：

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220419114852736.png" alt="image-20220419114852736" style="zoom: 50%;" />



**F(n,C)  n个物品，放入容量位C的背包，使得F最大**

分为两种状态：

1.将第i个物品放入

2.无视第i个物品

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220419115229514.png" alt="image-20220419115229514" style="zoom: 50%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220419164104755.png" alt="image-20220419164104755" style="zoom:50%;" />

### 最简单的方法：

```c++
class Solution{
	//自顶向下
	//用[0.....index]的物品，填充容量为c的背包的最大值
	int optimal_value(const vector<int>& w, const vector<int>& v, int index, int c) {
		if (index < 0 || c <= 0)return 0;

		int res = optimal_value(w, v, index - 1, c);
		if (c >= w[index])
			res = max(optimal_value(w, v, index - 1, c - w[index]), res);

		return res;
	}
public:
	int knapsack01(const vector<int>& w, const vector<int>& v, int C) {
		int n = w.size();
		return optimal_value(w, v, n - 1, C);
	}
};

```

### 优化1：

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220419123518622.png" alt="image-20220419123518622" style="zoom: 50%;" />

以上存在大量重复计算，因此采用记忆化数组的方法

因为有两个约束条件：**最大价值**、**不超过容量**C。因此采用二维数组。

F[ i ][ j  表示0-i的物品，装填容量为j的背包，的最大价值

最终解就是F【n-1】【C】

```c++
class Solution{
	vector<vector<int>> F;
	//自顶向下
	//用[0.....index]的物品，填充容量为c的背包的最大值
	int optimal_value(const vector<int>& w, const vector<int>& v, int index, int c) {
		if (index < 0 || c <= 0)return 0;

		if (F[index][c] != -1)
			return F[index][c];

		int res = optimal_value(w, v, index - 1, c);
		if (c >= w[index])
			res = max(optimal_value(w, v, index - 1, c - w[index]), res);
		F[index][c] = res;

		return res;
	}
public:
	int knapsack01(const vector<int>& w, const vector<int>& v, int C) {
		int n = w.size();
		F = vector<vector<int>>(n, vector<int>(C + 1, -1));
		return optimal_value(w, v, n - 1, C);
	}
};
```

### 动态规划

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220419123518622.png" alt="image-20220419123518622" style="zoom: 50%;" />

```c++
class Solution{
public:
	int knapsack01(const vector<int>& w, const vector<int>& v, int C) {
		assert(w.size() == v.size());
		int n = w.size();
		if (n == 0)return 0;
		vector<vector<int>> f(n, vector<int>(C + 1, -1));
		//初始化第一行,先放第一个（索引为0的）物品
		for (int j = 0; j <= C; j++)
			f[0][j] = (j > w[0] ? v[0] : 0);
		//
		for (int i = 1; i < n; i++)
			for (int j = 0; j <= C; j++) {
				f[i][j] = f[i - 1][j];
				if (j >= w[i])
					f[i][j] = max(f[i - 1][j], v[i] + f[i - 1][j - w[i]]);
			}
		return f[n - 1][C];
	}
};
```

### 优化空间复杂度 为O(C)

:不需要二维数组，相当于只需要一行去更新，二位数组的每一行。f【C】为最终结果

```c++
class Solution{
public:
	int knapsack01(const vector<int>& w, const vector<int>& v, int C) {
		assert(w.size() == v.size());
		int n = w.size();
		if (n == 0)return 0;


		vector<int> f(C + 1, -1);
		//初始化第一行,先放第一个（索引为0的）物品
		for (int j = 0; j <= C; j++)
			f[j] = (j > w[0] ? v[0] : 0);
		//
		for (int i = 1; i < n; i++)
			for (int j = C; j >= w[i]; j--) {
				f[j] = max(f[j], v[i] + f[j - w[i]]);
			}
		return f[C];
	}
};
```

### 416.分割等和子集

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220508115033589.png" alt="image-20220508115033589" style="zoom:80%;" />

dp[ i ] [ j ] 表示，从索引[0] 到索引[i]中选取若干个物品，能否使其和恰好为j。

```c++
//dp[ i ] [ j ] 表示，从索引[0...i]中选取若干个物品，能否使其和恰好为j。
//分割成两个等和子集
//因此 这个和 就是 数组所有元素和的一半,因此数组中元素和一定为偶数
//背包问题：
//         数组中找出n个元素，使其和为 sum/2，其中0<n<nums.size()
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int n = nums.size();
        int sum = 0;
        for(int i = 0;i < n;i++)
            sum += nums[i];
        if(sum%2) return 0;
        int c = sum/2;

        vector<vector<bool>> dp(n,vector<bool>(c+1,false));

        //初始条件
        // j = 0;
        //找出n个元素使得和为0，是可以找出的因此为true
        for(int i=0;i<n;i++)
            dp[i][0] = true;
        //i = 0; 表示只有索引为0的元素可以选取，因此若容量j恰好等于nums[0]，则为true
        for(int j=0;j<=c;j++)
            dp[0][j] = (j == nums[0]);
        //dp
        for(int i = 1;i < n; i++){
            for(int j = 1;j <= c; j++){
                dp[i][j] = dp[i - 1][j];
                if(j >= nums[i]) dp[i][j] = dp[i][j] || dp[i - 1][j - nums[i]];
            }
        }
        return dp[n-1][c];
    }
};
```

简化：因为我们获得的最终结果为dp[n-1] [c]，因此只需要一行数组即可，然后不断一行行更新

```c++
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int n = nums.size();
        int sum = 0;
        for(int i = 0;i < n;i++)
            sum += nums[i];
        if(sum%2) return false;
        int c = sum/2;

        vector<bool> dp(c+1,false);

        //初始条件
        //从索引为0的这个元素，恰好和为0
        dp[0] = true;
        //
        for(int j = 1;j <=c ;j++)
            dp[j] = (j == nums[0]);

        //dp
        for(int i = 1;i < n; i++){
            for(int j = c;j >= nums[i]; j--){
                dp[j] = dp[j] || dp[j - nums[i]];
                //当前   //跳过i     //选择i
            }
        }
        return dp[c];
    }
};
```

### 474.一和零

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220508124002345.png" alt="image-20220508124002345" style="zoom:80%;" />

```c++
//子集长度 == 元素个数
//选取尽可能多的元素，使得子集中0的个数小于等于m，1的个数小于等于n
//dp[i][j][k] 表示从索引[0,i]中选取若干个元素组成的子集，在使得0的个数小于等于j，1的个数小于等于k的前提下，所选择元素个数的最大值。
// 
class Solution {
    pair<int,int> f(string s){
        int a = 0;
        int b = 0;
        for(auto c:s){
            if(c=='0') a++;
            else b++;
        }
        return make_pair(a,b);
    }
public:
    int findMaxForm(vector<string>& strs, int m, int n) {
        int sz = strs.size();
        vector<vector<vector<int>>> dp(sz,vector<vector<int>>(m+1,vector<int>(n+1,0)));
        //init
        //判断初始条件
        int a = 0;
        int b = 0;
        for(auto c:strs[0]){
            if(c=='0') a++;
            else b++;
        }
        //初始值
        //将strs[0]的放入 背包中，
        for(int j = 0;j <= m; j++){
            for(int k = 0;k <= n; k++){
                dp[0][j][k] = (j >=a && k >= b)?1:0;
            }
        }

        for(int i = 1;i < sz; i++){
            for(int j = 0;j <= m; j++){
                for(int k = 0;k <= n; k++){
                    dp[i][j][k] = dp[i - 1][j][k];//可以选择跳过
                    if(j >= f(strs[i]).first && k >= f(strs[i]).second)//若容量还满足，可以选择放入
                    dp[i][j][k] = max(dp[i][j][k],dp[i - 1][j - f(strs[i]).first][k - f(strs[i]).second] + 1); 
                }
            }
        }
        return dp[sz-1][m][n];
    }
};
```

简化为二位数组，因为我们要求的是矩阵索引最大的那个值，因此之前的值是不需要的，覆盖上次的值即可

```c++
//子集长度 == 元素个数
//选取尽可能多的元素，使得子集中0的个数小于等于m，1的个数小于等于n
//dp[i][j][k] 表示从索引[0,i]中选取若干个元素组成的子集，在使得0的个数小于等于j，1的个数小于等于k的前提下，所选择元素个数的最大值。
// 
class Solution {
    pair<int,int> f(string s){
        int a = 0;
        int b = 0;
        for(auto c:s){
            if(c=='0') a++;
            else b++;
        }
        return make_pair(a,b);
    }
public:
    int findMaxForm(vector<string>& strs, int m, int n) {
        int sz = strs.size();
        vector<vector<int>> dp(m+1,vector<int>(n+1,0));
        //init
        //判断初始条件

        //初始值
        //将strs[0]的放入 背包中，
        for(int j = 0;j <= m; j++){
            for(int k = 0;k <= n; k++){
                dp[j][k] = (j >= f(strs[0]).first && k >= f(strs[0]).second)?1:0;
            }
        }

        for(int i = 1;i < sz; i++){
            for(int j = m;j >= f(strs[i]).first; j--){
                for(int k = n;k >= f(strs[i]).second; k--){
                    dp[j][k] = max(dp[j][k],dp[j - f(strs[i]).first][k - f(strs[i]).second] + 1); 
                }
            }
        }
        return dp[m][n];
    }
};
```

### 494.目标和

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220508142611718.png" alt="image-20220508142611718" style="zoom:80%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220508142628418.png" alt="image-20220508142628418" style="zoom:80%;" />

```c++
//添加"+"的整数之和为a
//添加"-"的整数之和为b

//sum = a + b;
//target = a - b;

//a = (sum + target)/2;         a是整数，则(sum + target)/2也一定是整数
//b = (sum - target)/2;         b是整数，则(sum - target)/2也一定是整数

//因此问题转化为从nums数组中选取若干个元素，使其和为(sum + target)/2(或者(sum - target)/2),两者等价，因为选出来一部分，剩下一部分也就自动选出来了。

//dp[i][j] 表示从前i个数中，选取若干个元素，能使得元素和为j 的不同方案的个数
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int target) {
        int n = nums.size();
        int sum = 0;
        for(auto x:nums)
            sum += x;
        if((sum - target) < 0 || (sum - target) % 2 == 1) return 0;

        int c = (sum - target) / 2;
        vector<vector<int>> dp(n + 1,vector<int>(c + 1,0));

        //初始化
        //dp[0][0] 表示从前0个数中，选取若干个元素，能使得元素和为0 的不同方案的个数
        //前0个数中没有数，因此此时方案就一种【不选】,就可使元素和为0
        dp[0][0] = 1;

        for(int i = 1;i <= n; i++){
            for(int j = 0;j <= c;j++){
                dp[i][j] = dp[i-1][j];
                if(j >= nums[i - 1]) dp[i][j] += dp[i - 1][j - nums[i - 1]];
            }
        }
        return dp[n][c];
    }
};
```

879.

322.

518.

1449.

1049.

279.



### 1.01背包问题(每件物品只能选1次或0次）

有 N 件物品和一个容量是 V 的背包。每件物品只能使用一次。

第 i 件物品的体积是 vi，价值是 wi。

求解将哪些物品装入背包，可使这些物品的总体积不超过背包容量，且总价值最大。
输出最大价值。

**输入格式**

第一行两个整数，N，V，用空格隔开，分别表示物品数量和背包容积。

接下来有 N行，每行两个整数 vi,wi，用空格隔开，分别表示第 i 件物品的体积和价值。

**输出格式**

输出一个整数，表示最大价值。

**数据范围**

0<N,V≤1000
0<vi,wi≤1000

**输入样例**

```
4 5
1 2
2 4
3 4
4 5
```

**输出样例**：

```
8
```

```c++
#include <iostream>
#include <vector>
using namespace std;
int n;
int c;

int main(){
    cin>>n>>c;
    vector<int> w;
    vector<int> v;
    for(int i=0;i<n;i++){
        int a;
        int b;
        cin>>a>>b;
        w.push_back(a);
        v.push_back(b);
    }
    /*
    //二维写法
    //dp[i][j]表示将0....i个物品放入容量为j的背包中，在不超过体积j的情况下，获得的最大价值
    vector<vector<int>> dp(n,vector<int>(c+1,0));
    
    for(int j=0;j<=c;j++)
        dp[0][j] = j>=w[0]?v[0]:0;
    
    for(int i=1;i<n;i++){
        for(int j=0;j<=c;j++){
            dp[i][j] = dp[i-1][j];
            if(j>=w[i]) dp[i][j] = max(dp[i][j],dp[i-1][j-w[i]]+v[i]);
        }
    }
    cout<<dp[n-1][c]<<endl;
    */
    
    vector<int> dp(c+1,0);
    
    for(int j=0;j<=c;j++)
        dp[j] = j>=w[0]?v[0]:0;
    
    //这里要从大到小枚举；
    //这样的话，比如说我们计算容量为j的时候，要用到dp[j-w[i]]，而j-w[i]一定比j小，而我们是从大到小枚举的，因此在本轮(第i轮)计算dp[j]的时候,用到的dp[j-w[i]]在本轮一定还未计算过，因此它的值保存的是第i-1轮，也就是上次计算的结果，这就相当于二维情况下的dp[i-1][j-w[i]];
    
    //否则从小到大枚举的话，
    //比如说我们计算容量为j的时候，要用到dp[j-w[i]]，而j-w[i]一定比j小，而我们是从小到大枚举的，因此在本轮(第i轮)计算dp[j]的时候,用到的dp[j-w[i]]在本轮已经被计算过了，相当于二维的dp[i][j-w[i]]，也就是它是索引为i的物品有可能已经用过后的计算结果，而这正是完全背包的解法：在每一轮不超过容量的情况下，可以无限次使用索引为i的物品。
    for(int i=1;i<n;i++){
        for(int j=c;j>=w[i];j--){
            dp[j] = max(dp[j],dp[j-w[i]]+v[i]);
        }
    }
    cout<<dp[c]<<endl;
    
}
```

### 2.完全背包问题（每件物品都可选无限次）

有 N 种物品和一个容量是 V 的背包，每种物品都有无限件可用。

第 i 种物品的体积是 vi，价值是 wi。

求解将哪些物品装入背包，可使这些物品的总体积不超过背包容量，且总价值最大。
输出最大价值。

**输入格式**

第一行两个整数N，V，用空格隔开，分别表示物品种数和背包容积。

接下来有 N 行，每行两个整数 vi,wi，用空格隔开，分别表示第 i 种物品的体积和价值。

**输出格式**

输出一个整数，表示最大价值。

**数据范围**

0<N,V≤1000
0<vi,wi≤1000

**输入样例**

```
4 5
1 2
2 4
3 4
4 5
```

**输出样例**：

```
10
```

```c++
#include <iostream>
#include <vector>
using namespace std;
int n;
int c;
int main(){
    cin>>n>>c;
    vector<int> w(n);
    vector<int> v(n);
    for(int i=0;i<n;i++)    
        cin>>w[i]>>v[i];
    /*
    vector<vector<int>> dp(n,vector<int>(c+1,0));
    
    for(int j=0;j<=c;j++){
        for(int k=0;k*w[0]<=j;k++){
            dp[0][j]=j>=(k*w[0])?k*v[0]:0;
        }
    }

    for(int i=1;i<n;i++){
        for(int j=0;j<=c;j++){
            dp[i][j]=dp[i-1][j];
            if(j>=w[i])dp[i][j]=max(dp[i][j],dp[i][j-w[i]]+v[i]);
        }
    }
    
    cout<<dp[n-1][c]<<endl;
    */
    vector<int> dp(c+1,0);
    
    for(int j=0;j<=c;j++){
        for(int k=0;k*w[0]<=j;k++){
            dp[j]=j>=(k*w[0])?k*v[0]:0;
        }
    }

    for(int i=1;i<n;i++){
        for(int j=w[i];j<=c;j++){
            dp[j]=max(dp[j],dp[j-w[i]]+v[i]);
        }
    }
    
    cout<<dp[c]<<endl;
}
```

### 3.多重背包问题（每件物品都可选有限次）

### 4.混合背包问题（物品类型是前三种的组合）

### 5.二维费用背包问题

### 6.分组背包问题（将物品先分组，每个组内物品只能选其中一个）

### 7.背包问题求方案数

### 8.求背包问题的方案

### 9.有依赖的背包问题













# 哈希表

# 红黑树

# 平衡树

# B树

# kmp算法

问题，两个字符串s和p，求出p作为子串在s中出现的所有位置（索引（下标）），用一个数组来记录。

暴力怎么做

如何去优化

```c++
//求出字符串p的，pi函数：表示【最长公共前后缀的长度】
vector<int> pi_table(string p, vector<int>& pi) {
	pi.resize(p.size());
	pi[0] = 0;
	int len = 0;// p[0....i-1]中的最长公共前后缀长度，初始值为0
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
//第二步，kmp算法过程
vector<int> kmp(vector<int>& res, string s, string p) {
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
	return res;
}
```

# Manacher算法

寻找一个字符串中的回文串。

# floyd算法

# dijistra算法

# b-f算法

# prim算法

# Morris 遍历

# kruskal算法

# 图论：

图可以分为：无向图，有向图。无向图可以看作特殊的有向图，（每条边都是双向的）。

​						稠密图，稀疏图。（稠密、稀疏指的是边的数量的多少）

图的表示可以分为：邻接表、邻接矩阵

**邻接矩阵**:多用于表示稠密图

```c++
class DenseGraph {
	int n;	//节点个数
	int m;	//边个数
	bool d;	//是否是有向图
	vector<vector<bool>> g;
public:
	DenseGraph(int n, int d) {
		this->n = n;
		this->m = 0;
		this->d = d;
		for (int i = 0; i < n; i++)
			g.push_back(vector<bool>(n,false));
	}
	~DenseGraph(){}
	
	int V() { return n; }		//节点个数
	int E() { return m; }		//边个数

	void addEdge(int i, int j) {
		assert(i >= 0 && i < n);
		assert(j >= 0 && j < n);
		//这种实现方式，屏蔽了平行边，比如两节点之间有多条边
		//默认只有一条边
		if (hasEdge(i, j)) return;

		g[i][j] = 1;
		if (!d)g[j][i] = 1;

		m++;//[注意]***m此处对于无向图、有向图都是兼容的
	}

	bool hasEdge(int i, int j) {
		assert(i >= 0 && i < n);
		assert(j >= 0 && j < n);

		return g[i][j];
	}


};
```

**邻接表**:多用于表示稀疏图

```c++
class SparseGraph {
	int n;	//节点个数
	int m;	//边个数
	bool d;	//是否是有向图
	vector<vector<int>> g;
public:
	SparseGraph(int n, int d) {
		this->n = n;
		this->m = 0;
		this->d = d;
		for (int i = 0; i < n; i++)
			g.push_back({});
	}
	~SparseGraph() {}

	int V() { return n; }		//节点个数
	int E() { return m; }		//边个数

	void addEdge(int i, int j) {
		assert(i >= 0 && i < n);
		assert(j >= 0 && j < n);
		//这种实现方式，屏蔽了平行边，比如两节点之间有多条边
		//默认只有一条边
		//if (hasEdge(i, j)) return;
		//将上一句注释掉，即认为可以有平行边
		g[i].push_back(j);
		if (!d)g[j].push_back(i);

		m++;//[注意]***m此处对于无向图、有向图都是兼容的
	}

	bool hasEdge(int i, int j) {
		assert(i >= 0 && i < n);
		assert(j >= 0 && j < n);

		for (int it = 0; it < g[i].size(); it++)
			if (g[i][it] == j)
				return true;

		return false;
	}

};
```

深度优先遍历:获得路径

深度优先遍历获得的路径，只是由深度优先搜索得到的路径，但并不保证是最短路径。

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220512112916572.png" alt="image-20220512112916572" style="zoom:50%;" />

```c++
class ShortestPath {
private:
	vector<vector<int>> g;
	int s;
	int d;
	vector<int> vis;
	vector<int> from;
	void dfs(int v) {
		vis[v] = 1;
		for (auto i : g[v]){
			if (!vis[i]) {
				from[i] = v;
				dfs(i);
			}
		}
	}
public:
	ShortestPath(vector<vector<int>> g, int s,int d){
		this->d = d;
		this->g = g;
		this->s = s;
		vis = vector<int>(g.size(), 0);
		from = vector<int>(g.size(), -1);
		dfs(s);
	}
	void path() {
		if (d > g.size()) {
			cout << "not have the distination node  " << d << "  over" << endl;
			return;
		}
		if (vis[d] == 0) {
			cout << "not have path from" << s << "to" << d << endl;
			return;
		}
		vector<int> path;
		int p = d;
		stack<int> stk;
		while (p != -1) {
			stk.push(p);
			p = from[p];
		}
		while (!stk.empty()) {
			path.push_back(stk.top());
			stk.pop();
		}
		for (auto x : path)
			cout << x << endl;
	}
};
//
int main() {
	vector<vector<int>> g;
	g.resize(7);
	g[0] = { 1,2,5,6 };
	g[1] = { 0 };
	g[2] = { 0 };
	g[3] = { 4,5 };
	g[4] = { 3,5,6 };
	g[5] = { 0,3,4 };
	g[6] = { 0,4 };

	ShortestPath(g, 0, 6).path();
    //
}
```

![image-20220512113013183](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220512113013183.png)







<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220503145735922.png" alt="image-20220503145735922" style="zoom:80%;" />

DFS和BFS都可以对空间进行遍历。

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220503150218223.png" alt="image-20220503150218223" style="zoom:80%;" />

DFS不具有最短性，BFS有最短性。

DFS:回溯、剪枝。

DFS最重要的是顺序性，一棵树的形式（爆搜，遍历所有结果）

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220503150828427.png" alt="image-20220503150828427" style="zoom:50%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220503151104045.png" alt="image-20220503151104045" style="zoom:80%;" />

# 一、排序算法

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210212355598.png" alt="image-20220210212355598" style="zoom:80%;" />

![img](https://img-blog.csdnimg.cn/20181103104121942.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2tpbmdtYXg1NDIxMjAwOA==,size_16,color_FFFFFF,t_70)

![image-20220210211928069](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220210211928069.png)

## 冒泡排序

平均时间复杂度：O(n^2)

最好情况：O(n)(数组有序，第一次遍历后未发生元素交换，则直接跳出循环)

最坏情况：O(n^2)

空间复杂度：O(1)

原地排序：是，不需要开辟额外空间

稳定排序：是(因为比较的时候用了>，若使用>=，则成为非稳定排序)

### 1.

i表示遍历的次数，相邻元素两两比较，遍历n-1次，最后只剩一个元素不需要动。

```c++
void bubbleSort(vector<int>& vec) {
	int n = vec.size();
		for (int i = 1; i <=n-1 ; i++) 
			for (int j = 0; j <= n - 1 - i; j++) {
				if (vec[j] > vec[j + 1])
					swap(vec[j], vec[j + 1]);
			}
}
```

### 2.优化

遍历一次后，若未发生元素交换的话，说明数组已有序。

```c++
void bubbleSort(vector<int>& vec) {
	int n = vec.size();
	for (int i = 1; i <= n - 1; i++) {
		bool flag = true;
		for (int j = 0; j <= n - 1 - i; j++) {
			if (vec[j] > vec[j + 1]) {
				swap(vec[j], vec[j + 1]);
				flag = false;
			}
		}
		if (flag)break;
	}
}
```

## 选择排序

平均时间复杂度：O(n^2)

最好情况：O(n^2)

最坏情况：O(n^2)

空间复杂度：O(1)

原地排序：是，不需要开辟额外空间

不是稳定排序：因为每次交换的位置是不确定的，有可能与重复元素的相对位置发生改变。

### 1.

```c++
void selectSort(vector<int>& vec) {
	int n = vec.size();
	for (int i = 0; i < n - 1; i++) {
		int index = i;
		for (int j = i + 1; j < n; j++) {
			if (vec[j] < vec[index])
				index = j;
		}
		swap(vec[i], vec[index]);
	}
}
```

## 插入排序

平均时间复杂度：O(n^2)

最好情况：O(n)

最坏情况：O(n^2)

空间复杂度：O(1)

原地排序：是，不需要开辟额外空间

是稳定排序：元素比较的时候采用小于号，遇到重复元素时，不进行交换，保持相对顺序。

1.

```c++
void insertSort(vector<int>& vec) {
	int n = vec.size();
	for (int i = 1; i < n; i++) {
		for (int j = i; j>0 && vec[j]<vec[j - 1]; j--) {
			swap(vec[j], vec[j - 1]);
		}
	}
}
```

2.优化：将赋值取代swap，减少操作次数。

```c++
void insertSort(vector<int>& vec) {
	int n = vec.size();
	for (int i = 1; i < n; i++) {
		int e = vec[i];
		int j = i;
		for (j; j > 0&& e < vec[j - 1]; j--)
				vec[j] = vec[j - 1];
		vec[j - 1]=e;
	}
}
```

## 希尔排序

## 归并排序

### 自底向上：

```c++
	void merge(vector<int>& vec, int l, int mid, int r) {
		vector<int> tmp(r - l + 1, 0);
		int i = l;
        int mid = (r + l)/2;
        int j = mid + 1;
        int k = 0;
        while(i <= mid && j <= r){
            if(q[i] < q[j]) t[k++] = q[i++];
            else t[k++] = q[j++];
        }
        while(i <= mid)t[k++] = q[i++];
        while(j <= r) t[k++] = q[j++];
        
        for(int i = l,k = 0;i<=r;i++,k++) q[i] = t[k];
	}
	void merge_sort(vector<int>& vec) {
		for (auto size = 1; size <= vec.size(); size *= 2)
			for (auto i = 0; i + size < vec.size(); i += size * 2)
				merge(vec, i, i + size - 1, min(i + 2 * size - 1, int(vec.size() - 1)));
	}
```

### 自顶向下：

```c++
	void merge(vector<int>& vec, int l, int mid, int r) {
		vector<int> tmp(r - l + 1, 0);
		for (int i = l; i <= r; i++)
			tmp[i - l] = vec[i];
		int i = l;
		int j = mid + 1;
		for (int k = l; k <= r; k++) {
			if (i > mid) {
				vec[k] = tmp[j - l];
				j++;
			}
			else if (j > r) {
				vec[k] = tmp[i - l];
				i++;
			}
			else if (tmp[i - l] < tmp[j - l]) {
				vec[k] = tmp[i - l];
				i++;
			}
			else {
				vec[k] = tmp[j - l];
				j++;
			}
		}
	}
	void merge_Sort(vector<int>& vec, int l, int r) {
		if (l >= r)return;
		int mid = (r - l) / 2+ l;
		merge_Sort(vec, l, mid);
		merge_Sort(vec, mid + 1, r);
		merge(vec, l, mid, r);
	}
	void merge_sortUB(vector<int>& vec) {
		merge_Sort(vec, 0, vec.size() - 1);
	}
```

## 快速排序

### 单路快排

```c++
	int partition1(vector<int>& vec, int l, int r) {
		swap(vec[l], vec[rand() % (r - l + 1) + l]);
		
		int v = vec[l];

		int i = l;
		for (int j = l + 1; j <= r; j++) {
			if (vec[j] < v) {
				swap(vec[i + 1], vec[j]);
				i++;
			}
		}
		swap(vec[l], vec[i]);
		return i;
	}
	void quick_Sort1(vector<int>& vec, int l, int r) {
		if(l >= r)return;
		int p = partition1(vec, l, r);
		quick_Sort1(vec, l, p - 1);
		quick_Sort1(vec, p + 1, r);
	}
	void quick_sort1(vector<int>& vec) {
        srand(time(0));
		quick_Sort1(vec, 0, vec.size() - 1);
	}
```

### 两路快排

```c++
	int partition2(vector<int>& vec, int l, int r) {
		swap(vec[l], vec[rand() % (r - l + 1) + l]);

		int v = vec[l];

		int i = l + 1;
		int j = r;
		while (1) {
			while (i <= r && vec[i] < v)i++;
			while (j >= l + 1 && vec[j] > v)j--;
			if (i > j) break;
			swap(vec[i], vec[j]);
			i++;
			j--;
		}
		swap(vec[l], vec[j]);
		return j;
	}
	void quick_Sort2(vector<int>& vec, int l, int r) {
		if (l >= r)return;
		int p = partition2(vec, l, r);
		quick_Sort2(vec, l, p - 1);
		quick_Sort2(vec, p + 1, r);
	}
	void quick_sort2(vector<int>& vec) {
		srand(time(0));
		quick_Sort2(vec, 0, vec.size() - 1);
	}
```

### 三路快排

```c
	void quick_Sort3(vector<int>& vec, int l, int r) {
		if (l >= r)return;
		//partition
		swap(vec[l], vec[rands() % (r - l + 1) + l]);
		int v = vec[l];

		int lt = l;			//vec[l+1,......lt] < v
		int gt = r + 1;		//vec[gt.........r] > v
		int i = l + 1;		//vec[lt+1.......i) == v
		while (i < gt) {
			if (vec[i] < v) {
				swap(vec[i], vec[lt + 1]);
				lt++;
				i++;
			}
			else if (vec[i] > v) {
				swap(vec[i], vec[gt - 1]);
				gt--;
			}
			else
				i++;
		}
		swap(vec[l], vec[lt]);
		quick_Sort3(vec, l, lt - 1);
		quick_Sort3(vec, gt, r);
	}
	void quick_sort3(vector<int>& vec) {
		srand(time(0));
		quick_Sort3(vec, 0, vec.size() - 1);

```

## 堆排序

```c++
void shift_down(vector<int>& vec, int n, int i) {
	while (2 * i + 1 < n) {
		int j = 2 * i + 1; //先找左孩子

		if (j + 1 < n && vec[j + 1] > vec[j])
			j = j + 1;//右孩子更大的话，让右孩子和它交换

		if (vec[i] >= vec[j])//如果已经比孩子大了，不需要再操作了，跳出循环
			break;

		swap(vec[i], vec[j]);//交换
		i = j;					//将j位置作为k继续循环操作
	}
}
void heap_sort(vector<int>& vec) {
	int n = vec.size();
	//heapify首先将数组堆化。
	for (int i = (n - 2) / 2; i >= 0; i--)
		shift_down(vec, n, i);
	//将最大值放到末尾，然后将前边的新的数组重新堆化
	for (int i = n - 1; i >= 0; i--) {
		swap(vec[0], vec[i]);
		shift_down(vec, i, 0);
	}
}
```

## 计数排序

平均时间复杂度：O(n+k)

最好情况：O(n+k)

最坏情况：O(n+k)

空间复杂度：O(n+k)

原地排序：否，需要开辟额外空间

```c++
void count_sort(vector<int>& vec) {
	int max = INT_MIN;
	for (auto x : vec)
		if (x > max)max = x;
	vector<int> count(max + 1, 0);
	for (auto x : vec)
		count[x]++;
	vector<int> res;
	for (int i = 0; i <= max; i++)
		for (int j = 0; j < count[i]; j++)
			res.push_back(i);
	vec = vector<int>(res.begin(), res.end());
}
```

## 桶排序

## 基数排序

# 二、单链表的基本实现

```c++
//数据类型：节点
struct ListNode {
	int val;
	ListNode* next;
	ListNode() : val(0), next(nullptr) {}
	ListNode(int x) : val(x), next(nullptr) {}
	ListNode(int x, ListNode* next) : val(x), next(next) {}
};
//通过数组创建一个链表，返回这个链表的头节点
ListNode* createLinkedList(vector<int> vec, int n) {
	if (n == 0) return NULL;
	ListNode* head = new ListNode(vec[0]);

	ListNode* cur = head;
	for (int i = 1; i < n; i++) {
		cur->next = new ListNode(vec[i]);
		cur = cur->next;
	}
	return head;
}
//打印链表信息
void printLinkedList(ListNode* head) {
	ListNode* cur = head;
	while (cur) {
		cout << cur->val << " -> ";
		cur = cur->next;
	}
	cout << "NULL" << endl;
}
//删除链表，并释放链表的每个节点的内存
void deleteLinkedList(ListNode* head) {
	ListNode* curNode = head;
	while (curNode) {
		ListNode*  delNode= curNode;
		curNode = curNode->next;
		delete delNode;
	}
}
```

# 三、二叉树的基本概念

## 树节点：

```c++
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr) {}
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
  };
```

​								前序遍历								中序遍历									后序遍历

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220216184645148.png" alt="image-20220216184645148" style="zoom:50%;" />

# 四、二分搜索树

```c++
class BST {
	struct Node {
		Key key;
		Value value;
		Node* left;
		Node* right;

		Node(Key key, Value value) {
			this->key = key;
			this->value = value;
			this->left = nullptr;
			this->right = nullptr;
		}
	};
	Node* root;
	int count;
public:
	BST() {
		root = nullptr;
		count = 0;
	}
	~BST() {
		destory(root);
	}

	int size() {
		return count;
	}

	bool is_empty() {
		return count == 0;
	}

	/***************************************************/
	//插入新节点：若已经存在则更新value的值，否则新创建一个节点
	void insert(Key key,Value value) {
		root = insert(root, key, value);
	}
	//插入新节点，返回新树的根
	Node* insert(Node* node, Key key, Value value) {
		if (!node) {
			count++;
			Node* node = new Node(key, value);
		}
		if (node->key == key)
			node->value = value;
		else if (key < node->key)
			return insert(node->left, key, value);
		else if (key > node->key)
			return insert(node->right, key, value);

		return node;
	}
	/**********************************************/
	//判断树中是否有键值key
	bool contain(Key key) {
		return contain(root, key);
	}
	bool contain(Node* node, Key key) {
		if (key == node->key)
			return true;
		else if (key < node->key)
			return contain(node->left, key);
		else if (key > node->key)
			return contain(node->right, key);
		return false;
	}
	/*************************************************/
	//查找键值key，对应的value指针，不存在则返回空
	Value* search(Key key) {
		return search(root, key);
	}
	Value* search(Node* node, Key key) {
		if (key == node->key)
			return &(node->value);
		else if (key < node->key)
			return contain(node->left, key);
		else if (key > node->key)
			return contain(node->right, key);
		return nullptr;
	}
	/*************************************************/
	//前序遍历
	void preorder() {
		preorder(root);
	}
	void preorder(Node* node) {
		if (node) {
			cout << node->key << endl;
			preorder(node->left);
			preorder(node->right);
		}
	}
	/**************************************************/
	//中序遍历
	void inorder() {
		inorder(root);
	}
	void inorder(Node* node) {
		if (node) {
			inorder(node->left);
			cout << node->key << endl;
			inorder(node->right);
		}
	}
	/*************************************************/
	//后序遍历
	void postorder() {
		postorder(root);
	}
	void postorder(Node* node) {
		if (node) {
			postorder(node->left);
			postorder(node->right);
			cout << node->key << endl;
		}
	}
	/************************************************/
	//删除节点
	void destory(Node* node) {
		if (node) {
			destory(node->left);
			destory(node->right);
			delete node;
			count--;
		}
	}
	/*************************************************/
	//寻找最小的键值
	Key minimum() {
		return minimum(root)->key;
	}
	Node* minimum(Node* node) {
		if (!node->left)
			return node;
		return minimum(node->left);
	}
	/**************************************************/
	//寻找最大的键值
	Key maximum() {
		return maximum(root)->key;
	}
	Node* maximum(Node* node) {
		if (!node->right)
			return node;
		return minimum(node->right);
	}
	/**************************************************/
	//移除最小键值
	void removeMin() {
		if (root)
			root = removeMin(root);
	}
	Node* removeMin(Node* node) {
		if (!node->left) {
			Node* rightNode = node->right;
			delete node;
			count--;
			return rightNode;
		}
		node->left = removeMin(node->left);
		return node;
	}
	/**************************************************/
	//移除最大键值
	void removeMax() {
		if (root)
			root = removeMax(root);
	}
	Node* removeMax(Node* node) {
		if (!node->right) {
			Node* leftNode = node->left;
			delete node;
			count--;
			return leftNode;
		}
		node->right = removeMax(node->right);
		return node;
	}
	/**************************************************/
	//删除掉键值为key的节点,
	//		**
	//	   ****
	//		**
	//1.先找到键值为key的节点，若找不到，不需要操作，返回root
	//2.找到之后若左孩子为空，返回右孩子
	//		   若右孩子为空，返回左孩子
	//3.若左右孩子都存在：
	// (1)用左子树的最大值，代替node
	//	或者
	// (2)用右子树的最小值，代替node
	void remove(Key key) {
		root = remove(root, key);
	}
	Node* remove(Node* node, Key key) {
		if (!node) return node;
		if (key < node->key) {
			node->left = remove(node->left, key);
			return node;
		}
		else if (key > node->key) {
			node->right = remove(node->right, key);
			return node;
		}
		else {//key == node->key
			if (!node->left) {
				Node* rightNode = node->right;
				delete node;
				count--;
				return rightNode;
			}
			else if (!node->right) {
				Node* leftNode = node->left;
				delete node;
				count--;
				return leftNode;
			}
			else /*if (node->left && node->right)*/ {
				Node* tmp = new Node(minimum(node->right)->key, minimum(node->right)->value);
				count++;
				tmp->right = removeMin(node->right);
				tmp->left = node->left;
				delete node;
				count--;
				/*
				Node* tmp = new Node(maximum(node->left)->key,maximum(node->left)->value);
				count++;
				tmp->left = removeMax(node->left);
				tmp->right = node->right;
				delelte node;
				count--
				*/
				return tmp;
			}
		}
		return nullptr;
	}
};
```

# 五、最大堆

堆是完全二叉树。

对于从1为索引开始存储的，堆的数组，索引i满足

父结点：parent:	i / 2

左孩子：left:			2 * i

右孩子：right:		2 * i + 1

对于从0为索引开始存储的，堆的数组，索引i满足

父结点：parent:	(i - 1) / 2

左孩子：left:			2 * i + 1

右孩子：right:		2 * i + 2

```c++
template<typename Item>
class MaxHeap {
private:
	Item* data;		//数据成员数组
	int count;		//元素个数
	int capacity;	//最大容量

	//新加入一个节点之后，保持堆的性质。
	void shift_up(int k) {
		while (k > 1 && data[k / 2] < data[k])//是否到达根节点，并且父节点大于子结点，若是则上移
		{
			swap(data[k / 2], data[k]);
			k /= 2;
		}
	}
	//1是根节点
	//对于索引i，其左右子结点分别为2i，2i+1
	void shift_down(int k) {
		while (2 * k <= count) {		// 有左孩子，就一定有孩子
			int j = 2 * k; //先找左孩子

			if (j + 1 <= count && data[j + 1] > data[j])
				j = j + 1;//右孩子更大的话，让右孩子和它交换

			if (data[k] >= data[j])//如果已经比孩子大了，不需要再操作了，跳出循环
				break;

			swap(data[k], data[j]);//交换
			k = j;					//将j位置作为k继续循环操作
		}
	}
public:
    //构造函数1
	MaxHeap(int capacity) {
		data = new Item[capacity + 1];
		count = 0;
		this->capacity = capacity;
	}
    //构造函数2
	//heapify操作
	//将一个数组堆化
	//从第一个非叶子节点(位置为:count/2)开始直到根节点，执行shift_down操作即可
	MaxHeap(vector<Item> vec) {
		count = vec.size();
		capacity = 2 * vec.size();
		data = new Item[capacity + 1];

		for (int i = 0; i < count; i++)
			data[i + 1] = vec[i];

		for (int i = count / 2; i >= 1; i--)
			shift_down(i);
	}

	~MaxHeap() {
		delete[] data;
	}
	//返回元素个数
	int size() {
		return count;
	}
	//返回是否为空
	bool is_empty() {
		return count == 0;
	}
	//插入元素
	void insert(Item item) {

		//assert(count + 1 <= capacity);

		data[count + 1] = item;
		count++;
		shift_up(count);
	}
	//取出堆顶元素
	Item extract_max() {
		assert(count > 0);

		Item ret = data[1];

		swap(data[1], data[count]);
		count--;
		shift_down(1);
		return ret;
	}
};
```

# 六、并查集

## 版本一：

```c++
//并查集，顾名思义，一个集合，可以进行【合并】和【查找】的操作
//并查集中有多个子集，可以查找某个元素所处子集的id，
//						可以将几个元素合并到同一子集
class UnionFind {
	int* id;//id表示集合的id 0 1 2 .......
	int count;
public:
	UnionFind(int n) {
		count = n;
		id = new int[n];
		for (int i = 0; i < n; i++)
			id[i] = i;
	}
	~UnionFind() {
		delete[] id;
	}
	//查找元素所处的id，查为o(1);
	int find(int i) {
		return id[i];
	}
	//判断两个元素是否在同一子集
	bool isConnected(int i, int j) {
		return id[i] == id[j];
	}
	//合并两个元素到同一子集（此时，由于子集中元素是连通的，两个元素所处子集的所有元素都要合并）
	//并操作复杂度为o(n),需要遍历
	void unionElements(int p, int q) {
		if (id[p] == id[q])
			return;
		for (int i = 0; i < count; i++)
			if (id[i] == id[p])
				id[i] = id[q];
        	/*
        	if(id[i] == id[q])
        		id[i] = id[p];	两种均可，都是把q和p所在组的成员合并到一个组，只是id号不同。
        	*/
	}
};
```

## 版本二（最常用）：

 ```c++
//并查集，顾名思义，一个集合，可以进行【合并】和【查找】的操作
//并查集中有多个子集，可以查找某个元素所处子集的id，
//						可以将几个元素合并到同一子集
class UnionFind {
	int* parent;//记录每个索引的父结点
	int count;
public:
	UnionFind(int n) {
		count = n;
		parent = new int[n];
		for (int i = 0; i < n; i++)
			parent[i] = i;
	}
	~UnionFind() {
		delete[] parent;
	}
	//查找元素所处的id，查为o(1);
	int find(int i) {
		while (i != parent[i]) {
     		parent[i] = parent[parent[i]];
			i = parent[i];
		}
		return parent[i];
	//  return i;
	}
	//判断两个元素是否在同一子集
	bool isConnected(int i, int j) {
		return find(i) == find(j);
	}
	//合并两个元素到同一子集（此时，由于子集中元素是连通的，两个元素所处子集的所有元素都要合并）
	//并操作复杂度为o(n),需要遍历
	void unionElements(int p, int q) {
		if (find(q) == find(p))
			return;
		parent[find(p)] = find(q);
	}
};
 ```

基于size的优化：

```c++
//并查集，顾名思义，一个集合，可以进行【合并】和【查找】的操作
//并查集中有多个子集，可以查找某个元素所处子集的id，
//						可以将几个元素合并到同一子集
class UnionFind {
	int* parent;//id表示集合的id 0 1 2 .......
	int* sz;	//sz表示以索引i为根的树的大小(包含元素个数)
	int count;
public:
	UnionFind(int n) {
		count = n;
		parent = new int[n];
		sz = new int[n];
		for (int i = 0; i < n; i++) {
			parent[i] = i;
			sz[i] = 1;
		}
	}
	~UnionFind() {
		delete[] parent;
        delete[] sz;
	}
	//查找元素所处的id，查为o(1);
	int find(int i) {
		while (i != parent[i]) {
            parent[i] = parent[parent[i]];
			i = parent[i];
		}
		return parent[i];
	//  return i;
	}
	//判断两个元素是否在同一子集
	bool isConnected(int i, int j) {
		return find(i) == find(j);
	}
	//合并两个元素到同一子集（此时，由于子集中元素是连通的，两个元素所处子集的所有元素都要合并）
	//并操作复杂度为o(n),需要遍历
	void unionElements(int p, int q) {
		if (find(q) == find(p))
			return;
		if (sz[find(p)] < sz[find(q)]) {
			parent[find(p)] = find(q);
			sz[find(q)] += sz[find(p)];
		}
		else {
			parent[find(q)] = find(p);
			sz[find(p)] += sz[find(q)];
		}
	}
};
```

## 基于rank的优化

```c++
//并查集，顾名思义，一个集合，可以进行【合并】和【查找】的操作
//并查集中有多个子集，可以查找某个元素所处子集的id，
//						可以将几个元素合并到同一子集
class UnionFind {
	int* parent;//id表示集合的id 0 1 2 .......
	int* rank;	//rank表示以索引i为根的树的层数（高度大小）
	int count;
public:
	UnionFind(int n) {
		count = n;
		parent = new int[n];
		rank = new int[n];
		for (int i = 0; i < n; i++) {
			parent[i] = i;
			rank[i] = 1;
		}
	}
	~UnionFind() {
		delete[] parent;
		delete[] rank;
	}
	//查找元素所处的id，查为o(1);
	int find(int i) {
		while (i != parent[i]) {
			parent[i] = parent[parent[i]];
            i = parent[i];
		}
		return parent[i];
	//  return i;
	}
	//判断两个元素是否在同一子集
	bool isConnected(int i, int j) {
		return find(i) == find(j);
	}
	//合并两个元素到同一子集（此时，由于子集中元素是连通的，两个元素所处子集的所有元素都要合并）
	//并操作复杂度为o(n),需要遍历
	void unionElements(int p, int q) {
		if (find(q) == find(p))
			return;
		if (rank[find(p)] < rank[find(q)]) {
			parent[find(p)] = find(q);
		}
		else if (rank[find(p)] > rank[find(p)]) {
			parent[find(q)] = find(p);
		}
		else {
			parent[find(p)] = find(q);
			rank[find(q)] += 1;
		}
	}
};
```

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220223165952235.png" alt="image-20220223165952235" style="zoom: 50%;" />



<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220201174741293.png" alt="image-20220201174741293" style="zoom:33%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220201174828208.png" alt="image-20220201174828208" style="zoom:33%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220201175334871.png" alt="image-20220201175334871" style="zoom:33%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220201183302008.png" alt="image-20220201183302008" style="zoom:33%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220201183601662.png" alt="image-20220201183601662" style="zoom:33%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220201184233706.png" alt="image-20220201184233706" style="zoom:33%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220201184322502.png" alt="image-20220201184322502" style="zoom:33%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220201221532220.png" alt="image-20220201221532220" style="zoom:33%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220201221905931.png" alt="image-20220201221905931" style="zoom:33%;" />

主定理

一般：一个算法从头到尾运行的复杂度。

# 均摊复杂度：

有时候一个算法的复杂度高是为了其他的操作，这个比较高的算法复杂度会均摊到其他的算法复杂度中。

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220203090751895.png" alt="image-20220203090751895" style="zoom:33%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220203090815597.png" alt="image-20220203090815597" style="zoom:33%;" />

```c++
#include <iostream>
#include <cassert>
using namespace std;
template<typename T>
class myvector {
private:
	T* data;
	int capacity;
	int size;

	void resize(int newcapacity) {
		assert(newcapacity >= size);
		T* newData = new T[newcapacity];
		for (int i = 0; i < size; i++)
			newData[i] = data[i];
		delete[] data;

		data = newData;
		capacity = newcapacity;
	}
public:
	myvector() {
		data = new T[10];
		capacity = 10;
		size = 0;
	}
	~myvector() {
		delete[] data;
	}
	//添加元素
	void push_back(T e) {
		
		//assert(size < capacity);
		if (size == capacity)
			resize(2 * capacity);
		data[size++] = e;
	}
	//删除最后一个元素
	T pop_back() {
		assert(size > 0);
		T ret = data[size - 1];
		size--;
		if (size == capacity / 4)
			resize(capacity / 4);
		return ret;
	}
};
template<typename T>
T binarysearch(T* arr, int n, T target) {

	int l = 0;
	int r = n - 1;
	while (l <= r) {
		int mid = (r - l) / 2 + l;
		if (arr[mid] == target)
			return mid;
		else if (arr[mid] > target)
			r = mid - 1;
		else
			l = mid + 1;
	}
	return -1;
}
int main() {
	int arr[10] = { 1,2,3,3,4,4,5,5,6,6 };
	cout << binarysearch(arr, 10, 5) << endl;
	return 0;
}
```

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220207213032716.png" alt="image-20220207213032716" style="zoom:33%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220207213204738.png" alt="image-20220207213204738" style="zoom:33%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220207223348342.png" alt="image-20220207223348342" style="zoom:33%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220207222246989.png" alt="image-20220207222246989" style="zoom: 50%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220207222313542.png" alt="image-20220207222313542" style="zoom:33%;" />

哈希表的缺点：使得数据没有了顺序性。

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220217164155462.png" alt="image-20220217164155462" style="zoom: 50%;" />
