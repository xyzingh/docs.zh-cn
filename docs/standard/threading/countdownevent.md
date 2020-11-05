---
title: CountdownEvent
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- synchronization primitives, CountdownEvent
ms.assetid: eec3812a-e20f-4ecd-bfef-6921d508b708
ms.openlocfilehash: de9b49de86eb6489181afc8d8f5fbb1222bf877d
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188401"
---
# <a name="countdownevent"></a><span data-ttu-id="77303-102">CountdownEvent</span><span class="sxs-lookup"><span data-stu-id="77303-102">CountdownEvent</span></span>

<span data-ttu-id="77303-103"><xref:System.Threading.CountdownEvent?displayProperty=nameWithType> 是在收到信号特定次数后取消阻止等待线程的同步基元。</span><span class="sxs-lookup"><span data-stu-id="77303-103"><xref:System.Threading.CountdownEvent?displayProperty=nameWithType> is a synchronization primitive that unblocks its waiting threads after it has been signaled a certain number of times.</span></span> <span data-ttu-id="77303-104"><xref:System.Threading.CountdownEvent> 适用于以下情况：不得不先使用 <xref:System.Threading.ManualResetEvent> 或 <xref:System.Threading.ManualResetEventSlim> 并手动递减变量，然后再向事件发出信号。</span><span class="sxs-lookup"><span data-stu-id="77303-104"><xref:System.Threading.CountdownEvent> is designed for scenarios in which you would otherwise have to use a <xref:System.Threading.ManualResetEvent> or <xref:System.Threading.ManualResetEventSlim> and manually decrement a variable before signaling the event.</span></span> <span data-ttu-id="77303-105">例如，在分支/联接方案中，可以只创建信号计数为 5 的 <xref:System.Threading.CountdownEvent>，然后在线程池中启动五个工作项，并让每个工作项在完成时调用 <xref:System.Threading.CountdownEvent.Signal%2A>。</span><span class="sxs-lookup"><span data-stu-id="77303-105">For example, in a fork/join scenario, you can just create a <xref:System.Threading.CountdownEvent> that has a signal count of 5, and then start five work items on the thread pool and have each work item call <xref:System.Threading.CountdownEvent.Signal%2A> when it completes.</span></span> <span data-ttu-id="77303-106">每次调用 <xref:System.Threading.CountdownEvent.Signal%2A> 都会让信号计数递减 1。</span><span class="sxs-lookup"><span data-stu-id="77303-106">Each call to <xref:System.Threading.CountdownEvent.Signal%2A> decrements the signal count by 1.</span></span> <span data-ttu-id="77303-107">在主线程上，<xref:System.Threading.CountdownEvent.Wait%2A> 调用一直阻止到信号计数为零。</span><span class="sxs-lookup"><span data-stu-id="77303-107">On the main thread, the call to <xref:System.Threading.CountdownEvent.Wait%2A> will block until the signal count is zero.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="77303-108">对于不需要与旧 .NET Framework 同步 API 交互的代码，请考虑使用 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 对象或 <xref:System.Threading.Tasks.Parallel.Invoke%2A> 方法，以更轻松地表示分支-联接并行度。</span><span class="sxs-lookup"><span data-stu-id="77303-108">For code that does not have to interact with legacy .NET Framework synchronization APIs, consider using <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> objects or the <xref:System.Threading.Tasks.Parallel.Invoke%2A> method for an even easier approach to expressing fork-join parallelism.</span></span>  
  
 <span data-ttu-id="77303-109"><xref:System.Threading.CountdownEvent> 还有以下功能：</span><span class="sxs-lookup"><span data-stu-id="77303-109"><xref:System.Threading.CountdownEvent> has these additional features:</span></span>  
  
- <span data-ttu-id="77303-110">可以使用取消令牌取消等待操作。</span><span class="sxs-lookup"><span data-stu-id="77303-110">The wait operation can be canceled by using cancellation tokens.</span></span>  
  
- <span data-ttu-id="77303-111">创建实例后，可以递增信号计数。</span><span class="sxs-lookup"><span data-stu-id="77303-111">Its signal count can be incremented after the instance is created.</span></span>  
  
