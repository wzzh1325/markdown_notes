## 1.快速排序

给定你一个长度为 n� 的整数数列。

请你使用快速排序对这个数列按照从小到大进行排序。

并将排好序的数列按顺序输出。

**输入格式**

输入共两行，第一行包含整数 n�。

第二行包含 n� 个整数（所有整数均在 1∼1091∼109 范围内），表示整个数列。

**输出格式**

输出共一行，包含 n� 个整数，表示排好序的数列。

**数据范围**

1≤n≤1000001≤�≤100000

**输入样例**：

```
5
3 1 2 4 5
```

输出样例：

```
1 2 3 4 5
```

```c++
#include <iostream>
#include <vector>
#include <string>
using namespace std;
void Quick_Sort1(vector<int>& arr, int l, int r)
{
	if (l >= r) return;
	swap(arr[l], arr[rand() % (r - l + 1) + l]);

	int j = l;
	for (int i = l + 1; i <= r; i++)
		if (arr[i] < arr[l])
			swap(arr[++j], arr[i]);
	swap(arr[l], arr[j]);

	Quick_Sort1(arr, l, j - 1);
	Quick_Sort1(arr, j + 1, r);
}
void Quick_Sort2(vector<int>& arr, int l, int r)
{
	if (l >= r) return;
	swap(arr[l], arr[rand() % (r - l + 1) + l]);

	int i = l + 1;
	int j = r;
	while (1)
	{
		while (i < j && arr[i] < arr[l]) i++;
		while (j >= l + 1 && arr[j] > arr[l])j--;
		if (i >= j) break;
		swap(arr[i++],arr[j--]);
	}
	swap(arr[l], arr[j]);

	Quick_Sort2(arr, l, j - 1);
	Quick_Sort2(arr, j + 1, r);
}
void Quick_Sort3(vector<int>& arr, int l, int r)
{
	if (l >= r) return;
	swap(arr[l], arr[rand() % (r - l + 1) + l]);

	int lt = l;
	int i = l + 1;
	int gt = r + 1;
	while (i < gt)
	{
		if (arr[i] < arr[l])
			swap(arr[++lt], arr[i++]);
		else if (arr[i] > arr[l])
			swap(arr[--gt], arr[i]);
		else
			i++;
	}
	
	swap(arr[l], arr[lt]);

	Quick_Sort3(arr, l, lt - 1);
	Quick_Sort3(arr, gt, r);
}
int main()
{
	int n; cin >> n;
	vector<int> arr(n, 0);
	for (auto& x : arr)
		cin >> x;
// 	Quick_Sort1(arr, 0, n - 1); //1会超时
 	Quick_Sort2(arr, 0, n - 1);
// 	Quick_Sort3(arr, 0, n - 1);
	for (auto& x : arr)
		cout << x << ' ';
}
```

## 2.第k大的数

给定一个长度为 n� 的整数数列，以及一个整数 k�，请用快速选择算法求出数列从小到大排序后的第 k� 个数。

**输入格式**

第一行包含两个整数 n� 和 k�。

第二行包含 n� 个整数（所有整数均在 1∼1091∼109 范围内），表示整数数列。

**输出格式**

输出一个整数，表示数列的第 k� 小数。

**数据范围**

1≤n≤1000001≤�≤100000,
1≤k≤n1≤�≤�

**输入样例**：

```
5 3
2 4 1 5 3
```

输出样例：

```
3
```

```c++
#include <iostream>
#include <vector>
#include <string>
using namespace std;
int Quick_Sort1(vector<int>& arr, int l, int r, int k)
{
 	if (l >= r) return l;
	swap(arr[l], arr[rand() % (r - l + 1) + l]);

	int j = l;
	for (int i = l + 1; i <= r; i++)
		if (arr[i] < arr[l])
			swap(arr[++j], arr[i]);
	swap(arr[l], arr[j]);
	if (k == j) return j;
	else if(k < j)
	    return Quick_Sort1(arr, l, j - 1, k);
	else
	    return Quick_Sort1(arr, j + 1, r, k);
}
int Quick_Sort2(vector<int>& arr, int l, int r, int k)
{
	if (l >= r) return l;
	swap(arr[l], arr[rand() % (r - l + 1) + l]);

	int i = l + 1;
	int j = r;
	while (1)
	{
		while (i <= r && arr[i] < arr[l]) i++;
		while (j >= l + 1 && arr[j] > arr[l])j--;
		if (i >= j) break;
		swap(arr[i++],arr[j--]);
	}
	swap(arr[l], arr[j]);
	if (k == j) return j;
	else if(k < j)
	    return Quick_Sort2(arr, l, j - 1, k);
	else
	    return Quick_Sort2(arr, j + 1, r, k);
}
int Quick_Sort3(vector<int>& arr, int l, int r, int k)
{
	if (l >= r) return l;
	swap(arr[l], arr[rand() % (r - l + 1) + l]);

	int lt = l;
	int i = l + 1;
	int gt = r + 1;
	while (i < gt)
	{
		if (arr[i] < arr[l])
			swap(arr[++lt], arr[i++]);
		else if (arr[i] > arr[l])
			swap(arr[--gt], arr[i]);
		else
			i++;
	}
	swap(arr[l], arr[lt]);
	if (k == lt) return lt;
	else if(k < lt)
	    return Quick_Sort3(arr, l, lt - 1, k);
	else
	    return Quick_Sort3(arr, lt + 1, r, k);
}
int main()
{
	int n; cin >> n;
	int k; cin >> k;
	vector<int> arr(n, 0);
	for (auto& x : arr)
		cin >> x;
// 	Quick_Sort1(arr, 0, n - 1, k - 1);
// 	Quick_Sort2(arr, 0, n - 1, k - 1);
// 	Quick_Sort3(arr, 0, n - 1, k - 1);
	cout << arr[Quick_Sort2(arr, 0, n - 1, k - 1)] << endl;
}
```

## 3.归并排序

给定你一个长度为 n� 的整数数列。

请你使用归并排序对这个数列按照从小到大进行排序。

并将排好序的数列按顺序输出。

**输入格式**

输入共两行，第一行包含整数 n�。

第二行包含 n� 个整数（所有整数均在 1∼1091∼109 范围内），表示整个数列。

**输出格式**

输出共一行，包含 n� 个整数，表示排好序的数列。

**数据范围**

1≤n≤1000001≤�≤100000

**输入样例**：

```
5
3 1 2 4 5
```

输出样例：

```
1 2 3 4 5
```

```c++
#include <iostream>
#include <vector>
#include <string>
using namespace std;
void Merge_Sort1(vector<int>& arr, int l, int r)
{
	if (l >= r) return;
	int mid = (l + r) >> 1;
	int i = l;
	int j = mid + 1;
	Merge_Sort1(arr, l, mid);
	Merge_Sort1(arr, mid + 1, r);
	
	int k = 0;
	vector<int> t(r - l + 1, 0);
	while (i <= mid && j <= r)
	{
		if (arr[i] < arr[j])t[k++] = arr[i++];
		else t[k++] = arr[j++];
	}
	while (i <= mid)t[k++] = arr[i++];
	while (j <= r)t[k++] = arr[j++];
	for (int i = l, k = 0; i <= r; i++, k++)arr[i] = t[k];
	
// 	Merge_Sort1(arr,l);
}
void merge(vector<int>& arr, int l, int mid, int r)
{
	if (l >= r) return;
	int i = l;
	int j = mid + 1;
	int k = 0;
	vector<int> t(r - l + 1, 0);
	while (i <= mid && j <= r)
	{
		if (arr[i] < arr[j])t[k++] = arr[i++];
		else t[k++] = arr[j++];
	}
	while (i <= mid)t[k++] = arr[i++];
	while (j <= r)t[k++] = arr[j++];
	for (int i = l, k = 0; i <= r; i++, k++)arr[i] = t[k];
}
void Merge_Sort2(vector<int>& arr)
{
	int n = arr.size();
	for (int size = 1; size < n; size *= 2)
		for (int l = 0; l + size < n; l += size * 2)
			merge(arr, l, l + size - 1, min(l + 2 * size - 1, n - 1));
}
int main()
{
	int n; cin >> n;
	vector<int> arr(n, 0);
	for (auto& x : arr)
		cin >> x;
	Merge_Sort1(arr, 0, n - 1);
// 	Merge_Sort2(arr);
	for (auto& x : arr)
		cout << x << ' ';
}
```

## 4.逆序对

给定一个长度为 n� 的整数数列，请你计算数列中的逆序对的数量。

逆序对的定义如下：对于数列的第 i� 个和第 j� 个元素，如果满足 i<j�<� 且 a[i]>a[j]�[�]>�[�]，则其为一个逆序对；否则不是。

**输入格式**

第一行包含整数 n�，表示数列的长度。

第二行包含 n� 个整数，表示整个数列。

**输出格式**

输出一个整数，表示逆序对的个数。

**数据范围**

1≤n≤1000001≤�≤100000，
数列中的元素的取值范围 [1,109][1,109]。

**输入样例**：

```
6
2 3 4 5 6 1
```

输出样例：

```
5
```

```c++
#include <iostream>
#include <vector>
#include <string>
using namespace std;
long long count = 0;
void Merge_Sort1(vector<int>& arr, int l, int r)
{
	if (l >= r) return;
	int mid = (l + r) >> 1;
	int i = l;
	int j = mid + 1;
	Merge_Sort1(arr, l, mid);
	Merge_Sort1(arr, mid + 1, r);
	
	int k = 0;
	vector<int> t(r - l + 1, 0);
	while (i <= mid && j <= r)
	{
		if (arr[i] <= arr[j])t[k++] = arr[i++];
		else {t[k++] = arr[j++];count += mid - i + 1;};
	}
	while (i <= mid)t[k++] = arr[i++];
	while (j <= r)t[k++] = arr[j++];
	for (int i = l, k = 0; i <= r; i++, k++)arr[i] = t[k];
	
// 	Merge_Sort1(arr,l);
}
void merge(vector<int>& arr, int l, int mid, int r)
{
	if (l >= r) return;
	int i = l;
	int j = mid + 1;
	int k = 0;
	vector<int> t(r - l + 1, 0);
	while (i <= mid && j <= r)
	{
		if (arr[i] <= arr[j])t[k++] = arr[i++];
		else {t[k++] = arr[j++];count += mid - i + 1;}
	}
	while (i <= mid)t[k++] = arr[i++];
	while (j <= r)t[k++] = arr[j++];
	for (int i = l, k = 0; i <= r; i++, k++)arr[i] = t[k];
}
void Merge_Sort2(vector<int>& arr)
{
	int n = arr.size();
	for (int size = 1; size < n; size *= 2)
		for (int l = 0; l + size < n; l += size * 2)
			merge(arr, l, l + size - 1, min(l + 2 * size - 1, n - 1));
}
int main()
{
	int n; cin >> n;
	vector<int> arr(n, 0);
	for (auto& x : arr)
		cin >> x;
	Merge_Sort1(arr, 0, n - 1);
// 	Merge_Sort2(arr);
	cout << count << ' ';
}
```

## 789.数的范围

![image-20240106110831576](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240106110831576.png)

![image-20240106110838613](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240106110838613.png)

```c++
#include <iostream>
#include <vector>
using namespace std;
int floor(vector<int>& arr, int x)
{
	int n = arr.size();
	int l = 0;
	int r = n - 1;
	while (l < r)
	{
		int mid = (l + r) >> 1;
		if (arr[mid] >= x) r = mid;
		else l = mid + 1;
	}
	if (arr[l] == x) return l;
	return -1;
}
int ceil(vector<int>& arr, int x)
{
	int n = arr.size();
	int l = 0;
	int r = n - 1;
	while (l < r)
	{
		int mid = (l + r + 1) >> 1;
		if (arr[mid] <= x) l = mid;
		else r = mid - 1;
	}
	if (arr[l] == x) return l;
	return -1;
}
int main()
{
	int n, m; cin >> n >> m;
	vector<int> arr(n);
	for (int i = 0; i < n; i++) cin >> arr[i];
	for (int i = 0; i < m; i++)
	{
	    int x; cin >> x;
		cout << floor(arr, x) << ' ' << ceil(arr, x) << endl;
    }
}
```

## 790.数的三次方根

给定一个浮点数 n�，求它的三次方根。

输入格式

共一行，包含一个浮点数 n�。

输出格式

共一行，包含一个浮点数，表示问题的解。

注意，结果保留 66 位小数。

数据范围

−10000≤n≤10000−10000≤�≤10000

输入样例：

```
1000.00
```

输出样例：

```
10.000000
```

```c++
#include <iostream>
#include <iomanip>
using namespace std;
int main()
{
    double x;cin >> x;
    double l = -10000, r = 10000;
    while(r - l > 10e-8)
    // for(int i = 0;i < 100; i++)
    {
        double mid = (l + r) / 2;
        if(mid * mid * mid > x) r = mid;
        else l = mid;
    }
    cout.setf(ios::fixed);
    cout <<setprecision(6)<< l << endl;
}
```

## 791.高精度加法

给定两个正整数（不含前导 00），计算它们的和。

输入格式

共两行，每行包含一个整数。

输出格式

共一行，包含所求的和。

数据范围

1≤整数长度≤1000001≤整数长度≤100000

输入样例：

```
12
23
```

输出样例：

```
35
```

```c++
#include <iostream>
#include <string>
#include <vector>
using namespace std;
void addition(string a, string b)
{
    vector<int> aa;
    vector<int> bb;
    int n1 = a.size();int n2 = b.size();
    for(int i = n1 - 1; i >= 0 ;i--) aa.push_back(a[i] - 48);
    for(int i = n2 - 1; i >= 0 ;i--) bb.push_back(b[i] - 48);
    vector<int> res;
    int cnt = 0;
    int i = 0;
    while(i < n1 || i < n2 || cnt != 0)
    {
        int x = (i < n1) ? aa[i] : 0;
        int y = (i < n2) ? bb[i] : 0;
        int sum = x + y + cnt;
        cnt = sum / 10;
        sum = sum % 10;
        res.push_back(sum);
        i++;
    }
    for(int i = res.size() - 1; i >= 0; i--) cout << res[i];

}
int main()
{
    string a, b;
    cin >> a >> b;
    addition(a, b);
}
```

**方法二**

```c++
#include <iostream>
#include <string>
#include <cctype>
#include <cstring>
using namespace std;
string addition(string a, string b)
{
    int i = a.size() - 1; 
    int j = b.size() - 1;
    string res = ""; 
    int cnt = 0;
    while(i >= 0 || j >= 0 || cnt != 0)
    {
        int x = i >= 0 ? (a[i--] - 48) : 0;
        int y = j >= 0 ? (b[j--] - 48) : 0;
        int sum = x + y + cnt;
        cnt = sum / 10;
        sum = sum % 10;
        res = to_string(sum) + res;
    }
    return res;
}
int main()
{
    string a, b;
    cin >> a >> b;
    cout << addition(a, b) << endl;;
}
```

## 792.高精度减法

给定两个正整数（不含前导 00），计算它们的差，计算结果可能为负数。

输入格式

共两行，每行包含一个整数。

输出格式

