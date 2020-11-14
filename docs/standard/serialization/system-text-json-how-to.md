---
title: 如何使用 C# 对 JSON 进行序列化和反序列化 - .NET
description: '了解如何使用 :::no-loc(System.Text.Json)::: 命名空间在 .NET 中向/从 JSON 进行序列化和反序列化。 包含示例代码。'
ms.date: 11/05/2020
no-loc:
- ':::no-loc(System.Text.Json):::'
- ':::no-loc(Newtonsoft.Json):::'
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 2c1358b2b63a92cb50b853043adbfaae23ccd897
ms.sourcegitcommit: 6bef8abde346c59771a35f4f76bf037ff61c5ba3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2020
ms.locfileid: "94329867"
---
# <a name="how-to-serialize-and-deserialize-marshal-and-unmarshal-json-in-net"></a><span data-ttu-id="0ffbe-104">如何在 .NET 中对 JSON 进行序列化和反序列化（封送和拆收）</span><span class="sxs-lookup"><span data-stu-id="0ffbe-104">How to serialize and deserialize (marshal and unmarshal) JSON in .NET</span></span>

<span data-ttu-id="0ffbe-105">本文演示如何使用 <xref::::no-loc(System.Text.Json):::?displayProperty=fullName> 命名空间向/从 JavaScript 对象表示法 (JSON) 进行序列化和反序列化。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-105">This article shows how to use the <xref::::no-loc(System.Text.Json):::?displayProperty=fullName> namespace to serialize to and deserialize from JavaScript Object Notation (JSON).</span></span> <span data-ttu-id="0ffbe-106">如果要从 `:::no-loc(Newtonsoft.Json):::` 移植现有代码，请参阅[如何迁移到 `:::no-loc(System.Text.Json):::`](system-text-json-migrate-from-newtonsoft-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-106">If you're porting existing code from `:::no-loc(Newtonsoft.Json):::`, see [How to migrate to `:::no-loc(System.Text.Json):::`](system-text-json-migrate-from-newtonsoft-how-to.md).</span></span>

<span data-ttu-id="0ffbe-107">方向和示例代码直接使用库，而不是通过框架（如 [ASP.NET Core](/aspnet/core/)）。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-107">The directions and sample code use the library directly, not through a framework such as [ASP.NET Core](/aspnet/core/).</span></span>

<span data-ttu-id="0ffbe-108">大多数序列化示例代码将 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> 设置为 `true`，以 JSON 进行优质打印（包含缩进和空格，以提高可读性）。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-108">Most of the serialization sample code sets <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> to `true` to "pretty-print" the JSON (with indentation and whitespace for human readability).</span></span> <span data-ttu-id="0ffbe-109">对于生产用途，通常对于此设置会接受默认值 `false`。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-109">For production use, you would typically accept the default value of `false` for this setting.</span></span>

<span data-ttu-id="0ffbe-110">代码示例引用下面的类及其变体：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-110">The code examples refer to the following class and variants of it:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

## <a name="namespaces"></a><span data-ttu-id="0ffbe-111">命名空间</span><span class="sxs-lookup"><span data-stu-id="0ffbe-111">Namespaces</span></span>

<span data-ttu-id="0ffbe-112"><xref::::no-loc(System.Text.Json):::> 命名空间包含所有入口点和主要类型。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-112">The <xref::::no-loc(System.Text.Json):::> namespace contains all the entry points and the main types.</span></span> <span data-ttu-id="0ffbe-113"><xref::::no-loc(System.Text.Json):::.Serialization> 命名空间包含用于高级方案的特性和 API，以及特定于序列化和反序列化的自定义。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-113">The <xref::::no-loc(System.Text.Json):::.Serialization> namespace contains attributes and APIs for advanced scenarios and customization specific to serialization and deserialization.</span></span> <span data-ttu-id="0ffbe-114">本文中演示的代码示例要求将 `using` 指令用于其中一个或两个命名空间：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-114">The code examples shown in this article require `using` directives for one or both of these namespaces:</span></span>

```csharp
using :::no-loc(System.Text.Json):::;
using :::no-loc(System.Text.Json):::.Serialization;
```

<span data-ttu-id="0ffbe-115">`:::no-loc(System.Text.Json):::` 中不支持 <xref:System.Runtime.Serialization> 命名空间中的特性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-115">Attributes from the <xref:System.Runtime.Serialization> namespace aren't supported in `:::no-loc(System.Text.Json):::`.</span></span>

## <a name="how-to-write-net-objects-to-json-serialize"></a><span data-ttu-id="0ffbe-116">如何将 .NET 对象编写为 JSON（序列化）</span><span class="sxs-lookup"><span data-stu-id="0ffbe-116">How to write .NET objects to JSON (serialize)</span></span>

<span data-ttu-id="0ffbe-117">若要将 JSON 编写为字符串或文件，请调用 <xref::::no-loc(System.Text.Json):::.JsonSerializer.Serialize%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-117">To write JSON to a string or to a file, call the <xref::::no-loc(System.Text.Json):::.JsonSerializer.Serialize%2A?displayProperty=nameWithType> method.</span></span>

<span data-ttu-id="0ffbe-118">下面的示例将 JSON 创建为字符串：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-118">The following example creates JSON as a string:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToString.cs?name=SnippetSerialize)]

<span data-ttu-id="0ffbe-119">下面的示例使用同步代码创建 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-119">The following example uses synchronous code to create a JSON file:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToFile.cs?name=SnippetSerialize)]

<span data-ttu-id="0ffbe-120">下面的示例使用异步代码创建 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-120">The following example uses asynchronous code to create a JSON file:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToFileAsync.cs?name=SnippetSerialize)]

<span data-ttu-id="0ffbe-121">前面的示例对要序列化的类型使用类型推理。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-121">The preceding examples use type inference for the type being serialized.</span></span> <span data-ttu-id="0ffbe-122">`Serialize()` 的重载采用泛型类型参数：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-122">An overload of `Serialize()` takes a generic type parameter:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToString.cs?name=SnippetSerializeWithGenericParameter)]

### <a name="serialization-example"></a><span data-ttu-id="0ffbe-123">序列化示例</span><span class="sxs-lookup"><span data-stu-id="0ffbe-123">Serialization example</span></span>

<span data-ttu-id="0ffbe-124">下面是一个包含集合类型属性和用户定义类型的示例类：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-124">Here's an example class that contains collection-type properties and a user-defined type:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithPOCOs)]

