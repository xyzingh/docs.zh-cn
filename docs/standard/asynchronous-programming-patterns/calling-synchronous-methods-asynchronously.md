---
title: 使用异步方式调用同步方法
description: 了解如何使用 BeginInvoke 和 EndInvoke 方法在 .NET 中以异步方式调用同步方法。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- asynchronous programming, delegates
- asynchronous delegates
- AsyncWaitHandle property
- callback methods
- calling synchronous methods in asynchronous manner
- WaitHandle class, code examples
- asynchronous programming, status polling
- polling asynchronous operation status
- delegates [.NET], asynchronous
- synchronous calling in asynchronous manner
- waiting for asynchronous calls
- status information [.NET], asynchronous operations
ms.assetid: 41972034-92ed-450a-9664-ab93fcc6f1fb
ms.openlocfilehash: d518e5f64096fde5c9b14222dc4fe0634e6bb7b1
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888888"
---
# <a name="calling-synchronous-methods-asynchronously"></a><span data-ttu-id="b0967-103">使用异步方式调用同步方法</span><span class="sxs-lookup"><span data-stu-id="b0967-103">Calling Synchronous Methods Asynchronously</span></span>

<span data-ttu-id="b0967-104">使用 .NET 可以以异步方式调用任何方法。</span><span class="sxs-lookup"><span data-stu-id="b0967-104">.NET enables you to call any method asynchronously.</span></span> <span data-ttu-id="b0967-105">为此，请定义一个委托，该委托具有与你要调用的方法相同的签名。</span><span class="sxs-lookup"><span data-stu-id="b0967-105">To do this, you define a delegate with the same signature as the method you want to call.</span></span> <span data-ttu-id="b0967-106">公共语言运行时将自动用适当的签名为此委托定义 `BeginInvoke` 和 `EndInvoke` 方法。</span><span class="sxs-lookup"><span data-stu-id="b0967-106">The common language runtime automatically defines `BeginInvoke` and `EndInvoke` methods for this delegate, with the appropriate signatures.</span></span>

> [!NOTE]
> <span data-ttu-id="b0967-107">.NET Compact Framework 不支持异步委托调用，也就是 `BeginInvoke` 和 `EndInvoke` 方法。</span><span class="sxs-lookup"><span data-stu-id="b0967-107">Asynchronous delegate calls, specifically the `BeginInvoke` and `EndInvoke` methods, are not supported in the .NET Compact Framework.</span></span>

<span data-ttu-id="b0967-108">`BeginInvoke` 方法启动异步调用。</span><span class="sxs-lookup"><span data-stu-id="b0967-108">The `BeginInvoke` method initiates the asynchronous call.</span></span> <span data-ttu-id="b0967-109">该方法具有与你要异步执行的方法相同的参数，另加两个可选参数。</span><span class="sxs-lookup"><span data-stu-id="b0967-109">It has the same parameters as the method that you want to execute asynchronously, plus two additional optional parameters.</span></span> <span data-ttu-id="b0967-110">第一个参数是一个 <xref:System.AsyncCallback> 委托，此委托引用在异步调用完成时要调用的方法。</span><span class="sxs-lookup"><span data-stu-id="b0967-110">The first parameter is an <xref:System.AsyncCallback> delegate that references a method to be called when the asynchronous call completes.</span></span> <span data-ttu-id="b0967-111">第二个参数是一个用户定义的对象，该对象将信息传递到回调方法。</span><span class="sxs-lookup"><span data-stu-id="b0967-111">The second parameter is a user-defined object that passes information into the callback method.</span></span> <span data-ttu-id="b0967-112">`BeginInvoke` 将立即返回，而不会等待异步调用完成。</span><span class="sxs-lookup"><span data-stu-id="b0967-112">`BeginInvoke` returns immediately and does not wait for the asynchronous call to complete.</span></span> <span data-ttu-id="b0967-113">`BeginInvoke` 返回可用于监视异步调用的进度的 <xref:System.IAsyncResult>。</span><span class="sxs-lookup"><span data-stu-id="b0967-113">`BeginInvoke` returns an <xref:System.IAsyncResult>, which can be used to monitor the progress of the asynchronous call.</span></span>

