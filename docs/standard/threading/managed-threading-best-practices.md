---
title: 托管线程处理的最佳做法
description: 了解 .NET 中托管线程处理的最佳做法。 处理复杂的情况，如协调多个线程或处理阻塞线程。
ms.date: 10/15/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- threading [.NET], design guidelines
- threading [.NET], best practices
- managed threading
ms.assetid: e51988e7-7f4b-4646-a06d-1416cee8d557
ms.openlocfilehash: 88e1f34388cd58fef59bc4005bcaf630c59a661e
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188999"
---
# <a name="managed-threading-best-practices"></a><span data-ttu-id="37dbc-104">托管线程处理的最佳做法</span><span class="sxs-lookup"><span data-stu-id="37dbc-104">Managed threading best practices</span></span>

<span data-ttu-id="37dbc-105">多线程处理需在编程时倍加注意。</span><span class="sxs-lookup"><span data-stu-id="37dbc-105">Multithreading requires careful programming.</span></span> <span data-ttu-id="37dbc-106">对于多数任务，通过将执行请求以线程池线程的方式排队，可以降低复杂性。</span><span class="sxs-lookup"><span data-stu-id="37dbc-106">For most tasks, you can reduce complexity by queuing requests for execution by thread pool threads.</span></span> <span data-ttu-id="37dbc-107">本主题将探讨更复杂的情形，比如协调多个线程的工作或处理造成阻止的线程。</span><span class="sxs-lookup"><span data-stu-id="37dbc-107">This topic addresses more difficult situations, such as coordinating the work of multiple threads, or handling threads that block.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="37dbc-108">自 .NET Framework 4 起，任务并行库和 PLINQ 提供了 API，可降低多线程编程的一些复杂性和风险。</span><span class="sxs-lookup"><span data-stu-id="37dbc-108">Starting with .NET Framework 4, the Task Parallel Library and PLINQ provide APIs that reduce some of the complexity and risks of multi-threaded programming.</span></span> <span data-ttu-id="37dbc-109">有关详细信息，请参阅 [.NET 中的并行编程](../parallel-programming/index.md)。</span><span class="sxs-lookup"><span data-stu-id="37dbc-109">For more information, see [Parallel Programming in .NET](../parallel-programming/index.md).</span></span>  
  
## <a name="deadlocks-and-race-conditions"></a><span data-ttu-id="37dbc-110">死锁和争用条件</span><span class="sxs-lookup"><span data-stu-id="37dbc-110">Deadlocks and race conditions</span></span>  
 <span data-ttu-id="37dbc-111">多线程处理解决了吞吐量和响应性问题，但引入此功能会带来新的问题：死锁和争用条件。</span><span class="sxs-lookup"><span data-stu-id="37dbc-111">Multithreading solves problems with throughput and responsiveness, but in doing so it introduces new problems: deadlocks and race conditions.</span></span>  
  
### <a name="deadlocks"></a><span data-ttu-id="37dbc-112">死锁</span><span class="sxs-lookup"><span data-stu-id="37dbc-112">Deadlocks</span></span>  
 <span data-ttu-id="37dbc-113">两个线程中的每一个线程都尝试锁定另外一个线程已锁定的资源时，就会发生死锁。</span><span class="sxs-lookup"><span data-stu-id="37dbc-113">A deadlock occurs when each of two threads tries to lock a resource the other has already locked.</span></span> <span data-ttu-id="37dbc-114">两个线程都不能继续执行。</span><span class="sxs-lookup"><span data-stu-id="37dbc-114">Neither thread can make any further progress.</span></span>  
  
 <span data-ttu-id="37dbc-115">托管线程处理类的许多方法都提供了超时设定，有助于检测死锁。</span><span class="sxs-lookup"><span data-stu-id="37dbc-115">Many methods of the managed threading classes provide time-outs to help you detect deadlocks.</span></span> <span data-ttu-id="37dbc-116">例如，下面的代码尝试在 `lockObject` 对象上获取锁。</span><span class="sxs-lookup"><span data-stu-id="37dbc-116">For example, the following code attempts to acquire a lock on an object named `lockObject`.</span></span> <span data-ttu-id="37dbc-117">如果在 300 毫秒内没有获取锁，<xref:System.Threading.Monitor.TryEnter%2A?displayProperty=nameWithType> 返回 `false`。</span><span class="sxs-lookup"><span data-stu-id="37dbc-117">If the lock is not obtained in 300 milliseconds, <xref:System.Threading.Monitor.TryEnter%2A?displayProperty=nameWithType> returns `false`.</span></span>  
  