> [!TIP]
> <span data-ttu-id="0ffbe-125">“POCO”代表[普通旧 CLR 对象](https://en.wikipedia.org/wiki/Plain_old_CLR_object)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-125">"POCO" stands for [plain old CLR object](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span></span> <span data-ttu-id="0ffbe-126">POCO 是一种 .NET 类型，它不通过继承或特性等依赖于任何框架特定类型。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-126">A POCO is a .NET type that doesn't depend on any framework-specific types, for example, through inheritance or attributes.</span></span>

<span data-ttu-id="0ffbe-127">序列化以上类型的实例的 JSON 输出类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-127">The JSON output from serializing an instance of the preceding type looks like the following example.</span></span> <span data-ttu-id="0ffbe-128">默认情况下，JSON 输出会缩小：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-128">The JSON output is minified by default:</span></span>

```json
{"Date":"2019-08-01T00:00:00-07:00","TemperatureCelsius":25,"Summary":"Hot","DatesAvailable":["2019-08-01T00:00:00-07:00","2019-08-02T00:00:00-07:00"],"TemperatureRanges":{"Cold":{"High":20,"Low":-10},"Hot":{"High":60,"Low":20}},"SummaryWords":["Cool","Windy","Humid"]}
```

<span data-ttu-id="0ffbe-129">下面的示例演示相同的 JSON，但进行了格式设置（即，具有空格和缩进的优质打印版本）：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-129">The following example shows the same JSON, but formatted (that is, pretty-printed with whitespace and indentation):</span></span>

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

### <a name="serialize-to-utf-8"></a><span data-ttu-id="0ffbe-130">序列化为 UTF-8</span><span class="sxs-lookup"><span data-stu-id="0ffbe-130">Serialize to UTF-8</span></span>

<span data-ttu-id="0ffbe-131">若要序列化为 UTF-8，请调用 <xref::::no-loc(System.Text.Json):::.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> 方法：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-131">To serialize to UTF-8, call the <xref::::no-loc(System.Text.Json):::.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> method:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToUtf8.cs?name=SnippetSerialize)]

<span data-ttu-id="0ffbe-132">还有一个采用 <xref::::no-loc(System.Text.Json):::.Utf8JsonWriter> 的 <xref::::no-loc(System.Text.Json):::.JsonSerializer.Serialize%2A> 重载可用。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-132">A <xref::::no-loc(System.Text.Json):::.JsonSerializer.Serialize%2A> overload that takes a <xref::::no-loc(System.Text.Json):::.Utf8JsonWriter> is also available.</span></span>

<span data-ttu-id="0ffbe-133">序列化为 UTF-8 比使用基于字符串的方法大约快 5-10%。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-133">Serializing to UTF-8 is about 5-10% faster than using the string-based methods.</span></span> <span data-ttu-id="0ffbe-134">出现这种差别的原因是字节（作为 UTF-8）不需要转换为字符串 (UTF-16)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-134">The difference is because the bytes (as UTF-8) don't need to be converted to strings (UTF-16).</span></span>

## <a name="serialization-behavior"></a><span data-ttu-id="0ffbe-135">序列化行为</span><span class="sxs-lookup"><span data-stu-id="0ffbe-135">Serialization behavior</span></span>
::: zone pivot="dotnet-5-0"

* <span data-ttu-id="0ffbe-136">默认情况下，所有公共属性都会序列化。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-136">By default, all public properties are serialized.</span></span> <span data-ttu-id="0ffbe-137">可以[指定要忽略的属性](#ignore-properties)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-137">You can [specify properties to ignore](#ignore-properties).</span></span>
* <span data-ttu-id="0ffbe-138">[默认编码器](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default)会转义非 ASCII 字符、ASCII 范围内的 HTML 敏感字符以及根据 [RFC 8259 JSON 规范](https://tools.ietf.org/html/rfc8259#section-7)必须进行转义的字符。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-138">The [default encoder](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) escapes non-ASCII characters, HTML-sensitive characters within the ASCII-range, and characters that must be escaped according to [the RFC 8259 JSON spec](https://tools.ietf.org/html/rfc8259#section-7).</span></span>
* <span data-ttu-id="0ffbe-139">默认情况下，JSON 会缩小。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-139">By default, JSON is minified.</span></span> <span data-ttu-id="0ffbe-140">可以[对 JSON 进行优质打印](#serialize-to-formatted-json)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-140">You can [pretty-print the JSON](#serialize-to-formatted-json).</span></span>
* <span data-ttu-id="0ffbe-141">默认情况下，JSON 名称的大小写与 .NET 名称匹配。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-141">By default, casing of JSON names matches the .NET names.</span></span> <span data-ttu-id="0ffbe-142">可以[自定义 JSON 名称大小写](#customize-json-names-and-values)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-142">You can [customize JSON name casing](#customize-json-names-and-values).</span></span>
* <span data-ttu-id="0ffbe-143">默认情况下，检测到循环引用并引发异常。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-143">By default, circular references are detected and exceptions thrown.</span></span> <span data-ttu-id="0ffbe-144">可以[保留引用并处理循环引用](#preserve-references-and-handle-circular-references)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-144">You can [preserve references and handle circular references](#preserve-references-and-handle-circular-references).</span></span>
* <span data-ttu-id="0ffbe-145">默认情况下忽略[字段](../../csharp/programming-guide/classes-and-structs/fields.md)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-145">By default, [fields](../../csharp/programming-guide/classes-and-structs/fields.md) are ignored.</span></span> <span data-ttu-id="0ffbe-146">可以[包含字段](#include-fields)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-146">You can [include fields](#include-fields).</span></span>

<span data-ttu-id="0ffbe-147">当你在 ASP.NET Core 应用中间接使用 :::no-loc(System.Text.Json)::: 时，某些默认行为会有所不同。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-147">When you use :::no-loc(System.Text.Json)::: indirectly in an ASP.NET Core app, some default behaviors are different.</span></span> <span data-ttu-id="0ffbe-148">有关详细信息，请参阅 [JsonSerializerOptions 的 Web 默认值](#web-defaults-for-jsonserializeroptions)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-148">For more information, see [Web defaults for JsonSerializerOptions](#web-defaults-for-jsonserializeroptions).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"

* <span data-ttu-id="0ffbe-149">默认情况下，所有公共属性都会序列化。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-149">By default, all public properties are serialized.</span></span> <span data-ttu-id="0ffbe-150">可以[指定要忽略的属性](#ignore-properties)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-150">You can [specify properties to ignore](#ignore-properties).</span></span>
* <span data-ttu-id="0ffbe-151">[默认编码器](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default)会转义非 ASCII 字符、ASCII 范围内的 HTML 敏感字符以及根据 [RFC 8259 JSON 规范](https://tools.ietf.org/html/rfc8259#section-7)必须进行转义的字符。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-151">The [default encoder](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) escapes non-ASCII characters, HTML-sensitive characters within the ASCII-range, and characters that must be escaped according to [the RFC 8259 JSON spec](https://tools.ietf.org/html/rfc8259#section-7).</span></span>
* <span data-ttu-id="0ffbe-152">默认情况下，JSON 会缩小。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-152">By default, JSON is minified.</span></span> <span data-ttu-id="0ffbe-153">可以[对 JSON 进行优质打印](#serialize-to-formatted-json)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-153">You can [pretty-print the JSON](#serialize-to-formatted-json).</span></span>
* <span data-ttu-id="0ffbe-154">默认情况下，JSON 名称的大小写与 .NET 名称匹配。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-154">By default, casing of JSON names matches the .NET names.</span></span> <span data-ttu-id="0ffbe-155">可以[自定义 JSON 名称大小写](#customize-json-names-and-values)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-155">You can [customize JSON name casing](#customize-json-names-and-values).</span></span>
* <span data-ttu-id="0ffbe-156">检测到循环引用并引发异常。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-156">Circular references are detected and exceptions thrown.</span></span>
* <span data-ttu-id="0ffbe-157">将忽略[字段](../../csharp/programming-guide/classes-and-structs/fields.md)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-157">[Fields](../../csharp/programming-guide/classes-and-structs/fields.md) are ignored.</span></span>
::: zone-end

<span data-ttu-id="0ffbe-158">支持的类型包括：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-158">Supported types include:</span></span>
::: zone pivot="dotnet-5-0"

* <span data-ttu-id="0ffbe-159">映射到 JavaScript 基元的 .NET 基元，如数值类型、字符串和布尔。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-159">.NET primitives that map to JavaScript primitives, such as numeric types, strings, and Boolean.</span></span>
* <span data-ttu-id="0ffbe-160">用户定义的[普通旧 CLR 对象 (POCO)](https://en.wikipedia.org/wiki/Plain_old_CLR_object)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-160">User-defined [plain old CLR objects (POCOs)](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span></span>
* <span data-ttu-id="0ffbe-161">一维和交错数组 (`T[][]`)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-161">One-dimensional and jagged arrays (`T[][]`).</span></span>
* <span data-ttu-id="0ffbe-162">以下命名空间中的集合和字典。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-162">Collections and dictionaries from the following namespaces.</span></span>
  * <xref:System.Collections>
  * <xref:System.Collections.Generic>
  * <xref:System.Collections.Immutable>
  * <xref:System.Collections.Concurrent>
  * <xref:System.Collections.Specialized>
  * <xref:System.Collections.ObjectModel>
::: zone-end

::: zone pivot="dotnet-core-3-1"

* <span data-ttu-id="0ffbe-163">映射到 JavaScript 基元的 .NET 基元，如数值类型、字符串和布尔。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-163">.NET primitives that map to JavaScript primitives, such as numeric types, strings, and Boolean.</span></span>
* <span data-ttu-id="0ffbe-164">用户定义的[普通旧 CLR 对象 (POCO)](https://en.wikipedia.org/wiki/Plain_old_CLR_object)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-164">User-defined [plain old CLR objects (POCOs)](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span></span>
* <span data-ttu-id="0ffbe-165">一维和交错数组 (`ArrayName[][]`)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-165">One-dimensional and jagged arrays (`ArrayName[][]`).</span></span>
* <span data-ttu-id="0ffbe-166">`Dictionary<string,TValue>`其中 `TValue` 是 `object`、`JsonElement` 或 POCO。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-166">`Dictionary<string,TValue>` where `TValue` is `object`, `JsonElement`, or a POCO.</span></span>
* <span data-ttu-id="0ffbe-167">以下命名空间中的集合。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-167">Collections from the following namespaces.</span></span>
  * <xref:System.Collections>
  * <xref:System.Collections.Generic>
  * <xref:System.Collections.Immutable>
  * <xref:System.Collections.Concurrent>
  * <xref:System.Collections.Specialized>
  * <xref:System.Collections.ObjectModel>
::: zone-end

<span data-ttu-id="0ffbe-168">可以[实现自定义转换器](system-text-json-converters-how-to.md)以处理其他类型或提供内置转换器不支持的功能。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-168">You can [implement custom converters](system-text-json-converters-how-to.md) to handle additional types or to provide functionality that isn't supported by the built-in converters.</span></span>

## <a name="how-to-read-json-into-net-objects-deserialize"></a><span data-ttu-id="0ffbe-169">如何将 JSON 读入 .NET 对象（反序列化）</span><span class="sxs-lookup"><span data-stu-id="0ffbe-169">How to read JSON into .NET objects (deserialize)</span></span>

<span data-ttu-id="0ffbe-170">若要从字符串或文件进行反序列化，请调用 <xref::::no-loc(System.Text.Json):::.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-170">To deserialize from a string or a file, call the <xref::::no-loc(System.Text.Json):::.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> method.</span></span>

<span data-ttu-id="0ffbe-171">下面的示例从字符串读取 JSON，并创建前面为[序列化示例](#serialization-example)显示的 `WeatherForecastWithPOCOs` 类的实例：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-171">The following example reads JSON from a string and creates an instance of the `WeatherForecastWithPOCOs` class shown earlier for the [serialization example](#serialization-example):</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToString.cs?name=SnippetDeserialize)]

<span data-ttu-id="0ffbe-172">若要使用同步代码从文件进行反序列化，请将文件读入字符串中，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-172">To deserialize from a file by using synchronous code, read the file into a string, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToFile.cs?name=SnippetDeserialize)]

<span data-ttu-id="0ffbe-173">若要使用异步代码从文件进行反序列化，请调用 <xref::::no-loc(System.Text.Json):::.JsonSerializer.DeserializeAsync%2A> 方法：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-173">To deserialize from a file by using asynchronous code, call the <xref::::no-loc(System.Text.Json):::.JsonSerializer.DeserializeAsync%2A> method:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToFileAsync.cs?name=SnippetDeserialize)]

### <a name="deserialize-from-utf-8"></a><span data-ttu-id="0ffbe-174">从 UTF-8 进行反序列化</span><span class="sxs-lookup"><span data-stu-id="0ffbe-174">Deserialize from UTF-8</span></span>

<span data-ttu-id="0ffbe-175">若要从 UTF-8 进行反序列化，请调用采用 `Utf8JsonReader` 或 `ReadOnlySpan<byte>` 的 <xref::::no-loc(System.Text.Json):::.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> 重载，如下面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-175">To deserialize from UTF-8, call a <xref::::no-loc(System.Text.Json):::.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> overload that takes a `Utf8JsonReader` or a `ReadOnlySpan<byte>`, as shown in the following examples.</span></span> <span data-ttu-id="0ffbe-176">这些示例假设 JSON 处于名为 jsonUtf8Bytes 的字节数组中。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-176">The examples assume the JSON is in a byte array named jsonUtf8Bytes.</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToUtf8.cs?name=SnippetDeserialize1)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToUtf8.cs?name=SnippetDeserialize2)]

## <a name="deserialization-behavior"></a><span data-ttu-id="0ffbe-177">反序列化行为</span><span class="sxs-lookup"><span data-stu-id="0ffbe-177">Deserialization behavior</span></span>

<span data-ttu-id="0ffbe-178">对 JSON 进行反序列化时，以下行为适用：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-178">The following behaviors apply when deserializing JSON:</span></span>

::: zone pivot="dotnet-5-0"

* <span data-ttu-id="0ffbe-179">默认情况下，属性名称匹配区分大小写。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-179">By default, property name matching is case-sensitive.</span></span> <span data-ttu-id="0ffbe-180">可以[指定不区分大小写](#case-insensitive-property-matching)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-180">You can [specify case-insensitivity](#case-insensitive-property-matching).</span></span>
* <span data-ttu-id="0ffbe-181">如果 JSON 包含只读属性的值，则会忽略该值，并且不引发异常。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-181">If the JSON contains a value for a read-only property, the value is ignored and no exception is thrown.</span></span>
* <span data-ttu-id="0ffbe-182">序列化程序会忽略非公共构造函数。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-182">Non-public constructors are ignored by the serializer.</span></span>
* <span data-ttu-id="0ffbe-183">支持反序列化为不可变对象或只读属性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-183">Deserialization to immutable objects or read-only properties is supported.</span></span> <span data-ttu-id="0ffbe-184">请参阅[不可变类型和记录](#immutable-types-and-records)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-184">See [Immutable types and Records](#immutable-types-and-records).</span></span>
* <span data-ttu-id="0ffbe-185">默认情况下，支持将枚举作为数字。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-185">By default, enums are supported as numbers.</span></span> <span data-ttu-id="0ffbe-186">可以[将枚举名称序列化为字符串](#enums-as-strings)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-186">You can [serialize enum names as strings](#enums-as-strings).</span></span>
* <span data-ttu-id="0ffbe-187">默认情况下忽略字段。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-187">By default, fields are ignored.</span></span> <span data-ttu-id="0ffbe-188">可以[包含字段](#include-fields)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-188">You can [include fields](#include-fields).</span></span>
* <span data-ttu-id="0ffbe-189">默认情况下，JSON 中的注释或尾随逗号会引发异常。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-189">By default, comments or trailing commas in the JSON throw exceptions.</span></span> <span data-ttu-id="0ffbe-190">可以[允许注释和尾随逗号](#allow-comments-and-trailing-commas)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-190">You can [allow comments and trailing commas](#allow-comments-and-trailing-commas).</span></span>
* <span data-ttu-id="0ffbe-191">[默认最大深度](xref::::no-loc(System.Text.Json):::.JsonReaderOptions.MaxDepth)为 64。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-191">The [default maximum depth](xref::::no-loc(System.Text.Json):::.JsonReaderOptions.MaxDepth) is 64.</span></span>

<span data-ttu-id="0ffbe-192">当你在 ASP.NET Core 应用中间接使用 :::no-loc(System.Text.Json)::: 时，某些默认行为会有所不同。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-192">When you use :::no-loc(System.Text.Json)::: indirectly in an ASP.NET Core app, some default behaviors are different.</span></span> <span data-ttu-id="0ffbe-193">有关详细信息，请参阅 [JsonSerializerOptions 的 Web 默认值](#web-defaults-for-jsonserializeroptions)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-193">For more information, see [Web defaults for JsonSerializerOptions](#web-defaults-for-jsonserializeroptions).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"

* <span data-ttu-id="0ffbe-194">默认情况下，属性名称匹配区分大小写。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-194">By default, property name matching is case-sensitive.</span></span> <span data-ttu-id="0ffbe-195">可以[指定不区分大小写](#case-insensitive-property-matching)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-195">You can [specify case-insensitivity](#case-insensitive-property-matching).</span></span> <span data-ttu-id="0ffbe-196">ASP.NET Core 应用[默认指定不区分大小写](#web-defaults-for-jsonserializeroptions)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-196">ASP.NET Core apps [specify case-insensitivity by default](#web-defaults-for-jsonserializeroptions).</span></span>
* <span data-ttu-id="0ffbe-197">如果 JSON 包含只读属性的值，则会忽略该值，并且不引发异常。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-197">If the JSON contains a value for a read-only property, the value is ignored and no exception is thrown.</span></span>
* <span data-ttu-id="0ffbe-198">无参数构造函数（可以是公共的、内部的或专用的）用于反序列化。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-198">A parameterless constructor, which can be public, internal, or private, is used for deserialization.</span></span>
* <span data-ttu-id="0ffbe-199">不支持反序列化为不可变对象或只读属性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-199">Deserialization to immutable objects or read-only properties isn't supported.</span></span>
* <span data-ttu-id="0ffbe-200">默认情况下，支持将枚举作为数字。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-200">By default, enums are supported as numbers.</span></span> <span data-ttu-id="0ffbe-201">可以[将枚举名称序列化为字符串](#enums-as-strings)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-201">You can [serialize enum names as strings](#enums-as-strings).</span></span>
* <span data-ttu-id="0ffbe-202">不支持字段。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-202">Fields aren't supported.</span></span>
* <span data-ttu-id="0ffbe-203">默认情况下，JSON 中的注释或尾随逗号会引发异常。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-203">By default, comments or trailing commas in the JSON throw exceptions.</span></span> <span data-ttu-id="0ffbe-204">可以[允许注释和尾随逗号](#allow-comments-and-trailing-commas)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-204">You can [allow comments and trailing commas](#allow-comments-and-trailing-commas).</span></span>
* <span data-ttu-id="0ffbe-205">[默认最大深度](xref::::no-loc(System.Text.Json):::.JsonReaderOptions.MaxDepth)为 64。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-205">The [default maximum depth](xref::::no-loc(System.Text.Json):::.JsonReaderOptions.MaxDepth) is 64.</span></span>

<span data-ttu-id="0ffbe-206">当你在 ASP.NET Core 应用中间接使用 :::no-loc(System.Text.Json)::: 时，某些默认行为会有所不同。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-206">When you use :::no-loc(System.Text.Json)::: indirectly in an ASP.NET Core app, some default behaviors are different.</span></span> <span data-ttu-id="0ffbe-207">有关详细信息，请参阅 [JsonSerializerOptions 的 Web 默认值](#web-defaults-for-jsonserializeroptions)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-207">For more information, see [Web defaults for JsonSerializerOptions](#web-defaults-for-jsonserializeroptions).</span></span>
::: zone-end

<span data-ttu-id="0ffbe-208">可以[实现自定义转换器](system-text-json-converters-how-to.md)以提供内置转换器不支持的功能。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-208">You can [implement custom converters](system-text-json-converters-how-to.md) to provide functionality that isn't supported by the built-in converters.</span></span>

## <a name="serialize-to-formatted-json"></a><span data-ttu-id="0ffbe-209">序列化为格式化 JSON</span><span class="sxs-lookup"><span data-stu-id="0ffbe-209">Serialize to formatted JSON</span></span>

<span data-ttu-id="0ffbe-210">若要对 JSON 输出进行优质打印，请将 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> 设置为 `true`：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-210">To pretty-print the JSON output, set <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> to `true`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripToString.cs?name=SnippetSerializePrettyPrint)]

<span data-ttu-id="0ffbe-211">下面是一个要进行序列化的示例类型，以及进行了优质打印的 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-211">Here's an example type to be serialized and pretty-printed JSON output:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

## <a name="include-fields"></a><span data-ttu-id="0ffbe-212">包含字段</span><span class="sxs-lookup"><span data-stu-id="0ffbe-212">Include fields</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="0ffbe-213">在序列化或反序列化时，使用 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.IncludeFields?displayProperty=nameWithType> 全局设置或 [[JsonInclude]](xref::::no-loc(System.Text.Json):::.Serialization.JsonIncludeAttribute) 特性来包含字段，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-213">Use the <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.IncludeFields?displayProperty=nameWithType> global setting or the [[JsonInclude]](xref::::no-loc(System.Text.Json):::.Serialization.JsonIncludeAttribute) attribute to include fields when serializing or deserializing, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/Fields.cs" highlight="15,17,19,31":::

<span data-ttu-id="0ffbe-214">若要忽略只读字段，请使用 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.IgnoreReadOnlyFields%2A?displayProperty=nameWithType> 全局设置。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-214">To ignore read-only fields, use the <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.IgnoreReadOnlyFields%2A?displayProperty=nameWithType> global setting.</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="0ffbe-215">.NET Core 3.1 的 :::no-loc(System.Text.Json)::: 中不支持字段。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-215">Fields are not supported in :::no-loc(System.Text.Json)::: in .NET Core 3.1.</span></span> <span data-ttu-id="0ffbe-216">[自定义转换器](system-text-json-converters-how-to.md)可提供此功能。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-216">[Custom converters](system-text-json-converters-how-to.md) can provide this functionality.</span></span>
::: zone-end

## <a name="customize-json-names-and-values"></a><span data-ttu-id="0ffbe-217">自定义 JSON 名称和值</span><span class="sxs-lookup"><span data-stu-id="0ffbe-217">Customize JSON names and values</span></span>

<span data-ttu-id="0ffbe-218">默认情况下，属性名称和字典键在 JSON 输出中保持不变，包括大小写。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-218">By default, property names and dictionary keys are unchanged in the JSON output, including case.</span></span> <span data-ttu-id="0ffbe-219">枚举值表示为数字。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-219">Enum values are represented as numbers.</span></span> <span data-ttu-id="0ffbe-220">本部分介绍如何：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-220">This section explains how to:</span></span>

* [<span data-ttu-id="0ffbe-221">自定义单个属性名称</span><span class="sxs-lookup"><span data-stu-id="0ffbe-221">Customize individual property names</span></span>](#customize-individual-property-names)
* [<span data-ttu-id="0ffbe-222">将所有属性名称转换为 camel 大小写</span><span class="sxs-lookup"><span data-stu-id="0ffbe-222">Convert all property names to camel case</span></span>](#use-camel-case-for-all-json-property-names)
* [<span data-ttu-id="0ffbe-223">实现自定义属性命名策略</span><span class="sxs-lookup"><span data-stu-id="0ffbe-223">Implement a custom property naming policy</span></span>](#use-a-custom-json-property-naming-policy)
* [<span data-ttu-id="0ffbe-224">将字典键转换为 camel 大小写</span><span class="sxs-lookup"><span data-stu-id="0ffbe-224">Convert dictionary keys to camel case</span></span>](#camel-case-dictionary-keys)
* [<span data-ttu-id="0ffbe-225">将枚举转换为字符串和 camel 大小写</span><span class="sxs-lookup"><span data-stu-id="0ffbe-225">Convert enums to strings and camel case</span></span>](#enums-as-strings)

<span data-ttu-id="0ffbe-226">对于需要对 JSON 属性名称和值进行特殊处理的其他方案，可以[实现自定义转换器](system-text-json-converters-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-226">For other scenarios that require special handling of JSON property names and values, you can [implement custom converters](system-text-json-converters-how-to.md).</span></span>

### <a name="customize-individual-property-names"></a><span data-ttu-id="0ffbe-227">自定义单个属性名称</span><span class="sxs-lookup"><span data-stu-id="0ffbe-227">Customize individual property names</span></span>

<span data-ttu-id="0ffbe-228">若要设置单个属性的名称，请使用 [[JsonPropertyName]](xref::::no-loc(System.Text.Json):::.Serialization.JsonPropertyNameAttribute) 特性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-228">To set the name of individual properties, use the [[JsonPropertyName]](xref::::no-loc(System.Text.Json):::.Serialization.JsonPropertyNameAttribute) attribute.</span></span>

<span data-ttu-id="0ffbe-229">下面是要进行序列化的示例类型和生成的 JSON：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-229">Here's an example type to serialize and resulting JSON:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithPropertyNameAttribute)]

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "Wind": 35
}
```

<span data-ttu-id="0ffbe-230">此特性设置的属性名称：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-230">The property name set by this attribute:</span></span>

* <span data-ttu-id="0ffbe-231">同时适用于两个方向（序列化和反序列化）。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-231">Applies in both directions, for serialization and deserialization.</span></span>
* <span data-ttu-id="0ffbe-232">优先于属性命名策略。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-232">Takes precedence over property naming policies.</span></span>

### <a name="use-camel-case-for-all-json-property-names"></a><span data-ttu-id="0ffbe-233">对所有 JSON 属性名称使用 camel 大小写</span><span class="sxs-lookup"><span data-stu-id="0ffbe-233">Use camel case for all JSON property names</span></span>

<span data-ttu-id="0ffbe-234">若要对所有 JSON 属性名称使用 camel 大小写，请将 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> 设置为 `JsonNamingPolicy.CamelCase`，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-234">To use camel case for all JSON property names, set <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> to `JsonNamingPolicy.CamelCase`, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundTripCamelCasePropertyNames.cs?name=Serialize)]

<span data-ttu-id="0ffbe-235">下面是要进行序列化的示例类和 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-235">Here's an example class to serialize and JSON output:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithPropertyNameAttribute)]

```json
{
  "date": "2019-08-01T00:00:00-07:00",
  "temperatureCelsius": 25,
  "summary": "Hot",
  "Wind": 35
}
```

<span data-ttu-id="0ffbe-236">camel 大小写属性命名策略：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-236">The camel case property naming policy:</span></span>

* <span data-ttu-id="0ffbe-237">适用于序列化和反序列化。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-237">Applies to serialization and deserialization.</span></span>
* <span data-ttu-id="0ffbe-238">由 `[JsonPropertyName]` 特性替代。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-238">Is overridden by `[JsonPropertyName]` attributes.</span></span> <span data-ttu-id="0ffbe-239">这便是示例中的 JSON 属性名称 `Wind` 不是 camel 大小写的原因。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-239">This is why the JSON property name `Wind` in the example is not camel case.</span></span>

### <a name="use-a-custom-json-property-naming-policy"></a><span data-ttu-id="0ffbe-240">使用自定义 JSON 属性命名策略</span><span class="sxs-lookup"><span data-stu-id="0ffbe-240">Use a custom JSON property naming policy</span></span>

<span data-ttu-id="0ffbe-241">若要使用自定义 JSON 属性命名策略，请创建派生自 <xref::::no-loc(System.Text.Json):::.JsonNamingPolicy> 的类，并替代 <xref::::no-loc(System.Text.Json):::.JsonNamingPolicy.ConvertName%2A> 方法，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-241">To use a custom JSON property naming policy, create a class that derives from <xref::::no-loc(System.Text.Json):::.JsonNamingPolicy> and override the <xref::::no-loc(System.Text.Json):::.JsonNamingPolicy.ConvertName%2A> method, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/UpperCaseNamingPolicy.cs)]

<span data-ttu-id="0ffbe-242">然后，将 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> 属性设置为命名策略类的实例：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-242">Then set the <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> property to an instance of your naming policy class:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripPropertyNamingPolicy.cs?name=SnippetSerialize)]

<span data-ttu-id="0ffbe-243">下面是要进行序列化的示例类和 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-243">Here's an example class to serialize and JSON output:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithPropertyNameAttribute)]

```json
{
  "DATE": "2019-08-01T00:00:00-07:00",
  "TEMPERATURECELSIUS": 25,
  "SUMMARY": "Hot",
  "Wind": 35
}
```

<span data-ttu-id="0ffbe-244">JSON 属性命名策略：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-244">The JSON property naming policy:</span></span>

* <span data-ttu-id="0ffbe-245">适用于序列化和反序列化。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-245">Applies to serialization and deserialization.</span></span>
* <span data-ttu-id="0ffbe-246">由 `[JsonPropertyName]` 特性替代。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-246">Is overridden by `[JsonPropertyName]` attributes.</span></span> <span data-ttu-id="0ffbe-247">这便是示例中的 JSON 属性名称 `Wind` 不是大写的原因。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-247">This is why the JSON property name `Wind` in the example is not upper case.</span></span>

### <a name="camel-case-dictionary-keys"></a><span data-ttu-id="0ffbe-248">Camel 大小写字典键</span><span class="sxs-lookup"><span data-stu-id="0ffbe-248">Camel case dictionary keys</span></span>

<span data-ttu-id="0ffbe-249">如果要序列化的对象的属性为 `Dictionary<string,TValue>` 类型，则 `string` 键可转换为 camel 大小写。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-249">If a property of an object to be serialized is of type `Dictionary<string,TValue>`, the `string` keys can be converted to camel case.</span></span> <span data-ttu-id="0ffbe-250">为此，请将 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.DictionaryKeyPolicy> 设置为 `JsonNamingPolicy.CamelCase`，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-250">To do that, set <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.DictionaryKeyPolicy> to `JsonNamingPolicy.CamelCase`, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeCamelCaseDictionaryKeys.cs?name=SnippetSerialize)]

<span data-ttu-id="0ffbe-251">使用名为 `TemperatureRanges` 且具有键值对 `"ColdMinTemp", 20` 和 `"HotMinTemp", 40` 的字典序列化对象会产生类似于以下示例的 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-251">Serializing an object with a dictionary named `TemperatureRanges` that has key-value pairs `"ColdMinTemp", 20` and `"HotMinTemp", 40` would result in JSON output like the following example:</span></span>

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

<span data-ttu-id="0ffbe-252">字典键的 camel 大小写命名策略仅适用于序列化。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-252">The camel case naming policy for dictionary keys applies to serialization only.</span></span> <span data-ttu-id="0ffbe-253">如果对字典进行反序列化，即使为 `DictionaryKeyPolicy`指定 `JsonNamingPolicy.CamelCase`，键也会与 JSON 文件匹配。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-253">If you deserialize a dictionary, the keys will match the JSON file even if you specify `JsonNamingPolicy.CamelCase` for the `DictionaryKeyPolicy`.</span></span>

### <a name="enums-as-strings"></a><span data-ttu-id="0ffbe-254">作为字符串的枚举</span><span class="sxs-lookup"><span data-stu-id="0ffbe-254">Enums as strings</span></span>

<span data-ttu-id="0ffbe-255">默认情况下，枚举会序列化为数字。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-255">By default, enums are serialized as numbers.</span></span> <span data-ttu-id="0ffbe-256">若要将枚举名称序列化为字符串，请使用 <xref::::no-loc(System.Text.Json):::.Serialization.JsonStringEnumConverter>。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-256">To serialize enum names as strings, use the <xref::::no-loc(System.Text.Json):::.Serialization.JsonStringEnumConverter>.</span></span>

<span data-ttu-id="0ffbe-257">例如，假设需要序列化以下具有枚举的类：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-257">For example, suppose you need to serialize the following class that has an enum:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithEnum)]

<span data-ttu-id="0ffbe-258">如果 Summary 为 `Hot`，则默认情况下序列化的 JSON 具有数值 3：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-258">If the Summary is `Hot`, by default the serialized JSON has the numeric value 3:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": 3
}
```

<span data-ttu-id="0ffbe-259">下面的示例代码序列化枚举名称(而不是数值)，并将名称转换为 camel 大小写：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-259">The following sample code serializes the enum names instead of the numeric values, and converts the names to camel case:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripEnumAsString.cs?name=SnippetSerialize)]

<span data-ttu-id="0ffbe-260">生成的 JSON 类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-260">The resulting JSON looks like the following example:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "hot"
}
```

<span data-ttu-id="0ffbe-261">还可以反序列化枚举字符串名称，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-261">Enum string names can be deserialized as well, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripEnumAsString.cs?name=SnippetDeserialize)]

## <a name="ignore-properties"></a><span data-ttu-id="0ffbe-262">忽略属性</span><span class="sxs-lookup"><span data-stu-id="0ffbe-262">Ignore properties</span></span>

<span data-ttu-id="0ffbe-263">默认情况下，所有公共属性都会序列化。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-263">By default, all public properties are serialized.</span></span> <span data-ttu-id="0ffbe-264">如果不想让某些属性出现在 JSON 输出中，则有几个选项可用。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-264">If you don't want some of them to appear in the JSON output, you have several options.</span></span> <span data-ttu-id="0ffbe-265">本部分介绍如何忽略：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-265">This section explains how to ignore:</span></span>

::: zone pivot="dotnet-5-0"

* [<span data-ttu-id="0ffbe-266">单个属性</span><span class="sxs-lookup"><span data-stu-id="0ffbe-266">Individual properties</span></span>](#ignore-individual-properties)
* [<span data-ttu-id="0ffbe-267">所有只读属性</span><span class="sxs-lookup"><span data-stu-id="0ffbe-267">All read-only properties</span></span>](#ignore-all-read-only-properties)
* [<span data-ttu-id="0ffbe-268">所有 null 值属性</span><span class="sxs-lookup"><span data-stu-id="0ffbe-268">All null-value properties</span></span>](#ignore-all-null-value-properties)
* [<span data-ttu-id="0ffbe-269">所有默认值属性</span><span class="sxs-lookup"><span data-stu-id="0ffbe-269">All default-value properties</span></span>](#ignore-all-default-value-properties)
::: zone-end

::: zone pivot="dotnet-core-3-1"

* [<span data-ttu-id="0ffbe-270">单个属性</span><span class="sxs-lookup"><span data-stu-id="0ffbe-270">Individual properties</span></span>](#ignore-individual-properties)
* [<span data-ttu-id="0ffbe-271">所有只读属性</span><span class="sxs-lookup"><span data-stu-id="0ffbe-271">All read-only properties</span></span>](#ignore-all-read-only-properties)
* [<span data-ttu-id="0ffbe-272">所有 null 值属性</span><span class="sxs-lookup"><span data-stu-id="0ffbe-272">All null-value properties</span></span>](#ignore-all-null-value-properties)
::: zone-end

### <a name="ignore-individual-properties"></a><span data-ttu-id="0ffbe-273">忽略单个属性</span><span class="sxs-lookup"><span data-stu-id="0ffbe-273">Ignore individual properties</span></span>

<span data-ttu-id="0ffbe-274">若要忽略单个属性，请使用 [[JsonIgnore]](xref::::no-loc(System.Text.Json):::.Serialization.JsonIgnoreAttribute) 特性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-274">To ignore individual properties, use the [[JsonIgnore]](xref::::no-loc(System.Text.Json):::.Serialization.JsonIgnoreAttribute) attribute.</span></span>

<span data-ttu-id="0ffbe-275">下面是要进行序列化的示例类型和 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-275">Here's an example type to serialize and JSON output:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithIgnoreAttribute)]

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
}
```

::: zone pivot="dotnet-5-0"
<span data-ttu-id="0ffbe-276">可以通过设置 [[JsonIgnore]](xref::::no-loc(System.Text.Json):::.Serialization.JsonIgnoreAttribute) 特性的 `Condition` 属性来指定条件排除。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-276">You can specify conditional exclusion by setting the [[JsonIgnore]](xref::::no-loc(System.Text.Json):::.Serialization.JsonIgnoreAttribute) attribute's `Condition` property.</span></span> <span data-ttu-id="0ffbe-277"><xref::::no-loc(System.Text.Json):::.Serialization.JsonIgnoreCondition> 枚举提供下列选项：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-277">The <xref::::no-loc(System.Text.Json):::.Serialization.JsonIgnoreCondition> enum provides the following options:</span></span>

* <span data-ttu-id="0ffbe-278">`Always` - 始终忽略属性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-278">`Always` - The property is always ignored.</span></span> <span data-ttu-id="0ffbe-279">如果未指定 `Condition`，则假设此选项。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-279">If no `Condition` is specified, this option is assumed.</span></span>
* <span data-ttu-id="0ffbe-280">`Never` - 无论 `DefaultIgnoreCondition`、`IgnoreReadOnlyProperties` 和 `IgnoreReadOnlyFields` 全局设置如何，始终序列化和反序列化属性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-280">`Never` - The property is always serialized and deserialized, regardless of the `DefaultIgnoreCondition`, `IgnoreReadOnlyProperties`, and `IgnoreReadOnlyFields` global settings.</span></span>
* <span data-ttu-id="0ffbe-281">`WhenWritingDefault` - 如果属性是引用类型 `null` 或值类型 `default`，则在序列化中忽略属性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-281">`WhenWritingDefault` - The property is ignored on serialization if it's a reference type `null` or a value type `default`.</span></span>
* <span data-ttu-id="0ffbe-282">`WhenWritingNull` - 如果属性是引用类型 `null`，则在序列化中忽略属性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-282">`WhenWritingNull` - The property is ignored on serialization if it's a reference type `null`.</span></span>

<span data-ttu-id="0ffbe-283">下面的示例说明 [[JsonIgnore]](xref::::no-loc(System.Text.Json):::.Serialization.JsonIgnoreAttribute) 特性的 `Condition` 属性的用法：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-283">The following example illustrates use of the [[JsonIgnore]](xref::::no-loc(System.Text.Json):::.Serialization.JsonIgnoreAttribute) attribute's `Condition` property:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/JsonIgnoreAttributeExample.cs" highlight="10,13,16":::
::: zone-end

### <a name="ignore-all-read-only-properties"></a><span data-ttu-id="0ffbe-284">忽略所有只读属性</span><span class="sxs-lookup"><span data-stu-id="0ffbe-284">Ignore all read-only properties</span></span>

<span data-ttu-id="0ffbe-285">如果属性包含公共 getter 而不是公共 setter，则属性为只读。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-285">A property is read-only if it contains a public getter but not a public setter.</span></span> <span data-ttu-id="0ffbe-286">若要在序列化时忽略所有只读属性，请将 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.IgnoreReadOnlyProperties?displayProperty=nameWithType> 设置为 `true`，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-286">To ignore all read-only properties when serializing, set the <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.IgnoreReadOnlyProperties?displayProperty=nameWithType> to `true`, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeExcludeReadOnlyProperties.cs?name=SnippetSerialize)]

<span data-ttu-id="0ffbe-287">下面是要进行序列化的示例类型和 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-287">Here's an example type to serialize and JSON output:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithROProperty)]

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
}
```

<span data-ttu-id="0ffbe-288">此选项仅适用于序列化。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-288">This option applies only to serialization.</span></span> <span data-ttu-id="0ffbe-289">在反序列化过程中，默认情况下会忽略只读属性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-289">During deserialization, read-only properties are ignored by default.</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="0ffbe-290">此选项仅适用于属性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-290">This option applies only to properties.</span></span> <span data-ttu-id="0ffbe-291">若要在[序列化字段](#include-fields)时忽略只读字段，请使用 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.IgnoreReadOnlyFields%2A?displayProperty=nameWithType> 全局设置。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-291">To ignore read-only fields when [serializing fields](#include-fields), use the <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.IgnoreReadOnlyFields%2A?displayProperty=nameWithType> global setting.</span></span>
::: zone-end

### <a name="ignore-all-null-value-properties"></a><span data-ttu-id="0ffbe-292">忽略所有 null 值属性</span><span class="sxs-lookup"><span data-stu-id="0ffbe-292">Ignore all null-value properties</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="0ffbe-293">若要忽略所有 null 值属性，请将 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.DefaultIgnoreCondition> 属性设置为 <xref::::no-loc(System.Text.Json):::.Serialization.JsonIgnoreCondition.WhenWritingNull>，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-293">To ignore all null-value properties, set the <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.DefaultIgnoreCondition> property to <xref::::no-loc(System.Text.Json):::.Serialization.JsonIgnoreCondition.WhenWritingNull>, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/IgnoreNullOnSerialize.cs" highlight="28":::

::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="0ffbe-294">若要在序列化时忽略所有 null 值属性，请将 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.IgnoreNullValues> 属性设置为 `true`，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-294">To ignore all null-value properties when serializing, set the <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.IgnoreNullValues> property to `true`, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeExcludeNullValueProperties.cs?name=SnippetSerialize)]

<span data-ttu-id="0ffbe-295">下面是要进行序列化的示例对象和 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-295">Here's an example object to serialize and JSON output:</span></span>

|<span data-ttu-id="0ffbe-296">Property</span><span class="sxs-lookup"><span data-stu-id="0ffbe-296">Property</span></span> |<span data-ttu-id="0ffbe-297">“值”</span><span class="sxs-lookup"><span data-stu-id="0ffbe-297">Value</span></span>  |
|---------|---------|
| <span data-ttu-id="0ffbe-298">日期</span><span class="sxs-lookup"><span data-stu-id="0ffbe-298">Date</span></span>    | <span data-ttu-id="0ffbe-299">8/1/2019 12:00:00 AM -07:00</span><span class="sxs-lookup"><span data-stu-id="0ffbe-299">8/1/2019 12:00:00 AM -07:00</span></span>|
| <span data-ttu-id="0ffbe-300">TemperatureCelsius</span><span class="sxs-lookup"><span data-stu-id="0ffbe-300">TemperatureCelsius</span></span>| <span data-ttu-id="0ffbe-301">25</span><span class="sxs-lookup"><span data-stu-id="0ffbe-301">25</span></span> |
| <span data-ttu-id="0ffbe-302">总结</span><span class="sxs-lookup"><span data-stu-id="0ffbe-302">Summary</span></span>| <span data-ttu-id="0ffbe-303">null</span><span class="sxs-lookup"><span data-stu-id="0ffbe-303">null</span></span>|

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25
}
```

::: zone-end

### <a name="ignore-all-default-value-properties"></a><span data-ttu-id="0ffbe-304">忽略所有默认值属性</span><span class="sxs-lookup"><span data-stu-id="0ffbe-304">Ignore all default-value properties</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="0ffbe-305">若要防止对值类型属性中的默认值进行序列化，请将 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.DefaultIgnoreCondition> 属性设置为 <xref::::no-loc(System.Text.Json):::.Serialization.JsonIgnoreCondition.WhenWritingDefault>，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-305">To prevent serialization of default values in value type properties, set the <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.DefaultIgnoreCondition> property to <xref::::no-loc(System.Text.Json):::.Serialization.JsonIgnoreCondition.WhenWritingDefault>, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/IgnoreValueDefaultOnSerialize.cs" highlight="28":::
::: zone-end

<span data-ttu-id="0ffbe-306">`WhenWritingDefault` 设置还会阻止对 null 值引用类型属性进行序列化。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-306">The `WhenWritingDefault` setting also prevents serialization of null-value reference type properties.</span></span>

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="0ffbe-307">在 .NET Core 3.1 的 :::no-loc(System.Text.Json)::: 中，无内置方式来阻止对值类型为默认值的属性进行序列化。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-307">There is no built-in way to prevent serialization of properties with value type defaults in :::no-loc(System.Text.Json)::: in .NET Core 3.1.</span></span>
::: zone-end

## <a name="customize-character-encoding"></a><span data-ttu-id="0ffbe-308">自定义字符编码</span><span class="sxs-lookup"><span data-stu-id="0ffbe-308">Customize character encoding</span></span>

<span data-ttu-id="0ffbe-309">默认情况下，序列化程序会转义所有非 ASCII 字符。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-309">By default, the serializer escapes all non-ASCII characters.</span></span>  <span data-ttu-id="0ffbe-310">即，会将它们替换为 `\uxxxx`，其中 `xxxx` 为字符的 Unicode 代码。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-310">That is, it replaces them with `\uxxxx` where `xxxx` is the Unicode code of the character.</span></span>  <span data-ttu-id="0ffbe-311">例如，如果 `Summary` 属性设置为西里尔文 жарко，则 `WeatherForecast` 对象会进行序列化，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-311">For example, if the `Summary` property is set to Cyrillic жарко, the `WeatherForecast` object is serialized as shown in this example:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "\u0436\u0430\u0440\u043A\u043E"
}
```

### <a name="serialize-language-character-sets"></a><span data-ttu-id="0ffbe-312">序列化语言字符集</span><span class="sxs-lookup"><span data-stu-id="0ffbe-312">Serialize language character sets</span></span>

<span data-ttu-id="0ffbe-313">若要序列化一种或多种语言的字符集而不进行转义，请在创建 <xref:System.Text.Encodings.Web.JavaScriptEncoder?displayProperty=fullName> 的实例时指定 [Unicode 范围](xref:System.Text.Unicode.UnicodeRanges)，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-313">To serialize the character set(s) of one or more languages without escaping, specify [Unicode range(s)](xref:System.Text.Unicode.UnicodeRanges) when creating an instance of <xref:System.Text.Encodings.Web.JavaScriptEncoder?displayProperty=fullName>, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs?name=SnippetUsings)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs?name=SnippetLanguageSets)]

<span data-ttu-id="0ffbe-314">此代码不转义西里尔文或希腊语字符。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-314">This code doesn't escape Cyrillic or Greek characters.</span></span> <span data-ttu-id="0ffbe-315">如果 `Summary` 属性设置为西里尔文 жарко，则 `WeatherForecast` 对象会进行序列化，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-315">If the `Summary` property is set to Cyrillic жарко, the `WeatherForecast` object is serialized as shown in this example:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "жарко"
}
```

<span data-ttu-id="0ffbe-316">若要序列化所有语言集而不进行转义，请使用 <xref:System.Text.Unicode.UnicodeRanges.All?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-316">To serialize all language sets without escaping, use <xref:System.Text.Unicode.UnicodeRanges.All?displayProperty=nameWithType>.</span></span>

### <a name="serialize-specific-characters"></a><span data-ttu-id="0ffbe-317">序列化特定字符</span><span class="sxs-lookup"><span data-stu-id="0ffbe-317">Serialize specific characters</span></span>

<span data-ttu-id="0ffbe-318">一种替代方法是指定要允许的单个字符，而不进行转义。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-318">An alternative is to specify individual characters that you want to allow through without being escaped.</span></span> <span data-ttu-id="0ffbe-319">下面的示例仅序列化 жарко 的前两个字符：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-319">The following example serializes only the first two characters of жарко:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs?name=SnippetUsings)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs?name=SnippetSelectedCharacters)]

<span data-ttu-id="0ffbe-320">下面是前面代码生成的 JSON 的示例：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-320">Here's an example of JSON produced by the preceding code:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "жа\u0440\u043A\u043E"
}
```

### <a name="serialize-all-characters"></a><span data-ttu-id="0ffbe-321">序列化所有字符</span><span class="sxs-lookup"><span data-stu-id="0ffbe-321">Serialize all characters</span></span>

<span data-ttu-id="0ffbe-322">若要最大程度地减少转义，可以使用 <xref:System.Text.Encodings.Web.JavaScriptEncoder.UnsafeRelaxedJsonEscaping?displayProperty=nameWithType>，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-322">To minimize escaping you can use <xref:System.Text.Encodings.Web.JavaScriptEncoder.UnsafeRelaxedJsonEscaping?displayProperty=nameWithType>, as shown in the following example:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs?name=SnippetUsings)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs?name=SnippetUnsafeRelaxed)]

> [!CAUTION]
> <span data-ttu-id="0ffbe-323">与默认编码器相比，`UnsafeRelaxedJsonEscaping` 编码器在允许字符通过而不进行转义方面更加宽松：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-323">Compared to the default encoder, the `UnsafeRelaxedJsonEscaping` encoder is more permissive about allowing characters to pass through unescaped:</span></span>
>
> * <span data-ttu-id="0ffbe-324">它不转义 HTML 敏感字符，如 `<`、`>`、`&` 和 `'`。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-324">It doesn't escape HTML-sensitive characters such as `<`, `>`, `&`, and `'`.</span></span>
> * <span data-ttu-id="0ffbe-325">它不提供任何针对 XSS 或信息泄露攻击（如客户端和服务器在字符集方面不一致所可能导致的攻击）的额外深度防御保护。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-325">It doesn't offer any additional defense-in-depth protections against XSS or information disclosure attacks, such as those which might result from the client and server disagreeing on the *charset*.</span></span>
>
> <span data-ttu-id="0ffbe-326">仅当知道客户端将生成的有效负载解释为 UTF-8 编码的 JSON 时，才使用不安全编码器。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-326">Use the unsafe encoder only when it's known that the client will be interpreting the resulting payload as UTF-8 encoded JSON.</span></span> <span data-ttu-id="0ffbe-327">例如，如果服务器在发送响应标头 `Content-Type: application/json; charset=utf-8`，则可以使用它。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-327">For example, you can use it if the server is sending the response header `Content-Type: application/json; charset=utf-8`.</span></span> <span data-ttu-id="0ffbe-328">永远不允许将原始 `UnsafeRelaxedJsonEscaping` 输出发出到 HTML 页面或 `<script>` 元素。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-328">Never allow the raw `UnsafeRelaxedJsonEscaping` output to be emitted into an HTML page or a `<script>` element.</span></span>

## <a name="serialize-properties-of-derived-classes"></a><span data-ttu-id="0ffbe-329">序列化派生类的属性</span><span class="sxs-lookup"><span data-stu-id="0ffbe-329">Serialize properties of derived classes</span></span>

<span data-ttu-id="0ffbe-330">不支持多态类型层次结构的序列化。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-330">Serialization of a polymorphic type hierarchy is not supported.</span></span> <span data-ttu-id="0ffbe-331">例如，如果属性定义为接口或抽象类，则即使运行时类型具有其他属性，也只会序列化对接口或抽象类定义的属性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-331">For example, if a property is defined as an interface or an abstract class, only the properties defined on the interface or abstract class are serialized, even if the runtime type has additional properties.</span></span> <span data-ttu-id="0ffbe-332">此部分中介绍了此行为的例外情况。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-332">The exceptions to this behavior are explained in this section.</span></span>

<span data-ttu-id="0ffbe-333">例如，假设有一个 `WeatherForecast` 类和一个派生类 `WeatherForecastDerived`：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-333">For example, suppose you have a `WeatherForecast` class and a derived class `WeatherForecastDerived`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFDerived)]

<span data-ttu-id="0ffbe-334">并且假设 `Serialize` 方法的类型参数在编译时为 `WeatherForecast`：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-334">And suppose the type argument of the `Serialize` method at compile time is `WeatherForecast`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs?name=SnippetSerializeDefault)]

<span data-ttu-id="0ffbe-335">在这种情况下，即使 `weatherForecast` 对象实际上是 `WeatherForecastDerived` 对象，也不会序列化 `WindSpeed` 属性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-335">In this scenario, the `WindSpeed` property is not serialized even if the `weatherForecast` object is actually a `WeatherForecastDerived` object.</span></span> <span data-ttu-id="0ffbe-336">仅序列化基类属性：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-336">Only the base class properties are serialized:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

<span data-ttu-id="0ffbe-337">此行为旨在帮助防止在运行时创建的派生类型中发生意外数据泄露。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-337">This behavior is intended to help prevent accidental exposure of data in a derived runtime-created type.</span></span>

<span data-ttu-id="0ffbe-338">若要序列化前面示例中派生类型的属性，请使用以下方法之一：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-338">To serialize the properties of the derived type in the preceding example, use one of the following approaches:</span></span>

* <span data-ttu-id="0ffbe-339">调用 <xref::::no-loc(System.Text.Json):::.JsonSerializer.Serialize%2A> 的重载，以便在运行时指定类型：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-339">Call an overload of <xref::::no-loc(System.Text.Json):::.JsonSerializer.Serialize%2A> that lets you specify the type at run time:</span></span>

  [!code-csharp[](snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs?name=SnippetSerializeGetType)]

* <span data-ttu-id="0ffbe-340">将要序列化的对象声明为 `object`。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-340">Declare the object to be serialized as `object`.</span></span>

  [!code-csharp[](snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs?name=SnippetSerializeObject)]

<span data-ttu-id="0ffbe-341">在前面的示例方案中，这两种方法都会使 `WindSpeed` 属性包含在 JSON 输出中：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-341">In the preceding example scenario, both approaches cause the `WindSpeed` property to be included in the JSON output:</span></span>

```json
{
  "WindSpeed": 35,
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

> [!IMPORTANT]
> <span data-ttu-id="0ffbe-342">这些方法只为要序列化的根对象提供多态序列化，而不为该根对象的属性提供。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-342">These approaches provide polymorphic serialization only for the root object to be serialized, not for properties of that root object.</span></span>

<span data-ttu-id="0ffbe-343">如果将较低级别的对象定义为类型 `object`，则可以对它们进行多态序列化。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-343">You can get polymorphic serialization for lower-level objects if you define them as type `object`.</span></span> <span data-ttu-id="0ffbe-344">例如，假设 `WeatherForecast` 类具有一个名为 `PreviousForecast` 的属性，该属性可以定义为类型 `WeatherForecast` 或 `object`：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-344">For example, suppose your `WeatherForecast` class has a property named `PreviousForecast` that can be defined as type `WeatherForecast` or `object`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithPrevious)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithPreviousAsObject)]

<span data-ttu-id="0ffbe-345">如果 `PreviousForecast` 属性包含 `WeatherForecastDerived` 的实例：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-345">If the `PreviousForecast` property contains an instance of `WeatherForecastDerived`:</span></span>

* <span data-ttu-id="0ffbe-346">序列化 `WeatherForecastWithPrevious` 的 JSON 输出不包含 `WindSpeed`。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-346">The JSON output from serializing `WeatherForecastWithPrevious` **doesn't include** `WindSpeed`.</span></span>
* <span data-ttu-id="0ffbe-347">序列化 `WeatherForecastWithPreviousAsObject` 的 JSON 输出包含 `WindSpeed`。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-347">The JSON output from serializing `WeatherForecastWithPreviousAsObject` **includes** `WindSpeed`.</span></span>

<span data-ttu-id="0ffbe-348">若要序列化 `WeatherForecastWithPreviousAsObject`，无需调用 `Serialize<object>` 或 `GetType`，因为根对象不是可能属于派生类型的对象。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-348">To serialize `WeatherForecastWithPreviousAsObject`, it isn't necessary to call `Serialize<object>` or `GetType` because the root object isn't the one that may be of a derived type.</span></span> <span data-ttu-id="0ffbe-349">下面的代码示例不调用 `Serialize<object>` 或 `GetType`：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-349">The following code example doesn't call `Serialize<object>` or `GetType`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs?name=SnippetSerializeSecondLevel)]

<span data-ttu-id="0ffbe-350">前面的代码会正确地序列化 `WeatherForecastWithPreviousAsObject`：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-350">The preceding code correctly serializes `WeatherForecastWithPreviousAsObject`:</span></span>

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

<span data-ttu-id="0ffbe-351">将属性定义为 `object` 的相同方法适用于接口。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-351">The same approach of defining properties as `object` works with interfaces.</span></span> <span data-ttu-id="0ffbe-352">假设具有以下接口和实现，并且要使用包含实现实例的属性序列化类：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-352">Suppose you have the following interface and implementation, and you want to serialize a class with properties that contain implementation instances:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/IForecast.cs)]

<span data-ttu-id="0ffbe-353">序列化 `Forecasts` 的实例时，只有 `Tuesday` 显示 `WindSpeed` 属性，因为 `Tuesday` 定义为 `object`：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-353">When you serialize an instance of `Forecasts`, only `Tuesday` shows the `WindSpeed` property, because `Tuesday` is defined as `object`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs?name=SnippetSerializeInterface)]

<span data-ttu-id="0ffbe-354">下面的示例显示前面代码生成的 JSON：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-354">The following example shows the JSON that results from the preceding code:</span></span>

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

<span data-ttu-id="0ffbe-355">有关多态序列化的详细信息，以及有关反序列化的信息，请参阅[如何从 :::no-loc(Newtonsoft.Json)::: 迁移到 :::no-loc(System.Text.Json):::](system-text-json-migrate-from-newtonsoft-how-to.md#polymorphic-serialization)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-355">For more information about polymorphic **serialization** , and for information about **deserialization** , see [How to migrate from :::no-loc(Newtonsoft.Json)::: to :::no-loc(System.Text.Json):::](system-text-json-migrate-from-newtonsoft-how-to.md#polymorphic-serialization).</span></span>

## <a name="allow-comments-and-trailing-commas"></a><span data-ttu-id="0ffbe-356">允许注释和尾随逗号</span><span class="sxs-lookup"><span data-stu-id="0ffbe-356">Allow comments and trailing commas</span></span>

<span data-ttu-id="0ffbe-357">默认情况下，JSON 中不允许使用注释和尾随逗号。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-357">By default, comments and trailing commas are not allowed in JSON.</span></span> <span data-ttu-id="0ffbe-358">若要在 JSON 中允许注释，请将 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.ReadCommentHandling?displayProperty=nameWithType> 属性设置为 `JsonCommentHandling.Skip`。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-358">To allow comments in the JSON, set the <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.ReadCommentHandling?displayProperty=nameWithType> property to `JsonCommentHandling.Skip`.</span></span>
<span data-ttu-id="0ffbe-359">若要允许尾随逗号，请将 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.AllowTrailingCommas?displayProperty=nameWithType> 属性设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-359">And to allow trailing commas, set the <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.AllowTrailingCommas?displayProperty=nameWithType> property to `true`.</span></span> <span data-ttu-id="0ffbe-360">下面的示例演示如何允许这两者：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-360">The following example shows how to allow both:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/DeserializeCommasComments.cs?name=SnippetDeserialize)]

<span data-ttu-id="0ffbe-361">下面是包含注释和尾随逗号的示例 JSON：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-361">Here's example JSON with comments and a trailing comma:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25, // Fahrenheit 77
  "Summary": "Hot", /* Zharko */
}
```

## <a name="case-insensitive-property-matching"></a><span data-ttu-id="0ffbe-362">不区分大小写的属性匹配</span><span class="sxs-lookup"><span data-stu-id="0ffbe-362">Case-insensitive property matching</span></span>

<span data-ttu-id="0ffbe-363">默认情况下，反序列化会查找 JSON 与目标对象属性之间区分大小写的属性名称匹配。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-363">By default, deserialization looks for case-sensitive property name matches between JSON and the target object properties.</span></span> <span data-ttu-id="0ffbe-364">若要更改该行为，请将 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.PropertyNameCaseInsensitive?displayProperty=nameWithType> 设置为 `true`：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-364">To change that behavior, set <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.PropertyNameCaseInsensitive?displayProperty=nameWithType> to `true`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/DeserializeCaseInsensitive.cs?name=SnippetDeserialize)]

<span data-ttu-id="0ffbe-365">下面是具有 camel 大小写属性名称的示例 JSON。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-365">Here's example JSON with camel case property names.</span></span> <span data-ttu-id="0ffbe-366">它可以反序列化为具有帕斯卡拼写法属性名称的以下类型。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-366">It can be deserialized into the following type that has Pascal case property names.</span></span>

```json
{
  "date": "2019-08-01T00:00:00-07:00",
  "temperatureCelsius": 25,
  "summary": "Hot",
}
```

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

## <a name="handle-overflow-json"></a><span data-ttu-id="0ffbe-367">处理溢出 JSON</span><span class="sxs-lookup"><span data-stu-id="0ffbe-367">Handle overflow JSON</span></span>

<span data-ttu-id="0ffbe-368">反序列化时，可能会在 JSON 中收到不是由目标类型的属性表示的数据。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-368">While deserializing, you might receive data in the JSON that is not represented by properties of the target type.</span></span> <span data-ttu-id="0ffbe-369">例如，假设目标类型如下：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-369">For example, suppose your target type is this:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

<span data-ttu-id="0ffbe-370">要反序列化的 JSON 如下：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-370">And the JSON to be deserialized is this:</span></span>

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

<span data-ttu-id="0ffbe-371">如果将显示的 JSON 反序列化为显示的类型，则 `DatesAvailable` 和 `SummaryWords` 属性无处可去，会丢失。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-371">If you deserialize the JSON shown into the type shown, the `DatesAvailable` and `SummaryWords` properties have nowhere to go and are lost.</span></span> <span data-ttu-id="0ffbe-372">若要捕获额外数据（如这些属性），请将 [[JsonExtensionData]](xref::::no-loc(System.Text.Json):::.Serialization.JsonExtensionDataAttribute) 特性应用于类型 `Dictionary<string,object>` 或 `Dictionary<string,JsonElement>` 的属性：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-372">To capture extra data such as these properties, apply the [[JsonExtensionData]](xref::::no-loc(System.Text.Json):::.Serialization.JsonExtensionDataAttribute) attribute to a property of type `Dictionary<string,object>` or `Dictionary<string,JsonElement>`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithExtensionData)]

<span data-ttu-id="0ffbe-373">将前面显示的 JSON 反序列化为此示例类型时，额外数据会成为 `ExtensionData` 属性的键值对：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-373">When you deserialize the JSON shown earlier into this sample type, the extra data becomes key-value pairs of the `ExtensionData` property:</span></span>

|<span data-ttu-id="0ffbe-374">Property</span><span class="sxs-lookup"><span data-stu-id="0ffbe-374">Property</span></span> |<span data-ttu-id="0ffbe-375">值</span><span class="sxs-lookup"><span data-stu-id="0ffbe-375">Value</span></span>  |<span data-ttu-id="0ffbe-376">说明</span><span class="sxs-lookup"><span data-stu-id="0ffbe-376">Notes</span></span>  |
|---------|---------|---------|
| <span data-ttu-id="0ffbe-377">日期</span><span class="sxs-lookup"><span data-stu-id="0ffbe-377">Date</span></span>    | <span data-ttu-id="0ffbe-378">8/1/2019 12:00:00 AM -07:00</span><span class="sxs-lookup"><span data-stu-id="0ffbe-378">8/1/2019 12:00:00 AM -07:00</span></span>||
| <span data-ttu-id="0ffbe-379">TemperatureCelsius</span><span class="sxs-lookup"><span data-stu-id="0ffbe-379">TemperatureCelsius</span></span>| <span data-ttu-id="0ffbe-380">0</span><span class="sxs-lookup"><span data-stu-id="0ffbe-380">0</span></span> | <span data-ttu-id="0ffbe-381">区分大小写的不匹配（JSON 中的 `temperatureCelsius`），因此未设置属性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-381">Case-sensitive mismatch (`temperatureCelsius` in the JSON), so the property isn't set.</span></span> |
| <span data-ttu-id="0ffbe-382">总结</span><span class="sxs-lookup"><span data-stu-id="0ffbe-382">Summary</span></span> | <span data-ttu-id="0ffbe-383">热</span><span class="sxs-lookup"><span data-stu-id="0ffbe-383">Hot</span></span> ||
| <span data-ttu-id="0ffbe-384">ExtensionData</span><span class="sxs-lookup"><span data-stu-id="0ffbe-384">ExtensionData</span></span> | <span data-ttu-id="0ffbe-385">temperatureCelsius：25</span><span class="sxs-lookup"><span data-stu-id="0ffbe-385">temperatureCelsius: 25</span></span> |<span data-ttu-id="0ffbe-386">因为大小写不匹配，所以此 JSON 属性是额外属性，会成为字典中的键值对。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-386">Since the case didn't match, this JSON property is an extra and becomes a key-value pair in the dictionary.</span></span>|
|| <span data-ttu-id="0ffbe-387">DatesAvailable：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-387">DatesAvailable:</span></span><br>  <span data-ttu-id="0ffbe-388">8/1/2019 12:00:00 AM -07:00</span><span class="sxs-lookup"><span data-stu-id="0ffbe-388">8/1/2019 12:00:00 AM -07:00</span></span><br><span data-ttu-id="0ffbe-389">8/2/2019 12:00:00 AM -07:00</span><span class="sxs-lookup"><span data-stu-id="0ffbe-389">8/2/2019 12:00:00 AM -07:00</span></span> |<span data-ttu-id="0ffbe-390">JSON 中的额外属性会成为键值对，将数组作为值对象。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-390">Extra property from the JSON becomes a key-value pair, with an array as the value object.</span></span>|
| |<span data-ttu-id="0ffbe-391">SummaryWords：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-391">SummaryWords:</span></span><br><span data-ttu-id="0ffbe-392">酷</span><span class="sxs-lookup"><span data-stu-id="0ffbe-392">Cool</span></span><br><span data-ttu-id="0ffbe-393">Windy</span><span class="sxs-lookup"><span data-stu-id="0ffbe-393">Windy</span></span><br><span data-ttu-id="0ffbe-394">Humid</span><span class="sxs-lookup"><span data-stu-id="0ffbe-394">Humid</span></span> |<span data-ttu-id="0ffbe-395">JSON 中的额外属性会成为键值对，将数组作为值对象。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-395">Extra property from the JSON becomes a key-value pair, with an array as the value object.</span></span>|

<span data-ttu-id="0ffbe-396">序列化目标对象时，扩展数据键值对会成为 JSON 属性，就如同它们处于传入 JSON 中一样：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-396">When the target object is serialized, the extension data key value pairs become JSON properties just as they were in the incoming JSON:</span></span>

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

<span data-ttu-id="0ffbe-397">请注意，`ExtensionData` 属性名称不会出现在 JSON 中。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-397">Notice that the `ExtensionData` property name doesn't appear in the JSON.</span></span> <span data-ttu-id="0ffbe-398">此行为使 JSON 可以进行往返，而不会丢失任何不会以其他方式进行反序列化的额外数据。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-398">This behavior lets the JSON make a round trip without losing any extra data that otherwise wouldn't be deserialized.</span></span>

## <a name="preserve-references-and-handle-circular-references"></a><span data-ttu-id="0ffbe-399">保留引用并处理循环引用</span><span class="sxs-lookup"><span data-stu-id="0ffbe-399">Preserve references and handle circular references</span></span>

::: zone pivot="dotnet-5-0"

<span data-ttu-id="0ffbe-400">若要保留引用并处理循环引用，请将 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.ReferenceHandler%2A> 设置为 <xref::::no-loc(System.Text.Json):::.Serialization.ReferenceHandler.Preserve%2A>。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-400">To preserve references and handle circular references, set <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.ReferenceHandler%2A> to <xref::::no-loc(System.Text.Json):::.Serialization.ReferenceHandler.Preserve%2A>.</span></span> <span data-ttu-id="0ffbe-401">此设置会导致以下行为：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-401">This setting causes the following behavior:</span></span>

* <span data-ttu-id="0ffbe-402">在序列化时：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-402">On serialize:</span></span>

  <span data-ttu-id="0ffbe-403">编写复杂类型时，序列化程序还会写入元数据属性（`$id`、`$values` 和 `$ref`）。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-403">When writing complex types, the serializer also writes metadata properties (`$id`, `$values`, and `$ref`).</span></span>

* <span data-ttu-id="0ffbe-404">在反序列化时：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-404">On deserialize:</span></span>

  <span data-ttu-id="0ffbe-405">需要元数据（虽然不是必需的），并且反序列化程序会尝试理解它。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-405">Metadata is expected (although not mandatory), and the deserializer tries to understand it.</span></span>

<span data-ttu-id="0ffbe-406">下面的代码演示 `Preserve` 属性的用法。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-406">The following code illustrates use of the `Preserve` setting.</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/PreserveReferences.cs" highlight="34":::

<span data-ttu-id="0ffbe-407">此功能不能用于保留值类型或不可变类型。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-407">This feature can't be used to preserve value types or immutable types.</span></span> <span data-ttu-id="0ffbe-408">在反序列化时，将在读取整个有效负载后创建不可变类型的实例。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-408">On deserialization, the instance of an immutable type is created after the entire payload is read.</span></span> <span data-ttu-id="0ffbe-409">因此，如果对同一实例的引用出现在 JSON 有效负载中，则无法对其进行反序列化。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-409">So it would be impossible to deserialize the same instance if a reference to it appears within the JSON payload.</span></span>

<span data-ttu-id="0ffbe-410">对于值类型、不可变类型和数组，不会序列化任何引用元数据。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-410">For value types, immutable types, and arrays, no reference metadata is serialized.</span></span> <span data-ttu-id="0ffbe-411">反序列化时，如果发现 `$ref` 或 `$id`，则会引发异常。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-411">On deserialization, an exception is thrown if `$ref` or `$id` is found.</span></span> <span data-ttu-id="0ffbe-412">但是，值类型忽略 `$id`（对于集合，则为 `$values`），以便可以反序列化使用 :::no-loc(Newtonsoft.Json)::: 序列化的有效负载。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-412">However, value types ignore `$id` (and `$values` in the case of collections) to make it possible to deserialize payloads that were serialized by using :::no-loc(Newtonsoft.Json):::.</span></span>  <span data-ttu-id="0ffbe-413">:::no-loc(Newtonsoft.Json)::: 为此类类型序列化元数据。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-413">:::no-loc(Newtonsoft.Json)::: does serialize metadata for such types.</span></span>

<span data-ttu-id="0ffbe-414">为了确定对象是否相等，:::no-loc(System.Text.Json)::: 在比较两个对象实例时使用引用相等性 (<xref:System.Object.ReferenceEquals(System.Object,System.Object)?displayProperty=nameWithType>) 而不是值相等性 (<xref:System.Object.Equals(System.Object)?displayProperty=nameWithType> 的 <xref:System.Collections.Generic.ReferenceEqualityComparer.Instance%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-414">To determine if objects are equal, :::no-loc(System.Text.Json)::: uses <xref:System.Collections.Generic.ReferenceEqualityComparer.Instance%2A?displayProperty=nameWithType>, which uses reference equality (<xref:System.Object.ReferenceEquals(System.Object,System.Object)?displayProperty=nameWithType>) instead of value equality (<xref:System.Object.Equals(System.Object)?displayProperty=nameWithType> when comparing two object instances.</span></span>

<span data-ttu-id="0ffbe-415">有关如何序列化和反序列化引用的详细信息，请参阅 <xref::::no-loc(System.Text.Json):::.Serialization.ReferenceHandler.Preserve%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-415">For more information about how references are serialized and deserialized, see <xref::::no-loc(System.Text.Json):::.Serialization.ReferenceHandler.Preserve%2A?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="0ffbe-416"><xref::::no-loc(System.Text.Json):::.Serialization.ReferenceResolver> 类定义在序列化和反序列化过程中保留引用的行为。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-416">The <xref::::no-loc(System.Text.Json):::.Serialization.ReferenceResolver> class defines the behavior of preserving references on serialization and deserialization.</span></span> <span data-ttu-id="0ffbe-417">创建派生类以指定自定义行为。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-417">Create a derived class to specify custom behavior.</span></span> <span data-ttu-id="0ffbe-418">有关示例，请参阅 [GuidReferenceResolver](https://github.com/dotnet/docs/blob/9d5e88edbd7f12be463775ffebbf07ac8415fe18/docs/standard/serialization/snippets/system-text-json-how-to-5-0/csharp/GuidReferenceResolverExample.cs)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-418">For an example, see [GuidReferenceResolver](https://github.com/dotnet/docs/blob/9d5e88edbd7f12be463775ffebbf07ac8415fe18/docs/standard/serialization/snippets/system-text-json-how-to-5-0/csharp/GuidReferenceResolverExample.cs).</span></span>

::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="0ffbe-419">.NET Core 3.1 中的 :::no-loc(System.Text.Json)::: 仅支持按值进行进行序列化，并对循环引用引发异常。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-419">:::no-loc(System.Text.Json)::: in .NET Core 3.1 only supports serialization by value and throws an exception for circular references.</span></span>
::: zone-end

## <a name="allow-or-write-numbers-in-quotes"></a><span data-ttu-id="0ffbe-420">允许或写入带引号的数字</span><span class="sxs-lookup"><span data-stu-id="0ffbe-420">Allow or write numbers in quotes</span></span>

::: zone pivot="dotnet-5-0"

<span data-ttu-id="0ffbe-421">某些序列化程序将数字编码为 JSON 字符串（括在引号中）。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-421">Some serializers encode numbers as JSON strings (surrounded by quotes).</span></span> <span data-ttu-id="0ffbe-422">例如，`{"DegreesCelsius":"23"}` 而非 `{"DegreesCelsius":23}`。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-422">For example: `{"DegreesCelsius":"23"}` instead of `{"DegreesCelsius":23}`.</span></span> <span data-ttu-id="0ffbe-423">若要在整个输入对象图中序列化带引号的数字或接受带引号的数字，请设置 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.NumberHandling%2A?displayProperty=nameWithType>，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-423">To serialize numbers in quotes or accept numbers in quotes across the entire input object graph, set <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.NumberHandling%2A?displayProperty=nameWithType> as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/QuotedNumbers.cs" highlight="27-28":::

<span data-ttu-id="0ffbe-424">在通过 ASP.NET Core 间接使用 :::no-loc(System.Text.Json)::: 时，反序列化时允许使用带引号的数字，因为 ASP.NET Core 指定 [Web 默认选项](xref::::no-loc(System.Text.Json):::.JsonSerializerDefaults.Web)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-424">When you use :::no-loc(System.Text.Json)::: indirectly through ASP.NET Core, quoted numbers are allowed when deserializing because ASP.NET Core specifies [web default options](xref::::no-loc(System.Text.Json):::.JsonSerializerDefaults.Web).</span></span>

<span data-ttu-id="0ffbe-425">若要允许或写入特定属性、字段或类型的带引号的数字，请使用 [[JsonNumberHandling]](xref::::no-loc(System.Text.Json):::.Serialization.JsonNumberHandlingAttribute) 特性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-425">To allow or write quoted numbers for specific properties, fields, or types, use the [[JsonNumberHandling]](xref::::no-loc(System.Text.Json):::.Serialization.JsonNumberHandlingAttribute) attribute.</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="0ffbe-426">.NET Core 3.1 中的 :::no-loc(System.Text.Json)::: 不支持序列化或反序列化用引号引起来的数字。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-426">:::no-loc(System.Text.Json)::: in .NET Core 3.1 doesn't support serializing or deserializing numbers surrounded by quotation marks.</span></span> <span data-ttu-id="0ffbe-427">有关详细信息，请参阅[允许或写入带引号的数字](system-text-json-migrate-from-newtonsoft-how-to.md#allow-or-write-numbers-in-quotes)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-427">For more information, see [Allow or write numbers in quotes](system-text-json-migrate-from-newtonsoft-how-to.md#allow-or-write-numbers-in-quotes).</span></span>
::: zone-end

## <a name="immutable-types-and-records"></a><span data-ttu-id="0ffbe-428">不可变类型和记录</span><span class="sxs-lookup"><span data-stu-id="0ffbe-428">Immutable types and Records</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="0ffbe-429">:::no-loc(System.Text.Json)::: 可以使用参数化构造函数，这可以反序列化不可变的类或结构。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-429">:::no-loc(System.Text.Json)::: can use a parameterized constructor, which makes it possible to deserialize an immutable class or struct.</span></span> <span data-ttu-id="0ffbe-430">对于类，如果唯一构造函数是参数化的构造函数，则将使用该构造函数。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-430">For a class, if the only constructor is a parameterized one, that constructor will be used.</span></span> <span data-ttu-id="0ffbe-431">对于结构或包含多个构造函数的类，通过应用 [[JsonConstructor]](xref::::no-loc(System.Text.Json):::.Serialization.JsonConstructorAttribute.%23ctor%2A) 特性来指定要使用的构造函数。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-431">For a struct, or a class with multiple constructors, specify the one to use by applying the [[JsonConstructor]](xref::::no-loc(System.Text.Json):::.Serialization.JsonConstructorAttribute.%23ctor%2A) attribute.</span></span> <span data-ttu-id="0ffbe-432">如果未使用该特性，则始终使用公共无参数构造函数（如果存在）。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-432">When the attribute is not used, a public parameterless constructor is always used if present.</span></span> <span data-ttu-id="0ffbe-433">该特性只能与公共构造函数一起使用。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-433">The attribute can only be used with public constructors.</span></span> <span data-ttu-id="0ffbe-434">以下示例使用 `[JsonConstructor]` 特性：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-434">The following example uses the `[JsonConstructor]` attribute:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/ImmutableTypes.cs" highlight="13":::

<span data-ttu-id="0ffbe-435">还支持 C# 9 记录，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-435">Records in C# 9 are also supported, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/Records.cs":::

<span data-ttu-id="0ffbe-436">对于因其所有属性资源库都是非公共的而不可变的类型，请参阅以下部分，了解[非公共属性访问器](#non-public-property-accessors)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-436">For types that are immutable because all their property setters are non-public, see the following section about [non-public property accessors](#non-public-property-accessors).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="0ffbe-437">.NET Core 3.1 不支持 `JsonConstructorAttribute` 和 C# 9 记录。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-437">`JsonConstructorAttribute` and C# 9 Record support aren't available in .NET Core 3.1.</span></span>
::: zone-end

## <a name="non-public-property-accessors"></a><span data-ttu-id="0ffbe-438">非公共属性访问器</span><span class="sxs-lookup"><span data-stu-id="0ffbe-438">Non-public property accessors</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="0ffbe-439">若要允许使用非公共属性访问器，请使用 [[JsonInclude]](xref::::no-loc(System.Text.Json):::.Serialization.JsonIncludeAttribute) 特性，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-439">To enable use of a non-public property accessor, use the [[JsonInclude]](xref::::no-loc(System.Text.Json):::.Serialization.JsonIncludeAttribute) attribute, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/NonPublicAccessors.cs" highlight="12,15":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="0ffbe-440">.NET Core 3.1 不支持非公共属性访问器。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-440">Non-public property accessors are not supported in .NET Core 3.1.</span></span> <span data-ttu-id="0ffbe-441">有关详细信息，请参阅[从 :::no-loc(Newtonsoft.Json)::: 迁移一文](system-text-json-migrate-from-newtonsoft-how-to.md#non-public-property-setters-and-getters)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-441">For more information, see [the Migrate from :::no-loc(Newtonsoft.Json)::: article](system-text-json-migrate-from-newtonsoft-how-to.md#non-public-property-setters-and-getters).</span></span>
::: zone-end

## <a name="copy-jsonserializeroptions"></a><span data-ttu-id="0ffbe-442">复制 JsonSerializerOptions</span><span class="sxs-lookup"><span data-stu-id="0ffbe-442">Copy JsonSerializerOptions</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="0ffbe-443">存在 [JsonSerializerOptions constructor](xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.%23ctor(:::no-loc(System.Text.Json):::.JsonSerializerOptions)) ，可让你使用与现有实例相同的选项来创建新的实例，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-443">There is a [JsonSerializerOptions constructor](xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.%23ctor(:::no-loc(System.Text.Json):::.JsonSerializerOptions)) that lets you create a new instance with the same options as an existing instance, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/CopyOptions.cs" highlight="29":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="0ffbe-444">使用现有实例的 `JsonSerializerOptions` 构造函数在 .NET Core 3.1 中不可用。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-444">A `JsonSerializerOptions` constructor that takes an existing instance is not available in .NET Core 3.1.</span></span>
::: zone-end

## <a name="web-defaults-for-jsonserializeroptions"></a><span data-ttu-id="0ffbe-445">JsonSerializerOptions 的 Web 默认值</span><span class="sxs-lookup"><span data-stu-id="0ffbe-445">Web defaults for JsonSerializerOptions</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="0ffbe-446">下面是具有 Web 应用不同默认值的选项：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-446">Here are the options that have different defaults for web apps:</span></span>

* <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.PropertyNameCaseInsensitive%2A> = `true`
* <xref::::no-loc(System.Text.Json):::.JsonNamingPolicy> = <xref::::no-loc(System.Text.Json):::.JsonNamingPolicy.CamelCase>
* <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.NumberHandling%2A> = <xref::::no-loc(System.Text.Json):::.Serialization.JsonNumberHandling.AllowReadingFromString>

<span data-ttu-id="0ffbe-447">存在 [JsonSerializerOptions constructor](xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.%23ctor(:::no-loc(System.Text.Json):::.JsonSerializerDefaults)?view=net-5.0&preserve-view=true)，可让你通过 ASP.NET Core 对 Web 应用使用的默认选项创建新的实例，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-447">There's a [JsonSerializerOptions constructor](xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.%23ctor(:::no-loc(System.Text.Json):::.JsonSerializerDefaults)?view=net-5.0&preserve-view=true) that lets you create a new instance with the default options that ASP.NET Core uses for web apps, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/OptionsDefaults.cs" highlight="24":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="0ffbe-448">下面是具有 Web 应用不同默认值的选项：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-448">Here are the options that have different defaults for web apps:</span></span>

* <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.PropertyNameCaseInsensitive%2A> = `true`
* <xref::::no-loc(System.Text.Json):::.JsonNamingPolicy> = <xref::::no-loc(System.Text.Json):::.JsonNamingPolicy.CamelCase>

<span data-ttu-id="0ffbe-449">指定一组默认值的 `JsonSerializerOptions` 构造函数在 .NET Core 3.1 中不可用。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-449">A `JsonSerializerOptions` constructor that specifies a set of defaults is not available in .NET Core 3.1.</span></span>
::: zone-end

## <a name="httpclient-and-httpcontent-extension-methods"></a><span data-ttu-id="0ffbe-450">HttpClient 和 HttpContent 扩展方法</span><span class="sxs-lookup"><span data-stu-id="0ffbe-450">HttpClient and HttpContent extension methods</span></span>

::: zone pivot="dotnet-5-0"

<span data-ttu-id="0ffbe-451">序列化和反序列化来自网络的 JSON 有效负载是常见的操作。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-451">Serializing and deserializing JSON payloads from the network are common operations.</span></span> <span data-ttu-id="0ffbe-452">[HttpClient](xref:System.Net.Http.Json.HttpClientJsonExtensions) 和 [HttpContent](xref:System.Net.Http.Json.HttpContentJsonExtensions) 上的扩展方法允许在单个代码行中执行这些操作。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-452">Extension methods on [HttpClient](xref:System.Net.Http.Json.HttpClientJsonExtensions) and [HttpContent](xref:System.Net.Http.Json.HttpContentJsonExtensions) let you do these operations in a single line of code.</span></span> <span data-ttu-id="0ffbe-453">这些扩展方法使用 [JsonSerializerOptions 的 Web 默认值](#web-defaults-for-jsonserializeroptions)。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-453">These extension methods use [web defaults for JsonSerializerOptions](#web-defaults-for-jsonserializeroptions).</span></span>

<span data-ttu-id="0ffbe-454">以下示例说明了 <xref:System.Net.Http.Json.HttpClientJsonExtensions.GetFromJsonAsync%2A?displayProperty=nameWithType> 和 <xref:System.Net.Http.Json.HttpClientJsonExtensions.PostAsJsonAsync%2A?displayProperty=nameWithType> 的用法：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-454">The following example illustrates use of <xref:System.Net.Http.Json.HttpClientJsonExtensions.GetFromJsonAsync%2A?displayProperty=nameWithType> and <xref:System.Net.Http.Json.HttpClientJsonExtensions.PostAsJsonAsync%2A?displayProperty=nameWithType>:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/HttpClientExtensionMethods.cs" highlight="23,30":::

<span data-ttu-id="0ffbe-455">此外还有 [HttpContent](xref:System.Net.Http.Json.HttpContentJsonExtensions) 上的 :::no-loc(System.Text.Json)::: 的扩展方法。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-455">There are also extension methods for :::no-loc(System.Text.Json)::: on [HttpContent](xref:System.Net.Http.Json.HttpContentJsonExtensions).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="0ffbe-456">`HttpClient` 和 `HttpContent` 上的扩展方法在 .NET Core 3.1 的 :::no-loc(System.Text.Json)::: 中不可用。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-456">Extension methods on `HttpClient` and `HttpContent` are not available in :::no-loc(System.Text.Json)::: in .NET Core 3.1.</span></span>
::: zone-end

## <a name="utf8jsonreader-utf8jsonwriter-and-jsondocument"></a><span data-ttu-id="0ffbe-457">Utf8JsonReader、Utf8JsonWriter 和 JsonDocument</span><span class="sxs-lookup"><span data-stu-id="0ffbe-457">Utf8JsonReader, Utf8JsonWriter, and JsonDocument</span></span>

<span data-ttu-id="0ffbe-458"><xref::::no-loc(System.Text.Json):::.Utf8JsonReader?displayProperty=fullName> 是面向 UTF-8 编码 JSON 文本的一个高性能、低分配的只进读取器，从 `ReadOnlySpan<byte>` 或 `ReadOnlySequence<byte>` 读取信息。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-458"><xref::::no-loc(System.Text.Json):::.Utf8JsonReader?displayProperty=fullName> is a high-performance, low allocation, forward-only reader for UTF-8 encoded JSON text, read from a `ReadOnlySpan<byte>` or `ReadOnlySequence<byte>`.</span></span> <span data-ttu-id="0ffbe-459">`Utf8JsonReader` 是一种低级类型，可用于生成自定义分析器和反序列化程序。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-459">The `Utf8JsonReader` is a low-level type that can be used to build custom parsers and deserializers.</span></span> <span data-ttu-id="0ffbe-460"><xref::::no-loc(System.Text.Json):::.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> 方法在后台使用 `Utf8JsonReader`。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-460">The <xref::::no-loc(System.Text.Json):::.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> method uses `Utf8JsonReader` under the covers.</span></span>

<span data-ttu-id="0ffbe-461"><xref::::no-loc(System.Text.Json):::.Utf8JsonWriter?displayProperty=fullName> 是一种高性能方式，从常见 .NET 类型（例如，`String`、`Int32` 和 `DateTime`）编写 UTF-8 编码的 JSON 文本。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-461"><xref::::no-loc(System.Text.Json):::.Utf8JsonWriter?displayProperty=fullName> is a high-performance way to write UTF-8 encoded JSON text from common .NET types like `String`, `Int32`, and `DateTime`.</span></span> <span data-ttu-id="0ffbe-462">该编写器是一种低级类型，可用于生成自定义序列化程序。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-462">The writer is a low-level type that can be used to build custom serializers.</span></span> <span data-ttu-id="0ffbe-463"><xref::::no-loc(System.Text.Json):::.JsonSerializer.Serialize%2A?displayProperty=nameWithType> 方法在后台使用 `Utf8JsonWriter`。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-463">The <xref::::no-loc(System.Text.Json):::.JsonSerializer.Serialize%2A?displayProperty=nameWithType> method uses `Utf8JsonWriter` under the covers.</span></span>

<span data-ttu-id="0ffbe-464"><xref::::no-loc(System.Text.Json):::.JsonDocument?displayProperty=fullName> 提供使用 `Utf8JsonReader` 生成只读文档对象模型 (DOM) 的功能。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-464"><xref::::no-loc(System.Text.Json):::.JsonDocument?displayProperty=fullName> provides the ability to build a read-only Document Object Model (DOM) by using `Utf8JsonReader`.</span></span> <span data-ttu-id="0ffbe-465">DOM 提供对 JSON 有效负载中的数据的随机访问。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-465">The DOM provides random access to data in a JSON payload.</span></span> <span data-ttu-id="0ffbe-466">可以通过 <xref::::no-loc(System.Text.Json):::.JsonElement> 类型访问构成有效负载的 JSON 元素。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-466">The JSON elements that compose the payload can be accessed via the <xref::::no-loc(System.Text.Json):::.JsonElement> type.</span></span> <span data-ttu-id="0ffbe-467">`JsonElement` 类型提供数组和对象枚举器，以及用于将 JSON 文本转换为常见 .NET 类型的 API。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-467">The `JsonElement` type provides array and object enumerators along with APIs to convert JSON text to common .NET types.</span></span> <span data-ttu-id="0ffbe-468">`JsonDocument` 公开了 <xref::::no-loc(System.Text.Json):::.JsonDocument.RootElement> 属性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-468">`JsonDocument` exposes a <xref::::no-loc(System.Text.Json):::.JsonDocument.RootElement> property.</span></span>

<span data-ttu-id="0ffbe-469">以下部分演示如何使用这些工具读取和写入 JSON。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-469">The following sections show how to use these tools for reading and writing JSON.</span></span>

## <a name="use-jsondocument-for-access-to-data"></a><span data-ttu-id="0ffbe-470">使用 JsonDocument 访问数据</span><span class="sxs-lookup"><span data-stu-id="0ffbe-470">Use JsonDocument for access to data</span></span>

<span data-ttu-id="0ffbe-471">下面的示例演示如何使用 <xref::::no-loc(System.Text.Json):::.JsonDocument> 类来随机访问 JSON 字符串中的数据：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-471">The following example shows how to use the <xref::::no-loc(System.Text.Json):::.JsonDocument> class for random access to data in a JSON string:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/JsonDocumentDataAccess.cs?name=SnippetAverageGrades1)]

<span data-ttu-id="0ffbe-472">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-472">The preceding code:</span></span>

* <span data-ttu-id="0ffbe-473">假设要分析的 JSON 处于名为 `jsonString` 的字符串中。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-473">Assumes the JSON to analyze is in a string named `jsonString`.</span></span>
* <span data-ttu-id="0ffbe-474">对 `Students` 数组中具有 `Grade` 属性的对象计算平均成绩。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-474">Calculates an average grade for objects in a `Students` array that have a `Grade` property.</span></span>
* <span data-ttu-id="0ffbe-475">为没有成绩的学生分配默认成绩 70。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-475">Assigns a default grade of 70 for students who don't have a grade.</span></span>
* <span data-ttu-id="0ffbe-476">通过在每次迭代时使 `count` 变量递增来对学生进行计数。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-476">Counts students by incrementing a `count` variable with each iteration.</span></span> <span data-ttu-id="0ffbe-477">一种替代方法是调用 <xref::::no-loc(System.Text.Json):::.JsonElement.GetArrayLength%2A>，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-477">An alternative is to call <xref::::no-loc(System.Text.Json):::.JsonElement.GetArrayLength%2A>, as shown in the following example:</span></span>

  [!code-csharp[](snippets/system-text-json-how-to/csharp/JsonDocumentDataAccess.cs?name=SnippetAverageGrades2)]

<span data-ttu-id="0ffbe-478">下面是此代码处理的 JSON 示例：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-478">Here's an example of the JSON that this code processes:</span></span>

[!code-json[](snippets/system-text-json-how-to/csharp/GradesPrettyPrint.json)]

## <a name="use-jsondocument-to-write-json"></a><span data-ttu-id="0ffbe-479">使用 JsonDocument 写入 JSON</span><span class="sxs-lookup"><span data-stu-id="0ffbe-479">Use JsonDocument to write JSON</span></span>

<span data-ttu-id="0ffbe-480">下面的示例演示如何通过 <xref::::no-loc(System.Text.Json):::.JsonDocument> 写入 JSON：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-480">The following example shows how to write JSON from a <xref::::no-loc(System.Text.Json):::.JsonDocument>:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/JsonDocumentWriteJson.cs?name=SnippetSerialize)]

<span data-ttu-id="0ffbe-481">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-481">The preceding code:</span></span>

* <span data-ttu-id="0ffbe-482">读取 JSON 文件，将数据加载到 `JsonDocument` 中，并将格式化（进行了优质打印的）JSON 写入文件。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-482">Reads a JSON file, loads the data into a `JsonDocument`, and writes formatted (pretty-printed) JSON to a file.</span></span>
* <span data-ttu-id="0ffbe-483">使用 <xref::::no-loc(System.Text.Json):::.JsonDocumentOptions> 可指定允许但会忽略输入 JSON 中的注释。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-483">Uses <xref::::no-loc(System.Text.Json):::.JsonDocumentOptions> to specify that comments in the input JSON are allowed but ignored.</span></span>
* <span data-ttu-id="0ffbe-484">完成后，对编写器调用 <xref::::no-loc(System.Text.Json):::.Utf8JsonWriter.Flush%2A>。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-484">When finished, calls <xref::::no-loc(System.Text.Json):::.Utf8JsonWriter.Flush%2A> on the writer.</span></span> <span data-ttu-id="0ffbe-485">一种替代方法是让编写器在释放时自动刷新。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-485">An alternative is to let the writer autoflush when it's disposed.</span></span>

<span data-ttu-id="0ffbe-486">下面是要由示例代码处理的 JSON 输入的示例：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-486">Here's an example of JSON input to be processed by the example code:</span></span>

[!code-json[](snippets/system-text-json-how-to/csharp/Grades.json)]

<span data-ttu-id="0ffbe-487">结果是以下进行了优质打印的 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-487">The result is the following pretty-printed JSON output:</span></span>

[!code-json[](snippets/system-text-json-how-to/csharp/GradesPrettyPrint.json)]

## <a name="use-utf8jsonwriter"></a><span data-ttu-id="0ffbe-488">使用 Utf8JsonWriter</span><span class="sxs-lookup"><span data-stu-id="0ffbe-488">Use Utf8JsonWriter</span></span>

<span data-ttu-id="0ffbe-489">下面的示例演示如何使用 <xref::::no-loc(System.Text.Json):::.Utf8JsonWriter> 类：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-489">The following example shows how to use the <xref::::no-loc(System.Text.Json):::.Utf8JsonWriter> class:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/Utf8WriterToStream.cs?name=SnippetSerialize)]

## <a name="use-utf8jsonreader"></a><span data-ttu-id="0ffbe-490">使用 Utf8JsonReader</span><span class="sxs-lookup"><span data-stu-id="0ffbe-490">Use Utf8JsonReader</span></span>

<span data-ttu-id="0ffbe-491">下面的示例演示如何使用 <xref::::no-loc(System.Text.Json):::.Utf8JsonReader> 类：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-491">The following example shows how to use the <xref::::no-loc(System.Text.Json):::.Utf8JsonReader> class:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/Utf8ReaderFromBytes.cs?name=SnippetDeserialize)]

<span data-ttu-id="0ffbe-492">前面的代码假设 `jsonUtf8` 变量是包含有效 JSON（编码为 UTF-8）的字节数组。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-492">The preceding code assumes that the `jsonUtf8` variable is a byte array that contains valid JSON, encoded as UTF-8.</span></span>

### <a name="filter-data-using-utf8jsonreader"></a><span data-ttu-id="0ffbe-493">使用 Utf8JsonReader 筛选数据</span><span class="sxs-lookup"><span data-stu-id="0ffbe-493">Filter data using Utf8JsonReader</span></span>

<span data-ttu-id="0ffbe-494">下面的示例演示如何同步读取文件并搜索值：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-494">The following example shows how to read a file synchronously and search for a value:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/Utf8ReaderFromFile.cs)]

<span data-ttu-id="0ffbe-495">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-495">The preceding code:</span></span>

* <span data-ttu-id="0ffbe-496">假设 JSON 包含一个对象数组，并且每个对象都可能包含一个字符串类型的“name”属性。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-496">Assumes the JSON contains an array of objects and each object may contain a "name" property of type string.</span></span>
* <span data-ttu-id="0ffbe-497">对对象以及以“University”结尾的属性值进行计数。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-497">Counts objects and "name" property values that end with "University".</span></span>
* <span data-ttu-id="0ffbe-498">假设文件编码为 UTF-16，并将它转码为 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-498">Assumes the file is encoded as UTF-16 and transcodes it into UTF-8.</span></span> <span data-ttu-id="0ffbe-499">可以使用以下代码，将编码为 UTF-8 的文件直接读入 `ReadOnlySpan<byte>`：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-499">A file encoded as UTF-8 can be read directly into a `ReadOnlySpan<byte>`, by using the following code:</span></span>

  ```csharp
  ReadOnlySpan<byte> jsonReadOnlySpan = File.ReadAllBytes(fileName);
  ```

  <span data-ttu-id="0ffbe-500">如果文件包含 UTF-8 字节顺序标记 (BOM)，请在将字节传递给 `Utf8JsonReader` 之前将它删除，因为读取器需要文本。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-500">If the file contains a UTF-8 byte order mark (BOM), remove it before passing the bytes to the `Utf8JsonReader`, since the reader expects text.</span></span> <span data-ttu-id="0ffbe-501">否则，BOM 被视为无效 JSON，读取器将引发异常。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-501">Otherwise, the BOM is considered invalid JSON, and the reader throws an exception.</span></span>

<span data-ttu-id="0ffbe-502">下面是前面的代码可以读取的 JSON 示例。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-502">Here's a JSON sample that the preceding code can read.</span></span> <span data-ttu-id="0ffbe-503">生成的摘要消息为“2 out of 4 have names that end with 'University'”：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-503">The resulting summary message is "2 out of 4 have names that end with 'University'":</span></span>

[!code-json[](snippets/system-text-json-how-to/csharp/Universities.json)]

### <a name="read-from-a-stream-using-utf8jsonreader"></a><span data-ttu-id="0ffbe-504">使用 Utf8JsonReader 从流中读取</span><span class="sxs-lookup"><span data-stu-id="0ffbe-504">Read from a stream using Utf8JsonReader</span></span>

<span data-ttu-id="0ffbe-505">当读取大型文件（例如，1 GB 或更大的文件）时，你可能希望避免一次性将整个文件加载到内存中。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-505">When reading a large file (a gigabyte or more in size, for example), you might want to avoid having to load the entire file into memory at once.</span></span> <span data-ttu-id="0ffbe-506">此时，可以使用 <xref:System.IO.FileStream>。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-506">For this scenario, you can use a <xref:System.IO.FileStream>.</span></span>

<span data-ttu-id="0ffbe-507">使用 `Utf8JsonReader` 从流中读取时，适用以下规则：</span><span class="sxs-lookup"><span data-stu-id="0ffbe-507">When using the `Utf8JsonReader` to read from a stream, the following rules apply:</span></span>

* <span data-ttu-id="0ffbe-508">包含部分 JSON 有效负载的缓冲区必须至少与其中的最大 JSON 令牌一样大，以便读取器可以推进进度。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-508">The buffer containing the partial JSON payload must be at least as large as the largest JSON token within it so that the reader can make forward progress.</span></span>
* <span data-ttu-id="0ffbe-509">缓冲区的大小必须至少与 JSON 中的最大空格序列一样大。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-509">The buffer must be at least as large as the largest sequence of white space within the JSON.</span></span>
* <span data-ttu-id="0ffbe-510">读取器不会跟踪已读取的数据，直到它完全读取 JSON 有效负载中的下一个 <xref::::no-loc(System.Text.Json):::.Utf8JsonReader.TokenType%2A>。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-510">The reader doesn't keep track of the data it has read until it completely reads the next <xref::::no-loc(System.Text.Json):::.Utf8JsonReader.TokenType%2A> in the JSON payload.</span></span> <span data-ttu-id="0ffbe-511">因此，当缓冲区中有剩余字节时，必须再次将它们传递给读取器。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-511">So when there are bytes left over in the buffer, you have to pass them to the reader again.</span></span> <span data-ttu-id="0ffbe-512">你可以使用 <xref::::no-loc(System.Text.Json):::.Utf8JsonReader.BytesConsumed%2A> 来确定剩余的字节数。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-512">You can use <xref::::no-loc(System.Text.Json):::.Utf8JsonReader.BytesConsumed%2A> to determine how many bytes are left over.</span></span>

<span data-ttu-id="0ffbe-513">下面的代码演示了如何从流中读取。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-513">The following code illustrates how to read from a stream.</span></span> <span data-ttu-id="0ffbe-514">本示例显示了 <xref:System.IO.MemoryStream>。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-514">The example shows a <xref:System.IO.MemoryStream>.</span></span> <span data-ttu-id="0ffbe-515">类似的代码将使用 <xref:System.IO.FileStream>，当 `FileStream` 在开头包含 UTF-8 BOM 时除外。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-515">Similar code will work with a <xref:System.IO.FileStream>, except when the `FileStream` contains a UTF-8 BOM at the start.</span></span> <span data-ttu-id="0ffbe-516">在这种情况下，需要先从缓冲区中去除这三个字节，然后再将剩余字节传递到 `Utf8JsonReader`。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-516">In that case, you need to strip those three bytes from the buffer before passing the remaining bytes to the `Utf8JsonReader`.</span></span> <span data-ttu-id="0ffbe-517">否则，读取器将引发异常，因为 BOM 不被视为 JSON 的有效部分。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-517">Otherwise the reader would throw an exception, since the BOM is not considered a valid part of the JSON.</span></span>

<span data-ttu-id="0ffbe-518">示例代码从 4 KB 缓冲区开始，每当发现大小不足以容纳完整的 JSON 令牌（必须容纳完整的令牌，读取器才能推动处理 JSON 有效负载）时，就会使缓冲区大小成倍增加。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-518">The sample code starts with a 4KB buffer and doubles the buffer size each time it finds that the size is not large enough to fit a complete JSON token, which is required for the reader to make forward progress on the JSON payload.</span></span> <span data-ttu-id="0ffbe-519">仅当设置的初始缓冲区非常小（例如 10 个字节）时，代码片段中提供的 JSON 示例才会触发缓冲区大小增加。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-519">The JSON sample provided in the snippet triggers a buffer size increase only if you set a very small initial buffer size, for example, 10 bytes.</span></span> <span data-ttu-id="0ffbe-520">如果将初始缓冲区大小设置为 10，则 `Console.WriteLine` 语句会说明缓冲区大小增加的原因和影响。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-520">If you set the initial buffer size to 10, the `Console.WriteLine` statements illustrate the cause and effect of buffer size increases.</span></span> <span data-ttu-id="0ffbe-521">在初始缓冲区大小为 4KB 时，每个 `Console.WriteLine` 都会显示整个示例 JSON，并且不必增加缓冲区大小。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-521">At the 4KB initial buffer size, the entire sample JSON is shown by each `Console.WriteLine`, and the buffer size never has to be increased.</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/Utf8ReaderPartialRead.cs)]

<span data-ttu-id="0ffbe-522">前面的示例未对缓冲区大小的增长设置任何限制。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-522">The preceding example sets no limit to how large the buffer can grow.</span></span> <span data-ttu-id="0ffbe-523">如果令牌大小太大，则代码可能会失败，并出现 <xref:System.OutOfMemoryException> 异常。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-523">If the token size is too large, the code could fail with an <xref:System.OutOfMemoryException> exception.</span></span> <span data-ttu-id="0ffbe-524">如果 JSON 包含大小约为 1 GB 或更大的令牌，则会发生这种情况，因为将 1 GB 大小加倍会导致令牌太大，无法放入 `int32` 缓冲区。</span><span class="sxs-lookup"><span data-stu-id="0ffbe-524">This can happen if the JSON contains a token that is around 1 GB or more in size, because doubling the 1 GB size results in a size that is too large to fit into an `int32` buffer.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0ffbe-525">其他资源</span><span class="sxs-lookup"><span data-stu-id="0ffbe-525">Additional resources</span></span>

* [<span data-ttu-id="0ffbe-526">:::no-loc(System.Text.Json)::: 概述</span><span class="sxs-lookup"><span data-stu-id="0ffbe-526">:::no-loc(System.Text.Json)::: overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="0ffbe-527">如何编写自定义转换器</span><span class="sxs-lookup"><span data-stu-id="0ffbe-527">How to write custom converters</span></span>](system-text-json-converters-how-to.md)
* [<span data-ttu-id="0ffbe-528">如何从 :::no-loc(Newtonsoft.Json)::: 迁移</span><span class="sxs-lookup"><span data-stu-id="0ffbe-528">How to migrate from :::no-loc(Newtonsoft.Json):::</span></span>](system-text-json-migrate-from-newtonsoft-how-to.md)
* [<span data-ttu-id="0ffbe-529">:::no-loc(System.Text.Json)::: 中的 DateTime 和 DateTimeOffset 支持</span><span class="sxs-lookup"><span data-stu-id="0ffbe-529">DateTime and DateTimeOffset support in :::no-loc(System.Text.Json):::</span></span>](../datetime/system-text-json-support.md)
* <span data-ttu-id="0ffbe-530">[:::no-loc(System.Text.Json)::: API 参考](xref::::no-loc(System.Text.Json):::)</span><span class="sxs-lookup"><span data-stu-id="0ffbe-530">[:::no-loc(System.Text.Json)::: API reference](xref::::no-loc(System.Text.Json):::)</span></span>
<!-- * [:::no-loc(System.Text.Json)::: roadmap](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/roadmap/README.md)-->