<span data-ttu-id="b0967-114">`EndInvoke` 方法用于检索异步调用的结果。</span><span class="sxs-lookup"><span data-stu-id="b0967-114">The `EndInvoke` method retrieves the results of the asynchronous call.</span></span> <span data-ttu-id="b0967-115">它可以在调用 `BeginInvoke`之后的任意时间调用。</span><span class="sxs-lookup"><span data-stu-id="b0967-115">It can be called any time after `BeginInvoke`.</span></span> <span data-ttu-id="b0967-116">如果异步调用尚未完成，那么 `EndInvoke` 将阻止调用线程，直到完成异步调用。</span><span class="sxs-lookup"><span data-stu-id="b0967-116">If the asynchronous call has not completed, `EndInvoke` blocks the calling thread until it completes.</span></span> <span data-ttu-id="b0967-117">`EndInvoke` 的参数包括要异步执行的方法的 `out` 和 `ref` 参数（Visual Basic 中的 `<Out>` `ByRef` 和 `ByRef`）以及 `BeginInvoke` 返回的 <xref:System.IAsyncResult>。</span><span class="sxs-lookup"><span data-stu-id="b0967-117">The parameters of `EndInvoke` include the `out` and `ref` parameters (`<Out>` `ByRef` and `ByRef` in Visual Basic) of the method that you want to execute asynchronously, plus the <xref:System.IAsyncResult> returned by `BeginInvoke`.</span></span>

> [!NOTE]
> <span data-ttu-id="b0967-118">Visual Studio 中的 IntelliSense 功能可显示 `BeginInvoke` 和 `EndInvoke` 的参数。</span><span class="sxs-lookup"><span data-stu-id="b0967-118">The IntelliSense feature in Visual Studio displays the parameters of `BeginInvoke` and `EndInvoke`.</span></span> <span data-ttu-id="b0967-119">如果未使用 Visual Studio 或类似工具，或者如果使用的是包含 Visual Studio 的 C#，请参阅[异步编程模型 (APM)](asynchronous-programming-model-apm.md)，获取关于为这些方法定义的参数的说明。</span><span class="sxs-lookup"><span data-stu-id="b0967-119">If you're not using Visual Studio or a similar tool, or if you're using C# with Visual Studio, see [Asynchronous Programming Model (APM)](asynchronous-programming-model-apm.md) for a description of the parameters defined for these methods.</span></span>

<span data-ttu-id="b0967-120">本主题的代码示例演示了使用 `BeginInvoke` 和 `EndInvoke` 进行异步调用的四种常用方法。</span><span class="sxs-lookup"><span data-stu-id="b0967-120">The code examples in this topic demonstrate four common ways to use `BeginInvoke` and `EndInvoke` to make asynchronous calls.</span></span> <span data-ttu-id="b0967-121">调用 `BeginInvoke` 之后可以执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="b0967-121">After calling `BeginInvoke` you can do the following:</span></span>

- <span data-ttu-id="b0967-122">执行一些操作，然后调用 `EndInvoke` 进行阻止，直到调用完成。</span><span class="sxs-lookup"><span data-stu-id="b0967-122">Do some work and then call `EndInvoke` to block until the call completes.</span></span>

- <span data-ttu-id="b0967-123">使用 <xref:System.Threading.WaitHandle> 属性获取 <xref:System.IAsyncResult.AsyncWaitHandle%2A?displayProperty=nameWithType> ，使用它的 <xref:System.Threading.WaitHandle.WaitOne%2A> 方法阻止执行，直到 <xref:System.Threading.WaitHandle> 收到信号，然后调用 `EndInvoke`。</span><span class="sxs-lookup"><span data-stu-id="b0967-123">Obtain a <xref:System.Threading.WaitHandle> using the <xref:System.IAsyncResult.AsyncWaitHandle%2A?displayProperty=nameWithType> property, use its <xref:System.Threading.WaitHandle.WaitOne%2A> method to block execution until the <xref:System.Threading.WaitHandle> is signaled, and then call `EndInvoke`.</span></span>

- <span data-ttu-id="b0967-124">对由 <xref:System.IAsyncResult> 返回的 `BeginInvoke` 进行轮询，以确定异步调用完成的时间，然后调用 `EndInvoke`。</span><span class="sxs-lookup"><span data-stu-id="b0967-124">Poll the <xref:System.IAsyncResult> returned by `BeginInvoke` to determine when the asynchronous call has completed, and then call `EndInvoke`.</span></span>

