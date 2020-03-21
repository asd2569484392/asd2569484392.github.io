## string vector 数组的基本使用

### string

```c++
	string word;
	//输入什么打印什么 
	while (cin >> word)
		cout << word << endl;
	
	
	//getline 读取一整行
	string line;
	while (getline(cin,line))
	{
		cout << line << endl;
	}

	//遇到空行跳过
	string line;
	while(getline(cin,line))
		if (!line.empty())
		{
			cout << line << endl;
		}


	string ok = "abcdefg";
	//全部替换成x
	for (int i = 0; i < ok.size(); i++)
	{
		ok[i] = 'x';
	}
	cout << ok << endl;

```



## verctor

集合，与ListArray类似。

需要引入 : #include<vector>

使用 :

```c++
	vector<int> number (10, 1);
	for (int i = 0; i < number.size(); i++)
	{
		cout << number[i] << endl;//输出111111111
	}
	number.push_back(0);
	//push 0

	//number.pop_back();
	//pop 0
	
	for (int i = 0; i < number.size(); i++)
	{
		cout << number[i] << endl;//输出111111111
	}

```



练习  :

```c++
//不合法,因为icec没有初始化长度
	vector<int> ivec;
	ivec[0] = 42;
	//出错了
	cout << ivec[0] << endl;
	//改进 vector<int> ivec(1); 或 vector<int> = {42}
```



## 迭代

```c++
string s("some string");
	if (s.begin() != s.end()) 
	{
		auto it = s.begin();
		*it = toupper(*it); //*it解引用
	}
	cout << s << endl;//Some string
```

注意，*解引用赋值。



**循环加条件**

```c++
	string s("some string");
	for (auto it = s.begin(); it != s.end() && !isspace(*it); ++it) {
		*it = toupper(*it);
	}
	cout << s << endl; //SOME string
```



**解引用对象访问**

如果迭代一个verctor，如何对迭代中的对象进行操作？

比如迭代verctor<string>，那么如何在迭代中判断值是否为空？

```c++
(*it).empty();
```

注意 : 必须加上()。

**练习**

```c++
//练习，用迭代器输出向量 
	vector<int> test(10, 56);
	for (auto it = test.begin(); it != test.end(); it++)
	{
		cout << *it << endl;
	}

//创建含有十个整数的verctor，用迭代器将所有值*2
	vector<int> ivec(10, 666);
	for (auto it = ivec.begin(); it != ivec.end(); it++) {
		*it = *it * 2;
	}
	for (auto it = ivec.begin(); it != ivec.end(); it++) {
		cout << *it << endl;
	}
	//1332
```

迭代器经典算法 : 二分查找

获取有序集合中间数，如果找的数下标小于中间数从前半部分查找，否则从后半部分查找，如果等于中间数直接返回。

```c++
    //二分查找

    string text("ASDFGHJKLQWERTYUIOOPZXCVBNMM");

    auto begin = text.begin(), end = text.end();
    auto mid = text.begin() - (end - begin) / 2; //初始状态下的中心点
    //遍历一遍
//    for (char &it : text) {
//        cout << it << endl;
//    }

    cout << *mid << endl;
    char sougth = 'f';
    while (mid != end && *mid != sougth) {

        if (sougth < *mid) { //判断要查找的元素在前半段还是后半段
            end = mid; //前半段
        } else {
            begin = mid + 1;//后半段
        }
        mid = begin + (end - begin) / 2; //如果还能分割，那么重新定义中心点
    }
    cout << *mid << endl;

```

其中 

```c++
begin = mid + 1
```

为什么mid要+1？

```
ASDFGHJKLQWERTYUIOOPZXCVBNMM  //find K
mid = ASDFGHJKLQWERTYUIOOPZXCVBNMM /2
比如mid = Y
如果 mid != Y
那么Y是不是要排除？
begin 是A end i是 M mid 是 Y
如果是后半段,不 -1 的检索范围是 YUIOOPZXCVBNMM 
-1 后是 UIOOPZXCVBNMM 
```



## 数组

```c++
    //array
    //数组的部分与Java类似，不过加入指针的情况还是要留意的 如：
    int *parr[cnt]; //这里存放的都是int类型指针
    //初始化情况

    int testArr[5] = {1,2,3}; //结果是 {1,2,3,0,0}

```

#### **迭代**

没明白什么意思的程序：

```c++
    unsigned scores[11] = {};
    unsigned grade;
    while (cin >> grade) {
        if (grade <= 100)
            ++scores[grade / 10];
    }//一直cin 

    for (auto i : scores) {
        cout << i << endl;
    }
```



#### **练习**

```c++
    //写一个程序，定义含有10个int的数组，令每个元素的值都是下标
    //size_t 表示数组长度和下标？
    constexpr size_t arr_size = 10;
    //初始化值都是0
    int arr[arr_size] = {};

    for (int i = 0; i < arr_size; ++i) {
        arr[i] = i;
    }

    for (auto val:arr) {
        cout << val << endl;
    }
    //输出 0123456789 正确
```



#### 指针和数组

```c++
 string nums[] = {"one","two","three"};
 string *sp = &nums[0];
 cout<<*sp<<endl;//one

string *p2 = nums;
cout<<*p2<<endl;//one
```



在很多用到数组的地方，编译器都会自动地将其转换为一个指向数组首元素的指针。



```c++
    int ia[10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};

	//指针循环
    int *e = &ia[10]; //×e 指向 ia最后一个元素 *a指向ia第一个元素
    for (int *a = ia; a != e; ++a) {
        cout << *a << endl;
    }
```





#### 练习

用指针将数组元素置为0，比较两个数组是否相等。

```c++
    int iarr[10] = {0, 1, 2, 3, 4, 5, 6, 7, 8};
    int *p = iarr;
    while (p != &iarr[10]) {
        *p = 0;
        p++;
    }

    for (int i : iarr) {
        cout << i << endl; //都是0
    }

    //比较两个数组是否相等？ 不太明白，是比较内存地址还是比较数组所以元素长度是否相等？不过内存地址肯定是不同的
    int arr1[10] = {0, 1, 2, 3, 4, 5, 6, 7};
    int arr2[10] = {0, 1, 2, 3, 66, 5, 6, 7};
    int *e1 = &arr1[10], *e2 = &arr2[10];

    for (int *a1 = arr1, *a2 = arr2; a1 != e1 && a2 != e2; a1++ && a2++) {
        if (*a1 != *a2){
            cout<<"不相等"<<endl;
            break;
        }
    }
```





### C风格



|      | 函数          |                          说明                           |
| ---- | ------------- | :-----------------------------------------------------: |
|      | strlen(p)     |                       返回P的长度                       |
|      | strcmp(p1,p2) | 比较p1==p2，相等返回0。如果p1>p2返回正值，p1<p2返回负值 |
|      | strcpy(p1,p2) |                      将p2拷贝给p1                       |
|      |               |                                                         |

### 使用数组初始化vector

```c++
    //使用数组初始化vector
    int arr[10] = {0,1,2,3,4,5,6,7,8};
    vector<int> ive(begin(arr),end(arr));
    for(int & it : ive){
        cout<<it<<endl;
    }

```









