---
title: 使用委托进行异步编程
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- BeginInvoke method
- asynchronous programming, delegates
- asynchronous delegates
- calling synchronous methods in asynchronous manner
- EndInvoke method
- calling asynchronous methods
- delegates [.NET], asynchronous
- synchronous calling in asynchronous manner
ms.assetid: 38a345ca-6963-4436-9608-5c9defef9c64
ms.openlocfilehash: 05e574536abe4eac823b7b74369f5b191724e5b5
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889252"
---
# <a name="asynchronous-programming-using-delegates"></a><span data-ttu-id="26d4a-102">使用委托进行异步编程</span><span class="sxs-lookup"><span data-stu-id="26d4a-102">Asynchronous Programming Using Delegates</span></span>

<span data-ttu-id="26d4a-103">使用委托可通过异步方式调用同步方法。</span><span class="sxs-lookup"><span data-stu-id="26d4a-103">Delegates enable you to call a synchronous method in an asynchronous manner.</span></span> <span data-ttu-id="26d4a-104">如果同步调用委托，`Invoke` 方法将在当前线程上直接调用目标方法。</span><span class="sxs-lookup"><span data-stu-id="26d4a-104">When you call a delegate synchronously, the `Invoke` method calls the target method directly on the current thread.</span></span> <span data-ttu-id="26d4a-105">如果调用 `BeginInvoke` 方法，公共语言运行时 (CLR) 将对请求进行排队并立即返回给调用方。</span><span class="sxs-lookup"><span data-stu-id="26d4a-105">If the `BeginInvoke` method is called, the common language runtime (CLR) queues the request and returns immediately to the caller.</span></span> <span data-ttu-id="26d4a-106">目标方法将在线程池中的某个线程上异步调用。</span><span class="sxs-lookup"><span data-stu-id="26d4a-106">The target method is called asynchronously on a thread from the thread pool.</span></span> <span data-ttu-id="26d4a-107">提交请求的原始线程可以不受限制地继续与目标方法并行执行。</span><span class="sxs-lookup"><span data-stu-id="26d4a-107">The original thread, which submitted the request, is free to continue executing in parallel with the target method.</span></span> <span data-ttu-id="26d4a-108">如果已在对 `BeginInvoke` 方法的调用中指定回叫方法，则目标方法结束时，将调用回叫方法。</span><span class="sxs-lookup"><span data-stu-id="26d4a-108">If a callback method has been specified in the call to the `BeginInvoke` method, the callback method is called when the target method ends.</span></span> <span data-ttu-id="26d4a-109">在回叫方法中，`EndInvoke` 方法将获取返回值和所有输入/输出或仅输出参数。</span><span class="sxs-lookup"><span data-stu-id="26d4a-109">In the callback method, the `EndInvoke` method obtains the return value and any input/output or output-only parameters.</span></span> <span data-ttu-id="26d4a-110">如果调用 `BeginInvoke` 时未指定回叫方法，则可能从调用 `BeginInvoke` 的线程上调用 `EndInvoke`。</span><span class="sxs-lookup"><span data-stu-id="26d4a-110">If no callback method is specified when calling `BeginInvoke`, `EndInvoke` can be called from the thread that called `BeginInvoke`.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="26d4a-111">编译器应使用由用户指定的委托签名，发出具有 `Invoke`、`BeginInvoke` 和 `EndInvoke` 方法的委托类。</span><span class="sxs-lookup"><span data-stu-id="26d4a-111">Compilers should emit delegate classes with `Invoke`, `BeginInvoke`, and `EndInvoke` methods using the delegate signature specified by the user.</span></span> <span data-ttu-id="26d4a-112">`BeginInvoke` 和 `EndInvoke` 方法应标记为本机方法。</span><span class="sxs-lookup"><span data-stu-id="26d4a-112">The `BeginInvoke` and `EndInvoke` methods should be decorated as native.</span></span> <span data-ttu-id="26d4a-113">由于这些方法被标记为本机方法，CLR 将在类加载时自动提供实现。</span><span class="sxs-lookup"><span data-stu-id="26d4a-113">Because these methods are marked as native, the CLR automatically provides the implementation at class load time.</span></span> <span data-ttu-id="26d4a-114">加载程序可确保其不会被替代。</span><span class="sxs-lookup"><span data-stu-id="26d4a-114">The loader ensures that they are not overridden.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="26d4a-115">本节内容</span><span class="sxs-lookup"><span data-stu-id="26d4a-115">In This Section</span></span>  
 [<span data-ttu-id="26d4a-116">使用异步方式调用同步方法</span><span class="sxs-lookup"><span data-stu-id="26d4a-116">Calling Synchronous Methods Asynchronously</span></span>](calling-synchronous-methods-asynchronously.md)  
 <span data-ttu-id="26d4a-117">讨论如何使用委托对普通方法进行异步调用，并提供简单的代码示例演示等待异步调用返回的四种方法。</span><span class="sxs-lookup"><span data-stu-id="26d4a-117">Discusses the use of delegates to make asynchronous calls to ordinary methods, and provides simple code examples that show the four ways to wait for an asynchronous call to return.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="26d4a-118">相关章节</span><span class="sxs-lookup"><span data-stu-id="26d4a-118">Related Sections</span></span>  
 [<span data-ttu-id="26d4a-119">基于事件的异步模式 (EAP)</span><span class="sxs-lookup"><span data-stu-id="26d4a-119">Event-based Asynchronous Pattern (EAP)</span></span>](event-based-asynchronous-pattern-eap.md)  
 <span data-ttu-id="26d4a-120">介绍 .NET 中的异步编程。</span><span class="sxs-lookup"><span data-stu-id="26d4a-120">Describes asynchronous programming in .NET.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="26d4a-121">另请参阅</span><span class="sxs-lookup"><span data-stu-id="26d4a-121">See also</span></span>

- <xref:System.Delegate>
