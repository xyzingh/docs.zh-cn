---
title: 比较 .NET 中的字符串
description: 了解用于比较 .NET 中字符串的方法。 了解 Compare、CompareOrdinal、CompareTo、StartsWith、EndsWith、Equals、IndexOf 和 LastIndexOf 方法。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- value comparisons of strings
- LastIndexOf method
- CompareTo method
- IndexOf method
- Compare method
- strings [.NET], comparing
- CompareOrdinal method
- EndsWith method
- Equals method
- StartsWith method
ms.assetid: 977dc094-fe19-4955-98ec-d2294d04a4ba
ms.openlocfilehash: 0efad4364d7d0070dd9c755234975e11ad524fbd
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400730"
---
# <a name="compare-strings-in-net"></a><span data-ttu-id="cebda-104">比较 .NET 中的字符串</span><span class="sxs-lookup"><span data-stu-id="cebda-104">Compare strings in .NET</span></span>

<span data-ttu-id="cebda-105">.NET 提供几种方法来比较字符串的值。</span><span class="sxs-lookup"><span data-stu-id="cebda-105">.NET provides several methods to compare the values of strings.</span></span> <span data-ttu-id="cebda-106">下表列出和描述值比较方法。</span><span class="sxs-lookup"><span data-stu-id="cebda-106">The following table lists and describes the value-comparison methods.</span></span>

|<span data-ttu-id="cebda-107">方法名称</span><span class="sxs-lookup"><span data-stu-id="cebda-107">Method name</span></span>|<span data-ttu-id="cebda-108">使用</span><span class="sxs-lookup"><span data-stu-id="cebda-108">Use</span></span>|
|-----------------|---------|
|<xref:System.String.Compare%2A?displayProperty=nameWithType>|<span data-ttu-id="cebda-109">比较两个字符串的值。</span><span class="sxs-lookup"><span data-stu-id="cebda-109">Compares the values of two strings.</span></span> <span data-ttu-id="cebda-110">返回一个整数值。</span><span class="sxs-lookup"><span data-stu-id="cebda-110">Returns an integer value.</span></span>|
|<xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType>|<span data-ttu-id="cebda-111">比较两个字符串的值而不考虑本地区域性。</span><span class="sxs-lookup"><span data-stu-id="cebda-111">Compares two strings without regard to local culture.</span></span> <span data-ttu-id="cebda-112">返回一个整数值。</span><span class="sxs-lookup"><span data-stu-id="cebda-112">Returns an integer value.</span></span>|
|<xref:System.String.CompareTo%2A?displayProperty=nameWithType>|<span data-ttu-id="cebda-113">比较当前字符串对象和另一个字符串。</span><span class="sxs-lookup"><span data-stu-id="cebda-113">Compares the current string object to another string.</span></span> <span data-ttu-id="cebda-114">返回一个整数值。</span><span class="sxs-lookup"><span data-stu-id="cebda-114">Returns an integer value.</span></span>|
|<xref:System.String.StartsWith%2A?displayProperty=nameWithType>|<span data-ttu-id="cebda-115">确定字符串是否以传递字的符串开头。</span><span class="sxs-lookup"><span data-stu-id="cebda-115">Determines whether a string begins with the string passed.</span></span> <span data-ttu-id="cebda-116">返回一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="cebda-116">Returns a Boolean value.</span></span>|
|<xref:System.String.EndsWith%2A?displayProperty=nameWithType>|<span data-ttu-id="cebda-117">确定字符串是否以传递的字符串结尾。</span><span class="sxs-lookup"><span data-stu-id="cebda-117">Determines whether a string ends with the string passed.</span></span> <span data-ttu-id="cebda-118">返回一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="cebda-118">Returns a Boolean value.</span></span>|
|<xref:System.String.Contains%2A?displayProperty=nameWithType>|<span data-ttu-id="cebda-119">确定一个字符或字符串是否出现在另一个字符串中。</span><span class="sxs-lookup"><span data-stu-id="cebda-119">Determines whether a character or string occurs within another string.</span></span> <span data-ttu-id="cebda-120">返回一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="cebda-120">Returns a Boolean value.</span></span>|
|<xref:System.String.Equals%2A?displayProperty=nameWithType>|<span data-ttu-id="cebda-121">确定两个字符串是否相同。</span><span class="sxs-lookup"><span data-stu-id="cebda-121">Determines whether two strings are the same.</span></span> <span data-ttu-id="cebda-122">返回一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="cebda-122">Returns a Boolean value.</span></span>|
|<xref:System.String.IndexOf%2A?displayProperty=nameWithType>|<span data-ttu-id="cebda-123">返回字符或字符串的索引位置，从正在检查的字符串的开头开始。</span><span class="sxs-lookup"><span data-stu-id="cebda-123">Returns the index position of a character or string, starting from the beginning of the string you are examining.</span></span> <span data-ttu-id="cebda-124">返回一个整数值。</span><span class="sxs-lookup"><span data-stu-id="cebda-124">Returns an integer value.</span></span>|
|<xref:System.String.LastIndexOf%2A?displayProperty=nameWithType>|<span data-ttu-id="cebda-125">返回字符或字符串的索引位置，从正在检查的字符串的结尾开始。</span><span class="sxs-lookup"><span data-stu-id="cebda-125">Returns the index position of a character or string, starting from the end of the string you are examining.</span></span> <span data-ttu-id="cebda-126">返回一个整数值。</span><span class="sxs-lookup"><span data-stu-id="cebda-126">Returns an integer value.</span></span>|

