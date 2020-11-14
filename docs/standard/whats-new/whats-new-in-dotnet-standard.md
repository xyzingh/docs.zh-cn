---
title: .NET Standard 中的新增功能
description: 本文总结了所有新版 .NET Standard 中的新功能和增强功能。
ms.custom: updateeachrelease
ms.date: 04/12/2018
ms.technology: dotnet-standard
ms.openlocfilehash: 419988901923b890aaf0a540d155775214e62c52
ms.sourcegitcommit: 74d05613d6c57106f83f82ce8ee71176874ea3f0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93282104"
---
# <a name="whats-new-in-net-standard"></a><span data-ttu-id="3d96e-103">.NET Standard 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="3d96e-103">What's new in .NET Standard</span></span>

<span data-ttu-id="3d96e-104">.NET Standard 是一种正式规范，它定义了一组版本化 API。这些 API 必须可用于符合相应 Standard 版本要求的 .NET 实现。</span><span class="sxs-lookup"><span data-stu-id="3d96e-104">.NET Standard is a formal specification that defines a versioned set of APIs that must be available on .NET implementations that comply with that version of the standard.</span></span> <span data-ttu-id="3d96e-105">.NET Standard 面向库开发者。</span><span class="sxs-lookup"><span data-stu-id="3d96e-105">.NET Standard is targeted at library developers.</span></span> <span data-ttu-id="3d96e-106">定目标到 .NET Standard 版本的库可用于任意 .NET Framework、.NET Core 或支持 Standard 版本的 Xamarin 实现。</span><span class="sxs-lookup"><span data-stu-id="3d96e-106">A library that targets a .NET Standard version can be used on any .NET Framework, .NET Core, or Xamarin implementation that supports that version of the standard.</span></span>

<span data-ttu-id="3d96e-107">.NET Core SDK 及选择 .NET Core 工作负载时的 Visual Studio 包含 .NET Standard。</span><span class="sxs-lookup"><span data-stu-id="3d96e-107">.NET Standard is included with the .NET Core SDK, as well as with Visual Studio when you select the .NET Core workload.</span></span>

## <a name="supported-net-implementations"></a><span data-ttu-id="3d96e-108">支持的 .NET 实现</span><span class="sxs-lookup"><span data-stu-id="3d96e-108">Supported .NET implementations</span></span>

<span data-ttu-id="3d96e-109">以下 .NET 实现支持 .NET Standard 2.0：</span><span class="sxs-lookup"><span data-stu-id="3d96e-109">.NET Standard 2.0 is supported by the following .NET implementations:</span></span>

- <span data-ttu-id="3d96e-110">.NET Core 2.0 或更高版本</span><span class="sxs-lookup"><span data-stu-id="3d96e-110">.NET Core 2.0 or later</span></span>
- <span data-ttu-id="3d96e-111">.NET Framework 4.6.1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="3d96e-111">.NET Framework 4.6.1 or later</span></span>
- <span data-ttu-id="3d96e-112">Mono 5.4 或更高版本</span><span class="sxs-lookup"><span data-stu-id="3d96e-112">Mono 5.4 or later</span></span>
- <span data-ttu-id="3d96e-113">Xamarin.iOS 10.14 或更高版本</span><span class="sxs-lookup"><span data-stu-id="3d96e-113">Xamarin.iOS 10.14 or later</span></span>
- <span data-ttu-id="3d96e-114">Xamarin.Mac 3.8 或更高版本</span><span class="sxs-lookup"><span data-stu-id="3d96e-114">Xamarin.Mac 3.8 or later</span></span>
- <span data-ttu-id="3d96e-115">Xamarin.Android 8.0 或更高版本</span><span class="sxs-lookup"><span data-stu-id="3d96e-115">Xamarin.Android 8.0 or later</span></span>
- <span data-ttu-id="3d96e-116">通用 Windows 平台 10.0.16299 或更高版本</span><span class="sxs-lookup"><span data-stu-id="3d96e-116">Universal Windows Platform 10.0.16299 or later</span></span>

## <a name="whats-new-in-net-standard-20"></a><span data-ttu-id="3d96e-117">.NET Standard 2.0 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="3d96e-117">What's new in .NET Standard 2.0</span></span>

<span data-ttu-id="3d96e-118">.NET Standard 2.0 新增了以下功能：</span><span class="sxs-lookup"><span data-stu-id="3d96e-118">.NET Standard 2.0 includes the following new features:</span></span>

