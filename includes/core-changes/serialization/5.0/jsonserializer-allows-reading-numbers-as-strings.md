---
ms.openlocfilehash: a93856aac97af5c392a2e4698d2da42413cfc3c8
ms.sourcegitcommit: 98d20cb038669dca4a195eb39af37d22ea9d008e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92434977"
---
### <a name="aspnet-core-apps-allow-deserializing-quoted-numbers"></a><span data-ttu-id="9ab46-101">ASP.NET Core 应用允许反序列化带引号的数字</span><span class="sxs-lookup"><span data-stu-id="9ab46-101">ASP.NET Core apps allow deserializing quoted numbers</span></span>

<span data-ttu-id="9ab46-102">从 .NET 5.0 开始，ASP.NET Core 应用使用 <xref:System.Text.Json.JsonSerializerDefaults.Web?displayProperty=nameWithType> 指定的默认反序列化选项。</span><span class="sxs-lookup"><span data-stu-id="9ab46-102">Starting in .NET 5.0, ASP.NET Core apps use the default deserialization options as specified by <xref:System.Text.Json.JsonSerializerDefaults.Web?displayProperty=nameWithType>.</span></span> <span data-ttu-id="9ab46-103"><xref:System.Text.Json.JsonSerializerDefaults.Web> 选项集包括将 <xref:System.Text.Json.JsonSerializerOptions.NumberHandling> 设置为 <xref:System.Text.Json.Serialization.JsonNumberHandling.AllowReadingFromString?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="9ab46-103">The <xref:System.Text.Json.JsonSerializerDefaults.Web> set of options includes setting <xref:System.Text.Json.JsonSerializerOptions.NumberHandling> to <xref:System.Text.Json.Serialization.JsonNumberHandling.AllowReadingFromString?displayProperty=nameWithType>.</span></span> <span data-ttu-id="9ab46-104">此更改意味着 ASP.NET Core 应用将成功反序列化以 JSON 字符串表示的数字，而不会引发异常。</span><span class="sxs-lookup"><span data-stu-id="9ab46-104">This change means that ASP.NET Core apps will successfully deserialize numbers that are represented as JSON strings, instead of throwing an exception.</span></span>

#### <a name="change-description"></a><span data-ttu-id="9ab46-105">更改描述</span><span class="sxs-lookup"><span data-stu-id="9ab46-105">Change description</span></span>

<span data-ttu-id="9ab46-106">在 .NET Core 3.0 - 3.1 中，如果 <xref:System.Text.Json.JsonSerializer> 在 JSON 有效负载中遇到带引号的数字，则在反序列化过程中将引发 <xref:System.Text.Json.JsonException>。</span><span class="sxs-lookup"><span data-stu-id="9ab46-106">In .NET Core 3.0 - 3.1, <xref:System.Text.Json.JsonSerializer> throws a <xref:System.Text.Json.JsonException> during deserialization if it encounters a quoted number in a JSON payload.</span></span> <span data-ttu-id="9ab46-107">带引号的数字用于映射对象图中的数字属性。</span><span class="sxs-lookup"><span data-stu-id="9ab46-107">The quoted numbers are used to map with number properties in object graphs.</span></span> <span data-ttu-id="9ab46-108">在 .NET Core 3.0 - 3.1 中，仅从 <xref:System.Text.Json.JsonTokenType.Number?displayProperty=nameWithType> 令牌中读取数字。</span><span class="sxs-lookup"><span data-stu-id="9ab46-108">In .NET Core 3.0 - 3.1, numbers are only read from <xref:System.Text.Json.JsonTokenType.Number?displayProperty=nameWithType> tokens.</span></span>

<span data-ttu-id="9ab46-109">从 .NET 5.0 开始，默认情况下，对于 ASP.NET Core 应用，JSON 有效负载中带引号的数字被视为有效。</span><span class="sxs-lookup"><span data-stu-id="9ab46-109">Starting in .NET 5.0, quoted numbers in JSON payloads are considered valid, by default, for ASP.NET Core apps.</span></span> <span data-ttu-id="9ab46-110">不会在反序列化带引号的数字期间引发异常。</span><span class="sxs-lookup"><span data-stu-id="9ab46-110">No exception is thrown during deserialization of quoted numbers.</span></span>