共一行，包含所求的差。

数据范围

1≤整数长度≤1051≤整数长度≤105

输入样例：

```
32
11
```

输出样例：

```
21
```

```c++
#include <iostream>
#include <string>
#include <vector>
using namespace std;
void subtraction(string a, string b)
{
    int f = 1;
    if(a.size() < b.size()) 
    {
        swap(a, b);
        f = -1;
    }
    if(a.size() == b.size())
        for(int i = 0;i < a.size(); i++)
        {
            if(a[i] > b[i]) break;
            else if(a[i] == b[i]) continue;
            else
            {
                swap(a, b);f = -1;
            }
        }
    vector<int> aa;
    vector<int> bb;
    for(int i = a.size() - 1;i >= 0; i--) aa.push_back(a[i] - 48);
    for(int i = b.size() - 1;i >= 0; i--) bb.push_back(b[i] - 48);
    int i = 0; 
    int cnt = 0;
    vector<int> res;
    while(i < a.size() || i < b.size() || cnt != 0)
    {
        int x = i < a.size() ? aa[i] : 0;
        int y = i < b.size() ? bb[i] : 0;
        if(x - y + cnt < 0)
        {
            res.push_back(x - y + cnt + 10);
            cnt = -1;
        }
        else
        {
            res.push_back(x - y + cnt);
            cnt = 0;
        }
        i++;
    }
    
    i = res.size() - 1;
    while(i >= 0 && res[i] == 0) i--;
    if(i == -1) cout << 0;
    else
    {
        if(f == -1) cout << '-';
        for(i;i >= 0; i--) cout << res[i];
    }


}
int main()
{
    string a, b;
    cin >> a >> b;
    // addition(a, b);
    subtraction(a, b);
    
}
```

## 793.高精度乘法

给定两个非负整数（不含前导 00） A� 和 B�，请你计算 A×B�×� 的值。

输入格式

共两行，第一行包含整数 A�，第二行包含整数 B�。

输出格式

共一行，包含 A×B�×� 的值。

数据范围

1≤A的长度≤1000001≤�的长度≤100000,
0≤B≤100000≤�≤10000

输入样例：

```
2
3
```

输出样例：

```
6
```

```c++
#include <iostream>
#include <algorithm>
#include <vector>
#include <string>
using namespace std;
void multiplication(string a, string b)
{
    vector<int> aa;
    for(int i = a.size() - 1;i >= 0;i--) aa.push_back(a[i] - 48);
    int bb = stoi(b);
    int cnt = 0;
    vector<int> res;
    int i = 0;
    while(i < (int)aa.size() || cnt != 0)
    {
        int product = aa[i] * bb + cnt;
        res.push_back(product % 10);
        cnt = product / 10;
        i++;
    }
    i = res.size() - 1;
    while(i >= 0 && res[i] == 0)i--;
    if(i == -1) cout << 0;
    else
    {
        for(i;i >= 0;i--)cout << res[i];
    }
}
void multiplication2(string a, string b)
{
    vector<int> aa;
    vector<int> bb;
    for(int i = a.size() - 1;i >= 0;i--) aa.push_back(a[i] - 48);
    for(int i = b.size() - 1;i >= 0;i--) bb.push_back(b[i] - 48);
    vector<int> res(a.size() + b.size());
    for(int i = 0;i < aa.size();i++)
        for(int j = 0;j < bb.size();j++)
            res[i + j] += aa[i] * bb[j];
    
    int cnt = 0;
    for(int i = 0;i < res.size();i++)
    {
        int product = res[i] + cnt;
        cnt = product / 10;
        res[i] = product % 10;
    }
    int i = res.size() - 1;
    while(i >= 0 && res[i] == 0)i--;
    if(i == -1) cout << 0;
    else
    {
        for(i;i >= 0;i--)cout << res[i];
    }
    
}
int main()
{
    string a, b; cin >> a >> b;
    multiplication2(a, b);
}
```

## 794.高精度除法

给定两个非负整数（不含前导 00） A，B�，�，请你计算 A/B�/� 的商和余数。

输入格式

共两行，第一行包含整数 A�，第二行包含整数 B�。

输出格式

共两行，第一行输出所求的商，第二行输出所求余数。

数据范围

1≤A的长度≤1000001≤�的长度≤100000,
1≤B≤100001≤�≤10000,
B� 一定不为 00

输入样例：

```
7
2
```

输出样例：

```
3
1
```

```c++
#include <iostream>
#include <string>
#include <vector>
using namespace std;
void division(string a, string b)
{
    vector<int> aa;
    for(int i = 0;i < (int)a.size();i++) aa.push_back(a[i] - 48);
    int bb = stoi(b);
    vector<int> res;
    int r = 0;
    for(int i = 0;i < (int)aa.size();i++)
    {
        res.push_back((r * 10 + aa[i]) / bb);
        r = (r * 10 + aa[i]) % bb;
    }
    int i = 0;
    while(i < (int)res.size() && res[i] == 0)i++;
    if(i == (int)res.size())
    {
        cout << 0 << '\n';
        cout << r << '\n';
    }
    else
    {
        for(i;i < (int)res.size();i++)
            cout << res[i];
        cout << '\n';
        cout << r;
    }
}
int main()
{
    string a;string b;
    cin >> a >> b;
    division(a, b);
}
```

## 795.前缀和

输入一个长度为 n� 的整数序列。

接下来再输入 m� 个询问，每个询问输入一对 l,r�,�。

对于每个询问，输出原序列中从第 l� 个数到第 r� 个数的和。

输入格式

第一行包含两个整数 n� 和 m�。

第二行包含 n� 个整数，表示整数数列。

接下来 m� 行，每行包含两个整数 l� 和 r�，表示一个询问的区间范围。

输出格式

共 m� 行，每行输出一个询问的结果。

数据范围

1≤l≤r≤n1≤�≤�≤�,
1≤n,m≤1000001≤�,�≤100000,
−1000≤数列中元素的值≤1000−1000≤数列中元素的值≤1000

输入样例：

```
5 3
2 1 3 6 4
1 2
1 3
2 4
```

输出样例：

```
3
6
10
```

```c++
#include <vector>
#include <iostream>
using namespace std;
int main()
{
    int n, m; cin >> n >> m;
    vector<int> arr(n + 1);
    for(int i = 1;i <= n; i++) cin >> arr[i];
    vector<int> s(n + 1);
    for(int i = 1;i <= n; i++) s[i] = s[i - 1] + arr[i];
    for(int i = 0;i < m; i++)
    {
        int l, r; cin >> l >> r;
        cout << s[r] - s[l - 1] << endl;
    }
}
```

## 796.子矩阵的和

输入一个 n� 行 m� 列的整数矩阵，再输入 q� 个询问，每个询问包含四个整数 x1,y1,x2,y2�1,�1,�2,�2，表示一个子矩阵的左上角坐标和右下角坐标。

对于每个询问输出子矩阵中所有数的和。

输入格式

第一行包含三个整数 n，m，q�，�，�。

接下来 n� 行，每行包含 m� 个整数，表示整数矩阵。

接下来 q� 行，每行包含四个整数 x1,y1,x2,y2�1,�1,�2,�2，表示一组询问。

输出格式

共 q� 行，每行输出一个询问的结果。

数据范围

1≤n,m≤10001≤�,�≤1000,
1≤q≤2000001≤�≤200000,
1≤x1≤x2≤n1≤�1≤�2≤�,
1≤y1≤y2≤m1≤�1≤�2≤�,
−1000≤矩阵内元素的值≤1000−1000≤矩阵内元素的值≤1000

输入样例：

```
3 4 3
1 7 2 4
3 6 2 8
2 1 2 3
1 1 2 2
2 1 3 4
1 3 3 4
```

输出样例：

```
17
27
21
```

```c++
#include <vector>
#include <iostream>
using namespace std;
int main()
{
    int n, m, q; cin >> n >> m >> q;
    vector<vector<int>> a(n + 1, vector<int>(m + 1, 0));
    for(int i = 1; i <= n; i++)
        for(int j = 1; j <= m; j++)
            cin >> a[i][j];
    vector<vector<int>> s(n + 1, vector<int>(m + 1, 0));
    for(int i = 1; i <= n; i++)
        for(int j = 1; j <= m; j++)
            s[i][j] = s[i][j - 1] + s[i - 1][j] - s[i - 1][j - 1] + a[i][j];
    for(int i = 0; i < q; i++)
    {
        int x1, y1, x2, y2;
        cin >> x1 >> y1 >> x2 >> y2;
        cout << s[x2][y2] - s[x2][y1 - 1] - s[x1 - 1][y2] + s[x1 - 1][y1 - 1] << endl;
    }
}
```

## 797.差分

输入一个长度为 n� 的整数序列。

接下来输入 m� 个操作，每个操作包含三个整数 l,r,c�,�,�，表示将序列中 [l,r][�,�] 之间的每个数加上 c�。

请你输出进行完所有操作后的序列。

输入格式

第一行包含两个整数 n� 和 m�。

第二行包含 n� 个整数，表示整数序列。

接下来 m� 行，每行包含三个整数 l，r，c�，�，�，表示一个操作。

输出格式

共一行，包含 n� 个整数，表示最终序列。

数据范围

1≤n,m≤1000001≤�,�≤100000,
1≤l≤r≤n1≤�≤�≤�,
−1000≤c≤1000−1000≤�≤1000,
−1000≤整数序列中元素的值≤1000−1000≤整数序列中元素的值≤1000

输入样例：

```
6 3
1 2 2 1 2 1
1 3 1
3 5 1
1 6 1
```

输出样例：

```
3 4 5 3 4 2
```

```c++
#include <vector>
#include <iostream>
using namespace std;
void insert(vector<int>& a, int l, int r, int x)
{
    a[l] += x;
    if(r + 1 >= a.size()); else a[r + 1] -= x;
}
int main()
{
    int n, m; cin >> n >> m;
    vector<int> s(n + 1);
    vector<int> a(n + 1);
    for(int i = 1; i <= n; i++) cin >> s[i];
    for(int i = 1; i <= n; i++) insert(a, i, i, s[i]);
    for(int i = 0; i < m; i++)
    {
        int l, r, x;
        cin >> l >> r >> x;
        insert(a, l, r, x);
    }
    for(int i = 1; i <= n; i++) a[i] += a[i - 1];
    for(int i = 1; i <= n; i++) cout << a[i] << ' ';
}
```

## 798.差分矩阵

![image-20230904224727524](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230904224727524.png)

![image-20230904224734632](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230904224734632.png)

```c++
#include <iostream>
#include <vector>
using namespace std;
void insert(vector<vector<int>>& a, int x1, int y1, int x2, int y2, int c)
{
    a[x1][y1] += c;
    if(y2 + 1 >= a[0].size()); else a[x1][y2 + 1] -= c;
    if(x2 + 1 >= a.size()); else a[x2 + 1][y1] -= c;
    if(x2 + 1 >= a.size() || y2 + 1 >= a[0].size()); else a[x2 + 1][y2 + 1] += c;
}
int main()
{
    int n, m, q; cin >> n >> m >> q;
    vector<vector<int>> s(n + 1, vector<int>(m + 1, 0));
    for(int i = 1; i <= n; i++)
        for(int j = 1; j <= m; j++)
            cin >> s[i][j];
    vector<vector<int>> a(n + 1, vector<int>(m + 1, 0));
    for(int i = 1; i <= n; i++)
        for(int j = 1; j <= m; j++)
            insert(a, i, j, i, j, s[i][j]);
    while(q--)
    {
        int x1, y1, x2, y2, c;
        cin >> x1 >> y1 >> x2 >> y2 >> c;
        insert(a, x1, y1, x2, y2, c);
    }
    for(int i = 1; i <= n; i++)
        for(int j = 1; j <= m; j++)
            a[i][j] += a[i - 1][j] + a[i][j - 1] - a[i - 1][j - 1];
    for(int i = 1; i <= n; i++)
    {   
        for(int j = 1; j <= m; j++)
            cout << a[i][j] << ' ';
        cout << endl;
    }
}
```

## 799.最长连续不重复子序列

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220609112901152.png" alt="image-20220609112901152" style="zoom:80%;" />

```c++
#include <iostream>
#include <vector>
using namespace std;
int f1(vector<int>& arr)
{
    int n = arr.size();
    int i = -1;
    int j = 0;
    int res = 0;
    int map[100010] = {0};
    while(j < n)
    {
        if(i + 1 < n && map[arr[i + 1]] == 0)
            map[arr[++i]]++;
        else
            map[arr[j++]]--;
        res = max(res, i - j + 1);
    }
    return res;
}
int f2(vector<int>& arr)
{
    int n = arr.size();
    int res = 0;
    int map[100001] = {0};
    for(int i = 0, j = 0; i < n; i++)
    {
        map[arr[i]]++;
        while(map[arr[i]] > 1)
            map[arr[j++]]--;
        res = max(res, i - j + 1);
    }
    return res;
}
int main()
{
    int n; cin >> n;
    vector<int> arr(n);
    for(int i = 0; i < n; i++) cin >> arr[i];
    // cout << f1(arr) << endl;
    cout << f2(arr) << endl;   
}
```

# 800.数组元素的目标和

![image-20240104233402412](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240104233402412.png)

![image-20240104233517983](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240104233517983.png)

```c++
#include <vector>
#include <iostream>
using namespace std;
pair<int,int> f1(vector<int>& arr1, vector<int>& arr2, int target)
{
    int n1 = arr1.size();
    int n2 = arr2.size();
    int i = 0;
    int j = n2 - 1;
    while(i < n1 && j >= 0)
    {
        if(arr1[i] + arr2[j] > target)
            j--;
        else if(arr1[i] + arr2[j] < target)
            i++;
        else
            return {i, j};
    }
    return {-1, -1};
}
pair<int,int> f2(vector<int>& arr1, vector<int>& arr2, int target)
{
    int n1 = arr1.size();
    int n2 = arr2.size();
    for(int i = 0, j = n2 - 1; i < n1; i++)
    {
        while(arr1[i] + arr2[j] > target && j - 1 >= 0) j--;
        if(arr1[i] + arr2[j] == target) return {i, j};
    }
    return {-1, -1};
}
int main()
{
    int n, m, t; cin >> n >> m >> t;
    vector<int> arr1(n);
    vector<int> arr2(m);
    for(int i = 0;i < n;i++) cin >> arr1[i];
    for(int i = 0;i < m;i++) cin >> arr2[i];
    // auto res = f1(arr1, arr2, t);
    auto res = f2(arr1, arr2, t);
    cout << res.first << ' ' << res.second << endl;
}
```

## 2816.判断子序列

![image-20230905175642373](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230905175642373.png)

![image-20230905175650987](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230905175650987.png)

