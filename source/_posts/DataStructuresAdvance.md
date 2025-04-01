---

title: Data_structures_Algorithms
tags: Data_s
categories: Data_structures
date: 2024-11-28
sticky: 21
mathjax: true
thumbnail: "/images/DataStructuresAdvance/mikulunch_lang.png"
cover: "/images/DataStructuresAdvance/mikulunch_lang.png"
excerpt: "数据结构好难啊，写不动哩"
---
Data_structures_Algorithms



![](/images/DataStructuresAdvance/mikucodes.png)

这个可视化网站可极大的降低数据结构学习的难度,再后续遇到逻辑难以相通时可用该网站进行辅助学习 {% btn regular::数据结构算法可视化::https://www.cs.usfca.edu/~galles/visualization/Algorithms.html::fa-solid fa-play-circle %} 

##  图



### 图的存储结构





### 图的遍历

#### 广度优先搜索

#### 深度优先搜索



### 图的应用

#### 生成最小树

##### 普里面姆算法(Prim)

##### 克鲁斯卡尔算法()



#### 最短路径

##### 迪杰斯特拉算法(Dijkstra)

##### 弗洛伊德算法(Floyd)





啊啊啊

依然是以后再来写,桀桀桀桀桀







## 串,数组,广义表



### 串(String)



### 串匹配算法

啊吧啊吧啊吧啊吧,不想写力,开摆!!!





### 数组(Arry)



### 矩阵(Matrix)

#### 矩阵的压缩存储





### 广义表(Generalized List)







## 查找

在正式进行查找算法实现前应先掌握基本的测试工具

#### 1. 随机生成数组

用于查找和排序的测试

```cpp
#define MAX_SIZE 10
typedef int ElementType;

typedef struct RList
{
    ElementType data[MAX_SIZE];
    int length;
};

//随机生成数组
void GenerateRandomList(RList &list)
{
    srand(time(NULL));
    for (int i = 0; i < MAX_SIZE; i++)
    {
        list.data[i] = rand() % 100;
    }
    list.length = MAX_SIZE;
}
```

#### 2. 数组复制

由于此处采用顺序表构造体做为基础创建随机数组,需要将构造体中的数组取出,并赋值到一个新的数组上
~~不要问我为什么不直接用数组,我懒得改代码~~

`memcpy` 是 C/C++ 标准库中的一个函数，用于**将一段内存中的数据复制到另一段内存**。它是高效的、适合字节级别复制的操作

```cpp
//数组复制
memcpy(str, random_list.data, sizeof(int) * random_list.length);
//    (目标地址,源地址         ,单个元素大小  *  元素总数           )
```

`memcpy`要求提供分别作为目标和源的两个相同数据类型的组的地址,以及所需内存大小

#### 3. 快速排序(Quick Sort)

`qsort(ElementType arr[], int num_of_elem, int size_of_everyelem, int (*compare)(const void *, const void *));`是C内置的快速排序函数

- `arr[]` 是需要排序的数组。
- `n` 是数组的元素个数。
- `sizeof(int)` 是每个数组元素的大小（即 `size` 参数）。
- `compare` 是比较函数，它会告诉 `qsrot` 如何排列数组元素。

```cpp
//比较函数
int compare(const void* left, const void* right)
{
    //return *(int*)left - *(int*)right; //升序排列
    return *(int*)right - *(int*)left; //降序排列
}

qsort(random_list.data, random_list.length,sizeof(ElementType),compare);
//   (数组              ,数组中元素个数      ,每个元素大小         ,排序算法); 
```

上述代码中的`const void* right` 表示一个指向 **不可变数据** 的通用指针。它是 C 语言中一种不带类型的指针。

因为 `qsort` 是一个通用排序函数，它可以排序任何类型的数据（如 `int`、`float` 或结构体等），所以 `qsort` 的比较函数接收的参数类型必须是通用的，即 `void*`。

`const` 的作用是 **保证数据只读**，即在比较函数中不能修改指针指向的数据。

在正式进行比较时应将其转换为目标数据类型的指针,即使用`(int*)right`

`*(int*)right`的含义为right指针指向的数据,即数组中的一个元素

#### 用于测试查找和排序的随机数组头文件

{% folding blue::SortTest_Header.h %}


``` cpp
#pragma once
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#define MAX_SIZE 10
typedef struct RandomList
{
    int data[MAX_SIZE];
    int length;
};

void GenerateRandomList_head(RandomList& list)
{
    srand(time(NULL));
    for (int i = 0; i < MAX_SIZE; i++)
    {
        list.data[i] = rand() % 100;
    }
    list.length = MAX_SIZE;
}
//比较函数
int compare_head(const void* left, const void* right)
{
    return *(int*)left - *(int*)right; //升序排列
    //return *(int*)right - *(int*)left; //降序排列
}

void CreatRandomList_head(RandomList &random_list)
{
    
    GenerateRandomList_head(random_list);
    int str[MAX_SIZE];
    memcpy(str, random_list.data, sizeof(int) * random_list.length);//拷贝数组
    //qsort(str, random_list.length, sizeof(int), compare_head); //排序
    for (int i = 0; i < MAX_SIZE; i++)
    {
        printf("%d ", str[i]);
    }
    printf("\n");
}

```

{% endfolding %}   



### 顺序查找(Sequence Search)

用于查找数组中指定值的元素的位置，实现算法为基于索引的顺序遍历,该代码在单链表章节已经实现过了，故不在此重复编写

详情请转到  **线性表---顺序表---4.查找**  



### 折半查找（Binary Search）

折半查找，也称为**二分查找**，是一种在有序数组中查找目标值的算法。其核心思想是每次将查找范围缩小一半，直至找到目标值或确认目标值不存在

**前提**：数组必须是**有序**的（升序或降序）。

**时间复杂度**：

- 最坏情况下：$O(log_2 n)$
- 最好情况下：$O(1)$

#### 折半查找的步骤

1. 设定**初始范围**，定义两个指针 `low`（范围起始索引）和 `high`（范围结束索引）。
2. 计算**中间索引** $mid=⌊(low+high)/2⌋$
3. 比较中间值：
   - 如果目标值等于中间值，则查找成功。
   - 如果目标值小于中间值，则将 `high` 移动到 `mid - 1`，缩小范围到左半部分。
   - 如果目标值大于中间值，则将 `low` 移动到 `mid + 1`，缩小范围到右半部分。
4. 重复以上步骤，直至找到目标值或 `low > high`（表示目标值不存在）。

```cpp
//二分查找(折半查找)
int BinarySearch(RList list, ElementType target)
{
    int low = 0 , high = list.length - 1 , mid;
    while (low <= high) //确保在循环到仅剩三个元素时仍会对mid=low的情况进行判断
    {
        mid = (low + high) / 2; //mid为中间位置，当low=high时，mid=low ，除法默认为整除，当low+hight为奇数时，结果向下取整
        if (list.data[mid] == target)
        {
            return mid;
        }
        else if (list.data[mid] < target)
        {
            low = mid + 1;//目标值在list.data[mid]的右半部分
        }
        else
        {
            high = mid - 1;//目标值在list.data[mid]的左半部分
        }
    }
    return -1;
}
```



#### 折半查找总体代码

{% folding blue::折半查找 %}


``` cpp
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#define MAX_SIZE 10
typedef int ElementType;

typedef struct RList
{
    ElementType data[MAX_SIZE];
    int length;
};

//随机生成数组
void GenerateRandomList(RList &list)
{
    srand(time(NULL));
    for (int i = 0; i < MAX_SIZE; i++)
    {
        list.data[i] = rand() % 100;
    }
    list.length = MAX_SIZE;
}

//打印数组
void PrintList(RList list)
{
    for (int i = 0; i < list.length; i++)
    {
        printf("data[%d] : %d |  ", i,list.data[i]);
    }
    printf("\n");
    printf("length : %d\n", list.length);
}


//二分查找(折半查找)
int BinarySearch(RList list, ElementType target)
{
    int low = 0 , high = list.length - 1 , mid;
    while (low <= high) //确保在循环到仅剩三个元素时仍会对mid=low的情况进行判断
    {
        mid = (low + high) / 2; //mid为中间位置，当low=high时，mid=low ，除法默认为整除，当low+hight为奇数时，结果向下取整
        if (list.data[mid] == target)
        {
            return mid;
        }
        else if (list.data[mid] < target)
        {
            low = mid + 1;//目标值在list.data[mid]的右半部分
        }
        else
        {
            high = mid - 1;//目标值在list.data[mid]的左半部分
        }
    }
    return -1;

}


//比较函数
int compare(const void* left, const void* right)
{
    return *(int*)left - *(int*)right;
}



int main()
{
    RList random_list;
    //random_list.data[0]= -1;
    GenerateRandomList(random_list);
    printf("Random List:\n");
    PrintList(random_list);

    //快速排序库函数qsrot(Quick Sort)
    qsort(random_list.data, random_list.length,sizeof(ElementType),compare);

    printf("Sorted List:\n");
    PrintList(random_list);

    //二分查找
    int target;
    printf("Enter the target value to search: ");
    scanf_s("%d", &target);
    int index = BinarySearch(random_list, target);
    if (index == -1)
    {
        printf("Not found!\n");
    }
    else
    {
        printf("Found at order %d!\n", index);
    }

    return 0;

}
```

{% endfolding %}



----



## 排序

### 二叉排序树(BinarySortTree)

二叉排序树是一棵二叉树，满足以下性质：

1. 每个节点的值大于其左子树中所有节点的值。
2. 每个节点的值小于其右子树中所有节点的值。
3. 每个子树本身也是一棵二叉排序树。

#### 创建和插入

##### 1. 创建

```cpp
//创建二叉排序树
void CreateBST(BST& root, KeyType str[], int count)
{
    root = NULL;
    for (int i = 0; i < count; i++)
    {
        InsertBST(root, str[i]);
    }
}
```

##### 2.1 常规循环插入

根据目标值与当前节点的比较：

- 如果目标值小于当前节点值，递归插入到左子树。
- 如果目标值大于当前节点值，递归插入到右子树。

插入时保持二叉排序树的性质。

**时间复杂度**：$O(h)$

```cpp
//插入节点
int InsertBST(BST& root, KeyType key_new)
{
    if (root == NULL)
    {
        root = (BST)calloc(1,sizeof(struct BinarySortTreeNode));
        root -> key = key_new;
        return 1; //第一个节点插入成功
    }
    BST p = root;//p用于遍历树
    BST parent = NULL;//用于储存目标节点的父节点
    while (p) //当p不为空时,执行循环,为空时中断
    {
        parent = p;
        if (key_new == p->key)
        {
            return 0; //节点已存在,插入失败
        }
        else if (key_new < p->key)
        {
            p = p->left;
        }
        else
        {
            p = p->right;
        }    
    }//在循环结束时,parent指向p应进入的叶子节点的父节点
    BST pnew = (BST)calloc(1,sizeof(struct BinarySortTreeNode));
    pnew->key = key_new;
    if (pnew->key < parent->key)
    {
        parent->left = pnew;
    }
    else
    {
        parent->right = pnew;
    }
    return 1; //插入成功    
}
```

##### 2.2 递归插入

**递归基准条件**：

- 如果当前节点为空（`NULL`），则新节点应该插入到此处。

**递归逻辑**：

- 如果插入值小于当前节点值，递归处理左子树。
- 如果插入值大于当前节点值，递归处理右子树。
- 如果插入值等于当前节点值，视为重复值，通常忽略或返回。

**返回值**：

- 每次递归调用返回当前节点指针，以确保树结构能够正确链接。

```cpp
//递归插入节点
BST InsertBST_recursion(BST &root, KeyType key_new)
{//将root作为递归遍历的核心节点,携带着key_new持续递归遍历到树底部,最后root为空则创建节点并放入key_new
    if (root == NULL)
    {
        root = (BST)calloc(1,sizeof(struct BinarySortTreeNode));
        root -> key = key_new;
        return root; //第一个节点插入成功
    }
    if (key_new < root->key)
    {
        root->left = InsertBST_recursion(root->left, key_new);
    }
    else
    {
        root->right = InsertBST_recursion(root->right, key_new);
    }
    return root; //插入成功 
}
```



#### 查找

按二叉排序树规则遍历查找

```cpp
//查找
int Search_BST(BST root, KeyType key)
{
    KeyType p = NULL;
    while (root != NULL && root->key != key)
    {
        if (key < root->key)
        {
            root = root->left;
        }
        else
        {
            root = root->right;
        }
    }//循环结束时,root指向目标节点或NULL
    if (root == NULL)
    {
        printf("未找到节点: %d\n", key);
        return 0; //未找到
    }
    else
    {
        printf("找到节点: %d\n", root->key);
        return 1; //找到
    }

}
```



#### 删除

##### 1. 查找目标节点

通过递归，根据二叉排序树的性质（左子树小于根，右子树大于根）：

- 如果目标值小于当前节点值，递归到左子树。
- 如果目标值大于当前节点值，递归到右子树。
- 如果相等，找到了需要删除的目标节点。

##### 2.分类讨论删除目标节点

根据目标节点的左右子树情况分为三种情况：

**(1) 目标节点为叶子节点（没有左右子树）**

- 直接删除节点，并将父节点指向它的指针设置为 `NULL`。
- **代码体现**：目标节点被替换为空（`root = NULL;`），然后释放该节点。

**(2) 目标节点只有一棵子树**

- 如果目标节点只有左子树或只有右子树：

  - 用它的唯一子树替代它的位置。
  - 将当前节点的指针更新为左子树或右子树，最后释放当前节点。

- 代码体现：

  - 如果 `root->left == NULL`，则 `root = root->right;`。
- 如果 `root->right == NULL`，则 `root = root->left;`。

**(3) 目标节点有两棵子树**

- 找到替换节点：

  - **右子树中的最小节点**，或
  - **左子树中的最大节点**。

- 用替换节点的值覆盖目标节点的值。

- 在对应的子树中递归删除替换节点。

- 代码体现：

  - 找到右子树中的最小节点：从 `root->right` 开始，向左寻找直到 `temp->left == NULL`。
- 覆盖值后递归调用删除函数。

```cpp
//删除节点
bool DeleteBST(BST& root, KeyType key)
{
    if (root == NULL)//树为空或树中无此节点递归查找目标节点失败
    {
        return false;
    }
    if (key < root->key)
    {
        return DeleteBST(root->left, key);
    }
    else if (key > root->key)
    {
        return DeleteBST(root->right, key);
    }
    else//找到了目标节点
    {
        if (root->left == NULL)//目标节点是叶子节点且只有右子树
        {           
            BST temp = root;//temp指针保存待指向删除节点的指针
            root = root->right;//root指针被修改为待指向删除节点的右子树
            free(temp);
        }
        else if (root->right == NULL)//目标节点是叶子节点且只有左子树
        {
            BST temp = root;
            root = root->left;
            free(temp);
        }
        //目标节点既有左子树又有右子树
        //此时删除目标节点后需用右子树中的最小节点替换目标节点,或用左子树中的最大节点替换目标节点
        //在操作层面体现为将替换节点移动到目标节点的位置然后删除替换节点
        else//右子树中的最小节点替换       
        {
         
            BST temp = root->right;//temp指针保存指向目标节点的右子树
            while (temp->left != NULL)//找到右子树中的最小节点
            {
                temp = temp->left;
            }
            root->key = temp->key;//将待删除节点的右子树中的最小节点的值赋给待删除节点
            DeleteBST(root->right, temp->key);//删除右子树中的最小节点
        }
        //else//左子树中的最大节点替换
        //{
        //    BST temp = root->left;//temp指针保存待指向删除节点的左子树
        //    while (temp->right != NULL)//找到左子树中的最大节点
        //    {
        //        temp = temp->right;
        //    }
        //    root->key = temp->key;//将待删除节点的左子树中的最大节点的值赋给待删除节点
        //    DeleteBST(root->left, temp->key);//删除左子树中的最大节点
        //}

        return true; //删除成功
    }

}
```





#### 二叉排序树总体代码

{% folding blue::二叉排序树 %}


``` cpp
#include "C_L_Header.h"

typedef int KeyType;

typedef struct BinarySortTreeNode
{
    KeyType key;
    BinarySortTreeNode* left;
    BinarySortTreeNode* right;
}*BST;

#define MAX_SIZE 10
typedef struct RList
{
    KeyType data[MAX_SIZE];
    int length;
};
void GenerateRandomList_T(RList& list)
{
    srand(time(NULL));
    for (int i = 0; i < MAX_SIZE; i++)
    {
        list.data[i] = rand() % 100;
    }
    list.length = MAX_SIZE;
}
//比较函数
int compare_T(const void* left, const void* right)
{
    return *(int*)left - *(int*)right; //升序排列
    //return *(int*)right - *(int*)left; //降序排列
}


//递归插入节点
BST InsertBST_recursion(BST &root, KeyType key_new)
{//将root作为递归遍历的核心节点,携带着key_new持续递归遍历到树底部,最后root为空则创建节点并放入key_new
    if (root == NULL)
    {
        root = (BST)calloc(1,sizeof(struct BinarySortTreeNode));
        root -> key = key_new;
        return root; //第一个节点插入成功
    }
    if (key_new < root->key)
    {
        root->left = InsertBST_recursion(root->left, key_new);
    }
    else
    {
        root->right = InsertBST_recursion(root->right, key_new);
    }
    return root; //插入成功 
}



//插入节点
int InsertBST(BST& root, KeyType key_new)
{
    if (root == NULL)
    {
        root = (BST)calloc(1,sizeof(struct BinarySortTreeNode));
        root -> key = key_new;
        return 1; //第一个节点插入成功
    }
    BST p = root;//p用于遍历树
    BST parent = NULL;//用于储存目标节点的父节点
    while (p) //当p不为空时,执行循环,为空时中断
    {
        parent = p;
        if (key_new == p->key)
        {
            return 0; //节点已存在,插入失败
        }
        else if (key_new < p->key)
        {
            p = p->left;
        }
        else
        {
            p = p->right;
        }    
    }//在循环结束时,parent指向p应进入的叶子节点的父节点
    BST pnew = (BST)calloc(1,sizeof(struct BinarySortTreeNode));
    pnew->key = key_new;
    if (pnew->key < parent->key)
    {
        parent->left = pnew;
    }
    else
    {
        parent->right = pnew;
    }
    return 1; //插入成功    
}

//创建二叉排序树
void CreateBST(BST& root, KeyType str[], int count)
{
    root = NULL;
    for (int i = 0; i < count; i++)
    {
        //InsertBST(root, str[i]);
        InsertBST_recursion(root, str[i]);
    }
}

//查找
int Search_BST(BST root, KeyType key)
{
    KeyType p = NULL;
    while (root != NULL && root->key != key)
    {
        if (key < root->key)
        {
            root = root->left;
        }
        else
        {
            root = root->right;
        }
    }//循环结束时,root指向目标节点或NULL
    if (root == NULL)
    {
        printf("未找到节点: %d\n", key);
        return 0; //未找到
    }
    else
    {
        printf("找到节点: %d\n", root->key);
        return 1; //找到
    }

}


//删除节点
bool DeleteBST(BST& root, KeyType key)
{
    if (root == NULL)//树为空或树中无此节点递归查找目标节点失败
    {
        printf("未找到节点: %d\n", key);
        return false;
    }
    if (key < root->key)
    {
        return DeleteBST(root->left, key);
    }
    else if (key > root->key)
    {
        return DeleteBST(root->right, key);
    }
    else//找到了目标节点
    {
        if (root->left == NULL)//目标节点是叶子节点且只有右子树
        {           
            BST temp = root;//temp指针保存待指向删除节点的指针
            root = root->right;//root指针被修改为待指向删除节点的右子树
            free(temp);
        }
        else if (root->right == NULL)//目标节点是叶子节点且只有左子树
        {
            BST temp = root;
            root = root->left;
            free(temp);
        }
        //目标节点既有左子树又有右子树
        //此时删除目标节点后需用右子树中的最小节点替换目标节点,或用左子树中的最大节点替换目标节点
        //在操作层面体现为将替换节点移动到目标节点的位置然后删除替换节点
        else//右子树中的最小节点替换       
        {
         
            BST temp = root->right;//temp指针保存指向目标节点的右子树
            while (temp->left != NULL)//找到右子树中的最小节点
            {
                temp = temp->left;
            }
            root->key = temp->key;//将待删除节点的右子树中的最小节点的值赋给待删除节点
            DeleteBST(root->right, temp->key);//删除右子树中的最小节点
        }
        //else//左子树中的最大节点替换
        //{
        //    BST temp = root->left;//temp指针保存待指向删除节点的左子树
        //    while (temp->right != NULL)//找到左子树中的最大节点
        //    {
        //        temp = temp->right;
        //    }
        //    root->key = temp->key;//将待删除节点的左子树中的最大节点的值赋给待删除节点
        //    DeleteBST(root->left, temp->key);//删除左子树中的最大节点
        //}

        return true; //删除成功
    }

}



// 打印树状二叉树
void PrintTree_T(BST root, const char* prefix, int isLeft)
{
    if (root == NULL)
    {
        return;
    }

    printf("%s", prefix);
    printf(isLeft ? "├── " : "└── ");
    printf("%d\n", root->key);

    char newPrefix[100];
    snprintf(newPrefix, sizeof(newPrefix), "%s%s", prefix, isLeft ? "│   " : "    ");
    PrintTree_T(root->right, newPrefix, 1);
    PrintTree_T(root->left, newPrefix, 0);
}


// 二叉排序树的中序遍历
void InorderTraversal_T(BST root, RList& list)
{
    if (root == NULL)
    {
        return;
    }
    InorderTraversal_T(root->left, list);
    list.data[list.length++] = root->key;
    InorderTraversal_T(root->right, list);
}
int main()
{
    RList random_list;
    GenerateRandomList_T(random_list);

    KeyType str[MAX_SIZE];
    memcpy(str, random_list.data, sizeof(KeyType) * random_list.length);
    for (int i = 0; i < MAX_SIZE; i++)
    {
        printf("%d ", str[i]);
    }
    printf("\n");


    BST root;//创建树根  
    CreateBST(root, str, MAX_SIZE);
    // 打印树状结构
    printf("树状打印结果:\n");
    PrintTree_T(root, "", 0);


    // 中序遍历
    RList inorder_list;
    inorder_list.length = 0;
    InorderTraversal_T(root, inorder_list);
    printf("root中序遍历结果:\n");
    for (int i = 0; i < inorder_list.length; i++)
    {
        printf("%d ", inorder_list.data[i]);
    }
    printf("\n");

    int s_bst;
    printf("请输入查找的节点: ");
    scanf_s("%d", &s_bst);

    Search_BST(root, s_bst);

    int d_bst;
    printf("请输入删除的节点: ");
    scanf_s("%d", &d_bst);

    DeleteBST(root, d_bst);
    printf("删除节点后树状打印结果:\n");
    PrintTree_T(root, "", 0);

    return 0;
}
```

{% endfolding %}

----



### 冒泡排序(Bubble Sort)

冒泡排序是一种基础的排序算法，通过多次比较和交换相邻元素，将数组中最大（或最小）的元素逐步“冒泡”到数组的一端，直至整个数组有序

#### 1. 外层循环

- 控制需要进行排序的范围（即已排序部分的长度）
- 每循环一次就会有一个最小的数冒泡到数组最右边,循环到index-1时仅剩最后两个元素,他们比较完成时数组就有序了,故最多需要 `n-1` 次（对于长度为 `n` 的数组）

#### **2. 内层循环**

- 完成一次冒泡操作，将当前范围内的最小元素移动到数组开头
- 由于从末尾取数向前比较,因此只需比较`n-1`次,故循环`n-1`次

```cpp
//交换两个数
void swap(int& a, int& b)
{
	int temp = a;
	a = b;
	b = temp;
}

//冒泡排序
void BubbleSort(int arr[], int n)
{
	int index = n - 1;//设置数组最后一个元素的索引
	int i, j;
	bool flag = false;
	for (i = 0;i < index ;i++) //每循环一次就会有一个最大的数冒泡到数组最右边,循环到index-1时仅剩最后两个元素,他们比较完成时数组就有序了
	{
		flag = false;
		for (j = index ;j > 0; j--)
		{
			if (arr[j] < arr[j - 1]) //改变符号即可实现倒叙
			{
				swap(arr[j], arr[j - 1]);
				flag = true;
			}
		}
		if (!flag) //如果没有发生交换,说明数组已经有序,可以提前结束循环
			break;
	}
}
```

### 插入排序(Insert Sort)

**初始化：**

- 从数组的第二个元素开始，因为一个元素自燃有序。
- 每次取出一个新的元素，插入到已经排序好的部分中。

**外层循环（逐步扩展有序部分）：**

- `i` 从 1 到 `n-1`，`i` 表示当前待插入元素的位置，逐步扩展已排序部分。
- `insertValue = arr[i]`，将当前待插入的元素存储在 `insertValue` 中。

**内层循环（查找插入位置）：**

- 内层循环通过 `j` 向前查找 `insertValue` 应插入的位置。

- 如果 `arr[j]` 大于 `insertValue`，则将 `arr[j]` 后移一位，即 `arr[j + 1] = arr[j]`。

- 循环会持续进行，直到找到一个不大于 `insertValue` 的位置，或者已经到达数组的起始位置。

- `j>=0 `确保了会对第一个元素进行判别,

  如果比第一个元素小,此时j=-1,在插入值进行覆盖操作时会覆盖在`arr[0]`的位置

**插入元素：**

- 插入值前的数组元素在大于插入值的前提下向后覆盖,直到不大于插入值时退出循环并将插入值覆盖在`j+1`处,因为每次循环覆盖后`j`先前移并指向未曾判别的元素,而`j`到了小于插入值元素时才会触发循环中断,此时目标位置在`j`前一位
- 插入 `insertValue`，即 `arr[j + 1] = insertValue`。

**重复过程：**

- 外层循环继续，直到所有元素都插入到合适的位置。

```cpp
//插入排序
void InsertSort(int arr[], int n)
{ 
	int i, j;
	for (i = 0;i < n ;i++)
	{
		int insertValue = arr[i]; //每次从未排序的数组中取出第一个元素
		for (j = i - 1; arr[j] > insertValue && j >= 0; j--)  //
		{
			arr[j + 1] = arr[j]; //将大于insertValue的元素后移一位
		}
		arr[j + 1] = insertValue; //将insertValue插入到正确的位置
	}
}
```



### 快速排序(Quick Sort)

#### 1. **选择基准元素（Pivot）**

- 你在 `Partition` 函数中选择数组的第一个元素 `A[left]` 作为基准元素。你也可以选择其他策略来选择基准元素（例如随机选择或者选择中位数等）。

#### 2. **分区操作**
`Partition`函数的目标是将数组分成两部分，使得：

  - 左侧部分的所有元素都小于等于基准元素。

  - 右侧部分的所有元素都大于等于基准元素。

- 具体过程：

  - 设置 `pivot` 为 `A[left]`（即基准元素）。
  - 使用两个指针：`left` 和 `right`，从两端开始，逐渐向中间逼近。
  - 移动 `right` 指针，直到找到一个小于 `pivot` 的元素。
  - 移动 `left` 指针，直到找到一个大于 `pivot` 的元素。
  - 如果 `left < right`，交换这两个元素。
  - 重复以上过程，直到 `left == right`，此时基准元素的位置已经确定，返回该位置。
  
  在循环流程中,right值会最先替换掉第一个left值,在这之后是left值替换right值,,再次循环到right值判断时替换的一定是上一次总循环中被选定的left值,,再次循环到left值判断时替换的一定是上一次总循环中被选定的right值,
  
  循环到left = right 时 left和right指向的值一定是上一次总循环中选定的left/right值,也意味着它在当前数组总存在复制体,此时用pivot对齐进行替换

#### 3. **递归排序左右子数组**

  `QuickSort`函数会对基准元素两侧的子数组递归地进行排序。

  - 在 `Partition` 完成后，返回基准元素的索引 `pivot`，此时 `arr[pivot]` 就是排好序的元素。
  - 然后，分别对基准元素左边（`arr[left, pivot-1]`）和右边（`arr[pivot+1, right]`）的子数组递归调用 `QuickSort`。

#### 4. **递归终止条件**

- 当子数组的大小小于或等于 1 时，递归终止，因为此时数组已经有序。

```cpp
//快速排序的分区函数
int Partition(int A[], int left, int right)
{
	int pivot = A[left];//选取第一个元素作为pivot
	while (left < right)
	{
		while (left < right && A[right] >= pivot)
			right--;
		A[left] = A[right];
		while (left < right && A[left] <= pivot)
			left++;
		A[right] = A[left];
	}
	A[left] = pivot;
	return right; //返回pivot的位置 此时lfet=right,返回哪个都行	
}
//快速排序
void QuickSort(int arr[], int left, int right)
{
	if (left < right)
	{
		int pivot = Partition(arr, left, right); //arr代表数组的首地址,即&arr[0]
		QuickSort(arr, left, pivot - 1); //递归左边
		QuickSort(arr, pivot + 1, right); //递归右边
		//经过左右不断拆分递归后,最终数组会被细分为只有一个元素的数组,此时left=right,此时数组已经有序
	}
}
```



### 选择排序(Selection Sort)

#### 1. **初始化变量**

- 使用 `minIndex` 变量记录当前未排序部分中最小元素的索引。
- 外层循环 `i` 表示当前处理的轮次，也是已排序部分的末尾索引。

#### 2. **寻找最小元素**

- 内层循环从 `i+1` 开始遍历未排序部分，找到其中最小的元素。
- 如果找到比当前记录的最小值还小的元素，则更新 `minIndex`。
- 从第一个元素开始向后遍历寻找最小的元素,将其与第一个元素替换,之后从第二个元素开始遍历寻找最小元素,将其与第二个元素替换,如此往复,循环完成倒数第二个元素时数组依然有序

#### 3. **交换元素**

- 如果 `minIndex` 不等于 `i`，说明找到一个新的最小值。
- 交换 `arr[i]` 和 `arr[minIndex]`，将最小值放到已排序部分的末尾。

#### 4. **重复上述过程**

- 每一轮结束后，未排序部分的长度减少 1。
- 外层循环继续，直到数组完全排序。
- sp : 倒数第二个元素在向后寻找最小元素时已经与最后一个元素进行了比较,故无需对最后一个而元素进行排序(~~就算想排也会出现数组索引溢出的bug~~)

```cpp
//选择排序
void SelectionSort(int arr[], int n)
{
	int i, j, minIndex;
	for (i = 0; i < n - 1; i++)
	{
		minIndex = i;
		for (j = i + 1;j<n;j++)
		{
			if (arr[j] < arr[minIndex])
			{
				minIndex = j; //找到最小的数的索引并将其索引赋值给minIndex
			}
		}
		if (minIndex != i) //在未找到新的最小数的情况下,i和minIndex相等,此时不需要交换
		{
			 swap(arr[i], arr[minIndex]); //交换最小数和i
		}
	}
}
```



### 堆排序(Heap Sort)

#### 1. **建立最大堆**

- **从最后一个非叶子节点开始**，逐步调整每个节点使其所在子树成为最大堆。
- 遍历从 `All_index / 2` 到 `0` 的所有节点，调用 `Heapify` 函数调整堆。

#### 2. **交换堆顶元素和最后一个元素**

- 最大堆的堆顶元素是当前堆的最大值，将堆顶与堆的最后一个元素交换。
- 交换后，当前堆的最后一个元素已经排序，将堆的范围缩小

#### 3. **重新调整堆**

- 调整堆的范围后，从堆顶开始调用 `Heapify` 函数，重新调整堆使其成为最大堆。

#### 4. **重复步骤 2 和 3**

- 不断缩小堆的范围，将堆顶元素交换到数组末尾并调整剩余堆，直到所有元素排序完成。

```cpp
//调整队列使其成为大根堆
void Heapify(int arr[], int Dad_index, int Last_index)
{
	int dad = Dad_index; //父节点的索引,也是局部最大值索引
	int son = 2 * dad + 1; //左子节点的索引
	while (son <= Last_index)
	{
		if (son + 1 <= Last_index && arr[son + 1] > arr[son]) //如果有右子节点且右子节点大于左子节点,则son+1为最大子节点
		{  //son + 1 <= Last_index为了避免数组越界
			son++; //索引后移指向最大子节点
		}
		if (arr[son] > arr[dad])
		{
			swap(arr[son], arr[dad]); //如果左子节点大于父节点,则交换两者
			dad = son; //dad指向新的父节点
			son = 2 * dad + 1; //son指向新的左子节点
			//dad 和 son 都指向新的父节点和左子节点,继续循环可将因本次调整而破坏的最大堆子树调整为最大堆
		}
		else
		{
			break; //如果左子节点小于等于父节点,则说明子树已经是最大堆,结束循环
		}
	}
}
//堆排序
void HeapSort(int arr[], int All_index)
{ 
	for (int i = All_index / 2 ; i >= 0; i--) //建立最大堆
	{
		Heapify(arr, i, All_index); //将以arr[i]为根节点的子树调整为最大堆
	}

	for (int i = All_index; i > 0; i--)
	{
		Heapify(arr,0,i); //将Dad_index赋值为0时,Heapify每次循环会将总体最大的元素放到堆顶
		swap(arr[0], arr[i]); //将堆顶元素和最后一个元素交换
	}

}
```



### 归并排序(Merge Sort)

#### 1. **分割阶段（分治过程）**

- **递归拆分**：将数组递归地分割成两半，每次通过计算中间位置 `mid = (left + right) / 2`，将数组分为两个子数组。
- **递归条件**：当 `left < right` 时，继续分割，否则停止递归。

**步骤：**

- 调用 `MergeSort(arr, left, mid)`，递归处理数组的左半部分。
- 调用 `MergeSort(arr, mid + 1, right)`，递归处理数组的右半部分。
- 递归的终止条件是子数组大小为1，即当 `left == right` 时，子数组只有一个元素，此时数组本身已经是有序的。

#### 2. **合并阶段**

- **合并两个有序子数组**：当两个子数组都已经排好序时，将它们合并成一个有序数组。合并时采用的是**归并算法**，即通过逐一比较两个子数组的元素，将较小的元素放入原数组，最终形成一个有序数组。

**步骤：**

- 将待合并的两个子数组的数据先复制到一个临时数组 `temp[]` 中。
- 使用三个指针：
  - `One_current` 指向左子数组的当前元素，
  - `Other_current` 指向右子数组的当前元素，
  - `Copy_current` 指向合并后的数组的当前插入位置。
- 比较左子数组和右子数组当前指针所指向的元素，将较小的元素放入原数组，更新相应指针。
- 如果一边的子数组已经合并完，而另一边还有剩余元素，直接将剩余的元素复制到原数组。

#### 3. **细节操作**

- **复制到临时数组**：在合并前，先将当前需要合并的子数组部分复制到临时数组 `temp[]` 中。
- **剩余元素处理**：合并过程中可能会有剩余的元素没有被比较，此时直接将剩余元素从 `temp[]` 复制到原数组中，因为这些剩余元素本身是有序的。

```cpp
//合并两个有序数组
void Merge(int arr[], int left, int mid, int right)
{
	static int temp[MAX_SIZE]; //定义一个临时数组 
	//static修饰符使得temp可被重复调用,同时其在被调用时初始化,函数结束时销毁,避免了重复申请释放内存
	int One_current , Other_current , Copy_current;//One_current表示一个数组的起始索引,Other_current表示另一个数组的起始索引,Copy_current表示正在合并的数组元素的索引

	//将待合并的数组复制到临时数组
	for (One_current = left; One_current <= right; One_current++)
	{
		temp[One_current] = arr[One_current]; //将待合并的数组复制到临时数组		
	}

	//比较两个数组的元素,将较小的元素放入原数组,每次将较小的元素放入原数组后将temp数组索引后移,实现合并
	for (One_current = left, Other_current = mid + 1, Copy_current = One_current; One_current <= mid && Other_current <= right; Copy_current++)
	{
		if (temp[One_current] <= temp[Other_current])
		{
			arr[Copy_current] = temp[One_current++]; //将较小的元素放入原数组然后temp数组索引后移
		}
		else
		{
			arr[Copy_current] = temp[Other_current++]; //将较小的元素放入原数组然后temp数组索引后移
		}
	}
	//当两个子数组元素数量不同时会有剩余的元素无法与零一数组的元素做比较并入原数组,此时将剩余元素本身就有序,故直接复制到原数组

	while(One_current <= mid) arr[Copy_current++] = temp[One_current++]; //将剩余的元素复制到原数组,第一个数组更长时触发
	while(Other_current <= right) arr[Copy_current++] = temp[Other_current++]; //将剩余的元素复制到原数组,第二个数组更长时触发
	
}

//归并排序
void MergeSort(int arr[], int left, int right)
{
	if (left < right)
	{
		int mid = (left + right) / 2;
		MergeSort(arr, left, mid); //递归左边
		MergeSort(arr, mid + 1, right); //递归右边
		//MergeSort会将数组递归拆分到仅有一个元素的数组,此时left=right,此时数组已经有序
		Merge(arr, left, mid, right); //合并左右两边的有序数组
	}
}
```



### Tips

个别排序算法过于抽象,因此需要图像辅助理解,脑内无法理清流程时去文章开头找到算法辅助网站去看一下流程吧

#### 各类排序方法的总体代码

{% folding blue::Different_Kands_of_Sort_Fuction %}


``` cpp
#include"SortTest_Header.h"

//交换两个数
void swap(int& a, int& b)
{
	int temp = a;
	a = b;
	b = temp;
}
//冒泡排序
void BubbleSort(int arr[], int n)
{
	int index = n - 1;//设置数组最后一个元素的索引
	int i, j;
	bool flag = false;
	for (i = 0;i < index ;i++) //每循环一次就会有一个最大的数冒泡到数组最右边,循环到index-1时仅剩最后两个元素,他们比较完成时数组就有序了
	{
		flag = false;
		for (j = index ;j > 0; j--)
		{
			if (arr[j] < arr[j - 1])
			{
				swap(arr[j], arr[j - 1]);
				flag = true;
			}
		}
		if (!flag) //如果没有发生交换,说明数组已经有序,可以提前结束循环
			break;
	}
}

//快速排序的分区函数
int Partition(int A[], int left, int right)
{
	int pivot = A[left];//选取第一个元素作为pivot
	while (left < right)
	{
		while (left < right && A[right] >= pivot)
			right--;
		A[left] = A[right];
		while (left < right && A[left] <= pivot)
			left++;
		A[right] = A[left];
	}
	A[left] = pivot;
	return right; //返回pivot的位置 此时lfet=right,返回哪个都行	
}
//快速排序
void QuickSort(int arr[], int left, int right)
{
	if (left < right)
	{
		int pivot = Partition(arr, left, right); //arr代表数组的首地址,即&arr[0]
		QuickSort(arr, left, pivot - 1); //递归左边
		QuickSort(arr, pivot + 1, right); //递归右边
		//经过左右不断拆分递归后,最终数组会被细分为只有一个元素的数组,此时left=right,此时数组已经有序
	}
}

//插入排序
void InsertSort(int arr[], int n)
{ 
	int i, j;
	for (i = 0;i < n ;i++)
	{
		int insertValue = arr[i]; //每次从未排序的数组中取出第一个元素
		for (j = i - 1; arr[j] > insertValue && j >= 0; j--)  //
		{
			arr[j + 1] = arr[j]; //将大于insertValue的元素后移一位
		}
		arr[j + 1] = insertValue; //将insertValue插入到正确的位置
	}
}

//调整队列使其成为大根堆
void Heapify(int arr[], int Dad_index, int Last_index)
{
	int dad = Dad_index; //父节点的索引,也是局部最大值索引
	int son = 2 * dad + 1; //左子节点的索引
	while (son <= Last_index)
	{
		if (son + 1 <= Last_index && arr[son + 1] > arr[son]) //如果有右子节点且右子节点大于左子节点,则son+1为最大子节点
		{  //son + 1 <= Last_index为了避免数组越界
			son++; //索引后移指向最大子节点
		}
		if (arr[son] > arr[dad])
		{
			swap(arr[son], arr[dad]); //如果左子节点大于父节点,则交换两者
			dad = son; //dad指向新的父节点
			son = 2 * dad + 1; //son指向新的左子节点
			//dad 和 son 都指向新的父节点和左子节点,继续循环可将因本次调整而破坏的最大堆子树调整为最大堆
		}
		else
		{
			break; //如果左子节点小于等于父节点,则说明子树已经是最大堆,结束循环
		}
	}
}
//堆排序
void HeapSort(int arr[], int All_index)
{ 
	for (int i = All_index / 2 ; i >= 0; i--) //建立最大堆
	{
		Heapify(arr, i, All_index); //将以arr[i]为根节点的子树调整为最大堆
	}

	for (int i = All_index; i > 0; i--)
	{
		Heapify(arr,0,i); //将Dad_index赋值为0时,Heapify每次循环会将总体最大的元素放到堆顶
		swap(arr[0], arr[i]); //将堆顶元素和最后一个元素交换
	}

}

//合并两个有序数组
void Merge(int arr[], int left, int mid, int right)
{
	static int temp[MAX_SIZE]; //定义一个临时数组 
	//static修饰符使得temp可被重复调用,同时其在被调用时初始化,函数结束时销毁,避免了重复申请释放内存
	int One_current , Other_current , Copy_current;//One_current表示一个数组的起始索引,Other_current表示另一个数组的起始索引,Copy_current表示正在合并的数组元素的索引

	//将待合并的数组复制到临时数组
	for (One_current = left; One_current <= right; One_current++)
	{
		temp[One_current] = arr[One_current]; //将待合并的数组复制到临时数组		
	}

	//比较两个数组的元素,将较小的元素放入原数组,每次将较小的元素放入原数组后将temp数组索引后移,实现合并
	for (One_current = left, Other_current = mid + 1, Copy_current = One_current; One_current <= mid && Other_current <= right; Copy_current++)
	{
		if (temp[One_current] <= temp[Other_current])
		{
			arr[Copy_current] = temp[One_current++]; //将较小的元素放入原数组然后temp数组索引后移
		}
		else
		{
			arr[Copy_current] = temp[Other_current++]; //将较小的元素放入原数组然后temp数组索引后移
		}
	}
	//当两个子数组元素数量不同时会有剩余的元素无法与零一数组的元素做比较并入原数组,此时将剩余元素本身就有序,故直接复制到原数组

	while(One_current <= mid) arr[Copy_current++] = temp[One_current++]; //将剩余的元素复制到原数组,第一个数组更长时触发
	while(Other_current <= right) arr[Copy_current++] = temp[Other_current++]; //将剩余的元素复制到原数组,第二个数组更长时触发
	
}

//归并排序
void MergeSort(int arr[], int left, int right)
{
	if (left < right)
	{
		int mid = (left + right) / 2;
		MergeSort(arr, left, mid); //递归左边
		MergeSort(arr, mid + 1, right); //递归右边
		//MergeSort会将数组递归拆分到仅有一个元素的数组,此时left=right,此时数组已经有序
		Merge(arr, left, mid, right); //合并左右两边的有序数组
	}
}

//选择排序
void SelectionSort(int arr[], int n)
{
	int i, j, minIndex;
	for (i = 0; i < n - 1; i++)
	{
		minIndex = i;
		for (j = i + 1;j<n;j++)
		{
			if (arr[j] < arr[minIndex])
			{
				minIndex = j; //找到最小的数的索引并将其索引赋值给minIndex
			}
		}
		if (minIndex != i) //在未找到新的最小数的情况下,i和minIndex相等,此时不需要交换
		{
			 swap(arr[i], arr[minIndex]); //交换最小数和i
		}
	}
}


int main()
{
	RandomList random_list;
	CreatRandomList_head(random_list);
	int str[MAX_SIZE];
	memcpy(str, random_list.data, sizeof(int) * random_list.length);//拷贝数组
	int n = random_list.length;

	//BubbleSort(str, n);
	//QuickSort(str, 0, n - 1);
	//InsertSort(str, n);
	//HeapSort(str, n - 1);
	MergeSort(str, 0, n - 1);
	//SelectionSort(str, n);		


	//printf("n=%d\n",n);

	PrintList_head(str);
	return 0;
}
//SP : 数组名本身就是一个指针，所以在传入参数时不需要&符号也能实现对数组的操作。
```

{% endfolding %}   

