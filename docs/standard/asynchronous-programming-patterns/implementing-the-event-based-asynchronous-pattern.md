---
title: 实现基于事件的异步模式
description: 了解如何在 .NET 中实现基于事件的异步模式 (EAP)。 EAP 是打包具有异步功能的类的标准方式。
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
- components [.NET], asynchronous
- AsyncOperation class
- AsyncCompletedEventArgs class
ms.assetid: 43402d19-8d30-426d-8785-1a4478233bfa
ms.openlocfilehash: ca4b1b3ff1fb7180250de7436db9a4d642e8118c
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888784"
---
# <a name="implementing-the-event-based-asynchronous-pattern"></a><span data-ttu-id="166b1-104">实现基于事件的异步模式</span><span class="sxs-lookup"><span data-stu-id="166b1-104">Implementing the Event-based Asynchronous Pattern</span></span>

<span data-ttu-id="166b1-105">如果要编写的类有一些可能会带来明显延迟的操作，请考虑按照[基于事件的异步模式](event-based-asynchronous-pattern-overview.md)中的步骤操作，为它实现异步功能。</span><span class="sxs-lookup"><span data-stu-id="166b1-105">If you are writing a class with some operations that may incur noticeable delays, consider giving it asynchronous functionality by implementing the [Event-based Asynchronous Pattern](event-based-asynchronous-pattern-overview.md).</span></span>

<span data-ttu-id="166b1-106">基于事件的异步模式提供了打包具有异步功能的类的标准化方式。</span><span class="sxs-lookup"><span data-stu-id="166b1-106">The Event-based Asynchronous Pattern provides a standardized way to package a class that has asynchronous features.</span></span> <span data-ttu-id="166b1-107">如果使用帮助程序类（如 <xref:System.ComponentModel.AsyncOperationManager>）进行实现，类可以在任何应用模型（包括 ASP.NET、控制台应用和 Windows 窗体应用）下正常运行。</span><span class="sxs-lookup"><span data-stu-id="166b1-107">If implemented with helper classes like <xref:System.ComponentModel.AsyncOperationManager>, your class will work correctly under any application model, including ASP.NET, Console applications, and Windows Forms applications.</span></span>

