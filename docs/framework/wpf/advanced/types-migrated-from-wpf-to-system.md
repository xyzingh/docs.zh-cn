---
title: 从 WPF 迁移到 System.Xaml 的类型
ms.date: 03/30/2017
helpviewer_keywords:
- WPF XAML [XAML Services], migration to System.Xaml
- XAML [XAML Services], System.Xaml and WPF
- System.Xaml [XAML Services], types migrated from WPF
ms.assetid: d79dabf5-a2ec-4e8d-a37a-67c4ba8a2b91
ms.openlocfilehash: 5aa2d8a39be47d9affb97c3b60e53c4722c63cce
ms.sourcegitcommit: 99b153b93bf94d0fecf7c7bcecb58ac424dfa47c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2020
ms.locfileid: "80249812"
---
# <a name="types-migrated-from-wpf-to-systemxaml"></a><span data-ttu-id="029cf-102">从 WPF 迁移到 System.Xaml 的类型</span><span class="sxs-lookup"><span data-stu-id="029cf-102">Types migrated from WPF to System.Xaml</span></span>

<span data-ttu-id="029cf-103">在 .NET 框架 3.5 和 .NET 框架 3.0 中，Windows 演示基础 （WPF） 和 Windows 工作流基础都包含 XAML 语言实现。</span><span class="sxs-lookup"><span data-stu-id="029cf-103">In .NET Framework 3.5 and .NET Framework 3.0, both Windows Presentation Foundation (WPF) and Windows Workflow Foundation included a XAML language implementation.</span></span> <span data-ttu-id="029cf-104">为 WPF XAML 实现提供扩展性的很多公共类型都存在于 WindowsBase、PresentationCore 和 PresentationFramework 程序集中。</span><span class="sxs-lookup"><span data-stu-id="029cf-104">Many of the public types that provided extensibility for the WPF XAML implementation existed in the WindowsBase, PresentationCore, and PresentationFramework assemblies.</span></span> <span data-ttu-id="029cf-105">同样，为 Windows 工作流基础 XAML 提供扩展性的公共类型存在于 System.Workflow.组件模型程序集中。</span><span class="sxs-lookup"><span data-stu-id="029cf-105">Likewise, public types that provided extensibility for Windows Workflow Foundation XAML existed in the System.Workflow.ComponentModel assembly.</span></span> <span data-ttu-id="029cf-106">在 .NET 框架 4 中，一些与 XAML 相关的类型已迁移到 System.Xaml 程序集。</span><span class="sxs-lookup"><span data-stu-id="029cf-106">In the .NET Framework 4, some of the XAML-related types were migrated to the System.Xaml assembly.</span></span> <span data-ttu-id="029cf-107">XAML 语言服务的通用 .NET 框架实现支持许多 XAML 扩展性方案，这些方案最初由特定框架的 XAML 实现定义，但现在是整体 .NET 框架 4 XAML 语言支持的一部分。</span><span class="sxs-lookup"><span data-stu-id="029cf-107">A common .NET Framework implementation of XAML language services enables many XAML extensibility scenarios that were originally defined by a specific framework's XAML implementation but are now part of overall .NET Framework 4 XAML language support.</span></span> <span data-ttu-id="029cf-108">本文列出了迁移的类型，并讨论了与迁移相关的问题。</span><span class="sxs-lookup"><span data-stu-id="029cf-108">This article lists the types that were migrated and discusses issues related to the migration.</span></span>

## <a name="assemblies-and-namespaces"></a><span data-ttu-id="029cf-109">程序集和命名空间</span><span class="sxs-lookup"><span data-stu-id="029cf-109">Assemblies and Namespaces</span></span>

<span data-ttu-id="029cf-110">在 .NET 框架 3.5 和 .NET 框架 3.0 中，WPF 为支持 XAML 而实现的类型通常位于<xref:System.Windows.Markup>命名空间中。</span><span class="sxs-lookup"><span data-stu-id="029cf-110">In .NET Framework 3.5 and .NET Framework 3.0, the types that WPF implemented to support XAML were generally in the <xref:System.Windows.Markup> namespace.</span></span> <span data-ttu-id="029cf-111">大多数这些类型都位于 WindowsBase 程序集中。</span><span class="sxs-lookup"><span data-stu-id="029cf-111">Most of these types were in the WindowsBase assembly.</span></span>

