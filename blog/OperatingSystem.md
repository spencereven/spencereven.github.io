# 1. 操作系统以及对应的基本概念

###    操作系统基本概念

| 基本概念： | 1.控制和管理整个计算机系系统的资源，调度计算机的工作和资源的分配(资源的调度和分配) | 2.为用户和其他的软件提供接口                                 |                                                              |      |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
| 特征       | 最基本特性:  并发(区分对应的并行的概念) 共享(同时共享 互斥共享) | 虚拟(例如虚拟处理器计数: 通过多道程序设计计数，采用让多道程序并发执行 来分时的分配处理机器 使用户感觉到多个处理机器在使用) | 异步（参考一下有关于进程失去封闭性相关的问题）               |      |
| 目标和功能 | 1.作为计算机系统资源的管理者(处理机管理  内存管理 设备管理 文件管理 存储器管理) | 2.为用户与计算机硬件系统之间的接口 - 1.命令接口(用户直接进行交互 - 有联机和脱机 区别就是是否是批处理) 2.程序接口: 系统调用--(广义指令) 通过程序间接进行使用才行(通过程序接口调用: **首先需要进入核心态之后由操作系统机型对应的操作**) | 3.用作扩充机器(硬件称之为裸机，  外层就是操作系统，通过操作系统将外层的更多功能提供给用户进行使用- 称操作系统为扩展机器) |      |
|            |                                                              | --对应什么的操作需要运行在核心态？ -- 对于系统的资源进行操作: I/O(设备) 文件 进程控制 进程通信 内存管理（因此对应的程序员调用对应的应该是 程序接口）![image-20210721224948540](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20210721224948540.png) |                                                              |      |

### 操作系统的发展阶段

| 对应的阶段               | 基本的描述                                                   | 解决了什么问题？有什么优点？                                 | 缺陷是什么？ 引出了下一代什么操作系统                        |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 手工阶段                 | 所有工作人工干预 人机矛盾(速度和资源利用)                    |                                                              | 人机矛盾 - 批处理阶段的系统                                  |
| 批处理阶段               | 1.单道批处理- 解决了人机矛盾以及 CPU和I/O设备速度的矛盾---- 2.多道批处理系统: 多个程序进入并且允许cpu进行交替地执行 | 手工阶段人机矛盾，单道批处理解决CPU/IO速度不匹配地矛盾    ------ 多道批处理:  解决了上述速度矛盾的问题，使其地**吞吐量提高** | 单道批处理: 依旧是告诉运转的cpu等待着缓慢地IO------ 多道批处理: **此就是缺少人机交互(引出分时系统)** |
| 分时操作系统             | 1.同时性 多个终端使用一台计算机               2.交互性 3.独立性:多个用户彼此独立的操作系统 4.及时性(**采用时间片轮转的方式 使一台计算机为多个终端进行服务**) | 批处理阶段缺少交互性的问题                                   | 由于基本分时的操作的划分是按照(时间片的划分进行对应资源的分配)  因此如果是要求少于时间片时间的操作就会出现问题--- 引出了实时系统 |
| 实时操作系统             | 严格的在时间段内处理完接受的事件 实时操作系统的主要特点: 1.及时性 2.可靠性 |                                                              |                                                              |
| 网络操作系统和分布式系统 | ![image-20210721231425435](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20210721231425435.png) |                                                              |                                                              |

基本的计算题: 甘特图的使用 - 有关于多道程序资源的利用问题:



![image-20210721232215176](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20210721232215176.png)

![image-20210721232247428](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20210721232247428.png)

![image-20210721232227592](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20210721232227592.png)



### 操作系统的运行环境

| 运行机制: 两种程序: 用户程序(应用程序) 内核程序 | 触发条件: I/O指令 置中断指令       | 对应的运行状态: 用户态和核心态                               |
| ----------------------------------------------- | ---------------------------------- | ------------------------------------------------------------ |
| 利用时钟管理                                    | 例子:分时操作系统的cpu的时间片轮转 |                                                              |
| 利用中断机制                                    | 并发性:依靠中断和异常实现          | 体现: 键盘鼠标信息输入 2.进程的管理和调度 3.系统功能调用(设备驱动 文件访问) |
| 利用原语                                        |                                    |                                                              |
| 系统控制的数据结构以及处理                      | 进程管理，存储器管理 设备管理      | ![image-20210722084333294](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20210722084333294.png) |

#### 中断和异常的概念：

![image-20210722084525492](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20210722084525492.png)

时间片结束，I/O设备使用完成 - 外中断

#### 系统调用:













# 2.进程有关PV操作对应问题

##### 管程的定义:

```tex
共享资源用共享数据结构表示的时候 资源管理程序可用对该数据结构进行操作的一组过程来表示 如资源的请求和释放过程request和releas 把这一组相关的数据结构和过程归为管程
(局限管程内的数据进行初始化 和一组操作)
"一个管程定义了一个数据结构和能为并发进程所执行在该数据结构上的一组操作" 这组操作能同步改变管程中的数据
 1.局部于管程的共享变量说明
 2.该数据结构进行操作的一组过程
 3.对局部与管程数据设置初始值的语句-此外还要给管程赋予名  字
管程一次只允许一个进程进入管程内部 从而既便于共享资源又能保证互斥
```





```tex

进程 - 实现操作系统的 并发性和共享性
引入PCB - 进程控制块
 1.进程存在的唯一标志
 2.用于控制管理进程
 3.进程实体的构成: 程序段(用于控制的逻辑) 相关数据 PCB
   组成 进程映象(静态) 进程(动态)

 4.系统进行资源分配和调度的独立单位
   -时间片是分配 处理机资源的独立单位
   

进程的五种状态和对应状态的转换
 需要区分的就是: 就绪态和阻塞态的区别
 以及运行->阻塞是主动过程 相反 阻塞->就绪就是被动过程
其中需要注意:
运行态-阻塞态
阻塞态-就绪态


进程的控制: -- 围绕着PCB和进程上下文环境
1.进程的创建
 关键点: PCB创建(标识号 分配对应的空间 进程运行所需资源)
  前者标识号没有 - 创建失败
  后者空间或者资源没有 - 阻塞状态(等待状态)
2.进程的撤销
 关键点: 正常还是非正常？ 资源的撤销(PCB 父程序 子程序)
  PCB队列如何
  正常撤销 - 检索PCB得出状态
3.进程的阻塞和唤醒
 关键点: 什么情况下阻塞和唤醒？ 主动还是被动？
        Block和Wake原语问题  PCB等待队列
4.进程的切换
 关键点: 一切都是由系统调用进入内核完成
        进程切换和处理及模式切换的区别
        环境的问题？ - 保存和恢复
        PCB的问题 - 
        
        
 
 1.单处理系统中 任何时刻并不是只有一个进程处于运行状态
 而是有可能所有的的进程都处于阻塞的状态
 2.并发进程封闭性是指: 自身运行的不同的速度 因为异步的关系
   并不会影响最终程序完成的时间
   而失去封闭性则是自身的速度会影响自身进程运行完成的时间
 3.在多对1的线程模型中 当一个多线程中的进程的某个线程阻塞之后
   整个进程都会被阻塞
 4.由于是单处理器 某一时刻只有一个进程能获得处理器的资源
   所以某一时间段内 并发运行，也正是因为CPU和IO设备的并行
   运行 才能使各进程并发执行
 5.PCB所含数据结构的内容: 进程标志信息 进程控制信息
   进程资源信息 CPU现场信息(则需要利用堆栈指针)
   而明显全局变量不属于
 6.进程中线程共享进程内的全部资源 但进程中某线程的栈指针对
 其他线程是透明的
 7.管道是一种文件 不同进程的是不同的数据和代码段 - 全局变量
 是同一进程而言的
 8.由于键盘的输入速度太慢了 因此完全可以用整个线程来处理整个键盘的输入
 9.临界资源和共享资源的区别: 在一段时间内能否允许多个进程访问 - 并发使用 显然磁盘属于共享设备 公用队列可供多个进程使用
但是一次只能一个进程使用
 -可重入代码 可以供给多个进程使用
  因此共享程序段必须要使用共享程序段进行书写
10.临界区的定义: 访问临界资源A的那段代码
  因此5个并发进程涉及同一个相同变量A
  则变量A相关临界区是由5个临界区构成
11.管程中的signal操作与信号量机制中V操作是不一样的
  信号机制中的V操作一定会改变信号量S=S+1
  而管程中signal操作是针对某个条件变量的 不存在因为
  该条件而阻塞的进程 则signal不会产生任何影响
12.关程局限于: 管程的共享变量说明，对管程内部数据结构进行操作的一组过程以及对局限于管程的数据设置初始值语句
 且 管程中定义的变量只能被管城内的过程访问
 

调度算法 -(可以适用于 作业调度或者是进程调度)
1.FIFO - 对短作业不友好
2.短作业优先SJF - 饥饿现象
3.优先级调度(抢占？ 非抢占？ 静态优先级？ 动态优先级)
4.高响应比 - 响应比: 等待时间+要求服务时间/要求服务时间
  -同时利用了FCFS和SJF 
   等待时间一样 要求服务越短 - 短作业优先
   要求服务时间一样 等待时间长 - 克服饥饿
5.时间片轮转 - 本质是先来先服务但是有时间片 时间片到了
  就阻塞然后排到最后
6.多级反应队列 - 

临界资源: 慢速打印机以及共享的变量-一次只允许一个进程进行访问
同步: 资源和资源使用之间存在先后的关系
互斥: 间接制约(对于临界区资源的访问)
 空闲让进
 忙则等待
 优先等待
 让权等待
```

