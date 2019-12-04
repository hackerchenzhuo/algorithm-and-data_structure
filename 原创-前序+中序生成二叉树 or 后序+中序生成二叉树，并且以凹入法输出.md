# 原创：前序+中序生成二叉树 or 后序+中序生成二叉树，并且以凹入法输出

 
```c++
#include<iostream>
#include<stdlib.h>
#include <windows.h>
 
 
using namespace std;
 
typedef struct Node
{
	char data;
	struct Node *leftChild;
	struct Node *rightChild;
 
} BiTreeNode;
 
void Initiate(BiTreeNode **root)
{
	*root = (BiTreeNode *)malloc(sizeof(BiTreeNode));
	(*root)->leftChild = NULL;
	(*root)->rightChild = NULL;
	(*root)->data = NULL;
}
 
void Destroy(BiTreeNode **root)
{
	if ((*root) != NULL && (*root)->leftChild != NULL)
		Destroy(&(*root)->leftChild);
	if ((*root) != NULL && (*root)->rightChild != NULL)
		Destroy(&(*root)->rightChild);
	free(*root);
}
 
int len(char a[])
{
	int i = 0;
	for (; a[i] != '\0'; )
		i++;
		return i;
}
int key=0;//判断输入是否正确对应
int flag = 1;//判断二叉树是否构建正确
int n1=0;//比较指针
BiTreeNode *fbuild(char *front,char *mid,int n)//前中生成二叉树
{
	if (key == 1)
	{
		return NULL;
	}
	BiTreeNode *root;
	Initiate(&root);
	char *rpos;
	int num;
	if (n <= 0) return NULL;
	root->data = *front;
	for (rpos = mid; rpos < mid + n; rpos++)
	{
		if (*rpos == *front) break;
	}
	if (*rpos != *front) {
		cout<<"\n输入的不是同一颗二叉树的前序序列和中序序列！！！"<<endl;
		key = 1;/////////输入不正确
	}
	num = rpos - mid;
	root->leftChild = fbuild(front + 1, mid, num);
	root->rightChild = fbuild(front + 1 + num, rpos + 1, n - 1 - num);
	return root;
 
}
BiTreeNode *rbuild(char *rear, char *mid, int n)//后中生成二叉树
{
	if (key == 1)
	{
		return NULL;
	}
	BiTreeNode *root;
	Initiate(&root);
	char *rpos;
	int num;
	if (n <= 0) return NULL;
	root->data = *(rear+n-1);
	for (rpos = mid+n-1; rpos >= mid ; rpos--)
	{
		if (*rpos == *(rear+n-1)) break;
	}
	if (*rpos != *(rear + n - 1)) {
		cout<<"\n输入的不是同一颗二叉树的后序序列和中序序列！！！\n\n";
		key = 1;
	}
	num = rpos-mid;
	root->leftChild = rbuild(rear, mid, num);
	root->rightChild = rbuild(rear + num, rpos + 1, n  - num-1);
	return root;
}
 
void PreOrderCompare(BiTreeNode * t,char *a) /*前序遍历比较结果*/
{
 
	if (t != NULL&&flag != 0)
	{
		char *b = a;
		b+=n1;
		if (t->data != *b)
		{
			flag = 0;
		}
		n1++;
 
		PreOrderCompare(t->leftChild, a);
		PreOrderCompare(t->rightChild, a);
	}
 
}
void InOrderCompare(BiTreeNode * t, char *a) /*中序遍历比较结果*/
{
 
	if (t != NULL&&flag != 0)
	{
		InOrderCompare(t->leftChild, a);
		char *b = a;
		b += n1;
		if (t->data != *b)
		{
			flag = 0;
		}
		n1++;
 
 
		InOrderCompare(t->rightChild, a);
	}
 
}
void PostOrderCompare(BiTreeNode * t, char *a) /*后序遍历比较结果*/
{
 
	if (t != NULL&&flag != 0)
	{
		PostOrderCompare(t->leftChild, a);
		PostOrderCompare(t->rightChild, a);
		char *b = a;
		b += n1;
		if (t->data != *b)
		{
			flag = 0;
		}
		n1++;
	}
 
}
void wait(int n)
{
	cout<<"验证中....";
	Sleep(500*n);
	cout<<"..";
	Sleep(500*n);
	cout<<"..\n\n";
	Sleep(500*n);
}
void compare1(BiTreeNode * t, char *a,char *b)//前中
{
		PreOrderCompare(t, a);//前序遍历比较
		n1 = 0;//初始化
		InOrderCompare(t, b);//中序遍历比较
		wait(1);
		if (flag == 1) cout<<"经验证构造正确！！！\n\n";
		else cout<<"经验证构造不正确！\n\n";
		n1 = 0;//初始化
		flag = 1;//初始化
 
}
void compare2(BiTreeNode * t, char *a, char *b)//后中
{
		PostOrderCompare(t, a);
		n1 = 0;//初始化
		InOrderCompare(t, b);
		wait(1);
		if (flag == 1) cout<<"经验证构造正确！！！\n\n";
		else cout<<"经验证构造不正确！\n\n";
		n1 = 0;//初始化
		flag = 1;//初始化
}
void PreOrderPrint(BiTreeNode * t)//前序遍历输出
{
	if (t != NULL)
	{
		cout<<t->data;
		PreOrderPrint(t->leftChild);
		PreOrderPrint(t->rightChild);
	}
}
void PostOrderPrint(BiTreeNode * t)//后续遍历输出
{
	if (t != NULL)
	{
		PostOrderPrint(t->leftChild);
		PostOrderPrint(t->rightChild);
		cout<<t->data;
	}
}
void PrintBiTree(BiTreeNode *root, int n)//以凹入法输出二叉树
{
	int i;
	if (root == NULL) return;
	PrintBiTree(root->rightChild, n + 1);
	for (i = 0; i < n; i++) cout<<"   ";
	if (n >= 0)
	{
		cout<<"---";
		cout<<root->data<<endl;
	}
	PrintBiTree(root->leftChild, n + 1);
}
 
 
int main()
{
 
	int judge = -1;
 
	while (judge != 0)
	{
		BiTreeNode*root;
		Initiate(&root);
		int lenth = 0;
		char mid[100];
		char other[100];
		cout<<"以前序序列中序序列生成二叉树请输入 1 \n\n以后序序列中序序列生成二叉树请输入 2 \n";
		cin>>judge;
		getchar();
		if (judge == 1)//"ABDEGCFHIJ";// "DBGEAHFIJC";
		{
			cout<<"请输入一个二叉树的前序序列：\n";
			gets(other);
			cout<<"请输入一个二叉树的中序序列：\n";
			gets(mid);
 
		}
		if (judge == 2)//"DCEGBFHKJIA";// "DCBGEAHFIJK";
		{
			cout<<"请输入一个二叉树的后序序列：\n";
			gets(other);
			cout<<"请输入一个二叉树的中序序列：\n";
			gets(mid);
		}
		if (judge != 1 && judge != 2)
		{
			cout<<"输入有误！\n";
			continue;
		}
		lenth = len(other);
		if (lenth != len(mid))
		{
			key = 2;//不等长
		}
		if (lenth == 0|| len(mid)==0)
		{
			key = 3;//长度为0
		}
		if (key == 2) cout<<"输入序列长度不等！！！\n\n";
		if (key == 3) cout<<"长度输入不能为0！！！\n\n";
		if (key != 2&&key!=3)
		{
			if (judge == 1)
			{
				root = fbuild(other, mid, lenth);
				if (key == 0)//成功创建
				{
					compare1(root, other, mid);//前中
					cout<<"后序遍历序列输出：  ";
					PostOrderPrint(root);
					cout<<"\n\n以凹入法输出二叉树：\n";
					PrintBiTree(root, 0);
				}
			}
			if (judge == 2)
			{
				root = rbuild(other, mid, lenth);
				if (key == 0)//成功创建
				{
					compare2(root, other, mid);//后中
					cout<<"前序遍历序列输出：  ";
					PreOrderPrint(root);
					cout<<"\n\n以凹入法输出二叉树：\n";
					PrintBiTree(root, 0);
				}
			}
		}
 
		Destroy(&root);
		key = 0;//初始化
		cout<<"\n\n请问是否需要退出程序？\n\n退出请输入 0 。\n\n输入任意键即可继续\n";
		cin>>judge;
		getchar();
	}
	return 0;
}
```