---
title: 如何：创建不含调整规则的时区
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET], adjustment rule
- time zones [.NET], creating
- adjustment rule [.NET]
ms.assetid: a6af8647-7893-4f29-95a9-d94c65a6e8dd
ms.openlocfilehash: e3bce4d915a8d979f043b5c4a49b20ce3e0596c9
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93063789"
---
# <a name="how-to-create-time-zones-without-adjustment-rules"></a><span data-ttu-id="b42b3-102">如何：创建不含调整规则的时区</span><span class="sxs-lookup"><span data-stu-id="b42b3-102">How to: Create time zones without adjustment rules</span></span>

<span data-ttu-id="b42b3-103">由于以下几个原因，应用程序所需的确切时区信息在特定系统上可能不存在：</span><span class="sxs-lookup"><span data-stu-id="b42b3-103">The precise time zone information that is required by an application may not be present on a particular system for several reasons:</span></span>

- <span data-ttu-id="b42b3-104">本地系统的注册表中从未定义过该时区。</span><span class="sxs-lookup"><span data-stu-id="b42b3-104">The time zone has never been defined in the local system's registry.</span></span>

- <span data-ttu-id="b42b3-105">已修改或删除注册表中有关时区的数据。</span><span class="sxs-lookup"><span data-stu-id="b42b3-105">Data about the time zone has been modified or removed from the registry.</span></span>

- <span data-ttu-id="b42b3-106">存在时区，但没有特定历史时间段的准确信息。</span><span class="sxs-lookup"><span data-stu-id="b42b3-106">The time zone exists but does not have accurate information about time zone adjustments for a particular historic period.</span></span>

<span data-ttu-id="b42b3-107">在这些情况下，可以调用 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 方法来定义应用程序所需的时区。</span><span class="sxs-lookup"><span data-stu-id="b42b3-107">In these cases, you can call the <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> method to define the time zone required by your application.</span></span> <span data-ttu-id="b42b3-108">您可以使用此方法的重载来创建具有或不带调整规则的时区。</span><span class="sxs-lookup"><span data-stu-id="b42b3-108">You can use the overloads of this method to create a time zone with or without adjustment rules.</span></span> <span data-ttu-id="b42b3-109">如果时区支持夏令时，则可以用固定或浮动调整规则定义调整。</span><span class="sxs-lookup"><span data-stu-id="b42b3-109">If the time zone supports daylight saving time, you can define adjustments with either fixed or floating adjustment rules.</span></span> <span data-ttu-id="b42b3-110"> (这些术语的定义，请参阅时区 [概述](time-zone-overview.md)中的 "时区术语" 部分。 ) </span><span class="sxs-lookup"><span data-stu-id="b42b3-110">(For definitions of these terms, see the "Time Zone Terminology" section in [Time zone overview](time-zone-overview.md).)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b42b3-111">通过调用方法创建的自定义时区 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 未添加到注册表中。</span><span class="sxs-lookup"><span data-stu-id="b42b3-111">Custom time zones created by calling the <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> method are not added to the registry.</span></span> <span data-ttu-id="b42b3-112">相反，只能通过方法调用返回的对象引用来访问这些对象 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 。</span><span class="sxs-lookup"><span data-stu-id="b42b3-112">Instead, they can be accessed only through the object reference returned by the <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> method call.</span></span>