```java
/*
单标志法: 缺陷是违反了空闲让进原则
开始为0
则P0程序可以进入临界区 并且出来
此时turn = 1
但是如果P1程序 不进入临界区的话
那么P0也无法进入
*/

boolean turn;
while(turn != 0);
//critical section
 turn = 1;
//remainder section

while(turn != 1);
//critical section
 turn = 0;
//remainder section

/*
采用双标志先检测法进行处理:
就是各自拥有各自的flag
其中分别为flag[i]和flag[j]

问题: 由于上下锁不是原子操作
因此会同时进入临界区 -- 违反忙则等待
*/
--明显就是进入了之后 在临界区之前先把对方上锁
  访问完临界区之后 就给对方解锁
    
 Pi
while(flag[i]);
flag[j]=true;
ceitical section;
flag[i]=false;
remainder section;

 Pj
while(flag[j]);
flag[i]=true;
ceitical section;
flag[i]=false;
remainder section;

/*
双标志后检测方法
就是先把自己上锁 然后让给对方
但是如果相互谦让(两变都把自己上锁 就造成了死锁)
违反了 空闲让进
*/
pi
flag[i]=true;
while(flag[j]);
critical section;
flag[i]=flase;
remainder section;

pj
flag[j]=true;
while(flag[i]);
critical section;
flag[j]=flase;
remainder section;

/*
Peterson算法
设置了两个检测变量
为了解决双标志后检测的死锁问题
又添加了turn 其实就是单标志和双标志的结合

如果flag[i]=true则表示Pi想要进入 若此时turn j=true
则说明了此时Pj已经在临界区里面 因此Pi不能访问
但是如果Pj为false则可以访问

*/
```

```java
//信号量的实现:
void wait(semaphore S){
    s.value--l
        if(s.value<0){
            add this process to S.L;
            block(P);
        }
} //请求资源 如果现在value表示的临界资源为0的话
  //则说明直接阻塞请求的进程 然后加入等待队列中
void signal(semaphore S){
    S.value ++;
    if(S.value<= 0){
        remove a process P from S.L;
        wakeup(P);
    }
} //释放资源: 当S.value在释放了之后 还是小于等于0
  //则说明依然有进程在等待队列中 因此就唤醒



//利用信号量实现进程同步 --S的初始值为0
semaphore S=0;
p1(){
    x; //语句x
    V(S); //就是产生了p2所需要的临界资源
}
p2(){
    P(S); //如果先执行P2 -则P2因为S会-- 因此阻塞
    y; //只有执行了p1之后 才会执行P2
}

//利用信号量实现进程互斥 --S的初始值为1
 //核心其实就是 -上锁 访问临界区 再解锁
p1(){
    P(S);
    V(S);
}
p2(){
    p(S);
    V(S);
}

信号量实现前驱关系 -包含了同步和互斥
  总结: 初始所需要的所有信号量为0
1.有多少出度 则需要多少v操作
2.有多少入度 则需要多少P操作 - 先P后V
```



```java
//对应的生产者消费者问题
--互斥的信号量一般初始化为1 同步的信号量一般初始化为0
/*
1.辨明同步和互斥的关系
 同步: 只有生产者生产出来之后 才能消费者拿
 互斥: 两个互斥量: 分别是当容量满的时候 不能够再写入
      以及当空间是空的时候 就不允许取出了
      
      分别设置为: full-一共有n个
      分别设置: empty - 起始为0个
      对于资源区的设置: mutex起始设置为1个
*/

    //为什么不能够先锁住 同步区？
    //因为如果先锁了同步去 然后进入之后 然后被empty锁住了
    //那么资源就一直被锁住了
Producer(){
    while(1){
        //p(mutex);
        p(empty);
        p(mutex);
        生产;
        v(mutex);
        v(full);
    }
}
Consumer(){
    while(1){
        p(full);
        p(mutex);
        消费;
        v(mutex);
        v(empty);
    }
}

//吃苹果问题
/*
桌子上有一个盘子 每次只能向其中放入一个水果 爸爸专向
盘子中放苹果  妈妈专门盘子放橘子 儿子专吃橘子 女儿专门吃
苹果 只有盘子为空的时候 爸爸或者妈妈才能放水果
仅当盘子有自己需要的水果时 儿子或者女儿才能取出
*/

/*
分析: 
1.明确同步关系: 爸苹果-女儿才能吃 妈橘子-儿子才能吃
2.明确互斥关系: 爸爸做或者妈妈做 女儿吃或者儿子吃之间
  都不能干扰  并且如何判断？此时盘子已经有苹果或者橘子了
*/

/*
设置信号量 apple(0) orange(0) mutex(1) current(0)
但仔细想想 一个mutex作为盘子设定1为可以放入 0不可以放入
就不再需要current这个信号量
*/

father(){
    while(1){
      p(current);
      p(mutex);
      produce an apple;
      v(apple);
      v(mutex);
    }
}

mother(){
    while(1){
        p(current);
        p(mutex);
        produce an orange;
        v(orange);
        v(mutex);
    }
}

son(){
    while(1){
        p(apple);
        p(mutex);
        consume an apple;
        v(current);
        v(mutex);
    }
}

daughter(){
    while(1){
        p(orange);
        p(mutex);
        consume an orange;
        v(current);
        v(mutex);
    }
}

/*
读者和写者的问题
1.同步: 只有写者写了之后 读者才能够进行读
2.互斥: 写者在的时候不能读 但是读者之间没有关系

则设置semaphore file(1) write(0) read(1)
其中read是用来限制 读者在看的时候 写入数据
其中file这个临界资源只有在写者操作的时候 才会使用
*/

writer(){
    while(1){
        p(read); //此时是否有读者
        p(file); //占据互斥变量
        write down a file;
        v(write);
        v(mutex);
    }
}
reader(){
    while(1){
        p(write);
        read a file;
        v(read); //为写者开辟空间
    }
}

//但实际上的解决 
/*
写者需要关心的操作比较简单:
只需要写的时候是互斥操作

读者比较复杂: 因为存在多个读者
此时利用count来记录读者的数量 -- 通法多个进程的时候
并且最后一个进程来解决开锁的问题

因为涉及到了count的加减 因此必须要用mutex信号量
来控制

semaphore mutex(1) rw(1) count(0) 
*/

writer(){
    while(1){
        p(rw);
        writing;
        v(rw);
    }
}
reader(){
    while(1){
        p(mutex);
        if(count==0){
            p(rw); //说明此时还没上锁
                   //如果不是第一个进程的话 则说明还有锁
        }
        count++
        v(mutex);
        reading;
        p(mutex)
            count--;
        if(count == 0){
            v(rw);
        }
        v(mutex);        
    }
}

/*
哲学家进餐问题 - 一张圆桌边上坐着5名哲学家
两个之间摆着一根筷子
*/

//将对应的筷子设置为信号量 哲学家进餐的关键就是在于
//如何同时获取到左右两边的筷子
//需要学会如何表示 左边筷子和右边筷子的序号
/*
chopstick[5] -chopstick[i] chopstick[(i+1)%5];
*/
Pi(){
    while(1){
        p(mutex);
        p(chopstick[i]);
        p(chipstick[(i+1)%5];
        v(mutex);
        eating;
        v(chopstick[i]);
        v(chopstick[(i+1)%5]);
        think;   
    } 
}

          
/*
吸烟者问题
抽烟需要三种材料
三个吸烟者 分别拥有除了2个其外的一个资源
生产者会随机产生两种的组合

semaphore offer1 offer2 offer3 finish(判断是否完成)
*/
    
Producer(){
 	while(1){
        random = Math.random();
        if(random%3 == 0){
            v(offer1);
        }
        if(random%3 == 1){
            v(offer2);
        }
        if(random%3 == 2){
            v(offer3);
        }
        p(finish);
    }   
}
process1(){
    while(1){
        p(offer1);
        卷烟 吸烟;
        v(finish);
    }
}
          其他的同理         
```

