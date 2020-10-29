---
title: .NET 类库
description: 了解如何通过 .NET 类库，将实用功能组合为可供多个应用程序使用的模块。
author: richlander
ms.date: 06/20/2016
ms.technology: dotnet-standard
ms.assetid: a67484c3-fe92-44d8-8fa3-36fa2071d880
ms.openlocfilehash: 35e408ed3552550f19879409128784b2513e56c8
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92224260"
---
# <a name="net-class-libraries"></a><span data-ttu-id="3d81b-103">.NET 类库</span><span class="sxs-lookup"><span data-stu-id="3d81b-103">.NET class libraries</span></span>

<span data-ttu-id="3d81b-104">类库是 .NET 的[共享库](https://en.wikipedia.org/wiki/Library_%28computing%29#Shared_libraries)概念。</span><span class="sxs-lookup"><span data-stu-id="3d81b-104">Class libraries are the [shared library](https://en.wikipedia.org/wiki/Library_%28computing%29#Shared_libraries) concept for .NET.</span></span> <span data-ttu-id="3d81b-105">通过类库可将实用功能组件化为可供多个应用程序使用的模块。</span><span class="sxs-lookup"><span data-stu-id="3d81b-105">They enable you to componentize useful functionality into modules that can be used by multiple applications.</span></span> <span data-ttu-id="3d81b-106">还可使用类库加载应用程序启动时不需要或未知的功能。</span><span class="sxs-lookup"><span data-stu-id="3d81b-106">They can also be used as a means of loading functionality that is not needed or not known at application startup.</span></span> <span data-ttu-id="3d81b-107">类库通过 [.NET 程序集文件格式](assembly/file-format.md)进行描述。</span><span class="sxs-lookup"><span data-stu-id="3d81b-107">Class libraries are described using the [.NET Assembly file format](assembly/file-format.md).</span></span>

<span data-ttu-id="3d81b-108">有三种类型的类库可供使用：</span><span class="sxs-lookup"><span data-stu-id="3d81b-108">There are three types of class libraries that you can use:</span></span>

* <span data-ttu-id="3d81b-109">**平台特定** 的类库可访问给定平台（例如，.NET Framework、Xamarin、iOS）中的所有 API，但只有面向该平台的应用和库可使用该类库。</span><span class="sxs-lookup"><span data-stu-id="3d81b-109">**Platform-specific** class libraries have access to all the APIs in a given platform (for example, .NET Framework, Xamarin iOS), but can only be used by apps and libraries that target that platform.</span></span>
* <span data-ttu-id="3d81b-110">**可移植** 类库可访问 API 的子集，并且可供面向多个平台的应用和库使用。</span><span class="sxs-lookup"><span data-stu-id="3d81b-110">**Portable** class libraries have access to a subset of APIs, and can be used by apps and libraries that target multiple platforms.</span></span>
* <span data-ttu-id="3d81b-111">.NET Standard 类库将平台专用库概念和可移植库概念合并到一个模型中，以同时获取两方面的优势。</span><span class="sxs-lookup"><span data-stu-id="3d81b-111">**.NET Standard** class libraries are a merger of the platform-specific and portable library concept into a single model that provides the best of both.</span></span>

## <a name="platform-specific-class-libraries"></a><span data-ttu-id="3d81b-112">平台特定的类库</span><span class="sxs-lookup"><span data-stu-id="3d81b-112">Platform-specific class libraries</span></span>

<span data-ttu-id="3d81b-113">平台特定的类库绑定到单个 .NET 实现（例如，Windows 上的 .NET Framework），因此它可以在已知的执行环境上接收重要的依赖项。</span><span class="sxs-lookup"><span data-stu-id="3d81b-113">Platform-specific libraries are bound to a single .NET implementation (for example, .NET Framework on Windows) and can therefore take significant dependencies on a known execution environment.</span></span> <span data-ttu-id="3d81b-114">此类环境会公开一组已知 API（.NET 和 OS API），维护并公开预期状态（例如，Windows 注册表）。</span><span class="sxs-lookup"><span data-stu-id="3d81b-114">Such an environment will expose a known set of APIs (.NET and OS APIs) and will maintain and expose expected state (for example, Windows registry).</span></span>

<span data-ttu-id="3d81b-115">创建平台特定的库的开发人员可充分利用基础平台。</span><span class="sxs-lookup"><span data-stu-id="3d81b-115">Developers who create platform-specific libraries can fully exploit the underlying platform.</span></span> <span data-ttu-id="3d81b-116">该库只会在给定平台上运行，因此不需要平台检查和其他形式的条件代码（针对多个平台取模单个源代码）。</span><span class="sxs-lookup"><span data-stu-id="3d81b-116">The libraries will only ever run on that given platform, making platform checks or other forms of conditional code unnecessary (modulo single sourcing code for multiple platforms).</span></span>

<span data-ttu-id="3d81b-117">平台特定的库一直是 .NET Framework 的主要类库类型。</span><span class="sxs-lookup"><span data-stu-id="3d81b-117">Platform-specific libraries have been the primary class library type for the .NET Framework.</span></span> <span data-ttu-id="3d81b-118">即使出现了其他 .NET 实现，平台特定的库也仍然是最主要的类库类型。</span><span class="sxs-lookup"><span data-stu-id="3d81b-118">Even as other .NET implementations emerged, platform-specific libraries remained the dominant library type.</span></span>

## <a name="portable-class-libraries"></a><span data-ttu-id="3d81b-119">可移植类库</span><span class="sxs-lookup"><span data-stu-id="3d81b-119">Portable class libraries</span></span>

<span data-ttu-id="3d81b-120">可移植库支持多个 .NET 实现。</span><span class="sxs-lookup"><span data-stu-id="3d81b-120">Portable libraries are supported on multiple .NET implementations.</span></span> <span data-ttu-id="3d81b-121">该库仍可在已知执行环境上接收依赖项，不过该环境是一种合成环境，由一组具体 .NET 实现的交集生成。</span><span class="sxs-lookup"><span data-stu-id="3d81b-121">They can still take dependencies on a known execution environment, however, the environment is a synthetic one that's generated by the intersection of a set of concrete .NET implementations.</span></span> <span data-ttu-id="3d81b-122">公开的 API 和平台假设是平台特定的库可用的子集。</span><span class="sxs-lookup"><span data-stu-id="3d81b-122">Exposed APIs and platform assumptions are a subset of what would be available to a platform-specific library.</span></span>

<span data-ttu-id="3d81b-123">创建可移植库时，需选择平台配置。</span><span class="sxs-lookup"><span data-stu-id="3d81b-123">You choose a platform configuration when you create a portable library.</span></span> <span data-ttu-id="3d81b-124">平台配置是需要支持的平台集（例如，.NET Framework 4.5+、Windows Phone 8.0+）。</span><span class="sxs-lookup"><span data-stu-id="3d81b-124">The platform configuration is the set of platforms that you need to support (for example, .NET Framework 4.5+, Windows Phone 8.0+).</span></span> <span data-ttu-id="3d81b-125">要支持的平台越多，可生成的 API 和平台假设就越少，公分母越小。</span><span class="sxs-lookup"><span data-stu-id="3d81b-125">The more platforms you opt to support, the fewer APIs and fewer platform assumptions you can make, the lowest common denominator.</span></span> <span data-ttu-id="3d81b-126">这一特性可能最初会令人感到疑惑，因为人们常认为“越多越好”，但却发现更多的支持平台带来的可用 API 更少。</span><span class="sxs-lookup"><span data-stu-id="3d81b-126">This characteristic can be confusing at first, since people often think "more is better" but find that more supported platforms results in fewer available APIs.</span></span>

<span data-ttu-id="3d81b-127">许多库开发人员已经从由一个源开发多个平台特定的库（使用条件编译指令）转向开发可移植库。</span><span class="sxs-lookup"><span data-stu-id="3d81b-127">Many library developers have switched from producing multiple platform-specific libraries from one source (using conditional compilation directives) to portable libraries.</span></span> <span data-ttu-id="3d81b-128">有[多种方法](https://blog.stephencleary.com/2012/11/portable-class-library-enlightenment.html)可在可移植库中访问平台特定的功能，其中“诱饵替换”是目前最广为接受的方法。</span><span class="sxs-lookup"><span data-stu-id="3d81b-128">There are [several approaches](https://blog.stephencleary.com/2012/11/portable-class-library-enlightenment.html) for accessing platform-specific functionality within portable libraries, with bait-and-switch being the most widely accepted technique at this point.</span></span>

## <a name="net-standard-class-libraries"></a><span data-ttu-id="3d81b-129">.NET Standard 类库</span><span class="sxs-lookup"><span data-stu-id="3d81b-129">.NET Standard class libraries</span></span>

<span data-ttu-id="3d81b-130">.NET Standard 库是平台特定的库和可移植库概念的替代。</span><span class="sxs-lookup"><span data-stu-id="3d81b-130">.NET Standard libraries are a replacement of the platform-specific and portable libraries concepts.</span></span> <span data-ttu-id="3d81b-131">.NET Core 库可从基础平台公开所有功能（无合成平台或平台交集），就此而言，它是平台特定的库。</span><span class="sxs-lookup"><span data-stu-id="3d81b-131">They are platform-specific in the sense that they expose all functionality from the underlying platform (no synthetic platforms or platform intersections).</span></span> <span data-ttu-id="3d81b-132">该库可在所有支持平台上运行，就此而言，它是可移植库。</span><span class="sxs-lookup"><span data-stu-id="3d81b-132">They are portable in the sense that they work on all supporting platforms.</span></span>

<span data-ttu-id="3d81b-133">.NET Standard 公开一组库协定。</span><span class="sxs-lookup"><span data-stu-id="3d81b-133">.NET Standard exposes a set of library _contracts_ .</span></span> <span data-ttu-id="3d81b-134">.NET 实现必须完全支持每个协定，否则就全都不支持。</span><span class="sxs-lookup"><span data-stu-id="3d81b-134">.NET implementations must support each contract fully or not at all.</span></span> <span data-ttu-id="3d81b-135">因此，每个实现都支持一组 .NET Standard 协定。</span><span class="sxs-lookup"><span data-stu-id="3d81b-135">Each implementation, therefore, supports a set of .NET Standard contracts.</span></span> <span data-ttu-id="3d81b-136">得出的必然结果是，.NET Standard 类库在支持其协定依赖项的平台上受到支持。</span><span class="sxs-lookup"><span data-stu-id="3d81b-136">The corollary is that each .NET Standard class library is supported on the platforms that support its contract dependencies.</span></span>

<span data-ttu-id="3d81b-137">.NET Standard 不公开整个 .NET Framework 的功能（也不将此作为目标），但相比可移植类库，其公开的 API 更多。</span><span class="sxs-lookup"><span data-stu-id="3d81b-137">.NET Standard does not expose the entire functionality of the .NET Framework (nor is that a goal), however, they do expose many more APIs than Portable Class Libraries.</span></span> <span data-ttu-id="3d81b-138">随着时间推移，将添加更多的 API。</span><span class="sxs-lookup"><span data-stu-id="3d81b-138">More APIs will be added over time.</span></span>

<span data-ttu-id="3d81b-139">下列平台支持 .NET Standard 库：</span><span class="sxs-lookup"><span data-stu-id="3d81b-139">The following platforms support .NET Standard libraries:</span></span>

* <span data-ttu-id="3d81b-140">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3d81b-140">.NET Core</span></span>
* <span data-ttu-id="3d81b-141">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3d81b-141">.NET Framework</span></span>
* <span data-ttu-id="3d81b-142">Mono</span><span class="sxs-lookup"><span data-stu-id="3d81b-142">Mono</span></span>
* <span data-ttu-id="3d81b-143">Xamarin.iOS、Xamarin.Mac、Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="3d81b-143">Xamarin.iOS, Xamarin.Mac, Xamarin.Android</span></span>
* <span data-ttu-id="3d81b-144">通用 Windows 平台 (UWP)</span><span class="sxs-lookup"><span data-stu-id="3d81b-144">Universal Windows Platform (UWP)</span></span>
* <span data-ttu-id="3d81b-145">Windows</span><span class="sxs-lookup"><span data-stu-id="3d81b-145">Windows</span></span>
* <span data-ttu-id="3d81b-146">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="3d81b-146">Windows Phone</span></span>
* <span data-ttu-id="3d81b-147">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="3d81b-147">Windows Phone Silverlight</span></span>

<span data-ttu-id="3d81b-148">有关详细信息，请参阅 [.NET Standard](net-standard.md)。</span><span class="sxs-lookup"><span data-stu-id="3d81b-148">For more information, see [.NET Standard](net-standard.md).</span></span>

## <a name="mono-class-libraries"></a><span data-ttu-id="3d81b-149">Mono 类库</span><span class="sxs-lookup"><span data-stu-id="3d81b-149">Mono class libraries</span></span>

<span data-ttu-id="3d81b-150">Mono 支持多种类库，包括上述三种类型的库。</span><span class="sxs-lookup"><span data-stu-id="3d81b-150">Class libraries are supported on Mono, including the three types of libraries described previously.</span></span> <span data-ttu-id="3d81b-151">Mono 常被（正确地）视为 .NET Framework 的跨平台实现。</span><span class="sxs-lookup"><span data-stu-id="3d81b-151">Mono has often been seen (correctly) as a cross-platform implementation of .NET Framework.</span></span> <span data-ttu-id="3d81b-152">部分原因是，平台特定的 .NET Framework 库可在 Mono 运行时上运行，而无需修改或重新编译。</span><span class="sxs-lookup"><span data-stu-id="3d81b-152">In part, this was because platform-specific .NET Framework libraries could run on the Mono runtime without modification or recompilation.</span></span> <span data-ttu-id="3d81b-153">创建可移植库之前，此特性就已存在，因此在 .NET Framework 和 Mono 之间启用二进制可移植性是显而易见的选择（虽然它只能单向运行）。</span><span class="sxs-lookup"><span data-stu-id="3d81b-153">This characteristic was in place before the creation of portable class libraries, so was an obvious choice to enable binary portability between the .NET Framework and Mono (although it only worked in one direction).</span></span>
