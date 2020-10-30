---
title: 如何：解析明确时间
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET], ambiguous time
- ambiguous time [.NET]
ms.assetid: 2cf5fb25-492c-4875-9245-98cac8348e97
ms.openlocfilehash: 467153ad1217e529f52bf90262c4264de069ff00
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93063516"
---
# <a name="how-to-resolve-ambiguous-times"></a><span data-ttu-id="db00b-102">如何：解析明确时间</span><span class="sxs-lookup"><span data-stu-id="db00b-102">How to: Resolve ambiguous times</span></span>

<span data-ttu-id="db00b-103">不明确时间是指映射到多个协调世界时 (UTC) 的时间。</span><span class="sxs-lookup"><span data-stu-id="db00b-103">An ambiguous time is a time that maps to more than one Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="db00b-104">在向后调整时钟时间时，例如从时区的夏令时调整到标准时间这段转换期间，便会出现不明确时间。</span><span class="sxs-lookup"><span data-stu-id="db00b-104">It occurs when the clock time is adjusted back in time, such as during the transition from a time zone's daylight saving time to its standard time.</span></span> <span data-ttu-id="db00b-105">在处理不明确时间时，可执行以下任一操作：</span><span class="sxs-lookup"><span data-stu-id="db00b-105">When handling an ambiguous time, you can do one of the following:</span></span>

- <span data-ttu-id="db00b-106">假设一下时间如何映射到 UTC。</span><span class="sxs-lookup"><span data-stu-id="db00b-106">Make an assumption about how the time maps to UTC.</span></span> <span data-ttu-id="db00b-107">例如，可以假定不明确时间始终以时区的标准时间表示。</span><span class="sxs-lookup"><span data-stu-id="db00b-107">For example, you can assume that an ambiguous time is always expressed in the time zone's standard time.</span></span>

- <span data-ttu-id="db00b-108">如果不明确时间是用户输入的数据项，则可以让用户自行解决。</span><span class="sxs-lookup"><span data-stu-id="db00b-108">If the ambiguous time is an item of data entered by the user, you can leave it to the user to resolve the ambiguity.</span></span>

<span data-ttu-id="db00b-109">本主题演示如何通过假定不明确时间表示时区的标准时间来解决它。</span><span class="sxs-lookup"><span data-stu-id="db00b-109">This topic shows how to resolve an ambiguous time by assuming that it represents the time zone's standard time.</span></span>

### <a name="to-map-an-ambiguous-time-to-a-time-zones-standard-time"></a><span data-ttu-id="db00b-110">将不明确时间映射到时区的标准时间</span><span class="sxs-lookup"><span data-stu-id="db00b-110">To map an ambiguous time to a time zone's standard time</span></span>

1. <span data-ttu-id="db00b-111">调用 <xref:System.TimeZoneInfo.IsAmbiguousTime%2A> 方法以确定时间是否不明确。</span><span class="sxs-lookup"><span data-stu-id="db00b-111">Call the <xref:System.TimeZoneInfo.IsAmbiguousTime%2A> method to determine whether the time is ambiguous.</span></span>

2. <span data-ttu-id="db00b-112">如果时间不明确，请从时区的属性所返回的对象中减去时间 <xref:System.TimeSpan> <xref:System.TimeZoneInfo.BaseUtcOffset%2A> 。</span><span class="sxs-lookup"><span data-stu-id="db00b-112">If the time is ambiguous, subtract the time from the <xref:System.TimeSpan> object returned by the time zone's <xref:System.TimeZoneInfo.BaseUtcOffset%2A> property.</span></span>

