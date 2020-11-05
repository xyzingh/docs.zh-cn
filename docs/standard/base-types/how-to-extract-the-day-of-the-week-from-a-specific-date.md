---
title: 如何：从特定日期中提取星期几
description: 了解如何在 .NET 中确定特定日期的周序数日期。 了解如何显示特定日期的本地化星期名称。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- formatting [.NET], dates
- DateTime.DayOfWeek property
- DateTime.ToString method
- dates [.NET], retrieving week information
- DateTimeOffset.DayOfWeek property
- dates [.NET], day of week
- Weekday function
- day of week [.NET]
- extracting day of week
- weekday names
- WeekdayName function
- numbers [.NET], day of week
- formatting [.NET], time
- DateTimeOffset.ToString method
- full weekday names
ms.assetid: 1c9bef76-5634-46cf-b91c-9b9eb72091d7
ms.openlocfilehash: f7a18a3ab414a07fa4908c67c5ec9334ce63953f
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888516"
---
# <a name="how-to-extract-the-day-of-the-week-from-a-specific-date"></a><span data-ttu-id="10ae0-104">如何：从特定日期中提取星期几</span><span class="sxs-lookup"><span data-stu-id="10ae0-104">How to: Extract the Day of the Week from a Specific Date</span></span>

<span data-ttu-id="10ae0-105">利用 .NET，可以很容易地确定某个特定日期是星期几，以及显示某个特定日期的本地化星期几名称。</span><span class="sxs-lookup"><span data-stu-id="10ae0-105">.NET makes it easy to determine the ordinal day of the week for a particular date, and to display the localized weekday name for a particular date.</span></span> <span data-ttu-id="10ae0-106">指示与特定日期相对应的星期几的枚举值可以从 <xref:System.DateTime.DayOfWeek%2A> 或 <xref:System.DateTimeOffset.DayOfWeek%2A> 属性中获取。</span><span class="sxs-lookup"><span data-stu-id="10ae0-106">An enumerated value that indicates the day of the week corresponding to a particular date is available from the <xref:System.DateTime.DayOfWeek%2A> or <xref:System.DateTimeOffset.DayOfWeek%2A> property.</span></span> <span data-ttu-id="10ae0-107">与此不同的是，检索星期几名称是一项格式化操作，可通过调用格式化方法来执行，例如日期和时间值的 `ToString` 方法或 <xref:System.String.Format%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="10ae0-107">In contrast, retrieving the weekday name is a formatting operation that can be performed by calling a formatting method, such as a date and time value's `ToString` method or the <xref:System.String.Format%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="10ae0-108">本主题演示如何执行这些格式化操作。</span><span class="sxs-lookup"><span data-stu-id="10ae0-108">This topic shows how to perform these formatting operations.</span></span>  
  
## <a name="extract-a-number-indicating-the-day-of-the-week"></a><span data-ttu-id="10ae0-109">提取指示星期几的数字</span><span class="sxs-lookup"><span data-stu-id="10ae0-109">Extract a number indicating the day of the week</span></span>
  
1. <span data-ttu-id="10ae0-110">如果要使用日期的字符串表示形式，请使用静态 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 方法将其转换为 <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> 或 <xref:System.DateTimeOffset.Parse%2A?displayProperty=nameWithType> 值。</span><span class="sxs-lookup"><span data-stu-id="10ae0-110">If you are working with the string representation of a date, convert it to a <xref:System.DateTime> or a <xref:System.DateTimeOffset> value by using the static <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> or <xref:System.DateTimeOffset.Parse%2A?displayProperty=nameWithType> method.</span></span>  
  
2. <span data-ttu-id="10ae0-111">使用 <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> 或 <xref:System.DateTimeOffset.DayOfWeek%2A?displayProperty=nameWithType> 属性检索指示星期几的 <xref:System.DayOfWeek> 值。</span><span class="sxs-lookup"><span data-stu-id="10ae0-111">Use the <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> or <xref:System.DateTimeOffset.DayOfWeek%2A?displayProperty=nameWithType> property to retrieve a <xref:System.DayOfWeek> value that indicates the day of the week.</span></span>  
  