## <a name="compare-method"></a><span data-ttu-id="cebda-127">“比较”方法</span><span class="sxs-lookup"><span data-stu-id="cebda-127">Compare method</span></span>

<span data-ttu-id="cebda-128">静态 <xref:System.String.Compare%2A?displayProperty=nameWithType> 方法可以全面比较两个字符串。</span><span class="sxs-lookup"><span data-stu-id="cebda-128">The static <xref:System.String.Compare%2A?displayProperty=nameWithType> method provides a thorough way of comparing two strings.</span></span> <span data-ttu-id="cebda-129">此方法区分区域性。</span><span class="sxs-lookup"><span data-stu-id="cebda-129">This method is culturally aware.</span></span> <span data-ttu-id="cebda-130">你可以使用此函数比较两个字符串或两个字符串的子字符串。</span><span class="sxs-lookup"><span data-stu-id="cebda-130">You can use this function to compare two strings or substrings of two strings.</span></span> <span data-ttu-id="cebda-131">此外，还提供考虑或忽略大小写和区域性差别的重载。</span><span class="sxs-lookup"><span data-stu-id="cebda-131">Additionally, overloads are provided that regard or disregard case and cultural variance.</span></span> <span data-ttu-id="cebda-132">下表显示此方法可能返回三个整数值。</span><span class="sxs-lookup"><span data-stu-id="cebda-132">The following table shows the three integer values that this method might return.</span></span>

