---
title: TPL 和传统 .NET 异步编程
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, with other asynchronous models
ms.assetid: e7b31170-a156-433f-9f26-b1fc7cd1776f
ms.openlocfilehash: 498bde82d05259bdc561d08819d024090b0417f0
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92688023"
---
# <a name="tpl-and-traditional-net-asynchronous-programming"></a><span data-ttu-id="507c2-102">TPL 和传统 .NET 异步编程</span><span class="sxs-lookup"><span data-stu-id="507c2-102">TPL and traditional .NET asynchronous programming</span></span>

<span data-ttu-id="507c2-103">.NET 提供了以下两种标准模式，用于执行 I/O 密集型和计算密集型异步操作：</span><span class="sxs-lookup"><span data-stu-id="507c2-103">.NET provides the following two standard patterns for performing I/O-bound and compute-bound asynchronous operations:</span></span>  
  
- <span data-ttu-id="507c2-104">异步编程模型 (APM)，在该模式中异步操作由一对 Begin/End 方法表示。</span><span class="sxs-lookup"><span data-stu-id="507c2-104">Asynchronous Programming Model (APM), in which asynchronous operations are represented by a pair of begin/end methods.</span></span> <span data-ttu-id="507c2-105">例如 <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType> 和 <xref:System.IO.Stream.EndRead%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="507c2-105">For example: <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType> and <xref:System.IO.Stream.EndRead%2A?displayProperty=nameWithType>.</span></span>  
  
- <span data-ttu-id="507c2-106">基于事件的异步模式 (EAP)，在该模式中异步操作由名为 `<OperationName>Async` 和 `<OperationName>Completed` 的方法/事件对表示。</span><span class="sxs-lookup"><span data-stu-id="507c2-106">Event-based asynchronous pattern (EAP), in which asynchronous operations are represented by a method/event pair that are named `<OperationName>Async` and `<OperationName>Completed`.</span></span> <span data-ttu-id="507c2-107">例如 <xref:System.Net.WebClient.DownloadStringAsync%2A?displayProperty=nameWithType> 和 <xref:System.Net.WebClient.DownloadStringCompleted?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="507c2-107">For example: <xref:System.Net.WebClient.DownloadStringAsync%2A?displayProperty=nameWithType> and <xref:System.Net.WebClient.DownloadStringCompleted?displayProperty=nameWithType>.</span></span>
  
<span data-ttu-id="507c2-108">任务并行库 (TPL) 可采用各种方法与任一异步模式协同使用。</span><span class="sxs-lookup"><span data-stu-id="507c2-108">The Task Parallel Library (TPL) can be used in various ways in conjunction with either of the asynchronous patterns.</span></span> <span data-ttu-id="507c2-109">可将 APM 和 EAP 操作作为 `Task` 对象向库使用者公开，也可以公开 APM 模式但用 `Task` 对象在内部实现它们。</span><span class="sxs-lookup"><span data-stu-id="507c2-109">You can expose both APM and EAP operations as `Task` objects to library consumers, or you can expose the APM patterns but use `Task` objects to implement them internally.</span></span> <span data-ttu-id="507c2-110">在这两种情况下，可使用 `Task` 对象简化代码以及利用以下有用的功能：</span><span class="sxs-lookup"><span data-stu-id="507c2-110">In both scenarios, by using `Task` objects, you can simplify the code and take advantage of the following useful functionality:</span></span>  
  
- <span data-ttu-id="507c2-111">在任务开始后随时以任务延续形式注册回调。</span><span class="sxs-lookup"><span data-stu-id="507c2-111">Register callbacks, in the form of task continuations, at any time after the task has started.</span></span>  
  
- <span data-ttu-id="507c2-112">使用 <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A> 和 <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A> 方法，或者 <xref:System.Threading.Tasks.Task.WaitAll%2A> 和 <xref:System.Threading.Tasks.Task.WaitAny%2A> 方法并列为响应 `Begin_` 方法而执行的多个操作。</span><span class="sxs-lookup"><span data-stu-id="507c2-112">Coordinate multiple operations that execute in response to a `Begin_` method by using the <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A> and <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A> methods, or the <xref:System.Threading.Tasks.Task.WaitAll%2A> and <xref:System.Threading.Tasks.Task.WaitAny%2A> methods.</span></span>  
  
