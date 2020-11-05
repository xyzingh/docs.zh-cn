---
title: 与其他异步模式和类型互操作
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- asynchronous design patterns, .NET
- TAP, .NET support for
- Task-based Asynchronous Pattern, .NET support for
- .NET, asynchronous design patterns
ms.assetid: f120a5d9-933b-4d1d-acb6-f034a57c3749
ms.openlocfilehash: 5ad49c70aaa69d8a4f830851b80b6a4839388b0f
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888745"
---
# <a name="interop-with-other-asynchronous-patterns-and-types"></a><span data-ttu-id="e9275-102">与其他异步模式和类型互操作</span><span class="sxs-lookup"><span data-stu-id="e9275-102">Interop with Other Asynchronous Patterns and Types</span></span>

<span data-ttu-id="e9275-103">.NET 中异步模式的简短历史记录：</span><span class="sxs-lookup"><span data-stu-id="e9275-103">A brief history of asynchronous patterns in .NET:</span></span>

- <span data-ttu-id="e9275-104">.NET Framework 1.0 引进了 <xref:System.IAsyncResult> 模式，也称为[异步编程模型 (APM)](asynchronous-programming-model-apm.md) 或 `Begin/End` 模式。</span><span class="sxs-lookup"><span data-stu-id="e9275-104">.NET Framework 1.0 introduced the <xref:System.IAsyncResult> pattern, otherwise known as the [Asynchronous Programming Model (APM)](asynchronous-programming-model-apm.md), or the `Begin/End` pattern.</span></span>
- <span data-ttu-id="e9275-105">.NET Framework 2.0 增加了[基于事件的异步模式 (EAP)](event-based-asynchronous-pattern-eap.md)。</span><span class="sxs-lookup"><span data-stu-id="e9275-105">.NET Framework 2.0 added the [Event-based Asynchronous Pattern (EAP)](event-based-asynchronous-pattern-eap.md).</span></span>
- <span data-ttu-id="e9275-106">.NET Framework 4 引进了[基于任务的异步模式 (TAP)](task-based-asynchronous-pattern-tap.md)，它取代了 APM 和 EAP，并能够轻松构建从早期模式中迁移的例程。</span><span class="sxs-lookup"><span data-stu-id="e9275-106">.NET Framework 4 introduced the [Task-based Asynchronous Pattern (TAP)](task-based-asynchronous-pattern-tap.md), which supersedes both APM and EAP and provides the ability to easily build migration routines from the earlier patterns.</span></span>
  
## <a name="tasks-and-the-asynchronous-programming-model-apm"></a><span data-ttu-id="e9275-107">任务和异步编程模型 (APM)</span><span class="sxs-lookup"><span data-stu-id="e9275-107">Tasks and the Asynchronous Programming Model (APM)</span></span>

