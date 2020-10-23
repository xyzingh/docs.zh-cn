---
title: 如何使用 C# 对 JSON 进行序列化和反序列化 - .NET
description: 了解如何使用 System.Text.Json 命名空间在 .NET 中向/从 JSON 进行序列化和反序列化。 文中包含示例代码。
ms.date: 10/09/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 0fda248b7d2e5a7cfa748447d0265565cb160b7e
ms.sourcegitcommit: e078b7540a8293ca1b604c9c0da1ff1506f0170b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "91997781"
---
# <a name="how-to-serialize-and-deserialize-marshal-and-unmarshal-json-in-net"></a><span data-ttu-id="0367b-104">如何在 .NET 中对 JSON 进行序列化和反序列化（封送和拆收）</span><span class="sxs-lookup"><span data-stu-id="0367b-104">How to serialize and deserialize (marshal and unmarshal) JSON in .NET</span></span>

<span data-ttu-id="0367b-105">本文演示如何使用 <xref:System.Text.Json?displayProperty=fullName> 命名空间向/从 JavaScript 对象表示法 (JSON) 进行序列化和反序列化。</span><span class="sxs-lookup"><span data-stu-id="0367b-105">This article shows how to use the <xref:System.Text.Json?displayProperty=fullName> namespace to serialize to and deserialize from JavaScript Object Notation (JSON).</span></span> <span data-ttu-id="0367b-106">如果要从 `Newtonsoft.Json` 移植现有代码，请参阅[如何迁移到 `System.Text.Json`](system-text-json-migrate-from-newtonsoft-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="0367b-106">If you're porting existing code from `Newtonsoft.Json`, see [How to migrate to `System.Text.Json`](system-text-json-migrate-from-newtonsoft-how-to.md).</span></span>

<span data-ttu-id="0367b-107">方向和示例代码直接使用库，而不是通过框架（如 [ASP.NET Core](/aspnet/core/)）。</span><span class="sxs-lookup"><span data-stu-id="0367b-107">The directions and sample code use the library directly, not through a framework such as [ASP.NET Core](/aspnet/core/).</span></span>

<span data-ttu-id="0367b-108">大多数序列化示例代码将 <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> 设置为 `true`，以 JSON 进行优质打印（包含缩进和空格，以提高可读性）。</span><span class="sxs-lookup"><span data-stu-id="0367b-108">Most of the serialization sample code sets <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> to `true` to "pretty-print" the JSON (with indentation and whitespace for human readability).</span></span> <span data-ttu-id="0367b-109">对于生产用途，通常对于此设置会接受默认值 `false`。</span><span class="sxs-lookup"><span data-stu-id="0367b-109">For production use, you would typically accept the default value of `false` for this setting.</span></span>

<span data-ttu-id="0367b-110">代码示例引用下面的类及其变体：</span><span class="sxs-lookup"><span data-stu-id="0367b-110">The code examples refer to the following class and variants of it:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

## <a name="namespaces"></a><span data-ttu-id="0367b-111">命名空间</span><span class="sxs-lookup"><span data-stu-id="0367b-111">Namespaces</span></span>

<span data-ttu-id="0367b-112"><xref:System.Text.Json> 命名空间包含所有入口点和主要类型。</span><span class="sxs-lookup"><span data-stu-id="0367b-112">The <xref:System.Text.Json> namespace contains all the entry points and the main types.</span></span> <span data-ttu-id="0367b-113"><xref:System.Text.Json.Serialization> 命名空间包含用于高级方案的特性和 API，以及特定于序列化和反序列化的自定义。</span><span class="sxs-lookup"><span data-stu-id="0367b-113">The <xref:System.Text.Json.Serialization> namespace contains attributes and APIs for advanced scenarios and customization specific to serialization and deserialization.</span></span> <span data-ttu-id="0367b-114">本文中演示的代码示例要求将 `using` 指令用于其中一个或两个命名空间：</span><span class="sxs-lookup"><span data-stu-id="0367b-114">The code examples shown in this article require `using` directives for one or both of these namespaces:</span></span>

```csharp
using System.Text.Json;
using System.Text.Json.Serialization;
```

<span data-ttu-id="0367b-115">`System.Text.Json`中当前不支持 <xref:System.Runtime.Serialization> 命名空间中的特性。</span><span class="sxs-lookup"><span data-stu-id="0367b-115">Attributes from the <xref:System.Runtime.Serialization> namespace aren't currently supported in `System.Text.Json`.</span></span>

## <a name="how-to-write-net-objects-to-json-serialize"></a><span data-ttu-id="0367b-116">如何将 .NET 对象编写为 JSON（序列化）</span><span class="sxs-lookup"><span data-stu-id="0367b-116">How to write .NET objects to JSON (serialize)</span></span>

<span data-ttu-id="0367b-117">若要将 JSON 编写为字符串或文件，请调用 <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="0367b-117">To write JSON to a string or to a file, call the <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> method.</span></span>

<span data-ttu-id="0367b-118">下面的示例将 JSON 创建为字符串：</span><span class="sxs-lookup"><span data-stu-id="0367b-118">The following example creates JSON as a string:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToString.cs?name=SnippetSerialize)]

<span data-ttu-id="0367b-119">下面的示例使用同步代码创建 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="0367b-119">The following example uses synchronous code to create a JSON file:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToFile.cs?name=SnippetSerialize)]

<span data-ttu-id="0367b-120">下面的示例使用异步代码创建 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="0367b-120">The following example uses asynchronous code to create a JSON file:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToFileAsync.cs?name=SnippetSerialize)]

<span data-ttu-id="0367b-121">前面的示例对要序列化的类型使用类型推理。</span><span class="sxs-lookup"><span data-stu-id="0367b-121">The preceding examples use type inference for the type being serialized.</span></span> <span data-ttu-id="0367b-122">`Serialize()` 的重载采用泛型类型参数：</span><span class="sxs-lookup"><span data-stu-id="0367b-122">An overload of `Serialize()` takes a generic type parameter:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToString.cs?name=SnippetSerializeWithGenericParameter)]

### <a name="serialization-example"></a><span data-ttu-id="0367b-123">序列化示例</span><span class="sxs-lookup"><span data-stu-id="0367b-123">Serialization example</span></span>

<span data-ttu-id="0367b-124">下面是一个包含集合类型属性和用户定义类型的示例类：</span><span class="sxs-lookup"><span data-stu-id="0367b-124">Here's an example class that contains collection-type properties and a user-defined type:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithPOCOs)]

