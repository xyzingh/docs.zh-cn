---
title: 垃圾回收和性能
description: 阅读与垃圾回收和内存使用情况相关的问题。 了解如何最大程度地降低垃圾回收对应用程序的影响。
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- garbage collection, troubleshooting
- garbage collection, performance
ms.assetid: c203467b-e95c-4ccf-b30b-953eb3463134
ms.openlocfilehash: 7c4a61c1e5e735313a355bcab348fd6ef58a8686
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93062966"
---
# <a name="garbage-collection-and-performance"></a><span data-ttu-id="947a2-104">垃圾回收和性能</span><span class="sxs-lookup"><span data-stu-id="947a2-104">Garbage Collection and Performance</span></span>

<span data-ttu-id="947a2-105">本主题介绍与垃圾回收和内存使用情况相关的问题。</span><span class="sxs-lookup"><span data-stu-id="947a2-105">This topic describes issues related to garbage collection and memory usage.</span></span> <span data-ttu-id="947a2-106">它解决了关于托管堆的问题，并解释了如何最小化垃圾回收对应用程序的影响。</span><span class="sxs-lookup"><span data-stu-id="947a2-106">It addresses issues that pertain to the managed heap and explains how to minimize the effect of garbage collection on your applications.</span></span> <span data-ttu-id="947a2-107">每个问题具有访问可用来调查问题的过程的链接。</span><span class="sxs-lookup"><span data-stu-id="947a2-107">Each issue has links to procedures that you can use to investigate problems.</span></span>

## <a name="performance-analysis-tools"></a><span data-ttu-id="947a2-108">性能分析工具</span><span class="sxs-lookup"><span data-stu-id="947a2-108">Performance Analysis Tools</span></span>