```vb  
If Monitor.TryEnter(lockObject, 300) Then  
    Try  
        ' Place code protected by the Monitor here.  
    Finally  
        Monitor.Exit(lockObject)  
    End Try  
Else  
    ' Code to execute if the attempt times out.  
End If  
```  
  
```csharp  
if (Monitor.TryEnter(lockObject, 300)) {  
    try {  
        // Place code protected by the Monitor here.  
    }  
    finally {  
        Monitor.Exit(lockObject);  
    }  
}  
else {  
    // Code to execute if the attempt times out.  
}  
```  
  
### <a name="race-conditions"></a><span data-ttu-id="37dbc-118">争用条件</span><span class="sxs-lookup"><span data-stu-id="37dbc-118">Race conditions</span></span>  
 <span data-ttu-id="37dbc-119">争用条件是程序的结果取决于两个或更多个线程中的哪一个先到达某一特定代码块时出现的一种 bug。</span><span class="sxs-lookup"><span data-stu-id="37dbc-119">A race condition is a bug that occurs when the outcome of a program depends on which of two or more threads reaches a particular block of code first.</span></span> <span data-ttu-id="37dbc-120">多次运行程序会产生不同的结果，并且无法预测任何给定运行的结果。</span><span class="sxs-lookup"><span data-stu-id="37dbc-120">Running the program many times produces different results, and the result of any given run cannot be predicted.</span></span>  
  
 <span data-ttu-id="37dbc-121">争用条件的一个简单例子是递增一个字段。</span><span class="sxs-lookup"><span data-stu-id="37dbc-121">A simple example of a race condition is incrementing a field.</span></span> <span data-ttu-id="37dbc-122">假定某个类有一个私有 **static** 字段（在 Visual Basic 中为 **Shared** ），每创建该类的一个实例时它都递增一次，使用的代码是 `objCt++;` (C#) 或 `objCt += 1` (Visual Basic)。</span><span class="sxs-lookup"><span data-stu-id="37dbc-122">Suppose a class has a private **static** field ( **Shared** in Visual Basic) that is incremented every time an instance of the class is created, using code such as `objCt++;` (C#) or `objCt += 1` (Visual Basic).</span></span> <span data-ttu-id="37dbc-123">此操作要求将 `objCt` 的值加载到寄存器中，使该值递增，然后将其存储到 `objCt` 中。</span><span class="sxs-lookup"><span data-stu-id="37dbc-123">This operation requires loading the value from `objCt` into a register, incrementing the value, and storing it in `objCt`.</span></span>  
  
 <span data-ttu-id="37dbc-124">在多线程应用程序中，一个已加载并递增该值的线程可能会被另一个线程抢先，抢先的线程执行全部三个步骤；第一个线程继续执行并存储其值时，它会覆盖 `objCt`，但不考虑该值在其暂停执行期间已更改这一事实。</span><span class="sxs-lookup"><span data-stu-id="37dbc-124">In a multithreaded application, a thread that has loaded and incremented the value might be preempted by another thread which performs all three steps; when the first thread resumes execution and stores its value, it overwrites `objCt` without taking into account the fact that the value has changed in the interim.</span></span>  
  
 <span data-ttu-id="37dbc-125">通过使用 <xref:System.Threading.Interlocked> 类的方法（如 <xref:System.Threading.Interlocked.Increment%2A?displayProperty=nameWithType>），可以轻松避免这种争用条件。</span><span class="sxs-lookup"><span data-stu-id="37dbc-125">This particular race condition is easily avoided by using methods of the <xref:System.Threading.Interlocked> class, such as <xref:System.Threading.Interlocked.Increment%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="37dbc-126">若要了解在多个线程间同步数据的其他技巧，请参阅[为多线程处理同步数据](synchronizing-data-for-multithreading.md)。</span><span class="sxs-lookup"><span data-stu-id="37dbc-126">To read about other techniques for synchronizing data among multiple threads, see [Synchronizing Data for Multithreading](synchronizing-data-for-multithreading.md).</span></span>  
  
 <span data-ttu-id="37dbc-127">争用条件也可能会在同步多个线程的活动时发生。</span><span class="sxs-lookup"><span data-stu-id="37dbc-127">Race conditions can also occur when you synchronize the activities of multiple threads.</span></span> <span data-ttu-id="37dbc-128">编写每一行代码时，都必须考虑出现以下情况时会发生什么情况：一个线程在执行该行代码（或构成该行的任何机器指令）前，其他线程抢先执行了该代码。</span><span class="sxs-lookup"><span data-stu-id="37dbc-128">Whenever you write a line of code, you must consider what might happen if a thread were preempted before executing the line (or before any of the individual machine instructions that make up the line), and another thread overtook it.</span></span>  
  
## <a name="static-members-and-static-constructors"></a><span data-ttu-id="37dbc-129">静态成员和静态构造函数</span><span class="sxs-lookup"><span data-stu-id="37dbc-129">Static members and static constructors</span></span>  
 <span data-ttu-id="37dbc-130">在类的类构造函数（C# 中为 `static` 构造函数、Visual Basic 中为 `Shared Sub New`）完成运行之前，该类不会初始化。</span><span class="sxs-lookup"><span data-stu-id="37dbc-130">A class is not initialized until its class constructor (`static` constructor in C#, `Shared Sub New` in Visual Basic) has finished running.</span></span> <span data-ttu-id="37dbc-131">为防止对未初始化的类型执行代码，在类构造函数完成运行之前，公共语言运行时会禁止从其他线程到类的 `static` 成员（在 Visual Basic 中为 `Shared` 成员）的所有调用。</span><span class="sxs-lookup"><span data-stu-id="37dbc-131">To prevent the execution of code on a type that is not initialized, the common language runtime blocks all calls from other threads to `static` members of the class (`Shared` members in Visual Basic) until the class constructor has finished running.</span></span>  
  
 <span data-ttu-id="37dbc-132">例如，如果某个类构造函数启动了一个新线程，并且该线程过程调用了该类的 `static` 成员，则在该类构造函数完成之前，会一直禁止新线程。</span><span class="sxs-lookup"><span data-stu-id="37dbc-132">For example, if a class constructor starts a new thread, and the thread procedure calls a `static` member of the class, the new thread blocks until the class constructor completes.</span></span>  
  
 <span data-ttu-id="37dbc-133">以上情况适用于可拥有 `static` 构造函数的任意类型。</span><span class="sxs-lookup"><span data-stu-id="37dbc-133">This applies to any type that can have a `static` constructor.</span></span>  

## <a name="number-of-processors"></a><span data-ttu-id="37dbc-134">处理器数量</span><span class="sxs-lookup"><span data-stu-id="37dbc-134">Number of processors</span></span>

<span data-ttu-id="37dbc-135">系统中是有多个处理器还是仅有一个处理器会影响多线程体系结构。</span><span class="sxs-lookup"><span data-stu-id="37dbc-135">Whether there are multiple processors or only one processor available on a system can influence multithreaded architecture.</span></span> <span data-ttu-id="37dbc-136">有关详细信息，请参阅[处理器数量](/previous-versions/dotnet/netframework-1.1/1c9txz50(v=vs.71)#number-of-processors)。</span><span class="sxs-lookup"><span data-stu-id="37dbc-136">For more information, see [Number of Processors](/previous-versions/dotnet/netframework-1.1/1c9txz50(v=vs.71)#number-of-processors).</span></span>

<span data-ttu-id="37dbc-137">使用 <xref:System.Environment.ProcessorCount?displayProperty=nameWithType> 属性来确定在运行时可用的处理器数量。</span><span class="sxs-lookup"><span data-stu-id="37dbc-137">Use the <xref:System.Environment.ProcessorCount?displayProperty=nameWithType> property to determine the number of processors available at run time.</span></span>
  
## <a name="general-recommendations"></a><span data-ttu-id="37dbc-138">一般性建议</span><span class="sxs-lookup"><span data-stu-id="37dbc-138">General recommendations</span></span>  
 <span data-ttu-id="37dbc-139">使用多线程时需考虑以下准则：</span><span class="sxs-lookup"><span data-stu-id="37dbc-139">Consider the following guidelines when using multiple threads:</span></span>  
  
- <span data-ttu-id="37dbc-140">请勿使用 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 终止其他线程。</span><span class="sxs-lookup"><span data-stu-id="37dbc-140">Don't use <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> to terminate other threads.</span></span> <span data-ttu-id="37dbc-141">对另一个线程调用 **Abort** 无异于引发该线程的异常，也不知道该线程已处理到哪个位置。</span><span class="sxs-lookup"><span data-stu-id="37dbc-141">Calling **Abort** on another thread is akin to throwing an exception on that thread, without knowing what point that thread has reached in its processing.</span></span>  
  
- <span data-ttu-id="37dbc-142">请勿使用 <xref:System.Threading.Thread.Suspend%2A?displayProperty=nameWithType> 和 <xref:System.Threading.Thread.Resume%2A?displayProperty=nameWithType> 同步多个线程的活动。</span><span class="sxs-lookup"><span data-stu-id="37dbc-142">Don't use <xref:System.Threading.Thread.Suspend%2A?displayProperty=nameWithType> and <xref:System.Threading.Thread.Resume%2A?displayProperty=nameWithType> to synchronize the activities of multiple threads.</span></span> <span data-ttu-id="37dbc-143">请使用 <xref:System.Threading.Mutex>、<xref:System.Threading.ManualResetEvent>、<xref:System.Threading.AutoResetEvent> 和 <xref:System.Threading.Monitor>。</span><span class="sxs-lookup"><span data-stu-id="37dbc-143">Do use <xref:System.Threading.Mutex>, <xref:System.Threading.ManualResetEvent>, <xref:System.Threading.AutoResetEvent>, and <xref:System.Threading.Monitor>.</span></span>  
  
- <span data-ttu-id="37dbc-144">不要从主程序中控制工作线程的执行（如使用事件）。</span><span class="sxs-lookup"><span data-stu-id="37dbc-144">Don't control the execution of worker threads from your main program (using events, for example).</span></span> <span data-ttu-id="37dbc-145">而应设计程序，使工作线程负责等待任务可用，然后执行任务，并在完成时通知程序的其他部分。</span><span class="sxs-lookup"><span data-stu-id="37dbc-145">Instead, design your program so that worker threads are responsible for waiting until work is available, executing it, and notifying other parts of your program when finished.</span></span> <span data-ttu-id="37dbc-146">如果不阻止工作线程，请考虑使用线程池线程。</span><span class="sxs-lookup"><span data-stu-id="37dbc-146">If your worker threads do not block, consider using thread pool threads.</span></span> <span data-ttu-id="37dbc-147"><xref:System.Threading.Monitor.PulseAll%2A?displayProperty=nameWithType> 非常适用于阻止工作线程。</span><span class="sxs-lookup"><span data-stu-id="37dbc-147"><xref:System.Threading.Monitor.PulseAll%2A?displayProperty=nameWithType> is useful in situations where worker threads block.</span></span>  
  
- <span data-ttu-id="37dbc-148">不要将类型用作锁定对象。</span><span class="sxs-lookup"><span data-stu-id="37dbc-148">Don't use types as lock objects.</span></span> <span data-ttu-id="37dbc-149">也就是说，避免一些代码，如 C# 中的 `lock(typeof(X))` 或 Visual Basic 中的 `SyncLock(GetType(X))`，或避免使用 <xref:System.Threading.Monitor.Enter%2A?displayProperty=nameWithType> 和 <xref:System.Type> 对象。</span><span class="sxs-lookup"><span data-stu-id="37dbc-149">That is, avoid code such as `lock(typeof(X))` in C# or `SyncLock(GetType(X))` in Visual Basic, or the use of <xref:System.Threading.Monitor.Enter%2A?displayProperty=nameWithType> with <xref:System.Type> objects.</span></span> <span data-ttu-id="37dbc-150">对于给定类型，每个应用域只有一个 <xref:System.Type?displayProperty=nameWithType> 实例。</span><span class="sxs-lookup"><span data-stu-id="37dbc-150">For a given type, there is only one instance of <xref:System.Type?displayProperty=nameWithType> per application domain.</span></span> <span data-ttu-id="37dbc-151">如果锁定对象的类型是“公共的”，那么不属于自己的代码也能锁定该对象，从而导致死锁。</span><span class="sxs-lookup"><span data-stu-id="37dbc-151">If the type you take a lock on is public, code other than your own can take locks on it, leading to deadlocks.</span></span> <span data-ttu-id="37dbc-152">有关其他问题，请参阅[可靠性最佳做法](../../framework/performance/reliability-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="37dbc-152">For additional issues, see [Reliability Best Practices](../../framework/performance/reliability-best-practices.md).</span></span>  
  
- <span data-ttu-id="37dbc-153">锁定实例时要谨慎，例如，C# 中的 `lock(this)` 或 Visual Basic 中的 `SyncLock(Me)`。</span><span class="sxs-lookup"><span data-stu-id="37dbc-153">Use caution when locking on instances, for example `lock(this)` in C# or `SyncLock(Me)` in Visual Basic.</span></span> <span data-ttu-id="37dbc-154">如果应用程序中不属于该类型的其他代码锁定了该对象，则会发生死锁。</span><span class="sxs-lookup"><span data-stu-id="37dbc-154">If other code in your application, external to the type, takes a lock on the object, deadlocks could occur.</span></span>  
  
- <span data-ttu-id="37dbc-155">请务必确保已进入监视器的线程始终离开该监视器，即使线程在监视器中时发生异常也是如此。</span><span class="sxs-lookup"><span data-stu-id="37dbc-155">Do ensure that a thread that has entered a monitor always leaves that monitor, even if an exception occurs while the thread is in the monitor.</span></span> <span data-ttu-id="37dbc-156">C# 的 [lock](../../csharp/language-reference/keywords/lock-statement.md) 语句和 Visual Basic 的 [SyncLock](../../visual-basic/language-reference/statements/synclock-statement.md) 语句可自动提供此行为，同时使用 **finally** 块来确保调用 <xref:System.Threading.Monitor.Exit%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="37dbc-156">The C# [lock](../../csharp/language-reference/keywords/lock-statement.md) statement and the Visual Basic [SyncLock](../../visual-basic/language-reference/statements/synclock-statement.md) statement provide this behavior automatically, employing a **finally** block to ensure that <xref:System.Threading.Monitor.Exit%2A?displayProperty=nameWithType> is called.</span></span> <span data-ttu-id="37dbc-157">如果无法确保调用 **Exit** ，请考虑将设计更改为使用 **Mutex** 。</span><span class="sxs-lookup"><span data-stu-id="37dbc-157">If you cannot ensure that **Exit** will be called, consider changing your design to use **Mutex**.</span></span> <span data-ttu-id="37dbc-158">Mutex 在当前拥有它的线程终止后会自动释放。</span><span class="sxs-lookup"><span data-stu-id="37dbc-158">A mutex is automatically released when the thread that currently owns it terminates.</span></span>  
  
- <span data-ttu-id="37dbc-159">请务必针对需要不同资源的任务使用多线程，避免向单个资源指定多个线程。</span><span class="sxs-lookup"><span data-stu-id="37dbc-159">Do use multiple threads for tasks that require different resources, and avoid assigning multiple threads to a single resource.</span></span> <span data-ttu-id="37dbc-160">例如，任何涉及 I/O 的任务都会从其拥有自己的线程这一点得到好处，因为此线程在 I/O 操作期间将阻止，从而允许其他线程执行。</span><span class="sxs-lookup"><span data-stu-id="37dbc-160">For example, any task involving I/O benefits from having its own thread, because that thread will block during I/O operations and thus allow other threads to execute.</span></span> <span data-ttu-id="37dbc-161">用户输入是另一种可从专用线程获益的资源。</span><span class="sxs-lookup"><span data-stu-id="37dbc-161">User input is another resource that benefits from a dedicated thread.</span></span> <span data-ttu-id="37dbc-162">在单处理器计算机上，涉及大量计算的任务可与用户输入和涉及 I/O 的任务并存，但多个计算量大的任务将相互竞争。</span><span class="sxs-lookup"><span data-stu-id="37dbc-162">On a single-processor computer, a task that involves intensive computation coexists with user input and with tasks that involve I/O, but multiple computation-intensive tasks contend with each other.</span></span>  
  
- <span data-ttu-id="37dbc-163">对于简单的状态更改，请考虑使用 <xref:System.Threading.Interlocked> 类的方法，而不是 `lock` 语句（Visual Basic 中的 `SyncLock`）。</span><span class="sxs-lookup"><span data-stu-id="37dbc-163">Consider using methods of the <xref:System.Threading.Interlocked> class for simple state changes, instead of using the `lock` statement (`SyncLock` in Visual Basic).</span></span> <span data-ttu-id="37dbc-164">虽然 `lock` 语句是实用的通用工具，但 <xref:System.Threading.Interlocked> 类提升了更新（必须是原子操作）的性能。</span><span class="sxs-lookup"><span data-stu-id="37dbc-164">The `lock` statement is a good general-purpose tool, but the <xref:System.Threading.Interlocked> class provides better performance for updates that must be atomic.</span></span> <span data-ttu-id="37dbc-165">如果不存在争用，它会在内部执行一个锁定前缀。</span><span class="sxs-lookup"><span data-stu-id="37dbc-165">Internally, it executes a single lock prefix if there is no contention.</span></span> <span data-ttu-id="37dbc-166">查看代码时，请注意类似于以下示例所示的代码。</span><span class="sxs-lookup"><span data-stu-id="37dbc-166">In code reviews, watch for code like that shown in the following examples.</span></span> <span data-ttu-id="37dbc-167">在第一个示例中，状态变量是递增的：</span><span class="sxs-lookup"><span data-stu-id="37dbc-167">In the first example, a state variable is incremented:</span></span>  
  
    ```vb  
    SyncLock lockObject  
        myField += 1  
    End SyncLock  
    ```  
  
    ```csharp  
    lock(lockObject)
    {  
        myField++;  
    }  
    ```  
  
     <span data-ttu-id="37dbc-168">若要提升性能，可以使用 <xref:System.Threading.Interlocked.Increment%2A> 方法代替 `lock` 语句，如下所示：</span><span class="sxs-lookup"><span data-stu-id="37dbc-168">You can improve performance by using the <xref:System.Threading.Interlocked.Increment%2A> method instead of the `lock` statement, as follows:</span></span>  
  
    ```vb  
    System.Threading.Interlocked.Increment(myField)  
    ```  
  
    ```csharp  
    System.Threading.Interlocked.Increment(myField);  
    ```  
  
    > [!NOTE]
    > <span data-ttu-id="37dbc-169">为大于 1 的原子增量使用 <xref:System.Threading.Interlocked.Add%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="37dbc-169">Use the <xref:System.Threading.Interlocked.Add%2A> method for atomic increments larger than 1.</span></span>  
  
     <span data-ttu-id="37dbc-170">在第二个示例中，仅当引用类型变量为空引用（在 Visual Basic 中为 `Nothing`）时才会将其更新。</span><span class="sxs-lookup"><span data-stu-id="37dbc-170">In the second example, a reference type variable is updated only if it is a null reference (`Nothing` in Visual Basic).</span></span>  
  
    ```vb  
    If x Is Nothing Then  
        SyncLock lockObject  
            If x Is Nothing Then  
                x = y  
            End If  
        End SyncLock  
    End If  
    ```  
  
    ```csharp  
    if (x == null)  
    {  
        lock (lockObject)  
        {  
            x ??= y;
        }  
    }  
    ```  
  
     <span data-ttu-id="37dbc-171">可以改用 <xref:System.Threading.Interlocked.CompareExchange%2A> 方法提升性能，如下所示：</span><span class="sxs-lookup"><span data-stu-id="37dbc-171">Performance can be improved by using the <xref:System.Threading.Interlocked.CompareExchange%2A> method instead, as follows:</span></span>  
  
    ```vb  
    System.Threading.Interlocked.CompareExchange(x, y, Nothing)  
    ```  
  
    ```csharp  
    System.Threading.Interlocked.CompareExchange(ref x, y, null);  
    ```  
  
    > [!NOTE]
    > <span data-ttu-id="37dbc-172"><xref:System.Threading.Interlocked.CompareExchange%60%601%28%60%600%40%2C%60%600%2C%60%600%29> 方法重载为引用类型提供类型安全的替代项。</span><span class="sxs-lookup"><span data-stu-id="37dbc-172">The <xref:System.Threading.Interlocked.CompareExchange%60%601%28%60%600%40%2C%60%600%2C%60%600%29> method overload provides a type-safe alternative for reference types.</span></span>
  
## <a name="recommendations-for-class-libraries"></a><span data-ttu-id="37dbc-173">类库相关建议</span><span class="sxs-lookup"><span data-stu-id="37dbc-173">Recommendations for class libraries</span></span>  
 <span data-ttu-id="37dbc-174">为多线程处理设计类库时，请考虑以下准则：</span><span class="sxs-lookup"><span data-stu-id="37dbc-174">Consider the following guidelines when designing class libraries for multithreading:</span></span>  
  
- <span data-ttu-id="37dbc-175">如果可能，请避免同步需求。</span><span class="sxs-lookup"><span data-stu-id="37dbc-175">Avoid the need for synchronization, if possible.</span></span> <span data-ttu-id="37dbc-176">对于大量使用的代码更应如此。</span><span class="sxs-lookup"><span data-stu-id="37dbc-176">This is especially true for heavily used code.</span></span> <span data-ttu-id="37dbc-177">例如，可以将一个算法调整为容忍争用情况，而不是完全消除争用情况。</span><span class="sxs-lookup"><span data-stu-id="37dbc-177">For example, an algorithm might be adjusted to tolerate a race condition rather than eliminate it.</span></span> <span data-ttu-id="37dbc-178">不必要的同步会降低性能，并且可能导致出现死锁和争用情况。</span><span class="sxs-lookup"><span data-stu-id="37dbc-178">Unnecessary synchronization decreases performance and creates the possibility of deadlocks and race conditions.</span></span>  
  
- <span data-ttu-id="37dbc-179">默认情况下使静态数据（在 Visual Basic 中为 `Shared`）是线程安全的。</span><span class="sxs-lookup"><span data-stu-id="37dbc-179">Make static data (`Shared` in Visual Basic) thread safe by default.</span></span>  
  
- <span data-ttu-id="37dbc-180">默认情况下不要使实例数据是线程安全的。</span><span class="sxs-lookup"><span data-stu-id="37dbc-180">Do not make instance data thread safe by default.</span></span> <span data-ttu-id="37dbc-181">通过添加锁来创建线程安全代码会降低性能、加剧锁争用情况，并且可能导致出现死锁。</span><span class="sxs-lookup"><span data-stu-id="37dbc-181">Adding locks to create thread-safe code decreases performance, increases lock contention, and creates the possibility for deadlocks to occur.</span></span> <span data-ttu-id="37dbc-182">在常见应用程序模型中，一次只有一个线程执行用户代码，从而最大限度降低线程安全性的需求。</span><span class="sxs-lookup"><span data-stu-id="37dbc-182">In common application models, only one thread at a time executes user code, which minimizes the need for thread safety.</span></span> <span data-ttu-id="37dbc-183">出于此原因，.NET 类库在默认情况下不是线程安全的类库。</span><span class="sxs-lookup"><span data-stu-id="37dbc-183">For this reason, the .NET class libraries are not thread safe by default.</span></span>  
  
- <span data-ttu-id="37dbc-184">避免提供可更改静态状态的静态方法。</span><span class="sxs-lookup"><span data-stu-id="37dbc-184">Avoid providing static methods that alter static state.</span></span> <span data-ttu-id="37dbc-185">在常见服务器方案中，静态状态可在各个请求之间共享，这意味着多个线程可同时执行该代码。</span><span class="sxs-lookup"><span data-stu-id="37dbc-185">In common server scenarios, static state is shared across requests, which means multiple threads can execute that code at the same time.</span></span> <span data-ttu-id="37dbc-186">这可能导致线程出现 bug。</span><span class="sxs-lookup"><span data-stu-id="37dbc-186">This opens up the possibility of threading bugs.</span></span> <span data-ttu-id="37dbc-187">请考虑使用一种设计模式，将数据封装到在各请求之间不共享的实例中。</span><span class="sxs-lookup"><span data-stu-id="37dbc-187">Consider using a design pattern that encapsulates data into instances that are not shared across requests.</span></span> <span data-ttu-id="37dbc-188">此外，如果同步静态数据，更改状态的静态方法间的调用可导致死锁或冗余同步，进而降低性能。</span><span class="sxs-lookup"><span data-stu-id="37dbc-188">Furthermore, if static data are synchronized, calls between static methods that alter state can result in deadlocks or redundant synchronization, adversely affecting performance.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="37dbc-189">请参阅</span><span class="sxs-lookup"><span data-stu-id="37dbc-189">See also</span></span>

- [<span data-ttu-id="37dbc-190">线程处理</span><span class="sxs-lookup"><span data-stu-id="37dbc-190">Threading</span></span>](index.md)
- [<span data-ttu-id="37dbc-191">线程与线程处理</span><span class="sxs-lookup"><span data-stu-id="37dbc-191">Threads and Threading</span></span>](threads-and-threading.md)
