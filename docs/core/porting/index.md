---
title: 从 .NET Framework 移植到 .NET Core
description: 了解移植过程以及发现在将 .NET Framework 项目移植到 .NET Core 时可能有用的工具。
author: cartermp
ms.date: 10/22/2019
ms.openlocfilehash: 7719742294c04aadbfd2e5f223040d3b5b485b5b
ms.sourcegitcommit: 30a686fd4377fe6472aa04e215c0de711bc1c322
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94439737"
---
# <a name="overview-of-porting-from-net-framework-to-net-core"></a><span data-ttu-id="ffaab-103">从 .NET Framework 移植到 .NET Core 的概述</span><span class="sxs-lookup"><span data-stu-id="ffaab-103">Overview of porting from .NET Framework to .NET Core</span></span>

<span data-ttu-id="ffaab-104">你可能有些代码当前正在 .NET Framework 上运行，但你想将这些代码移植到 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="ffaab-104">You might have code that currently runs on the .NET Framework that you're interested in porting to .NET Core.</span></span> <span data-ttu-id="ffaab-105">本文提供以下内容：</span><span class="sxs-lookup"><span data-stu-id="ffaab-105">This article provides:</span></span>

* <span data-ttu-id="ffaab-106">移植过程概述。</span><span class="sxs-lookup"><span data-stu-id="ffaab-106">An overview of the porting process.</span></span>
* <span data-ttu-id="ffaab-107">在将代码移植到 .NET Core 时，可能会发现一系列有用的工具。</span><span class="sxs-lookup"><span data-stu-id="ffaab-107">A list of tools that you may find helpful when you're porting your code to .NET Core.</span></span>

## <a name="overview-of-the-porting-process"></a><span data-ttu-id="ffaab-108">移植过程概述</span><span class="sxs-lookup"><span data-stu-id="ffaab-108">Overview of the porting process</span></span>

<span data-ttu-id="ffaab-109">针对多个项目从 .NET Framework 移植到 .NET Core（或 .NET Standard）的操作相对简单。</span><span class="sxs-lookup"><span data-stu-id="ffaab-109">Porting to .NET Core (or .NET Standard) from .NET Framework for many projects is relatively straight forward.</span></span> <span data-ttu-id="ffaab-110">需进行大量更改，但其中很多都遵循下面所列的模式。</span><span class="sxs-lookup"><span data-stu-id="ffaab-110">There are a number of changes that are required, but many of them follow the patterns outlined below.</span></span> <span data-ttu-id="ffaab-111">对于可在 .NET Core 中使用应用模式的项目（例如库、控制台应用和桌面应用程序），通常需要少量更改。</span><span class="sxs-lookup"><span data-stu-id="ffaab-111">Projects where the app-model is available in .NET Core (such as libraries, console apps, and desktop applications) usually require little changes.</span></span> <span data-ttu-id="ffaab-112">对于需使用新应用模式的项目（例如从 ASP.NET 移至 ASP.NET Core），需要的工作稍微多一点，但很多模式与可在转换过程中使用的模式类似。</span><span class="sxs-lookup"><span data-stu-id="ffaab-112">Projects that require a new app model, such as moving to ASP.NET Core from ASP.NET, require a bit more work, but many patterns have analogs that can be used during the conversion.</span></span> <span data-ttu-id="ffaab-113">本文档可帮助确定用户已经采用来成功转换其基本代码以面向 .NET Standard 或 .NET Core 的主要策略，还将处理“解决方案范围”和“项目特定”这两个级别的转换。</span><span class="sxs-lookup"><span data-stu-id="ffaab-113">This document should help with identifying the main strategies that have been employed by users to successfully convert their code bases to target .NET Standard or .NET Core and will address the conversion at two levels: solution-wide and project specific.</span></span> <span data-ttu-id="ffaab-114">有关应用模式特定的转换，请查看说明底部的链接。</span><span class="sxs-lookup"><span data-stu-id="ffaab-114">See the links at the bottom for directions on app-model specific conversions.</span></span>