- <span data-ttu-id="b0967-125">将回调方法的委托传递到 `BeginInvoke`。</span><span class="sxs-lookup"><span data-stu-id="b0967-125">Pass a delegate for a callback method to `BeginInvoke`.</span></span> <span data-ttu-id="b0967-126">异步调用完成后在 <xref:System.Threading.ThreadPool> 线程上执行此方法。</span><span class="sxs-lookup"><span data-stu-id="b0967-126">The method is executed on a <xref:System.Threading.ThreadPool> thread when the asynchronous call completes.</span></span> <span data-ttu-id="b0967-127">回调方法将调用 `EndInvoke`。</span><span class="sxs-lookup"><span data-stu-id="b0967-127">The callback method calls `EndInvoke`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0967-128">无论使用何种方法，都要调用 `EndInvoke` 来完成异步调用。</span><span class="sxs-lookup"><span data-stu-id="b0967-128">No matter which technique you use, always call `EndInvoke` to complete your asynchronous call.</span></span>

## <a name="defining-the-test-method-and-asynchronous-delegate"></a><span data-ttu-id="b0967-129">定义测试方法和异步委托</span><span class="sxs-lookup"><span data-stu-id="b0967-129">Defining the Test Method and Asynchronous Delegate</span></span>
 <span data-ttu-id="b0967-130">下面的代码示例演示了异步调用同一个长时间运行的方法 `TestMethod`的各种方式。</span><span class="sxs-lookup"><span data-stu-id="b0967-130">The code examples that follow demonstrate various ways of calling the same long-running method, `TestMethod`, asynchronously.</span></span> <span data-ttu-id="b0967-131">`TestMethod` 方法会显示一条控制台消息，说明该方法已开始处理，休眠了几秒钟，然后结束。</span><span class="sxs-lookup"><span data-stu-id="b0967-131">The `TestMethod` method displays a console message to show that it has begun processing, sleeps for a few seconds, and then ends.</span></span> <span data-ttu-id="b0967-132">`TestMethod` 有一个 `out` 参数，该参数用于演示将此类参数添加到 `BeginInvoke` 和 `EndInvoke`的签名中的方式。</span><span class="sxs-lookup"><span data-stu-id="b0967-132">`TestMethod` has an `out` parameter to demonstrate the way such parameters are added to the signatures of `BeginInvoke` and `EndInvoke`.</span></span> <span data-ttu-id="b0967-133">您可以按同样的方式处理 `ref` 参数。</span><span class="sxs-lookup"><span data-stu-id="b0967-133">You can handle `ref` parameters similarly.</span></span>

 <span data-ttu-id="b0967-134">下面的代码示例显示了 `TestMethod` 的定义和可用于异步调用 `AsyncMethodCaller` 的名称为 `TestMethod` 的委托。</span><span class="sxs-lookup"><span data-stu-id="b0967-134">The following code example shows the definition of `TestMethod` and the delegate named `AsyncMethodCaller` that can be used to call `TestMethod` asynchronously.</span></span> <span data-ttu-id="b0967-135">要编译此代码示例，必须包括 `TestMethod` 和 `AsyncMethodCaller` 委托的定义。</span><span class="sxs-lookup"><span data-stu-id="b0967-135">To compile the code examples, you must include the definitions for `TestMethod` and the `AsyncMethodCaller` delegate.</span></span>

 [!code-cpp[AsyncDelegateExamples#1](../../../samples/snippets/cpp/VS_Snippets_CLR/AsyncDelegateExamples/cpp/TestMethod.cpp#1)]
 [!code-csharp[AsyncDelegateExamples#1](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDelegateExamples/CS/TestMethod.cs#1)]
 [!code-vb[AsyncDelegateExamples#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDelegateExamples/VB/TestMethod.vb#1)]

## <a name="waiting-for-an-asynchronous-call-with-endinvoke"></a><span data-ttu-id="b0967-136">使用 EndInvoke 等待异步调用</span><span class="sxs-lookup"><span data-stu-id="b0967-136">Waiting for an Asynchronous Call with EndInvoke</span></span>
 <span data-ttu-id="b0967-137">异步执行方法的最简单方式是通过调用委托的 `BeginInvoke` 方法开始执行此方法，在主线程上执行一些操作，然后调用委托的 `EndInvoke` 方法。</span><span class="sxs-lookup"><span data-stu-id="b0967-137">The simplest way to execute a method asynchronously is to start executing the method by calling the delegate's `BeginInvoke` method, do some work on the main thread, and then call the delegate's `EndInvoke` method.</span></span> <span data-ttu-id="b0967-138">`EndInvoke` 可能会阻止调用线程，因为该方法直到异步调用完成后才返回。</span><span class="sxs-lookup"><span data-stu-id="b0967-138">`EndInvoke` might block the calling thread because it does not return until the asynchronous call completes.</span></span> <span data-ttu-id="b0967-139">这种方式非常适合执行文件或网络操作。</span><span class="sxs-lookup"><span data-stu-id="b0967-139">This is a good technique to use with file or network operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0967-140">因为 `EndInvoke` 可能会阻塞，所以不应从服务于用户界面的线程调用该方法。</span><span class="sxs-lookup"><span data-stu-id="b0967-140">Because `EndInvoke` might block, you should never call it from threads that service the user interface.</span></span>

 [!code-cpp[AsyncDelegateExamples#2](../../../samples/snippets/cpp/VS_Snippets_CLR/AsyncDelegateExamples/cpp/EndInvoke.cpp#2)]
 [!code-csharp[AsyncDelegateExamples#2](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDelegateExamples/CS/EndInvoke.cs#2)]
 [!code-vb[AsyncDelegateExamples#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDelegateExamples/VB/EndInvoke.vb#2)]

## <a name="waiting-for-an-asynchronous-call-with-waithandle"></a><span data-ttu-id="b0967-141">使用 WaitHandle 等待异步调用</span><span class="sxs-lookup"><span data-stu-id="b0967-141">Waiting for an Asynchronous Call with WaitHandle</span></span>
 <span data-ttu-id="b0967-142">可以使用由 <xref:System.Threading.WaitHandle> 返回的 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 的 <xref:System.IAsyncResult> 属性来获取 `BeginInvoke`。</span><span class="sxs-lookup"><span data-stu-id="b0967-142">You can obtain a <xref:System.Threading.WaitHandle> by using the <xref:System.IAsyncResult.AsyncWaitHandle%2A> property of the <xref:System.IAsyncResult> returned by `BeginInvoke`.</span></span> <span data-ttu-id="b0967-143">当异步调用完成时 <xref:System.Threading.WaitHandle> 会收到信号，而你可以通过调用 <xref:System.Threading.WaitHandle.WaitOne%2A> 方法来等待它。</span><span class="sxs-lookup"><span data-stu-id="b0967-143">The <xref:System.Threading.WaitHandle> is signaled when the asynchronous call completes, and you can wait for it by calling the <xref:System.Threading.WaitHandle.WaitOne%2A> method.</span></span>

 <span data-ttu-id="b0967-144">如果你使用 <xref:System.Threading.WaitHandle>，则在异步调用完成前后你可以执行其他处理，但必须在调用 `EndInvoke` 检索结果之前。</span><span class="sxs-lookup"><span data-stu-id="b0967-144">If you use a <xref:System.Threading.WaitHandle>, you can perform additional processing before or after the asynchronous call completes, but before calling `EndInvoke` to retrieve the results.</span></span>

> [!NOTE]
> <span data-ttu-id="b0967-145">调用 `EndInvoke`时不会自动关闭等待句柄。</span><span class="sxs-lookup"><span data-stu-id="b0967-145">The wait handle is not closed automatically when you call `EndInvoke`.</span></span> <span data-ttu-id="b0967-146">如果释放对等待句柄的所有引用，则当垃圾回收功能回收此等待句柄时将释放系统资源。</span><span class="sxs-lookup"><span data-stu-id="b0967-146">If you release all references to the wait handle, system resources are freed when garbage collection reclaims the wait handle.</span></span> <span data-ttu-id="b0967-147">要在使用完等待句柄后立即释放系统资源，请通过调用 <xref:System.Threading.WaitHandle.Close%2A?displayProperty=nameWithType> 方法来释放等待句柄。</span><span class="sxs-lookup"><span data-stu-id="b0967-147">To free the system resources as soon as you are finished using the wait handle, dispose of it by calling the <xref:System.Threading.WaitHandle.Close%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="b0967-148">显式释放可释放对象时，垃圾回收的工作效率更高。</span><span class="sxs-lookup"><span data-stu-id="b0967-148">Garbage collection works more efficiently when disposable objects are explicitly disposed.</span></span>

 [!code-cpp[AsyncDelegateExamples#3](../../../samples/snippets/cpp/VS_Snippets_CLR/AsyncDelegateExamples/cpp/waithandle.cpp#3)]
 [!code-csharp[AsyncDelegateExamples#3](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDelegateExamples/CS/waithandle.cs#3)]
 [!code-vb[AsyncDelegateExamples#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDelegateExamples/VB/WaitHandle.vb#3)]

## <a name="polling-for-asynchronous-call-completion"></a><span data-ttu-id="b0967-149">对异步调用的完成情况进行轮询</span><span class="sxs-lookup"><span data-stu-id="b0967-149">Polling for Asynchronous Call Completion</span></span>
 <span data-ttu-id="b0967-150">可以使用由 <xref:System.IAsyncResult.IsCompleted%2A> 返回的 <xref:System.IAsyncResult> 的 `BeginInvoke` 属性来发现异步调用何时完成。</span><span class="sxs-lookup"><span data-stu-id="b0967-150">You can use the <xref:System.IAsyncResult.IsCompleted%2A> property of the <xref:System.IAsyncResult> returned by `BeginInvoke` to discover when the asynchronous call completes.</span></span> <span data-ttu-id="b0967-151">从服务于用户界面的线程执行异步调用时需要执行此操作。</span><span class="sxs-lookup"><span data-stu-id="b0967-151">You might do this when making the asynchronous call from a thread that services the user interface.</span></span> <span data-ttu-id="b0967-152">对完成情况进行轮询允许在 <xref:System.Threading.ThreadPool> 线程中执行异步调用时继续执行调用线程。</span><span class="sxs-lookup"><span data-stu-id="b0967-152">Polling for completion allows the calling thread to continue executing while the asynchronous call executes on a <xref:System.Threading.ThreadPool> thread.</span></span>

 [!code-cpp[AsyncDelegateExamples#4](../../../samples/snippets/cpp/VS_Snippets_CLR/AsyncDelegateExamples/cpp/polling.cpp#4)]
 [!code-csharp[AsyncDelegateExamples#4](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDelegateExamples/CS/polling.cs#4)]
 [!code-vb[AsyncDelegateExamples#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDelegateExamples/VB/polling.vb#4)]

## <a name="executing-a-callback-method-when-an-asynchronous-call-completes"></a><span data-ttu-id="b0967-153">异步调用完成时执行回调方法</span><span class="sxs-lookup"><span data-stu-id="b0967-153">Executing a Callback Method When an Asynchronous Call Completes</span></span>
 <span data-ttu-id="b0967-154">如果启动异步调用的线程可以不是处理结果的线程，那么在调用完成时可以执行回调方法。</span><span class="sxs-lookup"><span data-stu-id="b0967-154">If the thread that initiates the asynchronous call does not need to be the thread that processes the results, you can execute a callback method when the call completes.</span></span> <span data-ttu-id="b0967-155">将在 <xref:System.Threading.ThreadPool> 线程上执行回调方法。</span><span class="sxs-lookup"><span data-stu-id="b0967-155">The callback method is executed on a <xref:System.Threading.ThreadPool> thread.</span></span>

 <span data-ttu-id="b0967-156">要使用回调方法，必须向 `BeginInvoke` 传递代表此回调方法的 <xref:System.AsyncCallback> 委托。</span><span class="sxs-lookup"><span data-stu-id="b0967-156">To use a callback method, you must pass `BeginInvoke` an <xref:System.AsyncCallback> delegate that represents the callback method.</span></span> <span data-ttu-id="b0967-157">你还可以传递包含此回调方法要使用的信息的对象。</span><span class="sxs-lookup"><span data-stu-id="b0967-157">You can also pass an object that contains information to be used by the callback method.</span></span> <span data-ttu-id="b0967-158">在回调方法中，可以将此回调方法的唯一参数 <xref:System.IAsyncResult>转换为 <xref:System.Runtime.Remoting.Messaging.AsyncResult> 对象。</span><span class="sxs-lookup"><span data-stu-id="b0967-158">In the callback method, you can cast the <xref:System.IAsyncResult>, which is the only parameter of the callback method, to an <xref:System.Runtime.Remoting.Messaging.AsyncResult> object.</span></span> <span data-ttu-id="b0967-159">然后使用 <xref:System.Runtime.Remoting.Messaging.AsyncResult.AsyncDelegate%2A?displayProperty=nameWithType> 属性获取用于启动调用的委托，以便可以调用 `EndInvoke`。</span><span class="sxs-lookup"><span data-stu-id="b0967-159">You can then use the <xref:System.Runtime.Remoting.Messaging.AsyncResult.AsyncDelegate%2A?displayProperty=nameWithType> property to get the delegate that was used to initiate the call so that you can call `EndInvoke`.</span></span>

 <span data-ttu-id="b0967-160">有关示例的注释：</span><span class="sxs-lookup"><span data-stu-id="b0967-160">Notes on the example:</span></span>

- <span data-ttu-id="b0967-161">`TestMethod` 的 `threadId` 参数为 `out` 参数（Visual Basic 中的 [`<Out>` `ByRef`），因此 `TestMethod` 从不使用它的输入值。</span><span class="sxs-lookup"><span data-stu-id="b0967-161">The `threadId` parameter of `TestMethod` is an `out` parameter ([`<Out>` `ByRef` in Visual Basic), so its input value is never used by `TestMethod`.</span></span> <span data-ttu-id="b0967-162">会将一个虚拟变量传递给 `BeginInvoke` 调用。</span><span class="sxs-lookup"><span data-stu-id="b0967-162">A dummy variable is passed to the `BeginInvoke` call.</span></span> <span data-ttu-id="b0967-163">如果 `threadId` 参数是 `ref` 参数（Visual Basic 中的`ByRef` ），那么此变量应为一个类级字段，以便可以将它传递给 `BeginInvoke` 和 `EndInvoke`。</span><span class="sxs-lookup"><span data-stu-id="b0967-163">If the `threadId` parameter were a `ref` parameter (`ByRef` in Visual Basic), the variable would have to be a class-level field so that it could be passed to both `BeginInvoke` and `EndInvoke`.</span></span>

- <span data-ttu-id="b0967-164">传递给 `BeginInvoke` 的状态信息是一个格式字符串，回调方法使用它来设置输出消息的格式。</span><span class="sxs-lookup"><span data-stu-id="b0967-164">The state information that is passed to `BeginInvoke` is a format string, which the callback method uses to format an output message.</span></span> <span data-ttu-id="b0967-165">因为该字符串是作为 <xref:System.Object>类型传递的，所以必须将此状态信息转换为适合的类型才可以使用。</span><span class="sxs-lookup"><span data-stu-id="b0967-165">Because it is passed as type <xref:System.Object>, the state information must be cast to its proper type before it can be used.</span></span>

- <span data-ttu-id="b0967-166">回调是在 <xref:System.Threading.ThreadPool> 线程上进行的。</span><span class="sxs-lookup"><span data-stu-id="b0967-166">The callback is made on a <xref:System.Threading.ThreadPool> thread.</span></span> <span data-ttu-id="b0967-167"><xref:System.Threading.ThreadPool> 线程是后台线程，当主线程结束时该线程不会使应用程序继续运行，因此该示例的主线程必须休眠足够长的时间以等待回调完成。</span><span class="sxs-lookup"><span data-stu-id="b0967-167"><xref:System.Threading.ThreadPool> threads are background threads, which do not keep the application running if the main thread ends, so the main thread of the example has to sleep long enough for the callback to finish.</span></span>

 [!code-cpp[AsyncDelegateExamples#5](../../../samples/snippets/cpp/VS_Snippets_CLR/AsyncDelegateExamples/cpp/callback.cpp#5)]
 [!code-csharp[AsyncDelegateExamples#5](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDelegateExamples/CS/callback.cs#5)]
 [!code-vb[AsyncDelegateExamples#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDelegateExamples/VB/callback.vb#5)]

## <a name="see-also"></a><span data-ttu-id="b0967-168">请参阅</span><span class="sxs-lookup"><span data-stu-id="b0967-168">See also</span></span>

- <xref:System.Delegate>
- [<span data-ttu-id="b0967-169">基于事件的异步模式 (EAP)</span><span class="sxs-lookup"><span data-stu-id="b0967-169">Event-based Asynchronous Pattern (EAP)</span></span>](event-based-asynchronous-pattern-eap.md)