![image-20211023224338590](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211023224338590.png)

```java
//首先一个明显的加强版生产者消费者问题
//其中多了一个奇偶的判断而已
semaphore odd=0 ven=0 mutex=1
oddnum=0; vennum
```





```tex
有关于死锁的解决方法:
对于四个死锁存在的必要条件
1.互斥资源的存在
2.不可剥夺
3.请求并保持
4.循环等待

对应采用了死锁的预防措施就是破坏上述的条件
1.破坏互斥资源 - 实现是不实际的 因为互斥资源的存在是程序
  安全性和正确性必不可少的一环
2.破坏不可剥夺条件: 顾名思义就是可以在死锁情况下强行剥夺资源. 坏处就是: 1.原来的任务进度可能没了 2.经常剥夺极大的增长了系统的开销
3.破坏请求并保持: 其实就是在开始的时候 就分配好所有运行过程中可能需要的资源 - 
```



































| PV操作对应的问题以及基本的问题介绍                           | 具体问题代码实现(对应下部java)-这里只是阐述细节              | 注意问题 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------- |
| 1.生产者和消费者问题 - (需要判明的同步互斥关系)  同步关系：互斥区域就是存放区域并且只能够存放n个生产对象 因此只有在区域不满的情况下才能放入  /  同理消费者只能够在生产区间有对象的时候才能够进行消费           互斥关系: 生产者在放入商品的过程中消费者不能够使用商品 | 同步关系都是:1. 释放资源的先V后P 此处表示利用P(full)表示判断容量是否已经满了之后再继续加入(如果此时已经满了就会阻塞)  同理p(empty)如果容量已经空了之后继续加入就会阻塞  2.互斥关系和同步关系的关系: 互斥的pv操作必须在同步操作之后 |          |
| 2.苹果桔子问题 -(同步关系: 父产苹果->儿子才能吃 母产桔子->女儿才能吃 使用盘子的过程其实仔细考虑它也是一个同步的关系: 因为只有当儿子和女儿使用了之后盘子才会为空 父母才能放东西(**同时儿子和女儿由于一定盘子有东西的时候这个pv操作-限制了必须当有东西的时候才能使用盘子**)) | 因此同步关系: 就如左边所介绍/理解是否需要临界资源的控制即是mutex--因为四方对于临界资源的访问只有一个临界资源而言 因此同步的过程中对于盘子这个临界资源是有先后顺序的使用 因此也可以不设置mutex ------ 应该是！！！ **一次对于临界资源只有一个人访问** |          |
| 3.吸烟者问题 -(同理可以看作是盘子: 一次只有一个进程访问临界资源因此可以不用特意使用互斥的mutex采用同步完成) 很简单只有有生产东西之后 吸烟者才能够卷烟/ 只有盘子是空的情况下才能够生产原材料放入盘子中(本质和上面的问题一样) ---- 需要注意的就是用户的变化 | 1.涉及到的细节一个就是用户的变化: 用户变量是否int count是否需要临界资源锁定？ count具体应该如何实现: count分别对应1 2 3(起始先count++) 最后跑完if else if之后再count=(count%3)即可  2.剩余的就是对应的同步操作 |          |
| 4.读者和写者问题 - (由于读读是可以进行 - 因此的问题就是临界资源可以同时被两者进行访问-因此临界资源mutex的设定是必不可少的) -其次就是在解决一般的同步问题的基础上如何解决？读读这一个可以进行的实现？ ---- 同样采用count这一变量(是否互斥？) | 1.涉及到的关键就是读读这一个处理？ 因此读者进程应该如何进行处理？ 设定了P(rw)临界变量就是限制读和写同步!!! 具体的实现方法是: 第一个进入的读进程进行加锁得操作 最后一个读进程完成解锁得操作 |          |
| 5.哲学家进餐问题 - 一个人需要同时占用两个临界资源并且还会形成循环等待队列 | 处理得主要方法: 1.破坏循环等待队列: 控制访问临界资源得人数因此必然有一个人是可以获得两个临界资源之后完成释放并且完成进程--- 具体得实现方法有: 最多只允许4个人对临界资源进行访问/ 只允许奇偶序列的允许访问  2.破坏请求和保持的这种情况: -- 直接将一个用户所需要的所有临界资源提前分配出去(**因此可以采用临界变量的mutex进行实现)** |          |

```java
//吸烟者问题
int offer1=0;
int offer2=0;
int offer3=0;
int plate=0;

void producer(int i){
    if(i == 0){
        //生产offer1
        v(offer1);
    }
    else if(i == 1){
        //生产offer2
        v(offer2);
    }
    else if(i == 2){
        //生产offer3
        v(offer3);
    }
    i = (i+1)%3
     wait(plate);
}

void smoker1(){
    while(true){
        p(offer1);
        //卷烟
        //吸烟
        v(plate);
    }
}
void smoker2(){
    while(true){
        p(offer2);
        //卷烟
        //吸烟
        v(plate);
    }
}
void smoker3(){
    while(true){
        p(offer3);
        //卷烟
        //吸烟
        v(plate);
    }
}




//关于读者写者问题的实现
int count = 0; //
int mutex = 1; //访问本次的互斥资源
int rw = 1;
public static void Writer(){
    //其实因为对于写进程而言 一次也是只能够访问一个临界资源的因此对于临界资源的访问可以不添加mutex
	    p(rw);
    	p(mutex);
    	//写入对应的数据
    	v(mutex);
    	v(rw);
}
public static void Reader(){ 
    	p(mutex);//需要同步资源进行count变量的增加 否则两个读者操作
    	if(count == 0)->p(rw);
    	count++;
    	v(mutex);
    	//读文件
         p(mutex);
    	 count--;
    	if(count==0)->v(rw);
    	v(mutex);   	
}

//关于哲学家进餐问题的实现:
semaphore chopsticks[5] = new boolean[5]; //并且所有赋值都是false
semaphore mutex = 1;
int i = 0;


//同时持有左右筷子--更合理的应该说取筷子是一种原子性操作
void philosphor(int i){
    while(1){
        p(mutex);
        p(chopsticks[i]);
        p(chopsticks[(i+1)%5]);
        v(mutex);
        //吃饭
        v(chopsticks[i]);
        v(chopsticks[(i+1)%5]);
        //思考
    }
}
//只允许四个哲学家进餐
void philosopher(int i){
    while(true){
        think();
        wait(room);
        wait(chopsticks[i]);
        wait(chopstick[(i+1)%5]);
        eat();
        signal(chopsticks[i]);
        signal(chopstick[(i+1)%5]);
    }
}
//奇数竞争左边筷子 偶数竞争右边筷子 --就不会出现一个人两边的取不到情况
void philosopher(int i){
    while(true){
        think();
        if(i%2 == 0){
             wait(chopstick[(i+1)%5]);
             wait(chopsticks[i]);
             eat();
             signal(chopsticks[i]);
        	 signal(chopstick[(i+1)%5]);
        }else{
             wait(chopsticks[i]);
             wait(chopstick[(i+1)%5]);
             eat();
             signal(chopstick[(i+1)%5]);
             signal(chopsticks[i]);
        }
    }
}
```





































