---
title: .NET 5+ 中已过时的功能
description: 了解在 .NET 5.0 和更高版本中标记为已过时并生成 SYSLIB 编译器警告的 API。
ms.date: 10/20/2020
ms.openlocfilehash: 13f5fb10cfe693ed621b3f45fc22e024875890c8
ms.sourcegitcommit: dfcbc096ad7908cd58a5f0aeabd2256f05266bac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92333061"
---
# <a name="obsolete-features-in-net-5"></a><span data-ttu-id="3a2c7-103">.NET 5 中已过时的功能</span><span class="sxs-lookup"><span data-stu-id="3a2c7-103">Obsolete features in .NET 5</span></span>

<span data-ttu-id="3a2c7-104">从 .NET 5.0 开始，一些新标记为已过时的 API 使用 <xref:System.ObsoleteAttribute> 上的两个新属性。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-104">Starting in .NET 5.0, some APIs that are newly marked as obsolete make use of two new properties on <xref:System.ObsoleteAttribute>.</span></span>

- <span data-ttu-id="3a2c7-105"><xref:System.ObsoleteAttribute.DiagnosticId?displayProperty=nameWithType> 属性指示编译器使用自定义诊断 ID 产生生成警告。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-105">The <xref:System.ObsoleteAttribute.DiagnosticId?displayProperty=nameWithType> property tells the compiler to generate build warnings using a custom diagnostic ID.</span></span> <span data-ttu-id="3a2c7-106">通过自定义 ID 可专门、单独地取消过时警告。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-106">The custom ID allows for obsoletion warning to be suppressed specifically and separately from one another.</span></span> <span data-ttu-id="3a2c7-107">对于 .NET 5+ 过时，自定义诊断 ID 的格式为 `SYSLIBxxxx`。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-107">In the case of the .NET 5+ obsoletions, the format for the custom diagnostic ID is `SYSLIBxxxx`.</span></span>

- <span data-ttu-id="3a2c7-108"><xref:System.ObsoleteAttribute.UrlFormat?displayProperty=nameWithType> 属性指示编译器包含一个 URL 链接，可了解有关过时的详细信息。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-108">The <xref:System.ObsoleteAttribute.UrlFormat?displayProperty=nameWithType> property tells the compiler to include a URL link to learn more about the obsoletion.</span></span>

