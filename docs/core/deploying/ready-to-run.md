---
title: ReadyToRun 部署概述
description: 了解什么是 ReadyToRun 部署，以及通过 .NET 5 和 .NET Core 3.0 及更高版本发布应用时为什么应考虑使用它。
author: davidwr
ms.author: davidwr
ms.date: 09/21/2020
ms.openlocfilehash: cd8eaebd05d79b11e90e255e702a52220fffda76
ms.sourcegitcommit: ffd4d5e824db6c5f0c3521c0e802fd9e8f0edcbe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2020
ms.locfileid: "93342626"
---
# <a name="readytorun-compilation"></a><span data-ttu-id="121be-103">ReadyToRun 编译</span><span class="sxs-lookup"><span data-stu-id="121be-103">ReadyToRun Compilation</span></span>

<span data-ttu-id="121be-104">可以通过将应用程序集编译为 ReadyToRun (R2R) 格式来改进 .NET Core 应用程序的启动时间和延迟。</span><span class="sxs-lookup"><span data-stu-id="121be-104">.NET application startup time and latency can be improved by compiling your application assemblies as ReadyToRun (R2R) format.</span></span> <span data-ttu-id="121be-105">R2R 是一种预先 (AOT) 编译形式。</span><span class="sxs-lookup"><span data-stu-id="121be-105">R2R is a form of ahead-of-time (AOT) compilation.</span></span>

<span data-ttu-id="121be-106">R2R 二进制文件通过减少应用程序加载时实时 (JIT) 编译器需要执行的工作量来改进启动性能。</span><span class="sxs-lookup"><span data-stu-id="121be-106">R2R binaries improve startup performance by reducing the amount of work the just-in-time (JIT) compiler needs to do as your application loads.</span></span> <span data-ttu-id="121be-107">二进制文件包含与 JIT 将生成的内容类似的本机代码。</span><span class="sxs-lookup"><span data-stu-id="121be-107">The binaries contain similar native code compared to what the JIT would produce.</span></span> <span data-ttu-id="121be-108">但是，R2R 二进制文件更大，因为它们包含中间语言 (IL) 代码（某些情况下仍需要此代码）和相同代码的本机版本。</span><span class="sxs-lookup"><span data-stu-id="121be-108">However, R2R binaries are larger because they contain both intermediate language (IL) code, which is still needed for some scenarios, and the native version of the same code.</span></span> <span data-ttu-id="121be-109">仅当发布面向特定运行时环境 (RID)（如 Linux x64 或 Windows x64）的应用时 R2R 才可用。</span><span class="sxs-lookup"><span data-stu-id="121be-109">R2R is only available when you publish an app that targets specific runtime environments (RID) such as Linux x64 or Windows x64.</span></span>

<span data-ttu-id="121be-110">若要将项目编译为 ReadyToRun，必须在将 PublishReadyToRun 属性设置为 true 时发布应用程序。</span><span class="sxs-lookup"><span data-stu-id="121be-110">To compile your project as ReadyToRun, the application must be published with the PublishReadyToRun property set to true.</span></span>

<span data-ttu-id="121be-111">可以通过两种方式将应用发布为 ReadyToRun：</span><span class="sxs-lookup"><span data-stu-id="121be-111">There are two ways to publish your app as ReadyToRun:</span></span>

