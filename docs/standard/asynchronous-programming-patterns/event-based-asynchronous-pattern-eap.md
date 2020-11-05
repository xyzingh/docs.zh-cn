---
title: 基于事件的异步模式 (EAP)
description: 点击链接即可参阅文章，了解基于事件的异步模式 (EAP) 的相关信息，如实现、最佳做法、实现 EAP 客户端等。
ms.date: 07/23/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- asynchronous calls
- asynchronous programming, design patterns
- asynchronous programming
ms.assetid: c6baed9f-2a25-4728-9a9a-53b7b14840cf
ms.openlocfilehash: 16aabeb55a56c63449a865d00044c463657de740
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888836"
---
# <a name="event-based-asynchronous-pattern-eap"></a><span data-ttu-id="22b35-103">基于事件的异步模式 (EAP)</span><span class="sxs-lookup"><span data-stu-id="22b35-103">Event-based Asynchronous Pattern (EAP)</span></span>

<span data-ttu-id="22b35-104">有多种方式可向客户端代码公开异步功能。</span><span class="sxs-lookup"><span data-stu-id="22b35-104">There are a number of ways to expose asynchronous features to client code.</span></span> <span data-ttu-id="22b35-105">基于事件的异步模式规定了类呈现异步行为的一种方式。</span><span class="sxs-lookup"><span data-stu-id="22b35-105">The Event-based Asynchronous Pattern prescribes one way for classes to present asynchronous behavior.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="22b35-106">从 .NET Framework 4 开始，任务并行库为异步编程和并行编程提供了一种新模型。</span><span class="sxs-lookup"><span data-stu-id="22b35-106">Starting with .NET Framework 4, the Task Parallel Library provides a new model for asynchronous and parallel programming.</span></span> <span data-ttu-id="22b35-107">有关详细信息，请参阅 “[任务并行库 (TPL)](../parallel-programming/task-parallel-library-tpl.md)” 和 “[基于任务的异步模式 (TAP)](task-based-asynchronous-pattern-tap.md)”。</span><span class="sxs-lookup"><span data-stu-id="22b35-107">For more information, see [Task Parallel Library (TPL)](../parallel-programming/task-parallel-library-tpl.md) and [Task-based Asynchronous Pattern (TAP)](task-based-asynchronous-pattern-tap.md).</span></span>
  
## <a name="in-this-section"></a><span data-ttu-id="22b35-108">本节内容</span><span class="sxs-lookup"><span data-stu-id="22b35-108">In This Section</span></span>

 [<span data-ttu-id="22b35-109">基于事件的异步模式概述</span><span class="sxs-lookup"><span data-stu-id="22b35-109">Event-based Asynchronous Pattern Overview</span></span>](event-based-asynchronous-pattern-overview.md)  
 <span data-ttu-id="22b35-110">描述基于事件的异步模式如何在隐藏多线程设计中固有的许多复杂问题的同时，提供多线程应用程序的优点。</span><span class="sxs-lookup"><span data-stu-id="22b35-110">Describes how the Event-based Asynchronous Pattern makes available the advantages of multithreaded applications while hiding many of the complex issues inherent in multithreaded design.</span></span>  
  
 [<span data-ttu-id="22b35-111">实现基于事件的异步模式</span><span class="sxs-lookup"><span data-stu-id="22b35-111">Implementing the Event-based Asynchronous Pattern</span></span>](implementing-the-event-based-asynchronous-pattern.md)  
 <span data-ttu-id="22b35-112">描述打包具有异步功能的类的标准方式。</span><span class="sxs-lookup"><span data-stu-id="22b35-112">Describes the standardized way to package a class that has asynchronous features.</span></span>  
  
 [<span data-ttu-id="22b35-113">实现基于事件的异步模式的最佳做法</span><span class="sxs-lookup"><span data-stu-id="22b35-113">Best Practices for Implementing the Event-based Asynchronous Pattern</span></span>](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)  
 <span data-ttu-id="22b35-114">描述根据基于事件的异步模式公开异步功能的需求。</span><span class="sxs-lookup"><span data-stu-id="22b35-114">Describes the requirements for exposing asynchronous features according to the Event-based Asynchronous Pattern.</span></span>  
  
 [<span data-ttu-id="22b35-115">确定何时实现基于事件的异步模式</span><span class="sxs-lookup"><span data-stu-id="22b35-115">Deciding When to Implement the Event-based Asynchronous Pattern</span></span>](deciding-when-to-implement-the-event-based-asynchronous-pattern.md)  
 <span data-ttu-id="22b35-116">描述如何确定何时应选择实现基于事件的异步模式而不是由[异步编程模型 (APM)](asynchronous-programming-model-apm.md) 表示的 <xref:System.IAsyncResult> 模式</span><span class="sxs-lookup"><span data-stu-id="22b35-116">Describes how to determine when you should choose to implement the Event-based Asynchronous Pattern instead of the <xref:System.IAsyncResult> pattern represented by the [Asynchronous Programming Model (APM)](asynchronous-programming-model-apm.md)</span></span>
  
 [<span data-ttu-id="22b35-117">如何：实现支持基于事件的异步模式的组件</span><span class="sxs-lookup"><span data-stu-id="22b35-117">How to: Implement a Component That Supports the Event-based Asynchronous Pattern</span></span>](component-that-supports-the-event-based-asynchronous-pattern.md)  
 <span data-ttu-id="22b35-118">说明如何创建实现基于事件的异步模式的组件。</span><span class="sxs-lookup"><span data-stu-id="22b35-118">Describes how to create a component that implements the Event-based Asynchronous Pattern.</span></span> <span data-ttu-id="22b35-119">它是使用 <xref:System.ComponentModel?displayProperty=nameWithType> 命名空间的帮助器类实现的，这可确保该组件在任何应用程序模型下均可正常工作。</span><span class="sxs-lookup"><span data-stu-id="22b35-119">It is implemented using helper classes from the <xref:System.ComponentModel?displayProperty=nameWithType> namespace, which ensures that the component works correctly under any application model.</span></span>  

 [<span data-ttu-id="22b35-120">如何：实现基于事件的异步模式的客户端</span><span class="sxs-lookup"><span data-stu-id="22b35-120">How to: Implement a Client of the Event-based Asynchronous Pattern</span></span>](how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md)  
 <span data-ttu-id="22b35-121">说明如何创建使用实现基于事件的异步模式的组件的客户端。</span><span class="sxs-lookup"><span data-stu-id="22b35-121">Describes how to create a client that uses a component that implements the Event-based Asynchronous Pattern.</span></span>
  
 [<span data-ttu-id="22b35-122">如何：使用支持基于事件的异步模式的组件</span><span class="sxs-lookup"><span data-stu-id="22b35-122">How to: Use Components That Support the Event-based Asynchronous Pattern</span></span>](how-to-use-components-that-support-the-event-based-asynchronous-pattern.md)  
 <span data-ttu-id="22b35-123">描述如何使用支持基于事件的异步模式的组件。</span><span class="sxs-lookup"><span data-stu-id="22b35-123">Describes how to use a component that supports the Event-based Asynchronous Pattern.</span></span>  
  