> [!TIP]
> <span data-ttu-id="0367b-125">“POCO”代表[普通旧 CLR 对象](https://en.wikipedia.org/wiki/Plain_old_CLR_object)。</span><span class="sxs-lookup"><span data-stu-id="0367b-125">"POCO" stands for [plain old CLR object](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span></span> <span data-ttu-id="0367b-126">POCO 是一种 .NET 类型，它不通过继承或特性等依赖于任何框架特定类型。</span><span class="sxs-lookup"><span data-stu-id="0367b-126">A POCO is a .NET type that doesn't depend on any framework-specific types, for example, through inheritance or attributes.</span></span>

<span data-ttu-id="0367b-127">序列化以上类型的实例的 JSON 输出类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="0367b-127">The JSON output from serializing an instance of the preceding type looks like the following example.</span></span> <span data-ttu-id="0367b-128">默认情况下，JSON 输出会缩小：</span><span class="sxs-lookup"><span data-stu-id="0367b-128">The JSON output is minified by default:</span></span>

```json
{"Date":"2019-08-01T00:00:00-07:00","TemperatureCelsius":25,"Summary":"Hot","DatesAvailable":["2019-08-01T00:00:00-07:00","2019-08-02T00:00:00-07:00"],"TemperatureRanges":{"Cold":{"High":20,"Low":-10},"Hot":{"High":60,"Low":20}},"SummaryWords":["Cool","Windy","Humid"]}
```

<span data-ttu-id="0367b-129">下面的示例演示相同的 JSON，但进行了格式设置（即，具有空格和缩进的优质打印版本）：</span><span class="sxs-lookup"><span data-stu-id="0367b-129">The following example shows the same JSON, but formatted (that is, pretty-printed with whitespace and indentation):</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "DatesAvailable": [
    "2019-08-01T00:00:00-07:00",
    "2019-08-02T00:00:00-07:00"
  ],
  "TemperatureRanges": {
    "Cold": {
      "High": 20,
      "Low": -10
    },
    "Hot": {
      "High": 60,
      "Low": 20
    }
  },
  "SummaryWords": [
    "Cool",
    "Windy",
    "Humid"
  ]
}
```

### <a name="serialize-to-utf-8"></a><span data-ttu-id="0367b-130">序列化为 UTF-8</span><span class="sxs-lookup"><span data-stu-id="0367b-130">Serialize to UTF-8</span></span>

<span data-ttu-id="0367b-131">若要序列化为 UTF-8，请调用 <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> 方法：</span><span class="sxs-lookup"><span data-stu-id="0367b-131">To serialize to UTF-8, call the <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> method:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToUtf8.cs?name=SnippetSerialize)]

<span data-ttu-id="0367b-132">还有一个采用 <xref:System.Text.Json.Utf8JsonWriter> 的 <xref:System.Text.Json.JsonSerializer.Serialize%2A> 重载可用。</span><span class="sxs-lookup"><span data-stu-id="0367b-132">A <xref:System.Text.Json.JsonSerializer.Serialize%2A> overload that takes a <xref:System.Text.Json.Utf8JsonWriter> is also available.</span></span>

<span data-ttu-id="0367b-133">序列化为 UTF-8 比使用基于字符串的方法大约快 5-10%。</span><span class="sxs-lookup"><span data-stu-id="0367b-133">Serializing to UTF-8 is about 5-10% faster than using the string-based methods.</span></span> <span data-ttu-id="0367b-134">出现这种差别的原因是字节（作为 UTF-8）不需要转换为字符串 (UTF-16)。</span><span class="sxs-lookup"><span data-stu-id="0367b-134">The difference is because the bytes (as UTF-8) don't need to be converted to strings (UTF-16).</span></span>

## <a name="serialization-behavior"></a><span data-ttu-id="0367b-135">序列化行为</span><span class="sxs-lookup"><span data-stu-id="0367b-135">Serialization behavior</span></span>

* <span data-ttu-id="0367b-136">默认情况下，所有公共属性都会序列化。</span><span class="sxs-lookup"><span data-stu-id="0367b-136">By default, all public properties are serialized.</span></span> <span data-ttu-id="0367b-137">可以[指定要排除的属性](#exclude-properties-from-serialization)。</span><span class="sxs-lookup"><span data-stu-id="0367b-137">You can [specify properties to exclude](#exclude-properties-from-serialization).</span></span>
* <span data-ttu-id="0367b-138">[默认编码器](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default)会转义非 ASCII 字符、ASCII 范围内的 HTML 敏感字符以及根据 [RFC 8259 JSON 规范](https://tools.ietf.org/html/rfc8259#section-7)必须进行转义的字符。</span><span class="sxs-lookup"><span data-stu-id="0367b-138">The [default encoder](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) escapes non-ASCII characters, HTML-sensitive characters within the ASCII-range, and characters that must be escaped according to [the RFC 8259 JSON spec](https://tools.ietf.org/html/rfc8259#section-7).</span></span>
* <span data-ttu-id="0367b-139">默认情况下，JSON 会缩小。</span><span class="sxs-lookup"><span data-stu-id="0367b-139">By default, JSON is minified.</span></span> <span data-ttu-id="0367b-140">可以[对 JSON 进行优质打印](#serialize-to-formatted-json)。</span><span class="sxs-lookup"><span data-stu-id="0367b-140">You can [pretty-print the JSON](#serialize-to-formatted-json).</span></span>
* <span data-ttu-id="0367b-141">默认情况下，JSON 名称的大小写与 .NET 名称匹配。</span><span class="sxs-lookup"><span data-stu-id="0367b-141">By default, casing of JSON names matches the .NET names.</span></span> <span data-ttu-id="0367b-142">可以[自定义 JSON 名称大小写](#customize-json-names-and-values)。</span><span class="sxs-lookup"><span data-stu-id="0367b-142">You can [customize JSON name casing](#customize-json-names-and-values).</span></span>
* <span data-ttu-id="0367b-143">检测到循环引用并引发异常。</span><span class="sxs-lookup"><span data-stu-id="0367b-143">Circular references are detected and exceptions thrown.</span></span>
* <span data-ttu-id="0367b-144">当前不包括[字段](../../csharp/programming-guide/classes-and-structs/fields.md)。</span><span class="sxs-lookup"><span data-stu-id="0367b-144">Currently, [fields](../../csharp/programming-guide/classes-and-structs/fields.md) are excluded.</span></span>

<span data-ttu-id="0367b-145">支持的类型包括：</span><span class="sxs-lookup"><span data-stu-id="0367b-145">Supported types include:</span></span>

* <span data-ttu-id="0367b-146">映射到 JavaScript 基元的 .NET 基元，如数值类型、字符串和布尔。</span><span class="sxs-lookup"><span data-stu-id="0367b-146">.NET primitives that map to JavaScript primitives, such as numeric types, strings, and Boolean.</span></span>
* <span data-ttu-id="0367b-147">用户定义的[普通旧 CLR 对象 (POCO)](https://en.wikipedia.org/wiki/Plain_old_CLR_object)。</span><span class="sxs-lookup"><span data-stu-id="0367b-147">User-defined [plain old CLR objects (POCOs)](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span></span>
* <span data-ttu-id="0367b-148">一维和交错数组 (`ArrayName[][]`)。</span><span class="sxs-lookup"><span data-stu-id="0367b-148">One-dimensional and jagged arrays (`ArrayName[][]`).</span></span>
* <span data-ttu-id="0367b-149">`Dictionary<string,TValue>`其中 `TValue` 是 `object`、`JsonElement` 或 POCO。</span><span class="sxs-lookup"><span data-stu-id="0367b-149">`Dictionary<string,TValue>` where `TValue` is `object`, `JsonElement`, or a POCO.</span></span>
* <span data-ttu-id="0367b-150">以下命名空间中的集合。</span><span class="sxs-lookup"><span data-stu-id="0367b-150">Collections from the following namespaces.</span></span>
  * <xref:System.Collections>
  * <xref:System.Collections.Generic>
  * <xref:System.Collections.Immutable>

<span data-ttu-id="0367b-151">可以[实现自定义转换器](system-text-json-converters-how-to.md)以处理其他类型或提供内置转换器不支持的功能。</span><span class="sxs-lookup"><span data-stu-id="0367b-151">You can [implement custom converters](system-text-json-converters-how-to.md) to handle additional types or to provide functionality that isn't supported by the built-in converters.</span></span>

## <a name="how-to-read-json-into-net-objects-deserialize"></a><span data-ttu-id="0367b-152">如何将 JSON 读入 .NET 对象（反序列化）</span><span class="sxs-lookup"><span data-stu-id="0367b-152">How to read JSON into .NET objects (deserialize)</span></span>

<span data-ttu-id="0367b-153">若要从字符串或文件进行反序列化，请调用 <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="0367b-153">To deserialize from a string or a file, call the <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> method.</span></span>

<span data-ttu-id="0367b-154">下面的示例从字符串读取 JSON，并创建前面为[序列化示例](#serialization-example)显示的 `WeatherForecastWithPOCOs` 类的实例：</span><span class="sxs-lookup"><span data-stu-id="0367b-154">The following example reads JSON from a string and creates an instance of the `WeatherForecastWithPOCOs` class shown earlier for the [serialization example](#serialization-example):</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToString.cs?name=SnippetDeserialize)]

<span data-ttu-id="0367b-155">若要使用同步代码从文件进行反序列化，请将文件读入字符串中，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0367b-155">To deserialize from a file by using synchronous code, read the file into a string, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToFile.cs?name=SnippetDeserialize)]

<span data-ttu-id="0367b-156">若要使用异步代码从文件进行反序列化，请调用 <xref:System.Text.Json.JsonSerializer.DeserializeAsync%2A> 方法：</span><span class="sxs-lookup"><span data-stu-id="0367b-156">To deserialize from a file by using asynchronous code, call the <xref:System.Text.Json.JsonSerializer.DeserializeAsync%2A> method:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToFileAsync.cs?name=SnippetDeserialize)]

### <a name="deserialize-from-utf-8"></a><span data-ttu-id="0367b-157">从 UTF-8 进行反序列化</span><span class="sxs-lookup"><span data-stu-id="0367b-157">Deserialize from UTF-8</span></span>

<span data-ttu-id="0367b-158">若要从 UTF-8 进行反序列化，请调用采用 `Utf8JsonReader` 或 `ReadOnlySpan<byte>` 的 <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> 重载，如下面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="0367b-158">To deserialize from UTF-8, call a <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> overload that takes a `Utf8JsonReader` or a `ReadOnlySpan<byte>`, as shown in the following examples.</span></span> <span data-ttu-id="0367b-159">这些示例假设 JSON 处于名为 jsonUtf8Bytes 的字节数组中。</span><span class="sxs-lookup"><span data-stu-id="0367b-159">The examples assume the JSON is in a byte array named jsonUtf8Bytes.</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToUtf8.cs?name=SnippetDeserialize1)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToUtf8.cs?name=SnippetDeserialize2)]

## <a name="deserialization-behavior"></a><span data-ttu-id="0367b-160">反序列化行为</span><span class="sxs-lookup"><span data-stu-id="0367b-160">Deserialization behavior</span></span>

<span data-ttu-id="0367b-161">对 JSON 进行反序列化时，以下行为适用：</span><span class="sxs-lookup"><span data-stu-id="0367b-161">The following behaviors apply when deserializing JSON:</span></span>

* <span data-ttu-id="0367b-162">默认情况下，属性名称匹配区分大小写。</span><span class="sxs-lookup"><span data-stu-id="0367b-162">By default, property name matching is case-sensitive.</span></span> <span data-ttu-id="0367b-163">可以[指定不区分大小写](#case-insensitive-property-matching)。</span><span class="sxs-lookup"><span data-stu-id="0367b-163">You can [specify case-insensitivity](#case-insensitive-property-matching).</span></span>
* <span data-ttu-id="0367b-164">如果 JSON 包含只读属性的值，则会忽略该值，并且不引发异常。</span><span class="sxs-lookup"><span data-stu-id="0367b-164">If the JSON contains a value for a read-only property, the value is ignored and no exception is thrown.</span></span>
* <span data-ttu-id="0367b-165">用于反序列化的构造函数：</span><span class="sxs-lookup"><span data-stu-id="0367b-165">Constructors for deserialization:</span></span>
  - <span data-ttu-id="0367b-166">在 .NET Core 3.0 和 3.1 上，无参数构造函数（可以是公共的、内部的或专用的）用于反序列化。</span><span class="sxs-lookup"><span data-stu-id="0367b-166">On .NET Core 3.0 and 3.1, a parameterless constructor, which can be public, internal, or private, is used for deserialization.</span></span>
  - <span data-ttu-id="0367b-167">在 .NET 5.0 和更高版本中，序列化程序会忽略非公共构造函数。</span><span class="sxs-lookup"><span data-stu-id="0367b-167">In .NET 5.0 and later, non-public constructors are ignored by the serializer.</span></span> <span data-ttu-id="0367b-168">但是，如果无参数构造函数不可用，则可以使用参数化构造函数。</span><span class="sxs-lookup"><span data-stu-id="0367b-168">However, parameterized constructors can be used if a parameterless constructor isn't available.</span></span>
* <span data-ttu-id="0367b-169">不支持反序列化为不可变对象或只读属性。</span><span class="sxs-lookup"><span data-stu-id="0367b-169">Deserialization to immutable objects or read-only properties isn't supported.</span></span>
* <span data-ttu-id="0367b-170">默认情况下，支持将枚举作为数字。</span><span class="sxs-lookup"><span data-stu-id="0367b-170">By default, enums are supported as numbers.</span></span> <span data-ttu-id="0367b-171">可以[将枚举名称序列化为字符串](#enums-as-strings)。</span><span class="sxs-lookup"><span data-stu-id="0367b-171">You can [serialize enum names as strings](#enums-as-strings).</span></span>
* <span data-ttu-id="0367b-172">不支持字段。</span><span class="sxs-lookup"><span data-stu-id="0367b-172">Fields aren't supported.</span></span>
* <span data-ttu-id="0367b-173">默认情况下，JSON 中的注释或尾随逗号会引发异常。</span><span class="sxs-lookup"><span data-stu-id="0367b-173">By default, comments or trailing commas in the JSON throw exceptions.</span></span> <span data-ttu-id="0367b-174">可以[允许注释和尾随逗号](#allow-comments-and-trailing-commas)。</span><span class="sxs-lookup"><span data-stu-id="0367b-174">You can [allow comments and trailing commas](#allow-comments-and-trailing-commas).</span></span>
* <span data-ttu-id="0367b-175">[默认最大深度](xref:System.Text.Json.JsonReaderOptions.MaxDepth)为 64。</span><span class="sxs-lookup"><span data-stu-id="0367b-175">The [default maximum depth](xref:System.Text.Json.JsonReaderOptions.MaxDepth) is 64.</span></span>

<span data-ttu-id="0367b-176">可以[实现自定义转换器](system-text-json-converters-how-to.md)以提供内置转换器不支持的功能。</span><span class="sxs-lookup"><span data-stu-id="0367b-176">You can [implement custom converters](system-text-json-converters-how-to.md) to provide functionality that isn't supported by the built-in converters.</span></span>

## <a name="serialize-to-formatted-json"></a><span data-ttu-id="0367b-177">序列化为格式化 JSON</span><span class="sxs-lookup"><span data-stu-id="0367b-177">Serialize to formatted JSON</span></span>

<span data-ttu-id="0367b-178">若要对 JSON 输出进行优质打印，请将 <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> 设置为 `true`：</span><span class="sxs-lookup"><span data-stu-id="0367b-178">To pretty-print the JSON output, set <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> to `true`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToString.cs?name=SnippetSerializePrettyPrint)]

<span data-ttu-id="0367b-179">下面是一个要进行序列化的示例类型，以及进行了优质打印的 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0367b-179">Here's an example type to be serialized and pretty-printed JSON output:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

## <a name="customize-json-names-and-values"></a><span data-ttu-id="0367b-180">自定义 JSON 名称和值</span><span class="sxs-lookup"><span data-stu-id="0367b-180">Customize JSON names and values</span></span>

<span data-ttu-id="0367b-181">默认情况下，属性名称和字典键在 JSON 输出中保持不变，包括大小写。</span><span class="sxs-lookup"><span data-stu-id="0367b-181">By default, property names and dictionary keys are unchanged in the JSON output, including case.</span></span> <span data-ttu-id="0367b-182">枚举值表示为数字。</span><span class="sxs-lookup"><span data-stu-id="0367b-182">Enum values are represented as numbers.</span></span> <span data-ttu-id="0367b-183">本部分介绍如何：</span><span class="sxs-lookup"><span data-stu-id="0367b-183">This section explains how to:</span></span>

* [<span data-ttu-id="0367b-184">自定义单个属性名称</span><span class="sxs-lookup"><span data-stu-id="0367b-184">Customize individual property names</span></span>](#customize-individual-property-names)
* [<span data-ttu-id="0367b-185">将所有属性名称转换为 camel 大小写</span><span class="sxs-lookup"><span data-stu-id="0367b-185">Convert all property names to camel case</span></span>](#use-camel-case-for-all-json-property-names)
* [<span data-ttu-id="0367b-186">实现自定义属性命名策略</span><span class="sxs-lookup"><span data-stu-id="0367b-186">Implement a custom property naming policy</span></span>](#use-a-custom-json-property-naming-policy)
* [<span data-ttu-id="0367b-187">将字典键转换为 camel 大小写</span><span class="sxs-lookup"><span data-stu-id="0367b-187">Convert dictionary keys to camel case</span></span>](#camel-case-dictionary-keys)
* [<span data-ttu-id="0367b-188">将枚举转换为字符串和 camel 大小写</span><span class="sxs-lookup"><span data-stu-id="0367b-188">Convert enums to strings and camel case</span></span>](#enums-as-strings)

<span data-ttu-id="0367b-189">对于需要对 JSON 属性名称和值进行特殊处理的其他方案，可以[实现自定义转换器](system-text-json-converters-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="0367b-189">For other scenarios that require special handling of JSON property names and values, you can [implement custom converters](system-text-json-converters-how-to.md).</span></span>

### <a name="customize-individual-property-names"></a><span data-ttu-id="0367b-190">自定义单个属性名称</span><span class="sxs-lookup"><span data-stu-id="0367b-190">Customize individual property names</span></span>

<span data-ttu-id="0367b-191">若要设置单个属性的名称，请使用 [[JsonPropertyName]](xref:System.Text.Json.Serialization.JsonPropertyNameAttribute) 特性。</span><span class="sxs-lookup"><span data-stu-id="0367b-191">To set the name of individual properties, use the [[JsonPropertyName]](xref:System.Text.Json.Serialization.JsonPropertyNameAttribute) attribute.</span></span>

<span data-ttu-id="0367b-192">下面是要进行序列化的示例类型和生成的 JSON：</span><span class="sxs-lookup"><span data-stu-id="0367b-192">Here's an example type to serialize and resulting JSON:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithPropertyNameAttribute)]

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "Wind": 35
}
```