```c++
#include <iostream>
#include <vector>
using namespace std;
bool f1(vector<int>& a, vector<int>& b)
{
    int i = 0;
    int j = 0;
    while(i < int(b.size()))
    {
        if(a[j] == b[i]) j++;
        if(j == int(a.size())) return true;
        i++;
    }
    return false;
}
bool f2(vector<int>& a, vector<int>& b)
{
    for(int i = 0, j = 0; i < int(b.size()); i++)
    {
        if(a[j] == b[i]) j++;
        if(j == int(a.size())) return true;
    }
    return false;
}
bool f3(vector<int>& a, vector<int>& b)
{
    int i = 0;
    int j = 0;
    while(i < a.size() && j < b.size())
    {
        if(a[i] == b[j]) i++;
        j++;
    }
    return i == a.size() ? true : false;
}
int main()
{
    int n, m; 
    cin >> n >> m;
    vector<int> a(n);
    vector<int> b(m);
    for(int i = 0;i < n;i++) cin >> a[i];
    for(int j = 0;j < m;j++) cin >> b[j];
    // string res =  f1(a, b) ? "Yes" : "No";
    // string res =  f2(a, b) ? "Yes" : "No";
    string res =  f3(a, b) ? "Yes" : "No";
    cout << res << endl;
}
```

## 801.二进制中1的个数

![image-20230905183307986](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230905183307986.png)

```c++
#include <bitset>
#include <iostream>
#include <vector>
using namespace std;
int f1(int n)
{
    int count = 0;
    while(n != 0)
    {
        if(n & 1) count++;
        n >>= 1;
    }
    return count; 
}
int f2(int n)
{
    return bitset<32>(n).count(); 
}
int f3(int n)
{
    int count = 0;
    while(n != 0)
    {
        count++;
        n &= n - 1;
    }
    return count; 
}
int f4(int n)
{
    int count = 0;
    while(n != 0)
    {
        count++;
        n -= (n & (~n + 1));
    }
    return count; 
}
int main()
{
    int n; cin >> n;
    vector<int> arr(n);
    for(int i = 0;i < n;i++) cin >> arr[i];
    // for(auto x:arr) cout << f1(x) << ' ';
    // for(auto x:arr) cout << f2(x) << ' ';
    // for(auto x:arr) cout << f3(x) << ' ';
    for(auto x:arr) cout << f4(x) << ' ';
}
```

## 802.区间和

![image-20230905204220863](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230905204220863.png)

![image-20230905204244965](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230905204244965.png)

```c++
#include <iostream>
#include <map>
#include <iterator>
using namespace std;
int main()
{
    map<int,int> mm;
    int n, m; cin >> n >> m;
    while(n--)
    {
        int index, x; cin >> index >> x;
        mm[index] += x;
    }
    for(auto it = ++mm.begin(); it != mm.end(); it++)
    {
        int tmp = (--it)->second;
        (++it)->second += tmp; 
    }
    while(m--)
    {
        int l, r; cin >> l >> r;
        cout << (--mm.upper_bound(r))->second - (--mm.lower_bound(l))->second << endl;
    }
}
```

## 803.合并区间

![image-20230905223129809](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230905223129809.png)

![image-20230905223141665](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230905223141665.png)

```c++
#include <iostream>
#include <map>
#include <vector>
#include <algorithm>
using namespace std;
int main()
{
    vector<vector<int>> a;
    int n; cin >> n;
    while(n--)
    {
        int l, r; cin >> l >> r;
        a.push_back({l,r});
    }
    sort(a.begin(), a.end());
    vector<vector<int>> res;
    res.push_back(a[0]);
    for(int i = 1; i < a.size(); i++)
    {
        if(res.back()[1] >= a[i][0])
            res.back()[1] = max(a[i][1], res.back()[1]);
        else
            res.push_back(a[i]);
    }
    cout << res.size() << endl;
}
```

# 数据结构（一）

## 826.单链表

![image-20230906190456615](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230906190456615.png)

![image-20230906190509641](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230906190509641.png)

```c++
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;
struct ListNode {
    int val;
    int rank;
    ListNode* next;
    ListNode(int val, int rank, ListNode* next):val(val), rank(rank), next(next){}
};
unordered_map<int,ListNode*> m;
// ListNode* find(ListNode* head, int k)
// {
//     ListNode* p = head;
//     while(p){
//         if(p->rank == k) return p;
//         p = p->next;
//     }
//     return nullptr;
// }
void print(ListNode* head)
{
    ListNode* p = head;
    while(p)
    {
        // cout << " (" << p->val << ' ' << p->rank << ") ";
        cout << p->val << ' ';
        p = p->next;
    }
    cout << '\n';
}
int main(){
    ListNode* head = nullptr;
    int n; cin >> n;
    int i = 0;
    while(n--)
    {
        char c; cin >> c;
        if(c == 'H')
        {
            i++;
            int x; cin >> x;
            ListNode* newhead = new ListNode(x, i, head);
            m[i] = newhead;
            head = newhead;
        }
        if(c == 'I')
        {
            i++;
            int k, x; cin >> k >> x;
            // ListNode* kthNode = find(head, k);
            ListNode* kthNode = m[k];
            ListNode* newNode = new ListNode(x, i, kthNode->next);
            m[i] = newNode;
            kthNode->next = newNode;
        }
        if(c == 'D')
        {
            int k; cin >> k;
            if(k == 0)
            {
                ListNode* delNode = head;
                head = head->next;
                m.erase(delNode->rank);
                delete delNode;
            }
            else
            {
                ListNode* kthNode = m[k];
                if(!kthNode->next->next)
                {
                    ListNode* delNode = kthNode->next;
                    kthNode->next = nullptr;
                    m.erase(delNode->rank);
                    delete delNode;
                }
                else
                {
                    ListNode* delNode = kthNode->next;
                    ListNode* newNext = kthNode->next->next;
                    kthNode->next = newNext;
                    m.erase(delNode->rank);
                    delete delNode;
                    
                }
            }
        }
    }
    print(head);
}
```

```c++
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;
struct ListNode {
    int val;
    int rank;
    ListNode* next;
    ListNode(int val, int rank, ListNode* next) :val(val), rank(rank), next(next) {}
};
void print(ListNode* head)
{
    ListNode* p = head;
    while (p)
    {
        // cout << " (" << p->val << ' ' << p->rank << ") ";
        cout << p->val << ' ';
        p = p->next;
    }
    cout << '\n';
}

ListNode* dummy_node = new ListNode(0, 0, nullptr);

unordered_map<int, ListNode*> m;

// 在第k个插入的数后面插入一个数 x
void I(int k, int i, int x)
{
    ListNode* kthNode = m[k];
    ListNode* newNode = new ListNode(x, i, kthNode->next);
    m[i] = newNode;
    kthNode->next = newNode;
}
// H和I的代码完全一致，只是k默认为0，即在第0个插入的元素后面，插入新元素
// 在第0个插入的数后面插入一个数 x
void H(int i, int x)
{
    I(0, i, x);
}
//  删除第k个插入的数
void D(int k)
{
    ListNode* kthNode = m[k];
    if (!kthNode->next->next)
    {
        ListNode* delNode = kthNode->next;
        kthNode->next = nullptr;
        m.erase(delNode->rank);
        delete delNode;
    }
    else
    {
        ListNode* delNode = kthNode->next;
        ListNode* newNext = kthNode->next->next;
        kthNode->next = newNext;
        m.erase(delNode->rank);
        delete delNode;
    }
}
int main() {
    int n; cin >> n;
    int i = 0; m[i] = dummy_node;
    while (n--)
    {
        char c; cin >> c;
        if (c == 'H')
        {
            i++;
            int x; cin >> x;
            H(i, x);
        }
        if (c == 'I')
        {
            i++;
            int k, x; cin >> k >> x;
            I(k, i, x);

        }
        if (c == 'D')
        {
            int k; cin >> k;
            D(k);
        }
    }
    print(dummy_node->next);
}
```

```c++
#include <iostream>
using namespace std;

const int N = 100000;

int head, e[N], ne[N], idx;

void H(int x)
{
    e[idx] = x;
    ne[idx] = head;
    head = idx;
    idx ++;
}

void I(int k, int x)
{
    e[idx] = x;
    ne[idx] = ne[k];
    ne[k] = idx;
    idx++;
}

void D(int k)
{
    ne[k] = ne[ne[k]];
}

int main()
{
    idx = 0;
    head = -1;
    int n; cin >> n;
    while(n--)
    {
        string s; cin >> s;
        if(s == "H")
        {
            int x; cin >> x;
            H(x);
        }
        if(s == "I")
        {
            int k, x; cin >> k >> x;
            I(k - 1, x);
        }
        if(s == "D")
        {
            int k; cin >> k;
            if(k == 0)
                head = ne[head];
            else
                D(k - 1);
        }
    }
    for(head; head != -1; head = ne[head])
        cout << e[head] << " ";
}
```

## 827.双链表

![image-20230907201713110](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230907201713110.png)

![image-20230907201725342](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230907201725342.png)

```c++
#include <iostream>
#include <unordered_map>
#include <climits>
using namespace std;
struct ListNode
{
    int val;
    int rank;
    ListNode* left;
    ListNode* right;
    ListNode(int val, int rank, ListNode* left, ListNode* right):val(val), rank(rank), left(left), right(right){}
};

unordered_map<int,ListNode*> m;
ListNode* dummy_head = new ListNode(0, 0, nullptr, nullptr);
ListNode* dummy_tail = new ListNode(0, INT_MAX, dummy_head, nullptr);

void D(int k)
{
    ListNode* kthNode = m[k];
    kthNode->left->right = kthNode->right;
    kthNode->right->left = kthNode->left;
    // m.erase(k);
    delete kthNode;
}
void IR(int k, int i, int x)
{
    ListNode* kthNode = m[k];
    ListNode* newNode = new ListNode(x, i, kthNode, kthNode->right);
    m[i] = newNode;
    kthNode->right->left = newNode;
    kthNode->right = newNode;
}
void IL(int k, int i, int x)
{
    ListNode* kthNode = m[k];
    ListNode* newNode = new ListNode(x, i, kthNode->left, kthNode);
    m[i] = newNode;
    kthNode->left->right = newNode;
    kthNode->left = newNode;
}
void R(int i, int x)
{
    IL(INT_MAX, i, x);
}
void L(int i, int x)
{
    IR(0, i, x);
}

void print(ListNode* dummy_head)
{
    int size = 0;
    ListNode* p = dummy_head->right;
    while(p != dummy_tail)
    { 
        size++;
        cout << p->val << ' '; 
        p = p->right;
    }
    // cout << '\n' << size << '\n';
}

int main()
{
    dummy_head->right = dummy_tail;
    m[0] = dummy_head;
    m[INT_MAX] = dummy_tail;
    
    int n; cin >> n;
    int i = 0;
    while(n--){
        string s; cin >> s;
        if(s == "D")
        {
            int k; cin >> k;
            D(k);
        }
        if(s == "L")
        {
            i++;
            int x; cin >> x;
            L(i, x);
        }
        if(s == "R")
        {
            i++;
            int x; cin >> x;
            R(i, x);
        }
        if(s == "IL")
        {
            i++;
            int k, x; cin >> k >> x;
            IL(k, i, x);
        }
        if(s == "IR")
        {
            i++;
            int k, x; cin >> k >> x;
            IR(k, i, x);
        }
    }
    print(dummy_head);
}
```

## 3302.表达式求值

![image-20230907201636683](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230907201636683.png)

```c++
#include <iostream>
#include <vector>
using namespace std;
int compute(string s, int l, int r)
{
    int num = 0;
    char op = '+';
    vector<int> res;
    for(int i = l; i <= r; i++)
    {
        if(s[i] == ' ') continue;
        if(isdigit(s[i])) num = num * 10 + (s[i] - 48);
        if(s[i] == '(')
        {
            int j = i + 1;
            int cnt = 1;
            while(cnt)
            {
                if(s[j] == '(') cnt++;
                if(s[j] == ')') cnt--;
                j++;
            }
            num = compute(s, i + 1, j - 2);
            i = j;
        }
        if(!isdigit(s[i]) || i == r)
        {
            switch (op)
            {
                case '+': res.push_back(num);break;
                case '-': res.push_back(-1 * num);break;
                case '*': res.back() *= num;break;
                case '/': res.back() /= num;break;
            }
            op = s[i];
            num = 0;
        }
    }
    int sum = 0;
    for(auto x:res) sum += x;
    return sum;
}
int main()
{
    string s; getline(cin, s);
    cout << compute(s, 0, s.size() - 1);
}
```

## 828.模拟栈

![image-20230906205338262](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230906205338262.png)

![image-20230906205356328](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230906205356328.png)

```c++
#include <iostream>
using namespace std;
class stk
{
private:
    int a[1000000];
    int index;
public:
    stk(int index)
    {
        this->index = index;
        for(int i = 0;i < 1000000;i++)
            this->a[i] = 0;
    }
    void push(int x)
    {
        a[index++] = x;
    }
    void pop()
    {
        a[--index] = 0;
    }
    int query()
    {
        int i = index - 1;
        return a[i];
    }
    bool empty()
    {
        return a[0] == 0;
    }
};
int main()
{
    int n; cin >> n;
    stk s(0);
    while(n--)
    {
        string str; cin >> str;
        if(str == "pop") 
            s.pop();
        if(str == "push")
        {
            int x; cin >> x;
            s.push(x);
        }
        if(str == "query")
            cout << s.query() << endl;
        if(str == "empty")
            cout << (s.empty() ? "YES" : "NO") << endl;
    }   
}
```

## 829.模拟队列

![image-20230907201511974](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230907201511974.png)

![image-20230907201524085](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230907201524085.png)

```c++
#include <iostream>
using namespace std;
class Queue
{
private:
    int a[1000000];
    int l;
    int r;
public:
    Queue()
    {
        this->l = 0;
        this->r = -1;
        for(int i = 0; i <= 1000000; i++)
            a[i] = 0;
    }
    void push(int x)
    {
        a[++r] = x;
    }
    void pop()
    {
        a[l++] = 0;
    }
    int query()
    {
        return this->a[l];
    }
    bool empty()
    {
        return l > r;
    }
};
int main()
{
    int n; cin >> n;
    Queue q;
    while(n--)
    {
        string s; cin >> s;
        if(s == "push")
        {
            int x; cin >> x;
            q.push(x);
        }
        if(s == "pop")
        {
            q.pop();
        }
        if(s == "empty")
        {
            cout << (q.empty() ? "YES" : "NO") << endl;
        }
        if(s == "query")
        {
            cout << q.query() << endl;
        }
    }
}
```

```c++
#include <iostream>
using namespace std;

const int N = 100010;

int q[N], hh, tt;

int main()
{
    int m; cin >> m;
    hh = 0; 
    tt = -1;
    
    while(m--)
    {
        string s; cin >> s;
        if(s == "push")
        {
            int x; cin >> x;
            q[++tt] = x;
        }
        if(s == "pop")
        {
            hh++;
        }
        if(s == "query")
            cout << q[hh] << endl;
        if(s == "empty")
            cout << (tt >= hh ? "NO" : "YES") << endl;
    }
}
```

## 830.单调栈

![image-20230908172736916](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230908172736916.png)

