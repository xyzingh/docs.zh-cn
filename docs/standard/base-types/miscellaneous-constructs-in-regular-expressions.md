---
title: 正则表达式中的其他构造
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- constructs, miscellaneous
- .NET regular expressions, miscellaneous constructs
- regular expressions, miscellaneous constructs
ms.assetid: 7d10d11f-680f-4721-b047-fb136316b4cd
ms.openlocfilehash: f7800dee67513f885339fad67c7a999cc06cca36
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889265"
---
# <a name="miscellaneous-constructs-in-regular-expressions"></a><span data-ttu-id="6fa24-102">正则表达式中的其他构造</span><span class="sxs-lookup"><span data-stu-id="6fa24-102">Miscellaneous Constructs in Regular Expressions</span></span>
<span data-ttu-id="6fa24-103">.NET 中的正则表达式包括三个其他语言构造。</span><span class="sxs-lookup"><span data-stu-id="6fa24-103">Regular expressions in .NET include three miscellaneous language constructs.</span></span> <span data-ttu-id="6fa24-104">其中一个使你可以在正则表达式模式中间启用或禁用特定匹配选项。</span><span class="sxs-lookup"><span data-stu-id="6fa24-104">One lets you enable or disable particular matching options in the middle of a regular expression pattern.</span></span> <span data-ttu-id="6fa24-105">其余两个使你可以在正则表达式中包含注释。</span><span class="sxs-lookup"><span data-stu-id="6fa24-105">The remaining two let you include comments in a regular expression.</span></span>  
  
## <a name="inline-options"></a><span data-ttu-id="6fa24-106">内联选项</span><span class="sxs-lookup"><span data-stu-id="6fa24-106">Inline Options</span></span>  
 <span data-ttu-id="6fa24-107">可以使用语法为正则表达式的一部分设置或禁用特定模式匹配选项</span><span class="sxs-lookup"><span data-stu-id="6fa24-107">You can set or disable specific pattern matching options for part of a regular expression by using the syntax</span></span>  
  
`(?imnsx-imnsx)`  
  
 <span data-ttu-id="6fa24-108">在问号后列出要启用的选项，在负号后列出要禁用的选项。</span><span class="sxs-lookup"><span data-stu-id="6fa24-108">You list the options you want to enable after the question mark, and the options you want to disable after the minus sign.</span></span> <span data-ttu-id="6fa24-109">下表对每个选项进行了描述。</span><span class="sxs-lookup"><span data-stu-id="6fa24-109">The following table describes each option.</span></span> <span data-ttu-id="6fa24-110">有关每个选项的更多信息，请参见[正则表达式选项](regular-expression-options.md)。</span><span class="sxs-lookup"><span data-stu-id="6fa24-110">For more information about each option, see [Regular Expression Options](regular-expression-options.md).</span></span>  
  
