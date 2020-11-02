---
title: 正则表达式示例：更改日期格式
ms.date: 06/30/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- searching with regular expressions, examples
- parsing text with regular expressions, examples
- regular expressions, examples
- .NET regular expressions, examples
- regular expressions [.NET], examples
- pattern-matching with regular expressions, examples
ms.assetid: 5fcc75a5-09d7-45ae-a4c0-9ad6085ac83d
ms.openlocfilehash: b5eca8c294349fada9cfb1cb3ed8e2012edd8bda
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889408"
---
# <a name="regular-expression-example-changing-date-formats"></a><span data-ttu-id="9447f-102">正则表达式示例：更改日期格式</span><span class="sxs-lookup"><span data-stu-id="9447f-102">Regular Expression Example: Changing Date Formats</span></span>
<span data-ttu-id="9447f-103">下面的代码示例使用 <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 方法，将格式为 mm  /dd  /yy  的日期替换为格式为 dd  -mm  -yy  的日期。</span><span class="sxs-lookup"><span data-stu-id="9447f-103">The following code example uses the <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> method to replace dates that have the form *mm*/*dd*/*yy* with dates that have the form *dd*-*mm*-*yy* .</span></span>  

[!INCLUDE [regex](../../../includes/regex.md)]

## <a name="example"></a><span data-ttu-id="9447f-104">示例</span><span class="sxs-lookup"><span data-stu-id="9447f-104">Example</span></span>  
 [!code-csharp[RegularExpressions.Examples.ChangeDateFormats#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/cs/Example_ChangeDateFormats1.cs#1)]
 [!code-vb[RegularExpressions.Examples.ChangeDateFormats#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/vb/Example_ChangeDateFormats1.vb#1)]  
  
 <span data-ttu-id="9447f-105">下面的代码演示如何在应用程序中调用 `MDYToDMY` 方法。</span><span class="sxs-lookup"><span data-stu-id="9447f-105">The following code shows how the `MDYToDMY` method can be called in an application.</span></span>  
  
 [!code-csharp[RegularExpressions.Examples.ChangeDateFormats#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/cs/Example_ChangeDateFormats1.cs#2)]
 [!code-vb[RegularExpressions.Examples.ChangeDateFormats#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/vb/Example_ChangeDateFormats1.vb#2)]  
  
## <a name="comments"></a><span data-ttu-id="9447f-106">注释</span><span class="sxs-lookup"><span data-stu-id="9447f-106">Comments</span></span>  
 <span data-ttu-id="9447f-107">正则表达式模式 `\b(?<month>\d{1,2})/(?<day>\d{1,2})/(?<year>\d{2,4})\b` 的释义如下表所示。</span><span class="sxs-lookup"><span data-stu-id="9447f-107">The regular expression pattern  `\b(?<month>\d{1,2})/(?<day>\d{1,2})/(?<year>\d{2,4})\b` is interpreted as shown in the following table.</span></span>  
  
|<span data-ttu-id="9447f-108">模式</span><span class="sxs-lookup"><span data-stu-id="9447f-108">Pattern</span></span>|<span data-ttu-id="9447f-109">说明</span><span class="sxs-lookup"><span data-stu-id="9447f-109">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="9447f-110">在单词边界处开始匹配。</span><span class="sxs-lookup"><span data-stu-id="9447f-110">Begin the match at a word boundary.</span></span>|  
|`(?<month>\d{1,2})`|<span data-ttu-id="9447f-111">匹配一个或两个十进制数字。</span><span class="sxs-lookup"><span data-stu-id="9447f-111">Match one or two decimal digits.</span></span> <span data-ttu-id="9447f-112">这是 `month` 捕获的组。</span><span class="sxs-lookup"><span data-stu-id="9447f-112">This is the `month` captured group.</span></span>|  
|`/`|<span data-ttu-id="9447f-113">匹配斜杠标记。</span><span class="sxs-lookup"><span data-stu-id="9447f-113">Match the slash mark.</span></span>|  
|`(?<day>\d{1,2})`|<span data-ttu-id="9447f-114">匹配一个或两个十进制数字。</span><span class="sxs-lookup"><span data-stu-id="9447f-114">Match one or two decimal digits.</span></span> <span data-ttu-id="9447f-115">这是 `day` 捕获的组。</span><span class="sxs-lookup"><span data-stu-id="9447f-115">This is the `day` captured group.</span></span>|  
|`/`|<span data-ttu-id="9447f-116">匹配斜杠标记。</span><span class="sxs-lookup"><span data-stu-id="9447f-116">Match the slash mark.</span></span>|  
|`(?<year>\d{2,4})`|<span data-ttu-id="9447f-117">匹配两个到四个十进制数。</span><span class="sxs-lookup"><span data-stu-id="9447f-117">Match from two to four decimal digits.</span></span> <span data-ttu-id="9447f-118">这是 `year` 捕获的组。</span><span class="sxs-lookup"><span data-stu-id="9447f-118">This is the `year` captured group.</span></span>|  
|`\b`|<span data-ttu-id="9447f-119">在单词边界处结束匹配。</span><span class="sxs-lookup"><span data-stu-id="9447f-119">End the match at a word boundary.</span></span>|  
  
 <span data-ttu-id="9447f-120">模式 `${day}-${month}-${year}` 如下表所示定义替换字符串。</span><span class="sxs-lookup"><span data-stu-id="9447f-120">The pattern `${day}-${month}-${year}` defines the replacement string as shown in the following table.</span></span>  
  
|<span data-ttu-id="9447f-121">模式</span><span class="sxs-lookup"><span data-stu-id="9447f-121">Pattern</span></span>|<span data-ttu-id="9447f-122">说明</span><span class="sxs-lookup"><span data-stu-id="9447f-122">Description</span></span>|  
|-------------|-----------------|  
|`$(day)`|<span data-ttu-id="9447f-123">添加由 `day` 捕获组捕获的字符串。</span><span class="sxs-lookup"><span data-stu-id="9447f-123">Add the string captured by the `day` capturing group.</span></span>|  
|`-`|<span data-ttu-id="9447f-124">添加连字符。</span><span class="sxs-lookup"><span data-stu-id="9447f-124">Add a hyphen.</span></span>|  
|`$(month)`|<span data-ttu-id="9447f-125">添加由 `month` 捕获组捕获的字符串。</span><span class="sxs-lookup"><span data-stu-id="9447f-125">Add the string captured by the `month` capturing group.</span></span>|  
|`-`|<span data-ttu-id="9447f-126">添加连字符。</span><span class="sxs-lookup"><span data-stu-id="9447f-126">Add a hyphen.</span></span>|  
|`$(year)`|<span data-ttu-id="9447f-127">添加由 `year` 捕获组捕获的字符串。</span><span class="sxs-lookup"><span data-stu-id="9447f-127">Add the string captured by the `year` capturing group.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="9447f-128">另请参阅</span><span class="sxs-lookup"><span data-stu-id="9447f-128">See also</span></span>

- [<span data-ttu-id="9447f-129">.NET 正则表达式</span><span class="sxs-lookup"><span data-stu-id="9447f-129">.NET Regular Expressions</span></span>](regular-expressions.md)
