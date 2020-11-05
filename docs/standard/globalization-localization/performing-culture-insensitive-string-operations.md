---
title: 执行不区分区域性的字符串操作
ms.date: 08/22/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- case mappings
- custom case mappings
- culture, custom sorting rules
- custom sorting rules
- culture-insensitive string operations, options for performing
- culture, custom case mappings
- culture-insensitive string operations, method overloads
ms.assetid: 579ef891-1f83-4c63-9ebd-2f40406b5b91
ms.openlocfilehash: 0f7e8dde395feb548e6808547a223a3fa8855561
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93063906"
---
# <a name="performing-culture-insensitive-string-operations"></a><span data-ttu-id="ce072-102">执行不区分区域性的字符串操作</span><span class="sxs-lookup"><span data-stu-id="ce072-102">Performing culture-insensitive string operations</span></span>

<span data-ttu-id="ce072-103">默认情况下，大多数执行区分区域性的字符串操作的 .NET 方法提供方法重载，以便于通过传递 <xref:System.Globalization.CultureInfo> 参数来显式指定要使用的区域性。</span><span class="sxs-lookup"><span data-stu-id="ce072-103">Most .NET methods that perform culture-sensitive string operations by default provide method overloads that allow you to explicitly specify the culture to use by passing a <xref:System.Globalization.CultureInfo> parameter.</span></span> <span data-ttu-id="ce072-104">这些重载允许消除大小写映射和排序规则中的区域性差异，保证获得不区分区域性的结果。</span><span class="sxs-lookup"><span data-stu-id="ce072-104">These overloads allow you to eliminate cultural variations in case mappings and sorting rules and guarantee culture-insensitive results.</span></span>  
  
 <span data-ttu-id="ce072-105">本节提供以下文章，用以说明如何使用默认区分区域性的 .NET 方法执行不区分区域性的字符串操作。</span><span class="sxs-lookup"><span data-stu-id="ce072-105">This section provides the following articles to demonstrate how to perform culture-insensitive string operations using .NET methods that are culture-sensitive by default.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="ce072-106">本节内容</span><span class="sxs-lookup"><span data-stu-id="ce072-106">In this section</span></span>  
 [<span data-ttu-id="ce072-107">执行不区分区域性的字符串比较</span><span class="sxs-lookup"><span data-stu-id="ce072-107">Performing Culture-Insensitive String Comparisons</span></span>](performing-culture-insensitive-string-comparisons.md)  
 <span data-ttu-id="ce072-108">介绍了如何使用 <xref:System.String.Compare%2A?displayProperty=nameWithType> 和 <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 方法执行非区域性敏感型字符串比较。</span><span class="sxs-lookup"><span data-stu-id="ce072-108">Describes how to use the <xref:System.String.Compare%2A?displayProperty=nameWithType> and <xref:System.String.CompareTo%2A?displayProperty=nameWithType> methods to perform culture-insensitive string comparisons.</span></span>  
  
 [<span data-ttu-id="ce072-109">执行不区分区域性的大小写更改</span><span class="sxs-lookup"><span data-stu-id="ce072-109">Performing Culture-Insensitive Case Changes</span></span>](performing-culture-insensitive-case-changes.md)  
 <span data-ttu-id="ce072-110">介绍了如何使用 <xref:System.String.ToUpper%2A?displayProperty=nameWithType>、<xref:System.String.ToLower%2A?displayProperty=nameWithType>、<xref:System.Char.ToUpper%2A?displayProperty=nameWithType> 和 <xref:System.Char.ToLower%2A?displayProperty=nameWithType> 方法执行非区域性敏感型大小写更改。</span><span class="sxs-lookup"><span data-stu-id="ce072-110">Describes how to use the <xref:System.String.ToUpper%2A?displayProperty=nameWithType>, <xref:System.String.ToLower%2A?displayProperty=nameWithType>, <xref:System.Char.ToUpper%2A?displayProperty=nameWithType>, and <xref:System.Char.ToLower%2A?displayProperty=nameWithType> methods to perform culture-insensitive case changes.</span></span>  
  
 [<span data-ttu-id="ce072-111">在集合中执行不区分区域性的字符串操作</span><span class="sxs-lookup"><span data-stu-id="ce072-111">Performing Culture-Insensitive String Operations in Collections</span></span>](performing-culture-insensitive-string-operations-in-collections.md)  
 <span data-ttu-id="ce072-112">介绍了如何使用 <xref:System.Collections.CaseInsensitiveComparer>、<xref:System.Collections.CaseInsensitiveHashCodeProvider> 类、<xref:System.Collections.SortedList>、<xref:System.Collections.ArrayList.Sort%2A?displayProperty=nameWithType> 和 <xref:System.Collections.Specialized.CollectionsUtil.CreateCaseInsensitiveHashtable%2A?displayProperty=nameWithType> 在集合中执行非区域性敏感型操作。</span><span class="sxs-lookup"><span data-stu-id="ce072-112">Describes how to use the <xref:System.Collections.CaseInsensitiveComparer>, <xref:System.Collections.CaseInsensitiveHashCodeProvider> class, <xref:System.Collections.SortedList>, <xref:System.Collections.ArrayList.Sort%2A?displayProperty=nameWithType> and <xref:System.Collections.Specialized.CollectionsUtil.CreateCaseInsensitiveHashtable%2A?displayProperty=nameWithType> to perform culture-insensitive operations in collections.</span></span>  
  
 [<span data-ttu-id="ce072-113">在数组中执行不区分区域性的字符串操作</span><span class="sxs-lookup"><span data-stu-id="ce072-113">Performing Culture-Insensitive String Operations in Arrays</span></span>](performing-culture-insensitive-string-operations-in-arrays.md)  
 <span data-ttu-id="ce072-114">介绍了如何使用 <xref:System.Array.Sort%2A?displayProperty=nameWithType> 和 <xref:System.Array.BinarySearch%2A?displayProperty=nameWithType> 方法在数组中执行非区域性敏感型操作。</span><span class="sxs-lookup"><span data-stu-id="ce072-114">Describes how to use the <xref:System.Array.Sort%2A?displayProperty=nameWithType> and <xref:System.Array.BinarySearch%2A?displayProperty=nameWithType> methods to perform culture-insensitive operations in arrays.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="ce072-115">相关章节</span><span class="sxs-lookup"><span data-stu-id="ce072-115">Related sections</span></span>  
 [<span data-ttu-id="ce072-116">不区分区域性的字符串操作</span><span class="sxs-lookup"><span data-stu-id="ce072-116">Culture-Insensitive String Operations</span></span>](culture-insensitive-string-operations.md)  
 <span data-ttu-id="ce072-117">介绍对字符串执行操作时应了解区域性的原因，并为何时执行区分区域性的操作、何时执行不区分区域性的操作提供了指南。</span><span class="sxs-lookup"><span data-stu-id="ce072-117">Describes why you should be aware of culture when performing operations on strings and provides guidelines for when to perform culture-sensitive operations and when to perform culture-insensitive operations.</span></span>

## <a name="see-also"></a><span data-ttu-id="ce072-118">另请参阅</span><span class="sxs-lookup"><span data-stu-id="ce072-118">See also</span></span>

- [<span data-ttu-id="ce072-119">排序权重表（适用于 Windows 系统上的 .NET）</span><span class="sxs-lookup"><span data-stu-id="ce072-119">Sorting Weight Tables (for .NET on Windows systems)</span></span>](https://www.microsoft.com/download/details.aspx?id=10921)
- [<span data-ttu-id="ce072-120">默认 Unicode 排序元素表（适用于 Linux 和 macOS 上 .NET Core）</span><span class="sxs-lookup"><span data-stu-id="ce072-120">Default Unicode Collation Element Table (for .NET Core on Linux and macOS)</span></span>](https://www.unicode.org/Public/UCA/latest/allkeys.txt)
