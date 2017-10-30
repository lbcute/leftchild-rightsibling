```#include<iostream>
#include<queue>
using namespace std;
struct Node
{//结点中包含数据，左孩子的指针以及有兄弟的指针
  int data;
  Node* leftchild;
  Node* rightsib;
};
Node* create()
{
  Node * root=NULL;//树的根结点
  queue<Node *>q;//声明q为队列，队列的元素为Node类型的指针
  root=new Node;
  cout<<"请输入树根结点的数据：\n";
  int temp;
  cin>>temp;
  root->data=temp;//给根结点赋值
  root->leftchild=root->rightsib=NULL;//设置根结点的左孩子还有右兄弟为空
  q.push(root);
  int parent,element;
  
  cout<<"下面以"<<temp<<"为根结点构建一棵树，请输入树的数据，每行输入两个数，第一个为结点的父亲数据，第二个为结点数据，以输入-1  -1结束你的输入\n";
  cin>>parent>>element;
  while(!((parent==-1)&&(element==-1)))//若输入两个数都是-1则结束树的输入
  {while(q.front()->data!=parent)//利用出队，找到要输入结点的父亲，如果不是该结点的父亲，则将其从队列中弹出，直到队列的第一个元素的输入元素的父亲结点
    q.pop();
    Node* t=q.front();//用t表示队列的第一个元素，也就是输入结点的父亲
    Node* p;
    if(t->leftchild==NULL)//左孩子为空，也就是目前t还没有孩子
    {p=new Node();
      p->data=element;
      t->leftchild=p;//将p设置为t的第一个孩子
      p->leftchild=p->rightsib=NULL;
      q.push(p);
      
    }
    else
    {
      p=t->leftchild;
      while(p->rightsib)
	p=p->rightsib;//结束while循环时，p是t处于最右边的孩子
      p->rightsib=new Node();//为p的有兄弟申请内存
      p=p->rightsib;//p向右移动一个，则为刚申请的内存空间
      p->data=element;
      p->leftchild=p->rightsib=NULL;
      q.push(p);
    }
    cin>>parent>>element;
  }
  return root;
}
//利用递归后序遍历
void postPrint(Node * root)
{
  if(root==NULL)
  return;
  postPrint(root->leftchild);
  cout<<root->data<<" ";
  postPrint(root->rightsib);
}
int main()
{
  Node* root;
  root=create();
  cout<<"后序遍历该树\n";
  postPrint(root);
  cout<<endl;
}
```
