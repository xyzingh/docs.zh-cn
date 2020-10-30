---
title: 在各时区之间转换时间
description: 了解如何在 .NET 中将从一个时区转换到另一个时区之间的时间。 还了解如何转换具有有限时区感知功能的 DateTimeOffset 值。
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- times [.NET], converting
- time zones [.NET], conversions
- UTC times, converting
- converting times
- local time conversions
ms.assetid: a51e1a3b-c983-4320-b31a-1f9fa3cf824a
ms.openlocfilehash: 3539b3c2b71be331bdea3161b7e8ba6da407cbab
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93063828"
---
# <a name="converting-times-between-time-zones"></a><span data-ttu-id="e40ca-104">在各时区之间转换时间</span><span class="sxs-lookup"><span data-stu-id="e40ca-104">Converting times between time zones</span></span>

<span data-ttu-id="e40ca-105">对任何使用日期和时间的应用程序而言，处理各时区之间的差异变得愈发重要。</span><span class="sxs-lookup"><span data-stu-id="e40ca-105">It is becoming increasingly important for any application that works with dates and times to handle differences between time zones.</span></span> <span data-ttu-id="e40ca-106">应用程序不能再假设所有时间都能用本地时间表示，这是从结构中可用的时间 <xref:System.DateTime> 。</span><span class="sxs-lookup"><span data-stu-id="e40ca-106">An application can no longer assume that all times can be expressed in the local time, which is the time available from the <xref:System.DateTime> structure.</span></span> <span data-ttu-id="e40ca-107">例如，显示美国东部当前时间的网页对东亚客户而言缺乏可信度。</span><span class="sxs-lookup"><span data-stu-id="e40ca-107">For example, a Web page that displays the current time in the eastern part of the United States will lack credibility to a customer in eastern Asia.</span></span> <span data-ttu-id="e40ca-108">本主题介绍如何将时间从一个时区转换到另一个时区，以及如何转换具有时区 <xref:System.DateTimeOffset> 感知限制的值。</span><span class="sxs-lookup"><span data-stu-id="e40ca-108">This topic explains how to convert times from one time zone to another, as well as how to convert <xref:System.DateTimeOffset> values that have limited time zone awareness.</span></span>

## <a name="converting-to-coordinated-universal-time"></a><span data-ttu-id="e40ca-109">转换为协调世界时</span><span class="sxs-lookup"><span data-stu-id="e40ca-109">Converting to Coordinated Universal Time</span></span>

<span data-ttu-id="e40ca-110">协调世界时 (UTC) 是一项高精度的原子时标准。</span><span class="sxs-lookup"><span data-stu-id="e40ca-110">Coordinated Universal Time (UTC) is a high-precision, atomic time standard.</span></span> <span data-ttu-id="e40ca-111">世界的时区表示为与 UTC 的正偏移量或负偏移量。</span><span class="sxs-lookup"><span data-stu-id="e40ca-111">The world's time zones are expressed as positive or negative offsets from UTC.</span></span> <span data-ttu-id="e40ca-112">因此，UTC 提供一种无时区或中间时区的时间。</span><span class="sxs-lookup"><span data-stu-id="e40ca-112">Thus, UTC provides a kind of time-zone free or time-zone neutral time.</span></span> <span data-ttu-id="e40ca-113">如果日期和时间在计算机之间的可移植性非常重要，则建议使用 UTC 时间。</span><span class="sxs-lookup"><span data-stu-id="e40ca-113">The use of UTC time is recommended when a date and time's portability across computers is important.</span></span> <span data-ttu-id="e40ca-114"> (有关使用日期和时间的详细信息和其他最佳做法，请参阅在 [.NET Framework 中使用 DateTime 的编码最佳做法](/previous-versions/dotnet/articles/ms973825(v=msdn.10))。 ) 将各个时区转换为 UTC 可简化时间比较。</span><span class="sxs-lookup"><span data-stu-id="e40ca-114">(For details and other best practices using dates and times, see [Coding best practices using DateTime in the .NET Framework](/previous-versions/dotnet/articles/ms973825(v=msdn.10)).) Converting individual time zones to UTC makes time comparisons easy.</span></span>

