---
ms.openlocfilehash: 43bd1481ca6c3d3444afda2e2a2c67e7236b4402
ms.sourcegitcommit: 98d20cb038669dca4a195eb39af37d22ea9d008e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92434899"
---
### <a name="binaryformatter-serialization-methods-are-obsolete-and-prohibited-in-aspnet-apps"></a><span data-ttu-id="7a5eb-101">BinaryFormatter 序列化方法已过时，并且已在 ASP.NET 应用中禁用</span><span class="sxs-lookup"><span data-stu-id="7a5eb-101">BinaryFormatter serialization methods are obsolete and prohibited in ASP.NET apps</span></span>

<span data-ttu-id="7a5eb-102"><xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter><xref:System.Runtime.Serialization.Formatter> 和 <xref:System.Runtime.Serialization.IFormatter> 上的 `Serialize` 和 `Deserialize` 方法现已过时，不再作为警告显示。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-102">`Serialize` and `Deserialize` methods on <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>, <xref:System.Runtime.Serialization.Formatter>, and <xref:System.Runtime.Serialization.IFormatter> are now obsolete as warning.</span></span> <span data-ttu-id="7a5eb-103">此外，ASP.NET 应用默认情况下禁止 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 序列化。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-103">Additionally, <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> serialization is prohibited by default for ASP.NET apps.</span></span>

#### <a name="change-description"></a><span data-ttu-id="7a5eb-104">更改描述</span><span class="sxs-lookup"><span data-stu-id="7a5eb-104">Change description</span></span>

