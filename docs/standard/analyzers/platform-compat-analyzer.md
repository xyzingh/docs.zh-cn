---
title: 平台兼容性分析器
description: 可帮助检测跨平台应用和库中的平台兼容性问题的 Roslyn 分析器。
author: buyaa-n
ms.date: 09/17/2020
ms.openlocfilehash: 44c2c2d9674b13f314a057f847df2d4d474cc2be
ms.sourcegitcommit: 636af37170ae75a11c4f7d1ecd770820e7dfe7bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91805293"
---
# <a name="platform-compatibility-analyzer"></a><span data-ttu-id="5a5ba-103">平台兼容性分析器</span><span class="sxs-lookup"><span data-stu-id="5a5ba-103">Platform compatibility analyzer</span></span>

<span data-ttu-id="5a5ba-104">你可能听说过“一个 .NET”的格言：一个统一的平台，用于生成任何类型的应用程序。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-104">You've probably heard the motto of "One .NET": a single, unified platform for building any type of application.</span></span> <span data-ttu-id="5a5ba-105">.NET 5.0 SDK 包括 ASP.NET Core、Entity Framework Core、WinForms、WPF、Xamarin 和 ML.NET，并且随着时间的推移，将添加对更多平台的支持。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-105">The .NET 5.0 SDK includes ASP.NET Core, Entity Framework Core, WinForms, WPF, Xamarin, and ML.NET, and will add support for more platforms over time.</span></span> <span data-ttu-id="5a5ba-106">.NET 5.0 旨在提供一种无需推出不同 .NET 风格，但不会尝试完全抽象出基础操作系统 (OS) 的体验。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-106">.NET 5.0 strives to provide an experience where you don't have to reason about the different flavors of .NET, but doesn't attempt to fully abstract away the underlying operating system (OS).</span></span> <span data-ttu-id="5a5ba-107">你将继续能够调用特定于平台的 API，例如 P/Invoke、WinRT 或适用于 iOS 和 Android 的 Xamarin 绑定。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-107">You'll continue to be able to call platform-specific APIs, for example, P/Invokes, WinRT, or the Xamarin bindings for iOS and Android.</span></span>

<span data-ttu-id="5a5ba-108">但在组件上使用特定于平台的 API 意味着代码在所有平台上都不再有效。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-108">But using platform-specific APIs on a component means the code no longer works across all platforms.</span></span> <span data-ttu-id="5a5ba-109">我们需要一种在设计时进行检测的方法，使开发人员在无意中使用特定于平台的 API 时获得诊断。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-109">We needed a way to detect this at design time so developers get diagnostics when they inadvertently use platform-specific APIs.</span></span> <span data-ttu-id="5a5ba-110">为了实现此目标，.NET 5.0 引入了[平台兼容性分析器](/visualstudio/code-quality/ca1416)和补充 API，帮助开发人员根据需要识别和使用特定于平台的 API。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-110">To achieve this goal, .NET 5.0 introduces the [platform compatibility analyzer](/visualstudio/code-quality/ca1416) and complementary APIs to help developers identify and use platform-specific APIs where appropriate.</span></span>
<span data-ttu-id="5a5ba-111">新的 API 包括：</span><span class="sxs-lookup"><span data-stu-id="5a5ba-111">The new APIs include:</span></span>

