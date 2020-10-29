---
title: .NET 库的跨平台定位
description: 有关创建跨平台 .NET 库的最佳做法建议。
ms.date: 08/12/2019
ms.openlocfilehash: 6309e300861ab286dcaba3256267b3459e6e0d10
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223344"
---
# <a name="cross-platform-targeting"></a><span data-ttu-id="917b9-103">跨平台定位</span><span class="sxs-lookup"><span data-stu-id="917b9-103">Cross-platform targeting</span></span>

<span data-ttu-id="917b9-104">新式 .NET 支持多个操作系统和设备。</span><span class="sxs-lookup"><span data-stu-id="917b9-104">Modern .NET supports multiple operating systems and devices.</span></span> <span data-ttu-id="917b9-105">.NETNET 开源库支持尽可能多的开发人员（无论是构建 Azure 中托管的 ASP.NET 网站的开发人员，还是在 Unity 中开发 .NET 游戏的开发人员），这一点非常重要。</span><span class="sxs-lookup"><span data-stu-id="917b9-105">It's important for .NET open-source libraries to support as many developers as possible, whether they're building an ASP.NET website hosted in Azure, or a .NET game in Unity.</span></span>

## <a name="net-standard"></a><span data-ttu-id="917b9-106">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="917b9-106">.NET Standard</span></span>

<span data-ttu-id="917b9-107">.NET Standard 是为 .NET 库启用跨平台支持的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="917b9-107">.NET Standard is the best way to add cross-platform support to a .NET library.</span></span> <span data-ttu-id="917b9-108">[.NET Standard](../net-standard.md) 是一套 .NET API 规范，在所有 .NET 实现中推出。</span><span class="sxs-lookup"><span data-stu-id="917b9-108">[.NET Standard](../net-standard.md) is a specification of .NET APIs that are available on all .NET implementations.</span></span> <span data-ttu-id="917b9-109">以 .NET Standard 为目标可以生成受限于使用给定版本的 .NET Standard 中的 API 的库，这意味着实现该版本的 .NET Standard 的所有平台都可以使用它。</span><span class="sxs-lookup"><span data-stu-id="917b9-109">Targeting .NET Standard lets you produce libraries that are constrained to use APIs that are in a given version of .NET Standard, which means it's usable by all platforms that implement that version of .NET Standard.</span></span>

<span data-ttu-id="917b9-110">![.NET Standard](./media/cross-platform-targeting/platforms-netstandard.png ".NET Standard")</span><span class="sxs-lookup"><span data-stu-id="917b9-110">![.NET Standard](./media/cross-platform-targeting/platforms-netstandard.png ".NET Standard")</span></span>

<span data-ttu-id="917b9-111">面向 .NET Standard 并且成功编译项目后，并不能保证库可以在所有平台上成功运行：</span><span class="sxs-lookup"><span data-stu-id="917b9-111">Targeting .NET Standard, and successfully compiling your project, doesn't guarantee the library will run successfully on all platforms:</span></span>

1. <span data-ttu-id="917b9-112">特定于平台的 API 将在其他平台上失败。</span><span class="sxs-lookup"><span data-stu-id="917b9-112">Platform-specific APIs will fail on other platforms.</span></span> <span data-ttu-id="917b9-113">例如，<xref:Microsoft.Win32.Registry?displayProperty=nameWithType> 可以在 Windows 上成功运行，但在任何其他操作系统上使用时，会引发 <xref:System.PlatformNotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="917b9-113">For example, <xref:Microsoft.Win32.Registry?displayProperty=nameWithType> will succeed on Windows and throw <xref:System.PlatformNotSupportedException> when used on any other OS.</span></span>
2. <span data-ttu-id="917b9-114">API 的行为可能有所不同。</span><span class="sxs-lookup"><span data-stu-id="917b9-114">APIs can behave differently.</span></span> <span data-ttu-id="917b9-115">例如，当应用程序在 iOS 或 UWP 上使用提前编译时，反射 API 具有不同的性能特征。</span><span class="sxs-lookup"><span data-stu-id="917b9-115">For example, reflection APIs have different performance characteristics when an application uses ahead-of-time compilation on iOS or UWP.</span></span>

> [!TIP]
> <span data-ttu-id="917b9-116">.NET 团队[提供了 Roslyn 分析器](../analyzers/api-analyzer.md)，可帮助你发现可能存在的问题。</span><span class="sxs-lookup"><span data-stu-id="917b9-116">The .NET team [offers a Roslyn analyzer](../analyzers/api-analyzer.md) to help you discover possible issues.</span></span>

<span data-ttu-id="917b9-117">✔️ 请务必首先包含一个 `netstandard2.0` 目标。</span><span class="sxs-lookup"><span data-stu-id="917b9-117">✔️ DO start with including a `netstandard2.0` target.</span></span>

