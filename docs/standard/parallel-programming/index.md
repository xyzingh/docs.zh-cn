---
title: .NET 中的并行编程
description: 了解 .NET 中的并行编程。 使用 .NET 运行时、类库类型和诊断工具来简化 .NET 开发。
ms.date: 09/12/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- parallel programming
ms.assetid: 4d83c690-ad2d-489e-a2e0-b85b898a672d
ms.openlocfilehash: edb3d38b0815c6703720292a45e302c62c81650b
ms.sourcegitcommit: 6d09ae36acba0b0e2ba47999f8f1a725795462a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2020
ms.locfileid: "92925332"
---
# <a name="parallel-programming-in-net"></a><span data-ttu-id="e5c3e-104">.NET 中的并行编程</span><span class="sxs-lookup"><span data-stu-id="e5c3e-104">Parallel Programming in .NET</span></span>

<span data-ttu-id="e5c3e-105">许多个人计算机和工作站都有多个 CPU 内核，以便多个线程能够同时执行。</span><span class="sxs-lookup"><span data-stu-id="e5c3e-105">Many personal computers and workstations have multiple CPU cores that enable multiple threads to be executed simultaneously.</span></span> <span data-ttu-id="e5c3e-106">为了利用硬件，你可以对代码进行并行化，以将工作分摊在多个处理器上。</span><span class="sxs-lookup"><span data-stu-id="e5c3e-106">To take advantage of the hardware, you can parallelize your code to distribute work across multiple processors.</span></span>

<span data-ttu-id="e5c3e-107">过去，并行化需要线程和锁的低级操作。</span><span class="sxs-lookup"><span data-stu-id="e5c3e-107">In the past, parallelization required low-level manipulation of threads and locks.</span></span> <span data-ttu-id="e5c3e-108">Visual Studio 和 .NET 提供了运行时、类库类型和诊断工具，从而增强了对并行编程的支持。</span><span class="sxs-lookup"><span data-stu-id="e5c3e-108">Visual Studio and .NET enhance support for parallel programming by providing a runtime, class library types, and diagnostic tools.</span></span> <span data-ttu-id="e5c3e-109">.NET Framework 4 中引入的这些功能简化了并行开发。</span><span class="sxs-lookup"><span data-stu-id="e5c3e-109">These features, which were introduced in .NET Framework 4, simplify parallel development.</span></span> <span data-ttu-id="e5c3e-110">你可以通过固有方法编写高效、细化且可伸缩的并行代码，而不必直接处理线程或线程池。</span><span class="sxs-lookup"><span data-stu-id="e5c3e-110">You can write efficient, fine-grained, and scalable parallel code in a natural idiom without having to work directly with threads or the thread pool.</span></span>

<span data-ttu-id="e5c3e-111">下图简要概述了 .NET 中的并行编程体系结构。</span><span class="sxs-lookup"><span data-stu-id="e5c3e-111">The following illustration provides a high-level overview of the parallel programming architecture in .NET.</span></span>

![.NET 并行编程体系结构](./media/tpl-architecture.png)

## <a name="related-topics"></a><span data-ttu-id="e5c3e-113">相关主题</span><span class="sxs-lookup"><span data-stu-id="e5c3e-113">Related Topics</span></span>