- <span data-ttu-id="5a5ba-112"><xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> 用于将 API 批注为特定于平台，<xref:System.Runtime.Versioning.UnsupportedOSPlatformAttribute> 用于将 API 批注为在特定 OS 上不受支持。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-112"><xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> to annotate APIs as being platform-specific and <xref:System.Runtime.Versioning.UnsupportedOSPlatformAttribute> to annotate APIs as being unsupported on a particular OS.</span></span> <span data-ttu-id="5a5ba-113">这些属性可以选择包括版本号，并且已应用于核心 .NET 库中的某些特定于平台的 API。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-113">These attributes can optionally include the version number, and have already been applied to some platform-specific APIs in the core .NET libraries.</span></span>
- <span data-ttu-id="5a5ba-114"><xref:System.OperatingSystem?displayProperty=nameWithType> 类中的 `Is<Platform>()` 和 `Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)` 静态方法，用于安全地调用特定于平台的 API。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-114">`Is<Platform>()` and `Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)` static methods in the <xref:System.OperatingSystem?displayProperty=nameWithType> class for safely calling platform-specific APIs.</span></span> <span data-ttu-id="5a5ba-115">例如，<xref:System.OperatingSystem.IsWindows?displayProperty=nameWithType> 可用于保护对特定于 Windows 的 API 的调用，<xref:System.OperatingSystem.IsWindowsVersionAtLeast%2A?displayProperty=nameWithType>() 可用于保护受版本控制的特定于 Windows 的 API 调用。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-115">For example, <xref:System.OperatingSystem.IsWindows?displayProperty=nameWithType> can be used to guard a call to a Windows-specific API, and <xref:System.OperatingSystem.IsWindowsVersionAtLeast%2A?displayProperty=nameWithType>() can be used to guard a versioned Windows-specific API call.</span></span> <span data-ttu-id="5a5ba-116">请参阅这些[示例](#guard-platform-specific-apis-with-guard-methods)，了解如何使用这些方法保护特定于平台的 API 引用。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-116">See these [examples](#guard-platform-specific-apis-with-guard-methods) of how these methods can be used as guards of platform-specific API references.</span></span>

> [!TIP]
> <span data-ttu-id="5a5ba-117">平台兼容性分析器升级并替换 [.NET API 分析器](../../standard/analyzers/api-analyzer.md)的[发现跨平台问题](../../standard/analyzers/api-analyzer.md#discover-cross-platform-issues)。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-117">The platform compatibility analyzer upgrades and replaces the [Discovering cross-platform issues](../../standard/analyzers/api-analyzer.md#discover-cross-platform-issues) feature of the [.NET API analyzer](../../standard/analyzers/api-analyzer.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a5ba-118">先决条件</span><span class="sxs-lookup"><span data-stu-id="5a5ba-118">Prerequisites</span></span>

<span data-ttu-id="5a5ba-119">平台兼容性分析器是 Roslyn 代码质量分析器之一。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-119">The platform compatibility analyzer is one of the Roslyn code quality analyzers.</span></span> <span data-ttu-id="5a5ba-120">从 .NET 5.0 开始，这些分析器[包含在 .NET SDK 中](../../fundamentals/code-analysis/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-120">Starting in .NET 5.0, these analyzers are [included with the .NET SDK](../../fundamentals/code-analysis/overview.md).</span></span> <span data-ttu-id="5a5ba-121">默认情况下，仅为面向 `net5.0` 或更高版本的项目启用平台兼容性分析器。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-121">The platform compatibility analyzer is enabled by default only for projects that target `net5.0` or a later version.</span></span> <span data-ttu-id="5a5ba-122">但是，可以为面向其他框架的项目[启用](/visualstudio/code-quality/ca1416.md#configurability)该分析器。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-122">However, you can [enable](/visualstudio/code-quality/ca1416.md#configurability) it for projects that target other frameworks.</span></span>

## <a name="how-the-analyzer-determines-platform-dependency"></a><span data-ttu-id="5a5ba-123">分析器如何确定平台依赖关系</span><span class="sxs-lookup"><span data-stu-id="5a5ba-123">How the analyzer determines platform dependency</span></span>

- <span data-ttu-id="5a5ba-124">无归属的 API 被视为适用于所有 OS 平台。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-124">An **unattributed API** is considered to work on **all OS platforms**.</span></span>
- <span data-ttu-id="5a5ba-125">标记为 `[SupportedOSPlatform("platform")]` 的 API 被视为仅可移植到指定 OS `platform`。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-125">An API marked with `[SupportedOSPlatform("platform")]` is considered only portable to the specified OS `platform`.</span></span>
  - <span data-ttu-id="5a5ba-126">可以多次应用该属性，以指示多个平台支持 (`[SupportedOSPlatform("windows"), SupportedOSPlatform("Android6.0")]`)。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-126">The attribute can be applied multiple times to indicate **multiple platform support** (`[SupportedOSPlatform("windows"), SupportedOSPlatform("Android6.0")]`).</span></span>
  - <span data-ttu-id="5a5ba-127">如果在没有正确的平台上下文的情况下引用特定于平台的 API，则分析器将生成警告：</span><span class="sxs-lookup"><span data-stu-id="5a5ba-127">The analyzer will produce a **warning** if platform-specific APIs are referenced without a proper **platform context**:</span></span>
    - <span data-ttu-id="5a5ba-128">如果项目不面向受支持的平台（例如，特定于 Windows 的 API 调用，且项目面向 `<TargetFramework>net5.0-ios14.0</TargetFramework>`），则将生成警告。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-128">**Warns** if the project doesn't target the supported platform (for example, a Windows-specific API call and the project targets `<TargetFramework>net5.0-ios14.0</TargetFramework>`).</span></span>
    - <span data-ttu-id="5a5ba-129">如果项目是多定向的 (`<TargetFramework>net5.0</TargetFramework>`)，则将生成警告。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-129">**Warns** if the project is multi-targeted (`<TargetFramework>net5.0</TargetFramework>`).</span></span>
    - <span data-ttu-id="5a5ba-130">如果在面向任何指定平台的项目中引用特定于平台的 API（例如，对于特定于 Windows 的 API 调用，且项目面向 `<TargetFramework>net5.0-windows</TargetFramework>`），则不会生成警告。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-130">**Doesn't warn** if the platform-specific API is referenced within a project that targets any of the **specified platforms** (for example, for a Windows-specific API call and the project targets `<TargetFramework>net5.0-windows</TargetFramework>`).</span></span>
    - <span data-ttu-id="5a5ba-131">如果特定于平台的 API 调用受到相应的平台检查方法（如 `if(OperatingSystem.IsWindows())`）的保护，则不会生成警告。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-131">**Doesn't warn** if the platform-specific API call is guarded by corresponding platform-check methods (for example, `if(OperatingSystem.IsWindows())`).</span></span>
    - <span data-ttu-id="5a5ba-132">如果在相同的特定于平台的上下文（使用 `[SupportedOSPlatform("platform")` 属性化的调用站点）中引用特定于平台的 API，则不会生成警告。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-132">**Doesn't warn** if the platform-specific API is referenced from the same platform-specific context (**call site also attributed** with `[SupportedOSPlatform("platform")`).</span></span>
- <span data-ttu-id="5a5ba-133">标记为 `[UnsupportedOSPlatform("platform")]` 的 API 被视为仅在指定的 OS `platform` 上不受支持，但在所有其他平台上受支持。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-133">An API marked with `[UnsupportedOSPlatform("platform")]` is considered unsupported only on the specified OS `platform` but supported for all other platforms.</span></span>
  - <span data-ttu-id="5a5ba-134">可以使用不同平台（例如 `[UnsupportedOSPlatform("iOS"), UnsupportedOSPlatform("Android6.0")]`）多次应用属性。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-134">The attribute can be applied multiple times with different platforms, for example, `[UnsupportedOSPlatform("iOS"), UnsupportedOSPlatform("Android6.0")]`.</span></span>
  - <span data-ttu-id="5a5ba-135">仅当 `platform` 对调用站点有效时，分析器才会生成警告：</span><span class="sxs-lookup"><span data-stu-id="5a5ba-135">The analyzer produces a **warning** only if the `platform` is effective for the call site:</span></span>
    - <span data-ttu-id="5a5ba-136">如果项目面向被属性化为不受支持的平台（例如，如果 API 使用 `[UnsupportedOSPlatform("windows")]` 进行了属性化，且调用站点面向 `<TargetFramework>net5.0-windows</TargetFramework>`），则将生成警告。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-136">**Warns** if the project targets the platform that's attributed as unsupported (for example, if the API is attributed with `[UnsupportedOSPlatform("windows")]` and the call site targets `<TargetFramework>net5.0-windows</TargetFramework>`).</span></span>
    - <span data-ttu-id="5a5ba-137">如果项目是多定向的，且 `platform` 包含在默认 [MSBuild `<SupportedPlatform>`](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) 项组中，或者 `platform` 手动包含在 `MSBuild` \<SupportedPlatform> 项组中，则将生成警告：</span><span class="sxs-lookup"><span data-stu-id="5a5ba-137">**Warns** if the project is multi-targeted and the `platform` is included in the default [MSBuild `<SupportedPlatform>`](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) items group, or the `platform` is manually included within the `MSBuild` \<SupportedPlatform> items group:</span></span>

      ```XML
      <ItemGroup>
          <SupportedPlatform Include="platform" />
      </ItemGroup>
      ```

    - <span data-ttu-id="5a5ba-138">如果要生成的应用不面向不受支持的平台或是多定向的，并且平台未包含在默认 [MSBuild `<SupportedPlatform>`](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) 项组中，则不会生成警告。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-138">**Doesn't warn** if you're building an app that doesn't target the unsupported platform or is multi-targeted and the platform is not included in the default [MSBuild `<SupportedPlatform>`](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) items group.</span></span>
- <span data-ttu-id="5a5ba-139">可以使用或不使用作为平台名称一部分的版本号对两个属性进行实例化。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-139">Both attributes can be instantiated with or without version numbers as part of the platform name.</span></span>
  - <span data-ttu-id="5a5ba-140">版本号的格式为 `major.minor[.build[.revision]]`；`major.minor` 是必需的，而 `build` 和 `revision` 部分是可选的。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-140">Version numbers are in the format of `major.minor[.build[.revision]]`; `major.minor` is required and the `build` and `revision` parts are optional.</span></span> <span data-ttu-id="5a5ba-141">例如，“Windows7.0”指示 Windows 版本 7.0，但“Windows”被解释为 Windows 0.0。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-141">For example, "Windows7.0" indicates Windows version 7.0, but "Windows" is interpreted as Windows 0.0.</span></span>

<span data-ttu-id="5a5ba-142">有关详细信息，请参阅[属性的工作方式及其导致的诊断的示例](#examples-of-how-the-attributes-work-and-what-diagnostics-they-produce)。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-142">For more information, see [examples of how the attributes work and what diagnostics they cause](#examples-of-how-the-attributes-work-and-what-diagnostics-they-produce).</span></span>

### <a name="advanced-scenarios-for-combining-attributes"></a><span data-ttu-id="5a5ba-143">组合属性的高级方案</span><span class="sxs-lookup"><span data-stu-id="5a5ba-143">Advanced scenarios for combining attributes</span></span>

- <span data-ttu-id="5a5ba-144">如果存在 `[SupportedOSPlatform]` 和 `[UnsupportedOSPlatform]` 属性的组合，则所有属性都按 OS 平台标识符分组：</span><span class="sxs-lookup"><span data-stu-id="5a5ba-144">If a combination of `[SupportedOSPlatform]` and `[UnsupportedOSPlatform]` attributes are present, all attributes are grouped by OS platform identifier:</span></span>
  - <span data-ttu-id="5a5ba-145">仅受支持的列表。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-145">**Supported only list**.</span></span> <span data-ttu-id="5a5ba-146">如果每个 OS 平台的最低版本是 `[SupportedOSPlatform]` 属性，则 API 会被视为仅在列出的平台上受支持，但在所有其他平台上不受支持。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-146">If the lowest version for each OS platform is a `[SupportedOSPlatform]` attribute, the API is considered to only be supported by the listed platforms and unsupported by all other platforms.</span></span> <span data-ttu-id="5a5ba-147">每个平台的可选 `[UnsupportedOSPlatform]` 属性只能具有较高版本的最低支持版本，这表示从指定的版本开始删除 API。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-147">The optional `[UnsupportedOSPlatform]` attributes for each platform can only have higher version of the minimum supported version, which denotes that the API is removed starting from the specified version.</span></span>

    ```csharp
    // The API only supported on Windows 8.0 and later, not supported for all other.
    // The API is removed/unsupported from version 10.0.19041.0.
    [SupportedOSPlatform("windows8.0")]
    [UnsupportedOSPlatform("windows10.0.19041.0")]
    public void ApiSupportedFromWindows80SupportFromCertainVersion();
    ```

  - <span data-ttu-id="5a5ba-148">仅不受支持的列表。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-148">**Unsupported only list**.</span></span> <span data-ttu-id="5a5ba-149">如果每个 OS 平台的最低版本是 `[UnsupportedOSPlatform]` 属性，则 API 会被视为仅在列出的平台上不受支持，但在所有其他平台上受支持。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-149">If the lowest version for each OS platform is an `[UnsupportedOSPlatform]` attribute, then the API is considered to only be unsupported by the listed platforms and supported by all other platforms.</span></span> <span data-ttu-id="5a5ba-150">此列表可能具有包含相同平台但版本较高的 `[SupportedOSPlatform]` 属性，这表示从该版本开始支持 API。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-150">The list could have `[SupportedOSPlatform]` attribute with the same platform but a higher version, which denotes that the API is supported starting from that version.</span></span>

    ```csharp
    // The API was unsupported on Windows until version 10.0.19041.0.
    // The API is considered supported everywhere else without constraints.
    [UnsupportedOSPlatform("windows")]
    [SupportedOSPlatform("windows10.0.19041.0")]
    public void ApiSupportedFromWindows8UnsupportFromWindows10();
    ```

  - <span data-ttu-id="5a5ba-151">不一致的列表。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-151">**Inconsistent list**.</span></span> <span data-ttu-id="5a5ba-152">如果某些平台的最低版本为 `[SupportedOSPlatform]`，而其他平台的最低版本为 `[UnsupportedOSPlatform]`，则会被视为不一致，不受分析器支持。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-152">If the lowest version for some platforms is `[SupportedOSPlatform]` while it is `[UnsupportedOSPlatform]` for other platforms, it's considered to be inconsistent, which is not supported for the analyzer.</span></span>
  - <span data-ttu-id="5a5ba-153">如果 `[SupportedOSPlatform]` 和 `[UnsupportedOSPlatform]` 属性的最低版本相同，则分析器会将平台视为“仅受支持的列表”的一部分。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-153">If the lowest versions of `[SupportedOSPlatform]` and `[UnsupportedOSPlatform]` attributes are equal, the analyzer considers the platform as part of the **Supported only list**.</span></span>
- <span data-ttu-id="5a5ba-154">平台属性可应用于类型、成员（方法、字段、属性和事件）以及具有不同平台名称或版本的程序集。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-154">Platform attributes can be applied to types, members (methods, fields, properties, and events) and assemblies with different platform names or versions.</span></span>
  - <span data-ttu-id="5a5ba-155">在顶级 `target` 应用的属性会影响其所有成员和类型。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-155">Attributes applied at the top level `target` affect all of its members and types.</span></span>
  - <span data-ttu-id="5a5ba-156">仅当遵守规则“子批注可以缩小平台支持范围，但无法将其扩大”时才会应用子级属性。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-156">Child-level attributes only apply if they adhere to the rule "child annotations can narrow the platforms support, but they cannot widen it".</span></span>
    - <span data-ttu-id="5a5ba-157">当父级具有仅受支持的列表时，子成员属性无法添加新的平台支持，因为这会扩大父级支持。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-157">When parent has **Supported only** list, then child member attributes cannot add a new platform support, as that would be extending parent support.</span></span> <span data-ttu-id="5a5ba-158">只能将新平台支持添加到父级本身。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-158">Support for a new platform can only be added to the parent itself.</span></span> <span data-ttu-id="5a5ba-159">但对于具有更高版本的同一平台，子级可以有 `Supported` 属性，因为这会缩小支持。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-159">But the child can have the `Supported` attribute for the same platform with later versions as that narrows the support.</span></span> <span data-ttu-id="5a5ba-160">另外，子级可以有同一平台的 `Unsupported` 属性，因为这也会缩小父级支持。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-160">Also, the child can have the `Unsupported` attribute with the same platform as that also narrows parent support.</span></span>
    - <span data-ttu-id="5a5ba-161">当父级有仅限不支持的列表时，子成员属性可以添加对新平台的支持，因为这会缩小父级支持。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-161">When parent has **Unsupported only** list, then child member attributes can add support for a new platform, as that narrows parent support.</span></span> <span data-ttu-id="5a5ba-162">但它不能具有与父级所在平台相同的 `Supported` 属性，因为这会扩大父级支持。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-162">But it cannot have the `Supported` attribute for the same platform as the parent, because that extends parent support.</span></span> <span data-ttu-id="5a5ba-163">只能将对同一平台的支持添加到应用了原始 `Unsupported` 属性的父级。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-163">Support for the same platform can only be added to the parent where the original `Unsupported` attribute was applied.</span></span>
  - <span data-ttu-id="5a5ba-164">如果对具有相同 `platform` 名称的 API 应用 `[SupportedOSPlatform("platformVersion")]` 一次以上，则分析器仅考虑最低版本的 API。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-164">If `[SupportedOSPlatform("platformVersion")]` is applied more than once for an API with the same `platform` name, the analyzer only considers the one with the minimum version.</span></span>
  - <span data-ttu-id="5a5ba-165">如果对具有相同 `platform` 名称的 API 应用 `[UnsupportedOSPlatform("platformVersion")]` 两次以上，则分析器仅考虑最早版本的两个 API。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-165">If `[UnsupportedOSPlatform("platformVersion")]` is applied more than twice for an API with the same `platform` name, the analyzer only considers the two with the earliest versions.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5a5ba-166">最初受支持但在更高版本中不受支持（删除）的 API 并不希望在更高版本中重新受支持。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-166">An API that was supported initially but unsupported (removed) in a later version is not expected to get resupported in an even later version.</span></span>

### <a name="examples-of-how-the-attributes-work-and-what-diagnostics-they-produce"></a><span data-ttu-id="5a5ba-167">属性的工作方式及其导致的诊断的示例</span><span class="sxs-lookup"><span data-stu-id="5a5ba-167">Examples of how the attributes work and what diagnostics they produce</span></span>

  ```csharp
  // An API supported only on Windows.
  [SupportedOSPlatform("Windows")]
  public void WindowsOnlyApi() { }

  // an API supported on Windows and Linux.
  [SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("Linux")]
  public void SupportedOnWindowsAndLinuxOnly() { }

  // an API only supported on Windows 8.0 and later, not supported for all other.
  // an API is removed/unsupported from version 10.0.19041.0.
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void ApiSupportedFromWindows8UnsupportFromWindows10() { }

  // an Assembly supported on Windows, the API added from version 10.0.19041.0.
  [assembly: SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("windows10.0.19041.0")]
  public void AssemblySupportedOnWindowsApiSupportedFromWindows10() { }

  public void Caller()
  {
      WindowsOnlyApi(); // warns: 'WindowsOnlyApi' is supported on 'windows'

      // warns: 'SupportedOnWindowsAndLinuxOnly' is supported on 'Windows'
      // warns: 'SupportedOnWindowsAndLinuxOnly' is supported on 'Linux'
      SupportedOnWindowsAndLinuxOnly();

      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 8.0 and later
      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is unsupported on 'windows' 10.0.19041.0 and later
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 10.0.19041.0 and later
      // for same platform analyzer only warn for the latest version.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  // an API not supported on android but supported on all other.
  [UnsupportedOSPlatform("android")]
  public void DoesNotWorkOnAndroid() { }

  // an API was unsupported on Windows until version 8.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  public void StartedWindowsSupportFromVersion8() { }

  // an API was unsupported on Windows until version8.0.
  // Then the API is removed (unsupported) from version 10.0.19041.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void StartedWindowsSupportFrom8UnsupportedFrom10() { }

  public void Caller2()
  {
      DoesNotWorkOnAndroid(); // warns 'DoesNotWorkOnAndroid' is unsupported on 'android'

      // warns:'StartedWindowsSupportFromVersion8' is unsupported on 'windows'
      // warns:'StartedWindowsSupportFromVersion8' is supported on 'windows' 8.0 and later
      StartedWindowsSupportFromVersion8();

      // warns:'StartedWindowsSupportFrom8UnsupportedFrom10' is unsupported on 'windows'
      // warns:'StartedWindowsSupportFrom8UnsupportedFrom10' is supported on 'windows' 8.0 and later
      // even there were 3 diagnostics found analyzer warn only for the first 2.
      StartedWindowsSupportFrom8UnsupportedFrom10();
  }
  ```

## <a name="handle-reported-warnings"></a><span data-ttu-id="5a5ba-168">处理报告的警告</span><span class="sxs-lookup"><span data-stu-id="5a5ba-168">Handle reported warnings</span></span>

<span data-ttu-id="5a5ba-169">处理这些诊断的建议方法是确保在相应的平台上运行时仅调用特定于平台的 API。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-169">The recommended way to deal with these diagnostics is to make sure you only call platform-specific APIs when running on an appropriate platform.</span></span> <span data-ttu-id="5a5ba-170">下面是可用于解决警告的选项；选择最适合你的情况的选项：</span><span class="sxs-lookup"><span data-stu-id="5a5ba-170">Following are the options you can use to address the warnings; choose whichever is most appropriate for your situation:</span></span>

- <span data-ttu-id="5a5ba-171">保护调用。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-171">**Guard the call**.</span></span> <span data-ttu-id="5a5ba-172">可以通过在运行时有条件地调用代码来实现此目的。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-172">You can achieve this by conditionally calling the code at run time.</span></span> <span data-ttu-id="5a5ba-173">使用平台检查方法之一检查是否正在所需的 `Platform` 上运行，例如 `OperatingSystem.Is<Platform>()` 或 `OperatingSystem.Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)`。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-173">Check whether you're running on a desired `Platform` by using one of platform-check methods, for example, `OperatingSystem.Is<Platform>()` or `OperatingSystem.Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)`.</span></span>

- <span data-ttu-id="5a5ba-174">将调用站点标记为特定于平台。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-174">**Mark the call site as platform-specific**.</span></span> <span data-ttu-id="5a5ba-175">还可以选择将自己的 API 标记为特定于平台，从而有效地将要求转发给调用方。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-175">You can also choose to mark your own APIs as being platform-specific, thus effectively just forwarding the requirements to your callers.</span></span> <span data-ttu-id="5a5ba-176">将包含的方法或类型或具有相同属性的整个程序集标记为引用的依赖平台的调用。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-176">Mark the containing method or type or the entire assembly with the same attributes as the referenced platform-dependent call.</span></span> <span data-ttu-id="5a5ba-177">[示例](#mark-call-site-as-platform-specific)。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-177">[Examples](#mark-call-site-as-platform-specific).</span></span>

- <span data-ttu-id="5a5ba-178">通过平台检查来断言调用站点。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-178">**Assert the call site with platform check**.</span></span> <span data-ttu-id="5a5ba-179">如果不希望在运行时增加额外的 `if` 语句，请使用 <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-179">If you don't want the overhead of an additional `if` statement at run time, use <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType>.</span></span> <span data-ttu-id="5a5ba-180">[示例](#assert-the-call-site-with-platform-check)。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-180">[Example](#assert-the-call-site-with-platform-check).</span></span>

- <span data-ttu-id="5a5ba-181">删除代码。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-181">**Delete the code**.</span></span> <span data-ttu-id="5a5ba-182">通常不是你想要的，因为这意味着当 Windows 用户使用代码时将失真。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-182">Generally not what you want because it means you lose fidelity when your code is used by Windows users.</span></span> <span data-ttu-id="5a5ba-183">对于存在跨平台替代方法的情况，更好的做法可能是在特定于平台的 API 上使用此方法。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-183">For cases where a cross-platform alternative exists, you're likely better off using that over platform-specific APIs.</span></span>

- <span data-ttu-id="5a5ba-184">禁止显示警告。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-184">**Suppress the warning**.</span></span> <span data-ttu-id="5a5ba-185">通过 EditorConfig 条目或 `#pragma warning disable ca1416` 即可禁止显示警告。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-185">You can also simply suppress the warning, either via an EditorConfig entry or `#pragma warning disable ca1416`.</span></span> <span data-ttu-id="5a5ba-186">但是，当使用特定于平台的 API 时，如非绝对必要，请勿使用此选项。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-186">However, this option should be a last resort when using platform-specific APIs.</span></span>

### <a name="guard-platform-specific-apis-with-guard-methods"></a><span data-ttu-id="5a5ba-187">使用保护方法保护特定于平台的 API</span><span class="sxs-lookup"><span data-stu-id="5a5ba-187">Guard platform-specific APIs with guard methods</span></span>

<span data-ttu-id="5a5ba-188">保护方法的平台名称应与依赖平台的调用 API 平台名称匹配。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-188">The guard method's platform name should match with the calling platform-dependent API platform name.</span></span> <span data-ttu-id="5a5ba-189">如果调用 API 的平台字符串包括版本：</span><span class="sxs-lookup"><span data-stu-id="5a5ba-189">If the platform string of the calling API includes the version:</span></span>

- <span data-ttu-id="5a5ba-190">对于 `[SupportedOSPlatform("platformVersion")]` 属性，保护方法平台 `version` 应大于或等于调用平台的 `Version`。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-190">For the `[SupportedOSPlatform("platformVersion")]` attribute, the guard method platform `version` should be greater than or equal to the calling platform's `Version`.</span></span>
- <span data-ttu-id="5a5ba-191">对于 `[UnsupportedOSPlatform("platformVersion")]` 属性，保护方法平台 `version` 应小于或等于调用平台的 `Version`。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-191">For the `[UnsupportedOSPlatform("platformVersion")]` attribute, the guard method's platform `version` should be less than or equal to the calling platform's `Version`.</span></span>

  ```csharp
  public void CallingSupportedOnlyApis() // Allow list calls
  {
      if (OperatingSystem.IsWindows())
      {
          WindowsOnlyApi(); // will not warn
      }

      if (OperatingSystem.IsLinux())
      {
          SupportedOnWindowsAndLinuxOnly(); // will not warn, within one of the supported context
      }

      // Can use &&, || logical operators to guard combined attributes
      if (OperatingSystem.IsWindowsVersionAtLeast(8) && !OperatingSystem.IsWindowsVersionAtLeast(10.0.19041)))
      {
          ApiSupportedFromWindows8UnsupportFromWindows10();
      }

      if (OperatingSystem.IsWindowsVersionAtLeast(10, 0, 1903))
      {
          AssemblySupportedOnWindowsApiSupportedFromWindows10(); // Only need to check latest supported version
      }
  }

  public void CallingUnsupportedApis()
  {
      if (!OperatingSystem.IsAndroid())
      {
          DoesNotWorkOnAndroid(); // will not warn
      }

      if (!OperatingSystem.IsWindows() || OperatingSystem.IsWindowsVersionAtLeast(8))
      {
          StartedWindowsSupportFromVersion8(); // will not warn
      }

      if (!OperatingSystem.IsWindows() || // supported all other platforms
         (OperatingSystem.IsWindowsVersionAtLeast(8) && !OperatingSystem.IsWindowsVersionAtLeast(10, 0, 1903)))
      {
          StartedWindowsSupportFrom8UnsupportedFrom10(); // will not warn
      }
  }
  ```

- <span data-ttu-id="5a5ba-192">如果需要保护面向新 <xref:System.OperatingSystem> API 不可用的 `netstandard` 或 `netcoreapp` 的代码，则可以使用 <xref:System.Runtime.InteropServices.RuntimeInformation.IsOSPlatform%2A?displayProperty=nameWithType> API 并由分析器遵守。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-192">If you need to guard code that targets `netstandard` or `netcoreapp` where new <xref:System.OperatingSystem> APIs are not available, the <xref:System.Runtime.InteropServices.RuntimeInformation.IsOSPlatform%2A?displayProperty=nameWithType> API can be used and will be respected by the analyzer.</span></span> <span data-ttu-id="5a5ba-193">但不如 <xref:System.OperatingSystem> 中添加的新 API 那样优化。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-193">But it's not as optimized as the new APIs added in <xref:System.OperatingSystem>.</span></span> <span data-ttu-id="5a5ba-194">如果平台在 <xref:System.Runtime.InteropServices.OSPlatform> 结构中不受支持，则可以调用 <xref:System.Runtime.InteropServices.OSPlatform.Create(System.String)?displayProperty=nameWithType> 并传入平台名称（分析器也会遵循此名称）。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-194">If the platform is not supported in the <xref:System.Runtime.InteropServices.OSPlatform> struct, you can call <xref:System.Runtime.InteropServices.OSPlatform.Create(System.String)?displayProperty=nameWithType> and pass in the platform name, which the analyzer also respects.</span></span>

  ```csharp
  public void CallingSupportedOnlyApis()
  {
      if (RuntimeInformation.IsOSPlatform(OSPlatform.Windows))
      {
          SupportedOnWindowsAndLinuxOnly(); // will not warn
      }

      if (RuntimeInformation.IsOSPlatform(OSPlatform.Create("browser")))
      {
          ApiOnlySupportedOnBrowser(); // call of browser specific API
      }
  }
  ```

### <a name="mark-call-site-as-platform-specific"></a><span data-ttu-id="5a5ba-195">将调用站点标记为特定于平台</span><span class="sxs-lookup"><span data-stu-id="5a5ba-195">Mark call site as platform-specific</span></span>

<span data-ttu-id="5a5ba-196">平台名称应与依赖平台的调用 API 匹配。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-196">Platform names should match the calling platform-dependent API.</span></span> <span data-ttu-id="5a5ba-197">如果平台字符串包括版本：</span><span class="sxs-lookup"><span data-stu-id="5a5ba-197">If the platform string includes a version:</span></span>

- <span data-ttu-id="5a5ba-198">对于 `[SupportedOSPlatform("platformVersion")]` 属性，调用站点平台 `version` 应大于或等于调用平台的 `Version`</span><span class="sxs-lookup"><span data-stu-id="5a5ba-198">For the `[SupportedOSPlatform("platformVersion")]` attribute, the call site platform `version` should be greater than or equal to the calling platform's `Version`</span></span>
- <span data-ttu-id="5a5ba-199">对于 `[UnsupportedOSPlatform("platformVersion")]` 属性，调用站点平台 `version` 应小于或等于调用平台的 `Version`</span><span class="sxs-lookup"><span data-stu-id="5a5ba-199">For the `[UnsupportedOSPlatform("platformVersion")]` attribute, the call site platform `version` should be less than or equal to the calling platform's `Version`</span></span>

  ```csharp
  // an API supported only on Windows.
  [SupportedOSPlatform("windows")]
  public void WindowsOnlyApi() { }

  // an API supported on Windows and Linux.
  [SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("Linux")]
  public void SupportedOnWindowsAndLinuxOnly() { }

  // an API only supported on Windows 8.0 and later, not supported for all other.
  // an API is removed/unsupported from version 10.0.19041.0.
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void ApiSupportedFromWindows8UnsupportFromWindows10() { }

  // an Assembly supported on Windows, the API added from version 10.0.19041.0.
  [assembly: SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("windows10.0.19041.0")]
  public void AssemblySupportedOnWindowsApiSupportedFromWindows10() { }

  [SupportedOSPlatform("windows8.0")] // call site attributed Windows 8.0 or above.
  public void Caller()
  {
      WindowsOnlyApi(); // will not warn as call site is for Windows.

      // will not warn as call site is for Windows.
      SupportedOnWindowsAndLinuxOnly();

      // will not warn for the API's [SupportedOSPlatform("windows8.0")] attribute.
      // Warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is unsupported on 'windows' 10.0.19041.0 and later
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 10.0.19041.0 and later
      // as the call site version is lower than calling version.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  [SupportedOSPlatform("windows11.0")] // call site attributed with windows 11.0 or above.
  public void Caller2()
  {
      // Warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is unsupported on 'windows' 10.0.19041.0 and later
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // will not warn as call site version higher than calling API.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")] // call site supports Windows from version 8.0 to 10.0.19041.0.
  public void Caller3()
  {
      // will not warn as caller has exact same attributes.
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // Warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 10.0.19041.0 and later
      // As call site stopped support from that version.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  // an API not supported on Android but supported on all other.
  [UnsupportedOSPlatform("android")]
  public void DoesNotWorkOnAndroid() { }

  // an API was unsupported on Windows until version 8.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  public void StartedWindowsSupportFromVersion8() { }

  // an API was unsupported on Windows until version8.0.
  // Then the API is removed (unsupported) from version 10.0.19041.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void StartedWindowsSupportFrom8UnsupportedFrom10() { }

  [UnsupportedOSPlatform("windows")] // Caller no support Windows for any version.
  public void Caller4()
  {
      DoesNotWorkOnAndroid(); // warns 'DoesNotWorkOnAndroid' is unsupported on 'Android'.

      // will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFromVersion8();

      // same, will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFrom8UnsupportedFrom10();
  }

  [UnsupportedOSPlatform("windows")]
  [UnsupportedOSPlatform("android")] // Caller not support Windows and Android for any version.
  public void Caller4()
  {
      DoesNotWorkOnAndroid(); // will not warn as call site not supports Android.

      // will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFromVersion8();

      // same, will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFrom8UnsupportedFrom10();
  }
  ```

### <a name="assert-the-call-site-with-platform-check"></a><span data-ttu-id="5a5ba-200">通过平台检查来断言调用站点</span><span class="sxs-lookup"><span data-stu-id="5a5ba-200">Assert the call-site with platform check</span></span>

<span data-ttu-id="5a5ba-201">[平台保护示例](#guard-platform-specific-apis-with-guard-methods)中使用的所有条件检查也可以用作 <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType> 的条件。</span><span class="sxs-lookup"><span data-stu-id="5a5ba-201">All the conditional checks used in the [platform guard examples](#guard-platform-specific-apis-with-guard-methods) can also be used as the condition for <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType>.</span></span>

  ```csharp
  // An API supported only on Linux.
  [SupportedOSPlatform("linux")]
  public void LinuxOnlyApi() { }

  public void Caller()
  {
      Debug.Assert(OperatingSystem.IsLinux());

      LinuxOnlyApi(); // will not warn
  }
  ```

## <a name="see-also"></a><span data-ttu-id="5a5ba-202">另请参阅</span><span class="sxs-lookup"><span data-stu-id="5a5ba-202">See also</span></span>

- [<span data-ttu-id="5a5ba-203">.NET 5 中的目标框架名称</span><span class="sxs-lookup"><span data-stu-id="5a5ba-203">Target Framework Names in .NET 5</span></span>](https://github.com/dotnet/designs/blob/master/accepted/2020/net5/net5.md)
- [<span data-ttu-id="5a5ba-204">批注特定于平台的 API 并检测其用法</span><span class="sxs-lookup"><span data-stu-id="5a5ba-204">Annotating platform-specific APIs and detecting its use</span></span>](https://github.com/dotnet/designs/blob/master/accepted/2020/platform-checks/platform-checks.md)
- [<span data-ttu-id="5a5ba-205">在特定平台上将 API 批注为不受支持</span><span class="sxs-lookup"><span data-stu-id="5a5ba-205">Annotating APIs as unsupported on specific platforms</span></span>](https://github.com/dotnet/designs/blob/master/accepted/2020/platform-exclusion/platform-exclusion.md)
- [<span data-ttu-id="5a5ba-206">CA1416 平台兼容性分析器</span><span class="sxs-lookup"><span data-stu-id="5a5ba-206">CA1416 Platform compatibility analyzer</span></span>](../../fundamentals/code-analysis/quality-rules/ca1416.md)
- [<span data-ttu-id="5a5ba-207">.NET API 分析器</span><span class="sxs-lookup"><span data-stu-id="5a5ba-207">.NET API analyzer</span></span>](../../standard/analyzers/api-analyzer.md)
