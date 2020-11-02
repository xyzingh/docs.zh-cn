---
title: 基于事件的异步模式概述
description: 了解 .NET 中基于事件的异步模式 (EAP)，它具有多线程应用程序的优点，并且可以简化部分设计。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET], asynchronous features
- AsyncOperation class
- AsyncCompletedEventArgs class
ms.assetid: 792aa8da-918b-458e-b154-9836b97735f3
ms.openlocfilehash: 5ab3229f71e264bbcd26d3d4c7bb52430b02865a
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888823"
---
# <a name="event-based-asynchronous-pattern-overview"></a><span data-ttu-id="817fa-103">基于事件的异步模式概述</span><span class="sxs-lookup"><span data-stu-id="817fa-103">Event-based Asynchronous Pattern Overview</span></span>
<span data-ttu-id="817fa-104">那些同时执行多项任务、但仍能响应用户交互的应用程序通常需要实施一种使用多线程的设计方案。</span><span class="sxs-lookup"><span data-stu-id="817fa-104">Applications that perform many tasks simultaneously, yet remain responsive to user interaction, often require a design that uses multiple threads.</span></span> <span data-ttu-id="817fa-105"><xref:System.Threading> 命名空间提供了创建高性能多线程应用程序所必需的所有工具，但要想有效地使用这些工具，需要有丰富的使用多线程软件工程的经验。</span><span class="sxs-lookup"><span data-stu-id="817fa-105">The <xref:System.Threading> namespace provides all the tools necessary to create high-performance multithreaded applications, but using these tools effectively requires significant experience with multithreaded software engineering.</span></span> <span data-ttu-id="817fa-106">对于相对简单的多线程应用程序，<xref:System.ComponentModel.BackgroundWorker> 组件提供了一个简单的解决方案。</span><span class="sxs-lookup"><span data-stu-id="817fa-106">For relatively simple multithreaded applications, the <xref:System.ComponentModel.BackgroundWorker> component provides a straightforward solution.</span></span> <span data-ttu-id="817fa-107">对于更复杂的异步应用程序，请考虑实现一个符合基于事件的异步模式的类。</span><span class="sxs-lookup"><span data-stu-id="817fa-107">For more sophisticated asynchronous applications, consider implementing a class that adheres to the Event-based Asynchronous Pattern.</span></span>  
  
 <span data-ttu-id="817fa-108">基于事件的异步模式具有多线程应用程序的优点，同时隐藏了多线程设计中固有的许多复杂问题。</span><span class="sxs-lookup"><span data-stu-id="817fa-108">The Event-based Asynchronous Pattern makes available the advantages of multithreaded applications while hiding many of the complex issues inherent in multithreaded design.</span></span> <span data-ttu-id="817fa-109">使用支持此模式的类，你将能够：</span><span class="sxs-lookup"><span data-stu-id="817fa-109">Using a class that supports this pattern can allow you to:</span></span>  
  
- <span data-ttu-id="817fa-110">“在后台”执行耗时任务（例如下载和数据库操作），但不会中断你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="817fa-110">Perform time-consuming tasks, such as downloads and database operations, "in the background," without interrupting your application.</span></span>  
  
- <span data-ttu-id="817fa-111">同时执行多个操作，每个操作完成时都会接到通知。</span><span class="sxs-lookup"><span data-stu-id="817fa-111">Execute multiple operations simultaneously, receiving notifications when each completes.</span></span>  
  
- <span data-ttu-id="817fa-112">等待资源变得可用，但不会停止（“阻止”）你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="817fa-112">Wait for resources to become available without stopping ("blocking") your application.</span></span>  
  
