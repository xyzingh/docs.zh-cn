---
title: 本地化评审
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- world-ready applications, localizability
- application development [.NET], localization
- localizability [.NET]
- international applications [.NET], localizability
- globalization [.NET], localizability
- culture, localizability
- localization [.NET], localizability
- global applications, localizability
- localizing resources
ms.assetid: 3aee2fbb-de47-4e37-8fe4-ddebb9719247
ms.openlocfilehash: 6aa0588ea4baa00be476a05c335cf2abaa22aab4
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93064153"
---
# <a name="localizability-review"></a><span data-ttu-id="9894b-102">本地化评审</span><span class="sxs-lookup"><span data-stu-id="9894b-102">Localizability review</span></span>

<span data-ttu-id="9894b-103">本地化分析检查是全球通用应用程序开发中的一个中间步骤。</span><span class="sxs-lookup"><span data-stu-id="9894b-103">The localizability review is an intermediate step in the development of a world-ready application.</span></span> <span data-ttu-id="9894b-104">它验证全球化应用程序是否已准备好进行本地化，以及是否能够识别需要特别处理的所有代码或所有用户界面元素。</span><span class="sxs-lookup"><span data-stu-id="9894b-104">It verifies that a globalized application is ready for localization and identifies any code or any aspects of the user interface that require special handling.</span></span> <span data-ttu-id="9894b-105">此步骤还有助于确保本地化过程不会将任何功能缺陷引入应用程序。</span><span class="sxs-lookup"><span data-stu-id="9894b-105">This step also helps ensure that the localization process will not introduce any functional defects into your application.</span></span> <span data-ttu-id="9894b-106">一旦本地化分析检查提出的所有问题都得到解决，就意味着可以对应用程序进行本地化了。</span><span class="sxs-lookup"><span data-stu-id="9894b-106">When all the issues raised by the localizability review have been addressed, your application is ready for localization.</span></span> <span data-ttu-id="9894b-107">如果本地化分析评审详尽彻底，则在本地化过程中应该不需要修改任何源代码。</span><span class="sxs-lookup"><span data-stu-id="9894b-107">If the localizability review is thorough, you should not have to modify any source code during the localization process.</span></span>

<span data-ttu-id="9894b-108">本地化分析检查包括以下三项检查：</span><span class="sxs-lookup"><span data-stu-id="9894b-108">The localizability review consists of the following three checks:</span></span>

