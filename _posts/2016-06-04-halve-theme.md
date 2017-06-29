#### 线性表
- **定义：**

  - 零个或多个数据元素的有限序列。	
 
- **抽象数据类型标准定义:**
  - ADT   抽象数据类型名

  - Date 数据元素之间逻辑关系的定义

  - Operation 操作
  
  - endADT
  
####  
- **线性表的存储结构：** 

  - **顺序存储结构**
  
      - **封装的三个属性：**
      
          - 存储空间的起始位置
          - 线性表的最大存储容量
          - 线性表的当前长度
       
       - **获得元素算法：**
          
          - 如果获取元素不存在，则抛出异常。
          - 如果表长等于0，则抛出异常。
          - 取得元素，返回成功。
       
       - **插入算法思路：**
	     
	     - 如果插入不合理，抛出异常。
	     - 如果线性表长度大于等于数组长度，则抛出异常或动态添加数组        容量。
	     - 从最后一个元素开始向前遍历到第i个位置，分别将它们都向后移动一个位置。
	     - 将要插入的元素填入位置i处。
	     - 线性表长度+1。
	     
	  - **删除算法思路：**
	  
	     - 如果删除位置不合理，抛出异常。
	     - 如果线性表长度大于数组长度，则抛出异常。
	     - 如果线性表长度等于 0，则抛出异常。
	     -  获取将要删除的元素。
	     - 从第一个元素开始向后遍历到第i个位置，分别将它们都向前移动一个位置。
	     - 线性表长度 -1。
	     
	  - **优缺点：**
	  
	      - **优点**
	          - 无须为表示表中元素之间的逻辑关系而增加额外存储空间。
	          - 可以快速地存取表中任意位置的元素。
	      - **缺点**
	         
	         - 插入和删除操作需要移动大量元素。
	         
	         - 当线性表长度变化较大时，难以确定存储空间的容量。
	         
	         - 容易造成存储空间的“碎片化”。
	         
	  - **代码片段:**

```
#define MAXSIZE 50
#define OK 1
#define ERROR 0

typedef int ElemType; 
typedef int Status;

typedef struct
{
	ElemType data[MAXSIZE];
	int length;
} SqList;


//获取元素算法
Status GetElem(SqList *L,int i, ElemType *e)
{
	if(L->length == 0 || i < 1 || i > L->length)
	{
		return ERROR;
	}
	
	*e = L->data[i-1];
	
	return OK;
	
} //时间复杂度为O(1)


//插入算法
Status LinkInsert(SqList *L, int i, ElemType *e)
{
	int k;
	
	if(i > L->length+1 || i < 1 || L->length == MAXSIZE )
	{
		return ERROR;
	}
	if(i < L->length)
	{
		for(k = L->length-1; k < i-1; k--)
		{
			L->data[k+1] = L->data[k];
		}
		
		L->data[i-1] = *e;
		L->length++;
		
		return OK;
	}
}  //时间复杂度为O(n)+ O(1)


//删除算法
Status LinkDelete(SqList *L, int i, ElemType e)
{
	int k;
	if(i<1 || i>L->length || L->length == 0)
	{
		return ERROR;
	}
	*e = L->data[i-1];
	for(k = i; k < L->length; k++)
	{
		L->data[k-1] = L->data[k];
	}
	
	L->length--;
	return OK;
} //时间复杂度为 O(n)

/*****************************************************************************************
 * SqList L 和 SqList *L 不加星号表示定义结构体变量，加了星号表示
 * 定义指向结构体的指针变量，这个加与不加无所谓，只是结构体中分量的访问
 * 形式不同。ElemType *e 是表示指针变量， ElemType e 是表示一般的
 * 变量。在此程序中是作为形参，表示传递不同的内容，前者传递地址值，后者
 * 传递数据。
 *****************************************************************************************/

```


                  
  - **链式存储结构**
     
     - **头指针与头节点异同**：
        
        - 头指针
			- 头指针是指链表指向第一个节点的指针，若链表有节点，则是指向头节点的指针。
			- 头指针具有标识作用，所以常用头指针冠以链表名（指针变量名）。
			- 无论链表是否为空，头指针均不为空。
			- 头指针是链表的必要元素。

       - 头节点

		   - 头节点是为了操作的统一和方便而设立的，放在第一个元素节点之前，其数据域一般无意义（但也可以用于存放链表长度）。
		   - 有了头节点，对在第一元素节点前插入节点，和删除第一节点起操作与其它的操作就统一了。
		   - 头节点不一定是链表的必要元素。
	
  - **获得链表第i个数据的算法思路：**
     - 声明一个节点p指向链表第一个节点，初始化j从1开始。 
     - 当j < i时，遍历链表，让p的指针向后移动，不断指向下一节点，j累加1。
     - 若到链表末尾p为空，则说明第i个元素不存在。
     - 否则查找成功，返回节点p的数据。
    
  - **单链表第i个数据插入结点的算法思路：**
    
    -  声明一节点p指向链表头节点，初始化j从1开始。
    - 当j < i 时，遍历链表，让p的指针向后移动，不断指向下一节点，j累加1。
    - 若到链表末尾p为空，则说明第i个元素不存在。
    - 否则查找成功，在系统中生成一个空结点s。
    - 将数据元素e赋值给s->data。
    - 单链表的插入刚才两个标准语句： s->next = p->next; p->next = s;
    - 返回成功。
  - **单链表第i个数据删除结点的算法思路：**
  
    - 声明一结点p指向链表头结点，初始化j从1开始。
    - 当j<1时，就遍历链表，让p的指针向后移动，不断指向下一结点，j累加1。
	- 若到链表末尾p为空，则说明第i个元素不存在。
    - 否则查找成功，将欲删除结点p->next赋值给q。
	- 单链表的删除标准语句 p->next = q->next；
    - 将q结点中的数据域赋值给e，作为返回。
	- 释放q结点。

  - **单链表整表创建算法思路：**
    - 声明一结点p和计数器变量i。
    - 初始化一空链表L。
    - 让L的头结点的指针指向NULL，即创建一个带头结点的单链表。
    - 循环实现后继结点的赋值和插入。
  
  - **头插法建立单链表思路：**
    - 把新加进来的元素放在表头后的第一个位置。
	- 先让新节点的next指向头节点。
	- 后让表头的next指向新节点。
	
  - **尾插法建立单链表思路：**
    - 思路与头插法相反。
    
  - **单链表整表删除算法思路：**
    - 声明节点p和q。
    - 将第一个节点赋值p，下一节点赋值给q。
    - 循环执行释放p和q赋值给p的操作。

  - **代码片段：**
  

