---
title: .NET Framework 的版本兼容性
description: 了解 .NET Framework 版本之间的兼容性，包括后向兼容性和并行执行。
ms.date: 04/02/2019
helpviewer_keywords:
- .NET Framework, version compatibility
- .NET Framework, compatibility with earlier versions
- .NET Framework versions, compatibility
ms.assetid: 2f25e522-456a-48c3-8a53-e5f39275649f
ms.openlocfilehash: 2be9c4e12d6a613e7f1062ec7492b0b99203f39d
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400691"
---
# <a name="version-compatibility"></a><span data-ttu-id="d89dc-103">版本兼容性</span><span class="sxs-lookup"><span data-stu-id="d89dc-103">Version compatibility</span></span>

<span data-ttu-id="d89dc-104">向后兼容性表示为某个平台的特定版本开发的应用程序将在该平台的更高版本上运行。</span><span class="sxs-lookup"><span data-stu-id="d89dc-104">Backward compatibility means that an app that was developed for a particular version of a platform will run on later versions of that platform.</span></span> <span data-ttu-id="d89dc-105">.NET Framework 尝试最大程度地支持后向兼容性：为某个版本的 .NET Framework 编写的源代码应在更高版本的 .NET Framework 上编译，而在某个版本的 .NET Framework 上运行的二进制文件的行为方式应与其在更高版本的 .NET Framework 上的行为方式相同。</span><span class="sxs-lookup"><span data-stu-id="d89dc-105">.NET Framework tries to maximize backward compatibility: Source code written for one version of .NET Framework should compile on later versions of .NET Framework, and binaries that run on one version of .NET Framework should behave identically on later versions of .NET Framework.</span></span>

## <a name="version-compatibility-for-apps"></a><a name="Apps"></a> <span data-ttu-id="d89dc-106">应用的版本兼容性</span><span class="sxs-lookup"><span data-stu-id="d89dc-106">Version compatibility for apps</span></span>

<span data-ttu-id="d89dc-107">默认情况下，应用将在其目标 .NET Framework 版本上运行。</span><span class="sxs-lookup"><span data-stu-id="d89dc-107">By default, an app runs on the version of .NET Framework that it was built for.</span></span> <span data-ttu-id="d89dc-108">如果该版本不存在且应用配置文件未定义支持的版本，则可能出现 .NET Framework 初始化错误。</span><span class="sxs-lookup"><span data-stu-id="d89dc-108">If that version isn't present and the app configuration file doesn't define supported versions, a .NET Framework initialization error may occur.</span></span> <span data-ttu-id="d89dc-109">在此情况下，尝试运行应用程序将失败。</span><span class="sxs-lookup"><span data-stu-id="d89dc-109">In this case, the attempt to run the app will fail.</span></span>

<span data-ttu-id="d89dc-110">若要定义运行应用的特定版本，请将一个或多个 [\<supportedRuntime>](../configure-apps/file-schema/startup/supportedruntime-element.md) 元素添加到应用的配置文件中。</span><span class="sxs-lookup"><span data-stu-id="d89dc-110">To define the specific versions on which your app runs, add one or more [\<supportedRuntime>](../configure-apps/file-schema/startup/supportedruntime-element.md) elements to your app's configuration file.</span></span> <span data-ttu-id="d89dc-111">每个 `<supportedRuntime>` 元素都列出了支持的运行时版本，第一个元素指定了优先级最高的版本，最后一个元素指定了优先级最低的版本。</span><span class="sxs-lookup"><span data-stu-id="d89dc-111">Each `<supportedRuntime>` element lists a supported version of the runtime, with the first specifying the most preferred version and the last specifying the least preferred version.</span></span>

```xml
<configuration>
   <startup>
      <supportedRuntime version="v2.0.50727" />
      <supportedRuntime version="v4.0" />
   </startup>
</configuration>
```

<span data-ttu-id="d89dc-112">有关详细信息，请参阅[如何：将应用配置为支持 .NET Framework 4 或 4.x](how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)。</span><span class="sxs-lookup"><span data-stu-id="d89dc-112">For more information, see [How to: Configure an App to Support .NET Framework 4 or 4.x](how-to-configure-an-app-to-support-net-framework-4-or-4-5.md).</span></span>