- [<span data-ttu-id="9894b-109">是否已实现全球化建议？</span><span class="sxs-lookup"><span data-stu-id="9894b-109">Are the globalization recommendations implemented?</span></span>](#global)

- [<span data-ttu-id="9894b-110">是否已正确处理区域性敏感型功能？</span><span class="sxs-lookup"><span data-stu-id="9894b-110">Are culture-sensitive features handled correctly?</span></span>](#culture)

- [<span data-ttu-id="9894b-111">是否已使用国际数据测试应用？</span><span class="sxs-lookup"><span data-stu-id="9894b-111">Have you tested your application with international data?</span></span>](#test)

<a name="global"></a>
## <a name="implement-globalization-recommendations"></a><span data-ttu-id="9894b-112">实现全球化建议</span><span class="sxs-lookup"><span data-stu-id="9894b-112">Implement globalization recommendations</span></span>

<span data-ttu-id="9894b-113">如果在设计和开发应用时考虑了本地化因素，并且遵循了[全球化](globalization.md)一文中给出的建议，那么可本地化评审在很大程度上就会成为质量保证关口。</span><span class="sxs-lookup"><span data-stu-id="9894b-113">If you have designed and developed your application with localization in mind, and if you have followed the recommendations discussed in the [Globalization](globalization.md) article, the localizability review will largely be a quality assurance pass.</span></span> <span data-ttu-id="9894b-114">否则，请在此阶段评审并实现[全球化](globalization.md)建议，修复源代码中妨碍本地化的错误。</span><span class="sxs-lookup"><span data-stu-id="9894b-114">Otherwise, during this stage you should review and implement the recommendations for [globalization](globalization.md) and fix the errors in source code that prevent localization.</span></span>

<a name="culture"></a>
## <a name="handle-culture-sensitive-features"></a><span data-ttu-id="9894b-115">处理区分区域性的功能</span><span class="sxs-lookup"><span data-stu-id="9894b-115">Handle culture-sensitive features</span></span>

<span data-ttu-id="9894b-116">.NET 在许多方面都不提供编程支持，而且各区域性之间差别很大。</span><span class="sxs-lookup"><span data-stu-id="9894b-116">.NET does not provide programmatic support in a number of areas that vary widely by culture.</span></span> <span data-ttu-id="9894b-117">大多数情况下，你必须编写自定义代码来处理诸如以下方面的功能特性：</span><span class="sxs-lookup"><span data-stu-id="9894b-117">In most cases, you have to write custom code to handle feature areas like the following:</span></span>

- <span data-ttu-id="9894b-118">地址</span><span class="sxs-lookup"><span data-stu-id="9894b-118">Addresses</span></span>

- <span data-ttu-id="9894b-119">电话号码</span><span class="sxs-lookup"><span data-stu-id="9894b-119">Telephone numbers</span></span>

- <span data-ttu-id="9894b-120">纸张大小</span><span class="sxs-lookup"><span data-stu-id="9894b-120">Paper sizes</span></span>

- <span data-ttu-id="9894b-121">用于长度、重量、面积、体积和温度的度量单位</span><span class="sxs-lookup"><span data-stu-id="9894b-121">Units of measure used for lengths, weights, area, volume, and temperatures</span></span>

   <span data-ttu-id="9894b-122">虽然 .NET 不对度量单位之间的转换提供内置支持，但可以使用 <xref:System.Globalization.RegionInfo.IsMetric%2A?displayProperty=nameWithType> 属性确定特定国家或地区是否使用公制，如下面的示例所示。</span><span class="sxs-lookup"><span data-stu-id="9894b-122">Although .NET does not offer built-in support for converting between units of measure, you can use the <xref:System.Globalization.RegionInfo.IsMetric%2A?displayProperty=nameWithType> property to determine whether a particular country or region uses the metric system, as the following example illustrates.</span></span>

   [!code-csharp[Conceptual.Localizability#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.localizability/cs/ismetric1.cs#1)]
   [!code-vb[Conceptual.Localizability#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.localizability/vb/ismetric1.vb#1)]

<a name="test"></a>
## <a name="test-your-application"></a><span data-ttu-id="9894b-123">测试应用程序</span><span class="sxs-lookup"><span data-stu-id="9894b-123">Test your application</span></span>

<span data-ttu-id="9894b-124">在本地化应用程序之前，应当使用国际数据在操作系统的国际版本上对其进行测试。</span><span class="sxs-lookup"><span data-stu-id="9894b-124">Before you localize your application, you should test it by using international data on international versions of the operating system.</span></span> <span data-ttu-id="9894b-125">虽然此时不会对大部分用户界面进行本地化，但可以检测到如下问题：</span><span class="sxs-lookup"><span data-stu-id="9894b-125">Although most of the user interface will not be localized at this point, you will be able to detect problems such as the following:</span></span>

- <span data-ttu-id="9894b-126">在操作系统版本之间无法正确执行反序列化的序列化数据。</span><span class="sxs-lookup"><span data-stu-id="9894b-126">Serialized data that does not deserialize correctly across operating system versions.</span></span>

- <span data-ttu-id="9894b-127">不反映当前区域性的约定的数值数据。</span><span class="sxs-lookup"><span data-stu-id="9894b-127">Numeric data that does not reflect the conventions of the current culture.</span></span> <span data-ttu-id="9894b-128">例如，显示的数字可能带有错误的组分隔符、小数分隔符或货币符号。</span><span class="sxs-lookup"><span data-stu-id="9894b-128">For example, numbers may be displayed with inaccurate group separators, decimal separators, or currency symbols.</span></span>

- <span data-ttu-id="9894b-129">不反映当前区域性的约定的日期和时间数据。</span><span class="sxs-lookup"><span data-stu-id="9894b-129">Date and time data that does not reflect the conventions of the current culture.</span></span> <span data-ttu-id="9894b-130">例如，表示月和日的数字可能会以错误的顺序出现，日期分隔符可能不正确，或者时区信息可能不正确。</span><span class="sxs-lookup"><span data-stu-id="9894b-130">For example, numbers that represent the month and day may appear in the wrong order, date separators may be incorrect, or time zone information may be incorrect.</span></span>

- <span data-ttu-id="9894b-131">找不到的资源，因为尚未确定应用程序的默认区域性。</span><span class="sxs-lookup"><span data-stu-id="9894b-131">Resources that cannot be found because you have not identified a default culture for your application.</span></span>

- <span data-ttu-id="9894b-132">以特定区域性中的异常顺序显示的字符串。</span><span class="sxs-lookup"><span data-stu-id="9894b-132">Strings that are displayed in an unusual order for the specific culture.</span></span>

- <span data-ttu-id="9894b-133">返回意外结果的字符串比较或相等比较。</span><span class="sxs-lookup"><span data-stu-id="9894b-133">String comparisons or comparisons for equality that return unexpected results.</span></span>

<span data-ttu-id="9894b-134">如果在开发应用时遵循了全球化建议，并正确处理了区域性敏感型功能，同时还发现并解决了测试期间出现的本地化问题，就可以执行下一步[本地化](localization.md)。</span><span class="sxs-lookup"><span data-stu-id="9894b-134">If you've followed the globalization recommendations when developing your application, handled culture-sensitive features correctly, and identified and addressed the localization issues that arose during testing, you can proceed to the next step, [Localization](localization.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="9894b-135">另请参阅</span><span class="sxs-lookup"><span data-stu-id="9894b-135">See also</span></span>

- [<span data-ttu-id="9894b-136">全球化和本地化</span><span class="sxs-lookup"><span data-stu-id="9894b-136">Globalization and Localization</span></span>](index.md)
- [<span data-ttu-id="9894b-137">本地化</span><span class="sxs-lookup"><span data-stu-id="9894b-137">Localization</span></span>](localization.md)
- [<span data-ttu-id="9894b-138">全球化</span><span class="sxs-lookup"><span data-stu-id="9894b-138">Globalization</span></span>](globalization.md)
- [<span data-ttu-id="9894b-139">桌面应用中的资源</span><span class="sxs-lookup"><span data-stu-id="9894b-139">Resources in Desktop Apps</span></span>](../../framework/resources/index.md)
