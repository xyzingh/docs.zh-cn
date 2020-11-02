---
title: 如何：往返行程日期和时间值
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- round-trip date and time values
- dates [.NET], round-trip values
- time zones [.NET], round-trip date and time values
- time [.NET], round-trip values
- formatting strings [.NET], round-trip values
ms.assetid: b609b277-edc6-4c74-b03e-ea73324ecbdb
ms.openlocfilehash: 4dce882e29afd5084dc84d3e176e6121c55f4af8
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889083"
---
# <a name="how-to-round-trip-date-and-time-values"></a><span data-ttu-id="290a1-102">如何：往返行程日期和时间值</span><span class="sxs-lookup"><span data-stu-id="290a1-102">How to: Round-trip Date and Time Values</span></span>

<span data-ttu-id="290a1-103">在许多应用程序中，日期和时间值旨在明确标识单个时间点。</span><span class="sxs-lookup"><span data-stu-id="290a1-103">In many applications, a date and time value is intended to unambiguously identify a single point in time.</span></span> <span data-ttu-id="290a1-104">本文演示了如何保存和还原 <xref:System.DateTime> 值、<xref:System.DateTimeOffset> 值以及包含时区信息的日期和时间值，以便还原后的值与保存的值标识的时间相同。</span><span class="sxs-lookup"><span data-stu-id="290a1-104">This article shows how to save and restore a <xref:System.DateTime> value, a <xref:System.DateTimeOffset> value, and a date and time value with time zone information so that the restored value identifies the same time as the saved value.</span></span>

## <a name="round-trip-a-datetime-value"></a><span data-ttu-id="290a1-105">往返 DateTime 值</span><span class="sxs-lookup"><span data-stu-id="290a1-105">Round-trip a DateTime value</span></span>

1. <span data-ttu-id="290a1-106">通过调用包含 "o" 格式说明符的 <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> 方法，将 <xref:System.DateTime> 值转换为字符串表示形式。</span><span class="sxs-lookup"><span data-stu-id="290a1-106">Convert the <xref:System.DateTime> value to its string representation by calling the <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> method with the "o" format specifier.</span></span>

2. <span data-ttu-id="290a1-107">将 <xref:System.DateTime> 值的字符串表示形式保存到文件中，或跨进程、应用域或计算机边界传递它。</span><span class="sxs-lookup"><span data-stu-id="290a1-107">Save the string representation of the <xref:System.DateTime> value to a file, or pass it across a process, application domain, or machine boundary.</span></span>

3. <span data-ttu-id="290a1-108">检索表示 <xref:System.DateTime> 值的字符串。</span><span class="sxs-lookup"><span data-stu-id="290a1-108">Retrieve the string that represents the <xref:System.DateTime> value.</span></span>

4. <span data-ttu-id="290a1-109">调用 <xref:System.DateTime.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=nameWithType> 方法，并以 `styles` 参数值的形式传递 <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="290a1-109">Call the <xref:System.DateTime.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=nameWithType> method, and pass <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType> as the value of the `styles` parameter.</span></span>

<span data-ttu-id="290a1-110">下面的示例展示了如何往返 <xref:System.DateTime> 值。</span><span class="sxs-lookup"><span data-stu-id="290a1-110">The following example illustrates how to round-trip a <xref:System.DateTime> value.</span></span>