- <span data-ttu-id="77303-112">在 <xref:System.Threading.CountdownEvent.Reset%2A> 方法调用返回 <xref:System.Threading.CountdownEvent.Wait%2A> 后，可以重用实例。</span><span class="sxs-lookup"><span data-stu-id="77303-112">Instances can be reused after <xref:System.Threading.CountdownEvent.Wait%2A> has returned by calling the <xref:System.Threading.CountdownEvent.Reset%2A> method.</span></span>  
  
- <span data-ttu-id="77303-113">实例公开 <xref:System.Threading.WaitHandle>，以与其他 .NET 同步 API（如 <xref:System.Threading.WaitHandle.WaitAll%2A>）集成。</span><span class="sxs-lookup"><span data-stu-id="77303-113">Instances expose a <xref:System.Threading.WaitHandle> for integration with other .NET synchronization APIs, such as <xref:System.Threading.WaitHandle.WaitAll%2A>.</span></span>  
  
## <a name="basic-usage"></a><span data-ttu-id="77303-114">基本用法</span><span class="sxs-lookup"><span data-stu-id="77303-114">Basic Usage</span></span>  
 <span data-ttu-id="77303-115">下面的示例展示了如何将 <xref:System.Threading.CountdownEvent> 与 <xref:System.Threading.ThreadPool> 工作项结合使用。</span><span class="sxs-lookup"><span data-stu-id="77303-115">The following example demonstrates how to use a <xref:System.Threading.CountdownEvent> with <xref:System.Threading.ThreadPool> work items.</span></span>  
  
 [!code-csharp[CDS_CountdownEvent#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_countdownevent/cs/countdownevent.cs#01)]
 [!code-vb[CDS_CountdownEvent#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_countdownevent/vb/module1.vb#01)]  
  
## <a name="countdownevent-with-cancellation"></a><span data-ttu-id="77303-116">结合使用 CountdownEvent 和取消令牌</span><span class="sxs-lookup"><span data-stu-id="77303-116">CountdownEvent With Cancellation</span></span>  
 <span data-ttu-id="77303-117">下面的示例展示了如何使用取消令牌对 <xref:System.Threading.CountdownEvent> 取消等待操作。</span><span class="sxs-lookup"><span data-stu-id="77303-117">The following example shows how to cancel the wait operation on <xref:System.Threading.CountdownEvent> by using a cancellation token.</span></span> <span data-ttu-id="77303-118">基本模式遵循 .NET Framework 4 中引入的统一取消模型。</span><span class="sxs-lookup"><span data-stu-id="77303-118">The basic pattern follows the model for unified cancellation, which was introduced in .NET Framework 4.</span></span> <span data-ttu-id="77303-119">有关详细信息，请参阅[托管线程中的取消](cancellation-in-managed-threads.md)。</span><span class="sxs-lookup"><span data-stu-id="77303-119">For more information, see [Cancellation in Managed Threads](cancellation-in-managed-threads.md).</span></span>  
  
 [!code-csharp[CDS_CountdownEvent#02](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_countdownevent/cs/countdownevent.cs#02)]
 [!code-vb[CDS_CountdownEvent#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_countdownevent/vb/canceleventwait.vb#02)]  
  
 <span data-ttu-id="77303-120">请注意，等待操作不会取消正在向它发出信号的线程。</span><span class="sxs-lookup"><span data-stu-id="77303-120">Note that the wait operation does not cancel the threads that are signaling it.</span></span> <span data-ttu-id="77303-121">通常情况下，取消应用于逻辑操作，可以包括事件等待操作，以及此等待操作要同步的所有工作项。</span><span class="sxs-lookup"><span data-stu-id="77303-121">Typically, cancellation is applied to a logical operation, and that can include waiting on the event as well as all the work items that the wait is synchronizing.</span></span> <span data-ttu-id="77303-122">在此示例中，每个工作项都传递有相同的取消令牌副本，以便能够响应取消请求。</span><span class="sxs-lookup"><span data-stu-id="77303-122">In this example, each work item is passed a copy of the same cancellation token so that it can respond to the cancellation request.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="77303-123">另请参阅</span><span class="sxs-lookup"><span data-stu-id="77303-123">See also</span></span>

- <xref:System.Threading.Semaphore?displayProperty=nameWithType>