### <a name="from-apm-to-tap"></a><span data-ttu-id="e9275-108">从 APM 到 TAP</span><span class="sxs-lookup"><span data-stu-id="e9275-108">From APM to TAP</span></span>  
 <span data-ttu-id="e9275-109">因为[异步编程模型 (APM)](asynchronous-programming-model-apm.md) 模式的结构合理，而且能够轻松生成包装，将 APM 实现公开为 TAP 实现。</span><span class="sxs-lookup"><span data-stu-id="e9275-109">Because the [Asynchronous Programming Model (APM)](asynchronous-programming-model-apm.md) pattern is structured, it is quite easy to build a wrapper to expose an APM implementation as a TAP implementation.</span></span> <span data-ttu-id="e9275-110">.NET Framework 4 及更高版本包含采用 <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A> 方法重载形式的帮助器例程来实现这种转换。</span><span class="sxs-lookup"><span data-stu-id="e9275-110">.NET Framework 4 and later versions include helper routines in the form of <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A> method overloads to provide this translation.</span></span>  
  
 <span data-ttu-id="e9275-111">请考虑 <xref:System.IO.Stream> 类及其 <xref:System.IO.Stream.BeginRead%2A> 和 <xref:System.IO.Stream.EndRead%2A> 方法，它们代表与同步 <xref:System.IO.Stream.Read%2A> 方法对应的 APM：</span><span class="sxs-lookup"><span data-stu-id="e9275-111">Consider the <xref:System.IO.Stream> class and its <xref:System.IO.Stream.BeginRead%2A> and <xref:System.IO.Stream.EndRead%2A> methods, which represent the APM counterpart to the synchronous <xref:System.IO.Stream.Read%2A> method:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Stream1.cs#1)]
 [!code-vb[Conceptual.AsyncInterop#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/stream1.vb#1)]  
[!code-csharp[Conceptual.AsyncInterop#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Stream1.cs#2)]
[!code-vb[Conceptual.AsyncInterop#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/stream1.vb#2)]  
[!code-csharp[Conceptual.AsyncInterop#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Stream1.cs#3)]
[!code-vb[Conceptual.AsyncInterop#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/stream1.vb#3)]  
  
 <span data-ttu-id="e9275-112">可以使用 <xref:System.Threading.Tasks.TaskFactory%601.FromAsync%2A?displayProperty=nameWithType> 方法来实现此操作的 TAP 包装，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e9275-112">You can use the <xref:System.Threading.Tasks.TaskFactory%601.FromAsync%2A?displayProperty=nameWithType> method to implement a TAP wrapper for this operation as follows:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wrap1.cs#4)]
 [!code-vb[Conceptual.AsyncInterop#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wrap1.vb#4)]  
  
 <span data-ttu-id="e9275-113">此实现类似于以下内容：</span><span class="sxs-lookup"><span data-stu-id="e9275-113">This implementation is similar to the following:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wrap2.cs#5)]
 [!code-vb[Conceptual.AsyncInterop#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wrap2.vb#5)]  
  
### <a name="from-tap-to-apm"></a><span data-ttu-id="e9275-114">从 TAP 到 APM</span><span class="sxs-lookup"><span data-stu-id="e9275-114">From TAP to APM</span></span>  
 <span data-ttu-id="e9275-115">如果现有的基础结构需要 APM 模式，则还需要采用 TAP 实现并在需要 APM 实现的地方使用它。</span><span class="sxs-lookup"><span data-stu-id="e9275-115">If your existing infrastructure expects the APM pattern, you'll also want to take a TAP implementation and use it where an APM implementation is expected.</span></span>  <span data-ttu-id="e9275-116">由于任务可以组合，并且 <xref:System.Threading.Tasks.Task> 类实现 <xref:System.IAsyncResult>，您可以使用一个简单的 helper 函数执行此操作。</span><span class="sxs-lookup"><span data-stu-id="e9275-116">Because tasks can be composed and  the <xref:System.Threading.Tasks.Task> class implements <xref:System.IAsyncResult>, you can use a straightforward helper function to do this.</span></span> <span data-ttu-id="e9275-117">以下代码使用 <xref:System.Threading.Tasks.Task%601> 类的扩展，但可以对非泛型任务使用几乎相同的函数。</span><span class="sxs-lookup"><span data-stu-id="e9275-117">The following code uses an extension of the <xref:System.Threading.Tasks.Task%601> class, but you can use an almost identical function for non-generic tasks.</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM1.cs#6)]
 [!code-vb[Conceptual.AsyncInterop#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM1.vb#6)]  
  
 <span data-ttu-id="e9275-118">现在，请考虑具有以下 TAP 实现的用例：</span><span class="sxs-lookup"><span data-stu-id="e9275-118">Now, consider a case where you have the following TAP implementation:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#7)]
 [!code-vb[Conceptual.AsyncInterop#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#7)]  
  
 <span data-ttu-id="e9275-119">并且想要提供此 APM 实现：</span><span class="sxs-lookup"><span data-stu-id="e9275-119">and you want to provide this APM implementation:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#8)]
 [!code-vb[Conceptual.AsyncInterop#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#8)]  
[!code-csharp[Conceptual.AsyncInterop#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#9)]
[!code-vb[Conceptual.AsyncInterop#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#9)]  
  
 <span data-ttu-id="e9275-120">以下示例演示了一种向 APM 迁移的方法：</span><span class="sxs-lookup"><span data-stu-id="e9275-120">The following example demonstrates one migration to APM:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#10)]
 [!code-vb[Conceptual.AsyncInterop#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#10)]  
  
## <a name="tasks-and-the-event-based-asynchronous-pattern-eap"></a><span data-ttu-id="e9275-121">任务和基于事件的异步模式 (EAP)</span><span class="sxs-lookup"><span data-stu-id="e9275-121">Tasks and the Event-based Asynchronous Pattern (EAP)</span></span>  
 <span data-ttu-id="e9275-122">包装 [基于事件的异步模式 (EAP)](event-based-asynchronous-pattern-eap.md) 实现比包装 APM 模式更为复杂，因为与 APM 模式相比，EAP 模式的变体更多，结构更少。</span><span class="sxs-lookup"><span data-stu-id="e9275-122">Wrapping an [Event-based Asynchronous Pattern (EAP)](event-based-asynchronous-pattern-eap.md) implementation is more involved than wrapping an APM pattern, because the EAP pattern has more variation and less structure than the APM pattern.</span></span>  <span data-ttu-id="e9275-123">为了演示，以下代码包装了 `DownloadStringAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="e9275-123">To demonstrate, the following code wraps the `DownloadStringAsync` method.</span></span>  <span data-ttu-id="e9275-124">`DownloadStringAsync` 接受 URI，在下载时引发 `DownloadProgressChanged` 事件，以报告进度的多个统计信息，并在完成时引发 `DownloadStringCompleted` 事件。</span><span class="sxs-lookup"><span data-stu-id="e9275-124">`DownloadStringAsync` accepts a URI, raises the `DownloadProgressChanged` event while downloading in order to report multiple statistics on progress, and raises the `DownloadStringCompleted` event when it's done.</span></span>  <span data-ttu-id="e9275-125">最终在指定 URI 中返回一个字符串，其中包含页面内容。</span><span class="sxs-lookup"><span data-stu-id="e9275-125">The final result is a string that contains the contents of the page at the specified URI.</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/EAP1.cs#11)]
 [!code-vb[Conceptual.AsyncInterop#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/EAP1.vb#11)]  
  
## <a name="tasks-and-wait-handles"></a><span data-ttu-id="e9275-126">任务和等待句柄</span><span class="sxs-lookup"><span data-stu-id="e9275-126">Tasks and Wait Handles</span></span>  
  
### <a name="from-wait-handles-to-tap"></a><span data-ttu-id="e9275-127">从等待句柄到 TAP</span><span class="sxs-lookup"><span data-stu-id="e9275-127">From Wait Handles to TAP</span></span>  
 <span data-ttu-id="e9275-128">虽然等待句柄不能实现异步模式，但高级开发人员可以在设置等待句柄时使用 <xref:System.Threading.WaitHandle> 类和 <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A?displayProperty=nameWithType> 方法实现异步通知。</span><span class="sxs-lookup"><span data-stu-id="e9275-128">Although wait handles don't implement an asynchronous pattern, advanced developers may use the <xref:System.Threading.WaitHandle> class and the <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A?displayProperty=nameWithType> method for asynchronous notifications when a wait handle is set.</span></span>  <span data-ttu-id="e9275-129">可以包装 <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A> 方法以在等待句柄中启用针对任何同步等待的基于任务的替代方法：</span><span class="sxs-lookup"><span data-stu-id="e9275-129">You can wrap the <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A> method to enable a task-based alternative to any synchronous wait on a wait handle:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#12](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wait1.cs#12)]
 [!code-vb[Conceptual.AsyncInterop#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wait1.vb#12)]  
  
 <span data-ttu-id="e9275-130">使用此方法，可以在异步方法中使用现有 <xref:System.Threading.WaitHandle> 实现。</span><span class="sxs-lookup"><span data-stu-id="e9275-130">With this method, you can use existing <xref:System.Threading.WaitHandle> implementations in asynchronous methods.</span></span>  <span data-ttu-id="e9275-131">例如，若要限制在任何特定时间执行的异步操作数，可以利用信号灯（<xref:System.Threading.SemaphoreSlim?displayProperty=nameWithType> 对象）。</span><span class="sxs-lookup"><span data-stu-id="e9275-131">For example, if you want to throttle the number of asynchronous operations that are executing at any particular time, you can utilize a semaphore (a <xref:System.Threading.SemaphoreSlim?displayProperty=nameWithType> object).</span></span>  <span data-ttu-id="e9275-132">可以将并发运行的操作数目限制到 N，方法为：初始化到 N 的信号量的数目、在想要执行操作时等待信号量，并在完成操作时释放信号量 ：</span><span class="sxs-lookup"><span data-stu-id="e9275-132">You can throttle to *N* the number of operations that run concurrently by initializing the semaphore's count to *N* , waiting on the semaphore any time you want to perform an operation, and releasing the semaphore when you're done with an operation:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Semaphore1.cs#13)]
 [!code-vb[Conceptual.AsyncInterop#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Semaphore1.vb#13)]  
  
 <span data-ttu-id="e9275-133">还可以构建不依赖等待句柄就完全可以处理任务的异步信号量。</span><span class="sxs-lookup"><span data-stu-id="e9275-133">You can also build an asynchronous semaphore that does not rely on wait handles and instead works completely with tasks.</span></span> <span data-ttu-id="e9275-134">若要执行此操作，可以使用 [使用基于任务的异步模式](consuming-the-task-based-asynchronous-pattern.md) 中所述的用于在 <xref:System.Threading.Tasks.Task>。</span><span class="sxs-lookup"><span data-stu-id="e9275-134">To do this, you can use techniques such as those discussed in [Consuming the Task-based Asynchronous Pattern](consuming-the-task-based-asynchronous-pattern.md) for building data structures on top of <xref:System.Threading.Tasks.Task>.</span></span>  
  
### <a name="from-tap-to-wait-handles"></a><span data-ttu-id="e9275-135">从 TAP 到等待句柄</span><span class="sxs-lookup"><span data-stu-id="e9275-135">From TAP to Wait Handles</span></span>  
 <span data-ttu-id="e9275-136">正如前面所述， <xref:System.Threading.Tasks.Task> 类实现 <xref:System.IAsyncResult>，且该实现公开 <xref:System.Threading.Tasks.Task.System%23IAsyncResult%23AsyncWaitHandle%2A> 属性，该属性会返回在 <xref:System.Threading.Tasks.Task> 完成时设置的等待句柄。</span><span class="sxs-lookup"><span data-stu-id="e9275-136">As previously mentioned, the <xref:System.Threading.Tasks.Task> class implements <xref:System.IAsyncResult>, and that implementation exposes an <xref:System.Threading.Tasks.Task.System%23IAsyncResult%23AsyncWaitHandle%2A> property that returns a wait handle that will be set when the <xref:System.Threading.Tasks.Task> completes.</span></span>  <span data-ttu-id="e9275-137">可以获得 <xref:System.Threading.WaitHandle> 的 <xref:System.Threading.Tasks.Task> ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e9275-137">You can get a <xref:System.Threading.WaitHandle> for a <xref:System.Threading.Tasks.Task> as follows:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#14](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wait1.cs#14)]
 [!code-vb[Conceptual.AsyncInterop#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wait1.vb#14)]  
  
## <a name="see-also"></a><span data-ttu-id="e9275-138">请参阅</span><span class="sxs-lookup"><span data-stu-id="e9275-138">See also</span></span>

- [<span data-ttu-id="e9275-139">基于任务的异步模式 (TAP)</span><span class="sxs-lookup"><span data-stu-id="e9275-139">Task-based Asynchronous Pattern (TAP)</span></span>](task-based-asynchronous-pattern-tap.md)
- [<span data-ttu-id="e9275-140">实现基于任务的异步模式</span><span class="sxs-lookup"><span data-stu-id="e9275-140">Implementing the Task-based Asynchronous Pattern</span></span>](implementing-the-task-based-asynchronous-pattern.md)
- [<span data-ttu-id="e9275-141">使用基于任务的异步模式</span><span class="sxs-lookup"><span data-stu-id="e9275-141">Consuming the Task-based Asynchronous Pattern</span></span>](consuming-the-task-based-asynchronous-pattern.md)