<span data-ttu-id="0367b-193">此特性设置的属性名称：</span><span class="sxs-lookup"><span data-stu-id="0367b-193">The property name set by this attribute:</span></span>

* <span data-ttu-id="0367b-194">同时适用于两个方向（序列化和反序列化）。</span><span class="sxs-lookup"><span data-stu-id="0367b-194">Applies in both directions, for serialization and deserialization.</span></span>
* <span data-ttu-id="0367b-195">优先于属性命名策略。</span><span class="sxs-lookup"><span data-stu-id="0367b-195">Takes precedence over property naming policies.</span></span>

### <a name="use-camel-case-for-all-json-property-names"></a><span data-ttu-id="0367b-196">对所有 JSON 属性名称使用 camel 大小写</span><span class="sxs-lookup"><span data-stu-id="0367b-196">Use camel case for all JSON property names</span></span>

<span data-ttu-id="0367b-197">若要对所有 JSON 属性名称使用 camel 大小写，请将 <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> 设置为 `JsonNamingPolicy.CamelCase`，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0367b-197">To use camel case for all JSON property names, set <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> to `JsonNamingPolicy.CamelCase`, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundTripCamelCasePropertyNames.cs?name=Serialize)]

<span data-ttu-id="0367b-198">下面是要进行序列化的示例类和 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0367b-198">Here's an example class to serialize and JSON output:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithPropertyNameAttribute)]

```json
{
  "date": "2019-08-01T00:00:00-07:00",
  "temperatureCelsius": 25,
  "summary": "Hot",
  "Wind": 35
}
```

<span data-ttu-id="0367b-199">camel 大小写属性命名策略：</span><span class="sxs-lookup"><span data-stu-id="0367b-199">The camel case property naming policy:</span></span>

* <span data-ttu-id="0367b-200">适用于序列化和反序列化。</span><span class="sxs-lookup"><span data-stu-id="0367b-200">Applies to serialization and deserialization.</span></span>
* <span data-ttu-id="0367b-201">由 `[JsonPropertyName]` 特性替代。</span><span class="sxs-lookup"><span data-stu-id="0367b-201">Is overridden by `[JsonPropertyName]` attributes.</span></span> <span data-ttu-id="0367b-202">这便是示例中的 JSON 属性名称 `Wind` 不是 camel 大小写的原因。</span><span class="sxs-lookup"><span data-stu-id="0367b-202">This is why the JSON property name `Wind` in the example is not camel case.</span></span>

### <a name="use-a-custom-json-property-naming-policy"></a><span data-ttu-id="0367b-203">使用自定义 JSON 属性命名策略</span><span class="sxs-lookup"><span data-stu-id="0367b-203">Use a custom JSON property naming policy</span></span>

<span data-ttu-id="0367b-204">若要使用自定义 JSON 属性命名策略，请创建派生自 <xref:System.Text.Json.JsonNamingPolicy> 的类，并替代 <xref:System.Text.Json.JsonNamingPolicy.ConvertName%2A> 方法，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0367b-204">To use a custom JSON property naming policy, create a class that derives from <xref:System.Text.Json.JsonNamingPolicy> and override the <xref:System.Text.Json.JsonNamingPolicy.ConvertName%2A> method, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/UpperCaseNamingPolicy.cs)]

<span data-ttu-id="0367b-205">然后，将 <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> 属性设置为命名策略类的实例：</span><span class="sxs-lookup"><span data-stu-id="0367b-205">Then set the <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> property to an instance of your naming policy class:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripPropertyNamingPolicy.cs?name=SnippetSerialize)]

<span data-ttu-id="0367b-206">下面是要进行序列化的示例类和 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0367b-206">Here's an example class to serialize and JSON output:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithPropertyNameAttribute)]

```json
{
  "DATE": "2019-08-01T00:00:00-07:00",
  "TEMPERATURECELSIUS": 25,
  "SUMMARY": "Hot",
  "Wind": 35
}
```

<span data-ttu-id="0367b-207">JSON 属性命名策略：</span><span class="sxs-lookup"><span data-stu-id="0367b-207">The JSON property naming policy:</span></span>

* <span data-ttu-id="0367b-208">适用于序列化和反序列化。</span><span class="sxs-lookup"><span data-stu-id="0367b-208">Applies to serialization and deserialization.</span></span>
* <span data-ttu-id="0367b-209">由 `[JsonPropertyName]` 特性替代。</span><span class="sxs-lookup"><span data-stu-id="0367b-209">Is overridden by `[JsonPropertyName]` attributes.</span></span> <span data-ttu-id="0367b-210">这便是示例中的 JSON 属性名称 `Wind` 不是大写的原因。</span><span class="sxs-lookup"><span data-stu-id="0367b-210">This is why the JSON property name `Wind` in the example is not upper case.</span></span>

### <a name="camel-case-dictionary-keys"></a><span data-ttu-id="0367b-211">Camel 大小写字典键</span><span class="sxs-lookup"><span data-stu-id="0367b-211">Camel case dictionary keys</span></span>

<span data-ttu-id="0367b-212">如果要序列化的对象的属性为 `Dictionary<string,TValue>` 类型，则 `string` 键可转换为 camel 大小写。</span><span class="sxs-lookup"><span data-stu-id="0367b-212">If a property of an object to be serialized is of type `Dictionary<string,TValue>`, the `string` keys can be converted to camel case.</span></span> <span data-ttu-id="0367b-213">为此，请将 <xref:System.Text.Json.JsonSerializerOptions.DictionaryKeyPolicy> 设置为 `JsonNamingPolicy.CamelCase`，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0367b-213">To do that, set <xref:System.Text.Json.JsonSerializerOptions.DictionaryKeyPolicy> to `JsonNamingPolicy.CamelCase`, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeCamelCaseDictionaryKeys.cs?name=SnippetSerialize)]

<span data-ttu-id="0367b-214">使用名为 `TemperatureRanges` 且具有键值对 `"ColdMinTemp", 20` 和 `"HotMinTemp", 40` 的字典序列化对象会产生类似于以下示例的 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0367b-214">Serializing an object with a dictionary named `TemperatureRanges` that has key-value pairs `"ColdMinTemp", 20` and `"HotMinTemp", 40` would result in JSON output like the following example:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "TemperatureRanges": {
    "coldMinTemp": 20,
    "hotMinTemp": 40
  }
}
```

<span data-ttu-id="0367b-215">字典键的 camel 大小写命名策略仅适用于序列化。</span><span class="sxs-lookup"><span data-stu-id="0367b-215">The camel case naming policy for dictionary keys applies to serialization only.</span></span> <span data-ttu-id="0367b-216">如果对字典进行反序列化，即使为 `DictionaryKeyPolicy`指定 `JsonNamingPolicy.CamelCase`，键也会与 JSON 文件匹配。</span><span class="sxs-lookup"><span data-stu-id="0367b-216">If you deserialize a dictionary, the keys will match the JSON file even if you specify `JsonNamingPolicy.CamelCase` for the `DictionaryKeyPolicy`.</span></span>

### <a name="enums-as-strings"></a><span data-ttu-id="0367b-217">作为字符串的枚举</span><span class="sxs-lookup"><span data-stu-id="0367b-217">Enums as strings</span></span>

<span data-ttu-id="0367b-218">默认情况下，枚举会序列化为数字。</span><span class="sxs-lookup"><span data-stu-id="0367b-218">By default, enums are serialized as numbers.</span></span> <span data-ttu-id="0367b-219">若要将枚举名称序列化为字符串，请使用 <xref:System.Text.Json.Serialization.JsonStringEnumConverter>。</span><span class="sxs-lookup"><span data-stu-id="0367b-219">To serialize enum names as strings, use the <xref:System.Text.Json.Serialization.JsonStringEnumConverter>.</span></span>

<span data-ttu-id="0367b-220">例如，假设需要序列化以下具有枚举的类：</span><span class="sxs-lookup"><span data-stu-id="0367b-220">For example, suppose you need to serialize the following class that has an enum:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithEnum)]

<span data-ttu-id="0367b-221">如果 Summary 为 `Hot`，则默认情况下序列化的 JSON 具有数值 3：</span><span class="sxs-lookup"><span data-stu-id="0367b-221">If the Summary is `Hot`, by default the serialized JSON has the numeric value 3:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": 3
}
```

<span data-ttu-id="0367b-222">下面的示例代码序列化枚举名称(而不是数值)，并将名称转换为 camel 大小写：</span><span class="sxs-lookup"><span data-stu-id="0367b-222">The following sample code serializes the enum names instead of the numeric values, and converts the names to camel case:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripEnumAsString.cs?name=SnippetSerialize)]

