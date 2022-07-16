# 数据结构代码

### 基础知识

```
//别名：
typedef int Elemtype;

//C中的内存分配函数 头文件<stdlib.h>
int* L;
L=(Elemtype*)malloc(sizeof(Elemtype)*Maxsize);
free(L);

//C++中的内存分配函数
int *p1 = new int;
int *p1 = new int(10); //分配并赋初值，这里初值是10
delete p1;
```

### 顺序表

#### 顺序存储

```
// 线性表
# include<iostream>
# include<stdio.h>
# include<stdlib.h>
using namespace std;
//函数结果状态代码
#define OK 1
#define ERROR 0
#define TRUE 1
#define FALSE 0
#define INFEASIBLE -1
#define OVERFLOW -2

typedef int Elemtype;
// 数组静态分配
#define Maxsize 100 //线性表存储空间的初始分配量
// typedef struct{
//   Elemtype data[Maxsize];
//   int length;
// }Sqlist;

// 线性表的定义
typedef struct{
  Elemtype *data;
  int length;
}Sqlist;

// 线性表的初始化
int InitList_Sq(Sqlist &L)
{
  L.data = new Elemtype[Maxsize];
  if(!L.data) exit(OVERFLOW); //存储分配失败
  L.length = 0;
  return OK;
}

// 销毁线性表
void DestroyList(Sqlist &L)
{
  if(L.data)//线性表存在且不空才能释放
    delete L.data;
}

// 清空线性表
void ClearList(Sqlist &L)
{
  L.length = 0;
}

// 求线性表长度
int GetLength(Sqlist L)
{
  return L.length;
}

// 判断线性表是否为空
int IsEmpty(Sqlist L)
{
  if(L.length == 0)
    return 1;
  else 
    return 0;
}

// 根据位置i获取对应位置数据元素的内容
int GetElem(Sqlist L, int i, Elemtype &e)
{
  if(i>L.length || i<1)
    return ERROR;
  else
    e = L.data[i-1];
  return OK;
}

// 顺序查找值为e的数据元素，并返回其序号(第几个元素)
int LocateElem(Sqlist L, Elemtype e)
{
  int i=0;
  while(i<L.length && L.data[i]!=e)
    i++;
  if(i<L.length)
    return i+1;
  return 0;
}

// 顺序表的插入，在第i个位置插入e
int ListInsert_Sq(Sqlist &L, int i, Elemtype e)
{
  if(i<1 || i>L.length+1)
    return ERROR;
  if(L.length==Maxsize)
    return ERROR;
  for(int j=L.length-1; j>i-1; j++)
    {
      L.data[j] = L.data[j-1];
    }
  L.data[i-1] = e;
  L.length++;
  return OK;
}

// 顺序表的删除，将第i个位置元素删除
int ListDelete_Sq(Sqlist &L, int i)
{
  if(i<1 || i>L.length+1)
    return ERROR;
  if(L.length==0)
    return ERROR;
  // e = L.data[i-1];
  for(int j=i-1; j<L.length-1; j++)
    {
      L.data[j] = L.data[j+1];
    }
  L.length--;
  return OK;
}

int main()
{
  Sqlist L_test;
  if(InitList_Sq(L_test) == 1)
    cout<<"初始化成功"<<endl;
  cout<<"表长为"<<GetLength(L_test)<<" "<<"表为空吗"<<IsEmpty(L_test)<<endl;
  if(ListInsert_Sq(L_test, 1, 1))
    cout<<L_test.data[0]<<endl;
  if(ListInsert_Sq(L_test, 2, 2))
    cout<<L_test.data[1]<<endl;
  if(ListDelete_Sq(L_test, 1))
    cout<<"表长为"<<GetLength(L_test)<<" "<<"表为空吗"<<IsEmpty(L_test)<<endl;
    cout<<LocateElem(L_test, 2);
}
```

链式存储

