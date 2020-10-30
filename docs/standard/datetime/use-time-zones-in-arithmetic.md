---
title: 如何：在日期和时间算术中使用时区
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET], arithmetic operations
- arithmetic operations [.NET], dates and times
- dates [.NET], adding and subtracting
ms.assetid: 83dd898d-1338-415d-8cd6-445377ab7871
ms.openlocfilehash: cb1abbcab10d52f9ba898e2f4e2468b04cfcff1f
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93064257"
---
# <a name="how-to-use-time-zones-in-date-and-time-arithmetic"></a><span data-ttu-id="0d7f1-102">如何：在日期和时间算术中使用时区</span><span class="sxs-lookup"><span data-stu-id="0d7f1-102">How to: Use time zones in date and time arithmetic</span></span>

<span data-ttu-id="0d7f1-103">通常，当您使用或值执行日期和时间算术运算时 <xref:System.DateTime> <xref:System.DateTimeOffset> ，结果将不反映任何时区调整规则。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-103">Ordinarily, when you perform date and time arithmetic using <xref:System.DateTime> or <xref:System.DateTimeOffset> values, the result does not reflect any time zone adjustment rules.</span></span> <span data-ttu-id="0d7f1-104">即使日期和时间值的时区可以清楚识别 (例如，将 <xref:System.DateTime.Kind%2A> 属性设置为) 时也是如此 <xref:System.DateTimeKind.Local> 。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-104">This is true even when the time zone of the date and time value is clearly identifiable (for example, when the <xref:System.DateTime.Kind%2A> property is set to <xref:System.DateTimeKind.Local>).</span></span> <span data-ttu-id="0d7f1-105">本主题演示如何对属于特定时区的日期和时间值执行算术运算。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-105">This topic shows how to perform arithmetic operations on date and time values that belong to a particular time zone.</span></span> <span data-ttu-id="0d7f1-106">算术运算的结果将反映时区调整规则。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-106">The results of the arithmetic operations will reflect the time zone's adjustment rules.</span></span>

### <a name="to-apply-adjustment-rules-to-date-and-time-arithmetic"></a><span data-ttu-id="0d7f1-107">将调整规则应用到日期和时间运算</span><span class="sxs-lookup"><span data-stu-id="0d7f1-107">To apply adjustment rules to date and time arithmetic</span></span>