> <span data-ttu-id="917b9-118">最常规用途的库应该不需要除 .NET Standard 2.0 之外的其他 API。</span><span class="sxs-lookup"><span data-stu-id="917b9-118">Most general-purpose libraries should not need APIs outside of .NET Standard 2.0.</span></span> <span data-ttu-id="917b9-119">所有新式平台都支持 .NET Standard 2.0，并且它是支持具有一个目标的多个平台的推荐方法。</span><span class="sxs-lookup"><span data-stu-id="917b9-119">.NET Standard 2.0 is supported by all modern platforms and is the recommended way to support multiple platforms with one target.</span></span>

<span data-ttu-id="917b9-120">❌ 请避免包含 `netstandard1.x` 目标。</span><span class="sxs-lookup"><span data-stu-id="917b9-120">❌ AVOID including a `netstandard1.x` target.</span></span>

> <span data-ttu-id="917b9-121">.NET Standard 1.x 作为一组精细的 NuGet 包分发，它创建了一个大型的包依赖项关系图，并导致开发人员在构建时下载大量的包。</span><span class="sxs-lookup"><span data-stu-id="917b9-121">.NET Standard 1.x is distributed as a granular set of NuGet packages, which creates a large package dependency graph and results in developers downloading a lot of packages when building.</span></span> <span data-ttu-id="917b9-122">新式 .NET 平台（包括 .NET Framework 4.6.1、UWP 和 Xamarin）全部支持 .NET Standard 2.0。</span><span class="sxs-lookup"><span data-stu-id="917b9-122">Modern .NET platforms, including .NET Framework 4.6.1, UWP and Xamarin, all support .NET Standard 2.0.</span></span> <span data-ttu-id="917b9-123">如果需要专门面向较旧的平台，则只能面向 .NET Standard。</span><span class="sxs-lookup"><span data-stu-id="917b9-123">You should only target .NET Standard 1.x if you specifically need to target an older platform.</span></span>

<span data-ttu-id="917b9-124">✔️ 如果需要面向 `netstandard1.x` 目标，请务必包括 `netstandard2.0` 目标。</span><span class="sxs-lookup"><span data-stu-id="917b9-124">✔️ DO include a `netstandard2.0` target if you require a `netstandard1.x` target.</span></span>

> <span data-ttu-id="917b9-125">所有支持 .NET Standard 2.0 的平台都将使用 `netstandard2.0` 目标，并从较小的包关系图中受益，而较旧的平台仍然可以正常运行并回退到使用 `netstandard1.x` 目标。</span><span class="sxs-lookup"><span data-stu-id="917b9-125">All platforms supporting .NET Standard 2.0 will use the `netstandard2.0` target and benefit from having a smaller package graph while older platforms will still work and fall back to using the `netstandard1.x` target.</span></span>

<span data-ttu-id="917b9-126">❌ 如果库依赖于平台特定的应用模型，请避免包括 .NET Standard 目标。</span><span class="sxs-lookup"><span data-stu-id="917b9-126">❌ DO NOT include a .NET Standard target if the library relies on a platform-specific app model.</span></span>

> <span data-ttu-id="917b9-127">例如，UWP 控件工具包库依赖的应用模型只能在 UWP 上使用。</span><span class="sxs-lookup"><span data-stu-id="917b9-127">For example, a UWP control toolkit library depends on an app model that is only available on UWP.</span></span> <span data-ttu-id="917b9-128">特定于应用模型的 API 将无法在 .NET Standard 中使用。</span><span class="sxs-lookup"><span data-stu-id="917b9-128">App model specific APIs will not be available in .NET Standard.</span></span>

## <a name="multi-targeting"></a><span data-ttu-id="917b9-129">多目标</span><span class="sxs-lookup"><span data-stu-id="917b9-129">Multi-targeting</span></span>

<span data-ttu-id="917b9-130">有时，需要从库中访问特定于框架的 API。</span><span class="sxs-lookup"><span data-stu-id="917b9-130">Sometimes you need to access framework-specific APIs from your libraries.</span></span> <span data-ttu-id="917b9-131">调用特定于框架的 API 的最佳方法是使用多目标，它为许多（而不是仅为一个）[.NET 目标框架](../frameworks.md)构建项目。</span><span class="sxs-lookup"><span data-stu-id="917b9-131">The best way to call framework-specific APIs is using multi-targeting, which builds your project for many [.NET target frameworks](../frameworks.md) rather than for just one.</span></span>

