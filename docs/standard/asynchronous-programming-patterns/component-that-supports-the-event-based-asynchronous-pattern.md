---
title: 如何：实现支持基于事件的异步模式的组件
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
- threading [Windows Forms], asynchronous features
- AsyncCompletedEventArgs class
ms.assetid: 61f676b5-936f-40f6-83ce-f22805ec9c2f
ms.openlocfilehash: 2294379d37d4cd9e7fae494a6548561258743d74
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888875"
---
# <a name="how-to-implement-a-component-that-supports-the-event-based-asynchronous-pattern"></a><span data-ttu-id="75540-102">如何：实现支持基于事件的异步模式的组件</span><span class="sxs-lookup"><span data-stu-id="75540-102">How to: Implement a Component That Supports the Event-based Asynchronous Pattern</span></span>

<span data-ttu-id="75540-103">若要编写的类有一些可能会带来明显延迟的操作，请考虑按照[基于事件的异步模式概述](event-based-asynchronous-pattern-overview.md)中的步骤操作，为它实现异步功能。</span><span class="sxs-lookup"><span data-stu-id="75540-103">If you are writing a class with some operations that may incur noticeable delays, consider giving it asynchronous functionality by implementing the [Event-based Asynchronous Pattern Overview](event-based-asynchronous-pattern-overview.md).</span></span>  
  
 <span data-ttu-id="75540-104">本演练展示了如何创建实现基于事件的异步模式的组件。</span><span class="sxs-lookup"><span data-stu-id="75540-104">This walkthrough illustrates how to create a component that implements the Event-based Asynchronous Pattern.</span></span> <span data-ttu-id="75540-105">此组件是使用 <xref:System.ComponentModel?displayProperty=nameWithType> 命名空间中的帮助程序类进行实现，这可确保它在任何应用模型（包括 ASP.NET、控制台应用和 Windows 窗体应用）下都能正常运行。</span><span class="sxs-lookup"><span data-stu-id="75540-105">It is implemented using helper classes from the <xref:System.ComponentModel?displayProperty=nameWithType> namespace, which ensures that the component works correctly under any application model, including ASP.NET, Console applications and Windows Forms applications.</span></span> <span data-ttu-id="75540-106">也可以使用 <xref:System.Windows.Forms.PropertyGrid> 控件和自己的自定义设计器来设计此组件。</span><span class="sxs-lookup"><span data-stu-id="75540-106">This component is also designable with a <xref:System.Windows.Forms.PropertyGrid> control and your own custom designers.</span></span>  
  
 <span data-ttu-id="75540-107">本演练使用异步计算质数的应用。</span><span class="sxs-lookup"><span data-stu-id="75540-107">When you are through, you will have an application that computes prime numbers asynchronously.</span></span> <span data-ttu-id="75540-108">应用有主用户界面 (UI) 线程，以及用于每次质数计算的线程。</span><span class="sxs-lookup"><span data-stu-id="75540-108">Your application will have a main user interface (UI) thread and a thread for each prime number calculation.</span></span> <span data-ttu-id="75540-109">尽管测试大数字是否为质数需要花费很长时间，但主 UI 线程不会被此延迟中断，并且窗体在计算期间仍为响应式。</span><span class="sxs-lookup"><span data-stu-id="75540-109">Although testing whether a large number is prime can take a noticeable amount of time, the main UI thread will not be interrupted by this delay, and the form will be responsive during the calculations.</span></span> <span data-ttu-id="75540-110">不仅可以同时运行计算（数量不限），还能选择性地取消挂起的计算。</span><span class="sxs-lookup"><span data-stu-id="75540-110">You will be able to run as many calculations as you like concurrently and selectively cancel pending calculations.</span></span>  
  
 <span data-ttu-id="75540-111">本演练涉及以下任务：</span><span class="sxs-lookup"><span data-stu-id="75540-111">Tasks illustrated in this walkthrough include:</span></span>  
  
- <span data-ttu-id="75540-112">创建组件</span><span class="sxs-lookup"><span data-stu-id="75540-112">Creating the Component</span></span>  
  
- <span data-ttu-id="75540-113">定义公共异步事件和委托</span><span class="sxs-lookup"><span data-stu-id="75540-113">Defining Public Asynchronous Events and Delegates</span></span>  
  
- <span data-ttu-id="75540-114">定义专用委托</span><span class="sxs-lookup"><span data-stu-id="75540-114">Defining Private Delegates</span></span>  
  
- <span data-ttu-id="75540-115">实现公共事件</span><span class="sxs-lookup"><span data-stu-id="75540-115">Implementing Public Events</span></span>  
  
- <span data-ttu-id="75540-116">实现完成方法</span><span class="sxs-lookup"><span data-stu-id="75540-116">Implementing the Completion Method</span></span>  
  
- <span data-ttu-id="75540-117">实现工作方法</span><span class="sxs-lookup"><span data-stu-id="75540-117">Implementing the Worker Methods</span></span>  
  