<span data-ttu-id="166b1-108">有关实现基于事件的异步模式的示例，请参阅[如何：实现支持基于事件的异步模式的组件](component-that-supports-the-event-based-asynchronous-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="166b1-108">For an example that implements the Event-based Asynchronous Pattern, see [How to: Implement a Component That Supports the Event-based Asynchronous Pattern](component-that-supports-the-event-based-asynchronous-pattern.md).</span></span>

<span data-ttu-id="166b1-109">对于简单的异步操作，可能会发现 <xref:System.ComponentModel.BackgroundWorker> 组件非常适合。</span><span class="sxs-lookup"><span data-stu-id="166b1-109">For simple asynchronous operations, you may find the <xref:System.ComponentModel.BackgroundWorker> component suitable.</span></span> <span data-ttu-id="166b1-110">有关 <xref:System.ComponentModel.BackgroundWorker> 的详细信息，请参阅[如何：在后台运行操作](/dotnet/desktop/winforms/controls/how-to-run-an-operation-in-the-background)。</span><span class="sxs-lookup"><span data-stu-id="166b1-110">For more information about <xref:System.ComponentModel.BackgroundWorker>, see [How to: Run an Operation in the Background](/dotnet/desktop/winforms/controls/how-to-run-an-operation-in-the-background).</span></span>

<span data-ttu-id="166b1-111">以下列表介绍本主题中讨论的基于事件的异步模式的功能。</span><span class="sxs-lookup"><span data-stu-id="166b1-111">The following list describes the features of the Event-based Asynchronous Pattern discussed in this topic.</span></span>

- <span data-ttu-id="166b1-112">实现基于事件的异步模式的时机</span><span class="sxs-lookup"><span data-stu-id="166b1-112">Opportunities for Implementing the Event-based Asynchronous Pattern</span></span>

- <span data-ttu-id="166b1-113">命名异步方法</span><span class="sxs-lookup"><span data-stu-id="166b1-113">Naming Asynchronous Methods</span></span>

- <span data-ttu-id="166b1-114">选择性地支持取消</span><span class="sxs-lookup"><span data-stu-id="166b1-114">Optionally Support Cancellation</span></span>

- <span data-ttu-id="166b1-115">选择性地支持 IsBusy 属性</span><span class="sxs-lookup"><span data-stu-id="166b1-115">Optionally Support the IsBusy Property</span></span>

- <span data-ttu-id="166b1-116">选择性地为进度报告提供支持</span><span class="sxs-lookup"><span data-stu-id="166b1-116">Optionally Provide Support for Progress Reporting</span></span>

- <span data-ttu-id="166b1-117">选择性地为返回增量结果提供支持</span><span class="sxs-lookup"><span data-stu-id="166b1-117">Optionally Provide Support for Returning Incremental Results</span></span>

- <span data-ttu-id="166b1-118">处理方法中的 Out 和 Ref 参数</span><span class="sxs-lookup"><span data-stu-id="166b1-118">Handling Out and Ref Parameters in Methods</span></span>

## <a name="opportunities-for-implementing-the-event-based-asynchronous-pattern"></a><span data-ttu-id="166b1-119">实现基于事件的异步模式的时机</span><span class="sxs-lookup"><span data-stu-id="166b1-119">Opportunities for Implementing the Event-based Asynchronous Pattern</span></span>

<span data-ttu-id="166b1-120">请在以下情况下，考虑实现基于事件的异步模式：</span><span class="sxs-lookup"><span data-stu-id="166b1-120">Consider implementing the Event-based Asynchronous Pattern when:</span></span>

- <span data-ttu-id="166b1-121">类的客户端不需要适用于异步操作的 <xref:System.Threading.WaitHandle> 和 <xref:System.IAsyncResult> 对象。也就是说，客户端需要生成轮询和 <xref:System.Threading.WaitHandle.WaitAll%2A> 或 <xref:System.Threading.WaitHandle.WaitAny%2A>。</span><span class="sxs-lookup"><span data-stu-id="166b1-121">Clients of your class do not need <xref:System.Threading.WaitHandle> and <xref:System.IAsyncResult> objects available for asynchronous operations, meaning that polling and <xref:System.Threading.WaitHandle.WaitAll%2A> or <xref:System.Threading.WaitHandle.WaitAny%2A> will need to be built up by the client.</span></span>

- <span data-ttu-id="166b1-122">你希望异步操作由客户端使用常见的事件/委托模型进行托管。</span><span class="sxs-lookup"><span data-stu-id="166b1-122">You want asynchronous operations to be managed by the client with the familiar event/delegate model.</span></span>

<span data-ttu-id="166b1-123">对于异步实现，任何操作都是候选项，但应优先考虑预计会产生较长延迟的操作。</span><span class="sxs-lookup"><span data-stu-id="166b1-123">Any operation is a candidate for an asynchronous implementation, but those you expect to incur long latencies should be considered.</span></span> <span data-ttu-id="166b1-124">最适合的操作是客户端在其中调用方法，并在完成时收到通知，无需进一步的干预。</span><span class="sxs-lookup"><span data-stu-id="166b1-124">Especially appropriate are operations in which clients call a method and are notified on completion, with no further intervention required.</span></span> <span data-ttu-id="166b1-125">其次是连续运行、定期向客户端通知进度、增量结果和状态更改的操作。</span><span class="sxs-lookup"><span data-stu-id="166b1-125">Also appropriate are operations which run continuously, periodically notifying clients of progress, incremental results, or state changes.</span></span>

<span data-ttu-id="166b1-126">若要深入了解决定何时支持基于事件的异步模式，请参阅[决定何时实现基于事件的异步模式](deciding-when-to-implement-the-event-based-asynchronous-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="166b1-126">For more information on deciding when to support the Event-based Asynchronous Pattern, see [Deciding When to Implement the Event-based Asynchronous Pattern](deciding-when-to-implement-the-event-based-asynchronous-pattern.md).</span></span>

## <a name="naming-asynchronous-methods"></a><span data-ttu-id="166b1-127">命名异步方法</span><span class="sxs-lookup"><span data-stu-id="166b1-127">Naming Asynchronous Methods</span></span>

<span data-ttu-id="166b1-128">对于要向其提供异步等效方法的每个同步方法 *MethodName* ：</span><span class="sxs-lookup"><span data-stu-id="166b1-128">For each synchronous method *MethodName* for which you want to provide an asynchronous counterpart:</span></span>

<span data-ttu-id="166b1-129">定义满足以下条件的 MethodNameAsync 方法：</span><span class="sxs-lookup"><span data-stu-id="166b1-129">Define a _MethodName_**Async** method that:</span></span>

- <span data-ttu-id="166b1-130">返回 `void`。</span><span class="sxs-lookup"><span data-stu-id="166b1-130">Returns `void`.</span></span>

- <span data-ttu-id="166b1-131">采用与 *MethodName* 方法相同的参数。</span><span class="sxs-lookup"><span data-stu-id="166b1-131">Takes the same parameters as the *MethodName* method.</span></span>

- <span data-ttu-id="166b1-132">接受多个调用。</span><span class="sxs-lookup"><span data-stu-id="166b1-132">Accepts multiple invocations.</span></span>

<span data-ttu-id="166b1-133">（可选）定义与 MethodNameAsync 完全相同的 MethodNameAsync 重载，但要额外添加对象赋值参数（即 `userState`）。</span><span class="sxs-lookup"><span data-stu-id="166b1-133">Optionally define a _MethodName_**Async** overload, identical to _MethodName_**Async** , but with an additional object-valued parameter called `userState`.</span></span> <span data-ttu-id="166b1-134">如果已准备好管理方法的多个并发调用（在这种情况下，`userState` 值将传递回所有事件处理程序以区分方法的调用），可使用此方法。</span><span class="sxs-lookup"><span data-stu-id="166b1-134">Do this if you're prepared to manage multiple concurrent invocations of your method, in which case the `userState` value will be delivered back to all event handlers to distinguish invocations of the method.</span></span> <span data-ttu-id="166b1-135">也可以选择将其简单地作为存储用户状态以供以后检索的位置。</span><span class="sxs-lookup"><span data-stu-id="166b1-135">You may also choose to do this simply as a place to store user state for later retrieval.</span></span>

<span data-ttu-id="166b1-136">对于各个 MethodNameAsync 方法签名：</span><span class="sxs-lookup"><span data-stu-id="166b1-136">For each separate _MethodName_**Async** method signature:</span></span>

1. <span data-ttu-id="166b1-137">在与方法相同的类中定义以下事件：</span><span class="sxs-lookup"><span data-stu-id="166b1-137">Define the following event in the same class as the method:</span></span>

    ```vb
    Public Event MethodNameCompleted As MethodNameCompletedEventHandler
    ```

    ```csharp
    public event MethodNameCompletedEventHandler MethodNameCompleted;
    ```

2. <span data-ttu-id="166b1-138">定义以下委托和 <xref:System.ComponentModel.AsyncCompletedEventArgs>。</span><span class="sxs-lookup"><span data-stu-id="166b1-138">Define the following delegate and <xref:System.ComponentModel.AsyncCompletedEventArgs>.</span></span> <span data-ttu-id="166b1-139">这些可能会在类本身之外、但在相同命名空间中定义。</span><span class="sxs-lookup"><span data-stu-id="166b1-139">These will likely be defined outside of the class itself, but in the same namespace.</span></span>

    ```vb
    Public Delegate Sub MethodNameCompletedEventHandler( _
        ByVal sender As Object, _
        ByVal e As MethodNameCompletedEventArgs)

    Public Class MethodNameCompletedEventArgs
        Inherits System.ComponentModel.AsyncCompletedEventArgs
    Public ReadOnly Property Result() As MyReturnType
    End Property
    ```

    ```csharp
    public delegate void MethodNameCompletedEventHandler(object sender,
        MethodNameCompletedEventArgs e);

    public class MethodNameCompletedEventArgs : System.ComponentModel.AsyncCompletedEventArgs
    {
        public MyReturnType Result { get; }
    }
    ```

    - <span data-ttu-id="166b1-140">请确保 MethodNameCompletedEventArgs 类将它的成员公开为只读属性（而不是字段），因为字段会阻止数据绑定。</span><span class="sxs-lookup"><span data-stu-id="166b1-140">Ensure that the _MethodName_**CompletedEventArgs** class exposes its members as read-only properties, and not fields, as fields prevent data binding.</span></span>

    - <span data-ttu-id="166b1-141">请勿为不产生结果的方法定义任何派生自 <xref:System.ComponentModel.AsyncCompletedEventArgs> 的类。</span><span class="sxs-lookup"><span data-stu-id="166b1-141">Do not define any <xref:System.ComponentModel.AsyncCompletedEventArgs>-derived classes for methods that do not produce results.</span></span> <span data-ttu-id="166b1-142">直接使用 <xref:System.ComponentModel.AsyncCompletedEventArgs> 本身的实例即可。</span><span class="sxs-lookup"><span data-stu-id="166b1-142">Simply use an instance of <xref:System.ComponentModel.AsyncCompletedEventArgs> itself.</span></span>

      > [!NOTE]
      > <span data-ttu-id="166b1-143">在可行且适当的情况下，重用委托和 <xref:System.ComponentModel.AsyncCompletedEventArgs> 类型是完全可以接受的。</span><span class="sxs-lookup"><span data-stu-id="166b1-143">It is perfectly acceptable, when feasible and appropriate, to reuse delegate and <xref:System.ComponentModel.AsyncCompletedEventArgs> types.</span></span> <span data-ttu-id="166b1-144">在这种情况下，命名会与方法名称不一致，因为给定委托和 <xref:System.ComponentModel.AsyncCompletedEventArgs> 不限于单个方法。</span><span class="sxs-lookup"><span data-stu-id="166b1-144">In this case, the naming will not be as consistent with the method name, since a given delegate and <xref:System.ComponentModel.AsyncCompletedEventArgs> won't be tied to a single method.</span></span>

## <a name="optionally-support-cancellation"></a><span data-ttu-id="166b1-145">选择性地支持取消</span><span class="sxs-lookup"><span data-stu-id="166b1-145">Optionally Support Cancellation</span></span>

<span data-ttu-id="166b1-146">如果你的类将支持取消异步操作，则应向客户端公开取消（如下所述）。</span><span class="sxs-lookup"><span data-stu-id="166b1-146">If your class will support canceling asynchronous operations, cancellation should be exposed to the client as described below.</span></span> <span data-ttu-id="166b1-147">请注意，定义取消支持之前，需要确定两点：</span><span class="sxs-lookup"><span data-stu-id="166b1-147">Note that there are two decision points that need to be reached before defining your cancellation support:</span></span>

- <span data-ttu-id="166b1-148">你的类（包括将来预计要添加的内容），是否只具有一个支持取消操作的异步操作？</span><span class="sxs-lookup"><span data-stu-id="166b1-148">Does your class, including future anticipated additions to it, have only one asynchronous operation that supports cancellation?</span></span>

- <span data-ttu-id="166b1-149">支持取消的异步操作是否能支持多个挂起操作？</span><span class="sxs-lookup"><span data-stu-id="166b1-149">Can the asynchronous operations that support cancellation support multiple pending operations?</span></span> <span data-ttu-id="166b1-150">也就是说，MethodNameAsync 方法是否需要使用 `userState` 参数？它是否允许在等待任何操作完成前执行多个调用？</span><span class="sxs-lookup"><span data-stu-id="166b1-150">That is, does the _MethodName_**Async** method take a `userState` parameter, and does it allow multiple invocations before waiting for any to finish?</span></span>

<span data-ttu-id="166b1-151">使用下表中的两个问题的答案来确定取消方法的签名。</span><span class="sxs-lookup"><span data-stu-id="166b1-151">Use the answers to these two questions in the table below to determine what the signature for your cancellation method should be.</span></span>

### <a name="visual-basic"></a><span data-ttu-id="166b1-152">Visual Basic</span><span class="sxs-lookup"><span data-stu-id="166b1-152">Visual Basic</span></span>

||<span data-ttu-id="166b1-153">支持多个并行操作</span><span class="sxs-lookup"><span data-stu-id="166b1-153">Multiple Simultaneous Operations Supported</span></span>|<span data-ttu-id="166b1-154">每次一个操作</span><span class="sxs-lookup"><span data-stu-id="166b1-154">Only One Operation at a Time</span></span>|
|------|------------------------------------------------|----------------------------------|
|<span data-ttu-id="166b1-155">整个类中具有一个异步操作</span><span class="sxs-lookup"><span data-stu-id="166b1-155">One Async Operation in entire class</span></span>|`Sub MethodNameAsyncCancel(ByVal userState As Object)`|`Sub MethodNameAsyncCancel()`|
|<span data-ttu-id="166b1-156">类中具有多个异步操作</span><span class="sxs-lookup"><span data-stu-id="166b1-156">Multiple Async Operations in class</span></span>|`Sub CancelAsync(ByVal userState As Object)`|`Sub CancelAsync()`|

### <a name="c"></a><span data-ttu-id="166b1-157">C\#</span><span class="sxs-lookup"><span data-stu-id="166b1-157">C\#</span></span>

||<span data-ttu-id="166b1-158">支持多个并行操作</span><span class="sxs-lookup"><span data-stu-id="166b1-158">Multiple Simultaneous Operations Supported</span></span>|<span data-ttu-id="166b1-159">每次一个操作</span><span class="sxs-lookup"><span data-stu-id="166b1-159">Only One Operation at a Time</span></span>|
|------|------------------------------------------------|----------------------------------|
|<span data-ttu-id="166b1-160">整个类中具有一个异步操作</span><span class="sxs-lookup"><span data-stu-id="166b1-160">One Async Operation in entire class</span></span>|`void MethodNameAsyncCancel(object userState);`|`void MethodNameAsyncCancel();`|
|<span data-ttu-id="166b1-161">类中具有多个异步操作</span><span class="sxs-lookup"><span data-stu-id="166b1-161">Multiple Async Operations in class</span></span>|`void CancelAsync(object userState);`|`void CancelAsync();`|

<span data-ttu-id="166b1-162">如果定义了 `CancelAsync(object userState)` 方法，客户端在选择状态值时必须小心，以使其能够区分对象上调用的所有异步方法，而不仅仅是在单个异步方法的所有调用之间进行区分。</span><span class="sxs-lookup"><span data-stu-id="166b1-162">If you define the `CancelAsync(object userState)` method, clients must be careful when choosing their state values to make them capable of distinguishing among all asynchronous methods invoked on the object, and not just between all invocations of a single asynchronous method.</span></span>

<span data-ttu-id="166b1-163">决定命名单一异步操作版本 MethodNameAsyncCancel 的依据是，能否在设计环境（如 Visual Studio 的 IntelliSense）中更轻松地发现方法。</span><span class="sxs-lookup"><span data-stu-id="166b1-163">The decision to name the single-async-operation version _MethodName_**AsyncCancel** is based on being able to more easily discover the method in a design environment like Visual Studio's IntelliSense.</span></span> <span data-ttu-id="166b1-164">这会对相关的成员进行分组，将与异步功能无关的其他成员区分开来。</span><span class="sxs-lookup"><span data-stu-id="166b1-164">This groups the related members and distinguishes them from other members that have nothing to do with asynchronous functionality.</span></span> <span data-ttu-id="166b1-165">如果预计可能在后续版本中添加其他异步操作，最好定义 `CancelAsync`。</span><span class="sxs-lookup"><span data-stu-id="166b1-165">If you expect that there may be additional asynchronous operations added in subsequent versions, it is better to define `CancelAsync`.</span></span>

<span data-ttu-id="166b1-166">请勿在同一类中定义上表中的多个方法。</span><span class="sxs-lookup"><span data-stu-id="166b1-166">Do not define multiple methods from the table above in the same class.</span></span> <span data-ttu-id="166b1-167">这将毫无意义，或者会由于方法的泛滥而使类接口变得混乱。</span><span class="sxs-lookup"><span data-stu-id="166b1-167">That will not make sense, or it will clutter the class interface with a proliferation of methods.</span></span>

<span data-ttu-id="166b1-168">通常，这些方法会立即返回，并且操作实际上可能会/无法取消。</span><span class="sxs-lookup"><span data-stu-id="166b1-168">These methods typically will return immediately, and the operation may or may not actually cancel.</span></span> <span data-ttu-id="166b1-169">在 MethodNameCompleted 事件的事件处理程序中，MethodNameCompletedEventArgs 对象包含 `Cancelled` 字段，客户端可使用此字段来确定是否取消了操作。</span><span class="sxs-lookup"><span data-stu-id="166b1-169">In the event handler for the _MethodName_**Completed** event, the _MethodName_**CompletedEventArgs** object contains a `Cancelled` field, which clients can use to determine whether the cancellation occurred.</span></span>

<span data-ttu-id="166b1-170">请遵守[实现基于事件的异步模式的最佳做法](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)中所述的取消语义。</span><span class="sxs-lookup"><span data-stu-id="166b1-170">Abide by the cancellation semantics described in [Best Practices for Implementing the Event-based Asynchronous Pattern](best-practices-for-implementing-the-event-based-asynchronous-pattern.md).</span></span>

## <a name="optionally-support-the-isbusy-property"></a><span data-ttu-id="166b1-171">选择性地支持 IsBusy 属性</span><span class="sxs-lookup"><span data-stu-id="166b1-171">Optionally Support the IsBusy Property</span></span>

<span data-ttu-id="166b1-172">如果你的类不支持多个并发调用，请考虑公开 `IsBusy` 属性。</span><span class="sxs-lookup"><span data-stu-id="166b1-172">If your class does not support multiple concurrent invocations, consider exposing an `IsBusy` property.</span></span> <span data-ttu-id="166b1-173">这样一来，开发人员可以确定能否运行 MethodNameAsync 方法，同时又不会捕获到 MethodNameAsync 方法抛出的异常。</span><span class="sxs-lookup"><span data-stu-id="166b1-173">This allows developers to determine whether a _MethodName_**Async** method is running without catching an exception from the _MethodName_**Async** method.</span></span>

<span data-ttu-id="166b1-174">请遵守[实现基于事件的异步模式的最佳做法](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)中所述的 `IsBusy` 语义。</span><span class="sxs-lookup"><span data-stu-id="166b1-174">Abide by the `IsBusy` semantics described in [Best Practices for Implementing the Event-based Asynchronous Pattern](best-practices-for-implementing-the-event-based-asynchronous-pattern.md).</span></span>

## <a name="optionally-provide-support-for-progress-reporting"></a><span data-ttu-id="166b1-175">选择性地为进度报告提供支持</span><span class="sxs-lookup"><span data-stu-id="166b1-175">Optionally Provide Support for Progress Reporting</span></span>

<span data-ttu-id="166b1-176">通常期望异步操作在其操作期间报告进度。</span><span class="sxs-lookup"><span data-stu-id="166b1-176">It is frequently desirable for an asynchronous operation to report progress during its operation.</span></span> <span data-ttu-id="166b1-177">基于事件的异步模式提供了执行此操作的准则。</span><span class="sxs-lookup"><span data-stu-id="166b1-177">The Event-based Asynchronous Pattern provides a guideline for doing so.</span></span>

- <span data-ttu-id="166b1-178">还可以选择性地定义由异步操作引发并在相应线程上调用的事件。</span><span class="sxs-lookup"><span data-stu-id="166b1-178">Optionally define an event to be raised by the asynchronous operation and invoked on the appropriate thread.</span></span> <span data-ttu-id="166b1-179"><xref:System.ComponentModel.ProgressChangedEventArgs> 对象随附整数值进度指示器，量程预计在 0 到 100 之间。</span><span class="sxs-lookup"><span data-stu-id="166b1-179">The <xref:System.ComponentModel.ProgressChangedEventArgs> object carries an integer-valued progress indicator that is expected to be between 0 and 100.</span></span>

- <span data-ttu-id="166b1-180">按照以下规则命名此事件：</span><span class="sxs-lookup"><span data-stu-id="166b1-180">Name this event as follows:</span></span>

  - <span data-ttu-id="166b1-181">如果类具有多个异步操作（或预期将来版本中会包括多个异步操作），则命名为 `ProgressChanged`；</span><span class="sxs-lookup"><span data-stu-id="166b1-181">`ProgressChanged` if the class has multiple asynchronous operations (or is expected to grow to include multiple asynchronous operations in future versions);</span></span>

  - <span data-ttu-id="166b1-182">MethodNameProgressChanged：如果类包含单一异步操作。</span><span class="sxs-lookup"><span data-stu-id="166b1-182">_MethodName_**ProgressChanged** if the class has a single asynchronous operation.</span></span>

  <span data-ttu-id="166b1-183">该命名方法与命名取消方法（如“选择性地支持取消”部分所述）相同。</span><span class="sxs-lookup"><span data-stu-id="166b1-183">This naming choice parallels that made for the cancellation method, as described in the Optionally Support Cancellation section.</span></span>

<span data-ttu-id="166b1-184">此事件应使用 <xref:System.ComponentModel.ProgressChangedEventHandler> 委托签名和 <xref:System.ComponentModel.ProgressChangedEventArgs> 类。</span><span class="sxs-lookup"><span data-stu-id="166b1-184">This event should use the <xref:System.ComponentModel.ProgressChangedEventHandler> delegate signature and the <xref:System.ComponentModel.ProgressChangedEventArgs> class.</span></span> <span data-ttu-id="166b1-185">或者，如果可以提供更多域专用进度指示器（例如，下载操作的读取字节数和总字节数），应定义 <xref:System.ComponentModel.ProgressChangedEventArgs> 的派生类。</span><span class="sxs-lookup"><span data-stu-id="166b1-185">Alternatively, if a more domain-specific progress indicator can be provided (for instance, bytes read and total bytes for a download operation), then you should define a derived class of <xref:System.ComponentModel.ProgressChangedEventArgs>.</span></span>

<span data-ttu-id="166b1-186">请注意，无论类支持多少个异步方法，都只有一个 `ProgressChanged` 或 MethodNameProgressChanged 事件。</span><span class="sxs-lookup"><span data-stu-id="166b1-186">Note that there is only one `ProgressChanged` or _MethodName_**ProgressChanged** event for the class, regardless of the number of asynchronous methods it supports.</span></span> <span data-ttu-id="166b1-187">客户端应使用传递给 MethodNameAsync 方法的 `userState` 对象，以区分多个并发操作的进度更新。</span><span class="sxs-lookup"><span data-stu-id="166b1-187">Clients are expected to use the `userState` object that is passed to the _MethodName_**Async** methods to distinguish among progress updates on multiple concurrent operations.</span></span>

<span data-ttu-id="166b1-188">可能出现多个操作支持进度，并且每个操作返回不同的进度指示器的情况。</span><span class="sxs-lookup"><span data-stu-id="166b1-188">There may be situations in which multiple operations support progress and each returns a different indicator for progress.</span></span> <span data-ttu-id="166b1-189">在这种情况下，不合适支持单个 `ProgressChanged` 事件，你可能需要考虑支持多个 `ProgressChanged` 事件。</span><span class="sxs-lookup"><span data-stu-id="166b1-189">In this case, a single `ProgressChanged` event is not appropriate, and you may consider supporting multiple `ProgressChanged` events.</span></span> <span data-ttu-id="166b1-190">在这种情况下，对每个 MethodNameAsync 方法使用 MethodNameProgressChanged 命名模式。</span><span class="sxs-lookup"><span data-stu-id="166b1-190">In this case use a naming pattern of _MethodName_**ProgressChanged** for each _MethodName_**Async** method.</span></span>

<span data-ttu-id="166b1-191">请遵守[实现基于事件的异步模式的最佳做法](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)中所述的进度报告语义。</span><span class="sxs-lookup"><span data-stu-id="166b1-191">Abide by the progress-reporting semantics described [Best Practices for Implementing the Event-based Asynchronous Pattern](best-practices-for-implementing-the-event-based-asynchronous-pattern.md).</span></span>

## <a name="optionally-provide-support-for-returning-incremental-results"></a><span data-ttu-id="166b1-192">选择性地为返回增量结果提供支持</span><span class="sxs-lookup"><span data-stu-id="166b1-192">Optionally Provide Support for Returning Incremental Results</span></span>

<span data-ttu-id="166b1-193">有时异步操作可以在完成之前返回增量结果。</span><span class="sxs-lookup"><span data-stu-id="166b1-193">Sometimes an asynchronous operation can return incremental results prior to completion.</span></span> <span data-ttu-id="166b1-194">可以通过多种方式支持此方案。</span><span class="sxs-lookup"><span data-stu-id="166b1-194">There are a number of options that can be used to support this scenario.</span></span> <span data-ttu-id="166b1-195">下面是一些示例。</span><span class="sxs-lookup"><span data-stu-id="166b1-195">Some examples follow.</span></span>

### <a name="single-operation-class"></a><span data-ttu-id="166b1-196">单一操作类</span><span class="sxs-lookup"><span data-stu-id="166b1-196">Single-operation Class</span></span>

<span data-ttu-id="166b1-197">如果你的类仅支持单一异步操作，并且能够返回增量结果，则可以：</span><span class="sxs-lookup"><span data-stu-id="166b1-197">If your class only supports a single asynchronous operation, and that operation is able to return incremental results, then:</span></span>

- <span data-ttu-id="166b1-198">将 <xref:System.ComponentModel.ProgressChangedEventArgs> 类型扩展为包含增量结果数据，并定义包含此扩展数据的 MethodNameProgressChanged 事件。</span><span class="sxs-lookup"><span data-stu-id="166b1-198">Extend the <xref:System.ComponentModel.ProgressChangedEventArgs> type to carry the incremental result data, and define a _MethodName_**ProgressChanged** event with this extended data.</span></span>

- <span data-ttu-id="166b1-199">若有要报告的增量结果，抛出此 MethodNameProgressChanged 事件。</span><span class="sxs-lookup"><span data-stu-id="166b1-199">Raise this _MethodName_**ProgressChanged** event when there is an incremental result to report.</span></span>

<span data-ttu-id="166b1-200">此解决方案特别适用于单一异步操作类，因为发生的同一事件可以对“所有操作”返回增量结果，与 MethodNameProgressChanged 事件一样。</span><span class="sxs-lookup"><span data-stu-id="166b1-200">This solution applies specifically to a single-async-operation class because there is no problem with the same event occurring to return incremental results on "all operations", as the _MethodName_**ProgressChanged** event does.</span></span>

### <a name="multiple-operation-class-with-homogeneous-incremental-results"></a><span data-ttu-id="166b1-201">使用同类增量结果的多操作类</span><span class="sxs-lookup"><span data-stu-id="166b1-201">Multiple-operation Class with Homogeneous Incremental Results</span></span>

<span data-ttu-id="166b1-202">在这种情况下，你的类支持多个异步方法，每个方法都能够返回增量结果，并且这些增量结果具有相同的数据类型。</span><span class="sxs-lookup"><span data-stu-id="166b1-202">In this case, your class supports multiple asynchronous methods, each capable of returning incremental results, and these incremental results all have the same type of data.</span></span>

<span data-ttu-id="166b1-203">请遵循上述适用于单一操作类的模型，因为同一 <xref:System.EventArgs> 结构适用于所有增量结果。</span><span class="sxs-lookup"><span data-stu-id="166b1-203">Follow the model described above for single-operation classes, as the same <xref:System.EventArgs> structure will work for all incremental results.</span></span> <span data-ttu-id="166b1-204">定义 `ProgressChanged` 事件，而不是 MethodNameProgressChanged 事件，因为它适用于多个异步方法。</span><span class="sxs-lookup"><span data-stu-id="166b1-204">Define a `ProgressChanged` event instead of a _MethodName_**ProgressChanged** event, since it applies to multiple asynchronous methods.</span></span>

### <a name="multiple-operation-class-with-heterogeneous-incremental-results"></a><span data-ttu-id="166b1-205">使用不同类增量结果的多操作类</span><span class="sxs-lookup"><span data-stu-id="166b1-205">Multiple-operation Class with Heterogeneous Incremental Results</span></span>

<span data-ttu-id="166b1-206">如果你的类支持多个异步方法，每个方法返回不同类型的数据，则应该：</span><span class="sxs-lookup"><span data-stu-id="166b1-206">If your class supports multiple asynchronous methods, each returning a different type of data, you should:</span></span>

- <span data-ttu-id="166b1-207">将增量结果报告与进度报告分开。</span><span class="sxs-lookup"><span data-stu-id="166b1-207">Separate your incremental result reporting from your progress reporting.</span></span>

- <span data-ttu-id="166b1-208">单独定义针对每个异步方法有适当 <xref:System.EventArgs> 的 MethodNameProgressChanged 事件，以处理此方法的增量结果数据。</span><span class="sxs-lookup"><span data-stu-id="166b1-208">Define a separate _MethodName_**ProgressChanged** event with appropriate <xref:System.EventArgs> for each asynchronous method to handle that method's incremental result data.</span></span>

<span data-ttu-id="166b1-209">按照[实现基于事件的异步模式的最佳做法](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)所述，在适当线程上调用事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="166b1-209">Invoke that event handler on the appropriate thread as described in [Best Practices for Implementing the Event-based Asynchronous Pattern](best-practices-for-implementing-the-event-based-asynchronous-pattern.md).</span></span>

## <a name="handling-out-and-ref-parameters-in-methods"></a><span data-ttu-id="166b1-210">处理方法中的 Out 和 Ref 参数</span><span class="sxs-lookup"><span data-stu-id="166b1-210">Handling Out and Ref Parameters in Methods</span></span>

<span data-ttu-id="166b1-211">虽然一般情况下，建议不要在 .NET 中使用 `out` 和 `ref`，但以下是使用它们时要遵循的规则：</span><span class="sxs-lookup"><span data-stu-id="166b1-211">Although the use of `out` and `ref` is, in general, discouraged in .NET, here are the rules to follow when they are present:</span></span>

<span data-ttu-id="166b1-212">给定同步方法 *MethodName* ：</span><span class="sxs-lookup"><span data-stu-id="166b1-212">Given a synchronous method *MethodName* :</span></span>

- <span data-ttu-id="166b1-213">MethodName 的 `out` 参数不应为 MethodNameAsync 的一部分。</span><span class="sxs-lookup"><span data-stu-id="166b1-213">`out` parameters to *MethodName* should not be part of _MethodName_**Async**.</span></span> <span data-ttu-id="166b1-214">它们应是 MethodNameCompletedEventArgs 的一部分，与 MethodName 中的相当参数同名（除非有更合适的名称）。</span><span class="sxs-lookup"><span data-stu-id="166b1-214">Instead, they should be part of _MethodName_**CompletedEventArgs** with the same name as its parameter equivalent in *MethodName* (unless there is a more appropriate name).</span></span>

- <span data-ttu-id="166b1-215">MethodName 的 `ref` 参数应显示为 MethodNameAsync 的一部分，并显示为 MethodNameCompletedEventArgs 的一部分，与 MethodName 中的相当参数同名（除非有更合适的名称）。</span><span class="sxs-lookup"><span data-stu-id="166b1-215">`ref` parameters to *MethodName* should appear as part of _MethodName_**Async** , and as part of _MethodName_**CompletedEventArgs** with the same name as its parameter equivalent in *MethodName* (unless there is a more appropriate name).</span></span>

<span data-ttu-id="166b1-216">例如，给定：</span><span class="sxs-lookup"><span data-stu-id="166b1-216">For example, given:</span></span>

```vb
Public Function MethodName(ByVal arg1 As String, ByRef arg2 As String, ByRef arg3 As String) As Integer
```

```csharp
public int MethodName(string arg1, ref string arg2, out string arg3);
```

<span data-ttu-id="166b1-217">异步方法及其 <xref:System.ComponentModel.AsyncCompletedEventArgs> 类如下所示：</span><span class="sxs-lookup"><span data-stu-id="166b1-217">Your asynchronous method and its <xref:System.ComponentModel.AsyncCompletedEventArgs> class would look like this:</span></span>

```vb
Public Sub MethodNameAsync(ByVal arg1 As String, ByVal arg2 As String)

Public Class MethodNameCompletedEventArgs
    Inherits System.ComponentModel.AsyncCompletedEventArgs
    Public ReadOnly Property Result() As Integer
    End Property
    Public ReadOnly Property Arg2() As String
    End Property
    Public ReadOnly Property Arg3() As String
    End Property
End Class
```

```csharp
public void MethodNameAsync(string arg1, string arg2);

public class MethodNameCompletedEventArgs : System.ComponentModel.AsyncCompletedEventArgs
{
    public int Result { get; };
    public string Arg2 { get; };
    public string Arg3 { get; };
}
```

## <a name="see-also"></a><span data-ttu-id="166b1-218">请参阅</span><span class="sxs-lookup"><span data-stu-id="166b1-218">See also</span></span>

- <xref:System.ComponentModel.ProgressChangedEventArgs>
- <xref:System.ComponentModel.AsyncCompletedEventArgs>
- [<span data-ttu-id="166b1-219">如何：实现支持基于事件的异步模式的组件</span><span class="sxs-lookup"><span data-stu-id="166b1-219">How to: Implement a Component That Supports the Event-based Asynchronous Pattern</span></span>](component-that-supports-the-event-based-asynchronous-pattern.md)
- [<span data-ttu-id="166b1-220">如何：在后台运行操作</span><span class="sxs-lookup"><span data-stu-id="166b1-220">How to: Run an Operation in the Background</span></span>](/dotnet/desktop/winforms/controls/how-to-run-an-operation-in-the-background)
- [<span data-ttu-id="166b1-221">如何：实现使用后台操作的窗体</span><span class="sxs-lookup"><span data-stu-id="166b1-221">How to: Implement a Form That Uses a Background Operation</span></span>](/dotnet/desktop/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation)
- [<span data-ttu-id="166b1-222">确定何时实现基于事件的异步模式</span><span class="sxs-lookup"><span data-stu-id="166b1-222">Deciding When to Implement the Event-based Asynchronous Pattern</span></span>](deciding-when-to-implement-the-event-based-asynchronous-pattern.md)
- [<span data-ttu-id="166b1-223">实现基于事件的异步模式的最佳做法</span><span class="sxs-lookup"><span data-stu-id="166b1-223">Best Practices for Implementing the Event-based Asynchronous Pattern</span></span>](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)
- [<span data-ttu-id="166b1-224">基于事件的异步模式 (EAP)</span><span class="sxs-lookup"><span data-stu-id="166b1-224">Event-based Asynchronous Pattern (EAP)</span></span>](event-based-asynchronous-pattern-eap.md)