## <a name="reference"></a><span data-ttu-id="22b35-124">参考</span><span class="sxs-lookup"><span data-stu-id="22b35-124">Reference</span></span>

 <xref:System.ComponentModel.AsyncOperation>  
 <span data-ttu-id="22b35-125">描述 <xref:System.ComponentModel.AsyncOperation> 类并提供指向其所有成员的链接。</span><span class="sxs-lookup"><span data-stu-id="22b35-125">Describes the <xref:System.ComponentModel.AsyncOperation> class and has links to all its members.</span></span>  
  
 <xref:System.ComponentModel.AsyncOperationManager>  
 <span data-ttu-id="22b35-126">描述 <xref:System.ComponentModel.AsyncOperationManager> 类并提供指向其所有成员的链接。</span><span class="sxs-lookup"><span data-stu-id="22b35-126">Describes the <xref:System.ComponentModel.AsyncOperationManager> class and has links to all its members.</span></span>  
  
 <xref:System.ComponentModel.BackgroundWorker>  
 <span data-ttu-id="22b35-127">描述 <xref:System.ComponentModel.BackgroundWorker> 组件并提供指向其所有成员的链接。</span><span class="sxs-lookup"><span data-stu-id="22b35-127">Describes the <xref:System.ComponentModel.BackgroundWorker> component and has links to all its members.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="22b35-128">相关章节</span><span class="sxs-lookup"><span data-stu-id="22b35-128">Related Sections</span></span>

 [<span data-ttu-id="22b35-129">任务并行库 (TPL)</span><span class="sxs-lookup"><span data-stu-id="22b35-129">Task Parallel Library (TPL)</span></span>](../parallel-programming/task-parallel-library-tpl.md)  
 <span data-ttu-id="22b35-130">描述用于异步和并行操作的编程模型。</span><span class="sxs-lookup"><span data-stu-id="22b35-130">Describes a programming model for asynchronous and parallel operations.</span></span>  
  
 [<span data-ttu-id="22b35-131">线程处理</span><span class="sxs-lookup"><span data-stu-id="22b35-131">Threading</span></span>](../threading/index.md)  
 <span data-ttu-id="22b35-132">描述 .NET 中的多线程处理功能。</span><span class="sxs-lookup"><span data-stu-id="22b35-132">Describes multithreading features in .NET.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="22b35-133">请参阅</span><span class="sxs-lookup"><span data-stu-id="22b35-133">See also</span></span>

- [<span data-ttu-id="22b35-134">托管线程处理的最佳做法</span><span class="sxs-lookup"><span data-stu-id="22b35-134">Managed Threading Best Practices</span></span>](../threading/managed-threading-best-practices.md)
- [<span data-ttu-id="22b35-135">事件</span><span class="sxs-lookup"><span data-stu-id="22b35-135">Events</span></span>](../events/index.md)
- [<span data-ttu-id="22b35-136">异步编程设计模式</span><span class="sxs-lookup"><span data-stu-id="22b35-136">Asynchronous Programming Design Patterns</span></span>](index.md)
