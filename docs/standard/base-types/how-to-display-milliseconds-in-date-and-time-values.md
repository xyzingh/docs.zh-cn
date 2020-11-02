---
title: 如何：显示日期和时间值中的毫秒
description: 本文介绍如何在 .NET 中格式化日期和时间字符串中包含日期和时间的毫秒部分。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DateTime.ToString method
- displaying date and time data
- time [.NET], milliseconds
- dates [.NET], milliseconds
- milliseconds [.NET]
ms.assetid: ae1a0610-90b9-4877-8eb6-4e30bc5e00cf
ms.openlocfilehash: bff458e73d603781155b18160bc7d088d8bd78cb
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888464"
---
# <a name="how-to-display-milliseconds-in-date-and-time-values"></a><span data-ttu-id="c5f95-103">如何：显示日期和时间值中的毫秒</span><span class="sxs-lookup"><span data-stu-id="c5f95-103">How to: Display Milliseconds in Date and Time Values</span></span>
<span data-ttu-id="c5f95-104">默认日期和时间格式设置方法（如 <xref:System.DateTime.ToString?displayProperty=nameWithType>）包含时间值的小时、分钟和秒部分，但不包含毫秒部分。</span><span class="sxs-lookup"><span data-stu-id="c5f95-104">The default date and time formatting methods, such as <xref:System.DateTime.ToString?displayProperty=nameWithType>, include the hours, minutes, and seconds of a time value but exclude its milliseconds component.</span></span> <span data-ttu-id="c5f95-105">本主题说明如何在格式化日期和时间字符串中包含日期和时间的毫秒部分。</span><span class="sxs-lookup"><span data-stu-id="c5f95-105">This topic shows how to include a date and time's millisecond component in formatted date and time strings.</span></span>  
  
### <a name="to-display-the-millisecond-component-of-a-datetime-value"></a><span data-ttu-id="c5f95-106">显示的 DateTime 值的毫秒部分</span><span class="sxs-lookup"><span data-stu-id="c5f95-106">To display the millisecond component of a DateTime value</span></span>  
  
1. <span data-ttu-id="c5f95-107">如果要使用日期的字符串表示形式，请使用静态 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 方法将其转换为 <xref:System.DateTime.Parse%28System.String%29?displayProperty=nameWithType> 或 <xref:System.DateTimeOffset.Parse%28System.String%29?displayProperty=nameWithType> 值。</span><span class="sxs-lookup"><span data-stu-id="c5f95-107">If you are working with the string representation of a date, convert it to a <xref:System.DateTime> or a <xref:System.DateTimeOffset> value by using the static <xref:System.DateTime.Parse%28System.String%29?displayProperty=nameWithType> or <xref:System.DateTimeOffset.Parse%28System.String%29?displayProperty=nameWithType> method.</span></span>  
  
2. <span data-ttu-id="c5f95-108">若要提取时间值的毫秒部分的字符串表示形式，请调用日期和时间值的 <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> 或 <xref:System.DateTimeOffset.ToString%2A> 方法，并将 `fff` 或 `FFF` 自定义格式模式单独传递，或与其他自定义格式说明符一起作为 `format` 参数传递。</span><span class="sxs-lookup"><span data-stu-id="c5f95-108">To extract the string representation of a time's millisecond component, call the date and time value's <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> or <xref:System.DateTimeOffset.ToString%2A> method, and pass the `fff` or `FFF` custom format pattern either alone or with other custom format specifiers as the `format` parameter.</span></span>  
  
