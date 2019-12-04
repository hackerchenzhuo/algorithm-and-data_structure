# 原创：二叉树基本算法实现：[二叉树构造，左右子树交换，key值查找]

###  ABC##DE#G##F###

 ![](https://img-blog.csdnimg.cn/20191028145525523.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

![](https://img-blog.csdnimg.cn/20191028145525523.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)


```c++
#include <iostream>
#include <string>
using namespace std;
string str;
int i;//全局变量
struct BinaryTree
{
	char val;
	struct BinaryTree* lchild, * rchild;
	BinaryTree(char c) :val(c), lchild(NULL), rchild(NULL) {}//构造函数
};
BinaryTree* createTree() {//递归建树
	char c = str[i++];//i是全局变量，所以函数里面的i等于是直接调用的全局i。str也是。str初始化在main函数中
	if (c == '#') return NULL;
	//因为给的是前序序列，遍历顺序是中(根)->前(左)->后(右)，所以先创空间，再依次递归左右子树
	BinaryTree* root = new BinaryTree(c);//空间创建
	root->lchild = createTree();//递归
	root->rchild = createTree();//递归
	return root;
}
 
void SwapTree(BinaryTree* root)//以根结点为参数，交换每个结点左右子树（前序递归）
{
	//思路：考虑用递归进行
	BinaryTree* temp = root->lchild;//临时变量存左孩子的值
	root->lchild = root->rchild;//交换
	root->rchild = temp;//完成了一轮交换
	if (root->lchild)//此时如果左孩子不为空
		SwapTree(root->lchild);//递归调用该函数，开始以左孩子为根结点，进行上述操作，一直递归到底【左孩子为空时】
	if (root->rchild)//此时如果右孩子不为空
		SwapTree(root->rchild);//递归调用该函数，开始以右孩子为根结点，进行上述操作，一直递归到底【右孩子为空时】，函数结束
}
 
int Find(char key, BinaryTree* root)//查找值为key的结点，并且输出该结点的所有祖先结点
{
	if (!root)  return 0;
	if (root->val == key)    return 1;
	//如果子树中可以找到匹配值 那么此节点肯定是祖先结点
	if (Find(key,root->lchild) || Find(key,root->rchild))
	{
		cout<< "<-"<<root->val;
		return 1;
	}
	return 0;
}
void inOrderTraversal(BinaryTree* root) {//中序遍历，顺序是：前->中->后
	if (!root) return;//到空了，就返回
	inOrderTraversal(root->lchild);
	cout << root->val << " ";
	inOrderTraversal(root->rchild);
}
int main() {
	cout << "请输入二叉树：" << endl;
	cin >> str;
	i = 0;
	BinaryTree* root = createTree();//二叉树构建
	cout << "请输入想查找的key值：(char)" << endl;
	char key;
	cin >> key;
	if (!Find(key, root))//如果没找到
	{
		cout << "不存在该key值！！" << endl;
	}
	cout << endl;
	cout << "交换前，中序遍历测试：" << endl;
	inOrderTraversal(root);
	cout << "开始交换左右子树......" << endl;
	SwapTree(root);
	cout << "交换左右子树完成！" << endl;
 
	//测试：
	cout << "交换后，中序遍历测试：" << endl;
	inOrderTraversal(root);
	return 0;
}
```