3. <span data-ttu-id="10ae0-112">如有必要，可将 <xref:System.DayOfWeek> 值强制转换（在 C# 中）或转换（在 Visual Basic 中）为整数。</span><span class="sxs-lookup"><span data-stu-id="10ae0-112">If necessary, cast (in C#) or convert (in Visual Basic) the <xref:System.DayOfWeek> value to an integer.</span></span>  
  
 <span data-ttu-id="10ae0-113">下面的示例将显示一个整数，用于表示特定日期的星期几。</span><span class="sxs-lookup"><span data-stu-id="10ae0-113">The following example displays an integer that represents the day of the week of a specific date.</span></span>  
  
 [!code-csharp[Formatting.Howto.WeekdayName#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/weekdaynumber7.cs#7)]
 [!code-vb[Formatting.Howto.WeekdayName#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/weekdaynumber7.vb#7)]  
  
## <a name="extract-the-abbreviated-weekday-name"></a><span data-ttu-id="10ae0-114">提取缩写的工作日名称</span><span class="sxs-lookup"><span data-stu-id="10ae0-114">Extract the abbreviated weekday name</span></span>
  
1. <span data-ttu-id="10ae0-115">如果要使用日期的字符串表示形式，请使用静态 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 方法将其转换为 <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> 或 <xref:System.DateTimeOffset.Parse%2A?displayProperty=nameWithType> 值。</span><span class="sxs-lookup"><span data-stu-id="10ae0-115">If you are working with the string representation of a date, convert it to a <xref:System.DateTime> or a <xref:System.DateTimeOffset> value by using the static <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> or <xref:System.DateTimeOffset.Parse%2A?displayProperty=nameWithType> method.</span></span>  
  
2. <span data-ttu-id="10ae0-116">你可以提取当前区域性或特定区域性的缩写的星期几名称：</span><span class="sxs-lookup"><span data-stu-id="10ae0-116">You can extract the abbreviated weekday name of the current culture or of a specific culture:</span></span>  
  
    1. <span data-ttu-id="10ae0-117">若要提取当前区域性的缩写的星期几名称，请调用日期和时间值的 <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> 或 <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType> 实例方法，并以 `format` 参数的形式传递字符串“ddd”。</span><span class="sxs-lookup"><span data-stu-id="10ae0-117">To extract the abbreviated weekday name for the current culture, call the date and time value's <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> or <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType> instance method, and pass the string "ddd" as the `format` parameter.</span></span> <span data-ttu-id="10ae0-118">下面的示例演示 <xref:System.DateTime.ToString%28System.String%29> 方法的调用。</span><span class="sxs-lookup"><span data-stu-id="10ae0-118">The following example illustrates the call to the <xref:System.DateTime.ToString%28System.String%29> method.</span></span>  
  
         [!code-csharp[Formatting.Howto.WeekdayName#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/abbrname1.cs#1)]
         [!code-vb[Formatting.Howto.WeekdayName#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/abbrname1.vb#1)]  
  
    2. <span data-ttu-id="10ae0-119">若要提取特定区域性的缩写的星期几名称，请调用日期和时间值的 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 或 <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 实例方法。</span><span class="sxs-lookup"><span data-stu-id="10ae0-119">To extract the abbreviated weekday name for a specific culture, call the date and time value's <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> or <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> instance method.</span></span> <span data-ttu-id="10ae0-120">同时以 `format` 参数形式传递字符串“ddd”。</span><span class="sxs-lookup"><span data-stu-id="10ae0-120">Pass the string "ddd" as the `format` parameter.</span></span> <span data-ttu-id="10ae0-121">以 <xref:System.Globalization.CultureInfo> 参数的形式传递表示要检索其星期几名称的区域性的 <xref:System.Globalization.DateTimeFormatInfo> 或 `provider` 对象。</span><span class="sxs-lookup"><span data-stu-id="10ae0-121">Pass either a <xref:System.Globalization.CultureInfo> or a <xref:System.Globalization.DateTimeFormatInfo> object that represents the culture whose weekday name you want to retrieve as the `provider` parameter.</span></span> <span data-ttu-id="10ae0-122">下面的代码阐释如何使用表示 fr-FR 区域性的 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29> 对象调用 <xref:System.Globalization.CultureInfo> 方法。</span><span class="sxs-lookup"><span data-stu-id="10ae0-122">The following code illustrates a call to the <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29> method using a <xref:System.Globalization.CultureInfo> object that represents the fr-FR culture.</span></span>  
  
         [!code-csharp[Formatting.Howto.WeekdayName#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/abbrname2.cs#2)]
         [!code-vb[Formatting.Howto.WeekdayName#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/abbrname2.vb#2)]  
  
## <a name="extract-the-full-weekday-name"></a><span data-ttu-id="10ae0-123">提取完整的工作日名称</span><span class="sxs-lookup"><span data-stu-id="10ae0-123">Extract the full weekday name</span></span>
  
1. <span data-ttu-id="10ae0-124">如果要使用日期的字符串表示形式，请使用静态 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 方法将其转换为 <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> 或 <xref:System.DateTimeOffset.Parse%2A?displayProperty=nameWithType> 值。</span><span class="sxs-lookup"><span data-stu-id="10ae0-124">If you are working with the string representation of a date, convert it to a <xref:System.DateTime> or a <xref:System.DateTimeOffset> value by using the static <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> or <xref:System.DateTimeOffset.Parse%2A?displayProperty=nameWithType> method.</span></span>  
  
2. <span data-ttu-id="10ae0-125">你可以提取当前区域性或特定区域性的完整的星期几名称：</span><span class="sxs-lookup"><span data-stu-id="10ae0-125">You can extract the full weekday name of the current culture or of a specific culture:</span></span>  
  
    1. <span data-ttu-id="10ae0-126">若要提取当前区域性的缩写的星期几名称，请调用日期和时间值的 <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> 或 <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType> 实例方法，并以 `format` 参数的形式传递字符串“dddd”。</span><span class="sxs-lookup"><span data-stu-id="10ae0-126">To extract the weekday name for the current culture, call the date and time value's <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> or <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType> instance method, and pass the string "dddd" as the `format` parameter.</span></span> <span data-ttu-id="10ae0-127">下面的示例演示 <xref:System.DateTime.ToString%28System.String%29> 方法的调用。</span><span class="sxs-lookup"><span data-stu-id="10ae0-127">The following example illustrates the call to the <xref:System.DateTime.ToString%28System.String%29> method.</span></span>  
  
         [!code-csharp[Formatting.Howto.WeekdayName#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/fullname4.cs#4)]
         [!code-vb[Formatting.Howto.WeekdayName#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/fullname4.vb#4)]  
  
    2. <span data-ttu-id="10ae0-128">若要提取特定区域性的星期几名称，请调用日期和时间值的 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 或 <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 实例方法。</span><span class="sxs-lookup"><span data-stu-id="10ae0-128">To extract the weekday name for a specific culture, call the date and time value's <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> or <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> instance method.</span></span> <span data-ttu-id="10ae0-129">同时以 `format` 参数形式传递字符串“dddd”。</span><span class="sxs-lookup"><span data-stu-id="10ae0-129">Pass the string "dddd" as the `format` parameter.</span></span> <span data-ttu-id="10ae0-130">以 <xref:System.Globalization.CultureInfo> 参数的形式传递表示要检索其星期几名称的区域性的 <xref:System.Globalization.DateTimeFormatInfo> 或 `provider` 对象。</span><span class="sxs-lookup"><span data-stu-id="10ae0-130">Pass either a <xref:System.Globalization.CultureInfo> or a <xref:System.Globalization.DateTimeFormatInfo> object that represents the culture whose weekday name you want to retrieve as the `provider` parameter.</span></span> <span data-ttu-id="10ae0-131">下面的代码阐释如何使用表示 es-ES 区域性的 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29> 对象调用 <xref:System.Globalization.CultureInfo> 方法。</span><span class="sxs-lookup"><span data-stu-id="10ae0-131">The following code illustrates a call to the <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29> method using a <xref:System.Globalization.CultureInfo> object that represents the es-ES culture.</span></span>  
  
         [!code-csharp[Formatting.Howto.WeekdayName#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/fullname5.cs#5)]
         [!code-vb[Formatting.Howto.WeekdayName#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/fullname5.vb#5)]  
  
## <a name="example"></a><span data-ttu-id="10ae0-132">示例</span><span class="sxs-lookup"><span data-stu-id="10ae0-132">Example</span></span>  
 <span data-ttu-id="10ae0-133">该示例演示如何调用 <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> 和 <xref:System.DateTimeOffset.DayOfWeek%2A?displayProperty=nameWithType> 属性以及 <xref:System.DateTime.ToString%2A?displayProperty=nameWithType> 和 <xref:System.DateTimeOffset.ToString%2A?displayProperty=nameWithType> 方法，以检索特定日期中表示星期几的数字、缩写的星期几名称和完整的星期几名称。</span><span class="sxs-lookup"><span data-stu-id="10ae0-133">The example illustrates calls to the <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> and <xref:System.DateTimeOffset.DayOfWeek%2A?displayProperty=nameWithType> properties and the <xref:System.DateTime.ToString%2A?displayProperty=nameWithType> and <xref:System.DateTimeOffset.ToString%2A?displayProperty=nameWithType> methods to retrieve the number that represents the day of the week, the abbreviated weekday name, and the full weekday name for a particular date.</span></span>  
  
 [!code-csharp[Formatting.Howto.WeekdayName#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/example6.cs#6)]
 [!code-vb[Formatting.Howto.WeekdayName#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/example6.vb#6)]  
  
 <span data-ttu-id="10ae0-134">个别语言可能提供与 .NET 所提供的功能相同或互为补充的功能。</span><span class="sxs-lookup"><span data-stu-id="10ae0-134">Individual languages may provide functionality that duplicates or supplements the functionality provided by .NET.</span></span> <span data-ttu-id="10ae0-135">例如，Visual Basic 包括这样的两个函数：</span><span class="sxs-lookup"><span data-stu-id="10ae0-135">For example, Visual Basic includes two such functions:</span></span>  
  
- <span data-ttu-id="10ae0-136">`Weekday`，它返回指示特定日期中表示星期几的数字。</span><span class="sxs-lookup"><span data-stu-id="10ae0-136">`Weekday`, which returns a number that indicates the day of the week of a particular date.</span></span> <span data-ttu-id="10ae0-137">此函数将一周中第一天的序数值视为一，而 <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> 属性却将其视为零。</span><span class="sxs-lookup"><span data-stu-id="10ae0-137">It considers the ordinal value of the first day of the week to be one, whereas the <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> property considers it to be zero.</span></span>  
  
- <span data-ttu-id="10ae0-138">`WeekdayName`，它返回当前区域性中与特定星期几相对应的周的名称。</span><span class="sxs-lookup"><span data-stu-id="10ae0-138">`WeekdayName`, which returns the name of the week in the current culture that corresponds to a particular weekday number.</span></span>  
  
 <span data-ttu-id="10ae0-139">下面的示例演示了 Visual Basic `Weekday` 和 `WeekdayName` 函数的用法。</span><span class="sxs-lookup"><span data-stu-id="10ae0-139">The following example illustrates the use of the Visual Basic `Weekday` and `WeekdayName` functions.</span></span>  
  
 [!code-vb[Formatting.HowTo.WeekdayName#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/example9.vb#9)]  
  
 <span data-ttu-id="10ae0-140">也可以使用 <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> 属性返回的值检索特定日期的星期几名称。</span><span class="sxs-lookup"><span data-stu-id="10ae0-140">You can also use the value returned by the <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> property to retrieve the weekday name of a particular date.</span></span> <span data-ttu-id="10ae0-141">此过程只需对 <xref:System.Enum.ToString%2A> 属性返回的值调用 <xref:System.DayOfWeek> 方法。</span><span class="sxs-lookup"><span data-stu-id="10ae0-141">This requires only a call to the <xref:System.Enum.ToString%2A> method on the <xref:System.DayOfWeek> value returned by the property.</span></span> <span data-ttu-id="10ae0-142">但是，此技术并不生成当前区域性的本地化星期几名称，如下面的示例所示。</span><span class="sxs-lookup"><span data-stu-id="10ae0-142">However, this technique does not produce a localized weekday name for the current culture, as the following example illustrates.</span></span>  
  
 [!code-csharp[Formatting.HowTo.WeekdayName#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/Howto1.cs#8)]
 [!code-vb[Formatting.HowTo.WeekdayName#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/Howto1.vb#8)]

## <a name="see-also"></a><span data-ttu-id="10ae0-143">请参阅</span><span class="sxs-lookup"><span data-stu-id="10ae0-143">See also</span></span>

- [<span data-ttu-id="10ae0-144">标准日期和时间格式字符串</span><span class="sxs-lookup"><span data-stu-id="10ae0-144">Standard Date and Time Format Strings</span></span>](standard-date-and-time-format-strings.md)
- [<span data-ttu-id="10ae0-145">自定义日期和时间格式字符串</span><span class="sxs-lookup"><span data-stu-id="10ae0-145">Custom Date and Time Format Strings</span></span>](custom-date-and-time-format-strings.md)
