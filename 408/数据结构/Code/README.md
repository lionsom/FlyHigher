# 终端写C程序

```shell
// 创建
$ vim 001.c

// Coding
#include <stdio.h>
int main(){
	printf("AAAA");
}

// GCC 编译
$ gcc 001.c         // 默认生成a.out
$ gcc -o 001.out 001.c    // 自定义生成001.out

// 运行
$ ./a.out
```



# C语言中的"&"问题

> 在c语言里，&代表取地址符或者逻辑与运算
>
> 在c++里，除了c语言的功能之外，还代表“引用”
>
> 只能在创建变量的时候使用，格式是：类型 &变量名=另一个变量。如：
>
> ```c++
> // 声明三个变量a、b、c，b和a等价，c是独立的变量
> int a = 0, &b = a, c;
> ```

```c

// 顺序表初始化
void InitList_1(SqList &L) {
    for (int i = 0; i < MAXSIZE; i++) {
        L.data[i] = 0;
    }
    L.length = 0;
}


// GCC编译不通过！！！
/*
 * 问题：编译的时候报:error: expected ';', ',' or ')' before '&' token
 * 原因：C语言中是不存在引用的，也就是说C语言中&表示的不是引用，仅仅是取地址符。
 * 解决：第一种：用指针来取代引用，在主函数中传进地址；
	 	第二种：将代码保存成.cpp文件(c++中支持引用)。
 */

// 指针传参
void InitList_2(SqList *L) {
    for (int i = 0; i < MaxSize; i++) {
        L->data[i] = 0;    // 赋默认值，否则会有脏数据
    }
    L->length = 0;
}

// 调用
SqList L2;          // 声明一个线性表
InitList_1(L2);     // 初始化该线性表
InitList_2(&L2);  	// 初始化该线性表
```