```c++
#include <vector>
#include <iostream>
#include <stack>
using namespace std;
//  纯暴力解法
vector<int> f1(vector<int>& arr)
{
    vector<int> res;
    int n = arr.size();
    for(int i = 0; i < n; i++)
    {
        int j = i - 1;
        for(j; j >= 0; j--)
        {
            if(arr[j] >= arr[i]) break;
        }
        if(j == -1) res.push_back(-1);
        else res.push_back(arr[j]);
    }
    return res;
}
//  也是暴力
vector<int> f2(vector<int>& arr)
{
    vector<int> res;
    int n = arr.size();
    for(int i = 0; i < n; i++)
    {
        if(i - 1 >= 0 && arr[i - 1] == -1 && arr[i] <= arr[i - 1]) 
        {
            res.push_back(-1);
            continue;
        }
        int j = i - 1;
        for(j; j >= 0; j--)
        {
            if(arr[j] < arr[i]) break;
        }
        if(j == -1) res.push_back(-1);
        else res.push_back(arr[j]);
    }
    return res;
}
//	单调栈
vector<int> f3(vector<int>& arr)
{
    int n = arr.size();
    stack<int> stk;
    vector<int> res;
    for(int i = 0; i < n; i++)
    {
        while(!stk.empty() && stk.top() >= arr[i])
            stk.pop();
        if(stk.empty()) res.push_back(-1);
        else res.push_back(stk.top());
        stk.push(arr[i]);
    }
    return res;
}
int main()
{
    int n; cin >> n;
    vector<int> arr(n);
    for(int i = 0; i < n; i++) cin >> arr[i];
    // vector<int> res = f1(arr);
    // vector<int> res = f2(arr);
    vector<int> res = f3(arr);
    for(auto x:res) cout << x << ' ';
}
```

## 154.滑动窗口

![image-20230909200103522](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230909200103522.png)

![image-20230909200114474](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230909200114474.png)

```c++
#include <iostream>
#include <vector>
#include <queue>
using namespace std;
vector<int> f_min(vector<int>& arr, int k)
{
    int n = arr.size();
    deque<int> dq;
    vector<int> res;
    for(int i = 0; i < n; i++)
    {
        while(!dq.empty() && arr[i] <= arr[dq.back()])
            dq.pop_back();
        while(!dq.empty() && dq.front() < i - k + 1)
            dq.pop_front();
        dq.push_back(i);
        if(i >= k - 1)res.push_back(arr[dq.front()]);
    }
    return res;
}
vector<int> f_max(vector<int>& arr, int k)
{
    int n = arr.size();
    deque<int> dq;
    vector<int> res;
    for(int i = 0; i < n; i++)
    {
        while(!dq.empty() && arr[i] >= arr[dq.back()])
            dq.pop_back();
        while(!dq.empty() && dq.front() < i - k + 1)
            dq.pop_front();
        dq.push_back(i);
        if(i >= k - 1)res.push_back(arr[dq.front()]);
    }
    return res;
}
int main()
{
    int n, k; cin >> n >> k;
    vector<int> arr(n);
    for(int i = 0; i < n; i++) cin >> arr[i];
    vector<int> res;
    res = f_min(arr, k);
    for(auto x:res) cout << x << ' ';
    cout << '\n';
    res = f_max(arr, k);
    for(auto x:res) cout << x << ' ';   
}
```

```c++
#include <iostream>
#include <cstring>
using namespace std;
const int N = 1000010;
int q[N];
int hh, tt = -1;
int main()
{
    int n, k;
    cin >> n >> k;
    int a[n];
    for (int i = 0; i < n; i++) cin >> a[i];
    
    for (int i = 0; i < n; i++) {
        while (tt >= hh && a[i] <= a[q[tt]]) tt--;
        q[++tt] = i;
        while (tt >= hh && q[hh] < i - (k - 1)) hh++;
        
        if(i >= k - 1) cout << a[q[hh]] << " ";
    }
    cout << "\n";
    memset(q, 0, sizeof q);
    for (int i = 0; i < n; i++) {
        while (tt >= hh && a[i] >= a[q[tt]]) tt--;
        q[++tt] = i;
        while (tt >= hh && q[hh] < i - (k - 1)) hh++;
        
        if(i >= k - 1) cout << a[q[hh]] << " ";
    }
    
}
```

## 831.KMP字符串

![image-20230909195944277](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230909195944277.png)

![image-20230909200025645](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230909200025645.png)

```c++
#include <string>
#include <vector>
#include <iostream>
using namespace std;
vector<int> ne;
void get_next(string p)
{
    for(int i = 2, j = 0; i <= (int)p.size(); i++)
    {
        while(j > 0 && p[i - 1] != p[j]) j = ne[j];
        if(p[i - 1] == p[j]) j++;
        ne[i] = j;
    }
}
// void get_next2(string p)
// {
//     int pn = p.size();
//     ne[0] = -10000000;
//     ne[1] = 0;
//     for(int j = 2; j <= pn; j++)
//     {
//         string tmp = p.substr(0, j);
//         for(int size = j - 1; size >= 1; size--)
//         {
//             if(tmp.substr(0, size) == tmp.substr(j - size, size))
//                 {ne[j] = size; break;}
//         }
//     }
// }

// int get_next3(string p, int j)
// {
//     if(j == 1) return 0;
//     string tmp = p.substr(0, j);
//     for(int size = j - 1; size >= 1; size--)
//     {
//         if(tmp.substr(0, size) == tmp.substr(j - size, size))
//             return size;
//     }
//     return 0;
// }

vector<int> kmp(string s, string p)
{
    vector<int> res;
    for(int i = 0, j = 0; i < (int)s.size(); i++)
    {
        while(j > 0 && s[i] != p[j]) j = ne[j];
        if(s[i] == p[j]) j++;
        if(j == (int)p.size())
        {
            res.push_back(i - j + 1);
            j = ne[j];
        }
    }
    return res;
}
int main()
{
    int pn, sn;
    string p, s;
    cin >> pn >> p >> sn >> s;
    ne.assign(pn + 1, 0);
    get_next(p);
    // get_next2(p);
    vector<int> res = kmp(s, p);
    for(auto x : res) cout << x << ' ';
}
```

## 835.Trie字符串树

![image-20230909200213962](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230909200213962.png)

![image-20230909200223677](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230909200223677.png)

```c++
#include <iostream>
#include <string>
#include <vector>
using namespace std;
class Trie
{
private:
    vector<Trie*> chars;
    vector<int> counts;
    Trie* serach_profix(string profix)
    {
        Trie* p = this;
        for(auto ch : profix)
        {
            ch -= 'a';
            if(!p->chars[ch])
                return nullptr;
            p = p->chars[ch];
        }
        return p;
    }
public:
    Trie()
    {
        for(int i = 0; i < 26; i++)
        {
            chars.push_back(nullptr);
            counts.push_back(0);
        }
    }
    
    void insert(string word)
    {
        Trie* p = this;
        for(auto ch : word)
        {
            ch -= 'a';
            if(!p->chars[ch]) p->chars[ch] = new Trie();
            p = p->chars[ch];
        }
        p->counts[word.back() - 'a']++;
    }
    
    int word_count(string word)
    {
        Trie* p = this;
        for(auto ch : word)
        {
            ch -= 'a';
            if(!p->chars[ch]) return 0;
            p = p->chars[ch];
        }
        return p->counts[word.back()- 'a'];
    }
    
    bool search(string word)
    {
        Trie* t = serach_profix(word);
        return t && t->counts[word.back() - 'a'];
    }
    
    bool startsWith(string profix)
    {
        return serach_profix(profix);
    }
};

int main()
{
    Trie* t = new Trie();
    int n; cin >> n;
    while(n--)
    {
        string s; cin >> s;
        string word; cin >> word;
        if(s == "I")
            t->insert(word);
        if(s == "Q")
            cout << t->word_count(word) << endl;
    }
}
```

## 143.最大异或对

![image-20230911195957155](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230911195957155.png)

```c++
#include <iostream>
#include <vector>
#include <climits>
#include <cmath>
using namespace std;
class Trie
{
public:
    Trie* bits[2];
    Trie()
    {
        for(int i = 0; i < 2; i++)
            bits[i] = nullptr;
    }
    void insert(int x)
    {
        Trie* p = this;
        for(int i = 30; i >= 0; i--)
        {
            int bit = (x >> i) & 1;
            if(!p->bits[bit])
                p->bits[bit] = new Trie();
            p = p->bits[bit];
        }
    }
};

int max_xor(vector<int>& arr)
{
    Trie* t = new Trie();
    for(auto& x : arr) t->insert(x);    //建树
    int max_val = INT_MIN;
    for(auto& x : arr)
    {
        Trie* p = t;
        int y = 0;
        for(int j = 30; j >= 0; j--)
        {
            int bit = (x >> j) & 1;
            if(p->bits[1 - bit]){
                p = p->bits[1 - bit];
                y = y * 2 + (1 - bit);
            }
            else{
                p = p->bits[bit];
                y = y * 2 + bit;
            }
        }
        max_val = max(max_val, x ^ y);
    }
    delete t;
    return max_val;
}
int main()
{
    cin.tie(0);
    ios::sync_with_stdio(false);
    int n; cin >> n;
    vector<int> arr(n);
    for(auto& x : arr) cin >> x;
    cout << max_xor(arr) << endl;
}
```

## 836.合并集合

![image-20230913180317613](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230913180317613.png)

![image-20230913180326317](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230913180326317.png)

```c++
#include <iostream>
using namespace std;
class UnionFind
{
private:
    int* parent;
    int count;
public:
    UnionFind(int n)
    {
        this->count = n;
        parent = new int[n + 1];
        for(int i = 1; i <= n; i++)
            parent[i] = i;
    }
    ~UnionFind()
    {
        delete [] parent;
    }
    int find(int a)
    {
        while(a != parent[a]){
            parent[a] = parent[parent[a]];
            a = parent[a];
        }
        return a;
    }
    void merge(int a, int b)
    {
        parent[find(b)] = find(a);
        // parent[a] = find(b);
    }
    bool is_connected(int a, int b)
    {
        return find(a) == find(b);
    }
};
int main()
{
    int n, m; cin >> n >> m;
    UnionFind* u = new UnionFind(n);
    while(m--)
    {
        string s; cin >> s;
        if(s == "M"){
            int a, b; cin >> a >> b;
            u->merge(a, b);
        }
        if(s == "Q"){
            int a, b; cin >> a >> b;
            cout << (u->is_connected(a, b) ? "Yes" : "No") << endl;
        }
    }
}
```

## 837. 连通块中点的数量

![image-20230913184015400](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230913184015400.png)

![image-20230913184024440](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230913184024440.png)

```c++
#include <iostream>
using namespace std;
class UnionFind
{
private:
    int* parent;
    int* size;
public:
    UnionFind(int n)
    {
        parent = new int[n + 1];
        size = new int[n + 1];
        for(int i = 1; i <= n; i++){
            parent[i] = i;
            size[i] = 1;
        }
    }
    ~UnionFind()
    {
        delete [] parent;
        delete [] size;
    }
    int find(int x)
    {
        while(x != parent[x]){
            parent[x] = parent[parent[x]];
            x = parent[x];
        }
        return parent[x];
    }
    void merge(int a, int b)
    {
        if(find(a) == find(b)) return;
        else if(size[a] < size[b]){
            size[find(b)] += size[find(a)];
            parent[find(a)] = find(b);
        }
        else{
            size[find(a)] += size[find(b)];
            parent[find(b)] = find(a);
        }
    }
    int parent_size(int a)
    {
        return size[find(a)];
    }
    bool is_connected(int a, int b)
    {
        return find(a) == find(b);
    }
};
int main()
{
    int n, m; cin >> n >> m;
    UnionFind* u = new UnionFind(n);
    while(m--){
        string s; cin >> s;
        if(s == "C"){
            int a, b; cin >> a >> b;
            u->merge(a, b);
        }    
        if(s == "Q1"){
            int a, b; cin >> a >> b;
            cout << (u->is_connected(a, b) ? "Yes" : "No") << endl;
        }
        if(s == "Q2"){
            int a; cin >> a;
            cout << u->parent_size(a) << endl;
        }       
    }
}
```

# 240.食物链

![image-20240104233856393](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240104233856393.png)

![image-20240104233907143](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240104233907143.png)

```c++
```

# 838.堆排序



# 839.模拟堆



## 840.模拟散列表

![image-20230915113216116](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230915113216116.png)

![image-20230915113222953](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230915113222953.png)

拉链法

```c++
#include <iostream>
#include <cstring>
using namespace std;

const int N = 100010;

int h[N], e[N], ne[N], idx;

void insert(int x)
{
    int k = (x % N + N) % N;
    e[idx] = x;
    ne[idx] = h[k];
    h[k] = idx;
    idx++;
}

bool find(int x)
{
    int k = (x % N + N) % N;
    for(int i = h[k]; i != -1; i = ne[i])
        if(e[i] == x) return true;
    return false;
}

int main()
{
    int n; cin >> n;
    memset(h, -1, sizeof h);
    while(n--)
    {
        string s; cin >> s;
        int x; cin >> x;
        if(s == "I")
        {
            insert(x);
        }
        if(s == "Q")
        {
            if(find(x)) cout << "Yes" << endl;
            else cout << "No" << endl;
        }
    }
}
```

开放寻址法

```c++
#include <iostream>
#include <cstring>
using namespace std;

const int N = 200003;
// const int null = 0x3f3f3f3f;

int h[N];

//x存在，返回x的索引
//x不存在，返回x该放入的位置索引
int find(int x)
{
    int k = (x % N + N) % N;
    while(h[k] != 2e9 && h[k] != x)
    {
        k++;
        if(k == N) k = 0;
    }
    return k;
}

int main()
{
    int n; cin >> n;
    for(int i = 0; i < N; i++)  h[i] = 2e9;
    // memset(h, 0x3f, sizeof h);
    while(n--)
    {
        string s; cin >> s;
        int x; cin >> x;
        if(s == "I")
            h[find(x)] = x;
        if(s == "Q")
        {
            if(h[find(x)] != 2e9) cout << "Yes" << endl;
            else cout << "No" << endl;
        }
    }
}
```

## 841.字符串哈希

![image-20230916091828417](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230916091828417.png)

![image-20230916091835970](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230916091835970.png)

```c++
#include <iostream>
using namespace std;
const int N = 100000, P = 131;

char s[N];
int h[N], p[N];

unsigned long long get(int l, int r)
{
    return h[r] - h[l - 1] * p[r - l + 1];
}
int main()
{
    int n, m; cin >> n >> m;

    scanf("%s", s + 1);
    p[0] = 1;
    for(int i = 1; i <= n; i++)
    {
        p[i] = p[i - 1] * P;
        h[i] = h[i - 1] * P + s[i];
    }
    
    while(m--)
    {
        int l1, r1, l2, r2;
        cin >> l1 >> r1 >> l2 >> r2;
        
        if(get(l1, r1) == get(l2, r2))
            cout << "Yes" << endl;
        else
            cout << "No" << endl;
    }
}
```

# 搜索与图论（一）

## 842.排列数字

![image-20230916110744119](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230916110744119.png)

