---
ms.openlocfilehash: 5b49dcae45e44bfd9ec3e150ad25c3f21d62c18e
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2020
ms.locfileid: "91955327"
---
### <a name="jsonserializerserialize-throws-argumentnullexception-when-type-parameter-is-null"></a><span data-ttu-id="9bc97-101">JsonSerializer.Serialize 在类型参数为 null 时引发 ArgumentNullException</span><span class="sxs-lookup"><span data-stu-id="9bc97-101">JsonSerializer.Serialize throws ArgumentNullException when type parameter is null</span></span>

<span data-ttu-id="9bc97-102">现在，每当为 <xref:System.Type> 参数传递 `null` 时，具有 <xref:System.Type> 参数的 <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType>、<xref:System.Text.Json.JsonSerializer.SerializeAsync%2A?displayProperty=nameWithType> 和 <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> 重载就会引发 <xref:System.ArgumentNullException>。</span><span class="sxs-lookup"><span data-stu-id="9bc97-102"><xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType>, <xref:System.Text.Json.JsonSerializer.SerializeAsync%2A?displayProperty=nameWithType>, and <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> overloads that have a <xref:System.Type> parameter now throw an <xref:System.ArgumentNullException> whenever `null` is passed for the <xref:System.Type> parameter.</span></span>

#### <a name="change-description"></a><span data-ttu-id="9bc97-103">更改描述</span><span class="sxs-lookup"><span data-stu-id="9bc97-103">Change description</span></span>

<span data-ttu-id="9bc97-104">在 .NET Core 3.1 中，当为 `Type inputType` 参数传递 `null` 时，具有 <xref:System.Type> 参数的 <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType>、<xref:System.Text.Json.JsonSerializer.SerializeAsync(System.IO.Stream,System.Object,System.Type,System.Text.Json.JsonSerializerOptions,System.Threading.CancellationToken)?displayProperty=nameWithType> 和 <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=nameWithType> 重载会引发 <xref:System.ArgumentNullException>，但如果 `Object value` 参数也为 `null`，则不会引发该异常。</span><span class="sxs-lookup"><span data-stu-id="9bc97-104">In .NET Core 3.1, the <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType>, <xref:System.Text.Json.JsonSerializer.SerializeAsync(System.IO.Stream,System.Object,System.Type,System.Text.Json.JsonSerializerOptions,System.Threading.CancellationToken)?displayProperty=nameWithType>, and <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=nameWithType> overloads that have a <xref:System.Type> parameter throw an <xref:System.ArgumentNullException> when `null` is passed for the `Type inputType` parameter, but not if the `Object value` parameter is also `null`.</span></span> <span data-ttu-id="9bc97-105">从 .NET 5.0 开始，当为 <xref:System.Type> 参数传递 `null` 时，这些方法始终会引发 <xref:System.ArgumentNullException>。</span><span class="sxs-lookup"><span data-stu-id="9bc97-105">Starting in .NET 5.0, these methods *always* throw an <xref:System.ArgumentNullException> when `null` is passed for the <xref:System.Type> parameter.</span></span>

<span data-ttu-id="9bc97-106">在 .NET Core 3.1 中的行为：</span><span class="sxs-lookup"><span data-stu-id="9bc97-106">Behavior in .NET Core 3.1:</span></span>

```csharp
// Returns a string with value "null".
JsonSerializer.Serialize(null, null);

// Returns a byte array with value "null".
JsonSerializer.SerializeToUtf8Bytes(null, null);
```

<span data-ttu-id="9bc97-107">在 .NET 5.0 和更高版本中的行为：</span><span class="sxs-lookup"><span data-stu-id="9bc97-107">Behavior in .NET 5.0 and later:</span></span>

```csharp
// Throws ArgumentNullException: "Value cannot be null. (Parameter 'inputType')".
JsonSerializer.Serialize(null, null);

// Throws ArgumentNullException: "Value cannot be null. (Parameter 'inputType')".
JsonSerializer.SerializeToUtf8Bytes(null, null);
```

#### <a name="version-introduced"></a><span data-ttu-id="9bc97-108">引入的版本</span><span class="sxs-lookup"><span data-stu-id="9bc97-108">Version introduced</span></span>

<span data-ttu-id="9bc97-109">5.0</span><span class="sxs-lookup"><span data-stu-id="9bc97-109">5.0</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="9bc97-110">更改原因</span><span class="sxs-lookup"><span data-stu-id="9bc97-110">Reason for change</span></span>

<span data-ttu-id="9bc97-111">为 `Type inputType` 参数传入 `null` 是不被接受的，应始终引发 <xref:System.ArgumentNullException>。</span><span class="sxs-lookup"><span data-stu-id="9bc97-111">Passing in `null` for the `Type inputType` parameter is unacceptable and should always throw an <xref:System.ArgumentNullException>.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="9bc97-112">建议的操作</span><span class="sxs-lookup"><span data-stu-id="9bc97-112">Recommended action</span></span>

<span data-ttu-id="9bc97-113">请确保不会为这些方法的 `Type inputType` 参数传递 `null`。</span><span class="sxs-lookup"><span data-stu-id="9bc97-113">Make sure that you are not passing `null` for the `Type inputType` parameter of these methods.</span></span>

#### <a name="category"></a><span data-ttu-id="9bc97-114">类别</span><span class="sxs-lookup"><span data-stu-id="9bc97-114">Category</span></span>

<span data-ttu-id="9bc97-115">序列化</span><span class="sxs-lookup"><span data-stu-id="9bc97-115">Serialization</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="9bc97-116">受影响的 API</span><span class="sxs-lookup"><span data-stu-id="9bc97-116">Affected APIs</span></span>

- <xref:System.Text.Json.JsonSerializer.Serialize(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.Serialize(System.Text.Json.Utf8JsonWriter,System.Object,System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.SerializeAsync(System.IO.Stream,System.Object,System.Type,System.Text.Json.JsonSerializerOptions,System.Threading.CancellationToken)?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=fullName>

<!--

#### Affected APIs

- `M:System.Text.Json.JsonSerializer.Serialize(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)`
- `M:System.Text.Json.JsonSerializer.Serialize(System.Text.Json.Utf8JsonWriter,System.Object,System.Type,System.Text.Json.JsonSerializerOptions)`
- `M:System.Text.Json.JsonSerializer.SerializeAsync(System.IO.Stream,System.Object,System.Type,System.Text.Json.JsonSerializerOptions,System.Threading.CancellationToken)`
- `M:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)`

-->