<span data-ttu-id="0367b-223">生成的 JSON 类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="0367b-223">The resulting JSON looks like the following example:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "hot"
}
```

<span data-ttu-id="0367b-224">还可以反序列化枚举字符串名称，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0367b-224">Enum string names can be deserialized as well, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripEnumAsString.cs?name=SnippetDeserialize)]

## <a name="exclude-properties-from-serialization"></a><span data-ttu-id="0367b-225">从序列化中排除属性</span><span class="sxs-lookup"><span data-stu-id="0367b-225">Exclude properties from serialization</span></span>

<span data-ttu-id="0367b-226">默认情况下，所有公共属性都会序列化。</span><span class="sxs-lookup"><span data-stu-id="0367b-226">By default, all public properties are serialized.</span></span> <span data-ttu-id="0367b-227">如果不想让某些属性出现在 JSON 输出中，则有几个选项可用。</span><span class="sxs-lookup"><span data-stu-id="0367b-227">If you don't want some of them to appear in the JSON output, you have several options.</span></span> <span data-ttu-id="0367b-228">本部分介绍如何排除：</span><span class="sxs-lookup"><span data-stu-id="0367b-228">This section explains how to exclude:</span></span>

* [<span data-ttu-id="0367b-229">单个属性</span><span class="sxs-lookup"><span data-stu-id="0367b-229">Individual properties</span></span>](#exclude-individual-properties)
* [<span data-ttu-id="0367b-230">所有只读属性</span><span class="sxs-lookup"><span data-stu-id="0367b-230">All read-only properties</span></span>](#exclude-all-read-only-properties)
* [<span data-ttu-id="0367b-231">所有 null 值属性</span><span class="sxs-lookup"><span data-stu-id="0367b-231">All null-value properties</span></span>](#exclude-all-null-value-properties)

### <a name="exclude-individual-properties"></a><span data-ttu-id="0367b-232">排除单个属性</span><span class="sxs-lookup"><span data-stu-id="0367b-232">Exclude individual properties</span></span>

<span data-ttu-id="0367b-233">若要忽略单个属性，请使用 [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) 特性。</span><span class="sxs-lookup"><span data-stu-id="0367b-233">To ignore individual properties, use the [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) attribute.</span></span>

<span data-ttu-id="0367b-234">下面是要进行序列化的示例类型和 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0367b-234">Here's an example type to serialize and JSON output:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithIgnoreAttribute)]

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
}
```

### <a name="exclude-all-read-only-properties"></a><span data-ttu-id="0367b-235">排除所有只读属性</span><span class="sxs-lookup"><span data-stu-id="0367b-235">Exclude all read-only properties</span></span>

<span data-ttu-id="0367b-236">如果属性包含公共 getter 而不是公共 setter，则属性为只读。</span><span class="sxs-lookup"><span data-stu-id="0367b-236">A property is read-only if it contains a public getter but not a public setter.</span></span> <span data-ttu-id="0367b-237">若要排除所有只读属性，请将 <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyProperties?displayProperty=nameWithType> 设置为 `true`，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0367b-237">To exclude all read-only properties, set the <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyProperties?displayProperty=nameWithType> to `true`, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeExcludeReadOnlyProperties.cs?name=SnippetSerialize)]

<span data-ttu-id="0367b-238">下面是要进行序列化的示例类型和 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0367b-238">Here's an example type to serialize and JSON output:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithROProperty)]

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
}
```

<span data-ttu-id="0367b-239">此选项仅适用于序列化。</span><span class="sxs-lookup"><span data-stu-id="0367b-239">This option applies only to serialization.</span></span> <span data-ttu-id="0367b-240">在反序列化过程中，默认情况下会忽略只读属性。</span><span class="sxs-lookup"><span data-stu-id="0367b-240">During deserialization, read-only properties are ignored by default.</span></span>

### <a name="exclude-all-null-value-properties"></a><span data-ttu-id="0367b-241">排除所有 null 值属性</span><span class="sxs-lookup"><span data-stu-id="0367b-241">Exclude all null value properties</span></span>

<span data-ttu-id="0367b-242">若要排除所有 null 值属性，请将 <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues> 属性设置为 `true`，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0367b-242">To exclude all null value properties, set the <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues> property to `true`, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeExcludeNullValueProperties.cs?name=SnippetSerialize)]

<span data-ttu-id="0367b-243">下面是要进行序列化的示例对象和 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0367b-243">Here's an example object to serialize and JSON output:</span></span>

|<span data-ttu-id="0367b-244">Property</span><span class="sxs-lookup"><span data-stu-id="0367b-244">Property</span></span> |<span data-ttu-id="0367b-245">“值”</span><span class="sxs-lookup"><span data-stu-id="0367b-245">Value</span></span>  |
|---------|---------|
| <span data-ttu-id="0367b-246">日期</span><span class="sxs-lookup"><span data-stu-id="0367b-246">Date</span></span>    | <span data-ttu-id="0367b-247">8/1/2019 12:00:00 AM -07:00</span><span class="sxs-lookup"><span data-stu-id="0367b-247">8/1/2019 12:00:00 AM -07:00</span></span>|
| <span data-ttu-id="0367b-248">TemperatureCelsius</span><span class="sxs-lookup"><span data-stu-id="0367b-248">TemperatureCelsius</span></span>| <span data-ttu-id="0367b-249">25</span><span class="sxs-lookup"><span data-stu-id="0367b-249">25</span></span> |
| <span data-ttu-id="0367b-250">总结</span><span class="sxs-lookup"><span data-stu-id="0367b-250">Summary</span></span>| <span data-ttu-id="0367b-251">null</span><span class="sxs-lookup"><span data-stu-id="0367b-251">null</span></span>|

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25
}
```

<span data-ttu-id="0367b-252">此设置适用于序列化和反序列化。</span><span class="sxs-lookup"><span data-stu-id="0367b-252">This setting applies to serialization and deserialization.</span></span> <span data-ttu-id="0367b-253">有关对反序列化的影响的信息，请参阅[在反序列化时忽略 null](#ignore-null-when-deserializing)。</span><span class="sxs-lookup"><span data-stu-id="0367b-253">For information about its effect on deserialization, see [Ignore null when deserializing](#ignore-null-when-deserializing).</span></span>

## <a name="customize-character-encoding"></a><span data-ttu-id="0367b-254">自定义字符编码</span><span class="sxs-lookup"><span data-stu-id="0367b-254">Customize character encoding</span></span>

<span data-ttu-id="0367b-255">默认情况下，序列化程序会转义所有非 ASCII 字符。</span><span class="sxs-lookup"><span data-stu-id="0367b-255">By default, the serializer escapes all non-ASCII characters.</span></span>  <span data-ttu-id="0367b-256">即，会将它们替换为 `\uxxxx`，其中 `xxxx` 为字符的 Unicode 代码。</span><span class="sxs-lookup"><span data-stu-id="0367b-256">That is, it replaces them with `\uxxxx` where `xxxx` is the Unicode code of the character.</span></span>  <span data-ttu-id="0367b-257">例如，如果 `Summary` 属性设置为西里尔文 жарко，则 `WeatherForecast` 对象会进行序列化，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0367b-257">For example, if the `Summary` property is set to Cyrillic жарко, the `WeatherForecast` object is serialized as shown in this example:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "\u0436\u0430\u0440\u043A\u043E"
}
```

### <a name="serialize-language-character-sets"></a><span data-ttu-id="0367b-258">序列化语言字符集</span><span class="sxs-lookup"><span data-stu-id="0367b-258">Serialize language character sets</span></span>

<span data-ttu-id="0367b-259">若要序列化一种或多种语言的字符集而不进行转义，请在创建 <xref:System.Text.Encodings.Web.JavaScriptEncoder?displayProperty=fullName> 的实例时指定 [Unicode 范围](xref:System.Text.Unicode.UnicodeRanges)，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0367b-259">To serialize the character set(s) of one or more languages without escaping, specify [Unicode range(s)](xref:System.Text.Unicode.UnicodeRanges) when creating an instance of <xref:System.Text.Encodings.Web.JavaScriptEncoder?displayProperty=fullName>, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs?name=SnippetUsings)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs?name=SnippetLanguageSets)]

<span data-ttu-id="0367b-260">此代码不转义西里尔文或希腊语字符。</span><span class="sxs-lookup"><span data-stu-id="0367b-260">This code doesn't escape Cyrillic or Greek characters.</span></span> <span data-ttu-id="0367b-261">如果 `Summary` 属性设置为西里尔文 жарко，则 `WeatherForecast` 对象会进行序列化，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0367b-261">If the `Summary` property is set to Cyrillic жарко, the `WeatherForecast` object is serialized as shown in this example:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "жарко"
}
```

<span data-ttu-id="0367b-262">若要序列化所有语言集而不进行转义，请使用 <xref:System.Text.Unicode.UnicodeRanges.All?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="0367b-262">To serialize all language sets without escaping, use <xref:System.Text.Unicode.UnicodeRanges.All?displayProperty=nameWithType>.</span></span>

### <a name="serialize-specific-characters"></a><span data-ttu-id="0367b-263">序列化特定字符</span><span class="sxs-lookup"><span data-stu-id="0367b-263">Serialize specific characters</span></span>

<span data-ttu-id="0367b-264">一种替代方法是指定要允许的单个字符，而不进行转义。</span><span class="sxs-lookup"><span data-stu-id="0367b-264">An alternative is to specify individual characters that you want to allow through without being escaped.</span></span> <span data-ttu-id="0367b-265">下面的示例仅序列化 жарко 的前两个字符：</span><span class="sxs-lookup"><span data-stu-id="0367b-265">The following example serializes only the first two characters of жарко:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs?name=SnippetUsings)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs?name=SnippetSelectedCharacters)]

<span data-ttu-id="0367b-266">下面是前面代码生成的 JSON 的示例：</span><span class="sxs-lookup"><span data-stu-id="0367b-266">Here's an example of JSON produced by the preceding code:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "жа\u0440\u043A\u043E"
}
```

### <a name="serialize-all-characters"></a><span data-ttu-id="0367b-267">序列化所有字符</span><span class="sxs-lookup"><span data-stu-id="0367b-267">Serialize all characters</span></span>

<span data-ttu-id="0367b-268">若要最大程度地减少转义，可以使用 <xref:System.Text.Encodings.Web.JavaScriptEncoder.UnsafeRelaxedJsonEscaping?displayProperty=nameWithType>，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0367b-268">To minimize escaping you can use <xref:System.Text.Encodings.Web.JavaScriptEncoder.UnsafeRelaxedJsonEscaping?displayProperty=nameWithType>, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs?name=SnippetUsings)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs?name=SnippetUnsafeRelaxed)]

> [!CAUTION]
> <span data-ttu-id="0367b-269">与默认编码器相比，`UnsafeRelaxedJsonEscaping` 编码器在允许字符通过而不进行转义方面更加宽松：</span><span class="sxs-lookup"><span data-stu-id="0367b-269">Compared to the default encoder, the `UnsafeRelaxedJsonEscaping` encoder is more permissive about allowing characters to pass through unescaped:</span></span>
>
> * <span data-ttu-id="0367b-270">它不转义 HTML 敏感字符，如 `<`、`>`、`&` 和 `'`。</span><span class="sxs-lookup"><span data-stu-id="0367b-270">It doesn't escape HTML-sensitive characters such as `<`, `>`, `&`, and `'`.</span></span>
> * <span data-ttu-id="0367b-271">它不提供任何针对 XSS 或信息泄露攻击（如客户端和服务器在字符集方面不一致所可能导致的攻击）的额外深度防御保护。</span><span class="sxs-lookup"><span data-stu-id="0367b-271">It doesn't offer any additional defense-in-depth protections against XSS or information disclosure attacks, such as those which might result from the client and server disagreeing on the *charset*.</span></span>
>
> <span data-ttu-id="0367b-272">仅当知道客户端将生成的有效负载解释为 UTF-8 编码的 JSON 时，才使用不安全编码器。</span><span class="sxs-lookup"><span data-stu-id="0367b-272">Use the unsafe encoder only when it's known that the client will be interpreting the resulting payload as UTF-8 encoded JSON.</span></span> <span data-ttu-id="0367b-273">例如，如果服务器在发送响应标头 `Content-Type: application/json; charset=utf-8`，则可以使用它。</span><span class="sxs-lookup"><span data-stu-id="0367b-273">For example, you can use it if the server is sending the response header `Content-Type: application/json; charset=utf-8`.</span></span> <span data-ttu-id="0367b-274">永远不允许将原始 `UnsafeRelaxedJsonEscaping` 输出发出到 HTML 页面或 `<script>` 元素。</span><span class="sxs-lookup"><span data-stu-id="0367b-274">Never allow the raw `UnsafeRelaxedJsonEscaping` output to be emitted into an HTML page or a `<script>` element.</span></span>