- <span data-ttu-id="507c2-113">封装同一 `Task` 对象中的异步 I/O 密集型和计算密集型操作。</span><span class="sxs-lookup"><span data-stu-id="507c2-113">Encapsulate asynchronous I/O-bound and compute-bound operations in the same `Task` object.</span></span>  
  
- <span data-ttu-id="507c2-114">监视 `Task` 对象的状态。</span><span class="sxs-lookup"><span data-stu-id="507c2-114">Monitor the status of the `Task` object.</span></span>  
  
- <span data-ttu-id="507c2-115">使用 <xref:System.Threading.Tasks.TaskCompletionSource%601> 将操作状态封送处理至 `Task` 对象。</span><span class="sxs-lookup"><span data-stu-id="507c2-115">Marshal the status of an operation to a `Task` object by using <xref:System.Threading.Tasks.TaskCompletionSource%601>.</span></span>  
  
## <a name="wrap-apm-operations-in-a-task"></a><span data-ttu-id="507c2-116">在 Task 中包装 APM 操作</span><span class="sxs-lookup"><span data-stu-id="507c2-116">Wrap APM operations in a Task</span></span>  

 <span data-ttu-id="507c2-117"><xref:System.Threading.Tasks.TaskFactory?displayProperty=nameWithType> 和 <xref:System.Threading.Tasks.TaskFactory%601?displayProperty=nameWithType> 类都提供了 <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A?displayProperty=nameWithType> 和 <xref:System.Threading.Tasks.TaskFactory%601.FromAsync%2A?displayProperty=nameWithType> 方法的几个重载，由此可将 APM begin/end 方法对封装在 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601> 实例中。</span><span class="sxs-lookup"><span data-stu-id="507c2-117">Both the <xref:System.Threading.Tasks.TaskFactory?displayProperty=nameWithType> and <xref:System.Threading.Tasks.TaskFactory%601?displayProperty=nameWithType> classes provide several overloads of the <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A?displayProperty=nameWithType> and <xref:System.Threading.Tasks.TaskFactory%601.FromAsync%2A?displayProperty=nameWithType> methods that let you encapsulate an APM begin/end method pair in one <xref:System.Threading.Tasks.Task> or <xref:System.Threading.Tasks.Task%601> instance.</span></span> <span data-ttu-id="507c2-118">各种重载都可容纳任何具有零至三个输入参数的 begin/end 方法对。</span><span class="sxs-lookup"><span data-stu-id="507c2-118">The various overloads accommodate any begin/end method pair that have from zero to three input parameters.</span></span>  
  
 <span data-ttu-id="507c2-119">对于具有返回值（在 Visual Basic 中为 `Function`）的 `End` 方法的对，使用 <xref:System.Threading.Tasks.TaskFactory%601> 中创建 <xref:System.Threading.Tasks.Task%601> 的方法。</span><span class="sxs-lookup"><span data-stu-id="507c2-119">For pairs that have `End` methods that return a value (a `Function` in Visual Basic), use the methods in <xref:System.Threading.Tasks.TaskFactory%601> that create a <xref:System.Threading.Tasks.Task%601>.</span></span> <span data-ttu-id="507c2-120">对于具有返回 void（在 Visual Basic 中为 `Sub`）的 `End` 方法，使用 <xref:System.Threading.Tasks.TaskFactory> 中创建 <xref:System.Threading.Tasks.Task> 的方法。</span><span class="sxs-lookup"><span data-stu-id="507c2-120">For `End` methods that return void (a `Sub` in Visual Basic), use the methods in <xref:System.Threading.Tasks.TaskFactory> that create a <xref:System.Threading.Tasks.Task>.</span></span>  
  
 <span data-ttu-id="507c2-121">在极少情况下，如果 `Begin` 方法具有三个以上参数或包含 `ref` 或 `out` 参数，则提供仅封装 `End` 方法的其他 `FromAsync` 重载。</span><span class="sxs-lookup"><span data-stu-id="507c2-121">For those few cases in which the `Begin` method has more than three parameters or contains `ref` or `out` parameters, additional `FromAsync` overloads that encapsulate only the `End` method are provided.</span></span>  
  
 <span data-ttu-id="507c2-122">下面的示例显示了匹配 <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType> 和 <xref:System.IO.FileStream.EndRead%2A?displayProperty=nameWithType> 方法的 `FromAsync` 重载的签名。</span><span class="sxs-lookup"><span data-stu-id="507c2-122">The following example shows the signature for the `FromAsync` overload that matches the <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType> and <xref:System.IO.FileStream.EndRead%2A?displayProperty=nameWithType> methods.</span></span>
  
 [!code-csharp[FromAsync#01](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#01)]
 [!code-vb[FromAsync#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#01)]  
  
<span data-ttu-id="507c2-123">此重载采用三个输入参数，如下所示。</span><span class="sxs-lookup"><span data-stu-id="507c2-123">This overload takes three input parameters, as follows.</span></span> <span data-ttu-id="507c2-124">第一个参数是匹配 <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType> 方法签名的 <xref:System.Func%606> 委托。</span><span class="sxs-lookup"><span data-stu-id="507c2-124">The first parameter is a <xref:System.Func%606> delegate that matches the signature of the <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="507c2-125">第二个参数使用 <xref:System.IAsyncResult> 并返回 `TResult` 的 <xref:System.Func%602> 委托。</span><span class="sxs-lookup"><span data-stu-id="507c2-125">The second parameter is a <xref:System.Func%602> delegate that takes an <xref:System.IAsyncResult> and returns a `TResult`.</span></span> <span data-ttu-id="507c2-126">由于 <xref:System.IO.FileStream.EndRead%2A> 返回一个整数，因此编译器会将 `TResult` 类型推断为 <xref:System.Int32> 并将任务类型推断为 <xref:System.Threading.Tasks.Task>。</span><span class="sxs-lookup"><span data-stu-id="507c2-126">Because <xref:System.IO.FileStream.EndRead%2A> returns an integer, the compiler infers the type of `TResult` as <xref:System.Int32> and the type of the task as <xref:System.Threading.Tasks.Task>.</span></span> <span data-ttu-id="507c2-127">最后第四个参数与 <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType> 方法中的参数相同：</span><span class="sxs-lookup"><span data-stu-id="507c2-127">The last four parameters are identical to those in the <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType> method:</span></span>  
  
- <span data-ttu-id="507c2-128">存储文件数据的缓冲区。</span><span class="sxs-lookup"><span data-stu-id="507c2-128">The buffer in which to store the file data.</span></span>  
  
- <span data-ttu-id="507c2-129">开始写入数据的缓冲区的偏移量。</span><span class="sxs-lookup"><span data-stu-id="507c2-129">The offset in the buffer at which to begin writing data.</span></span>  
  
- <span data-ttu-id="507c2-130">要从文件中读取的最大数据量。</span><span class="sxs-lookup"><span data-stu-id="507c2-130">The maximum amount of data to read from the file.</span></span>  
  
- <span data-ttu-id="507c2-131">存储要传递至回调的用户定义状态数据的可选对象。</span><span class="sxs-lookup"><span data-stu-id="507c2-131">An optional object that stores user-defined state data to pass to the callback.</span></span>  
  
### <a name="use-continuewith-for-the-callback-functionality"></a><span data-ttu-id="507c2-132">使用 ContinueWith 执行回调功能</span><span class="sxs-lookup"><span data-stu-id="507c2-132">Use ContinueWith for the callback functionality</span></span>

 <span data-ttu-id="507c2-133">如果需要访问文件中的数据，而不仅仅访问字节数，则 <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A> 方法不能满足此操作。</span><span class="sxs-lookup"><span data-stu-id="507c2-133">If you require access to the data in the file, as opposed to just the number of bytes, the <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A> method is not sufficient.</span></span> <span data-ttu-id="507c2-134">请改用 <xref:System.Threading.Tasks.Task>，其 `Result` 属性包含文件数据。</span><span class="sxs-lookup"><span data-stu-id="507c2-134">Instead, use <xref:System.Threading.Tasks.Task>, whose `Result` property contains the file data.</span></span> <span data-ttu-id="507c2-135">可以通过向原始任务添加延续来实现这种操作。</span><span class="sxs-lookup"><span data-stu-id="507c2-135">You can do this by adding a continuation to the original task.</span></span> <span data-ttu-id="507c2-136">延续执行通常由 <xref:System.AsyncCallback> 委托执行的任务。</span><span class="sxs-lookup"><span data-stu-id="507c2-136">The continuation performs the work that would typically be performed by the <xref:System.AsyncCallback> delegate.</span></span> <span data-ttu-id="507c2-137">先前任务完成且填充了数据缓冲区后调用此操作。</span><span class="sxs-lookup"><span data-stu-id="507c2-137">It is invoked when the antecedent completes, and the data buffer has been filled.</span></span> <span data-ttu-id="507c2-138">（<xref:System.IO.FileStream> 对象应在返回前关闭。）</span><span class="sxs-lookup"><span data-stu-id="507c2-138">(The <xref:System.IO.FileStream> object should be closed before returning.)</span></span>  
  
 <span data-ttu-id="507c2-139">下面的示例演示如何返回封装 <xref:System.IO.FileStream> 类的 `BeginRead`/`EndRead` 对的 <xref:System.Threading.Tasks.Task>。</span><span class="sxs-lookup"><span data-stu-id="507c2-139">The following example shows how to return a <xref:System.Threading.Tasks.Task> that encapsulates the `BeginRead`/`EndRead` pair of the <xref:System.IO.FileStream> class.</span></span>  
  
 [!code-csharp[FromAsync#03](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#03)]
 [!code-vb[FromAsync#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#03)]  
  
 <span data-ttu-id="507c2-140">然后可调用此方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="507c2-140">The method can then be called, as follows.</span></span>  
  
 [!code-csharp[FromAsync#04](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#04)]
 [!code-vb[FromAsync#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#04)]  
  
### <a name="provide-custom-state-data"></a><span data-ttu-id="507c2-141">提供自定义状态数据</span><span class="sxs-lookup"><span data-stu-id="507c2-141">Provide custom state data</span></span>

 <span data-ttu-id="507c2-142">在通常的 <xref:System.IAsyncResult> 操作中，如果<xref:System.AsyncCallback> 委托需要一些自定义状态数据，则必须通过 `Begin` 方法中的最后一个参数将它传入，以便可将数据打包到最终要传递至回调方法的 <xref:System.IAsyncResult> 对象中。</span><span class="sxs-lookup"><span data-stu-id="507c2-142">In typical <xref:System.IAsyncResult> operations, if your <xref:System.AsyncCallback> delegate requires some custom state data, you have to pass it in through the last parameter in the `Begin` method, so that the data can be packaged into the <xref:System.IAsyncResult> object that is eventually passed to the callback method.</span></span> <span data-ttu-id="507c2-143">当使用 `FromAsync` 方法时，通常无需此操作。</span><span class="sxs-lookup"><span data-stu-id="507c2-143">This is typically not required when the `FromAsync` methods are used.</span></span> <span data-ttu-id="507c2-144">如果延续知道自定义数据，可直接在延续委托中捕获它。</span><span class="sxs-lookup"><span data-stu-id="507c2-144">If the custom data is known to the continuation, then it can be captured directly in the continuation delegate.</span></span> <span data-ttu-id="507c2-145">下面的示例与以前的示例类似，但延续检查此延续的用户委托可直接访问的自定义状态数据，而不是检查历史任务的 `Result` 属性。</span><span class="sxs-lookup"><span data-stu-id="507c2-145">The following example resembles the previous example, but instead of examining the `Result` property of the antecedent, the continuation examines the custom state data that is directly accessible to the user delegate of the continuation.</span></span>  
  
 [!code-csharp[FromAsync#05](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#05)]
 [!code-vb[FromAsync#05](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#05)]  
  
### <a name="synchronize-multiple-fromasync-tasks"></a><span data-ttu-id="507c2-146">同步多个 FromAsync 任务</span><span class="sxs-lookup"><span data-stu-id="507c2-146">Synchronize multiple FromAsync tasks</span></span>

 <span data-ttu-id="507c2-147">当结合使用 `FromAsync` 方法时，静态 <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A> 和 <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A> 方法具有更大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="507c2-147">The static <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A> and <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A> methods provide added flexibility when used in conjunction with the `FromAsync` methods.</span></span> <span data-ttu-id="507c2-148">下面的示例显示如何启动多个异步 I/O 操作，然后等待所有这些操作都完成后再执行延续。</span><span class="sxs-lookup"><span data-stu-id="507c2-148">The following example shows how to initiate multiple asynchronous I/O operations, and then wait for all of them to complete before you execute the continuation.</span></span>  
  
 [!code-csharp[FromAsync#06](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#06)]
 [!code-vb[FromAsync#06](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#06)]  
  
### <a name="fromasync-tasks-for-only-the-end-method"></a><span data-ttu-id="507c2-149">仅用于 End 方法的 FromAsync 任务</span><span class="sxs-lookup"><span data-stu-id="507c2-149">FromAsync tasks for only the End method</span></span>

 <span data-ttu-id="507c2-150">在极少情况下，如果 `Begin` 方法需要三个以上的输入参数，或具有 `ref` 或 `out` 参数，可以使用仅表示 `End` 方法的 `FromAsync` 重载，例如，<xref:System.Threading.Tasks.TaskFactory%601.FromAsync%28System.IAsyncResult%2CSystem.Func%7BSystem.IAsyncResult%2C%600%7D%29?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="507c2-150">For those few cases in which the `Begin` method requires more than three input parameters or has `ref` or `out` parameters, you can use the `FromAsync` overloads, for example, <xref:System.Threading.Tasks.TaskFactory%601.FromAsync%28System.IAsyncResult%2CSystem.Func%7BSystem.IAsyncResult%2C%600%7D%29?displayProperty=nameWithType>, that represent only the `End` method.</span></span> <span data-ttu-id="507c2-151">这些方法还可用于传递 <xref:System.IAsyncResult> 并将其封装到 Task 的任何方案中。</span><span class="sxs-lookup"><span data-stu-id="507c2-151">These methods can also be used in any scenario in which you're passed an <xref:System.IAsyncResult> and want to encapsulate it in a Task.</span></span>  
  
 [!code-csharp[FromAsync#07](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#07)]
 [!code-vb[FromAsync#07](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#07)]  
  
### <a name="start-and-cancel-fromasync-tasks"></a><span data-ttu-id="507c2-152">开始和取消 FromAsync 任务</span><span class="sxs-lookup"><span data-stu-id="507c2-152">Start and cancel FromAsync tasks</span></span>

 <span data-ttu-id="507c2-153">`FromAsync` 方法返回的任务具有 `WaitingForActivation` 状态，并在创建任务后在某个时刻由操作系统启动。</span><span class="sxs-lookup"><span data-stu-id="507c2-153">The task returned by a `FromAsync` method has a status of `WaitingForActivation` and will be started by the system at some point after the task is created.</span></span> <span data-ttu-id="507c2-154">如果尝试调用此类任务上的“启动”，将引发异常。</span><span class="sxs-lookup"><span data-stu-id="507c2-154">If you attempt to call Start on such a task, an exception will be raised.</span></span>  
  
 <span data-ttu-id="507c2-155">无法取消 `FromAsync` 任务，因为基础 .NET API 目前不支持取消正在进行中的文件或网络 I/O。</span><span class="sxs-lookup"><span data-stu-id="507c2-155">You cannot cancel a `FromAsync` task, because the underlying .NET APIs currently do not support in-progress cancellation of file or network I/O.</span></span> <span data-ttu-id="507c2-156">可以将取消功能添加到封装 `FromAsync` 调用的方法中，但只能在调用 `FromAsync` 之前或在调用完成之后响应取消（例如，在延续任务中）。</span><span class="sxs-lookup"><span data-stu-id="507c2-156">You can add cancellation functionality to a method that encapsulates a `FromAsync` call, but you can only respond to the cancellation before `FromAsync` is called or after it completed (for example, in a continuation task).</span></span>  
  
 <span data-ttu-id="507c2-157">一些支持 EAP 的类（如 <xref:System.Net.WebClient>）不支持取消，但可以通过使用取消标记集成该本机取消功能。</span><span class="sxs-lookup"><span data-stu-id="507c2-157">Some classes that support EAP, for example, <xref:System.Net.WebClient>, do support cancellation, and you can integrate that native cancellation functionality by using cancellation tokens.</span></span>  
  
## <a name="expose-complex-eap-operations-as-tasks"></a><span data-ttu-id="507c2-158">将复杂的 EAP 操作公开为任务</span><span class="sxs-lookup"><span data-stu-id="507c2-158">Expose complex EAP operations As tasks</span></span>

 <span data-ttu-id="507c2-159">TPL 不提供任何专用于以 `FromAsync` 系列方法包装 <xref:System.IAsyncResult> 模式相同的方式封装基于事件的异步操作的方法。</span><span class="sxs-lookup"><span data-stu-id="507c2-159">The TPL does not provide any methods that are specifically designed to encapsulate an event-based asynchronous operation in the same way that the `FromAsync` family of methods wrap the <xref:System.IAsyncResult> pattern.</span></span> <span data-ttu-id="507c2-160">但是，TPL 会提供 <xref:System.Threading.Tasks.TaskCompletionSource%601?displayProperty=nameWithType> 类，此类可用于将任意一组操作表示为 <xref:System.Threading.Tasks.Task%601>。</span><span class="sxs-lookup"><span data-stu-id="507c2-160">However, the TPL does provide the <xref:System.Threading.Tasks.TaskCompletionSource%601?displayProperty=nameWithType> class, which can be used to represent any arbitrary set of operations as a <xref:System.Threading.Tasks.Task%601>.</span></span> <span data-ttu-id="507c2-161">这些操作可能同步、可能异步，可能是 I/O 密集型、也可能是计算密集型，还可能两者都是。</span><span class="sxs-lookup"><span data-stu-id="507c2-161">The operations may be synchronous or asynchronous, and may be I/O bound or compute-bound, or both.</span></span>  
  
 <span data-ttu-id="507c2-162">下面的示例显示如何使用 <xref:System.Threading.Tasks.TaskCompletionSource%601> 将一组异步 <xref:System.Net.WebClient> 操作作为基础 <xref:System.Threading.Tasks.Task%601> 向客户端代码公开。</span><span class="sxs-lookup"><span data-stu-id="507c2-162">The following example shows how to use a <xref:System.Threading.Tasks.TaskCompletionSource%601> to expose a set of asynchronous <xref:System.Net.WebClient> operations to client code as a basic <xref:System.Threading.Tasks.Task%601>.</span></span> <span data-ttu-id="507c2-163">此方法允许输入 Web URL 数组和术语或名称来进行搜索，然后返回每个站点搜索字词出现的次数。</span><span class="sxs-lookup"><span data-stu-id="507c2-163">The method lets you enter an array of Web URLs, and a term or name to search for, and then returns the number of times the search term occurs on each site.</span></span>  
  
 [!code-csharp[FromAsync#10](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/snippet10.cs#10)]
 [!code-vb[FromAsync#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/snippet10.vb#10)]  
  
 <span data-ttu-id="507c2-164">有关包括其他异常处理且展示了如何通过客户端代码调用方法的更完整示例，请参阅[如何：在任务中包装 EAP 模式](how-to-wrap-eap-patterns-in-a-task.md)。</span><span class="sxs-lookup"><span data-stu-id="507c2-164">For a more complete example, which includes additional exception handling and shows how to call the method from client code, see [How to: Wrap EAP Patterns in a Task](how-to-wrap-eap-patterns-in-a-task.md).</span></span>  
  
 <span data-ttu-id="507c2-165">请记住，通过 <xref:System.Threading.Tasks.TaskCompletionSource%601> 创建的任何任务均由 `TaskCompletionSource` 启动，因此用户代码不应在此任务中调用 `Start` 方法。</span><span class="sxs-lookup"><span data-stu-id="507c2-165">Remember that any task that's created by a <xref:System.Threading.Tasks.TaskCompletionSource%601> will be started by that `TaskCompletionSource` and, therefore, user code should not call the `Start` method on that task.</span></span>  
  
## <a name="implement-the-apm-pattern-by-using-tasks"></a><span data-ttu-id="507c2-166">使用任务实现 APM 模式</span><span class="sxs-lookup"><span data-stu-id="507c2-166">Implement the APM pattern by using tasks</span></span>

 <span data-ttu-id="507c2-167">在某些情况下，可能需要通过使用 API 中 begin/end 方法对直接公开 <xref:System.IAsyncResult> 模式。</span><span class="sxs-lookup"><span data-stu-id="507c2-167">In some scenarios, it may be desirable to directly expose the <xref:System.IAsyncResult> pattern by using begin/end method pairs in an API.</span></span> <span data-ttu-id="507c2-168">例如，可能想要与现有的 API 保持一致，或者可能具有需要这种模式的自动化工具。</span><span class="sxs-lookup"><span data-stu-id="507c2-168">For example, you may want to maintain consistency with existing APIs, or you may have automated tools that require this pattern.</span></span> <span data-ttu-id="507c2-169">在这种情况下，可使用 `Task` 对象来简化在内部实现 APM 模式的方式。</span><span class="sxs-lookup"><span data-stu-id="507c2-169">In such cases, you can use `Task` objects to simplify how the APM pattern is implemented internally.</span></span>  
  
 <span data-ttu-id="507c2-170">下面的示例显示如何使用任务实现长时间运行计算密集型方法的 APM begin/end 方法对。</span><span class="sxs-lookup"><span data-stu-id="507c2-170">The following example shows how to use tasks to implement an APM begin/end method pair for a long-running compute-bound method.</span></span>  
  
 [!code-csharp[FromAsync#09](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#09)]
 [!code-vb[FromAsync#09](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#09)]  
  
## <a name="use-the-streamextensions-sample-code"></a><span data-ttu-id="507c2-171">使用 StreamExtensions 示例代码</span><span class="sxs-lookup"><span data-stu-id="507c2-171">Use the StreamExtensions sample code</span></span>

 <span data-ttu-id="507c2-172"> [.NET Standard parallel extensions extras](/samples/dotnet/samples/parallel-programming-extensions-extras-cs/) 存储库中的 StreamExtensions.cs 文件包含将 `Task` 对象用于异步文件和网络 I/O 的若干参考实现。</span><span class="sxs-lookup"><span data-stu-id="507c2-172">The *StreamExtensions.cs* file, in the [.NET Standard parallel extensions extras](/samples/dotnet/samples/parallel-programming-extensions-extras-cs/) repository, contains several reference implementations that use `Task` objects for asynchronous file and network I/O.</span></span>
  
## <a name="see-also"></a><span data-ttu-id="507c2-173">请参阅</span><span class="sxs-lookup"><span data-stu-id="507c2-173">See also</span></span>

- [<span data-ttu-id="507c2-174">任务并行库 (TPL)</span><span class="sxs-lookup"><span data-stu-id="507c2-174">Task Parallel Library (TPL)</span></span>](task-parallel-library-tpl.md)
