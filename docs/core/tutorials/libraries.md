---
title: 使用 .NET Core CLI 开发库
description: 了解如何使用 .NET Core CLI 创建 .NET Core 库。 将创建一个支持多个框架的库。
author: cartermp
ms.topic: how-to
ms.date: 05/01/2017
ms.openlocfilehash: e98ce9e08c8d92bb4c89348e21cece60de811848
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223699"
---
# <a name="develop-libraries-with-the-net-core-cli"></a><span data-ttu-id="ec95d-104">使用 .NET Core CLI 开发库</span><span class="sxs-lookup"><span data-stu-id="ec95d-104">Develop libraries with the .NET Core CLI</span></span>

<span data-ttu-id="ec95d-105">本文介绍如何使用 .NET Core CLI 编写 .NET 的库。</span><span class="sxs-lookup"><span data-stu-id="ec95d-105">This article covers how to write libraries for .NET using the .NET Core CLI.</span></span> <span data-ttu-id="ec95d-106">CLI 提供可跨任何支持的 OS 工作的高效低级别体验。</span><span class="sxs-lookup"><span data-stu-id="ec95d-106">The CLI provides an efficient and low-level experience that works across any supported OS.</span></span> <span data-ttu-id="ec95d-107">仍可使用 Visual Studio 生成库，如果你首选这种体验，请[参阅 Visual Studio 指南](library-with-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="ec95d-107">You can still build libraries with Visual Studio, and if that is your preferred experience [refer to the Visual Studio guide](library-with-visual-studio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec95d-108">先决条件</span><span class="sxs-lookup"><span data-stu-id="ec95d-108">Prerequisites</span></span>

<span data-ttu-id="ec95d-109">需要在计算机上安装 [.NET Core SDK 和 CLI](https://dotnet.microsoft.com/download) 。</span><span class="sxs-lookup"><span data-stu-id="ec95d-109">You need [the .NET Core SDK and CLI](https://dotnet.microsoft.com/download) installed on your machine.</span></span>

<span data-ttu-id="ec95d-110">对于本文档中处理 .NET Framework 版本的部分，需要在 Windows 计算机上安装 [.NET Framework](https://dotnet.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="ec95d-110">For the sections of this document dealing with .NET Framework versions, you need the [.NET Framework](https://dotnet.microsoft.com) installed on a Windows machine.</span></span>

<span data-ttu-id="ec95d-111">此外，如果想要支持较旧的 .NET Framework 目标，需要从 [.NET 下载存档页](https://dotnet.microsoft.com/download/archives)安装目标包或开发人员工具包。</span><span class="sxs-lookup"><span data-stu-id="ec95d-111">Additionally, if you wish to support older .NET Framework targets, you need to install targeting packs or developer packs from the [.NET download archives page](https://dotnet.microsoft.com/download/archives).</span></span> <span data-ttu-id="ec95d-112">请参阅此表：</span><span class="sxs-lookup"><span data-stu-id="ec95d-112">Refer to this table:</span></span>

| <span data-ttu-id="ec95d-113">.NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="ec95d-113">.NET Framework version</span></span> | <span data-ttu-id="ec95d-114">下载内容</span><span class="sxs-lookup"><span data-stu-id="ec95d-114">What to download</span></span>                                       |
| ---------------------- | ------------------------------------------------------ |
| <span data-ttu-id="ec95d-115">4.6.1</span><span class="sxs-lookup"><span data-stu-id="ec95d-115">4.6.1</span></span>                  | <span data-ttu-id="ec95d-116">.NET Framework 4.6.1 目标包</span><span class="sxs-lookup"><span data-stu-id="ec95d-116">.NET Framework 4.6.1 Targeting Pack</span></span>                    |
| <span data-ttu-id="ec95d-117">4.6</span><span class="sxs-lookup"><span data-stu-id="ec95d-117">4.6</span></span>                    | <span data-ttu-id="ec95d-118">.NET Framework 4.6 目标包</span><span class="sxs-lookup"><span data-stu-id="ec95d-118">.NET Framework 4.6 Targeting Pack</span></span>                      |
| <span data-ttu-id="ec95d-119">4.5.2</span><span class="sxs-lookup"><span data-stu-id="ec95d-119">4.5.2</span></span>                  | <span data-ttu-id="ec95d-120">.NET Framework 4.5.2 开发人员工具包</span><span class="sxs-lookup"><span data-stu-id="ec95d-120">.NET Framework 4.5.2 Developer Pack</span></span>                    |
| <span data-ttu-id="ec95d-121">4.5.1</span><span class="sxs-lookup"><span data-stu-id="ec95d-121">4.5.1</span></span>                  | <span data-ttu-id="ec95d-122">.NET Framework 4.5.1 开发人员工具包</span><span class="sxs-lookup"><span data-stu-id="ec95d-122">.NET Framework 4.5.1 Developer Pack</span></span>                    |
| <span data-ttu-id="ec95d-123">4.5</span><span class="sxs-lookup"><span data-stu-id="ec95d-123">4.5</span></span>                    | <span data-ttu-id="ec95d-124">适用于 Windows 8 的 Windows 软件开发工具包</span><span class="sxs-lookup"><span data-stu-id="ec95d-124">Windows Software Development Kit for Windows 8</span></span>         |
| <span data-ttu-id="ec95d-125">4.0</span><span class="sxs-lookup"><span data-stu-id="ec95d-125">4.0</span></span>                    | <span data-ttu-id="ec95d-126">Windows SDK for Windows 7 和 .NET Framework 4</span><span class="sxs-lookup"><span data-stu-id="ec95d-126">Windows SDK for Windows 7 and .NET Framework 4</span></span>         |
| <span data-ttu-id="ec95d-127">2.0、3.0 和 3.5</span><span class="sxs-lookup"><span data-stu-id="ec95d-127">2.0, 3.0, and 3.5</span></span>      | <span data-ttu-id="ec95d-128">.NET Framework 3.5 SP1 运行时（或 Windows 8+ 版本）</span><span class="sxs-lookup"><span data-stu-id="ec95d-128">.NET Framework 3.5 SP1 Runtime (or Windows 8+ version)</span></span> |

## <a name="how-to-target-net-standard"></a><span data-ttu-id="ec95d-129">如何以 .NET Standard 为目标</span><span class="sxs-lookup"><span data-stu-id="ec95d-129">How to target .NET Standard</span></span>

<span data-ttu-id="ec95d-130">如果不熟悉 .NET Standard，请参阅 [.NET Standard](../../standard/net-standard.md) 了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="ec95d-130">If you're not familiar with .NET Standard, refer to [.NET Standard](../../standard/net-standard.md) to learn more.</span></span>

<span data-ttu-id="ec95d-131">在该文中，提供有一个将 .NET Standard 版本映射到各种实现的表格：</span><span class="sxs-lookup"><span data-stu-id="ec95d-131">In that article, there is a table that maps .NET Standard versions to various implementations:</span></span>

[!INCLUDE [net-standard-table](../../../includes/net-standard-table.md)]

<span data-ttu-id="ec95d-132">以下是此表格对于创建库的意义：</span><span class="sxs-lookup"><span data-stu-id="ec95d-132">Here's what this table means for the purposes of creating a library:</span></span>

<span data-ttu-id="ec95d-133">选择 .NET Standard 版本时，需要在能够访问最新 API 与能够定位更多 .NET 实现代码和 .NET Standard 版本之间进行权衡。</span><span class="sxs-lookup"><span data-stu-id="ec95d-133">The version of .NET Standard you pick will be a tradeoff between access to the newest APIs and the ability to target more .NET implementations and .NET Standard versions.</span></span> <span data-ttu-id="ec95d-134">通过选择 `netstandardX.X` 版本（其中 `X.X` 是版本号）并将其添加到项目文件（`.csproj` 或 `.fsproj`），控制可面向的平台和版本范围。</span><span class="sxs-lookup"><span data-stu-id="ec95d-134">You control the range of targetable platforms and versions by picking a version of `netstandardX.X` (where `X.X` is a version number) and adding it to your project file (`.csproj` or `.fsproj`).</span></span>

<span data-ttu-id="ec95d-135">面向 .NET Standard 时，有三种主要选项，具体取决于你的需求。</span><span class="sxs-lookup"><span data-stu-id="ec95d-135">You have three primary options when targeting .NET Standard, depending on your needs.</span></span>

1. <span data-ttu-id="ec95d-136">可使用 .NET Standard 的默认版本，该版本由 `netstandard1.4` 模板提供，可提供对 .NET Standard 上大多数 API 的访问权限，同时仍与 UWP、.NET Framework 4.6.1 和 .NET Standard 2.0 兼容。</span><span class="sxs-lookup"><span data-stu-id="ec95d-136">You can use the default version of .NET Standard supplied by templates, `netstandard1.4`, which gives you access to most APIs on .NET Standard while still being compatible with UWP, .NET Framework 4.6.1, and .NET Standard 2.0.</span></span>

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
      <PropertyGroup>
        <TargetFramework>netstandard1.4</TargetFramework>
      </PropertyGroup>
    </Project>
    ```

2. <span data-ttu-id="ec95d-137">可通过修改项目文件 `TargetFramework` 节点中的值来使用更低或更高版本的 .NET Standard。</span><span class="sxs-lookup"><span data-stu-id="ec95d-137">You can use a lower or higher version of .NET Standard by modifying the value in the `TargetFramework` node of your project file.</span></span>

    <span data-ttu-id="ec95d-138">.NET Standard 版本可后向兼容。</span><span class="sxs-lookup"><span data-stu-id="ec95d-138">.NET Standard versions are backward compatible.</span></span> <span data-ttu-id="ec95d-139">这意味着 `netstandard1.0` 库可在 `netstandard1.1` 平台以及更高版本上运行。</span><span class="sxs-lookup"><span data-stu-id="ec95d-139">That means that `netstandard1.0` libraries run on `netstandard1.1` platforms and higher.</span></span> <span data-ttu-id="ec95d-140">但是，没有向前兼容性。</span><span class="sxs-lookup"><span data-stu-id="ec95d-140">However, there is no forward compatibility.</span></span> <span data-ttu-id="ec95d-141">低版本的 .NET Standard 平台无法引用较高版本的平台。</span><span class="sxs-lookup"><span data-stu-id="ec95d-141">Lower .NET Standard platforms cannot reference higher ones.</span></span> <span data-ttu-id="ec95d-142">这意味着 `netstandard1.0` 库不能引用面向 `netstandard1.1` 或更高版本的库。</span><span class="sxs-lookup"><span data-stu-id="ec95d-142">This means that `netstandard1.0` libraries cannot reference libraries targeting `netstandard1.1` or higher.</span></span> <span data-ttu-id="ec95d-143">选择适合所需、恰当混合有 API 和平台支持的 Standard 版本。</span><span class="sxs-lookup"><span data-stu-id="ec95d-143">Select the Standard version that has the right mix of APIs and platform support for your needs.</span></span> <span data-ttu-id="ec95d-144">目前，我们建议 `netstandard1.4`。</span><span class="sxs-lookup"><span data-stu-id="ec95d-144">We recommend `netstandard1.4` for now.</span></span>

3. <span data-ttu-id="ec95d-145">如果希望面向 .NET Framework 版本 4.0 或更低版本，或者要使用 .NET Framework 中提供但 .NET Standard 中不提供的 API（例如 `System.Drawing`），请阅读以下部分，了解如何设定多目标。</span><span class="sxs-lookup"><span data-stu-id="ec95d-145">If you want to target .NET Framework versions 4.0 or below, or you wish to use an API available in .NET Framework but not in .NET Standard (for example, `System.Drawing`), read the following sections and learn how to multitarget.</span></span>

## <a name="how-to-target-net-framework"></a><span data-ttu-id="ec95d-146">如何面向 .NET framework</span><span class="sxs-lookup"><span data-stu-id="ec95d-146">How to target .NET Framework</span></span>

> [!NOTE]
> <span data-ttu-id="ec95d-147">这些说明假定计算机上安装有 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="ec95d-147">These instructions assume you have .NET Framework installed on your machine.</span></span> <span data-ttu-id="ec95d-148">请参阅[先决条件](#prerequisites) 获取安装的依赖项。</span><span class="sxs-lookup"><span data-stu-id="ec95d-148">Refer to the [Prerequisites](#prerequisites) to get dependencies installed.</span></span>

<span data-ttu-id="ec95d-149">请记住，此处使用的某些 .NET Framework 版本不再受支持。</span><span class="sxs-lookup"><span data-stu-id="ec95d-149">Keep in mind that some of the .NET Framework versions used here are no longer supported.</span></span> <span data-ttu-id="ec95d-150">有关不受支持的版本信息，请参阅 [.NET Framework 支持生命周期策略常见问题](https://support.microsoft.com/gp/framework_faq/en-us)。</span><span class="sxs-lookup"><span data-stu-id="ec95d-150">Refer to the [.NET Framework Support Lifecycle Policy FAQ](https://support.microsoft.com/gp/framework_faq/en-us) about unsupported versions.</span></span>

<span data-ttu-id="ec95d-151">如果要达到最大数量的开发人员和项目，可将 .NET Framework 4.0 用作基线目标。</span><span class="sxs-lookup"><span data-stu-id="ec95d-151">If you want to reach the maximum number of developers and projects, use .NET Framework 4.0 as your baseline target.</span></span> <span data-ttu-id="ec95d-152">若要以 .NET Framework 为目标，首先使用与要支持的 .NET Framework 版本相对应的正确目标框架名字对象 (TFM)。</span><span class="sxs-lookup"><span data-stu-id="ec95d-152">To target .NET Framework, begin by using the correct Target Framework Moniker (TFM) that corresponds to the .NET Framework version you wish to support.</span></span>

| <span data-ttu-id="ec95d-153">.NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="ec95d-153">.NET Framework version</span></span> | <span data-ttu-id="ec95d-154">TFM</span><span class="sxs-lookup"><span data-stu-id="ec95d-154">TFM</span></span>      |
| ---------------------- | -------- |
| <span data-ttu-id="ec95d-155">.NET Framework 2.0</span><span class="sxs-lookup"><span data-stu-id="ec95d-155">.NET Framework 2.0</span></span>     | `net20`  |
| <span data-ttu-id="ec95d-156">.NET Framework 3.0</span><span class="sxs-lookup"><span data-stu-id="ec95d-156">.NET Framework 3.0</span></span>     | `net30`  |
| <span data-ttu-id="ec95d-157">.NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="ec95d-157">.NET Framework 3.5</span></span>     | `net35`  |
| <span data-ttu-id="ec95d-158">.NET Framework 4.0</span><span class="sxs-lookup"><span data-stu-id="ec95d-158">.NET Framework 4.0</span></span>     | `net40`  |
| <span data-ttu-id="ec95d-159">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="ec95d-159">.NET Framework 4.5</span></span>     | `net45`  |
| <span data-ttu-id="ec95d-160">.NET Framework 4.5.1</span><span class="sxs-lookup"><span data-stu-id="ec95d-160">.NET Framework 4.5.1</span></span>   | `net451` |
| <span data-ttu-id="ec95d-161">.NET Framework 4.5.2</span><span class="sxs-lookup"><span data-stu-id="ec95d-161">.NET Framework 4.5.2</span></span>   | `net452` |
| <span data-ttu-id="ec95d-162">.NET Framework 4.6</span><span class="sxs-lookup"><span data-stu-id="ec95d-162">.NET Framework 4.6</span></span>     | `net46`  |
| <span data-ttu-id="ec95d-163">.NET Framework 4.6.1</span><span class="sxs-lookup"><span data-stu-id="ec95d-163">.NET Framework 4.6.1</span></span>   | `net461` |
| <span data-ttu-id="ec95d-164">.NET Framework 4.6.2</span><span class="sxs-lookup"><span data-stu-id="ec95d-164">.NET Framework 4.6.2</span></span>   | `net462` |
| <span data-ttu-id="ec95d-165">.NET Framework 4.7</span><span class="sxs-lookup"><span data-stu-id="ec95d-165">.NET Framework 4.7</span></span>     | `net47`  |
| <span data-ttu-id="ec95d-166">.NET Framework 4.8</span><span class="sxs-lookup"><span data-stu-id="ec95d-166">.NET Framework 4.8</span></span>     | `net48`  |

<span data-ttu-id="ec95d-167">然后将此 TFM 插入项目文件的 `TargetFramework` 部分。</span><span class="sxs-lookup"><span data-stu-id="ec95d-167">You then insert this TFM into the `TargetFramework` section of your project file.</span></span> <span data-ttu-id="ec95d-168">例如，下面展示了如何编写面向 .NET Framework 4.0 的库：</span><span class="sxs-lookup"><span data-stu-id="ec95d-168">For example, here's how you would write a library that targets .NET Framework 4.0:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>net40</TargetFramework>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="ec95d-169">大功告成！</span><span class="sxs-lookup"><span data-stu-id="ec95d-169">And that's it!</span></span> <span data-ttu-id="ec95d-170">虽然此库仅针对 .NET Framework 4 编译，但可在较新版本的 .NET Framework 上使用此库。</span><span class="sxs-lookup"><span data-stu-id="ec95d-170">Although this compiled only for .NET Framework 4, you can use the library on newer versions of .NET Framework.</span></span>

## <a name="how-to-multitarget"></a><span data-ttu-id="ec95d-171">如何设定多目标</span><span class="sxs-lookup"><span data-stu-id="ec95d-171">How to multitarget</span></span>

> [!NOTE]
> <span data-ttu-id="ec95d-172">以下说明假定计算机上安装有 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="ec95d-172">The following instructions assume you have the .NET Framework installed on your machine.</span></span> <span data-ttu-id="ec95d-173">请参阅[先决条件](#prerequisites)部分，了解需要安装哪些依赖项以及在何处下载。</span><span class="sxs-lookup"><span data-stu-id="ec95d-173">Refer to the [Prerequisites](#prerequisites) section to learn which dependencies you need to install and where to download them from.</span></span>

<span data-ttu-id="ec95d-174">如果项目同时支持 .NET Framework 和 .NET Core，可能需要面向较旧版本的 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="ec95d-174">You may need to target older versions of the .NET Framework when your project supports both the .NET Framework and .NET Core.</span></span> <span data-ttu-id="ec95d-175">在此方案中，如果要为较新目标使用较新的 API 和语言构造，请在代码中使用 `#if` 指令。</span><span class="sxs-lookup"><span data-stu-id="ec95d-175">In this scenario, if you want to use newer APIs and language constructs for the newer targets, use `#if` directives in your code.</span></span> <span data-ttu-id="ec95d-176">可能还需要为要面向的每个平台添加不同的包和依赖项，以包含每种情况所需的不同 API。</span><span class="sxs-lookup"><span data-stu-id="ec95d-176">You also might need to add different packages and dependencies for each platform you're targeting to include the different APIs needed for each case.</span></span>

<span data-ttu-id="ec95d-177">例如，假设有一个库，它通过 HTTP 执行联网操作。</span><span class="sxs-lookup"><span data-stu-id="ec95d-177">For example, let's say you have a library that performs networking operations over HTTP.</span></span> <span data-ttu-id="ec95d-178">对于 .NET Standard 和 .NET Framework 版本 4.5 或更高版本，可从 `System.Net.Http` 命名空间使用 `HttpClient` 类。</span><span class="sxs-lookup"><span data-stu-id="ec95d-178">For .NET Standard and the .NET Framework versions 4.5 or higher, you can use the `HttpClient` class from the `System.Net.Http` namespace.</span></span> <span data-ttu-id="ec95d-179">但是，.NET Framework 的早期版本没有 `HttpClient` 类，因此可对早期版本使用 `System.Net` 命名空间中的 `WebClient` 类。</span><span class="sxs-lookup"><span data-stu-id="ec95d-179">However, earlier versions of the .NET Framework don't have the `HttpClient` class, so you could use the `WebClient` class from the `System.Net` namespace for those instead.</span></span>

<span data-ttu-id="ec95d-180">项目文件可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="ec95d-180">Your project file could look like this:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFrameworks>netstandard1.4;net40;net45</TargetFrameworks>
  </PropertyGroup>

  <!-- Need to conditionally bring in references for the .NET Framework 4.0 target -->
  <ItemGroup Condition="'$(TargetFramework)' == 'net40'">
    <Reference Include="System.Net" />
  </ItemGroup>

  <!-- Need to conditionally bring in references for the .NET Framework 4.5 target -->
  <ItemGroup Condition="'$(TargetFramework)' == 'net45'">
    <Reference Include="System.Net.Http" />
    <Reference Include="System.Threading.Tasks" />
  </ItemGroup>
</Project>
```

<span data-ttu-id="ec95d-181">在此处可看到三项主要更改：</span><span class="sxs-lookup"><span data-stu-id="ec95d-181">You'll notice three major changes here:</span></span>

1. <span data-ttu-id="ec95d-182">`TargetFramework` 节点已替换为 `TargetFrameworks`，其中表示了三个 TFM。</span><span class="sxs-lookup"><span data-stu-id="ec95d-182">The `TargetFramework` node has been replaced by `TargetFrameworks`, and three TFMs are expressed inside.</span></span>
1. <span data-ttu-id="ec95d-183">`net40` 目标有一个 `<ItemGroup>` 节点，拉取一个 .NET Framework 引用。</span><span class="sxs-lookup"><span data-stu-id="ec95d-183">There is an `<ItemGroup>` node for the `net40` target pulling in one .NET Framework reference.</span></span>
1. <span data-ttu-id="ec95d-184">`net45` 目标中有一个 `<ItemGroup>` 节点，拉取两个 .NET Framework 引用。</span><span class="sxs-lookup"><span data-stu-id="ec95d-184">There is an `<ItemGroup>` node for the `net45` target pulling in two .NET Framework references.</span></span>

<span data-ttu-id="ec95d-185">生成系统可识别以下用在 `#if` 指令中的处理器符号：</span><span class="sxs-lookup"><span data-stu-id="ec95d-185">The build system is aware of the following preprocessor symbols used in `#if` directives:</span></span>

[!INCLUDE [Preprocessor symbols](../../../includes/preprocessor-symbols.md)]

<span data-ttu-id="ec95d-186">以下是使用每目标条件编译的示例：</span><span class="sxs-lookup"><span data-stu-id="ec95d-186">Here is an example making use of conditional compilation per-target:</span></span>

```csharp
using System;
using System.Text.RegularExpressions;
#if NET40
// This only compiles for the .NET Framework 4 targets
using System.Net;
#else
 // This compiles for all other targets
using System.Net.Http;
using System.Threading.Tasks;
#endif

namespace MultitargetLib
{
    public class Library
    {
#if NET40
        private readonly WebClient _client = new WebClient();
        private readonly object _locker = new object();
#else
        private readonly HttpClient _client = new HttpClient();
#endif

#if NET40
        // .NET Framework 4.0 does not have async/await
        public string GetDotNetCount()
        {
            string url = "https://www.dotnetfoundation.org/";

            var uri = new Uri(url);

            string result = "";

            // Lock here to provide thread-safety.
            lock(_locker)
            {
                result = _client.DownloadString(uri);
            }

            int dotNetCount = Regex.Matches(result, ".NET").Count;

            return $"Dotnet Foundation mentions .NET {dotNetCount} times!";
        }
#else
        // .NET 4.5+ can use async/await!
        public async Task<string> GetDotNetCountAsync()
        {
            string url = "https://www.dotnetfoundation.org/";

            // HttpClient is thread-safe, so no need to explicitly lock here
            var result = await _client.GetStringAsync(url);

            int dotNetCount = Regex.Matches(result, ".NET").Count;

            return $"dotnetfoundation.org mentions .NET {dotNetCount} times in its HTML!";
        }
#endif
    }
}
```

<span data-ttu-id="ec95d-187">如果使用 `dotnet build` 生成此项目，则在 `bin/` 文件夹下有三个目录：</span><span class="sxs-lookup"><span data-stu-id="ec95d-187">If you build this project with `dotnet build`, you'll notice three directories under the `bin/` folder:</span></span>

```
net40/
net45/
netstandard1.4/
```

<span data-ttu-id="ec95d-188">其中每个目录都包含每个目标的 `.dll` 文件。</span><span class="sxs-lookup"><span data-stu-id="ec95d-188">Each of these contain the `.dll` files for each target.</span></span>

## <a name="how-to-test-libraries-on-net-core"></a><span data-ttu-id="ec95d-189">如何在 .NET Core 上测试库</span><span class="sxs-lookup"><span data-stu-id="ec95d-189">How to test libraries on .NET Core</span></span>

<span data-ttu-id="ec95d-190">能够跨平台进行测试至关重要。</span><span class="sxs-lookup"><span data-stu-id="ec95d-190">It's important to be able to test across platforms.</span></span> <span data-ttu-id="ec95d-191">可使用现成的 [xUnit](https://xunit.github.io/) 或 MSTest。</span><span class="sxs-lookup"><span data-stu-id="ec95d-191">You can use either [xUnit](https://xunit.github.io/) or MSTest out of the box.</span></span> <span data-ttu-id="ec95d-192">它们都十分适合在 .NET Core 上对库进行单元测试。</span><span class="sxs-lookup"><span data-stu-id="ec95d-192">Both are perfectly suitable for unit testing your library on .NET Core.</span></span> <span data-ttu-id="ec95d-193">如何使用测试项目设置解决方案取决于[解决方案的结构](#structuring-a-solution)。</span><span class="sxs-lookup"><span data-stu-id="ec95d-193">How you set up your solution with test projects will depend on the [structure of your solution](#structuring-a-solution).</span></span> <span data-ttu-id="ec95d-194">下面的示例假设测试和源目录位于同一顶级目录下。</span><span class="sxs-lookup"><span data-stu-id="ec95d-194">The following example assumes that the test and source directories live in the same top-level directory.</span></span>

> [!NOTE]
> <span data-ttu-id="ec95d-195">此示例将使用某些 [.NET Core CLI](../tools/index.md) 命令。</span><span class="sxs-lookup"><span data-stu-id="ec95d-195">This uses some [.NET Core CLI](../tools/index.md) commands.</span></span> <span data-ttu-id="ec95d-196">有关详细信息，请参阅 [dotnet new](../tools/dotnet-new.md) 和 [dotnet sln](../tools/dotnet-sln.md)。</span><span class="sxs-lookup"><span data-stu-id="ec95d-196">See [dotnet new](../tools/dotnet-new.md) and [dotnet sln](../tools/dotnet-sln.md) for more information.</span></span>

1. <span data-ttu-id="ec95d-197">设置解决方案。</span><span class="sxs-lookup"><span data-stu-id="ec95d-197">Set up your solution.</span></span> <span data-ttu-id="ec95d-198">可使用以下命令实现此目的：</span><span class="sxs-lookup"><span data-stu-id="ec95d-198">You can do so with the following commands:</span></span>

   ```dotnetcli
   mkdir SolutionWithSrcAndTest
   cd SolutionWithSrcAndTest
   dotnet new sln
   dotnet new classlib -o MyProject
   dotnet new xunit -o MyProject.Test
   dotnet sln add MyProject/MyProject.csproj
   dotnet sln add MyProject.Test/MyProject.Test.csproj
   ```

   <span data-ttu-id="ec95d-199">这将创建多个项目，并一个解决方案中将这些项目链接在一起。</span><span class="sxs-lookup"><span data-stu-id="ec95d-199">This will create projects and link them together in a solution.</span></span> <span data-ttu-id="ec95d-200">`SolutionWithSrcAndTest` 的目录应如下所示：</span><span class="sxs-lookup"><span data-stu-id="ec95d-200">Your directory for `SolutionWithSrcAndTest` should look like this:</span></span>

   ```
   /SolutionWithSrcAndTest
   |__SolutionWithSrcAndTest.sln
   |__MyProject/
   |__MyProject.Test/
   ```

1. <span data-ttu-id="ec95d-201">导航到测试项目的目录，然后添加对 `MyProject` 中的 `MyProject.Test` 的引用。</span><span class="sxs-lookup"><span data-stu-id="ec95d-201">Navigate to the test project's directory and add a reference to `MyProject.Test` from `MyProject`.</span></span>

   ```dotnetcli
   cd MyProject.Test
   dotnet add reference ../MyProject/MyProject.csproj
   ```

1. <span data-ttu-id="ec95d-202">还原包和生成项目：</span><span class="sxs-lookup"><span data-stu-id="ec95d-202">Restore packages and build projects:</span></span>

   ```dotnetcli
   dotnet restore
   dotnet build
   ```

   [!INCLUDE[DotNet Restore Note](../../../includes/dotnet-restore-note.md)]

1. <span data-ttu-id="ec95d-203">执行 `dotnet test` 命令，验证 xUnit 是否在运行。</span><span class="sxs-lookup"><span data-stu-id="ec95d-203">Verify that xUnit runs by executing the `dotnet test` command.</span></span> <span data-ttu-id="ec95d-204">如果选择使用 MSTest，则应改为运行 MSTest 控制台运行程序。</span><span class="sxs-lookup"><span data-stu-id="ec95d-204">If you chose to use MSTest, then the MSTest console runner should run instead.</span></span>

<span data-ttu-id="ec95d-205">大功告成！</span><span class="sxs-lookup"><span data-stu-id="ec95d-205">And that's it!</span></span> <span data-ttu-id="ec95d-206">现在可以使用命令行工具跨所有平台测试库。</span><span class="sxs-lookup"><span data-stu-id="ec95d-206">You can now test your library across all platforms using command-line tools.</span></span> <span data-ttu-id="ec95d-207">若要继续测试，现已设置好了所有内容，测试库将非常简单：</span><span class="sxs-lookup"><span data-stu-id="ec95d-207">To continue testing now that you have everything set up, testing your library is very simple:</span></span>

1. <span data-ttu-id="ec95d-208">对库进行更改。</span><span class="sxs-lookup"><span data-stu-id="ec95d-208">Make changes to your library.</span></span>
1. <span data-ttu-id="ec95d-209">使用 `dotnet test` 命令在测试目录中从命令行运行测试。</span><span class="sxs-lookup"><span data-stu-id="ec95d-209">Run tests from the command line, in your test directory, with `dotnet test` command.</span></span>

<span data-ttu-id="ec95d-210">调用 `dotnet test` 命令时，将自动重新生成代码。</span><span class="sxs-lookup"><span data-stu-id="ec95d-210">Your code will be automatically rebuilt when you invoke `dotnet test` command.</span></span>

## <a name="how-to-use-multiple-projects"></a><span data-ttu-id="ec95d-211">如何使用多个项目</span><span class="sxs-lookup"><span data-stu-id="ec95d-211">How to use multiple projects</span></span>

<span data-ttu-id="ec95d-212">对于较大的库，通常需要将功能置于不同项目中。</span><span class="sxs-lookup"><span data-stu-id="ec95d-212">A common need for larger libraries is to place functionality in different projects.</span></span>

<span data-ttu-id="ec95d-213">假设要生成一个可以惯用的 C# 和 F# 使用的库。</span><span class="sxs-lookup"><span data-stu-id="ec95d-213">Imagine you want to build a library that could be consumed in idiomatic C# and F#.</span></span> <span data-ttu-id="ec95d-214">这意味着库的使用者可通过对 C# 或 F# 来说很自然的方式来使用它。</span><span class="sxs-lookup"><span data-stu-id="ec95d-214">That would mean that consumers of your library consume it in ways that are natural to C# or F#.</span></span> <span data-ttu-id="ec95d-215">例如，在 C# 中，了能会这样使用库：</span><span class="sxs-lookup"><span data-stu-id="ec95d-215">For example, in C# you might consume the library like this:</span></span>

```csharp
using AwesomeLibrary.CSharp;

public Task DoThings(Data data)
{
    var convertResult = await AwesomeLibrary.ConvertAsync(data);
    var result = AwesomeLibrary.Process(convertResult);
    // do something with result
}
```

<span data-ttu-id="ec95d-216">在 F# 中可能是这样：</span><span class="sxs-lookup"><span data-stu-id="ec95d-216">In F#, it might look like this:</span></span>

```fsharp
open AwesomeLibrary.FSharp

let doWork data = async {
    let! result = AwesomeLibrary.AsyncConvert data // Uses an F# async function rather than C# async method
    // do something with result
}
```

<span data-ttu-id="ec95d-217">这样的使用方案意味着被访问的 API 必须具有用于 C# 和 F# 的不同结构。</span><span class="sxs-lookup"><span data-stu-id="ec95d-217">Consumption scenarios like this mean that the APIs being accessed have to have a different structure for C# and F#.</span></span>  <span data-ttu-id="ec95d-218">通常的方法是将库的所有逻辑因子转化到核心项目中，C# 和 F# 项目定义调用到核心项目的 API 层。</span><span class="sxs-lookup"><span data-stu-id="ec95d-218">A common approach to accomplishing this is to factor all of the logic of a library into a core project, with C# and F# projects defining the API layers that call into that core project.</span></span>  <span data-ttu-id="ec95d-219">该部分的其余部分将使用以下名称：</span><span class="sxs-lookup"><span data-stu-id="ec95d-219">The rest of the section will use the following names:</span></span>

* <span data-ttu-id="ec95d-220">**AwesomeLibrary.Core** - 核心项目，其中包含库的所有逻辑</span><span class="sxs-lookup"><span data-stu-id="ec95d-220">**AwesomeLibrary.Core** - A core project that contains all logic for the library</span></span>
* <span data-ttu-id="ec95d-221">**AwesomeLibrary.CSharp** - 具有打算在 C# 中使用的公共 API 的项目</span><span class="sxs-lookup"><span data-stu-id="ec95d-221">**AwesomeLibrary.CSharp** - A project with public APIs intended for consumption in C#</span></span>
* <span data-ttu-id="ec95d-222">**AwesomeLibrary.FSharp** - 具有打算在 F# 中使用的公共 API 的项目</span><span class="sxs-lookup"><span data-stu-id="ec95d-222">**AwesomeLibrary.FSharp** - A project with public APIs intended for consumption in F#</span></span>

<span data-ttu-id="ec95d-223">可在终端运行下列命令，生成与下列指南相同的结构：</span><span class="sxs-lookup"><span data-stu-id="ec95d-223">You can run the following commands in your terminal to produce the same structure as this guide:</span></span>

```dotnetcli
mkdir AwesomeLibrary && cd AwesomeLibrary
dotnet new sln
mkdir AwesomeLibrary.Core && cd AwesomeLibrary.Core && dotnet new classlib
cd ..
mkdir AwesomeLibrary.CSharp && cd AwesomeLibrary.CSharp && dotnet new classlib
cd ..
mkdir AwesomeLibrary.FSharp && cd AwesomeLibrary.FSharp && dotnet new classlib -lang "F#"
cd ..
dotnet sln add AwesomeLibrary.Core/AwesomeLibrary.Core.csproj
dotnet sln add AwesomeLibrary.CSharp/AwesomeLibrary.CSharp.csproj
dotnet sln add AwesomeLibrary.FSharp/AwesomeLibrary.FSharp.fsproj
```

<span data-ttu-id="ec95d-224">这将添加上述三个项目和将它们链接在一起的解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="ec95d-224">This will add the three projects above and a solution file that links them together.</span></span> <span data-ttu-id="ec95d-225">创建解决方案文件并链接项目后，可从顶级还原和生成项目。</span><span class="sxs-lookup"><span data-stu-id="ec95d-225">Creating the solution file and linking projects will allow you to restore and build projects from a top level.</span></span>

### <a name="project-to-project-referencing"></a><span data-ttu-id="ec95d-226">项目到项目的引用</span><span class="sxs-lookup"><span data-stu-id="ec95d-226">Project-to-project referencing</span></span>

<span data-ttu-id="ec95d-227">引用项目的最佳方式是使用 .NET Core CLI 添加项目引用。</span><span class="sxs-lookup"><span data-stu-id="ec95d-227">The best way to reference a project is to use the .NET Core CLI to add a project reference.</span></span> <span data-ttu-id="ec95d-228">在 AwesomeLibrary.CSharp  和 AwesomeLibrary.FSharp  项目目录中，可运行下列命令：</span><span class="sxs-lookup"><span data-stu-id="ec95d-228">From the **AwesomeLibrary.CSharp** and **AwesomeLibrary.FSharp** project directories, you can run the following command:</span></span>

```dotnetcli
dotnet add reference ../AwesomeLibrary.Core/AwesomeLibrary.Core.csproj
```

<span data-ttu-id="ec95d-229">AwesomeLibrary.CSharp  和 AwesomeLibrary.FSharp  的项目文件现在需要将 AwesomeLibrary.Core  作为 `ProjectReference` 目标引用。</span><span class="sxs-lookup"><span data-stu-id="ec95d-229">The project files for both **AwesomeLibrary.CSharp** and **AwesomeLibrary.FSharp** will now reference **AwesomeLibrary.Core** as a `ProjectReference` target.</span></span>  <span data-ttu-id="ec95d-230">可通过检查项目文件和查看其中的下列内容来进行验证：</span><span class="sxs-lookup"><span data-stu-id="ec95d-230">You can verify this by inspecting the project files and seeing the following in them:</span></span>

```xml
<ItemGroup>
  <ProjectReference Include="..\AwesomeLibrary.Core\AwesomeLibrary.Core.csproj" />
</ItemGroup>
```

<span data-ttu-id="ec95d-231">如果不想使用 .NET Core CLI，可手动将此部分添加到每个项目文件。</span><span class="sxs-lookup"><span data-stu-id="ec95d-231">You can add this section to each project file manually if you prefer not to use the .NET Core CLI.</span></span>

### <a name="structuring-a-solution"></a><span data-ttu-id="ec95d-232">结构化解决方案</span><span class="sxs-lookup"><span data-stu-id="ec95d-232">Structuring a solution</span></span>

<span data-ttu-id="ec95d-233">多项目解决方案的另一个重要方面是建立良好的整体项目结构。</span><span class="sxs-lookup"><span data-stu-id="ec95d-233">Another important aspect of multi-project solutions is establishing a good overall project structure.</span></span> <span data-ttu-id="ec95d-234">可根据自己的喜好随意组织代码，只要使用 `dotnet sln add` 将每个项目链接到解决方案文件，就可在解决方案级别运行 `dotnet restore` 和 `dotnet build`。</span><span class="sxs-lookup"><span data-stu-id="ec95d-234">You can organize code however you like, and as long as you link each project to your solution file with `dotnet sln add`, you will be able to run `dotnet restore` and `dotnet build` at the solution level.</span></span>