- <span data-ttu-id="75540-118">实现启动和取消方法</span><span class="sxs-lookup"><span data-stu-id="75540-118">Implementing Start and Cancel Methods</span></span>  
  
 <span data-ttu-id="75540-119">若要将本主题中的代码复制为一个代码清单，请参阅[如何：实现基于事件的异步模式的客户端](how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="75540-119">To copy the code in this topic as a single listing, see [How to: Implement a Client of the Event-based Asynchronous Pattern](how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md).</span></span>  
  
## <a name="creating-the-component"></a><span data-ttu-id="75540-120">创建组件</span><span class="sxs-lookup"><span data-stu-id="75540-120">Creating the Component</span></span>  
 <span data-ttu-id="75540-121">第一步是，创建实现基于事件的异步模式的组件。</span><span class="sxs-lookup"><span data-stu-id="75540-121">The first step is to create the component that will implement the Event-based Asynchronous Pattern.</span></span>  
  
### <a name="to-create-the-component"></a><span data-ttu-id="75540-122">创建组件的具体步骤</span><span class="sxs-lookup"><span data-stu-id="75540-122">To create the component</span></span>  
  
- <span data-ttu-id="75540-123">创建继承自 <xref:System.ComponentModel.Component> 的类 `PrimeNumberCalculator`。</span><span class="sxs-lookup"><span data-stu-id="75540-123">Create a class called `PrimeNumberCalculator` that inherits from <xref:System.ComponentModel.Component>.</span></span>  
  
## <a name="defining-public-asynchronous-events-and-delegates"></a><span data-ttu-id="75540-124">定义公共异步事件和委托</span><span class="sxs-lookup"><span data-stu-id="75540-124">Defining Public Asynchronous Events and Delegates</span></span>  
 <span data-ttu-id="75540-125">组件使用事件与客户端进行通信。</span><span class="sxs-lookup"><span data-stu-id="75540-125">Your component communicates to clients using events.</span></span> <span data-ttu-id="75540-126">_MethodName_**Completed** 事件预警客户端注意异步任务完成， _MethodName_**ProgressChanged** 事件向客户端告知异步任务的进度。</span><span class="sxs-lookup"><span data-stu-id="75540-126">The _MethodName_**Completed** event alerts clients to the completion of an asynchronous task, and the _MethodName_**ProgressChanged** event informs clients of the progress of an asynchronous task.</span></span>  
  
### <a name="to-define-asynchronous-events-for-clients-of-your-component"></a><span data-ttu-id="75540-127">若要定义组件客户端的异步事件，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="75540-127">To define asynchronous events for clients of your component:</span></span>  
  
1. <span data-ttu-id="75540-128">在文件顶部，导入 <xref:System.Threading?displayProperty=nameWithType> 和 <xref:System.Collections.Specialized?displayProperty=nameWithType> 命名空间。</span><span class="sxs-lookup"><span data-stu-id="75540-128">Import the <xref:System.Threading?displayProperty=nameWithType> and <xref:System.Collections.Specialized?displayProperty=nameWithType> namespaces at the top of your file.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#11](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#11)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#11](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#11)]  
  
2. <span data-ttu-id="75540-129">在 `PrimeNumberCalculator` 类定义前面，声明进度和完成事件的委托。</span><span class="sxs-lookup"><span data-stu-id="75540-129">Before the `PrimeNumberCalculator` class definition, declare delegates for progress and completion events.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#7](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#7)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#7](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#7)]  
  
3. <span data-ttu-id="75540-130">在 `PrimeNumberCalculator` 类定义中，声明向客户端报告进度和完成事件的事件。</span><span class="sxs-lookup"><span data-stu-id="75540-130">In the `PrimeNumberCalculator` class definition, declare events for reporting progress and completion to clients.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#8](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#8)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#8](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#8)]  
  
4. <span data-ttu-id="75540-131">在 `PrimeNumberCalculator` 类定义后面，派生 `CalculatePrimeCompletedEventArgs` 类，向 `CalculatePrimeCompleted` 事件的客户端事件处理程序报告每次计算的结果。</span><span class="sxs-lookup"><span data-stu-id="75540-131">After the `PrimeNumberCalculator` class definition, derive the `CalculatePrimeCompletedEventArgs` class for reporting the outcome of each calculation to the client's event handler for the `CalculatePrimeCompleted`.event.</span></span> <span data-ttu-id="75540-132">除了 `AsyncCompletedEventArgs` 属性外，客户端还可以使用此类确定测试的数字是什么、数字是否为质数，以及第一个除数是什么（如果不是质数的话）。</span><span class="sxs-lookup"><span data-stu-id="75540-132">In addition to the `AsyncCompletedEventArgs` properties, this class enables the client to determine what number was tested, whether it is prime, and what the first divisor is if it is not prime.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#6](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#6)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#6](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#6)]  
  
## <a name="checkpoint"></a><span data-ttu-id="75540-133">检查点</span><span class="sxs-lookup"><span data-stu-id="75540-133">Checkpoint</span></span>  
 <span data-ttu-id="75540-134">此时，可以生成组件。</span><span class="sxs-lookup"><span data-stu-id="75540-134">At this point, you can build the component.</span></span>  
  
### <a name="to-test-your-component"></a><span data-ttu-id="75540-135">测试组件的具体步骤</span><span class="sxs-lookup"><span data-stu-id="75540-135">To test your component</span></span>  
  
- <span data-ttu-id="75540-136">编译组件。</span><span class="sxs-lookup"><span data-stu-id="75540-136">Compile the component.</span></span>  
  
     <span data-ttu-id="75540-137">将看到下面两个编译器警告：</span><span class="sxs-lookup"><span data-stu-id="75540-137">You will receive two compiler warnings:</span></span>  
  
    ```console  
    warning CS0067: The event 'AsynchronousPatternExample.PrimeNumberCalculator.ProgressChanged' is never used  
    warning CS0067: The event 'AsynchronousPatternExample.PrimeNumberCalculator.CalculatePrimeCompleted' is never used  
    ```  
  
     <span data-ttu-id="75540-138">这些警告会在下一部分中得到清除。</span><span class="sxs-lookup"><span data-stu-id="75540-138">These warnings will be cleared in the next section.</span></span>  
  
## <a name="defining-private-delegates"></a><span data-ttu-id="75540-139">定义专用委托</span><span class="sxs-lookup"><span data-stu-id="75540-139">Defining Private Delegates</span></span>  
 <span data-ttu-id="75540-140">`PrimeNumberCalculator` 组件的异步特性是通过特殊的 <xref:System.Threading.SendOrPostCallback> 委托在内部进行实现。</span><span class="sxs-lookup"><span data-stu-id="75540-140">The asynchronous aspects of the `PrimeNumberCalculator` component are implemented internally with a special delegate known as a <xref:System.Threading.SendOrPostCallback>.</span></span> <span data-ttu-id="75540-141"><xref:System.Threading.SendOrPostCallback> 表示对 <xref:System.Threading.ThreadPool> 线程执行的回调方法。</span><span class="sxs-lookup"><span data-stu-id="75540-141">A <xref:System.Threading.SendOrPostCallback> represents a callback method that executes on a <xref:System.Threading.ThreadPool> thread.</span></span> <span data-ttu-id="75540-142">回调方法必须有需要使用单个 <xref:System.Object> 类型参数的签名。也就是说，需要在包装类中的各委托之间传递状态。</span><span class="sxs-lookup"><span data-stu-id="75540-142">The callback method must have a signature that takes a single parameter of type <xref:System.Object>, which means you will need to pass state among delegates in a wrapper class.</span></span> <span data-ttu-id="75540-143">有关详细信息，请参阅 <xref:System.Threading.SendOrPostCallback>。</span><span class="sxs-lookup"><span data-stu-id="75540-143">For more information, see <xref:System.Threading.SendOrPostCallback>.</span></span>  
  
### <a name="to-implement-your-components-internal-asynchronous-behavior"></a><span data-ttu-id="75540-144">若要实现组件的内部异步行为，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="75540-144">To implement your component's internal asynchronous behavior:</span></span>  
  
1. <span data-ttu-id="75540-145">在 `PrimeNumberCalculator` 类中声明并创建 <xref:System.Threading.SendOrPostCallback> 委托。</span><span class="sxs-lookup"><span data-stu-id="75540-145">Declare and create the <xref:System.Threading.SendOrPostCallback> delegates in the `PrimeNumberCalculator` class.</span></span> <span data-ttu-id="75540-146">在 `InitializeDelegates` 实用工具方法中创建 <xref:System.Threading.SendOrPostCallback> 对象。</span><span class="sxs-lookup"><span data-stu-id="75540-146">Create the <xref:System.Threading.SendOrPostCallback> objects in a utility method called `InitializeDelegates`.</span></span>  
  
     <span data-ttu-id="75540-147">需要使用两个委托：一个用于向客户端报告进度事件，另一个用于向客户端报告完成事件。</span><span class="sxs-lookup"><span data-stu-id="75540-147">You will need two delegates: one for reporting progress to the client, and one for reporting completion to the client.</span></span>  

     [!code-csharp[System.ComponentModel.AsyncOperationManager#9](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#9)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#9](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#9)]  
    [!code-csharp[System.ComponentModel.AsyncOperationManager#20](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#20)]
    [!code-vb[System.ComponentModel.AsyncOperationManager#20](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#20)]  
  
2. <span data-ttu-id="75540-148">在组件的构造函数中调用 `InitializeDelegates` 方法。</span><span class="sxs-lookup"><span data-stu-id="75540-148">Call the `InitializeDelegates` method in your component's constructor.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#21](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#21)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#21](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#21)]  
  
3. <span data-ttu-id="75540-149">在 `PrimeNumberCalculator` 类中声明委托，以处理实际要异步完成的工作。</span><span class="sxs-lookup"><span data-stu-id="75540-149">Declare a delegate in the `PrimeNumberCalculator` class that handles the actual work to be done asynchronously.</span></span> <span data-ttu-id="75540-150">此委托包装用于测试数字是否为质数的工作方法。</span><span class="sxs-lookup"><span data-stu-id="75540-150">This delegate wraps the worker method that tests whether a number is prime.</span></span> <span data-ttu-id="75540-151">此委托需要使用 <xref:System.ComponentModel.AsyncOperation> 参数，用于跟踪异步操作的生存期。</span><span class="sxs-lookup"><span data-stu-id="75540-151">The delegate takes an <xref:System.ComponentModel.AsyncOperation> parameter, which will be used to track the lifetime of the asynchronous operation.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#22](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#22)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#22](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#22)]  
  
4. <span data-ttu-id="75540-152">创建一个集合，用于管理挂起的异步操作的生存期。</span><span class="sxs-lookup"><span data-stu-id="75540-152">Create a collection for managing lifetimes of pending asynchronous operations.</span></span> <span data-ttu-id="75540-153">客户端需要通过一种途径，跟踪已执行和完成的操作。若要执行这样的跟踪，客户端必须在调用异步方法时，传递唯一令牌或任务 ID。</span><span class="sxs-lookup"><span data-stu-id="75540-153">The client needs a way to track operations as they are executed and completed, and this tracking is done by requiring the client to pass a unique token, or task ID, when the client makes the call to the asynchronous method.</span></span> <span data-ttu-id="75540-154">`PrimeNumberCalculator` 组件必须跟踪所有调用，具体方法是将任务 ID 与其对应的调用相关联。</span><span class="sxs-lookup"><span data-stu-id="75540-154">The `PrimeNumberCalculator` component must keep track of each call by associating the task ID with its corresponding invocation.</span></span> <span data-ttu-id="75540-155">如果客户端传递的任务 ID 不唯一，`PrimeNumberCalculator` 组件必须抛出异常。</span><span class="sxs-lookup"><span data-stu-id="75540-155">If the client passes a task ID that is not unique, the `PrimeNumberCalculator` component must raise an exception.</span></span>  
  
     <span data-ttu-id="75540-156">`PrimeNumberCalculator` 组件使用特殊的集合类 <xref:System.Collections.Specialized.HybridDictionary> 跟踪任务 ID。</span><span class="sxs-lookup"><span data-stu-id="75540-156">The `PrimeNumberCalculator` component keeps track of task ID by using a special collection class called a <xref:System.Collections.Specialized.HybridDictionary>.</span></span> <span data-ttu-id="75540-157">在类定义中，创建名为 `userTokenToLifetime` 的 <xref:System.Collections.Specialized.HybridDictionary>。</span><span class="sxs-lookup"><span data-stu-id="75540-157">In the class definition, create a <xref:System.Collections.Specialized.HybridDictionary> called `userTokenToLifetime`.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#23](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#23)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#23](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#23)]  
  
## <a name="implementing-public-events"></a><span data-ttu-id="75540-158">实现公共事件</span><span class="sxs-lookup"><span data-stu-id="75540-158">Implementing Public Events</span></span>  
 <span data-ttu-id="75540-159">实现基于事件的异步模式的组件使用事件与客户端进行通信。</span><span class="sxs-lookup"><span data-stu-id="75540-159">Components that implement the Event-based Asynchronous Pattern communicate to clients using events.</span></span> <span data-ttu-id="75540-160">这些事件在 <xref:System.ComponentModel.AsyncOperation> 类的相助下对适当的线程调用。</span><span class="sxs-lookup"><span data-stu-id="75540-160">These events are invoked on the proper thread with the help of the <xref:System.ComponentModel.AsyncOperation> class.</span></span>  
  
### <a name="to-raise-events-to-your-components-clients"></a><span data-ttu-id="75540-161">若要向组件的客户端抛出事件，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="75540-161">To raise events to your component's clients:</span></span>  
  
1. <span data-ttu-id="75540-162">实现公共事件，以向客户端报告事件。</span><span class="sxs-lookup"><span data-stu-id="75540-162">Implement public events for reporting to clients.</span></span> <span data-ttu-id="75540-163">需要实现两个事件，一个用于报告进度事件，另一个用于报告完成事件。</span><span class="sxs-lookup"><span data-stu-id="75540-163">You will need an event for reporting progress and one for reporting completion.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#24](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#24)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#24](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#24)]  
  
## <a name="implementing-the-completion-method"></a><span data-ttu-id="75540-164">实现完成方法</span><span class="sxs-lookup"><span data-stu-id="75540-164">Implementing the Completion Method</span></span>  
 <span data-ttu-id="75540-165">完成委托是在异步操作最终成功完成、出错或取消时，由基础的自由线程异步行为调用的方法。</span><span class="sxs-lookup"><span data-stu-id="75540-165">The completion delegate is the method that the underlying, free-threaded asynchronous behavior will invoke when the asynchronous operation ends by successful completion, error, or cancellation.</span></span> <span data-ttu-id="75540-166">此调用发生在任意线程上。</span><span class="sxs-lookup"><span data-stu-id="75540-166">This invocation happens on an arbitrary thread.</span></span>  
  
 <span data-ttu-id="75540-167">在此方法中，客户端任务 ID 从唯一客户端令牌的内部集合中删除。</span><span class="sxs-lookup"><span data-stu-id="75540-167">This method is where the client's task ID is removed from the internal collection of unique client tokens.</span></span> <span data-ttu-id="75540-168">另外，此方法还对相应的 <xref:System.ComponentModel.AsyncOperation> 调用 <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A>方法，结束特定异步操作的生存期。</span><span class="sxs-lookup"><span data-stu-id="75540-168">This method also ends the lifetime of a particular asynchronous operation by calling the <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A> method on the corresponding <xref:System.ComponentModel.AsyncOperation>.</span></span> <span data-ttu-id="75540-169">此调用对适用于应用模型的线程抛出完成事件。</span><span class="sxs-lookup"><span data-stu-id="75540-169">This call raises the completion event on the thread that is appropriate for the application model.</span></span> <span data-ttu-id="75540-170">调用 <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A> 后，便无法再使用此 <xref:System.ComponentModel.AsyncOperation> 实例，随后只要尝试使用它，就会导致异常抛出。</span><span class="sxs-lookup"><span data-stu-id="75540-170">After the <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A> method is called, this instance of <xref:System.ComponentModel.AsyncOperation> can no longer be used, and any subsequent attempts to use it will throw an exception.</span></span>  
  
 <span data-ttu-id="75540-171">`CompletionMethod` 签名必须保留描述异步操作结果所需的全部状态。</span><span class="sxs-lookup"><span data-stu-id="75540-171">The `CompletionMethod` signature must hold all state necessary to describe the outcome of the asynchronous operation.</span></span> <span data-ttu-id="75540-172">它保留以下状态：此异步操作测试的数字是什么、数字是否为质数，以及第一个除数的值是什么（如果不是质数的话）。</span><span class="sxs-lookup"><span data-stu-id="75540-172">It holds state for the number that was tested by this particular asynchronous operation, whether the number is prime, and the value of its first divisor if it is not a prime number.</span></span> <span data-ttu-id="75540-173">此外，它还保留描述所发生的任何异常的状态，以及与此任务对应的 <xref:System.ComponentModel.AsyncOperation>。</span><span class="sxs-lookup"><span data-stu-id="75540-173">It also holds state describing any exception that occurred, and the <xref:System.ComponentModel.AsyncOperation> corresponding to this particular task.</span></span>  
  
### <a name="to-complete-an-asynchronous-operation"></a><span data-ttu-id="75540-174">若要完成异步操作，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="75540-174">To complete an asynchronous operation:</span></span>  
  
- <span data-ttu-id="75540-175">实现完成方法。</span><span class="sxs-lookup"><span data-stu-id="75540-175">Implement the completion method.</span></span> <span data-ttu-id="75540-176">此方法需要使用六个参数，用于填充通过客户端的 `CalculatePrimeCompletedEventHandler` 返回到客户端的 `CalculatePrimeCompletedEventArgs`。</span><span class="sxs-lookup"><span data-stu-id="75540-176">It takes six parameters, which it uses to populate a `CalculatePrimeCompletedEventArgs` that is returned to the client through the client's `CalculatePrimeCompletedEventHandler`.</span></span> <span data-ttu-id="75540-177">它还从内部集合中删除客户端的任务 ID 令牌，并通过调用 <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A> 结束异步操作的生存期。</span><span class="sxs-lookup"><span data-stu-id="75540-177">It removes the client's task ID token from the internal collection, and it ends the asynchronous operation's lifetime with a call to <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A>.</span></span> <span data-ttu-id="75540-178"><xref:System.ComponentModel.AsyncOperation> 封送对适用于应用模型的线程或上下文执行的调用。</span><span class="sxs-lookup"><span data-stu-id="75540-178">The <xref:System.ComponentModel.AsyncOperation> marshals the call to the thread or context that is appropriate for the application model.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#26](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#26)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#26](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#26)]  
  
## <a name="checkpoint"></a><span data-ttu-id="75540-179">检查点</span><span class="sxs-lookup"><span data-stu-id="75540-179">Checkpoint</span></span>  
 <span data-ttu-id="75540-180">此时，可以生成组件。</span><span class="sxs-lookup"><span data-stu-id="75540-180">At this point, you can build the component.</span></span>  
  
### <a name="to-test-your-component"></a><span data-ttu-id="75540-181">测试组件的具体步骤</span><span class="sxs-lookup"><span data-stu-id="75540-181">To test your component</span></span>  
  
- <span data-ttu-id="75540-182">编译组件。</span><span class="sxs-lookup"><span data-stu-id="75540-182">Compile the component.</span></span>  
  
     <span data-ttu-id="75540-183">将看到下面的一个编译器警告：</span><span class="sxs-lookup"><span data-stu-id="75540-183">You will receive one compiler warning:</span></span>  
  
    ```console  
    warning CS0169: The private field 'AsynchronousPatternExample.PrimeNumberCalculator.workerDelegate' is never used  
    ```  
  
     <span data-ttu-id="75540-184">此警告会在下一部分中得到解析。</span><span class="sxs-lookup"><span data-stu-id="75540-184">This warning will be resolved in the next section.</span></span>  
  
## <a name="implementing-the-worker-methods"></a><span data-ttu-id="75540-185">实现工作方法</span><span class="sxs-lookup"><span data-stu-id="75540-185">Implementing the Worker Methods</span></span>  
 <span data-ttu-id="75540-186">至此，已实现 `PrimeNumberCalculator` 组件的支持异步代码。</span><span class="sxs-lookup"><span data-stu-id="75540-186">So far, you have implemented the supporting asynchronous code for the `PrimeNumberCalculator` component.</span></span> <span data-ttu-id="75540-187">现在，可以实现执行实际工作的代码。</span><span class="sxs-lookup"><span data-stu-id="75540-187">Now you can implement the code that does the actual work.</span></span> <span data-ttu-id="75540-188">将实现以下三个方法：`CalculateWorker`、`BuildPrimeNumberList` 和 `IsPrime`。</span><span class="sxs-lookup"><span data-stu-id="75540-188">You will implement three methods: `CalculateWorker`, `BuildPrimeNumberList`, and `IsPrime`.</span></span> <span data-ttu-id="75540-189">`BuildPrimeNumberList` 和 `IsPrime` 共同构成了著名的埃拉托斯特尼筛法，通过在测试数字的平方根范围内查找所有质数，确定数字是否为质数。</span><span class="sxs-lookup"><span data-stu-id="75540-189">Together, `BuildPrimeNumberList` and `IsPrime` comprise a well-known algorithm called the Sieve of Eratosthenes, which determines if a number is prime by finding all the prime numbers up to the square root of the test number.</span></span> <span data-ttu-id="75540-190">如果使用这种方法没有找到任何除数，表明测试数字为质数。</span><span class="sxs-lookup"><span data-stu-id="75540-190">If no divisors are found by that point, the test number is prime.</span></span>  
  
 <span data-ttu-id="75540-191">如果此组件旨在最大限度地提高效率，便会记住对不同测试数字执行各种调用时发现的所有质数。</span><span class="sxs-lookup"><span data-stu-id="75540-191">If this component were written for maximum efficiency, it would remember all the prime numbers discovered by various invocations for different test numbers.</span></span> <span data-ttu-id="75540-192">它还会检查是否有最简单的除数（如 2、3 和 5）。</span><span class="sxs-lookup"><span data-stu-id="75540-192">It would also check for trivial divisors like 2, 3, and 5.</span></span> <span data-ttu-id="75540-193">虽然此示例旨在展示如何异步执行非常耗时的操作，但这些优化是留给大家练练手的。</span><span class="sxs-lookup"><span data-stu-id="75540-193">The intent of this example is to demonstrate how time-consuming operations can be executed asynchronously, however, so these optimizations are left as an exercise for you.</span></span>  
  
 <span data-ttu-id="75540-194">`CalculateWorker` 方法包装在委托中，通过调用 `BeginInvoke` 进行异步调用。</span><span class="sxs-lookup"><span data-stu-id="75540-194">The `CalculateWorker` method is wrapped in a delegate and is invoked asynchronously with a call to `BeginInvoke`.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="75540-195">进度事件报告是在 `BuildPrimeNumberList` 方法中实现。</span><span class="sxs-lookup"><span data-stu-id="75540-195">Progress reporting is implemented in the `BuildPrimeNumberList` method.</span></span> <span data-ttu-id="75540-196">在快速运行的计算机上，`ProgressChanged` 事件可能会快速连续抛出。</span><span class="sxs-lookup"><span data-stu-id="75540-196">On fast computers, `ProgressChanged` events can be raised in rapid succession.</span></span> <span data-ttu-id="75540-197">对其抛出这些事件的客户端线程必须能够处理这种情况。</span><span class="sxs-lookup"><span data-stu-id="75540-197">The client thread, on which these events are raised, must be able to handle this situation.</span></span> <span data-ttu-id="75540-198">消息可能会像洪水般涌入用户界面代码，导致代码无法不断更新，继而导致无响应。</span><span class="sxs-lookup"><span data-stu-id="75540-198">User interface code may be flooded with messages and unable to keep up, resulting in unresponsiveness.</span></span> <span data-ttu-id="75540-199">有关处理这种情况的示例用户界面，请参阅[如何：实现基于事件的异步模式的客户端](how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="75540-199">For an example user interface that handles this situation, see [How to: Implement a Client of the Event-based Asynchronous Pattern](how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md).</span></span>  
  
### <a name="to-execute-the-prime-number-calculation-asynchronously"></a><span data-ttu-id="75540-200">若要异步执行质数计算，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="75540-200">To execute the prime number calculation asynchronously:</span></span>  
  
1. <span data-ttu-id="75540-201">实现 `TaskCanceled` 实用工具方法。</span><span class="sxs-lookup"><span data-stu-id="75540-201">Implement the `TaskCanceled` utility method.</span></span> <span data-ttu-id="75540-202">此方法检查任务生存期集合中是否有给定的任务 ID；如果找不到任务 ID，就会返回 `true`。</span><span class="sxs-lookup"><span data-stu-id="75540-202">This checks the task lifetime collection for the given task ID, and returns `true` if the task ID is not found.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#32](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#32)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#32](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#32)]  
  
2. <span data-ttu-id="75540-203">实现 `CalculateWorker` 方法。</span><span class="sxs-lookup"><span data-stu-id="75540-203">Implement the `CalculateWorker` method.</span></span> <span data-ttu-id="75540-204">它需要使用下面两个参数：要测试的数字和 <xref:System.ComponentModel.AsyncOperation>。</span><span class="sxs-lookup"><span data-stu-id="75540-204">It takes two parameters: a number to test, and an <xref:System.ComponentModel.AsyncOperation>.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#27](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#27)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#27](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#27)]  
  
3. <span data-ttu-id="75540-205">实现 `BuildPrimeNumberList`。</span><span class="sxs-lookup"><span data-stu-id="75540-205">Implement `BuildPrimeNumberList`.</span></span> <span data-ttu-id="75540-206">它需要使用下面两个参数：要测试的数字和 <xref:System.ComponentModel.AsyncOperation>。</span><span class="sxs-lookup"><span data-stu-id="75540-206">It takes two parameters: the number to test, and an <xref:System.ComponentModel.AsyncOperation>.</span></span> <span data-ttu-id="75540-207">此方法使用 <xref:System.ComponentModel.AsyncOperation> 报告进度和增量结果。</span><span class="sxs-lookup"><span data-stu-id="75540-207">It uses the <xref:System.ComponentModel.AsyncOperation> to report progress and incremental results.</span></span> <span data-ttu-id="75540-208">这可确保对适用于应用模型的线程或上下文调用客户端的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="75540-208">This assures that the client's event handlers are called on the proper thread or context for the application model.</span></span> <span data-ttu-id="75540-209">如果 `BuildPrimeNumberList` 找到了质数，它会将此作为增量结果，报告给 `ProgressChanged` 事件的客户端事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="75540-209">When `BuildPrimeNumberList` finds a prime number, it reports this as an incremental result to the client's event handler for the `ProgressChanged` event.</span></span> <span data-ttu-id="75540-210">为此，必须使用派生自 <xref:System.ComponentModel.ProgressChangedEventArgs> 的类 `CalculatePrimeProgressChangedEventArgs`，其中新增有一个属性，即 `LatestPrimeNumber`。</span><span class="sxs-lookup"><span data-stu-id="75540-210">This requires a class derived from <xref:System.ComponentModel.ProgressChangedEventArgs>, called `CalculatePrimeProgressChangedEventArgs`, which has one added property called `LatestPrimeNumber`.</span></span>  
  
     <span data-ttu-id="75540-211">`BuildPrimeNumberList` 方法还会定期调用 `TaskCanceled` 方法，并在此方法返回 `true` 时退出。</span><span class="sxs-lookup"><span data-stu-id="75540-211">The `BuildPrimeNumberList` method also periodically calls the `TaskCanceled` method and exits if the method returns `true`.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#5](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#5)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#5](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#5)]  
  
4. <span data-ttu-id="75540-212">实现 `IsPrime`。</span><span class="sxs-lookup"><span data-stu-id="75540-212">Implement `IsPrime`.</span></span> <span data-ttu-id="75540-213">它需要使用下面三个参数：已知质数列表、要测试的数字，以及找到的第一个除数的输出参数。</span><span class="sxs-lookup"><span data-stu-id="75540-213">It takes three parameters: a list of known prime numbers, the number to test, and an output parameter for the first divisor found.</span></span> <span data-ttu-id="75540-214">它根据质数列表确定测试数字是否为质数。</span><span class="sxs-lookup"><span data-stu-id="75540-214">Given the list of prime numbers, it determines if the test number is prime.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#28](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#28)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#28](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#28)]  
  
5. <span data-ttu-id="75540-215">从 <xref:System.ComponentModel.ProgressChangedEventArgs> 派生 `CalculatePrimeProgressChangedEventArgs`。</span><span class="sxs-lookup"><span data-stu-id="75540-215">Derive `CalculatePrimeProgressChangedEventArgs` from <xref:System.ComponentModel.ProgressChangedEventArgs>.</span></span> <span data-ttu-id="75540-216">必须有此类，才能向 `ProgressChanged` 事件的客户端事件处理程序报告增量结果。</span><span class="sxs-lookup"><span data-stu-id="75540-216">This class is necessary for reporting incremental results to the client's event handler for the `ProgressChanged` event.</span></span> <span data-ttu-id="75540-217">它新增有一个属性，即 `LatestPrimeNumber`。</span><span class="sxs-lookup"><span data-stu-id="75540-217">It has one added property called `LatestPrimeNumber`.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#29](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#29)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#29](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#29)]  
  
## <a name="checkpoint"></a><span data-ttu-id="75540-218">检查点</span><span class="sxs-lookup"><span data-stu-id="75540-218">Checkpoint</span></span>  
 <span data-ttu-id="75540-219">此时，可以生成组件。</span><span class="sxs-lookup"><span data-stu-id="75540-219">At this point, you can build the component.</span></span>  
  
### <a name="to-test-your-component"></a><span data-ttu-id="75540-220">测试组件的具体步骤</span><span class="sxs-lookup"><span data-stu-id="75540-220">To test your component</span></span>  
  
- <span data-ttu-id="75540-221">编译组件。</span><span class="sxs-lookup"><span data-stu-id="75540-221">Compile the component.</span></span>  
  
     <span data-ttu-id="75540-222">剩下要编写的就是，异步操作的启动和取消方法，即 `CalculatePrimeAsync` 和 `CancelAsync`。</span><span class="sxs-lookup"><span data-stu-id="75540-222">All that remains to be written are the methods to start and cancel asynchronous operations, `CalculatePrimeAsync` and `CancelAsync`.</span></span>  
  
## <a name="implementing-the-start-and-cancel-methods"></a><span data-ttu-id="75540-223">实现启动和取消方法</span><span class="sxs-lookup"><span data-stu-id="75540-223">Implementing the Start and Cancel Methods</span></span>  
 <span data-ttu-id="75540-224">若要对它自己的线程启动工作方法，请对包装方法的委托调用 `BeginInvoke`。</span><span class="sxs-lookup"><span data-stu-id="75540-224">You start the worker method on its own thread by calling `BeginInvoke` on the delegate that wraps it.</span></span> <span data-ttu-id="75540-225">若要管理特定异步操作的生存期，请对 <xref:System.ComponentModel.AsyncOperationManager> 帮助程序类调用 <xref:System.ComponentModel.AsyncOperationManager.CreateOperation%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="75540-225">To manage the lifetime of a particular asynchronous operation, you call the <xref:System.ComponentModel.AsyncOperationManager.CreateOperation%2A> method on the <xref:System.ComponentModel.AsyncOperationManager> helper class.</span></span> <span data-ttu-id="75540-226">这会返回 <xref:System.ComponentModel.AsyncOperation>，将对客户端事件处理程序的调用封送到适当的线程或上下文。</span><span class="sxs-lookup"><span data-stu-id="75540-226">This returns an <xref:System.ComponentModel.AsyncOperation>, which marshals calls on the client's event handlers to the proper thread or context.</span></span>  
  
 <span data-ttu-id="75540-227">若要取消特定挂起操作，请对相应的 <xref:System.ComponentModel.AsyncOperation> 调用 <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A>。</span><span class="sxs-lookup"><span data-stu-id="75540-227">You cancel a particular pending operation by calling <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A> on its corresponding <xref:System.ComponentModel.AsyncOperation>.</span></span> <span data-ttu-id="75540-228">这样一来，可以结束操作，随后只要调用 <xref:System.ComponentModel.AsyncOperation> 都会导致异常抛出。</span><span class="sxs-lookup"><span data-stu-id="75540-228">This ends that operation, and any subsequent calls to its <xref:System.ComponentModel.AsyncOperation> will throw an exception.</span></span>  
  
### <a name="to-implement-start-and-cancel-functionality"></a><span data-ttu-id="75540-229">若要实现启动和取消功能，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="75540-229">To implement Start and Cancel functionality:</span></span>  
  
1. <span data-ttu-id="75540-230">实现 `CalculatePrimeAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="75540-230">Implement the `CalculatePrimeAsync` method.</span></span> <span data-ttu-id="75540-231">请确保相对于表示当前挂起任务的所有令牌，客户端提供的令牌（任务 ID）都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="75540-231">Make sure the client-supplied token (task ID) is unique with respect to all the tokens representing currently pending tasks.</span></span> <span data-ttu-id="75540-232">如果客户端传入的令牌不唯一，`CalculatePrimeAsync` 会抛出异常。</span><span class="sxs-lookup"><span data-stu-id="75540-232">If the client passes in a non-unique token, `CalculatePrimeAsync` raises an exception.</span></span> <span data-ttu-id="75540-233">如果唯一，令牌会被添加到任务 ID 集合中。</span><span class="sxs-lookup"><span data-stu-id="75540-233">Otherwise, the token is added to the task ID collection.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#3](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#3)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#3](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#3)]  
  
2. <span data-ttu-id="75540-234">实现 `CancelAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="75540-234">Implement the `CancelAsync` method.</span></span> <span data-ttu-id="75540-235">如果令牌集合中有 `taskId` 参数，将会删除此参数。</span><span class="sxs-lookup"><span data-stu-id="75540-235">If the `taskId` parameter exists in the token collection, it is removed.</span></span> <span data-ttu-id="75540-236">这可以防止尚未启动的已取消任务运行。</span><span class="sxs-lookup"><span data-stu-id="75540-236">This prevents canceled tasks that have not started from running.</span></span> <span data-ttu-id="75540-237">如果任务正在运行，`BuildPrimeNumberList` 方法会在检测到任务 ID 已从生存期集合中删除时退出。</span><span class="sxs-lookup"><span data-stu-id="75540-237">If the task is running, the `BuildPrimeNumberList` method exits when it detects that the task ID has been removed from the lifetime collection.</span></span>  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#4](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#4)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#4](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#4)]  
  
## <a name="checkpoint"></a><span data-ttu-id="75540-238">检查点</span><span class="sxs-lookup"><span data-stu-id="75540-238">Checkpoint</span></span>  
 <span data-ttu-id="75540-239">此时，可以生成组件。</span><span class="sxs-lookup"><span data-stu-id="75540-239">At this point, you can build the component.</span></span>  
  
### <a name="to-test-your-component"></a><span data-ttu-id="75540-240">测试组件的具体步骤</span><span class="sxs-lookup"><span data-stu-id="75540-240">To test your component</span></span>  
  
- <span data-ttu-id="75540-241">编译组件。</span><span class="sxs-lookup"><span data-stu-id="75540-241">Compile the component.</span></span>  
  
 <span data-ttu-id="75540-242">`PrimeNumberCalculator` 组件现已完成且可供使用。</span><span class="sxs-lookup"><span data-stu-id="75540-242">The `PrimeNumberCalculator` component is now complete and ready to use.</span></span>  
  
 <span data-ttu-id="75540-243">有关使用 `PrimeNumberCalculator` 组件的示例客户端，请参阅[如何：实现基于事件的异步模式的客户端](how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="75540-243">For an example client that uses the `PrimeNumberCalculator` component, see [How to: Implement a Client of the Event-based Asynchronous Pattern](how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="75540-244">后续步骤</span><span class="sxs-lookup"><span data-stu-id="75540-244">Next Steps</span></span>  
 <span data-ttu-id="75540-245">可以编写与 `CalculatePrimeAsync` 方法相当的同步方法 `CalculatePrime`，扩充此示例。</span><span class="sxs-lookup"><span data-stu-id="75540-245">You can fill out this example by writing `CalculatePrime`, the synchronous equivalent of `CalculatePrimeAsync` method.</span></span> <span data-ttu-id="75540-246">这样一来，`PrimeNumberCalculator` 组件就完全符合基于事件的异步模式了。</span><span class="sxs-lookup"><span data-stu-id="75540-246">This will make the `PrimeNumberCalculator` component fully compliant with the Event-based Asynchronous Pattern.</span></span>  
  
 <span data-ttu-id="75540-247">若要改进此示例，可以保留对不同测试数字执行各种调用时发现的所有质数列表。</span><span class="sxs-lookup"><span data-stu-id="75540-247">You can improve this example by retaining the list of all the prime numbers discovered by various invocations for different test numbers.</span></span> <span data-ttu-id="75540-248">使用这种方法，所有任务都将受益于前面完成的任务。</span><span class="sxs-lookup"><span data-stu-id="75540-248">Using this approach, each task will benefit from the work done by previous tasks.</span></span> <span data-ttu-id="75540-249">请使用 `lock` 区域小心保护此列表，以序列化不同线程对列表的访问。</span><span class="sxs-lookup"><span data-stu-id="75540-249">Be careful to protect this list with `lock` regions, so access to the list by different threads is serialized.</span></span>  
  
 <span data-ttu-id="75540-250">还可以测试是否有最简单的除数（如 2、3 和 5）来改进此示例。</span><span class="sxs-lookup"><span data-stu-id="75540-250">You can also improve this example by testing for trivial divisors, like 2, 3, and 5.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="75540-251">另请参阅</span><span class="sxs-lookup"><span data-stu-id="75540-251">See also</span></span>

- [<span data-ttu-id="75540-252">如何：在后台运行操作</span><span class="sxs-lookup"><span data-stu-id="75540-252">How to: Run an Operation in the Background</span></span>](/dotnet/desktop/winforms/controls/how-to-run-an-operation-in-the-background)
- [<span data-ttu-id="75540-253">基于事件的异步模式概述</span><span class="sxs-lookup"><span data-stu-id="75540-253">Event-based Asynchronous Pattern Overview</span></span>](event-based-asynchronous-pattern-overview.md)
- [<span data-ttu-id="75540-254">基于事件的异步模式 (EAP)</span><span class="sxs-lookup"><span data-stu-id="75540-254">Event-based Asynchronous Pattern (EAP)</span></span>](event-based-asynchronous-pattern-eap.md)
