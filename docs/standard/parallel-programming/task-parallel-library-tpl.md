---
title: 任务并行库 (TPL)
description: 了解任务并行库 (TPL)，这是一组公共类型和 API，可简化将并行和并发添加到 .NET 中的应用程序的过程。
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- .NET, concurrency in
- .NET, parallel programming in
- Parallel Programming
ms.assetid: b8f99f43-9104-45fd-9bff-385a20488a23
ms.openlocfilehash: 596671b267484561a8697546caa5a4764242ebd3
ms.sourcegitcommit: 6d09ae36acba0b0e2ba47999f8f1a725795462a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2020
ms.locfileid: "92925228"
---
# <a name="task-parallel-library-tpl"></a><span data-ttu-id="e7eaf-103">任务并行库 (TPL)</span><span class="sxs-lookup"><span data-stu-id="e7eaf-103">Task Parallel Library (TPL)</span></span>

<span data-ttu-id="e7eaf-104">任务并行库 (TPL) 是 <xref:System.Threading?displayProperty=nameWithType> 和 <xref:System.Threading.Tasks?displayProperty=nameWithType> 空间中的一组公共类型和 API。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-104">The Task Parallel Library (TPL) is a set of public types and APIs in the <xref:System.Threading?displayProperty=nameWithType> and <xref:System.Threading.Tasks?displayProperty=nameWithType> namespaces.</span></span> <span data-ttu-id="e7eaf-105">TPL 的目的是通过简化将并行和并发添加到应用程序的过程来提高开发人员的工作效率。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-105">The purpose of the TPL is to make developers more productive by simplifying the process of adding parallelism and concurrency to applications.</span></span> <span data-ttu-id="e7eaf-106">TPL 动态缩放并发的程度以最有效地使用所有可用的处理器。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-106">The TPL scales the degree of concurrency dynamically to most efficiently use all the processors that are available.</span></span> <span data-ttu-id="e7eaf-107">此外，TPL 还处理工作分区、<xref:System.Threading.ThreadPool> 上的线程调度、取消支持、状态管理以及其他低级别的细节操作。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-107">In addition, the TPL handles the partitioning of the work, the scheduling of threads on the <xref:System.Threading.ThreadPool>, cancellation support, state management, and other low-level details.</span></span> <span data-ttu-id="e7eaf-108">通过使用 TPL，你可以在将精力集中于程序要完成的工作，同时最大程度地提高代码的性能。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-108">By using TPL, you can maximize the performance of your code while focusing on the work that your program is designed to accomplish.</span></span>  
  
 <span data-ttu-id="e7eaf-109">自 .NET Framework 4 起，首选 TPL 编写多线程代码和并行代码。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-109">Starting with .NET Framework 4, the TPL is the preferred way to write multithreaded and parallel code.</span></span> <span data-ttu-id="e7eaf-110">但是，并不是所有代码都适合并行化。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-110">However, not all code is suitable for parallelization.</span></span> <span data-ttu-id="e7eaf-111">例如，如果某个循环在每次迭代时只执行少量工作，或它在很多次迭代时都不运行，那么并行化的开销可能导致代码运行更慢。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-111">For example, if a loop performs only a small amount of work on each iteration, or it doesn't run for many iterations, then the overhead of parallelization can cause the code to run more slowly.</span></span> <span data-ttu-id="e7eaf-112">此外，像任何多线程代码一样，并行化会增加程序执行的复杂性。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-112">Furthermore, parallelization like any multithreaded code adds complexity to your program execution.</span></span> <span data-ttu-id="e7eaf-113">尽管 TPL 简化了多线程方案，但我们建议你对线程处理概念（例如，锁、死锁和争用条件）进行基本的了解，以便能够有效地使用 TPL。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-113">Although the TPL simplifies multithreaded scenarios, we recommend that you have a basic understanding of threading concepts, for example, locks, deadlocks, and race conditions, so that you can use the TPL effectively.</span></span>  
  