- <span data-ttu-id="817fa-113">使用熟悉的事件和委托模型与挂起的异步操作通信。</span><span class="sxs-lookup"><span data-stu-id="817fa-113">Communicate with pending asynchronous operations using the familiar events-and-delegates model.</span></span> <span data-ttu-id="817fa-114">若要详细了解如何使用事件处理程序和委托，请参阅[事件](../events/index.md)。</span><span class="sxs-lookup"><span data-stu-id="817fa-114">For more information on using event handlers and delegates, see [Events](../events/index.md).</span></span>  
  
 <span data-ttu-id="817fa-115">支持基于事件的异步模式的类将具有一个或多个命名为 _MethodName_**Async** 的方法。</span><span class="sxs-lookup"><span data-stu-id="817fa-115">A class that supports the Event-based Asynchronous Pattern will have one or more methods named _MethodName_**Async** .</span></span> <span data-ttu-id="817fa-116">这些方法可能会创建同步版本的镜像，这些同步版本会在当前线程上执行相同的操作。</span><span class="sxs-lookup"><span data-stu-id="817fa-116">These methods may mirror synchronous versions, which perform the same operation on the current thread.</span></span> <span data-ttu-id="817fa-117">该类还可能具有 _MethodName_**Completed** 事件，并且可能会具有 _MethodName_**AsyncCancel** （或只是 **CancelAsync** ）方法。</span><span class="sxs-lookup"><span data-stu-id="817fa-117">The class may also have a _MethodName_**Completed** event and it may have a _MethodName_**AsyncCancel** (or simply **CancelAsync** ) method.</span></span>  
  
 <span data-ttu-id="817fa-118"><xref:System.Windows.Forms.PictureBox> 是一个支持基于事件的异步模式的典型组件。</span><span class="sxs-lookup"><span data-stu-id="817fa-118"><xref:System.Windows.Forms.PictureBox> is a typical component that supports the Event-based Asynchronous Pattern.</span></span> <span data-ttu-id="817fa-119">你可以通过调用其 <xref:System.Windows.Forms.PictureBox.Load%2A> 方法来同步下载图像，但是如果图像很大，或者网络连接很慢，应用程序将停止响应，直到下载操作完成并且对 <xref:System.Windows.Forms.PictureBox.Load%2A> 的调用返回后才会继续执行。</span><span class="sxs-lookup"><span data-stu-id="817fa-119">You can download an image synchronously by calling its <xref:System.Windows.Forms.PictureBox.Load%2A> method, but if the image is large, or if the network connection is slow, your application will stop responding until the download operation is completed and the call to <xref:System.Windows.Forms.PictureBox.Load%2A> returns.</span></span>  
  
 <span data-ttu-id="817fa-120">如果你想要应用程序在加载图像时保持运行，你可以调用 <xref:System.Windows.Forms.PictureBox.LoadAsync%2A> 方法，处理 <xref:System.Windows.Forms.PictureBox.LoadCompleted> 事件，这与你处理任何其他事件一样。</span><span class="sxs-lookup"><span data-stu-id="817fa-120">If you want your application to keep running while the image is loading, you can call the <xref:System.Windows.Forms.PictureBox.LoadAsync%2A> method and handle the <xref:System.Windows.Forms.PictureBox.LoadCompleted> event, just as you would handle any other event.</span></span> <span data-ttu-id="817fa-121">调用 <xref:System.Windows.Forms.PictureBox.LoadAsync%2A> 方法时，你的应用程序将继续运行，而下载操作将在另一个线程上（“在后台”）继续。</span><span class="sxs-lookup"><span data-stu-id="817fa-121">When you call the <xref:System.Windows.Forms.PictureBox.LoadAsync%2A> method, your application will continue to run while the download proceeds on a separate thread ("in the background").</span></span> <span data-ttu-id="817fa-122">图像加载操作完成时，将调用你的事件处理程序，并且你的事件处理程序可以检查 <xref:System.ComponentModel.AsyncCompletedEventArgs> 参数以确定该下载是否已成功完成。</span><span class="sxs-lookup"><span data-stu-id="817fa-122">Your event handler will be called when the image-loading operation is complete, and your event handler can examine the <xref:System.ComponentModel.AsyncCompletedEventArgs> parameter to determine if the download completed successfully.</span></span>  
  
 <span data-ttu-id="817fa-123">基于事件的异步模式要求异步操作可以取消，并且 <xref:System.Windows.Forms.PictureBox> 控件使用其 <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> 方法支持此要求。</span><span class="sxs-lookup"><span data-stu-id="817fa-123">The Event-based Asynchronous Pattern requires that an asynchronous operation can be canceled, and the <xref:System.Windows.Forms.PictureBox> control supports this requirement with its <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> method.</span></span> <span data-ttu-id="817fa-124">调用 <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> 会提交一个停止挂起的下载的请求，任务取消时会引发 <xref:System.Windows.Forms.PictureBox.LoadCompleted> 事件。</span><span class="sxs-lookup"><span data-stu-id="817fa-124">Calling <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> submits a request to stop the pending download, and when the task is canceled, the <xref:System.Windows.Forms.PictureBox.LoadCompleted> event is raised.</span></span>  
  