```c++
#include <iostream>

using namespace std;
int n;
const int N = 7;

int nums[N];
bool used[N + 1];

void dfs(int u)
{
    if(u == n)
    {
        for(int i = 0; i < n; i++)
            cout << nums[i] << ' ';
        cout << "\n";
    }
    for(int i = 1; i <= n; i++)
    {
        if(!used[i])
        {
            nums[u] = i;
            used[i] = true;
            dfs(u + 1);
            used[i] = false;
        }
    }
}
int main()
{
    cin >> n;
    dfs(0);
    return 0;
}
```

##  843.n皇后问题

![image-20230916185640501](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230916185640501.png)

![image-20230916185659973](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230916185659973.png)

```c++
#include <iostream>
using namespace std;
int n;
const int N = 20;
int col[N], diag[N], udiag[N];
char g[N][N];

void dfs(int i)
{
    if(i == n)
    {
        for(int i = 0; i < n; i++)
            cout << g[i] << endl;
        cout << "\n";
    }
    
    for(int j = 0; j < n; j++)
    {
        if(!col[j] && !diag[i + j] && !udiag[i - j + n])
        {
            g[i][j] = 'Q';
            col[j] = diag[i + j] = udiag[i - j + n] = true;
            dfs(i + 1);
            g[i][j] = '.';
            col[j] = diag[i + j] = udiag[i - j + n] = false;
        }
    }
}

int main()
{
    cin >> n;
    for(int i = 0; i < n; i++)
        for(int j = 0; j < n; j++)
            g[i][j] = '.';
    dfs(0);
    return 0;
}
```

```c++
#include <iostream>
using namespace std;

int n;
const int N = 20;
int row[N], col[N], diag[N], udiag[N];
char g[N][N];

void dfs(int x, int y, int s)
{
    if(y == n)
    {
        y = 0;
        x++;
    }
    if(x == n)
    {
        if(s == n)
        {
            for(int i = 0; i < n; i++)
                cout << g[i] << endl;
            cout << "\n";
        }
        return ;
    }
    //不放
    dfs(x, y + 1, s);
    //放
    if(!row[x] && !col[y] && !diag[x + y] && !udiag[x - y + n])
    {
        g[x][y] = 'Q';
        row[x] = col[y] = diag[x + y] = udiag[x - y + n] = true;
        dfs(x, y + 1, s + 1);
        row[x] = col[y] = diag[x + y] = udiag[x - y + n] = false;
        g[x][y] = '.';
    }
}
int main()
{
    cin >> n;
    for(int i = 0; i < n; i++)
        for(int j = 0; j < n; j++)
            g[i][j] = '.';
    dfs(0, 0, 0);
    return 0;
}
```

## 844.走迷宫

![image-20230916224608577](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230916224608577.png)

![image-20230916224640079](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230916224640079.png)

```c++
#include <iostream>
using namespace std;

const int N = 101;

int g[N][N];
int d[N][N];
pair<int, int> q[N * N], previous_path[N][N];

int n, m;

int bfs()
{
    int hh = 0, tt = -1;
    d[0][0] = 0;
    q[++tt] = pair<int, int>(0, 0);
    int dx[] = {-1, 0, 1, 0};
    int dy[] = {0, 1, 0, -1};
    
    while(hh <= tt)
    {
        auto t = q[hh++];
        for(int i = 0; i < 4; i++)
        {
            int x = t.first + dx[i];
            int y = t.second + dy[i];
            if(x >= 0 && x < n && y >= 0 && y < m && g[x][y] == 0 && d[x][y] == -1)
            {
                d[x][y] = d[t.first][t.second] + 1;
                previous_path[x][y] = t;
                q[++tt] = {x, y};
            }
        }
    }
    
    // int x = n - 1;
    // int y = m - 1;
    // while(x || y)
    // {
    //     cout << x << " " << y << endl;
    //     auto t = previous_path[x][y];
    //     x = t.first, y = t.second;
    // }
    
    return d[n - 1][m - 1];
}

int main()
{
    cin >> n >> m;
    for(int i = 0; i < n; i++)
        for(int j = 0; j < m; j++)
        {
            cin >> g[i][j];
            d[i][j] = -1;
        }
    cout << bfs() << endl;
}
```

# 845.八数码

​	





## 846.树的重心

![image-20230917092123169](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230917092123169.png)

![image-20230917092131275](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230917092131275.png)

```c++
#include <iostream>

using namespace std;

int n;
const int N = 100010, M = 2 * N;
int h[N], e[M], ne[M], idx;
bool st[N];
int ans = N;


void add(int a, int b)// 使得节点a和节点b相连，a和b之间添加一条边（单向a->b）
{
    e[idx] = b;
    ne[idx] = h[a];
    h[a] = idx++;
}

// 以u结点为根的子树的size大小。（节点数量）
int dfs(int u)
{
    st[u] = true;
    int sum = 1;    //以u结点为根的子树的size大小
    int res = 0;    //删除u结点后，连通块的节点数量最大值
    for(int i = h[u]; i != -1; i = ne[i])
    {
        int j = e[i];
        if(!st[j])
        {
            int s = dfs(j);
            res = max(res, s);
            sum += s;
        }
    }
    
    res = max(res, n - sum);
    ans = min(res, ans);
    
    return sum;
}
int main()
{
    for(int i = 0; i < N; i++) h[i] = -1;
    cin >> n;
    for(int i = 0; i < n - 1; i++)
    {
        int a, b; cin >> a >> b;
        add(a, b);
        add(b, a);
    }
    dfs(1);
    cout << ans;
}
```

## 847.图中点的层次

![image-20230917101520642](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230917101520642.png)

```c++
#include <iostream>

using namespace std;

int n, m;
const int N = 100010, M = N * 2;

int h[N], e[M], ne[M], idx;
int d[N], q[N];

void add(int a, int b)
{
    e[idx] = b;
    ne[idx] = h[a];
    h[a] = idx++;
}

int bfs()
{
    int hh = 0;
    int tt = -1;
    q[++tt] = 1;
    d[1] = 0;
    while(hh <= tt)
    {
        auto t = q[hh++];
        
        for(int i = h[t]; i != -1; i = ne[i])
        {
            int j = e[i];
            if(d[j] == -1)
            {
                d[j] = d[t] + 1;
                q[++tt] = j;
            }
        }
    }
    return d[n];
}
int main()
{
    for(int i = 0; i < N; i++) h[i] = -1, d[i] = -1;
    cin >> n >> m;
    while(m--)
    {
        int a, b; cin >> a >> b;
        add(a, b);
    }
    cout << bfs() << endl;
}
```

## 848.有向图的拓扑序列

![image-20230917101659396](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230917101659396.png)

```c++
/*
存在环的话，一定不存在拓扑序列
有向无环图，一定存在拓扑序列，也成为拓扑图
有向图，每个点有一个出度和入度
入度： 有几条边指向自己
出度：有几条边，从自己出来

入度为0：表示没有一条边指向我，也就是没有节点在我之前。
因此所有入度为0的点，可以排在最前面的位置，因此拓扑排序第一步就是将所有入度为0的点入队
*/
#include <iostream>

using namespace std;
const int N = 100010;
int h[N], e[N], ne[N], idx;
int n, m;
int q[N], d[N];

void add(int a, int b)
{
    e[idx] = b;
    ne[idx] = h[a];
    h[a] = idx++;
}

bool topsort()
{
    int hh = 0;
    int tt = -1;
    for(int i = 1; i <= n; i++)
        if(!d[i])
            q[++tt] = i;
    while(hh <= tt)
    {
        int t = q[hh++];
        for(int i = h[t]; i != -1; i = ne[i])
        {
            int j = e[i];
            d[j] -- ;
            if(d[j] == 0) q[++ tt] = j;
        }
    }
    return tt == n - 1;
}

int main()
{
    cin >> n >> m;
    for(int i = 0; i < N; i++) h[i] = -1;
    while(m--)
    {
        int a, b; cin >> a >> b;
        add(a, b);
        d[b]++;
    }
    
    if(topsort())
    {
        for(int i = 0; i < n; i++) cout << q[i] << " ";
        cout << "\n";
    }
    else
        cout << -1;
}
```

# 搜索与图论（二）

n是点数，m是边数。 $m = O(n^2)$

![image-20230917111238764](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230917111238764.png)

```
单源最短路是求一个点到所有点的最短路距离（1号点到其他点的最短路）
    
多源汇最短路：起点不固定，起点和终点都是随机的（任选两个点）。

/*
源点：起点
汇点：终点

/*
最短路分为：单源最短路、多源汇最短路

单源最短路：所有边权都是正数、存在边权是负数两种情况。

无向图是一种特殊的有向图。有向图包含了无向图。

无向图和有向图的最短路一样的，算法实现上没有区别，因此只使用有向图即可。

SPFA算法可以看作BF算法的优化
但是如果求最短路，限制经过的边个数的话，只能用BF算法，不能用SPFA算法。

/*
朴素版dijkstra算法适用于稠密图，因为其复杂度和边数无关。比如当m = n^2 的时候 显然，o(n^2) < o(mlogn)
堆优化版dijkstra算法适用于稀疏图，比如当m = n，m和n是一个数量级的时候，显然，o(n^2) > o(mlogn) 

/*
最短路算法的难点：建模。讲原始问题抽象为一个最短路问题，如何建图，点和边。
```

## 849.dijkstra最短路1

![image-20231018091414618](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231018091414618.png)

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20230917194125943.png" alt="image-20230917194125943" style="zoom:80%;" />

```c++
#include <iostream>
#include <cstring>
using namespace std;

const int N = 510;
const int M = 100010;

int n, m;       //  顶点数， 边数
int g[N][N];    //  邻接矩阵
int dist[N];    //  dist[i] 表示 i 到 1 的距离(i >= 1) dist[1] = 0
bool st[N];     //  某个点是否被遍历过了，(到1的最短距离已经确定了)

int dijkstra()
{
    dist[1] = 0;
    for(int i = 0; i < n - 1; i++)
    {
        int t = -1;
        for(int j = 1; j <= n; j++)	//从1 到 n中，最短路径未确定的点中，找到最短的一个
            if(!st[j] && (t == -1 || dist[j] < dist[t])) t = j;
        st[t] = true;
        
        for(int k = 1; k <= n; k++)
            dist[k] = min(dist[k], dist[t] + g[t][k]);
    }
    
    if(dist[n] == 0x3f3f3f3f) return -1;
    return dist[n];
}
int main()
{
    cin >> n >> m;
    
    memset(g, 0x3f, sizeof g);
    memset(dist, 0x3f, sizeof dist);
    for(int i = 0; i < m; i++)
    {
        int x, y, z;
        cin >> x >> y >> z;
        g[x][y] = min(g[x][y], z);  //去除重边，保留最小的
    }
    cout << dijkstra() << endl;
}
```

## 850.dijkstra最短路2

​		如何判断稠密图稀疏图？看给的数据，如果点数和边数是一个数量级，就是稀疏图。如果边数远大于点数，就是稠密图.。

​		堆优化版的：dijkstra

![image-20231018230753281](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231018230753281.png)

```c++
#include <iostream>
#include <queue>
#include <cstring>
using namespace std;

const int N = 150100;
const int M = 150100;

int n, m;
int h[N], e[N], ne[N], w[N], idx;
bool st[N];
int dist[N];

int add(int a, int b, int c)
{
    e[idx] = b;
    w[idx] = c;
    ne[idx] = h[a];
    h[a] = idx++;
}

int dijkstra()
{
    dist[1] = 0;
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> heap;
    heap.emplace(dist[1], 1);
    
    while(heap.size())
    {
        auto t = heap.top();
        heap.pop();
        
        int d = t.first;
        int no = t.second;
        if(st[no]) continue;
        st[no] = true;
        
        for(int i = h[no]; i != -1; i = ne[i])
        {
            int j = e[i];
            if(d + w[i] < dist[j])
            {
                dist[j] = d + w[i];
                heap.emplace(dist[j], j);
            }
        }
    }
    if(dist[n] == 0x3f3f3f3f) return -1;
    return dist[n];
}


int main()
{
    cin >> n >> m;
    memset(h, -1, sizeof h);
    memset(dist, 0x3f, sizeof dist);
    // memset(w, 0x3f, sizeof w);   邻接表方式存储的话，权重没必要初始化，因为遍历不到
    
    for(int i = 0; i < m; i++)
    {
        int x, y, z;
        cin >> x >> y >> z;
        add(x, y, z);
    }
    cout << dijkstra();
}
```

## 853.有边数限制的最短路

![image-20231206094710470](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231206094710470.png)

![image-20231206094721700](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231206094721700.png)

```c++
#include <iostream>
#include <cstring>
#include <algorithm>
using namespace std;
const int N = 510, M = 10010;
int n, m, k;
int dist[N];
int last[N];

struct Edge
{
    int a, b, w;
} edges[M];

void bellman_ford()
{
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;
    for(int i = 0; i < k; i ++)
    {
        memcpy(last, dist, sizeof dist);// 每次用上一次迭代的结果更新，否则会连续更新两次，出现串联。//必须保证每次只增加一条边
        for(int j = 0; j < m; j++)
        {
            auto e = edges[j];
            dist[e.b] = min(dist[e.b], last[e.a] + e.w);
        }
    }
}

int main()
{
    scanf("%d %d %d", &n, &m, &k);
    for(int i = 0; i < m; i++)
        scanf("%d %d %d", &edges[i].a, &edges[i].b, &edges[i].w);
    
    bellman_ford();
    if(dist[n] > 0x3f3f3f3f / 2) puts("impossible");
    else cout << dist[n];
}
```

## 851.spfa最短路

![image-20231206183658302](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231206183658302.png)

```c++
#include <iostream>
#include <cstring>
#include <queue>
using namespace std;

const int N = 100010;

int h[N], w[N], e[N], ne[N], idx;
int n, m;
int dist[N];
bool st[N];

void add(int a, int b, int c)
{
    e[idx] = b;
    w[idx] = c;
    ne[idx] = h[a];
    h[a] = idx++;
}

void spfa()
{
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;
    
    queue<int> q;
    q.push(1);      
    st[1] = true;   //表示1号点已经在队列当中
    
    while(q.size())
    {
        int t = q.front();
        st[t] = false;
        q.pop();
        for(int i = h[t]; i != -1; i = ne[i])
        {
            int j = e[i];
            if(dist[j] > dist[t] + w[i])
            {
                dist[j] = dist[t] + w[i];
                if(!st[j])
                {
                    q.push(j);
                    st[j] = true;
                }
            }
        }
    }
}

int main()
{
    scanf("%d %d", &n, &m);
    memset(h, -1, sizeof h);
    while(m--)
    {
        int a, b, c;
        scanf("%d%d%d", &a, &b, &c);
        add(a, b, c);
    }
    spfa();
    if(dist[n] == 0x3f3f3f3f) cout << "impossible";
    else cout << dist[n];
}
```

## 852.spfa判断负环