<span data-ttu-id="029cf-112">在 .NET 框架 4 中<xref:System.Xaml>，有一个新的命名空间和一个新的 System.Xaml 程序集。</span><span class="sxs-lookup"><span data-stu-id="029cf-112">In .NET Framework 4, there is a new <xref:System.Xaml> namespace and a new System.Xaml assembly.</span></span> <span data-ttu-id="029cf-113">最初为 WPF XAML 实现的很多类型现在作为任何 XAML 实现的扩展性点或服务提供。</span><span class="sxs-lookup"><span data-stu-id="029cf-113">Many of the types that were originally implemented for WPF XAML are now provided as extensibility points or services for any implementation of XAML.</span></span> <span data-ttu-id="029cf-114">为了使其可用于更普通的方案，将类型从其最初所在的 WPF 程序集类型转发到 System.Xaml 程序集。</span><span class="sxs-lookup"><span data-stu-id="029cf-114">As part of making them available for more general scenarios, the types are type-forwarded from their original WPF assembly to the System.Xaml assembly.</span></span> <span data-ttu-id="029cf-115">这支持 XAML 扩展性方案，而无需包括其他框架（如 WPF 和 Windows 工作流基础）的程序集。</span><span class="sxs-lookup"><span data-stu-id="029cf-115">This enables XAML extensibility scenarios without having to include the assemblies of other frameworks (such as WPF and Windows Workflow Foundation).</span></span>

<span data-ttu-id="029cf-116">对于已迁移的类型，大多数类型仍位于 <xref:System.Windows.Markup> 命名空间中。</span><span class="sxs-lookup"><span data-stu-id="029cf-116">For migrated types, most of the types remain in the <xref:System.Windows.Markup> namespace.</span></span> <span data-ttu-id="029cf-117">这是做部分是为了避免中断每个文件上现有实现中的 CLR 命名空间映射。</span><span class="sxs-lookup"><span data-stu-id="029cf-117">This was partially to avoid breaking CLR namespace mappings in existing implementations on a per-file basis.</span></span> <span data-ttu-id="029cf-118">因此，.NET<xref:System.Windows.Markup>框架 4 中的命名空间包含一般 XAML 语言支持类型（来自 System.Xaml 程序集）和特定于 WPF XAML 实现的类型（来自 WindowsBase 和其他 WPF 程序集）的混合。</span><span class="sxs-lookup"><span data-stu-id="029cf-118">As a result, the <xref:System.Windows.Markup> namespace in .NET Framework 4 contains a mixture of general XAML language support types (from the System.Xaml assembly) and types that are specific to the WPF XAML implementation (from WindowsBase and other WPF assemblies).</span></span> <span data-ttu-id="029cf-119">在版本 4 的 WPF 程序集中，已迁移到 System.Xaml，但以前存在于 WPF 程序集中的任何类型都具有类型转发支持。</span><span class="sxs-lookup"><span data-stu-id="029cf-119">Any type that was migrated to System.Xaml, but existed previously in a WPF assembly, has type-forwarding support in version 4 of the WPF assembly.</span></span>

### <a name="workflow-xaml-support-types"></a><span data-ttu-id="029cf-120">工作流 XAML 支持类型</span><span class="sxs-lookup"><span data-stu-id="029cf-120">Workflow XAML Support Types</span></span>

<span data-ttu-id="029cf-121">Windows 工作流基础还提供 XAML 支持类型，在许多情况下，这些类型与 WPF 等效项具有相同的短名称。</span><span class="sxs-lookup"><span data-stu-id="029cf-121">Windows Workflow Foundation also provided XAML support types, and in many cases these had identical short names to a WPF equivalent.</span></span> <span data-ttu-id="029cf-122">以下是 Windows 工作流基础 XAML 支持类型的列表：</span><span class="sxs-lookup"><span data-stu-id="029cf-122">The following is a list of Windows Workflow Foundation XAML support types:</span></span>