|<span data-ttu-id="e5c3e-114">技术</span><span class="sxs-lookup"><span data-stu-id="e5c3e-114">Technology</span></span>|<span data-ttu-id="e5c3e-115">描述</span><span class="sxs-lookup"><span data-stu-id="e5c3e-115">Description</span></span>|
|----------------|-----------------|
|[<span data-ttu-id="e5c3e-116">任务并行库 (TPL)</span><span class="sxs-lookup"><span data-stu-id="e5c3e-116">Task Parallel Library (TPL)</span></span>](task-parallel-library-tpl.md)|<span data-ttu-id="e5c3e-117">提供针对 <xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType> 类的文档（包括 `For` 和 `ForEach` 循环的并行版本），还提供了针对 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 类的文档（描绘了表示异步操作的首选方式）。</span><span class="sxs-lookup"><span data-stu-id="e5c3e-117">Provides documentation for the <xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType> class, which includes parallel versions of `For` and `ForEach` loops, and also for the <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> class, which represents the preferred way to express asynchronous operations.</span></span>|
|[<span data-ttu-id="e5c3e-118">并行 LINQ (PLINQ)</span><span class="sxs-lookup"><span data-stu-id="e5c3e-118">Parallel LINQ (PLINQ)</span></span>](introduction-to-plinq.md)|<span data-ttu-id="e5c3e-119">LINQ to Objects 的并行实现，该实现显著提高了许多情况下的性能。</span><span class="sxs-lookup"><span data-stu-id="e5c3e-119">A parallel implementation of LINQ to Objects that significantly improves performance in many scenarios.</span></span>|
|[<span data-ttu-id="e5c3e-120">用于并行编程的数据结构</span><span class="sxs-lookup"><span data-stu-id="e5c3e-120">Data Structures for Parallel Programming</span></span>](data-structures-for-parallel-programming.md)|<span data-ttu-id="e5c3e-121">提供一些链接，这些链接指向有关线程安全集合类、轻量同步类型以及延迟初始化类型的文档。</span><span class="sxs-lookup"><span data-stu-id="e5c3e-121">Provides links to documentation for thread-safe collection classes, lightweight synchronization types, and types for lazy initialization.</span></span>|
|[<span data-ttu-id="e5c3e-122">并行诊断工具</span><span class="sxs-lookup"><span data-stu-id="e5c3e-122">Parallel Diagnostic Tools</span></span>](parallel-diagnostic-tools.md)|<span data-ttu-id="e5c3e-123">提供一些链接，这些链接指向任务和并行堆栈的 Visual Studio 调试器窗口和[并发可视化工具](/visualstudio/profiling/concurrency-visualizer)的文档。</span><span class="sxs-lookup"><span data-stu-id="e5c3e-123">Provides links to documentation for Visual Studio debugger windows for tasks and parallel stacks, and for the [Concurrency Visualizer](/visualstudio/profiling/concurrency-visualizer).</span></span>|
|[<span data-ttu-id="e5c3e-124">PLINQ 和 TPL 的自定义分区程序</span><span class="sxs-lookup"><span data-stu-id="e5c3e-124">Custom Partitioners for PLINQ and TPL</span></span>](custom-partitioners-for-plinq-and-tpl.md)|<span data-ttu-id="e5c3e-125">描述分区程序的工作方式，以及如何配置默认分区程序或创建新的分区程序。</span><span class="sxs-lookup"><span data-stu-id="e5c3e-125">Describes how partitioners work and how to configure the default partitioners or create a new partitioner.</span></span>|
|[<span data-ttu-id="e5c3e-126">任务计划程序</span><span class="sxs-lookup"><span data-stu-id="e5c3e-126">Task Schedulers</span></span>](xref:System.Threading.Tasks.TaskScheduler)|<span data-ttu-id="e5c3e-127">描述计划程序的工作方式，以及如何配置默认计划程序。</span><span class="sxs-lookup"><span data-stu-id="e5c3e-127">Describes how schedulers work and how the default schedulers may be configured.</span></span>|
|[<span data-ttu-id="e5c3e-128">PLINQ 和 TPL 中的 Lambda 表达式</span><span class="sxs-lookup"><span data-stu-id="e5c3e-128">Lambda Expressions in PLINQ and TPL</span></span>](lambda-expressions-in-plinq-and-tpl.md)|<span data-ttu-id="e5c3e-129">简要概述 C# 和 Visual Basic 中的 Lambda 表达式，并演示如何在 PLINQ 和任务并行库中使用这些表达式。</span><span class="sxs-lookup"><span data-stu-id="e5c3e-129">Provides a brief overview of lambda expressions in C# and Visual Basic, and shows how they are used in PLINQ and the Task Parallel Library.</span></span>|
|[<span data-ttu-id="e5c3e-130">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="e5c3e-130">For Further Reading</span></span>](for-further-reading-parallel-programming.md)|<span data-ttu-id="e5c3e-131">收录了指向其他信息以及 .NET 中并行编程示例资源的链接。</span><span class="sxs-lookup"><span data-stu-id="e5c3e-131">Provides links to additional information and sample resources for parallel programming in .NET.</span></span>|

## <a name="see-also"></a><span data-ttu-id="e5c3e-132">请参阅</span><span class="sxs-lookup"><span data-stu-id="e5c3e-132">See also</span></span>

- [<span data-ttu-id="e5c3e-133">异步概述</span><span class="sxs-lookup"><span data-stu-id="e5c3e-133">Async Overview</span></span>](../async.md)
- [<span data-ttu-id="e5c3e-134">托管线程</span><span class="sxs-lookup"><span data-stu-id="e5c3e-134">Managed Threading</span></span>](../threading/index.md)