## <a name="serialize-properties-of-derived-classes"></a><span data-ttu-id="0367b-275">序列化派生类的属性</span><span class="sxs-lookup"><span data-stu-id="0367b-275">Serialize properties of derived classes</span></span>

<span data-ttu-id="0367b-276">不支持多态类型层次结构的序列化。</span><span class="sxs-lookup"><span data-stu-id="0367b-276">Serialization of a polymorphic type hierarchy is not supported.</span></span> <span data-ttu-id="0367b-277">例如，如果属性定义为接口或抽象类，则即使运行时类型具有其他属性，也只会序列化对接口或抽象类定义的属性。</span><span class="sxs-lookup"><span data-stu-id="0367b-277">For example, if a property is defined as an interface or an abstract class, only the properties defined on the interface or abstract class are serialized, even if the runtime type has additional properties.</span></span> <span data-ttu-id="0367b-278">此部分中介绍了此行为的例外情况。</span><span class="sxs-lookup"><span data-stu-id="0367b-278">The exceptions to this behavior are explained in this section.</span></span>

<span data-ttu-id="0367b-279">例如，假设有一个 `WeatherForecast` 类和一个派生类 `WeatherForecastDerived`：</span><span class="sxs-lookup"><span data-stu-id="0367b-279">For example, suppose you have a `WeatherForecast` class and a derived class `WeatherForecastDerived`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFDerived)]

<span data-ttu-id="0367b-280">并且假设 `Serialize` 方法的类型参数在编译时为 `WeatherForecast`：</span><span class="sxs-lookup"><span data-stu-id="0367b-280">And suppose the type argument of the `Serialize` method at compile time is `WeatherForecast`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs?name=SnippetSerializeDefault)]

<span data-ttu-id="0367b-281">在这种情况下，即使 `weatherForecast` 对象实际上是 `WeatherForecastDerived` 对象，也不会序列化 `WindSpeed` 属性。</span><span class="sxs-lookup"><span data-stu-id="0367b-281">In this scenario, the `WindSpeed` property is not serialized even if the `weatherForecast` object is actually a `WeatherForecastDerived` object.</span></span> <span data-ttu-id="0367b-282">仅序列化基类属性：</span><span class="sxs-lookup"><span data-stu-id="0367b-282">Only the base class properties are serialized:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

<span data-ttu-id="0367b-283">此行为旨在帮助防止在运行时创建的派生类型中发生意外数据泄露。</span><span class="sxs-lookup"><span data-stu-id="0367b-283">This behavior is intended to help prevent accidental exposure of data in a derived runtime-created type.</span></span>

<span data-ttu-id="0367b-284">若要序列化前面示例中派生类型的属性，请使用以下方法之一：</span><span class="sxs-lookup"><span data-stu-id="0367b-284">To serialize the properties of the derived type in the preceding example, use one of the following approaches:</span></span>

* <span data-ttu-id="0367b-285">调用 <xref:System.Text.Json.JsonSerializer.Serialize%2A> 的重载，以便在运行时指定类型：</span><span class="sxs-lookup"><span data-stu-id="0367b-285">Call an overload of <xref:System.Text.Json.JsonSerializer.Serialize%2A> that lets you specify the type at run time:</span></span>

  [!code-csharp[](snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs?name=SnippetSerializeGetType)]

* <span data-ttu-id="0367b-286">将要序列化的对象声明为 `object`。</span><span class="sxs-lookup"><span data-stu-id="0367b-286">Declare the object to be serialized as `object`.</span></span>

  [!code-csharp[](snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs?name=SnippetSerializeObject)]

<span data-ttu-id="0367b-287">在前面的示例方案中，这两种方法都会使 `WindSpeed` 属性包含在 JSON 输出中：</span><span class="sxs-lookup"><span data-stu-id="0367b-287">In the preceding example scenario, both approaches cause the `WindSpeed` property to be included in the JSON output:</span></span>

```json
{
  "WindSpeed": 35,
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

> [!IMPORTANT]
> <span data-ttu-id="0367b-288">这些方法只为要序列化的根对象提供多态序列化，而不为该根对象的属性提供。</span><span class="sxs-lookup"><span data-stu-id="0367b-288">These approaches provide polymorphic serialization only for the root object to be serialized, not for properties of that root object.</span></span>

<span data-ttu-id="0367b-289">如果将较低级别的对象定义为类型 `object`，则可以对它们进行多态序列化。</span><span class="sxs-lookup"><span data-stu-id="0367b-289">You can get polymorphic serialization for lower-level objects if you define them as type `object`.</span></span> <span data-ttu-id="0367b-290">例如，假设 `WeatherForecast` 类具有一个名为 `PreviousForecast` 的属性，该属性可以定义为类型 `WeatherForecast` 或 `object`：</span><span class="sxs-lookup"><span data-stu-id="0367b-290">For example, suppose your `WeatherForecast` class has a property named `PreviousForecast` that can be defined as type `WeatherForecast` or `object`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithPrevious)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithPreviousAsObject)]

<span data-ttu-id="0367b-291">如果 `PreviousForecast` 属性包含 `WeatherForecastDerived` 的实例：</span><span class="sxs-lookup"><span data-stu-id="0367b-291">If the `PreviousForecast` property contains an instance of `WeatherForecastDerived`:</span></span>

* <span data-ttu-id="0367b-292">序列化 `WeatherForecastWithPrevious` 的 JSON 输出不包含 `WindSpeed`。</span><span class="sxs-lookup"><span data-stu-id="0367b-292">The JSON output from serializing `WeatherForecastWithPrevious` **doesn't include** `WindSpeed`.</span></span>
* <span data-ttu-id="0367b-293">序列化 `WeatherForecastWithPreviousAsObject` 的 JSON 输出包含 `WindSpeed`。</span><span class="sxs-lookup"><span data-stu-id="0367b-293">The JSON output from serializing `WeatherForecastWithPreviousAsObject` **includes** `WindSpeed`.</span></span>

<span data-ttu-id="0367b-294">若要序列化 `WeatherForecastWithPreviousAsObject`，无需调用 `Serialize<object>` 或 `GetType`，因为根对象不是可能属于派生类型的对象。</span><span class="sxs-lookup"><span data-stu-id="0367b-294">To serialize `WeatherForecastWithPreviousAsObject`, it isn't necessary to call `Serialize<object>` or `GetType` because the root object isn't the one that may be of a derived type.</span></span> <span data-ttu-id="0367b-295">下面的代码示例不调用 `Serialize<object>` 或 `GetType`：</span><span class="sxs-lookup"><span data-stu-id="0367b-295">The following code example doesn't call `Serialize<object>` or `GetType`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs?name=SnippetSerializeSecondLevel)]

<span data-ttu-id="0367b-296">前面的代码会正确地序列化 `WeatherForecastWithPreviousAsObject`：</span><span class="sxs-lookup"><span data-stu-id="0367b-296">The preceding code correctly serializes `WeatherForecastWithPreviousAsObject`:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "PreviousForecast": {
    "WindSpeed": 35,
    "Date": "2019-08-01T00:00:00-07:00",
    "TemperatureCelsius": 25,
    "Summary": "Hot"
  }
}
```

<span data-ttu-id="0367b-297">将属性定义为 `object` 的相同方法适用于接口。</span><span class="sxs-lookup"><span data-stu-id="0367b-297">The same approach of defining properties as `object` works with interfaces.</span></span> <span data-ttu-id="0367b-298">假设具有以下接口和实现，并且要使用包含实现实例的属性序列化类：</span><span class="sxs-lookup"><span data-stu-id="0367b-298">Suppose you have the following interface and implementation, and you want to serialize a class with properties that contain implementation instances:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/IForecast.cs)]

<span data-ttu-id="0367b-299">序列化 `Forecasts` 的实例时，只有 `Tuesday` 显示 `WindSpeed` 属性，因为 `Tuesday` 定义为 `object`：</span><span class="sxs-lookup"><span data-stu-id="0367b-299">When you serialize an instance of `Forecasts`, only `Tuesday` shows the `WindSpeed` property, because `Tuesday` is defined as `object`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs?name=SnippetSerializeInterface)]

<span data-ttu-id="0367b-300">下面的示例显示前面代码生成的 JSON：</span><span class="sxs-lookup"><span data-stu-id="0367b-300">The following example shows the JSON that results from the preceding code:</span></span>

```json
{
  "Monday": {
    "Date": "2020-01-06T00:00:00-08:00",
    "TemperatureCelsius": 10,
    "Summary": "Cool"
  },
  "Tuesday": {
    "Date": "2020-01-07T00:00:00-08:00",
    "TemperatureCelsius": 11,
    "Summary": "Rainy",
    "WindSpeed": 10
  }
}
```

<span data-ttu-id="0367b-301">有关多态序列化的详细信息，以及有关反序列化的信息，请参阅[如何从 Newtonsoft.Json 迁移到 System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md#polymorphic-serialization)。</span><span class="sxs-lookup"><span data-stu-id="0367b-301">For more information about polymorphic **serialization**, and for information about **deserialization**, see [How to migrate from Newtonsoft.Json to System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md#polymorphic-serialization).</span></span>

## <a name="allow-comments-and-trailing-commas"></a><span data-ttu-id="0367b-302">允许注释和尾随逗号</span><span class="sxs-lookup"><span data-stu-id="0367b-302">Allow comments and trailing commas</span></span>

<span data-ttu-id="0367b-303">默认情况下，JSON 中不允许使用注释和尾随逗号。</span><span class="sxs-lookup"><span data-stu-id="0367b-303">By default, comments and trailing commas are not allowed in JSON.</span></span> <span data-ttu-id="0367b-304">若要在 JSON 中允许注释，请将 <xref:System.Text.Json.JsonSerializerOptions.ReadCommentHandling?displayProperty=nameWithType> 属性设置为 `JsonCommentHandling.Skip`。</span><span class="sxs-lookup"><span data-stu-id="0367b-304">To allow comments in the JSON, set the <xref:System.Text.Json.JsonSerializerOptions.ReadCommentHandling?displayProperty=nameWithType> property to `JsonCommentHandling.Skip`.</span></span>
<span data-ttu-id="0367b-305">若要允许尾随逗号，请将 <xref:System.Text.Json.JsonSerializerOptions.AllowTrailingCommas?displayProperty=nameWithType> 属性设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="0367b-305">And to allow trailing commas, set the <xref:System.Text.Json.JsonSerializerOptions.AllowTrailingCommas?displayProperty=nameWithType> property to `true`.</span></span> <span data-ttu-id="0367b-306">下面的示例演示如何允许这两者：</span><span class="sxs-lookup"><span data-stu-id="0367b-306">The following example shows how to allow both:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/DeserializeCommasComments.cs?name=SnippetDeserialize)]

