# Leetcode 1074.元素和为目标值的子矩阵数量

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=1421191783&auto=1&height=66"></iframe>

## 题目

来源：力扣（LeetCode） 1074.元素和为目标值的子矩阵数量  
[题目传送门](https://leetcode-cn.com/problems/number-of-submatrices-that-sum-to-target)

## 题解学习
算一个大矩阵中**子矩阵元素和**等于目标值的子矩阵数量方法：***前缀和+哈希表***

```c
struct HashTable {
    int key, val;
    UT_hash_handle hh;
};

int subarraySum(int* nums, int numsSize, int k) {
    struct HashTable* hashTable = NULL;
    struct HashTable* tmp = malloc(sizeof(struct HashTable));
    tmp->key = 0, tmp->val = 1;
    HASH_ADD_INT(hashTable, key, tmp);
    int count = 0, pre = 0;
    for(int i = 0; i < numsSize; i++) {
        pre += nums[i];
        int x = pre - k;
        HASH_FIND_INT(hashTable, &x, tmp);
        if(tmp) {
            count += tmp->val;
        }
        HASH_FIND_INT(hashTable, &pre, tmp);
        if(tmp) { //如果hash表中找到tmp，就把次数+1；
            tmp->val++;
        } else { //没找到就add一下
            tmp = malloc(sizeof(struct HashTable));
            tmp->key = pre, tmp->val = 1;
            HASH_ADD_INT(hashTable, key, tmp);
        }
    }
    return count;
}

int numSubmatrixSumTarget(int** matrix, int matrixSize, int* matrixColSize, int target) {
    int ans = 0;
    int m = matrixSize, n = matrixColSize[0];
    for(int i = 0; i < m; i++) {
        int sum[n];
        memset(sum, 0, sizeof(sum));
        for(int j = i; j < m; j++) { //一次次的增加下边界
            for(int c = 0; c < n; c++) {
                sum[c] += matrix[j][c];
            }
            ans += subarraySum(sum, n, target);
        }
    }
    return ans;
}
```

### uthash相关链接
[官方git地址](https://github.com/troydhanson/uthash)  
[官方简单文档](https://troydhanson.github.io/uthash/)  
[官方详细文档](https://troydhanson.github.io/uthash/userguide.html)  

uthash是c写的项目，实现了常见的hash操作。支持的操作有：
1. add/reolace
2. find
3. delete
4. count
5. iterate
6. sort  

> Is it a library?  
No, it’s just a single header file: uthash.h. All you need to do is copy the header file into your project, and:  
#include "uthash.h"  
Since uthash is a header file only, there is no library code to link against.

使用只用包含头文件就行了，不是一个库，把官方git仓库里**uthash.h**文件下载到本地。
> C/C++ and platforms
This software can be used in C and C++ programs. It has been tested on:  
Linux  
Windows using Visual Studio 2008 and 2010  
Solaris  
OpenBSD  
FreeBSD  
Android

支持以上平台。

### 使用方法

* 包含头文件(方git仓库里**uthash.h**文件下载到本地)和定义hash结构体。
```c
#include "uthash.h"

struct my_struct {
    int id;            /* we'll use this field as the key */
    char name[10];
    UT_hash_handle hh; /* makes this structure hashable */
};
```

* 声明哈希指针变量。  
   声明的哈希指针变量必须被初始化为`NULL`。
```c
struct my_struct *users = NULL;    /* important! initialize to NULL */
```

* 增加一项到哈希表里（要检查一下唯一性）
```c
void add_user(int user_id, char *name) {
    struct my_struct *s;
    HASH_FIND_INT(users, &user_id, s);  /* 检查哈希表中是否已经存在 */
    if (s == NULL) {
      s = (struct my_struct *)malloc(sizeof *s);
      s->id = user_id;
      HASH_ADD_INT(users, id, s);  /* id: name of key field */
    }
    strcpy(s->name, name);
}
```

> Passing the hash pointer into functions  
> In the example above users is a global variable, but what if the caller wanted to pass the hash pointer into the add_user function? At first glance it would appear that you could simply pass users as an argument, but that won’t work right.
```c
/* bad */
void add_user(struct my_struct *users, int user_id, char *name) {
...
HASH_ADD_INT(users, id, s);
}
```
>You really need to pass a pointer to the hash pointer:
```c
/* good */
void add_user(struct my_struct **users, int user_id, char *name) { ...
...
HASH_ADD_INT(*users, id, s);
}
```
作者建议用这种好的方式传参。因为调用者可能会想传递**hash pointer**。

* 删除操作
```c
void delete_user(struct my_struct *user) {
    HASH_DEL(users, user);  /* user: pointer to deletee */
    free(user);             /* optional; it's up to you! */
}
//删除所有Item
void delete_all() {
  struct my_struct *current_user, *tmp;

  HASH_ITER(hh, users, current_user, tmp) {
    HASH_DEL(users, current_user);  /* delete; users advances to next */
    free(current_user);             /* optional- if you want to free  */
  }
}
```

---

> : 嘟囔  
> URL: http://localhost:1313/posts/leetcode-1074/  

