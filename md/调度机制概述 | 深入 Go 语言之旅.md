> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [go.cyub.vip](https://go.cyub.vip/gmp/gmp-model/)

> GMP 模型 # Golang 的一大特色就是 Goroutine。

Golang 的一大特色就是 Goroutine。Goroutine 是 Golang 支持高并发的重要保障。Golang 可以创建成千上万个 Goroutine 来处理任务，将这些 Goroutine 分配、负载、调度到处理器上采用的是 G-M-P 模型。

什么是 Goroutine [#](#%e4%bb%80%e4%b9%88%e6%98%afgoroutine)
--------------------------------------------------------

Goroutine = Golang + Coroutine。**Goroutine 是 golang 实现的协程，是用户级线程**。Goroutine 具有以下特点：

*   相比线程，其启动的代价很小，以很小栈空间启动（2Kb 左右）
*   能够动态地伸缩栈的大小，最大可以支持到 Gb 级别
*   工作在用户态，切换成很小
*   与线程关系是 n:m，即可以在 n 个系统线程上多工调度 m 个 Goroutine

进程、线程、Goroutine [#](#%e8%bf%9b%e7%a8%8b%e7%ba%bf%e7%a8%8bgoroutine)
-------------------------------------------------------------------

在仅支持进程的操作系统中，进程是拥有资源和独立调度的基本单位。在引入线程的操作系统中，**线程是独立调度的基本单位，进程是资源拥有的基本单位**。在同一进程中，线程的切换不会引起进程切换。在不同进程中进行线程切换, 如从一个进程内的线程切换到另一个进程中的线程时，会引起进程切换

线程创建、管理、调度等采用的方式称为线程模型。线程模型一般分为以下三种：

*   内核级线程 (Kernel Level Thread) 模型
*   用户级线程 (User Level Thread) 模型
*   两级线程模型，也称混合型线程模型

三大线程模型最大差异就在于用户级线程与内核调度实体 KSE（KSE，Kernel Scheduling Entity）之间的对应关系。**KSE 是 Kernel Scheduling Entity 的缩写，其是可被操作系统内核调度器调度的对象实体，是操作系统内核的最小调度单元，可以简单理解为内核级线程**。

**用户级线程即协程**，由应用程序创建与管理，协程必须与内核级线程绑定之后才能执行。**线程由 CPU 调度是抢占式的，协程由用户态调度是协作式的，一个协程让出 CPU 后，才执行下一个协程**。

用户级线程 (ULT) 与内核级线程 (KLT) 比较：

<table><thead><tr><th>特性</th><th>用户级线程</th><th>内核级线程</th></tr></thead><tbody><tr><td>创建者</td><td><strong>应用程序</strong></td><td><strong>内核</strong></td></tr><tr><td>操作系统是否感知存在</td><td>否</td><td>是</td></tr><tr><td>开销成本</td><td><strong>创建成本低，上下文切换成本低</strong>，上下文切换不需要硬件支持</td><td><strong>创建成本高，上下文切换成本高</strong>，上下文切换需要硬件支持</td></tr><tr><td>如果线程阻塞</td><td>整个进程将被阻塞。即不能利用多处理来发挥并发优势</td><td>其他线程可以继续执行, 进程不会阻塞</td></tr><tr><td>案例</td><td>Java thread, POSIX threads</td><td>Window Solaris</td></tr></tbody></table>

### 内核级线程模型 [#](#%e5%86%85%e6%a0%b8%e7%ba%a7%e7%ba%bf%e7%a8%8b%e6%a8%a1%e5%9e%8b)

![](https://static.cyub.vip/images/202008/ult_klt_1_1.jpg)

**内核级线程模型中用户线程与内核线程是一对一关系（1 : 1）**。**线程的创建、销毁、切换工作都是有内核完成的**。应用程序不参与线程的管理工作，只能调用内核级线程编程接口 (应用程序创建一个新线程或撤销一个已有线程时，都会进行一个系统调用）。每个用户线程都会被绑定到一个内核线程。用户线程在其生命期内都会绑定到该内核线程。一旦用户线程终止，两个线程都将离开系统。

操作系统调度器管理、调度并分派这些线程。运行时库为每个用户级线程请求一个内核级线程。操作系统的内存管理和调度子系统必须要考虑到数量巨大的用户级线程。操作系统为每个线程创建上下文。进程的每个线程在资源可用时都可以被指派到处理器内核。

内核级线程模型有如下优点：

*   在多处理器系统中，内核能够并行执行同一进程内的多个线程
*   如果进程中的一个线程被阻塞，不会阻塞其他线程，是能够切换同一进程内的其他线程继续执行
*   当一个线程阻塞时，内核根据选择可以运行另一个进程的线程，而用户空间实现的线程中，运行时系统始终运行自己进程中的线程

缺点：

*   线程的创建与删除都需要 CPU 参与，成本大

### 用户级线程模型 [#](#%e7%94%a8%e6%88%b7%e7%ba%a7%e7%ba%bf%e7%a8%8b%e6%a8%a1%e5%9e%8b)

![](https://static.cyub.vip/images/202008/ult_klt_n_1.jpg)

**用户线程模型中的用户线程与内核线程 KSE 是多对一关系（N : 1）**。**线程的创建、销毁以及线程之间的协调、同步等工作都是在用户态完成**，具体来说就是由应用程序的线程库来完成。**内核对这些是无感知的，内核此时的调度都是基于进程的**。线程的并发处理从宏观来看，任意时刻每个进程只能够有一个线程在运行，且只有一个处理器内核会被分配给该进程。

从上图中可以看出来：库调度器从进程的多个线程中选择一个线程，然后该线程和该进程允许的一个内核线程关联起来。内核线程将被操作系统调度器指派到处理器内核。用户级线程是一种” 多对一” 的线程映射

用户级线程有如下优点：

*   创建和销毁线程、线程切换代价等线程管理的代价比内核线程少得多, 因为保存线程状态的过程和调用程序都只是本地过程
*   线程能够利用的表空间和堆栈空间比内核级线程多

缺点：

*   线程发生 I/O 或页面故障引起的阻塞时，如果调用阻塞系统调用则内核由于不知道有多线程的存在，而会阻塞整个进程从而阻塞所有线程, 因此同一进程中只能同时有一个线程在运行
*   资源调度按照进程进行，多个处理机下，同一个进程中的线程只能在同一个处理机下分时复用

### 两级线程模型 [#](#%e4%b8%a4%e7%ba%a7%e7%ba%bf%e7%a8%8b%e6%a8%a1%e5%9e%8b)

![](https://static.cyub.vip/images/202008/ult_klt_n_m.jpg)

**两级线程模型中用户线程与内核线程是一对一关系（N : M）**。两级线程模型充分吸收上面两种模型的优点，尽量规避缺点。其线程创建在用户空间中完成，线程的调度和同步也在应用程序中进行。一个应用程序中的多个用户级线程被绑定到一些（小于或等于用户级线程的数目）内核级线程上。

### Golang 的线程模型 [#](#golang%e7%9a%84%e7%ba%bf%e7%a8%8b%e6%a8%a1%e5%9e%8b)

**Golang 在底层实现了混合型线程模型**。M 即系统线程，由系统调用产生，一个 M 关联一个 KSE，即两级线程模型中的系统线程。G 为 Groutine，即两级线程模型的的应用及线程。M 与 G 的关系是 N:M。

![](https://static.cyub.vip/images/202008/golang_ult_klt.jpg)

G-M-P 模型概览 [#](#g-m-p%e6%a8%a1%e5%9e%8b%e6%a6%82%e8%a7%88)
----------------------------------------------------------

![](https://static.cyub.vip/images/202402/gmp.jpeg)

G-M-P 分别代表：

*   G - Goroutine，Go 协程，是参与调度与执行的最小单位
*   M - Machine，指的是系统级线程
*   P - Processor，指的是逻辑处理器，P 关联了的本地可运行 G 的队列 (也称为 LRQ)，最多可存放 256 个 G。

GMP 调度流程大致如下：

*   线程 M 想运行任务就需得获取 P，即与 P 关联。
*   然从 P 的本地队列 (LRQ) 获取 G
*   若 LRQ 中没有可运行的 G，M 会尝试从全局队列 (GRQ) 拿一批 G 放到 P 的本地队列，
*   若全局队列也未找到可运行的 G 时候，M 会随机从其他 P 的本地队列偷一半放到自己 P 的本地队列。
*   拿到可运行的 G 之后，M 运行 G，G 执行之后，M 会从 P 获取下一个 G，不断重复下去。

### 调度的生命周期 [#](#%e8%b0%83%e5%ba%a6%e7%9a%84%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f)

![](https://static.cyub.vip/images/202008/golang_schedule_lifetime2.png)

*   M0 是启动程序后的编号为 0 的主线程，这个 M 对应的实例会在全局变量 runtime.m0 中，不需要在 heap 上分配，M0 负责执行初始化操作和启动第一个 G， 在之后 M0 就和其他的 M 一样了
*   G0 是每次启动一个 M 都会第一个创建的 gourtine，G0 仅用于负责调度的 G，G0 不指向任何可执行的函数，每个 M 都会有一个自己的 G0。在调度或系统调用时会使用 G0 的栈空间，全局变量的 G0 是 M0 的 G0

上面生命周期流程说明：

*   runtime 创建最初的线程 m0 和 goroutine g0，并把两者进行关联（g0.m = m0)
*   调度器初始化：设置 M 最大数量，P 个数，栈和内存出事，以及创建 GOMAXPROCS 个 P
*   示例代码中的 main 函数是 main.main，runtime 中也有 1 个 main 函数 ——runtime.main，代码经过编译后，runtime.main 会调用 main.main，程序启动时会为 runtime.main 创建 goroutine，称它为 main goroutine 吧，然后把 main goroutine 加入到 P 的本地队列。
*   启动 m0，m0 已经绑定了 P，会从 P 的本地队列获取 G，获取到 main goroutine。
*   G 拥有栈，M 根据 G 中的栈信息和调度信息设置运行环境
*   M 运行 G
*   G 退出，再次回到 M 获取可运行的 G，这样重复下去，直到 main.main 退出，runtime.main 执行 Defer 和 Panic 处理，或调用 runtime.exit 退出程序。

### G-M-P 的数量 [#](#g-m-p%e7%9a%84%e6%95%b0%e9%87%8f)

G 的数量：

理论上没有数量上限限制的。查看当前 G 的数量可以使用`runtime. NumGoroutine()`

P 的数量：

由启动时环境变量 `$GOMAXPROCS` 或者是由`runtime.GOMAXPROCS()` 决定。这意味着在程序执行的任意时刻都只有 $GOMAXPROCS 个 goroutine 在同时运行。

M 的数量:

go 语言本身的限制：go 程序启动时，会设置 M 的最大数量，默认 10000. 但是内核很难支持这么多的线程数，所以这个限制可以忽略。 runtime/debug 中的 SetMaxThreads 函数，设置 M 的最大数量 一个 M 阻塞了，会创建新的 M。M 与 P 的数量没有绝对关系，一个 M 阻塞，P 就会去创建或者切换另一个 M，所以，即使 P 的默认数量是 1，也有可能会创建很多个 M 出来。

### 调度的流程状态 [#](#%e8%b0%83%e5%ba%a6%e7%9a%84%e6%b5%81%e7%a8%8b%e7%8a%b6%e6%80%81)

![](https://static.cyub.vip/images/202008/golang_schedule_status.jpeg)

从上图我们可以看出来：

*   每个 P 有个局部队列，局部队列保存待执行的 goroutine(流程 2)，当 M 绑定的 P 的的局部队列已经满了之后就会把 goroutine 放到全局队列 (流程 2-1)
*   每个 P 和一个 M 绑定，M 是真正的执行 P 中 goroutine 的实体 (流程 3)，M 从绑定的 P 中的局部队列获取 G 来执行
*   当 M 绑定的 P 的局部队列为空时，M 会从全局队列获取到本地队列来执行 G(流程 3.1)，当从全局队列中没有获取到可执行的 G 时候，M 会从其他 P 的局部队列中偷取 G 来执行 (流程 3.2)，这种从其他 P 偷的方式称为 **work stealing**
*   当 G 因系统调用 (syscall) 阻塞时会阻塞 M，此时 P 会和 M 解绑即 **hand off**，并寻找新的 idle 的 M，若没有 idle 的 M 就会新建一个 M(流程 5.1)。
*   当 G 因 channel 或者 network I/O 阻塞时，不会阻塞 M，M 会寻找其他 runnable 的 G；当阻塞的 G 恢复后会重新进入 runnable 进入 P 队列等待执行 (流程 5.3)

### 调度过程中阻塞 [#](#%e8%b0%83%e5%ba%a6%e8%bf%87%e7%a8%8b%e4%b8%ad%e9%98%bb%e5%a1%9e)

GMP 模型的阻塞可能发生在下面几种情况：

*   I/O，select
*   block on syscall
*   channel
*   等待锁
*   runtime.Gosched()

#### 用户态阻塞 [#](#%e7%94%a8%e6%88%b7%e6%80%81%e9%98%bb%e5%a1%9e)

当 goroutine 因为 channel 操作或者 network I/O 而阻塞时（实际上 golang 已经用 netpoller 实现了 goroutine 网络 I/O 阻塞不会导致 M 被阻塞，仅阻塞 G），对应的 G 会被放置到某个 wait 队列 (如 channel 的 waitq)，该 G 的状态由_Gruning 变为_Gwaitting，而 M 会跳过该 G 尝试获取并执行下一个 G，如果此时没有 runnable 的 G 供 M 运行，那么 M 将解绑 P，并进入 sleep 状态；当阻塞的 G 被另一端的 G2 唤醒时（比如 channel 的可读 / 写通知），G 被标记为 runnable，尝试加入 G2 所在 P 的 runnext，然后再是 P 的 Local 队列和 Global 队列。

#### 系统调用阻塞 [#](#%e7%b3%bb%e7%bb%9f%e8%b0%83%e7%94%a8%e9%98%bb%e5%a1%9e)

当 G 被阻塞在某个系统调用上时，此时 G 会阻塞在_Gsyscall 状态，M 也处于 block on syscall 状态，此时的 M 可被抢占调度：执行该 G 的 M 会与 P 解绑，而 P 则尝试与其它 idle 的 M 绑定，继续执行其它 G。如果没有其它 idle 的 M，但 P 的 Local 队列中仍然有 G 需要执行，则创建一个新的 M；当系统调用完成后，G 会重新尝试获取一个 idle 的 P 进入它的 Local 队列恢复执行，如果没有 idle 的 P，G 会被标记为 runnable 加入到 Global 队列。

G-M-P 内部结构 [#](#g-m-p%e5%86%85%e9%83%a8%e7%bb%93%e6%9e%84)
----------------------------------------------------------

### G 的内部结构 [#](#g%e7%9a%84%e5%86%85%e9%83%a8%e7%bb%93%e6%9e%84)

G 的内部结构中重要字段如下，完全结构参见 [源码](https://github.com/golang/go/blob/5622128a77b4af5e5dc02edf53ecac545e3af730/src/runtime/runtime2.go#L387)

```
type g struct {
    stack       stack   // g自己的栈
    m            *m      // 隶属于哪个M
    sched        gobuf   // 保存了g的现场，goroutine切换时通过它来恢复
    atomicstatus uint32  // G的运行状态
    goid         int64
    schedlink    guintptr // 下一个g, g链表
    preempt      bool //抢占标记
    lockedm      muintptr // 锁定的M,g中断恢复指定M执行
    gopc          uintptr  // 创建该goroutine的指令地址
    startpc       uintptr  // goroutine 函数的指令地址
}


```

G 的状态有以下 9 种，可以参见 [代码](https://github.com/golang/go/blob/5622128a77b4af5e5dc02edf53ecac545e3af730/src/runtime/runtime2.go#L15)：

<table><thead><tr><th>状态</th><th>值</th><th>含义</th></tr></thead><tbody><tr><td>_Gidle</td><td>0</td><td>刚刚被分配，还没有进行初始化。</td></tr><tr><td>_Grunnable</td><td>1</td><td>已经在运行队列中，还没有执行用户代码。</td></tr><tr><td>_Grunning</td><td>2</td><td>不在运行队列里中，已经可以执行用户代码，此时已经分配了 M 和 P。</td></tr><tr><td>_Gsyscall</td><td>3</td><td>正在执行系统调用，此时分配了 M。</td></tr><tr><td>_Gwaiting</td><td>4</td><td>在运行时被阻止，没有执行用户代码，也不在运行队列中，此时它正在某处阻塞等待中。Groutine wait 的原因有哪些参加 <a href="https://github.com/golang/go/blob/5622128a77b4af5e5dc02edf53ecac545e3af730/src/runtime/runtime2.go#L846">代码</a></td></tr><tr><td>_Gmoribund_unused</td><td>5</td><td>尚未使用，但是在 gdb 中进行了硬编码。</td></tr><tr><td>_Gdead</td><td>6</td><td>尚未使用，这个状态可能是刚退出或是刚被初始化，此时它并没有执行用户代码，有可能有也有可能没有分配堆栈。</td></tr><tr><td>_Genqueue_unused</td><td>7</td><td>尚未使用。</td></tr><tr><td>_Gcopystack</td><td>8</td><td>正在复制堆栈，并没有执行用户代码，也不在运行队列中。</td></tr></tbody></table>

### M 的结构 [#](#m%e7%9a%84%e7%bb%93%e6%9e%84)

M 的内部结构，完整结构参见 [源码](https://github.com/golang/go/blob/5622128a77b4af5e5dc02edf53ecac545e3af730/src/runtime/runtime2.go#L452)

```
type m struct {
    g0      *g     // g0, 每个M都有自己独有的g0

    curg          *g       // 当前正在运行的g
    p             puintptr // 隶属于哪个P
    nextp         puintptr // 当m被唤醒时，首先拥有这个p
    id            int64
    spinning      bool // 是否处于自旋

    park          note
    alllink       *m // on allm
    schedlink     muintptr // 下一个m, m链表
    mcache        *mcache  // 内存分配
    lockedg       guintptr // 和 G 的lockedm对应
    freelink      *m // on sched.freem
}


```

### P 的内部结构 [#](#p%e7%9a%84%e5%86%85%e9%83%a8%e7%bb%93%e6%9e%84)

P 的内部结构，完全结构参见 [源码](https://github.com/golang/go/blob/5622128a77b4af5e5dc02edf53ecac545e3af730/src/runtime/runtime2.go#L523)

```
type p struct {
    id          int32
    status      uint32 // P的状态
    link        puintptr // 下一个P, P链表
    m           muintptr // 拥有这个P的M
    mcache      *mcache  

    // P本地runnable状态的G队列，无锁访问
    runqhead uint32
    runqtail uint32
    runq     [256]guintptr
    
    runnext guintptr // 一个比runq优先级更高的runnable G

    // 状态为dead的G链表，在获取G时会从这里面获取
    gFree struct {
        gList
        n int32
    }

    gcBgMarkWorker       guintptr // (atomic)
    gcw gcWork

}


```

P 有以下几种状态，参加 [源码](https://github.com/golang/go/blob/5622128a77b4af5e5dc02edf53ecac545e3af730/src/runtime/runtime2.go#L100)

<table><thead><tr><th>状态</th><th>值</th><th>含义</th></tr></thead><tbody><tr><td>_Pidle</td><td>0</td><td>刚刚被分配，还没有进行进行初始化。</td></tr><tr><td>_Prunning</td><td>1</td><td>当 M 与 P 绑定调用 acquirep 时，P 的状态会改变为 _Prunning。</td></tr><tr><td>_Psyscall</td><td>2</td><td>正在执行系统调用。</td></tr><tr><td>_Pgcstop</td><td>3</td><td>暂停运行，此时系统正在进行 GC，直至 GC 结束后才会转变到下一个状态阶段。</td></tr><tr><td>_Pdead</td><td>4</td><td>废弃，不再使用。</td></tr></tbody></table>

### 调度器的内部结构 [#](#%e8%b0%83%e5%ba%a6%e5%99%a8%e7%9a%84%e5%86%85%e9%83%a8%e7%bb%93%e6%9e%84)

调度器内部结构，完全结构参见 [源码](https://github.com/golang/go/blob/5622128a77b4af5e5dc02edf53ecac545e3af730/src/runtime/runtime2.go#L604)

```
type schedt struct {

    lock mutex

    midle        muintptr // 空闲M链表
    nmidle       int32    // 空闲M数量
    nmidlelocked int32    // 被锁住的M的数量
    mnext        int64    // 已创建M的数量，以及下一个M ID
    maxmcount    int32    // 允许创建最大的M数量
    nmsys        int32    // 不计入死锁的M数量
    nmfreed      int64    // 累计释放M的数量

    pidle      puintptr // 空闲的P链表
    npidle     uint32   // 空闲的P数量

    runq     gQueue // 全局runnable的G队列
    runqsize int32  // 全局runnable的G数量

    // Global cache of dead G's.
    gFree struct {
        lock    mutex
        stack   gList // Gs with stacks
        noStack gList // Gs without stacks
        n       int32
    }

    // freem is the list of m's waiting to be freed when their
    // m.exited is set. Linked through m.freelink.
    freem *m
}


```

观察调度流程 [#](#%e8%a7%82%e5%af%9f%e8%b0%83%e5%ba%a6%e6%b5%81%e7%a8%8b)
-------------------------------------------------------------------

### GODEBUG trace 方式 [#](#godebug-trace%e6%96%b9%e5%bc%8f)

GODEBUG 变量可以控制运行时内的调试变量，参数以逗号分隔，格式为：name=val。观察 GMP 可以使用下面两个参数：

*   schedtrace：设置 schedtrace=X 参数可以使运行时在每 X 毫秒输出一行调度器的摘要信息到标准 err 输出中。
    
*   scheddetail：设置 schedtrace=X 和 scheddetail=1 可以使运行时在每 X 毫秒输出一次详细的多行信息，信息内容主要包括调度程序、处理器、OS 线程 和 Goroutine 的状态。
    

```
package main

import (
    "sync"
    "time"
)

func main() {
	var wg sync.WaitGroup

	for i := 0; i < 2000; i++ {
		wg.Add(1)
		go func() {
			a := 0

			for i := 0; i < 1e6; i++ {
				a += 1
			}

			wg.Done()
        }()
        time.Sleep(100 * time.Millisecond)
	}

	wg.Wait()
}


```

执行一下命令：

> GODEBUG=schedtrace=1000 go run ./test.go

输出内容如下：

```
SCHED 0ms: gomaxprocs=1 idleprocs=1 threads=4 spinningthreads=0 idlethreads=1 runqueue=0 [0]
SCHED 1001ms: gomaxprocs=1 idleprocs=1 threads=4 spinningthreads=0 idlethreads=2 runqueue=0 [0]
SCHED 2002ms: gomaxprocs=1 idleprocs=1 threads=4 spinningthreads=0 idlethreads=2 runqueue=0 [0]
SCHED 3002ms: gomaxprocs=1 idleprocs=1 threads=4 spinningthreads=0 idlethreads=2 runqueue=0 [0]
SCHED 4003ms: gomaxprocs=1 idleprocs=1 threads=4 spinningthreads=0 idlethreads=2 runqueue=0 [0]


```

输出内容解释说明：

*   SCHED XXms: SCHED 是调度日志输出标志符。XXms 是自程序启动之后到输出当前行时间
*   gomaxprocs： P 的数量，等于当前的 CPU 核心数，或者 GOMAXPROCS 环境变量的值
*   idleprocs： 空闲 P 的数量，与 gomaxprocs 的差值即运行中 P 的数量
*   threads： 线程数量，即 M 的数量
*   spinningthreads：自旋状态线程的数量。当 M 没有找到可供其调度执行的 Goroutine 时，该线程并不会销毁，而是出于自旋状态
*   idlethreads：空闲线程的数量
*   runqueue：全局队列中 G 的数量
*   [0]：表示 P 本地队列下 G 的数量，有几个 P 中括号里面就会有几个数字

### Go tool trace 方式 [#](#go-tool-trace%e6%96%b9%e5%bc%8f)

```
func main() {
	// 创建trace文件
	f, err := os.Create("trace.out")
	if err != nil {
		panic(err)
	}
	defer f.Close()

	// 启动trace goroutine
	err = trace.Start(f)
	if err != nil {
		panic(err)
	}
	defer trace.Stop()

	// main
	fmt.Println("Hello trace")
}


```

执行下面命令产生 trace 文件 trace.out：

> go run test.go

执行下面命令，打开浏览器，打开控制台查看。

> go tool trace trace.out

### 总结 [#](#%e6%80%bb%e7%bb%93)

1.  Golang 的线程模型采用的是混合型线程模型，线程与协程关系是 N:M。
2.  Golang 混合型线程模型实现采用 GMP 模型进行调度，G 是 goroutine，是 golang 实现的协程，M 是 OS 线程，P 是逻辑处理器。
3.  每一个 M 都需要与一个 P 绑定，P 拥有本地可运行 G 队列，M 是执行 G 的单元，M 获取可运行 G 流程是先从 P 的本地队列获取，若未获取到，则从其他 P 偷取过来（即 work steal)，若其他的 P 也没有则从全局 G 队列获取，若都未获取到，则 M 将处于自旋状态，并不会销毁。
4.  当执行 G 时候，发生通道阻塞等用户级别阻塞时候，此时 M 不会阻塞，M 会继续寻找其他可运行的 G，当阻塞的 G 恢复之后，重新进入 P 的队列等待执行，若 G 进行系统调用时候，会阻塞 M，此时 P 会和 M 解绑 (即 hand off)，并寻找新的空闲的 M。若没有空闲的就会创建一个新的 M。
5.  Work Steal 和 Hand Off 保证了线程的高效利用。

**G-M-P 高效的保证策略有：**

*   M 是可以复用的，不需要反复创建与销毁，当没有可执行的 Goroutine 时候就处于自旋状态，等待唤醒
*   Work Stealing 和 Hand Off 策略保证了 M 的高效利用
*   内存分配状态 (mcache) 位于 P，G 可以跨 M 调度，不再存在跨 M 调度局部性差的问题
*   M 从关联的 P 中获取 G，不需要使用锁，是 lock free 的

参考资料 [#](#%e5%8f%82%e8%80%83%e8%b5%84%e6%96%99)
-----------------------------------------------

*   [Golang 调度器 GMP 原理与调度全分析](https://learnku.com/articles/41728)
*   [Go: Work-Stealing in Go Scheduler](https://medium.com/a-journey-with-go/go-work-stealing-in-go-scheduler-d439231be64d)
*   [线程的 3 种实现方式–内核级线程, 用户级线程和混合型线程](https://blog.csdn.net/gatieme/article/details/51892437)