- <xref:System.Workflow.ComponentModel.Serialization.ContentPropertyAttribute>

- <xref:System.Workflow.ComponentModel.Serialization.RuntimeNamePropertyAttribute>

- <xref:System.Workflow.ComponentModel.Serialization.XmlnsPrefixAttribute>

<span data-ttu-id="029cf-123">这些支持类型仍然存在于 .NET 框架 4 的 Windows 工作流基础程序集中，但仍可用于特定的 Windows 工作流基础应用程序;但是，它们不应被不使用 Windows 工作流基础的应用程序或框架引用。</span><span class="sxs-lookup"><span data-stu-id="029cf-123">These support types still exist in the Windows Workflow Foundation assemblies for .NET Framework 4 and can still be used for specific Windows Workflow Foundation applications; however, they should not be referenced by applications or frameworks that do not use Windows Workflow Foundation.</span></span>

## <a name="markupextension"></a><span data-ttu-id="029cf-124">MarkupExtension</span><span class="sxs-lookup"><span data-stu-id="029cf-124">MarkupExtension</span></span>

<span data-ttu-id="029cf-125">在 .NET 框架 3.5 和 .NET 框架<xref:System.Windows.Markup.MarkupExtension>3.0 中，WPF 的类位于 WindowsBase 程序集中。</span><span class="sxs-lookup"><span data-stu-id="029cf-125">In the .NET Framework 3.5 and .NET Framework 3.0, the <xref:System.Windows.Markup.MarkupExtension> class for WPF was in the WindowsBase assembly.</span></span> <span data-ttu-id="029cf-126">Windows 工作流基础<xref:System.Workflow.ComponentModel.Serialization.MarkupExtension>的并行类存在于 System.Workflow.组件模型程序集中。</span><span class="sxs-lookup"><span data-stu-id="029cf-126">A parallel class for Windows Workflow Foundation, <xref:System.Workflow.ComponentModel.Serialization.MarkupExtension>, existed in the System.Workflow.ComponentModel assembly.</span></span> <span data-ttu-id="029cf-127">在 .NET 框架 4<xref:System.Windows.Markup.MarkupExtension>中，类将迁移到 System.Xaml 程序集。</span><span class="sxs-lookup"><span data-stu-id="029cf-127">In the .NET Framework 4, the <xref:System.Windows.Markup.MarkupExtension> class is migrated to the System.Xaml assembly.</span></span> <span data-ttu-id="029cf-128">在 .NET 框架<xref:System.Windows.Markup.MarkupExtension>4 中，适用于使用 .NET XAML 服务的任何 XAML 扩展性方案，而不仅仅是基于特定框架的服务。</span><span class="sxs-lookup"><span data-stu-id="029cf-128">In the .NET Framework 4, <xref:System.Windows.Markup.MarkupExtension> is intended for any XAML extensibility scenario that uses .NET XAML Services, not just for those that build on specific frameworks.</span></span> <span data-ttu-id="029cf-129">在可能的情况下，特定的框架或架构中的用户代码也应在 XAML 扩展的 <xref:System.Windows.Markup.MarkupExtension> 类上生成。</span><span class="sxs-lookup"><span data-stu-id="029cf-129">When possible, specific frameworks or user code in the framework should also build on the <xref:System.Windows.Markup.MarkupExtension> class for XAML extension.</span></span>

## <a name="markupextension-supporting-service-classes"></a><span data-ttu-id="029cf-130">MarkupExtension 支持服务类</span><span class="sxs-lookup"><span data-stu-id="029cf-130">MarkupExtension Supporting Service Classes</span></span>

<span data-ttu-id="029cf-131">WPF 的 .NET 框架 3.5 和 .NET 框架 3.0 提供了一些服务，这些服务可用于<xref:System.Windows.Markup.MarkupExtension>实施者和<xref:System.ComponentModel.TypeConverter>实现，以支持 XAML 中的类型/属性使用。</span><span class="sxs-lookup"><span data-stu-id="029cf-131">.NET Framework 3.5 and .NET Framework 3.0 for WPF provided several services that were available to <xref:System.Windows.Markup.MarkupExtension> implementers and <xref:System.ComponentModel.TypeConverter> implementations to support type/property usage in XAML.</span></span> <span data-ttu-id="029cf-132">这些服务如下所示：</span><span class="sxs-lookup"><span data-stu-id="029cf-132">These services are the following:</span></span>