<span data-ttu-id="3a2c7-109">如果由于使用过时的 API 而遇到生成警告或错误，请遵循[参考](#reference)部分中列出的诊断 ID 所提供的特定指导。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-109">If you encounter build warnings or errors due to usage of an obsolete API, follow the specific guidance provided for the diagnostic ID listed in the [Reference](#reference) section.</span></span> <span data-ttu-id="3a2c7-110">不能使用过时类型或成员的[标准诊断 ID (CS0618)](../../csharp/language-reference/compiler-messages/cs0618.md) 取消有关这些过时类型或成员的警告或错误；请改用自定义 `SYSLIBxxxx` 诊断 ID 值。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-110">Warnings or errors for these obsoletions *can't* be suppressed using the [standard diagnostic ID (CS0618)](../../csharp/language-reference/compiler-messages/cs0618.md) for obsolete types or members; use the custom `SYSLIBxxxx` diagnostic ID values instead.</span></span> <span data-ttu-id="3a2c7-111">有关详细信息，请参阅[取消警告](#suppress-warnings)。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-111">For more information, see [Suppress warnings](#suppress-warnings).</span></span>

## <a name="reference"></a><span data-ttu-id="3a2c7-112">参考</span><span class="sxs-lookup"><span data-stu-id="3a2c7-112">Reference</span></span>

<span data-ttu-id="3a2c7-113">下表提供了 .NET 5+ 中 `SYSLIBxxxx` 过时的索引。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-113">The following table provides an index to the `SYSLIBxxxx` obsoletions in .NET 5+.</span></span>

| <span data-ttu-id="3a2c7-114">诊断 ID</span><span class="sxs-lookup"><span data-stu-id="3a2c7-114">Diagnostic ID</span></span> | <span data-ttu-id="3a2c7-115">说明</span><span class="sxs-lookup"><span data-stu-id="3a2c7-115">Description</span></span> |
| - | - |
| [<span data-ttu-id="3a2c7-116">SYSLIB0001</span><span class="sxs-lookup"><span data-stu-id="3a2c7-116">SYSLIB0001</span></span>](syslib0001.md) | <span data-ttu-id="3a2c7-117">UTF-7 编码不安全，因此不应使用。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-117">The UTF-7 encoding is insecure and should not be used.</span></span> <span data-ttu-id="3a2c7-118">请考虑改用 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-118">Consider using UTF-8 instead.</span></span> |
| [<span data-ttu-id="3a2c7-119">SYSLIB0002</span><span class="sxs-lookup"><span data-stu-id="3a2c7-119">SYSLIB0002</span></span>](syslib0002.md) | <span data-ttu-id="3a2c7-120"><xref:System.Security.Permissions.PrincipalPermissionAttribute> 不受运行时支持，不得使用。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-120"><xref:System.Security.Permissions.PrincipalPermissionAttribute> is not honored by the runtime and must not be used.</span></span> |
| [<span data-ttu-id="3a2c7-121">SYSLIB0003</span><span class="sxs-lookup"><span data-stu-id="3a2c7-121">SYSLIB0003</span></span>](syslib0003.md) | <span data-ttu-id="3a2c7-122">运行时不支持或不接受代码访问安全性 (CAS)。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-122">Code access security (CAS) is not supported or honored by the runtime.</span></span> |
| [<span data-ttu-id="3a2c7-123">SYSLIB0004</span><span class="sxs-lookup"><span data-stu-id="3a2c7-123">SYSLIB0004</span></span>](syslib0004.md) | <span data-ttu-id="3a2c7-124">不支持受约束的执行区域 (CER) 功能。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-124">The constrained execution region (CER) feature is not supported.</span></span> |
| [<span data-ttu-id="3a2c7-125">SYSLIB0005</span><span class="sxs-lookup"><span data-stu-id="3a2c7-125">SYSLIB0005</span></span>](syslib0005.md) | <span data-ttu-id="3a2c7-126">不支持全局程序集缓存 (GAC)。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-126">The global assembly cache (GAC) is not supported.</span></span> |
| [<span data-ttu-id="3a2c7-127">SYSLIB0006</span><span class="sxs-lookup"><span data-stu-id="3a2c7-127">SYSLIB0006</span></span>](syslib0006.md) | <span data-ttu-id="3a2c7-128"><xref:System.Threading.Thread.Abort?displayProperty=nameWithType> 不受支持并会引发 <xref:System.PlatformNotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-128"><xref:System.Threading.Thread.Abort?displayProperty=nameWithType> is not supported and throws <xref:System.PlatformNotSupportedException>.</span></span> |
| [<span data-ttu-id="3a2c7-129">SYSLIB0007</span><span class="sxs-lookup"><span data-stu-id="3a2c7-129">SYSLIB0007</span></span>](syslib0007.md) | <span data-ttu-id="3a2c7-130">不支持此加密算法的默认实现。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-130">The default implementation of this cryptography algorithm is not supported.</span></span> |
| [<span data-ttu-id="3a2c7-131">SYSLIB0008</span><span class="sxs-lookup"><span data-stu-id="3a2c7-131">SYSLIB0008</span></span>](syslib0008.md) | <span data-ttu-id="3a2c7-132"><xref:System.Runtime.CompilerServices.DebugInfoGenerator.CreatePdbGenerator> API 不受支持并会引发 <xref:System.PlatformNotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-132">The <xref:System.Runtime.CompilerServices.DebugInfoGenerator.CreatePdbGenerator> API is not supported and throws <xref:System.PlatformNotSupportedException>.</span></span> |
| [<span data-ttu-id="3a2c7-133">SYSLIB0009</span><span class="sxs-lookup"><span data-stu-id="3a2c7-133">SYSLIB0009</span></span>](syslib0009.md) | <span data-ttu-id="3a2c7-134"><xref:System.Net.AuthenticationManager.Authenticate%2A?displayProperty=nameWithType> 和 <xref:System.Net.AuthenticationManager.PreAuthenticate%2A?displayProperty=nameWithType> 方法都不受支持并会引发 <xref:System.PlatformNotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-134">The <xref:System.Net.AuthenticationManager.Authenticate%2A?displayProperty=nameWithType> and <xref:System.Net.AuthenticationManager.PreAuthenticate%2A?displayProperty=nameWithType> methods are not supported and throw <xref:System.PlatformNotSupportedException>.</span></span> |
| [<span data-ttu-id="3a2c7-135">SYSLIB0010</span><span class="sxs-lookup"><span data-stu-id="3a2c7-135">SYSLIB0010</span></span>](syslib0010.md) | <span data-ttu-id="3a2c7-136">某些远程处理 API 不受支持并会引发 <xref:System.PlatformNotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-136">Some remoting APIs are not supported and throw <xref:System.PlatformNotSupportedException>.</span></span> |
| [<span data-ttu-id="3a2c7-137">SYSLIB0011</span><span class="sxs-lookup"><span data-stu-id="3a2c7-137">SYSLIB0011</span></span>](syslib0011.md) | <span data-ttu-id="3a2c7-138"><xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 序列化已过时，不应使用。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-138"><xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> serialization is obsolete and should not be used.</span></span> |
| [<span data-ttu-id="3a2c7-139">SYSLIB0012</span><span class="sxs-lookup"><span data-stu-id="3a2c7-139">SYSLIB0012</span></span>](syslib0012.md) | <span data-ttu-id="3a2c7-140">包含 <xref:System.Reflection.Assembly.CodeBase?displayProperty=nameWithType> 和 <xref:System.Reflection.Assembly.EscapedCodeBase?displayProperty=nameWithType> 只是为了实现 .NET Framework 兼容性。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-140"><xref:System.Reflection.Assembly.CodeBase?displayProperty=nameWithType> and <xref:System.Reflection.Assembly.EscapedCodeBase?displayProperty=nameWithType> are only included for .NET Framework compatibility.</span></span> <span data-ttu-id="3a2c7-141">请改用 <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-141">Use <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType> instead.</span></span> |

## <a name="suppress-warnings"></a><span data-ttu-id="3a2c7-142">禁止显示警告</span><span class="sxs-lookup"><span data-stu-id="3a2c7-142">Suppress warnings</span></span>

<span data-ttu-id="3a2c7-143">如果必须使用过时 API，并且 `SYSLIBxxxx` 诊断没有显示为错误，则可以在代码或项目文件中取消该警告。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-143">If you must use the obsolete APIs and the `SYSLIBxxxx` diagnostic does not surface as an error, you can suppress the warning in code or in your project file.</span></span>

<span data-ttu-id="3a2c7-144">在代码中：</span><span class="sxs-lookup"><span data-stu-id="3a2c7-144">In code:</span></span>

```csharp
// Disable the warning.
#pragma warning disable SYSLIB0001
// Code that uses obsolete API.
...
// Re-enable the warning.
#pragma warning restore SYSLIB0001
```

<span data-ttu-id="3a2c7-145">项目文件：</span><span class="sxs-lookup"><span data-stu-id="3a2c7-145">Project file:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
   <TargetFramework>net5.0</TargetFramework>
   <!-- NoWarn below suppresses SYSLIB0001 project-wide -->
   <NoWarn>$(NoWarn);SYSLIB0001</NoWarn>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="3a2c7-146">以这种方式取消警告只会禁用特定的过时警告。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-146">Suppressing a warning in this way only disables that specific obsoletion warning.</span></span> <span data-ttu-id="3a2c7-147">它不会禁用任何其他警告，包括其他过时警告。</span><span class="sxs-lookup"><span data-stu-id="3a2c7-147">It doesn't disable any other warnings, including other obsoletion warnings.</span></span>