01. <span data-ttu-id="121be-112">向 dotnet publish 命令直接指定 PublishReadyToRun 标志。</span><span class="sxs-lookup"><span data-stu-id="121be-112">Specify the PublishReadyToRun flag directly to the dotnet publish command.</span></span> <span data-ttu-id="121be-113">有关详细信息，请参阅 [dotnet publish](../tools/dotnet-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="121be-113">See [dotnet publish](../tools/dotnet-publish.md) for details.</span></span>

    ```dotnetcli
    dotnet publish -c Release -r win-x64 -p:PublishReadyToRun=true
    ```

02. <span data-ttu-id="121be-114">在项目中指定属性</span><span class="sxs-lookup"><span data-stu-id="121be-114">Specify the property in the project</span></span>

    - <span data-ttu-id="121be-115">向项目中添加 `<PublishReadyToRun>` 设置。</span><span class="sxs-lookup"><span data-stu-id="121be-115">Add the `<PublishReadyToRun>` setting to your project.</span></span>

    ```xml
    <PropertyGroup>
      <PublishReadyToRun>true</PublishReadyToRun>
    </PropertyGroup>
    ```

    - <span data-ttu-id="121be-116">在不使用任何特殊参数的情况下发布应用程序。</span><span class="sxs-lookup"><span data-stu-id="121be-116">Publish the application without any special parameters.</span></span>

    ```dotnetcli
    dotnet publish -c Release -r win-x64
    ```

## <a name="impact-of-using-the-readytorun-feature"></a><span data-ttu-id="121be-117">使用 ReadyToRun 功能的影响</span><span class="sxs-lookup"><span data-stu-id="121be-117">Impact of using the ReadyToRun feature</span></span>

<span data-ttu-id="121be-118">预先编译会对应用程序性能产生复杂的性能影响，这种影响可能很难预测。</span><span class="sxs-lookup"><span data-stu-id="121be-118">Ahead-of-time compilation has complex performance impact on application performance, which may be difficult to predict.</span></span> <span data-ttu-id="121be-119">通常情况下，程序集的大小将增长到两到三倍。</span><span class="sxs-lookup"><span data-stu-id="121be-119">In general, the size of an assembly will grow to between two to three times larger.</span></span> <span data-ttu-id="121be-120">这种文件物理大小的增加可能会降低从磁盘加载程序集的性能，并增加进程的工作集。</span><span class="sxs-lookup"><span data-stu-id="121be-120">This increase in the physical size of the file may reduce the performance of loading the assembly from disk, and increase working set of the process.</span></span> <span data-ttu-id="121be-121">但相对地，在运行时编译的方法数通常会大幅减少。</span><span class="sxs-lookup"><span data-stu-id="121be-121">However, in return the number of methods compiled at runtime is typically reduced substantially.</span></span> <span data-ttu-id="121be-122">因此，启用 ReadyToRun，包含大量代码的大多数应用程序都会获得很大的性能增益。</span><span class="sxs-lookup"><span data-stu-id="121be-122">The result is that most applications that have large amounts of code receive large performance benefits from enabling ReadyToRun.</span></span> <span data-ttu-id="121be-123">由于 .NET 运行时库已使用 ReadyToRun 进行预编译，因此启用 ReadyToRun 时，具有少量代码的应用程序很可能不会获得显著改进。</span><span class="sxs-lookup"><span data-stu-id="121be-123">Applications, which have small amounts of code will likely not experience a significant improvement from enabling ReadyToRun, as the .NET runtime libraries have already been precompiled with ReadyToRun.</span></span>

<span data-ttu-id="121be-124">这里讨论的启动改进不仅适用于应用程序启动，还适用于在应用程序中首次使用任何代码。</span><span class="sxs-lookup"><span data-stu-id="121be-124">The startup improvement discussed here applies not only to application startup, but also to the first use of any code in the application.</span></span> <span data-ttu-id="121be-125">例如，ReadyToRun 可用于降低在 ASP.NET 应用程序中首次使用 Web API 时的响应延迟。</span><span class="sxs-lookup"><span data-stu-id="121be-125">For instance, ReadyToRun can be used to reduce the response latency of the first use  of Web API in an ASP.NET application.</span></span>

### <a name="interaction-with-tiered-compilation"></a><span data-ttu-id="121be-126">通过分层编译进行交互</span><span class="sxs-lookup"><span data-stu-id="121be-126">Interaction with tiered compilation</span></span>

<span data-ttu-id="121be-127">预先生成代码优化程度不如 JIT 生成的代码。</span><span class="sxs-lookup"><span data-stu-id="121be-127">Ahead-of-time generated is not as highly optimized as code produced by the JIT.</span></span> <span data-ttu-id="121be-128">为了解决此问题，分层编译将使用 JIT 生成的方法替换常用的 ReadyToRun 方法。</span><span class="sxs-lookup"><span data-stu-id="121be-128">To address this issue, tiered compilation will replace commonly used ReadyToRun methods with JIT-generated methods.</span></span>

## <a name="how-is-the-set-of-precompiled-assemblies-chosen"></a><span data-ttu-id="121be-129">如何选择预编译的一组程序集？</span><span class="sxs-lookup"><span data-stu-id="121be-129">How is the set of precompiled assemblies chosen?</span></span>

<span data-ttu-id="121be-130">SDK 将预编译随应用程序一起分发的程序集。</span><span class="sxs-lookup"><span data-stu-id="121be-130">The SDK will precompile the assemblies that are distributed with the application.</span></span> <span data-ttu-id="121be-131">对于独立应用程序，这组程序集将包括框架。</span><span class="sxs-lookup"><span data-stu-id="121be-131">For self-contained applications, this set of assemblies will include the framework.</span></span> <span data-ttu-id="121be-132">C++/CLI 二进制文件不适合 ReadyToRun 编译。</span><span class="sxs-lookup"><span data-stu-id="121be-132">C++/CLI binaries are not eligible for ReadyToRun compilation.</span></span>

## <a name="how-is-the-set-of-methods-to-precompile-chosen"></a><span data-ttu-id="121be-133">如何选择要预编译的一组方法？</span><span class="sxs-lookup"><span data-stu-id="121be-133">How is the set of methods to precompile chosen?</span></span>

<span data-ttu-id="121be-134">编译器会尝试预编译尽可能多的方法。</span><span class="sxs-lookup"><span data-stu-id="121be-134">The compiler will attempt to pre-compile as many methods as it can.</span></span> <span data-ttu-id="121be-135">但由于各种原因，不应预期使用 ReadyToRun 功能会导致无法执行 JIT。</span><span class="sxs-lookup"><span data-stu-id="121be-135">However various reasons it is not expected that using the ReadyToRun feature will result in preventing the JIT from executing.</span></span>

<span data-ttu-id="121be-136">这些原因包括（但不限于）：</span><span class="sxs-lookup"><span data-stu-id="121be-136">Such reasons may include, but are not limited to:</span></span>

- <span data-ttu-id="121be-137">使用在单独的程序集中定义的泛型类型</span><span class="sxs-lookup"><span data-stu-id="121be-137">Use of generic types defined in separate assemblies</span></span>
- <span data-ttu-id="121be-138">与本机代码互操作</span><span class="sxs-lookup"><span data-stu-id="121be-138">Interop with native code</span></span>
- <span data-ttu-id="121be-139">使用编译器无法证明可在目标计算机上安全使用的硬件内部函数</span><span class="sxs-lookup"><span data-stu-id="121be-139">Use of hardware intrinsics that the compiler cannot prove are safe to use on a target machine</span></span>
- <span data-ttu-id="121be-140">某些异常 IL 模式</span><span class="sxs-lookup"><span data-stu-id="121be-140">Certain unusual IL patterns</span></span>
- <span data-ttu-id="121be-141">通过反射或 LINQ 创建动态方法</span><span class="sxs-lookup"><span data-stu-id="121be-141">Dynamic method creation via reflection, or LINQ</span></span>

## <a name="cross-platformarchitecture-restrictions"></a><span data-ttu-id="121be-142">跨平台/体系结构限制</span><span class="sxs-lookup"><span data-stu-id="121be-142">Cross platform/architecture restrictions</span></span>

<span data-ttu-id="121be-143">对于某些 SDK 平台，ReadyToRun 编译器可以进行针对其他目标平台的交叉编译。</span><span class="sxs-lookup"><span data-stu-id="121be-143">For some SDK platforms, the ReadyToRun compiler is capable of cross-compiling for other target platforms.</span></span> <span data-ttu-id="121be-144">下表介绍了支持的编译目标。</span><span class="sxs-lookup"><span data-stu-id="121be-144">Supported compilation targets are described in the table below.</span></span>

| <span data-ttu-id="121be-145">SDK 平台</span><span class="sxs-lookup"><span data-stu-id="121be-145">SDK platform</span></span> | <span data-ttu-id="121be-146">支持的目标平台</span><span class="sxs-lookup"><span data-stu-id="121be-146">Supported target platforms</span></span> |
| ------------ | --------------------------- |
| <span data-ttu-id="121be-147">Windows X64</span><span class="sxs-lookup"><span data-stu-id="121be-147">Windows X64</span></span>  | <span data-ttu-id="121be-148">Windows X86、Windows X64、Windows ARM32、Windows ARM64</span><span class="sxs-lookup"><span data-stu-id="121be-148">Windows X86, Windows X64, Windows ARM32, Windows ARM64</span></span> |
| <span data-ttu-id="121be-149">Windows X86</span><span class="sxs-lookup"><span data-stu-id="121be-149">Windows X86</span></span>  | <span data-ttu-id="121be-150">Windows X86、Windows ARM32</span><span class="sxs-lookup"><span data-stu-id="121be-150">Windows X86, Windows ARM32</span></span> |
| <span data-ttu-id="121be-151">Linux X64</span><span class="sxs-lookup"><span data-stu-id="121be-151">Linux X64</span></span>    | <span data-ttu-id="121be-152">Linux X86、Linux X64、Linux ARM32、Linux ARM64</span><span class="sxs-lookup"><span data-stu-id="121be-152">Linux X86, Linux X64, Linux ARM32, Linux ARM64</span></span> |
| <span data-ttu-id="121be-153">Linux ARM32</span><span class="sxs-lookup"><span data-stu-id="121be-153">Linux ARM32</span></span>  | <span data-ttu-id="121be-154">Linux ARM32</span><span class="sxs-lookup"><span data-stu-id="121be-154">Linux ARM32</span></span> |
| <span data-ttu-id="121be-155">Linux ARM64</span><span class="sxs-lookup"><span data-stu-id="121be-155">Linux ARM64</span></span>  | <span data-ttu-id="121be-156">Linux ARM64</span><span class="sxs-lookup"><span data-stu-id="121be-156">Linux ARM64</span></span> |
| <span data-ttu-id="121be-157">macOS X64</span><span class="sxs-lookup"><span data-stu-id="121be-157">macOS X64</span></span>    | <span data-ttu-id="121be-158">macOS X64</span><span class="sxs-lookup"><span data-stu-id="121be-158">macOS X64</span></span> |
