---
title: SDK 样式项目中的目标框架 - .NET
description: 了解用于 .NET 应用和库的目标框架。
ms.date: 09/08/2020
ms.custom: updateeachrelease
ms.technology: dotnet-standard
ms.openlocfilehash: 85bc05f07cfcc5f59a8a27790ee3d78a497cecdc
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223462"
---
# <a name="target-frameworks-in-sdk-style-projects"></a><span data-ttu-id="0f9df-103">SDK 样式项目中的目标框架</span><span class="sxs-lookup"><span data-stu-id="0f9df-103">Target frameworks in SDK-style projects</span></span>

<span data-ttu-id="0f9df-104">以应用或库中的框架为目标时，需要指定想要向应用或库提供的 API 集。</span><span class="sxs-lookup"><span data-stu-id="0f9df-104">When you target a framework in an app or library, you're specifying the set of APIs that you'd like to make available to the app or library.</span></span> <span data-ttu-id="0f9df-105">使用目标框架名字对象 (TFM) 在项目文件中指定目标框架。</span><span class="sxs-lookup"><span data-stu-id="0f9df-105">You specify the target framework in your project file using target framework monikers (TFMs).</span></span>

<span data-ttu-id="0f9df-106">应用或库可以使用 [.NET Standard](net-standard.md) 版本作为目标。</span><span class="sxs-lookup"><span data-stu-id="0f9df-106">An app or library can target a version of [.NET Standard](net-standard.md).</span></span> <span data-ttu-id="0f9df-107">.NET Standard 版本表示所有 .NET 实现中的标准化 API 集。</span><span class="sxs-lookup"><span data-stu-id="0f9df-107">.NET Standard versions represent standardized sets of APIs across all .NET implementations.</span></span> <span data-ttu-id="0f9df-108">例如，库可以使用 .NET Standard 1.6 作为目标，并获得对可使用相同基本代码跨 .NET Core 和 .NET Framework 工作的 API 的访问权限。</span><span class="sxs-lookup"><span data-stu-id="0f9df-108">For example, a library can target .NET Standard 1.6 and gain access to APIs that function across .NET Core and .NET Framework using the same codebase.</span></span>

<span data-ttu-id="0f9df-109">应用或库还能以一个特定 .NET 实现为目标，获得特定于实现的 API 的访问权限。</span><span class="sxs-lookup"><span data-stu-id="0f9df-109">An app or library can also target a specific .NET implementation to gain access to implementation-specific APIs.</span></span> <span data-ttu-id="0f9df-110">例如，面向 Xamarin.iOS 的应用（如 `Xamarin.iOS10`）有权访问 Xamarin 提供的适用于 iOS 10 的 iOS API 包装器；面向通用 Windows 平台 (UWP) 的应用（如 `uap10.0`）有权访问为运行 Windows 10 的设备编译的 API。</span><span class="sxs-lookup"><span data-stu-id="0f9df-110">For example, an app that targets Xamarin.iOS (for example, `Xamarin.iOS10`) has access to Xamarin-provided iOS API wrappers for iOS 10, or an app that targets Universal Windows Platform (UWP, `uap10.0`) has access to APIs that compile for devices that run Windows 10.</span></span>

<span data-ttu-id="0f9df-111">对于某些目标框架（例如 .NET Framework），API 由框架在系统上安装的程序集定义，并且可能包括应用程序框架 API（例如 ASP.NET）。</span><span class="sxs-lookup"><span data-stu-id="0f9df-111">For some target frameworks (for example, .NET Framework), the APIs are defined by the assemblies that the framework installs on a system and may include application framework APIs (for example, ASP.NET).</span></span>

<span data-ttu-id="0f9df-112">对于基于包的目标框架（例如 .NET Standard 和 .NET Core），API 由包含在应用或库中的包定义。</span><span class="sxs-lookup"><span data-stu-id="0f9df-112">For package-based target frameworks (for example, .NET Standard and .NET Core), the APIs are defined by the packages included in the app or library.</span></span> <span data-ttu-id="0f9df-113">元包  是一个 NuGet 包，NuGet 包本身不包含任何内容，只是一个依赖项列表（其他包）。</span><span class="sxs-lookup"><span data-stu-id="0f9df-113">A *metapackage* is a NuGet package that has no content of its own but is a list of dependencies (other packages).</span></span> <span data-ttu-id="0f9df-114">基于 NuGet 包的目标框架隐式指定一个元包，该元包引用一起构成框架的所有包。</span><span class="sxs-lookup"><span data-stu-id="0f9df-114">A NuGet package-based target framework implicitly specifies a metapackage that references all the packages that together make up the framework.</span></span>