### <a name="a-vastly-expanded-set-of-apis"></a><span data-ttu-id="3d96e-119">大幅扩展了 API 集</span><span class="sxs-lookup"><span data-stu-id="3d96e-119">A vastly expanded set of APIs</span></span>

<span data-ttu-id="3d96e-120">.NET Standard 版本 1.6 中包含了相对较小的一部分 API。</span><span class="sxs-lookup"><span data-stu-id="3d96e-120">Through version 1.6, .NET Standard included a comparatively small subset of APIs.</span></span> <span data-ttu-id="3d96e-121">不包含的 API 许多都是 .NET Framework 或 Xamarin 中的常用 API。</span><span class="sxs-lookup"><span data-stu-id="3d96e-121">Among those excluded were many APIs that were commonly used in .NET Framework or Xamarin.</span></span> <span data-ttu-id="3d96e-122">这样一来，开发变得更为棘手，因为开发人员必须在开发定目标到多个 .NET 实现的应用和库时，寻找常用 API 的合适替代项。</span><span class="sxs-lookup"><span data-stu-id="3d96e-122">This complicates development, since it requires that developers find suitable replacements for familiar APIs when they develop applications and libraries that target multiple .NET implementations.</span></span> <span data-ttu-id="3d96e-123">为了消除此限制，.NET Standard 2.0 向 Standard 旧版本 .NET Standard 1.6 中的可用 API 补充了 20,000 多个 API。</span><span class="sxs-lookup"><span data-stu-id="3d96e-123">.NET Standard 2.0 addresses this limitation by adding over 20,000 more APIs than were available in .NET Standard 1.6, the previous version of the standard.</span></span> <span data-ttu-id="3d96e-124">有关添加到 .NET Standard 2.0 的 API 列表，请参阅 [.NET Standard 2.0 与 1.6](https://raw.githubusercontent.com/dotnet/standard/master/docs/versions/netstandard2.0_diff.md)。</span><span class="sxs-lookup"><span data-stu-id="3d96e-124">For a list of the APIs that have been added to .NET Standard 2.0, see [.NET Standard 2.0 vs 1.6](https://raw.githubusercontent.com/dotnet/standard/master/docs/versions/netstandard2.0_diff.md).</span></span>

<span data-ttu-id="3d96e-125">.NET Standard 2.0 的 <xref:System> 命名空间中新增的一些功能包括：</span><span class="sxs-lookup"><span data-stu-id="3d96e-125">Some of the additions to the <xref:System> namespace in .NET Standard 2.0 include:</span></span>

- <span data-ttu-id="3d96e-126">支持 <xref:System.AppDomain> 类。</span><span class="sxs-lookup"><span data-stu-id="3d96e-126">Support for the <xref:System.AppDomain> class.</span></span>
- <span data-ttu-id="3d96e-127">更好地支持通过 <xref:System.Array> 类中的附加成员处理数组。</span><span class="sxs-lookup"><span data-stu-id="3d96e-127">Better support for working with arrays from additional members in the <xref:System.Array> class.</span></span>
- <span data-ttu-id="3d96e-128">更好地支持通过 <xref:System.Attribute> 类中的附加成员处理属性。</span><span class="sxs-lookup"><span data-stu-id="3d96e-128">Better support for working with attributes from additional members in the <xref:System.Attribute> class.</span></span>
- <span data-ttu-id="3d96e-129">改进了日历支持，并附加了 <xref:System.DateTime> 值的格式设置选项。</span><span class="sxs-lookup"><span data-stu-id="3d96e-129">Better calendar support and additional formatting options for <xref:System.DateTime> values.</span></span>
- <span data-ttu-id="3d96e-130">附加了 <xref:System.Decimal> 舍入功能。</span><span class="sxs-lookup"><span data-stu-id="3d96e-130">Additional <xref:System.Decimal> rounding functionality.</span></span>
- <span data-ttu-id="3d96e-131">在 <xref:System.Environment> 类中附加了功能。</span><span class="sxs-lookup"><span data-stu-id="3d96e-131">Additional functionality in the <xref:System.Environment> class.</span></span>
- <span data-ttu-id="3d96e-132">增强了通过 <xref:System.GC> 类控制垃圾回收器。</span><span class="sxs-lookup"><span data-stu-id="3d96e-132">Enhanced control over the garbage collector through the <xref:System.GC> class.</span></span>
- <span data-ttu-id="3d96e-133">增强了 <xref:System.String> 类中的字符串比较、枚举和规范化支持。</span><span class="sxs-lookup"><span data-stu-id="3d96e-133">Enhanced support for string comparison, enumeration, and normalization in the <xref:System.String> class.</span></span>
- <span data-ttu-id="3d96e-134"><xref:System.TimeZoneInfo.AdjustmentRule> 和 <xref:System.TimeZoneInfo.TransitionTime> 类支持夏令时调整和时间转换。</span><span class="sxs-lookup"><span data-stu-id="3d96e-134">Support for daylight saving adjustments and transition times in the <xref:System.TimeZoneInfo.AdjustmentRule> and <xref:System.TimeZoneInfo.TransitionTime> classes.</span></span>
- <span data-ttu-id="3d96e-135">显著改进了 <xref:System.Type> 类中的功能。</span><span class="sxs-lookup"><span data-stu-id="3d96e-135">Significantly enhanced functionality in the <xref:System.Type> class.</span></span>
- <span data-ttu-id="3d96e-136">通过添加包含 <xref:System.Runtime.Serialization.SerializationInfo> 和 <xref:System.Runtime.Serialization.StreamingContext> 参数的异常构造函数，改进了对异常对象反序列化的支持。</span><span class="sxs-lookup"><span data-stu-id="3d96e-136">Better support for deserialization of exception objects by adding an exception constructor with <xref:System.Runtime.Serialization.SerializationInfo> and <xref:System.Runtime.Serialization.StreamingContext> parameters.</span></span>

### <a name="support-for-net-framework-libraries"></a><span data-ttu-id="3d96e-137">支持 .NET Framework 库</span><span class="sxs-lookup"><span data-stu-id="3d96e-137">Support for .NET Framework libraries</span></span>

<span data-ttu-id="3d96e-138">许多库定目标到 .NET Framework，而不是 .NET Standard。</span><span class="sxs-lookup"><span data-stu-id="3d96e-138">Many libraries target .NET Framework rather than .NET Standard.</span></span> <span data-ttu-id="3d96e-139">不过，这些库大多调用的是 .NET Standard 2.0 中的 API。</span><span class="sxs-lookup"><span data-stu-id="3d96e-139">However, most of the calls in those libraries are to APIs that are included in .NET Standard 2.0.</span></span> <span data-ttu-id="3d96e-140">自 .NET Standard 2.0 起，可以使用[兼容性填充码](https://github.com/dotnet/standard/blob/master/docs/planning/netstandard-2.0/README.md#assembly-unification)从 .NET Standard 库访问 .NET Framework 库。</span><span class="sxs-lookup"><span data-stu-id="3d96e-140">Starting with .NET Standard 2.0, you can access .NET Framework libraries from a .NET Standard library by using a [compatibility shim](https://github.com/dotnet/standard/blob/master/docs/planning/netstandard-2.0/README.md#assembly-unification).</span></span> <span data-ttu-id="3d96e-141">此兼容性层对开发人员透明；无需执行任何操作，即可使用 .NET Framework 库。</span><span class="sxs-lookup"><span data-stu-id="3d96e-141">This compatibility layer is transparent to developers; you don't have to do anything to take advantage of .NET Framework libraries.</span></span>

<span data-ttu-id="3d96e-142">只有一项要求就是，.NET Framework 类库调用的 API 必须是 .NET Standard 2.0 中的 API。</span><span class="sxs-lookup"><span data-stu-id="3d96e-142">The single requirement is that the APIs called by the .NET Framework class library must be included in .NET Standard 2.0.</span></span>

### <a name="support-for-visual-basic"></a><span data-ttu-id="3d96e-143">支持 Visual Basic</span><span class="sxs-lookup"><span data-stu-id="3d96e-143">Support for Visual Basic</span></span>

<span data-ttu-id="3d96e-144">现在可以使用 Visual Basic 开发 .NET Standard 库。</span><span class="sxs-lookup"><span data-stu-id="3d96e-144">You can now develop .NET Standard libraries in Visual Basic.</span></span> <span data-ttu-id="3d96e-145">安装了 .NET Core 工作负载的 Visual Studio 2019 和 Visual Studio 2017 版本 15.3 或更高版本包含 .NET Standard 类库模板。</span><span class="sxs-lookup"><span data-stu-id="3d96e-145">Visual Studio 2019 and Visual Studio 2017 version 15.3 or later with the .NET Core workload installed include a .NET Standard Class Library template.</span></span> <span data-ttu-id="3d96e-146">对于使用其他开发工具和环境的 Visual Basic 开发人员，可以使用 [dotnet new](../../core/tools/dotnet-new.md) 命令创建 .NET Standard 库项目。</span><span class="sxs-lookup"><span data-stu-id="3d96e-146">For Visual Basic developers who use other development tools and environments, you can use the [dotnet new](../../core/tools/dotnet-new.md) command to create a .NET Standard Library project.</span></span> <span data-ttu-id="3d96e-147">有关详细信息，请参阅 [.NET Standard 库的工具支持](#tooling-support-for-net-standard-libraries)。</span><span class="sxs-lookup"><span data-stu-id="3d96e-147">For more information, see the [Tooling support for .NET Standard libraries](#tooling-support-for-net-standard-libraries).</span></span>

### <a name="tooling-support-for-net-standard-libraries"></a><span data-ttu-id="3d96e-148">.NET Standard 库的工具支持</span><span class="sxs-lookup"><span data-stu-id="3d96e-148">Tooling support for .NET Standard libraries</span></span>

<span data-ttu-id="3d96e-149">随着 .NET Core 2.0 和 .NET Standard 2.0 发布，Visual Studio 2017 和 [.NET Core CLI](../../core/tools/index.md) 均包含创建 .NET Standard 库所需的工具支持。</span><span class="sxs-lookup"><span data-stu-id="3d96e-149">With the release of .NET Core 2.0 and .NET Standard 2.0, both Visual Studio 2017 and the [.NET Core CLI](../../core/tools/index.md) include tooling support for creating .NET Standard libraries.</span></span>

<span data-ttu-id="3d96e-150">如果安装含 .NET Core 跨平台开发工作负荷  的 Visual Studio，可以使用项目模板创建 .NET Standard 2.0 库项目，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="3d96e-150">If you install Visual Studio with the **.NET Core cross-platform development** workload, you can create a .NET Standard 2.0 library project by using a project template, as the following figure shows:</span></span>

<!-- markdownlint-disable MD025 -->

# <a name="c"></a>[<span data-ttu-id="3d96e-151">C#</span><span class="sxs-lookup"><span data-stu-id="3d96e-151">C#</span></span>](#tab/csharp)

![添加新的 .NET Standard 库项目](./media/std-project-cs.png)

<span data-ttu-id="3d96e-153">如果使用的是 .NET Core CLI，可以运行下面的 [dotnet new](../../core/tools/dotnet-new.md) 命令，以创建以 .NET Standard 2.0 为目标的类库项目：</span><span class="sxs-lookup"><span data-stu-id="3d96e-153">If you're using the .NET Core CLI, the following [dotnet new](../../core/tools/dotnet-new.md) command creates a class library project that targets .NET Standard 2.0:</span></span>

```dotnetcli
dotnet new classlib
```

# <a name="visual-basic"></a>[<span data-ttu-id="3d96e-154">Visual Basic</span><span class="sxs-lookup"><span data-stu-id="3d96e-154">Visual Basic</span></span>](#tab/vb)

![添加新的 .NET Standard 库项目](./media/std-project-vb.png)

<span data-ttu-id="3d96e-156">如果使用的是 .NET Core CLI，可以运行下面的 [dotnet new](../../core/tools/dotnet-new.md) 命令，以创建以 .NET Standard 2.0 为目标的类库项目：</span><span class="sxs-lookup"><span data-stu-id="3d96e-156">If you're using the .NET Core CLI, the following [dotnet new](../../core/tools/dotnet-new.md) command creates a class library project that targets .NET Standard 2.0:</span></span>

```dotnetcli
dotnet new classlib -lang vb
```

---

## <a name="see-also"></a><span data-ttu-id="3d96e-157">请参阅</span><span class="sxs-lookup"><span data-stu-id="3d96e-157">See also</span></span>

- [<span data-ttu-id="3d96e-158">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="3d96e-158">.NET Standard</span></span>](../net-standard.md)
- [<span data-ttu-id="3d96e-159">.NET Standard 简介</span><span class="sxs-lookup"><span data-stu-id="3d96e-159">Introducing .NET Standard</span></span>](https://devblogs.microsoft.com/dotnet/introducing-net-standard/)