<span data-ttu-id="0367b-307">下面是包含注释和尾随逗号的示例 JSON：</span><span class="sxs-lookup"><span data-stu-id="0367b-307">Here's example JSON with comments and a trailing comma:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25, // Fahrenheit 77
  "Summary": "Hot", /* Zharko */
}
```

## <a name="case-insensitive-property-matching"></a><span data-ttu-id="0367b-308">不区分大小写的属性匹配</span><span class="sxs-lookup"><span data-stu-id="0367b-308">Case-insensitive property matching</span></span>

<span data-ttu-id="0367b-309">默认情况下，反序列化会查找 JSON 与目标对象属性之间区分大小写的属性名称匹配。</span><span class="sxs-lookup"><span data-stu-id="0367b-309">By default, deserialization looks for case-sensitive property name matches between JSON and the target object properties.</span></span> <span data-ttu-id="0367b-310">若要更改该行为，请将 <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive?displayProperty=nameWithType> 设置为 `true`：</span><span class="sxs-lookup"><span data-stu-id="0367b-310">To change that behavior, set <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive?displayProperty=nameWithType> to `true`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/DeserializeCaseInsensitive.cs?name=SnippetDeserialize)]

<span data-ttu-id="0367b-311">下面是具有 camel 大小写属性名称的示例 JSON。</span><span class="sxs-lookup"><span data-stu-id="0367b-311">Here's example JSON with camel case property names.</span></span> <span data-ttu-id="0367b-312">它可以反序列化为具有帕斯卡拼写法属性名称的以下类型。</span><span class="sxs-lookup"><span data-stu-id="0367b-312">It can be deserialized into the following type that has Pascal case property names.</span></span>

```json
{
  "date": "2019-08-01T00:00:00-07:00",
  "temperatureCelsius": 25,
  "summary": "Hot",
}
```

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

## <a name="handle-overflow-json"></a><span data-ttu-id="0367b-313">处理溢出 JSON</span><span class="sxs-lookup"><span data-stu-id="0367b-313">Handle overflow JSON</span></span>

<span data-ttu-id="0367b-314">反序列化时，可能会在 JSON 中收到不是由目标类型的属性表示的数据。</span><span class="sxs-lookup"><span data-stu-id="0367b-314">While deserializing, you might receive data in the JSON that is not represented by properties of the target type.</span></span> <span data-ttu-id="0367b-315">例如，假设目标类型如下：</span><span class="sxs-lookup"><span data-stu-id="0367b-315">For example, suppose your target type is this:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

<span data-ttu-id="0367b-316">要反序列化的 JSON 如下：</span><span class="sxs-lookup"><span data-stu-id="0367b-316">And the JSON to be deserialized is this:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "temperatureCelsius": 25,
  "Summary": "Hot",
  "DatesAvailable": [
    "2019-08-01T00:00:00-07:00",
    "2019-08-02T00:00:00-07:00"
  ],
  "SummaryWords": [
    "Cool",
    "Windy",
    "Humid"
  ]
}
```

<span data-ttu-id="0367b-317">如果将显示的 JSON 反序列化为显示的类型，则 `DatesAvailable` 和 `SummaryWords` 属性无处可去，会丢失。</span><span class="sxs-lookup"><span data-stu-id="0367b-317">If you deserialize the JSON shown into the type shown, the `DatesAvailable` and `SummaryWords` properties have nowhere to go and are lost.</span></span> <span data-ttu-id="0367b-318">若要捕获额外数据（如这些属性），请将 [JsonExtensionData](xref:System.Text.Json.Serialization.JsonExtensionDataAttribute) 特性应用于类型 `Dictionary<string,object>` 或 `Dictionary<string,JsonElement>` 的属性：</span><span class="sxs-lookup"><span data-stu-id="0367b-318">To capture extra data such as these properties, apply the [JsonExtensionData](xref:System.Text.Json.Serialization.JsonExtensionDataAttribute) attribute to a property of type `Dictionary<string,object>` or `Dictionary<string,JsonElement>`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithExtensionData)]

<span data-ttu-id="0367b-319">将前面显示的 JSON 反序列化为此示例类型时，额外数据会成为 `ExtensionData` 属性的键值对：</span><span class="sxs-lookup"><span data-stu-id="0367b-319">When you deserialize the JSON shown earlier into this sample type, the extra data becomes key-value pairs of the `ExtensionData` property:</span></span>

|<span data-ttu-id="0367b-320">Property</span><span class="sxs-lookup"><span data-stu-id="0367b-320">Property</span></span> |<span data-ttu-id="0367b-321">“值”</span><span class="sxs-lookup"><span data-stu-id="0367b-321">Value</span></span>  |<span data-ttu-id="0367b-322">说明</span><span class="sxs-lookup"><span data-stu-id="0367b-322">Notes</span></span>  |
|---------|---------|---------|
| <span data-ttu-id="0367b-323">日期</span><span class="sxs-lookup"><span data-stu-id="0367b-323">Date</span></span>    | <span data-ttu-id="0367b-324">8/1/2019 12:00:00 AM -07:00</span><span class="sxs-lookup"><span data-stu-id="0367b-324">8/1/2019 12:00:00 AM -07:00</span></span>||
| <span data-ttu-id="0367b-325">TemperatureCelsius</span><span class="sxs-lookup"><span data-stu-id="0367b-325">TemperatureCelsius</span></span>| <span data-ttu-id="0367b-326">0</span><span class="sxs-lookup"><span data-stu-id="0367b-326">0</span></span> | <span data-ttu-id="0367b-327">区分大小写的不匹配（JSON 中的 `temperatureCelsius`），因此未设置属性。</span><span class="sxs-lookup"><span data-stu-id="0367b-327">Case-sensitive mismatch (`temperatureCelsius` in the JSON), so the property isn't set.</span></span> |
| <span data-ttu-id="0367b-328">总结</span><span class="sxs-lookup"><span data-stu-id="0367b-328">Summary</span></span> | <span data-ttu-id="0367b-329">热</span><span class="sxs-lookup"><span data-stu-id="0367b-329">Hot</span></span> ||
| <span data-ttu-id="0367b-330">ExtensionData</span><span class="sxs-lookup"><span data-stu-id="0367b-330">ExtensionData</span></span> | <span data-ttu-id="0367b-331">temperatureCelsius：25</span><span class="sxs-lookup"><span data-stu-id="0367b-331">temperatureCelsius: 25</span></span> |<span data-ttu-id="0367b-332">因为大小写不匹配，所以此 JSON 属性是额外属性，会成为字典中的键值对。</span><span class="sxs-lookup"><span data-stu-id="0367b-332">Since the case didn't match, this JSON property is an extra and becomes a key-value pair in the dictionary.</span></span>|
|| <span data-ttu-id="0367b-333">DatesAvailable：</span><span class="sxs-lookup"><span data-stu-id="0367b-333">DatesAvailable:</span></span><br>  <span data-ttu-id="0367b-334">8/1/2019 12:00:00 AM -07:00</span><span class="sxs-lookup"><span data-stu-id="0367b-334">8/1/2019 12:00:00 AM -07:00</span></span><br><span data-ttu-id="0367b-335">8/2/2019 12:00:00 AM -07:00</span><span class="sxs-lookup"><span data-stu-id="0367b-335">8/2/2019 12:00:00 AM -07:00</span></span> |<span data-ttu-id="0367b-336">JSON 中的额外属性会成为键值对，将数组作为值对象。</span><span class="sxs-lookup"><span data-stu-id="0367b-336">Extra property from the JSON becomes a key-value pair, with an array as the value object.</span></span>|
| |<span data-ttu-id="0367b-337">SummaryWords：</span><span class="sxs-lookup"><span data-stu-id="0367b-337">SummaryWords:</span></span><br><span data-ttu-id="0367b-338">酷</span><span class="sxs-lookup"><span data-stu-id="0367b-338">Cool</span></span><br><span data-ttu-id="0367b-339">Windy</span><span class="sxs-lookup"><span data-stu-id="0367b-339">Windy</span></span><br><span data-ttu-id="0367b-340">Humid</span><span class="sxs-lookup"><span data-stu-id="0367b-340">Humid</span></span> |<span data-ttu-id="0367b-341">JSON 中的额外属性会成为键值对，将数组作为值对象。</span><span class="sxs-lookup"><span data-stu-id="0367b-341">Extra property from the JSON becomes a key-value pair, with an array as the value object.</span></span>|

<span data-ttu-id="0367b-342">序列化目标对象时，扩展数据键值对会成为 JSON 属性，就如同它们处于传入 JSON 中一样：</span><span class="sxs-lookup"><span data-stu-id="0367b-342">When the target object is serialized, the extension data key value pairs become JSON properties just as they were in the incoming JSON:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 0,
  "Summary": "Hot",
  "temperatureCelsius": 25,
  "DatesAvailable": [
    "2019-08-01T00:00:00-07:00",
    "2019-08-02T00:00:00-07:00"
  ],
  "SummaryWords": [
    "Cool",
    "Windy",
    "Humid"
  ]
}
```

<span data-ttu-id="0367b-343">请注意，`ExtensionData` 属性名称不会出现在 JSON 中。</span><span class="sxs-lookup"><span data-stu-id="0367b-343">Notice that the `ExtensionData` property name doesn't appear in the JSON.</span></span> <span data-ttu-id="0367b-344">此行为使 JSON 可以进行往返，而不会丢失任何不会以其他方式进行反序列化的额外数据。</span><span class="sxs-lookup"><span data-stu-id="0367b-344">This behavior lets the JSON make a round trip without losing any extra data that otherwise wouldn't be deserialized.</span></span>

## <a name="ignore-null-when-deserializing"></a><span data-ttu-id="0367b-345">反序列化时忽略 null</span><span class="sxs-lookup"><span data-stu-id="0367b-345">Ignore null when deserializing</span></span>

<span data-ttu-id="0367b-346">默认情况下，如果 JSON 中的属性为 null，则目标对象中的对应属性会设置为 null。</span><span class="sxs-lookup"><span data-stu-id="0367b-346">By default, if a property in JSON is null, the corresponding property in the target object is set to null.</span></span> <span data-ttu-id="0367b-347">在某些情况下，目标属性可能具有默认值，并且你不希望 null 值替代默认值。</span><span class="sxs-lookup"><span data-stu-id="0367b-347">In some scenarios, the target property might have a default value, and you don't want a null value to override the default.</span></span>

<span data-ttu-id="0367b-348">例如，假设以下代码表示目标对象：</span><span class="sxs-lookup"><span data-stu-id="0367b-348">For example, suppose the following code represents your target object:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithDefault)]

<span data-ttu-id="0367b-349">假设反序列化以下 JSON：</span><span class="sxs-lookup"><span data-stu-id="0367b-349">And suppose the following JSON is deserialized:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": null
}
```

<span data-ttu-id="0367b-350">反序列化之后，`WeatherForecastWithDefault` 对象的 `Summary` 属性为 null。</span><span class="sxs-lookup"><span data-stu-id="0367b-350">After deserialization, the `Summary` property of the `WeatherForecastWithDefault` object is null.</span></span>

<span data-ttu-id="0367b-351">若要更改此行为，请将 <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues?displayProperty=nameWithType> 设置为 `true`，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0367b-351">To change this behavior, set <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues?displayProperty=nameWithType> to `true`, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/DeserializeIgnoreNull.cs?name=SnippetDeserialize)]

