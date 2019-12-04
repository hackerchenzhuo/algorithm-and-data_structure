# 原创：STL--queue学习笔记

# [STL--queue学习笔记](https://www.cnblogs.com/LjwCarrot/p/9050623.html)

# &lt;queue&gt;

只能访问queue&lt;T&gt;容器适配器的第一个和最后一个元素。只能在容器的末尾添加新元素，只能从头部移除元素。FIFO（先进先出）

### 1.初始化

> 
需要头文件&lt;queue&gt;
queue&lt;int&gt;que;


 

### 2.成员函数

> 
C++队列Queue类成员函数如下:
back()返回最后一个元素
empty()如果队列空则返回真
front()返回第一个元素
pop()删除第一个元素
push()在末尾加入一个元素
size()返回队列中元素的个数


 

### 3.queue 的基本操作举例如下：

> 
queue入队，如例：q.push(x); 将x 接到队列的末端。
queue出队，如例：q.pop(); 弹出队列的第一个元素，注意，并不会返回被弹出元素的值。
访问queue队首元素，如例：q.front()，即最早被压入队列的元素。
访问queue队尾元素，如例：q.back()，即最后被压入队列的元素。
判断queue队列空，如例：q.empty()，当队列空时，返回true。
访问队列中的元素个数，如例：q.size()


 

### queue队列中没有clear（）操作：

### 因此清空队列有几种方法：

 

**第一种：直接用空的队列对象赋值**

> 
<pre>
queue&lt;int&gt;q1
q1=queue&lt;int&gt;();</pre>


**第二种：遍历出队列**

> 
<pre>
while(!q.empty())q.pop();</pre>


**第三种：使用swap，这种是最高效的，定义clear，保持STL容器的标准**

> 
<pre>
void clear(queue&lt;int&gt;&amp; q)
{
    queue&lt;int&gt;empty;
    swap(empty,q);
}</pre>


 

### 举个例子

```c++
#include<queue>
#include<iostream>
using namespace std;
void clear(queue<int>&q)
{
    queue<int>empty;
    swap(empty,q);
 } 
int main()
{
    queue<int>q;
    q.push(1);                //在队列末尾依次插入1 2 3 
    q.push(2);
    q.push(3);
    
    int u=q.back();            //返回队列中最后一个元素 
    cout<<"队列最后一个元素为："<<u<<endl;
    
    int v=q.front();        //返回队列中第一个元素 
    cout<<"队列第一个元素为:"<<v<<endl;
    
    q.pop();                //删除第一个元素 
    v=q.front();
    cout<<"队列第一个元素为："<<v<<endl; 
 
    int size=q.size();                //size返回元素个数 
    cout<<"队列中存在"<<size<<"个元素"<<endl; 
    
    cout<<"判断队列是否为空，空输出1 否则输出1："<<endl;
    int flag=q.empty();            //判断队列是否为空，为空返回1，否则返回0 
    cout<<flag<<endl;
//情况queue的三种方法    
/*    q=queue<int>();*/
 
/*    while(!q.empty())
        q.pop();*/
    
    clear(q);                //queue中没有clear操作，用函数定义clear函数，使用swap 
    cout<<q.empty()<<endl;
    return 0;
 }
 ```