|<span data-ttu-id="6fa24-111">选项</span><span class="sxs-lookup"><span data-stu-id="6fa24-111">Option</span></span>|<span data-ttu-id="6fa24-112">描述</span><span class="sxs-lookup"><span data-stu-id="6fa24-112">Description</span></span>|  
|------------|-----------------|  
|`i`|<span data-ttu-id="6fa24-113">不区分大小写的匹配。</span><span class="sxs-lookup"><span data-stu-id="6fa24-113">Case-insensitive matching.</span></span>|  
|`m`|<span data-ttu-id="6fa24-114">多行模式。</span><span class="sxs-lookup"><span data-stu-id="6fa24-114">Multiline mode.</span></span>|  
|`n`|<span data-ttu-id="6fa24-115">仅显式捕获。</span><span class="sxs-lookup"><span data-stu-id="6fa24-115">Explicit captures only.</span></span> <span data-ttu-id="6fa24-116">（圆括号不充当捕获组。）</span><span class="sxs-lookup"><span data-stu-id="6fa24-116">(Parentheses do not act as capturing groups.)</span></span>|  
|`s`|<span data-ttu-id="6fa24-117">单行模式。</span><span class="sxs-lookup"><span data-stu-id="6fa24-117">Single-line mode.</span></span>|  
|`x`|<span data-ttu-id="6fa24-118">忽略未转义空格，并允许 x 模式注释。</span><span class="sxs-lookup"><span data-stu-id="6fa24-118">Ignore unescaped white space, and allow x-mode comments.</span></span>|  
  
 <span data-ttu-id="6fa24-119">如果 `(?imnsx-imnsx)` 构造定义的正则表达式选项有任何更改，更改在封闭组结束前一直有效。</span><span class="sxs-lookup"><span data-stu-id="6fa24-119">Any change in regular expression options defined by the `(?imnsx-imnsx)` construct remains in effect until the end of the enclosing group.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="6fa24-120">`(?imnsx-imnsx:`subexpression  `)` 分组构造为子表达式提供了完全相同的功能。</span><span class="sxs-lookup"><span data-stu-id="6fa24-120">The `(?imnsx-imnsx:`*subexpression*`)` grouping construct provides identical functionality for a subexpression.</span></span> <span data-ttu-id="6fa24-121">有关详细信息，请参阅 [分组构造](grouping-constructs-in-regular-expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="6fa24-121">For more information, see [Grouping Constructs](grouping-constructs-in-regular-expressions.md).</span></span>  
  
 <span data-ttu-id="6fa24-122">下面的示例使用 `i`、`n` 和 `x` 选项，启用不区分大小写和显式捕获，并在正则表达式中间忽略正则表达式模式中的空格。</span><span class="sxs-lookup"><span data-stu-id="6fa24-122">The following example uses the `i`, `n`, and `x` options to enable case insensitivity and explicit captures, and to ignore white space in the regular expression pattern in the middle of a regular expression.</span></span>  
  
 [!code-csharp[RegularExpressions.Language.Miscellaneous#1](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.miscellaneous/cs/miscellaneous1.cs#1)]
 [!code-vb[RegularExpressions.Language.Miscellaneous#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.miscellaneous/vb/miscellaneous1.vb#1)]  
  
 <span data-ttu-id="6fa24-123">该示例定义两个正则表达式。</span><span class="sxs-lookup"><span data-stu-id="6fa24-123">The example defines two regular expressions.</span></span> <span data-ttu-id="6fa24-124">第一个 `\b(D\w+)\s(d\w+)\b` 匹配以一个大写“D”和一个小写“d”开头的两个连续单词。</span><span class="sxs-lookup"><span data-stu-id="6fa24-124">The first, `\b(D\w+)\s(d\w+)\b`, matches two consecutive words that begin with an uppercase "D" and a lowercase "d".</span></span> <span data-ttu-id="6fa24-125">第二个正则表达式 `\b(D\w+)(?ixn) \s (d\w+) \b` 使用内联选项修改此模式，如下表所述。</span><span class="sxs-lookup"><span data-stu-id="6fa24-125">The second regular expression, `\b(D\w+)(?ixn) \s (d\w+) \b`, uses inline options to modify this pattern, as described in the following table.</span></span> <span data-ttu-id="6fa24-126">结果的比较会确认 `(?ixn)` 构造的效果。</span><span class="sxs-lookup"><span data-stu-id="6fa24-126">A comparison of the results confirms the effect of the `(?ixn)` construct.</span></span>  
  
|<span data-ttu-id="6fa24-127">模式</span><span class="sxs-lookup"><span data-stu-id="6fa24-127">Pattern</span></span>|<span data-ttu-id="6fa24-128">描述</span><span class="sxs-lookup"><span data-stu-id="6fa24-128">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="6fa24-129">在单词边界处开始。</span><span class="sxs-lookup"><span data-stu-id="6fa24-129">Start at a word boundary.</span></span>|  
|`(D\w+)`|<span data-ttu-id="6fa24-130">匹配后跟一个或多个单词字符的大写“D”。</span><span class="sxs-lookup"><span data-stu-id="6fa24-130">Match a capital "D" followed by one or more word characters.</span></span> <span data-ttu-id="6fa24-131">这是第一个捕获组。</span><span class="sxs-lookup"><span data-stu-id="6fa24-131">This is the first capture group.</span></span>|  
|`(?ixn)`|<span data-ttu-id="6fa24-132">从此处起，使比较不区分大小写，仅进行显式捕获，以及忽略正则表达式模式中的空格。</span><span class="sxs-lookup"><span data-stu-id="6fa24-132">From this point on, make comparisons case-insensitive, make only explicit captures, and ignore white space in the regular expression pattern.</span></span>|  
|`\s`|<span data-ttu-id="6fa24-133">与空白字符匹配。</span><span class="sxs-lookup"><span data-stu-id="6fa24-133">Match a white-space character.</span></span>|  
|`(d\w+)`|<span data-ttu-id="6fa24-134">匹配后跟一个或多个单词字符的大写或小写“d”。</span><span class="sxs-lookup"><span data-stu-id="6fa24-134">Match an uppercase or lowercase "d" followed by one or more word characters.</span></span> <span data-ttu-id="6fa24-135">因为 `n`（显式捕获）选项已启用，所以不会捕获此组。</span><span class="sxs-lookup"><span data-stu-id="6fa24-135">This group is not captured because the `n` (explicit capture) option was enabled..</span></span>|  
|`\b`|<span data-ttu-id="6fa24-136">与字边界匹配。</span><span class="sxs-lookup"><span data-stu-id="6fa24-136">Match a word boundary.</span></span>|  
  
## <a name="inline-comment"></a><span data-ttu-id="6fa24-137">内联注释</span><span class="sxs-lookup"><span data-stu-id="6fa24-137">Inline Comment</span></span>  
 <span data-ttu-id="6fa24-138">`(?#` comment`)` 构造可用于在正则表达式中添加内联注释  。</span><span class="sxs-lookup"><span data-stu-id="6fa24-138">The `(?#` *comment*`)` construct lets you include an inline comment in a regular expression.</span></span> <span data-ttu-id="6fa24-139">正则表达式引擎在模式匹配中不使用注释的任何部分，尽管注释仍包含在 <xref:System.Text.RegularExpressions.Regex.ToString%2A?displayProperty=nameWithType> 方法返回的字符串中。</span><span class="sxs-lookup"><span data-stu-id="6fa24-139">The regular expression engine does not use any part of the comment in pattern matching, although the comment is included in the string that is returned by the <xref:System.Text.RegularExpressions.Regex.ToString%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="6fa24-140">该注释在第一个右括号处终止。</span><span class="sxs-lookup"><span data-stu-id="6fa24-140">The comment ends at the first closing parenthesis.</span></span>  
  
 <span data-ttu-id="6fa24-141">下面的示例重复了上一部分的示例中的第一个正则表达式模式。</span><span class="sxs-lookup"><span data-stu-id="6fa24-141">The following example repeats the first regular expression pattern from the example in the previous section.</span></span> <span data-ttu-id="6fa24-142">它将两个内联注释添加到该正则表达式，以指示比较是否区分大小写。</span><span class="sxs-lookup"><span data-stu-id="6fa24-142">It adds two inline comments to the regular expression to indicate whether the comparison is case-sensitive.</span></span> <span data-ttu-id="6fa24-143">正则表达式模式 `\b((?# case-sensitive comparison)D\w+)\s(?ixn)((?#case-insensitive comparison)d\w+)\b` 按以下方式定义。</span><span class="sxs-lookup"><span data-stu-id="6fa24-143">The regular expression pattern, `\b((?# case-sensitive comparison)D\w+)\s(?ixn)((?#case-insensitive comparison)d\w+)\b`, is defined as follows.</span></span>  
  
|<span data-ttu-id="6fa24-144">模式</span><span class="sxs-lookup"><span data-stu-id="6fa24-144">Pattern</span></span>|<span data-ttu-id="6fa24-145">描述</span><span class="sxs-lookup"><span data-stu-id="6fa24-145">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="6fa24-146">在单词边界处开始。</span><span class="sxs-lookup"><span data-stu-id="6fa24-146">Start at a word boundary.</span></span>|  
|`(?# case-sensitive comparison)`|<span data-ttu-id="6fa24-147">注释。</span><span class="sxs-lookup"><span data-stu-id="6fa24-147">A comment.</span></span> <span data-ttu-id="6fa24-148">它不影响模式匹配行为。</span><span class="sxs-lookup"><span data-stu-id="6fa24-148">It does not affect pattern-matching behavior.</span></span>|  
|`(D\w+)`|<span data-ttu-id="6fa24-149">匹配后跟一个或多个单词字符的大写“D”。</span><span class="sxs-lookup"><span data-stu-id="6fa24-149">Match a capital "D" followed by one or more word characters.</span></span> <span data-ttu-id="6fa24-150">这是第一个捕获组。</span><span class="sxs-lookup"><span data-stu-id="6fa24-150">This is the first capturing group.</span></span>|  
|`\s`|<span data-ttu-id="6fa24-151">与空白字符匹配。</span><span class="sxs-lookup"><span data-stu-id="6fa24-151">Match a white-space character.</span></span>|  
|`(?ixn)`|<span data-ttu-id="6fa24-152">从此处起，使比较不区分大小写，仅进行显式捕获，以及忽略正则表达式模式中的空格。</span><span class="sxs-lookup"><span data-stu-id="6fa24-152">From this point on, make comparisons case-insensitive, make only explicit captures, and ignore white space in the regular expression pattern.</span></span>|  
|`(?#case-insensitive comparison)`|<span data-ttu-id="6fa24-153">注释。</span><span class="sxs-lookup"><span data-stu-id="6fa24-153">A comment.</span></span> <span data-ttu-id="6fa24-154">它不影响模式匹配行为。</span><span class="sxs-lookup"><span data-stu-id="6fa24-154">It does not affect pattern-matching behavior.</span></span>|  
|`(d\w+)`|<span data-ttu-id="6fa24-155">匹配后跟一个或多个单词字符的大写或小写“d”。</span><span class="sxs-lookup"><span data-stu-id="6fa24-155">Match an uppercase or lowercase "d" followed by one or more word characters.</span></span> <span data-ttu-id="6fa24-156">这是第二个捕获组。</span><span class="sxs-lookup"><span data-stu-id="6fa24-156">This is the second capture group.</span></span>|  
|`\b`|<span data-ttu-id="6fa24-157">与字边界匹配。</span><span class="sxs-lookup"><span data-stu-id="6fa24-157">Match a word boundary.</span></span>|  
  
 [!code-csharp[RegularExpressions.Language.Miscellaneous#2](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.miscellaneous/cs/miscellaneous2.cs#2)]
 [!code-vb[RegularExpressions.Language.Miscellaneous#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.miscellaneous/vb/miscellaneous2.vb#2)]  
  
## <a name="end-of-line-comment"></a><span data-ttu-id="6fa24-158">行尾注释</span><span class="sxs-lookup"><span data-stu-id="6fa24-158">End-of-Line Comment</span></span>  
 <span data-ttu-id="6fa24-159">数字符号 (`#`) 标记 x 模式注释，即从正则表达式模式末尾的未转义 # 字符开始一直延续到行末。</span><span class="sxs-lookup"><span data-stu-id="6fa24-159">A number sign (`#`)marks an x-mode comment, which starts at the unescaped # character at the end of the regular expression pattern and continues until the end of the line.</span></span> <span data-ttu-id="6fa24-160">若要使用此构造，必须启用 `x` 选项（通过内联选项），或在实例化 <xref:System.Text.RegularExpressions.Regex> 对象或调用静态 <xref:System.Text.RegularExpressions.Regex> 方法时向 `option` 参数提供 <xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace?displayProperty=nameWithType> 值。</span><span class="sxs-lookup"><span data-stu-id="6fa24-160">To use this construct, you must either enable the `x` option (through inline options) or supply the <xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace?displayProperty=nameWithType> value to the `option` parameter when instantiating the <xref:System.Text.RegularExpressions.Regex> object or calling a static <xref:System.Text.RegularExpressions.Regex> method.</span></span>  
  
 <span data-ttu-id="6fa24-161">下面的示例说明行尾注释构造。</span><span class="sxs-lookup"><span data-stu-id="6fa24-161">The following example illustrates the end-of-line comment construct.</span></span> <span data-ttu-id="6fa24-162">它确定字符串是否为包含至少一个格式项的复合格式字符串。</span><span class="sxs-lookup"><span data-stu-id="6fa24-162">It determines whether a string is a composite format string that includes at least one format item.</span></span> <span data-ttu-id="6fa24-163">下表描述了正则表达式模式中的构造：</span><span class="sxs-lookup"><span data-stu-id="6fa24-163">The following table describes the constructs in the regular expression pattern:</span></span>  
  
 `\{\d+(,-*\d+)*(\:\w{1,4}?)*\}(?x) # Looks for a composite format item.`  
  
|<span data-ttu-id="6fa24-164">模式</span><span class="sxs-lookup"><span data-stu-id="6fa24-164">Pattern</span></span>|<span data-ttu-id="6fa24-165">描述</span><span class="sxs-lookup"><span data-stu-id="6fa24-165">Description</span></span>|  
|-------------|-----------------|  
|`\{`|<span data-ttu-id="6fa24-166">匹配左大括号。</span><span class="sxs-lookup"><span data-stu-id="6fa24-166">Match an opening brace.</span></span>|  
|`\d+`|<span data-ttu-id="6fa24-167">匹配一个或多个十进制数字。</span><span class="sxs-lookup"><span data-stu-id="6fa24-167">Match one or more decimal digits.</span></span>|  
|`(,-*\d+)*`|<span data-ttu-id="6fa24-168">与零个或一个后跟一个可选负号、再后跟一个或多个十进制数字的逗号匹配。</span><span class="sxs-lookup"><span data-stu-id="6fa24-168">Match zero or one occurrence of a comma, followed by an optional minus sign, followed by one or more decimal digits.</span></span>|  
|`(\:\w{1,4}?)*`|<span data-ttu-id="6fa24-169">与零个或一个后跟一到四个（但尽可能少）空白字符的冒号匹配。</span><span class="sxs-lookup"><span data-stu-id="6fa24-169">Match zero or one occurrence of a colon, followed by one to four, but as few as possible, white-space characters.</span></span>|  
|`\}`|<span data-ttu-id="6fa24-170">匹配右大括号。</span><span class="sxs-lookup"><span data-stu-id="6fa24-170">Match a closing brace.</span></span>|  
|`(?x)`|<span data-ttu-id="6fa24-171">启用忽略模式空格选项，以便识别行尾注释。</span><span class="sxs-lookup"><span data-stu-id="6fa24-171">Enable the ignore pattern white-space option so that the end-of-line comment will be recognized.</span></span>|  
|`# Looks for a composite format item.`|<span data-ttu-id="6fa24-172">行尾注释。</span><span class="sxs-lookup"><span data-stu-id="6fa24-172">An end-of-line comment.</span></span>|  
  
 [!code-csharp[RegularExpressions.Language.Miscellaneous#3](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.miscellaneous/cs/miscellaneous3.cs#3)]
 [!code-vb[RegularExpressions.Language.Miscellaneous#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.miscellaneous/vb/miscellaneous3.vb#3)]  
  
 <span data-ttu-id="6fa24-173">请注意，还可以调用 <xref:System.Text.RegularExpressions.Regex.IsMatch%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=nameWithType> 方法并向它传递 <xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace?displayProperty=nameWithType> 枚举值，从而识别注释，而不用在正则表达式中提供 `(?x)` 构造。</span><span class="sxs-lookup"><span data-stu-id="6fa24-173">Note that, instead of providing the `(?x)` construct in the regular expression, the comment could also have been recognized by calling the <xref:System.Text.RegularExpressions.Regex.IsMatch%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=nameWithType> method and passing it the <xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace?displayProperty=nameWithType> enumeration value.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6fa24-174">请参阅</span><span class="sxs-lookup"><span data-stu-id="6fa24-174">See also</span></span>

- [<span data-ttu-id="6fa24-175">正则表达式语言 - 快速参考</span><span class="sxs-lookup"><span data-stu-id="6fa24-175">Regular Expression Language - Quick Reference</span></span>](regular-expression-language-quick-reference.md)