> [!CAUTION]
> <span data-ttu-id="817fa-125">下载有可能刚好在发出 <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> 请求时完成，因此 <xref:System.ComponentModel.AsyncCompletedEventArgs.Cancelled%2A> 可能没有反映取消请求。</span><span class="sxs-lookup"><span data-stu-id="817fa-125">It is possible that the download will finish just as the <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> request is made, so <xref:System.ComponentModel.AsyncCompletedEventArgs.Cancelled%2A> may not reflect the request to cancel.</span></span> <span data-ttu-id="817fa-126">这称为“争用条件”，也是多线程编程中的常见问题。</span><span class="sxs-lookup"><span data-stu-id="817fa-126">This is called a *race condition* and is a common issue in multithreaded programming.</span></span> <span data-ttu-id="817fa-127">若要详细了解多线程编程中的问题，请参阅[托管线程最佳做法](../threading/managed-threading-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="817fa-127">For more information on issues in multithreaded programming, see [Managed Threading Best Practices](../threading/managed-threading-best-practices.md).</span></span>  
  
## <a name="characteristics-of-the-event-based-asynchronous-pattern"></a><span data-ttu-id="817fa-128">基于事件的异步模式的特征</span><span class="sxs-lookup"><span data-stu-id="817fa-128">Characteristics of the Event-based Asynchronous Pattern</span></span>  
 <span data-ttu-id="817fa-129">基于事件的异步模式可以采用多种形式，具体取决于某个特定类支持的操作的复杂程度。</span><span class="sxs-lookup"><span data-stu-id="817fa-129">The Event-based Asynchronous Pattern may take several forms, depending on the complexity of the operations supported by a particular class.</span></span> <span data-ttu-id="817fa-130">最简单的类可能包含一个 _MethodName_**Async** 方法和对应的 M _MethodName_**Completed** 事件。</span><span class="sxs-lookup"><span data-stu-id="817fa-130">The simplest classes may have a single _MethodName_**Async** method and a corresponding _MethodName_**Completed** event.</span></span> <span data-ttu-id="817fa-131">更复杂的类可能包含多个 _MethodName_**Async** 方法（每个方法具有一个对应的 _MethodName_**Completed** 事件），以及这些方法的同步版本。</span><span class="sxs-lookup"><span data-stu-id="817fa-131">More complex classes may have several _MethodName_**Async** methods, each with a corresponding _MethodName_**Completed** event, as well as synchronous versions of these methods.</span></span> <span data-ttu-id="817fa-132">这些类有选择性地分别支持各种异步方法的取消、进度报告和增量结果。</span><span class="sxs-lookup"><span data-stu-id="817fa-132">Classes can optionally support cancellation, progress reporting, and incremental results for each asynchronous method.</span></span>  
  
 <span data-ttu-id="817fa-133">异步方法可能还支持多个挂起的调用（多个并发调用），允许你的代码在此方法完成其他挂起的操作之前调用此方法任意多次。</span><span class="sxs-lookup"><span data-stu-id="817fa-133">An asynchronous method may also support multiple pending calls (multiple concurrent invocations), allowing your code to call it any number of times before it completes other pending operations.</span></span> <span data-ttu-id="817fa-134">若要正确处理此种情况，需要让你的应用程序能够跟踪各个操作的完成。</span><span class="sxs-lookup"><span data-stu-id="817fa-134">Correctly handling this situation may require your application to track the completion of each operation.</span></span>  
  
### <a name="examples-of-the-event-based-asynchronous-pattern"></a><span data-ttu-id="817fa-135">基于事件的异步模式示例</span><span class="sxs-lookup"><span data-stu-id="817fa-135">Examples of the Event-based Asynchronous Pattern</span></span>  
 <span data-ttu-id="817fa-136"><xref:System.Media.SoundPlayer> 和 <xref:System.Windows.Forms.PictureBox> 组件表示基于事件的异步模式的简单实现。</span><span class="sxs-lookup"><span data-stu-id="817fa-136">The <xref:System.Media.SoundPlayer> and <xref:System.Windows.Forms.PictureBox> components represent simple implementations of the Event-based Asynchronous Pattern.</span></span> <span data-ttu-id="817fa-137"><xref:System.Net.WebClient> 和 <xref:System.ComponentModel.BackgroundWorker> 组件表示基于事件的异步模式的更复杂实现。</span><span class="sxs-lookup"><span data-stu-id="817fa-137">The <xref:System.Net.WebClient> and <xref:System.ComponentModel.BackgroundWorker> components represent more complex implementations of the Event-based Asynchronous Pattern.</span></span>  
  
 <span data-ttu-id="817fa-138">下面是一个符合此模式的类声明示例：</span><span class="sxs-lookup"><span data-stu-id="817fa-138">Below is an example class declaration that conforms to the pattern:</span></span>  
  
```vb  
Public Class AsyncExample  
    ' Synchronous methods.  
    Public Function Method1(ByVal param As String) As Integer
    Public Sub Method2(ByVal param As Double)
  
    ' Asynchronous methods.  
    Overloads Public Sub Method1Async(ByVal param As String)
    Overloads Public Sub Method1Async(ByVal param As String, ByVal userState As Object)
    Public Event Method1Completed As Method1CompletedEventHandler  
  
    Overloads Public Sub Method2Async(ByVal param As Double)
    Overloads Public Sub Method2Async(ByVal param As Double, ByVal userState As Object)
    Public Event Method2Completed As Method2CompletedEventHandler  
  
    Public Sub CancelAsync(ByVal userState As Object)
  
    Public ReadOnly Property IsBusy () As Boolean  
  
    ' Class implementation not shown.  
End Class  
```  
  
```csharp  
public class AsyncExample  
{  
    // Synchronous methods.  
    public int Method1(string param);  
    public void Method2(double param);  
  
    // Asynchronous methods.  
    public void Method1Async(string param);  
    public void Method1Async(string param, object userState);  
    public event Method1CompletedEventHandler Method1Completed;  
  
    public void Method2Async(double param);  
    public void Method2Async(double param, object userState);  
    public event Method2CompletedEventHandler Method2Completed;  
  
    public void CancelAsync(object userState);  
  
    public bool IsBusy { get; }  
  
    // Class implementation not shown.  
}  
```  
  
 <span data-ttu-id="817fa-139">这里虚构的 `AsyncExample` 类有两个方法，都支持同步和异步调用。</span><span class="sxs-lookup"><span data-stu-id="817fa-139">The fictitious `AsyncExample` class has two methods, both of which support synchronous and asynchronous invocations.</span></span> <span data-ttu-id="817fa-140">同步重载的行为类似于方法调用，它们对调用线程执行操作；如果操作很耗时，则调用的返回可能会有明显的延迟。</span><span class="sxs-lookup"><span data-stu-id="817fa-140">The synchronous overloads behave like any method call and execute the operation on the calling thread; if the operation is time-consuming, there may be a noticeable delay before the call returns.</span></span> <span data-ttu-id="817fa-141">异步重载将在另一个线程上启动操作，然后立即返回，允许在调用线程继续执行的同时让操作“在后台”执行。</span><span class="sxs-lookup"><span data-stu-id="817fa-141">The asynchronous overloads will start the operation on another thread and then return immediately, allowing the calling thread to continue while the operation executes "in the background."</span></span>  
  
### <a name="asynchronous-method-overloads"></a><span data-ttu-id="817fa-142">异步方法重载</span><span class="sxs-lookup"><span data-stu-id="817fa-142">Asynchronous Method Overloads</span></span>  
 <span data-ttu-id="817fa-143">异步操作可以有两个重载：单调用和多调用。</span><span class="sxs-lookup"><span data-stu-id="817fa-143">There are potentially two overloads for the asynchronous operations: single-invocation and multiple-invocation.</span></span> <span data-ttu-id="817fa-144">你可以通过方法签名来区分这两种形式：多调用形式有一个额外的参数，即 `userState`。</span><span class="sxs-lookup"><span data-stu-id="817fa-144">You can distinguish these two forms by their method signatures: the multiple-invocation form has an extra parameter called `userState`.</span></span> <span data-ttu-id="817fa-145">使用这种形式，你的代码可以多次调用 `Method1Async(string param, object userState)`，而不必等待任何挂起的异步操作的完成。</span><span class="sxs-lookup"><span data-stu-id="817fa-145">This form makes it possible for your code to call `Method1Async(string param, object userState)` multiple times without waiting for any pending asynchronous operations to finish.</span></span> <span data-ttu-id="817fa-146">另一方面，如果你尝试在前一个调用尚未完成时调用 `Method1Async(string param)`，该方法将引发 <xref:System.InvalidOperationException>。</span><span class="sxs-lookup"><span data-stu-id="817fa-146">If, on the other hand, you try to call `Method1Async(string param)` before a previous invocation has completed, the method raises an <xref:System.InvalidOperationException>.</span></span>  
  
 <span data-ttu-id="817fa-147">多调用重载的 `userState` 参数可帮助你区分各个异步操作。</span><span class="sxs-lookup"><span data-stu-id="817fa-147">The `userState` parameter for the multiple-invocation overloads allows you to distinguish among asynchronous operations.</span></span> <span data-ttu-id="817fa-148">应分别为各个 `Method1Async(string param, object userState)` 调用提供唯一值（例如，GUID 或哈希代码）；这样，当各个操作完成时，事件处理程序便可以确定是哪个操作实例抛出了完成事件。</span><span class="sxs-lookup"><span data-stu-id="817fa-148">You provide a unique value (for example, a GUID or hash code) for each call to `Method1Async(string param, object userState)`, and when each operation is completed, your event handler can determine which instance of the operation raised the completion event.</span></span>  
  
### <a name="tracking-pending-operations"></a><span data-ttu-id="817fa-149">跟踪挂起的操作</span><span class="sxs-lookup"><span data-stu-id="817fa-149">Tracking Pending Operations</span></span>  
 <span data-ttu-id="817fa-150">如果你使用多调用重载，你的代码将需要跟踪挂起任务的 `userState` 对象（任务 ID）。</span><span class="sxs-lookup"><span data-stu-id="817fa-150">If you use the multiple-invocation overloads, your code will need to keep track of the `userState` objects (task IDs) for pending tasks.</span></span> <span data-ttu-id="817fa-151">对于各个 `Method1Async(string param, object userState)` 调用，通常会生成新的唯一 `userState` 对象，并将它添加到集合中。</span><span class="sxs-lookup"><span data-stu-id="817fa-151">For each call to `Method1Async(string param, object userState)`, you will typically generate a new, unique `userState` object and add it to a collection.</span></span> <span data-ttu-id="817fa-152">当对应于此 `userState` 对象的任务引发完成事件时，你的完成方法实现将检查 <xref:System.ComponentModel.AsyncCompletedEventArgs.UserState%2A?displayProperty=nameWithType> 并将此对象从集合中删除。</span><span class="sxs-lookup"><span data-stu-id="817fa-152">When the task corresponding to this `userState` object raises the completion event, your completion method implementation will examine <xref:System.ComponentModel.AsyncCompletedEventArgs.UserState%2A?displayProperty=nameWithType> and remove it from your collection.</span></span> <span data-ttu-id="817fa-153">在以这种方式使用时，`userState` 参数充当任务 ID 的角色。</span><span class="sxs-lookup"><span data-stu-id="817fa-153">Used this way, the `userState` parameter takes the role of a task ID.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="817fa-154">在为你对多调用重载的调用中的 `userState` 提供唯一值时，一定要小心。</span><span class="sxs-lookup"><span data-stu-id="817fa-154">You must be careful to provide a unique value for `userState` in your calls to multiple-invocation overloads.</span></span> <span data-ttu-id="817fa-155">如果任务 ID 不唯一，将导致异步类引发 <xref:System.ArgumentException>。</span><span class="sxs-lookup"><span data-stu-id="817fa-155">Non-unique task IDs will cause the asynchronous class throw an <xref:System.ArgumentException>.</span></span>  
  
### <a name="canceling-pending-operations"></a><span data-ttu-id="817fa-156">取消挂起的操作</span><span class="sxs-lookup"><span data-stu-id="817fa-156">Canceling Pending Operations</span></span>  
 <span data-ttu-id="817fa-157">我们必须能够在异步操作完成之前随时取消它们，这一点很重要。</span><span class="sxs-lookup"><span data-stu-id="817fa-157">It is important to be able to cancel asynchronous operations at any time before their completion.</span></span> <span data-ttu-id="817fa-158">实现基于事件的异步模式的类包含 `CancelAsync` 方法（如果只有一个异步方法），或 _MethodName_**AsyncCancel** 方法（如果有多个异步方法）。</span><span class="sxs-lookup"><span data-stu-id="817fa-158">Classes that implement the Event-based Asynchronous Pattern will have a `CancelAsync` method (if there is only one asynchronous method) or a _MethodName_**AsyncCancel** method (if there are multiple asynchronous methods).</span></span>  
  
 <span data-ttu-id="817fa-159">允许多个调用采用 `userState` 参数的方法，此类方法可用于跟踪每个任务的生存期。</span><span class="sxs-lookup"><span data-stu-id="817fa-159">Methods that allow multiple invocations take a `userState` parameter, which can be used to track the lifetime of each task.</span></span> <span data-ttu-id="817fa-160">`CancelAsync` 采用 `userState` 参数，该参数可用于取消特定挂起任务。</span><span class="sxs-lookup"><span data-stu-id="817fa-160">`CancelAsync` takes a `userState` parameter, which allows you to cancel particular pending tasks.</span></span>  
  
 <span data-ttu-id="817fa-161">一次只支持一个挂起操作的方法（如 `Method1Async(string param)`）是不可取消的。</span><span class="sxs-lookup"><span data-stu-id="817fa-161">Methods that support only a single pending operation at a time, like `Method1Async(string param)`, are not cancelable.</span></span>  
  
### <a name="receiving-progress-updates-and-incremental-results"></a><span data-ttu-id="817fa-162">接收进度更新和增量结果</span><span class="sxs-lookup"><span data-stu-id="817fa-162">Receiving Progress Updates and Incremental Results</span></span>  
 <span data-ttu-id="817fa-163">符合基于事件的异步模式的类可以为跟踪进度和增量结果提供事件。</span><span class="sxs-lookup"><span data-stu-id="817fa-163">A class that adheres to the Event-based Asynchronous Pattern may optionally provide an event for tracking progress and incremental results.</span></span> <span data-ttu-id="817fa-164">此事件通常命名为 `ProgressChanged` 或 _MethodName_**ProgressChanged** ，其对应的事件处理程序将使用 <xref:System.ComponentModel.ProgressChangedEventArgs> 参数。</span><span class="sxs-lookup"><span data-stu-id="817fa-164">This will typically be named `ProgressChanged` or _MethodName_**ProgressChanged** , and its corresponding event handler will take a <xref:System.ComponentModel.ProgressChangedEventArgs> parameter.</span></span>  
  
 <span data-ttu-id="817fa-165">`ProgressChanged` 事件的事件处理程序可以检查 <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A?displayProperty=nameWithType> 属性，以确定异步任务完成百分比。</span><span class="sxs-lookup"><span data-stu-id="817fa-165">The event handler for the `ProgressChanged` event can examine the <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A?displayProperty=nameWithType> property to determine what percentage of an asynchronous task has been completed.</span></span> <span data-ttu-id="817fa-166">此属性的范围是 0 到 100，可用来更新 <xref:System.Windows.Forms.ProgressBar.Value%2A> 的 <xref:System.Windows.Forms.ProgressBar> 属性。</span><span class="sxs-lookup"><span data-stu-id="817fa-166">This property will range from 0 to 100, and it can be used to update the <xref:System.Windows.Forms.ProgressBar.Value%2A> property of a <xref:System.Windows.Forms.ProgressBar>.</span></span> <span data-ttu-id="817fa-167">如果有多个异步操作挂起，你可以使用 <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A?displayProperty=nameWithType> 属性来分辨出哪个操作在报告进度。</span><span class="sxs-lookup"><span data-stu-id="817fa-167">If multiple asynchronous operations are pending, you can use the <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A?displayProperty=nameWithType> property to distinguish which operation is reporting progress.</span></span>  
  
 <span data-ttu-id="817fa-168">一些类可能会在异步操作继续时报告增量结果。</span><span class="sxs-lookup"><span data-stu-id="817fa-168">Some classes may report incremental results as asynchronous operations proceed.</span></span> <span data-ttu-id="817fa-169">这些结果将存储在从 <xref:System.ComponentModel.ProgressChangedEventArgs> 派生的类中并显示为此派生类中的属性。</span><span class="sxs-lookup"><span data-stu-id="817fa-169">These results will be stored in a class that derives from <xref:System.ComponentModel.ProgressChangedEventArgs> and they will appear as properties in the derived class.</span></span> <span data-ttu-id="817fa-170">你可以在 `ProgressChanged` 事件的事件处理程序中访问这些结果，就像访问 <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A> 属性一样。</span><span class="sxs-lookup"><span data-stu-id="817fa-170">You can access these results in the event handler for the `ProgressChanged` event, just as you would access the <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A> property.</span></span> <span data-ttu-id="817fa-171">如果有多个异步操作挂起，你可以使用 <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A> 属性来分辨出哪个操作在报告增量结果。</span><span class="sxs-lookup"><span data-stu-id="817fa-171">If multiple asynchronous operations are pending, you can use the <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A> property to distinguish which operation is reporting incremental results.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="817fa-172">请参阅</span><span class="sxs-lookup"><span data-stu-id="817fa-172">See also</span></span>

- <xref:System.ComponentModel.ProgressChangedEventArgs>
- <xref:System.ComponentModel.BackgroundWorker>
- <xref:System.ComponentModel.AsyncCompletedEventArgs>
- [<span data-ttu-id="817fa-173">如何：使用支持基于事件的异步模式的组件</span><span class="sxs-lookup"><span data-stu-id="817fa-173">How to: Use Components That Support the Event-based Asynchronous Pattern</span></span>](how-to-use-components-that-support-the-event-based-asynchronous-pattern.md)
- [<span data-ttu-id="817fa-174">如何：在后台运行操作</span><span class="sxs-lookup"><span data-stu-id="817fa-174">How to: Run an Operation in the Background</span></span>](/dotnet/desktop/winforms/controls/how-to-run-an-operation-in-the-background)
- [<span data-ttu-id="817fa-175">如何：实现使用后台操作的窗体</span><span class="sxs-lookup"><span data-stu-id="817fa-175">How to: Implement a Form That Uses a Background Operation</span></span>](/dotnet/desktop/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation)
- [<span data-ttu-id="817fa-176">基于事件的异步模式 (EAP)</span><span class="sxs-lookup"><span data-stu-id="817fa-176">Event-based Asynchronous Pattern (EAP)</span></span>](event-based-asynchronous-pattern-eap.md)
- [<span data-ttu-id="817fa-177">实现基于事件的异步模式的最佳做法</span><span class="sxs-lookup"><span data-stu-id="817fa-177">Best Practices for Implementing the Event-based Asynchronous Pattern</span></span>](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)
- [<span data-ttu-id="817fa-178">确定何时实现基于事件的异步模式</span><span class="sxs-lookup"><span data-stu-id="817fa-178">Deciding When to Implement the Event-based Asynchronous Pattern</span></span>](deciding-when-to-implement-the-event-based-asynchronous-pattern.md)
