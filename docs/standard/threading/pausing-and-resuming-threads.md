---
title: 暂停和中断线程
description: 了解如何在 .NET 中暂停和中断线程。 了解如何使用方法（如 Thread.Sleep 和 Thread.Interrupt）和异常（如 ThreadInterruptedException）。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- interrupting threads
- threading [.NET], pausing
- pausing threads
ms.assetid: 9fce4859-a19d-4506-b082-7dd0792688ca
ms.openlocfilehash: 07fe374acb3d2a3de3a1b51861feb5f8551ecc2e
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188960"
---
# <a name="pausing-and-interrupting-threads"></a><span data-ttu-id="ee5ff-104">暂停和中断线程</span><span class="sxs-lookup"><span data-stu-id="ee5ff-104">Pausing and interrupting threads</span></span>

<span data-ttu-id="ee5ff-105">同步线程活动最常见的方法是阻止和释放线程，或者锁定对象或代码区域。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-105">The most common ways to synchronize the activities of threads are to block and release threads, or to lock objects or regions of code.</span></span> <span data-ttu-id="ee5ff-106">有关这些锁定和阻止机制的详细信息，请参阅[同步基元概述](overview-of-synchronization-primitives.md)。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-106">For more information on these locking and blocking mechanisms, see [Overview of Synchronization Primitives](overview-of-synchronization-primitives.md).</span></span>  
  
 <span data-ttu-id="ee5ff-107">也可使线程将自身置于睡眠状态。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-107">You can also have threads put themselves to sleep.</span></span> <span data-ttu-id="ee5ff-108">当线程被阻止或处于休眠状态时，可以使用 <xref:System.Threading.ThreadInterruptedException> 使它们脱离等待状态。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-108">When threads are blocked or sleeping, you can use a <xref:System.Threading.ThreadInterruptedException> to break them out of their wait states.</span></span>  
  