#### 哲学家进餐问题



![image-20210724174323467](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20210724174323467.png)

![image-20210724175250452](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20210724175250452.png)

![image-20210724175754682](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20210724175754682.png)

![image-20210724180022512](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20210724180022512.png)









#### 进程死锁相关的内容

| 死锁产生的情况对应需要满足的条件                             | 进程的安全序列以及不安全序列以及所对应的相对应的状态，以及前者与死锁形成的一种充分必要条件的关系 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1.共同竞争大于所有进程请求该资源总数的**临界资源**- 临界访问 | 1.首先需要明确： **如果要产生死锁 - 必须满足左边四个条件**   |
| 2.进程在持有临界资源之后由于本身进程的不可剥夺性质-不可剥夺性 | 2.满足左边的四个条件才能称之为进程处于不安全状态(是不安全序列) 缺一不可 |
| 3.进程持有临界资源之后依旧请求其他临界资源的状态 - 持有请求性 | 3.同理只要左边条件有一个不满足 进程就是处于安全序列 安全状态 |
| 4.所有在请求临界资源的进程形成一个循环等待队列               |                                                              |



| 死锁的处理以及对应的机制                                     | 机制所对应的方法的具体实现步骤                               | 方法的缺陷                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1.死锁的预防    根据死锁的产生的四个必要条件进行破坏 其中有互斥访问的共享资源/临界资源访问的不可剥夺性/进程持有临界资源依旧等待的情况/循环等待队列的产生 | 1.破坏临界资源: 采用了spooling的临界资源共享机制  2.破坏不可剥夺性质: 即临界资源可以在本进程时间片执行完毕之后进行剥夺 / 或者给对应的i就能成设立优先级  3.破坏请求保持状态: 事先将进程所需要的临界资源一次性分配完成  4.破坏循环等待队列：采用必须按照顺序分配资源的方式 | 1.临界资源本身就是互斥的一个特性，强行设置为可以共享的一种机制首先在安全性方面就存在巨大的隐患/因此这种方法只能够运用于单处理机的系统  2.进程存在已经完成了一大部分的工作只需要等待最后一点临界资源，因此开销特别大  3.同理 如果提前将所有的资源都分配出去的话(该进程对一个临界资源的需求时间很短 但是却占用了很大的时间)  4.增加新的设备十分困难/ 用户可以对进程的编号进行修改 / 用户实现编程的难度比较大 |
| 2.死锁的避免   最具有代表性质的就是银行家算法                | 银行家算法: 对应代表的含义: 一维数组表示: Request-单次需要请求的临界资源  Avalible-表示系统能够提供临界资源最多的情况  1.Max(总共需要的所有) 2.Allocation - 已经分配的资源 3.Needed - Max-Allocation剩余的需要资源--- 对应的比较策略： 1.Request和Needed进行比较 2.Request和Availible进行比较 3.进行预分配查看如果分配此处的资源是否能够满足  4.采用对应的算法分配之后查看系统是否处于安全的状态 |                                                              |
| 3.死锁的检测以及解除 - 检测采用的就是特殊数据结构以及算法(图和消边实现)/解除采用的就是剥夺资源/解除进程/进程回调的对应机制进行实现 | 对应的图结构： 对应图所代表的意义 1.P进程为其中一种点 2.对应的临界资源(可以利用list<Resources>进行存储代表的是另外一种对应的点) 3.资源->进程表示已经分配的资源(出度)  4.进程->资源(资源的入度)代表 **还需要的临界资源！！**   对应的消除算法：找到可以满足最大临界资源请求的进程->释放对应的临界资源以此类推查看是否最后能否将图中所有的边消除            死锁的解除： 1.前面所提到算法知道了阻塞的进程采用直接剥夺临界资源的方法 2.直接将阻塞进程杀死 3.进程的回调 | 1.直接剥夺临界资源-直接导致了前面所完成的任务结束- 对于系统开销大 2.直接将阻塞进程杀死同理 |

# 3.内存分配相关问题

#### 1.编译装入相关

| 程序执行过程对应的步骤以及对应步骤使用的对应技术 --程序->编译->链接->装配 | 对应所使用技术的一些特点(优点缺点)                           |      |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
| 一般的源程序就是我们高级程序语言距离而言就是.java文件将程序进行编译-- (如果在操作系统上而言编译就是： 将高级语言翻译成汇编语言)java通过的就是java虚拟机 |                                                              |      |
| 链接-> 就是将我们已经形成的汇编语言的指令同对应的类库，其中链接的好处有: 可以将我们的程序进行对应的 **模块化**--- 一个程序可以分成很多的源程序文件 - 1.模块化之后就可以构成我们的公共函数库 数学库用于代码的复用   2.效率更高: 时间上:可以分开编译 只需要重新编译修改的源程序文件即可  空间上: 无需包含共享库中的所有代码: 例如我们调用print这个函数-并不需要写入对应的它的底层代码实现  --- 操作系统方面: 我们应当更加的关注链接的方式: -- 1.静态链接的方式(在装入之前链接完成形成模块)  2.动态链接：运行前装入的过程中进行链接(可能装入不运行) 3.运行时动态链接- 顾名思义就是确定运行之后装入并且链接 |                                                              |      |
| 装配: 就是将我们已经链接完成的程序已经是生成像是java的话就是.java文件就可以直接放入内存中进行运行 --  需要理解的就是装配的几种方式 以及对应方式的缺点   以及对应方式所对应装入内存时候的地址是如何安排的？  1.绝对装入:编译和链接的时候就已经决定了程序在内存中的绝对地址：只适合单程序处理机器   2.静态重定位装入：(需要分配到连续的存储空间中)若要装入内存则需要分配所需的内存空间 否则不装入 装入之后不可移动(每一个内存块的逻辑地址都是从0开始)        3.动态重定位装入: 存入的都是对应的逻辑地址所有都是从0开始 -- 可以分配进入不连续的空间当真正要运行的时候才会分配对应的内存 | 1.绝对装入的：只能够装入到单程序的机器中，在编译和链接的时候就已经决定好了实际的物理地址   2.静态重定位装入: 优点：无需硬件的支持       缺点：--- 地址空间需要连续 进入内存之后不能够移动   3.动态重定位：1）目标模块装入内存时无需任何修改，因而装入之后再搬迁也不会影响其正确执行，这对于存储器紧缩、解决碎片问题是极其有利的（2）一个程序由若干个相对独立的目标模块组成时，每个目标模块各装入一个存储区域，这些存储区域可以不是顺序相邻的，只要各个模块有自己对应的定位寄存器就行。 |      |