- <xref:System.Windows.Markup.IProvideValueTarget>

- <xref:System.Windows.Markup.IUriContext>

- <xref:System.Windows.Markup.IXamlTypeResolver>

> [!NOTE]
> <span data-ttu-id="029cf-133">.NET Framework 3.5 中与标记扩展相关的另一个服务是<xref:System.Windows.Markup.IReceiveMarkupExtension>接口。</span><span class="sxs-lookup"><span data-stu-id="029cf-133">Another service from .NET Framework 3.5 that is related to markup extensions is the <xref:System.Windows.Markup.IReceiveMarkupExtension> interface.</span></span> <span data-ttu-id="029cf-134"><xref:System.Windows.Markup.IReceiveMarkupExtension>未迁移，标记为`[Obsolete]`.NET 框架 4。</span><span class="sxs-lookup"><span data-stu-id="029cf-134"><xref:System.Windows.Markup.IReceiveMarkupExtension> was not migrated and is marked `[Obsolete]` for .NET Framework 4.</span></span> <span data-ttu-id="029cf-135">以前使用 <xref:System.Windows.Markup.IReceiveMarkupExtension> 的方案应改用 <xref:System.Windows.Markup.XamlSetMarkupExtensionAttribute> 特性化回调。</span><span class="sxs-lookup"><span data-stu-id="029cf-135">Scenarios that previously used <xref:System.Windows.Markup.IReceiveMarkupExtension> should instead use <xref:System.Windows.Markup.XamlSetMarkupExtensionAttribute> attributed callbacks.</span></span> <span data-ttu-id="029cf-136"><xref:System.Windows.Markup.AcceptedMarkupExtensionExpressionTypeAttribute> 也标记为 `[Obsolete]`。</span><span class="sxs-lookup"><span data-stu-id="029cf-136"><xref:System.Windows.Markup.AcceptedMarkupExtensionExpressionTypeAttribute> is also marked `[Obsolete]`.</span></span>

## <a name="xaml-language-features"></a><span data-ttu-id="029cf-137">XAML 语言功能</span><span class="sxs-lookup"><span data-stu-id="029cf-137">XAML Language Features</span></span>

<span data-ttu-id="029cf-138">WPF 的多个 XAML 语言功能和组件以前存在于 PresentationFramework 程序集中。</span><span class="sxs-lookup"><span data-stu-id="029cf-138">Several XAML language features and components for WPF previously existed in the PresentationFramework assembly.</span></span> <span data-ttu-id="029cf-139">这些功能和组件作为 <xref:System.Windows.Markup.MarkupExtension> 子类实现以在 XAML 标记中公开标记扩展用法。</span><span class="sxs-lookup"><span data-stu-id="029cf-139">These were implemented as a <xref:System.Windows.Markup.MarkupExtension> subclass to expose markup extension usages in XAML markup.</span></span> <span data-ttu-id="029cf-140">在 .NET 框架 4 中，这些功能存在于 System.Xaml 程序集中，以便不包含 WPF 程序集的项目可以使用这些 XAML 语言级功能。</span><span class="sxs-lookup"><span data-stu-id="029cf-140">In .NET Framework 4, these exist in the System.Xaml assembly so that projects that do not include WPF assemblies can use these XAML language-level features.</span></span> <span data-ttu-id="029cf-141">WPF 对 .NET 框架 4 应用程序使用相同的实现。</span><span class="sxs-lookup"><span data-stu-id="029cf-141">WPF uses these same implementations for .NET Framework 4 applications.</span></span> <span data-ttu-id="029cf-142">与本主题中列出的其他情况一样，这些支持类型继续存在于 <xref:System.Windows.Markup> 命名空间中，以避免中断以前的引用。</span><span class="sxs-lookup"><span data-stu-id="029cf-142">As with the other cases that are listed in this topic, the supporting types continue to exist in the <xref:System.Windows.Markup> namespace to avoid breaking previous references.</span></span>

