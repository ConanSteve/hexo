---
title: C++基础知识
date: 2022-02-01 10:00:00
author: 陌上人如玉
hide: trueS
---

# 基础

# STL

## string

### 基本操作

```
s.empty()
s.size()
```

读写一行字符串：`getline(cin, line)`



> atoi(char) 头文件 #include <cstdlib>
> `atoi(line.c_str())`记住要转为C风格字符串

### 处理string中的字符

头文件：`#include <cctype>`
> 是否是字符数字：` isalnum(c)`
> 是否是字母：`isalpha(c)`
> 是否是小写字母：`islower(c)`
> 是否是大写字母：`isupper(c)`
> 是否是数字：`isdigit(c)`
> 是否是16进制数字：`isxdigit(c)`
> 转小写字母：`tolower(c)`
> 转大写字母：`toupper(c)`
> 是否是标点符号：`ispunct(c)`

#### Demo code

```C++
#include <iostream>
#include <string>
#include <cctype>
using namespace std;

int main()
{
    string input;
    getline(cin,input);
    cout<<"sentence："+input<<endl;
    string s="Hello World!!!";
    int cnt_punct=0;
    for(auto c :s)
    {
        if(ispunct(c))
        {
            ++cnt_punct;
        }
    }
    cout<<cnt_punct<<endl;
    return 0;
}
```
`string.split()`

```C++
#include <iostream>
#include <string>
#include <vector>
using namespace std;


void Stringsplit(const string& str, const char split, vector<string>& res)
{
    if (str == "")      return;
    //在字符串末尾也加入分隔符，方便截取最后一段
    string strs = str + split;
    size_t pos = strs.find(split);

    // 若找不到内容则字符串搜索函数返回 npos
    while (pos != strs.npos)
    {
        string temp = strs.substr(0, pos);
        res.push_back(temp);
        //去掉已分割的字符串,在剩下的字符串中进行分割
        strs = strs.substr(pos + 1, strs.size());
        pos = strs.find(split);
    }
}

// 使用字符串分割
void Stringsplit(const string& str, const string& splits, vector<string>& res)
{
    if (str == "")      return;
    //在字符串末尾也加入分隔符，方便截取最后一段
    string strs = str + splits;
    size_t pos = strs.find(splits);
    int step = splits.size();

    // 若找不到内容则字符串搜索函数返回 npos
    while (pos != strs.npos)
    {
        string temp = strs.substr(0, pos);
        res.push_back(temp);
        //去掉已分割的字符串,在剩下的字符串中进行分割
        strs = strs.substr(pos + step, strs.size());
        pos = strs.find(splits);
    }
}


int main()
{
    vector<string> strList;
    string str("This-is-a-test");
    Stringsplit(str, '-', strList);
    for (auto s : strList)
        cout << s << " ";
    cout << endl;

    vector<string> strList2;
    string str2("This%20is%20a%20test");
    Stringsplit(str2, "%20", strList2);
    for (auto s : strList2)
        cout << s << " ";
    cout << endl;
    return 0;
}
```

