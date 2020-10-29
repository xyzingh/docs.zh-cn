---
title: 分析依赖项将代码移植到 .NET Core
description: 了解如何分析外部依赖项，以便将项目从 .NET Framework 移植到 .NET Core。
author: cartermp
ms.date: 10/22/2019
ms.openlocfilehash: 430da45052e3953ab49f182b1773fc6d74bd2221
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223607"
---
# <a name="analyze-your-dependencies-to-port-code-to-net-core"></a><span data-ttu-id="a6a0e-103">分析依赖项将代码移植到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="a6a0e-103">Analyze your dependencies to port code to .NET Core</span></span>

<span data-ttu-id="a6a0e-104">若要将代码移植到 .NET Core 或.NET Standard，必须了解依赖项。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-104">To port your code to .NET Core or .NET Standard, you must understand your dependencies.</span></span> <span data-ttu-id="a6a0e-105">外部依赖项是在项目中引用但没有自行构建的 NuGet 包或 `.dll` 文件。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-105">External dependencies are the NuGet packages or `.dll` files you reference in your project, but that you don't build yourself.</span></span>

## <a name="migrate-your-nuget-packages-to-packagereference"></a><span data-ttu-id="a6a0e-106">将 NuGet 包迁移到 `PackageReference`</span><span class="sxs-lookup"><span data-stu-id="a6a0e-106">Migrate your NuGet packages to `PackageReference`</span></span>

<span data-ttu-id="a6a0e-107">.NET Core 使用 [PackageReference](/nuget/consume-packages/package-references-in-project-files) 来指定包依赖项。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-107">.NET Core uses [PackageReference](/nuget/consume-packages/package-references-in-project-files) to specify package dependencies.</span></span> <span data-ttu-id="a6a0e-108">如果使用 [packages.config](/nuget/reference/packages-config) 在项目中指定包，则将其转换为 `PackageReference` 格式，因为 .NET Core 不支持 `packages.config`。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-108">If you're using [packages.config](/nuget/reference/packages-config) to specify your packages in your project, convert it to the `PackageReference` format, because `packages.config` isn't supported in .NET Core.</span></span>

<span data-ttu-id="a6a0e-109">如需了解如何迁移，请参阅[从 packages.config 迁移到 PackageReference](/nuget/reference/migrate-packages-config-to-package-reference)一文。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-109">To learn how to migrate, see the [Migrate from packages.config to PackageReference](/nuget/reference/migrate-packages-config-to-package-reference) article.</span></span>

## <a name="upgrade-your-nuget-packages"></a><span data-ttu-id="a6a0e-110">升级 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="a6a0e-110">Upgrade your NuGet packages</span></span>

<span data-ttu-id="a6a0e-111">将项目迁移为 `PackageReference` 格式后，验证包是否与 .NET Core 兼容。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-111">After you migrate your project to the `PackageReference` format, verify if your packages are compatible with .NET Core.</span></span>

<span data-ttu-id="a6a0e-112">首先，请将包升级到可以使用的最新版本。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-112">First, upgrade your packages to the latest version that you can.</span></span> <span data-ttu-id="a6a0e-113">可通过 Visual Studio 中的 NuGet 包管理器 UI 完成此操作。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-113">This can be done with the NuGet Package Manager UI in Visual Studio.</span></span> <span data-ttu-id="a6a0e-114">包依赖项的较新版本可能已经与 .NET Core 兼容。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-114">It's likely that newer versions of your package dependencies are already compatible with .NET Core.</span></span>

## <a name="analyze-your-package-dependencies"></a><span data-ttu-id="a6a0e-115">分析包依赖项</span><span class="sxs-lookup"><span data-stu-id="a6a0e-115">Analyze your package dependencies</span></span>

<span data-ttu-id="a6a0e-116">如果尚未验证转换和升级后的包依赖项是否适用于 .NET Core，可通过以下几种方法实现此目的：</span><span class="sxs-lookup"><span data-stu-id="a6a0e-116">If you haven't already verified that your converted and upgraded package dependencies work on .NET Core, there are a few ways that you can achieve that:</span></span>

### <a name="analyze-nuget-packages-using-nugetorg"></a><span data-ttu-id="a6a0e-117">使用 nuget.org 分析 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="a6a0e-117">Analyze NuGet packages using nuget.org</span></span>