```
#define OK 1
#define ERROR 0
#include<stdlib.h>

typedef int ElemType;
typedef int Status;

typedef struct Node
{
	ElemType data;
	struct Node *next;
} Node;

typedef struct Node *LinkList;


//获得元素算法
Status GetElem(LinkList *L,int i, ElemType *e)
{
	LinkList p;
	int j = 1;
	p = L->next;

	while(p && j<i)
	{
		p = p->next;
		++j;
	}
	if(j>i || !p)
	{
		return ERROR;
	}
	
	*e = p->data;
	
	return OK;
} //时间复杂度为O(n)


//插入算法
Status LinkListInsert(LinkList *L, int i, ElemType *e)
{
	int j = 1;
	LinkList p,s;
	p = *L;

	while(p && j<i)
	{
		p = p->data;
		j++;
	}
	if(!p || j>i)
	{
		return ERROR;
	}
	
	s = (LinkList)malloc(sizeof(Node));
	s->data = e;
	s->next = p->next;
	p->next = s;
	
	return OK;
} //时间复杂度为O(n)


//删除算法
Status LinkListDelete(LinkList *L, int i, ElemType *e)
{
	int j = 1;
	LinkList p,q;
	
	while(p->next && j<i)
	{
		p = p->next;
		++j;
	}
	if(!(p->next) || j>i)
	{
		return ERROR;
	}
	
	q = p->next;
	p->next = q->next;
	*e = q->data;
	free(q);
	
	return OK;
	
}


//头插法创建单链表
void CreateListHead(LinkList *L. int n)
{
	int i;
	LinkList p;
	srand(time(0));   //初始化随机种子

	*L = (LinkList)malloc(sizeof(Node));
	(*L)->next = NULL;
	
	for(i = 0; i < n; i++)
	{
		p = (Node *)malloc(sizeof(Node));
		p->data = rand()%100 +1;
		
		p->next = (*L)->next;
		p = (*L)->next; 
	}
}  //时间复杂度为O(n)


//尾插法创建单链表
Status CreateListTail(LinkList *L, int n)
{
	int i;
	LinkList p,r;
	srand(time(0));
	
	*L = (LinkList)malloc(sizeof(Node));
	r = *L;

	for(i = 0; i < n; i++)
	{
		p = (Node *)malloc(sizeof(Node));
		p->data = rand()%100 +1;
		r->next = p;
		r = p;
	}
	r->next = NULL;
}



```