```c++
#include <iostream>
#include <cstring>
#include <queue>
using namespace std;

const int N = 100010;

int h[N], w[N], e[N], ne[N], idx;
int n, m;
int dist[N];
bool st[N];
int cnt[N];

void add(int a, int b, int c)
{
    e[idx] = b;
    w[idx] = c;
    ne[idx] = h[a];
    h[a] = idx++;
}

bool spfa()
{
    // memset(dist, 0x3f, sizeof dist);
    // dist[1] = 0;
    // cnt[1] = 0;
    
    queue<int> q;
    for(int i = 1; i <= n; i++) 
    {
        q.push(i);      
        st[i] = true;   //表示1号点已经在队列当中
    }
    while(q.size())
    {
        int t = q.front();
        st[t] = false;
        q.pop();
        for(int i = h[t]; i != -1; i = ne[i])
        {
            int j = e[i];
            if(dist[j] > dist[t] + w[i])
            {
                dist[j] = dist[t] + w[i];
                cnt[j] = cnt[t] + 1;
                if(cnt[j] >= n) return true;
                if(!st[j])
                {
                    q.push(j);
                    st[j] = true;
                }
            }
        }
    }
    return false;
}

int main()
{
    scanf("%d %d", &n, &m);
    memset(h, -1, sizeof h);
    while(m--)
    {
        int a, b, c;
        scanf("%d%d%d", &a, &b, &c);
        add(a, b, c);
    }
    if(spfa())  cout << "Yes";
    else    cout << "No";
    // if(dist[n] == 0x3f3f3f3f) cout << "impossible";
    // else cout << dist[n];   
}
```

## 854.Floyd求最短路

![image-20231206195954095](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231206195954095.png)

![image-20231206200002604](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231206200002604.png)

```c++
#include <iostream>
using namespace std;

const int N = 210;

int d[N][N];
int n, m, q;

void floyd()
{
    for(int k = 1; k <= n; k++)
        for(int i = 1; i <= n; i++)
            for(int j = 1; j <= n; j++)
                d[i][j] = min(d[i][j], d[i][k] + d[k][j]);
}

int main()
{
    scanf("%d%d%d", &n, &m, &q);
    for(int i = 1; i <= n; i++)
        for(int j = 1; j <= n; j++)
            if(i == j) d[i][j] = 0;
            else d[i][j] = 1e9;
    while(m--)
    {
        int a, b, c;
        scanf("%d%d%d", &a, &b, &c);
        d[a][b] = min(d[a][b], c);
    }
    floyd();
    while(q--)
    {
        int a, b; cin >> a >> b;
        if(d[a][b] > 1e9 / 2) cout << "impossible" << endl;
        else cout << d[a][b] << endl;
    }
}
```

```
最小生成树，都是无向图
	Prim算法：1.朴素版（稠密图）	o(n^2)
			 2.堆优化版（稀疏图） o(mlogn)
	Kruskal算法	(o(mlogm))（稀疏图）

二分图：1.染色法	(o(m + n))
	   2.匈牙利算法	(最坏：o(mn))
	   
	 
```

# 搜索与图论（三）

## 858.Prim算法求最小生成树

![image-20231207103747053](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231207103747053.png)

![image-20231207103756033](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231207103756033.png)

```c++
#include <iostream>
#include <cstring>
using namespace std;

const int N = 510;

int g[N][N];
int dist[N];        //dist[j]表示的是j节点到 已存在节点所构成树的距离
int n, m;
bool st[N];

int prim()
{
    int res = 0;
    for(int i = 0; i < n; i++)
    {
        int t = -1;
        for(int j = 1; j <= n; j++)
            if(!st[j] && (t == -1 || dist[j] < dist[t])) t = j;
        
        if(i && dist[t] == 0x3f3f3f3f) return dist[t];  //一旦有一个节点到树的距离为无穷大，则不能构成最小生成树，直接返回
        if(i) res += dist[t];
        
        for(int j = 1; j <= n; j++)
            dist[j] = min(dist[j], g[t][j]);
        st[t] = true;
    }
    return res;
}
int main()
{
    memset(g, 0x3f, sizeof g);
    memset(dist, 0x3f, sizeof dist);
    cin >> n >> m;
    while(m--)
    {
        int a, b, c;
        cin >> a >> b >> c;
        g[a][b] = g[b][a] = min(g[a][b], c);
    }
    int t = prim();
    if(t == 0x3f3f3f3f) cout << "impossible";
    else cout << t;
}
```

## 859.kruskal算法求最小生成树

![image-20231218081234339](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231218081234339.png)

![image-20231218081243452](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231218081243452.png)

```c++
#include <iostream>
#include <algorithm>
using namespace std;

const int N = 200010;

int n, m;
int p[N];

struct Edge
{
    int a;
    int b;
    int w;
    bool operator<(const Edge& e)const
    {
        return w < e.w;
    }
} edges[N];

int find(int x)
{
    if(p[x] != x) p[x] = find(p[x]);
    return p[x];
}

void kruskal()
{
    sort(edges, edges + m);
    for(int i = 1; i <= n; i++) p[i] = i;
    
    int res = 0;    //res为当前最小生成树中所有边权重之和
    int cnt = 0;    //cnt存的是当前最小生成树加入了多少条边
    for(int i = 0; i < m; i++)
    {
        int a = edges[i].a, b = edges[i].b, w = edges[i].w;
        
        a = find(a), b = find(b);
        if(a != b)
        {
            p[a] = b;
            res += w;
            cnt++;
        }
    }
    if(cnt < n - 1) cout << "impossible";
    else cout << res;
}


int main()
{
    cin >> n >> m;
    for(int i = 0; i < m; i++)
    {
        int a, b, w;
        cin >> a >> b >> w;
        edges[i] = {a, b, w};
    }
    kruskal();
}
```

## 860.染色法判定二分图

![image-20231218201626948](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231218201626948.png)

```c++
#include <iostream>
#include <cstring>
#include <cstdio>
using namespace std;

const int N = 100010;
const int M = 200010;

int n, m;
int h[N], e[M], ne[M], idx;
int color[N];

void add(int a, int b)
{
    e[idx] = b;
    ne[idx] = h[a];
    h[a] = idx++;
}

bool dfs(int u, int c)
{
    color[u] = c;   
    for(int i = h[u]; i != -1; i = ne[i])
    {
        int j = e[i];
        if(!color[j])
        {
            if(!dfs(j, 3 - c)) return false;
        }
        else if(color[j] == c) return false;
    }
    return true;
}

int main()
{
    cin >> n >> m;
    memset(h, -1, sizeof h);
    while(m--)
    {
        int a, b; cin >> a >> b;
        add(a, b); add(b, a);
    }
    
    bool flag = true;
    for(int i = 1; i <= n; i++)
    {
        if(!color[i])
        {
            if(!dfs(i, 1))
            {
                flag = false;
                break;
            }
        }
    }
    
    if(flag) cout << "Yes";
    else cout << "No";
}
```

## 861.二分图的最大匹配

![image-20231218201745956](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231218201745956.png)

```c++
#include <iostream>
#include <cstring>
using namespace std;

const int N = 510, M = 100010;

int n1, n2, m;
int h[N], e[M], ne[M], idx;
int match[N];
bool st[N];

void add(int a, int b)
{
    e[idx] = b;
    ne[idx] = h[a];
    h[a] = idx++;
}

bool find(int x)
{
    for(int i = h[x]; i != -1; i = ne[i])
    {
        int j = e[i];
        if(!st[j])
        {
            st[j] = true;
            if(match[j] == 0 || find(match[j]))
            {
                match[j] = x;
                return true;
            }
        }
    }
    return false;
}

int main()
{
    cin >> n1 >> n2 >> m;
    memset(h, -1, sizeof h);
    while(m--)
    {
        int a, b; cin >> a >> b;
        add(a, b);
    }
    int res = 0;
    for(int i = 1; i <= n1; i++)
    {
        memset(st, false, sizeof st);
        if(find(i)) res++;
    }
    cout << res;
}
```

二分图的定义：可以将一个图分为两部分，这两部分各自内部的点均不相连。

# 数学知识（一）

## 866.试除法判断质数

![image-20231218201917175](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231218201917175.png)

```c++
#include <iostream>
using namespace std;
bool is_prime(int n)
{
    if(n < 2) return false;
    for(int i = 2; i <= n / i; i++)
        if(n % i == 0) return false;
    return true;
}
int main()
{
    int n; cin >> n;
    while(n--)
    {
        int x; cin >> x;
        if(is_prime(x)) cout << "Yes\n";
        else cout << "No\n";
    }
}
```

## 867.分解质因数

![image-20231218201847135](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231218201847135.png)

```c++
#include <iostream>
using namespace std;
void devide(int n)
{
    for(int i = 2; i <= n / i; i++)
    {
        int cnt = 0;
        while(n % i == 0)
        {
            cnt++;
            n /= i;
        }
        if(cnt)printf("%d %d\n", i, cnt);
    }
    if(n > 1) printf("%d %d\n", n, 1);
    printf("\n");
}
int main()
{
    int n; cin >> n;
    while(n--)
    {
        int x; cin >> x;
        devide(x);
    }
}
```

## 868.筛质数

![image-20231222151836077](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231222151836077.png)

```c++
#include <iostream>
using namespace std;
const int N = 1000010;
bool st[N];
int primes[N];
// 方法一：最朴素做法：从前往后，依次筛掉每一个数的倍数
// 原理：假设一个数x没有被筛掉的话，说明从2到x-1都不能整除x，说明x是一个倍数（充分条件）
// 复杂度：n/2 + n/3 + n/4 + ...n / n -> O{nln(n)}     150ms
int get_primes1(int n)
{
    int cnt = 0;
    for(int i = 2; i <= n; i++)
    {
        if(!st[i]) cnt++;
        for(int j = i + i; j <= n; j += i) st[j] = true;
    }
    return cnt;
}
// 方法二：方法一的改进，从前往后，依次筛掉每一个质数的倍数。   也叫做埃及筛法
// 原理：从2到x-1中的所有质数都不能整除x的话，x就是一个质数了，不需要判断2到x-1之间的所有数
// 复杂度：（质数定理：1到n之间有（n/logn）个质数），所以相比方法一：变成了O{nln(ln(n))}    44ms
int get_primes2(int n)
{
    int cnt = 0;
    for(int i = 2; i <= n; i++)
    {
        if(!st[i]) {cnt++;
        for(int j = i + i; j <= n; j += i) st[j] = true;}
    }
    return cnt;
}
//方法三：线性筛法（核心思想，一个数n只会被其最小质因子筛掉）
//  复杂度：27ms
//  原理：如果 i % primes[j] == 0， 那么 primes[j] 一定是 primes[j] * i的最小质因子，st[primes[j] * i] = true;
//        如果 i % primes[j] != 0， 那么 primes[j] 一定小于 i 的最小质因子，因此primes[j] 也一定是 primes[j] * i的最小质因子
int get_primes3(int n)
{
    int cnt = 0;
    for(int i = 2; i <= n; i++)
    {
        if(!st[i]) primes[cnt++] = i;
        for(int j = 0; primes[j] <= n / i; j++)
        {
            st[primes[j] * i] = true;
            if(i % primes[j] == 0) break;
        }
    }
    return cnt;
}
int main()
{
    int n; cin >> n;
    cout << get_primes3(n);
}
```

## 869.试除法求约数

![image-20231222152017727](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231222152017727.png)

```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
const int N = 1000;
int l[N], li;   //存储小于等于根号n的约数
int r[N], ri;   //存储大于等于根号n的约数
//  写法一
void devide(int n)
{
    vector<int> res;
    for(int i = 1; i <= n / i; i++)
        if(n % i == 0)
        {
            res.push_back(i);
            if(i != n / i) res.push_back(n / i);
        }
    sort(res.begin(), res.end());
    for(int i = 0; i < (int)res.size(); i++) 
        cout << res[i] << " ";
    cout << "\n";
}
//  写法二
// void devide(int n)
// {
//     for(int i = 1; i <= n / i; i++)
//         if(n % i == 0)
//         {
//             l[li++] = i;
//             if(i != n / i) r[ri++] = n / i;
//         }
//     for(int i = 0; i < li; i++) cout << l[i] << " ";
//     for(int i = ri - 1; i >= 0; i--) cout << r[i] << " ";
//     ri = 0;li = 0;
//     cout << "\n";
// }
/*
一个数n的约数个数的期望值，
1 2 ... n 的约数个数总和
1 是所有数的约数
2 是n/2个数的约数
...
n 是 n/n 个数的约数
所以，1到n总共约数个数 = n(1 + 1 / 2 + 1 / 3 + ... 1 / n)  = nlogn
所以，1到n中平均一个数的约数个数 logn

所以这道题的复杂度为 根号n + logn*(log(logn)) 
*/
int main()
{
    int n; cin >> n;
    while(n--)
    {
        int x; cin >> x;
        devide(x);
    }
}
```

## 870.约数个数

![image-20231222152120372](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231222152120372.png)

一个数分解质因数的结果
$$
n = p^{\alpha_1}_1 \times p^{\alpha_2}_2 \times p^{\alpha_3}_3 \times...\times p^{\alpha_n}_n
$$
那么n的约数个数为
$$
(\alpha_1 + 1)\times (\alpha_2 + 1)\times (\alpha_3 + 1)\times....\times (\alpha_4 + 1)
$$
n的所有约数的和为
$$
(p^{0}_1 + p^{1}_1 + ... + p^{\alpha_1}_1)\times (p^{0}_2 + p^{1}_2 + ... + p^{\alpha_2}_2)\times (p^{0}_3 + p^{1}_3 + ... + p^{\alpha_3}_3)\times ... \times(p^{0}_n + p^{1}_n + ... + p^{\alpha_n}_n)
$$

```c++
#include <iostream>
#include <unordered_map>
using namespace std;
const int mod = 1000000007;
unordered_map<int, int> primes;
void devide(int n)
{
    for(int i = 2; i <= n / i; i++)
    {
        while(n % i == 0)
        {
            primes[i]++;
            n /= i;
        }
    }
    if(n > 1) primes[n]++;
}
int main()
{
    int n; cin >> n;
    long long res = 1;
    while(n--)
    {
        int x; cin >> x;
        devide(x);
    }
    for(auto prime : primes) 
        res = res * (prime.second + 1) % mod;
    cout << res;
}
```

## 871.约数之和

![image-20231222152151479](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231222152151479.png)

```c++
#include <iostream>
#include <unordered_map>
using namespace std;
const int mod = 1000000007;
unordered_map<int, int> primes;
void devide(int n)
{
    for(int i = 2; i <= n / i; i++)
    {
        while(n % i == 0)
        {
            primes[i]++;
            n /= i;
        }
    }
    if(n > 1) primes[n]++;
}
int main()
{
    int n; cin >> n;
    long long res = 1;
    while(n--)
    {
        int x; cin >> x;
        devide(x);
    }
    for(auto prime : primes)
    {
        int a = prime.first;
        int b = prime.second;
        long long t = 1;
        while(b--) t = (t * a + 1) % mod;
        res = res * t % mod;
    }
    cout << res;
}
```

## 872.最大公约数

![image-20231222112228235](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231222112228235.png)

```c++
/*
	核心思想：a 和 b 的最大公约数 等价于 b 和 (a % b) 的最大公约数。
	a 和 0 的最大公约数为 a。
*/
#include <iostream>
using namespace std;
int gcd(int a, int b)
{
    return b ? gcd(b, a % b) : a;
}
int main()
{
    int n; cin >> n;
    while(n--)
    {
        int a, b; cin >> a >> b;
        cout << gcd(a, b) << endl;
    }
}
```