#### 2.覆盖和交换以及内存保护

| 引入：应用硬盘存储需要10GB但是电脑的运存根本不满足，但是电脑运行完全没有问题 | 对应技术的优缺点：                                           |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 覆盖技术：同级别的调用结构例如A和B -- 内存创建的就是两者较大的一个因为程序运行有先后因此都可满足 | 缺点: 1 .必须要程序员声明覆盖的结构 操作系统完成自动覆盖 2.对用户不透明 增加了用户编程的负担(因为操作系统完成覆盖) |
| 交换技术: 联系对应的三重调度中的中级调度(就是外存和内存之间的调度关系)--将一个程序不需要使用的块先在外存等待，需要运行时候才调入 | 需要理解的问题：1.应该在外村的什么位置保存换出的进程？ 2.什么时候应该交换？ 3.应该换出哪一些进程？   --------1.磁盘空间分为文件区和对换区域：文件区存放文件 主要追求存储空间的利用率(对文件区空间) 管理采用**离散分配方式**   / 对换区追求的是交换的速度 -- 因此采用的是连续存储的方式 - 并且占用的空间小 |
| 内存的保护：                                                 | 保护用户进程不受其他用户进程的影响： 1 上 下限寄存器-存放用户作业在主存中的下限和上限地址  2.采用重定位寄存器-(存储最低的物理地址) 和限长寄存器--逻辑地址的最大值：每个逻辑地址值必须小于界地址寄存器 |

联想进程的七状态模型

| 对应的就绪挂起态 /以及阻塞挂起态 |
| -------------------------------- |



#### 3.内存的连续管理的方式

| 连续分配管理的方式对应方法的描述                             | 对应方法的优缺点等等                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1.单一连续存储的方式- 将对应的整块程序(也只能能够是单一的一个进程存储进入内存中) | 操作简单 也不会造成任何的外部碎片(但是内部碎片很大)/ 只适合于单处理机单进程的程序 -- 存储的利用率特别底 |
| 2.固定分块的连续存储方式 - 将内存切分为等大的若干个内存块分配给对应的进程 | -因为内存块的大小是固定的 因此如果存入非常大的程序是不能够进入内存的 / 同样也是不会产生外部碎片(但是会产生大量的内部碎片) -- / 如果是运用到锅炉控制等一个操作系统中效率挺高 |
| 3.动态分区分配 - 就是可以对上述固定的分块进行按照大小进行不同的分类用于满足用户进程大小的需要/ 同时在这个基础上可以采用覆盖的方式来复用进程 | --因为是动态的分配进程因此是不会产生内部碎片 但是内存块总体还是按照连续存储的方式不断地往下排 因此会形成一些特别小的碎块在内存块的最底部不会再被利用 - 因此会产生外部碎片  ------- |



| 动态分区分配的一些对应的实现算法                             | 这些算法对应的问题                                           | 动态分区算法回收内存分区                | 对应的分区存储结构 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------------------------------------- | ------------------ |
| 1.首次适应算法 - 根据内存地址由低到高                        | 优点: 算法开销小 / 回收分区之后一般不需要对空闲分区重新排列  | 回收区域之后有相邻的空闲分区-直接合并   | 空闲分区表         |
| 2.最佳适应- 空闲分区按容量递增形成分区链                     | 1. 每次都选最小的内存进行匹配因此到最后会产生外部碎片 -- 并且对于回收完成的进程会存在共同的问题就是: 2.合并之后的内存大小依旧满足这个算法排序的顺序 ----- 因此每一次回收都需要重新排序因此会增大系统的开销 | 回收区域之前有相邻的空闲分区-直接合并   | 空闲分区链         |
| 3.最坏适应 - (最大适应)-容量从大到小                         | 从最大开始适应的话 --1. 在后面需要一个比较大的内存存储块对新的内存进行存储的话 就会无法装入---  2.同理会增大系统的开销 | 回收区域前后都有： -同样合并            |                    |
| 4.邻近适应 - 分配内存时从上次查找的位置向下寻找(**空闲分区以地址递增的次序进行排列)** | 优点：同首次算法一样都是算法的花销比较小 ---- 缺点：会使高地址大分区也被用完 | 回收区前后都没有 - 自己作为一个新的分区 |                    |



#### 4.内存的非连续管理的方式

| 非连续管理方式的引入和主要的操作形式: 最主要的就是可以使内存中内存块对一个程序的运行和存储不需要一个连续的地址块，具体的实现就是：将进程同理进行分块/将内存同样进行分块 -- 其中两者的大小都是相等的： --- 对应的称之为： 页面 页框 |
| ------------------------------------------------------------ |
| 其中本次方式所涉及到的地址转换问题： 一个页面(进程块存储的都是逻辑地址-编号从0开始到一个对应的单元)，在准备装入内存的时候根据查看“页表的信息找到对应的内存块”-- 内存块同样拥有一个起始地址：此时一个进程块的逻辑地址+内存块的起始地址就是真实的物理地址 |
| 对应的地址有关计算方面：1.按照几位存储(表示内存全体一共拥有多少位数) 2.页面大小(同时就意味着页框内存块的大小) 3.因此根据前面2的大小可以计算出总共的内存块的数量：2的(几位存储-页面大小)次方 -------- 当然此处也会存在记录进程块和内存块映射相关页表的大小 ---- 其中**页表的组成** -- 为了寻找以及本身系统性能的要求都是存储在内存中的-因此会占用一定的空间 |
| 一般可能涉及到的计算: 一个内存总共有4GB->2的32因此总共包含有32位的二进制长度来表示 - 其中页面大小4KB -- 2的12次方 因此总共有20位的二进制位数可以用来表示进程块 -- 同理如果再给出一个进程的逻辑地址-- 可以通过对应计算： 逻辑地址/页面大小 = 页号  对应的： 偏移量就是取余数 -------- 紧接着根据对应页表中 页号和内存块的对应可以知道实际上是第几物理块b:  因此物理地址： 物理块大小*页面大小(页框大小)+偏移量 |
| 上面所述了因为有20位的页号用来表示，因此我们的页表项中的一个页表项： 应该是(页号 物理块位置)-- 物理块位置就需要3B的字节进行存储 |



| 基本分页存储管理方式究竟的好处在： | 像分区相等的固定分区技术，分页管理不会产生外部碎片，但是它又有本质的不同点：块的大小相对分区要小很多 而且进程也按照块进行划分--- 进程最后一个不完整的块申请一个主存块空间时 才产生主存碎片-但是这个碎片很小---每个进程平均只产生半块大小的内部碎片(页内碎片) |
| ---------------------------------- | ------------------------------------------------------------ |
| 基于地址变换机构                   | 对应所涉及到的硬件结构: 页表寄存器(PTR) 存放页表的起始位置F和页表的长度M --- 进程未开始执行的时候 放在PCB中 执行之后放入PyemianpianyiliangTR中 |
| 基本的查询方式                     | 进程的逻辑地址A(计算出页号P和页内偏移量W)-- 同PTR中的页表长度比较M如果P>=M(因为M从1开始)则越界--否则就通过页表查询(页号*页表项长度+起始地址)对应的内存块B --- B*页面大小+页面偏移量得到物理地址 |
| 分页管理的主要问题                 | 1.每次访存都需要进行逻辑地址到物理地址的转换，地址转换过程必须足够快 否则访存速率会降低 2.每个进程引入页表 用于存储映射机制-页表不能太大 否则内存利用率会降低 |



#### 5.具有快表的地址变换机构

| 具体要区别页表比较慢和快表查询的一个区别: 主要区分与访问的次数以及访问的一个步骤：  基于快表的 1.逻辑地址原先是经过对应页面大小的计算->页表寄存器比较和页表长度是否越界 --- 基于快表的就是可以直接对应物理地址 |
| ------------------------------------------------------------ |





