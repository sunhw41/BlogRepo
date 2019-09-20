---
title:      结构体包含联合体与数组的复制
date:       2018-06-21 15:31:19
author:     孙宏伟
summary:    union and struct
categories: C/C++
tags:
 - union
 - struct
---

## 位域结构体

&ensp; &ensp; &ensp; &ensp; 有时候在通信时仅代表一个bool型的量，不需单独占用一个byte，通过定义**位域结构体**可以将若干个变量放到一个byte里，一个变量占用若干bits（小于8），这样就能节省很多空间，例如：

```
typedef struct BITSTRUCT{
    int A:2;
    int B:5;
    int C:1;
}BitStruct;
```
&ensp; &ensp; &ensp; &ensp; 以**64位X86上的Ubuntu16.04**为例，这样一个BitStruct的结构体一共使用了一个Byte的空间，其中A占了低端的2bit，B占了中间的5bit，C占了最高的1bit：
<table>
    <tr>
        <td>bit7</td> 
        <td>bit6</td> 
        <td>bit5</td> 
        <td>bit4</td> 
        <td>bit3</td> 
        <td>bit2</td> 
        <td>bit1</td> 
        <td>bit0</td>  
   </tr>
    <tr>
        <td colspan="1">C</td>
        <td colspan="5">B</td>    
        <td colspan="2">A</td>    
    </tr>
</table>

---

## 联合体

 &ensp; &ensp;&ensp; &ensp;  但也有一些情况比如一个长度的变量占用了4个byte，每次解析时都通过左移、右移也很麻烦，这样就可以通过**联合体**来包含一个结构体，在这个联合体中定义一个long int的长整型，然后同时再在这个联合体了放一个包含4个byte的结构体，这样就可以用来拼接字符串进行消息通信了：
     
```
typedef union UNIST{
    long int nTotal;
    struct{
        char c1;
        char c2;
        char c3;
        char c4;
    }cSep;
}UniSt;
```
---


## 下面是一段代码供参考

```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

#pragma pack(8)

typedef unsigned char       BYTE;
typedef unsigned short int  WORD;
typedef unsigned long  int  DWORD;

typedef union {
    DWORD head;
    struct {
        DWORD a:6;
        DWORD b:6;
        DWORD c:6;
        DWORD d:6;
        DWORD e:6;
        DWORD f:2;
    }headst;
}uHead;
typedef union {
    WORD end;
    struct {
        WORD a:5;
        WORD b:2;
        WORD c:7;
        WORD d:2;
    }endst;
}endst;

typedef struct {
    uHead head;
    BYTE  len;
    BYTE  end;
}First;


int main()
{
    int n;
    BYTE   orig[8];
    First mf;
    mf.head.headst.a=33;
    mf.head.headst.b=36;
    mf.head.headst.c=39;
    mf.head.headst.d=49;
    mf.head.headst.e=55;
    mf.head.headst.f=2;
    mf.len=18;
    mf.end=22;
    memcpy(&orig,&mf,8);
    for(n=0;n<8;n++)
        printf("%d-",orig[n]);
    printf("\n");
    printf("head=0x%x,int:%lu\n",mf.head.head,mf.head.head);
   return 0;
}
```


***输出如下***
> 33-121-198-183-18-22-92-183-

> head=0xb7c67921,int:3083237665