<span data-ttu-id="0367b-352">利用此选项时，`WeatherForecastWithDefault` 对象的 `Summary` 属性在反序列化之后是默认值“No summary”。</span><span class="sxs-lookup"><span data-stu-id="0367b-352">With this option, the `Summary` property of the `WeatherForecastWithDefault` object is the default value "No summary" after deserialization.</span></span>

<span data-ttu-id="0367b-353">JSON 中的 Null 值仅在有效时才会被忽略。</span><span class="sxs-lookup"><span data-stu-id="0367b-353">Null values in the JSON are ignored only if they are valid.</span></span> <span data-ttu-id="0367b-354">不可为 null 的值类型的 Null 值会导致异常。</span><span class="sxs-lookup"><span data-stu-id="0367b-354">Null values for non-nullable value types cause exceptions.</span></span>

## <a name="utf8jsonreader-utf8jsonwriter-and-jsondocument"></a><span data-ttu-id="0367b-355">Utf8JsonReader、Utf8JsonWriter 和 JsonDocument</span><span class="sxs-lookup"><span data-stu-id="0367b-355">Utf8JsonReader, Utf8JsonWriter, and JsonDocument</span></span>

<span data-ttu-id="0367b-356"><xref:System.Text.Json.Utf8JsonReader?displayProperty=fullName> 是面向 UTF-8 编码 JSON 文本的一个高性能、低分配的只进读取器，从 `ReadOnlySpan<byte>` 或 `ReadOnlySequence<byte>` 读取信息。</span><span class="sxs-lookup"><span data-stu-id="0367b-356"><xref:System.Text.Json.Utf8JsonReader?displayProperty=fullName> is a high-performance, low allocation, forward-only reader for UTF-8 encoded JSON text, read from a `ReadOnlySpan<byte>` or `ReadOnlySequence<byte>`.</span></span> <span data-ttu-id="0367b-357">`Utf8JsonReader` 是一种低级类型，可用于生成自定义分析器和反序列化程序。</span><span class="sxs-lookup"><span data-stu-id="0367b-357">The `Utf8JsonReader` is a low-level type that can be used to build custom parsers and deserializers.</span></span> <span data-ttu-id="0367b-358"><xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> 方法在后台使用 `Utf8JsonReader`。</span><span class="sxs-lookup"><span data-stu-id="0367b-358">The <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> method uses `Utf8JsonReader` under the covers.</span></span>

<span data-ttu-id="0367b-359"><xref:System.Text.Json.Utf8JsonWriter?displayProperty=fullName> 是一种高性能方式，从常见 .NET 类型（例如，`String`、`Int32` 和 `DateTime`）编写 UTF-8 编码的 JSON 文本。</span><span class="sxs-lookup"><span data-stu-id="0367b-359"><xref:System.Text.Json.Utf8JsonWriter?displayProperty=fullName> is a high-performance way to write UTF-8 encoded JSON text from common .NET types like `String`, `Int32`, and `DateTime`.</span></span> <span data-ttu-id="0367b-360">该编写器是一种低级类型，可用于生成自定义序列化程序。</span><span class="sxs-lookup"><span data-stu-id="0367b-360">The writer is a low-level type that can be used to build custom serializers.</span></span> <span data-ttu-id="0367b-361"><xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> 方法在后台使用 `Utf8JsonWriter`。</span><span class="sxs-lookup"><span data-stu-id="0367b-361">The <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> method uses `Utf8JsonWriter` under the covers.</span></span>

<span data-ttu-id="0367b-362"><xref:System.Text.Json.JsonDocument?displayProperty=fullName> 提供使用 `Utf8JsonReader` 生成只读文档对象模型 (DOM) 的功能。</span><span class="sxs-lookup"><span data-stu-id="0367b-362"><xref:System.Text.Json.JsonDocument?displayProperty=fullName> provides the ability to build a read-only Document Object Model (DOM) by using `Utf8JsonReader`.</span></span> <span data-ttu-id="0367b-363">DOM 提供对 JSON 有效负载中的数据的随机访问。</span><span class="sxs-lookup"><span data-stu-id="0367b-363">The DOM provides random access to data in a JSON payload.</span></span> <span data-ttu-id="0367b-364">可以通过 <xref:System.Text.Json.JsonElement> 类型访问构成有效负载的 JSON 元素。</span><span class="sxs-lookup"><span data-stu-id="0367b-364">The JSON elements that compose the payload can be accessed via the <xref:System.Text.Json.JsonElement> type.</span></span> <span data-ttu-id="0367b-365">`JsonElement` 类型提供数组和对象枚举器，以及用于将 JSON 文本转换为常见 .NET 类型的 API。</span><span class="sxs-lookup"><span data-stu-id="0367b-365">The `JsonElement` type provides array and object enumerators along with APIs to convert JSON text to common .NET types.</span></span> <span data-ttu-id="0367b-366">`JsonDocument` 公开了 <xref:System.Text.Json.JsonDocument.RootElement> 属性。</span><span class="sxs-lookup"><span data-stu-id="0367b-366">`JsonDocument` exposes a <xref:System.Text.Json.JsonDocument.RootElement> property.</span></span>

<span data-ttu-id="0367b-367">以下部分演示如何使用这些工具读取和写入 JSON。</span><span class="sxs-lookup"><span data-stu-id="0367b-367">The following sections show how to use these tools for reading and writing JSON.</span></span>

## <a name="use-jsondocument-for-access-to-data"></a><span data-ttu-id="0367b-368">使用 JsonDocument 访问数据</span><span class="sxs-lookup"><span data-stu-id="0367b-368">Use JsonDocument for access to data</span></span>

<span data-ttu-id="0367b-369">下面的示例演示如何使用 <xref:System.Text.Json.JsonDocument> 类来随机访问 JSON 字符串中的数据：</span><span class="sxs-lookup"><span data-stu-id="0367b-369">The following example shows how to use the <xref:System.Text.Json.JsonDocument> class for random access to data in a JSON string:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/JsonDocumentDataAccess.cs?name=SnippetAverageGrades1)]

<span data-ttu-id="0367b-370">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="0367b-370">The preceding code:</span></span>

* <span data-ttu-id="0367b-371">假设要分析的 JSON 处于名为 `jsonString` 的字符串中。</span><span class="sxs-lookup"><span data-stu-id="0367b-371">Assumes the JSON to analyze is in a string named `jsonString`.</span></span>
* <span data-ttu-id="0367b-372">对 `Students` 数组中具有 `Grade` 属性的对象计算平均成绩。</span><span class="sxs-lookup"><span data-stu-id="0367b-372">Calculates an average grade for objects in a `Students` array that have a `Grade` property.</span></span>
* <span data-ttu-id="0367b-373">为没有成绩的学生分配默认成绩 70。</span><span class="sxs-lookup"><span data-stu-id="0367b-373">Assigns a default grade of 70 for students who don't have a grade.</span></span>
* <span data-ttu-id="0367b-374">通过在每次迭代时使 `count` 变量递增来对学生进行计数。</span><span class="sxs-lookup"><span data-stu-id="0367b-374">Counts students by incrementing a `count` variable with each iteration.</span></span> <span data-ttu-id="0367b-375">一种替代方法是调用 <xref:System.Text.Json.JsonElement.GetArrayLength%2A>，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0367b-375">An alternative is to call <xref:System.Text.Json.JsonElement.GetArrayLength%2A>, as shown in the following example:</span></span>

  [!code-csharp[](snippets/system-text-json-how-to/csharp/JsonDocumentDataAccess.cs?name=SnippetAverageGrades2)]

<span data-ttu-id="0367b-376">下面是此代码处理的 JSON 示例：</span><span class="sxs-lookup"><span data-stu-id="0367b-376">Here's an example of the JSON that this code processes:</span></span>

[!code-json[](snippets/system-text-json-how-to/csharp/GradesPrettyPrint.json)]

## <a name="use-jsondocument-to-write-json"></a><span data-ttu-id="0367b-377">使用 JsonDocument 写入 JSON</span><span class="sxs-lookup"><span data-stu-id="0367b-377">Use JsonDocument to write JSON</span></span>

<span data-ttu-id="0367b-378">下面的示例演示如何通过 <xref:System.Text.Json.JsonDocument> 写入 JSON：</span><span class="sxs-lookup"><span data-stu-id="0367b-378">The following example shows how to write JSON from a <xref:System.Text.Json.JsonDocument>:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/JsonDocumentWriteJson.cs?name=SnippetSerialize)]

<span data-ttu-id="0367b-379">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="0367b-379">The preceding code:</span></span>

* <span data-ttu-id="0367b-380">读取 JSON 文件，将数据加载到 `JsonDocument` 中，并将格式化（进行了优质打印的）JSON 写入文件。</span><span class="sxs-lookup"><span data-stu-id="0367b-380">Reads a JSON file, loads the data into a `JsonDocument`, and writes formatted (pretty-printed) JSON to a file.</span></span>
* <span data-ttu-id="0367b-381">使用 <xref:System.Text.Json.JsonDocumentOptions> 可指定允许但会忽略输入 JSON 中的注释。</span><span class="sxs-lookup"><span data-stu-id="0367b-381">Uses <xref:System.Text.Json.JsonDocumentOptions> to specify that comments in the input JSON are allowed but ignored.</span></span>
* <span data-ttu-id="0367b-382">完成后，对编写器调用 <xref:System.Text.Json.Utf8JsonWriter.Flush%2A>。</span><span class="sxs-lookup"><span data-stu-id="0367b-382">When finished, calls <xref:System.Text.Json.Utf8JsonWriter.Flush%2A> on the writer.</span></span> <span data-ttu-id="0367b-383">一种替代方法是让编写器在释放时自动刷新。</span><span class="sxs-lookup"><span data-stu-id="0367b-383">An alternative is to let the writer autoflush when it's disposed.</span></span>

<span data-ttu-id="0367b-384">下面是要由示例代码处理的 JSON 输入的示例：</span><span class="sxs-lookup"><span data-stu-id="0367b-384">Here's an example of JSON input to be processed by the example code:</span></span>

[!code-json[](snippets/system-text-json-how-to/csharp/Grades.json)]

<span data-ttu-id="0367b-385">结果是以下进行了优质打印的 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0367b-385">The result is the following pretty-printed JSON output:</span></span>

[!code-json[](snippets/system-text-json-how-to/csharp/GradesPrettyPrint.json)]

## <a name="use-utf8jsonwriter"></a><span data-ttu-id="0367b-386">使用 Utf8JsonWriter</span><span class="sxs-lookup"><span data-stu-id="0367b-386">Use Utf8JsonWriter</span></span>

<span data-ttu-id="0367b-387">下面的示例演示如何使用 <xref:System.Text.Json.Utf8JsonWriter> 类：</span><span class="sxs-lookup"><span data-stu-id="0367b-387">The following example shows how to use the <xref:System.Text.Json.Utf8JsonWriter> class:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/Utf8WriterToStream.cs?name=SnippetSerialize)]

## <a name="use-utf8jsonreader"></a><span data-ttu-id="0367b-388">使用 Utf8JsonReader</span><span class="sxs-lookup"><span data-stu-id="0367b-388">Use Utf8JsonReader</span></span>

<span data-ttu-id="0367b-389">下面的示例演示如何使用 <xref:System.Text.Json.Utf8JsonReader> 类：</span><span class="sxs-lookup"><span data-stu-id="0367b-389">The following example shows how to use the <xref:System.Text.Json.Utf8JsonReader> class:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/Utf8ReaderFromBytes.cs?name=SnippetDeserialize)]