#### 6.二级页表以及多级页表的搜寻结构

| 来源: 32位的逻辑地址页面大小是4KB需要占据10位的逻辑地址才能够表示一个页面的所有位置，因此剩余了20位的逻辑地址就可以表示2的20次方-1个页面的总长度，因为如果采用页表机制的话就会导致  一个页表项需要3B总共就是24位的逻辑地址才能够包含所有的页表项以及对应的物理块(这里的页号是可以通过计算得出的就是所谓的 逻辑地址/页面大小) ---- 总共有2的20次方个页面因此就需要2的20次方个页表项，  一个页表项3B因此总共就需要3*2的20次方的存储空间专门的连续存储在内存中 |
| ------------------------------------------------------------ |
| 为了解决页表项需要一整块连续的内存进行存储的机制，因此就引入二级页表的概念-引入了二级页表的话只需要在内存需要对应的页号的时候通过查询二级页表就可以找到一级页表再调入内存中就可以知道物理块的位置 ------ 同时引申出来了访问内存的一个次数问题：不在具有快表结构进行访问的话：一级页表是->PCB中的页表寄存器获得对应的页表在内存中的起始位置以及对应页所需要页表的逻辑地址->就可以查询到页表号以及所对应的内存中的物理地址：此时算是访问内存的第一次--- 查询到页表之后通过页表对应的物理块再查询进程实际所在的物理地址(总共访问了两次) ------------ 二级页表的访问次数以此类推多访问一次表就增加多一次 |
| 同时关于二级页表的一个大小的处理问题: 为了解决一级页表连续在内存中的问题，同一级页表解决内存块相同问题一样 采取的一级页表的大小同样是满足最大一个进程块的大小： 例如就是4KB--因此按照上面假设的总共有2的20次方个页表项的话  一个页表(进程块)就可以存放2的8次方个一级页表项---所以是8位数字的一个逻辑地址的占用  因此总共划分就是: 0-7是二级页表所对应的位置 8-19同样包含着一级页表的存放位置，最后的20-31就是存放着真是物理地址偏移量的位置 |
| 关于二级页表越界的一个问题(上面最大长度的一个延申) -- 题目如下: 40位逻辑地址 页面大小4KB 页表项长度4B --- 因此一个页面大小就是2的12次方/2的2次方可以存储最多是10位逻辑地址的长度的页表 40-12-10-10 -8=0 因此除了12是存储了物理地址的实际偏移量其余的都是页表的存储 ------ 因此总共是需要3级页表进行存储 |
| 可以很明显的发现不管是单层还是多层页表的一个操作->对于页表本身的存储的大小还是一个页面的大小 --> 因此为后面引入不同容量的存储单元作了铺垫---->分页存储 |



#### 7.分页存储结构







```tex
有关于页面的置换算法相关:
1.OPT最佳置换算法(永不使用 长时间不使用)-不能实现
2.FIFO - 先进先出(产生分配物理块增大 但是页故障不减反增的异常现象 - Belady异常) 只有FIFO出现
 -基于队列实现算法 不是堆栈类
3.LRU-最近最久未被适用(设置访问字段 记录上次访问的时间) - 需要寄存器和栈的支持
4.时钟CLOCK置换算法
  算法循环扫描缓冲区
 简单的CLOCK算法 - 给帧一个关联附加位-使用位
 只有一个关联位: 
  起始全部都设置为0 因为存入还没满 满了之后就全部为1 要替换的时候 寻找第一个0 但此时全部都是1  则这一圈遇见1就将1置为0  第二圈开始就遇见0置换出去
  
  再加一个修改位: 改进型CLOCK
  <访问位，修改位>
  访问位优先于 修改位  意思访问位若1 先将修改位为1但是访问位为0的置换出去
  

页面分配策略:
 1.固定分配局部置换
  -- 固定块 灵活性差 大小不能把握
  分配的多了: 浪费资源 分配少了: 缺页常出现
 2.可变分配全局置换
  固定一块链表做冗余 如果缺页直接分配
  盲目增加物理块 影响其他进程
 3.可变分配局部置换
  先缺页-采用置换算法
  如果缺页频繁-才调入新的块
  减少了又减少内存块的分配
  
 页面调用时机:
  预先调页-程序员指出 -成功率不是很高
     调入多了-浪费 少了又是缺页多
  请求调页-一次只能调入一页 IO开销大
  
 何处调入页面？
外存分为: 文件区(离散分配)和对换区(连续分配)
因此对换区读取速度>文件区
1.系统拥有足够的对换区空间 
  直接全部对换区交换
2.如果缺少对换区空间

3.Unix - 进程有关的都放在文件区(未运行过的页面 文件区)
  曾经运行过但是被换出 - 对换区


工作集概念: 前面的n个(包括本身)
```

![image-20211102112309666](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211102112309666.png)





















#### 8.内存管理大题

```tex
1.主要的形式和考察:
二级页表+TLB+Cache 其中TLB包括全相联映射和组相联映射

1.各种不同名称之间的推导和大小的计算
2.结合16进制表示的地址-通常有结合数组存储的题目
3.关于虚拟存储置换算法之间的内容和选取
```

```tex
有关于关系重点理清 一级页表和二级页表再到实际物理地址之间的关系
1.一级页表的称之为页目录项 二级页表称之为页表项
 页目录项:  页目录号隐含 二级页表块号(一张二级页表的起始地址)
            以及用于置换算法的(例如有效位和修改位)
 页表项: 同理页表号隐含了  存储的物理块号  以及置换算法的位数
2. 机器字长->虚拟地址->(块内地址+页目录号+页表号/页表索引)
  页目录号+页目录项长度+起始地址 = 页目录表总大小+地址范围
  由于二级页表是由一级推出 因此只需要知道一级页表的地址即可
3.有关TLB 
  虚拟地址全部映射用于比较tag - 全相联方式
  虚拟地址拆分两个部分(第一个部分tag 第二个部分为组数)
  -对应的几路组相联 由 TLB对应对比的"坑"的数量决定
4.小概念问题:
  进程之间切换vs线程之间切换 - 设计TLB是否需要更新？
  以及进程调度的时候 TLB信息存储在哪里？- PCB
```

![image-20211031011244133](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211031011244133.png)

![image-20211031084826007](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211031084826007.png)

```tex
结合了数组的类型 - 数组是按照行进行存储的 并且题目明显是二级页表的形式 告诉了页目录项和页表项长度
-因此对应就可以查询一个一级页表和二级页表的大小
已知一个数组元素4B 而一行有1024个元素 则一共有4KB一行 - 同时一块的大小(页内偏移量则)为4KB
则一块正好可以存放一行数组元素

1.a[1][2] -则是第二行的第三个元素的位置: 已知数组的虚拟地址是10800000（则就是逻辑地址）
逻辑地址肯定是连续的 (然而物理地址不一定连续)-这也是一个考点
拆分为虚拟页号+页内偏移量： 页内偏移量就是第几个页: 由于偏移了一行 因此正好一块 因此虚拟页号只需要+1
而列是第三个元素的开始(就是经过了两个元素 2*4B) 因此10801 008H
展开转译为对应的页目录号和页号
要明确页目录号就是对应在页目录表中的偏移量  页号也是同理
10801 008H
0001 0000 10 | 000 0000 0001 | 0000 0000 1000
  重新4个4个划分: 042H 001H 008H
  对应的042就是页目录项偏移了42个(0-41) 因此就是42*4=168H
  因此已知 页目录表的起始地址 要算页目录项的位置: 起始地址+168H -(同样需要转换...)
  然后已知对应目录表项的页框号(其实就是对应二级页表的物理起始地址) 已知二级页表中的偏移量是001H
  因此再根据一个表项4B 就是 起始地址+4i就可以得出正确答案
  
  本题目所解决的就是一个 如何利用表项来计算偏移量 以及数组的形式应该怎么进行地址的变换-这个比较重要
```



