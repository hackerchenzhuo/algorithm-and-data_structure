# 原创：人生苦短，然而我还得用c++——之 大精读数计算模板

# **这是c++在刷题过程中的必经之路：大数计算。**

很经典的问题。主要就是因为c++中数值范围，无法计算大整数，以及POJ中1001也提到了——大小数。

总之，这种题最重要的就是一个函数，这个函数思想掌握了，以后可以用更简单的语句实现：

 

> 
<p>bigIn operator +(const bigIn &amp;A) const{<br/>
        <br/>
        bigIn ret;<br/>
        int carry=0;<br/>
        for(int i=0;i&lt;A.size||i&lt;size;i++)<br/>
        {<br/>
            int tmp=A.dig[i]+dig[i]+carry;<br/>
            carry=tmp/10000;<br/>
            tmp%=10000;<br/>
            ret.dig[ret.size++]=tmp;<br/>
        }<br/>
        if(carry!=0)<br/>
            {<br/>
                ret.dig[ret.size++]=carry;//保存进位<br/>
            }<br/>
        return ret;<br/>
    }</p>


 

意思就是，从前往后，依次进行相加，判断是否有余数。

这里的**前，**其实是指原本字符串的**后**。

 

因为最开始读入的时候是从后往前读入的，（真的佩他们想得出）

下面这个题目就是这样的：

> 
<h2>题目描述</h2>
<p>在计算机中，由于处理器位宽限制，只能处理有限精度的十进制整数加减法，比如在32位宽处理器计算机中，<br/>
参与运算的操作数和结果必须在-2^31~2^31-1之间。如果需要进行更大范围的十进制整数加法，需要使用特殊<br/>
的方式实现，比如使用字符串保存操作数和结果，采取逐位运算的方式。如下：<br/>
9876543210 + 1234567890 = ?<br/>
让字符串 num1="9876543210"，字符串 num2="1234567890"，结果保存在字符串 result = "11111111100"。<br/>
-9876543210 + (-1234567890) = ?<br/>
让字符串 num1="-9876543210"，字符串 num2="-1234567890"，结果保存在字符串 result = "-11111111100"。</p>
 
<p><br/>
要求编程实现上述高精度的十进制加法。<br/>
要求实现方法： <br/>
public String add (String num1, String num2)<br/>
【输入】num1：字符串形式操作数1，如果操作数为负，则num1的前缀为符号位'-'<br/>
num2：字符串形式操作数2，如果操作数为负，则num2的前缀为符号位'-'<br/>
【返回】保存加法计算结果字符串，如果结果为负，则字符串的前缀为'-'<br/>
注：<br/>
(1)当输入为正数时，'+'不会出现在输入字符串中；当输入为负数时，'-'会出现在输入字符串中，且一定在输入字符串最左边位置；<br/>
(2)输入字符串所有位均代表有效数字，即不存在由'0'开始的输入字符串，比如"0012", "-0012"不会出现；<br/>
(3)要求输出字符串所有位均为有效数字，结果为正或0时'+'不出现在输出字符串，结果为负时输出字符串最左边位置为'-'。</p>


来自华为的机试：

<img alt="" height="608" src="https://img-blog.csdnimg.cn/20190322211729725.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70" width="816"/> 

 

，（**小声BB：用python，几句话的事）**

上代码：

 

 

其实乘也是同一个原理。也是

> 
carry=tmp/10000；//（进位）
tmp%=10000;//去除进位部分


从某某大神那搞到了一个大数乘的模板,他这个是按位的。（其实可以多位一起）

> 
<pre>
<code>string mul(string multiplied,string multiplier)
{
	tmp = string(150,'0');
	int carrier=0;//进位;
	int answer=0;//得数;
	int j = 0;int i = 0;
	for (i = 0; i &lt; multiplied.length(); i++)
	{
		carrier = 0;
		for (j = 0; j &lt; multiplier.length(); j++)
		{
			answer  = ((multiplier.at(j)-'0')*(multiplied.at(i)-'0') + (tmp.at(i+j)-'0') + carrier )%10;
			carrier = ((multiplier.at(j)-'0')*(multiplied.at(i)-'0') + (tmp.at(i+j)-'0') + carrier )/10;
			tmp[i+j] = answer + '0';
		}
		if (carrier)
		{
			tmp[i+j] = carrier + '0';
		}
	}
	//tmp[i+j]='/0';//不知道这个是否有必要;
	tmp = tmp.substr(0,i+j);
	return tmp;
}
</code></pre>
 