<span data-ttu-id="7a5eb-105">由于 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 存在[安全漏洞](../../../../docs/standard/serialization/binaryformatter-security-guide.md#binaryformatter-security-vulnerabilities)，因此，以下方法现已过时，并生成 ID 为 `SYSLIB0011` 的编译时警告。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-105">Due to [security vulnerabilities](../../../../docs/standard/serialization/binaryformatter-security-guide.md#binaryformatter-security-vulnerabilities) in <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>, the following methods are now obsolete and produce a compile-time warning with ID `SYSLIB0011`.</span></span> <span data-ttu-id="7a5eb-106">此外，在 ASP.NET Core 5.0 及更高版本的应用中，除非 Web 应用已重新启用 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 功能，否则它们会引发 <xref:System.NotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-106">Additionally, in ASP.NET Core 5.0 and later apps, they will throw a <xref:System.NotSupportedException>, unless the web app has re-enabled <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> functionality.</span></span>

- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=nameWithType>

<span data-ttu-id="7a5eb-107">以下序列化方法现在也已过时并生成警告 `SYSLIB0011`，但没有行为变更：</span><span class="sxs-lookup"><span data-stu-id="7a5eb-107">The following serialization methods are also obsolete and produce warning `SYSLIB0011`, but have no behavioral changes:</span></span>

- <xref:System.Runtime.Serialization.Formatter.Serialize(System.IO.Stream,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.IFormatter.Serialize(System.IO.Stream,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.IFormatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType>

#### <a name="version-introduced"></a><span data-ttu-id="7a5eb-108">引入的版本</span><span class="sxs-lookup"><span data-stu-id="7a5eb-108">Version introduced</span></span>

<span data-ttu-id="7a5eb-109">5.0 预览版 8</span><span class="sxs-lookup"><span data-stu-id="7a5eb-109">5.0 Preview 8</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="7a5eb-110">更改原因</span><span class="sxs-lookup"><span data-stu-id="7a5eb-110">Reason for change</span></span>

<span data-ttu-id="7a5eb-111">在 .NET 生态系统中逐步停用 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 的过程中，这些方法被标记为“过时”。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-111">These methods are marked obsolete as part of an effort to wind down usage of <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> within the .NET ecosystem.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="7a5eb-112">建议操作</span><span class="sxs-lookup"><span data-stu-id="7a5eb-112">Recommended action</span></span>

- <span data-ttu-id="7a5eb-113">停止在代码中使用 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-113">Stop using <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> in your code.</span></span> <span data-ttu-id="7a5eb-114">此时，考虑使用 <xref:System.Text.Json.JsonSerializer> 或 <xref:System.Xml.Serialization.XmlSerializer>。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-114">Instead, consider using <xref:System.Text.Json.JsonSerializer> or <xref:System.Xml.Serialization.XmlSerializer>.</span></span> <span data-ttu-id="7a5eb-115">有关详细信息，请参阅 [BinaryFormatter 安全指南](../../../../docs/standard/serialization/binaryformatter-security-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-115">For more information, see [BinaryFormatter security guide](../../../../docs/standard/serialization/binaryformatter-security-guide.md).</span></span>

- <span data-ttu-id="7a5eb-116">可以暂时取消 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 编译时警告 `SYSLIB0011`。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-116">You can temporarily suppress the <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> compile-time warning, which is `SYSLIB0011`.</span></span> <span data-ttu-id="7a5eb-117">建议在选择此选项之前，全面评估代码风险。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-117">We recommend that you thoroughly assess your code for risks before choosing this option.</span></span> <span data-ttu-id="7a5eb-118">取消警告的最简单方法是用 `#pragma` 指令将单个调用站点括起来。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-118">The easiest way to suppress the warnings is to surround the individual call site with `#pragma` directives.</span></span>

  ```csharp
  // Now read the purchase order back from disk
  using (var readStream = new FileStream("myfile.bin", FileMode.Open))
  {
      var formatter = new BinaryFormatter();
  #pragma warning disable SYSLIB0011
      return (PurchaseOrder)formatter.Deserialize(readStream);
  #pragma warning restore SYSLIB0011
  }
  ```

  <span data-ttu-id="7a5eb-119">另外，还可以在项目文件中取消警告。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-119">You can also suppress the warning in the project file.</span></span>

  ```xml
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net5.0</TargetFramework>
    <!-- Disable "BinaryFormatter is obsolete" warnings for entire project -->
    <NoWarn>$(NoWarn);SYSLIB0011</NoWarn>
  </PropertyGroup>
  ```

  <span data-ttu-id="7a5eb-120">如果在项目文件中取消警告，会取消项目中所有代码文件的警告。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-120">If you suppress the warning in the project file, the warning is suppressed for all code files in the project.</span></span> <span data-ttu-id="7a5eb-121">取消 `SYSLIB0011` 不会取消因使用其他过时 API 导致的警告。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-121">Suppressing `SYSLIB0011` does not suppress warnings caused by using other obsolete APIs.</span></span>

- <span data-ttu-id="7a5eb-122">若要继续在 ASP.NET 应用中使用 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>，可以在项目文件中重新启用它。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-122">To continue using <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> in ASP.NET apps, you can re-enable it in the project file.</span></span> <span data-ttu-id="7a5eb-123">不过，非常不建议这样做。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-123">However, it's strongly recommended not to do this.</span></span> <span data-ttu-id="7a5eb-124">有关详细信息，请参阅 [BinaryFormatter 安全指南](../../../../docs/standard/serialization/binaryformatter-security-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-124">For more information, see [BinaryFormatter security guide](../../../../docs/standard/serialization/binaryformatter-security-guide.md).</span></span>

  ```xml
  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    <!-- Warning: Setting the following switch is *NOT* recommended in web apps. -->
    <EnableUnsafeBinaryFormatterSerialization>true</EnableUnsafeBinaryFormatterSerialization>
  </PropertyGroup>
  ```

<span data-ttu-id="7a5eb-125">若要详细了解建议的操作，请参阅[修复 BinaryFormatter 过时和禁用错误](https://aka.ms/binaryformatter)。</span><span class="sxs-lookup"><span data-stu-id="7a5eb-125">For more information about recommended actions, see [Resolving BinaryFormatter obsoletion and disablement errors](https://aka.ms/binaryformatter).</span></span>

#### <a name="category"></a><span data-ttu-id="7a5eb-126">类别</span><span class="sxs-lookup"><span data-stu-id="7a5eb-126">Category</span></span>

- <span data-ttu-id="7a5eb-127">Core .NET 库</span><span class="sxs-lookup"><span data-stu-id="7a5eb-127">Core .NET libraries</span></span>
- <span data-ttu-id="7a5eb-128">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7a5eb-128">ASP.NET</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="7a5eb-129">受影响的 API</span><span class="sxs-lookup"><span data-stu-id="7a5eb-129">Affected APIs</span></span>

- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=fullName>
- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=fullName>
- <xref:System.Runtime.Serialization.Formatter.Serialize(System.IO.Stream,System.Object)?displayProperty=fullName>
- <xref:System.Runtime.Serialization.Formatter.Deserialize(System.IO.Stream)?displayProperty=fullName>
- <xref:System.Runtime.Serialization.IFormatter.Serialize(System.IO.Stream,System.Object)?displayProperty=fullName>
- <xref:System.Runtime.Serialization.IFormatter.Deserialize(System.IO.Stream)?displayProperty=fullName>

<!--

#### Affected APIs

- `Overload:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize`
- `Overload:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize`
- `M:System.Runtime.Serialization.Formatter.Serialize(System.IO.Stream,System.Object)`
- `M:System.Runtime.Serialization.Formatter.Deserialize(System.IO.Stream)`
- `M:System.Runtime.Serialization.IFormatter.Serialize(System.IO.Stream,System.Object)`
- `M:System.Runtime.Serialization.IFormatter.Deserialize(System.IO.Stream)`

-->