![image-20211031092332275](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211031092332275.png)

```tex
再来经受 此图的洗礼把！！！ 
TLB - translation lookaisde buffer! 其中TLBL-translation lookaside buffer tag！
上述的表示 VPN - virtual page number/虚拟页号 + VPO - virtual page offset 偏移量

1.显然是一个组相联并且是一个思路组相联的TLB示意图  TLBI就是可以表示分为多少个组
  其中TLB中的“坑” - 4个 表示的就是 四位组相联的映射
2.此图也展示了四级页表的形式... 同理
整一个:
   先访问快表TLB - 不成功则访问慢表的一个情况就很清晰了
```

![image-20211031093346054](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211031093346054.png)

```tex
1.很基础 12位 ->4KB - 虚拟地址空间: 总共32位: 4GB/4KB = 1M就是2的20次方页
2.告诉你页目录项4B -> 一级页表一共就是有 2的10次方项  大小就是4*KB =4KB刚好就是一页
  因为有1024项 因此二级页表就占用了1024页(一张二级页表 也是和一级页表一样大) 一共就是 1025页
3.涉及到了从一个虚拟地址到另外一个虚拟地址的问题: 首先要明确虚拟地址是连续的
  接下来的就是要看偏移了多少个一级 页目录项(1个=1024个二级页表)
  0000 0001 00 | 00 0000 0000 | 0000 0000 0000
  0000 0001 00 | 01 0001 0010 | 0000 0100 1000
  首先一级页表项没有变化---因此访问的二级页表没有变化 只需访问1个二级页表
  看二级页表变化  2+16+256 = 274个-说明经过了274个二级页表项
```

![image-20211031094617830](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211031094617830.png)

```tex
刚开始看 是不是特别..吓人！！！！  哈哈哈  
但其实你看到了问题的本质 其实就是熟悉的类型罢了:
首先同理: 这一个题目也是采用二级请求页式管理的内容 对应的页目录号 页表索引以及 页内偏移量
第一个小问: 说f1机器指令代码多少页
很清晰的发现: 最左边就是对应机器指令的虚拟地址(8位16进制进行表示 那么也刚刚好就是32位表示)
0040107F
00401020
     1. 5F-> 5*16+15=95B 很明显变化的也只是页内偏移 因此只是一页
     2.就是一个基本的虚拟地址查看问题: 0040 1020
                               0000 0000 01| 00 0000 0001| 0000 0010 0000
                                01H  01H 020 H
                                很明显都是从第1个表项开始 
     3.涉及的就是IO问题 - 复习了IO之后再来解答
```

![image-20211031101236002](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211031101236002.png)

```tex
1.很明显就是基本考察:  12位偏移了 就是4KB  
  页表大小: 页表项长度*页表项个数 因为采用的一级页表 且一共20位 则一共就是 1M个页表项
  1M*4B = 4MB 4MB/4KB = 1k页
2.同样也是基本表达式的转换问题:
  分别要求解 一级页目录号和二级页号
  LA/2的10次方 ---- 感觉有点像给定了秒数 叫你求解时间的感觉
  LA%2的10次方/2的10十次方
3.由逻辑地址开始 0000 8000H 由于前面0000 8表示的是页号
  00008 000 因为总长度是8KB  则正好两个 00009 000
  页表项的地址: 起始0020 0000H 分别是第一个和第二个 +4 +8
  
```































![image-20210726204615135](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20210726204615135.png)





![image-20210726212309113](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20210726212309113.png)





```tex
虚拟内存:
两种体现的方式:
1.装入程序的时候 只是装入一部分的程序 另外一部分装入在内存之中 当缺页的时候 就会将外村的数据调入内存中
2.当内存执行的过程中 不需要使用的数据也会暂时调出到外存

 部分装入 请求调入 置换功能(对用户完全透明)
 多次性 虚拟性 对换性
 
请求分页管理方式:
1.请求调页面功能和页面置换功能(页表机制 缺页中断机构 地址变换机构)
页表项和普通的分页系统的区别
多了: 状态位P 访问字段A 修改位M 外村地址
```

![image-20211024125219472](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211024125219472.png)





























# 4.文件系统

#### 1.基本的概念和知识

- 为什么需要文件系统？ -希望访问文件 修改文件 保存文件 对文件进行维护管理
- 文件的组成？ 1.数据 2.访问权限信息 3.索引信息(对应索引方便查找)
- 关于文件用户关注: 命名 分类 查找 数据的安全性 文件的操作/ 对于存储细节不涉及
- 文件的结构(可以看作一种存储数据的一种数据类型): -1.数据项： 分为基本数据项 和 组合的数据项 2.记录: 类比于就是一个类包含了相关的数据项 3.文件： 一个对于记录的集合存储---- 逻辑上可以看作为:有结构和无结构 //其中无结构就是所谓的流式存储

-----

**一些概念的基本联系**

1.目录结构和文件的关系： - 目录结构就是关注文件之间式如何被组织起来的， 因此对应的文件信息都保存在目录结构中---- 目录结构存储在外存----- 目录条目包括： 1.文件的名称和唯一的标识符   / 其中标识符定位其他文件属性信息

2.写文件： 系统调用，指明文件的名称和内容，系统搜索**目录**，查找之后维护一个**写的指针**

3.读文件： 系统调用，指定文件的名称和文件块的**内存位置**-- 查找之后维护一个读指针

---

文件属性：

![image-20210802165329995](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20210802165329995.png)

---

文件的打开和关闭

- 

#### 2.目录结构相关知识：

![image-20210804164243546](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20210804164243546.png)





```tex
1.UNIX操作系统中 所有的设备都被视为特殊的文件 因为UNIX操作系统控制和访问外部设备的方式 和任何一个其他文件都是一样的
2.文件的逻辑结构是用户组织数据的结构形式 数据组织形式来自自身的要求 而物理结构是操作系统组织物理存储块的结构方式
3.索引文件由 逻辑文件和索引表组成 文件的逻辑结构和物理结构都有索引的概念 引入逻辑索引和物理索引的目的截然不同 逻辑索引的目的
是加快文件数据的定位 是从用户角度出发 而物理索引的主要目的是管理不连续的物理块
4.read系统调用通过陷入将CPU从用户态切换到核心态 从而获取操作系统提供的服务  读一个文件: 首先需要open系统调用打开文件 open中参数包括了 路径名和文件名 而read只需要调用open返回来的指针即可
5.文件目录项其实就是所谓的FCB-FCB通常包括 文件基本信息 存取控制信息和实用信息组成  基本信息包括: 文件物理地址但是不包括本身FCB在物理块中的地址
6.有关硬连接和软连接有关引用值得问题: 软连接在引用文件的时候
首先是调用文件本身得引用值 而硬连接是在基础上+1， 在删除得时候
对于软连接而言是不会被察觉得(因此软连接得值是不会改变得)
硬连接由于直接删除得话 - 会直接产生错误--因此只是将记录值-1
当记录值为0得时候 在来删除对应的文件
7.相对于加密保护机制 访问控制机制的安全性比较差 因为访问控制的级别和保护力度较小 因此它的灵活性相对比较高  若访问控制不由系统实现 则系统本身的安全性是无法得到保障- 加密机制若由系统实现 则加密方法将无法被拓展
8.系统及安全管理包括: 注册和登录
9.一个文件被用户进程首次打开 即被执行了open操作 会把文件的FCB调入内存中 而不会把文件内容读入内存 只有进程希望获取文件内容时才会读入文件内容
10.用户访问权限抽象为一个矩阵 行代表用户 列代表访问权限  因此有多少用户 每种用户有多少种操作 一共需要n*m比特位

文件系统的层次结构 - 从用户访问开始出发
 1.调用对应的文件访问接口
 2.通过接口寻找到对应的FCB(需要文件目录系统)
   FCB又称之为文件目录项
 3.此时就需要验证了 FCB有对应的控制访问权限
   此时就到了存取控制验证模块
 4.用户验证之后 就开始真正的寻址 - 先寻找逻辑地址
   操作系统经过逻辑文件系统(无结构 有结构(索引 索引顺序))
   的方式找到了
 5.逻辑转-物理(则需要物理文件系统完成)
 6.寻址完成之后 就要关心这块空间如何管理 若要释放空间
 则任务交给-辅助分配模块 若要把这块空间分配给设备用于输入/输出
 则把任务交给设备管理程序模块
```





























