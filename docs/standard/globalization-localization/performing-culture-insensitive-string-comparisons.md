---
title: 执行不区分区域性的字符串比较
ms.date: 08/22/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- String.CompareTo method
- String.Compare method
- string comparison [.NET], culture-insensitive
- strings [.NET], comparing
- culture-insensitive string operations, comparisons
- culture parameter
ms.assetid: abae50ef-32f7-4a50-a540-fd256fd1aed0
ms.openlocfilehash: 1d8dc3f1bf686550eb94d7fb3003d4c21741739e
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93064140"
---
# <a name="performing-culture-insensitive-string-comparisons"></a><span data-ttu-id="e12cb-102">执行不区分区域性的字符串比较</span><span class="sxs-lookup"><span data-stu-id="e12cb-102">Performing Culture-Insensitive String Comparisons</span></span>
<span data-ttu-id="e12cb-103">默认情况下，<xref:System.String.Compare%2A?displayProperty=nameWithType> 方法执行区分区域性和区分大小写的比较。</span><span class="sxs-lookup"><span data-stu-id="e12cb-103">By default, the <xref:System.String.Compare%2A?displayProperty=nameWithType> method performs culture-sensitive and case-sensitive comparisons.</span></span> <span data-ttu-id="e12cb-104">此方法还包括多个重载，这些重载提供了一个 `culture` 参数和一个 `comparisonType` 参数，前者允许你指定要使用的区域性，后者允许你指定要使用的比较规则。</span><span class="sxs-lookup"><span data-stu-id="e12cb-104">This method also includes several overloads that provide a `culture` parameter that lets you specify the culture to use, and a `comparisonType` parameter that lets you specify the comparison rules to use.</span></span> <span data-ttu-id="e12cb-105">调用这些方法（而非调用默认重载）将消除与特定方法调用中使用的规则相关的任何歧义，并阐明某个特定比较是区分区域性的还是不区分区域性的。</span><span class="sxs-lookup"><span data-stu-id="e12cb-105">Calling these methods instead of the default overload removes any ambiguity about the rules used in a particular method call, and makes it clear whether a particular comparison is culture-sensitive or culture-insensitive.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="e12cb-106"><xref:System.String.CompareTo%2A?displayProperty=nameWithType> 方法的两种重载都执行区分区域性且区分大小写的比较；你不能使用此方法来执行不区分区域性的比较。</span><span class="sxs-lookup"><span data-stu-id="e12cb-106">Both overloads of the <xref:System.String.CompareTo%2A?displayProperty=nameWithType> method perform culture-sensitive and case-sensitive comparisons; you cannot use this method to perform culture-insensitive comparisons.</span></span> <span data-ttu-id="e12cb-107">为了使代码简单明了，建议你改用 <xref:System.String.Compare%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="e12cb-107">For code clarity, we recommend that you use the <xref:System.String.Compare%2A?displayProperty=nameWithType> method instead.</span></span>  
  
 <span data-ttu-id="e12cb-108">对于区分区域性的操作，请将 <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType> 或 <xref:System.StringComparison.CurrentCultureIgnoreCase?displayProperty=nameWithType> 枚举值指定为 `comparisonType` 参数。</span><span class="sxs-lookup"><span data-stu-id="e12cb-108">For culture-sensitive operations, specify the <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType> or <xref:System.StringComparison.CurrentCultureIgnoreCase?displayProperty=nameWithType> enumeration value as the `comparisonType` parameter.</span></span> <span data-ttu-id="e12cb-109">若要使用除当前区域性之外的指定区域性来执行区域性敏感型比较，请将表示相应区域性的 <xref:System.Globalization.CultureInfo> 对象指定为 `culture` 参数。</span><span class="sxs-lookup"><span data-stu-id="e12cb-109">If you want to perform a culture-sensitive comparison using a designated culture other than the current culture, specify the <xref:System.Globalization.CultureInfo> object that represents that culture as the `culture` parameter.</span></span>  
  
 <span data-ttu-id="e12cb-110"><xref:System.String.Compare%2A?displayProperty=nameWithType> 方法所支持的不区分区域性的字符串比较可以是语义的（基于固定区域性的排序约定）或非语义的（基于字符串中字符的序号值）。</span><span class="sxs-lookup"><span data-stu-id="e12cb-110">The culture-insensitive string comparisons supported by the <xref:System.String.Compare%2A?displayProperty=nameWithType> method are either linguistic (based on the sorting conventions of the invariant culture) or non-linguistic (based on the ordinal value of the characters in the string).</span></span> <span data-ttu-id="e12cb-111">大多数不区分区域性的字符串比较是非语义的。</span><span class="sxs-lookup"><span data-stu-id="e12cb-111">Most culture-insensitive string comparisons are non-linguistic.</span></span> <span data-ttu-id="e12cb-112">对于这些比较，请将 <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> 或 <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> 枚举值指定为 `comparisonType` 参数。</span><span class="sxs-lookup"><span data-stu-id="e12cb-112">For these comparisons, specify the <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> or <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> enumeration value as the `comparisonType` parameter.</span></span> <span data-ttu-id="e12cb-113">例如，如果安全决策（例如，用户名或密码比较）基于字符串比较的结果，则操作应不区分区域性且是非语义的，以确保结果不受特定区域性或语言的约定的影响。</span><span class="sxs-lookup"><span data-stu-id="e12cb-113">For example, if a security decision (such as a user name or password comparison) is based on the result of a string comparison, the operation should be culture-insensitive and non-linguistic to ensure that the result is not affected by the conventions of a particular culture or language.</span></span>  
  
 <span data-ttu-id="e12cb-114">如果你希望以一致方式处理来自多个区域性的语义相关字符串，请使用不区分区域性的语义字符串比较。</span><span class="sxs-lookup"><span data-stu-id="e12cb-114">Use culture-insensitive linguistic string comparison if you want to handle linguistically relevant strings from multiple cultures in a consistent way.</span></span> <span data-ttu-id="e12cb-115">例如，如果你的应用程序在列表框中显示使用多个字符集的字词，则不管当前区域性如何，你可能都需要按相同的顺序来显示这些字词。</span><span class="sxs-lookup"><span data-stu-id="e12cb-115">For example, if your application displays words that use multiple character sets in a list box, you might want to display words in the same order regardless of the current culture.</span></span> <span data-ttu-id="e12cb-116">对于不区分区域性的语义比较，.NET 将定义一个基于英语的语义约定的固定区域性。</span><span class="sxs-lookup"><span data-stu-id="e12cb-116">For culture-insensitive linguistic comparisons, .NET defines an invariant culture that is based on the linguistic conventions of English.</span></span> <span data-ttu-id="e12cb-117">若要执行不区分区域性的语义比较，请将 <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> 或 <xref:System.StringComparison.InvariantCultureIgnoreCase?displayProperty=nameWithType> 指定为 `comparisonType` 参数。</span><span class="sxs-lookup"><span data-stu-id="e12cb-117">To perform a culture-insensitive linguistic comparison, specify <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> or <xref:System.StringComparison.InvariantCultureIgnoreCase?displayProperty=nameWithType> as the `comparisonType` parameter.</span></span>  
  
 <span data-ttu-id="e12cb-118">下面的示例将执行两个不区分区域性的非语义字符串比较。</span><span class="sxs-lookup"><span data-stu-id="e12cb-118">The following example performs two culture-insensitive, non-linguistic string comparisons.</span></span> <span data-ttu-id="e12cb-119">第一个比较区分大小写，而第二个比较不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="e12cb-119">The first is case-sensitive, but the second is not.</span></span>  
  
 [!code-csharp[Conceptual.Strings.CultureInsensitiveComparison#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.cultureinsensitivecomparison/cs/cultureinsensitive1.cs#1)]
 [!code-vb[Conceptual.Strings.CultureInsensitiveComparison#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.cultureinsensitivecomparison/vb/cultureinsensitive1.vb#1)]  

<span data-ttu-id="e12cb-120">可以下载[排序权重表](https://www.microsoft.com/download/details.aspx?id=10921)，这是一组文本文件，其中包含有关 Windows 操作系统排序和比较操作中所使用的字符权重的信息，也可以下载[默认 Unicode 排序元素表](https://www.unicode.org/Public/UCA/latest/allkeys.txt)，这是适用于 Linux 和 macOS 的排序权重表。</span><span class="sxs-lookup"><span data-stu-id="e12cb-120">You can download the [Sorting Weight Tables](https://www.microsoft.com/download/details.aspx?id=10921), a set of text files that contain information on the character weights used in sorting and comparison operations for Windows operating systems, and the [Default Unicode Collation Element Table](https://www.unicode.org/Public/UCA/latest/allkeys.txt), the sort weight table for Linux and macOS.</span></span>

## <a name="see-also"></a><span data-ttu-id="e12cb-121">另请参阅</span><span class="sxs-lookup"><span data-stu-id="e12cb-121">See also</span></span>

- <xref:System.String.Compare%2A?displayProperty=nameWithType>
- <xref:System.String.CompareTo%2A?displayProperty=nameWithType>
- [<span data-ttu-id="e12cb-122">执行不区分区域性的字符串操作</span><span class="sxs-lookup"><span data-stu-id="e12cb-122">Performing Culture-Insensitive String Operations</span></span>](performing-culture-insensitive-string-operations.md)
- [<span data-ttu-id="e12cb-123">有关使用字符串的最佳做法</span><span class="sxs-lookup"><span data-stu-id="e12cb-123">Best Practices for Using Strings</span></span>](../base-types/best-practices-strings.md)