<span data-ttu-id="0367b-390">前面的代码假设 `jsonUtf8` 变量是包含有效 JSON（编码为 UTF-8）的字节数组。</span><span class="sxs-lookup"><span data-stu-id="0367b-390">The preceding code assumes that the `jsonUtf8` variable is a byte array that contains valid JSON, encoded as UTF-8.</span></span>

### <a name="filter-data-using-utf8jsonreader"></a><span data-ttu-id="0367b-391">使用 Utf8JsonReader 筛选数据</span><span class="sxs-lookup"><span data-stu-id="0367b-391">Filter data using Utf8JsonReader</span></span>

<span data-ttu-id="0367b-392">下面的示例演示如何同步读取文件并搜索值：</span><span class="sxs-lookup"><span data-stu-id="0367b-392">The following example shows how to read a file synchronously and search for a value:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/Utf8ReaderFromFile.cs)]

<span data-ttu-id="0367b-393">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="0367b-393">The preceding code:</span></span>

* <span data-ttu-id="0367b-394">假设 JSON 包含一个对象数组，并且每个对象都可能包含一个字符串类型的“name”属性。</span><span class="sxs-lookup"><span data-stu-id="0367b-394">Assumes the JSON contains an array of objects and each object may contain a "name" property of type string.</span></span>
* <span data-ttu-id="0367b-395">对对象以及以“University”结尾的属性值进行计数。</span><span class="sxs-lookup"><span data-stu-id="0367b-395">Counts objects and "name" property values that end with "University".</span></span>
* <span data-ttu-id="0367b-396">假设文件编码为 UTF-16，并将它转码为 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="0367b-396">Assumes the file is encoded as UTF-16 and transcodes it into UTF-8.</span></span> <span data-ttu-id="0367b-397">可以使用以下代码，将编码为 UTF-8 的文件直接读入 `ReadOnlySpan<byte>`：</span><span class="sxs-lookup"><span data-stu-id="0367b-397">A file encoded as UTF-8 can be read directly into a `ReadOnlySpan<byte>`, by using the following code:</span></span>

  ```csharp
  ReadOnlySpan<byte> jsonReadOnlySpan = File.ReadAllBytes(fileName);
  ```

  <span data-ttu-id="0367b-398">如果文件包含 UTF-8 字节顺序标记 (BOM)，请在将字节传递给 `Utf8JsonReader` 之前将它删除，因为读取器需要文本。</span><span class="sxs-lookup"><span data-stu-id="0367b-398">If the file contains a UTF-8 byte order mark (BOM), remove it before passing the bytes to the `Utf8JsonReader`, since the reader expects text.</span></span> <span data-ttu-id="0367b-399">否则，BOM 被视为无效 JSON，读取器将引发异常。</span><span class="sxs-lookup"><span data-stu-id="0367b-399">Otherwise, the BOM is considered invalid JSON, and the reader throws an exception.</span></span>

<span data-ttu-id="0367b-400">下面是前面的代码可以读取的 JSON 示例。</span><span class="sxs-lookup"><span data-stu-id="0367b-400">Here's a JSON sample that the preceding code can read.</span></span> <span data-ttu-id="0367b-401">生成的摘要消息为“2 out of 4 have names that end with 'University'”：</span><span class="sxs-lookup"><span data-stu-id="0367b-401">The resulting summary message is "2 out of 4 have names that end with 'University'":</span></span>

[!code-json[](snippets/system-text-json-how-to/csharp/Universities.json)]

### <a name="read-from-a-stream-using-utf8jsonreader"></a><span data-ttu-id="0367b-402">使用 Utf8JsonReader 从流中读取</span><span class="sxs-lookup"><span data-stu-id="0367b-402">Read from a stream using Utf8JsonReader</span></span>

<span data-ttu-id="0367b-403">当读取大型文件（例如，1 GB 或更大的文件）时，你可能希望避免一次性将整个文件加载到内存中。</span><span class="sxs-lookup"><span data-stu-id="0367b-403">When reading a large file (a gigabyte or more in size, for example), you might want to avoid having to load the entire file into memory at once.</span></span> <span data-ttu-id="0367b-404">此时，可以使用 <xref:System.IO.FileStream>。</span><span class="sxs-lookup"><span data-stu-id="0367b-404">For this scenario, you can use a <xref:System.IO.FileStream>.</span></span>

<span data-ttu-id="0367b-405">使用 `Utf8JsonReader` 从流中读取时，适用以下规则：</span><span class="sxs-lookup"><span data-stu-id="0367b-405">When using the `Utf8JsonReader` to read from a stream, the following rules apply:</span></span>

* <span data-ttu-id="0367b-406">包含部分 JSON 有效负载的缓冲区必须至少与其中的最大 JSON 令牌一样大，以便读取器可以推进进度。</span><span class="sxs-lookup"><span data-stu-id="0367b-406">The buffer containing the partial JSON payload must be at least as big as the largest JSON token within it so that the reader can make forward progress.</span></span>
* <span data-ttu-id="0367b-407">缓冲区的大小必须至少与 JSON 中的最大空格序列一样大。</span><span class="sxs-lookup"><span data-stu-id="0367b-407">The buffer must be at least as big as the largest sequence of white space within the JSON.</span></span>
* <span data-ttu-id="0367b-408">读取器不会跟踪已读取的数据，直到它完全读取 JSON 有效负载中的下一个 <xref:System.Text.Json.Utf8JsonReader.TokenType%2A>。</span><span class="sxs-lookup"><span data-stu-id="0367b-408">The reader doesn't keep track of the data it has read until it completely reads the next <xref:System.Text.Json.Utf8JsonReader.TokenType%2A> in the JSON payload.</span></span> <span data-ttu-id="0367b-409">因此，当缓冲区中有剩余字节时，必须再次将它们传递给读取器。</span><span class="sxs-lookup"><span data-stu-id="0367b-409">So when there are bytes left over in the buffer, you have to pass them to the reader again.</span></span> <span data-ttu-id="0367b-410">你可以使用 <xref:System.Text.Json.Utf8JsonReader.BytesConsumed%2A> 来确定剩余的字节数。</span><span class="sxs-lookup"><span data-stu-id="0367b-410">You can use <xref:System.Text.Json.Utf8JsonReader.BytesConsumed%2A> to determine how many bytes are left over.</span></span>

<span data-ttu-id="0367b-411">下面的代码演示了如何从流中读取。</span><span class="sxs-lookup"><span data-stu-id="0367b-411">The following code illustrates how to read from a stream.</span></span> <span data-ttu-id="0367b-412">本示例显示了 <xref:System.IO.MemoryStream>。</span><span class="sxs-lookup"><span data-stu-id="0367b-412">The example shows a <xref:System.IO.MemoryStream>.</span></span> <span data-ttu-id="0367b-413">类似的代码将使用 <xref:System.IO.FileStream>，当 `FileStream` 在开头包含 UTF-8 BOM 时除外。</span><span class="sxs-lookup"><span data-stu-id="0367b-413">Similar code will work with a <xref:System.IO.FileStream>, except when the `FileStream` contains a UTF-8 BOM at the start.</span></span> <span data-ttu-id="0367b-414">在这种情况下，需要先从缓冲区中去除这三个字节，然后再将剩余字节传递到 `Utf8JsonReader`。</span><span class="sxs-lookup"><span data-stu-id="0367b-414">In that case, you need to strip those three bytes from the buffer before passing the remaining bytes to the `Utf8JsonReader`.</span></span> <span data-ttu-id="0367b-415">否则，读取器将引发异常，因为 BOM 不被视为 JSON 的有效部分。</span><span class="sxs-lookup"><span data-stu-id="0367b-415">Otherwise the reader would throw an exception, since the BOM is not considered a valid part of the JSON.</span></span>

<span data-ttu-id="0367b-416">示例代码从 4KB 缓冲区开始，每当发现大小不足以容纳完整的 JSON 令牌（必须容纳完整的令牌，读取器才能推动处理 JSON 有效负载）时，就会使缓冲区大小成倍增加。</span><span class="sxs-lookup"><span data-stu-id="0367b-416">The sample code starts with a 4KB buffer and doubles the buffer size each time it finds that the size is not big enough to fit a complete JSON token, which is required for the reader to make forward progress on the JSON payload.</span></span> <span data-ttu-id="0367b-417">仅当设置的初始缓冲区非常小（例如 10 个字节）时，代码片段中提供的 JSON 示例才会触发缓冲区大小增加。</span><span class="sxs-lookup"><span data-stu-id="0367b-417">The JSON sample provided in the snippet triggers a buffer size increase only if you set a very small initial buffer size, for example, 10 bytes.</span></span> <span data-ttu-id="0367b-418">如果将初始缓冲区大小设置为 10，则 `Console.WriteLine` 语句会说明缓冲区大小增加的原因和影响。</span><span class="sxs-lookup"><span data-stu-id="0367b-418">If you set the initial buffer size to 10, the `Console.WriteLine` statements illustrate the cause and effect of buffer size increases.</span></span> <span data-ttu-id="0367b-419">在初始缓冲区大小为 4KB 时，每个 `Console.WriteLine` 都会显示整个示例 JSON，并且不必增加缓冲区大小。</span><span class="sxs-lookup"><span data-stu-id="0367b-419">At the 4KB initial buffer size, the entire sample JSON is shown by each `Console.WriteLine`, and the buffer size never has to be increased.</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/Utf8ReaderPartialRead.cs)]

<span data-ttu-id="0367b-420">前面的示例未对缓冲区大小的增长设置任何限制。</span><span class="sxs-lookup"><span data-stu-id="0367b-420">The preceding example sets no limit to how big the buffer can grow.</span></span> <span data-ttu-id="0367b-421">如果令牌大小太大，则代码可能会失败，并出现 <xref:System.OutOfMemoryException> 异常。</span><span class="sxs-lookup"><span data-stu-id="0367b-421">If the token size is too large, the code could fail with an <xref:System.OutOfMemoryException> exception.</span></span> <span data-ttu-id="0367b-422">如果 JSON 包含大小约为 1 GB 或更大的令牌，则会发生这种情况，因为将 1 GB 大小加倍会导致令牌太大，无法放入 `int32` 缓冲区。</span><span class="sxs-lookup"><span data-stu-id="0367b-422">This can happen if the JSON contains a token that is around 1 GB or more in size, because doubling the 1 GB size results in a size that is too large to fit into an `int32` buffer.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0367b-423">其他资源</span><span class="sxs-lookup"><span data-stu-id="0367b-423">Additional resources</span></span>

* [<span data-ttu-id="0367b-424">System.Text.Json 概述</span><span class="sxs-lookup"><span data-stu-id="0367b-424">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="0367b-425">如何编写自定义转换器</span><span class="sxs-lookup"><span data-stu-id="0367b-425">How to write custom converters</span></span>](system-text-json-converters-how-to.md)
* [<span data-ttu-id="0367b-426">如何从 Newtonsoft.Json 迁移</span><span class="sxs-lookup"><span data-stu-id="0367b-426">How to migrate from Newtonsoft.Json</span></span>](system-text-json-migrate-from-newtonsoft-how-to.md)
* [<span data-ttu-id="0367b-427">System.Text.Json 中的 DateTime 和 DateTimeOffset 支持</span><span class="sxs-lookup"><span data-stu-id="0367b-427">DateTime and DateTimeOffset support in System.Text.Json</span></span>](../datetime/system-text-json-support.md)
* <span data-ttu-id="0367b-428">[System.Text.Json API 参考](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="0367b-428">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
<!-- * [System.Text.Json roadmap](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/roadmap/README.md)-->