[!code-csharp[Formatting.HowTo.RoundTrip#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#1)]
[!code-vb[Formatting.HowTo.RoundTrip#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#1)]

<span data-ttu-id="290a1-111">往返 <xref:System.DateTime> 值时，此方法成功暂留所有本地时间和世界时间。</span><span class="sxs-lookup"><span data-stu-id="290a1-111">When round-tripping a <xref:System.DateTime> value, this technique successfully preserves the time for all local and universal times.</span></span> <span data-ttu-id="290a1-112">例如，如果本地 <xref:System.DateTime> 值保存在采用美国太平洋标准时区的系统会，并在位于美国中部标准时区的系统上还原，则还原的日期和时间会比原始时间晚两个小时，这反映了两个时区之间的时差。</span><span class="sxs-lookup"><span data-stu-id="290a1-112">For example, if a local <xref:System.DateTime> value is saved on a system in the U.S. Pacific Standard Time zone and is restored on a system in the U.S. Central Standard Time zone, the restored date and time will be two hours later than the original time, which reflects the time difference between the two time zones.</span></span> <span data-ttu-id="290a1-113">但是，此方法对于未指定时间不一定准确。</span><span class="sxs-lookup"><span data-stu-id="290a1-113">However, this technique is not necessarily accurate for unspecified times.</span></span> <span data-ttu-id="290a1-114">所有 <xref:System.DateTime.Kind%2A> 属性为 <xref:System.DateTimeKind.Unspecified> 的 <xref:System.DateTime> 值都会被视为本地时间。</span><span class="sxs-lookup"><span data-stu-id="290a1-114">All <xref:System.DateTime> values whose <xref:System.DateTime.Kind%2A> property is <xref:System.DateTimeKind.Unspecified> are treated as if they are local times.</span></span> <span data-ttu-id="290a1-115">如果不是本地时间，则 <xref:System.DateTime> 不会成功标识正确的时间点。</span><span class="sxs-lookup"><span data-stu-id="290a1-115">If it's not a local time, the <xref:System.DateTime> doesn't successfully identify the correct point in time.</span></span> <span data-ttu-id="290a1-116">针对此限制的解决方法是将日期和时间值与其时区紧密耦合，以便进行保存和还原操作。</span><span class="sxs-lookup"><span data-stu-id="290a1-116">The workaround for this limitation is to tightly couple a date and time value with its time zone for the save and restore operation.</span></span>

## <a name="round-trip-a-datetimeoffset-value"></a><span data-ttu-id="290a1-117">往返 DateTimeOffset 值</span><span class="sxs-lookup"><span data-stu-id="290a1-117">Round-trip a DateTimeOffset value</span></span>

1. <span data-ttu-id="290a1-118">通过调用包含 "o" 格式说明符的 <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType> 方法，将 <xref:System.DateTimeOffset> 值转换为字符串表示形式。</span><span class="sxs-lookup"><span data-stu-id="290a1-118">Convert the <xref:System.DateTimeOffset> value to its string representation by calling the <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType> method with the "o" format specifier.</span></span>

2. <span data-ttu-id="290a1-119">将 <xref:System.DateTimeOffset> 值的字符串表示形式保存到文件中，或跨进程、应用域或计算机边界传递它。</span><span class="sxs-lookup"><span data-stu-id="290a1-119">Save the string representation of the <xref:System.DateTimeOffset> value to a file, or pass it across a process, application domain, or machine boundary.</span></span>

3. <span data-ttu-id="290a1-120">检索表示 <xref:System.DateTimeOffset> 值的字符串。</span><span class="sxs-lookup"><span data-stu-id="290a1-120">Retrieve the string that represents the <xref:System.DateTimeOffset> value.</span></span>

4. <span data-ttu-id="290a1-121">调用 <xref:System.DateTimeOffset.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=nameWithType> 方法，并以 `styles` 参数值的形式传递 <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="290a1-121">Call the <xref:System.DateTimeOffset.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=nameWithType> method, and pass <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType> as the value of the `styles` parameter.</span></span>

<span data-ttu-id="290a1-122">下面的示例展示了如何往返 <xref:System.DateTimeOffset> 值。</span><span class="sxs-lookup"><span data-stu-id="290a1-122">The following example illustrates how to round-trip a <xref:System.DateTimeOffset> value.</span></span>

[!code-csharp[Formatting.HowTo.RoundTrip#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#2)]
[!code-vb[Formatting.HowTo.RoundTrip#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#2)]

<span data-ttu-id="290a1-123">此方法始终将 <xref:System.DateTimeOffset> 值明确标识为单个时间点。</span><span class="sxs-lookup"><span data-stu-id="290a1-123">This technique always unambiguously identifies a <xref:System.DateTimeOffset> value as a single point in time.</span></span> <span data-ttu-id="290a1-124">然后，可以调用 <xref:System.DateTimeOffset.ToUniversalTime%2A?displayProperty=nameWithType> 方法，将此值转换为协调世界时 (UTC)；也可以调用 <xref:System.DateTimeOffset.ToOffset%2A?displayProperty=nameWithType> 或 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> 方法，将此值转换为特定时区时间。</span><span class="sxs-lookup"><span data-stu-id="290a1-124">The value can then be converted to Coordinated Universal Time (UTC) by calling the <xref:System.DateTimeOffset.ToUniversalTime%2A?displayProperty=nameWithType> method, or it can be converted to the time in a particular time zone by calling the <xref:System.DateTimeOffset.ToOffset%2A?displayProperty=nameWithType> or <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="290a1-125">此方法的主要限制在于，如果对表示特定时区时间的 <xref:System.DateTimeOffset> 值执行日期和时间算术，生成的结果对于相应时区来说可能并不准确。</span><span class="sxs-lookup"><span data-stu-id="290a1-125">The major limitation of this technique is that date and time arithmetic, when performed on a <xref:System.DateTimeOffset> value that represents the time in a particular time zone, may not produce accurate results for that time zone.</span></span> <span data-ttu-id="290a1-126">这是因为 <xref:System.DateTimeOffset> 值在实例化时就与时区解除关联。</span><span class="sxs-lookup"><span data-stu-id="290a1-126">This is because when a <xref:System.DateTimeOffset> value is instantiated, it is disassociated from its time zone.</span></span> <span data-ttu-id="290a1-127">因此，执行日期和时间计算时，无法再应用该时区的调整规则。</span><span class="sxs-lookup"><span data-stu-id="290a1-127">Therefore, that time zone's adjustment rules can no longer be applied when you perform date and time calculations.</span></span> <span data-ttu-id="290a1-128">可以通过定义包含日期和时间值以及其随附时区的自定义类型，来解决此问题。</span><span class="sxs-lookup"><span data-stu-id="290a1-128">You can work around this problem by defining a custom type that includes both a date and time value and its accompanying time zone.</span></span>

## <a name="round-trip-a-date-and-time-value-with-its-time-zone"></a><span data-ttu-id="290a1-129">往返包含时区信息的日期和时间值的具体步骤</span><span class="sxs-lookup"><span data-stu-id="290a1-129">Round-trip a date and time value with its time zone</span></span>

1. <span data-ttu-id="290a1-130">定义包含两个字段的类或结构。</span><span class="sxs-lookup"><span data-stu-id="290a1-130">Define a class or a structure with two fields.</span></span> <span data-ttu-id="290a1-131">第一个字段是 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 对象，第二个字段是 <xref:System.TimeZoneInfo> 对象。</span><span class="sxs-lookup"><span data-stu-id="290a1-131">The first field is either a <xref:System.DateTime> or a <xref:System.DateTimeOffset> object, and the second is a <xref:System.TimeZoneInfo> object.</span></span> <span data-ttu-id="290a1-132">下面的示例展示了这种类型的简单版本。</span><span class="sxs-lookup"><span data-stu-id="290a1-132">The following example is a simple version of such a type.</span></span>

    [!code-csharp[Formatting.HowTo.RoundTrip#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#3)]
    [!code-vb[Formatting.HowTo.RoundTrip#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#3)]

2. <span data-ttu-id="290a1-133">使用 <xref:System.SerializableAttribute> 属性标记类。</span><span class="sxs-lookup"><span data-stu-id="290a1-133">Mark the class with the <xref:System.SerializableAttribute> attribute.</span></span>

3. <span data-ttu-id="290a1-134">使用 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType> 方法串行化对象。</span><span class="sxs-lookup"><span data-stu-id="290a1-134">Serialize the object using the <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType> method.</span></span>

4. <span data-ttu-id="290a1-135">使用 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A> 方法还原对象。</span><span class="sxs-lookup"><span data-stu-id="290a1-135">Restore the object using the <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A> method.</span></span>

5. <span data-ttu-id="290a1-136">将反串行化的对象强制转换（在 C# 中）或转换（在 Visual Basic 中）为相应类型的对象。</span><span class="sxs-lookup"><span data-stu-id="290a1-136">Cast (in C#) or convert (in Visual Basic) the deserialized object to an object of the appropriate type.</span></span>

<span data-ttu-id="290a1-137">下面的示例展示了如何往返同时存储时区以及日期和时间信息的对象。</span><span class="sxs-lookup"><span data-stu-id="290a1-137">The following example illustrates how to round-trip an object that stores both time zone and date and time information.</span></span>

[!code-csharp[Formatting.HowTo.RoundTrip#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#4)]
[!code-vb[Formatting.HowTo.RoundTrip#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#4)]

<span data-ttu-id="290a1-138">此方法应始终在保存和还原时间前后明确反映正确的时间点，前提是组合的日期和时间及时区对象的实现不允许日期值与时区值不同步。</span><span class="sxs-lookup"><span data-stu-id="290a1-138">This technique should always unambiguously reflect the correct point of time both before and after it is saved and restored, provided that the implementation of the combined date and time and time zone object does not allow the date value to become out of sync with the time zone value.</span></span>

## <a name="compile-the-code"></a><span data-ttu-id="290a1-139">编译代码</span><span class="sxs-lookup"><span data-stu-id="290a1-139">Compile the code</span></span>

<span data-ttu-id="290a1-140">这些示例需要：</span><span class="sxs-lookup"><span data-stu-id="290a1-140">These examples require that:</span></span>

- <span data-ttu-id="290a1-141">使用 C# `using` 指令或 Visual Basic `Imports` 语句导入下列命名空间：</span><span class="sxs-lookup"><span data-stu-id="290a1-141">The following namespaces be imported with C# `using` directives or Visual Basic `Imports` statements:</span></span>

  - <span data-ttu-id="290a1-142"><xref:System>（仅限 C#）</span><span class="sxs-lookup"><span data-stu-id="290a1-142"><xref:System> (C# only)</span></span>

  - <xref:System.Globalization?displayProperty=nameWithType>

  - <xref:System.IO?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.Formatters.Binary?displayProperty=nameWithType>

- <span data-ttu-id="290a1-143">每个代码示例（`DateInTimeZone` 除外）都添加到类或 Visual Basic 模块中，且被包装到方法中，并通过 `Main` 进行调用。</span><span class="sxs-lookup"><span data-stu-id="290a1-143">Each code example, other than the `DateInTimeZone` class, be included in a class or Visual Basic module, wrapped in methods, and called from the `Main` method.</span></span>

## <a name="see-also"></a><span data-ttu-id="290a1-144">请参阅</span><span class="sxs-lookup"><span data-stu-id="290a1-144">See also</span></span>

- [<span data-ttu-id="290a1-145">在 DateTime、DateTimeOffset、TimeSpan 和 TimeZoneInfo 之间进行选择</span><span class="sxs-lookup"><span data-stu-id="290a1-145">Choosing Between DateTime, DateTimeOffset, TimeSpan, and TimeZoneInfo</span></span>](../datetime/choosing-between-datetime.md)
- [<span data-ttu-id="290a1-146">标准日期和时间格式字符串</span><span class="sxs-lookup"><span data-stu-id="290a1-146">Standard Date and Time Format Strings</span></span>](standard-date-and-time-format-strings.md)
