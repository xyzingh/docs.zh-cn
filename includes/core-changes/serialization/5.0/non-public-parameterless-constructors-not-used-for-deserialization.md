---
ms.openlocfilehash: 3692848a0cbd4bbbe3c7bb4d2c22a2b19de732e4
ms.sourcegitcommit: 39b1d5f2978be15409c189a66ab30781d9082cd8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2020
ms.locfileid: "92050454"
---
### <a name="non-public-parameterless-constructors-not-used-for-deserialization"></a><span data-ttu-id="74a07-101">非公共的无参数构造函数不用于反序列化</span><span class="sxs-lookup"><span data-stu-id="74a07-101">Non-public, parameterless constructors not used for deserialization</span></span>

<span data-ttu-id="74a07-102">为了在所有受支持的目标框架名字对象 (TFM) 之间保持一致，默认情况下，非公共的无参数构造函数不再用于 <xref:System.Text.Json.JsonSerializer> 的反序列化。</span><span class="sxs-lookup"><span data-stu-id="74a07-102">For consistency across all supported target framework monikers (TFMs), non-public, parameterless constructors are no longer used for deserialization with <xref:System.Text.Json.JsonSerializer>, by default.</span></span>

#### <a name="change-description"></a><span data-ttu-id="74a07-103">更改描述</span><span class="sxs-lookup"><span data-stu-id="74a07-103">Change description</span></span>

<span data-ttu-id="74a07-104">支持 .NET Standard 2.0 及更高版本（即版本 4.6.0 - 4.7.2）的独立 [System.Text.Json NuGet 包](https://www.nuget.org/packages/System.Text.Json/)的行为与 .NET Core 3.0 和 3.1 上的内置行为不一致。</span><span class="sxs-lookup"><span data-stu-id="74a07-104">The standalone [System.Text.Json NuGet packages](https://www.nuget.org/packages/System.Text.Json/) that support .NET Standard 2.0 and higher, that is, versions 4.6.0-4.7.2, behave inconsistently with the built-in behavior on .NET Core 3.0 and 3.1.</span></span> <span data-ttu-id="74a07-105">在 .NET Core 3.x 上，内部和专用构造函数可用于反序列化。</span><span class="sxs-lookup"><span data-stu-id="74a07-105">On .NET Core 3.x, internal and private constructors can be used for deserialization.</span></span> <span data-ttu-id="74a07-106">在独立包中，不允许使用非公共构造函数，如果未定义任何公共的无参数构造函数，则会引发 <xref:System.MissingMethodException>。</span><span class="sxs-lookup"><span data-stu-id="74a07-106">In the standalone packages, non-public constructors are not allowed, and a <xref:System.MissingMethodException> is thrown if no public, parameterless constructor is defined.</span></span>

<span data-ttu-id="74a07-107">从 .NET 5.0 和 System.Text.Json NuGet 包 5.0.0 开始，NuGet 包与内置 API 的行为一致。</span><span class="sxs-lookup"><span data-stu-id="74a07-107">Starting with .NET 5.0 and System.Text.Json NuGet package 5.0.0, the behavior is consistent between the NuGet package and the built-in APIs.</span></span> <span data-ttu-id="74a07-108">默认情况下，序列化程序会忽略非公共构造函数，包括无参数构造函数。</span><span class="sxs-lookup"><span data-stu-id="74a07-108">Non-public constructors, including parameterless constructors, are ignored by the serializer by default.</span></span> <span data-ttu-id="74a07-109">序列化程序使用下面一种构造函数进行反序列化：</span><span class="sxs-lookup"><span data-stu-id="74a07-109">The serializer uses one of the following constructors for deserialization:</span></span>

- <span data-ttu-id="74a07-110">用 <xref:System.Text.Json.Serialization.JsonConstructorAttribute> 注释的公共构造函数。</span><span class="sxs-lookup"><span data-stu-id="74a07-110">Public constructor annotated with <xref:System.Text.Json.Serialization.JsonConstructorAttribute>.</span></span>
- <span data-ttu-id="74a07-111">公共无参数构造函数。</span><span class="sxs-lookup"><span data-stu-id="74a07-111">Public parameterless constructor.</span></span>
- <span data-ttu-id="74a07-112">公共参数化构造函数（如果它是唯一的公共构造函数）。</span><span class="sxs-lookup"><span data-stu-id="74a07-112">Public parameterized constructor (if it's the only public constructor present).</span></span>

<span data-ttu-id="74a07-113">如果这些构造函数都不可用，则在尝试对该类型进行反序列化时，将引发 <xref:System.NotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="74a07-113">If none of these constructors are available, a <xref:System.NotSupportedException> is thrown if you attempt to deserialize the type.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="74a07-114">引入的版本</span><span class="sxs-lookup"><span data-stu-id="74a07-114">Version introduced</span></span>

<span data-ttu-id="74a07-115">5.0</span><span class="sxs-lookup"><span data-stu-id="74a07-115">5.0</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="74a07-116">更改原因</span><span class="sxs-lookup"><span data-stu-id="74a07-116">Reason for change</span></span>

- <span data-ttu-id="74a07-117">为了在 <xref:System.Text.Json?displayProperty=fullName> 针对其生成的所有目标框架名字对象 (TFM) 之间强制执行一致的行为（.NET Core 3.0 和更高版本以及 .NET Standard 2.0）</span><span class="sxs-lookup"><span data-stu-id="74a07-117">To enforce consistent behavior between all target framework monikers (TFMs) that <xref:System.Text.Json?displayProperty=fullName> builds for (.NET Core 3.0 and later versions and .NET Standard 2.0)</span></span>
- <span data-ttu-id="74a07-118">因为 <xref:System.Text.Json.JsonSerializer> 不应调用某类型的非公共外围应用，无论它是构造函数、属性还是字段。</span><span class="sxs-lookup"><span data-stu-id="74a07-118">Because <xref:System.Text.Json.JsonSerializer> shouldn't call the non-public surface area of a type, whether that's a constructor, a property, or a field.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="74a07-119">建议的操作</span><span class="sxs-lookup"><span data-stu-id="74a07-119">Recommended action</span></span>

- <span data-ttu-id="74a07-120">如果你拥有该类型并且这样可行，则将无参数构造函数设为公共。</span><span class="sxs-lookup"><span data-stu-id="74a07-120">If you own the type and it's feasible, make the parameterless constructor public.</span></span>
- <span data-ttu-id="74a07-121">否则，针对该类型实现 `JsonConverter<T>`，并控制反序列化行为。</span><span class="sxs-lookup"><span data-stu-id="74a07-121">Otherwise, implement a `JsonConverter<T>` for the type and control the deserialization behavior.</span></span>

#### <a name="category"></a><span data-ttu-id="74a07-122">类别</span><span class="sxs-lookup"><span data-stu-id="74a07-122">Category</span></span>

<span data-ttu-id="74a07-123">序列化</span><span class="sxs-lookup"><span data-stu-id="74a07-123">Serialization</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="74a07-124">受影响的 API</span><span class="sxs-lookup"><span data-stu-id="74a07-124">Affected APIs</span></span>

- <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.DeserializeAsync%2A?displayProperty=fullName>

<!--

#### Affected APIs

- `Overload:System.Text.Json.JsonSerializer.Deserialize`
- `Overload:System.Text.Json.JsonSerializer.DeserializeAsync`

-->