## <a name="latest-versions"></a><span data-ttu-id="0f9df-115">最新版本</span><span class="sxs-lookup"><span data-stu-id="0f9df-115">Latest versions</span></span>

<span data-ttu-id="0f9df-116">下表定义了最常见的目标框架、如何引用这些框架，以及它们实现的 [.NET Standard](net-standard.md) 版本。</span><span class="sxs-lookup"><span data-stu-id="0f9df-116">The following table defines the most common target frameworks, how they're referenced, and which version of [.NET Standard](net-standard.md) they implement.</span></span> <span data-ttu-id="0f9df-117">这些目标框架版本是最新的稳定版本。</span><span class="sxs-lookup"><span data-stu-id="0f9df-117">These target framework versions are the latest stable versions.</span></span> <span data-ttu-id="0f9df-118">预览版不会显示。</span><span class="sxs-lookup"><span data-stu-id="0f9df-118">Pre-release versions aren't shown.</span></span> <span data-ttu-id="0f9df-119">目标框架名字对象 (TFM) 是一个标准化令牌格式，用于指定 .NET 应用或库的目标框架。</span><span class="sxs-lookup"><span data-stu-id="0f9df-119">A target framework moniker (TFM) is a standardized token format for specifying the target framework of a .NET app or library.</span></span>

| <span data-ttu-id="0f9df-120">目标框架</span><span class="sxs-lookup"><span data-stu-id="0f9df-120">Target framework</span></span>      | <span data-ttu-id="0f9df-121">最新</span><span class="sxs-lookup"><span data-stu-id="0f9df-121">Latest</span></span> <br/> <span data-ttu-id="0f9df-122">稳定版本</span><span class="sxs-lookup"><span data-stu-id="0f9df-122">stable version</span></span> | <span data-ttu-id="0f9df-123">目标框架名字对象 (TFM)</span><span class="sxs-lookup"><span data-stu-id="0f9df-123">Target framework moniker (TFM)</span></span> | <span data-ttu-id="0f9df-124">已实现</span><span class="sxs-lookup"><span data-stu-id="0f9df-124">Implemented</span></span> <br/> <span data-ttu-id="0f9df-125">.NET Standard 版本</span><span class="sxs-lookup"><span data-stu-id="0f9df-125">.NET Standard version</span></span> |
| :-: | :-: | :-: | :-: |
| <span data-ttu-id="0f9df-126">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="0f9df-126">.NET Standard</span></span>         | <span data-ttu-id="0f9df-127">2.1</span><span class="sxs-lookup"><span data-stu-id="0f9df-127">2.1</span></span>                         | <span data-ttu-id="0f9df-128">netstandard2.1</span><span class="sxs-lookup"><span data-stu-id="0f9df-128">netstandard2.1</span></span>                 | <span data-ttu-id="0f9df-129">空值</span><span class="sxs-lookup"><span data-stu-id="0f9df-129">N/A</span></span>                                     |
| <span data-ttu-id="0f9df-130">.NET Core</span><span class="sxs-lookup"><span data-stu-id="0f9df-130">.NET Core</span></span>             | <span data-ttu-id="0f9df-131">3.1</span><span class="sxs-lookup"><span data-stu-id="0f9df-131">3.1</span></span>                         | <span data-ttu-id="0f9df-132">netcoreapp3.1</span><span class="sxs-lookup"><span data-stu-id="0f9df-132">netcoreapp3.1</span></span>                  | <span data-ttu-id="0f9df-133">2.1</span><span class="sxs-lookup"><span data-stu-id="0f9df-133">2.1</span></span>                                     |
| <span data-ttu-id="0f9df-134">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="0f9df-134">.NET Framework</span></span>        | <span data-ttu-id="0f9df-135">4.8</span><span class="sxs-lookup"><span data-stu-id="0f9df-135">4.8</span></span>                         | <span data-ttu-id="0f9df-136">net48</span><span class="sxs-lookup"><span data-stu-id="0f9df-136">net48</span></span>                          | <span data-ttu-id="0f9df-137">2.0</span><span class="sxs-lookup"><span data-stu-id="0f9df-137">2.0</span></span>                                     |

## <a name="supported-target-frameworks"></a><span data-ttu-id="0f9df-138">支持的目标框架</span><span class="sxs-lookup"><span data-stu-id="0f9df-138">Supported target frameworks</span></span>

