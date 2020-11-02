---
title: 正则表达式示例：扫描 HREF
description: 请参见 .NET 中的正则表达式示例。 此示例搜索输入字符串并显示所有 href 属性值和它们的位置。
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
ms.assetid: fae2c15b-7adf-4b15-b118-58eb3906994f
ms.openlocfilehash: f2f7cca1e357971d2b0be2a0d7ddfb8ae208a44a
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889395"
---
# <a name="regular-expression-example-scanning-for-hrefs"></a><span data-ttu-id="95d98-104">正则表达式示例：扫描 HREF</span><span class="sxs-lookup"><span data-stu-id="95d98-104">Regular Expression Example: Scanning for HREFs</span></span>
<span data-ttu-id="95d98-105">下面的示例搜索输入字符串并显示所有 href="…" 的值和它们在字符串中的位置。</span><span class="sxs-lookup"><span data-stu-id="95d98-105">The following example searches an input string and displays all the href="…" values and their locations in the string.</span></span>  

[!INCLUDE [regex](../../../includes/regex.md)]

## <a name="the-regex-object"></a><span data-ttu-id="95d98-106">Regex 对象</span><span class="sxs-lookup"><span data-stu-id="95d98-106">The Regex Object</span></span>
 <span data-ttu-id="95d98-107">因为可以通过用户代码多次调用 `DumpHRefs` 方法，所以它使用 `static`（Visual Basic 中的 `Shared`）<xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="95d98-107">Because the `DumpHRefs` method can be called multiple times from user code, it uses the `static` (`Shared` in Visual Basic) <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="95d98-108">这样一来，正则表达式引擎不仅可以缓存正则表达式，还杜绝了每次调用方法时实例化新 <xref:System.Text.RegularExpressions.Regex> 对象产生的开销。</span><span class="sxs-lookup"><span data-stu-id="95d98-108">This enables the regular expression engine to cache the regular expression and avoids the overhead of instantiating a new <xref:System.Text.RegularExpressions.Regex> object each time the method is called.</span></span> <span data-ttu-id="95d98-109">随后使用 <xref:System.Text.RegularExpressions.Match> 对象循环访问字符串中的所有匹配。</span><span class="sxs-lookup"><span data-stu-id="95d98-109">A <xref:System.Text.RegularExpressions.Match> object is then used to iterate through all matches in the string.</span></span>  
  
 [!code-csharp[RegularExpressions.Examples.HREF#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.HREF/cs/example.cs#1)]
 [!code-vb[RegularExpressions.Examples.HREF#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.HREF/vb/example.vb#1)]  
  
 <span data-ttu-id="95d98-110">下面的示例演示对 `DumpHRefs` 方法的调用。</span><span class="sxs-lookup"><span data-stu-id="95d98-110">The following example then illustrates a call to the `DumpHRefs` method.</span></span>  
  
 [!code-csharp[RegularExpressions.Examples.HREF#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.HREF/cs/example.cs#2)]
 [!code-vb[RegularExpressions.Examples.HREF#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.HREF/vb/example.vb#2)]  
  
 <span data-ttu-id="95d98-111">正则表达式模式 `href\s*=\s*(?:["'](?<1>[^"']*)["']|(?<1>\S+))` 的含义如下表所示。</span><span class="sxs-lookup"><span data-stu-id="95d98-111">The regular expression pattern `href\s*=\s*(?:["'](?<1>[^"']*)["']|(?<1>\S+))` is interpreted as shown in the following table.</span></span>  
  
|<span data-ttu-id="95d98-112">模式</span><span class="sxs-lookup"><span data-stu-id="95d98-112">Pattern</span></span>|<span data-ttu-id="95d98-113">描述</span><span class="sxs-lookup"><span data-stu-id="95d98-113">Description</span></span>|  
|-------------|-----------------|  
|`href`|<span data-ttu-id="95d98-114">匹配文本字符串“href”。</span><span class="sxs-lookup"><span data-stu-id="95d98-114">Match the literal string "href".</span></span> <span data-ttu-id="95d98-115">匹配不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="95d98-115">The match is case-insensitive.</span></span>|  
|`\s*`|<span data-ttu-id="95d98-116">匹配零个或多个空白字符。</span><span class="sxs-lookup"><span data-stu-id="95d98-116">Match zero or more white-space characters.</span></span>|  
|`=`|<span data-ttu-id="95d98-117">匹配等于号。</span><span class="sxs-lookup"><span data-stu-id="95d98-117">Match the equals sign.</span></span>|  
|`\s*`|<span data-ttu-id="95d98-118">匹配零个或多个空白字符。</span><span class="sxs-lookup"><span data-stu-id="95d98-118">Match zero or more white-space characters.</span></span>|  
|`(?:\["'\](?<1>\[^"'\]*)["']|(?<1>\S+))`|<span data-ttu-id="95d98-119">匹配以下项之一，而不将结果分配到捕获组：</span><span class="sxs-lookup"><span data-stu-id="95d98-119">Match one of the following without assigning the result to a captured group:</span></span><br /> <ul><li><p><span data-ttu-id="95d98-120">一个引号或单引号，后跟零个或多个引号或单引号以外的任意字符，然后再后跟一个引号或单引号。</span><span class="sxs-lookup"><span data-stu-id="95d98-120">A quotation mark or apostrophe, followed by zero or more occurrences of any character other than a quotation mark or apostrophe, followed by a quotation mark or apostrophe.</span></span> <span data-ttu-id="95d98-121">名为 `1` 的组包含在此模式。</span><span class="sxs-lookup"><span data-stu-id="95d98-121">The group named `1` is included in this pattern.</span></span></p></li><li><p><span data-ttu-id="95d98-122">一个或多个非空格字符。</span><span class="sxs-lookup"><span data-stu-id="95d98-122">One or more non-white-space characters.</span></span> <span data-ttu-id="95d98-123">名为 `1` 的组包含在此模式。</span><span class="sxs-lookup"><span data-stu-id="95d98-123">The group named `1` is included in this pattern.</span></span></p></li></ul>|  
|`(?<1>[^"']*)`|<span data-ttu-id="95d98-124">将零个或多个引号或单引号以外的任意字符分配给名为 `1` 的捕获组。</span><span class="sxs-lookup"><span data-stu-id="95d98-124">Assign zero or more occurrences of any character other than a quotation mark or apostrophe to the capturing group named `1`.</span></span>|  
|`(?<1>\S+)`|<span data-ttu-id="95d98-125">将一个或多个非空白字符分配给名为 `1` 的捕获组。</span><span class="sxs-lookup"><span data-stu-id="95d98-125">Assign one or more non-white-space characters to the capturing group named `1`.</span></span>|  
  
## <a name="match-result-class"></a><span data-ttu-id="95d98-126">匹配结果类</span><span class="sxs-lookup"><span data-stu-id="95d98-126">Match Result Class</span></span>  
 <span data-ttu-id="95d98-127">搜索结果存储在 <xref:System.Text.RegularExpressions.Match> 类中，此类可访问搜索提取的所有子字符串。</span><span class="sxs-lookup"><span data-stu-id="95d98-127">The results of a search are stored in the <xref:System.Text.RegularExpressions.Match> class, which provides access to all the substrings extracted by the search.</span></span> <span data-ttu-id="95d98-128">它还会记住搜索的字符串和使用的正则表达式，因此可以调用 <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> 方法，从上一次搜索结束的位置开始执行另一次搜索。</span><span class="sxs-lookup"><span data-stu-id="95d98-128">It also remembers the string being searched and the regular expression being used, so it can call the <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> method to perform another search starting where the last one ended.</span></span>  
  
## <a name="explicitly-named-captures"></a><span data-ttu-id="95d98-129">显式命名的捕获</span><span class="sxs-lookup"><span data-stu-id="95d98-129">Explicitly Named Captures</span></span>  
 <span data-ttu-id="95d98-130">在传统正则表达式中，捕获圆括号会自动按顺序编号。</span><span class="sxs-lookup"><span data-stu-id="95d98-130">In traditional regular expressions, capturing parentheses are automatically numbered sequentially.</span></span> <span data-ttu-id="95d98-131">这会导致两个问题。</span><span class="sxs-lookup"><span data-stu-id="95d98-131">This leads to two problems.</span></span> <span data-ttu-id="95d98-132">首先，如果通过插入或删除一组圆括号修改正则表达式，则必须重新编写引用带编号捕获的所有代码才能反映新编号。</span><span class="sxs-lookup"><span data-stu-id="95d98-132">First, if a regular expression is modified by inserting or removing a set of parentheses, all code that refers to the numbered captures must be rewritten to reflect the new numbering.</span></span> <span data-ttu-id="95d98-133">其次，由于不同的圆括号组通常用于为可接受的匹配项提供两个替代表达式，则可能难以确定这两个表达式中的哪个表达式实际返回了结果。</span><span class="sxs-lookup"><span data-stu-id="95d98-133">Second, because different sets of parentheses often are used to provide two alternative expressions for an acceptable match, it might be difficult to determine which of the two expressions actually returned a result.</span></span>  
  
 <span data-ttu-id="95d98-134">为了解决这些问题，<xref:System.Text.RegularExpressions.Regex> 类支持语法 `(?<name>…)`，以便将匹配捕获到指定槽中（可以使用字符串或整数命名槽；如果使用整数命名，可以更快地召回）。</span><span class="sxs-lookup"><span data-stu-id="95d98-134">To address these problems, the <xref:System.Text.RegularExpressions.Regex> class supports the syntax `(?<name>…)` for capturing a match into a specified slot (the slot can be named using a string or an integer; integers can be recalled more quickly).</span></span> <span data-ttu-id="95d98-135">因此，相同字符串的替代匹配全都可以定向到相同位置。</span><span class="sxs-lookup"><span data-stu-id="95d98-135">Thus, alternative matches for the same string all can be directed to the same place.</span></span> <span data-ttu-id="95d98-136">发生冲突时，放入槽中的最后一个匹配项是成功的匹配项。</span><span class="sxs-lookup"><span data-stu-id="95d98-136">In case of a conflict, the last match dropped into a slot is the successful match.</span></span> <span data-ttu-id="95d98-137">（但是，提供了适用于单个槽的多个匹配项的完整列表。</span><span class="sxs-lookup"><span data-stu-id="95d98-137">(However, a complete list of multiple matches for a single slot is available.</span></span> <span data-ttu-id="95d98-138">有关详细信息，请参阅 <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> 集合。）</span><span class="sxs-lookup"><span data-stu-id="95d98-138">See the <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> collection for details.)</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="95d98-139">请参阅</span><span class="sxs-lookup"><span data-stu-id="95d98-139">See also</span></span>

- [<span data-ttu-id="95d98-140">.NET 正则表达式</span><span class="sxs-lookup"><span data-stu-id="95d98-140">.NET Regular Expressions</span></span>](regular-expressions.md)