<span data-ttu-id="917b9-132">为了让使用者不必针对各个框架构建，应该尽量获取 .NET Standard 输出以及一个或多个特定于框架的输出。</span><span class="sxs-lookup"><span data-stu-id="917b9-132">To shield your consumers from having to build for individual frameworks, you should strive to have a .NET Standard output plus one or more framework-specific outputs.</span></span> <span data-ttu-id="917b9-133">通过多目标，所有程序集都打包在一个 NuGet 包中。</span><span class="sxs-lookup"><span data-stu-id="917b9-133">With multi-targeting, all assemblies are packaged inside a single NuGet package.</span></span> <span data-ttu-id="917b9-134">然后，使用者可以引用同一个包，NuGet 将选择适当的实现。</span><span class="sxs-lookup"><span data-stu-id="917b9-134">Consumers can then reference the same package and NuGet will pick the appropriate implementation.</span></span> <span data-ttu-id="917b9-135">你的 .NET Standard 库充当在任何地方使用的回退库（NuGet 包提供特定于框架的实现的情况除外）。</span><span class="sxs-lookup"><span data-stu-id="917b9-135">Your .NET Standard library serves as the fallback library that is used everywhere, except for the cases where your NuGet package offers a framework-specific implementation.</span></span> <span data-ttu-id="917b9-136">通过多目标可以在代码中使用条件编译并调用特定于框架的 API。</span><span class="sxs-lookup"><span data-stu-id="917b9-136">Multi-targeting allows you to use conditional compilation in your code and call framework-specific APIs.</span></span>

<span data-ttu-id="917b9-137">![包含多个程序集的 NuGet 包](./media/cross-platform-targeting/nuget-package-multiple-assemblies.png "包含多个程序集的 NuGet 包")</span><span class="sxs-lookup"><span data-stu-id="917b9-137">![NuGet package with multiple assemblies](./media/cross-platform-targeting/nuget-package-multiple-assemblies.png "NuGet package with multiple assemblies")</span></span>

<span data-ttu-id="917b9-138">✔️ 请在面向 .NET Standard 的基础上考虑面向 .NET 实现。</span><span class="sxs-lookup"><span data-stu-id="917b9-138">✔️ CONSIDER targeting .NET implementations in addition to .NET Standard.</span></span>

> <span data-ttu-id="917b9-139">通过面向 .NET 实现，可以调用 .NET Standard 范围之外的特定于平台的 API。</span><span class="sxs-lookup"><span data-stu-id="917b9-139">Targeting .NET implementations allows you to call platform-specific APIs that are outside of .NET Standard.</span></span>
>
> <span data-ttu-id="917b9-140">执行此操作时，请不要放弃对 .NET Standard 的支持。</span><span class="sxs-lookup"><span data-stu-id="917b9-140">Do not drop support for .NET Standard when you do this.</span></span> <span data-ttu-id="917b9-141">相反，从实现引发并提供功能 API。</span><span class="sxs-lookup"><span data-stu-id="917b9-141">Instead, throw from the implementation and offer capability APIs.</span></span> <span data-ttu-id="917b9-142">这样一来，你的库可以在任何地方使用，并支持运行时启动功能。</span><span class="sxs-lookup"><span data-stu-id="917b9-142">This way, your library can be used anywhere and supports runtime light-up of features.</span></span>

```csharp
public static class GpsLocation
{
    // This project uses multi-targeting to expose device-specific APIs to .NET Standard.
    public static async Task<(double latitude, double longitude)> GetCoordinatesAsync()
    {
#if NET461
        return CallDotNetFramworkApi();
#elif WINDOWS_UWP
        return CallUwpApi();
#else
        throw new PlatformNotSupportedException();
#endif
    }

    // Allows callers to check without having to catch PlatformNotSupportedException
    // or replicating the OS check.
    public static bool IsSupported
    {
        get
        {
#if NET461 || WINDOWS_UWP
            return true;
#else
            return false;
#endif
        }
    }
}
```

<span data-ttu-id="917b9-143">❌ 如果你的源代码源代码对所有目标都相同，请避免多目标以及面向 .NET Standard。</span><span class="sxs-lookup"><span data-stu-id="917b9-143">❌ AVOID multi-targeting as well as targeting .NET Standard, if your source code is the same for all targets.</span></span>

> <span data-ttu-id="917b9-144">.NET Standard 程序集将自动供 NuGet 使用。</span><span class="sxs-lookup"><span data-stu-id="917b9-144">The .NET Standard assembly will automatically be used by NuGet.</span></span> <span data-ttu-id="917b9-145">面向单个 .NET 实现会增加 `*.nupkg` 大小，不会提供任何好处。</span><span class="sxs-lookup"><span data-stu-id="917b9-145">Targeting individual .NET implementations increases the `*.nupkg` size for no benefit.</span></span>

<span data-ttu-id="917b9-146">✔️ 请考虑在提供 `netstandard2.0` 目标时为 `net461` 添加目标。</span><span class="sxs-lookup"><span data-stu-id="917b9-146">✔️ CONSIDER adding a target for `net461` when you're offering a `netstandard2.0` target.</span></span>