<span data-ttu-id="ffaab-115">建议在将项目移植到 .NET Core 时使用以下过程。</span><span class="sxs-lookup"><span data-stu-id="ffaab-115">We recommend you use the following process when porting your project to .NET Core.</span></span> <span data-ttu-id="ffaab-116">其中每个步骤都可能导致行为更改，因此请确保你在继续执行后续步骤之前，对你的库或应用程序进行了充分的测试。</span><span class="sxs-lookup"><span data-stu-id="ffaab-116">Each of these steps introduces potential places for behavior changes, so ensure that you adequately test your library or application before continuing on to later steps.</span></span> <span data-ttu-id="ffaab-117">首先是准备好项目来切换到 .NET Standard 或 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="ffaab-117">The first steps are to get your project ready for a switch to .NET Standard or .NET Core.</span></span> <span data-ttu-id="ffaab-118">如果你有单元测试，则最好先转换它们，以便你能够在你使用的产品中继续测试相关更改。</span><span class="sxs-lookup"><span data-stu-id="ffaab-118">If you have unit tests, it's best to convert them first so that you can continue testing changes in the product you're working on.</span></span> <span data-ttu-id="ffaab-119">由于移植到 .NET Core 对代码库来说是很大的更改，因此强烈建议移植测试项目，以便在移植代码后运行测试。</span><span class="sxs-lookup"><span data-stu-id="ffaab-119">Because porting to .NET Core is such a significant change to your codebase, it's highly recommended to port your test projects so that you can run tests as you port your code over.</span></span> <span data-ttu-id="ffaab-120">MSTest、xUnit 和 NUnit 都适用于 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="ffaab-120">MSTest, xUnit, and NUnit all work on .NET Core.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ffaab-121">入门</span><span class="sxs-lookup"><span data-stu-id="ffaab-121">Getting started</span></span>

<span data-ttu-id="ffaab-122">将在整个过程中使用以下工具：</span><span class="sxs-lookup"><span data-stu-id="ffaab-122">The following tools will be used throughout the process:</span></span>