<span data-ttu-id="029cf-143">下表包含在 System.Xaml 中定义的 XAML 功能支持类的列表。</span><span class="sxs-lookup"><span data-stu-id="029cf-143">The following table contains a list of the XAML feature-support classes that are defined in System.Xaml.</span></span>

|<span data-ttu-id="029cf-144">XAML 语言功能</span><span class="sxs-lookup"><span data-stu-id="029cf-144">XAML Language Feature</span></span>|<span data-ttu-id="029cf-145">使用情况</span><span class="sxs-lookup"><span data-stu-id="029cf-145">Usage</span></span>|
|---------------------------|-----------|
|<xref:System.Windows.Markup.ArrayExtension>|`<x:Array ...>`|
|<xref:System.Windows.Markup.NullExtension>|`{x:Null}`|
|<xref:System.Windows.Markup.StaticExtension>|`{x:Static ...}`|
|<xref:System.Windows.Markup.TypeExtension>|`{x:Type ...}`|

<span data-ttu-id="029cf-146">虽然 System.Xaml 可能没有特定支持类，但用于处理 XAML 语言的语言功能的常规逻辑现在位于 System.Xaml 及其实现的 XAML 读取器和 XAML 编写器中。</span><span class="sxs-lookup"><span data-stu-id="029cf-146">Although System.Xaml may not have specific support classes, the general logic for processing language features for the XAML language now resides in System.Xaml and its implemented XAML readers and XAML writers.</span></span> <span data-ttu-id="029cf-147">例如， `x:TypeArguments` 是一个由 System.Xaml 实现中的 XAML 读取器和 XAML 编写器处理的特性；该特性可在 XAML 节点流中说明，可在默认的（基于 CLR 的）XAML 架构上下文中进行处理，具有 XAML 类型系统表示形式，等等。</span><span class="sxs-lookup"><span data-stu-id="029cf-147">For example, `x:TypeArguments` is an attribute that is processed by XAML readers and XAML writers from System.Xaml implementations; it can be noted in the XAML node stream, has handling in the default (CLR-based) XAML schema context, has a XAML type-system representation, and so on.</span></span> <span data-ttu-id="029cf-148">因此，所有 XAML 语言级别功能的参考文档是[Windows 演示基础 （WPF） 桌面指南](../../../desktop-wpf/overview/index.md)中[XAML 服务的](../../../desktop-wpf/xaml-services/index.md)子主题。</span><span class="sxs-lookup"><span data-stu-id="029cf-148">As a result, the reference documentation for all XAML language-level features is a subtopic for [XAML Services](../../../desktop-wpf/xaml-services/index.md) in the [Desktop Guide for Windows Presentation Foundation (WPF)](../../../desktop-wpf/overview/index.md).</span></span>

## <a name="valueserializer-and-supporting-classes"></a><span data-ttu-id="029cf-149">ValueSerializer 和支持类</span><span class="sxs-lookup"><span data-stu-id="029cf-149">ValueSerializer and Supporting Classes</span></span>

<span data-ttu-id="029cf-150"><xref:System.Windows.Markup.ValueSerializer> 类支持到字符串的类型转换，尤其对于序列化可能需要输出中有多个模式或节点的 XAML 序列化情况。</span><span class="sxs-lookup"><span data-stu-id="029cf-150">The <xref:System.Windows.Markup.ValueSerializer> class supports type conversion to a string, particularly for XAML serialization cases where serialization may require multiple modes or nodes in the output.</span></span> <span data-ttu-id="029cf-151">在 .NET 框架 3.5 和 .NET<xref:System.Windows.Markup.ValueSerializer>框架 3.0 中，WPF 的 是在 WindowsBase 程序集中。</span><span class="sxs-lookup"><span data-stu-id="029cf-151">In .NET Framework 3.5 and .NET Framework 3.0, the <xref:System.Windows.Markup.ValueSerializer> for WPF was in the WindowsBase assembly.</span></span> <span data-ttu-id="029cf-152">在 .NET 框架 4<xref:System.Windows.Markup.ValueSerializer>中，该类位于 System.Xaml 中，适用于任何 XAML 扩展性方案，而不仅仅是基于 WPF 构建的方案。</span><span class="sxs-lookup"><span data-stu-id="029cf-152">In the .NET Framework 4, the <xref:System.Windows.Markup.ValueSerializer> class is in System.Xaml and is intended for any XAML extensibility scenario, not just for those that build on WPF.</span></span> <span data-ttu-id="029cf-153"><xref:System.Windows.Markup.IValueSerializerContext> （支持服务）和 <xref:System.Windows.Markup.DateTimeValueSerializer> （特定子类）也会被迁移到 System.Xaml。</span><span class="sxs-lookup"><span data-stu-id="029cf-153"><xref:System.Windows.Markup.IValueSerializerContext> (a supporting service) and <xref:System.Windows.Markup.DateTimeValueSerializer> (a specific subclass) are also migrated to System.Xaml.</span></span>