3. <span data-ttu-id="db00b-113">调用 `static` `Shared` Visual Basic .net) 方法中的 (<xref:System.DateTime.SpecifyKind%2A> ，将 UTC 日期和时间值的 <xref:System.DateTime.Kind%2A> 属性设置为 <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="db00b-113">Call the `static` (`Shared` in Visual Basic .NET) <xref:System.DateTime.SpecifyKind%2A> method to set the UTC date and time value's <xref:System.DateTime.Kind%2A> property to <xref:System.DateTimeKind.Utc?displayProperty=nameWithType>.</span></span>

## <a name="example"></a><span data-ttu-id="db00b-114">示例</span><span class="sxs-lookup"><span data-stu-id="db00b-114">Example</span></span>

<span data-ttu-id="db00b-115">下面的示例演示了如何通过假设表示本地时区的标准时间，将不明确的时间转换为 UTC。</span><span class="sxs-lookup"><span data-stu-id="db00b-115">The following example illustrates how to convert an ambiguous time to UTC by assuming that it represents the local time zone's standard time.</span></span>

[!code-csharp[System.TimeZone2.Concepts#10](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#10)]
[!code-vb[System.TimeZone2.Concepts#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#10)]

<span data-ttu-id="db00b-116">该示例包含一个名为 `ResolveAmbiguousTime` 的方法，该方法确定 <xref:System.DateTime> 传递给它的值是否不明确。</span><span class="sxs-lookup"><span data-stu-id="db00b-116">The example consists of a method named `ResolveAmbiguousTime` that determines whether the <xref:System.DateTime> value passed to it is ambiguous.</span></span> <span data-ttu-id="db00b-117">如果值不明确，则该方法将返回一个 <xref:System.DateTime> 表示相应 UTC 时间的值。</span><span class="sxs-lookup"><span data-stu-id="db00b-117">If the value is ambiguous, the method returns a <xref:System.DateTime> value that represents the corresponding UTC time.</span></span> <span data-ttu-id="db00b-118">方法通过从本地时间减去本地时区的属性的值来处理此转换 <xref:System.TimeZoneInfo.BaseUtcOffset%2A> 。</span><span class="sxs-lookup"><span data-stu-id="db00b-118">The method handles this conversion by subtracting the value of the local time zone's <xref:System.TimeZoneInfo.BaseUtcOffset%2A> property from the local time.</span></span>

<span data-ttu-id="db00b-119">通常，通过调用 <xref:System.TimeZoneInfo.GetAmbiguousTimeOffsets%2A> 方法来检索对象数组（ <xref:System.TimeSpan> 其中包含不明确时间的可能 UTC 偏移量），来处理不明确时间。</span><span class="sxs-lookup"><span data-stu-id="db00b-119">Ordinarily, an ambiguous time is handled by calling the <xref:System.TimeZoneInfo.GetAmbiguousTimeOffsets%2A> method to retrieve an array of <xref:System.TimeSpan> objects that contain the ambiguous time's possible UTC offsets.</span></span> <span data-ttu-id="db00b-120">但是，本示例建立在一个大胆假设之上，即不明确时间始终映射到时区的标准时间。</span><span class="sxs-lookup"><span data-stu-id="db00b-120">However, this example makes the arbitrary assumption that an ambiguous time should always be mapped to the time zone's standard time.</span></span> <span data-ttu-id="db00b-121"><xref:System.TimeZoneInfo.BaseUtcOffset%2A>属性返回 UTC 与时区的标准时间之间的偏移量。</span><span class="sxs-lookup"><span data-stu-id="db00b-121">The <xref:System.TimeZoneInfo.BaseUtcOffset%2A> property returns the offset between UTC and a time zone's standard time.</span></span>

<span data-ttu-id="db00b-122">在此示例中，对本地时区的所有引用都是通过属性进行的 <xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> ; 本地时区从不分配给对象变量。</span><span class="sxs-lookup"><span data-stu-id="db00b-122">In this example, all references to the local time zone are made through the <xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> property; the local time zone is never assigned to an object variable.</span></span> <span data-ttu-id="db00b-123">这是建议的做法，因为对方法的调用会 <xref:System.TimeZoneInfo.ClearCachedData%2A?displayProperty=nameWithType> 使本地时区分配到的任何对象无效。</span><span class="sxs-lookup"><span data-stu-id="db00b-123">This is a recommended practice because a call to the <xref:System.TimeZoneInfo.ClearCachedData%2A?displayProperty=nameWithType> method invalidates any objects that the local time zone is assigned to.</span></span>

## <a name="compiling-the-code"></a><span data-ttu-id="db00b-124">编译代码</span><span class="sxs-lookup"><span data-stu-id="db00b-124">Compiling the code</span></span>

<span data-ttu-id="db00b-125">此示例需要：</span><span class="sxs-lookup"><span data-stu-id="db00b-125">This example requires:</span></span>

- <span data-ttu-id="db00b-126"><xref:System>要导入的命名空间与 `using` c # 代码) 中 (必需的语句一起导入。</span><span class="sxs-lookup"><span data-stu-id="db00b-126">That the <xref:System> namespace be imported with the `using` statement (required in C# code).</span></span>

## <a name="see-also"></a><span data-ttu-id="db00b-127">另请参阅</span><span class="sxs-lookup"><span data-stu-id="db00b-127">See also</span></span>

- [<span data-ttu-id="db00b-128">日期、时间和时区</span><span class="sxs-lookup"><span data-stu-id="db00b-128">Dates, times, and time zones</span></span>](index.md)
- [<span data-ttu-id="db00b-129">如何：让用户解决不明确的时间</span><span class="sxs-lookup"><span data-stu-id="db00b-129">How to: Let users resolve ambiguous times</span></span>](let-users-resolve-ambiguous-times.md)
