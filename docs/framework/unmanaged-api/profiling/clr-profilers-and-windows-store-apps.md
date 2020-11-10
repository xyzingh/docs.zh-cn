---
title: CLR 探查器和 Windows 应用商店应用
ms.date: 03/30/2017
dev_langs:
- csharp
applies_to:
- Windows 10
- Windows 8
helpviewer_keywords:
- profiling API
- profiling API [.NET Framework]
- profiling managed code
- profiling managed code [Windows Store Apps]
ms.assetid: 1c8eb2e7-f20a-42f9-a795-71503486a0f5
ms.openlocfilehash: 04b4b529a5a1adaa40e804988dee506942c863c4
ms.sourcegitcommit: 30a686fd4377fe6472aa04e215c0de711bc1c322
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94440075"
---
# <a name="clr-profilers-and-windows-store-apps"></a><span data-ttu-id="02b69-102">CLR 探查器和 Windows 应用商店应用</span><span class="sxs-lookup"><span data-stu-id="02b69-102">CLR Profilers and Windows Store Apps</span></span>

<span data-ttu-id="02b69-103">本主题讨论编写分析 Windows 应用商店应用内运行的托管代码的诊断工具时需要考虑的事项。</span><span class="sxs-lookup"><span data-stu-id="02b69-103">This topic discusses what you need to think about when writing diagnostic tools that analyze managed code running inside a Windows Store app.</span></span> <span data-ttu-id="02b69-104">它还提供了修改现有开发工具的指导原则，使其在针对 Windows 应用商店应用程序运行时继续运行。</span><span class="sxs-lookup"><span data-stu-id="02b69-104">It also provides guidelines to modify your existing development tools so they continue to work when you run them against Windows Store apps.</span></span> <span data-ttu-id="02b69-105">若要了解此信息，最好是在熟悉公共语言运行时分析 API 的情况下，已在可对 Windows 桌面应用程序正常运行的诊断工具中使用此 API，并且现在有兴趣修改该工具，以便正确地针对 Windows 应用商店应用程序运行。</span><span class="sxs-lookup"><span data-stu-id="02b69-105">To understand this information, it’s best if you're  familiar with the Common Language Runtime Profiling API, you’ve already used this API in a diagnostic tool that runs correctly against Windows desktop applications, and you’re now interested in modifying the tool to run correctly against Windows Store apps.</span></span>

## <a name="introduction"></a><span data-ttu-id="02b69-106">介绍</span><span class="sxs-lookup"><span data-stu-id="02b69-106">Introduction</span></span>

<span data-ttu-id="02b69-107">如果您在介绍的段落之后进行了介绍，那么您就会熟悉 CLR 分析 API。</span><span class="sxs-lookup"><span data-stu-id="02b69-107">If you made it past the introductory paragraph, then you’re familiar with the CLR Profiling API.</span></span> <span data-ttu-id="02b69-108">你已经编写了一个适合托管桌面应用程序的诊断工具。</span><span class="sxs-lookup"><span data-stu-id="02b69-108">You’ve already written a diagnostic tool that works well against managed desktop applications.</span></span> <span data-ttu-id="02b69-109">现在，您想知道如何使用托管的 Windows 应用商店应用程序。</span><span class="sxs-lookup"><span data-stu-id="02b69-109">Now you’re curious what to do so that your tool works with a managed Windows Store app.</span></span> <span data-ttu-id="02b69-110">也许您已经尝试过此工作，并发现它并不是一个简单的任务。</span><span class="sxs-lookup"><span data-stu-id="02b69-110">Perhaps you’ve already tried to make this work, and have discovered that it’s not a straightforward task.</span></span> <span data-ttu-id="02b69-111">事实上，对于所有工具开发人员而言，可能不会有很多注意事项。</span><span class="sxs-lookup"><span data-stu-id="02b69-111">Indeed, there are a number of considerations that might not be obvious to all tools developers.</span></span> <span data-ttu-id="02b69-112">例如：</span><span class="sxs-lookup"><span data-stu-id="02b69-112">For example:</span></span>

- <span data-ttu-id="02b69-113">Windows 应用商店应用在权限严重降低的上下文中运行。</span><span class="sxs-lookup"><span data-stu-id="02b69-113">Windows Store apps run in a context with severely reduced permissions.</span></span>

- <span data-ttu-id="02b69-114">与传统的托管模块相比，Windows 元数据文件具有独特的特征。</span><span class="sxs-lookup"><span data-stu-id="02b69-114">Windows Metadata files have unique characteristics when compared to traditional managed modules.</span></span>

- <span data-ttu-id="02b69-115">当交互式功能下降时，Windows 应用商店应用程序习惯挂起自身。</span><span class="sxs-lookup"><span data-stu-id="02b69-115">Windows Store apps have a habit of suspending themselves when interactivity goes down.</span></span>

- <span data-ttu-id="02b69-116">由于各种原因，进程间通信机制可能不再工作。</span><span class="sxs-lookup"><span data-stu-id="02b69-116">Your inter-process communication mechanisms may no longer work for various reasons.</span></span>

<span data-ttu-id="02b69-117">本主题列出了需要注意的问题以及如何正确处理它们。</span><span class="sxs-lookup"><span data-stu-id="02b69-117">This topic lists the things you need to be aware of and how to deal with them properly.</span></span>

<span data-ttu-id="02b69-118">如果你不熟悉 CLR 分析 API，请跳转到本主题末尾的资源，找到更好的介绍性信息。</span><span class="sxs-lookup"><span data-stu-id="02b69-118">If you’re new to the CLR Profiling API, skip down to the Resources at the end of this topic to find better introductory information.</span></span>

<span data-ttu-id="02b69-119">提供有关特定 Windows Api 的详细信息以及如何使用这些 Api 的详细信息，请参阅本主题的讨论范围。</span><span class="sxs-lookup"><span data-stu-id="02b69-119">Providing detail about specific Windows APIs and how they should be used is also outside the scope of this topic.</span></span> <span data-ttu-id="02b69-120">请考虑本主题中的一个起点，并参考 MSDN，详细了解此处引用的任何 Windows Api。</span><span class="sxs-lookup"><span data-stu-id="02b69-120">Consider this topic a starting point, and refer to MSDN to learn more about any Windows APIs referenced here.</span></span>

## <a name="architecture-and-terminology"></a><span data-ttu-id="02b69-121">体系结构和术语</span><span class="sxs-lookup"><span data-stu-id="02b69-121">Architecture and terminology</span></span>

<span data-ttu-id="02b69-122">通常，诊断工具的体系结构如下图所示。</span><span class="sxs-lookup"><span data-stu-id="02b69-122">Typically, a diagnostic tool has an architecture like the one shown in the following illustration.</span></span> <span data-ttu-id="02b69-123">它使用术语 "探查器"，但许多此类工具比典型的性能或内存分析更好于代码覆盖率、模拟对象框架、时间行程调试、应用程序监视等方面。</span><span class="sxs-lookup"><span data-stu-id="02b69-123">It uses the term "profiler," but many such tools go well beyond typical performance or memory profiling into areas such as code coverage, mock object frameworks, time-travel debugging, application monitoring, and so on.</span></span> <span data-ttu-id="02b69-124">为简单起见，本主题将继续引用所有这些工具作为探查器。</span><span class="sxs-lookup"><span data-stu-id="02b69-124">For simplicity, this topic will continue to refer to all these tools as profilers.</span></span>

<span data-ttu-id="02b69-125">本主题中使用了以下术语：</span><span class="sxs-lookup"><span data-stu-id="02b69-125">The following terminology is used throughout this topic:</span></span>

<span data-ttu-id="02b69-126">应用程序</span><span class="sxs-lookup"><span data-stu-id="02b69-126">**Application**</span></span>

<span data-ttu-id="02b69-127">这是探查器正在分析的应用程序。</span><span class="sxs-lookup"><span data-stu-id="02b69-127">This is the application that the profiler is analyzing.</span></span> <span data-ttu-id="02b69-128">通常，此应用程序的开发人员现在使用探查器来帮助诊断应用程序的问题。</span><span class="sxs-lookup"><span data-stu-id="02b69-128">Typically, the developer of this application is now using the profiler to help diagnose issues with the application.</span></span> <span data-ttu-id="02b69-129">通常，此应用程序将是 Windows 桌面应用程序，但在本主题中，我们将查看 Windows 应用商店应用。</span><span class="sxs-lookup"><span data-stu-id="02b69-129">Traditionally, this application would be a Windows desktop application, but in this topic, we’re looking at Windows Store apps.</span></span>

<span data-ttu-id="02b69-130">**探查器 DLL**</span><span class="sxs-lookup"><span data-stu-id="02b69-130">**Profiler DLL**</span></span>

<span data-ttu-id="02b69-131">这是加载到正在分析的应用程序的进程空间中的组件。</span><span class="sxs-lookup"><span data-stu-id="02b69-131">This is the component that loads into the process space of the application being analyzed.</span></span> <span data-ttu-id="02b69-132">此组件（也称为探查器 "agent"）实现 [ICorProfilerCallback](icorprofilercallback-interface.md)[ICorProfilerCallback 接口](icorprofilercallback-interface.md) (2、3等。 ) 接口并使用 [ICorProfilerInfo](icorprofilerinfo-interface.md) (2、3等 ) 接口来收集有关分析的应用程序的数据，并可能修改应用程序行为的各个方面。</span><span class="sxs-lookup"><span data-stu-id="02b69-132">This component, also known as the profiler "agent," implements the [ICorProfilerCallback](icorprofilercallback-interface.md)[ICorProfilerCallback Interface](icorprofilercallback-interface.md)(2,3,etc.) interfaces and consumes the [ICorProfilerInfo](icorprofilerinfo-interface.md)(2,3,etc.) interfaces to collect data about the analyzed application and potentially modify aspects of the application’s behavior.</span></span>

<span data-ttu-id="02b69-133">**探查器 UI**</span><span class="sxs-lookup"><span data-stu-id="02b69-133">**Profiler UI**</span></span>

<span data-ttu-id="02b69-134">这是探查器用户与之交互的桌面应用程序。</span><span class="sxs-lookup"><span data-stu-id="02b69-134">This is a desktop application that the profiler user interacts with.</span></span> <span data-ttu-id="02b69-135">它负责向用户显示应用程序状态，并为用户提供控制分析的应用程序行为的方法。</span><span class="sxs-lookup"><span data-stu-id="02b69-135">It’s responsible for displaying application status to the user and giving the user the means to control the behavior of the analyzed application.</span></span> <span data-ttu-id="02b69-136">此组件始终在其自己的进程空间中运行，独立于正在分析的应用程序的进程空间。</span><span class="sxs-lookup"><span data-stu-id="02b69-136">This component always runs in its own process space, separate from the process space of the application being profiled.</span></span> <span data-ttu-id="02b69-137">探查器 UI 还可以充当 "附加触发器"，这是调用 [ICLRProfiling：： AttachProfiler](iclrprofiling-attachprofiler-method.md) 方法的过程，在探查器 dll 未在启动时加载的情况下，该过程将导致分析的应用程序加载探查器 dll。</span><span class="sxs-lookup"><span data-stu-id="02b69-137">The Profiler UI can also act as the "attach trigger," which is the process that calls the [ICLRProfiling::AttachProfiler](iclrprofiling-attachprofiler-method.md) method, to cause the analyzed application to load the Profiler DLL in those cases where the profiler DLL did not load on startup.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02b69-138">探查器 UI 应保留为 Windows 桌面应用程序，即使它用于控制和报告 Windows 应用商店应用程序也是如此。</span><span class="sxs-lookup"><span data-stu-id="02b69-138">Your Profiler UI should remain a Windows desktop application, even when it is used to control and report on a Windows Store app.</span></span> <span data-ttu-id="02b69-139">不希望能够在 Windows 应用商店中打包和交付您的诊断工具。</span><span class="sxs-lookup"><span data-stu-id="02b69-139">Don’t expect to be able to package and ship your diagnostics tool in the Windows Store.</span></span> <span data-ttu-id="02b69-140">你的工具需要执行 Windows 应用商店应用无法执行的操作，而其中的许多问题都驻留在探查器 UI 中。</span><span class="sxs-lookup"><span data-stu-id="02b69-140">Your tool needs to do things that Windows Store apps cannot do, and many of those things reside inside your Profiler UI.</span></span>

