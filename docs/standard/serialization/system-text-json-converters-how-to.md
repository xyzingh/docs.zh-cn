---
title: 如何编写用于 JSON 序列化的自定义转换器 - .NET
description: '了解如何为 :::no-loc(System.Text.Json)::: 命名空间中提供的 JSON 序列化类创建自定义转换器。'
ms.date: 01/10/2020
no-loc:
- ':::no-loc(System.Text.Json):::'
- ':::no-loc(Newtonsoft.Json):::'
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
- converters
ms.openlocfilehash: ba6b61232ccf7ed493fe5809e5c0b8ba21091d3d
ms.sourcegitcommit: 6bef8abde346c59771a35f4f76bf037ff61c5ba3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2020
ms.locfileid: "94329802"
---
# <a name="how-to-write-custom-converters-for-json-serialization-marshalling-in-net"></a><span data-ttu-id="31725-103">如何在 .NET 中编写用于 JSON 序列化（封送）的自定义转换器</span><span class="sxs-lookup"><span data-stu-id="31725-103">How to write custom converters for JSON serialization (marshalling) in .NET</span></span>

<span data-ttu-id="31725-104">本文介绍如何为 <xref::::no-loc(System.Text.Json):::> 命名空间中提供的 JSON 序列化类创建自定义转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-104">This article shows how to create custom converters for the JSON serialization classes that are provided in the <xref::::no-loc(System.Text.Json):::> namespace.</span></span> <span data-ttu-id="31725-105">有关 `:::no-loc(System.Text.Json):::` 简介，请参阅[如何在 .NET 中对 JSON 数据进行序列化和反序列化](system-text-json-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="31725-105">For an introduction to `:::no-loc(System.Text.Json):::`, see [How to serialize and deserialize JSON in .NET](system-text-json-how-to.md).</span></span>

<span data-ttu-id="31725-106">转换器是一种将对象或值与 JSON 相互转换的类。</span><span class="sxs-lookup"><span data-stu-id="31725-106">A *converter* is a class that converts an object or a value to and from JSON.</span></span> <span data-ttu-id="31725-107">`:::no-loc(System.Text.Json):::` 命名空间为映射到 JavaScript 基元的大多数基元类型提供内置转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-107">The `:::no-loc(System.Text.Json):::` namespace has built-in converters for most primitive types that map to JavaScript primitives.</span></span> <span data-ttu-id="31725-108">可以编写自定义转换器来实现以下目标：</span><span class="sxs-lookup"><span data-stu-id="31725-108">You can write custom converters:</span></span>

* <span data-ttu-id="31725-109">重写内置转换器的默认行为。</span><span class="sxs-lookup"><span data-stu-id="31725-109">To override the default behavior of a built-in converter.</span></span> <span data-ttu-id="31725-110">例如，可能希望用 mm/dd/yyyy 格式而不是默认 ISO 8601-1:2019 格式来表示 `DateTime` 值。</span><span class="sxs-lookup"><span data-stu-id="31725-110">For example, you might want `DateTime` values to be represented by mm/dd/yyyy format instead of the default  ISO 8601-1:2019 format.</span></span>
* <span data-ttu-id="31725-111">支持自定义值类型。</span><span class="sxs-lookup"><span data-stu-id="31725-111">To support a custom value type.</span></span> <span data-ttu-id="31725-112">例如，`PhoneNumber` 结构。</span><span class="sxs-lookup"><span data-stu-id="31725-112">For example, a `PhoneNumber` struct.</span></span>

<span data-ttu-id="31725-113">还可以编写自定义转换器，以使用当前版本中未包含的功能自定义或扩展 `:::no-loc(System.Text.Json):::`。</span><span class="sxs-lookup"><span data-stu-id="31725-113">You can also write custom converters to customize or extend `:::no-loc(System.Text.Json):::` with functionality not included in the current release.</span></span> <span data-ttu-id="31725-114">本文后面部分介绍了以下方案：</span><span class="sxs-lookup"><span data-stu-id="31725-114">The following scenarios are covered later in this article:</span></span>

::: zone pivot="dotnet-5-0"