## <a name="related-articles"></a><span data-ttu-id="e7eaf-114">相关文章</span><span class="sxs-lookup"><span data-stu-id="e7eaf-114">Related articles</span></span>  
  
|<span data-ttu-id="e7eaf-115">Title</span><span class="sxs-lookup"><span data-stu-id="e7eaf-115">Title</span></span>|<span data-ttu-id="e7eaf-116">描述</span><span class="sxs-lookup"><span data-stu-id="e7eaf-116">Description</span></span>|  
|-|-|  
|[<span data-ttu-id="e7eaf-117">数据并行</span><span class="sxs-lookup"><span data-stu-id="e7eaf-117">Data Parallelism</span></span>](data-parallelism-task-parallel-library.md)|<span data-ttu-id="e7eaf-118">描述如何创建并行的 `for` 和 `foreach` 循环（在 Visual Basic 中为 `For` 和 `For Each`）。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-118">Describes how to create parallel `for` and `foreach` loops (`For` and `For Each` in Visual Basic).</span></span>|  
|[<span data-ttu-id="e7eaf-119">基于任务的异步编程</span><span class="sxs-lookup"><span data-stu-id="e7eaf-119">Task-based Asynchronous Programming</span></span>](task-based-asynchronous-programming.md)|<span data-ttu-id="e7eaf-120">描述如何通过使用 <xref:System.Threading.Tasks.Parallel.Invoke%2A?displayProperty=nameWithType> 隐式创建和运行任务，或通过直接使用 <xref:System.Threading.Tasks.Task> 对象显式创建和运行任务。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-120">Describes how to create and run tasks implicitly by using <xref:System.Threading.Tasks.Parallel.Invoke%2A?displayProperty=nameWithType> or explicitly by using <xref:System.Threading.Tasks.Task> objects directly.</span></span>|  
|[<span data-ttu-id="e7eaf-121">数据流</span><span class="sxs-lookup"><span data-stu-id="e7eaf-121">Dataflow</span></span>](dataflow-task-parallel-library.md)|<span data-ttu-id="e7eaf-122">描述如何使用 TPL 数据流库中的数据流组件处理多项运算，这些运算必须彼此通信，或在数据可用时处理数据。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-122">Describes how to use the dataflow components in the TPL Dataflow Library to handle multiple operations that must communicate with one another or to process data as it becomes available.</span></span>|
|[<span data-ttu-id="e7eaf-123">数据和任务并行的潜在问题</span><span class="sxs-lookup"><span data-stu-id="e7eaf-123">Potential Pitfalls in Data and Task Parallelism</span></span>](potential-pitfalls-in-data-and-task-parallelism.md)|<span data-ttu-id="e7eaf-124">描述一些常见缺陷以及如何避免它们。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-124">Describes some common pitfalls and how to avoid them.</span></span>|  
|[<span data-ttu-id="e7eaf-125">并行 LINQ (PLINQ)</span><span class="sxs-lookup"><span data-stu-id="e7eaf-125">Parallel LINQ (PLINQ)</span></span>](introduction-to-plinq.md)|<span data-ttu-id="e7eaf-126">描述如何使用 LINQ 查询实现数据并行化。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-126">Describes how to achieve data parallelism with LINQ queries.</span></span>|  
|[<span data-ttu-id="e7eaf-127">并行编程</span><span class="sxs-lookup"><span data-stu-id="e7eaf-127">Parallel Programming</span></span>](index.md)|<span data-ttu-id="e7eaf-128">.NET 并行编程的顶级节点。</span><span class="sxs-lookup"><span data-stu-id="e7eaf-128">Top level node for .NET parallel programming.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="e7eaf-129">请参阅</span><span class="sxs-lookup"><span data-stu-id="e7eaf-129">See also</span></span>

- [<span data-ttu-id="e7eaf-130">使用 .NET Core 和 .NET Standard 并行编程的示例</span><span class="sxs-lookup"><span data-stu-id="e7eaf-130">Samples for Parallel Programming with the .NET Core & .NET Standard</span></span>](/samples/browse/?products=dotnet-core%2Cdotnet-standard&term=parallel)