<span data-ttu-id="02b69-141">在本文档中，示例代码假定：</span><span class="sxs-lookup"><span data-stu-id="02b69-141">Throughout this document, the sample code assumes that:</span></span>

- <span data-ttu-id="02b69-142">探查器 DLL 是用 c + + 编写的，因为它必须是本机 DLL，这要按照 CLR 分析 API 的要求。</span><span class="sxs-lookup"><span data-stu-id="02b69-142">Your Profiler DLL is written in C++, because it must be a native DLL, as per the requirements of the CLR Profiling API.</span></span>

- <span data-ttu-id="02b69-143">探查器 UI 是用 c # 编写的。</span><span class="sxs-lookup"><span data-stu-id="02b69-143">Your Profiler UI is written in C#.</span></span> <span data-ttu-id="02b69-144">这并不是必需的，但由于探查器 UI 过程的语言没有任何要求，为什么不选择简洁而简单的语言？</span><span class="sxs-lookup"><span data-stu-id="02b69-144">This isn’t necessary, but because there are no requirements on the language for your Profiler UI’s process, why not pick a language that’s concise and simple?</span></span>

### <a name="windows-rt-devices"></a><span data-ttu-id="02b69-145">Windows RT 设备</span><span class="sxs-lookup"><span data-stu-id="02b69-145">Windows RT devices</span></span>

<span data-ttu-id="02b69-146">Windows RT 设备已被锁定。</span><span class="sxs-lookup"><span data-stu-id="02b69-146">Windows RT devices are quite locked down.</span></span> <span data-ttu-id="02b69-147">此类设备上不能加载第三方探查器。</span><span class="sxs-lookup"><span data-stu-id="02b69-147">Third-party profilers simply cannot be loaded on such devices.</span></span> <span data-ttu-id="02b69-148">本文档重点介绍 Windows 8 Pc。</span><span class="sxs-lookup"><span data-stu-id="02b69-148">This document focuses on Windows 8 PCs.</span></span>

## <a name="consuming-windows-runtime-apis"></a><span data-ttu-id="02b69-149">使用 Windows 运行时 Api</span><span class="sxs-lookup"><span data-stu-id="02b69-149">Consuming Windows Runtime APIs</span></span>

<span data-ttu-id="02b69-150">在以下各节中讨论的几个方案中，探查器 UI 桌面应用程序需要使用一些新的 Windows 运行时 Api。</span><span class="sxs-lookup"><span data-stu-id="02b69-150">In a number of scenarios discussed in the following sections, your Profiler UI desktop application needs to consume some new Windows Runtime APIs.</span></span> <span data-ttu-id="02b69-151">你需要参考文档来了解可以在桌面应用程序中使用哪些 Windows 运行时 Api，以及从桌面应用程序和 Windows 应用商店应用程序调用它们的行为是否不同。</span><span class="sxs-lookup"><span data-stu-id="02b69-151">You’ll want to consult the documentation to understand which Windows Runtime APIs can be used from desktop applications, and whether their behavior is different when called from desktop applications and Windows Store apps.</span></span>

<span data-ttu-id="02b69-152">如果探查器 UI 是用托管代码编写的，则需要执行几个步骤，以便轻松地使用这些 Windows 运行时 Api。</span><span class="sxs-lookup"><span data-stu-id="02b69-152">If your Profiler UI is written in managed code, there will be a few steps you’ll need to do to make consuming those Windows Runtime APIs easy.</span></span> <span data-ttu-id="02b69-153">有关详细信息，请参阅 [托管桌面应用和 Windows 运行时](/previous-versions/windows/apps/jj856306(v=win.10)) 文章。</span><span class="sxs-lookup"><span data-stu-id="02b69-153">For more information, see the [Managed desktop apps and Windows Runtime](/previous-versions/windows/apps/jj856306(v=win.10)) article.</span></span>

## <a name="loading-the-profiler-dll"></a><span data-ttu-id="02b69-154">加载探查器 DLL</span><span class="sxs-lookup"><span data-stu-id="02b69-154">Loading the Profiler DLL</span></span>

<span data-ttu-id="02b69-155">本部分介绍探查器 UI 如何使 Windows 应用商店应用程序加载探查器 DLL。</span><span class="sxs-lookup"><span data-stu-id="02b69-155">This section describes how your Profiler UI causes the Windows Store app to load your Profiler DLL.</span></span> <span data-ttu-id="02b69-156">本节中讨论的代码属于探查器 UI 桌面应用程序，因此涉及使用适用于桌面应用程序的 Windows Api，但对于 Windows 应用商店应用程序不一定是安全的。</span><span class="sxs-lookup"><span data-stu-id="02b69-156">The code discussed in this section belongs in your Profiler UI desktop app, and therefore involves using Windows APIs that are safe for desktop apps but not necessarily safe for Windows Store apps.</span></span>

<span data-ttu-id="02b69-157">探查器 UI 会使探查器 DLL 以两种方式加载到应用程序的进程空间中：</span><span class="sxs-lookup"><span data-stu-id="02b69-157">Your Profiler UI can cause your Profiler DLL to be loaded into the application’s process space in two ways:</span></span>

- <span data-ttu-id="02b69-158">在应用程序启动时，由环境变量控制。</span><span class="sxs-lookup"><span data-stu-id="02b69-158">At application startup, as controlled by environment variables.</span></span>

- <span data-ttu-id="02b69-159">通过调用 [ICLRProfiling：： AttachProfiler](iclrprofiling-attachprofiler-method.md) 方法，在启动完成后附加到应用程序。</span><span class="sxs-lookup"><span data-stu-id="02b69-159">By attaching to the application after startup is complete by calling the [ICLRProfiling::AttachProfiler](iclrprofiling-attachprofiler-method.md) method.</span></span>

<span data-ttu-id="02b69-160">你的第一项障碍是将探查器 DLL 的启动加载和附加负载加载到一起，以便在 Windows 应用商店应用程序中正常工作。</span><span class="sxs-lookup"><span data-stu-id="02b69-160">One of your first roadblocks will be getting startup-load and attach-load of your Profiler DLL to work properly with Windows Store apps.</span></span> <span data-ttu-id="02b69-161">这两种形式的加载均共用一些特别的注意事项，因此让我们从它们开始。</span><span class="sxs-lookup"><span data-stu-id="02b69-161">Both forms of loading share some special considerations in common, so let’s start with them.</span></span>

### <a name="common-considerations-for-startup-and-attach-loads"></a><span data-ttu-id="02b69-162">启动和附加加载的常见注意事项</span><span class="sxs-lookup"><span data-stu-id="02b69-162">Common considerations for startup and attach loads</span></span>

<span data-ttu-id="02b69-163">**对探查器 DLL 进行签名**</span><span class="sxs-lookup"><span data-stu-id="02b69-163">**Signing your Profiler DLL**</span></span>

<span data-ttu-id="02b69-164">当 Windows 尝试加载探查器 DLL 时，它将验证探查器 DLL 是否已正确签名。</span><span class="sxs-lookup"><span data-stu-id="02b69-164">When Windows attempts to load your Profiler DLL, it verifies that your Profiler DLL is properly signed.</span></span> <span data-ttu-id="02b69-165">如果不是，则默认情况下加载失败。</span><span class="sxs-lookup"><span data-stu-id="02b69-165">If not, the load fails by default.</span></span> <span data-ttu-id="02b69-166">可通过两种方式实现此目的：</span><span class="sxs-lookup"><span data-stu-id="02b69-166">There are two ways to do this:</span></span>

- <span data-ttu-id="02b69-167">确保探查器 DLL 已签名。</span><span class="sxs-lookup"><span data-stu-id="02b69-167">Ensure that your Profiler DLL is signed.</span></span>

- <span data-ttu-id="02b69-168">请告诉你的用户，他们必须先在 Windows 8 计算机上安装开发人员许可证，然后才能使用你的工具。</span><span class="sxs-lookup"><span data-stu-id="02b69-168">Tell your user that they must install a developer license on their Windows 8 machine before using your tool.</span></span> <span data-ttu-id="02b69-169">可以通过 Visual Studio 自动完成此操作，也可以从命令提示符手动完成此操作。</span><span class="sxs-lookup"><span data-stu-id="02b69-169">This can be done automatically from Visual Studio or manually from a command prompt.</span></span> <span data-ttu-id="02b69-170">有关详细信息，请参阅 [获取开发人员许可证](/previous-versions/windows/apps/hh974578(v=win.10))。</span><span class="sxs-lookup"><span data-stu-id="02b69-170">For more information, see [Get a developer license](/previous-versions/windows/apps/hh974578(v=win.10)).</span></span>

<span data-ttu-id="02b69-171">**文件系统权限**</span><span class="sxs-lookup"><span data-stu-id="02b69-171">**File system permissions**</span></span>

<span data-ttu-id="02b69-172">Windows 应用商店应用程序必须有权从文件系统上的 residesBy 默认值加载和执行探查器 DLL，Windows 应用商店应用程序对大多数目录没有此类权限，尝试加载探查器 DLL 将在 Windows 应用程序事件日志中生成类似于以下内容的条目：:</span><span class="sxs-lookup"><span data-stu-id="02b69-172">The Windows Store app must have permission to load and execute your Profiler DLL from the location on the file system in which it residesBy default, the Windows Store app doesn’t have such permission on most directories, and any failed attempt to load your Profiler DLL will produce an entry in the Windows Application event log that looks something like this:</span></span>

```output
NET Runtime version 4.0.30319.17929 - Loading profiler failed during CoCreateInstance.  Profiler CLSID: '{xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}'.  HRESULT: 0x80070005.  Process ID (decimal): 4688.  Message ID: [0x2504].
```

<span data-ttu-id="02b69-173">通常，仅允许 Windows 应用商店应用访问磁盘上有限的位置集。</span><span class="sxs-lookup"><span data-stu-id="02b69-173">Generally, Windows Store apps are only allowed to access a limited set of locations on the disk.</span></span> <span data-ttu-id="02b69-174">每个 Windows 应用商店应用程序都可以访问自己的应用程序数据文件夹，还可以访问文件系统中所有 Windows 应用商店应用获得访问权限的其他一些区域。</span><span class="sxs-lookup"><span data-stu-id="02b69-174">Each Windows Store app can access its own application data folders, as well as a few other areas in the file system for which all Windows Store apps are granted access.</span></span> <span data-ttu-id="02b69-175">最好将探查器 DLL 及其依赖项安装在程序文件或程序文件 (x86) 下，因为所有 Windows 应用商店应用程序在默认情况下都具有读取和执行权限。</span><span class="sxs-lookup"><span data-stu-id="02b69-175">It's best to install your Profiler DLL and its dependencies somewhere under Program Files or Program Files (x86), because all Windows Store apps have read and execute permissions there by default.</span></span>

### <a name="startup-load"></a><span data-ttu-id="02b69-176">启动负载</span><span class="sxs-lookup"><span data-stu-id="02b69-176">Startup load</span></span>

