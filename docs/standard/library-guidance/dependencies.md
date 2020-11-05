---
title: 依赖项和.NET 库
description: 管理 .NET 库中 NuGet 依赖项的最佳做法建议。
ms.date: 10/02/2018
ms.openlocfilehash: d189a3364b501272e29de72b6018844877bf2128
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93189298"
---
# <a name="dependencies"></a><span data-ttu-id="7b7ca-103">依赖项</span><span class="sxs-lookup"><span data-stu-id="7b7ca-103">Dependencies</span></span>

<span data-ttu-id="7b7ca-104">向 .NET 库添加依赖项的主要方法是引用 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-104">The primary way of adding dependencies to a .NET library is referencing NuGet packages.</span></span> <span data-ttu-id="7b7ca-105">通过 NuGet 包引用，可以快速重用和利用已编写的功能，但它们是 .NET 开发人员产生冲突的一个常见原因。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-105">NuGet package references allow you to quickly reuse and leverage already written functionality, but they're a common source of friction for .NET developers.</span></span> <span data-ttu-id="7b7ca-106">请务必正确管理依赖项，这可以防止其他 .NET 库中的更改破坏你的 .NET 库，反之亦然！</span><span class="sxs-lookup"><span data-stu-id="7b7ca-106">Correctly managing dependencies is important to prevent changes in other .NET libraries from breaking your .NET library, and vice versa!</span></span>

## <a name="diamond-dependencies"></a><span data-ttu-id="7b7ca-107">菱形依赖关系</span><span class="sxs-lookup"><span data-stu-id="7b7ca-107">Diamond dependencies</span></span>

<span data-ttu-id="7b7ca-108">.NET 项目在其依赖关系树中具有多个版本的包，这种情况非常常见。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-108">It's a common situation for a .NET project to have multiple versions of a package in its dependency tree.</span></span> <span data-ttu-id="7b7ca-109">例如，应用程序依赖于两个 NuGet 包，每个包依赖于同一包的不同版本。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-109">For example, an app depends on two NuGet packages, each of which depends on different versions of the same package.</span></span> <span data-ttu-id="7b7ca-110">应用的依赖项关系图中现在存在菱形依赖关系。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-110">A diamond dependency now exists in the app's dependency graph.</span></span>

<span data-ttu-id="7b7ca-111">![菱形依赖关系](./media/dependencies/diamond-dependency.png "菱形依赖关系")</span><span class="sxs-lookup"><span data-stu-id="7b7ca-111">![Diamond dependency](./media/dependencies/diamond-dependency.png "Diamond dependency")</span></span>

<span data-ttu-id="7b7ca-112">在构建时，NuGet 会分析项目依赖的所有包，包括依赖项的依赖项。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-112">At build time, NuGet analyzes all the packages that a project depends on, including the dependencies of dependencies.</span></span> <span data-ttu-id="7b7ca-113">检测到包的多个版本时，将评估规则以便选择一个版本。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-113">When multiple versions of a package are detected, rules are evaluated to pick one.</span></span> <span data-ttu-id="7b7ca-114">统一包是必要的，因为如果在同一个应用程序中运行某个程序集的并行版本，在 .NET 中会出现问题。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-114">Unifying packages is necessary because running side-by-side versions of an assembly in the same application is problematic in .NET.</span></span>

<span data-ttu-id="7b7ca-115">大多数菱形依赖关系很容易解决；但是，在某些情况下，它们可能会引发问题：</span><span class="sxs-lookup"><span data-stu-id="7b7ca-115">Most diamond dependencies are easily resolved; however, they can create issues in certain circumstances:</span></span>

- <span data-ttu-id="7b7ca-116">存在冲突的 NuGet 包引用会导致在包还原期间无法解析版本。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-116">**Conflicting NuGet package references** prevent a version from being resolved during package restore.</span></span>
- <span data-ttu-id="7b7ca-117">各版本之间的重大更改会在运行时导致 bug 和异常。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-117">**Breaking changes between the versions** cause bugs and exceptions at run time.</span></span>
- <span data-ttu-id="7b7ca-118">包程序集具有强名称，程序集版本会发生更改，并且在 .NET Framework 上运行应用。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-118">**The package assembly is strong named** , the assembly version changed, and the app is running on .NET Framework.</span></span> <span data-ttu-id="7b7ca-119">程序集绑定重定向是必需的。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-119">Assembly binding redirects are required.</span></span>

<span data-ttu-id="7b7ca-120">无法确定哪些包将与你自己的包一起使用。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-120">It's not possible to know what packages will be used alongside your own.</span></span> <span data-ttu-id="7b7ca-121">降低菱形依赖关系破坏库的可能性的一个好方法是将依赖的包的数量降至最低。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-121">A good way to reduce the likelihood of a diamond dependency breaking your library is to minimize the number of packages you depend on.</span></span>