## <a name="the-threadsleep-method"></a><span data-ttu-id="ee5ff-109">Thread.Sleep 方法</span><span class="sxs-lookup"><span data-stu-id="ee5ff-109">The Thread.Sleep method</span></span>

 <span data-ttu-id="ee5ff-110">调用 <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType> 方法会导致当前线程立即受阻止，时间为传递到方法的毫秒数或时间间隔，结果是将时间片的剩余部分生成给其他线程。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-110">Calling the <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType> method causes the current thread to immediately block for the number of milliseconds or the time interval you pass to the method, and yields the remainder of its time slice to another thread.</span></span> <span data-ttu-id="ee5ff-111">受阻时间过后，休眠线程继续执行。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-111">Once that interval elapses, the sleeping thread resumes execution.</span></span>  
  
 <span data-ttu-id="ee5ff-112">一个线程不能调用另一线程上的 <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-112">One thread cannot call <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType> on another thread.</span></span>  <span data-ttu-id="ee5ff-113"><xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType> 是一种始终让当前线程进入睡眠状态的静态方法。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-113"><xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType> is a static method that always causes the current thread to sleep.</span></span>  
  
 <span data-ttu-id="ee5ff-114">调用 <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType>（值为 <xref:System.Threading.Timeout.Infinite?displayProperty=nameWithType>）可以让线程进入睡眠状态，直到另一个对睡眠线程调用 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 方法的线程中断它，或直到 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 方法调用终止它。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-114">Calling <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType> with a value of <xref:System.Threading.Timeout.Infinite?displayProperty=nameWithType> causes a thread to sleep until it is interrupted by another thread that calls the  <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> method on the sleeping thread, or until it is terminated by a call to its <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> method.</span></span>  <span data-ttu-id="ee5ff-115">下面的示例阐释了这两种中断休眠线程的方法。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-115">The following example illustrates both methods of interrupting a sleeping thread.</span></span>  
  
 [!code-csharp[Conceptual.Threading.Resuming#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.Threading.Resuming/cs/Sleep1.cs#1)]
 [!code-vb[Conceptual.Threading.Resuming#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.Threading.Resuming/vb/Sleep1.vb#1)]  
  
## <a name="interrupting-threads"></a><span data-ttu-id="ee5ff-116">中断线程</span><span class="sxs-lookup"><span data-stu-id="ee5ff-116">Interrupting threads</span></span>

 <span data-ttu-id="ee5ff-117">可以中断正在等待的线程，具体操作是对受阻止的线程调用 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 方法，从而抛出 <xref:System.Threading.ThreadInterruptedException>，以中断对线程执行的阻止调用。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-117">You can interrupt a waiting thread by calling the <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> method on the blocked thread to throw a <xref:System.Threading.ThreadInterruptedException>, which breaks the thread out of the blocking call.</span></span> <span data-ttu-id="ee5ff-118">线程应该捕获 <xref:System.Threading.ThreadInterruptedException> 并执行任何适于继续工作的操作。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-118">The thread should catch the <xref:System.Threading.ThreadInterruptedException> and do whatever is appropriate to continue working.</span></span> <span data-ttu-id="ee5ff-119">如果线程忽略该异常，则运行时捕获异常，并停止该线程。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-119">If the thread ignores the exception, the runtime catches the exception and stops the thread.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="ee5ff-120">如果在调用 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 时，未阻止目标线程，则线程在被阻止前将不会中断。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-120">If the target thread is not blocked when <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> is called, the thread is not interrupted until it blocks.</span></span> <span data-ttu-id="ee5ff-121">如果线程永远不被阻止，则它可在不被中断的情况下完成。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-121">If the thread never blocks, it could complete without ever being interrupted.</span></span>  
  
 <span data-ttu-id="ee5ff-122">如果等待是托管的等待，则 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 和 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 都会立即唤醒线程。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-122">If a wait is a managed wait, then <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> and <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> both wake the thread immediately.</span></span> <span data-ttu-id="ee5ff-123">如果等待是非托管等待（例如，调用 Win32 [WaitForSingleObject](/windows/desktop/api/synchapi/nf-synchapi-waitforsingleobject) 函数的平台调用），<xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 和 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 都不能控制线程，直到它返回到或调用托管代码。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-123">If a wait is an unmanaged wait (for example, a platform invoke call to the Win32 [WaitForSingleObject](/windows/desktop/api/synchapi/nf-synchapi-waitforsingleobject) function), neither <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> nor <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> can take control of the thread until it returns to or calls into managed code.</span></span> <span data-ttu-id="ee5ff-124">在托管代码中，该行为如下：</span><span class="sxs-lookup"><span data-stu-id="ee5ff-124">In managed code, the behavior is as follows:</span></span>  
  
- <span data-ttu-id="ee5ff-125"><xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 将线程从其可能处于的任何等待中唤醒，并导致在目标线程中引发 <xref:System.Threading.ThreadInterruptedException>。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-125"><xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> wakes a thread out of any wait it might be in and causes a <xref:System.Threading.ThreadInterruptedException> to be thrown in the destination thread.</span></span>  
  
- <span data-ttu-id="ee5ff-126"><xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 将线程从可能处于的任何等待中唤醒，并导致 <xref:System.Threading.ThreadAbortException> 在线程中抛出。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-126"><xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> wakes a thread out of any wait it might be in and causes a <xref:System.Threading.ThreadAbortException> to be thrown on the thread.</span></span> <span data-ttu-id="ee5ff-127">有关详细信息，请参阅[销毁线程](destroying-threads.md)。</span><span class="sxs-lookup"><span data-stu-id="ee5ff-127">For details, see [Destroying Threads](destroying-threads.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ee5ff-128">请参阅</span><span class="sxs-lookup"><span data-stu-id="ee5ff-128">See also</span></span>

- <xref:System.Threading.Thread>
- <xref:System.Threading.ThreadInterruptedException>
- <xref:System.Threading.ThreadAbortException>
- [<span data-ttu-id="ee5ff-129">线程处理</span><span class="sxs-lookup"><span data-stu-id="ee5ff-129">Threading</span></span>](index.md)
- [<span data-ttu-id="ee5ff-130">使用线程和线程处理</span><span class="sxs-lookup"><span data-stu-id="ee5ff-130">Using Threads and Threading</span></span>](using-threads-and-threading.md)
- [<span data-ttu-id="ee5ff-131">同步基元概述</span><span class="sxs-lookup"><span data-stu-id="ee5ff-131">Overview of Synchronization Primitives</span></span>](overview-of-synchronization-primitives.md)