<span data-ttu-id="947a2-109">以下各节介绍了可用于调查内存使用情况和垃圾回收问题的工具。</span><span class="sxs-lookup"><span data-stu-id="947a2-109">The following sections describe the tools that are available for investigating memory usage and garbage collection issues.</span></span> <span data-ttu-id="947a2-110">本主题中稍后提供的[过程](#performance-check-procedures)将引用这些工具。</span><span class="sxs-lookup"><span data-stu-id="947a2-110">The [procedures](#performance-check-procedures) provided later in this topic refer to these tools.</span></span>

### <a name="memory-performance-counters"></a><span data-ttu-id="947a2-111">内存性能计数器</span><span class="sxs-lookup"><span data-stu-id="947a2-111">Memory Performance Counters</span></span>

<span data-ttu-id="947a2-112">可以使用性能计数器来收集性能数据。</span><span class="sxs-lookup"><span data-stu-id="947a2-112">You can use performance counters to gather performance data.</span></span> <span data-ttu-id="947a2-113">有关说明，请参阅[运行时分析](../../framework/debug-trace-profile/runtime-profiling.md)。</span><span class="sxs-lookup"><span data-stu-id="947a2-113">For instructions, see [Runtime Profiling](../../framework/debug-trace-profile/runtime-profiling.md).</span></span> <span data-ttu-id="947a2-114">如 [.NET 中的性能计数器](../../framework/debug-trace-profile/performance-counters.md)中所述，性能计数器的 .NET CLR 内存类别提供有关垃圾回收器的信息。</span><span class="sxs-lookup"><span data-stu-id="947a2-114">The .NET CLR Memory category of performance counters, as described in [Performance Counters in .NET](../../framework/debug-trace-profile/performance-counters.md), provides information about the garbage collector.</span></span>

### <a name="debugging-with-sos"></a><span data-ttu-id="947a2-115">用 SOS 调试</span><span class="sxs-lookup"><span data-stu-id="947a2-115">Debugging with SOS</span></span>

<span data-ttu-id="947a2-116">可以使用 [Windows 调试器 (WinDbg)](/windows-hardware/drivers/debugger/index) 检查托管堆上的对象。</span><span class="sxs-lookup"><span data-stu-id="947a2-116">You can use the [Windows Debugger (WinDbg)](/windows-hardware/drivers/debugger/index) to inspect objects on the managed heap.</span></span>

<span data-ttu-id="947a2-117">若要安装 WinDbg，请从[下载 Windows 调试工具](/windows-hardware/drivers/debugger/debugger-download-tools)页安装 Windows 调试工具。</span><span class="sxs-lookup"><span data-stu-id="947a2-117">To install WinDbg, install Debugging Tools for Windows from the [Download Debugging Tools for Windows](/windows-hardware/drivers/debugger/debugger-download-tools) page.</span></span>

### <a name="garbage-collection-etw-events"></a><span data-ttu-id="947a2-118">垃圾回收 ETW 事件</span><span class="sxs-lookup"><span data-stu-id="947a2-118">Garbage Collection ETW Events</span></span>

<span data-ttu-id="947a2-119">Windows 事件跟踪 (ETW) 是一个跟踪系统，对由 .NET 提供的分析和调试支持提供补充。</span><span class="sxs-lookup"><span data-stu-id="947a2-119">Event tracing for Windows (ETW) is a tracing system that supplements the profiling and debugging support provided by .NET.</span></span> <span data-ttu-id="947a2-120">从 .NET Framework 4 开始，[垃圾回收 ETW 事件](../../framework/performance/garbage-collection-etw-events.md)将捕获有用信息，用于从统计的角度来分析托管堆。</span><span class="sxs-lookup"><span data-stu-id="947a2-120">Starting with .NET Framework 4, [garbage collection ETW events](../../framework/performance/garbage-collection-etw-events.md) capture useful information for analyzing the managed heap from a statistical point of view.</span></span> <span data-ttu-id="947a2-121">例如，在将要发生垃圾回收时引发的 `GCStart_V1` 事件提供了以下信息：</span><span class="sxs-lookup"><span data-stu-id="947a2-121">For example, the `GCStart_V1` event, which is raised when a garbage collection is about to occur, provides the following information:</span></span>

- <span data-ttu-id="947a2-122">正在收集哪一代对象。</span><span class="sxs-lookup"><span data-stu-id="947a2-122">Which generation of objects is being collected.</span></span>

- <span data-ttu-id="947a2-123">是什么触发了垃圾回收。</span><span class="sxs-lookup"><span data-stu-id="947a2-123">What triggered the garbage collection.</span></span>

- <span data-ttu-id="947a2-124">垃圾回收的类型（并发或非并发）。</span><span class="sxs-lookup"><span data-stu-id="947a2-124">Type of garbage collection (concurrent or not concurrent).</span></span>

<span data-ttu-id="947a2-125">ETW 事件日志有效，且不会掩盖与垃圾回收相关的任何性能问题。</span><span class="sxs-lookup"><span data-stu-id="947a2-125">ETW event logging is efficient and will not mask any performance problems associated with garbage collection.</span></span> <span data-ttu-id="947a2-126">一个进程可以通过结合 ETW 事件来提供其自身的事件。</span><span class="sxs-lookup"><span data-stu-id="947a2-126">A process can provide its own events in conjunction with ETW events.</span></span> <span data-ttu-id="947a2-127">登录后，可以关联应用程序事件和垃圾回收事件，以确定如何以及何时出现堆问题。</span><span class="sxs-lookup"><span data-stu-id="947a2-127">When logged, both the application's events and the garbage collection events can be correlated to determine how and when heap problems occur.</span></span> <span data-ttu-id="947a2-128">例如，服务器应用程序可以在客户端请求开始和结束时提供事件。</span><span class="sxs-lookup"><span data-stu-id="947a2-128">For example, a server application could provide events at the start and end of a client request.</span></span>

### <a name="the-profiling-api"></a><span data-ttu-id="947a2-129">分析 API</span><span class="sxs-lookup"><span data-stu-id="947a2-129">The Profiling API</span></span>

<span data-ttu-id="947a2-130">公共语言运行时 (CLR) 分析接口将提供有关垃圾回收期间受影响对象的详细信息。</span><span class="sxs-lookup"><span data-stu-id="947a2-130">The common language runtime (CLR) profiling interfaces provide detailed information about the objects that were affected during garbage collection.</span></span> <span data-ttu-id="947a2-131">垃圾回收开始和结束时，可以通知探查器。</span><span class="sxs-lookup"><span data-stu-id="947a2-131">A profiler can be notified when a garbage collection starts and ends.</span></span> <span data-ttu-id="947a2-132">它可以提供有关托管堆上对象的报告，其中包括每一代对象的标识。</span><span class="sxs-lookup"><span data-stu-id="947a2-132">It can provide reports about the objects on the managed heap, including an identification of objects in each generation.</span></span> <span data-ttu-id="947a2-133">有关详细信息，请参阅[分析概述](../../framework/unmanaged-api/profiling/profiling-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="947a2-133">For more information, see [Profiling Overview](../../framework/unmanaged-api/profiling/profiling-overview.md).</span></span>

<span data-ttu-id="947a2-134">探查器可以提供全面的信息。</span><span class="sxs-lookup"><span data-stu-id="947a2-134">Profilers can provide comprehensive information.</span></span> <span data-ttu-id="947a2-135">但是，复杂的探查器可能会修改应用程序的行为。</span><span class="sxs-lookup"><span data-stu-id="947a2-135">However, complex profilers can potentially modify an application's behavior.</span></span>

### <a name="application-domain-resource-monitoring"></a><span data-ttu-id="947a2-136">应用程序域资源监控</span><span class="sxs-lookup"><span data-stu-id="947a2-136">Application Domain Resource Monitoring</span></span>

<span data-ttu-id="947a2-137">从 .NET Framework 4 开始，应用程序域资源监视 (ARM) 使主机可以通过应用程序域监视 CPU 和内存使用情况。</span><span class="sxs-lookup"><span data-stu-id="947a2-137">Starting with .NET Framework 4, Application domain resource monitoring (ARM) enables hosts to monitor CPU and memory usage by application domain.</span></span> <span data-ttu-id="947a2-138">有关详细信息，请参阅[应用程序域资源监控](app-domain-resource-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="947a2-138">For more information, see [Application Domain Resource Monitoring](app-domain-resource-monitoring.md).</span></span>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="947a2-139">故障排除性能问题</span><span class="sxs-lookup"><span data-stu-id="947a2-139">Troubleshooting Performance Issues</span></span>

<span data-ttu-id="947a2-140">第一步是[确定问题是否确实为垃圾回收](#IsGC)。</span><span class="sxs-lookup"><span data-stu-id="947a2-140">The first step is to [determine whether the issue is actually garbage collection](#IsGC).</span></span> <span data-ttu-id="947a2-141">如果确定是，则从以下列表进行选择，以解决该问题。</span><span class="sxs-lookup"><span data-stu-id="947a2-141">If you determine that it is, select from the following list to troubleshoot the problem.</span></span>

- [<span data-ttu-id="947a2-142">引发内存不足异常</span><span class="sxs-lookup"><span data-stu-id="947a2-142">An out-of-memory exception is thrown</span></span>](#Issue_OOM)

- [<span data-ttu-id="947a2-143">进程占用过多内存</span><span class="sxs-lookup"><span data-stu-id="947a2-143">The process uses too much memory</span></span>](#Issue_TooMuchMemory)

- [<span data-ttu-id="947a2-144">垃圾回收器回收对象的速度不够快</span><span class="sxs-lookup"><span data-stu-id="947a2-144">The garbage collector does not reclaim objects fast enough</span></span>](#Issue_NotFastEnough)

- [<span data-ttu-id="947a2-145">托管堆太零碎</span><span class="sxs-lookup"><span data-stu-id="947a2-145">The managed heap is too fragmented</span></span>](#Issue_Fragmentation)

- [<span data-ttu-id="947a2-146">垃圾回收暂停时间太长</span><span class="sxs-lookup"><span data-stu-id="947a2-146">Garbage collection pauses are too long</span></span>](#Issue_LongPauses)

- [<span data-ttu-id="947a2-147">第 0 代太大</span><span class="sxs-lookup"><span data-stu-id="947a2-147">Generation 0 is too big</span></span>](#Issue_Gen0)

- [<span data-ttu-id="947a2-148">垃圾回收期间的 CPU 使用率太高</span><span class="sxs-lookup"><span data-stu-id="947a2-148">CPU usage during a garbage collection is too high</span></span>](#Issue_HighCPU)

<a name="Issue_OOM"></a>

### <a name="issue-an-out-of-memory-exception-is-thrown"></a><span data-ttu-id="947a2-149">问题：抛出内存不足异常</span><span class="sxs-lookup"><span data-stu-id="947a2-149">Issue: An Out-of-Memory Exception Is Thrown</span></span>

<span data-ttu-id="947a2-150">对于引发的托管 <xref:System.OutOfMemoryException>，存在以下两种合理的情况：</span><span class="sxs-lookup"><span data-stu-id="947a2-150">There are two legitimate cases for a managed <xref:System.OutOfMemoryException> to be thrown:</span></span>

- <span data-ttu-id="947a2-151">虚拟内存不足。</span><span class="sxs-lookup"><span data-stu-id="947a2-151">Running out of virtual memory.</span></span>

  <span data-ttu-id="947a2-152">垃圾回收器按预先确定大小的分段来分配系统内存。</span><span class="sxs-lookup"><span data-stu-id="947a2-152">The garbage collector allocates memory from the system in segments of a pre-determined size.</span></span> <span data-ttu-id="947a2-153">如果分配需要其他段，但在进程的虚拟内存空间中没有剩余的连续可用块了，则托管堆的分配将失败。</span><span class="sxs-lookup"><span data-stu-id="947a2-153">If an allocation requires an additional segment, but there is no contiguous free block left in the process's virtual memory space, the allocation for the managed heap will fail.</span></span>

- <span data-ttu-id="947a2-154">没有足够的物理内存来分配。</span><span class="sxs-lookup"><span data-stu-id="947a2-154">Not having enough physical memory to allocate.</span></span>

|<span data-ttu-id="947a2-155">性能检查</span><span class="sxs-lookup"><span data-stu-id="947a2-155">Performance checks</span></span>|
|------------------------|
|[<span data-ttu-id="947a2-156">确定是否已托管内存不足异常。</span><span class="sxs-lookup"><span data-stu-id="947a2-156">Determine whether the out-of-memory exception is managed.</span></span>](#OOMIsManaged)<br /><br /> [<span data-ttu-id="947a2-157">确定可保留的虚拟内存量。</span><span class="sxs-lookup"><span data-stu-id="947a2-157">Determine how much virtual memory can be reserved.</span></span>](#GetVM)<br /><br /> [<span data-ttu-id="947a2-158">确定是否有足够的物理内存。</span><span class="sxs-lookup"><span data-stu-id="947a2-158">Determine whether there is enough physical memory.</span></span>](#Physical)|

<span data-ttu-id="947a2-159">如果确定异常不合法，请使用以下信息与 Microsoft 客户服务和支持联系：</span><span class="sxs-lookup"><span data-stu-id="947a2-159">If you determine that the exception is not legitimate, contact Microsoft Customer Service and Support with the following information:</span></span>

- <span data-ttu-id="947a2-160">带有托管内存不足异常的堆栈。</span><span class="sxs-lookup"><span data-stu-id="947a2-160">The stack with the managed out-of-memory exception.</span></span>

- <span data-ttu-id="947a2-161">完整内存转储。</span><span class="sxs-lookup"><span data-stu-id="947a2-161">Full memory dump.</span></span>

- <span data-ttu-id="947a2-162">证明这不是合法内存不足异常的数据包括显示虚拟或物理内存不是问题的数据。</span><span class="sxs-lookup"><span data-stu-id="947a2-162">Data that proves that it is not a legitimate out-of-memory exception, including data that shows that virtual or physical memory is not an issue.</span></span>

<a name="Issue_TooMuchMemory"></a>

### <a name="issue-the-process-uses-too-much-memory"></a><span data-ttu-id="947a2-163">问题：进程占用过多内存</span><span class="sxs-lookup"><span data-stu-id="947a2-163">Issue: The Process Uses Too Much Memory</span></span>

<span data-ttu-id="947a2-164">通常会假设 Windows 任务管理器“性能”选项卡上的内存使用量显示可以指示何时使用了太多内存。</span><span class="sxs-lookup"><span data-stu-id="947a2-164">A common assumption is that the memory usage display on the **Performance** tab of Windows Task Manager can indicate when too much memory is being used.</span></span> <span data-ttu-id="947a2-165">然而，该显示与工作集相关；它不提供有关虚拟内存使用量的信息。</span><span class="sxs-lookup"><span data-stu-id="947a2-165">However, that display pertains to the working set; it does not provide information about virtual memory usage.</span></span>

<span data-ttu-id="947a2-166">如果确定问题是托管堆引发的，必须测量一段时间的托管堆，以确定模式。</span><span class="sxs-lookup"><span data-stu-id="947a2-166">If you determine that the issue is caused by the managed heap, you must measure the managed heap over time to determine any patterns.</span></span>

<span data-ttu-id="947a2-167">如果确定问题不是托管堆引发的，则必须使用本地调试。</span><span class="sxs-lookup"><span data-stu-id="947a2-167">If you determine that the problem is not caused by the managed heap, you must use native debugging.</span></span>

|<span data-ttu-id="947a2-168">性能检查</span><span class="sxs-lookup"><span data-stu-id="947a2-168">Performance checks</span></span>|
|------------------------|
|[<span data-ttu-id="947a2-169">确定可保留的虚拟内存量。</span><span class="sxs-lookup"><span data-stu-id="947a2-169">Determine how much virtual memory can be reserved.</span></span>](#GetVM)<br /><br /> [<span data-ttu-id="947a2-170">确定托管堆的内存提交量。</span><span class="sxs-lookup"><span data-stu-id="947a2-170">Determine how much memory the managed heap is committing.</span></span>](#ManagedHeapCommit)<br /><br /> [<span data-ttu-id="947a2-171">确定托管堆的内存保留量。</span><span class="sxs-lookup"><span data-stu-id="947a2-171">Determine how much memory the managed heap reserves.</span></span>](#ManagedHeapReserve)<br /><br /> [<span data-ttu-id="947a2-172">确定第 2 代中的大型对象。</span><span class="sxs-lookup"><span data-stu-id="947a2-172">Determine large objects in generation 2.</span></span>](#ExamineGen2)<br /><br /> [<span data-ttu-id="947a2-173">确定对对象的引用。</span><span class="sxs-lookup"><span data-stu-id="947a2-173">Determine references to objects.</span></span>](#ObjRef)|

<a name="Issue_NotFastEnough"></a>

### <a name="issue-the-garbage-collector-does-not-reclaim-objects-fast-enough"></a><span data-ttu-id="947a2-174">问题：垃圾回收器回收对象的速度不够快</span><span class="sxs-lookup"><span data-stu-id="947a2-174">Issue: The Garbage Collector Does Not Reclaim Objects Fast Enough</span></span>

<span data-ttu-id="947a2-175">当出现对象好像未按垃圾回收的预期进行回收的情况时，必须确定是否存在任何对这些对象的强引用。</span><span class="sxs-lookup"><span data-stu-id="947a2-175">When it appears as if objects are not being reclaimed as expected for garbage collection, you must determine if there are any strong references to those objects.</span></span>

<span data-ttu-id="947a2-176">如果没有对包含死对象的一代进行垃圾回收，这表示尚未运行死对象的终结器，你也可能会遇到以上问题。</span><span class="sxs-lookup"><span data-stu-id="947a2-176">You may also encounter this issue if there has been no garbage collection for the generation that contains a dead object, which indicates that the finalizer for the dead object has not been run.</span></span> <span data-ttu-id="947a2-177">例如，当正在运行一个单线程单元 (STA) 应用程序并且服务终结器队列的线程不能调用至其中时，可能发生这种问题。</span><span class="sxs-lookup"><span data-stu-id="947a2-177">For example, this is possible when you are running a single-threaded apartment (STA) application and the thread that services the finalizer queue cannot call into it.</span></span>

|<span data-ttu-id="947a2-178">性能检查</span><span class="sxs-lookup"><span data-stu-id="947a2-178">Performance checks</span></span>|
|------------------------|
|[<span data-ttu-id="947a2-179">检查对对象的引用。</span><span class="sxs-lookup"><span data-stu-id="947a2-179">Check references to objects.</span></span>](#ObjRef)<br /><br /> [<span data-ttu-id="947a2-180">确定是否已运行终结器。</span><span class="sxs-lookup"><span data-stu-id="947a2-180">Determine whether a finalizer has been run.</span></span>](#Induce)<br /><br /> [<span data-ttu-id="947a2-181">确定是否存在等待终结的对象。</span><span class="sxs-lookup"><span data-stu-id="947a2-181">Determine whether there are objects waiting to be finalized.</span></span>](#Finalize)|

<a name="Issue_Fragmentation"></a>

### <a name="issue-the-managed-heap-is-too-fragmented"></a><span data-ttu-id="947a2-182">问题：托管堆太零碎</span><span class="sxs-lookup"><span data-stu-id="947a2-182">Issue: The Managed Heap Is Too fragmented</span></span>

<span data-ttu-id="947a2-183">碎片级别将计算为可用空间占这一代已分配的总内存的比率。</span><span class="sxs-lookup"><span data-stu-id="947a2-183">The fragmentation level is calculated as the ratio of free space over the total allocated memory for the generation.</span></span> <span data-ttu-id="947a2-184">对于第 2 代，可接受的碎片级别不能超过 20%。</span><span class="sxs-lookup"><span data-stu-id="947a2-184">For generation 2, an acceptable level of fragmentation is no more than 20%.</span></span> <span data-ttu-id="947a2-185">因为第 2 代可以变得很大，所以碎片的比率比绝对值更重要。</span><span class="sxs-lookup"><span data-stu-id="947a2-185">Because generation 2 can get very big, the ratio of fragmentation is more important than the absolute value.</span></span>

<span data-ttu-id="947a2-186">第 0 代中存在大量可用空间，这不是问题，因为新的对象将在其中进行分配。</span><span class="sxs-lookup"><span data-stu-id="947a2-186">Having lots of free space in generation 0 is not a problem because this is the generation where new objects are allocated.</span></span>

<span data-ttu-id="947a2-187">碎片始终出现在大型对象堆中，因为它没有进行压缩。</span><span class="sxs-lookup"><span data-stu-id="947a2-187">Fragmentation always occurs in the large object heap because it is not compacted.</span></span> <span data-ttu-id="947a2-188">相邻的可用对象会自然地折叠至一个单个的空间，以满足大型对象的分配请求。</span><span class="sxs-lookup"><span data-stu-id="947a2-188">Free objects that are adjacent are naturally collapsed into a single space to satisfy large object allocation requests.</span></span>

<span data-ttu-id="947a2-189">在第 1 代和第 2 代中，碎片可能会成为问题。</span><span class="sxs-lookup"><span data-stu-id="947a2-189">Fragmentation can become a problem in generation 1 and generation 2.</span></span> <span data-ttu-id="947a2-190">如果它们在垃圾回收后还有大量的可用空间，则应用程序对象的使用可能需要进行修改，并且应考虑重新评估长期对象的生存期。</span><span class="sxs-lookup"><span data-stu-id="947a2-190">If these generations have a large amount of free space after a garbage collection, an application's object usage may need modification, and you should consider re-evaluating the lifetime of long-term objects.</span></span>

<span data-ttu-id="947a2-191">固定对象过多可能会增加碎片。</span><span class="sxs-lookup"><span data-stu-id="947a2-191">Excessive pinning of objects can increase fragmentation.</span></span> <span data-ttu-id="947a2-192">如果碎片太多，则可以固定许多对象。</span><span class="sxs-lookup"><span data-stu-id="947a2-192">If fragmentation is high, too many objects could have been pinned.</span></span>

<span data-ttu-id="947a2-193">如果虚拟内存的碎片阻止垃圾回收器添加段，原因可能是下列之一：</span><span class="sxs-lookup"><span data-stu-id="947a2-193">If fragmentation of virtual memory is preventing the garbage collector from adding segments, the causes could be one of the following:</span></span>

- <span data-ttu-id="947a2-194">频繁加载和卸载许多小的程序集。</span><span class="sxs-lookup"><span data-stu-id="947a2-194">Frequent loading and unloading of many small assemblies.</span></span>

- <span data-ttu-id="947a2-195">与非托管代码互操作时，保留了太多对 COM 对象的引用。</span><span class="sxs-lookup"><span data-stu-id="947a2-195">Holding too many references to COM objects when interoperating with unmanaged code.</span></span>

- <span data-ttu-id="947a2-196">大型暂时性对象的创建会导致大型对象堆频繁分配和释放堆段。</span><span class="sxs-lookup"><span data-stu-id="947a2-196">Creation of large transient objects, which causes the large object heap to allocate and free heap segments frequently.</span></span>

  <span data-ttu-id="947a2-197">当承载 CLR 时，应用程序可以请求垃圾回收器保留其片段。</span><span class="sxs-lookup"><span data-stu-id="947a2-197">When hosting the CLR, an application can request that the garbage collector retain its segments.</span></span> <span data-ttu-id="947a2-198">这将减少段分配的频率。</span><span class="sxs-lookup"><span data-stu-id="947a2-198">This reduces the frequency of segment allocations.</span></span> <span data-ttu-id="947a2-199">通过使用 [STARTUP_FLAGS 枚举](../../framework/unmanaged-api/hosting/startup-flags-enumeration.md)中的 STARTUP_HOARD_GC_VM 标志来完成。</span><span class="sxs-lookup"><span data-stu-id="947a2-199">This is accomplished by using the STARTUP_HOARD_GC_VM flag in the [STARTUP_FLAGS Enumeration](../../framework/unmanaged-api/hosting/startup-flags-enumeration.md).</span></span>

|<span data-ttu-id="947a2-200">性能检查</span><span class="sxs-lookup"><span data-stu-id="947a2-200">Performance checks</span></span>|
|------------------------|
|[<span data-ttu-id="947a2-201">确定托管堆中的可用空间量。</span><span class="sxs-lookup"><span data-stu-id="947a2-201">Determine the amount of free space in the managed heap.</span></span>](#Fragmented)<br /><br /> [<span data-ttu-id="947a2-202">确定固定对象的数目。</span><span class="sxs-lookup"><span data-stu-id="947a2-202">Determine the number of pinned objects.</span></span>](#Pinned)|

<span data-ttu-id="947a2-203">如果认为没有出现碎片的合理原因，请与 Microsoft 客户服务和支持联系。</span><span class="sxs-lookup"><span data-stu-id="947a2-203">If you think that there is no legitimate cause for the fragmentation, contact Microsoft Customer Service and Support.</span></span>

<a name="Issue_LongPauses"></a>

### <a name="issue-garbage-collection-pauses-are-too-long"></a><span data-ttu-id="947a2-204">问题：垃圾回收暂停时间太长</span><span class="sxs-lookup"><span data-stu-id="947a2-204">Issue: Garbage Collection Pauses Are Too Long</span></span>

<span data-ttu-id="947a2-205">由于垃圾回收软实时操作，因此应用程序必须能够容忍暂停。</span><span class="sxs-lookup"><span data-stu-id="947a2-205">Garbage collection operates in soft real time, so an application must be able to tolerate some pauses.</span></span> <span data-ttu-id="947a2-206">软实时的一个衡量标准是 95% 的操作必须按时完成。</span><span class="sxs-lookup"><span data-stu-id="947a2-206">A criterion for soft real time is that 95% of the operations must finish on time.</span></span>

<span data-ttu-id="947a2-207">在并发垃圾回收中，允许托管线程在一个回收过程中运行，这意味着暂停时间会非常短。</span><span class="sxs-lookup"><span data-stu-id="947a2-207">In concurrent garbage collection, managed threads are allowed to run during a collection, which means that pauses are very minimal.</span></span>

<span data-ttu-id="947a2-208">短暂的垃圾回收（第 0 代和第 1 代）只会持续几毫秒，所以减少暂停时间通常是不可行的。</span><span class="sxs-lookup"><span data-stu-id="947a2-208">Ephemeral garbage collections (generations 0 and 1) last only a few milliseconds, so decreasing pauses is usually not feasible.</span></span> <span data-ttu-id="947a2-209">然而，你可以通过更改应用程序的分配请求的模式，在第 2 代回收中减少暂停。</span><span class="sxs-lookup"><span data-stu-id="947a2-209">However, you can decrease the pauses in generation 2 collections by changing the pattern of allocation requests by an application.</span></span>

<span data-ttu-id="947a2-210">另一个更准确的方法是使用[垃圾回收 ETW 事件](../../framework/performance/garbage-collection-etw-events.md)。</span><span class="sxs-lookup"><span data-stu-id="947a2-210">Another, more accurate, method is to use [garbage collection ETW events](../../framework/performance/garbage-collection-etw-events.md).</span></span> <span data-ttu-id="947a2-211">可以通过为某个事件序列添加时间戳的差异来查找回收的计时。</span><span class="sxs-lookup"><span data-stu-id="947a2-211">You can find the timings for collections by adding the time stamp differences for a sequence of events.</span></span> <span data-ttu-id="947a2-212">整个集合序列包括暂停执行引擎、垃圾回收本身以及恢复执行引擎。</span><span class="sxs-lookup"><span data-stu-id="947a2-212">The whole collection sequence includes suspension of the execution engine, the garbage collection itself, and the resumption of the execution engine.</span></span>

<span data-ttu-id="947a2-213">可以使用[垃圾回收通知](notifications.md)，确定服务器是否将要进行第 2 代回收，以及将请求重新路由到另一个服务器是否可以减轻任何暂停问题。</span><span class="sxs-lookup"><span data-stu-id="947a2-213">You can use [Garbage Collection Notifications](notifications.md) to determine whether a server is about to have a generation 2 collection, and whether rerouting requests to another server could ease any problems with pauses.</span></span>

|<span data-ttu-id="947a2-214">性能检查</span><span class="sxs-lookup"><span data-stu-id="947a2-214">Performance checks</span></span>|
|------------------------|
|[<span data-ttu-id="947a2-215">确定垃圾回收中的时长。</span><span class="sxs-lookup"><span data-stu-id="947a2-215">Determine the length of time in a garbage collection.</span></span>](#TimeInGC)<br /><br /> [<span data-ttu-id="947a2-216">确定导致垃圾回收的原因。</span><span class="sxs-lookup"><span data-stu-id="947a2-216">Determine what caused a garbage collection.</span></span>](#Triggered)|

<a name="Issue_Gen0"></a>

### <a name="issue-generation-0-is-too-big"></a><span data-ttu-id="947a2-217">问题：第 0 代太大</span><span class="sxs-lookup"><span data-stu-id="947a2-217">Issue: Generation 0 Is Too Big</span></span>

<span data-ttu-id="947a2-218">第 0 代可能在 64 位系统上有更多的对象，尤其是当使用服务器垃圾回收而不是工作站垃圾回收时。</span><span class="sxs-lookup"><span data-stu-id="947a2-218">Generation 0 is likely to have a larger number of objects on a 64-bit system, especially when you use server garbage collection instead of workstation garbage collection.</span></span> <span data-ttu-id="947a2-219">这是因为触发 0 代垃圾回收的阈值在这些环境中更高，且 0 代回收可以变得更大。</span><span class="sxs-lookup"><span data-stu-id="947a2-219">This is because the threshold to trigger a generation 0 garbage collection is higher in these environments, and generation 0 collections can get much bigger.</span></span> <span data-ttu-id="947a2-220">触发垃圾回收之前，当应用程序分配更多的内存时，性能将会提高。</span><span class="sxs-lookup"><span data-stu-id="947a2-220">Performance is improved when an application allocates more memory before a garbage collection is triggered.</span></span>

<a name="Issue_HighCPU"></a>

### <a name="issue-cpu-usage-during-a-garbage-collection-is-too-high"></a><span data-ttu-id="947a2-221">问题：垃圾回收期间的 CPU 使用率太高</span><span class="sxs-lookup"><span data-stu-id="947a2-221">Issue: CPU Usage During a Garbage Collection Is Too High</span></span>

<span data-ttu-id="947a2-222">在垃圾回收期间，CPU 的使用率会很高。</span><span class="sxs-lookup"><span data-stu-id="947a2-222">CPU usage will be high during a garbage collection.</span></span> <span data-ttu-id="947a2-223">如果在垃圾回收中花费大量的处理时间，则回收的数量将过于频繁或回收的持续时间将过长。</span><span class="sxs-lookup"><span data-stu-id="947a2-223">If a significant amount of process time is spent in a garbage collection, the number of collections is too frequent or the collection is lasting too long.</span></span> <span data-ttu-id="947a2-224">托管堆上增加的对象分配率将导致垃圾回收更频繁地发生。</span><span class="sxs-lookup"><span data-stu-id="947a2-224">An increased allocation rate of objects on the managed heap causes garbage collection to occur more frequently.</span></span> <span data-ttu-id="947a2-225">减少分配速率可减少垃圾回收的频率。</span><span class="sxs-lookup"><span data-stu-id="947a2-225">Decreasing the allocation rate reduces the frequency of garbage collections.</span></span>

<span data-ttu-id="947a2-226">可以通过使用 `Allocated Bytes/second` 性能计数器来监视分配速率。</span><span class="sxs-lookup"><span data-stu-id="947a2-226">You can monitor allocation rates by using the `Allocated Bytes/second` performance counter.</span></span> <span data-ttu-id="947a2-227">有关更多信息，请参阅 [.NET 中的性能计数器](../../framework/debug-trace-profile/performance-counters.md)。</span><span class="sxs-lookup"><span data-stu-id="947a2-227">For more information, see [Performance Counters in .NET](../../framework/debug-trace-profile/performance-counters.md).</span></span>

<span data-ttu-id="947a2-228">收集的持续时间是分配后幸存对象数量的主要因素。</span><span class="sxs-lookup"><span data-stu-id="947a2-228">The duration of a collection is primarily a factor of the number of objects that survive after allocation.</span></span> <span data-ttu-id="947a2-229">如果有许多对象仍需收集，则垃圾回收器必须要检查大量的内存。</span><span class="sxs-lookup"><span data-stu-id="947a2-229">The garbage collector must go through a large amount of memory if many objects remain to be collected.</span></span> <span data-ttu-id="947a2-230">压缩幸存对象的工作很耗时。</span><span class="sxs-lookup"><span data-stu-id="947a2-230">The work to compact the survivors is time-consuming.</span></span> <span data-ttu-id="947a2-231">若要确定回收期间处理对象的数量，请在指定代的垃圾回收结束时，在调试器中设置一个断点。</span><span class="sxs-lookup"><span data-stu-id="947a2-231">To determine how many objects were handled during a collection, set a breakpoint in the debugger at the end of a garbage collection for a specified generation.</span></span>

|<span data-ttu-id="947a2-232">性能检查</span><span class="sxs-lookup"><span data-stu-id="947a2-232">Performance checks</span></span>|
|------------------------|
|[<span data-ttu-id="947a2-233">确定 CPU 的使用率过高是否由垃圾回收引起。</span><span class="sxs-lookup"><span data-stu-id="947a2-233">Determine if high CPU usage is caused by garbage collection.</span></span>](#HighCPU)<br /><br /> [<span data-ttu-id="947a2-234">在垃圾回收结束时，设置一个断点。</span><span class="sxs-lookup"><span data-stu-id="947a2-234">Set a breakpoint at the end of garbage collection.</span></span>](#GenBreak)|

## <a name="troubleshooting-guidelines"></a><span data-ttu-id="947a2-235">故障排除指南</span><span class="sxs-lookup"><span data-stu-id="947a2-235">Troubleshooting Guidelines</span></span>

<span data-ttu-id="947a2-236">本部分介绍在开始调查时应考虑的准则。</span><span class="sxs-lookup"><span data-stu-id="947a2-236">This section describes guidelines that you should consider as you begin your investigations.</span></span>

### <a name="workstation-or-server-garbage-collection"></a><span data-ttu-id="947a2-237">工作站或服务器垃圾回收</span><span class="sxs-lookup"><span data-stu-id="947a2-237">Workstation or Server Garbage Collection</span></span>

<span data-ttu-id="947a2-238">确定是否正在使用正确的垃圾回收类型。</span><span class="sxs-lookup"><span data-stu-id="947a2-238">Determine if you are using the correct type of garbage collection.</span></span> <span data-ttu-id="947a2-239">如果应用程序使用多个线程和对象实例，则使用服务器垃圾回收，而不是工作站垃圾回收。</span><span class="sxs-lookup"><span data-stu-id="947a2-239">If your application uses multiple threads and object instances, use server garbage collection instead of workstation garbage collection.</span></span> <span data-ttu-id="947a2-240">服务器垃圾回收在多个线程上进行操作，而工作站垃圾回收则需要应用程序的多个实例运行它们自己的垃圾回收线程并争取 CPU 时间。</span><span class="sxs-lookup"><span data-stu-id="947a2-240">Server garbage collection operates on multiple threads, whereas workstation garbage collection requires multiple instances of an application to run their own garbage collection threads and compete for CPU time.</span></span>

<span data-ttu-id="947a2-241">低负载且不常在后台（如服务）执行任务的应用程序，可以在禁用并发垃圾回收的情况下使用工作站垃圾回收。</span><span class="sxs-lookup"><span data-stu-id="947a2-241">An application that has a low load and that performs tasks infrequently in the background, such as a service, could use workstation garbage collection with concurrent garbage collection disabled.</span></span>

### <a name="when-to-measure-the-managed-heap-size"></a><span data-ttu-id="947a2-242">何时衡量托管堆的大小</span><span class="sxs-lookup"><span data-stu-id="947a2-242">When to Measure the Managed Heap Size</span></span>

<span data-ttu-id="947a2-243">除非使用探查器，否则必须建立一致的测量模式，以有效地诊断性能问题。</span><span class="sxs-lookup"><span data-stu-id="947a2-243">Unless you are using a profiler, you will have to establish a consistent measuring pattern to effectively diagnose performance issues.</span></span> <span data-ttu-id="947a2-244">若要建立一个计划，请考虑以下几点：</span><span class="sxs-lookup"><span data-stu-id="947a2-244">Consider the following points to establish a schedule:</span></span>

- <span data-ttu-id="947a2-245">如果在第 2 代垃圾回收后测量，则整个托管的堆将不再存在垃圾（死对象）。</span><span class="sxs-lookup"><span data-stu-id="947a2-245">If you measure after a generation 2 garbage collection, the entire managed heap will be free of garbage (dead objects).</span></span>

- <span data-ttu-id="947a2-246">如果在一个 0 代垃圾回收后立即进行测量，则尚不会收集第 1 代和 2 中的对象。</span><span class="sxs-lookup"><span data-stu-id="947a2-246">If you measure immediately after a generation 0 garbage collection, the objects in generations 1 and 2 will not be collected yet.</span></span>

- <span data-ttu-id="947a2-247">如果在垃圾回收之前立即进行测量，则你将在垃圾回收启动之前，测量尽可能多的分配。</span><span class="sxs-lookup"><span data-stu-id="947a2-247">If you measure immediately before a garbage collection, you will measure as much allocation as possible before the garbage collection starts.</span></span>

- <span data-ttu-id="947a2-248">在垃圾回收期间进行测量会出现问题，因为垃圾回收器的数据结构对于遍历是无效状态，可能不能提供完整的结果。</span><span class="sxs-lookup"><span data-stu-id="947a2-248">Measuring during a garbage collection is problematic, because the garbage collector data structures are not in a valid state for traversal and may not be able to give you the complete results.</span></span> <span data-ttu-id="947a2-249">这是设计使然。</span><span class="sxs-lookup"><span data-stu-id="947a2-249">This is by design.</span></span>

- <span data-ttu-id="947a2-250">当与并发垃圾回收一起使用工作站垃圾回收时，回收的对象不会进行压缩，因此，堆的大小可能会相同或更大（碎片可以使它看起来更大）。</span><span class="sxs-lookup"><span data-stu-id="947a2-250">When you are using workstation garbage collection with concurrent garbage collection, the reclaimed objects are not compacted, so the heap size can be the same or larger (fragmentation can make it appear to be larger).</span></span>

- <span data-ttu-id="947a2-251">第 2 代上的并发垃圾回收在物理内存加载过高时，将被延迟。</span><span class="sxs-lookup"><span data-stu-id="947a2-251">Concurrent garbage collection on generation 2 is delayed when the physical memory load is too high.</span></span>

<span data-ttu-id="947a2-252">以下过程介绍如何设置一个断点，以便测量托管堆。</span><span class="sxs-lookup"><span data-stu-id="947a2-252">The following procedure describes how to set a breakpoint so that you can measure the managed heap.</span></span>

<a name="GenBreak"></a>

#### <a name="to-set-a-breakpoint-at-the-end-of-garbage-collection"></a><span data-ttu-id="947a2-253">若要在垃圾回收结束时设置一个断点</span><span class="sxs-lookup"><span data-stu-id="947a2-253">To set a breakpoint at the end of garbage collection</span></span>

- <span data-ttu-id="947a2-254">在加载了 SOS 调试器扩展的 WinDbg 中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="947a2-254">In WinDbg with the SOS debugger extension loaded, type the following command:</span></span>

  <span data-ttu-id="947a2-255">**bp mscorwks!WKS::GCHeap::RestartEE "j (dwo(mscorwks!WKS::GCHeap::GcCondemnedGeneration)==2) 'kb';'g'"**</span><span class="sxs-lookup"><span data-stu-id="947a2-255">**bp mscorwks!WKS::GCHeap::RestartEE "j (dwo(mscorwks!WKS::GCHeap::GcCondemnedGeneration)==2) 'kb';'g'"**</span></span>

  <span data-ttu-id="947a2-256">其中， **GcCondemnedGeneration** 设置为所需的代。</span><span class="sxs-lookup"><span data-stu-id="947a2-256">where **GcCondemnedGeneration** is set to the desired generation.</span></span> <span data-ttu-id="947a2-257">此命令要求私有符号。</span><span class="sxs-lookup"><span data-stu-id="947a2-257">This command requires private symbols.</span></span>

  <span data-ttu-id="947a2-258">如果在已回收第 2 代对象以进行垃圾回收后执行 **RestartEE** ，则此命令会强制中断。</span><span class="sxs-lookup"><span data-stu-id="947a2-258">This command forces a break if **RestartEE** is executed after generation 2 objects have been reclaimed for garbage collection.</span></span>

  <span data-ttu-id="947a2-259">在服务器垃圾回收中，只有一个线程调用 **RestartEE** ，因此在第 2 代垃圾回收期间，此断点只会出现一次。</span><span class="sxs-lookup"><span data-stu-id="947a2-259">In server garbage collection, only one thread calls **RestartEE** , so the breakpoint will occur only once during a generation 2 garbage collection.</span></span>

## <a name="performance-check-procedures"></a><span data-ttu-id="947a2-260">性能检查过程</span><span class="sxs-lookup"><span data-stu-id="947a2-260">Performance Check Procedures</span></span>

<span data-ttu-id="947a2-261">本部分将介绍下列过程，以避免造成性能问题的原因：</span><span class="sxs-lookup"><span data-stu-id="947a2-261">This section describes the following procedures to isolate the cause of your performance issue:</span></span>

- [<span data-ttu-id="947a2-262">确定问题是否由垃圾回收引起。</span><span class="sxs-lookup"><span data-stu-id="947a2-262">Determine whether the problem is caused by garbage collection.</span></span>](#IsGC)

- [<span data-ttu-id="947a2-263">确定是否已托管内存不足异常。</span><span class="sxs-lookup"><span data-stu-id="947a2-263">Determine whether the out-of-memory exception is managed.</span></span>](#OOMIsManaged)

- [<span data-ttu-id="947a2-264">确定可保留的虚拟内存量。</span><span class="sxs-lookup"><span data-stu-id="947a2-264">Determine how much virtual memory can be reserved.</span></span>](#GetVM)

- [<span data-ttu-id="947a2-265">确定是否有足够的物理内存。</span><span class="sxs-lookup"><span data-stu-id="947a2-265">Determine whether there is enough physical memory.</span></span>](#Physical)

- [<span data-ttu-id="947a2-266">确定托管堆的内存提交量。</span><span class="sxs-lookup"><span data-stu-id="947a2-266">Determine how much memory the managed heap is committing.</span></span>](#ManagedHeapCommit)

- [<span data-ttu-id="947a2-267">确定托管堆的内存保留量。</span><span class="sxs-lookup"><span data-stu-id="947a2-267">Determine how much memory the managed heap reserves.</span></span>](#ManagedHeapReserve)

- [<span data-ttu-id="947a2-268">确定第 2 代中的大型对象。</span><span class="sxs-lookup"><span data-stu-id="947a2-268">Determine large objects in generation 2.</span></span>](#ExamineGen2)

- [<span data-ttu-id="947a2-269">确定对对象的引用。</span><span class="sxs-lookup"><span data-stu-id="947a2-269">Determine references to objects.</span></span>](#ObjRef)

- [<span data-ttu-id="947a2-270">确定是否已运行终结器。</span><span class="sxs-lookup"><span data-stu-id="947a2-270">Determine whether a finalizer has been run.</span></span>](#Induce)

- [<span data-ttu-id="947a2-271">确定是否存在等待终结的对象。</span><span class="sxs-lookup"><span data-stu-id="947a2-271">Determine whether there are objects waiting to be finalized.</span></span>](#Finalize)

- [<span data-ttu-id="947a2-272">确定托管堆中的可用空间量。</span><span class="sxs-lookup"><span data-stu-id="947a2-272">Determine the amount of free space in the managed heap.</span></span>](#Fragmented)

- [<span data-ttu-id="947a2-273">确定固定对象的数目。</span><span class="sxs-lookup"><span data-stu-id="947a2-273">Determine the number of pinned objects.</span></span>](#Pinned)

- [<span data-ttu-id="947a2-274">确定垃圾回收中的时长。</span><span class="sxs-lookup"><span data-stu-id="947a2-274">Determine the length of time in a garbage collection.</span></span>](#TimeInGC)

- [<span data-ttu-id="947a2-275">确定触发垃圾回收的原因。</span><span class="sxs-lookup"><span data-stu-id="947a2-275">Determine what triggered a garbage collection.</span></span>](#Triggered)

- [<span data-ttu-id="947a2-276">确定 CPU 的使用率过高是否由垃圾回收引起。</span><span class="sxs-lookup"><span data-stu-id="947a2-276">Determine whether high CPU usage is caused by garbage collection.</span></span>](#HighCPU)

<a name="IsGC"></a>

### <a name="to-determine-whether-the-problem-is-caused-by-garbage-collection"></a><span data-ttu-id="947a2-277">若要确定问题是否是垃圾回收引起</span><span class="sxs-lookup"><span data-stu-id="947a2-277">To determine whether the problem is caused by garbage collection</span></span>

- <span data-ttu-id="947a2-278">请检查以下两个内存性能计数器：</span><span class="sxs-lookup"><span data-stu-id="947a2-278">Examine the following two memory performance counters:</span></span>

  - <span data-ttu-id="947a2-279">**GC 所占时间百分比** 。</span><span class="sxs-lookup"><span data-stu-id="947a2-279">**% Time in GC**.</span></span> <span data-ttu-id="947a2-280">显示执行最后一个垃圾回收周期后，执行垃圾回收所用运行时间的百分比。</span><span class="sxs-lookup"><span data-stu-id="947a2-280">Displays the percentage of elapsed time that was spent performing a garbage collection after the last garbage collection cycle.</span></span> <span data-ttu-id="947a2-281">使用此计数器确定垃圾回收器是否花费太多时间来使托管堆空间可用。</span><span class="sxs-lookup"><span data-stu-id="947a2-281">Use this counter to determine whether the garbage collector is spending too much time to make managed heap space available.</span></span> <span data-ttu-id="947a2-282">如果垃圾回收所用的时间相对较短，这可能表示托管堆之外存在资源问题。</span><span class="sxs-lookup"><span data-stu-id="947a2-282">If the time spent in garbage collection is relatively low, that could indicate a resource problem outside the managed heap.</span></span> <span data-ttu-id="947a2-283">当涉及并发或后台垃圾回收时，此计数器可能不准确。</span><span class="sxs-lookup"><span data-stu-id="947a2-283">This counter may not be accurate when concurrent or background garbage collection is involved.</span></span>

  - <span data-ttu-id="947a2-284">**已提交的字节总数** 。</span><span class="sxs-lookup"><span data-stu-id="947a2-284">**# Total committed Bytes**.</span></span> <span data-ttu-id="947a2-285">显示垃圾回收器当前已提交的虚拟内存量。</span><span class="sxs-lookup"><span data-stu-id="947a2-285">Displays the amount of virtual memory currently committed by the garbage collector.</span></span> <span data-ttu-id="947a2-286">使用此计数器确定垃圾回收器所占用的内存是否是应用程序所使用的内存的过多部分。</span><span class="sxs-lookup"><span data-stu-id="947a2-286">Use this counter to determine whether the memory consumed by the garbage collector is an excessive portion of the memory that your application uses.</span></span>

  <span data-ttu-id="947a2-287">大多数的内存性能计数器会在每次垃圾回收结束时进行更新。</span><span class="sxs-lookup"><span data-stu-id="947a2-287">Most of the memory performance counters are updated at the end of each garbage collection.</span></span> <span data-ttu-id="947a2-288">因此，它们可能不会反映你希望了解的当前情况。</span><span class="sxs-lookup"><span data-stu-id="947a2-288">Therefore, they may not reflect the current conditions that you want information about.</span></span>

<a name="OOMIsManaged"></a>

### <a name="to-determine-whether-the-out-of-memory-exception-is-managed"></a><span data-ttu-id="947a2-289">若要确定是否已托管内存不足异常</span><span class="sxs-lookup"><span data-stu-id="947a2-289">To determine whether the out-of-memory exception is managed</span></span>

1. <span data-ttu-id="947a2-290">在加载了 SOS 调试器扩展的 WinDbg 或 Visual Studio 调试器中，键入打印异常 ( **pe** ) 命令：</span><span class="sxs-lookup"><span data-stu-id="947a2-290">In the WinDbg or Visual Studio debugger with the SOS debugger extension loaded, type the print exception ( **pe** ) command:</span></span>

    <span data-ttu-id="947a2-291">**!pe**</span><span class="sxs-lookup"><span data-stu-id="947a2-291">**!pe**</span></span>

    <span data-ttu-id="947a2-292">如果已托管异常，<xref:System.OutOfMemoryException> 将显示为异常类型，如以下示例中所示。</span><span class="sxs-lookup"><span data-stu-id="947a2-292">If the exception is managed, <xref:System.OutOfMemoryException> is displayed as the exception type, as shown in the following example.</span></span>

    ```console
    Exception object: 39594518
    Exception type: System.OutOfMemoryException
    Message: <none>
    InnerException: <none>
    StackTrace (generated):
    ```

2. <span data-ttu-id="947a2-293">如果输出没有指定异常，则必须确定内存不足异常来自哪个线程。</span><span class="sxs-lookup"><span data-stu-id="947a2-293">If the output does not specify an exception, you have to determine which thread the out-of-memory exception is from.</span></span> <span data-ttu-id="947a2-294">在调试器中键入以下命令，以显示所有带调用堆栈的线程：</span><span class="sxs-lookup"><span data-stu-id="947a2-294">Type the following command in the debugger to show all the threads with their call stacks:</span></span>

    <span data-ttu-id="947a2-295">**~\*kb**</span><span class="sxs-lookup"><span data-stu-id="947a2-295">**~\*kb**</span></span>

    <span data-ttu-id="947a2-296">具有存在异常调用的堆栈的线程会由 `RaiseTheException` 参数进行指示。</span><span class="sxs-lookup"><span data-stu-id="947a2-296">The thread with the stack that has exception calls is indicated by the `RaiseTheException` argument.</span></span> <span data-ttu-id="947a2-297">这是托管异常对象。</span><span class="sxs-lookup"><span data-stu-id="947a2-297">This is the managed exception object.</span></span>

    ```console
    28adfb44 7923918f 5b61f2b4 00000000 5b61f2b4 mscorwks!RaiseTheException+0xa0
    ```

3. <span data-ttu-id="947a2-298">可以使用以下命令来转储嵌套的异常。</span><span class="sxs-lookup"><span data-stu-id="947a2-298">You can use the following command to dump nested exceptions.</span></span>

    <span data-ttu-id="947a2-299">**!pe -nested**</span><span class="sxs-lookup"><span data-stu-id="947a2-299">**!pe -nested**</span></span>

    <span data-ttu-id="947a2-300">如果找不到任何异常，则非托管代码将产生内存不足异常。</span><span class="sxs-lookup"><span data-stu-id="947a2-300">If you do not find any exceptions, the out-of-memory exception originated from unmanaged code.</span></span>

<a name="GetVM"></a>

### <a name="to-determine-how-much-virtual-memory-can-be-reserved"></a><span data-ttu-id="947a2-301">若要确定可保留的虚拟内存量</span><span class="sxs-lookup"><span data-stu-id="947a2-301">To determine how much virtual memory can be reserved</span></span>

- <span data-ttu-id="947a2-302">在加载了 SOS 调试器扩展的 WinDbg 中键入以下命令，以获取最大的可用区域：</span><span class="sxs-lookup"><span data-stu-id="947a2-302">In WinDbg with the SOS debugger extension loaded, type the following command to get the largest free region:</span></span>

  <span data-ttu-id="947a2-303">**!address -summary**</span><span class="sxs-lookup"><span data-stu-id="947a2-303">**!address -summary**</span></span>

  <span data-ttu-id="947a2-304">最大可用区域将如以下输出所示进行显示。</span><span class="sxs-lookup"><span data-stu-id="947a2-304">The largest free region is displayed as shown in the following output.</span></span>

  ```console
  Largest free region: Base 54000000 - Size 0003A980
  ```

  <span data-ttu-id="947a2-305">在此示例中，最大可用区域的大小大约为 24000 KB（按十六进制形式则为 3A980）。</span><span class="sxs-lookup"><span data-stu-id="947a2-305">In this example, the size of the largest free region is approximately 24000 KB (3A980 in hexadecimal).</span></span> <span data-ttu-id="947a2-306">此区域比垃圾回收器对分段所需的大小要小得多。</span><span class="sxs-lookup"><span data-stu-id="947a2-306">This region is much smaller than what the garbage collector needs for a segment.</span></span>

  <span data-ttu-id="947a2-307">\- 或 -</span><span class="sxs-lookup"><span data-stu-id="947a2-307">-or-</span></span>

- <span data-ttu-id="947a2-308">使用 **vmstat** 命令：</span><span class="sxs-lookup"><span data-stu-id="947a2-308">Use the **vmstat** command:</span></span>

  <span data-ttu-id="947a2-309">**!vmstat**</span><span class="sxs-lookup"><span data-stu-id="947a2-309">**!vmstat**</span></span>

  <span data-ttu-id="947a2-310">最大可用区域是 MAXIMUM 列中的最大值，如以下输出所示。</span><span class="sxs-lookup"><span data-stu-id="947a2-310">The largest free region is the largest value in the MAXIMUM column, as shown in the following output.</span></span>

  ```console
  TYPE        MINIMUM   MAXIMUM     AVERAGE   BLK COUNT   TOTAL
  ~~~~        ~~~~~~~   ~~~~~~~     ~~~~~~~   ~~~~~~~~~~  ~~~~
  Free:
  Small       8K        64K         46K       36          1,671K
  Medium      80K       864K        349K      3           1,047K
  Large       1,384K    1,278,848K  151,834K  12          1,822,015K
  Summary     8K        1,278,848K  35,779K   51          1,824,735K
  ```

<a name="Physical"></a>

### <a name="to-determine-whether-there-is-enough-physical-memory"></a><span data-ttu-id="947a2-311">若要确定是否有足够的物理内存</span><span class="sxs-lookup"><span data-stu-id="947a2-311">To determine whether there is enough physical memory</span></span>

1. <span data-ttu-id="947a2-312">则启动 Windows 任务管理器。</span><span class="sxs-lookup"><span data-stu-id="947a2-312">Start Windows Task Manager.</span></span>

2. <span data-ttu-id="947a2-313">在“性能”选项卡上，查看已提交的值。</span><span class="sxs-lookup"><span data-stu-id="947a2-313">On the **Performance** tab, look at the committed value.</span></span> <span data-ttu-id="947a2-314">（在 Windows 7 中，查看“系统组”中的“提交 (KB)”。）</span><span class="sxs-lookup"><span data-stu-id="947a2-314">(In Windows 7, look at **Commit (KB)** in the **System group**.)</span></span>

    <span data-ttu-id="947a2-315">如果“总数”接近“限值”，则物理内存将不足。</span><span class="sxs-lookup"><span data-stu-id="947a2-315">If the **Total** is close to the **Limit** , you are running low on physical memory.</span></span>

<a name="ManagedHeapCommit"></a>

### <a name="to-determine-how-much-memory-the-managed-heap-is-committing"></a><span data-ttu-id="947a2-316">若要确定托管堆的内存提交量</span><span class="sxs-lookup"><span data-stu-id="947a2-316">To determine how much memory the managed heap is committing</span></span>

- <span data-ttu-id="947a2-317">使用 `# Total committed bytes` 内存性能计数器获取托管堆提交的字节数。</span><span class="sxs-lookup"><span data-stu-id="947a2-317">Use the `# Total committed bytes` memory performance counter to get the number of bytes that the managed heap is committing.</span></span> <span data-ttu-id="947a2-318">垃圾回收器根据需要在某个段上提交区块，但不会全部在同一时间进行。</span><span class="sxs-lookup"><span data-stu-id="947a2-318">The garbage collector commits chunks on a segment as needed, not all at the same time.</span></span>

  > [!NOTE]
  > <span data-ttu-id="947a2-319">请不要使用 `# Bytes in all Heaps` 性能计数器，因为它不表示托管堆的实际内存使用情况。</span><span class="sxs-lookup"><span data-stu-id="947a2-319">Do not use the `# Bytes in all Heaps` performance counter, because it does not represent actual memory usage by the managed heap.</span></span> <span data-ttu-id="947a2-320">代的大小包括在此值中，且实际上是其阈值大小，即如果代以对象进行填充，将引发垃圾回收的大小。</span><span class="sxs-lookup"><span data-stu-id="947a2-320">The size of a generation is included in this value and is actually its threshold size, that is, the size that induces a garbage collection if the generation is filled with objects.</span></span> <span data-ttu-id="947a2-321">因此，此值通常为零。</span><span class="sxs-lookup"><span data-stu-id="947a2-321">Therefore, this value is usually zero.</span></span>

<a name="ManagedHeapReserve"></a>

### <a name="to-determine-how-much-memory-the-managed-heap-reserves"></a><span data-ttu-id="947a2-322">若要确定托管堆的内存保留量</span><span class="sxs-lookup"><span data-stu-id="947a2-322">To determine how much memory the managed heap reserves</span></span>

- <span data-ttu-id="947a2-323">使用 `# Total reserved bytes`内存性能计数器。</span><span class="sxs-lookup"><span data-stu-id="947a2-323">Use the `# Total reserved bytes` memory performance counter.</span></span>

  <span data-ttu-id="947a2-324">垃圾回收器在段中保留内存，你可以使用 **eeheap** 命令确定段的开始位置。</span><span class="sxs-lookup"><span data-stu-id="947a2-324">The garbage collector reserves memory in segments, and you can determine where a segment starts by using the **eeheap** command.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="947a2-325">尽管可以确定垃圾回收器为每个段分配的内存量，但是段的大小是特定于实现的，并可能会在任何时间（包括在定期更新中）进行更改。</span><span class="sxs-lookup"><span data-stu-id="947a2-325">Although you can determine the amount of memory the garbage collector allocates for each segment, segment size is implementation-specific and is subject to change at any time, including in periodic updates.</span></span> <span data-ttu-id="947a2-326">应用程序不应假设特定段的大小或依赖于此大小，也不应尝试配置段分配可用的内存量。</span><span class="sxs-lookup"><span data-stu-id="947a2-326">Your app should never make assumptions about or depend on a particular segment size, nor should it attempt to configure the amount of memory available for segment allocations.</span></span>

- <span data-ttu-id="947a2-327">在加载了 SOS 调试器扩展的 WinDbg 或 Visual Studio 调试器中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="947a2-327">In the WinDbg or Visual Studio debugger with the SOS debugger extension loaded, type the following command:</span></span>

  <span data-ttu-id="947a2-328">**!eeheap -gc**</span><span class="sxs-lookup"><span data-stu-id="947a2-328">**!eeheap -gc**</span></span>

  <span data-ttu-id="947a2-329">结果如下所示：</span><span class="sxs-lookup"><span data-stu-id="947a2-329">The result is as follows.</span></span>

  ```console
  Number of GC Heaps: 2
  ------------------------------
  Heap 0 (002db550)
  generation 0 starts at 0x02abe29c
  generation 1 starts at 0x02abdd08
  generation 2 starts at 0x02ab0038
  ephemeral segment allocation context: none
    segment    begin allocated     size
  02ab0000 02ab0038  02aceff4 0x0001efbc(126908)
  Large object heap starts at 0x0aab0038
    segment    begin allocated     size
  0aab0000 0aab0038  0aab2278 0x00002240(8768)
  Heap Size   0x211fc(135676)
  ------------------------------
  Heap 1 (002dc958)
  generation 0 starts at 0x06ab1bd8
  generation 1 starts at 0x06ab1bcc
  generation 2 starts at 0x06ab0038
  ephemeral segment allocation context: none
    segment    begin allocated     size
  06ab0000 06ab0038  06ab3be4 0x00003bac(15276)
  Large object heap starts at 0x0cab0038
    segment    begin allocated     size
  0cab0000 0cab0038  0cab0048 0x00000010(16)
  Heap Size    0x3bbc(15292)
  ------------------------------
  GC Heap Size   0x24db8(150968)
  ```

  <span data-ttu-id="947a2-330">由“段”指示的地址是段的起始地址。</span><span class="sxs-lookup"><span data-stu-id="947a2-330">The addresses indicated by "segment" are the starting addresses of the segments.</span></span>

<a name="ExamineGen2"></a>

### <a name="to-determine-large-objects-in-generation-2"></a><span data-ttu-id="947a2-331">若要确定第 2 代中的大型对象</span><span class="sxs-lookup"><span data-stu-id="947a2-331">To determine large objects in generation 2</span></span>

- <span data-ttu-id="947a2-332">在加载了 SOS 调试器扩展的 WinDbg 或 Visual Studio 调试器中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="947a2-332">In the WinDbg or Visual Studio debugger with the SOS debugger extension loaded, type the following command:</span></span>

  <span data-ttu-id="947a2-333">**!dumpheap –stat**</span><span class="sxs-lookup"><span data-stu-id="947a2-333">**!dumpheap –stat**</span></span>

  <span data-ttu-id="947a2-334">如果托管堆很大，则 **dumpheap** 可能需要一段时间才能完成。</span><span class="sxs-lookup"><span data-stu-id="947a2-334">If the managed heap is big, **dumpheap** may take a while to finish.</span></span>

  <span data-ttu-id="947a2-335">你可以从输出的最后几行开始分析，因为它们列出了占用了大多数空间的对象。</span><span class="sxs-lookup"><span data-stu-id="947a2-335">You can start analyzing from the last few lines of the output, because they list the objects that use the most space.</span></span> <span data-ttu-id="947a2-336">例如：</span><span class="sxs-lookup"><span data-stu-id="947a2-336">For example:</span></span>

  ```console
  2c6108d4   173712     14591808 DevExpress.XtraGrid.Views.Grid.ViewInfo.GridCellInfo
  00155f80      533     15216804      Free
  7a747c78   791070     15821400 System.Collections.Specialized.ListDictionary+DictionaryNode
  7a747bac   700930     19626040 System.Collections.Specialized.ListDictionary
  2c64e36c    78644     20762016 DevExpress.XtraEditors.ViewInfo.TextEditViewInfo
  79124228   121143     29064120 System.Object[]
  035f0ee4    81626     35588936 Toolkit.TlkOrder
  00fcae40     6193     44911636 WaveBasedStrategy.Tick_Snap[]
  791242ec    40182     90664128 System.Collections.Hashtable+bucket[]
  790fa3e0  3154024    137881448 System.String
  Total 8454945 objects
  ```

  <span data-ttu-id="947a2-337">所列出的最后一个对象是一个字符串，且占用的空间最多。</span><span class="sxs-lookup"><span data-stu-id="947a2-337">The last object listed is a string and occupies the most space.</span></span> <span data-ttu-id="947a2-338">可以检查应用程序，以查看如何优化字符串对象。</span><span class="sxs-lookup"><span data-stu-id="947a2-338">You can examine your application to see how your string objects can be optimized.</span></span> <span data-ttu-id="947a2-339">若要查看 150 到 200 个字节之间的字符串，请键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="947a2-339">To see strings that are between 150 and 200 bytes, type the following:</span></span>

  <span data-ttu-id="947a2-340">**!dumpheap -type System.String -min 150 -max 200**</span><span class="sxs-lookup"><span data-stu-id="947a2-340">**!dumpheap -type System.String -min 150 -max 200**</span></span>

  <span data-ttu-id="947a2-341">如下所示是结果的一个示例。</span><span class="sxs-lookup"><span data-stu-id="947a2-341">An example of the results is as follows.</span></span>

  ```console
  Address  MT           Size  Gen
  1875d2c0 790fa3e0      152    2 System.String HighlightNullStyle_Blotter_PendingOrder-11_Blotter_PendingOrder-11
  …
  ```

  <span data-ttu-id="947a2-342">对 ID 使用整数而非字符串，这样可能会更有效。</span><span class="sxs-lookup"><span data-stu-id="947a2-342">Using an integer instead of a string for an ID can be more efficient.</span></span> <span data-ttu-id="947a2-343">如果数千次重复相同的字符串，请考虑字符串暂留。</span><span class="sxs-lookup"><span data-stu-id="947a2-343">If the same string is being repeated thousands of times, consider string interning.</span></span> <span data-ttu-id="947a2-344">有关字符串暂留的详细信息，请参阅 <xref:System.String.Intern%2A?displayProperty=nameWithType> 方法的参考主题。</span><span class="sxs-lookup"><span data-stu-id="947a2-344">For more information about string interning, see the reference topic for the <xref:System.String.Intern%2A?displayProperty=nameWithType> method.</span></span>

<a name="ObjRef"></a>

### <a name="to-determine-references-to-objects"></a><span data-ttu-id="947a2-345">若要确定对对象的引用</span><span class="sxs-lookup"><span data-stu-id="947a2-345">To determine references to objects</span></span>

- <span data-ttu-id="947a2-346">在加载了 SOS 调试器扩展的 WinDbg 中，键入以下命令，以列出对对象的引用：</span><span class="sxs-lookup"><span data-stu-id="947a2-346">In WinDbg with the SOS debugger extension loaded, type the following command to list references to objects:</span></span>

  <span data-ttu-id="947a2-347">**!gcroot**</span><span class="sxs-lookup"><span data-stu-id="947a2-347">**!gcroot**</span></span>

  `-or-`

- <span data-ttu-id="947a2-348">若要确定对特定对象的引用，包括地址：</span><span class="sxs-lookup"><span data-stu-id="947a2-348">To determine the references for a specific object, include the address:</span></span>

  <span data-ttu-id="947a2-349">**!gcroot 1c37b2ac**</span><span class="sxs-lookup"><span data-stu-id="947a2-349">**!gcroot 1c37b2ac**</span></span>

  <span data-ttu-id="947a2-350">在堆栈上找到的根可能是误报。</span><span class="sxs-lookup"><span data-stu-id="947a2-350">Roots found on stacks may be false positives.</span></span> <span data-ttu-id="947a2-351">有关详细信息，请参阅命令 `!help gcroot`。</span><span class="sxs-lookup"><span data-stu-id="947a2-351">For more information, use the command `!help gcroot`.</span></span>

  ```console
  ebx:Root:19011c5c(System.Windows.Forms.Application+ThreadContext)->
  19010b78(DemoApp.FormDemoApp)->
  19011158(System.Windows.Forms.PropertyStore)->
  … [omitted]
  1c3745ec(System.Data.DataTable)->
  1c3747a8(System.Data.DataColumnCollection)->
  1c3747f8(System.Collections.Hashtable)->
  1c376590(System.Collections.Hashtable+bucket[])->
  1c376c98(System.Data.DataColumn)->
  1c37b270(System.Data.Common.DoubleStorage)->
  1c37b2ac(System.Double[])
  Scan Thread 0 OSTHread 99c
  Scan Thread 6 OSTHread 484
  ```

  <span data-ttu-id="947a2-352">**gcroot** 命令可能需要很长时间才能完成。</span><span class="sxs-lookup"><span data-stu-id="947a2-352">The **gcroot** command can take a long time to finish.</span></span> <span data-ttu-id="947a2-353">任何不通过垃圾回收进行回收的对象是活动对象。</span><span class="sxs-lookup"><span data-stu-id="947a2-353">Any object that is not reclaimed by garbage collection is a live object.</span></span> <span data-ttu-id="947a2-354">这意味着，某些根直接或间接地保留于该对象，因此 **gcroot** 应将路径信息返回到该对象。</span><span class="sxs-lookup"><span data-stu-id="947a2-354">This means that some root is directly or indirectly holding onto the object, so **gcroot** should return path information to the object.</span></span> <span data-ttu-id="947a2-355">应检查返回的关系图，并查看仍然引用这些对象的原因。</span><span class="sxs-lookup"><span data-stu-id="947a2-355">You should examine the graphs returned and see why these objects are still referenced.</span></span>

<a name="Induce"></a>

### <a name="to-determine-whether-a-finalizer-has-been-run"></a><span data-ttu-id="947a2-356">若要确定是否已运行终结器</span><span class="sxs-lookup"><span data-stu-id="947a2-356">To determine whether a finalizer has been run</span></span>

- <span data-ttu-id="947a2-357">则运行包含以下代码的测试程序：</span><span class="sxs-lookup"><span data-stu-id="947a2-357">Run a test program that contains the following code:</span></span>

  ```csharp
  GC.Collect();
  GC.WaitForPendingFinalizers();
  GC.Collect();
  ```

  <span data-ttu-id="947a2-358">如果测试解决了此问题，这意味着垃圾回收器未回收对象，因为这些对象的终结器已被挂起。</span><span class="sxs-lookup"><span data-stu-id="947a2-358">If the test resolves the problem, this means that the garbage collector was not reclaiming objects, because the finalizers for those objects had been suspended.</span></span> <span data-ttu-id="947a2-359"><xref:System.GC.WaitForPendingFinalizers%2A?displayProperty=nameWithType> 方法将启用这些终结器来完成其任务，并解决问题。</span><span class="sxs-lookup"><span data-stu-id="947a2-359">The <xref:System.GC.WaitForPendingFinalizers%2A?displayProperty=nameWithType> method enables the finalizers to complete their tasks, and fixes the problem.</span></span>

<a name="Finalize"></a>

### <a name="to-determine-whether-there-are-objects-waiting-to-be-finalized"></a><span data-ttu-id="947a2-360">若要确定是否存在等待被终结的对象</span><span class="sxs-lookup"><span data-stu-id="947a2-360">To determine whether there are objects waiting to be finalized</span></span>

1. <span data-ttu-id="947a2-361">在加载了 SOS 调试器扩展的 WinDbg 或 Visual Studio 调试器中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="947a2-361">In the WinDbg or Visual Studio debugger with the SOS debugger extension loaded, type the following command:</span></span>

    <span data-ttu-id="947a2-362">**!finalizequeue**</span><span class="sxs-lookup"><span data-stu-id="947a2-362">**!finalizequeue**</span></span>

    <span data-ttu-id="947a2-363">查看已准备好进行终结的对象的数目。</span><span class="sxs-lookup"><span data-stu-id="947a2-363">Look at the number of objects that are ready for finalization.</span></span> <span data-ttu-id="947a2-364">如果数目很多，则必须检查这些终结器完全没有进展或进展速度不够快的原因。</span><span class="sxs-lookup"><span data-stu-id="947a2-364">If the number is high, you must examine why these finalizers cannot progress at all or cannot progress fast enough.</span></span>

2. <span data-ttu-id="947a2-365">若要获取线程的输出，请键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="947a2-365">To get an output of threads, type the following command:</span></span>

    <span data-ttu-id="947a2-366">**threads -special**</span><span class="sxs-lookup"><span data-stu-id="947a2-366">**threads -special**</span></span>

    <span data-ttu-id="947a2-367">此命令提供如下所示的输出。</span><span class="sxs-lookup"><span data-stu-id="947a2-367">This command provides output such as the following.</span></span>

    ```console
       OSID     Special thread type
    2    cd0    DbgHelper
    3    c18    Finalizer
    4    df0    GC SuspendEE
    ```

    <span data-ttu-id="947a2-368">终结器线程将指示当前正在运行的终结器（如果存在）。</span><span class="sxs-lookup"><span data-stu-id="947a2-368">The finalizer thread indicates which finalizer, if any, is currently being run.</span></span> <span data-ttu-id="947a2-369">当终结器线程没有运行任何终结器时，则它正在等待一个事件告诉它进行工作。</span><span class="sxs-lookup"><span data-stu-id="947a2-369">When a finalizer thread is not running any finalizers, it is waiting for an event to tell it to do its work.</span></span> <span data-ttu-id="947a2-370">大多数情况下，你将看到此状态中的终结器线程，因为它在 THREAD_HIGHEST_PRIORITY 处运行，并应快速完成运行终结器（如果存在）。</span><span class="sxs-lookup"><span data-stu-id="947a2-370">Most of the time you will see the finalizer thread in this state because it runs at THREAD_HIGHEST_PRIORITY and is supposed to finish running finalizers, if any, very quickly.</span></span>

<a name="Fragmented"></a>

### <a name="to-determine-the-amount-of-free-space-in-the-managed-heap"></a><span data-ttu-id="947a2-371">若要确定托管堆中的可用空间量</span><span class="sxs-lookup"><span data-stu-id="947a2-371">To determine the amount of free space in the managed heap</span></span>

- <span data-ttu-id="947a2-372">在加载了 SOS 调试器扩展的 WinDbg 或 Visual Studio 调试器中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="947a2-372">In the WinDbg or Visual Studio debugger with the SOS debugger extension loaded, type the following command:</span></span>

  <span data-ttu-id="947a2-373">**!dumpheap -type Free -stat**</span><span class="sxs-lookup"><span data-stu-id="947a2-373">**!dumpheap -type Free -stat**</span></span>

  <span data-ttu-id="947a2-374">此命令将显示托管堆上所有可用对象的总大小，如以下示例中所示。</span><span class="sxs-lookup"><span data-stu-id="947a2-374">This command displays the total size of all the free objects on the managed heap, as shown in the following example.</span></span>

  ```console
  total 230 objects
  Statistics:
        MT    Count    TotalSize Class Name
  00152b18      230     40958584      Free
  Total 230 objects
  ```

- <span data-ttu-id="947a2-375">若要确定第 0 代中的可用空间，请键入以下命令以获取代的内存使用信息：</span><span class="sxs-lookup"><span data-stu-id="947a2-375">To determine the free space in generation 0, type the following command for memory consumption information by generation:</span></span>

  <span data-ttu-id="947a2-376">**!eeheap -gc**</span><span class="sxs-lookup"><span data-stu-id="947a2-376">**!eeheap -gc**</span></span>

  <span data-ttu-id="947a2-377">该命令将显示类似以下所示的输出。</span><span class="sxs-lookup"><span data-stu-id="947a2-377">This command displays output similar to the following.</span></span> <span data-ttu-id="947a2-378">最后一行将显示暂时段。</span><span class="sxs-lookup"><span data-stu-id="947a2-378">The last line shows the ephemeral segment.</span></span>

  ```console
  Heap 0 (0015ad08)
  generation 0 starts at 0x49521f8c
  generation 1 starts at 0x494d7f64
  generation 2 starts at 0x007f0038
  ephemeral segment allocation context: none
  segment  begin     allocated  size
  00178250 7a80d84c  7a82f1cc   0x00021980(137600)
  00161918 78c50e40  78c7056c   0x0001f72c(128812)
  007f0000 007f0038  047eed28   0x03ffecf0(67103984)
  3a120000 3a120038  3a3e84f8   0x002c84c0(2917568)
  46120000 46120038  49e05d04   0x03ce5ccc(63855820)
  ```

- <span data-ttu-id="947a2-379">计算 0 代使用的空间：</span><span class="sxs-lookup"><span data-stu-id="947a2-379">Calculate the space used by generation 0:</span></span>

  <span data-ttu-id="947a2-380">**?49e05d04-0x49521f8c**</span><span class="sxs-lookup"><span data-stu-id="947a2-380">**? 49e05d04-0x49521f8c**</span></span>

  <span data-ttu-id="947a2-381">结果如下所示：</span><span class="sxs-lookup"><span data-stu-id="947a2-381">The result is as follows.</span></span> <span data-ttu-id="947a2-382">0 代大约为 9 MB。</span><span class="sxs-lookup"><span data-stu-id="947a2-382">Generation 0 is approximately 9 MB.</span></span>

  ```console
  Evaluate expression: 9321848 = 008e3d78
  ```

- <span data-ttu-id="947a2-383">以下命令将转储 0 代范围内的可用空间：</span><span class="sxs-lookup"><span data-stu-id="947a2-383">The following command dumps the free space within the generation 0 range:</span></span>

  <span data-ttu-id="947a2-384">**!dumpheap -type Free -stat 0x49521f8c 49e05d04**</span><span class="sxs-lookup"><span data-stu-id="947a2-384">**!dumpheap -type Free -stat 0x49521f8c 49e05d04**</span></span>

  <span data-ttu-id="947a2-385">结果如下所示：</span><span class="sxs-lookup"><span data-stu-id="947a2-385">The result is as follows.</span></span>

  ```console
  ------------------------------
  Heap 0
  total 409 objects
  ------------------------------
  Heap 1
  total 0 objects
  ------------------------------
  Heap 2
  total 0 objects
  ------------------------------
  Heap 3
  total 0 objects
  ------------------------------
  total 409 objects
  Statistics:
        MT    Count TotalSize Class Name
  0015a498      409   7296540      Free
  Total 409 objects
  ```

  <span data-ttu-id="947a2-386">此输出显示堆的 0 代部分正在对对象使用 9 MB 的空间并且有 7 MB 可用。</span><span class="sxs-lookup"><span data-stu-id="947a2-386">This output shows that the generation 0 portion of the heap is using 9 MB of space for objects and has 7 MB free.</span></span> <span data-ttu-id="947a2-387">此分析显示了 0 代对碎片的贡献程度。</span><span class="sxs-lookup"><span data-stu-id="947a2-387">This analysis shows the extent to which generation 0 contributes to fragmentation.</span></span> <span data-ttu-id="947a2-388">此堆的使用量应从总量中扣除，作为长期对象所产生的碎片的原因。</span><span class="sxs-lookup"><span data-stu-id="947a2-388">This amount of heap usage should be discounted from the total amount as the cause of fragmentation by long-term objects.</span></span>

<a name="Pinned"></a>

### <a name="to-determine-the-number-of-pinned-objects"></a><span data-ttu-id="947a2-389">若要确定固定对象的数目</span><span class="sxs-lookup"><span data-stu-id="947a2-389">To determine the number of pinned objects</span></span>

- <span data-ttu-id="947a2-390">在加载了 SOS 调试器扩展的 WinDbg 或 Visual Studio 调试器中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="947a2-390">In the WinDbg or Visual Studio debugger with the SOS debugger extension loaded, type the following command:</span></span>

  <span data-ttu-id="947a2-391">**!gchandles**</span><span class="sxs-lookup"><span data-stu-id="947a2-391">**!gchandles**</span></span>

  <span data-ttu-id="947a2-392">显示的统计信息包括固定句柄的数量，如以下示例所示。</span><span class="sxs-lookup"><span data-stu-id="947a2-392">The statistics displayed includes the number of pinned handles, as the following example shows.</span></span>

  ```console
  GC Handle Statistics:
  Strong Handles:      29
  Pinned Handles:      10
  ```

<a name="TimeInGC"></a>

### <a name="to-determine-the-length-of-time-in-a-garbage-collection"></a><span data-ttu-id="947a2-393">若要确定垃圾回收中的时间</span><span class="sxs-lookup"><span data-stu-id="947a2-393">To determine the length of time in a garbage collection</span></span>

- <span data-ttu-id="947a2-394">检查 `% Time in GC` 内存性能计数器。</span><span class="sxs-lookup"><span data-stu-id="947a2-394">Examine the `% Time in GC` memory performance counter.</span></span>

  <span data-ttu-id="947a2-395">通过使用采样间隔时间来计算值。</span><span class="sxs-lookup"><span data-stu-id="947a2-395">The value is calculated by using a sample interval time.</span></span> <span data-ttu-id="947a2-396">因为该计数器在每次垃圾回收结束时进行更新，所以如果在间隔期间没有产生任何回收，则当前的示例将具有与之前的示例相同的值。</span><span class="sxs-lookup"><span data-stu-id="947a2-396">Because the counters are updated at the end of each garbage collection, the current sample will have the same value as the previous sample if no collections occurred during the interval.</span></span>

  <span data-ttu-id="947a2-397">回收时间是通过将采样间隔时间乘以百分比值获取的。</span><span class="sxs-lookup"><span data-stu-id="947a2-397">Collection time is obtained by multiplying the sample interval time with the percentage value.</span></span>

  <span data-ttu-id="947a2-398">以下数据显示了为时 8 秒的研究的 4 个采样，彼此间隔 2 秒。</span><span class="sxs-lookup"><span data-stu-id="947a2-398">The following data shows four sampling intervals of two seconds, for an 8-second study.</span></span> <span data-ttu-id="947a2-399">`Gen0`、`Gen1` 和 `Gen2` 列显示了该代的间隔期间发生的垃圾回收数。</span><span class="sxs-lookup"><span data-stu-id="947a2-399">The `Gen0`, `Gen1`, and `Gen2` columns show the number of garbage collections that occurred during that interval for that generation.</span></span>

  ```console
  Interval    Gen0    Gen1    Gen2    % Time in GC
          1       9       3       1              10
          2      10       3       1               1
          3      11       3       1               3
          4      11       3       1               3
  ```

  <span data-ttu-id="947a2-400">当垃圾回收发生时，将不会显示此信息，但可以确定时间间隔中发生的垃圾回收数。</span><span class="sxs-lookup"><span data-stu-id="947a2-400">This information does not show when the garbage collection occurred, but you can determine the number of garbage collections that occurred in an interval of time.</span></span> <span data-ttu-id="947a2-401">假设最坏的情况下，第 10 个 0 代垃圾回收在第 2 个间隔开始时完成，且第 11 个 0 代垃圾回收在第 5 个间隔结束时完成。</span><span class="sxs-lookup"><span data-stu-id="947a2-401">Assuming the worst case, the tenth generation 0 garbage collection finished at the start of the second interval, and the eleventh generation 0 garbage collection finished at the end of the fifth interval.</span></span> <span data-ttu-id="947a2-402">第 10 个和第 11 个垃圾回收结束时之间的时间约为 2 秒钟，并且性能计数器显示为 3%，因此第 11 个 0 代垃圾回收的持续时间为（2 秒 \* 3%= 60 毫秒）。</span><span class="sxs-lookup"><span data-stu-id="947a2-402">The time between the end of the tenth and the end of the eleventh garbage collection is about 2 seconds, and the performance counter shows 3%, so the duration of the eleventh generation 0 garbage collection was (2 seconds \* 3% = 60ms).</span></span>

  <span data-ttu-id="947a2-403">在此示例中，存在 5 个周期。</span><span class="sxs-lookup"><span data-stu-id="947a2-403">In this example, there are 5 periods.</span></span>

  ```console
  Interval    Gen0    Gen1    Gen2     % Time in GC
          1       9       3       1                3
          2      10       3       1                1
          3      11       4       2                1
          4      11       4       2                1
          5      11       4       2               20
  ```

  <span data-ttu-id="947a2-404">第 2 个第 2代垃圾回收在第 3 个间隔期间开始并在第 5 个间隔处完成。</span><span class="sxs-lookup"><span data-stu-id="947a2-404">The second generation 2 garbage collection started during the third interval and finished at the fifth interval.</span></span> <span data-ttu-id="947a2-405">假设最坏情况下，最后一次垃圾回收是针对在第 2 个间隔开始时完成的 0 代回收，且第 2 代垃圾回收在第 5 个间隔结束时完成。</span><span class="sxs-lookup"><span data-stu-id="947a2-405">Assuming the worst case, the last garbage collection was for a generation 0 collection that finished at the start of the second interval, and the generation 2 garbage collection finished at the end of the fifth interval.</span></span> <span data-ttu-id="947a2-406">因此，第 0 代垃圾回收结束和第 2 代垃圾回收结束之间的时间是 4 秒。</span><span class="sxs-lookup"><span data-stu-id="947a2-406">Therefore, the time between the end of the generation 0 garbage collection and the end of the generation 2 garbage collection is 4 seconds.</span></span> <span data-ttu-id="947a2-407">因为 `% Time in GC` 计数器为 20%，所以第 2 代垃圾回收可能使用的最长时间为（4 秒 \* 20%= 800 毫秒）。</span><span class="sxs-lookup"><span data-stu-id="947a2-407">Because the `% Time in GC` counter is 20%, the maximum amount of time the generation 2 garbage collection could have taken is (4 seconds \* 20% = 800ms).</span></span>

- <span data-ttu-id="947a2-408">或者，可以通过使用[垃圾回收 ETW 事件](../../framework/performance/garbage-collection-etw-events.md)，确定垃圾回收的时长，并分析此信息以确定垃圾回收的持续时间。</span><span class="sxs-lookup"><span data-stu-id="947a2-408">Alternatively, you can determine the length of a garbage collection by using [garbage collection ETW events](../../framework/performance/garbage-collection-etw-events.md), and analyze the information to determine the duration of garbage collection.</span></span>

  <span data-ttu-id="947a2-409">例如，以下数据显示了一个发生在非并发垃圾回收期间的事件序列。</span><span class="sxs-lookup"><span data-stu-id="947a2-409">For example, the following data shows an event sequence that occurred during a non-concurrent garbage collection.</span></span>

  ```console
  Timestamp    Event name
  513052        GCSuspendEEBegin_V1
  513078        GCSuspendEEEnd
  513090        GCStart_V1
  517890        GCEnd_V1
  517894        GCHeapStats
  517897        GCRestartEEBegin
  517918        GCRestartEEEnd
  ```

  <span data-ttu-id="947a2-410">挂起托管线程花费了 26us (`GCSuspendEEEnd` – `GCSuspendEEBegin_V1`)。</span><span class="sxs-lookup"><span data-stu-id="947a2-410">Suspending the managed thread took 26us (`GCSuspendEEEnd` – `GCSuspendEEBegin_V1`).</span></span>

  <span data-ttu-id="947a2-411">实际的垃圾回收花费了 4.8 毫秒 (`GCEnd_V1` – `GCStart_V1`)。</span><span class="sxs-lookup"><span data-stu-id="947a2-411">The actual garbage collection took 4.8ms (`GCEnd_V1` – `GCStart_V1`).</span></span>

  <span data-ttu-id="947a2-412">回复执行托管线程花费了 21us (`GCRestartEEEnd` – `GCRestartEEBegin`)。</span><span class="sxs-lookup"><span data-stu-id="947a2-412">Resuming the managed threads took 21us (`GCRestartEEEnd` – `GCRestartEEBegin`).</span></span>

  <span data-ttu-id="947a2-413">以下输出为后台垃圾回收提供了一个示例，并包括进程、线程和事件字段。</span><span class="sxs-lookup"><span data-stu-id="947a2-413">The following output provides an example for background garbage collection, and includes the process, thread, and event fields.</span></span> <span data-ttu-id="947a2-414">（没有显示所有数据。）</span><span class="sxs-lookup"><span data-stu-id="947a2-414">(Not all data is shown.)</span></span>

  ```console
  timestamp(us)    event name            process    thread    event field
  42504385        GCSuspendEEBegin_V1    Test.exe    4372             1
  42504648        GCSuspendEEEnd         Test.exe    4372
  42504816        GCStart_V1             Test.exe    4372        102019
  42504907        GCStart_V1             Test.exe    4372        102020
  42514170        GCEnd_V1               Test.exe    4372
  42514204        GCHeapStats            Test.exe    4372        102020
  42832052        GCRestartEEBegin       Test.exe    4372
  42832136        GCRestartEEEnd         Test.exe    4372
  63685394        GCSuspendEEBegin_V1    Test.exe    4744             6
  63686347        GCSuspendEEEnd         Test.exe    4744
  63784294        GCRestartEEBegin       Test.exe    4744
  63784407        GCRestartEEEnd         Test.exe    4744
  89931423        GCEnd_V1               Test.exe    4372        102019
  89931464        GCHeapStats            Test.exe    4372
  ```

  <span data-ttu-id="947a2-415">42504816 处的 `GCStart_V1` 事件指示此为一个后台垃圾回收，因为最后一个字段是 `1`。</span><span class="sxs-lookup"><span data-stu-id="947a2-415">The `GCStart_V1` event at 42504816 indicates that this is a background garbage collection, because the last field is `1`.</span></span> <span data-ttu-id="947a2-416">这将变为垃圾回收 No.</span><span class="sxs-lookup"><span data-stu-id="947a2-416">This becomes garbage collection No.</span></span> <span data-ttu-id="947a2-417">102019。</span><span class="sxs-lookup"><span data-stu-id="947a2-417">102019.</span></span>

  <span data-ttu-id="947a2-418">将发生 `GCStart` 事件，因为在开始后台垃圾回收之前，需要一个暂时垃圾回收。</span><span class="sxs-lookup"><span data-stu-id="947a2-418">The `GCStart` event occurs because there is a need for an ephemeral garbage collection before you start a background garbage collection.</span></span> <span data-ttu-id="947a2-419">这将变为垃圾回收 No.</span><span class="sxs-lookup"><span data-stu-id="947a2-419">This becomes garbage collection No.</span></span> <span data-ttu-id="947a2-420">102020。</span><span class="sxs-lookup"><span data-stu-id="947a2-420">102020.</span></span>

  <span data-ttu-id="947a2-421">在 42514170 处，垃圾回收 No.</span><span class="sxs-lookup"><span data-stu-id="947a2-421">At 42514170, garbage collection No.</span></span> <span data-ttu-id="947a2-422">102020 结束。</span><span class="sxs-lookup"><span data-stu-id="947a2-422">102020 finishes.</span></span> <span data-ttu-id="947a2-423">此时，将重新启动托管线程。</span><span class="sxs-lookup"><span data-stu-id="947a2-423">The managed threads are restarted at this point.</span></span> <span data-ttu-id="947a2-424">这将在触发此后台垃圾回收的线程 4372 上完成。</span><span class="sxs-lookup"><span data-stu-id="947a2-424">This is completed on thread 4372, which triggered this background garbage collection.</span></span>

  <span data-ttu-id="947a2-425">在线程 4744 上，发生了一个挂起。</span><span class="sxs-lookup"><span data-stu-id="947a2-425">On thread 4744, a suspension occurs.</span></span> <span data-ttu-id="947a2-426">这是唯一一次后台垃圾回收不得不挂起托管线程。</span><span class="sxs-lookup"><span data-stu-id="947a2-426">This is the only time at which the background garbage collection has to suspend managed threads.</span></span> <span data-ttu-id="947a2-427">此持续时间为大约 99 毫秒 ((63784407-63685394)/1000)。</span><span class="sxs-lookup"><span data-stu-id="947a2-427">This duration is approximately 99ms ((63784407-63685394)/1000).</span></span>

  <span data-ttu-id="947a2-428">后台垃圾回收的 `GCEnd` 事件位于 89931423。</span><span class="sxs-lookup"><span data-stu-id="947a2-428">The `GCEnd` event for the background garbage collection is at 89931423.</span></span> <span data-ttu-id="947a2-429">这意味着后台垃圾回收持续了大约 47 秒 ((89931423-42504816)/1000)。</span><span class="sxs-lookup"><span data-stu-id="947a2-429">This means that the background garbage collection lasted for about 47seconds ((89931423-42504816)/1000).</span></span>

  <span data-ttu-id="947a2-430">托管线程运行时，可以查看发生的任意数量的暂时垃圾回收。</span><span class="sxs-lookup"><span data-stu-id="947a2-430">While the managed threads are running, you can see any number of ephemeral garbage collections occurring.</span></span>

<a name="Triggered"></a>

### <a name="to-determine-what-triggered-a-garbage-collection"></a><span data-ttu-id="947a2-431">若要确定触发垃圾回收的原因</span><span class="sxs-lookup"><span data-stu-id="947a2-431">To determine what triggered a garbage collection</span></span>

- <span data-ttu-id="947a2-432">在加载了 SOS 调试器扩展的 WinDbg 或 Visual Studio 调试器中，键入以下命令，以显示所有带调用堆栈的线程：</span><span class="sxs-lookup"><span data-stu-id="947a2-432">In the WinDbg or Visual Studio debugger with the SOS debugger extension loaded, type the following command to show all the threads with their call stacks:</span></span>

  <span data-ttu-id="947a2-433">**~\*kb**</span><span class="sxs-lookup"><span data-stu-id="947a2-433">**~\*kb**</span></span>

  <span data-ttu-id="947a2-434">该命令将显示类似以下所示的输出。</span><span class="sxs-lookup"><span data-stu-id="947a2-434">This command displays output similar to the following.</span></span>

  ```console
  0012f3b0 79ff0bf8 mscorwks!WKS::GCHeap::GarbageCollect
  0012f454 30002894 mscorwks!GCInterface::CollectGeneration+0xa4
  0012f490 79fa22bd fragment_ni!request.Main(System.String[])+0x48
  ```

  <span data-ttu-id="947a2-435">如果垃圾回收是操作系统的内存不足通知引起的，则调用堆栈会非常相似，除了线程是终结器线程之外。</span><span class="sxs-lookup"><span data-stu-id="947a2-435">If the garbage collection was caused by a low memory notification from the operating system, the call stack is similar, except that the thread is the finalizer thread.</span></span> <span data-ttu-id="947a2-436">终结器线程将获取异步内存不足的通知，并引发垃圾回收。</span><span class="sxs-lookup"><span data-stu-id="947a2-436">The finalizer thread gets an asynchronous low memory notification and induces the garbage collection.</span></span>

  <span data-ttu-id="947a2-437">如果垃圾回收是内存分配引起的，则堆栈显示如下：</span><span class="sxs-lookup"><span data-stu-id="947a2-437">If the garbage collection was caused by memory allocation, the stack appears as follows:</span></span>

  ```console
  0012f230 7a07c551 mscorwks!WKS::GCHeap::GarbageCollectGeneration
  0012f2b8 7a07cba8 mscorwks!WKS::gc_heap::try_allocate_more_space+0x1a1
  0012f2d4 7a07cefb mscorwks!WKS::gc_heap::allocate_more_space+0x18
  0012f2f4 7a02a51b mscorwks!WKS::GCHeap::Alloc+0x4b
  0012f310 7a02ae4c mscorwks!Alloc+0x60
  0012f364 7a030e46 mscorwks!FastAllocatePrimitiveArray+0xbd
  0012f424 300027f4 mscorwks!JIT_NewArr1+0x148
  000af70f 3000299f fragment_ni!request..ctor(Int32, Single)+0x20c
  0000002a 79fa22bd fragment_ni!request.Main(System.String[])+0x153
  ```

  <span data-ttu-id="947a2-438">实时帮助程序 (`JIT_New*`) 最终调用 `GCHeap::GarbageCollectGeneration`。</span><span class="sxs-lookup"><span data-stu-id="947a2-438">A just-in-time helper (`JIT_New*`) eventually calls `GCHeap::GarbageCollectGeneration`.</span></span> <span data-ttu-id="947a2-439">如果确定第 2 代垃圾回收是分配引起的，则必须确定第 2 代垃圾回收所分配的对象以及如何避免它们。</span><span class="sxs-lookup"><span data-stu-id="947a2-439">If you determine that generation 2 garbage collections are caused by allocations, you must determine which objects are collected by a generation 2 garbage collection and how to avoid them.</span></span> <span data-ttu-id="947a2-440">也就是说，想要确定第 2 代垃圾回收的开始和结束之间的差异，以及引发第 2 代回收的对象。</span><span class="sxs-lookup"><span data-stu-id="947a2-440">That is, you want to determine the difference between the start and the end of a generation 2 garbage collection, and the objects that caused the generation 2 collection.</span></span>

  <span data-ttu-id="947a2-441">例如，在调试器中键入以下命令，以显示第 2 代回收的开始：</span><span class="sxs-lookup"><span data-stu-id="947a2-441">For example, type the following command in the debugger to show the beginning of a generation 2 collection:</span></span>

  <span data-ttu-id="947a2-442">**!dumpheap –stat**</span><span class="sxs-lookup"><span data-stu-id="947a2-442">**!dumpheap –stat**</span></span>

  <span data-ttu-id="947a2-443">输出示例（经过删减以显示使用的最多空间的对象）：</span><span class="sxs-lookup"><span data-stu-id="947a2-443">Example output (abridged to show the objects that use the most space):</span></span>

  ```console
  79124228    31857      9862328 System.Object[]
  035f0384    25668     11601936 Toolkit.TlkPosition
  00155f80    21248     12256296      Free
  79103b6c   297003     13068132 System.Threading.ReaderWriterLock
  7a747ad4   708732     14174640 System.Collections.Specialized.HybridDictionary
  7a747c78   786498     15729960 System.Collections.Specialized.ListDictionary+DictionaryNode
  7a747bac   700298     19608344 System.Collections.Specialized.ListDictionary
  035f0ee4    89192     38887712 Toolkit.TlkOrder
  00fcae40     6193     44911636 WaveBasedStrategy.Tick_Snap[]
  7912c444    91616     71887080 System.Double[]
  791242ec    32451     82462728 System.Collections.Hashtable+bucket[]
  790fa3e0  2459154    112128436 System.String
  Total 6471774 objects
  ```

  <span data-ttu-id="947a2-444">在第 2 代结束时，重复该命令：</span><span class="sxs-lookup"><span data-stu-id="947a2-444">Repeat the command at the end of generation 2:</span></span>

  <span data-ttu-id="947a2-445">**!dumpheap –stat**</span><span class="sxs-lookup"><span data-stu-id="947a2-445">**!dumpheap –stat**</span></span>

  <span data-ttu-id="947a2-446">输出示例（经过删减以显示使用的最多空间的对象）：</span><span class="sxs-lookup"><span data-stu-id="947a2-446">Example output (abridged to show the objects that use the most space):</span></span>

  ```console
  79124228    26648      9314256 System.Object[]
  035f0384    25668     11601936 Toolkit.TlkPosition
  79103b6c   296770     13057880 System.Threading.ReaderWriterLock
  7a747ad4   708730     14174600 System.Collections.Specialized.HybridDictionary
  7a747c78   786497     15729940 System.Collections.Specialized.ListDictionary+DictionaryNode
  7a747bac   700298     19608344 System.Collections.Specialized.ListDictionary
  00155f80    13806     34007212      Free
  035f0ee4    89187     38885532 Toolkit.TlkOrder
  00fcae40     6193     44911636 WaveBasedStrategy.Tick_Snap[]
  791242ec    32370     82359768 System.Collections.Hashtable+bucket[]
  790fa3e0  2440020    111341808 System.String
  Total 6417525 objects
  ```

  <span data-ttu-id="947a2-447">`double[]` 对象从输出的末尾消失，这意味着它们被回收了。</span><span class="sxs-lookup"><span data-stu-id="947a2-447">The `double[]` objects disappeared from the end of the output, which means that they were collected.</span></span> <span data-ttu-id="947a2-448">这些对象大约占 70 MB。</span><span class="sxs-lookup"><span data-stu-id="947a2-448">These objects account for approximately 70 MB.</span></span> <span data-ttu-id="947a2-449">剩余的对象没有太多变化。</span><span class="sxs-lookup"><span data-stu-id="947a2-449">The remaining objects did not change much.</span></span> <span data-ttu-id="947a2-450">因此，这些 `double[]` 对象是第 2 代垃圾回收发生的原因。</span><span class="sxs-lookup"><span data-stu-id="947a2-450">Therefore, these `double[]` objects were the reason why this generation 2 garbage collection occurred.</span></span> <span data-ttu-id="947a2-451">下一步是确定 `double[]` 对象存在以及他们最后死亡的原因。</span><span class="sxs-lookup"><span data-stu-id="947a2-451">Your next step is to determine why the `double[]` objects are there and why they died.</span></span> <span data-ttu-id="947a2-452">可以询问代码开发人员这些对象的来源，或使用 **gcroot** 命令。</span><span class="sxs-lookup"><span data-stu-id="947a2-452">You can ask the code developer where these objects came from, or you can use the **gcroot** command.</span></span>

<a name="HighCPU"></a>

### <a name="to-determine-whether-high-cpu-usage-is-caused-by-garbage-collection"></a><span data-ttu-id="947a2-453">若要确定 CPU 的使用率高是否是垃圾回收引起的</span><span class="sxs-lookup"><span data-stu-id="947a2-453">To determine whether high CPU usage is caused by garbage collection</span></span>

- <span data-ttu-id="947a2-454">将 `% Time in GC` 内存性能计数器的值与处理时间相关联。</span><span class="sxs-lookup"><span data-stu-id="947a2-454">Correlate the `% Time in GC` memory performance counter value with the process time.</span></span>

  <span data-ttu-id="947a2-455">如果 `% Time in GC` 值在与处理时间同时达到峰值，则垃圾回收将造成 CPU 使用率过高。</span><span class="sxs-lookup"><span data-stu-id="947a2-455">If the `% Time in GC` value spikes at the same time as process time, garbage collection is causing a high CPU usage.</span></span> <span data-ttu-id="947a2-456">否则，配置应用程序，以查找发生使用率过高的位置。</span><span class="sxs-lookup"><span data-stu-id="947a2-456">Otherwise, profile the application to find where the high usage is occurring.</span></span>

## <a name="see-also"></a><span data-ttu-id="947a2-457">请参阅</span><span class="sxs-lookup"><span data-stu-id="947a2-457">See also</span></span>

- [<span data-ttu-id="947a2-458">垃圾回收</span><span class="sxs-lookup"><span data-stu-id="947a2-458">Garbage Collection</span></span>](index.md)