> [!NOTE]
> <span data-ttu-id="e40ca-115">您还可以 <xref:System.DateTimeOffset> 对结构进行序列化以明确表示单个时间点。</span><span class="sxs-lookup"><span data-stu-id="e40ca-115">You can also serialize a <xref:System.DateTimeOffset> structure to unambiguously represent a single point in time.</span></span> <span data-ttu-id="e40ca-116">由于 <xref:System.DateTimeOffset> 对象会存储日期和时间值以及其相对于 utc 的偏移量，因此，它们始终表示与 utc 的关系中的特定时间点。</span><span class="sxs-lookup"><span data-stu-id="e40ca-116">Because <xref:System.DateTimeOffset> objects store a date and time value along with its offset from UTC, they always represent a particular point in time in relationship to UTC.</span></span>

<span data-ttu-id="e40ca-117">将时间转换为 UTC 的最简单方法是 `static` `Shared` 在 Visual Basic) 方法中调用 (<xref:System.TimeZoneInfo.ConvertTimeToUtc%28System.DateTime%29?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="e40ca-117">The easiest way to convert a time to UTC is to call the `static` (`Shared` in Visual Basic) <xref:System.TimeZoneInfo.ConvertTimeToUtc%28System.DateTime%29?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="e40ca-118">方法所执行的确切转换取决于 `dateTime` 参数的属性的值，如下 <xref:System.DateTime.Kind%2A> 表所示。</span><span class="sxs-lookup"><span data-stu-id="e40ca-118">The exact conversion performed by the method depends on the value of the `dateTime` parameter's <xref:System.DateTime.Kind%2A> property, as the following table shows.</span></span>

| `DateTime.Kind`            | <span data-ttu-id="e40ca-119">转换</span><span class="sxs-lookup"><span data-stu-id="e40ca-119">Conversion</span></span>                                                                     |
| -------------------------- | ------------------------------------------------------------------------------ |
| `DateTimeKind.Local`       | <span data-ttu-id="e40ca-120">将本地时间转换为 UTC。</span><span class="sxs-lookup"><span data-stu-id="e40ca-120">Converts local time to UTC.</span></span>                                                    |
| `DateTimeKind.Unspecified` | <span data-ttu-id="e40ca-121">假定 `dateTime` 参数为本地时间并将本地时间转换为 UTC。</span><span class="sxs-lookup"><span data-stu-id="e40ca-121">Assumes the `dateTime` parameter is local time and converts local time to UTC.</span></span> |
| `DateTimeKind.Utc`         | <span data-ttu-id="e40ca-122">返回未更改的 `dateTime` 参数。</span><span class="sxs-lookup"><span data-stu-id="e40ca-122">Returns the `dateTime` parameter unchanged.</span></span>                                    |

<span data-ttu-id="e40ca-123">以下代码可将当前本地时间转换为 UTC，并将结果显示在控制台上。</span><span class="sxs-lookup"><span data-stu-id="e40ca-123">The following code converts the current local time to UTC and displays the result to the console.</span></span>

[!code-csharp[System.TimeZone2.Concepts#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#6)]
[!code-vb[System.TimeZone2.Concepts#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#6)]

<span data-ttu-id="e40ca-124">如果日期和时间值不表示本地时间或 UTC，则该 <xref:System.DateTime.ToUniversalTime%2A> 方法可能会返回错误的结果。</span><span class="sxs-lookup"><span data-stu-id="e40ca-124">If the date and time value does not represent either the local time or UTC, the <xref:System.DateTime.ToUniversalTime%2A> method will likely return an erroneous result.</span></span> <span data-ttu-id="e40ca-125">但是，您可以使用 <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A?displayProperty=nameWithType> 方法来转换指定时区的日期和时间。</span><span class="sxs-lookup"><span data-stu-id="e40ca-125">However, you can use the <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A?displayProperty=nameWithType> method to convert the date and time from a specified time zone.</span></span> <span data-ttu-id="e40ca-126"> (有关检索表示目标时区的对象的详细信息 <xref:System.TimeZoneInfo> ，请参阅 [查找本地系统上定义的时区](finding-the-time-zones-on-local-system.md)。 ) 下面的代码使用 <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A?displayProperty=nameWithType> 方法将东部标准时间转换为 UTC。</span><span class="sxs-lookup"><span data-stu-id="e40ca-126">(For details on retrieving a <xref:System.TimeZoneInfo> object that represents the destination time zone, see [Finding the time zones defined on a local system](finding-the-time-zones-on-local-system.md).) The following code uses the <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A?displayProperty=nameWithType> method to convert Eastern Standard Time to UTC.</span></span>

[!code-csharp[System.TimeZone2.Concepts#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#7)]
[!code-vb[System.TimeZone2.Concepts#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#7)]

<span data-ttu-id="e40ca-127">请注意， <xref:System.ArgumentException> 如果 <xref:System.DateTime> 对象的 <xref:System.DateTime.Kind%2A> 属性与时区不匹配，此方法将引发。</span><span class="sxs-lookup"><span data-stu-id="e40ca-127">Note that this method throws an <xref:System.ArgumentException> if the <xref:System.DateTime> object's <xref:System.DateTime.Kind%2A> property and the time zone are mismatched.</span></span> <span data-ttu-id="e40ca-128">如果 <xref:System.DateTime.Kind%2A> 属性为 <xref:System.DateTimeKind.Local?displayProperty=nameWithType> <xref:System.TimeZoneInfo> ，但对象不表示本地时区，或者 <xref:System.DateTime.Kind%2A> 属性为 <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> 但对象不 <xref:System.TimeZoneInfo> 相等， <xref:System.TimeZoneInfo.Utc?displayProperty=nameWithType> 则会发生不匹配。</span><span class="sxs-lookup"><span data-stu-id="e40ca-128">A mismatch occurs if the <xref:System.DateTime.Kind%2A> property is <xref:System.DateTimeKind.Local?displayProperty=nameWithType> but the <xref:System.TimeZoneInfo> object does not represent the local time zone, or if the <xref:System.DateTime.Kind%2A> property is <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> but the <xref:System.TimeZoneInfo> object does not equal <xref:System.TimeZoneInfo.Utc?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="e40ca-129">所有这些方法都 <xref:System.DateTime> 将值作为参数，并返回一个 <xref:System.DateTime> 值。</span><span class="sxs-lookup"><span data-stu-id="e40ca-129">All of these methods take <xref:System.DateTime> values as parameters and return a <xref:System.DateTime> value.</span></span> <span data-ttu-id="e40ca-130">对于 <xref:System.DateTimeOffset> 值， <xref:System.DateTimeOffset> 结构具有 <xref:System.DateTimeOffset.ToUniversalTime%2A> 实例方法，该方法可将当前实例的日期和时间转换为 UTC。</span><span class="sxs-lookup"><span data-stu-id="e40ca-130">For <xref:System.DateTimeOffset> values, the <xref:System.DateTimeOffset> structure has a <xref:System.DateTimeOffset.ToUniversalTime%2A> instance method that converts the date and time of the current instance to UTC.</span></span> <span data-ttu-id="e40ca-131">下面的示例调用方法，将 <xref:System.DateTimeOffset.ToUniversalTime%2A> 本地时间和几个其他时间转换为协调世界时 (UTC) 。</span><span class="sxs-lookup"><span data-stu-id="e40ca-131">The following example calls the <xref:System.DateTimeOffset.ToUniversalTime%2A> method to convert a local time and several other times to Coordinated Universal Time (UTC).</span></span>

[!code-csharp[System.DateTimeOffset.Methods#16](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Methods/cs/Methods.cs#16)]
[!code-vb[System.DateTimeOffset.Methods#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Methods/vb/Methods.vb#16)]

## <a name="converting-utc-to-a-designated-time-zone"></a><span data-ttu-id="e40ca-132">将 UTC 转换为指定的时区</span><span class="sxs-lookup"><span data-stu-id="e40ca-132">Converting UTC to a designated time zone</span></span>

<span data-ttu-id="e40ca-133">若要将 UTC 转换为本地时间，请参阅后面的 "将 UTC 转换为本地时间" 一节。</span><span class="sxs-lookup"><span data-stu-id="e40ca-133">To convert UTC to local time, see the "Converting UTC to Local Time" section that follows.</span></span> <span data-ttu-id="e40ca-134">若要将 UTC 转换为任何指定时区中的时间，请调用 <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="e40ca-134">To convert UTC to the time in any time zone that you designate, call the <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A> method.</span></span> <span data-ttu-id="e40ca-135">该方法采用以下两种参数：</span><span class="sxs-lookup"><span data-stu-id="e40ca-135">The method takes two parameters:</span></span>

- <span data-ttu-id="e40ca-136">要转换的 UTC。</span><span class="sxs-lookup"><span data-stu-id="e40ca-136">The UTC to convert.</span></span> <span data-ttu-id="e40ca-137">这必须是 <xref:System.DateTime> 其 <xref:System.DateTime.Kind%2A> 属性设置为或的值 `Unspecified` `Utc` 。</span><span class="sxs-lookup"><span data-stu-id="e40ca-137">This must be a <xref:System.DateTime> value whose <xref:System.DateTime.Kind%2A> property is set to `Unspecified` or `Utc`.</span></span>

- <span data-ttu-id="e40ca-138">UTC 要转换的目标时区。</span><span class="sxs-lookup"><span data-stu-id="e40ca-138">The time zone to convert the UTC to.</span></span>

<span data-ttu-id="e40ca-139">以下代码可将 UTC 转换为中部标准时间。</span><span class="sxs-lookup"><span data-stu-id="e40ca-139">The following code converts UTC to Central Standard Time.</span></span>

[!code-csharp[System.TimeZone2.Concepts#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#8)]
[!code-vb[System.TimeZone2.Concepts#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#8)]

## <a name="converting-utc-to-local-time"></a><span data-ttu-id="e40ca-140">将 UTC 转换为本地时间</span><span class="sxs-lookup"><span data-stu-id="e40ca-140">Converting UTC to local time</span></span>

<span data-ttu-id="e40ca-141">若要将 UTC 转换为本地时间，请调用 <xref:System.DateTime.ToLocalTime%2A> <xref:System.DateTime> 要转换其时间的对象的方法。</span><span class="sxs-lookup"><span data-stu-id="e40ca-141">To convert UTC to local time, call the <xref:System.DateTime.ToLocalTime%2A> method of the <xref:System.DateTime> object whose time you want to convert.</span></span> <span data-ttu-id="e40ca-142">此方法的确切行为取决于对象的 <xref:System.DateTime.Kind%2A> 属性值，如下表所示。</span><span class="sxs-lookup"><span data-stu-id="e40ca-142">The exact behavior of the method depends on the value of the object's <xref:System.DateTime.Kind%2A> property, as the following table shows.</span></span>

| `DateTime.Kind`            | <span data-ttu-id="e40ca-143">转换</span><span class="sxs-lookup"><span data-stu-id="e40ca-143">Conversion</span></span>                                                                               |
| -------------------------- | ---------------------------------------------------------------------------------------- |
| `DateTimeKind.Local`       | <span data-ttu-id="e40ca-144">返回 <xref:System.DateTime> 未更改的值。</span><span class="sxs-lookup"><span data-stu-id="e40ca-144">Returns the <xref:System.DateTime> value unchanged.</span></span>                                      |
| `DateTimeKind.Unspecified` | <span data-ttu-id="e40ca-145">假定 <xref:System.DateTime> 值为 utc 并将 utc 转换为本地时间。</span><span class="sxs-lookup"><span data-stu-id="e40ca-145">Assumes that the <xref:System.DateTime> value is UTC and converts the UTC to local time.</span></span> |
| `DateTimeKind.Utc`         | <span data-ttu-id="e40ca-146">将 <xref:System.DateTime> 值转换为本地时间。</span><span class="sxs-lookup"><span data-stu-id="e40ca-146">Converts the <xref:System.DateTime> value to local time.</span></span>                                 |

> [!NOTE]
> <span data-ttu-id="e40ca-147">此 <xref:System.TimeZone.ToLocalTime%2A?displayProperty=nameWithType> 方法的行为与 `DateTime.ToLocalTime` 方法相同。</span><span class="sxs-lookup"><span data-stu-id="e40ca-147">The <xref:System.TimeZone.ToLocalTime%2A?displayProperty=nameWithType> method behaves identically to the `DateTime.ToLocalTime` method.</span></span> <span data-ttu-id="e40ca-148">它采用单个参数，即要转换的日期和时间值。</span><span class="sxs-lookup"><span data-stu-id="e40ca-148">It takes a single parameter, which is the date and time value to convert.</span></span>

<span data-ttu-id="e40ca-149">还可以通过使用 `static` `Shared` Visual Basic) 方法中的 (，将任何指定时区中的时间转换为本地时间 <xref:System.TimeZoneInfo.ConvertTime%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="e40ca-149">You can also convert the time in any designated time zone to local time by using the `static` (`Shared` in Visual Basic) <xref:System.TimeZoneInfo.ConvertTime%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="e40ca-150">下一节将讨论此方法。</span><span class="sxs-lookup"><span data-stu-id="e40ca-150">This technique is discussed in the next section.</span></span>

## <a name="converting-between-any-two-time-zones"></a><span data-ttu-id="e40ca-151">在任意两个时区之间转换</span><span class="sxs-lookup"><span data-stu-id="e40ca-151">Converting between any two time zones</span></span>

<span data-ttu-id="e40ca-152">您可以通过使用 `static` `Shared` 类的 Visual Basic) 方法中的以下两个 (之一在任意两个时区之间进行转换 <xref:System.TimeZoneInfo> ：</span><span class="sxs-lookup"><span data-stu-id="e40ca-152">You can convert between any two time zones by using either of the following two `static` (`Shared` in Visual Basic) methods of the <xref:System.TimeZoneInfo> class:</span></span>

- <xref:System.TimeZoneInfo.ConvertTime%2A>

  <span data-ttu-id="e40ca-153">此方法的参数是要转换的日期和时间值、 `TimeZoneInfo` 表示日期和时间值的时区的对象，以及 `TimeZoneInfo` 表示将日期和时间值转换为的时区的对象。</span><span class="sxs-lookup"><span data-stu-id="e40ca-153">This method's parameters are the date and time value to convert, a `TimeZoneInfo` object that represents the time zone of the date and time value, and a `TimeZoneInfo` object that represents the time zone to convert the date and time value to.</span></span>

- <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A>

  <span data-ttu-id="e40ca-154">此方法的参数是要转换的日期和时间值、日期和时间值的时区的标识符，以及要将日期和时间值转换为的时区的标识符。</span><span class="sxs-lookup"><span data-stu-id="e40ca-154">This method's parameters are the date and time value to convert, the identifier of the date and time value's time zone, and the identifier of the time zone to convert the date and time value to.</span></span>

<span data-ttu-id="e40ca-155">这两种方法都要求 <xref:System.DateTime.Kind%2A> 要转换的日期和时间值的属性，以及 <xref:System.TimeZoneInfo> 表示其时区的对象或时区标识符彼此对应。</span><span class="sxs-lookup"><span data-stu-id="e40ca-155">Both methods require that the <xref:System.DateTime.Kind%2A> property of the date and time value to convert and the <xref:System.TimeZoneInfo> object or time zone identifier that represents its time zone correspond to one another.</span></span> <span data-ttu-id="e40ca-156">否则会引发 <xref:System.ArgumentException>。</span><span class="sxs-lookup"><span data-stu-id="e40ca-156">Otherwise, an <xref:System.ArgumentException> is thrown.</span></span> <span data-ttu-id="e40ca-157">例如，如果 `Kind` 日期和时间值的属性为 `DateTimeKind.Local` ，则当 `TimeZoneInfo` 作为参数传递给方法的对象不等于时，将引发异常 `TimeZoneInfo.Local` 。</span><span class="sxs-lookup"><span data-stu-id="e40ca-157">For example, if the `Kind` property of the date and time value is `DateTimeKind.Local`, an exception is thrown if the `TimeZoneInfo` object passed as a parameter to the method is not equal to `TimeZoneInfo.Local`.</span></span> <span data-ttu-id="e40ca-158">如果作为参数传递给该方法的标识符不等于，则也会引发异常 `TimeZoneInfo.Local.Id` 。</span><span class="sxs-lookup"><span data-stu-id="e40ca-158">An exception is also thrown if the identifier passed as a parameter to the method is not equal to `TimeZoneInfo.Local.Id`.</span></span>

<span data-ttu-id="e40ca-159">下面的示例使用 <xref:System.TimeZoneInfo.ConvertTime%2A> 方法将夏威夷标准时间转换为本地时间。</span><span class="sxs-lookup"><span data-stu-id="e40ca-159">The following example uses the <xref:System.TimeZoneInfo.ConvertTime%2A> method to convert from Hawaiian Standard Time to local time.</span></span>

[!code-csharp[System.TimeZone2.Concepts#9](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#9)]
[!code-vb[System.TimeZone2.Concepts#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#9)]

## <a name="converting-datetimeoffset-values"></a><span data-ttu-id="e40ca-160">转换 DateTimeOffset 值</span><span class="sxs-lookup"><span data-stu-id="e40ca-160">Converting DateTimeOffset values</span></span>

<span data-ttu-id="e40ca-161">对象所表示的日期和时间值 <xref:System.DateTimeOffset> 不能完全识别时区，因为在实例化对象时，对象与其时区无关。</span><span class="sxs-lookup"><span data-stu-id="e40ca-161">Date and time values represented by <xref:System.DateTimeOffset> objects are not fully time-zone aware because the object is disassociated from its time zone at the time it is instantiated.</span></span> <span data-ttu-id="e40ca-162">但是，大多数情况下，应用程序仅需根据两种相对于 UTC 的偏移量，而不是特定时区的时间来转换日期和时间。</span><span class="sxs-lookup"><span data-stu-id="e40ca-162">However, in many cases an application simply needs to convert a date and time based on two different offsets from UTC rather than on the time in particular time zones.</span></span> <span data-ttu-id="e40ca-163">若要执行此转换，可以调用当前实例的 <xref:System.DateTimeOffset.ToOffset%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="e40ca-163">To perform this conversion, you can call the current instance's <xref:System.DateTimeOffset.ToOffset%2A> method.</span></span> <span data-ttu-id="e40ca-164">该方法的单个参数是此方法要返回的新日期和时间值的偏移量。</span><span class="sxs-lookup"><span data-stu-id="e40ca-164">The method's single parameter is the offset of the new date and time value that the method is to return.</span></span>

<span data-ttu-id="e40ca-165">例如，如果用户所请求网页的日期和时间已知，并且已被序列化为 MM/dd/yyyy hh:mm:ss zzzz 格式的字符串，以下 `ReturnTimeOnServer` 方法会将此日期和时间值转换为 Web 服务器上的日期和时间。</span><span class="sxs-lookup"><span data-stu-id="e40ca-165">For example, if the date and time of a user request for a Web page is known and is serialized as a string in the format MM/dd/yyyy hh:mm:ss zzzz, the following `ReturnTimeOnServer` method converts this date and time value to the date and time on the Web server.</span></span>

[!code-csharp[System.DateTimeOffset.Conceptual.OffsetConversions#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/cs/TimeConversions.cs#1)]
[!code-vb[System.DateTimeOffset.Conceptual.OffsetConversions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/vb/TimeConversions.vb#1)]

<span data-ttu-id="e40ca-166">如果向该方法传递字符串“9/1/2007 5:32:07 -05:00”（表示比 UTC 早五个小时的时区中的日期和时间），则对于处在美国太平洋标准时区中的服务器，它将返回 9/1/2007 3:32:07 AM -07:00。</span><span class="sxs-lookup"><span data-stu-id="e40ca-166">If the method is passed the string "9/1/2007 5:32:07 -05:00", which represents the date and time in a time zone five hours earlier than UTC, it returns 9/1/2007 3:32:07 AM -07:00 for a server located in the U.S. Pacific Standard Time zone.</span></span>

<span data-ttu-id="e40ca-167"><xref:System.TimeZoneInfo>类还包含 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> 方法的重载，该重载使用值执行时区转换 <xref:System.DateTimeOffset.ToOffset(System.TimeSpan)> 。</span><span class="sxs-lookup"><span data-stu-id="e40ca-167">The <xref:System.TimeZoneInfo> class also includes an overload of the <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> method that performs time zone conversions with <xref:System.DateTimeOffset.ToOffset(System.TimeSpan)> values.</span></span> <span data-ttu-id="e40ca-168">此方法的参数是一个值和一个对要将时间转换到的时区的 <xref:System.DateTimeOffset> 引用。</span><span class="sxs-lookup"><span data-stu-id="e40ca-168">The method's parameters are a <xref:System.DateTimeOffset> value and a reference to the time zone to which the time is to be converted.</span></span> <span data-ttu-id="e40ca-169">方法调用将返回一个 <xref:System.DateTimeOffset> 值。</span><span class="sxs-lookup"><span data-stu-id="e40ca-169">The method call returns a <xref:System.DateTimeOffset> value.</span></span> <span data-ttu-id="e40ca-170">例如，可以 `ReturnTimeOnServer` 按如下所示重写上一示例中的方法，以调用 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29> 方法。</span><span class="sxs-lookup"><span data-stu-id="e40ca-170">For example, the `ReturnTimeOnServer` method in the previous example could be rewritten as follows to call the <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29> method.</span></span>

[!code-csharp[System.DateTimeOffset.Conceptual.OffsetConversions#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/cs/timeconversions2.cs#2)]
[!code-vb[System.DateTimeOffset.Conceptual.OffsetConversions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/vb/TimeConversions2.vb#2)]

## <a name="see-also"></a><span data-ttu-id="e40ca-171">另请参阅</span><span class="sxs-lookup"><span data-stu-id="e40ca-171">See also</span></span>

- <xref:System.TimeZoneInfo>
- [<span data-ttu-id="e40ca-172">日期、时间和时区</span><span class="sxs-lookup"><span data-stu-id="e40ca-172">Dates, times, and time zones</span></span>](index.md)
- [<span data-ttu-id="e40ca-173">查找本地系统上定义的时区</span><span class="sxs-lookup"><span data-stu-id="e40ca-173">Finding the time zones defined on a local system</span></span>](finding-the-time-zones-on-local-system.md)
