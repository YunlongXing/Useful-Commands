# printf底层调用分析

对于编译型语言，程序的运行需要经过预编译、编译、汇编和链接四个步骤。接下来以```printf```函数为例，分别使用动态```GDB```调试和静态源码分析获取其底层实现流程。

测试环境为：

平台|版本
:----: | :---:
处理器 | Intel i5-8257U
操作系统 | Ubuntu 20.04
内核 | Linux kernel 5.8.0
编译器 | gcc 9.3.0

测试代码如下：
```c
#include <stdio.h>

int main()
{
    printf("Hello, world!\n");
    return 0;
}
```

首先，预编译会替换源码中的宏，如```#include```。预编译结束后，可以在被修改的源程序中看到```printf```的声明：
```
$ gcc -E hello.c -o hello.i
```
```c
...
extern int printf (const char *__restrict __format, ...);
...
int main()
{
    printf("Hello, world!\n");

    return 0;
}
```

然后，编译器将高级语言转换为汇编代码：
```
$ gcc -S hello.i -o hello.s
```
```asm
	.file	"hello.c"
	.text
	.section	.rodata
.LC0:
	.string	"Hello, world!"
	.text
	.globl	main
	.type	main, @function
main:
.LFB0:
	.cfi_startproc
	endbr64
	pushq	%rbp
	.cfi_def_cfa_offset 16
	.cfi_offset 6, -16
	movq	%rsp, %rbp
	.cfi_def_cfa_register 6
	leaq	.LC0(%rip), %rdi
	
	call	puts@PLT
	
	movl	$0, %eax
	popq	%rbp
	.cfi_def_cfa 7, 8
	ret
...
```

从汇编代码中可以看出，```printf```函数被转换成了```call puts```指令，而不是```call printf```指令。究其原因，这是编译器对```printf```函数的优化，如果```printf```的参数是以```\n```结束的纯字符串，则```printf```函数会被优化为```puts```函数，且字符串末尾的```‘\n’```被消除；否则，将会正常输出```call printf```指令。


![printf动态调用流程](images/printfGDB.svg)



![printf静态代码分析](images/printfCODE.svg)


## 参考链接：
[printf背后的故事](https://www.cnblogs.com/fanzhidongyzby/p/3519838.html) <br>
[I/O设备管理实验 - 代码分析](http://edward-zhu.github.io/special/os_exp/2015/01/03/exp-6.2.html)