[C++ string详解，C++字符串详解](http://c.biancheng.net/view/2236.html)

[C++ string的常用操作](https://www.jianshu.com/p/7b0e25d6c2c8)

## List 双向链表

[C++ list（STL list）容器完全攻略（超级详细）](http://c.biancheng.net/view/6892.html)

## Array

```c++
#include <iostream>
#include <array>
using namespace std;
int main()
{
    array<int, 4> values{};
    //初始化 values 容器为 {0,1,2,3}
    for (int i = 0; i < values.size(); i++) {
        values.at(i) = i;
    }
    //使用 get() 重载函数输出指定位置元素
    cout << get<3>(values) << endl;
    //如果容器不为空，则输出容器中所有的元素
    if (!values.empty()) {
        for (auto val = values.begin(); val < values.end(); val++) {
            cout << *val << " ";
        }
    }
}
```

[C++ array(STL array)容器用法详解](http://c.biancheng.net/view/6688.html)

## vector

尾部添加元素：`push_back()`

```c++
#include <iostream>
#include <vector>
using namespace std;



int main() {
    vector<int> vals,sub;
    vals.push_back(1);
    vals.push_back(1);
    vals.push_back(1);
    sub.push_back(2);
    sub.push_back(2);
    vals.insert(vals.begin()+1,sub.begin(), sub.end());
    for(auto a:vals) cout<<a<<" ";

    return 0;
}
```

[C++ STL vector容器详解](http://c.biancheng.net/view/6749.html)

## Queue



queue 和 stack 有一些成员函数相似，但在一些情况下，工作方式有些不同：

- front()：返回 queue 中第一个元素的引用。如果 queue 是常量，就返回一个常引用；如果 queue 为空，返回值是未定义的。

- back()：返回 queue 中最后一个元素的引用。如果 queue 是常量，就返回一个常引用；如果 queue 为空，返回值是未定义的。

- push(const T& obj)：在 queue 的尾部添加一个元素的副本。这是通过调用底层容器的成员函数 push_back() 来完成的。

- push(T&& obj)：以移动的方式在 queue 的尾部添加元素。这是通过调用底层容器的具有右值引用参数的成员函数 push_back() 来完成的。

- pop()：删除 queue 中的第一个元素。

- size()：返回 queue 中元素的个数。

- empty()：如果 queue 中没有元素的话，返回 true。

- emplace()：用传给 emplace() 的参数调用 T 的构造函数，在 queue 的尾部生成对象。

- swap(queue<T> &other_q)：将当前 queue 中的元素和参数 queue 中的元素交换。它们需要包含相同类型的元素。也可以调用全局函数模板 swap() 来完成同样的操作。

```C++
#include <iostream>
#include <string>
#include <queue>
#include <deque>
using namespace std;

int main()
{
    deque<double> values {1.5, 2.5, 3.5, 4.5}; 
    queue<double> numbers(values);
    for(int i=0;i<5;++i)
    {
        numbers.push(i); //队尾添加元素
    }

    while (!numbers.empty())
    {
        cout <<numbers.front() << " "; // 查询队首
        numbers.pop();  // 弹出队首
    }
    cout<<endl;
    return 0;
}
```

[C++ queue(STL queue)用法详](http://c.biancheng.net/view/479.html)**[解](http://c.biancheng.net/view/479.html)**

## deque 双边队列

[C++ STL deque容器（详解版）](http://c.biancheng.net/view/6860.html)

## stack

下面是 stack 容器可以提供的一套完整操作：

- top()：返回一个栈顶元素的引用，类型为 T&。如果栈为空，返回值未定义。

- push(const T& obj)：可以将对象副本压入栈顶。这是通过调用底层容器的 push_back() 函数完成的。

- push(T&& obj)：以移动对象的方式将对象压入栈顶。这是通过调用底层容器的有右值引用参数的 push_back() 函数完成的。

- pop()：弹出栈顶元素。

- size()：返回栈中元素的个数。

- empty()：在栈中没有元素的情况下返回 true。

- emplace()：用传入的参数调用构造函数，在栈顶生成对象。

- swap(stack<T> & other_stack)：将当前栈中的元素和参数中的元素交换。参数所包含元素的类型必须和当前栈的相同。对于 stack 对象有一个特例化的全局函数 swap() 可以使用。

### Demo code

```C++
#include <iostream>
#include <string>
#include <stack>
#include <list>
using namespace std;

int main()
{   
    list<string> ls{"java","python","go","c++"};
    stack<string,list<string>> st(ls);
    st.emplace("ruby");
    while(!st.empty())
    {
        cout<<st.top()<<endl;
        st.pop();
    }
    return 0;
```

[C++ stack(STL stack)用法详解](http://c.biancheng.net/view/478.html)

## map

底层用的红黑树，会自动按照key排序，如果不需要排序，建议使用`unordered_map`

```C++
#include <iostream>
#include <string>
#include <map>
using namespace std;

int main()
{   
    map<string, int> myMap{ {"c",10},{"d",20} };
    map<string, int>newMap(++myMap.begin(), myMap.end());
    myMap.insert(make_pair("java",30));    
    myMap.emplace(pair<string, int>("go", 5));
    myMap.emplace(make_pair("C++",40));
    auto itera = myMap.find("java");
    if(itera!= myMap.end()){
        cout<<itera->second;
    }
    for(auto p : myMap)
    {
        cout<<p.first<<"\t"<<p.second<<endl;
    }
    return 0;
}
```

[C++ STL map容器详解](http://c.biancheng.net/view/7173.html)

[C++ STL unordered_map容器用法详解](http://c.biancheng.net/view/7231.html)



## Set

```C++
#include <iostream>
#include <string>
#include <set>
using namespace std;

int main()
{   
    set<string> sets{"c++","java","go"};
    sets.insert("python");
    for(auto a : sets)
    {
        cout<<a<<endl;
    }
    sets.erase();  
    return 0;
}
```

[C++ set容器（STL set容器）](http://c.biancheng.net/stl/set/)

[C++ STL set容器完全攻略（超级详细）](http://c.biancheng.net/view/7192.html)

## 泛型算法

#include <algorithm>

```
swap(a,b)
```

reverse()

sort()

```C++
#include <iostream>
#include <string>
#include <array>
#include <algorithm>
using namespace std;
int main()
{   
    array<int,7> a{0,6,3,2,4,5,1};
    array<int,4> b{2,7,5,3};
    
    sort(a.begin(),a.end());
    for(auto t:a)
        cout<<t<<"\t";
    cout<<endl;

    sort(a.begin(),a.end(),[](int a, int b) -> bool { return a > b; });
    for(auto t:a)
        cout<<t<<"\t";
    cout<<endl;

    reverse(a.begin(),a.end());
    for(auto t:a)
        cout<<t<<"\t";
    cout<<endl;

    return 0;
}
```

[C++ unique(STL unique)算法详解](http://c.biancheng.net/view/607.html)

```C++
#include <iostream>
#include <string>
#include <algorithm>
#include <iterator>
#include <array>
using namespace std;

int main()
{   
    // int a[] = {1,2,3,7,6,3,4};
    array<int,7> a{1,2,3,7,6,3,4};
    cout<<sizeof(a)/sizeof(int)<<endl;
    sort(begin(a), end(a));
    for(auto t:a)
    {
        cout<<t<<" ";
    }
    cout<<endl;
    auto end_iter = unique(begin(a), end(a));
    copy(begin(a), end(a), ostream_iterator<int>{cout, " "});
    cout<<endl;
    for(auto t:a)
    {
        cout<<t<<" ";
    }
    return 0;
}
```

[常用算法](https://www.cnblogs.com/ylaoda/p/11412081.html)

## Lamda

[C++11 lambda表达式精讲](http://c.biancheng.net/view/3741.html)

[C++11 lambda表达式](https://www.cnblogs.com/DswCnblog/p/5629165.html)

min_element()

partition()

```Julia
partition(nums.begin(), nums.end(), [](const int n){ return n&1; });
```

# 面试宝典

[史上最全的C++面试宝典（合集）](https://blog.csdn.net/qq_35034604/article/details/107959429)

[C/C++面试宝典2020版(最新版)](https://blog.csdn.net/y601500359/article/details/105262815)

# 待定

###### HelloWorld

```C++
#include <iostream>
using namespace std;
int main()
{
    cout<<"HelloWorld!"<<endl;    
    system("pause");
    return 0;
}
```

###### 输入输出

```C++
#include <iostream>
#include <string>
#include <vector>
using namespace std;

int main()
{
    string input;
    // Hello World!
    while(getline(cin,input))
    {
        cout<<"sentence："+input<<endl;
        vector<string>  strs;
              
    }

    cout<<"Hello World"<<endl;
    return 0;
}
```