## <a name="version-compatibility-for-components"></a><span data-ttu-id="d89dc-113">组件的版本兼容性</span><span class="sxs-lookup"><span data-stu-id="d89dc-113">Version compatibility for components</span></span>

<span data-ttu-id="d89dc-114">应用可以控制运行它的 .NET Framework 的版本，但组件不能。</span><span class="sxs-lookup"><span data-stu-id="d89dc-114">An app can control the version of the .NET Framework on which it runs, but a component can't.</span></span> <span data-ttu-id="d89dc-115">因为组件和类库在特定应用的上下文中加载，所以它们会自动在运行应用的 .NET Framework 版本上运行。</span><span class="sxs-lookup"><span data-stu-id="d89dc-115">Components and class libraries are loaded in the context of a particular app, and that's why they automatically run on the version of the .NET Framework that the app runs on.</span></span>

<span data-ttu-id="d89dc-116">由于存在此限制，因此兼容性保证对组件特别重要。</span><span class="sxs-lookup"><span data-stu-id="d89dc-116">Because of this restriction, compatibility guarantees are especially important for components.</span></span> <span data-ttu-id="d89dc-117">从 .NET Framework 4 开始，你可以通过将 <xref:System.Runtime.Versioning.ComponentGuaranteesAttribute?displayProperty=nameWithType> 特性应用于某个组件，来指定希望该组件与多个版本的兼容程度。</span><span class="sxs-lookup"><span data-stu-id="d89dc-117">Starting with the .NET Framework 4, you can specify the degree to which a component is expected to remain compatible across multiple versions by applying the <xref:System.Runtime.Versioning.ComponentGuaranteesAttribute?displayProperty=nameWithType> attribute to that component.</span></span> <span data-ttu-id="d89dc-118">工具可使用此特性来检测组件的将来版本中的兼容性保证的潜在冲突。</span><span class="sxs-lookup"><span data-stu-id="d89dc-118">Tools can use this attribute to detect potential violations of the compatibility guarantee in future versions of a component.</span></span>

## <a name="backward-compatibility"></a><span data-ttu-id="d89dc-119">向后兼容性</span><span class="sxs-lookup"><span data-stu-id="d89dc-119">Backward compatibility</span></span>