|<span data-ttu-id="cebda-133">返回值</span><span class="sxs-lookup"><span data-stu-id="cebda-133">Return value</span></span>|<span data-ttu-id="cebda-134">条件</span><span class="sxs-lookup"><span data-stu-id="cebda-134">Condition</span></span>|
|------------------|---------------|
|<span data-ttu-id="cebda-135">负整数</span><span class="sxs-lookup"><span data-stu-id="cebda-135">A negative integer</span></span>|<span data-ttu-id="cebda-136">在排序顺序中，第一个字符串在第二个字符串之前。</span><span class="sxs-lookup"><span data-stu-id="cebda-136">The first string precedes the second string in the sort order.</span></span><br /><br /> <span data-ttu-id="cebda-137">\- 或 -</span><span class="sxs-lookup"><span data-stu-id="cebda-137">-or-</span></span><br /><br /> <span data-ttu-id="cebda-138">第一个字符串是 `null`。</span><span class="sxs-lookup"><span data-stu-id="cebda-138">The first string is `null`.</span></span>|
|<span data-ttu-id="cebda-139">0</span><span class="sxs-lookup"><span data-stu-id="cebda-139">0</span></span>|<span data-ttu-id="cebda-140">第一个字符串和第二个字符串相等。</span><span class="sxs-lookup"><span data-stu-id="cebda-140">The first string and the second string are equal.</span></span><br /><br /> <span data-ttu-id="cebda-141">\- 或 -</span><span class="sxs-lookup"><span data-stu-id="cebda-141">-or-</span></span><br /><br /> <span data-ttu-id="cebda-142">两个字符串都是 `null`。</span><span class="sxs-lookup"><span data-stu-id="cebda-142">Both strings are `null`.</span></span>|
|<span data-ttu-id="cebda-143">正整数</span><span class="sxs-lookup"><span data-stu-id="cebda-143">A positive integer</span></span><br /><br /> <span data-ttu-id="cebda-144">\- 或 -</span><span class="sxs-lookup"><span data-stu-id="cebda-144">-or-</span></span><br /><br /> <span data-ttu-id="cebda-145">1</span><span class="sxs-lookup"><span data-stu-id="cebda-145">1</span></span>|<span data-ttu-id="cebda-146">在排序顺序中，第一个字符串在第二个字符串之后。</span><span class="sxs-lookup"><span data-stu-id="cebda-146">The first string follows the second string in the sort order.</span></span><br /><br /> <span data-ttu-id="cebda-147">\- 或 -</span><span class="sxs-lookup"><span data-stu-id="cebda-147">-or-</span></span><br /><br /> <span data-ttu-id="cebda-148">第二个字符串是 `null`。</span><span class="sxs-lookup"><span data-stu-id="cebda-148">The second string is `null`.</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="cebda-149"><xref:System.String.Compare%2A?displayProperty=nameWithType> 方法主要用于对字符串进行排序。</span><span class="sxs-lookup"><span data-stu-id="cebda-149">The <xref:System.String.Compare%2A?displayProperty=nameWithType> method is primarily intended for use when ordering or sorting strings.</span></span> <span data-ttu-id="cebda-150">不应使用 <xref:System.String.Compare%2A?displayProperty=nameWithType> 方法来测试相等性（即，显式查找返回值 0 而不考虑一个字符串是否小于或大于另一个）。</span><span class="sxs-lookup"><span data-stu-id="cebda-150">You should not use the <xref:System.String.Compare%2A?displayProperty=nameWithType> method to test for equality (that is, to explicitly look for a return value of 0 with no regard for whether one string is less than or greater than the other).</span></span> <span data-ttu-id="cebda-151">相反，若要确定两个字符串是否相等，请使用 <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="cebda-151">Instead, to determine whether two strings are equal, use the <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> method.</span></span>

 <span data-ttu-id="cebda-152">下面的示例使用 <xref:System.String.Compare%2A?displayProperty=nameWithType> 方法来确定两个字符串的相对值。</span><span class="sxs-lookup"><span data-stu-id="cebda-152">The following example uses the <xref:System.String.Compare%2A?displayProperty=nameWithType> method to determine the relative values of two strings.</span></span>

 [!code-cpp[Conceptual.String.BasicOps#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#6)]
 [!code-csharp[Conceptual.String.BasicOps#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#6)]
 [!code-vb[Conceptual.String.BasicOps#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#6)]

 <span data-ttu-id="cebda-153">此示例向控制台显示 `-1` 。</span><span class="sxs-lookup"><span data-stu-id="cebda-153">This example displays `-1` to the console.</span></span>

 <span data-ttu-id="cebda-154">前面的示例默认区分区域性。</span><span class="sxs-lookup"><span data-stu-id="cebda-154">The preceding example is culture-sensitive by default.</span></span> <span data-ttu-id="cebda-155">若要执行不区分区域性的字符串比较，请使用 <xref:System.String.Compare%2A?displayProperty=nameWithType> 方法的重载，这样就可以通过提供 *区域性* 参数来指定要使用的区域性。</span><span class="sxs-lookup"><span data-stu-id="cebda-155">To perform a culture-insensitive string comparison, use an overload of the <xref:System.String.Compare%2A?displayProperty=nameWithType> method that allows you to specify the culture to use by supplying a *culture* parameter.</span></span> <span data-ttu-id="cebda-156">有关展示了如何使用 <xref:System.String.Compare%2A?displayProperty=nameWithType> 方法执行非区域性敏感型比较的示例，请参阅[非区域性敏感型字符串比较](../globalization-localization/performing-culture-insensitive-string-comparisons.md)。</span><span class="sxs-lookup"><span data-stu-id="cebda-156">For an example that demonstrates how to use the <xref:System.String.Compare%2A?displayProperty=nameWithType> method to perform a culture-insensitive comparison, see [Culture-insensitive string comparisons](../globalization-localization/performing-culture-insensitive-string-comparisons.md).</span></span>

## <a name="compareordinal-method"></a><span data-ttu-id="cebda-157">CompareOrdinal 方法</span><span class="sxs-lookup"><span data-stu-id="cebda-157">CompareOrdinal method</span></span>

<span data-ttu-id="cebda-158"><xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType> 方法比较两个字符串对象而不考虑本地区域性。</span><span class="sxs-lookup"><span data-stu-id="cebda-158">The <xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType> method compares two string objects without considering the local culture.</span></span> <span data-ttu-id="cebda-159">此方法的返回值与上表中 `Compare` 方法返回的值相同。</span><span class="sxs-lookup"><span data-stu-id="cebda-159">The return values of this method are identical to the values returned by the `Compare` method in the previous table.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cebda-160"><xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType> 方法主要用于对字符串进行排序。</span><span class="sxs-lookup"><span data-stu-id="cebda-160">The <xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType> method is primarily intended for use when ordering or sorting strings.</span></span> <span data-ttu-id="cebda-161">不应使用 <xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType> 方法来测试相等性（即，显式查找返回值 0 而不考虑一个字符串是否小于或大于另一个）。</span><span class="sxs-lookup"><span data-stu-id="cebda-161">You should not use the <xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType> method to test for equality (that is, to explicitly look for a return value of 0 with no regard for whether one string is less than or greater than the other).</span></span> <span data-ttu-id="cebda-162">相反，若要确定两个字符串是否相等，请使用 <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="cebda-162">Instead, to determine whether two strings are equal, use the <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> method.</span></span>

 <span data-ttu-id="cebda-163">下面的示例使用 `CompareOrdinal` 方法来比较两个字符串的值。</span><span class="sxs-lookup"><span data-stu-id="cebda-163">The following example uses the `CompareOrdinal` method to compare the values of two strings.</span></span>

 [!code-cpp[Conceptual.String.BasicOps#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#7)]
 [!code-csharp[Conceptual.String.BasicOps#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#7)]
 [!code-vb[Conceptual.String.BasicOps#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#7)]

 <span data-ttu-id="cebda-164">此示例向控制台显示 `-32` 。</span><span class="sxs-lookup"><span data-stu-id="cebda-164">This example displays `-32` to the console.</span></span>

## <a name="compareto-method"></a><span data-ttu-id="cebda-165">CompareTo 方法</span><span class="sxs-lookup"><span data-stu-id="cebda-165">CompareTo method</span></span>

<span data-ttu-id="cebda-166"><xref:System.String.CompareTo%2A?displayProperty=nameWithType> 方法比较当前字符串对象封装到另一个字符串或对象的字符串。</span><span class="sxs-lookup"><span data-stu-id="cebda-166">The <xref:System.String.CompareTo%2A?displayProperty=nameWithType> method compares the string that the current string object encapsulates to another string or object.</span></span> <span data-ttu-id="cebda-167">此方法的返回值与上表中 <xref:System.String.Compare%2A?displayProperty=nameWithType> 方法返回的值相同。</span><span class="sxs-lookup"><span data-stu-id="cebda-167">The return values of this method are identical to the values returned by the <xref:System.String.Compare%2A?displayProperty=nameWithType> method in the previous table.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cebda-168"><xref:System.String.CompareTo%2A?displayProperty=nameWithType> 方法主要用于对字符串进行排序。</span><span class="sxs-lookup"><span data-stu-id="cebda-168">The <xref:System.String.CompareTo%2A?displayProperty=nameWithType> method is primarily intended for use when ordering or sorting strings.</span></span> <span data-ttu-id="cebda-169">不应使用 <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 方法来测试相等性（即，显式查找返回值 0 而不考虑一个字符串是否小于或大于另一个）。</span><span class="sxs-lookup"><span data-stu-id="cebda-169">You should not use the <xref:System.String.CompareTo%2A?displayProperty=nameWithType> method to test for equality (that is, to explicitly look for a return value of 0 with no regard for whether one string is less than or greater than the other).</span></span> <span data-ttu-id="cebda-170">相反，若要确定两个字符串是否相等，请使用 <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="cebda-170">Instead, to determine whether two strings are equal, use the <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> method.</span></span>

 <span data-ttu-id="cebda-171">下面的示例使用 <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 方法来比较 `string1` 对象和 `string2` 对象。</span><span class="sxs-lookup"><span data-stu-id="cebda-171">The following example uses the <xref:System.String.CompareTo%2A?displayProperty=nameWithType> method to compare the `string1` object to the `string2` object.</span></span>

 [!code-cpp[Conceptual.String.BasicOps#8](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#8)]
 [!code-csharp[Conceptual.String.BasicOps#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#8)]
 [!code-vb[Conceptual.String.BasicOps#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#8)]

 <span data-ttu-id="cebda-172">此示例向控制台显示 `-1` 。</span><span class="sxs-lookup"><span data-stu-id="cebda-172">This example displays `-1` to the console.</span></span>

 <span data-ttu-id="cebda-173"><xref:System.String.CompareTo%2A?displayProperty=nameWithType> 方法的所有重载均默认执行区分区域性且区分大小写的比较。</span><span class="sxs-lookup"><span data-stu-id="cebda-173">All overloads of the <xref:System.String.CompareTo%2A?displayProperty=nameWithType> method perform culture-sensitive and case-sensitive comparisons by default.</span></span> <span data-ttu-id="cebda-174">此方法不提供任何允许执行不区分区域性的比较的重载。</span><span class="sxs-lookup"><span data-stu-id="cebda-174">No overloads of this method are provided that allow you to perform a culture-insensitive comparison.</span></span> <span data-ttu-id="cebda-175">为了代码的清楚起见，建议改为使用 `String.Compare` 方法，指定 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> 执行区分区域性的操作或指定 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 执行不区分区域性的操作。</span><span class="sxs-lookup"><span data-stu-id="cebda-175">For code clarity, we recommend that you use the `String.Compare` method instead, specifying <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> for culture-sensitive operations or <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> for culture-insensitive operations.</span></span> <span data-ttu-id="cebda-176">有关演示如何使用 `String.Compare` 方法来执行区分和不区分区域性的比较的示例，请参阅 [执行不区分区域性的字符串比较](../globalization-localization/performing-culture-insensitive-string-comparisons.md)。</span><span class="sxs-lookup"><span data-stu-id="cebda-176">For examples that demonstrate how to use the `String.Compare` method to perform both culture-sensitive and culture-insensitive comparisons, see [Performing Culture-Insensitive String Comparisons](../globalization-localization/performing-culture-insensitive-string-comparisons.md).</span></span>

## <a name="equals-method"></a><span data-ttu-id="cebda-177">Equals 方法</span><span class="sxs-lookup"><span data-stu-id="cebda-177">Equals method</span></span>

<span data-ttu-id="cebda-178"><xref:System.String.Equals%2A?displayProperty=nameWithType> 方法能够轻松确定两个字符串是否相等。</span><span class="sxs-lookup"><span data-stu-id="cebda-178">The <xref:System.String.Equals%2A?displayProperty=nameWithType> method can easily determine if two strings are the same.</span></span> <span data-ttu-id="cebda-179">这个区分大小写的方法返回 `true` 或 `false` 布尔值。</span><span class="sxs-lookup"><span data-stu-id="cebda-179">This case-sensitive method returns a `true` or `false` Boolean value.</span></span> <span data-ttu-id="cebda-180">它可以在现有类中使用，如下一个示例所示。</span><span class="sxs-lookup"><span data-stu-id="cebda-180">It can be used from an existing class, as illustrated in the next example.</span></span> <span data-ttu-id="cebda-181">下面的示例使用 `Equals` 方法来确定一个字符串对象是否包含短语“Hello World”。</span><span class="sxs-lookup"><span data-stu-id="cebda-181">The following example uses the `Equals` method to determine whether a string object contains the phrase "Hello World".</span></span>

 [!code-cpp[Conceptual.String.BasicOps#9](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#9)]
 [!code-csharp[Conceptual.String.BasicOps#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#9)]
 [!code-vb[Conceptual.String.BasicOps#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#9)]

 <span data-ttu-id="cebda-182">此示例向控制台显示 `True` 。</span><span class="sxs-lookup"><span data-stu-id="cebda-182">This example displays `True` to the console.</span></span>

 <span data-ttu-id="cebda-183">此方法还可作为静态方法使用。</span><span class="sxs-lookup"><span data-stu-id="cebda-183">This method can also be used as a static method.</span></span> <span data-ttu-id="cebda-184">以下示例使用静态方法比较两个字符串对象。</span><span class="sxs-lookup"><span data-stu-id="cebda-184">The following example compares two string objects using a static method.</span></span>

 [!code-cpp[Conceptual.String.BasicOps#10](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#10)]
 [!code-csharp[Conceptual.String.BasicOps#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#10)]
 [!code-vb[Conceptual.String.BasicOps#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#10)]

 <span data-ttu-id="cebda-185">此示例向控制台显示 `True` 。</span><span class="sxs-lookup"><span data-stu-id="cebda-185">This example displays `True` to the console.</span></span>

## <a name="startswith-and-endswith-methods"></a><span data-ttu-id="cebda-186">StartsWith 和 EndsWith 方法</span><span class="sxs-lookup"><span data-stu-id="cebda-186">StartsWith and EndsWith methods</span></span>

<span data-ttu-id="cebda-187">可以使用 <xref:System.String.StartsWith%2A?displayProperty=nameWithType> 方法来确定一个字符串对象是否与另一个字符串以相同字符开头。</span><span class="sxs-lookup"><span data-stu-id="cebda-187">You can use the <xref:System.String.StartsWith%2A?displayProperty=nameWithType> method to determine whether a string object begins with the same characters that encompass another string.</span></span> <span data-ttu-id="cebda-188">如果当前字符串对象以传递的字符串开头，这个区分大小写的方法将返回 `true`，否则返回 `false`。</span><span class="sxs-lookup"><span data-stu-id="cebda-188">This case-sensitive method returns `true` if the current string object begins with the passed string and `false` if it does not.</span></span> <span data-ttu-id="cebda-189">以下示例使用此方法来确定一个字符串对象是否以“Hello”开头。</span><span class="sxs-lookup"><span data-stu-id="cebda-189">The following example uses this method to determine if a string object begins with "Hello".</span></span>

 [!code-cpp[Conceptual.String.BasicOps#11](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#11)]
 [!code-csharp[Conceptual.String.BasicOps#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#11)]
 [!code-vb[Conceptual.String.BasicOps#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#11)]

 <span data-ttu-id="cebda-190">此示例向控制台显示 `True` 。</span><span class="sxs-lookup"><span data-stu-id="cebda-190">This example displays `True` to the console.</span></span>

 <span data-ttu-id="cebda-191"><xref:System.String.EndsWith%2A?displayProperty=nameWithType> 方法比较传递的字符串和当前字符串对象末尾的字符。</span><span class="sxs-lookup"><span data-stu-id="cebda-191">The <xref:System.String.EndsWith%2A?displayProperty=nameWithType> method compares a passed string to the characters that exist at the end of the current string object.</span></span> <span data-ttu-id="cebda-192">它也返回一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="cebda-192">It also returns a Boolean value.</span></span> <span data-ttu-id="cebda-193">下面的示例使用 `EndsWith` 方法检查字符串的末尾。</span><span class="sxs-lookup"><span data-stu-id="cebda-193">The following example checks the end of a string using the `EndsWith` method.</span></span>

 [!code-cpp[Conceptual.String.BasicOps#12](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#12)]
 [!code-csharp[Conceptual.String.BasicOps#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#12)]
 [!code-vb[Conceptual.String.BasicOps#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#12)]

 <span data-ttu-id="cebda-194">此示例向控制台显示 `False` 。</span><span class="sxs-lookup"><span data-stu-id="cebda-194">This example displays `False` to the console.</span></span>

## <a name="indexof-and-lastindexof-methods"></a><span data-ttu-id="cebda-195">IndexOf 和 LastIndexOf 方法</span><span class="sxs-lookup"><span data-stu-id="cebda-195">IndexOf and LastIndexOf methods</span></span>

<span data-ttu-id="cebda-196">可以使用 <xref:System.String.IndexOf%2A?displayProperty=nameWithType> 方法来确定特定字符在字符串中的第一个匹配项的位置。</span><span class="sxs-lookup"><span data-stu-id="cebda-196">You can use the <xref:System.String.IndexOf%2A?displayProperty=nameWithType> method to determine the position of the first occurrence of a particular character within a string.</span></span> <span data-ttu-id="cebda-197">这个区分大小写的方法使用从零开始的索引从字符串的开头开始计数，并返回所传递字符的位置。</span><span class="sxs-lookup"><span data-stu-id="cebda-197">This case-sensitive method starts counting from the beginning of a string and returns the position of a passed character using a zero-based index.</span></span> <span data-ttu-id="cebda-198">如果无法找到该字符，则返回值 –1。</span><span class="sxs-lookup"><span data-stu-id="cebda-198">If the character cannot be found, a value of –1 is returned.</span></span>

<span data-ttu-id="cebda-199">下面的示例使用 `IndexOf` 方法搜索字符“`l`”在字符串中的第一个匹配项。</span><span class="sxs-lookup"><span data-stu-id="cebda-199">The following example uses the `IndexOf` method to search for the first occurrence of the '`l`' character in a string.</span></span>

 [!code-cpp[Conceptual.String.BasicOps#13](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#13)]
 [!code-csharp[Conceptual.String.BasicOps#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#13)]
 [!code-vb[Conceptual.String.BasicOps#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#13)]

 <span data-ttu-id="cebda-200">此示例向控制台显示 `2` 。</span><span class="sxs-lookup"><span data-stu-id="cebda-200">This example displays `2` to the console.</span></span>

 <span data-ttu-id="cebda-201"><xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> 方法类似于 `String.IndexOf` 方法，但它返回特定字符在字符串中的最后一个匹配项的位置。</span><span class="sxs-lookup"><span data-stu-id="cebda-201">The <xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> method is similar to the `String.IndexOf` method except that it returns the position of the last occurrence of a particular character within a string.</span></span> <span data-ttu-id="cebda-202">它不区分大小写，并且使用从零开始的索引。</span><span class="sxs-lookup"><span data-stu-id="cebda-202">It is case-sensitive and uses a zero-based index.</span></span>

 <span data-ttu-id="cebda-203">下面的示例使用 `LastIndexOf` 方法搜索字符“`l`”在字符串中的最后一个匹配项。</span><span class="sxs-lookup"><span data-stu-id="cebda-203">The following example uses the `LastIndexOf` method to search for the last occurrence of the '`l`' character in a string.</span></span>

 [!code-cpp[Conceptual.String.BasicOps#14](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#14)]
 [!code-csharp[Conceptual.String.BasicOps#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#14)]
 [!code-vb[Conceptual.String.BasicOps#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#14)]

 <span data-ttu-id="cebda-204">此示例向控制台显示 `9` 。</span><span class="sxs-lookup"><span data-stu-id="cebda-204">This example displays `9` to the console.</span></span>

 <span data-ttu-id="cebda-205">与 <xref:System.String.Remove%2A?displayProperty=nameWithType> 方法结合使用时，这两种方法都很有用。</span><span class="sxs-lookup"><span data-stu-id="cebda-205">Both methods are useful when used in conjunction with the <xref:System.String.Remove%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="cebda-206">可以使用 `IndexOf` 或 `LastIndexOf` 方法来检索字符的位置，然后将该位置提供给 `Remove` 方法，以删除字符或以该字符开头的单词。</span><span class="sxs-lookup"><span data-stu-id="cebda-206">You can use either the `IndexOf` or `LastIndexOf` methods to retrieve the position of a character, and then supply that position to the `Remove` method in order to remove a character or a word that begins with that character.</span></span>

## <a name="see-also"></a><span data-ttu-id="cebda-207">请参阅</span><span class="sxs-lookup"><span data-stu-id="cebda-207">See also</span></span>

- [<span data-ttu-id="cebda-208">有关使用 .NET 中字符串的最佳做法</span><span class="sxs-lookup"><span data-stu-id="cebda-208">Best Practices for Using Strings in .NET</span></span>](best-practices-strings.md)
- [<span data-ttu-id="cebda-209">基本字符串操作</span><span class="sxs-lookup"><span data-stu-id="cebda-209">Basic String Operations</span></span>](basic-string-operations.md)
- [<span data-ttu-id="cebda-210">执行不区分区域性的字符串操作</span><span class="sxs-lookup"><span data-stu-id="cebda-210">Performing Culture-Insensitive String Operations</span></span>](../globalization-localization/performing-culture-insensitive-string-operations.md)
- <span data-ttu-id="cebda-211">[排序权重表](https://www.microsoft.com/download/details.aspx?id=10921) - 适用于 Windows 上的 .NET Framework 和 .NET Core 1.0-3.1</span><span class="sxs-lookup"><span data-stu-id="cebda-211">[Sorting Weight Tables](https://www.microsoft.com/download/details.aspx?id=10921) - used by .NET Framework and .NET Core 1.0-3.1 on Windows</span></span>
- <span data-ttu-id="cebda-212">[默认 Unicode 排序元素表](https://www.unicode.org/Public/UCA/latest/allkeys.txt) - 适用于所有平台上的 .NET 5，以及 Linux 和 macOS 上的 .NET Core</span><span class="sxs-lookup"><span data-stu-id="cebda-212">[Default Unicode Collation Element Table](https://www.unicode.org/Public/UCA/latest/allkeys.txt) - used by .NET 5 on all platforms, and by .NET Core on Linux and macOS</span></span>