> [!TIP]
>
> - <span data-ttu-id="9ab46-111">默认的独立 <xref:System.Text.Json.JsonSerializer> 或 <xref:System.Text.Json.JsonSerializerOptions> 没有任何行为更改。</span><span class="sxs-lookup"><span data-stu-id="9ab46-111">There is no behavior change for the default, standalone <xref:System.Text.Json.JsonSerializer> or <xref:System.Text.Json.JsonSerializerOptions>.</span></span>
> - <span data-ttu-id="9ab46-112">从技术上说，这并不是一项中断性变更，因为这样做会使方案更宽松，而不是更严格（也就是说，它会强制来自 JSON 字符串的数字，而不是引发异常）。</span><span class="sxs-lookup"><span data-stu-id="9ab46-112">This is technically not a breaking change, since it makes a scenario more permissive instead of more restrictive (that is, it succeeds in coercing a number from a JSON string instead of throwing an exception).</span></span> <span data-ttu-id="9ab46-113">然而，由于这是一项重大的行为变更，会影响许多 ASP.NET Core 应用，因此在此处进行了说明。</span><span class="sxs-lookup"><span data-stu-id="9ab46-113">However, since this is a significant behavioral change that affects many ASP.NET Core apps, it is documented here.</span></span>
> - <span data-ttu-id="9ab46-114"><xref:System.Net.Http.Json.HttpClientJsonExtensions.GetFromJsonAsync%2A?displayProperty=nameWithType> 和 <xref:System.Net.Http.Json.HttpContentJsonExtensions.ReadFromJsonAsync%2A?displayProperty=nameWithType> 扩展方法还使用 <xref:System.Text.Json.JsonSerializerDefaults.Web> 序列化选项集。</span><span class="sxs-lookup"><span data-stu-id="9ab46-114">The <xref:System.Net.Http.Json.HttpClientJsonExtensions.GetFromJsonAsync%2A?displayProperty=nameWithType> and <xref:System.Net.Http.Json.HttpContentJsonExtensions.ReadFromJsonAsync%2A?displayProperty=nameWithType> extension methods also use the <xref:System.Text.Json.JsonSerializerDefaults.Web> set of serialization options.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="9ab46-115">引入的版本</span><span class="sxs-lookup"><span data-stu-id="9ab46-115">Version introduced</span></span>

<span data-ttu-id="9ab46-116">5.0</span><span class="sxs-lookup"><span data-stu-id="9ab46-116">5.0</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="9ab46-117">更改原因</span><span class="sxs-lookup"><span data-stu-id="9ab46-117">Reason for change</span></span>

<span data-ttu-id="9ab46-118">多个用户已请求在 <xref:System.Text.Json.JsonSerializer> 中进行更宽松的数字处理的选项。</span><span class="sxs-lookup"><span data-stu-id="9ab46-118">Multiple users have requested an option for more permissive number handling in <xref:System.Text.Json.JsonSerializer>.</span></span> <span data-ttu-id="9ab46-119">此反馈表明，许多 JSON 创建方（例如 Web 上的服务）发出带引号的数字。</span><span class="sxs-lookup"><span data-stu-id="9ab46-119">This feedback indicates that many JSON producers (for example, services across the web) emit quoted numbers.</span></span> <span data-ttu-id="9ab46-120">通过允许读取带引号的数字（反序列化），.NET 应用可以在 Web 上下文中（默认情况下）成功解析这些有效负载。</span><span class="sxs-lookup"><span data-stu-id="9ab46-120">By allowing quoted numbers to be read (deserialized), .NET apps can successfully parse these payloads, by default, in web contexts.</span></span> <span data-ttu-id="9ab46-121">该配置通过 <xref:System.Text.Json.JsonSerializerDefaults.Web?displayProperty=nameWithType> 公开，因此你可以在不同的应用程序层（例如客户端、服务器和共享）上指定相同的选项。</span><span class="sxs-lookup"><span data-stu-id="9ab46-121">The configuration is exposed via <xref:System.Text.Json.JsonSerializerDefaults.Web?displayProperty=nameWithType> so that you can specify the same options across different application layers, for example, client, server, and shared.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="9ab46-122">建议操作</span><span class="sxs-lookup"><span data-stu-id="9ab46-122">Recommended action</span></span>

<span data-ttu-id="9ab46-123">如果此更改是中断性的，例如，如果依赖于验证的严格数字处理，则可以重新启用以前的行为。</span><span class="sxs-lookup"><span data-stu-id="9ab46-123">If this change is disruptive, for example, if you depend on the strict number handling for validation, you can re-enable the previous behavior.</span></span> <span data-ttu-id="9ab46-124">将 <xref:System.Text.Json.JsonSerializerOptions.NumberHandling?displayProperty=nameWithType> 选项设置为 <xref:System.Text.Json.Serialization.JsonNumberHandling.Strict?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="9ab46-124">Set the <xref:System.Text.Json.JsonSerializerOptions.NumberHandling?displayProperty=nameWithType> option to <xref:System.Text.Json.Serialization.JsonNumberHandling.Strict?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="9ab46-125">对于 ASP.NET Core MVC 和 Web API 应用，可以使用以下代码在 `Startup` 中配置选项：</span><span class="sxs-lookup"><span data-stu-id="9ab46-125">For ASP.NET Core MVC and web API apps, you can configure the option in `Startup` by using the following code:</span></span>

```csharp
services.AddControllers()
   .AddJsonOptions(options.NumberHandling = JsonNumberHandling.Strict);
```

#### <a name="category"></a><span data-ttu-id="9ab46-126">类别</span><span class="sxs-lookup"><span data-stu-id="9ab46-126">Category</span></span>

- <span data-ttu-id="9ab46-127">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="9ab46-127">ASP.NET Core</span></span>
- <span data-ttu-id="9ab46-128">序列化</span><span class="sxs-lookup"><span data-stu-id="9ab46-128">Serialization</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="9ab46-129">受影响的 API</span><span class="sxs-lookup"><span data-stu-id="9ab46-129">Affected APIs</span></span>

- <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.DeserializeAsync%2A?displayProperty=fullName>

<!--

#### Affected APIs

- `Overload:System.Text.Json.JsonSerializer.Deserialize`
- `Overload:System.Text.Json.JsonSerializer.DeserializeAsync`

-->