> <span data-ttu-id="917b9-147">在 .NET Framework 中使用 .NET Standard 2.0 存在一些问题，这些在 .NET Framework 4.7.2 中已得到解决。</span><span class="sxs-lookup"><span data-stu-id="917b9-147">Using .NET Standard 2.0 from .NET Framework has some issues that were addressed in .NET Framework 4.7.2.</span></span> <span data-ttu-id="917b9-148">可以为仍在使用 .NET Framework 4.6.1 - 4.7.1 的开发人员提供为 .NET Framework 4.6.1 构建的二进制文件，从而改善其体验。</span><span class="sxs-lookup"><span data-stu-id="917b9-148">You can improve the experience for developers that are still on .NET Framework 4.6.1 - 4.7.1 by offering them a binary that is built for .NET Framework 4.6.1.</span></span>

<span data-ttu-id="917b9-149">✔️ 请使用 NuGet 包分发库。</span><span class="sxs-lookup"><span data-stu-id="917b9-149">✔️ DO distribute your library using a NuGet package.</span></span>

> <span data-ttu-id="917b9-150">NuGet 将为开发人员选择最佳目标，使他们无需选择适当实现。</span><span class="sxs-lookup"><span data-stu-id="917b9-150">NuGet will select the best target for the developer and shield them having to pick the appropriate implementation.</span></span>

<span data-ttu-id="917b9-151">✔️ 请务必在使用多目标时使用项目文件的 `TargetFrameworks` 属性。</span><span class="sxs-lookup"><span data-stu-id="917b9-151">✔️ DO use a project file's `TargetFrameworks` property when multi-targeting.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <!-- This project will output netstandard2.0 and net461 assemblies -->
    <TargetFrameworks>netstandard2.0;net461</TargetFrameworks>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="917b9-152">✔️ 请考虑在对 UWP 和 Xamarin 进行多目标定位时使用 [MSBuild.Sdk.Extras](https://github.com/onovotny/MSBuildSdkExtras)，它可以极大地简化项目文件。</span><span class="sxs-lookup"><span data-stu-id="917b9-152">✔️ CONSIDER using [MSBuild.Sdk.Extras](https://github.com/onovotny/MSBuildSdkExtras) when multi-targeting for UWP and Xamarin as it greatly simplifies your project file.</span></span>

## <a name="older-targets"></a><span data-ttu-id="917b9-153">较旧的目标</span><span class="sxs-lookup"><span data-stu-id="917b9-153">Older targets</span></span>

<span data-ttu-id="917b9-154">.NET 支持长期不受支持的 .NET Framework 的目标版本以及不再经常使用的平台。</span><span class="sxs-lookup"><span data-stu-id="917b9-154">.NET supports targeting versions of the .NET Framework that are long out of support as well as platforms that are no longer commonly used.</span></span> <span data-ttu-id="917b9-155">尽管使库在尽可能多的目标上工作是有价值的，但这种情况下必须解决缺少的 API 问题，这会增加很大的开销。</span><span class="sxs-lookup"><span data-stu-id="917b9-155">While there's value in making your library work on as many targets as possible, having to work around missing APIs can add significant overhead.</span></span> <span data-ttu-id="917b9-156">考虑到某些框架的使用范围和局限性，我们认为不再值得面向这些框架。</span><span class="sxs-lookup"><span data-stu-id="917b9-156">We believe certain frameworks are no longer worth targeting, considering their reach and limitations.</span></span>

<span data-ttu-id="917b9-157">❌ 请避免包括可移植类库 (PCL) 目标。</span><span class="sxs-lookup"><span data-stu-id="917b9-157">❌ DO NOT include a Portable Class Library (PCL) target.</span></span> <span data-ttu-id="917b9-158">例如，`portable-net45+win8+wpa81+wp8` 。</span><span class="sxs-lookup"><span data-stu-id="917b9-158">For example, `portable-net45+win8+wpa81+wp8`.</span></span>

> <span data-ttu-id="917b9-159">.NET standard 是支持跨平台 .NET 库的新式方法，它可以替代 PCL。</span><span class="sxs-lookup"><span data-stu-id="917b9-159">.NET Standard is the modern way to support cross-platform .NET libraries and replaces PCLs.</span></span>

<span data-ttu-id="917b9-160">❌ 请避免包括面向不再受支持的 .NET 平台的目标。</span><span class="sxs-lookup"><span data-stu-id="917b9-160">❌ DO NOT include targets for .NET platforms that are no longer supported.</span></span> <span data-ttu-id="917b9-161">例如：`SL4`、`WP`。</span><span class="sxs-lookup"><span data-stu-id="917b9-161">For example, `SL4`, `WP`.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="917b9-162">[上一页](get-started.md)
>[下一页](strong-naming.md)</span><span class="sxs-lookup"><span data-stu-id="917b9-162">[Previous](get-started.md)
[Next](strong-naming.md)</span></span>