##  873.欧拉函数

容斥原理：

```
求1~N中和N互质的数的个数
1.从1~N中去掉p1 p2 ... pn 的所有倍数
2.加上 pi * pj 的所有倍数
3.减去 pi * pj * pk 的所有倍数
....
以此类推
```

$$
N-N\times\sum_{i=1}^{n}\frac{1}{p_i} + N\times\sum_{1\le i\le j\le n}^{}\frac{1}{p_i}\frac{1}{p_j} + .... + N\times(-1)^{n}\frac{1}{p_i}\frac{1}{p_j}...\frac{1}{p_n}
$$

上面这个式子就是下面这个式子的展开。
$$
N\times(1-\frac{1}{p_1})\times(1-\frac{1}{p_2})...\times(1-\frac{1}{p_n})
$$
![image-20231222121246124](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231222121246124.png)

![image-20231222121259475](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231222121259475.png)

```c++
#include <iostream>
using namespace std;
int devide(int n)
{
    int res = n;
    for(int i = 2; i <= n / i; i++)
    {
        if(n % i == 0)
        {
            res = res / i * (i - 1);    // 先除再乘，防止超过int最大范围
            while(n % i == 0)
                n /= i;
        }
    }
    if(n > 1) res = res / n * (n - 1);
    return res;
}
int main()
{
    int n; cin >> n;
    while(n--)
    {
        int x; cin >> x;
        cout << devide(x) << endl;
    }
}
```

## 874.筛法求欧拉函数

![image-20231222152328653](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231222152328653.png)
$$
\rm phi(i)=i\times(1-\frac{1}{p_1})\times(1-\frac{1}{p_2})...\times(1-\frac{1}{p_k})
\\\rm如果primes[j] 能整除 i:\ \ \ \ \ \ \ \ phi(primes[j]*i) = primes[j] * phi(i)
\\\rm如果primes[j] 不能整除 i:\ \ \ \ phi(primes[j]*i) = primes[j] * phi(i) * (1 - \frac{1}{primes[j]})
$$

```c++
#include <iostream>
using namespace std;

const int N = 1000010;
bool st[N];
int primes[N], cnt;
int phi[N];

long long get_eulers(int n)
{
    phi[1] = 1;
    for(int i = 2; i <= n; i++)
    {
        if(!st[i])
        {
            primes[cnt++] = i;
            phi[i] = i - 1;     // 质数的欧拉函数为其本身减一，因为除了n，1 ~ n-1中的所有数和n都互质
        }
        for(int j = 0; primes[j] <= n / i; j++)
        {
            st[primes[j] * i] = true;
            if(i % primes[j] == 0) 
            {
                phi[primes[j] * i] = phi[i] * primes[j];
                break;
            }
            else
                phi[primes[j] * i] = phi[i] * (primes[j] - 1);
        }
    }
    long long res = 0;
    for(int i = 1; i <= n; i++)
        res += phi[i];
    return res;
}
int main()
{
    int n; cin >> n;
    cout << get_eulers(n);
}
```

欧拉定理：

若a与n互质，则$\rm a^{\phi(n)}\equiv 1(mod\ n)$。如果n为质数，就是费马定理。

# 数学知识（二）

## 875.快速幂

![image-20231222172049813](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231222172049813.png)

```c++
#include <iostream>
using namespace std;

long long fast_power(long long a, int k, int p)
{
    long long res = 1;
    while(k)
    {
        if(k & 1) res = res * a % p;
        k >>= 1;
        a = a * a % p;
    }
    return res;
}
int main()
{
    int n; cin >> n;
    while(n--)
    {
        int a, b, p;
        cin >> a >> b >> p;
        cout << fast_power(a, b, p) << endl;
    }
}
```

## 876.快速幂求逆元

定义假设b 能 整除 a，则存在一个 x 使得$\frac{a}{b}\equiv a\cdot x\ \rm (mod\ p)$，x称为b的逆元

逆元性质:$x\times b \equiv1\rm(mod\ p)$ 

有根据费马定理：$b^{p-1}\equiv1\rm(mod\ p)$，因此$x=b^{p-2}$

![image-20231222173214552](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231222173214552.png)

![image-20231222173224435](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231222173224435.png)

```c++
#include <iostream>
using namespace std;

long long fast_power(long long a, int k, int p)
{
    long long res = 1;
    while(k)
    {
        if(k & 1) res = res * a % p;
        k >>= 1;
        a = a * a % p;
    }
    return res;
}
int main()
{
    int n; cin >> n;
    while(n--)
    {
        int a, p;
        cin >> a >> p;
        if(a % p) cout << fast_power(a, p - 2, p) << endl;
        else cout << "impossible\n";
    }
}
```

## 877.扩展欧几里得算法

利用了欧几里得算法的性质

![image-20231223105412476](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231223105412476.png)
$$
\rm ax + by=gcd(a,b)\\相当于，找到x \ y满足\\
\rm by + (a\%b)x = gcd(b,a\%b)\\
\rm 也就是\ \ ax+b(y-\frac{a}{b}x)=gcd(a,b)\\
\rm 因此x的系数没变，y的系数变为y-\frac{a}{b}x
$$

```c++
#include <cstdio>
using namespace std;
int exgcd(int a, int b, int& x, int& y)
{
    if(!b)
    {
        x = 1;
        y = 0;
        return a;        
    }
    int d = exgcd(b, a % b, y, x);
    y -= a / b * x;
    return d;
}
int main()
{
    int n; scanf("%d", &n);
    while(n--)
    {
        int x, y, a, b; 
        scanf("%d%d", &a, &b);
        exgcd(a, b, x, y);
        printf("%d %d\n", x, y);
    }
}
```

## 878.线性同余方程

$$
\rm 求x使得，ax\equiv b(mod\ m)\\
\rm 相当于求，ax =my + b,即ax + my = b\\
\rm 再根据欧几里得算法，如果b是gcd(a,m)的倍数，就成了扩展欧几里得算法，求满足解的x和y即可，就一定有解
$$

![image-20231223111758447](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231223111758447.png)

```c++
#include <cstdio>
using namespace std;
//	扩展欧几里得算法的返回值仍为 a b 的最大公约数，只不过顺带求了x 和 y
int exgcd(int a, int b, int& x, int& y)
{
    if(!b)
    {
        x = 1;
        y = 0;
        return a;        
    }
    int d = exgcd(b, a % b, y, x);
    y -= a / b * x;
    return d;
}
int main()
{
    int n; scanf("%d", &n);
    while(n--)
    {
        int a, b, m;
        int x, y;
        scanf("%d%d%d", &a, &b, &m);
        int d = exgcd(a, m, x, y);
        if(b % d) printf("impossible\n");
        else printf("%d\n", (long long)x * (b / d) % m);
    }
}
```

## 204.表达整数的奇怪方式

## 883.高斯消元解线性方程组

![image-20231223162612820](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231223162612820.png)

![image-20231223182732942](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231223182732942.png)

![image-20231223182749103](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231223182749103.png)

```c++
/*
	高斯消元过程：
		for 枚举每i列
			找到该列中绝对值最大数的所在的行
			将该行和第i行交换
			将第i行的第i个数变为1
			消去该行往下所有行的第i个数
*/
#include <iostream>
#include <algorithm>
#include <cmath>
using namespace std;

const int N = 110;
const double e = 1e-6;

int n;
double a[N][N];
int gauss()
{
    int c, r;
    for(c = 0, r = 0; c < n; c++)
    {
        int t = r;
        for(int i = r; i < n; i++)
            if(fabs(a[i][c]) > fabs(a[t][c])) t = i;
        if(fabs(a[t][c]) < e) continue;
        for(int i = c; i <= n; i++) swap(a[t][i], a[r][i]);
        for(int i = n; i >= c; i--) a[r][i] /= a[r][c];
        for(int i = r + 1; i < n; i++)
            if(fabs(a[i][c]) > e)
            for(int j = n; j >= c; j--)
                a[i][j] -= a[i][c] * a[r][j];
        r++;
    }
    if(r < n)
    {
        for(int i = r; i < n; i++)
            if(fabs(a[i][n]) > e) return 0;
        return 2;
    }
    for(int i = n - 1; i >= 0; i--)
        for(int j = i + 1; j < n; j++)
            a[i][n] -= a[j][n] * a[i][j];
    return 1;
}
int main()
{
    cin >> n;
    for(int i = 0; i < n; i++)
        for(int j = 0; j < n + 1; j++)
            cin >> a[i][j];
    int t = gauss();
    if(t == 1) for(int i = 0; i < n; i++) printf("%.2lf\n", a[i][n]);
    else if(t == 0) cout << "No solution";
    else cout << "Infinite group solutions";
}
```

# 884.高斯消元解异或线性方程组

# 数学知识（三）

## 885.求组合数1

![image-20231223183435730](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231223183435730.png)

```c++
#include <iostream>
using namespace std;
const int N = 2010;
const int p = 1e9 + 7;
int c[N][N];

void init()
{
    for(int i = 0; i < N; i++)
        for(int j = 0; j <= i; j++)
            if(!j) c[i][j] = 1;
            else c[i][j] = (c[i - 1][j] + c[i - 1][j - 1]) % p;
}

int main()
{
    init();
    int n; cin >> n;
    while(n--)
    {
        int a, b; cin >> a >> b;
        cout << c[a][b] << endl;
    }
}
```

## 886.求组合数2

![image-20231223201457025](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231223201457025.png)

```c++
#include <iostream>
using namespace std;

const int N = 100010;
const int p = 1e9 + 7;
int fact[N];
int infact[N];

long long fast_power(int a, int k)
{
    long long res = 1;
    while(k)
    {
        if(k & 1) res = res * a % p;
        k >>= 1;
        a = (long long)a * a % p;
    }
    return res;
}

int main()
{
    int n; cin >> n;
    fact[0] = infact[0] = 1;
    for(int i = 1; i < N; i++)
    {
        fact[i] = (long long)fact[i - 1] * i % p;
        infact[i] = (long long)infact[i - 1] * fast_power(i, p - 2) % p;
    }
    while(n--)
    {
        int a, b;
        cin >> a >> b;
        cout << (long long)fact[a] * infact[b] % p * infact[a - b] % p << endl; 
    }
}
```

## 887.求组合数3

卢卡斯定理，求组合数
$$
\binom{b}{a} \equiv\binom{b\ \%\ p}{a\ \% \ p}\cdot\binom{b/p}{a/p}(mod\ p)
$$
![image-20231223221110721](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231223221110721.png)

```c++
#include <iostream>
using namespace std;
typedef long long LL;
int p;

LL fast_power(LL a, LL b)
{
    LL res = 1;
    while(b)
    {
        if(b & 1) res = res * a % p;
        b >>= 1;
        a = a * a % p;
    }
    return res;
}

LL C(int a, int b)
{
    LL res = 1;
    for(int i = 1, j = a; i <= b; i++, j--)
    {
        res = res * j % p;
        res = res * fast_power(i, p - 2) % p;
    }
    return res;
}

LL lucas(LL a, LL b)
{
    if(a < p && b < p) return C(a, b);
    return C(a % p, b % p) * lucas(a / p, b / p) % p;
}
int main()
{
    int n; cin >> n;
    while(n--)
    {
        LL a, b;
        cin >> a >> b >> p;
        cout << lucas(a, b) << endl;
    }
}
```

## 888.求组合数4

![image-20240102173411435](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240102173411435.png)

```c++
#include <iostream>
#include <vector>
using namespace std;

const int N = 5010;
int primes[N], cnt;
int sum[N]; // sum[i] 存放的是 primes[i]在组合数中出现的次数（分解质因子后primes[i]的指数）
int st[N];

void get_primes(int n)
{
    for(int i = 2; i <= n; i++)
    {
        if(!st[i]) primes[cnt++] = i;
        for(int j = 0; primes[j] <= n / i; j++)
        {
            st[primes[j] * i] = true;
            if(i % primes[j] == 0) break;
        }
    }
}
/*
    get(n, p) 返回的是n的阶乘n!中 有多少个 p 相乘(p为质数)
    示例1：get(14, 3) = 5
            3  6  9  12   4个
            9             1个 一共5个
    示例2：get(16, 2) = 15
            2  4  6  8  10  12  14  16  
            4  8  12  16            
            8  16
            16          8 + 4 + 2 + 1 = 15。16的阶乘中15个2相乘，或者说16!分解质因子后，2的指数为15
*/
int get(int n, int p)
{
    int res = 0;
    while(n)
    {
        res += n / p;
        n /= p;
    }
    return res;
}
//  高精度乘法
vector<int> mul(vector<int>& a, int b)
{
    vector<int> c;
    int t = 0;
    for(int i = 0; i < (int)a.size(); i++)
    {
        t += a[i] * b;
        c.push_back(t % 10);
        t /= 10;
    }
    while(t)
    {
        c.push_back(t % 10);
        t /= 10;
    }
    return c;
}

int main()
{
    int a, b; cin >> a >> b;
    get_primes(a);
    
    for(int i = 0; i < cnt; i++)
    {
        int p = primes[i];
        sum[i] = get(a, p) - get(b, p)- get(a - b, p);
    }
    
    vector<int> res;
    res.push_back(1);
    
    for(int i = 0; i < cnt; i++)
        for(int j = 1; j <= sum[i]; j++)
            res = mul(res, primes[i]);
            
    for(int i = res.size() - 1; i >= 0; i--) cout << res[i];
    // cout << endl;
    
}
```

## 889.满足条件的01序列

![image-20240102173449448](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240102173449448.png)

卡特兰数
$$
\binom{n}{2n} - \binom{n - 1}{2n} = \frac{1}{n+1}\frac{2n!}{(n!)(n!)}
$$

```c++
#include <iostream>
using namespace std;
typedef long long LL;

const int p = 1e9 + 7;

LL fast_power(int x, int k)
{
    LL res = 1;
    while(k)
    {
        if(k & 1) res = (LL)res * x % p;
        k >>= 1;
        x = (LL)x * x % p;
    }
    return res;
}

int main()
{
    LL n; cin >> n;
    LL res = 1;
    for(LL i = 2 * n; i > n; i--) res = (LL)res * i % p;
    for(LL i = 1; i <= n; i++) res = (LL)res * fast_power(i, p - 2) % p;
    res = res * fast_power(n + 1, p - 2) % p;
    cout << res;
}
```

# 数学知识（四）

## 890.能被整除的数

容斥原理

![image-20240102174359973](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240102174359973.png)

![image-20240102174956109](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240102174956109.png)



```c++
#include <iostream>
using namespace std;
typedef long long LL;
int p[20];

int main()
{
    int n, m; cin >> n >> m;
    for(int i = 0; i < m; i++) cin >> p[i];
    int res = 0;
    for(int i = 1; i < 1 << m; i++)
    {
        LL t = 1, cnt = 0;
        for(int j = 0; j < m; j++)
            if(i >> j & 1)
            {
                cnt++;
                if(t * p[j] > n)
                {
                    t = -1;
                    break;
                }
                t *= p[j];
            }
        if(t != -1)
        {
            if(cnt % 2) res += n / t;
            else res -= n / t;
        }
    }
    cout << res;
}
```