- <span data-ttu-id="ffaab-123">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="ffaab-123">Visual Studio 2019</span></span>
- <span data-ttu-id="ffaab-124">下载 [.NET 可移植性分析器](../../standard/analyzers/portability-analyzer.md)</span><span class="sxs-lookup"><span data-stu-id="ffaab-124">Download [.NET Portability Analyzer](../../standard/analyzers/portability-analyzer.md)</span></span>
- <span data-ttu-id="ffaab-125">可选：安装 [dotnet try-convert](https://github.com/dotnet/try-convert)</span><span class="sxs-lookup"><span data-stu-id="ffaab-125">_Optional_ Install [dotnet try-convert](https://github.com/dotnet/try-convert)</span></span>

## <a name="porting-a-solution"></a><span data-ttu-id="ffaab-126">移植解决方案</span><span class="sxs-lookup"><span data-stu-id="ffaab-126">Porting a solution</span></span>

<span data-ttu-id="ffaab-127">如果解决方案中有多个项目，则移植可能看起来更复杂，因为必须按特定顺序处理项目。</span><span class="sxs-lookup"><span data-stu-id="ffaab-127">When there are multiple projects in a solution, the porting can seem more complicated because you must address projects in a specific order.</span></span> <span data-ttu-id="ffaab-128">应按从上到下的顺序执行转换过程，其中先转换解决方案中不依赖其他项目的项目，再继续转换，完成整个解决方案的处理。</span><span class="sxs-lookup"><span data-stu-id="ffaab-128">The conversion process should be a bottom-up approach, where the projects with no dependencies on other projects in the solution are converted first, and continue up through the whole solution.</span></span>

<span data-ttu-id="ffaab-129">为确定项目的迁移顺序，可使用以下工具：</span><span class="sxs-lookup"><span data-stu-id="ffaab-129">In order to identify the order projects should be migrated, you can use the following tools:</span></span>

- <span data-ttu-id="ffaab-130">[Visual Studio 中的依赖项关系图](/visualstudio/modeling/create-layer-diagrams-from-your-code)可在解决方案中创建代码定向图。</span><span class="sxs-lookup"><span data-stu-id="ffaab-130">[Dependency Diagrams in Visual Studio](/visualstudio/modeling/create-layer-diagrams-from-your-code) can create a directed graph of the code in a solution.</span></span>
- <span data-ttu-id="ffaab-131">运行 `msbuild _SolutionPath_ /t:GenerateRestoreGraphFile /p:RestoreGraphOutputPath=graph.dg.json` 以生成一个包含项目引用列表的 json 文档。</span><span class="sxs-lookup"><span data-stu-id="ffaab-131">Run `msbuild _SolutionPath_ /t:GenerateRestoreGraphFile /p:RestoreGraphOutputPath=graph.dg.json` to generate a json document that includes list of project references.</span></span>
- <span data-ttu-id="ffaab-132">使用 `-r DGML` 开关运行 [.NET 可移植性分析器](../../standard/analyzers/portability-analyzer.md)，检索程序集的依赖项关系图。</span><span class="sxs-lookup"><span data-stu-id="ffaab-132">Run [.NET Portability Analyzer](../../standard/analyzers/portability-analyzer.md) with the `-r DGML` switch to retrieve a dependency diagram of the assemblies.</span></span> <span data-ttu-id="ffaab-133">有关详细信息，请参阅[此文](../../standard/analyzers/portability-analyzer.md#solution-wide-view)。</span><span class="sxs-lookup"><span data-stu-id="ffaab-133">For more information, see [here](../../standard/analyzers/portability-analyzer.md#solution-wide-view).</span></span>

<span data-ttu-id="ffaab-134">拥有依赖项信息后，可用它来在叶节点开始操作，一直到应用下一部分相关步骤的依赖项树。</span><span class="sxs-lookup"><span data-stu-id="ffaab-134">Once you have dependency information, you can use that information to start at the leaf nodes and work your way up the dependency tree applying the steps in the next section.</span></span>

## <a name="per-project-steps"></a><span data-ttu-id="ffaab-135">按项目步骤</span><span class="sxs-lookup"><span data-stu-id="ffaab-135">Per project steps</span></span>

<span data-ttu-id="ffaab-136">建议在将项目移植到 .NET Core 时使用以下过程：</span><span class="sxs-lookup"><span data-stu-id="ffaab-136">We recommend you use the following process when porting your project to .NET Core:</span></span>

1. <span data-ttu-id="ffaab-137">通过 [Visual Studio 中的转换工具](/nuget/consume-packages/migrate-packages-config-to-package-reference)将所有 `packages.config` 依赖项转换为 [PackageReference](/nuget/consume-packages/package-references-in-project-files) 格式。</span><span class="sxs-lookup"><span data-stu-id="ffaab-137">Convert all of your `packages.config` dependencies to the [PackageReference](/nuget/consume-packages/package-references-in-project-files) format with the [conversion tool in Visual Studio](/nuget/consume-packages/migrate-packages-config-to-package-reference).</span></span>

   <span data-ttu-id="ffaab-138">此步骤涉及到转换旧 `packages.config` 格式的依赖项。</span><span class="sxs-lookup"><span data-stu-id="ffaab-138">This step involves converting your dependencies from the legacy `packages.config` format.</span></span> <span data-ttu-id="ffaab-139">`packages.config` 不适用于 .NET Core，因此，如果你有包依赖项，则需要进行此转换。</span><span class="sxs-lookup"><span data-stu-id="ffaab-139">`packages.config` doesn't work on .NET Core, so this conversion is required if you have package dependencies.</span></span> <span data-ttu-id="ffaab-140">此外，它仅需要你直接在项目中使用的依赖项，这通过减少必须管理的依赖项数量，使后续步骤更加简单。</span><span class="sxs-lookup"><span data-stu-id="ffaab-140">It also only requires the dependencies you are directly using in a project, which makes later steps easier by reducing the number of dependencies you must manage.</span></span>

1. <span data-ttu-id="ffaab-141">将项目文件转换为新的 SDK 样式文件结构。</span><span class="sxs-lookup"><span data-stu-id="ffaab-141">Convert your project file to the new SDK-style files structure.</span></span> <span data-ttu-id="ffaab-142">你可为 .NET Core 创建新项目并覆盖源文件，也可尝试使用工具转换现有的项目文件。</span><span class="sxs-lookup"><span data-stu-id="ffaab-142">You can create new projects for .NET Core and copy over source files, or attempt to convert your existing project file with a tool.</span></span>

   <span data-ttu-id="ffaab-143">.NET Core 使用不同于 .NET Framework 的更简化的[项目文件格式](../tools/csproj.md)。</span><span class="sxs-lookup"><span data-stu-id="ffaab-143">.NET Core uses a simplified (and different) [project file format](../tools/csproj.md) than .NET Framework.</span></span> <span data-ttu-id="ffaab-144">需要将项目文件转换为此格式才能继续操作。</span><span class="sxs-lookup"><span data-stu-id="ffaab-144">You'll need to convert your project files into this format to continue.</span></span> <span data-ttu-id="ffaab-145">借助此项目样式，还可面向 .NET Framework（你此时仍需要面向此模型）。</span><span class="sxs-lookup"><span data-stu-id="ffaab-145">This project style allows you to also target .NET Framework, which at this point you'll still want to target.</span></span>

   <span data-ttu-id="ffaab-146">你可尝试使用 [dotnet try-convert](https://github.com/dotnet/try-convert) 工具，通过一次操作将较小的解决方案或单个项目移植到 .NET Core 项目文件格式。</span><span class="sxs-lookup"><span data-stu-id="ffaab-146">You can attempt to port smaller solutions or individual projects in one operation to the .NET Core project file format with the [dotnet try-convert](https://github.com/dotnet/try-convert) tool.</span></span> <span data-ttu-id="ffaab-147">不能保证 `dotnet try-convert` 适用于所有项目，它可能导致所依赖的行为发生细微变化。</span><span class="sxs-lookup"><span data-stu-id="ffaab-147">`dotnet try-convert` is not guaranteed to work for all your projects, and it may cause subtle changes in behavior that you depended on.</span></span> <span data-ttu-id="ffaab-148">使用它作为起点，以自动化可自动执行的基本操作。</span><span class="sxs-lookup"><span data-stu-id="ffaab-148">Use it as a _starting point_ that automates the basic things that can be automated.</span></span> <span data-ttu-id="ffaab-149">该解决方案不保证会迁移项目，因为与旧样式的项目文件相比，SDK 样式的项目使用的目标中存在诸多差异。</span><span class="sxs-lookup"><span data-stu-id="ffaab-149">It isn't a guaranteed solution to migrating a project, as there are many differences in the targets used by the SDK style projects compared to the old-style project files.</span></span>

1. <span data-ttu-id="ffaab-150">将希望移植的所有项目重定向到目标 .NET Framework 4.7.2 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="ffaab-150">Retarget all projects you wish to port to target .NET Framework 4.7.2 or higher.</span></span>

   <span data-ttu-id="ffaab-151">此步骤可确保在 .NET Core 不支持特殊 API 的情况下，可以为特定于 .NET Framework 的目标使用备用 API。</span><span class="sxs-lookup"><span data-stu-id="ffaab-151">This step ensures that you can use API alternatives for .NET Framework-specific targets when .NET Core doesn't support a particular API.</span></span>

1. <span data-ttu-id="ffaab-152">将所有依赖项更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="ffaab-152">Update all dependencies to the latest version.</span></span> <span data-ttu-id="ffaab-153">项目可能在使用更旧的库版本，而这些版本可能不支持 .NET Standard。</span><span class="sxs-lookup"><span data-stu-id="ffaab-153">Projects may be using older versions of libraries that may not have .NET Standard support.</span></span> <span data-ttu-id="ffaab-154">但是，之后的版本可能支持该规范，只用简单切换一下就行。</span><span class="sxs-lookup"><span data-stu-id="ffaab-154">However, later versions may support it with a simple switch.</span></span> <span data-ttu-id="ffaab-155">如果库中存在中断性变更，则这可能需要更改代码。</span><span class="sxs-lookup"><span data-stu-id="ffaab-155">This may require code changes if there are breaking changes in libraries.</span></span>

1. <span data-ttu-id="ffaab-156">使用 [.NET 可移植性分析器](../../standard/analyzers/portability-analyzer.md)来分析程序集，并查看这些程序集是否可移植到 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="ffaab-156">Use the [.NET Portability Analyzer](../../standard/analyzers/portability-analyzer.md) to analyze your assemblies and see if they're portable to .NET Core.</span></span>

   <span data-ttu-id="ffaab-157">.NET 可移植性分析器工具可分析已编译的程序集并生成报表。</span><span class="sxs-lookup"><span data-stu-id="ffaab-157">The .NET Portability Analyzer tool analyzes your compiled assemblies and generates a report.</span></span> <span data-ttu-id="ffaab-158">此报表显示高级别可移植性摘要，以及你所使用的不适用于 .NET Core 的各个 API 细目。</span><span class="sxs-lookup"><span data-stu-id="ffaab-158">This report shows a high-level portability summary and a breakdown of each API you're using that isn't available on .NET Core.</span></span> <span data-ttu-id="ffaab-159">使用该工具时，只提交你正在转换的单个项目，从而专注于可能需要的 API 更改。</span><span class="sxs-lookup"><span data-stu-id="ffaab-159">While using the tool, only submit the individual project you are converting to focus on the API changes that are potentially needed.</span></span> <span data-ttu-id="ffaab-160">很多 API 在 .NET Core 中具有相同的可用性，而你需要切换到该平台。</span><span class="sxs-lookup"><span data-stu-id="ffaab-160">Many of the APIs have equivalent availability in .NET Core, which you'll want to switch to.</span></span>

   <span data-ttu-id="ffaab-161">在读取分析器生成的报表时，重要的信息是正在使用的实际 API，而不一定是对目标平台的支持百分比。</span><span class="sxs-lookup"><span data-stu-id="ffaab-161">While reading the reports generated by the analyzer, the important information is the actual APIs that are being used and not necessarily the percentage of support for the target platform.</span></span> <span data-ttu-id="ffaab-162">很多 API 在 .NET Standard/Core 中都有等效选项，因此了解你的库或应用程序需要 API 实现的方案将有助于确定可移植性的影响。</span><span class="sxs-lookup"><span data-stu-id="ffaab-162">Many APIs have equivalent options in .NET Standard/Core, and so understanding the scenarios your library or application needs the API for will help determine the implication for portability.</span></span>

   <span data-ttu-id="ffaab-163">在某些情况下，API 不是等效的，需要执行一些编译器预处理器指令（即 `#if NET45`）来应对平台的特殊情况。</span><span class="sxs-lookup"><span data-stu-id="ffaab-163">There are some cases where APIs are not equivalent and you'll need to do some compiler preprocessor directives (that is, `#if NET45`) to special case the platforms.</span></span> <span data-ttu-id="ffaab-164">此时，你的项目仍然面向 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="ffaab-164">At this point, your project will still be targeting .NET Framework.</span></span> <span data-ttu-id="ffaab-165">对于上述每种有针对性的情况，建议使用可被理解为方案的已知条件。</span><span class="sxs-lookup"><span data-stu-id="ffaab-165">For each of these targeted cases, it is recommended to use well-known conditionals that can be understood as a scenario.</span></span>  <span data-ttu-id="ffaab-166">例如，.NET Core 中的 AppDomain 支持受到限制，但是对于加载和卸载程序集的方案，有一个新的 API 无法在 .NET Core 中使用。</span><span class="sxs-lookup"><span data-stu-id="ffaab-166">For example, AppDomain support in .NET Core is limited, but for the scenario of loading and unloading assemblies, there is a new API that's not available in .NET Core.</span></span> <span data-ttu-id="ffaab-167">要在代码中处理此情况，一种常见的方式如下所示：</span><span class="sxs-lookup"><span data-stu-id="ffaab-167">A common way to handle this in code would be something like this:</span></span>

   ```csharp
   #if FEATURE_APPDOMAIN_LOADING
   // Code that uses appdomains
   #elif FEATURE_ASSEMBLY_LOAD_CONTEXT
   // Code that uses assembly load context
   #else
   #error Unsupported platform
   #endif
   ```

1. <span data-ttu-id="ffaab-168">将 [.NET API 分析器](../../standard/analyzers/api-analyzer.md)安装到项目中，以识别在某些平台上会引发 <xref:System.PlatformNotSupportedException> 的 API 以及一些其他潜在的兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="ffaab-168">Install the [.NET API analyzer](../../standard/analyzers/api-analyzer.md) into your projects to identify APIs that throw <xref:System.PlatformNotSupportedException> on some platforms and some other potential compatibility issues.</span></span>

   <span data-ttu-id="ffaab-169">此工具与可移植性分析器类似，但它不会分析是否可以在 .NET Core 上构建代码，而是分析你是否正在以会导致在运行时引发 <xref:System.PlatformNotSupportedException> 的某种方式使用 API。</span><span class="sxs-lookup"><span data-stu-id="ffaab-169">This tool is similar to the portability analyzer, but instead of analyzing if code can build on .NET Core, it analyzes whether you're using an API in a way that will throw a <xref:System.PlatformNotSupportedException> at run time.</span></span> <span data-ttu-id="ffaab-170">尽管这并不常见，但如果从 .NET Framework 4.7.2 或更高版本进行移动，最好进行检查。</span><span class="sxs-lookup"><span data-stu-id="ffaab-170">Although this isn't common if you're moving from .NET Framework 4.7.2 or higher, it's good to check.</span></span> <span data-ttu-id="ffaab-171">如需详细了解会在 .NET Core 上引发异常的 API 信息，请参阅[在 .NET Core上始终引发异常的 API](../compatibility/unsupported-apis.md)。</span><span class="sxs-lookup"><span data-stu-id="ffaab-171">For more information about APIs that throw exceptions on .NET Core, see [APIs that always throw exceptions on .NET Core](../compatibility/unsupported-apis.md).</span></span>

1. <span data-ttu-id="ffaab-172">此时，你可切换为面向 .NET Core（通常用于应用程序）或 .NET Standard（用于库）。</span><span class="sxs-lookup"><span data-stu-id="ffaab-172">At this point, you can switch to targeting .NET Core (generally for applications) or .NET Standard (for libraries).</span></span>

   <span data-ttu-id="ffaab-173">选择 .NET Core 还是 .NET Standard 主要取决于将运行项目的位置。</span><span class="sxs-lookup"><span data-stu-id="ffaab-173">The choice between .NET Core and .NET Standard is largely dependent on where the project will be run.</span></span> <span data-ttu-id="ffaab-174">如果它是其他应用程序将使用的库或将通过 NuGet 分发的库，通常首选的是面向 .NET Standard。</span><span class="sxs-lookup"><span data-stu-id="ffaab-174">If it is a library that will be consumed by other applications or distributed via NuGet, the preference is usually to target .NET Standard.</span></span> <span data-ttu-id="ffaab-175">但是，出于性能原因或其他原因，可能有一些 API 只能在 .NET Core 上使用；如果不是这样，则应面向 .NET Core，但可能也有 .NET Standard 版本可供使用，其性能或功能有所降低。</span><span class="sxs-lookup"><span data-stu-id="ffaab-175">However, there may be APIs that are only available on .NET Core for performance or other reasons; if that's the case, .NET Core should be targeted with potentially a .NET Standard build available as well with reduced performance or functionality.</span></span> <span data-ttu-id="ffaab-176">通过面向 .NET Standard，项目将能够在新平台（如 WebAssembly）上运行。</span><span class="sxs-lookup"><span data-stu-id="ffaab-176">By targeting .NET Standard, the project will be ready to run on new platforms (such as WebAssembly).</span></span> <span data-ttu-id="ffaab-177">如果项目对特定应用框架（如 ASP.NET Core）具有依赖项，则面向的目标将受到依赖项支持的内容限制。</span><span class="sxs-lookup"><span data-stu-id="ffaab-177">If the project has dependencies on specific app frameworks (such as ASP.NET Core), then the target will be limited by what the dependencies support.</span></span>

   <span data-ttu-id="ffaab-178">如果对 .NET Framework 或 .NET Standard 来说，没有针对条件编译代码的预处理器指令，则该操作将如同在项目文件中查找以下内容一样简单：</span><span class="sxs-lookup"><span data-stu-id="ffaab-178">If there are no preprocessor directives to conditional compile code for .NET Framework or .NET Standard, this will be as simple as finding the following in the project file:</span></span>

   ```xml
   <TargetFramework>net472</TargetFramework>
   ```

   <span data-ttu-id="ffaab-179">并将它切换到所需框架。</span><span class="sxs-lookup"><span data-stu-id="ffaab-179">and switch it to the desired framework.</span></span> <span data-ttu-id="ffaab-180">对于 .NET Core 3.1，这为：</span><span class="sxs-lookup"><span data-stu-id="ffaab-180">For .NET Core 3.1, this would be:</span></span>

   ```xml
   <TargetFramework>netcoreapp3.1</TargetFramework>
   ```

   <span data-ttu-id="ffaab-181">但是，如果这是一个库，而你希望它继续支持 .NET Framework 特定的版本，则可通过将其替换为以下内容来设置[多目标](../../standard/library-guidance/cross-platform-targeting.md)：</span><span class="sxs-lookup"><span data-stu-id="ffaab-181">However, if this is a library for which you want to continue supporting .NET Framework-specific builds, you can [multi-target](../../standard/library-guidance/cross-platform-targeting.md) by replacing it with the following:</span></span>

   ```xml
   <TargetFrameworks>net472;netstandard2.0</TargetFrameworks>
   ```

   <span data-ttu-id="ffaab-182">如果正在使用特定于 Windows 的 API（例如注册表访问），请安装 [Windows 兼容包](./windows-compat-pack.md)。</span><span class="sxs-lookup"><span data-stu-id="ffaab-182">If you're using Windows-specific APIs (such as registry access), install the [Windows Compatibility Pack](./windows-compat-pack.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffaab-183">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ffaab-183">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="ffaab-184">[分析依赖项](third-party-deps.md)
> [打包 NuGet 包](../deploying/creating-nuget-packages.md)</span><span class="sxs-lookup"><span data-stu-id="ffaab-184">[Analyze dependencies](third-party-deps.md)
[Package a NuGet package](../deploying/creating-nuget-packages.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="ffaab-185">请参阅</span><span class="sxs-lookup"><span data-stu-id="ffaab-185">See also</span></span>

- [<span data-ttu-id="ffaab-186">ASP.NET 到 ASP.NET Core 迁移</span><span class="sxs-lookup"><span data-stu-id="ffaab-186">ASP.NET to ASP.NET Core migration</span></span>](/aspnet/core/migration/proper-to-2x)
- [<span data-ttu-id="ffaab-187">将 WPF 应用迁移到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="ffaab-187">Migrate WPF apps to .NET Core</span></span>](/dotnet/desktop/wpf/migration/convert-project-from-net-framework)
- [<span data-ttu-id="ffaab-188">将 .NET Framework Windows 窗体应用迁移到 .NET</span><span class="sxs-lookup"><span data-stu-id="ffaab-188">Migrate .NET Framework Windows Forms apps to .NET</span></span>](/dotnet/desktop/winforms/migration/?view=netdesktop-5.0&preserve-view=true)