<span data-ttu-id="b42b3-113">本主题说明如何创建不带调整规则的时区。</span><span class="sxs-lookup"><span data-stu-id="b42b3-113">This topic shows how to create a time zone without adjustment rules.</span></span> <span data-ttu-id="b42b3-114">若要创建支持夏令时调整规则的时区，请参阅 [如何：创建带有调整规则的时区](create-time-zones-with-adjustment-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="b42b3-114">To create a time zone that supports daylight saving time adjustment rules, see [How to: Create time zones with adjustment rules](create-time-zones-with-adjustment-rules.md).</span></span>

### <a name="to-create-a-time-zone-without-adjustment-rules"></a><span data-ttu-id="b42b3-115">创建不含调整规则的时区</span><span class="sxs-lookup"><span data-stu-id="b42b3-115">To create a time zone without adjustment rules</span></span>

1. <span data-ttu-id="b42b3-116">定义时区的显示名称。</span><span class="sxs-lookup"><span data-stu-id="b42b3-116">Define the time zone's display name.</span></span>

   <span data-ttu-id="b42b3-117">显示名称采用了一种非常标准的格式，其中，时区与协调世界时的时差 (UTC) 括在括号中，后面跟有标识时区的字符串、时区中的一个或多个城市，或者时区中的一个或多个国家或地区。</span><span class="sxs-lookup"><span data-stu-id="b42b3-117">The display name follows a fairly standard format in which the time zone's offset from Coordinated Universal Time (UTC) is enclosed in parentheses and is followed by a string that identifies the time zone, one or more of the cities in the time zone, or one or more of the countries or regions in the time zone.</span></span>

2. <span data-ttu-id="b42b3-118">定义时区标准时间的名称。</span><span class="sxs-lookup"><span data-stu-id="b42b3-118">Define the name of the time zone's standard time.</span></span> <span data-ttu-id="b42b3-119">通常，此字符串还用作时区的标识符。</span><span class="sxs-lookup"><span data-stu-id="b42b3-119">Typically, this string is also used as the time zone's identifier.</span></span>

3. <span data-ttu-id="b42b3-120">如果要使用不同于时区的标准名称的标识符，请定义时区标识符。</span><span class="sxs-lookup"><span data-stu-id="b42b3-120">If you want to use a different identifier than the time zone's standard name, define the time zone identifier.</span></span>

4. <span data-ttu-id="b42b3-121">实例化 <xref:System.TimeSpan> 定义时区与 UTC 的偏移量的对象。</span><span class="sxs-lookup"><span data-stu-id="b42b3-121">Instantiate a <xref:System.TimeSpan> object that defines the time zone's offset from UTC.</span></span> <span data-ttu-id="b42b3-122">时间时区晚于 UTC 的时区具有正偏移量。</span><span class="sxs-lookup"><span data-stu-id="b42b3-122">Time zones with times that are later than UTC have a positive offset.</span></span> <span data-ttu-id="b42b3-123">其时间早于 UTC 的时区具有负偏移量。</span><span class="sxs-lookup"><span data-stu-id="b42b3-123">Time zones with times that are earlier than UTC have a negative offset.</span></span>

5. <span data-ttu-id="b42b3-124">调用 <xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%29?displayProperty=nameWithType> 方法以实例化新时区。</span><span class="sxs-lookup"><span data-stu-id="b42b3-124">Call the <xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%29?displayProperty=nameWithType> method to instantiate the new time zone.</span></span>

## <a name="example"></a><span data-ttu-id="b42b3-125">示例</span><span class="sxs-lookup"><span data-stu-id="b42b3-125">Example</span></span>

<span data-ttu-id="b42b3-126">下面的示例定义了莫森，南极洲的自定义时区，该时区没有调整规则。</span><span class="sxs-lookup"><span data-stu-id="b42b3-126">The following example defines a custom time zone for Mawson, Antarctica, which has no adjustment rules.</span></span>

[!code-csharp[System.TimeZone2.CreateTimeZone#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#1)]
[!code-vb[System.TimeZone2.CreateTimeZone#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#1)]

<span data-ttu-id="b42b3-127">分配给属性的字符串 <xref:System.TimeZoneInfo.DisplayName%2A> 遵循标准格式，其中，时区与 UTC 的偏移量后跟时区的友好说明。</span><span class="sxs-lookup"><span data-stu-id="b42b3-127">The string assigned to the <xref:System.TimeZoneInfo.DisplayName%2A> property follows a standard format in which the time zone's offset from UTC is followed by a friendly description of the time zone.</span></span>

## <a name="compiling-the-code"></a><span data-ttu-id="b42b3-128">编译代码</span><span class="sxs-lookup"><span data-stu-id="b42b3-128">Compiling the code</span></span>

<span data-ttu-id="b42b3-129">此示例需要：</span><span class="sxs-lookup"><span data-stu-id="b42b3-129">This example requires:</span></span>

- <span data-ttu-id="b42b3-130">导入以下命名空间：</span><span class="sxs-lookup"><span data-stu-id="b42b3-130">That the following namespaces be imported:</span></span>

  [!code-csharp[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#6)]
  [!code-vb[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#6)]

## <a name="see-also"></a><span data-ttu-id="b42b3-131">另请参阅</span><span class="sxs-lookup"><span data-stu-id="b42b3-131">See also</span></span>

- [<span data-ttu-id="b42b3-132">日期、时间和时区</span><span class="sxs-lookup"><span data-stu-id="b42b3-132">Dates, times, and time zones</span></span>](index.md)
- [<span data-ttu-id="b42b3-133">时区概述</span><span class="sxs-lookup"><span data-stu-id="b42b3-133">Time zone overview</span></span>](time-zone-overview.md)
- [<span data-ttu-id="b42b3-134">如何：创建带有调整规则的时区</span><span class="sxs-lookup"><span data-stu-id="b42b3-134">How to: Create time zones with adjustment rules</span></span>](create-time-zones-with-adjustment-rules.md)