## <a name="example"></a><span data-ttu-id="c5f95-109">示例</span><span class="sxs-lookup"><span data-stu-id="c5f95-109">Example</span></span>  
 <span data-ttu-id="c5f95-110">此示例展示了如何向控制台传递 <xref:System.DateTime> 和 <xref:System.DateTimeOffset> 值的毫秒部分（单独传递以及包含在更长的日期和时间字符串中传递）。</span><span class="sxs-lookup"><span data-stu-id="c5f95-110">The example displays the millisecond component of a <xref:System.DateTime> and a <xref:System.DateTimeOffset> value to the console, both alone and included in a longer date and time string.</span></span>  
  
 [!code-csharp[Formatting.HowTo.Millisecond#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Millisecond/cs/Millisecond.cs#1)]
 [!code-vb[Formatting.HowTo.Millisecond#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Millisecond/vb/Millisecond.vb#1)]  
  
 <span data-ttu-id="c5f95-111">`fff` 格式模式包含毫秒值中的任何尾随零。</span><span class="sxs-lookup"><span data-stu-id="c5f95-111">The `fff` format pattern includes any trailing zeros in the millisecond value.</span></span> <span data-ttu-id="c5f95-112">`FFF` 格式模式禁止显示它们。</span><span class="sxs-lookup"><span data-stu-id="c5f95-112">The `FFF` format pattern suppresses them.</span></span> <span data-ttu-id="c5f95-113">下面的示例阐释了差异。</span><span class="sxs-lookup"><span data-stu-id="c5f95-113">The difference is illustrated in the following example.</span></span>  
  
 [!code-csharp[Formatting.HowTo.Millisecond#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Millisecond/cs/Millisecond.cs#2)]
 [!code-vb[Formatting.HowTo.Millisecond#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Millisecond/vb/Millisecond.vb#2)]  
  
 <span data-ttu-id="c5f95-114">与定义包含日期和时间的毫秒部分的完整自定义格式说明符有关的一个问题在于，它定义可能与应用程序当前区域性中的时间元素排列不对应的硬编码格式。</span><span class="sxs-lookup"><span data-stu-id="c5f95-114">A problem with defining a complete custom format specifier that includes the millisecond component of a date and time is that it defines a hard-coded format that may not correspond to the arrangement of time elements in the application's current culture.</span></span> <span data-ttu-id="c5f95-115">更好的替换方法是，检索当前区域性的 <xref:System.Globalization.DateTimeFormatInfo> 对象定义的日期和时间显示模式之一，并将它修改为包含毫秒部分。</span><span class="sxs-lookup"><span data-stu-id="c5f95-115">A better alternative is to retrieve one of the date and time display patterns defined by the current culture's <xref:System.Globalization.DateTimeFormatInfo> object and modify it to include milliseconds.</span></span> <span data-ttu-id="c5f95-116">该示例也阐释了这种方法。</span><span class="sxs-lookup"><span data-stu-id="c5f95-116">The example also illustrates this approach.</span></span> <span data-ttu-id="c5f95-117">它会从 <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A?displayProperty=nameWithType> 属性检索当前区域性的完整日期和时间模式，再在秒模式后面插入自定义模式 `.ffff`。</span><span class="sxs-lookup"><span data-stu-id="c5f95-117">It retrieves the current culture's full date and time pattern from the <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A?displayProperty=nameWithType> property, and then inserts the custom pattern `.ffff` after its seconds pattern.</span></span> <span data-ttu-id="c5f95-118">请注意，该示例使用正则表达式在单个方法调用中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="c5f95-118">Note that the example uses a regular expression to perform this operation in a single method call.</span></span>  
  
 <span data-ttu-id="c5f95-119">还可以使用自定义格式说明符来显示毫秒之外的秒的小数部分。</span><span class="sxs-lookup"><span data-stu-id="c5f95-119">You can also use a custom format specifier to display a fractional part of seconds other than milliseconds.</span></span> <span data-ttu-id="c5f95-120">例如，`f` 或 `F` 自定义格式说明符显示十分之几秒，`ff` 或 `FF` 自定义格式说明符显示百分之几秒，`ffff` 或 `FFFF` 自定义格式说明符显示万分之几秒。</span><span class="sxs-lookup"><span data-stu-id="c5f95-120">For example, the `f` or `F` custom format specifier displays tenths of a second, the `ff` or `FF` custom format specifier displays hundredths of a second, and the `ffff` or `FFFF` custom format specifier displays ten thousandths of a second.</span></span> <span data-ttu-id="c5f95-121">毫秒的小数部分在返回的字符串中会进行截断而不是舍入。</span><span class="sxs-lookup"><span data-stu-id="c5f95-121">Fractional parts of a millisecond are truncated instead of rounded in the returned string.</span></span> <span data-ttu-id="c5f95-122">下面的示例中使用了这些格式说明符。</span><span class="sxs-lookup"><span data-stu-id="c5f95-122">These format specifiers are used in the following example.</span></span>  
  
 [!code-csharp[Formatting.HowTo.Millisecond#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Millisecond/cs/Millisecond.cs#3)]
 [!code-vb[Formatting.HowTo.Millisecond#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Millisecond/vb/Millisecond.vb#3)]  
  
> [!NOTE]
> <span data-ttu-id="c5f95-123">可以显示秒的非常小的小数单位，如万分之几秒或十万分之几秒。</span><span class="sxs-lookup"><span data-stu-id="c5f95-123">It is possible to display very small fractional units of a second, such as ten thousandths of a second or hundred-thousandths of a second.</span></span> <span data-ttu-id="c5f95-124">但是，这些值可能没有意义。</span><span class="sxs-lookup"><span data-stu-id="c5f95-124">However, these values may not be meaningful.</span></span> <span data-ttu-id="c5f95-125">日期和时间值的精度取决于系统时钟的分辨率。</span><span class="sxs-lookup"><span data-stu-id="c5f95-125">The precision of date and time values depends on the resolution of the system clock.</span></span> <span data-ttu-id="c5f95-126">在 Windows NT 3.5 和更高版本以及 Windows Vista 操作系统上，时钟的分辨率大约为 10-15 毫秒。</span><span class="sxs-lookup"><span data-stu-id="c5f95-126">On Windows NT 3.5 and later, and Windows Vista operating systems, the clock's resolution is approximately 10-15 milliseconds.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c5f95-127">请参阅</span><span class="sxs-lookup"><span data-stu-id="c5f95-127">See also</span></span>

- <xref:System.Globalization.DateTimeFormatInfo>
- [<span data-ttu-id="c5f95-128">自定义日期和时间格式字符串</span><span class="sxs-lookup"><span data-stu-id="c5f95-128">Custom Date and Time Format Strings</span></span>](custom-date-and-time-format-strings.md)
