# 转载：C++中的四舍五入【转】

在C++的输出流中使用控制符，可以实现对输出格式的控制，包括对输出小数的精度的控制：  
```c++
double a=123.456789012345; //对a赋初值
cout<<setiosflags(ios∷fixed)<<setprecision(8)<<a; //输出: 123.45678901 
```
 

设置小数的精度后，程序会对数据进行自动的四舍五入。 <br/>
但是在普通的整形计算表达式中，程序不会自动进行四舍五入，例如：

```c++
int main(){
    int a = 0.69;
    cout<<"a = "<<a<<endl;
    return 0;
}
```

 

输出结果为： <br/><img alt="这里写图片描述" src="https://img-blog.csdn.net/20170523102858267?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzYwMTY0MDc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast"/>

 

在math.h或cmath头文件中有四舍五入有关的函数： <br/><img alt="这里写图片描述" src="https://img-blog.csdn.net/20170523103144877?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzYwMTY0MDc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast"/> 

 

# **round函数就可以完成四舍五入的工作。**

下面自己编写一个将double四舍五入为整形int的函数：

```c++
#include <iostream>
#include <cmath>
using namespace std;
 
int r(double a){
    int b;
    if(a > 0){
        b = (a*2+1)/2;
    }else{
        b = (a*2-1)/2;  
    }
    return b;
}
 
int main(){ 
    double a = -0.69;
    a = r(a);   
    cout<<"a = "<<a<<endl;  
    cout<<"round(a) = "<<round(a)<<endl;    
    return 0;
}
```
 

输出为： <br/><img alt="这里写图片描述" src="https://img-blog.csdn.net/20170523103639180?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzYwMTY0MDc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast"/>