<span data-ttu-id="0f9df-139">目标框架通常由 TFM 引用。</span><span class="sxs-lookup"><span data-stu-id="0f9df-139">A target framework is typically referenced by a TFM.</span></span> <span data-ttu-id="0f9df-140">下表显示 .NET SDK 和 NuGet 客户端支持的目标框架。</span><span class="sxs-lookup"><span data-stu-id="0f9df-140">The following table shows the target frameworks supported by the .NET SDK and the NuGet client.</span></span> <span data-ttu-id="0f9df-141">等效项显示在括号内。</span><span class="sxs-lookup"><span data-stu-id="0f9df-141">Equivalents are shown within brackets.</span></span> <span data-ttu-id="0f9df-142">例如，`win81` 对于 `netcore451` 来说等效于 TFM。</span><span class="sxs-lookup"><span data-stu-id="0f9df-142">For example, `win81` is an equivalent TFM to `netcore451`.</span></span>

| <span data-ttu-id="0f9df-143">目标 Framework</span><span class="sxs-lookup"><span data-stu-id="0f9df-143">Target Framework</span></span>           | <span data-ttu-id="0f9df-144">TFM</span><span class="sxs-lookup"><span data-stu-id="0f9df-144">TFM</span></span> |
| -------------------------- | --- |
| <span data-ttu-id="0f9df-145">.NET 5（和 .NET Core）</span><span class="sxs-lookup"><span data-stu-id="0f9df-145">.NET 5 (and .NET Core)</span></span>     | <span data-ttu-id="0f9df-146">netcoreapp1.0</span><span class="sxs-lookup"><span data-stu-id="0f9df-146">netcoreapp1.0</span></span><br><span data-ttu-id="0f9df-147">netcoreapp1.1</span><span class="sxs-lookup"><span data-stu-id="0f9df-147">netcoreapp1.1</span></span><br><span data-ttu-id="0f9df-148">netcoreapp2.0</span><span class="sxs-lookup"><span data-stu-id="0f9df-148">netcoreapp2.0</span></span><br><span data-ttu-id="0f9df-149">netcoreapp2.1</span><span class="sxs-lookup"><span data-stu-id="0f9df-149">netcoreapp2.1</span></span><br><span data-ttu-id="0f9df-150">netcoreapp2.2</span><span class="sxs-lookup"><span data-stu-id="0f9df-150">netcoreapp2.2</span></span><br><span data-ttu-id="0f9df-151">netcoreapp3.0</span><span class="sxs-lookup"><span data-stu-id="0f9df-151">netcoreapp3.0</span></span><br><span data-ttu-id="0f9df-152">netcoreapp3.1</span><span class="sxs-lookup"><span data-stu-id="0f9df-152">netcoreapp3.1</span></span><br><span data-ttu-id="0f9df-153">net5.0\*</span><span class="sxs-lookup"><span data-stu-id="0f9df-153">net5.0\*</span></span> |
| <span data-ttu-id="0f9df-154">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="0f9df-154">.NET Standard</span></span>              | <span data-ttu-id="0f9df-155">netstandard1.0</span><span class="sxs-lookup"><span data-stu-id="0f9df-155">netstandard1.0</span></span><br><span data-ttu-id="0f9df-156">netstandard1.1</span><span class="sxs-lookup"><span data-stu-id="0f9df-156">netstandard1.1</span></span><br><span data-ttu-id="0f9df-157">netstandard1.2</span><span class="sxs-lookup"><span data-stu-id="0f9df-157">netstandard1.2</span></span><br><span data-ttu-id="0f9df-158">netstandard1.3</span><span class="sxs-lookup"><span data-stu-id="0f9df-158">netstandard1.3</span></span><br><span data-ttu-id="0f9df-159">netstandard1.4</span><span class="sxs-lookup"><span data-stu-id="0f9df-159">netstandard1.4</span></span><br><span data-ttu-id="0f9df-160">netstandard1.5</span><span class="sxs-lookup"><span data-stu-id="0f9df-160">netstandard1.5</span></span><br><span data-ttu-id="0f9df-161">netstandard1.6</span><span class="sxs-lookup"><span data-stu-id="0f9df-161">netstandard1.6</span></span><br><span data-ttu-id="0f9df-162">netstandard2.0</span><span class="sxs-lookup"><span data-stu-id="0f9df-162">netstandard2.0</span></span><br><span data-ttu-id="0f9df-163">netstandard2.1</span><span class="sxs-lookup"><span data-stu-id="0f9df-163">netstandard2.1</span></span> |
| <span data-ttu-id="0f9df-164">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="0f9df-164">.NET Framework</span></span>             | <span data-ttu-id="0f9df-165">net11</span><span class="sxs-lookup"><span data-stu-id="0f9df-165">net11</span></span><br><span data-ttu-id="0f9df-166">net20</span><span class="sxs-lookup"><span data-stu-id="0f9df-166">net20</span></span><br><span data-ttu-id="0f9df-167">net35</span><span class="sxs-lookup"><span data-stu-id="0f9df-167">net35</span></span><br><span data-ttu-id="0f9df-168">net40</span><span class="sxs-lookup"><span data-stu-id="0f9df-168">net40</span></span><br><span data-ttu-id="0f9df-169">net403</span><span class="sxs-lookup"><span data-stu-id="0f9df-169">net403</span></span><br><span data-ttu-id="0f9df-170">net45</span><span class="sxs-lookup"><span data-stu-id="0f9df-170">net45</span></span><br><span data-ttu-id="0f9df-171">net451</span><span class="sxs-lookup"><span data-stu-id="0f9df-171">net451</span></span><br><span data-ttu-id="0f9df-172">net452</span><span class="sxs-lookup"><span data-stu-id="0f9df-172">net452</span></span><br><span data-ttu-id="0f9df-173">net46</span><span class="sxs-lookup"><span data-stu-id="0f9df-173">net46</span></span><br><span data-ttu-id="0f9df-174">net461</span><span class="sxs-lookup"><span data-stu-id="0f9df-174">net461</span></span><br><span data-ttu-id="0f9df-175">net462</span><span class="sxs-lookup"><span data-stu-id="0f9df-175">net462</span></span><br><span data-ttu-id="0f9df-176">net47</span><span class="sxs-lookup"><span data-stu-id="0f9df-176">net47</span></span><br><span data-ttu-id="0f9df-177">net471</span><span class="sxs-lookup"><span data-stu-id="0f9df-177">net471</span></span><br><span data-ttu-id="0f9df-178">net472</span><span class="sxs-lookup"><span data-stu-id="0f9df-178">net472</span></span><br><span data-ttu-id="0f9df-179">net48</span><span class="sxs-lookup"><span data-stu-id="0f9df-179">net48</span></span> |
| <span data-ttu-id="0f9df-180">Windows 应用商店</span><span class="sxs-lookup"><span data-stu-id="0f9df-180">Windows Store</span></span>              | <span data-ttu-id="0f9df-181">netcore [netcore45]</span><span class="sxs-lookup"><span data-stu-id="0f9df-181">netcore [netcore45]</span></span><br><span data-ttu-id="0f9df-182">netcore45 [win] [win8]</span><span class="sxs-lookup"><span data-stu-id="0f9df-182">netcore45 [win] [win8]</span></span><br><span data-ttu-id="0f9df-183">netcore451 [win81]</span><span class="sxs-lookup"><span data-stu-id="0f9df-183">netcore451 [win81]</span></span> |
| <span data-ttu-id="0f9df-184">.NET Micro Framework</span><span class="sxs-lookup"><span data-stu-id="0f9df-184">.NET Micro Framework</span></span>       | <span data-ttu-id="0f9df-185">netmf</span><span class="sxs-lookup"><span data-stu-id="0f9df-185">netmf</span></span> |
| <span data-ttu-id="0f9df-186">Silverlight</span><span class="sxs-lookup"><span data-stu-id="0f9df-186">Silverlight</span></span>                | <span data-ttu-id="0f9df-187">sl4</span><span class="sxs-lookup"><span data-stu-id="0f9df-187">sl4</span></span><br><span data-ttu-id="0f9df-188">sl5</span><span class="sxs-lookup"><span data-stu-id="0f9df-188">sl5</span></span> |
| <span data-ttu-id="0f9df-189">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="0f9df-189">Windows Phone</span></span>              | <span data-ttu-id="0f9df-190">wp [wp7]</span><span class="sxs-lookup"><span data-stu-id="0f9df-190">wp [wp7]</span></span><br><span data-ttu-id="0f9df-191">wp7</span><span class="sxs-lookup"><span data-stu-id="0f9df-191">wp7</span></span><br><span data-ttu-id="0f9df-192">wp75</span><span class="sxs-lookup"><span data-stu-id="0f9df-192">wp75</span></span><br><span data-ttu-id="0f9df-193">wp8</span><span class="sxs-lookup"><span data-stu-id="0f9df-193">wp8</span></span><br><span data-ttu-id="0f9df-194">wp81</span><span class="sxs-lookup"><span data-stu-id="0f9df-194">wp81</span></span><br><span data-ttu-id="0f9df-195">wpa81</span><span class="sxs-lookup"><span data-stu-id="0f9df-195">wpa81</span></span> |
| <span data-ttu-id="0f9df-196">通用 Windows 平台</span><span class="sxs-lookup"><span data-stu-id="0f9df-196">Universal Windows Platform</span></span> | <span data-ttu-id="0f9df-197">uap [uap10.0]</span><span class="sxs-lookup"><span data-stu-id="0f9df-197">uap [uap10.0]</span></span><br><span data-ttu-id="0f9df-198">uap10.0 [win10] [netcore50]</span><span class="sxs-lookup"><span data-stu-id="0f9df-198">uap10.0 [win10] [netcore50]</span></span> |