<span data-ttu-id="02b69-177">通常情况下，在桌面应用程序中，探查器 UI 会通过初始化包含所需 CLR 分析 API 环境 (变量的环境块（例如，、、和) ）来提示探查器 DLL 的启动负载， `COR_PROFILER` `COR_ENABLE_PROFILING` `COR_PROFILER_PATH` 然后使用该环境块创建新的进程。</span><span class="sxs-lookup"><span data-stu-id="02b69-177">Typically, in a desktop app, your Profiler UI prompts a startup load of your Profiler DLL by initializing an environment block that contains the required CLR Profiling API environment variables (i.e., `COR_PROFILER`, `COR_ENABLE_PROFILING`, and `COR_PROFILER_PATH`), and then creating a new process with that environment block.</span></span> <span data-ttu-id="02b69-178">这同样适用于 Windows 应用商店应用，但机制有所不同。</span><span class="sxs-lookup"><span data-stu-id="02b69-178">The same holds true for Windows Store apps, but the mechanisms are different.</span></span>

<span data-ttu-id="02b69-179">**请勿运行提升**</span><span class="sxs-lookup"><span data-stu-id="02b69-179">**Don’t run elevated**</span></span>

<span data-ttu-id="02b69-180">如果处理尝试生成 Windows 应用商店应用进程 B，则进程 A 应以中等完整性级别运行，而不是在高完整性级别运行 (即，不) 提升。</span><span class="sxs-lookup"><span data-stu-id="02b69-180">If Process A attempts to spawn Windows Store app Process B, Process A should be run at medium integrity level, not at high integrity level (that is, not elevated).</span></span> <span data-ttu-id="02b69-181">这意味着探查器 UI 应以中等完整性级别运行，或者必须在中等完整性级别生成另一个桌面进程，才能启动 Windows 应用商店应用。</span><span class="sxs-lookup"><span data-stu-id="02b69-181">This means that either your Profiler UI should be running at medium integrity level, or it must spawn another desktop process at medium integrity level to take care of launching the Windows Store app.</span></span>

<span data-ttu-id="02b69-182">**选择要分析的 Windows 应用商店应用程序**</span><span class="sxs-lookup"><span data-stu-id="02b69-182">**Choosing a Windows Store App to profile**</span></span>

<span data-ttu-id="02b69-183">首先，需要询问探查器用户要启动哪个 Windows 应用商店应用。</span><span class="sxs-lookup"><span data-stu-id="02b69-183">First, you’ll want to ask your profiler user which Windows Store app to launch.</span></span> <span data-ttu-id="02b69-184">对于桌面应用程序，可能会显示文件浏览对话框，用户将找到并选择 .exe 文件。</span><span class="sxs-lookup"><span data-stu-id="02b69-184">For desktop apps, perhaps you’d show a file Browse dialog, and the user would find and select an .exe file.</span></span> <span data-ttu-id="02b69-185">但 Windows 应用商店应用程序是不同的，使用 "浏览" 对话框没有什么意义。</span><span class="sxs-lookup"><span data-stu-id="02b69-185">But Windows Store apps are different, and using a Browse dialog doesn’t make sense.</span></span> <span data-ttu-id="02b69-186">相反，更好的做法是向用户显示为该用户安装的 Windows 应用商店应用列表，以供选择。</span><span class="sxs-lookup"><span data-stu-id="02b69-186">Instead, it’s better to show the user a list of Windows Store apps installed for that user to select from.</span></span>

<span data-ttu-id="02b69-187">您可以使用 <xref:Windows.Management.Deployment.PackageManager> 类来生成此列表。</span><span class="sxs-lookup"><span data-stu-id="02b69-187">You can use the <xref:Windows.Management.Deployment.PackageManager> class to generate this list.</span></span> <span data-ttu-id="02b69-188">`PackageManager` 是可供桌面应用使用的 Windows 运行时类，实际上它 *仅* 适用于桌面应用程序。</span><span class="sxs-lookup"><span data-stu-id="02b69-188">`PackageManager` is a Windows Runtime class that is available to desktop apps, and in fact it is *only* available to desktop apps.</span></span>

<span data-ttu-id="02b69-189">下面的代码示例来自用 c # 编写为桌面应用程序的假设探查器 UI 使用 `PackageManager` 来生成 Windows 应用列表：</span><span class="sxs-lookup"><span data-stu-id="02b69-189">The following code example from a hypothetical Profiler UI written as a desktop app in C# uses the `PackageManager` to generate a list of Windows apps:</span></span>

```csharp
string currentUserSID = WindowsIdentity.GetCurrent().User.ToString();
IAppxFactory appxFactory = (IAppxFactory) new AppxFactory();
PackageManager packageManager = new PackageManager();
IEnumerable<Package> packages = packageManager.FindPackagesForUser(currentUserSID);
```

<span data-ttu-id="02b69-190">**指定自定义环境块**</span><span class="sxs-lookup"><span data-stu-id="02b69-190">**Specifying the custom environment block**</span></span>

<span data-ttu-id="02b69-191">使用新的 COM 接口 [IPackageDebugSettings](/windows/desktop/api/shobjidl_core/nn-shobjidl_core-ipackagedebugsettings)，你可以自定义 Windows 应用商店应用程序的执行行为，使某些形式的诊断变得更容易。</span><span class="sxs-lookup"><span data-stu-id="02b69-191">A new COM interface, [IPackageDebugSettings](/windows/desktop/api/shobjidl_core/nn-shobjidl_core-ipackagedebugsettings), allows you to customize the execution behavior of a Windows Store app to make some forms of diagnostics easier.</span></span> <span data-ttu-id="02b69-192">它的一个方法（ [EnableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-enabledebugging)）可让你在 Windows 应用商店应用程序启动时将其传递到 Windows 应用商店应用程序，以及其他有用的效果，如禁用自动进程挂起。</span><span class="sxs-lookup"><span data-stu-id="02b69-192">One of its methods, [EnableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-enabledebugging), lets you pass an environment block to the Windows Store app when it’s launched, along with other useful effects like disabling automatic process suspension.</span></span> <span data-ttu-id="02b69-193">环境块很重要，因为在这种情况下，需要指定 CLR 使用的环境变量 `COR_PROFILER` ， (、 `COR_ENABLE_PROFILING` 和) 来 `COR_PROFILER_PATH)` 加载探查器 DLL。</span><span class="sxs-lookup"><span data-stu-id="02b69-193">The environment block is important because that’s where you need to specify the environment variables (`COR_PROFILER`, `COR_ENABLE_PROFILING`, and `COR_PROFILER_PATH)`) used by the CLR to load your Profiler DLL .</span></span>

<span data-ttu-id="02b69-194">请思考以下代码片段：</span><span class="sxs-lookup"><span data-stu-id="02b69-194">Consider the following code snippet:</span></span>

```csharp
IPackageDebugSettings pkgDebugSettings = new PackageDebugSettings();
pkgDebugSettings.EnableDebugging(packageFullName, debuggerCommandLine,
                                                                 (IntPtr)fixedEnvironmentPzz);
```

<span data-ttu-id="02b69-195">你需要获取几项权限：</span><span class="sxs-lookup"><span data-stu-id="02b69-195">There are a couple of items you'll need to get right:</span></span>

- <span data-ttu-id="02b69-196">`packageFullName` 可以在循环访问包和抓取时确定 `package.Id.FullName` 。</span><span class="sxs-lookup"><span data-stu-id="02b69-196">`packageFullName` can be determined while iterating over the packages and grabbing `package.Id.FullName`.</span></span>

- <span data-ttu-id="02b69-197">`debuggerCommandLine` 稍微有趣一些。</span><span class="sxs-lookup"><span data-stu-id="02b69-197">`debuggerCommandLine` is a bit more interesting.</span></span> <span data-ttu-id="02b69-198">若要将自定义环境块传递到 Windows 应用商店应用程序，需要编写自己的、简化的虚拟调试器。</span><span class="sxs-lookup"><span data-stu-id="02b69-198">In order to pass the custom environment block to the Windows Store app, you need to write your own, simplistic dummy debugger.</span></span> <span data-ttu-id="02b69-199">Windows 将生成 Windows 应用商店应用程序，然后通过使用以下示例中的命令行启动调试器来附加调试器：</span><span class="sxs-lookup"><span data-stu-id="02b69-199">Windows spawns the Windows Store app suspended and then attaches your debugger by launching your debugger with a command line like in this example:</span></span>

    ```console
    MyDummyDebugger.exe -p 1336 -tid 1424
    ```

     <span data-ttu-id="02b69-200">其中， `-p 1336` 表示 Windows 应用商店应用程序的进程 id 为1336， `-tid 1424` 表示线程 id 1424 是已挂起的线程。</span><span class="sxs-lookup"><span data-stu-id="02b69-200">where `-p 1336` means the Windows Store app has Process ID 1336, and `-tid 1424` means Thread ID 1424 is the thread that is suspended.</span></span> <span data-ttu-id="02b69-201">虚拟调试器将从命令行分析 ThreadID，恢复该线程，然后退出。</span><span class="sxs-lookup"><span data-stu-id="02b69-201">Your dummy debugger would parse the ThreadID from the command-line, resume that thread, and then exit.</span></span>

     <span data-ttu-id="02b69-202">下面是用于执行此操作的一些示例 c + + 代码 (确保添加错误检查！ ) ：</span><span class="sxs-lookup"><span data-stu-id="02b69-202">Here’s some example C++ code to do this (be sure to add error checking!):</span></span>

    ```cpp
    int wmain(int argc, wchar_t* argv[])
    {
        // …
        // Parse command line here
        // …

        HANDLE hThread = OpenThread(THREAD_SUSPEND_RESUME,
                                                                  FALSE /* bInheritHandle */, nThreadID);
        ResumeThread(hThread);
        CloseHandle(hThread);
        return 0;
    }
    ```

     <span data-ttu-id="02b69-203">需要在诊断工具安装过程中部署此虚拟调试器，然后在参数中指定此调试器的路径 `debuggerCommandLine` 。</span><span class="sxs-lookup"><span data-stu-id="02b69-203">You’ll need to deploy this dummy debugger as part of your diagnostics tool installation, and then specify the path to this debugger in the `debuggerCommandLine` parameter.</span></span>

<span data-ttu-id="02b69-204">**启动 Windows 应用商店应用程序**</span><span class="sxs-lookup"><span data-stu-id="02b69-204">**Launching the Windows Store app**</span></span>

<span data-ttu-id="02b69-205">开始 Windows 应用商店应用程序的启动时间最后到达。</span><span class="sxs-lookup"><span data-stu-id="02b69-205">The moment to launch the Windows Store app has finally arrived.</span></span> <span data-ttu-id="02b69-206">如果已尝试自行执行此操作，则可能已注意到 [CreateProcess](/windows/desktop/api/processthreadsapi/nf-processthreadsapi-createprocessa) 并不是创建 Windows 应用商店应用程序进程的方式。</span><span class="sxs-lookup"><span data-stu-id="02b69-206">If you’ve already tried doing this yourself, you may have noticed that [CreateProcess](/windows/desktop/api/processthreadsapi/nf-processthreadsapi-createprocessa) is not how you create a Windows Store app process.</span></span> <span data-ttu-id="02b69-207">相反，你将需要使用 [IApplicationActivationManager：： ActivateApplication](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-iapplicationactivationmanager-activateapplication) 方法。</span><span class="sxs-lookup"><span data-stu-id="02b69-207">Instead, you’ll need to use the [IApplicationActivationManager::ActivateApplication](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-iapplicationactivationmanager-activateapplication) method.</span></span> <span data-ttu-id="02b69-208">为此，需要获取正在启动的 Windows 应用商店应用程序的应用程序用户模型 ID。</span><span class="sxs-lookup"><span data-stu-id="02b69-208">To do that, you’ll need to get the App User Model ID of the Windows Store app that you’re launching.</span></span> <span data-ttu-id="02b69-209">这意味着你需要通过清单执行一些深入。</span><span class="sxs-lookup"><span data-stu-id="02b69-209">And that means you’ll need to do a little digging through the manifest.</span></span>

