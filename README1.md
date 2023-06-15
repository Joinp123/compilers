# [**实 验 报 告**](http://sigcc.gitee.io/plc2021/#/./lab/proj.final?id=实-验-报-告)

![zucc](http://sigcc.gitee.io/plc2021/lab/zucc.png)

- 课程名称:编程语言原理与编译
- 实验项目:期末大作业
- 专业班级：计算机2001
- 学生学号：32001151 32001130
- 学生姓名：司德昊 张文杰
- 实验指导教师:郭鸣

# 运行脚本

```F#
#r "nuget: fslexyacc"

#load "Absyn.fs";;
#load "Debug.fs";;
#load "CPar.fs";;
#load "CLex.fs";;


open FSharp.Text.Lexing

let show e = 
  printfn "%A" e

let test s =
    let lexbuf = LexBuffer<char>.FromString (s+"\n") in
    CPar.Main CLex.Token lexbuf;

```

```F#
dotnet build ./interpc.fsproj
dotnet fsi

#r "nuget: FsLexYacc";;  //添加包引用
#load "Absyn.fs" "Debug.fs" "CPar.fs" "CLex.fs" "Parse.fs" "Interp.fs" "ParseAndRun.fs" ;; 

open ParseAndRun;;    //导入模块 ParseAndRun
fromFile "myexample\unary.c";;    //显示 ex1.c的语法树
run (fromFile "example\ex1.c") [17];; //解释执行 ex1.c
run (fromFile "myexample\unary.c") [8];; //解释执行 ex11.c

Debug.debug <-  true  //打开调试
```

# 实现的功能点

- （**）注释
- 前缀自增自减
- For循环
- switch语法
- break

## （**）注释

### 测试代码

```c
//test1 (* *)注释测试

void main(int n){
    //annotation 1
    /*annotation 2*/
}
 (* here is annotation 0*)
   
void main(int n){
    //annotation 1
    /*annotation 2*/
   (* here is annotation 0*)
   
}

void main(int n){
    //annotation 1
    /*annotation 2*/
   (* here (*is annot*)ation 0*)
   
}
```

### 解释执行

![](![image-20210629210735576](image-20210629210735576.png).png)

## 自增自减

### 测试代码

```c
// 测试自增自减
void main (int n){
    int i;
    i=5;
    print i;
    print ++i;
    print i;
    print --i;
    print i;
}

/*
void main (int n){
    int i;
    //i++;

}
*/
/*
void main (int n){
    int i;
    i++;
    i--;
}
*/

```

### 语法树

![](![image-20210630000715891](image-20210630000715891.png).png)

### 解释运行

![](![image-20210630013501380](image-20210630013501380.png).png)

## FOR循环实现

### 测试代码

```c
/*
void main(int n){
    print n;
}
*/
void main(int n){
    int i;
    i=0;
    for(i=1;i<n;i++){
        print i;
    }
}
```

![](2023-06-11-21-15-11.png)

### 语法树

![](![image-20210630020954522](image-20210630020954522.png).png)

### 解释执行

![](![image-20210630021043518](image-20210630021043518.png))

## switch

## 测试代码

```
void main(int n){

    switch(n){
        case 0:print 0;
        case 1:print 1;
        case 3:print 3;
        case 4:print 4;

    }

}
```

### 语法树

![1686580292856](image/README/1686580292856.png)

### 解释执行

![1686580319823](image/README/1686580319823.png)

## **break**

### 测试代码

```
void main (int n){
/*
    if( n > 0)
        print n;

  */  
  
    int a ;
    a = 1;
    while(a  < n){
        a = a+1;
        if(a==4) break;
        print a;
    }
 
}
# 执行命令
# .\bin\Debug\net5.0\microc.exe -g .\myexample\break.c 5;
# .\bin\Debug\net5.0\machine.exe  .\break.out 7
```

### 编译执行

![1686755654323](image/README/1686755654323.png)

### 指令

![1686755677926](image/README/1686755677926.png)

# 总结

## 绩效评价

| 姓名   | 学号     | 班级       | 任务       | 权重   |
| ------ | -------- | ---------- | ---------- | ------ |
| Name   | No.      | Class      | Task       | Factor |
| 司德昊 | 32001151 | 计算机2001 | 设计、编码 | 0.5    |
| 张文杰 | 32001130 | 计算机2001 | 报告，测试 | 0.5    |

## 成员代码提交日志

![1686836956985](image/README1/1686836956985.png)![1686836958375](image/README1/1686836958375.png)![1686836958393](image/README1/1686836958393.png)

![1686836917875](image/README1/1686836917875.png)v

![1686836860146](image/README1/1686836860146.png)

![1686836808677](image/README1/1686836808677.png)

![1686836782909](image/README1/1686836782909.png)

## 完成情况

| 实现          | 完成评价 | 备注 |
| ------------- | -------- | ---- |
| （**）注释    | ⭐⭐⭐   |      |
| 前缀自增自减  | ⭐       |      |
| For循环       | ⭐⭐     |      |
| switch语法    | ⭐       |      |
| break编译执行 | ⭐⭐     |      |

## 个人经验教训总结

### 张文杰

通过该课程的设计，掌握了什么是编译程序，编译程序工作的基本过程及其各阶段的基本任务，熟悉了编译程序总流程框图，了解了编译程序的生成过程、构造工具及其相关的技术对课本上的知识有了更深的理解，课本上的知识师机械的，表面的。通过把该算法的内容，算法的执行顺序在计算机上实现，把原来以为很深奥的书本知识变的更为简单，对实验原理有更深的理解