* <span data-ttu-id="31725-115">[将推断类型反序列化为对象属性](#deserialize-inferred-types-to-object-properties)。</span><span class="sxs-lookup"><span data-stu-id="31725-115">[Deserialize inferred types to object properties](#deserialize-inferred-types-to-object-properties).</span></span>
* <span data-ttu-id="31725-116">[支持多态反序列化](#support-polymorphic-deserialization)。</span><span class="sxs-lookup"><span data-stu-id="31725-116">[Support polymorphic deserialization](#support-polymorphic-deserialization).</span></span>
* <span data-ttu-id="31725-117">[支持堆栈的往返\<T>](#support-round-trip-for-stackt)。</span><span class="sxs-lookup"><span data-stu-id="31725-117">[Support round-trip for Stack\<T>](#support-round-trip-for-stackt).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"

* <span data-ttu-id="31725-118">[将推断类型反序列化为对象属性](#deserialize-inferred-types-to-object-properties)。</span><span class="sxs-lookup"><span data-stu-id="31725-118">[Deserialize inferred types to object properties](#deserialize-inferred-types-to-object-properties).</span></span>
* <span data-ttu-id="31725-119">[支持包含非字符串键的字典](#support-dictionary-with-non-string-key)。</span><span class="sxs-lookup"><span data-stu-id="31725-119">[Support Dictionary with non-string key](#support-dictionary-with-non-string-key).</span></span>
* <span data-ttu-id="31725-120">[支持多态反序列化](#support-polymorphic-deserialization)。</span><span class="sxs-lookup"><span data-stu-id="31725-120">[Support polymorphic deserialization](#support-polymorphic-deserialization).</span></span>
* <span data-ttu-id="31725-121">[支持堆栈的往返\<T>](#support-round-trip-for-stackt)。</span><span class="sxs-lookup"><span data-stu-id="31725-121">[Support round-trip for Stack\<T>](#support-round-trip-for-stackt).</span></span>
::: zone-end

## <a name="custom-converter-patterns"></a><span data-ttu-id="31725-122">自定义转换器模式</span><span class="sxs-lookup"><span data-stu-id="31725-122">Custom converter patterns</span></span>

<span data-ttu-id="31725-123">用于创建自定义转换器的模式有两种：基本模式和工厂模式。</span><span class="sxs-lookup"><span data-stu-id="31725-123">There are two patterns for creating a custom converter: the basic pattern and the factory pattern.</span></span> <span data-ttu-id="31725-124">工厂模式适用于处理类型 `Enum` 或开放式泛型的转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-124">The factory pattern is for converters that handle type `Enum` or open generics.</span></span> <span data-ttu-id="31725-125">基本模式适用于非泛型或封闭式泛型类型。</span><span class="sxs-lookup"><span data-stu-id="31725-125">The basic pattern is for non-generic and closed generic types.</span></span>  <span data-ttu-id="31725-126">例如，适用于以下类型的转换器需要工厂模式：</span><span class="sxs-lookup"><span data-stu-id="31725-126">For example, converters for the following types require the factory pattern:</span></span>

* `Dictionary<TKey, TValue>`
* `Enum`
* `List<T>`

<span data-ttu-id="31725-127">可以通过基本模式处理的类型的一些示例包括：</span><span class="sxs-lookup"><span data-stu-id="31725-127">Some examples of types that can be handled by the basic pattern include:</span></span>

* `Dictionary<int, string>`
* `WeekdaysEnum`
* `List<DateTimeOffset>`
* `DateTime`
* `Int32`

<span data-ttu-id="31725-128">基本模式创建的类可以处理一种类型。</span><span class="sxs-lookup"><span data-stu-id="31725-128">The basic pattern creates a class that can handle one type.</span></span> <span data-ttu-id="31725-129">工厂模式创建的类在运行时确定所需的特定类型，并动态创建适当的转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-129">The factory pattern creates a class that determines, at run time, which specific type is required and dynamically creates the appropriate converter.</span></span>

## <a name="sample-basic-converter"></a><span data-ttu-id="31725-130">示例基本转换器</span><span class="sxs-lookup"><span data-stu-id="31725-130">Sample basic converter</span></span>

<span data-ttu-id="31725-131">下面的示例是一个转换器，可重写现有数据类型的默认序列化。</span><span class="sxs-lookup"><span data-stu-id="31725-131">The following sample is a converter that overrides default serialization for an existing data type.</span></span> <span data-ttu-id="31725-132">该转换器将 mm/dd/yyyy 格式用于 `DateTimeOffset` 属性。</span><span class="sxs-lookup"><span data-stu-id="31725-132">The converter uses mm/dd/yyyy format for `DateTimeOffset` properties.</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/DateTimeOffsetConverter.cs)]

## <a name="sample-factory-pattern-converter"></a><span data-ttu-id="31725-133">示例工厂模式转换器</span><span class="sxs-lookup"><span data-stu-id="31725-133">Sample factory pattern converter</span></span>

<span data-ttu-id="31725-134">下面的代码演示一个处理 `Dictionary<Enum,TValue>` 的自定义转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-134">The following code shows a custom converter that works with `Dictionary<Enum,TValue>`.</span></span> <span data-ttu-id="31725-135">该代码遵循工厂模式，因为第一个泛型类型参数是 `Enum`，第二个参数是开放参数。</span><span class="sxs-lookup"><span data-stu-id="31725-135">The code follows the factory pattern because the first generic type parameter is `Enum` and the second is open.</span></span> <span data-ttu-id="31725-136">`CanConvert` 方法仅对具有两个泛型参数的 `Dictionary` 返回 `true`，其中第一个参数是 `Enum` 类型。</span><span class="sxs-lookup"><span data-stu-id="31725-136">The `CanConvert` method returns `true` only for a `Dictionary` with two generic parameters, the first of which is an `Enum` type.</span></span> <span data-ttu-id="31725-137">内部转换器获取现有转换器，以处理在运行时为 `TValue` 提供的任何类型。</span><span class="sxs-lookup"><span data-stu-id="31725-137">The inner converter gets an existing converter to handle whichever type is provided at run time for `TValue`.</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/DictionaryTKeyEnumTValueConverter.cs)]

<span data-ttu-id="31725-138">前面的代码与本文后面的[支持包含非字符串键的字典](#support-dictionary-with-non-string-key)中演示的代码相同。</span><span class="sxs-lookup"><span data-stu-id="31725-138">The preceding code is the same as what is shown in the [Support Dictionary with non-string key](#support-dictionary-with-non-string-key) later in this article.</span></span>

## <a name="steps-to-follow-the-basic-pattern"></a><span data-ttu-id="31725-139">遵循基本模式的步骤</span><span class="sxs-lookup"><span data-stu-id="31725-139">Steps to follow the basic pattern</span></span>

<span data-ttu-id="31725-140">以下步骤说明如何遵循基本模式来创建转换器：</span><span class="sxs-lookup"><span data-stu-id="31725-140">The following steps explain how to create a converter by following the basic pattern:</span></span>

* <span data-ttu-id="31725-141">创建一个派生自 <xref::::no-loc(System.Text.Json):::.Serialization.JsonConverter%601> 的类，其中 `T` 是要进行序列化和反序列化的类型。</span><span class="sxs-lookup"><span data-stu-id="31725-141">Create a class that derives from <xref::::no-loc(System.Text.Json):::.Serialization.JsonConverter%601> where `T` is the type to be serialized and deserialized.</span></span>
* <span data-ttu-id="31725-142">重写 `Read` 方法，以反序列化传入 JSON 并将其转换为类型 `T`。</span><span class="sxs-lookup"><span data-stu-id="31725-142">Override the `Read` method to deserialize the incoming JSON and convert it to type `T`.</span></span> <span data-ttu-id="31725-143">使用传递给方法的 <xref::::no-loc(System.Text.Json):::.Utf8JsonReader> 读取 JSON。</span><span class="sxs-lookup"><span data-stu-id="31725-143">Use the <xref::::no-loc(System.Text.Json):::.Utf8JsonReader> that is passed to the method to read the JSON.</span></span>
* <span data-ttu-id="31725-144">重写 `Write` 方法以序列化 `T` 类型的传入对象。</span><span class="sxs-lookup"><span data-stu-id="31725-144">Override the `Write` method to serialize the incoming object of type `T`.</span></span> <span data-ttu-id="31725-145">使用传递给方法的 <xref::::no-loc(System.Text.Json):::.Utf8JsonWriter> 写入 JSON。</span><span class="sxs-lookup"><span data-stu-id="31725-145">Use the <xref::::no-loc(System.Text.Json):::.Utf8JsonWriter> that is passed to the method to write the JSON.</span></span>
* <span data-ttu-id="31725-146">仅当需要时才重写 `CanConvert` 方法。</span><span class="sxs-lookup"><span data-stu-id="31725-146">Override the `CanConvert` method only if necessary.</span></span> <span data-ttu-id="31725-147">当要转换的类型属于类型 `T` 时，默认实现会返回 `true`。</span><span class="sxs-lookup"><span data-stu-id="31725-147">The default implementation returns `true` when the type to convert is of type `T`.</span></span> <span data-ttu-id="31725-148">因此，仅支持类型 `T` 的转换器不需要重写此方法。</span><span class="sxs-lookup"><span data-stu-id="31725-148">Therefore, converters that support only type `T` don't need to override this method.</span></span> <span data-ttu-id="31725-149">有关的确需要重写此方法的转换器的示例，请参阅本文后面的[多态反序列化](#support-polymorphic-deserialization)部分。</span><span class="sxs-lookup"><span data-stu-id="31725-149">For an example of a converter that does need to override this method, see the [polymorphic deserialization](#support-polymorphic-deserialization) section later in this article.</span></span>

<span data-ttu-id="31725-150">可以参阅[内置转换器源代码](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/src/System/Text/Json/Serialization/Converters/)作为用于编写自定义转换器的参考实现。</span><span class="sxs-lookup"><span data-stu-id="31725-150">You can refer to the [built-in converters source code](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/src/System/Text/Json/Serialization/Converters/) as reference implementations for writing custom converters.</span></span>

## <a name="steps-to-follow-the-factory-pattern"></a><span data-ttu-id="31725-151">遵循工厂模式的步骤</span><span class="sxs-lookup"><span data-stu-id="31725-151">Steps to follow the factory pattern</span></span>

<span data-ttu-id="31725-152">以下步骤说明如何遵循工厂模式来创建转换器：</span><span class="sxs-lookup"><span data-stu-id="31725-152">The following steps explain how to create a converter by following the factory pattern:</span></span>

* <span data-ttu-id="31725-153">创建一个从 <xref::::no-loc(System.Text.Json):::.Serialization.JsonConverterFactory> 派生的类。</span><span class="sxs-lookup"><span data-stu-id="31725-153">Create a class that derives from <xref::::no-loc(System.Text.Json):::.Serialization.JsonConverterFactory>.</span></span>
* <span data-ttu-id="31725-154">重写 `CanConvert` 方法，以在要转换的类型是转换器可处理的类型时返回 true。</span><span class="sxs-lookup"><span data-stu-id="31725-154">Override the `CanConvert` method to return true when the type to convert is one that the converter can handle.</span></span> <span data-ttu-id="31725-155">例如，如果转换器适用于 `List<T>`，则它可能仅处理 `List<int>`、`List<string>` 和 `List<DateTime>`。</span><span class="sxs-lookup"><span data-stu-id="31725-155">For example, if the converter is for `List<T>` it might only handle `List<int>`, `List<string>`, and `List<DateTime>`.</span></span>
* <span data-ttu-id="31725-156">重写 `CreateConverter` 方法，以返回将处理在运行时提供的要转换的类型的转换器类实例。</span><span class="sxs-lookup"><span data-stu-id="31725-156">Override the `CreateConverter` method to return an instance of a converter class that will handle the type-to-convert that is provided at run time.</span></span>
* <span data-ttu-id="31725-157">创建 `CreateConverter` 方法实例化的转换器类。</span><span class="sxs-lookup"><span data-stu-id="31725-157">Create the converter class that the `CreateConverter` method instantiates.</span></span>

<span data-ttu-id="31725-158">开放式泛型需要工厂模式，因为用于将对象与字符串相互转换的代码对于所有类型并不相同。</span><span class="sxs-lookup"><span data-stu-id="31725-158">The factory pattern is required for open generics because the code to convert an object to and from a string isn't the same for all types.</span></span> <span data-ttu-id="31725-159">适用于开放式泛型类型（例如 `List<T>`）的转换器必须在幕后为封闭式泛型类型（例如 `List<DateTime>`）创建转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-159">A converter for an open generic type (`List<T>`, for example) has to create a converter for a closed generic type (`List<DateTime>`, for example) behind the scenes.</span></span> <span data-ttu-id="31725-160">必须编写代码来处理转换器可处理的每种封闭式泛型类型。</span><span class="sxs-lookup"><span data-stu-id="31725-160">Code must be written to handle each closed-generic type that the converter can handle.</span></span>

<span data-ttu-id="31725-161">`Enum` 类型类似于开放式泛型类型：适用于 `Enum` 的转换器必须在幕后为特定 `Enum`（例如`WeekdaysEnum`）创建转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-161">The `Enum` type is similar to an open generic type: a converter for `Enum` has to create a converter for a specific `Enum` (`WeekdaysEnum`, for example) behind the scenes.</span></span>

## <a name="error-handling"></a><span data-ttu-id="31725-162">错误处理</span><span class="sxs-lookup"><span data-stu-id="31725-162">Error handling</span></span>

<span data-ttu-id="31725-163">如果需要在错误处理代码中引发异常，请考虑在不使用消息的情况下引发 <xref::::no-loc(System.Text.Json):::.JsonException>。</span><span class="sxs-lookup"><span data-stu-id="31725-163">If you need to throw an exception in error-handling code, consider throwing a <xref::::no-loc(System.Text.Json):::.JsonException> without a message.</span></span> <span data-ttu-id="31725-164">此异常类型会自动创建消息，其中包括导致错误的 JSON 部分的路径。</span><span class="sxs-lookup"><span data-stu-id="31725-164">This exception type automatically creates a message that includes the path to the part of the JSON that caused the error.</span></span> <span data-ttu-id="31725-165">例如，语句 `throw new JsonException();` 会生成如以下示例的错误消息：</span><span class="sxs-lookup"><span data-stu-id="31725-165">For example, the statement `throw new JsonException();` produces an error message like the following example:</span></span>

```output
Unhandled exception. :::no-loc(System.Text.Json):::.JsonException:
The JSON value could not be converted to System.Object.
Path: $.Date | LineNumber: 1 | BytePositionInLine: 37.
```

<span data-ttu-id="31725-166">如果提供消息（例如 `throw new JsonException("Error occurred")`），则异常仍会在 <xref::::no-loc(System.Text.Json):::.JsonException.Path> 属性中提供路径。</span><span class="sxs-lookup"><span data-stu-id="31725-166">If you do provide a message (for example, `throw new JsonException("Error occurred")`, the exception still provides the path in the <xref::::no-loc(System.Text.Json):::.JsonException.Path> property.</span></span>

## <a name="register-a-custom-converter"></a><span data-ttu-id="31725-167">注册自定义转换器</span><span class="sxs-lookup"><span data-stu-id="31725-167">Register a custom converter</span></span>

<span data-ttu-id="31725-168">注册自定义转换器，使 `Serialize` 和 `Deserialize` 方法可使用它。</span><span class="sxs-lookup"><span data-stu-id="31725-168">*Register* a custom converter to make the `Serialize` and `Deserialize` methods use it.</span></span> <span data-ttu-id="31725-169">选择以下方法之一：</span><span class="sxs-lookup"><span data-stu-id="31725-169">Choose one of the following approaches:</span></span>

* <span data-ttu-id="31725-170">向 <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.Converters?displayProperty=nameWithType> 集合添加转换器类的实例。</span><span class="sxs-lookup"><span data-stu-id="31725-170">Add an instance of the converter class to the <xref::::no-loc(System.Text.Json):::.JsonSerializerOptions.Converters?displayProperty=nameWithType> collection.</span></span>
* <span data-ttu-id="31725-171">将 [[JsonConverter]](xref::::no-loc(System.Text.Json):::.Serialization.JsonConverterAttribute) 特性应用于需要自定义转换器的属性。</span><span class="sxs-lookup"><span data-stu-id="31725-171">Apply the [[JsonConverter]](xref::::no-loc(System.Text.Json):::.Serialization.JsonConverterAttribute) attribute to the properties that require the custom converter.</span></span>
* <span data-ttu-id="31725-172">将 [[JsonConverter]](xref::::no-loc(System.Text.Json):::.Serialization.JsonConverterAttribute) 特性应用于表示自定义值类型的类或结构。</span><span class="sxs-lookup"><span data-stu-id="31725-172">Apply the [[JsonConverter]](xref::::no-loc(System.Text.Json):::.Serialization.JsonConverterAttribute) attribute to a class or a struct that represents a custom value type.</span></span>

## <a name="registration-sample---converters-collection"></a><span data-ttu-id="31725-173">注册示例 - 转换器集合</span><span class="sxs-lookup"><span data-stu-id="31725-173">Registration sample - Converters collection</span></span>

<span data-ttu-id="31725-174">下面是一个示例，该示例将 <xref:System.ComponentModel.DateTimeOffsetConverter> 设为类型 <xref:System.DateTimeOffset> 的属性的默认值：</span><span class="sxs-lookup"><span data-stu-id="31725-174">Here's an example that makes the <xref:System.ComponentModel.DateTimeOffsetConverter> the default for properties of type <xref:System.DateTimeOffset>:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RegisterConverterWithConvertersCollection.cs?name=SnippetSerialize)]

<span data-ttu-id="31725-175">假设序列化以下类型的实例：</span><span class="sxs-lookup"><span data-stu-id="31725-175">Suppose you serialize an instance of the following type:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

<span data-ttu-id="31725-176">下面是演示使用自定义转换器的 JSON 输出的示例：</span><span class="sxs-lookup"><span data-stu-id="31725-176">Here's an example of JSON output that shows the custom converter was used:</span></span>

```json
{
  "Date": "08/01/2019",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

<span data-ttu-id="31725-177">下面的代码使用的方法与使用自定义 `DateTimeOffset` 转换器进行反序列化相同：</span><span class="sxs-lookup"><span data-stu-id="31725-177">The following code uses the same approach to deserialize using the custom `DateTimeOffset` converter:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RegisterConverterWithConvertersCollection.cs?name=SnippetDeserialize)]

## <a name="registration-sample---jsonconverter-on-a-property"></a><span data-ttu-id="31725-178">注册示例 - 属性上的 [JsonConverter]</span><span class="sxs-lookup"><span data-stu-id="31725-178">Registration sample - [JsonConverter] on a property</span></span>

<span data-ttu-id="31725-179">下面的代码为 `Date` 属性选择自定义转换器：</span><span class="sxs-lookup"><span data-stu-id="31725-179">The following code selects a custom converter for the `Date` property:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithConverterAttribute)]

<span data-ttu-id="31725-180">用于序列化 `WeatherForecastWithConverterAttribute` 的代码不需要使用 `JsonSerializeOptions.Converters`：</span><span class="sxs-lookup"><span data-stu-id="31725-180">The code to serialize `WeatherForecastWithConverterAttribute` doesn't require the use of `JsonSerializeOptions.Converters`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RegisterConverterWithAttributeOnProperty.cs?name=SnippetSerialize)]

<span data-ttu-id="31725-181">用于反序列化的代码也不需要使用 `Converters`：</span><span class="sxs-lookup"><span data-stu-id="31725-181">The code to deserialize also doesn't require the use of `Converters`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RegisterConverterWithAttributeOnProperty.cs?name=SnippetDeserialize)]

## <a name="registration-sample---jsonconverter-on-a-type"></a><span data-ttu-id="31725-182">注册示例 - 类型上的 [JsonConverter]</span><span class="sxs-lookup"><span data-stu-id="31725-182">Registration sample - [JsonConverter] on a type</span></span>

<span data-ttu-id="31725-183">下面的代码创建一个结构并向它应用 `[JsonConverter]` 属性：</span><span class="sxs-lookup"><span data-stu-id="31725-183">Here's code that creates a struct and applies the `[JsonConverter]` attribute to it:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/Temperature.cs)]

<span data-ttu-id="31725-184">下面是适用于上述结构的自定义转换器：</span><span class="sxs-lookup"><span data-stu-id="31725-184">Here's the custom converter for the preceding struct:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/TemperatureConverter.cs)]

<span data-ttu-id="31725-185">结构上的 `[JsonConvert]` 属性将自定义转换器注册为类型 `Temperature` 的属性的默认值。</span><span class="sxs-lookup"><span data-stu-id="31725-185">The `[JsonConvert]` attribute on the struct registers the custom converter as the default for properties of type `Temperature`.</span></span> <span data-ttu-id="31725-186">进行序列化或反序列化时，转换器会自动用于以下类型的 `TemperatureCelsius` 属性：</span><span class="sxs-lookup"><span data-stu-id="31725-186">The converter is automatically used on the `TemperatureCelsius` property of the following type when you serialize or deserialize it:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithTemperatureStruct)]

## <a name="converter-registration-precedence"></a><span data-ttu-id="31725-187">转换器注册优先级</span><span class="sxs-lookup"><span data-stu-id="31725-187">Converter registration precedence</span></span>

<span data-ttu-id="31725-188">在序列化或反序列化过程中，按以下顺序（从最高优先级到最低优先级来列出）为每个 JSON 元素选择转换器：</span><span class="sxs-lookup"><span data-stu-id="31725-188">During serialization or deserialization, a converter is chosen for each JSON element in the following order, listed from highest priority to lowest:</span></span>

* <span data-ttu-id="31725-189">应用于属性的 `[JsonConverter]`。</span><span class="sxs-lookup"><span data-stu-id="31725-189">`[JsonConverter]` applied to a property.</span></span>
* <span data-ttu-id="31725-190">向 `Converters` 集合添加的转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-190">A converter added to the `Converters` collection.</span></span>
* <span data-ttu-id="31725-191">应用于自定义值类型或 POCO 的 `[JsonConverter]`。</span><span class="sxs-lookup"><span data-stu-id="31725-191">`[JsonConverter]` applied to a custom value type or POCO.</span></span>

<span data-ttu-id="31725-192">如果在 `Converters` 集合中注册了适用于某种类型的多个自定义转换器，则使用第一个为 `CanConvert` 返回 true 的转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-192">If multiple custom converters for a type are registered in the `Converters` collection, the first converter that returns true for `CanConvert` is used.</span></span>

<span data-ttu-id="31725-193">仅当未注册适用自定义转换器时，才会选择内置转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-193">A built-in converter is chosen only if no applicable custom converter is registered.</span></span>

## <a name="converter-samples-for-common-scenarios"></a><span data-ttu-id="31725-194">常见方案的转换器示例</span><span class="sxs-lookup"><span data-stu-id="31725-194">Converter samples for common scenarios</span></span>

<span data-ttu-id="31725-195">以下各部分提供的转换器示例用于解决内置功能不处理的一些常见方案。</span><span class="sxs-lookup"><span data-stu-id="31725-195">The following sections provide converter samples that address some common scenarios that built-in functionality doesn't handle.</span></span>

::: zone pivot="dotnet-5-0"

* <span data-ttu-id="31725-196">[将推断类型反序列化为对象属性](#deserialize-inferred-types-to-object-properties)。</span><span class="sxs-lookup"><span data-stu-id="31725-196">[Deserialize inferred types to object properties](#deserialize-inferred-types-to-object-properties).</span></span>
* <span data-ttu-id="31725-197">[支持多态反序列化](#support-polymorphic-deserialization)。</span><span class="sxs-lookup"><span data-stu-id="31725-197">[Support polymorphic deserialization](#support-polymorphic-deserialization).</span></span>
* <span data-ttu-id="31725-198">[支持堆栈的往返\<T>](#support-round-trip-for-stackt)。</span><span class="sxs-lookup"><span data-stu-id="31725-198">[Support round-trip for Stack\<T>](#support-round-trip-for-stackt).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"

* <span data-ttu-id="31725-199">[将推断类型反序列化为对象属性](#deserialize-inferred-types-to-object-properties)。</span><span class="sxs-lookup"><span data-stu-id="31725-199">[Deserialize inferred types to object properties](#deserialize-inferred-types-to-object-properties).</span></span>
* <span data-ttu-id="31725-200">[支持包含非字符串键的字典](#support-dictionary-with-non-string-key)。</span><span class="sxs-lookup"><span data-stu-id="31725-200">[Support Dictionary with non-string key](#support-dictionary-with-non-string-key).</span></span>
* <span data-ttu-id="31725-201">[支持多态反序列化](#support-polymorphic-deserialization)。</span><span class="sxs-lookup"><span data-stu-id="31725-201">[Support polymorphic deserialization](#support-polymorphic-deserialization).</span></span>
* <span data-ttu-id="31725-202">[支持堆栈的往返\<T>](#support-round-trip-for-stackt)。</span><span class="sxs-lookup"><span data-stu-id="31725-202">[Support round-trip for Stack\<T>](#support-round-trip-for-stackt).</span></span>
::: zone-end

### <a name="deserialize-inferred-types-to-object-properties"></a><span data-ttu-id="31725-203">将推断类型反序列化为对象属性</span><span class="sxs-lookup"><span data-stu-id="31725-203">Deserialize inferred types to object properties</span></span>

<span data-ttu-id="31725-204">反序列化为类型 `object` 的属性时，将创建一个 `JsonElement` 对象。</span><span class="sxs-lookup"><span data-stu-id="31725-204">When deserializing to a property of type `object`, a `JsonElement` object is created.</span></span> <span data-ttu-id="31725-205">这是因为反序列化程序不知道要创建的 CLR 类型，也不会尝试进行猜测。</span><span class="sxs-lookup"><span data-stu-id="31725-205">The reason is that the deserializer doesn't know what CLR type to create, and it doesn't try to guess.</span></span> <span data-ttu-id="31725-206">例如，如果 JSON 属性具有“true”，则反序列化程序不会推断值为 `Boolean`，如果元素具有“01/01/2019”，则反序列化程序不会推断它是 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="31725-206">For example, if a JSON property has "true", the deserializer doesn't infer that the value is a `Boolean`, and if an element has "01/01/2019", the deserializer doesn't infer that it's a `DateTime`.</span></span>

<span data-ttu-id="31725-207">类型推理可能不准确。</span><span class="sxs-lookup"><span data-stu-id="31725-207">Type inference can be inaccurate.</span></span> <span data-ttu-id="31725-208">如果反序列化程序将没有小数点的 JSON 数字分析为 `long`，则当值最初序列化为 `ulong` 或 `BigInteger` 时，这可能会导致超出范围问题。</span><span class="sxs-lookup"><span data-stu-id="31725-208">If the deserializer parses a JSON number that has no decimal point as a `long`, that might result in out-of-range issues if the value was originally serialized as a `ulong` or `BigInteger`.</span></span> <span data-ttu-id="31725-209">如果数字最初序列化为 `decimal`，则将具有小数点的数字分析为 `double` 可能会损失精度。</span><span class="sxs-lookup"><span data-stu-id="31725-209">Parsing a number that has a decimal point as a `double` might lose precision if the number was originally serialized as a `decimal`.</span></span>

<span data-ttu-id="31725-210">对于需要类型推理的方案，以下代码演示适用于 `object` 属性的自定义转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-210">For scenarios that require type inference, the following code shows a custom converter for `object` properties.</span></span> <span data-ttu-id="31725-211">代码：</span><span class="sxs-lookup"><span data-stu-id="31725-211">The code converts:</span></span>

* <span data-ttu-id="31725-212">将 `true` 和 `false` 转换为 `Boolean`</span><span class="sxs-lookup"><span data-stu-id="31725-212">`true` and `false` to `Boolean`</span></span>
* <span data-ttu-id="31725-213">将不带小数的数字转换为 `long`</span><span class="sxs-lookup"><span data-stu-id="31725-213">Numbers without a decimal to `long`</span></span>
* <span data-ttu-id="31725-214">将带有小数的数字转换为 `double`</span><span class="sxs-lookup"><span data-stu-id="31725-214">Numbers with a decimal to `double`</span></span>
* <span data-ttu-id="31725-215">将日期转换为 `DateTime`</span><span class="sxs-lookup"><span data-stu-id="31725-215">Dates to `DateTime`</span></span>
* <span data-ttu-id="31725-216">将字符串转换为 `string`</span><span class="sxs-lookup"><span data-stu-id="31725-216">Strings to `string`</span></span>
* <span data-ttu-id="31725-217">将其他所有内容转换为 `JsonElement`</span><span class="sxs-lookup"><span data-stu-id="31725-217">Everything else to `JsonElement`</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/ObjectToInferredTypesConverter.cs)]

<span data-ttu-id="31725-218">下面的代码注册转换器：</span><span class="sxs-lookup"><span data-stu-id="31725-218">The following code registers the converter:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/DeserializeInferredTypesToObject.cs?name=SnippetRegister)]

<span data-ttu-id="31725-219">下面是一种具有 `object` 属性的示例类型：</span><span class="sxs-lookup"><span data-stu-id="31725-219">Here's an example type with `object` properties:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithObjectProperties)]

<span data-ttu-id="31725-220">以下要反序列化的 JSON 示例包含将作为 `DateTime`、`long` 和 `string` 进行反序列化的值：</span><span class="sxs-lookup"><span data-stu-id="31725-220">The following example of JSON to deserialize contains values that will be deserialized as `DateTime`, `long`, and `string`:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
}
```

<span data-ttu-id="31725-221">如果没有自定义转换器，则反序列化会将 `JsonElement` 放入每个属性中。</span><span class="sxs-lookup"><span data-stu-id="31725-221">Without the custom converter, deserialization puts a `JsonElement` in each property.</span></span>

<span data-ttu-id="31725-222">`:::no-loc(System.Text.Json):::.Serialization` 命名空间中的[单元测试文件夹](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/)包含处理到 `object` 属性的反序列化的自定义转换器的更多示例。</span><span class="sxs-lookup"><span data-stu-id="31725-222">The [unit tests folder](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/) in the `:::no-loc(System.Text.Json):::.Serialization` namespace has more examples of custom converters that handle deserialization to `object` properties.</span></span>

::: zone pivot="dotnet-core-3-1"

### <a name="support-dictionary-with-non-string-key"></a><span data-ttu-id="31725-223">支持包含非字符串键的字典</span><span class="sxs-lookup"><span data-stu-id="31725-223">Support Dictionary with non-string key</span></span>

<span data-ttu-id="31725-224">对字典集合的内置支持适用于 `Dictionary<string, TValue>`。</span><span class="sxs-lookup"><span data-stu-id="31725-224">The built-in support for dictionary collections is for `Dictionary<string, TValue>`.</span></span> <span data-ttu-id="31725-225">即，键必须是字符串。</span><span class="sxs-lookup"><span data-stu-id="31725-225">That is, the key must be a string.</span></span> <span data-ttu-id="31725-226">若要支持将整数或某种其他类型用作键的字典，需要自定义转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-226">To support a dictionary with an integer or some other type as the key, a custom converter is required.</span></span>

<span data-ttu-id="31725-227">下面的代码演示一个处理 `Dictionary<Enum,TValue>` 的自定义转换器：</span><span class="sxs-lookup"><span data-stu-id="31725-227">The following code shows a custom converter that works with `Dictionary<Enum,TValue>`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/DictionaryTKeyEnumTValueConverter.cs)]

<span data-ttu-id="31725-228">下面的代码注册转换器：</span><span class="sxs-lookup"><span data-stu-id="31725-228">The following code registers the converter:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripDictionaryTkeyEnumTValue.cs?name=SnippetRegister)]

<span data-ttu-id="31725-229">该转换器可以序列化和反序列化使用以下 `Enum` 的以下类的 `TemperatureRanges` 属性：</span><span class="sxs-lookup"><span data-stu-id="31725-229">The converter can serialize and deserialize the `TemperatureRanges` property of the following class that uses the following `Enum`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithEnumDictionary)]

<span data-ttu-id="31725-230">来自序列化的 JSON 输出类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="31725-230">The JSON output from serialization looks like the following example:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "TemperatureRanges": {
    "Cold": 20,
    "Hot": 40
  }
}
```

<span data-ttu-id="31725-231">`:::no-loc(System.Text.Json):::.Serialization` 命名空间中的[单元测试文件夹](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/)包含处理非字符串键字典的自定义转换器的更多示例。</span><span class="sxs-lookup"><span data-stu-id="31725-231">The [unit tests folder](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/) in the `:::no-loc(System.Text.Json):::.Serialization` namespace has more examples of custom converters that handle non-string-key dictionaries.</span></span>
::: zone-end

### <a name="support-polymorphic-deserialization"></a><span data-ttu-id="31725-232">支持多态反序列化</span><span class="sxs-lookup"><span data-stu-id="31725-232">Support polymorphic deserialization</span></span>

<span data-ttu-id="31725-233">内置功能提供有限范围的[多态序列化](system-text-json-how-to.md#serialize-properties-of-derived-classes)，但完全不支持反序列化。</span><span class="sxs-lookup"><span data-stu-id="31725-233">Built-in features provide a limited range of [polymorphic serialization](system-text-json-how-to.md#serialize-properties-of-derived-classes) but no support for deserialization at all.</span></span> <span data-ttu-id="31725-234">反序列化需要自定义转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-234">Deserialization requires a custom converter.</span></span>

<span data-ttu-id="31725-235">例如，假设有一个 `Person` 抽象基类，其中包含 `Employee` 和 `Customer` 派生类。</span><span class="sxs-lookup"><span data-stu-id="31725-235">Suppose, for example, you have a `Person` abstract base class, with `Employee` and `Customer` derived classes.</span></span> <span data-ttu-id="31725-236">多态反序列化意味着可以在设计时将 `Person` 指定为反序列化目标，JSON 中的 `Customer` 和 `Employee` 对象会在运行时正确地进行反序列化。</span><span class="sxs-lookup"><span data-stu-id="31725-236">Polymorphic deserialization means that at design time you can specify `Person` as the deserialization target, and `Customer` and `Employee` objects in the JSON are correctly deserialized at run time.</span></span> <span data-ttu-id="31725-237">在反序列化过程中，必须查找标识 JSON 中所需类型的线索。</span><span class="sxs-lookup"><span data-stu-id="31725-237">During deserialization, you have to find clues that identify the required type in the JSON.</span></span> <span data-ttu-id="31725-238">可用的线索类型因各个方案而异。</span><span class="sxs-lookup"><span data-stu-id="31725-238">The kinds of clues available vary with each scenario.</span></span> <span data-ttu-id="31725-239">例如，可以使用鉴别器属性，或者可能必须依赖于特定属性是否存在。</span><span class="sxs-lookup"><span data-stu-id="31725-239">For example, a discriminator property might be available or you might have to rely on the presence or absence of a particular property.</span></span> <span data-ttu-id="31725-240">`:::no-loc(System.Text.Json):::` 的当前版本不提供属性来指定如何处理多态反序列化方案，因此需要自定义转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-240">The current release of `:::no-loc(System.Text.Json):::` doesn't provide attributes to specify how to handle polymorphic deserialization scenarios, so custom converters are required.</span></span>

<span data-ttu-id="31725-241">下面的代码演示一个基类、两个派生类和适用于它们的一个自定义转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-241">The following code shows a base class, two derived classes, and a custom converter for them.</span></span> <span data-ttu-id="31725-242">该转换器使用鉴别器属性执行多态反序列化。</span><span class="sxs-lookup"><span data-stu-id="31725-242">The converter uses a discriminator property to do polymorphic deserialization.</span></span> <span data-ttu-id="31725-243">类型鉴别器不在类定义中，而是在序列化过程中创建，在反序列化过程中进行读取。</span><span class="sxs-lookup"><span data-stu-id="31725-243">The type discriminator isn't in the class definitions but is created during serialization and is read during deserialization.</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/Person.cs?name=SnippetPerson)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/PersonConverterWithTypeDiscriminator.cs)]

<span data-ttu-id="31725-244">下面的代码注册转换器：</span><span class="sxs-lookup"><span data-stu-id="31725-244">The following code registers the converter:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripPolymorphic.cs?name=SnippetRegister)]

<span data-ttu-id="31725-245">该转换器可以反序列化通过用于序列化的相同转换器而创建的 JSON，例如：</span><span class="sxs-lookup"><span data-stu-id="31725-245">The converter can deserialize JSON that was created by using the same converter to serialize, for example:</span></span>

```json
[
  {
    "TypeDiscriminator": 1,
    "CreditLimit": 10000,
    "Name": "John"
  },
  {
    "TypeDiscriminator": 2,
    "OfficeNumber": "555-1234",
    "Name": "Nancy"
  }
]
```

<span data-ttu-id="31725-246">前面示例中的转换器代码会手动读取和写入每个属性。</span><span class="sxs-lookup"><span data-stu-id="31725-246">The converter code in the preceding example reads and writes each property manually.</span></span> <span data-ttu-id="31725-247">一种替代方法是调用 `Deserialize` 或 `Serialize` 以执行某些工作。</span><span class="sxs-lookup"><span data-stu-id="31725-247">An alternative is to call `Deserialize` or `Serialize` to do some of the work.</span></span> <span data-ttu-id="31725-248">有关示例，请参阅[此 StackOverflow 文章](https://stackoverflow.com/a/59744873/12509023)。</span><span class="sxs-lookup"><span data-stu-id="31725-248">For an example, see [this StackOverflow post](https://stackoverflow.com/a/59744873/12509023).</span></span>

### <a name="support-round-trip-for-stackt"></a><span data-ttu-id="31725-249">支持堆栈的往返\<T></span><span class="sxs-lookup"><span data-stu-id="31725-249">Support round trip for Stack\<T></span></span>

<span data-ttu-id="31725-250">如果将 JSON 字符串反序列化为 <xref:System.Collections.Generic.Stack%601> 对象，然后再序列化该对象，则堆栈的内容将按相反的顺序排列。</span><span class="sxs-lookup"><span data-stu-id="31725-250">If you deserialize a JSON string into a <xref:System.Collections.Generic.Stack%601> object and then serialize that object, the contents of the stack are in reverse order.</span></span> <span data-ttu-id="31725-251">此行为适用于以下类型和接口以及从它们派生的用户定义类型：</span><span class="sxs-lookup"><span data-stu-id="31725-251">This behavior applies to the following types and interface, and user-defined types that derive from them:</span></span>

* <xref:System.Collections.Stack>
* <xref:System.Collections.Generic.Stack%601>
* <xref:System.Collections.Concurrent.ConcurrentStack%601>
* <xref:System.Collections.Immutable.ImmutableStack%601>
* <xref:System.Collections.Immutable.IImmutableStack%601>

<span data-ttu-id="31725-252">若要支持在堆栈中保留原始顺序的序列化和反序列化，则需要自定义转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-252">To support serialization and deserialization that retains the original order in the stack, a custom converter is required.</span></span>

<span data-ttu-id="31725-253">下面的代码演示了一个自定义转换器，用于实现与 `Stack<T>` 对象之间的来回转换：</span><span class="sxs-lookup"><span data-stu-id="31725-253">The following code shows a custom converter that enables round-tripping to and from `Stack<T>` objects:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/JsonConverterFactoryForStackOfT.cs)]

<span data-ttu-id="31725-254">下面的代码注册转换器：</span><span class="sxs-lookup"><span data-stu-id="31725-254">The following code registers the converter:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripStackOfT.cs?name=SnippetRegister)]

## <a name="handle-null-values"></a><span data-ttu-id="31725-255">处理 NULL 值</span><span class="sxs-lookup"><span data-stu-id="31725-255">Handle null values</span></span>

<span data-ttu-id="31725-256">默认情况下，序列化程序处理 null 值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="31725-256">By default, the serializer handles null values as follows:</span></span>

* <span data-ttu-id="31725-257">对于引用类型和 `Nullable<T>` 类型：</span><span class="sxs-lookup"><span data-stu-id="31725-257">For reference types and `Nullable<T>` types:</span></span>

  * <span data-ttu-id="31725-258">它在序列化时不会将 `null` 传递到自定义转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-258">It does not pass `null` to custom converters on serialization.</span></span>
  * <span data-ttu-id="31725-259">它在反序列化时不会将 `JsonTokenType.Null` 传递到自定义转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-259">It does not pass `JsonTokenType.Null` to custom converters on deserialization.</span></span>
  * <span data-ttu-id="31725-260">它在反序列化时返回 `null` 实例。</span><span class="sxs-lookup"><span data-stu-id="31725-260">It returns a `null` instance on deserialization.</span></span>
  * <span data-ttu-id="31725-261">它在序列化时直接使用编写器写入 `null`。</span><span class="sxs-lookup"><span data-stu-id="31725-261">It writes `null` directly with the writer on serialization.</span></span>

* <span data-ttu-id="31725-262">对于不可为 null 的值类型：</span><span class="sxs-lookup"><span data-stu-id="31725-262">For non-nullable value types:</span></span>

  * <span data-ttu-id="31725-263">它在反序列化时将 `JsonTokenType.Null` 传递到自定义转换器。</span><span class="sxs-lookup"><span data-stu-id="31725-263">It passes `JsonTokenType.Null` to custom converters on deserialization.</span></span> <span data-ttu-id="31725-264">（如果没有可用的自定义转换器，则由该类型的内部转换器引发 `JsonException` 异常。）</span><span class="sxs-lookup"><span data-stu-id="31725-264">(If no custom converter is available, a `JsonException` exception is thrown by the internal converter for the type.)</span></span>

<span data-ttu-id="31725-265">此 null 处理行为主要用于，通过跳过对转换器的额外调用来优化性能。</span><span class="sxs-lookup"><span data-stu-id="31725-265">This null-handling behavior is primarily to optimize performance by skipping an extra call to the converter.</span></span> <span data-ttu-id="31725-266">此外，它可避免在每个 `Read` 和 `Write` 方法重写开始时强制可以为 null 的类型的转换器检查 `null`。</span><span class="sxs-lookup"><span data-stu-id="31725-266">In addition, it avoids forcing converters for nullable types to check for `null` at the start of every `Read` and `Write` method override.</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="31725-267">若要启用自定义转换器来处理引用或值类型的 `null`，请重写 <xref::::no-loc(System.Text.Json):::.Serialization.JsonConverter%601.HandleNull%2A?displayProperty=nameWithType> 以返回 `true`，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="31725-267">To enable a custom converter to handle `null` for a reference or value type, override <xref::::no-loc(System.Text.Json):::.Serialization.JsonConverter%601.HandleNull%2A?displayProperty=nameWithType> to return `true`, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/CustomConverterHandleNull.cs" highlight="19":::
::: zone-end

## <a name="other-custom-converter-samples"></a><span data-ttu-id="31725-268">其他自定义转换器示例</span><span class="sxs-lookup"><span data-stu-id="31725-268">Other custom converter samples</span></span>

<span data-ttu-id="31725-269">[从 :::no-loc(Newtonsoft.Json)::: 迁移到 :::no-loc(System.Text.Json):::](system-text-json-migrate-from-newtonsoft-how-to.md) 一文包含自定义转换器的其他示例。</span><span class="sxs-lookup"><span data-stu-id="31725-269">The [Migrate from :::no-loc(Newtonsoft.Json)::: to :::no-loc(System.Text.Json):::](system-text-json-migrate-from-newtonsoft-how-to.md) article contains additional samples of custom converters.</span></span>

<span data-ttu-id="31725-270">`:::no-loc(System.Text.Json):::.Serialization` 源代码中的[单元测试文件夹](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/)包含其他自定义转换器示例，例如：</span><span class="sxs-lookup"><span data-stu-id="31725-270">The [unit tests folder](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/) in the `:::no-loc(System.Text.Json):::.Serialization` source code includes other custom converter samples, such as:</span></span>

* <span data-ttu-id="31725-271">[在反序列化时将 null 转换为 0 的 Int32 转换器](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/CustomConverterTests.NullValueType.cs)</span><span class="sxs-lookup"><span data-stu-id="31725-271">[Int32 converter that converts null to 0 on deserialize](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/CustomConverterTests.NullValueType.cs)</span></span>
* <span data-ttu-id="31725-272">[在反序列化时允许同时使用字符串和数字值的 Int32 转换器](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/CustomConverterTests.Int32.cs)</span><span class="sxs-lookup"><span data-stu-id="31725-272">[Int32 converter that allows both string and number values on deserialize](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/CustomConverterTests.Int32.cs)</span></span>
* <span data-ttu-id="31725-273">[枚举转换器](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/CustomConverterTests.Enum.cs)</span><span class="sxs-lookup"><span data-stu-id="31725-273">[Enum converter](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/CustomConverterTests.Enum.cs)</span></span>
* <span data-ttu-id="31725-274">接受外部数据的 [List\<T> 转换器](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/CustomConverterTests.List.cs)</span><span class="sxs-lookup"><span data-stu-id="31725-274">[List\<T> converter that accepts external data](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/CustomConverterTests.List.cs)</span></span>
* <span data-ttu-id="31725-275">[处理以逗号分隔的数字列表的 Long[] 转换器](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/CustomConverterTests.Array.cs)</span><span class="sxs-lookup"><span data-stu-id="31725-275">[Long[] converter that works with a comma-delimited list of numbers](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/tests/Serialization/CustomConverterTests.Array.cs)</span></span>

<span data-ttu-id="31725-276">如果需要创建修改现有内置转换器行为的转换器，则可以获取[现有转换器的源代码](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/src/System/Text/Json/Serialization/Converters)作为自定义的起点。</span><span class="sxs-lookup"><span data-stu-id="31725-276">If you need to make a converter that modifies the behavior of an existing built-in converter, you can get [the source code of the existing converter](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/src/System/Text/Json/Serialization/Converters) to serve as a starting point for customization.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="31725-277">其他资源</span><span class="sxs-lookup"><span data-stu-id="31725-277">Additional resources</span></span>

* <span data-ttu-id="31725-278">[内置转换器的源代码](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/src/System/Text/Json/Serialization/Converters)</span><span class="sxs-lookup"><span data-stu-id="31725-278">[Source code for built-in converters](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/src/System/Text/Json/Serialization/Converters)</span></span>
* [<span data-ttu-id="31725-279">:::no-loc(System.Text.Json)::: 中的 DateTime 和 DateTimeOffset 支持</span><span class="sxs-lookup"><span data-stu-id="31725-279">DateTime and DateTimeOffset support in :::no-loc(System.Text.Json):::</span></span>](../datetime/system-text-json-support.md)
* [<span data-ttu-id="31725-280">:::no-loc(System.Text.Json)::: 概述</span><span class="sxs-lookup"><span data-stu-id="31725-280">:::no-loc(System.Text.Json)::: overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="31725-281">如何使用 :::no-loc(System.Text.Json):::</span><span class="sxs-lookup"><span data-stu-id="31725-281">How to use :::no-loc(System.Text.Json):::</span></span>](system-text-json-how-to.md)
* [<span data-ttu-id="31725-282">如何从 :::no-loc(Newtonsoft.Json)::: 迁移</span><span class="sxs-lookup"><span data-stu-id="31725-282">How to migrate from :::no-loc(Newtonsoft.Json):::</span></span>](system-text-json-migrate-from-newtonsoft-how-to.md)
* <span data-ttu-id="31725-283">[:::no-loc(System.Text.Json)::: API 参考](xref::::no-loc(System.Text.Json):::)</span><span class="sxs-lookup"><span data-stu-id="31725-283">[:::no-loc(System.Text.Json)::: API reference](xref::::no-loc(System.Text.Json):::)</span></span>
* <span data-ttu-id="31725-284">[:::no-loc(System.Text.Json):::.Serialization API 参考](xref::::no-loc(System.Text.Json):::.Serialization)</span><span class="sxs-lookup"><span data-stu-id="31725-284">[:::no-loc(System.Text.Json):::.Serialization API reference](xref::::no-loc(System.Text.Json):::.Serialization)</span></span>
<!-- * [:::no-loc(System.Text.Json)::: roadmap](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/:::no-loc(System.Text.Json):::/roadmap/README.md)-->