<span data-ttu-id="02b69-210">遍历包时 (参阅前面的 [启动加载](#startup-load) 部分中的 "选择要配置的 Windows 应用商店应用程序") ，你将需要获取当前包清单中包含的应用程序集：</span><span class="sxs-lookup"><span data-stu-id="02b69-210">While iterating over your packages (see "Choosing a Windows Store App to Profile" in the [Startup load](#startup-load) section earlier), you’ll want to grab the set of applications contained in the current package’s manifest:</span></span>

```csharp
string manifestPath = package.InstalledLocation.Path + "\\AppxManifest.xml";

AppxPackaging.IStream manifestStream;
SHCreateStreamOnFileEx(
                    manifestPath,
                    0x00000040,     // STGM_READ | STGM_SHARE_DENY_NONE
                    0,              // file creation attributes
                    false,          // fCreate
                    null,           // reserved
                    out manifestStream);

IAppxManifestReader manifestReader = appxFactory.CreateManifestReader(manifestStream);

IAppxManifestApplicationsEnumerator appsEnum = manifestReader.GetApplications();
```

<span data-ttu-id="02b69-211">是，一个包可以包含多个应用程序，每个应用程序都有自己的应用程序用户模型 ID。</span><span class="sxs-lookup"><span data-stu-id="02b69-211">Yes, one package can have multiple applications, and each application has its own Application User Model ID.</span></span> <span data-ttu-id="02b69-212">因此，您需要询问用户要分析的应用程序，并从该特定应用程序获取应用程序用户模型 ID：</span><span class="sxs-lookup"><span data-stu-id="02b69-212">So you’ll want to ask your user which application to profile, and grab the Application User Model ID from that particular application:</span></span>

```csharp
while (appsEnum.GetHasCurrent() != 0)
{
    IAppxManifestApplication app = appsEnum.GetCurrent();
    string appUserModelId = app.GetAppUserModelId();
    //...
}
```

<span data-ttu-id="02b69-213">最后，你将需要启动 Windows 应用商店应用程序：</span><span class="sxs-lookup"><span data-stu-id="02b69-213">Finally, you now have what you need to launch the Windows Store app:</span></span>

```csharp
IApplicationActivationManager appActivationMgr = new ApplicationActivationManager();
appActivationMgr.ActivateApplication(appUserModelId, appArgs, ACTIVATEOPTIONS.AO_NONE, out pid);
```

<span data-ttu-id="02b69-214">**记得调用 DisableDebugging**</span><span class="sxs-lookup"><span data-stu-id="02b69-214">**Remember to call DisableDebugging**</span></span>

<span data-ttu-id="02b69-215">调用 [IPackageDebugSettings：： EnableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-enabledebugging)时，通过调用 [IPackageDebugSettings：:D isabledebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-disabledebugging) 方法，你就会作出一种承诺，因此在分析会话结束时请务必执行此操作。</span><span class="sxs-lookup"><span data-stu-id="02b69-215">When you called [IPackageDebugSettings::EnableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-enabledebugging), you made a promise that you would clean up after yourself by calling the [IPackageDebugSettings::DisableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-disabledebugging) method, so be sure to do that when the profiling session is over.</span></span>

### <a name="attach-load"></a><span data-ttu-id="02b69-216">附加负载</span><span class="sxs-lookup"><span data-stu-id="02b69-216">Attach load</span></span>

<span data-ttu-id="02b69-217">当探查器 UI 要将其探查器 DLL 附加到已开始运行的应用程序时，它将使用 [ICLRProfiling：： AttachProfiler](iclrprofiling-attachprofiler-method.md)。</span><span class="sxs-lookup"><span data-stu-id="02b69-217">When your Profiler UI wants to attach its Profiler DLL to an application that has already started running, it uses [ICLRProfiling::AttachProfiler](iclrprofiling-attachprofiler-method.md).</span></span> <span data-ttu-id="02b69-218">这同样适用于 Windows 应用商店应用。</span><span class="sxs-lookup"><span data-stu-id="02b69-218">The same holds true with Windows Store apps.</span></span> <span data-ttu-id="02b69-219">但除了前面列出的常见注意事项外，还请确保目标 Windows 应用商店应用未挂起。</span><span class="sxs-lookup"><span data-stu-id="02b69-219">But in addition to the common considerations listed earlier, make sure the that the target Windows Store app is not suspended.</span></span>

<span data-ttu-id="02b69-220">**EnableDebugging**</span><span class="sxs-lookup"><span data-stu-id="02b69-220">**EnableDebugging**</span></span>

<span data-ttu-id="02b69-221">与启动负载一样，请调用 [IPackageDebugSettings：： EnableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-enabledebugging) 方法。</span><span class="sxs-lookup"><span data-stu-id="02b69-221">As with startup load, call the [IPackageDebugSettings::EnableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-enabledebugging) method.</span></span> <span data-ttu-id="02b69-222">不需要它来传递环境块，但需要其其他功能之一：禁用自动进程挂起。</span><span class="sxs-lookup"><span data-stu-id="02b69-222">You don’t need it for passing an environment block, but you need one of its other features: disabling automatic process suspension.</span></span> <span data-ttu-id="02b69-223">否则，当探查器 UI 调用 [AttachProfiler](iclrprofiling-attachprofiler-method.md)时，可能会挂起目标 Windows 应用商店应用。</span><span class="sxs-lookup"><span data-stu-id="02b69-223">Otherwise, when your Profiler UI calls [AttachProfiler](iclrprofiling-attachprofiler-method.md), the target Windows Store app may be suspended.</span></span> <span data-ttu-id="02b69-224">事实上，如果用户现在与探查器 UI 交互，Windows 应用商店应用程序在用户的任何屏幕上都处于非活动状态，则可能会出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="02b69-224">In fact, this is likely if the user is now interacting with your Profiler UI, and the Windows Store app is not active on any of the user’s screens.</span></span> <span data-ttu-id="02b69-225">如果 Windows 应用商店应用程序被挂起，它将无法响应 CLR 向其发送的任何信号来附加探查器 DLL。</span><span class="sxs-lookup"><span data-stu-id="02b69-225">And if the Windows Store app is suspended, it won’t be able to respond to any signal that the CLR sends to it to attach your Profiler DLL.</span></span>

<span data-ttu-id="02b69-226">因此，您需要执行如下所示的操作：</span><span class="sxs-lookup"><span data-stu-id="02b69-226">So you’ll want to do something like this:</span></span>

```csharp
IPackageDebugSettings pkgDebugSettings = new PackageDebugSettings();
pkgDebugSettings.EnableDebugging(packageFullName, null /* debuggerCommandLine */,
                                                                 IntPtr.Zero /* environment */);
```

<span data-ttu-id="02b69-227">除了指定调试器命令行或环境块以外，还可以对启动负载情况进行此调用。</span><span class="sxs-lookup"><span data-stu-id="02b69-227">This is the same call you’d make for the startup load case, except you don’t specify a debugger command line or an environment block.</span></span>

<span data-ttu-id="02b69-228">**DisableDebugging**</span><span class="sxs-lookup"><span data-stu-id="02b69-228">**DisableDebugging**</span></span>

<span data-ttu-id="02b69-229">与往常一样，请不要忘记在分析会话完成时调用 [IPackageDebugSettings：:D isabledebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-disabledebugging) 。</span><span class="sxs-lookup"><span data-stu-id="02b69-229">As always, don’t forget to call [IPackageDebugSettings::DisableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-disabledebugging) when your profiling session is completed.</span></span>

## <a name="running-inside-the-windows-store-app"></a><span data-ttu-id="02b69-230">在 Windows 应用商店应用内运行</span><span class="sxs-lookup"><span data-stu-id="02b69-230">Running inside the Windows Store app</span></span>

<span data-ttu-id="02b69-231">因此，Windows 应用商店应用最终会加载探查器 DLL。</span><span class="sxs-lookup"><span data-stu-id="02b69-231">So the Windows Store app has finally loaded your Profiler DLL.</span></span> <span data-ttu-id="02b69-232">现在，必须通过 Windows 应用商店应用所需的不同规则来讲授探查器 DLL 的播放方式，其中包括允许哪些 Api 以及如何使用降低的权限运行。</span><span class="sxs-lookup"><span data-stu-id="02b69-232">Now your Profiler DLL must be taught how to play by the different rules required by Windows Store apps, including which APIs are allowable and how to run with reduced permissions.</span></span>

### <a name="stick-to-the-windows-store-app-apis"></a><span data-ttu-id="02b69-233">坚持 Windows 应用商店应用 Api</span><span class="sxs-lookup"><span data-stu-id="02b69-233">Stick to the Windows Store app APIs</span></span>

<span data-ttu-id="02b69-234">浏览 Windows API 时，你会注意到，每个 API 都记录为适用于桌面应用、Windows 应用商店应用或两者。</span><span class="sxs-lookup"><span data-stu-id="02b69-234">As you browse the Windows API, you’ll notice that every API is documented as being applicable to desktop apps, Windows Store apps, or both.</span></span> <span data-ttu-id="02b69-235">例如， [InitializeCriticalSectionAndSpinCount](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionandspincount)函数文档的 " **要求** " 部分指示该函数仅适用于桌面应用程序。</span><span class="sxs-lookup"><span data-stu-id="02b69-235">For example, the **Requirements** section of the documentation for the [InitializeCriticalSectionAndSpinCount](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionandspincount) function indicates that the function applies to desktop apps only.</span></span> <span data-ttu-id="02b69-236">与此相反， [InitializeCriticalSectionEx](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionex) 函数可用于桌面应用和 Windows 应用商店应用。</span><span class="sxs-lookup"><span data-stu-id="02b69-236">In contrast, the [InitializeCriticalSectionEx](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionex) function is available for both desktop apps and Windows Store apps.</span></span>

<span data-ttu-id="02b69-237">在开发探查器 DLL 时，将它视为 Windows 应用商店应用程序，并且仅使用 Windows 应用商店应用程序所记录的 Api。</span><span class="sxs-lookup"><span data-stu-id="02b69-237">When developing your Profiler DLL, treat it as if it’s a Windows Store app and only use APIs that are documented as available to Windows Store apps.</span></span> <span data-ttu-id="02b69-238">分析依赖关系 (例如，你可以 `link /dump /imports` 针对探查器 DLL 运行审核) ，然后在文档中搜索，以查看哪些依赖项正常，哪些依赖项不正常。</span><span class="sxs-lookup"><span data-stu-id="02b69-238">Analyze your dependencies (for example, you can run `link /dump /imports` against your Profiler DLL to audit), and then search the docs to see which of your dependencies are ok and which aren’t.</span></span> <span data-ttu-id="02b69-239">在大多数情况下，只需将冲突替换为一种较新的 API 形式，将其替换为安全 (（例如，将 [InitializeCriticalSectionAndSpinCount](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionandspincount) 替换为 [InitializeCriticalSectionEx](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionex)) ，即可解决冲突。</span><span class="sxs-lookup"><span data-stu-id="02b69-239">In most cases, your violations can be fixed by simply replacing them with a newer form of the API that is documented as safe (for example, replacing [InitializeCriticalSectionAndSpinCount](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionandspincount) with [InitializeCriticalSectionEx](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionex)).</span></span>

<span data-ttu-id="02b69-240">你可能会注意到，探查器 DLL 会调用一些仅适用于桌面应用的 Api，并且即使在 Windows 应用商店应用程序中加载探查器 DLL，它们仍可正常工作。</span><span class="sxs-lookup"><span data-stu-id="02b69-240">You might notice that your Profiler DLL calls some APIs that apply to desktop apps only, and yet they seem to work even when your Profiler DLL is loaded inside a Windows Store app.</span></span> <span data-ttu-id="02b69-241">请注意，在加载到 Windows 应用商店应用程序进程中时，使用未记录在 Windows 应用商店应用中的任何 API 会出现风险：</span><span class="sxs-lookup"><span data-stu-id="02b69-241">Be aware that it’s risky to use any API not documented for use with Windows Store apps in your Profiler DLL when loaded into a Windows Store app process:</span></span>

- <span data-ttu-id="02b69-242">在运行 Windows 应用商店应用的唯一上下文中调用此类 Api 时，不一定能够正常工作。</span><span class="sxs-lookup"><span data-stu-id="02b69-242">Such APIs are not guaranteed to work when called in the unique context that Windows Store apps run in.</span></span>

- <span data-ttu-id="02b69-243">从不同的 Windows 应用商店应用程序进程中调用此类 Api 可能不会运行。</span><span class="sxs-lookup"><span data-stu-id="02b69-243">Such APIs might not work consistently when called from within different Windows Store app processes.</span></span>

- <span data-ttu-id="02b69-244">在当前版本的 windows 中，此类 Api 看起来可以正常工作，但可能会在将来的 Windows 版本中中断或禁用。</span><span class="sxs-lookup"><span data-stu-id="02b69-244">Such APIs might seem to work fine from Windows Store apps in the current version of Windows, but may break or be disabled in future releases of Windows.</span></span>

<span data-ttu-id="02b69-245">最好的做法是解决所有冲突，并避免风险。</span><span class="sxs-lookup"><span data-stu-id="02b69-245">The best advice is to fix all your violations and avoid the risk.</span></span>

<span data-ttu-id="02b69-246">你可能会发现，如果没有特定的 API，则无法找到适合 Windows 应用商店应用的替换。</span><span class="sxs-lookup"><span data-stu-id="02b69-246">You might find that you absolutely cannot do without a particular API and cannot find a replacement suitable for Windows Store apps.</span></span> <span data-ttu-id="02b69-247">在这种情况下，至少要：</span><span class="sxs-lookup"><span data-stu-id="02b69-247">In such a case, at a minimum:</span></span>

- <span data-ttu-id="02b69-248">测试、测试、测试生活中的 daylights 使用该 API。</span><span class="sxs-lookup"><span data-stu-id="02b69-248">Test, test, test the living daylights out of your usage of that API.</span></span>

- <span data-ttu-id="02b69-249">了解如果在 Windows 未来版本中从 Windows 应用商店应用程序内部调用，API 可能突然中断或消失。</span><span class="sxs-lookup"><span data-stu-id="02b69-249">Understand that the API might suddenly break or disappear if called from inside Windows Store apps in future releases of Windows.</span></span> <span data-ttu-id="02b69-250">这不会被认为是 Microsoft 的兼容性问题，并且支持你的使用不会成为优先考虑。</span><span class="sxs-lookup"><span data-stu-id="02b69-250">This won’t be considered a compatibility concern by Microsoft, and supporting your usage of it will not be a priority.</span></span>

### <a name="reduced-permissions"></a><span data-ttu-id="02b69-251">降低的权限</span><span class="sxs-lookup"><span data-stu-id="02b69-251">Reduced permissions</span></span>

<span data-ttu-id="02b69-252">本主题的范围超出了 Windows 应用商店应用程序权限与桌面应用程序的不同之处。</span><span class="sxs-lookup"><span data-stu-id="02b69-252">It’s outside the scope of this topic to list all the ways that Windows Store app permissions differ from desktop apps.</span></span> <span data-ttu-id="02b69-253">但在加载到 Windows 应用商店应用程序中时，与桌面应用程序) 尝试访问任何资源时，每次加载到 Windows 应用商店应用程序时，行为都是不同的 (。</span><span class="sxs-lookup"><span data-stu-id="02b69-253">But certainly the behavior will be different every time your Profiler DLL (when loaded into a Windows Store app as compared to a desktop app) tries to access any resources.</span></span> <span data-ttu-id="02b69-254">文件系统是最常见的示例。</span><span class="sxs-lookup"><span data-stu-id="02b69-254">The file system is the most common example.</span></span> <span data-ttu-id="02b69-255">某些情况下，给定的 Windows 应用商店应用程序可以访问磁盘上的一些位置 (请参阅 [文件访问和权限 (Windows 运行时应用程序](/previous-versions/windows/apps/hh967755(v=win.10))) ，探查器 DLL 将受到相同的限制。</span><span class="sxs-lookup"><span data-stu-id="02b69-255">There are but a few places on disk that a given Windows Store app is allowed to access (see [File access and permissions (Windows Runtime apps](/previous-versions/windows/apps/hh967755(v=win.10))), and your Profiler DLL will be under the same restrictions.</span></span> <span data-ttu-id="02b69-256">彻底测试你的代码。</span><span class="sxs-lookup"><span data-stu-id="02b69-256">Test your code thoroughly.</span></span>

### <a name="inter-process-communication"></a><span data-ttu-id="02b69-257">进程内通信</span><span class="sxs-lookup"><span data-stu-id="02b69-257">Inter-process communication</span></span>

<span data-ttu-id="02b69-258">正如本文开头的关系图中所示，探查器 DLL (加载到 Windows 应用商店应用程序的进程空间中) 可能需要与探查器 UI 通信， (在单独的桌面应用程序进程空间中运行) 通过自定义的进程间通信 (IPC) 通道。</span><span class="sxs-lookup"><span data-stu-id="02b69-258">As shown in the diagram at the beginning of this paper, your Profiler DLL (loaded into the Windows Store app process space) will likely need to communicate with your Profiler UI (running in a separate desktop app process space) through your own custom inter-process communication (IPC) channel.</span></span> <span data-ttu-id="02b69-259">探查器 UI 将信号发送到探查器 DLL 以修改其行为，探查器 DLL 将数据从经过分析的 Windows 应用商店应用程序发送回探查器 UI，以便后期处理和向探查器用户显示。</span><span class="sxs-lookup"><span data-stu-id="02b69-259">The Profiler UI sends signals to the Profiler DLL to modify its behavior, and the Profiler DLL sends data from the analyzed Windows Store app back to the Profiler UI for post-processing and displaying to the profiler user.</span></span>

<span data-ttu-id="02b69-260">大多数探查器都需要这样的工作，但当探查器 DLL 加载到 Windows 应用商店应用程序中时，对 IPC 机制的选择更受限制。</span><span class="sxs-lookup"><span data-stu-id="02b69-260">Most profilers need to work this way, but your choices for IPC mechanisms are more limited when your Profiler DLL is loaded into a Windows Store app.</span></span> <span data-ttu-id="02b69-261">例如，命名管道不是 Windows 应用商店应用 SDK 的一部分，因此不能使用它们。</span><span class="sxs-lookup"><span data-stu-id="02b69-261">For example, named pipes are not part of the Windows Store app SDK, so you cannot use them.</span></span>

<span data-ttu-id="02b69-262">当然，文件仍处于中，不过，这种方式的方式更有限。</span><span class="sxs-lookup"><span data-stu-id="02b69-262">But of course, files are still in, albeit in a more limited fashion.</span></span> <span data-ttu-id="02b69-263">事件也可用。</span><span class="sxs-lookup"><span data-stu-id="02b69-263">Events are also available.</span></span>

<span data-ttu-id="02b69-264">**通过文件通信**</span><span class="sxs-lookup"><span data-stu-id="02b69-264">**Communicating via files**</span></span>

<span data-ttu-id="02b69-265">你的大多数数据可能会通过文件在探查器 DLL 和探查器 UI 之间传递。</span><span class="sxs-lookup"><span data-stu-id="02b69-265">Most of your data will likely pass between the Profiler DLL and Profiler UI via files.</span></span> <span data-ttu-id="02b69-266">关键是在 Windows 应用商店应用的上下文中选取探查器 DLL (的文件位置) 并且探查器 UI 具有对的读写访问权限。</span><span class="sxs-lookup"><span data-stu-id="02b69-266">The key is to pick a file location that both your Profiler DLL (in the context of a Windows Store app) and Profiler UI have read and write access to.</span></span> <span data-ttu-id="02b69-267">例如，临时文件夹路径是探查器 DLL 和探查器 UI 可以访问的位置，但其他 Windows 应用商店应用包都不能访问 (因此防护您从其他 Windows 应用商店应用包) 的任何信息。</span><span class="sxs-lookup"><span data-stu-id="02b69-267">For example, the Temporary Folder path is a location that both your Profiler DLL and Profiler UI can access, but no other Windows Store app package can access (thus shielding any information you log from other Windows Store app packages).</span></span>

<span data-ttu-id="02b69-268">探查器 UI 和探查器 DLL 都可以独立确定此路径。</span><span class="sxs-lookup"><span data-stu-id="02b69-268">Both your Profiler UI and Profiler DLL can determine this path independently.</span></span> <span data-ttu-id="02b69-269">探查器 UI （当它循环访问为当前用户安装的所有包时 (查看之前) 的示例代码），获取对类的访问权限 `PackageId` ，通过此代码片段，可以使用类似于此代码段的代码来派生临时文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="02b69-269">Your Profiler UI, when it iterates through all packages installed for the current user (see the sample code earlier), gets access to the `PackageId` class, from which the Temporary Folder path can be derived with code similar to this snippet.</span></span> <span data-ttu-id="02b69-270"> (为 "始终"，将省略错误检查以便于简洁。 ) </span><span class="sxs-lookup"><span data-stu-id="02b69-270">(As always, error checking is omitted for brevity.)</span></span>

```csharp
// C# code for the Profiler UI.
ApplicationData appData =
    ApplicationDataManager.CreateForPackageFamily(
        packageId.FamilyName);

tempDir = appData.TemporaryFolder.Path;
```

<span data-ttu-id="02b69-271">同时，探查器 DLL 可以执行基本相同的操作，尽管它可以 <xref:Windows.Storage.ApplicationData> 通过使用 [ApplicationData](xref:Windows.Storage.ApplicationData.Current%2A) 属性更轻松地访问类。</span><span class="sxs-lookup"><span data-stu-id="02b69-271">Meanwhile, your Profiler DLL can do basically the same thing, though it can more easily get to the <xref:Windows.Storage.ApplicationData> class by using the [ApplicationData.Current](xref:Windows.Storage.ApplicationData.Current%2A) property.</span></span>

<span data-ttu-id="02b69-272">**通过事件通信**</span><span class="sxs-lookup"><span data-stu-id="02b69-272">**Communicating via events**</span></span>

<span data-ttu-id="02b69-273">如果需要探查器 UI 与探查器 DLL 之间的简单信号语义，可以在 Windows 应用商店应用程序和桌面应用程序中使用事件。</span><span class="sxs-lookup"><span data-stu-id="02b69-273">If you want simple signaling semantics between your Profiler UI and Profiler DLL, you can use events inside Windows Store apps as well as desktop apps.</span></span>

<span data-ttu-id="02b69-274">在探查器 DLL 中，只需调用 [CreateEventEx](/windows/desktop/api/synchapi/nf-synchapi-createeventexa) 函数，就可以使用您喜欢的任何名称创建命名事件。</span><span class="sxs-lookup"><span data-stu-id="02b69-274">From your Profiler DLL, you can simply call the [CreateEventEx](/windows/desktop/api/synchapi/nf-synchapi-createeventexa) function to create a named event with any name you like.</span></span> <span data-ttu-id="02b69-275">例如：</span><span class="sxs-lookup"><span data-stu-id="02b69-275">For example:</span></span>

```cpp
// Profiler DLL in Windows Store app (C++).
CreateEventEx(
    NULL,  // Not inherited
    "MyNamedEvent"
    CREATE_EVENT_MANUAL_RESET, /* explicit ResetEvent() required; leave initial state unsignaled */
    EVENT_ALL_ACCESS);
```

<span data-ttu-id="02b69-276">然后，探查器 UI 需要查找 Windows 应用商店应用的命名空间下的命名事件。</span><span class="sxs-lookup"><span data-stu-id="02b69-276">Your Profiler UI then needs to find that named event under the Windows Store app’s namespace.</span></span> <span data-ttu-id="02b69-277">例如，探查器 UI 可以调用 [CreateEventEx](/windows/desktop/api/synchapi/nf-synchapi-createeventexa)，并将事件名称指定为</span><span class="sxs-lookup"><span data-stu-id="02b69-277">For example, your Profiler UI could call [CreateEventEx](/windows/desktop/api/synchapi/nf-synchapi-createeventexa), specifying the event name as</span></span>

`AppContainerNamedObjects\<acSid>\MyNamedEvent`

<span data-ttu-id="02b69-278">`<acSid>` 是 Windows 应用商店应用的 AppContainer SID。</span><span class="sxs-lookup"><span data-stu-id="02b69-278">`<acSid>` is the Windows Store app’s AppContainer SID.</span></span> <span data-ttu-id="02b69-279">本主题前面部分介绍了如何循环访问为当前用户安装的包。</span><span class="sxs-lookup"><span data-stu-id="02b69-279">An earlier section of this topic showed how to iterate over the packages installed for the current user.</span></span> <span data-ttu-id="02b69-280">通过该示例代码，你可以获取 packageId。</span><span class="sxs-lookup"><span data-stu-id="02b69-280">From that sample code, you can obtain the packageId.</span></span> <span data-ttu-id="02b69-281">然后，可以从 packageId 中获取如下 `<acSid>` 代码：</span><span class="sxs-lookup"><span data-stu-id="02b69-281">And from the packageId, you can obtain the `<acSid>` with code similar to the following:</span></span>

```csharp
IntPtr acPSID;
DeriveAppContainerSidFromAppContainerName(packageId.FamilyName, out acPSID);

string acSid;
ConvertSidToStringSid(acPSID, out acSid);

string acDir;
GetAppContainerFolderPath(acSid, out acDir);
```

### <a name="no-shutdown-notifications"></a><span data-ttu-id="02b69-282">无关闭通知</span><span class="sxs-lookup"><span data-stu-id="02b69-282">No shutdown notifications</span></span>

<span data-ttu-id="02b69-283">在 Windows 应用商店应用程序中运行时，探查器 DLL 不应依赖于 [ICorProfilerCallback：： Shutdown](icorprofilercallback-shutdown-method.md) ，甚至是) 使用 [DllMain](/windows/desktop/Dlls/dllmain) (`DLL_PROCESS_DETACH` 来通知探查器 dll Windows 应用商店应用程序正在退出。</span><span class="sxs-lookup"><span data-stu-id="02b69-283">When running inside a Windows Store app, your Profiler DLL should not rely on either [ICorProfilerCallback::Shutdown](icorprofilercallback-shutdown-method.md) or even [DllMain](/windows/desktop/Dlls/dllmain) (with `DLL_PROCESS_DETACH`) being called to notify your Profiler DLL that the Windows Store app is exiting.</span></span> <span data-ttu-id="02b69-284">事实上，您应该永远不会调用它们。</span><span class="sxs-lookup"><span data-stu-id="02b69-284">In fact, you should expect they will never be called.</span></span> <span data-ttu-id="02b69-285">从历史上看，许多探查器 Dll 已使用这些通知作为将缓存刷新到磁盘、关闭文件、将通知发送回探查器 UI 等的便利位置。但现在，需要以略有不同的方式组织探查器 DLL。</span><span class="sxs-lookup"><span data-stu-id="02b69-285">Historically, many Profiler DLLs have used those notifications as convenient places to flush caches to disk, close files, send notifications back to the Profiler UI, etc. But now your Profiler DLL needs to be organized a little differently.</span></span>

<span data-ttu-id="02b69-286">探查器 DLL 应在记录信息时进行记录。</span><span class="sxs-lookup"><span data-stu-id="02b69-286">Your Profiler DLL should be logging information as it goes.</span></span> <span data-ttu-id="02b69-287">出于性能方面的考虑，可能需要在内存中批处理信息，并将其刷新到磁盘，因为批大小超过了某个阈值。</span><span class="sxs-lookup"><span data-stu-id="02b69-287">For performance reasons, you may want to batch information in memory and flush it to disk as the batch grows in size past some threshold.</span></span> <span data-ttu-id="02b69-288">但假定尚未刷新到磁盘的任何信息可能会丢失。</span><span class="sxs-lookup"><span data-stu-id="02b69-288">But assume that any information not yet flushed to disk can be lost.</span></span> <span data-ttu-id="02b69-289">这意味着你需要明智地选择阈值，并且需要强化探查器 UI 才能处理探查器 DLL 编写的不完整信息。</span><span class="sxs-lookup"><span data-stu-id="02b69-289">This means you’ll want to pick your threshold wisely, and that your Profiler UI needs to be hardened to deal with incomplete information written by the Profiler DLL.</span></span>

## <a name="windows-runtime-metadata-files"></a><span data-ttu-id="02b69-290">Windows 运行时元数据文件</span><span class="sxs-lookup"><span data-stu-id="02b69-290">Windows Runtime metadata files</span></span>

<span data-ttu-id="02b69-291">它不在本文档的讨论范围内，可以详细了解 WinMD) 文件 (Windows 运行时元数据。</span><span class="sxs-lookup"><span data-stu-id="02b69-291">It is outside the scope of this document to go into detail on what Windows Runtime metadata (WinMD) files are.</span></span> <span data-ttu-id="02b69-292">此部分仅限于在探查器 DLL 正在分析的 Windows 应用商店应用程序加载 WinMD 文件时，CLR 分析 API 如何做出反应。</span><span class="sxs-lookup"><span data-stu-id="02b69-292">This section is limited to how the CLR Profiling API reacts when WinMD files are loaded by the Windows Store app your Profiler DLL is analyzing.</span></span>

### <a name="managed-and-non-managed-winmds"></a><span data-ttu-id="02b69-293">托管和非托管 Winmd</span><span class="sxs-lookup"><span data-stu-id="02b69-293">Managed and non-managed WinMDs</span></span>

<span data-ttu-id="02b69-294">如果开发人员使用 Visual Studio 来创建新的 Windows 运行时组件项目，则该项目的生成将生成一个 WinMD 文件，该文件描述由开发人员创作 ) 类、接口等的类型说明中的元数据 (。</span><span class="sxs-lookup"><span data-stu-id="02b69-294">If a developer uses Visual Studio to create a new Windows Runtime Component project, a build of that project produces a WinMD file that describes the metadata (the type descriptions of classes, interfaces, etc.) authored by the developer.</span></span> <span data-ttu-id="02b69-295">如果此项目是使用 c # 或 Visual Basic 编写的托管语言项目，同一 WinMD 文件也包含这些类型的实现 (意味着它包含从开发人员的源代码) 编译的所有 IL。</span><span class="sxs-lookup"><span data-stu-id="02b69-295">If this project is a managed language project written in C# or Visual Basic, that same WinMD file also contains the implementation of those types (meaning that it contains all the IL compiled from the developer’s source code).</span></span> <span data-ttu-id="02b69-296">此类文件称为托管 WinMD 文件。</span><span class="sxs-lookup"><span data-stu-id="02b69-296">Such files are known as managed WinMD files.</span></span> <span data-ttu-id="02b69-297">它们非常有趣，因为它们既包含 Windows 运行时元数据，也包含基础实现。</span><span class="sxs-lookup"><span data-stu-id="02b69-297">They're interesting in that they contain both Windows Runtime metadata and the underlying implementation.</span></span>

<span data-ttu-id="02b69-298">与此相反，如果开发人员创建一个用于 c + + 的 Windows 运行时组件项目，则该项目的生成将生成一个仅包含元数据的 WinMD 文件，并且该实现将编译为单独的本机 DLL。</span><span class="sxs-lookup"><span data-stu-id="02b69-298">In contrast, if a developer creates a Windows Runtime Component project for C++, a build of that project produces a WinMD file that contains only metadata, and the implementation is compiled into a separate native DLL.</span></span> <span data-ttu-id="02b69-299">同样，在 Windows SDK 中附带的 WinMD 文件仅包含元数据，并将实现编译为 Windows 附带的单独本机 Dll。</span><span class="sxs-lookup"><span data-stu-id="02b69-299">Similarly, the WinMD files that ship in the Windows SDK contain only metadata, with the implementation compiled into separate native DLLs that ship as part of Windows.</span></span>

<span data-ttu-id="02b69-300">下面的信息适用于托管 Winmd，其中包含元数据和实现，以及非托管 Winmd （仅包含元数据）。</span><span class="sxs-lookup"><span data-stu-id="02b69-300">The information below applies to both managed WinMDs, which contain metadata and implementation, and to non-managed WinMDs, which contain only metadata.</span></span>

### <a name="winmd-files-look-like-clr-modules"></a><span data-ttu-id="02b69-301">WinMD 文件类似于 CLR 模块</span><span class="sxs-lookup"><span data-stu-id="02b69-301">WinMD files look like CLR modules</span></span>

<span data-ttu-id="02b69-302">与 CLR 相关，所有 WinMD 文件都是模块。</span><span class="sxs-lookup"><span data-stu-id="02b69-302">As far as the CLR is concerned, all WinMD files are modules.</span></span> <span data-ttu-id="02b69-303">因此，CLR 分析 API 会告诉探查器 DLL 何时加载 WinMD 文件以及它们的 Moduleid，其方式与其他托管模块相同。</span><span class="sxs-lookup"><span data-stu-id="02b69-303">The CLR Profiling API therefore tells your Profiler DLL when WinMD files load and what their ModuleIDs are, in the same way as for other managed modules.</span></span>

<span data-ttu-id="02b69-304">探查器 DLL 可以通过调用 [ICorProfilerInfo3：： GetModuleInfo2](icorprofilerinfo3-getmoduleinfo2-method.md) 方法并检查 `pdwModuleFlags` [COR_PRF_MODULE_WINDOWS_RUNTIME](cor-prf-module-flags-enumeration.md) 标志的输出参数来区分来自其他模块的 WinMD 文件。</span><span class="sxs-lookup"><span data-stu-id="02b69-304">Your Profiler DLL can distinguish WinMD files from other modules by calling the [ICorProfilerInfo3::GetModuleInfo2](icorprofilerinfo3-getmoduleinfo2-method.md) method and inspecting the `pdwModuleFlags` output parameter for the [COR_PRF_MODULE_WINDOWS_RUNTIME](cor-prf-module-flags-enumeration.md) flag.</span></span> <span data-ttu-id="02b69-305"> (当且仅当 ModuleID 表示 WinMD 时设置。 ) </span><span class="sxs-lookup"><span data-stu-id="02b69-305">(It’s set if and only if the ModuleID represents a WinMD.)</span></span>

### <a name="reading-metadata-from-winmds"></a><span data-ttu-id="02b69-306">从 Winmd 读取元数据</span><span class="sxs-lookup"><span data-stu-id="02b69-306">Reading metadata from WinMDs</span></span>

<span data-ttu-id="02b69-307">WinMD 文件（如常规模块）包含可通过 [元数据 api](../metadata/index.md)读取的元数据。</span><span class="sxs-lookup"><span data-stu-id="02b69-307">WinMD files, like regular modules, contain metadata that can be read via the [Metadata APIs](../metadata/index.md).</span></span> <span data-ttu-id="02b69-308">但是，在读取 WinMD 文件时，CLR 将 Windows 运行时类型映射到 .NET Framework 类型，以便在托管代码中编写和使用 WinMD 文件的开发人员具有更自然的编程体验。</span><span class="sxs-lookup"><span data-stu-id="02b69-308">However, the CLR maps Windows Runtime types to .NET Framework types when it reads WinMD files so that developers who program in managed code and consume the WinMD file can have a more natural programming experience.</span></span> <span data-ttu-id="02b69-309">有关这些映射的一些示例，请参阅 [Windows 应用商店应用和 Windows 运行时 .NET Framework 支持](../../cross-platform/support-for-windows-store-apps-and-windows-runtime.md)。</span><span class="sxs-lookup"><span data-stu-id="02b69-309">For some examples of these mappings, see [.NET Framework Support for Windows Store Apps and Windows Runtime](../../cross-platform/support-for-windows-store-apps-and-windows-runtime.md).</span></span>

<span data-ttu-id="02b69-310">在使用元数据 Api 时，探查器会获得哪个视图：原始 Windows 运行时视图或映射的 .NET Framework 视图？</span><span class="sxs-lookup"><span data-stu-id="02b69-310">So which view will your profiler get when it uses the metadata APIs: the raw Windows Runtime view, or the mapped .NET Framework view?</span></span>  <span data-ttu-id="02b69-311">答案是：由您负责。</span><span class="sxs-lookup"><span data-stu-id="02b69-311">The answer: it’s up to you.</span></span>

<span data-ttu-id="02b69-312">调用 WinMD 上的 [ICorProfilerInfo：： GetModuleMetaData](icorprofilerinfo-getmodulemetadata-method.md) 方法以获取元数据接口（如 [IMetaDataImport](../metadata/imetadataimport-interface.md)）时，可以选择在参数中设置 [ofNoTransform](../metadata/coropenflags-enumeration.md) `dwOpenFlags` 以关闭此映射。</span><span class="sxs-lookup"><span data-stu-id="02b69-312">When you call the [ICorProfilerInfo::GetModuleMetaData](icorprofilerinfo-getmodulemetadata-method.md) method on a WinMD to obtain a metadata interface, such as [IMetaDataImport](../metadata/imetadataimport-interface.md),  you can choose to set [ofNoTransform](../metadata/coropenflags-enumeration.md) in the `dwOpenFlags` parameter to turn off this mapping.</span></span> <span data-ttu-id="02b69-313">否则，默认情况下将启用映射。</span><span class="sxs-lookup"><span data-stu-id="02b69-313">Otherwise, by default, the mapping will be enabled.</span></span> <span data-ttu-id="02b69-314">通常，探查器将保持启用映射，以便探查器 DLL 从 WinMD 元数据中获取的字符串 (例如，) 类型的名称将对探查器用户非常熟悉和自然。</span><span class="sxs-lookup"><span data-stu-id="02b69-314">Typically, a profiler will keep the mapping enabled, so that the strings that the Profiler DLL obtains from the WinMD metadata (for example, names of types) will look familiar and natural to the profiler user.</span></span>

### <a name="modifying-metadata-from-winmds"></a><span data-ttu-id="02b69-315">修改 Winmd 中的元数据</span><span class="sxs-lookup"><span data-stu-id="02b69-315">Modifying metadata from WinMDs</span></span>

<span data-ttu-id="02b69-316">不支持修改 Winmd 中的元数据。</span><span class="sxs-lookup"><span data-stu-id="02b69-316">Modifying metadata in WinMDs is not supported.</span></span> <span data-ttu-id="02b69-317">如果为 WinMD 文件调用 [ICorProfilerInfo：： GetModuleMetaData](icorprofilerinfo-getmodulemetadata-method.md) 方法并在参数中指定 [ofWrite](../metadata/coropenflags-enumeration.md) `dwOpenFlags` ，或者要求提供可写的元数据接口（如 [IMetaDataEmit](../metadata/imetadataemit-interface.md)），则 [GetModuleMetaData](icorprofilerinfo-getmodulemetadata-method.md) 将会失败。</span><span class="sxs-lookup"><span data-stu-id="02b69-317">If you call the [ICorProfilerInfo::GetModuleMetaData](icorprofilerinfo-getmodulemetadata-method.md) method for a WinMD file and specify [ofWrite](../metadata/coropenflags-enumeration.md) in the `dwOpenFlags` parameter or ask for a writeable metadata interface such as [IMetaDataEmit](../metadata/imetadataemit-interface.md), [GetModuleMetaData](icorprofilerinfo-getmodulemetadata-method.md) will fail.</span></span> <span data-ttu-id="02b69-318">这对于 IL 重写探查器尤其重要，后者需要修改元数据以支持其检测 (例如，将引用或新方法添加) 。</span><span class="sxs-lookup"><span data-stu-id="02b69-318">This is of particular importance to IL-rewriting profilers, which need to modify metadata to support their instrumentation (for example, to add AssemblyRefs or new methods).</span></span> <span data-ttu-id="02b69-319">因此，你应该按照上一部分中所述来检查 [COR_PRF_MODULE_WINDOWS_RUNTIME](cor-prf-module-flags-enumeration.md) 第一个 () 并避免在此类模块上请求可写的元数据接口。</span><span class="sxs-lookup"><span data-stu-id="02b69-319">So you should check for [COR_PRF_MODULE_WINDOWS_RUNTIME](cor-prf-module-flags-enumeration.md) first (as discussed in the previous section) and refrain from asking for writeable metadata interfaces on such modules.</span></span>

### <a name="resolving-assembly-references-with-winmds"></a><span data-ttu-id="02b69-320">用 Winmd 解析程序集引用</span><span class="sxs-lookup"><span data-stu-id="02b69-320">Resolving assembly references with WinMDs</span></span>

<span data-ttu-id="02b69-321">许多探查器需要手动解析元数据引用，以帮助进行检测或类型检查。</span><span class="sxs-lookup"><span data-stu-id="02b69-321">Many profilers need to resolve metadata references manually to aid with instrumentation or type inspection.</span></span> <span data-ttu-id="02b69-322">此类探查器需要了解 CLR 如何解析指向 Winmd 的程序集引用，因为这些引用的解析方式与标准程序集引用完全不同。</span><span class="sxs-lookup"><span data-stu-id="02b69-322">Such profilers need to be aware of how the CLR resolves assembly references that point to WinMDs, because those references are resolved in a completely different way than standard assembly references.</span></span>

## <a name="memory-profilers"></a><span data-ttu-id="02b69-323">内存探查器</span><span class="sxs-lookup"><span data-stu-id="02b69-323">Memory profilers</span></span>

<span data-ttu-id="02b69-324">在 Windows 应用商店应用和桌面应用中，垃圾回收器和托管堆根本不是不同的。</span><span class="sxs-lookup"><span data-stu-id="02b69-324">The garbage collector and managed heap are not fundamentally different in a Windows Store app and a desktop app.</span></span> <span data-ttu-id="02b69-325">但是，探查器作者需要注意一些细微的差异。</span><span class="sxs-lookup"><span data-stu-id="02b69-325">However, there are some subtle differences that profiler authors need to be aware of.</span></span>

### <a name="forcegc-creates-a-managed-thread"></a><span data-ttu-id="02b69-326">ForceGC 创建托管线程</span><span class="sxs-lookup"><span data-stu-id="02b69-326">ForceGC creates a managed thread</span></span>

<span data-ttu-id="02b69-327">进行内存分析时，探查器 DLL 通常会创建一个单独的线程来调用 [ForceGC 方法](icorprofilerinfo-forcegc-method.md) 方法。</span><span class="sxs-lookup"><span data-stu-id="02b69-327">When doing memory profiling, your Profiler DLL typically creates a separate thread from which to call the [ForceGC Method](icorprofilerinfo-forcegc-method.md) method.</span></span> <span data-ttu-id="02b69-328">这不是什么新内容。</span><span class="sxs-lookup"><span data-stu-id="02b69-328">This is nothing new.</span></span> <span data-ttu-id="02b69-329">但可能会令人吃惊的是，在 Windows 应用商店应用程序中执行垃圾回收的操作可能会将线程转换为托管线程 (例如，将为该线程) 创建分析 API ThreadID。</span><span class="sxs-lookup"><span data-stu-id="02b69-329">But what might be surprising is that the act of doing a garbage collection inside a Windows Store app may transform your thread into a managed thread (for example, a Profiling API ThreadID will be created for that thread).</span></span>

<span data-ttu-id="02b69-330">若要理解这一点，请务必了解 CLR 分析 API 定义的同步和异步调用之间的差异。</span><span class="sxs-lookup"><span data-stu-id="02b69-330">To understand the consequences of this, it’s important to understand the differences between synchronous and asynchronous calls as defined by the CLR Profiling API.</span></span> <span data-ttu-id="02b69-331">请注意，这与 Windows 应用商店应用程序中异步调用的概念非常不同。</span><span class="sxs-lookup"><span data-stu-id="02b69-331">Note that this is very different from the concept of asynchronous calls in Windows Store apps.</span></span> <span data-ttu-id="02b69-332">有关详细信息，请参阅博客文章 [CORPROF_E_UNSUPPORTED_CALL_SEQUENCE 原因](/archive/blogs/davbr/why-we-have-corprof_e_unsupported_call_sequence) 。</span><span class="sxs-lookup"><span data-stu-id="02b69-332">See the blog post [Why we have CORPROF_E_UNSUPPORTED_CALL_SEQUENCE](/archive/blogs/davbr/why-we-have-corprof_e_unsupported_call_sequence) for more information.</span></span>

<span data-ttu-id="02b69-333">相关的一点是，在探查器创建的线程上进行的调用始终被视为同步调用，即使这些调用是从某个探查器 DLL 的 [ICorProfilerCallback](icorprofilercallback-interface.md) 方法的实现之外进行的。</span><span class="sxs-lookup"><span data-stu-id="02b69-333">The relevant point is that calls made on threads created by your profiler are always considered synchronous, even if those calls are made from outside an implementation of one of your Profiler DLL’s [ICorProfilerCallback](icorprofilercallback-interface.md) methods.</span></span> <span data-ttu-id="02b69-334">至少，这种情况下也是如此。</span><span class="sxs-lookup"><span data-stu-id="02b69-334">At least, that used to be the case.</span></span> <span data-ttu-id="02b69-335">由于调用了 [ForceGC 方法](icorprofilerinfo-forcegc-method.md)，CLR 已将探查器的线程转换为托管线程，该线程不再被视为探查器的线程。</span><span class="sxs-lookup"><span data-stu-id="02b69-335">Now that the CLR has turned your profiler’s thread into a managed thread because of your call to [ForceGC Method](icorprofilerinfo-forcegc-method.md), that thread is no longer considered your profiler’s thread.</span></span> <span data-ttu-id="02b69-336">因此，CLR 强制实施更严格的定义，该定义对该线程来说是同步的（也就是说，调用必须从探查器 DLL 的 [ICorProfilerCallback](icorprofilercallback-interface.md) 方法之一开始，才能作为同步。</span><span class="sxs-lookup"><span data-stu-id="02b69-336">As such, the CLR enforces a more stringent definition of what qualifies as synchronous for that thread—namely that a call must originate from inside one of your Profiler DLL’s [ICorProfilerCallback](icorprofilercallback-interface.md) methods to qualify as synchronous.</span></span>

<span data-ttu-id="02b69-337">这在实践中是什么意思？</span><span class="sxs-lookup"><span data-stu-id="02b69-337">What does this mean in practice?</span></span> <span data-ttu-id="02b69-338">大多数 [ICorProfilerInfo](icorprofilerinfo-interface.md) 方法只是以同步方式调用，并且会立即失败。</span><span class="sxs-lookup"><span data-stu-id="02b69-338">Most [ICorProfilerInfo](icorprofilerinfo-interface.md) methods are only safe to be called synchronously, and will immediately fail otherwise.</span></span> <span data-ttu-id="02b69-339">因此，如果探查器 DLL 对通常在探查器创建的线程上执行的其他调用重复使用 [ForceGC 方法](icorprofilerinfo-forcegc-method.md) 线程 (例如， [RequestProfilerDetach](icorprofilerinfo3-requestprofilerdetach-method.md)、 [RequestReJIT](icorprofilerinfo4-requestrejit-method.md)或 [RequestRevert](icorprofilerinfo4-requestrevert-method.md)) ，则会遇到问题。</span><span class="sxs-lookup"><span data-stu-id="02b69-339">So if your Profiler DLL reuses your [ForceGC Method](icorprofilerinfo-forcegc-method.md) thread for other calls typically made on profiler-created threads (for example, to [RequestProfilerDetach](icorprofilerinfo3-requestprofilerdetach-method.md), [RequestReJIT](icorprofilerinfo4-requestrejit-method.md), or [RequestRevert](icorprofilerinfo4-requestrevert-method.md)), you’re going to have trouble.</span></span> <span data-ttu-id="02b69-340">在从托管线程调用时，甚至异步安全函数（如 [DoStackSnapshot](icorprofilerinfo2-dostacksnapshot-method.md) ）都有特殊的规则。</span><span class="sxs-lookup"><span data-stu-id="02b69-340">Even an asynchronous-safe function such as [DoStackSnapshot](icorprofilerinfo2-dostacksnapshot-method.md) has special rules when called from managed threads.</span></span> <span data-ttu-id="02b69-341"> (参见博客文章 [探查器堆栈遍历：基础知识和](/archive/blogs/davbr/profiler-stack-walking-basics-and-beyond) 更高版本，了解详细信息。 ) </span><span class="sxs-lookup"><span data-stu-id="02b69-341">(See the blog post [Profiler stack walking: Basics and beyond](/archive/blogs/davbr/profiler-stack-walking-basics-and-beyond) for more information.)</span></span>

<span data-ttu-id="02b69-342">因此，建议使用探查器 DLL 创建的任何线程来调用 [ForceGC 方法](icorprofilerinfo-forcegc-method.md) ， *只* 应使用它来触发 GC，然后响应 gc 回调。</span><span class="sxs-lookup"><span data-stu-id="02b69-342">Therefore, we recommend that any thread your Profiler DLL creates to call [ForceGC Method](icorprofilerinfo-forcegc-method.md) should be used *only* for the purpose of triggering GCs and then responding to the GC callbacks.</span></span> <span data-ttu-id="02b69-343">它不应调入分析 API 来执行其他任务，如堆栈采样或分离。</span><span class="sxs-lookup"><span data-stu-id="02b69-343">It should not call into the Profiling API to perform other tasks like stack sampling or detaching.</span></span>

### <a name="conditionalweaktablereferences"></a><span data-ttu-id="02b69-344">ConditionalWeakTableReferences</span><span class="sxs-lookup"><span data-stu-id="02b69-344">ConditionalWeakTableReferences</span></span>

<span data-ttu-id="02b69-345">从 .NET Framework 4.5 开始，有一个新的 GC 回调 [ConditionalWeakTableElementReferences](icorprofilercallback5-conditionalweaktableelementreferences-method.md)，它为探查器提供有关 *依赖句柄* 的更完整信息。</span><span class="sxs-lookup"><span data-stu-id="02b69-345">Starting with the .NET Framework 4.5, there is a new GC callback, [ConditionalWeakTableElementReferences](icorprofilercallback5-conditionalweaktableelementreferences-method.md), which gives the profiler more complete information about *dependent handles*.</span></span> <span data-ttu-id="02b69-346">出于 GC 生存期管理的目的，这些处理会有效地将从源对象的引用添加到目标对象。</span><span class="sxs-lookup"><span data-stu-id="02b69-346">These handles effectively add a reference from a source object to a target object for the purpose of GC lifetime management.</span></span> <span data-ttu-id="02b69-347">从属句柄并不新，并且在托管代码中编程的开发人员可以使用类创建自己的依赖句柄， <xref:System.Runtime.CompilerServices.ConditionalWeakTable%602?displayProperty=nameWithType> 即使在 Windows 8 和 .NET Framework 4.5 之前也是如此。</span><span class="sxs-lookup"><span data-stu-id="02b69-347">Dependent handles are nothing new, and developers who program in managed code have been able to create their own dependent handles by using the <xref:System.Runtime.CompilerServices.ConditionalWeakTable%602?displayProperty=nameWithType> class even before Windows 8 and the .NET Framework 4.5.</span></span>

<span data-ttu-id="02b69-348">但是，托管的 XAML Windows 应用商店应用现在会大量使用依赖句柄。</span><span class="sxs-lookup"><span data-stu-id="02b69-348">However, managed XAML Windows Store apps now make heavy use of dependent handles.</span></span> <span data-ttu-id="02b69-349">具体而言，CLR 使用它们来帮助管理托管对象和非托管 Windows 运行时对象之间的引用周期。</span><span class="sxs-lookup"><span data-stu-id="02b69-349">In particular, the CLR uses them to aid with managing reference cycles between managed objects and unmanaged Windows Runtime objects.</span></span> <span data-ttu-id="02b69-350">这意味着，与以往相比，要通知这些从属句柄的内存探查器比以往更重要，这样，就可以与堆图中的其余边缘一起可视化。</span><span class="sxs-lookup"><span data-stu-id="02b69-350">This means that it’s more important now than ever for memory profilers to be informed of these dependent handles so that they can be visualized along with the rest of the edges in the heap graph.</span></span> <span data-ttu-id="02b69-351">探查器 DLL 应将 [RootReferences2](icorprofilercallback2-rootreferences2-method.md)、 [ObjectReferences](icorprofilercallback-objectreferences-method.md)和 [ConditionalWeakTableElementReferences](icorprofilercallback5-conditionalweaktableelementreferences-method.md) 一起使用，以形成堆关系图的完整视图。</span><span class="sxs-lookup"><span data-stu-id="02b69-351">Your Profiler DLL should use [RootReferences2](icorprofilercallback2-rootreferences2-method.md), [ObjectReferences](icorprofilercallback-objectreferences-method.md), and [ConditionalWeakTableElementReferences](icorprofilercallback5-conditionalweaktableelementreferences-method.md) together to form a complete view of the heap graph.</span></span>

## <a name="conclusion"></a><span data-ttu-id="02b69-352">结论</span><span class="sxs-lookup"><span data-stu-id="02b69-352">Conclusion</span></span>

<span data-ttu-id="02b69-353">可以使用 CLR 分析 API 来分析 Windows 应用商店应用内运行的托管代码。</span><span class="sxs-lookup"><span data-stu-id="02b69-353">It is possible to use the CLR Profiling API to analyze managed code running inside Windows Store apps.</span></span> <span data-ttu-id="02b69-354">事实上，你可以获取正在开发的现有探查器，并进行一些具体的更改，使其面向 Windows 应用商店应用。</span><span class="sxs-lookup"><span data-stu-id="02b69-354">In fact, you can take an existing profiler that you’re developing and make some specific changes so that it can target Windows Store apps.</span></span> <span data-ttu-id="02b69-355">探查器 UI 应使用新的 Api 在调试模式下激活 Windows 应用商店应用。</span><span class="sxs-lookup"><span data-stu-id="02b69-355">Your Profiler UI should use the new APIs for activating the Windows Store app in debugging mode.</span></span> <span data-ttu-id="02b69-356">请确保探查器 DLL 仅使用适用于 Windows 应用商店应用的 Api。</span><span class="sxs-lookup"><span data-stu-id="02b69-356">Make sure that your Profiler DLL consumes only those APIs applicable for Windows Store apps.</span></span> <span data-ttu-id="02b69-357">探查器 DLL 和探查器 UI 之间的通信机制应该在编写时考虑到 Windows 应用商店应用程序 API 限制，并了解 Windows 应用商店应用程序的受限权限。</span><span class="sxs-lookup"><span data-stu-id="02b69-357">The communication mechanism between your Profiler DLL and Profiler UI should be written with the Windows Store app API restrictions in mind and with awareness of the restricted permissions in place for Windows Store apps.</span></span> <span data-ttu-id="02b69-358">探查器 DLL 应知道 CLR 如何处理 Winmd，以及垃圾回收器的行为与托管线程的行为是不同的。</span><span class="sxs-lookup"><span data-stu-id="02b69-358">Your Profiler DLL should be aware of how the CLR treats WinMDs, and how the Garbage Collector’s behavior is different with respect to managed threads.</span></span>

## <a name="resources"></a><span data-ttu-id="02b69-359">资源</span><span class="sxs-lookup"><span data-stu-id="02b69-359">Resources</span></span>

<span data-ttu-id="02b69-360">**公共语言运行时**</span><span class="sxs-lookup"><span data-stu-id="02b69-360">**The Common Language Runtime**</span></span>

- [<span data-ttu-id="02b69-361">分析 (非托管 API 参考) </span><span class="sxs-lookup"><span data-stu-id="02b69-361">Profiling (Unmanaged API Reference)</span></span>](index.md)

- [<span data-ttu-id="02b69-362"> (非托管 API 参考的元数据) </span><span class="sxs-lookup"><span data-stu-id="02b69-362">Metadata (Unmanaged API Reference)</span></span>](../metadata/index.md)

<span data-ttu-id="02b69-363">**CLR 与 Windows 运行时的交互**</span><span class="sxs-lookup"><span data-stu-id="02b69-363">**The CLR's interaction with the Windows Runtime**</span></span>

- [<span data-ttu-id="02b69-364">.NET Framework 对 Windows 应用商店应用和 Windows 运行时的支持情况</span><span class="sxs-lookup"><span data-stu-id="02b69-364">.NET Framework Support for Windows Store Apps and Windows Runtime</span></span>](../../cross-platform/support-for-windows-store-apps-and-windows-runtime.md)

<span data-ttu-id="02b69-365">**Windows 应用商店应用程序**</span><span class="sxs-lookup"><span data-stu-id="02b69-365">**Windows Store apps**</span></span>

- <span data-ttu-id="02b69-366">[Windows 运行时应用 (的文件访问和权限](/previous-versions/windows/apps/hh967755(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="02b69-366">[File access and permissions (Windows Runtime apps](/previous-versions/windows/apps/hh967755(v=win.10))</span></span>

- <span data-ttu-id="02b69-367">[获取开发人员许可证](/previous-versions/windows/apps/hh974578(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="02b69-367">[Get a developer license](/previous-versions/windows/apps/hh974578(v=win.10))</span></span>

- [<span data-ttu-id="02b69-368">IPackageDebugSettings 接口</span><span class="sxs-lookup"><span data-stu-id="02b69-368">IPackageDebugSettings Interface</span></span>](/windows/desktop/api/shobjidl_core/nn-shobjidl_core-ipackagedebugsettings)