<span data-ttu-id="d89dc-120">.NET Framework 4.5 及更高版本与使用早期版本的 .NET Framework 生成的应用向后兼容。</span><span class="sxs-lookup"><span data-stu-id="d89dc-120">The .NET Framework 4.5 and later versions are backward-compatible with apps that were built with earlier versions of the .NET Framework.</span></span> <span data-ttu-id="d89dc-121">换句话说，使用早期版本的 .NET Framework 生成的应用和组件将运行，而无需在 .NET Framework 4.5 及更高版本上进行修改。</span><span class="sxs-lookup"><span data-stu-id="d89dc-121">In other words, apps and components built with previous versions will work without modification on the .NET Framework 4.5 and later versions.</span></span> <span data-ttu-id="d89dc-122">但在默认情况下，应用在其进行开发的公共语言运行时版本上运行，因此必须提供配置文件，使应用能在 .NET Framework 4.5 及更高版本上运行。</span><span class="sxs-lookup"><span data-stu-id="d89dc-122">However, by default, apps run on the version of the common language runtime for which they were developed, so you may have to provide a configuration file to enable your app to run on the .NET Framework 4.5 or later versions.</span></span> <span data-ttu-id="d89dc-123">有关详细信息，请参阅本文前面的[应用的版本兼容性](#Apps)一节。</span><span class="sxs-lookup"><span data-stu-id="d89dc-123">For more information, see the [Version compatibility for apps](#Apps) section earlier in this article.</span></span>

<span data-ttu-id="d89dc-124">实际上，.NET Framework 中看似无关紧要的更改和编程技术上的更改会损坏此兼容性。</span><span class="sxs-lookup"><span data-stu-id="d89dc-124">In practice, this compatibility can be broken by seemingly inconsequential changes in the .NET Framework and changes in programming techniques.</span></span> <span data-ttu-id="d89dc-125">例如，.NET Framework 4.5 中的性能改进会公开早期版本中未出现的争用条件。</span><span class="sxs-lookup"><span data-stu-id="d89dc-125">For example, performance improvements in the .NET Framework 4.5 can expose a race condition that did not occur on earlier versions.</span></span> <span data-ttu-id="d89dc-126">同样，使用 .NET Framework 程序集的硬编码路径，执行与特定版本的 .NET Framework 的相等比较，以及使用反射获取私有字段的值都不是向后兼容的做法。</span><span class="sxs-lookup"><span data-stu-id="d89dc-126">Similarly, using a hard-coded path to .NET Framework assemblies, performing an equality comparison with a particular version of the .NET Framework, and getting the value of a private field by using reflection are not backward-compatible practices.</span></span> <span data-ttu-id="d89dc-127">此外，每个版本的 .NET Framework 都包含 Bug 修复和可能影响某些应用程序和组件的兼容性的安全相关更改。</span><span class="sxs-lookup"><span data-stu-id="d89dc-127">In addition, each version of the .NET Framework includes bug fixes and security-related changes that can affect the compatibility of some apps and components.</span></span>

<span data-ttu-id="d89dc-128">如果应用或组件在 .NET Framework 4.5（包括其单点版本，即 .NET Framework 4.5.1、4.5.2、4.6、4.6.1、4.6.2、4.7、4.7.1、4.7.2 或 4.8）上未按预期运行，请使用以下清单：</span><span class="sxs-lookup"><span data-stu-id="d89dc-128">If your app or component doesn't work as expected on the .NET Framework 4.5 (including its point releases, the .NET Framework 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1, 4.7.2, or 4.8), use the following checklists:</span></span>

- <span data-ttu-id="d89dc-129">如果你开发的应用是为在 .NET Framework 4.0 以后的任何 .NET Framework 版本上运行，请参阅[应用程序兼容性](application-compatibility.md)，以生成目标 .NET Framework 版本与运行应用的版本之间的更改列表。</span><span class="sxs-lookup"><span data-stu-id="d89dc-129">If your app was developed to run on any version of the .NET Framework starting with the .NET Framework 4.0, see [Application compatibility](application-compatibility.md) to generate lists of changes between your targeted .NET Framework version and the version on which your app is running.</span></span>

- <span data-ttu-id="d89dc-130">如果使用 .NET Framework 3.5 应用，另请参阅 [.NET Framework 4 迁移问题](net-framework-4-migration-issues.md)。</span><span class="sxs-lookup"><span data-stu-id="d89dc-130">If you have a .NET Framework 3.5 app, also see [.NET Framework 4 Migration Issues](net-framework-4-migration-issues.md).</span></span>

- <span data-ttu-id="d89dc-131">如果使用 .NET Framework 2.0 应用，另请参阅 [.NET Framework 3.5 SP1 中的更改](/previous-versions/dotnet/articles/dd310284(v=msdn.10))。</span><span class="sxs-lookup"><span data-stu-id="d89dc-131">If you have a .NET Framework 2.0 app, also see [Changes in .NET Framework 3.5 SP1](/previous-versions/dotnet/articles/dd310284(v=msdn.10)).</span></span>

- <span data-ttu-id="d89dc-132">如果使用 .NET Framework 1.1 应用，另请参阅 [.NET Framework 2.0 中的更改](/previous-versions/aa570326(v=msdn.10))。</span><span class="sxs-lookup"><span data-stu-id="d89dc-132">If you have a .NET Framework 1.1 app, also see [Changes in .NET Framework 2.0](/previous-versions/aa570326(v=msdn.10)).</span></span>

- <span data-ttu-id="d89dc-133">如果要重新编译现有源代码以在 .NET Framework 4.5 或其单点版本上运行，或如果要通过现有源代码库开发面向 .NET Framework 4.5 或其单点版本的新版本应用或组件，请查看[类库中的过时内容](../whats-new/whats-obsolete.md)以了解过时的类型和成员，并应用所述的解决方法。</span><span class="sxs-lookup"><span data-stu-id="d89dc-133">If you're recompiling existing source code to run on the .NET Framework 4.5 or its point releases, or if you're developing a new version of an app or component that targets the .NET Framework 4.5 or its point releases from an existing source code base, check [What's Obsolete in the Class Library](../whats-new/whats-obsolete.md) for obsolete types and members, and apply the workaround described.</span></span> <span data-ttu-id="d89dc-134">（以前编译的代码将继续针对已标记为过时的类型和成员运行。）</span><span class="sxs-lookup"><span data-stu-id="d89dc-134">(Previously compiled code will continue to run against types and members that have been marked as obsolete.)</span></span>

- <span data-ttu-id="d89dc-135">如果确定 .NET Framework 4.5 中的更改已损坏应用，请查看[运行时设置架构](../configure-apps/file-schema/runtime/index.md)（特别是 [\<AppContextSwitchOverrides> 元素](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)），以确定是否能够在应用的配置文件中使用运行时设置来还原以前的行为。</span><span class="sxs-lookup"><span data-stu-id="d89dc-135">If you determine that a change in the .NET Framework 4.5 has broken your app, check the [Runtime Settings Schema](../configure-apps/file-schema/runtime/index.md), and particularly the [\<AppContextSwitchOverrides> Element](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md), to determine whether you can use a runtime setting in your app's configuration file to restore the previous behavior.</span></span>

- <span data-ttu-id="d89dc-136">如果遇到未记录的问题，请在[适用于 .NET 的开发人员社区网站](https://aka.ms/feedback/report?space=61)中新开一个问题，或在 [Microsoft/dotnet GitHub 存储库](https://github.com/microsoft/dotnet/issues)中新开一个问题。</span><span class="sxs-lookup"><span data-stu-id="d89dc-136">If you come across an issue that isn't documented, open a problem on the [Developer Community site for .NET](https://aka.ms/feedback/report?space=61) or open an issue in the [Microsoft/dotnet GitHub repo](https://github.com/microsoft/dotnet/issues).</span></span>

## <a name="side-by-side-execution"></a><span data-ttu-id="d89dc-137">并行执行</span><span class="sxs-lookup"><span data-stu-id="d89dc-137">Side-by-side execution</span></span>

<span data-ttu-id="d89dc-138">如果找不到解决问题的适当方法，请记住，.NET Framework 4.5（或其单点版本之一）与版本 1.1、2.0 和 3.5 并行运行，并且是取代版本 4 的就地更新。</span><span class="sxs-lookup"><span data-stu-id="d89dc-138">If you can't find a suitable workaround for your issue, remember that .NET Framework 4.5 (or one of its point releases) runs side by side with versions 1.1, 2.0, and 3.5, and is an in-place update that replaces version 4.</span></span> <span data-ttu-id="d89dc-139">对于以版本 1.1、2.0 和 3.5 为目标的应用程序，你可以在目标计算机上安装适当的 .NET Framework 版本以在其最佳环境中运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="d89dc-139">For apps that target versions 1.1, 2.0, and 3.5, you can install the appropriate version of .NET Framework on the target machine to run the app in its best environment.</span></span> <span data-ttu-id="d89dc-140">有关并行执行的详细信息，请参阅[并行执行](../deployment/side-by-side-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="d89dc-140">For more information about side-by-side execution, see [Side-by-Side Execution](../deployment/side-by-side-execution.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d89dc-141">请参阅</span><span class="sxs-lookup"><span data-stu-id="d89dc-141">See also</span></span>

- [<span data-ttu-id="d89dc-142">新增功能</span><span class="sxs-lookup"><span data-stu-id="d89dc-142">What's New</span></span>](../whats-new/index.md)
- [<span data-ttu-id="d89dc-143">类库中过时的内容</span><span class="sxs-lookup"><span data-stu-id="d89dc-143">What's Obsolete in the Class Library</span></span>](../whats-new/whats-obsolete.md)
- [<span data-ttu-id="d89dc-144">应用程序兼容性</span><span class="sxs-lookup"><span data-stu-id="d89dc-144">Application Compatibility</span></span>](application-compatibility.md)
- [<span data-ttu-id="d89dc-145">.NET Framework 官方支持策略</span><span class="sxs-lookup"><span data-stu-id="d89dc-145">.NET Framework official support policy</span></span>](https://dotnet.microsoft.com/platform/support/policy/dotnet-framework)
- [<span data-ttu-id="d89dc-146">.NET Framework 4 迁移问题</span><span class="sxs-lookup"><span data-stu-id="d89dc-146">.NET Framework 4 Migration Issues</span></span>](net-framework-4-migration-issues.md)