## 891.Nim游戏

![image-20240102185045614](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240102185045614.png)

```c++
/*
	异或为0，先手必败。
	异或非0，先手必胜。
	
	异或为0，后续一定是必胜态。 然后必胜必败相互交替，
	异或非0，后续存在一个必败态。
*/
#include <iostream>
using namespace std;
int main()
{
    int n; cin >> n;
    int res = 0;
    while(n--)
    {
        int x; cin >> x;
        res ^= x;
    }
    if(res) cout << "Yes";
    else cout << "No";
}
```

# 892.台阶Nim游戏

## 893.集合Nim游戏

![image-20240103121451802](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240103121451802.png)

![image-20240103121501311](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240103121501311.png)

```C++
/*
Mex运算：找到集合中 不存在的最小自然数
*/
/*
SG函数：1.SG(终点) = 0
	   2.SG(x) = Mex{SG(y1), SG(y2), ... SG(yk)},其中yi是x能到达的点
*/

/*
当只有一个图的时候，SG(x) = 0 必败(0状态是走不到0的)
		     	 SG(x) != 0 必胜(非0状态至少存在一条路径可以到0状态)：举例4->0, 4->2->0, 13->6->0
*/
#include <iostream>
#include <cstring>
#include <unordered_set>
using namespace std;
const int N = 110;
const int M = 10010;
int f[M];
int s[N];
int k;
int sg(int x)
{
    if(f[x] != -1) return f[x];
    unordered_set<int> S;
    for(int i = 0; i < k; i++)
        if(x >= s[i]) S.insert(sg(x - s[i]));
    for(int i = 0;;i++)
        if(!S.count(i)) return f[x] = i;
}

int main()
{
    memset(f, -1, sizeof f);
    cin >> k;
    for(int i = 0; i < k; i++) cin >> s[i];
    int n; cin >> n;
    int res = 0;
    while(n--)
    {
        int x; cin >> x;
        res ^= sg(x);
    }
    if(res) cout << "Yes";
    else cout << "No";
}
```

# 894.拆分Nim游戏

# 动态规划（一）

## 2.01背包问题

![image-20240103165848347](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240103165848347.png)

![image-20240103165857460](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240103165857460.png)

```c++
/*
01背包：每件物品使用一次
完全背包：每件物品使用无限次次
多重背包：每件物品有限个（朴素、优化）
分组背包：物品n组，每组物品有若干个（水果组、蔬菜组、肉组中每组只能选一个，组内互斥）
```

动态规划

```
DP: 1.状态表示(需要几维)	f[i, j]
    	1.集合	所有选法：条件1只从前i个物品中选。条件2总体积 <= j
    	2.属性	1.Max 2.Min 3.数量
    2.状态计算
		集合的划分：1.包含i 2.不包含i
         集合划分原则：不重复、不漏掉
```

```c++
/*	二维	*/
#include <iostream>
using namespace std;
const int N = 1010;
const int V = 1010;
int f[N][V];
int w[N];
int v[N];

int main()
{
    int n, m; cin >> n >> m;
    for(int i = 1; i <= n; i++) cin >> v[i] >> w[i];
    // f[0][...]
    for(int i = 1; i <= n; i++)
        for(int j = 0; j <= m; j++)
        {
            f[i][j] = f[i - 1][j];
            if(j >= v[i]) f[i][j] = max(f[i][j], f[i - 1][j - v[i]] + w[i]);
        }
    cout << f[n][m];
}
```

一维优化

```c++
#include <iostream>
using namespace std;
const int N = 1010;
const int V = 1010;
int f[V];
int w[N];
int v[N];

int main()
{
    int n, m; cin >> n >> m;
    for(int i = 1; i <= n; i++) cin >> v[i] >> w[i];
    // f[0][...]
    for(int i = 1; i <= n; i++)
        for(int j = m; j >= v[i]; j--)
            f[j] = max(f[j], f[j - v[i]] + w[i]);
    cout << f[m];
}
```

## 3.完全背包问题

![image-20240103173225172](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240103173225172.png)

![image-20240103173234951](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240103173234951.png)

![image-20240103171547372](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240103171547372.png)

**超时朴素写法：可以看出来01背包是完全背包的一种特例，完全背包是01背包的一般形式**

```c++
#include <iostream>
using namespace std;
const int N = 1010;
const int V = 1010;
int w[N];
int v[N];
int f[N][V];

int main()
{
    int n, m; cin >> n >> m;
    for(int i = 1; i <= n; i++) cin >> v[i] >> w[i];
    
    for(int i = 1; i <= n; i++)
        for(int j = 0; j <= m; j++)
            for(int k = 0; k <= j / v[i]; k++)
                f[i][j] = max(f[i][j], f[i - 1][j - k * v[i]] + k * w[i]);
    cout << f[n][m];
}
```

二维优化

```
f[i][j]   = max(f[i-1][j], f[i-1][j-v] + w, f[i-1][j-2v] + 2w, f[i-1][j-3v] + 3w...)
f[i][j-v] = max(           f[i-1][j-v],     f[i-1][j-2v] + w,  f[i-1][j-3v] + 2w...)
得出
f[i][j] = max(f[i-1][j], f[i][j-v] + w)
```

```c++
#include <iostream>
using namespace std;
const int N = 1010;
const int V = 1010;
int w[N];
int v[N];
int f[N][V];

int main()
{
    int n, m; cin >> n >> m;
    for(int i = 1; i <= n; i++) cin >> v[i] >> w[i];
    
    for(int i = 1; i <= n; i++)
        for(int j = 0; j <= m; j++){
            f[i][j] = f[i - 1][j];
            if(j >= v[i]) f[i][j] = max(f[i][j], f[i][j - v[i]] + w[i]);
        }
    cout << f[n][m];
}
```

一维优化

```c++
#include <iostream>
using namespace std;
const int N = 1010;
const int V = 1010;
int w[N];
int v[N];
int f[V];

int main()
{
    int n, m; cin >> n >> m;
    for(int i = 1; i <= n; i++) cin >> v[i] >> w[i];
    
    for(int i = 1; i <= n; i++)
        for(int j = v[i]; j <= m; j++)
            f[j] = max(f[j], f[j - v[i]] + w[i]);
    cout << f[m];
}
```

## 4.多重背包问题

![image-20240103173937521](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240103173937521.png)

![image-20240103174006453](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240103174006453.png)

```c++
#include <iostream>
using namespace std;
const int N = 1010;
const int V = 1010;
int v[N];
int w[N];
int s[N];
int f[N][V];

int main()
{
    int n, m; cin >> n >> m;
    for(int i = 1; i <= n; i++) cin >> v[i] >> w[i] >> s[i];
    for(int i = 1; i <= n; i++)
        for(int j = 0; j <= m; j++)
            for(int k = 0; k <= min(j / v[i], s[i]); k++)
                f[i][j] = max(f[i][j], f[i - 1][j - k * v[i]] + k * w[i]);
    cout << f[n][m];
}
```

## 5.多重背包问题2

![image-20240103174521661](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240103174521661.png)

![image-20240103174531667](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240103174531667.png)

优化

```
f[i][j] =   max(f[i-1][j], f[i-1][j-v]+w, f[i-1][j-2v] + 2w, ... f[i-1][j-sv] + sw)
f[i][j-v] = max(           f[i-1][j-v],   f[i-1][j-2v] + w,   ...f[i-1][j-sv] + (s-1)w, f[i-1][j-sv] + sw)
```

```c++
#include <iostream>
using namespace std;
const int N = 11001;
const int V = 2010;
int v[N];
int w[N];
int f[V];

int main()
{
    int n, m; cin >> n >> m;
    int cnt = 0;
    for(int i = 1; i <= n; i++)
    {
        int a, b, s; cin >> a >> b >> s;
        for(int k = 1; k <= s; k <<= 1){
            cnt++;
            v[cnt] = k * a;
            w[cnt] = k * b;
            s -= k;
        }
        if(s > 0) {
            cnt++;
            v[cnt] = s * a;
            w[cnt] = s * b;
        }
    }
    for(int i = 1; i <= cnt; i++)
        for(int j = m; j >= v[i]; j--)
            f[j] = max(f[j], f[j - v[i]] + w[i]);
    cout << f[m];
    
}
```

## 9.分组背包问题

![image-20240103202850015](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240103202850015.png)

![image-20240103202858664](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240103202858664.png)

```c++
/*二维*/
#include <iostream>
using namespace std;
const int N = 105;
int v[N][N], w[N][N], s[N];
int f[N][N];

int main()
{
    int n, m; cin >> n >> m;
    for(int i = 1; i <= n; i++)
    {
        cin >> s[i];
        for(int j = 1; j <= s[i]; j++)
            cin >> v[i][j] >> w[i][j];
    }
    
    for(int i = 1; i <= n; i++)
        for(int j = 0; j <= m; j++)
        {
            f[i][j] = f[i - 1][j];
            for(int k = 1; k <= s[i]; k++)
                if(j >= v[i][k]) f[i][j] = max(f[i][j], f[i - 1][j - v[i][k]] + w[i][k]);
        }
    cout << f[n][m];
}
```

```c++
#include <iostream>
using namespace std;
const int N = 105;
int v[N][N], w[N][N], s[N];
int f[N];

int main()
{
    int n, m; cin >> n >> m;
    for(int i = 1; i <= n; i++)
    {
        cin >> s[i];
        for(int j = 1; j <= s[i]; j++)
            cin >> v[i][j] >> w[i][j];
    }
    
    for(int i = 1; i <= n; i++)
        for(int j = m; j >= 0; j--)
            for(int k = 1; k <= s[i]; k++)
                if(j >= v[i][k]) f[j] = max(f[j], f[j - v[i][k]] + w[i][k]);
    cout << f[m];
}
```





















# 动态规划（二）

















































## 898.数字三角形

![image-20231226234037778](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231226234037778.png)

![image-20231226234049319](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231226234049319.png)

```c++
#include <iostream>
using namespace std;
const int N = 510;
int a[N][N];
int f[N][N];
int main()
{
    int n; cin >> n;
    for(int i = 1; i <= n; i++)
        for(int j = 1; j <= i; j++)
            cin >> a[i][j];
            
    for(int i = 0; i <= n; i++)
        for(int j = 0; j <= i + 1; j++)
            f[i][j] = -1e9;	// 因为是最大值，因此初始化为一个很小的数，这里j从0到i+1，要多初始化两列
    f[1][1] = a[1][1];	// 初始条件
    
    for(int i = 2; i <= n; i++)
        for(int j = 1; j <= i; j++)
            f[i][j] = max(f[i-1][j-1] + a[i][j], f[i-1][j] + a[i][j]);
    
    int res = f[n][n];
    for(int i = 1; i <= n; i++)
        res = max(res, f[n][i]);
    cout << res;
}
```

## 895.最长上升子序列

![image-20231227200543071](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20231227200543071.png)

```c++
/*
	动态规划：状态表示f[i]：集合：所有以i结尾的上升子序列
						属性：长度的最大值
*/
#include <iostream>
using namespace std;
const int N = 1010;
int a[N];
int f[N];
// int g[N];
int main()
{
    int n; cin >> n;
    for(int i = 1; i <= n; i++)
        cin >> a[i];
        
    for(int i = 1; i <= n; i++)
    {
        f[i] = 1;
        // g[i] = 0;
        for(int j = 1; j < i; j++)
            if(a[i] > a[j])
                if(f[i] < f[j] + 1)
                // {
                    f[i] = f[j] + 1;
                    // g[i] = j;	// 记录i是由哪个j转移过来的
                // }
    }
    int res = 0;
    int k = 0;
    for(int i = 1; i <= n; i++)
        if(f[i] > f[k])
        {
            res = f[i];
            k = i;
        }
    cout << res << endl;
    // for(int i = 0; i < res; i++)
    // {
    //     cout << a[k] << " ";
    //     k = g[k];			
    // }
}
```

# 896.最长上升子序列2

```c++
/*
	一个长度为n的序列
	我们把长度为k的上升子序列，结尾的最小值取出来，就是一个严格单调递增的序列 k = 1,2,3,...n
	证明：假设长度为k的上升子序列结尾最小值，小于长度为k-1的上升子序列的最小值，那么长度为k-1的上升子序列的最小值，就应该比其当前的值小，这就矛盾了。
*/
```











## 897.最长公共子序列

![image-20240103225649169](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240103225649169.png)

```c++
动态规划 状态表示	1.集合：f[i][j],所有在第一个序列中的前i个字母中出现，并且在第二个序列的前j个字母中出现的子序列
    	   		  2.属性：Max
    	状态计算
```

```c++
#include <iostream>
using namespace std;
const int N = 1010;
char a[N], b[N];
int f[N][N];
int main()
{
    int n, m; cin >> n >> m;
    scanf("%s %s", a + 1, b + 1);
    for(int i = 1; i <= n; i++)
        for(int j = 1; j <= m; j++)
        {
            if(a[i] == b[j]) f[i][j] = f[i - 1][j - 1] + 1;
            else f[i][j] = max(f[i - 1][j], f[i][j - 1]);
        }
    cout << f[n][m];
}
```

# 899.编辑距离

# 902.最短编辑距离

## 282.合并石子

![image-20240104003028321](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240104003028321.png)

![image-20240104003039339](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240104003039339.png)

```c++
动态规划：状态表示f[i][j]：集合：所有将第i堆石子，到第j堆石子合并成一堆石子的合并方式
    				    属性：Min
	     状态计算：分类，最后一次合并的分界线来分类。
```

```c++
#include <iostream>
using namespace std;
const int N = 310;
int s[N];
int f[N][N];
int main()
{
    int n; cin >> n;
    for(int i = 1; i <= n; i++) cin >> s[i];
    for(int i = 1; i <= n; i++) s[i] += s[i - 1];
        
    for(int len = 2; len <= n; len++)
        for(int i = 1; i + len - 1 <= n; i++)
        {
            int l = i, r = i + len - 1;
            f[l][r] = 1e8;
            for(int k = l; k < r ; k++)
                f[l][r] = min(f[l][r], f[l][k] + f[k + 1][r] + s[r] - s[l - 1]);
        }
    cout << f[1][n];
}
```



# 动态规划（三）

## 338.计数问题

![image-20240104114539767](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240104114539767.png)

![image-20240104114600088](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20240104114600088.png)

``` 
count(n, x); // 求出 1 - n 中 数字x出现的次数
1 ~ abcdefg 中第4位(第4位是从右到左数，个、十、百、千)上 3 出现的次数
1. 如果 xxx < abc 000 ~ abc - 1 后三位000~999随便取，结果 ： abc * 1000;
2. 如果 xxx = abc d < 3 : 结果：0
                  d = 3 : 000 ~ efg 结果：efg + 1
                  d > 3 : 000 ~ 1000 结果：1000
边界	1.如果求某个数在个位上出现的次数，情况1.就不需要算
      2.如果求0在某位出现次数，前缀不能是前导0
```







# 贪心算法（一）



# 贪心算法（二）