<span data-ttu-id="a6a0e-118">可以在包页面“依赖项”部分的 [nuget.org](https://www.nuget.org/) 上查看每个包所支持的目标框架名字对象 (TFM)  。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-118">You can see the Target Framework Monikers (TFMs) that each package supports on [nuget.org](https://www.nuget.org/) under the **Dependencies** section of the package page.</span></span>

<span data-ttu-id="a6a0e-119">尽管使用站点验证兼容性是一种比较简单的方法，但站点上并未提供所有包的“依赖项”信息  。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-119">Although using the site is an easier method to verify the compatibility, **Dependencies** information isn't available on the site for all packages.</span></span>

### <a name="analyze-nuget-packages-using-nuget-package-explorer"></a><span data-ttu-id="a6a0e-120">使用 NuGet 包资源管理器分析 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="a6a0e-120">Analyze NuGet packages using NuGet Package Explorer</span></span>

<span data-ttu-id="a6a0e-121">NuGet 包本身就是一组包含特定于平台的程序集的文件夹。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-121">A NuGet package is itself a set of folders that contain platform-specific assemblies.</span></span> <span data-ttu-id="a6a0e-122">检查包中是否有包含兼容程序集的文件夹。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-122">Check if there's a folder that contains a compatible assembly inside the package.</span></span>

<span data-ttu-id="a6a0e-123">检查 NuGet 包文件夹最简单方法是使用 [NuGet 包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)工具。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-123">The easiest way to inspect NuGet package folders is to use the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="a6a0e-124">安装完成后，使用以下步骤查看文件夹名称：</span><span class="sxs-lookup"><span data-stu-id="a6a0e-124">After installing it, use the following steps to see the folder names:</span></span>

1. <span data-ttu-id="a6a0e-125">打开 NuGet 包资源管理器。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-125">Open the NuGet Package Explorer.</span></span>
2. <span data-ttu-id="a6a0e-126">单击“从在线源打开包”  。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-126">Click **Open package from online feed** .</span></span>
3. <span data-ttu-id="a6a0e-127">搜索包的名称。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-127">Search for the name of the package.</span></span>
4. <span data-ttu-id="a6a0e-128">从搜索结果中选择包的名称，然后点击“打开”  。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-128">Select the package name from the search results and click **open** .</span></span>
5. <span data-ttu-id="a6a0e-129">展开右侧的“lib”文件夹并查看文件夹名称  。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-129">Expand the *lib* folder on the right-hand side and look at folder names.</span></span>

<span data-ttu-id="a6a0e-130">使用以下模式之一查找具有名称的文件夹：`netstandardX.Y` 或 `netcoreappX.Y`。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-130">Look for a folder with names using one the following patterns: `netstandardX.Y` or `netcoreappX.Y`.</span></span>

<span data-ttu-id="a6a0e-131">这些值是映射到 [.NET Standard](../../standard/net-standard.md) 版本的[目标框架名字对象 (TFM)](../../standard/frameworks.md)、.NET Core 以及与 .NET Core 兼容的传统可移植类库 (PCL) 配置文件。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-131">These values are the [Target Framework Monikers (TFMs)](../../standard/frameworks.md) that map to versions of [.NET Standard](../../standard/net-standard.md), .NET Core, and traditional Portable Class Library (PCL) profiles that are compatible with .NET Core.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6a0e-132">查看包支持的 TFM 时，请注意 `netcoreapp*`，它在兼容时，仅适用于 .NET Core 项目，不适用于 .NET Standard 项目。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-132">When looking at the TFMs that a package supports, note that `netcoreapp*`, while compatible, is for .NET Core projects only and not for .NET Standard projects.</span></span>
> <span data-ttu-id="a6a0e-133">仅面向 `netcoreapp*` 而不是 `netstandard*` 的库只能用于其他 .NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-133">A library that only targets `netcoreapp*` and not `netstandard*` can only be consumed by other .NET Core apps.</span></span>

## <a name="net-framework-compatibility-mode"></a><span data-ttu-id="a6a0e-134">.NET Framework 兼容性模式</span><span class="sxs-lookup"><span data-stu-id="a6a0e-134">.NET Framework compatibility mode</span></span>

<span data-ttu-id="a6a0e-135">在分析完 NuGet 包之后，你可能会发现它们仅面向 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-135">After analyzing the NuGet packages, you might find that they only target the .NET Framework.</span></span>

<span data-ttu-id="a6a0e-136">从 .NET Standard 2.0 开始，引入了 .NET Framework 兼容性模式。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-136">Starting with .NET Standard 2.0, the .NET Framework compatibility mode was introduced.</span></span> <span data-ttu-id="a6a0e-137">此兼容性模式允许 .NET Standard 和 .NET Core 项目引用 .NET Framework 库。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-137">This compatibility mode allows .NET Standard and .NET Core projects to reference .NET Framework libraries.</span></span> <span data-ttu-id="a6a0e-138">引用 .NET Framework 库不适用于所有项目（如库使用 Windows Presentation Foundation (WPF) API 时），但它的开启了很多移植方案。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-138">Referencing .NET Framework libraries doesn't work for all projects, such as if the library uses Windows Presentation Foundation (WPF) APIs, but it does unblock many porting scenarios.</span></span>

<span data-ttu-id="a6a0e-139">在项目中引用面向 .NET Framework 的 NuGet 包时（如 [Huitian.PowerCollections](https://www.nuget.org/packages/Huitian.PowerCollections)），会收到与以下示例类似的包回退警告 ([NU1701](/nuget/reference/errors-and-warnings/nu1701))：</span><span class="sxs-lookup"><span data-stu-id="a6a0e-139">When you reference NuGet packages that target .NET Framework in your project, such as [Huitian.PowerCollections](https://www.nuget.org/packages/Huitian.PowerCollections), you get a package fallback warning ([NU1701](/nuget/reference/errors-and-warnings/nu1701)) similar to the following example:</span></span>

`NU1701: Package ‘Huitian.PowerCollections 1.0.0’ was restored using ‘.NETFramework,Version=v4.6.1’ instead of the project target framework ‘.NETStandard,Version=v2.0’. This package may not be fully compatible with your project.`

<span data-ttu-id="a6a0e-140">当添加包以及每次生成时都会显示该警告，以确保在项目中测试该包。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-140">That warning is displayed when you add the package and every time you build to make sure you test that package with your project.</span></span> <span data-ttu-id="a6a0e-141">如果项目按预期工作，可通过在 Visual Studio 中编辑包属性或在最喜欢的代码编辑器中手动编辑项目文件来取消该警告。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-141">If your project works as expected, you can suppress that warning by editing the package properties in Visual Studio or by manually editing the project file in your favorite code editor.</span></span>

<span data-ttu-id="a6a0e-142">若要通过编辑项目文件来取消警告，请找到要取消警告的包的 `PackageReference` 条目并添加 `NoWarn` 属性。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-142">To suppress the warning by editing the project file, find the `PackageReference` entry for the package you want to suppress the warning for and add the `NoWarn` attribute.</span></span> <span data-ttu-id="a6a0e-143">`NoWarn` 属性接受所有警告 ID 的逗号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-143">The `NoWarn` attribute accepts a comma-separated list of all the warning IDs.</span></span> <span data-ttu-id="a6a0e-144">以下示例显示如何通过手动编辑项目文件来取消 `Huitian.PowerCollections` 包的 `NU1701` 警告：</span><span class="sxs-lookup"><span data-stu-id="a6a0e-144">The following example shows how to suppress the `NU1701` warning for the `Huitian.PowerCollections` package by editing your project file manually:</span></span>

```xml
<ItemGroup>
  <PackageReference Include="Huitian.PowerCollections" Version="1.0.0" NoWarn="NU1701" />
</ItemGroup>
```

<span data-ttu-id="a6a0e-145">有关如何在 Visual Studio 中取消编译器警告的详细信息，请参阅[取消 NuGet 包的警告](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages)。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-145">For more information on how to suppress compiler warnings in Visual Studio, see [Suppressing warnings for NuGet packages](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages).</span></span>

## <a name="what-to-do-when-your-nuget-package-dependency-doesnt-run-on-net-core"></a><span data-ttu-id="a6a0e-146">NuGet 包依赖项未在.NET Core 上运行时应执行的操作</span><span class="sxs-lookup"><span data-stu-id="a6a0e-146">What to do when your NuGet package dependency doesn't run on .NET Core</span></span>

<span data-ttu-id="a6a0e-147">如果所依赖的 NuGet 包无法在 .NET Core 上运行，可以执行以下几项操作：</span><span class="sxs-lookup"><span data-stu-id="a6a0e-147">There are a few things you can do if a NuGet package you depend on doesn't run on .NET Core:</span></span>

- <span data-ttu-id="a6a0e-148">如果项目是开放源代码并托管在诸如 GitHub 中，则可以直接与开发人员交流。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-148">If the project is open source and hosted somewhere like GitHub, you can engage the developers directly.</span></span>
- <span data-ttu-id="a6a0e-149">可直接在 [nuget.org](https://www.nuget.org/) 上联系作者。搜索包并单击包页面左侧的“联系所有者”  。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-149">You can contact the author directly on [nuget.org](https://www.nuget.org/). Search for the package and click **Contact Owners** on the left-hand side of the package's page.</span></span>
- <span data-ttu-id="a6a0e-150">可以搜索在 .NET Core 上运行的其他包，它与所使用的包进行的是相同的任务。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-150">You can search for another package that runs on .NET Core that accomplishes the same task as the package you were using.</span></span>
- <span data-ttu-id="a6a0e-151">可以尝试自己编写包所执行的代码。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-151">You can attempt to write the code the package was doing yourself.</span></span>
- <span data-ttu-id="a6a0e-152">可以通过更改应用的功能来清除对包的依赖性，至少在该包有可用的兼容性版本之前都能这样做。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-152">You could eliminate the dependency on the package by changing the functionality of your app, at least until a compatible version of the package becomes available.</span></span>

<span data-ttu-id="a6a0e-153">请注意，开源项目维护人员和 NuGet 包发布者通常是志愿者。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-153">Remember that open-source project maintainers and NuGet package publishers are often volunteers.</span></span> <span data-ttu-id="a6a0e-154">他们因为关注某个特定领域而免费提供服务，通常从事另外一份职业。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-154">They contribute because they care about a given domain, do it for free, and often have a different daytime job.</span></span> <span data-ttu-id="a6a0e-155">当联系他们请求 .NET Core 支持时请注意这点。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-155">Be mindful of that when contacting them to ask for .NET Core support.</span></span>

<span data-ttu-id="a6a0e-156">如果使用上述任何选项都无法解决问题，则可能需要移植到最近版本的 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-156">If you can't resolve your issue with any of these options, you may have to port to .NET Core at a later date.</span></span>

<span data-ttu-id="a6a0e-157">.NET 团队需要了解哪些库最需要使用 .NET Core 支持。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-157">The .NET Team would like to know which libraries are the most important to support with .NET Core.</span></span> <span data-ttu-id="a6a0e-158">你可以发送电子邮件到 dotnet@microsoft.com，谈谈你想要使用的库。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-158">You can send an email to dotnet@microsoft.com about the libraries you'd like to use.</span></span>

## <a name="analyze-dependencies-that-arent-nuget-packages"></a><span data-ttu-id="a6a0e-159">分析不是 NuGet 包的依赖项</span><span class="sxs-lookup"><span data-stu-id="a6a0e-159">Analyze dependencies that aren't NuGet packages</span></span>

<span data-ttu-id="a6a0e-160">用户可能拥有不是 NuGet 包的依赖项，如文件系统中的 DLL。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-160">You may have a dependency that isn't a NuGet package, such as a DLL in the file system.</span></span> <span data-ttu-id="a6a0e-161">确定该依赖项是否可移植的唯一方法是运行 [.NET 可移植性分析器](https://github.com/Microsoft/dotnet-apiport)工具。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-161">The only way to determine the portability of that dependency is to run the [.NET Portability Analyzer](https://github.com/Microsoft/dotnet-apiport) tool.</span></span> <span data-ttu-id="a6a0e-162">该工具可以分析面向 .NET Framework 的程序集，并识别不可移植到其他 .NET 平台（如 .NET Core）的 API。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-162">The tool analyzes assemblies that target the .NET Framework and identifies APIs that aren't portable to other .NET platforms such as .NET Core.</span></span> <span data-ttu-id="a6a0e-163">可将该工具作为控制台应用程序或作为 [Visual Studio 扩展](../../standard/analyzers/portability-analyzer.md)来运行。</span><span class="sxs-lookup"><span data-stu-id="a6a0e-163">You can run the tool as a console application or as a [Visual Studio extension](../../standard/analyzers/portability-analyzer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6a0e-164">后续步骤</span><span class="sxs-lookup"><span data-stu-id="a6a0e-164">Next steps</span></span>

>[!div class="nextstepaction"]
>[<span data-ttu-id="a6a0e-165">移植库</span><span class="sxs-lookup"><span data-stu-id="a6a0e-165">Port libraries</span></span>](libraries.md)