1. <span data-ttu-id="0d7f1-108">采取措施将日期和时间值与其所属时区紧密耦合。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-108">Implement some method of closely coupling a date and time value with the time zone to which it belongs.</span></span> <span data-ttu-id="0d7f1-109">例如声明同时包含日期和时间值及其时区的结构。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-109">For example, declare a structure that includes both the date and time value and its time zone.</span></span> <span data-ttu-id="0d7f1-110">下面的示例使用此方法将 <xref:System.DateTime> 值与其时区链接。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-110">The following example uses this approach to link a <xref:System.DateTime> value with its time zone.</span></span>

   [!code-csharp[System.DateTimeOffset.Conceptual#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual6.cs#6)]
   [!code-vb[System.DateTimeOffset.Conceptual#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual6.vb#6)]

2. <span data-ttu-id="0d7f1-111">通过调用方法或方法，将时间转换为协调世界时 (UTC) <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A> <xref:System.TimeZoneInfo.ConvertTime%2A> 。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-111">Convert a time to Coordinated Universal Time (UTC) by calling either the <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A> method or the <xref:System.TimeZoneInfo.ConvertTime%2A> method.</span></span>

3. <span data-ttu-id="0d7f1-112">对 UTC 时间执行算术运算。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-112">Perform the arithmetic operation on the UTC time.</span></span>

4. <span data-ttu-id="0d7f1-113">通过调用方法将时间从 UTC 转换为原始时间的关联时区 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTime%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-113">Convert the time from UTC to the original time's associated time zone by calling the <xref:System.TimeZoneInfo.ConvertTime%28System.DateTime%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> method.</span></span>

## <a name="example"></a><span data-ttu-id="0d7f1-114">示例</span><span class="sxs-lookup"><span data-stu-id="0d7f1-114">Example</span></span>

<span data-ttu-id="0d7f1-115">下方示例向中部标准时间 2008 年 3 月 9 日凌晨 1:30 添加了</span><span class="sxs-lookup"><span data-stu-id="0d7f1-115">The following example adds two hours and thirty minutes to March 9, 2008, at 1:30 A.M.</span></span> <span data-ttu-id="0d7f1-116">2 小时 30 分钟。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-116">Central Standard Time.</span></span> <span data-ttu-id="0d7f1-117">30 分钟后（即 2008 年 3 月 9 日凌晨 2:00）</span><span class="sxs-lookup"><span data-stu-id="0d7f1-117">The time zone's transition to daylight saving time occurs thirty minutes later, at 2:00 A.M.</span></span> <span data-ttu-id="0d7f1-118">两个半小时的代码。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-118">on March 9, 2008.</span></span> <span data-ttu-id="0d7f1-119">由于该示例遵从了上一部分中列出的四个步骤，因此它将最终时间正确地报告为 </span><span class="sxs-lookup"><span data-stu-id="0d7f1-119">Because the example follows the four steps listed in the previous section, it correctly reports the resulting time as 5:00 A.M.</span></span> <span data-ttu-id="0d7f1-120">两个半小时的代码。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-120">on March 9, 2008.</span></span>

[!code-csharp[System.DateTimeOffset.Conceptual#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual8.cs#8)]
[!code-vb[System.DateTimeOffset.Conceptual#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual8.vb#8)]

<span data-ttu-id="0d7f1-121"><xref:System.DateTime>和 <xref:System.DateTimeOffset> 值都与它们所属的任何时区解除关联。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-121">Both <xref:System.DateTime> and <xref:System.DateTimeOffset> values are disassociated from any time zone to which they might belong.</span></span> <span data-ttu-id="0d7f1-122">只有能够立即识别任意日期和时间所属的时区，才能在执行日期和时间运算时自动应用时区调整规则。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-122">To perform date and time arithmetic in a way that automatically applies a time zone's adjustment rules, the time zone to which any date and time value belongs must be immediately identifiable.</span></span> <span data-ttu-id="0d7f1-123">这意味着，日期和时间及其关联时区必须紧密耦合。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-123">This means that a date and time and its associated time zone must be tightly coupled.</span></span> <span data-ttu-id="0d7f1-124">可通过方法进行此操作，其中包括：</span><span class="sxs-lookup"><span data-stu-id="0d7f1-124">There are several ways to do this, which include the following:</span></span>

- <span data-ttu-id="0d7f1-125">假设应用程序中使用的所有时间均属于某个特定时区。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-125">Assume that all times used in an application belong to a particular time zone.</span></span> <span data-ttu-id="0d7f1-126">尽管在某些情况下适用，但此方法的灵活性和可移植性有限。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-126">Although appropriate in some cases, this approach offers limited flexibility and possibly limited portability.</span></span>

- <span data-ttu-id="0d7f1-127">在类型字段中包括日期和时间及其关联时区，定义将二者紧密耦合的类型。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-127">Define a type that tightly couples a date and time with its associated time zone by including both as fields of the type.</span></span> <span data-ttu-id="0d7f1-128">代码示例中使用了此方法，定义了将日期和时间以及时区存储在两个成员字段中的结构。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-128">This approach is used in the code example, which defines a structure to store the date and time and the time zone in two member fields.</span></span>

<span data-ttu-id="0d7f1-129">该示例演示如何对值执行算术运算，以便将时区 <xref:System.DateTime> 调整规则应用到结果。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-129">The example illustrates how to perform arithmetic operations on <xref:System.DateTime> values so that time zone adjustment rules are applied to the result.</span></span> <span data-ttu-id="0d7f1-130">但是， <xref:System.DateTimeOffset> 可以轻松地使用值。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-130">However, <xref:System.DateTimeOffset> values can be used just as easily.</span></span> <span data-ttu-id="0d7f1-131">下面的示例演示了如何调整原始示例中的代码， <xref:System.DateTimeOffset> 而不是使用 <xref:System.DateTime> 值。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-131">The following example illustrates how the code in the original example might be adapted to use <xref:System.DateTimeOffset> instead of <xref:System.DateTime> values.</span></span>

[!code-csharp[System.DateTimeOffset.Conceptual#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual6.cs#7)]
[!code-vb[System.DateTimeOffset.Conceptual#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual6.vb#7)]

<span data-ttu-id="0d7f1-132">请注意，如果此加法只是对 <xref:System.DateTimeOffset> 值执行，而不是先将其转换为 UTC，则结果将反映正确的时间点，但其偏移量不反映指定时区的时间。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-132">Note that if this addition is simply performed on the <xref:System.DateTimeOffset> value without first converting it to UTC, the result reflects the correct point in time but its offset does not reflect that of the designated time zone for that time.</span></span>

## <a name="compiling-the-code"></a><span data-ttu-id="0d7f1-133">编译代码</span><span class="sxs-lookup"><span data-stu-id="0d7f1-133">Compiling the code</span></span>

<span data-ttu-id="0d7f1-134">此示例需要：</span><span class="sxs-lookup"><span data-stu-id="0d7f1-134">This example requires:</span></span>

- <span data-ttu-id="0d7f1-135"><xref:System>要导入的命名空间与 `using` c # 代码) 中 (必需的语句一起导入。</span><span class="sxs-lookup"><span data-stu-id="0d7f1-135">That the <xref:System> namespace be imported with the `using` statement (required in C# code).</span></span>

## <a name="see-also"></a><span data-ttu-id="0d7f1-136">另请参阅</span><span class="sxs-lookup"><span data-stu-id="0d7f1-136">See also</span></span>

- [<span data-ttu-id="0d7f1-137">日期、时间和时区</span><span class="sxs-lookup"><span data-stu-id="0d7f1-137">Dates, times, and time zones</span></span>](index.md)
- [<span data-ttu-id="0d7f1-138">用日期和时间执行算术运算</span><span class="sxs-lookup"><span data-stu-id="0d7f1-138">Performing arithmetic operations with dates and times</span></span>](performing-arithmetic-operations.md)