<span data-ttu-id="7b7ca-122">✔️ 请务必查看 .NET 库中是否存在不必要的依赖项。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-122">✔️ DO review your .NET library for unnecessary dependencies.</span></span>

## <a name="nuget-dependency-version-ranges"></a><span data-ttu-id="7b7ca-123">NuGet 依赖项版本范围</span><span class="sxs-lookup"><span data-stu-id="7b7ca-123">NuGet dependency version ranges</span></span>

<span data-ttu-id="7b7ca-124">包引用指定允许的有效包的范围。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-124">A package reference specifies the range of valid packages it allows.</span></span> <span data-ttu-id="7b7ca-125">通常情况下，项目文件中的包引用版本是最小版本，并且不存在最大版本。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-125">Typically, the package reference version in the project file is the minimum version and there's no maximum.</span></span>

```xml
<!-- Accepts any version 1.0 and above. -->
<PackageReference Include="ExamplePackage" Version="1.0" />
```

<span data-ttu-id="7b7ca-126">NuGet 在解析依赖关系时使用的规则是 [complex](/nuget/consume-packages/dependency-resolution)，但[默认情况下](/nuget/consume-packages/install-use-packages-visual-studio#install-and-update-options)，NuGet 始终查找适用的最低版本。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-126">The rules that NuGet uses when resolving dependencies are [complex](/nuget/consume-packages/dependency-resolution), but NuGet [by default](/nuget/consume-packages/install-use-packages-visual-studio#install-and-update-options) looks for the lowest applicable version.</span></span> <span data-ttu-id="7b7ca-127">NuGet 倾向于使用最低适用版本，而不使用最高版本，因为最低版本的兼容性问题最少。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-127">NuGet prefers the lowest applicable version over using the highest available because the lowest will have the least compatibility issues.</span></span>

<span data-ttu-id="7b7ca-128">鉴于 NuGet 的最低适用版本规则，没有必要在包引用时放置较高版本或确切范围，以避免获取最新版本。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-128">Because of NuGet's lowest applicable version rule, it isn't necessary to place an upper version or exact range on package references to avoid getting the latest version.</span></span> <span data-ttu-id="7b7ca-129">NuGet 已经尝试为你查找兼容性最高的最低版本。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-129">NuGet already tries to find the lowest, most compatible version for you.</span></span>

```xml
<!-- Accepts 1.0 up to 1.x, but not 2.0 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.0,2.0)" />

<!-- Accepts exactly 1.0. -->
<PackageReference Include="ExamplePackage" Version="[1.0]" />
```

<span data-ttu-id="7b7ca-130">如果存在冲突，较高版本限制将导致 NuGet 失败。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-130">Upper version limits will cause NuGet to fail if there's a conflict.</span></span> <span data-ttu-id="7b7ca-131">例如，一个库接受 1.0 版本，而另一个库需要 2.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-131">For example, one library accepts exactly 1.0 while another library requires 2.0 or above.</span></span> <span data-ttu-id="7b7ca-132">虽然版本 2.0 中可能引入了重大更改，但严格的或上限版本依赖项绝对会出现错误。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-132">While breaking changes may have been introduced in version 2.0, a strict or upper limit version dependency guarantees an error.</span></span>

<span data-ttu-id="7b7ca-133">![菱形依赖关系冲突](./media/dependencies/diamond-dependency-conflict.png "菱形依赖关系冲突")</span><span class="sxs-lookup"><span data-stu-id="7b7ca-133">![Diamond dependency conflict](./media/dependencies/diamond-dependency-conflict.png "Diamond dependency conflict")</span></span>

<span data-ttu-id="7b7ca-134">❌ 请避免执行无最低版本的 NuGet 包引用。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-134">❌ DO NOT have NuGet package references with no minimum version.</span></span>

<span data-ttu-id="7b7ca-135">❌ 请避免使用需要确切版本的 NuGet 包引用。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-135">❌ AVOID NuGet package references that demand an exact version.</span></span>

<span data-ttu-id="7b7ca-136">❌ 请避免执行存在版本上限的 NuGet 包引用。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-136">❌ AVOID NuGet package references with a version upper limit.</span></span>

## <a name="nuget-shared-source-packages"></a><span data-ttu-id="7b7ca-137">NuGet 共享源包</span><span class="sxs-lookup"><span data-stu-id="7b7ca-137">NuGet shared source packages</span></span>

<span data-ttu-id="7b7ca-138">减少外部 NuGet 包依赖项的一种方法是引用共享源包。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-138">One way to reduce external NuGet package dependencies is to reference shared source packages.</span></span> <span data-ttu-id="7b7ca-139">共享源包包含引用时项目中所含的[源代码文件](/nuget/reference/nuspec#including-content-files)。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-139">A shared source package contains [source code files](/nuget/reference/nuspec#including-content-files) that are included in a project when referenced.</span></span> <span data-ttu-id="7b7ca-140">由于只包括使用项目的其余部分编译的源代码文件，因此，没有外部依赖项，也没有存在冲突的可能性。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-140">Because you're just including source code files that are compiled with the rest of your project, there's no external dependency and chance of conflict.</span></span>

<span data-ttu-id="7b7ca-141">共享源包非常适合包含一些小功能。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-141">Shared source packages are great for including small pieces of functionality.</span></span> <span data-ttu-id="7b7ca-142">例如，用于进行 HTTP 调用的帮助程序方法的共享源包。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-142">For example, a shared source package of helper methods for making HTTP calls.</span></span>

<span data-ttu-id="7b7ca-143">![共享源包](./media/dependencies/shared-source-package.png "共享源包")</span><span class="sxs-lookup"><span data-stu-id="7b7ca-143">![Shared source package](./media/dependencies/shared-source-package.png "Shared source package")</span></span>

```xml
<PackageReference Include="Microsoft.Extensions.Buffers.Testing.Sources" PrivateAssets="All" Version="1.0" />
```

<span data-ttu-id="7b7ca-144">![共享源项目](./media/dependencies/shared-source-project.png "共享源项目")</span><span class="sxs-lookup"><span data-stu-id="7b7ca-144">![Shared source project](./media/dependencies/shared-source-project.png "Shared source project")</span></span>

<span data-ttu-id="7b7ca-145">共享源包存在一些限制。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-145">Shared source packages have some limitations.</span></span> <span data-ttu-id="7b7ca-146">它们只能由 `PackageReference` 引用，因此排除了较旧的 `packages.config` 项目。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-146">They can only be referenced by `PackageReference`, so older `packages.config` projects are excluded.</span></span> <span data-ttu-id="7b7ca-147">另外，共享源包只能由具有相同语言类型的项目使用。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-147">Also shared source packages are only usable by projects with the same language type.</span></span> <span data-ttu-id="7b7ca-148">由于这些限制，共享源包最好用于在开源项目中共享功能。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-148">Because of these limitations shared source packages are best used to share functionality within an open-source project.</span></span>

<span data-ttu-id="7b7ca-149">✔️ 请考虑引用共享源包并用于一些小型的内部功能。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-149">✔️ CONSIDER referencing shared source packages for small, internal pieces of functionality.</span></span>

<span data-ttu-id="7b7ca-150">✔️ 请考虑在包提供一些小型内部功能时将其用作共享源包。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-150">✔️ CONSIDER making your package a shared source package if it provides small, internal pieces of functionality.</span></span>

<span data-ttu-id="7b7ca-151">✔️ 请务必使用 `PrivateAssets="All"` 引用共享源包。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-151">✔️ DO reference shared source packages with `PrivateAssets="All"`.</span></span>

> <span data-ttu-id="7b7ca-152">此项设置将告知 NuGet：包只在开发时使用，不应作为公共依赖项公开。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-152">This setting tells NuGet the package is only to be used at development time and shouldn't be exposed as a public dependency.</span></span>

<span data-ttu-id="7b7ca-153">❌ 请避免在公共 API 中包含共享源包类型。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-153">❌ DO NOT have shared source package types in your public API.</span></span>

> <span data-ttu-id="7b7ca-154">共享源类型将编译到引用程序集中，并且无法跨程序集边界进行交换。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-154">Shared source types are compiled into the referencing assembly and can't be exchanged across assembly boundaries.</span></span> <span data-ttu-id="7b7ca-155">例如，一个项目中的共享源 `IRepository` 类型与另一个项目中的同一共享源 `IRepository` 是彼此独立的类型。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-155">For example, a shared-source `IRepository` type in one project is a separate type from the same shared-source `IRepository` in another project.</span></span> <span data-ttu-id="7b7ca-156">共享源包中的类型应具有 `internal` 可见性。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-156">Types in shared source packages should have an `internal` visibility.</span></span>

<span data-ttu-id="7b7ca-157">❌ 请避免将共享源包发布到 NuGet.org。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-157">❌ DO NOT publish shared source packages to NuGet.org.</span></span>

> <span data-ttu-id="7b7ca-158">共享源包包含源代码，只能由具有相同语言类型的项目使用。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-158">Shared source packages contain source code and can only be used by projects with the same language type.</span></span> <span data-ttu-id="7b7ca-159">例如，F# 应用程序无法使用 C# 共享源包。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-159">For example, a C# shared source package cannot be used by an F# application.</span></span>
>
> <span data-ttu-id="7b7ca-160">发布共享源包到[本地数据源或 MyGet](./publish-nuget-package.md)，以在项目内部使用它们。</span><span class="sxs-lookup"><span data-stu-id="7b7ca-160">Publish shared source packages to a [local feed or MyGet](./publish-nuget-package.md) to consume them internally within your project.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="7b7ca-161">[上一页](nuget.md)
>[下一页](sourcelink.md)</span><span class="sxs-lookup"><span data-stu-id="7b7ca-161">[Previous](nuget.md)
[Next](sourcelink.md)</span></span>