## <a name="xaml-related-attributes"></a><span data-ttu-id="029cf-154">与 XAML 相关的属性</span><span class="sxs-lookup"><span data-stu-id="029cf-154">XAML-Related Attributes</span></span>

<span data-ttu-id="029cf-155">WPF XAML 包含多个特性，这些特性可应用于 CLR 类型以指示有关它们的 XAML 行为的某些内容。</span><span class="sxs-lookup"><span data-stu-id="029cf-155">WPF XAML included several attributes that can be applied to CLR types to indicate something about their XAML behavior.</span></span> <span data-ttu-id="029cf-156">以下是 .NET 框架 3.5 和 .NET 框架 3.0 中 WPF 程序集中存在的属性的列表。</span><span class="sxs-lookup"><span data-stu-id="029cf-156">The following is a list of the attributes that existed in WPF assemblies in .NET Framework 3.5 and .NET Framework 3.0.</span></span> <span data-ttu-id="029cf-157">这些属性将迁移到 .NET 框架 4 中的 System.Xaml。</span><span class="sxs-lookup"><span data-stu-id="029cf-157">These attributes are migrated to System.Xaml in .NET Framework 4.</span></span>

- <xref:System.Windows.Markup.AmbientAttribute>

- <xref:System.Windows.Markup.ContentPropertyAttribute>

- <xref:System.Windows.Markup.ContentWrapperAttribute>

- <xref:System.Windows.Markup.DependsOnAttribute>

- <xref:System.Windows.Markup.MarkupExtensionReturnTypeAttribute>

- <xref:System.Windows.Markup.NameScopePropertyAttribute>

- <xref:System.Windows.Markup.RootNamespaceAttribute>

- <xref:System.Windows.Markup.RuntimeNamePropertyAttribute>

- <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute>

- <xref:System.Windows.Markup.ValueSerializerAttribute>

- <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>

- <xref:System.Windows.Markup.XmlLangPropertyAttribute>

- <xref:System.Windows.Markup.XmlnsCompatibleWithAttribute>

- <xref:System.Windows.Markup.XmlnsDefinitionAttribute>

- <xref:System.Windows.Markup.XmlnsPrefixAttribute>

## <a name="miscellaneous-classes"></a><span data-ttu-id="029cf-158">其他类</span><span class="sxs-lookup"><span data-stu-id="029cf-158">Miscellaneous Classes</span></span>

<span data-ttu-id="029cf-159">该<xref:System.Windows.Markup.IComponentConnector>接口存在于 .NET 框架 3.5 和 .NET 框架 3.0 中的 WindowsBase 中，但存在于 .NET 框架 4 中的 System.Xaml 中。</span><span class="sxs-lookup"><span data-stu-id="029cf-159">The <xref:System.Windows.Markup.IComponentConnector> interface existed in WindowsBase in .NET Framework 3.5 and .NET Framework 3.0, but exists in System.Xaml in .NET Framework 4.</span></span> <span data-ttu-id="029cf-160"><xref:System.Windows.Markup.IComponentConnector> 主要适用于工具支持和 XAML 标记编译器。</span><span class="sxs-lookup"><span data-stu-id="029cf-160"><xref:System.Windows.Markup.IComponentConnector> is primarily intended for tooling support and XAML markup compilers.</span></span>