# 5.IO

```tex
1.什么是IO设备
2.使用特性分类
 -1.人机交互类 - 数据传输速度慢
 -2.存储设备 - 数据传输速度快
 -3.网络通信设备 - 速度介于前两者之间
3.传输速率分类
 -1.低速 - 键盘鼠标
 -2.中速 - 打印机
 -3.高速设备 - 磁盘
 
4.信息交换单位分类
 -1. 块设备 - 传输速率高 可寻址(随机读写一块)
 -2. 字符设备 传输速率快 不可寻址(输入 输出采用中断)
 
2.IO控制器
 1.机械部件(我们看的见摸得着)
 2.电子部件- IO控制器 设备控制器--印刷电路板
 
 IO控制器功能:
  1.接受和识别CPU发出的命令  - 各种寄存器
  2.向CPU报告设备状态 - 各种寄存器
  3.数据交换 - 各种寄存器
  4.地址识别 - 各种寄存器也需要地址确定
  
与组成原理结合: 要求IO进行写操作
CPU要求写操作->通过数据线利用状态寄存器发出命令字
->状态寄存器经过电路返回对应IO设备的状态并且寄存->CPU读取了对应的状态然后发出写命令字->IO完成之后寄存在了IO控制器的数据寄存器中 -->采用轮询的方式或者中断方式CPU获取数据

```

![image-20211014092145351](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014092145351.png)

```tex
1.一个IO控制器对应多个设备
2.因为有多个设备因此 数据寄存器 控制寄存器 状态寄存器
  可能会有多个
3.且这些寄存器都应该有相应的地址 才能方便CPU操作 有的计算机会让寄存器占用内存地址一部分
 1.内存映像IO - 地址在内存中
 2.IO专用地址 - 地址虽然在内存中,但是寄存器独立编址
```

![image-20211014092537390](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014092537390.png)

```tex
IO控制方式 -- 重点
1.完成一次读写操作的流程
2.CPU干预的频率
3.数据传送的单位
4.数据的流向
5.主要缺点和优点


1.程序直接控制方式 - 轮询
读操作:
CPU->IO逻辑(发出读命令)--轮询检查状态寄存器
-->IO设备准备好数据传给控制器 发送准备好状态-->
控制器将数据放到数据寄存器中 将就绪状态搞定 -->CPU从
数据寄存器中取出到CPU寄存器再放入内存
2.CPU的干预频率如何？
 一直轮询CPU需要不断地轮询检查
3.数据传送单位:
 每次读写一个 字
4.数据流向:
 读操作-数据输入
 写操作 - 数据输出
5.优点: 简单实现-利用程序即可
  缺点: CPU和设备只能传性工作 长期处于忙等 利用率低
```

![image-20211014093247573](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014093247573.png)

```tex
2.中断驱动方式
-计算机组成原理对 中断的整个流程有很详细的讲解
1.一般中断在指令执行周期之后
2.PC+1->判断到是中断程序
 则产生一个向量地址
3.(因为可能多设备产生中断 因此需要对优先级进行判断)
 采用硬件的方式 和软件的方式实现
4.向量地址->入口地址
  入口地址找到对应的指令 一般是JMP跳转指令
  才能够找到中断程序入口
```

![image-20211014094144827](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014094144827.png)

```tex
3.为了将数据流向要经过CPU去除
 引入了DMA方式
 
1.数据传送单位: 由字->块
```

![image-20211014094316026](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014094316026.png)

```tex
DMA控制器就是替换了IO控制器
1.DMA和内存直接连接 因此只需要一开始由CPU指定
 写或者读在内存中的地址 以及读写的次数 即可
2.DMA接受到之后 通过对应的IO控制逻辑 则实现和利用
 IO控制器一样的操作 进行状态的询问 以及数据地寄存
3.获取数据在对应的寄存器之后 只需要一个中断的操作
  DMA可以自动和内存进行数据的传送
  
  --当然对应的寄存器是不止一套的 因为对应了
  不止一个设备接口
  
  但是一次IO指令 只能读写一个或多个连续的数据块
 因此当要读写 离散存储的数据块 CPU要发出多条IO指令
 进行多次中断才能实现
```

![image-20211014094643882](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014094643882.png)

![image-20211014094831133](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014094831133.png)

```tex
4.通道控制方式- 为了解决DMA传送数据的问题
 - 弱鸡版的CPU
 CPU只需要将一开始 通道要执行的通道指令的位置
 传送给通道即可
 通道会自行现在内存中 找到对应的指令
 然后一条一条地执行 并且将对应的数据
 缓冲在通道里面 当所有命令完成之后
 通道才会发出一次中断指令
```

![image-20211014095046003](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014095046003.png)

![image-20211014095200317](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014095200317.png)



```tex
IO的软件层次结构:
1.硬件底层
2.IO核心子系统
3.用户层
```

![image-20211014095338326](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014095338326.png)

```tex
其中用户层 通过对应的编程语言
编译的时候 利用代码所调用的库函数进行
与设备独立性软件层的一个交互 ----- 又称之为系统调用层

为何不同的设备需要同步的设备驱动程序？ -- 设备驱动程序层
--主要是不同设备的硬件特性不同
这些特性只有厂家才能知道 因此厂家必须提供与设备相对应的
驱动方式 CPU执行驱动程序的指令序列 来完成设置
设备寄存器 检查设备状态等工作
---驱动程序一般会以一个独立进程的方式存在
```

![image-20211014100233332](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014100233332.png)

```tex
考查方式 
1.一个IO请求的处理次序？
2.发生IO应答时候？ 什么是顺序？

什么功能？
硬件细节: - 中断处理程序+硬件

逻辑设备表LUR
逻辑设备名 物理设备名 驱动程序入口
```



```tex
IO核心子系统--设备独立性软件+设备驱动程序+中断处理程序
1.重点理解和掌握
 IO调度
 设备保护
 假脱机技术- SPOOLING
 设备分配与回收
 缓冲区管理-(缓冲与高速缓存)

```

![image-20211014100705209](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014100705209.png)

![image-20211014100753668](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014100753668.png)



```tex
假脱机技术- SPOOLING
1.什么是脱机技术？ 解决什么问题？
```

![image-20211014101137201](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014101137201.png)

```tex
因此假脱机计数SPOOLNG的本质就是
利用软件来模拟上述的方式
主要的构成有:
1.输入进程 - 输入情况下外围控制机
2.输出进程 - 输出情况下的外围控制机
3.输入井 输出井 --一一对应(输入磁带 输出磁带)
```

![image-20211014101546125](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014101546125.png)

![image-20211014101920105](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014101920105.png)

![image-20211014101946239](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014101946239.png)

```tex
多个用户进程请求打印的时候
1.系统答应 但是不是直接分配打印机而是由假脱机进程 在
 对应的输出井上 开辟一块硬盘的存储空间
  然后将对应的打印任务清单 形成一个假脱机文件队列 存储在
  输出进程上
  --因此依次的进行打印任务
```

![image-20211014102124677](C:\Users\16953\AppData\Roaming\Typora\typora-user-images\image-20211014102124677.png)



```tex
设备的分配与回收

```











