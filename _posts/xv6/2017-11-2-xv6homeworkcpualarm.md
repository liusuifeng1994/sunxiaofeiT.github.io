---
layout: blog
istop: true
code: true
title: "操作系统xv6学习笔记-homework xv6 CPU alarm"
background-image: "../img/2017-11-01.jpg"
date: 2017-11-01 23:30:00
category: xv6
tags:
- xv6
- 操作系统
- homework
- 作业完成
- xv6 CPU alarm
---

# 操作系统作业 os03

## CPU ALARM    

- 使用 `grep` 命令找出带有 `update` 的文件，仿照这个系统调用来完成我们的作业

- 在 `syscal.c` 文件中增加函数声明

第一处：
```c
extern .......
extern .......
 .
 .
 .
extern int sys_alarm(void)    //new
```

第二处：
```c
[SYS_...]   ....
 .
 .
 .
[SYS_alarm]     sys_akarm,      //new
```

- 在`syscall.h` 中添加调用号：

```c
#define SYS_...     1
 .                  .
 .                  .
 .                  .
#define SYS_alarm   23
```

- 在`sysproc.c`文件中实现函数 `syscall_alarm`:

```c
int sys_alarm(void){
    int ticks;
    void (*handler)();

    if (argint(0,&ticks) < 0 ){
        return -1;
    }
    if (argptr(1,(char**)&handler,1) < 0 ){

        return -1;
    }
    proc -> alarmticks = ticks;
    proc -> alarmhandler = handler;
    return 0;
}
```

- 在`user.h`中添加函数`alarm`的定义：

```c
int ....
 .
 .
 .
int alarm(int ticks, void (*handler()));    //new
```

-在`useys.S`中，添加：

```c
SYSCALL(...)
 .
 .
 .
SYSCALL(alarm)      //new
```

- 创建新文件`alarmtest.c`

```c
#include "types.h"
#include "stat.h"
#include "user.h"

void periodic();

int
main(int argc, char *argv[])
{
  int i;
  printf(1, "alarmtest starting\n");
  alarm(10, periodic);
  for(i = 0; i < 25*500000; i++){
    if((i % 250000) == 0)
      write(2, ".", 1);
  }
  exit();
}

void
periodic()
{
  printf(1, "alarm!\n");
}
```

- 修改文件`MakeFile`，在 ``UPROGS=\`中添加：

```c
_alarmtest/
```

- 修改`proc.h`文件，在`proc`结构体中增加：

```c   
int alarmticks;             //new
void (* alarmhandler)();    //new
int tickscount;             //new
```

- 修改`trap.c`文件，添加：

```c
 if(cpuid() == 0){
      acquire(&tickslock);
      ticks++;
      wakeup(&ticks);
      release(&tickslock);
    }
    //new-----------------------------------
    if(myproc() &&  (tf -> cs & 3) == 3){
      myproc() -> tickscount++;
      if (myproc() -> tickscount == myproc()->alarmticks){
        myproc() -> tickscount =0;
        tf->esp -= 4;
        *(uint *) tf -> esp = tf -> eip;
        tf -> eip = (uint) myproc() -> alarmhandler;
      }
    }
```