<span data-ttu-id="029cf-161">该<xref:System.Windows.Markup.INameScope>接口存在于 .NET 框架 3.5 和 .NET 框架 3.0 中的 WindowsBase 中，但存在于 .NET 框架 4 中的 System.Xaml 中。</span><span class="sxs-lookup"><span data-stu-id="029cf-161">The <xref:System.Windows.Markup.INameScope> interface existed in WindowsBase in .NET Framework 3.5 and .NET Framework 3.0, but exists in System.Xaml in .NET Framework 4.</span></span> <span data-ttu-id="029cf-162"><xref:System.Windows.Markup.INameScope> 定义用于 XAML 名称范围的基本操作。</span><span class="sxs-lookup"><span data-stu-id="029cf-162"><xref:System.Windows.Markup.INameScope> defines basic operations for a XAML namescope.</span></span>

## <a name="xaml-related-classes-with-shared-names-that-exist-in-wpf-and-systemxaml"></a><span data-ttu-id="029cf-163">存在于 WPF 和 System.Xaml 中具有共享名称的与 XAML 相关的类</span><span class="sxs-lookup"><span data-stu-id="029cf-163">XAML-related Classes with Shared Names that Exist in WPF and System.Xaml</span></span>

<span data-ttu-id="029cf-164">以下类存在于 .NET 框架 4 中的 WPF 程序集和 System.Xaml 程序集中：</span><span class="sxs-lookup"><span data-stu-id="029cf-164">The following classes exist in both the WPF assemblies and the System.Xaml assembly in .NET Framework 4:</span></span>

`XamlReader`

`XamlWriter`

`XamlParseException`

<span data-ttu-id="029cf-165">WPF 实现位于 <xref:System.Windows.Markup> 命名空间和 PresentationFramework 程序集中。</span><span class="sxs-lookup"><span data-stu-id="029cf-165">The WPF implementation is found in the <xref:System.Windows.Markup> namespace, and PresentationFramework assembly.</span></span> <span data-ttu-id="029cf-166">System.Xaml 实现位于 <xref:System.Xaml> 命名空间中。</span><span class="sxs-lookup"><span data-stu-id="029cf-166">The System.Xaml implementation is found in the <xref:System.Xaml> namespace.</span></span> <span data-ttu-id="029cf-167">如果你使用的是 WPF 类型或是从 WPF 类型派生的，则通常应使用 <xref:System.Windows.Markup.XamlReader> 和 <xref:System.Windows.Markup.XamlWriter> 的 WPF 实现，而不是 System.Xaml 实现。</span><span class="sxs-lookup"><span data-stu-id="029cf-167">If you are using WPF types or are deriving from WPF types, you should typically use the WPF implementations of <xref:System.Windows.Markup.XamlReader> and <xref:System.Windows.Markup.XamlWriter> instead of the System.Xaml implementations.</span></span> <span data-ttu-id="029cf-168">有关详细信息，请参阅 <xref:System.Windows.Markup.XamlReader?displayProperty=nameWithType> 和 <xref:System.Windows.Markup.XamlWriter?displayProperty=nameWithType>中的“备注”。</span><span class="sxs-lookup"><span data-stu-id="029cf-168">For more information, see Remarks in <xref:System.Windows.Markup.XamlReader?displayProperty=nameWithType> and <xref:System.Windows.Markup.XamlWriter?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="029cf-169">如果要包括对 WPF 程序集和 System.Xaml 的应用，并且还要对 `include` 和 <xref:System.Windows.Markup> 命名空间使用 <xref:System.Xaml> 语句，则可能需要完全限定对这些 API 的调用，以便清楚无误地解析类型。</span><span class="sxs-lookup"><span data-stu-id="029cf-169">If you are including references to both WPF assemblies and System.Xaml, and you also are using `include` statements for both the <xref:System.Windows.Markup> and <xref:System.Xaml> namespaces, you may need to fully qualify the calls to these APIs in order to resolve the types without ambiguity.</span></span>