<span data-ttu-id="0f9df-199">\* .NET 5.0 及更高版本的 TFM 包含特定于 OS 的变体。</span><span class="sxs-lookup"><span data-stu-id="0f9df-199">\* .NET 5.0 and later TFMs include OS-specific variations.</span></span> <span data-ttu-id="0f9df-200">有关详细信息，请参阅下一节：[.NET 5 特定于 OS 的 TFM](#net-5-os-specific-tfms)。</span><span class="sxs-lookup"><span data-stu-id="0f9df-200">For more information, see the following section, [.NET 5 OS-specific TFMs](#net-5-os-specific-tfms).</span></span>

### <a name="net-5-os-specific-tfms"></a><span data-ttu-id="0f9df-201">.NET 5 特定于 OS 的 TFM</span><span class="sxs-lookup"><span data-stu-id="0f9df-201">.NET 5 OS-specific TFMs</span></span>

<span data-ttu-id="0f9df-202">对于每个 .NET 5.0 及更高版本的 TFM（例如 `net5.0`），都存在包含特定于 OS 的绑定的 TFM 变体。</span><span class="sxs-lookup"><span data-stu-id="0f9df-202">For each .NET 5.0 and later TFM, for example, `net5.0`, there are TFM variations that include OS-specific bindings.</span></span> <span data-ttu-id="0f9df-203">下表中显示了这些变体。</span><span class="sxs-lookup"><span data-stu-id="0f9df-203">These variations are shown in the following table.</span></span>

| <span data-ttu-id="0f9df-204">特定于 OS 的格式</span><span class="sxs-lookup"><span data-stu-id="0f9df-204">OS-specific format</span></span> | <span data-ttu-id="0f9df-205">示例</span><span class="sxs-lookup"><span data-stu-id="0f9df-205">Example</span></span>        |
|--------------------|----------------|
| <span data-ttu-id="0f9df-206">\<base-tfm>-android</span><span class="sxs-lookup"><span data-stu-id="0f9df-206">\<base-tfm>-android</span></span> | <span data-ttu-id="0f9df-207">net5.0-android</span><span class="sxs-lookup"><span data-stu-id="0f9df-207">net5.0-android</span></span> |
| <span data-ttu-id="0f9df-208">\<base-tfm>-ios</span><span class="sxs-lookup"><span data-stu-id="0f9df-208">\<base-tfm>-ios</span></span>     | <span data-ttu-id="0f9df-209">net5.0-ios</span><span class="sxs-lookup"><span data-stu-id="0f9df-209">net5.0-ios</span></span>     |
| <span data-ttu-id="0f9df-210">\<base-tfm>-macos</span><span class="sxs-lookup"><span data-stu-id="0f9df-210">\<base-tfm>-macos</span></span>   | <span data-ttu-id="0f9df-211">net5.0-macos</span><span class="sxs-lookup"><span data-stu-id="0f9df-211">net5.0-macos</span></span>   |
| <span data-ttu-id="0f9df-212">\<base-tfm>-tvos</span><span class="sxs-lookup"><span data-stu-id="0f9df-212">\<base-tfm>-tvos</span></span>    | <span data-ttu-id="0f9df-213">net5.0-tvos</span><span class="sxs-lookup"><span data-stu-id="0f9df-213">net5.0-tvos</span></span>    |
| <span data-ttu-id="0f9df-214">\<base-tfm>-watchos</span><span class="sxs-lookup"><span data-stu-id="0f9df-214">\<base-tfm>-watchos</span></span> | <span data-ttu-id="0f9df-215">net5.0-watchos</span><span class="sxs-lookup"><span data-stu-id="0f9df-215">net5.0-watchos</span></span> |
| <span data-ttu-id="0f9df-216">\<base-tfm>-windows</span><span class="sxs-lookup"><span data-stu-id="0f9df-216">\<base-tfm>-windows</span></span> | <span data-ttu-id="0f9df-217">net5.0-windows</span><span class="sxs-lookup"><span data-stu-id="0f9df-217">net5.0-windows</span></span> |

<span data-ttu-id="0f9df-218">你还可以指定可选的 OS 版本，例如 `net5.0-ios12.0`。</span><span class="sxs-lookup"><span data-stu-id="0f9df-218">You can also specify an optional OS version, for example, `net5.0-ios12.0`.</span></span>

<span data-ttu-id="0f9df-219">有关 .NET 5 TFM 的详细信息，请参阅 [.NET 5 中的目标框架名称](https://github.com/dotnet/designs/blob/master/accepted/2020/net5/net5.md)。</span><span class="sxs-lookup"><span data-stu-id="0f9df-219">For more information about .NET 5 TFMs, see [Target framework names in .NET 5](https://github.com/dotnet/designs/blob/master/accepted/2020/net5/net5.md).</span></span>

## <a name="how-to-specify-a-target-framework"></a><span data-ttu-id="0f9df-220">如何指定目标框架</span><span class="sxs-lookup"><span data-stu-id="0f9df-220">How to specify a target framework</span></span>

<span data-ttu-id="0f9df-221">在项目文件中指定目标框架。</span><span class="sxs-lookup"><span data-stu-id="0f9df-221">Target frameworks are specified in a project file.</span></span> <span data-ttu-id="0f9df-222">指定单个目标框架时，使用 TargetFramework  元素。</span><span class="sxs-lookup"><span data-stu-id="0f9df-222">When a single target framework is specified, use the **TargetFramework** element.</span></span> <span data-ttu-id="0f9df-223">以下控制台应用项目文件演示了如何面向 .NET 5.0：</span><span class="sxs-lookup"><span data-stu-id="0f9df-223">The following console app project file demonstrates how to target .NET 5.0:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net5.0</TargetFramework>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="0f9df-224">指定多个目标框架时，可有条件地为每个目标框架引用程序集。</span><span class="sxs-lookup"><span data-stu-id="0f9df-224">When you specify multiple target frameworks, you may conditionally reference assemblies for each target framework.</span></span> <span data-ttu-id="0f9df-225">在代码中，可使用具有 -if-then-else  逻辑的预处理器符号，有条件地针对这些程序集进行编译。</span><span class="sxs-lookup"><span data-stu-id="0f9df-225">In your code, you can conditionally compile against those assemblies by using preprocessor symbols with *if-then-else* logic.</span></span>

<span data-ttu-id="0f9df-226">以下库项目面向 .NET Standard (`netstandard1.4`) 和 .NET Framework（`net40` 和 `net45`）的 API。</span><span class="sxs-lookup"><span data-stu-id="0f9df-226">The following library project targets APIs of .NET Standard (`netstandard1.4`) and .NET Framework (`net40` and `net45`).</span></span> <span data-ttu-id="0f9df-227">将复数形式的 TargetFrameworks  元素与多个目标框架一起使用。</span><span class="sxs-lookup"><span data-stu-id="0f9df-227">Use the plural **TargetFrameworks** element with multiple target frameworks.</span></span> <span data-ttu-id="0f9df-228">为两个 .NET Framework TFM 编译库时，`Condition` 属性包括特定于实现的包：</span><span class="sxs-lookup"><span data-stu-id="0f9df-228">The `Condition` attributes include implementation-specific packages when the library is compiled for the two .NET Framework TFMs:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard1.4;net40;net45</TargetFrameworks>
  </PropertyGroup>

  <!-- Conditionally obtain references for the .NET Framework 4.0 target -->
  <ItemGroup Condition=" '$(TargetFramework)' == 'net40' ">
    <Reference Include="System.Net" />
  </ItemGroup>

  <!-- Conditionally obtain references for the .NET Framework 4.5 target -->
  <ItemGroup Condition=" '$(TargetFramework)' == 'net45' ">
    <Reference Include="System.Net.Http" />
    <Reference Include="System.Threading.Tasks" />
  </ItemGroup>

</Project>
```

<span data-ttu-id="0f9df-229">在库或应用中，使用[预处理器指令](../csharp/language-reference/preprocessor-directives/preprocessor-if.md)编写条件代码，针对每个目标框架进行编译：</span><span class="sxs-lookup"><span data-stu-id="0f9df-229">Within your library or app, you write conditional code using [preprocessor directives](../csharp/language-reference/preprocessor-directives/preprocessor-if.md) to compile for each target framework:</span></span>

```csharp
public class MyClass
{
    static void Main()
    {
#if NET40
        Console.WriteLine("Target framework: .NET Framework 4.0");
#elif NET45
        Console.WriteLine("Target framework: .NET Framework 4.5");
#else
        Console.WriteLine("Target framework: .NET Standard 1.4");
#endif
    }
}
```

<span data-ttu-id="0f9df-230">使用 SDK 样式项目时，生成系统可识别预处理器符号，这些符号表示[支持的目标框架版本](#supported-target-frameworks)表中所示的目标框架。</span><span class="sxs-lookup"><span data-stu-id="0f9df-230">The build system is aware of preprocessor symbols representing the target frameworks shown in the [Supported target framework versions](#supported-target-frameworks) table when you're using SDK-style projects.</span></span> <span data-ttu-id="0f9df-231">使用表示 .NET Standard、.NET Core 或 .NET 5 TFM 的符号时，请用下划线替换点和连字符，并将小写字母更改为大写字母（例如，`netstandard1.4` 的符号为 `NETSTANDARD1_4`）。</span><span class="sxs-lookup"><span data-stu-id="0f9df-231">When using a symbol that represents a .NET Standard, .NET Core, or .NET 5 TFM, replace dots and hyphens with an underscore and change lowercase letters to uppercase (for example, the symbol for `netstandard1.4` is `NETSTANDARD1_4`).</span></span>

<span data-ttu-id="0f9df-232">.NET 目标框架的预处理器符号的完整列表如下：</span><span class="sxs-lookup"><span data-stu-id="0f9df-232">The complete list of preprocessor symbols for .NET target frameworks is:</span></span>

[!INCLUDE [Preprocessor symbols](../../includes/preprocessor-symbols.md)]

## <a name="deprecated-target-frameworks"></a><span data-ttu-id="0f9df-233">已弃用的目标框架</span><span class="sxs-lookup"><span data-stu-id="0f9df-233">Deprecated target frameworks</span></span>

<span data-ttu-id="0f9df-234">以下目标框架已弃用。</span><span class="sxs-lookup"><span data-stu-id="0f9df-234">The following target frameworks are deprecated.</span></span> <span data-ttu-id="0f9df-235">面向这些目标框架的包应迁移到指定的替代框架。</span><span class="sxs-lookup"><span data-stu-id="0f9df-235">Packages that target these target frameworks should migrate to the indicated replacements.</span></span>

| <span data-ttu-id="0f9df-236">已弃用的 TFM</span><span class="sxs-lookup"><span data-stu-id="0f9df-236">Deprecated TFM</span></span>                                                                             | <span data-ttu-id="0f9df-237">Replacement</span><span class="sxs-lookup"><span data-stu-id="0f9df-237">Replacement</span></span> |
| ------------------------------------------------------------------------------------------ | ----------- |
| <span data-ttu-id="0f9df-238">aspnet50</span><span class="sxs-lookup"><span data-stu-id="0f9df-238">aspnet50</span></span><br><span data-ttu-id="0f9df-239">aspnetcore50</span><span class="sxs-lookup"><span data-stu-id="0f9df-239">aspnetcore50</span></span><br><span data-ttu-id="0f9df-240">dnxcore50</span><span class="sxs-lookup"><span data-stu-id="0f9df-240">dnxcore50</span></span><br><span data-ttu-id="0f9df-241">dnx</span><span class="sxs-lookup"><span data-stu-id="0f9df-241">dnx</span></span><br><span data-ttu-id="0f9df-242">dnx45</span><span class="sxs-lookup"><span data-stu-id="0f9df-242">dnx45</span></span><br><span data-ttu-id="0f9df-243">dnx451</span><span class="sxs-lookup"><span data-stu-id="0f9df-243">dnx451</span></span><br><span data-ttu-id="0f9df-244">dnx452</span><span class="sxs-lookup"><span data-stu-id="0f9df-244">dnx452</span></span>                  | <span data-ttu-id="0f9df-245">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="0f9df-245">netcoreapp</span></span>  |
| <span data-ttu-id="0f9df-246">dotnet</span><span class="sxs-lookup"><span data-stu-id="0f9df-246">dotnet</span></span><br><span data-ttu-id="0f9df-247">dotnet50</span><span class="sxs-lookup"><span data-stu-id="0f9df-247">dotnet50</span></span><br><span data-ttu-id="0f9df-248">dotnet51</span><span class="sxs-lookup"><span data-stu-id="0f9df-248">dotnet51</span></span><br><span data-ttu-id="0f9df-249">dotnet52</span><span class="sxs-lookup"><span data-stu-id="0f9df-249">dotnet52</span></span><br><span data-ttu-id="0f9df-250">dotnet53</span><span class="sxs-lookup"><span data-stu-id="0f9df-250">dotnet53</span></span><br><span data-ttu-id="0f9df-251">dotnet54</span><span class="sxs-lookup"><span data-stu-id="0f9df-251">dotnet54</span></span><br><span data-ttu-id="0f9df-252">dotnet55</span><span class="sxs-lookup"><span data-stu-id="0f9df-252">dotnet55</span></span><br><span data-ttu-id="0f9df-253">dotnet56</span><span class="sxs-lookup"><span data-stu-id="0f9df-253">dotnet56</span></span> | <span data-ttu-id="0f9df-254">netstandard</span><span class="sxs-lookup"><span data-stu-id="0f9df-254">netstandard</span></span> |
| <span data-ttu-id="0f9df-255">netcore50</span><span class="sxs-lookup"><span data-stu-id="0f9df-255">netcore50</span></span>                                                                                  | <span data-ttu-id="0f9df-256">uap10.0</span><span class="sxs-lookup"><span data-stu-id="0f9df-256">uap10.0</span></span>     |
| <span data-ttu-id="0f9df-257">win</span><span class="sxs-lookup"><span data-stu-id="0f9df-257">win</span></span>                                                                                        | <span data-ttu-id="0f9df-258">netcore45</span><span class="sxs-lookup"><span data-stu-id="0f9df-258">netcore45</span></span>   |
| <span data-ttu-id="0f9df-259">win8</span><span class="sxs-lookup"><span data-stu-id="0f9df-259">win8</span></span>                                                                                       | <span data-ttu-id="0f9df-260">netcore45</span><span class="sxs-lookup"><span data-stu-id="0f9df-260">netcore45</span></span>   |
| <span data-ttu-id="0f9df-261">win81</span><span class="sxs-lookup"><span data-stu-id="0f9df-261">win81</span></span>                                                                                      | <span data-ttu-id="0f9df-262">netcore451</span><span class="sxs-lookup"><span data-stu-id="0f9df-262">netcore451</span></span>  |
| <span data-ttu-id="0f9df-263">win10</span><span class="sxs-lookup"><span data-stu-id="0f9df-263">win10</span></span>                                                                                      | <span data-ttu-id="0f9df-264">uap10.0</span><span class="sxs-lookup"><span data-stu-id="0f9df-264">uap10.0</span></span>     |
| <span data-ttu-id="0f9df-265">winrt</span><span class="sxs-lookup"><span data-stu-id="0f9df-265">winrt</span></span>                                                                                      | <span data-ttu-id="0f9df-266">netcore45</span><span class="sxs-lookup"><span data-stu-id="0f9df-266">netcore45</span></span>   |

## <a name="see-also"></a><span data-ttu-id="0f9df-267">另请参阅</span><span class="sxs-lookup"><span data-stu-id="0f9df-267">See also</span></span>

- [<span data-ttu-id="0f9df-268">使用跨平台工具开发库</span><span class="sxs-lookup"><span data-stu-id="0f9df-268">Developing Libraries with Cross Platform Tools</span></span>](../core/tutorials/libraries.md)
- [<span data-ttu-id="0f9df-269">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="0f9df-269">.NET Standard</span></span>](net-standard.md)
- [<span data-ttu-id="0f9df-270">.NET Core 版本控制</span><span class="sxs-lookup"><span data-stu-id="0f9df-270">.NET Core Versioning</span></span>](../core/versions/index.md)
- [<span data-ttu-id="0f9df-271">dotnet/standard GitHub 存储库</span><span class="sxs-lookup"><span data-stu-id="0f9df-271">dotnet/standard GitHub repository</span></span>](https://github.com/dotnet/standard)
- [<span data-ttu-id="0f9df-272">NuGet 工具 GitHub 存储库</span><span class="sxs-lookup"><span data-stu-id="0f9df-272">NuGet Tools GitHub Repository</span></span>](https://github.com/joelverhagen/NuGetTools)
- [<span data-ttu-id="0f9df-273">.NET 中的框架配置文件</span><span class="sxs-lookup"><span data-stu-id="0f9df-273">Framework Profiles in .NET</span></span>](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html)
