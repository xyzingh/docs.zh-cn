---
title: 正则表达式中的限定符
description: 了解正则表达式限定符，该类限定符指定输入中必须存在字符、组或字符类的多少实例才能进行匹配。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- regular expressions, quantifiers
- metacharacters, quantifiers
- minimal matching quantifiers
- quantifiers in regular expressions
- .NET regular expressions, quantifiers
- quantifiers
- lazy quantifiers
ms.assetid: 36b81212-6511-49ed-a8f1-ff080415312f
ms.openlocfilehash: 361286b992180e1d7fdf18d88022780cc3aa53fc
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889421"
---
# <a name="quantifiers-in-regular-expressions"></a><span data-ttu-id="40848-103">正则表达式中的限定符</span><span class="sxs-lookup"><span data-stu-id="40848-103">Quantifiers in Regular Expressions</span></span>
<span data-ttu-id="40848-104">限定符指定输入中必须存在字符、组或字符类的多少实例才能找到匹配项。</span><span class="sxs-lookup"><span data-stu-id="40848-104">Quantifiers specify how many instances of a character, group, or character class must be present in the input for a match to be found.</span></span>  <span data-ttu-id="40848-105">下表列出了 .NET 支持的限定符。</span><span class="sxs-lookup"><span data-stu-id="40848-105">The following table lists the quantifiers supported by .NET.</span></span>  
  
|<span data-ttu-id="40848-106">贪婪限定符</span><span class="sxs-lookup"><span data-stu-id="40848-106">Greedy quantifier</span></span>|<span data-ttu-id="40848-107">惰性限定符</span><span class="sxs-lookup"><span data-stu-id="40848-107">Lazy quantifier</span></span>|<span data-ttu-id="40848-108">描述</span><span class="sxs-lookup"><span data-stu-id="40848-108">Description</span></span>|  
|-----------------------|---------------------|-----------------|  
|`*`|`*?`|<span data-ttu-id="40848-109">匹配零次或多次。</span><span class="sxs-lookup"><span data-stu-id="40848-109">Match zero or more times.</span></span>|  
|`+`|`+?`|<span data-ttu-id="40848-110">匹配一次或多次。</span><span class="sxs-lookup"><span data-stu-id="40848-110">Match one or more times.</span></span>|  
|`?`|`??`|<span data-ttu-id="40848-111">匹配零次或一次。</span><span class="sxs-lookup"><span data-stu-id="40848-111">Match zero or one time.</span></span>|  
|<span data-ttu-id="40848-112">`{` n `}`</span><span class="sxs-lookup"><span data-stu-id="40848-112">`{` *n* `}`</span></span>|<span data-ttu-id="40848-113">`{` n `}?`</span><span class="sxs-lookup"><span data-stu-id="40848-113">`{` *n* `}?`</span></span>|<span data-ttu-id="40848-114">恰好匹配 n 次。</span><span class="sxs-lookup"><span data-stu-id="40848-114">Match exactly *n* times.</span></span>|  
|<span data-ttu-id="40848-115">`{` n `,}`</span><span class="sxs-lookup"><span data-stu-id="40848-115">`{` *n* `,}`</span></span>|<span data-ttu-id="40848-116">`{` n `,}?`</span><span class="sxs-lookup"><span data-stu-id="40848-116">`{` *n* `,}?`</span></span>|<span data-ttu-id="40848-117">至少匹配 n 次。</span><span class="sxs-lookup"><span data-stu-id="40848-117">Match at least *n* times.</span></span>|  
|<span data-ttu-id="40848-118">`{` n `,` m `}` </span><span class="sxs-lookup"><span data-stu-id="40848-118">`{` *n* `,` *m* `}`</span></span>|<span data-ttu-id="40848-119">`{` n `,` m `}?` </span><span class="sxs-lookup"><span data-stu-id="40848-119">`{` *n* `,` *m* `}?`</span></span>|<span data-ttu-id="40848-120">匹配 n 到 m 次 。</span><span class="sxs-lookup"><span data-stu-id="40848-120">Match from *n* to *m* times.</span></span>|  
  
 <span data-ttu-id="40848-121">数量 `n` 和 `m` 是整数常量。</span><span class="sxs-lookup"><span data-stu-id="40848-121">The quantities `n` and `m` are integer constants.</span></span> <span data-ttu-id="40848-122">通常，限定符是贪婪的；它们使正则表达式引擎匹配尽可能多的特定模式实例。</span><span class="sxs-lookup"><span data-stu-id="40848-122">Ordinarily, quantifiers are greedy; they cause the regular expression engine to match as many occurrences of particular patterns as possible.</span></span> <span data-ttu-id="40848-123">向限定符追加 `?` 字符可使它成为惰性的；会使正则表达式引擎匹配尽可能少的实例。</span><span class="sxs-lookup"><span data-stu-id="40848-123">Appending the `?` character to a quantifier makes it lazy; it causes the regular expression engine to match as few occurrences as possible.</span></span> <span data-ttu-id="40848-124">有关贪婪与惰性限定符之间的差异的完整说明，请参见本主题后面的[贪婪与惰性限定符](#Greedy)部分。</span><span class="sxs-lookup"><span data-stu-id="40848-124">For a complete description of the difference between greedy and lazy quantifiers, see the section [Greedy and Lazy Quantifiers](#Greedy) later in this topic.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="40848-125">嵌套限定符（例如正则表达式模式 `(a*)*` 的行为）可以按输入字符串中的字符数的指数函数形式，来增加正则表达式引擎必须执行的比较次数。</span><span class="sxs-lookup"><span data-stu-id="40848-125">Nesting quantifiers (for example, as the regular expression pattern `(a*)*` does) can increase the number of comparisons that the regular expression engine must perform, as an exponential function of the number of characters in the input string.</span></span> <span data-ttu-id="40848-126">若要详细了解此行为及其解决方法，请参阅[回溯](backtracking-in-regular-expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="40848-126">For more information about this behavior and its workarounds, see [Backtracking](backtracking-in-regular-expressions.md).</span></span>  
  
## <a name="regular-expression-quantifiers"></a><span data-ttu-id="40848-127">正则表达式限定符</span><span class="sxs-lookup"><span data-stu-id="40848-127">Regular Expression Quantifiers</span></span>  
 <span data-ttu-id="40848-128">以下部分列出了 .NET 正则表达式支持的限定符。</span><span class="sxs-lookup"><span data-stu-id="40848-128">The following sections list the quantifiers supported by .NET regular expressions.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="40848-129">如果在正则表达式模式中遇到 \*、+、?、{ 和 } 字符，正则表达式引擎会将它们解释为量符或量符构造的一部分，除非它们包含在[字符类](character-classes-in-regular-expressions.md)中。</span><span class="sxs-lookup"><span data-stu-id="40848-129">If the \*, +, ?, {, and } characters are encountered in a regular expression pattern, the regular expression engine interprets them as quantifiers or part of quantifier constructs unless they are included in a [character class](character-classes-in-regular-expressions.md).</span></span> <span data-ttu-id="40848-130">若要在字符类外部将这些字符解释文本字符，必须通过在它们前面加反斜杠来对它们进行转义。</span><span class="sxs-lookup"><span data-stu-id="40848-130">To interpret these as literal characters outside a character class, you must escape them by preceding them with a backslash.</span></span> <span data-ttu-id="40848-131">例如，正则表达式模式中的字符串 `\*` 会被解释为文本星号（“\*”）字符。</span><span class="sxs-lookup"><span data-stu-id="40848-131">For example, the string `\*` in a regular expression pattern is interpreted as a literal asterisk ("\*") character.</span></span>  
  
### <a name="match-zero-or-more-times-"></a><span data-ttu-id="40848-132">匹配零次或多次：\*</span><span class="sxs-lookup"><span data-stu-id="40848-132">Match Zero or More Times: \*</span></span>  
 <span data-ttu-id="40848-133">`*` 限定符与前面的元素匹配零次或多次。</span><span class="sxs-lookup"><span data-stu-id="40848-133">The `*` quantifier matches the preceding element zero or more times.</span></span> <span data-ttu-id="40848-134">它相当于 `{0,}` 量符。</span><span class="sxs-lookup"><span data-stu-id="40848-134">It is equivalent to the `{0,}` quantifier.</span></span> <span data-ttu-id="40848-135">`*` 是贪婪量符，相当的惰性量符是 `*?`。</span><span class="sxs-lookup"><span data-stu-id="40848-135">`*` is a greedy quantifier whose lazy equivalent is `*?`.</span></span>  
  
 <span data-ttu-id="40848-136">下面的示例说明此正则表达式。</span><span class="sxs-lookup"><span data-stu-id="40848-136">The following example illustrates this regular expression.</span></span> <span data-ttu-id="40848-137">在输入字符串中的九个数字组中，五个与模式匹配，四个（`95`、`929`、`9219` 和 `9919`）不匹配。</span><span class="sxs-lookup"><span data-stu-id="40848-137">Of the nine digit groups in the input string, five match the pattern and four (`95`, `929`, `9219`, and `9919`) do not.</span></span>  
  
 [!code-csharp[RegularExpressions.Quantifiers#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#1)]
 [!code-vb[RegularExpressions.Quantifiers#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#1)]  
  
 <span data-ttu-id="40848-138">正则表达式模式的定义如下表所示。</span><span class="sxs-lookup"><span data-stu-id="40848-138">The regular expression pattern is defined as shown in the following table.</span></span>  
  
|<span data-ttu-id="40848-139">模式</span><span class="sxs-lookup"><span data-stu-id="40848-139">Pattern</span></span>|<span data-ttu-id="40848-140">描述</span><span class="sxs-lookup"><span data-stu-id="40848-140">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="40848-141">在单词边界处开始。</span><span class="sxs-lookup"><span data-stu-id="40848-141">Start at a word boundary.</span></span>|  
|`91*`|<span data-ttu-id="40848-142">匹配后跟零个或多个“1”字符的“9”。</span><span class="sxs-lookup"><span data-stu-id="40848-142">Match a "9" followed by zero or more "1" characters.</span></span>|  
|`9*`|<span data-ttu-id="40848-143">匹配零个或多个“9”字符。</span><span class="sxs-lookup"><span data-stu-id="40848-143">Match zero or more "9" characters.</span></span>|  
|`\b`|<span data-ttu-id="40848-144">在字边界结束。</span><span class="sxs-lookup"><span data-stu-id="40848-144">End at a word boundary.</span></span>|  
  
### <a name="match-one-or-more-times-"></a><span data-ttu-id="40848-145">匹配一次或多次：+</span><span class="sxs-lookup"><span data-stu-id="40848-145">Match One or More Times: +</span></span>  
 <span data-ttu-id="40848-146">`+` 量符匹配上一元素一次或多次。</span><span class="sxs-lookup"><span data-stu-id="40848-146">The `+` quantifier matches the preceding element one or more times.</span></span> <span data-ttu-id="40848-147">它相当于 `{1,}`。</span><span class="sxs-lookup"><span data-stu-id="40848-147">It is equivalent to `{1,}`.</span></span> <span data-ttu-id="40848-148">`+` 是贪婪量符，相当的惰性量符是 `+?`。</span><span class="sxs-lookup"><span data-stu-id="40848-148">`+` is a greedy quantifier whose lazy equivalent is `+?`.</span></span>  
  
 <span data-ttu-id="40848-149">例如，正则表达式 `\ban+\w*?\b` 会尝试匹配以后跟字母 `n` 的一个或多个实例的字母 `a` 开头的完整单词。</span><span class="sxs-lookup"><span data-stu-id="40848-149">For example, the regular expression `\ban+\w*?\b` tries to match entire words that begin with the letter `a` followed by one or more instances of the letter `n`.</span></span> <span data-ttu-id="40848-150">下面的示例说明此正则表达式。</span><span class="sxs-lookup"><span data-stu-id="40848-150">The following example illustrates this regular expression.</span></span> <span data-ttu-id="40848-151">正则表达式会匹配单词 `an`、`annual`、`announcement` 和 `antique`，并且正确地无法匹配 `autumn` 和 `all`。</span><span class="sxs-lookup"><span data-stu-id="40848-151">The regular expression matches the words `an`, `annual`, `announcement`, and `antique`, and correctly fails to match `autumn` and `all`.</span></span>  
  
 [!code-csharp[RegularExpressions.Quantifiers#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#2)]
 [!code-vb[RegularExpressions.Quantifiers#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#2)]  
  
 <span data-ttu-id="40848-152">正则表达式模式的定义如下表所示。</span><span class="sxs-lookup"><span data-stu-id="40848-152">The regular expression pattern is defined as shown in the following table.</span></span>  
  
|<span data-ttu-id="40848-153">模式</span><span class="sxs-lookup"><span data-stu-id="40848-153">Pattern</span></span>|<span data-ttu-id="40848-154">描述</span><span class="sxs-lookup"><span data-stu-id="40848-154">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="40848-155">在单词边界处开始。</span><span class="sxs-lookup"><span data-stu-id="40848-155">Start at a word boundary.</span></span>|  
|`an+`|<span data-ttu-id="40848-156">匹配后跟一个或多个“n”字符的“a”。</span><span class="sxs-lookup"><span data-stu-id="40848-156">Match an "a" followed by one or more "n" characters.</span></span>|  
|`\w*?`|<span data-ttu-id="40848-157">匹配单词字符零次或多次，但次数尽可能少。</span><span class="sxs-lookup"><span data-stu-id="40848-157">Match a word character zero or more times, but as few times as possible.</span></span>|  
|`\b`|<span data-ttu-id="40848-158">在字边界结束。</span><span class="sxs-lookup"><span data-stu-id="40848-158">End at a word boundary.</span></span>|  
  
### <a name="match-zero-or-one-time-"></a><span data-ttu-id="40848-159">匹配零次或一次：?</span><span class="sxs-lookup"><span data-stu-id="40848-159">Match Zero or One Time: ?</span></span>  
 <span data-ttu-id="40848-160">`?` 量符匹配上一元素零次或一次。</span><span class="sxs-lookup"><span data-stu-id="40848-160">The `?` quantifier matches the preceding element zero or one time.</span></span> <span data-ttu-id="40848-161">它相当于 `{0,1}`。</span><span class="sxs-lookup"><span data-stu-id="40848-161">It is equivalent to `{0,1}`.</span></span> <span data-ttu-id="40848-162">`?` 是贪婪量符，相当的惰性量符是 `??`。</span><span class="sxs-lookup"><span data-stu-id="40848-162">`?` is a greedy quantifier whose lazy equivalent is `??`.</span></span>  
  
 <span data-ttu-id="40848-163">例如，正则表达式 `\ban?\b` 会尝试匹配以后跟字母 `n` 的零个或一个实例的字母 `a` 开头的完整单词。</span><span class="sxs-lookup"><span data-stu-id="40848-163">For example, the regular expression `\ban?\b` tries to match entire words that begin with the letter `a` followed by zero or one instances of the letter `n`.</span></span> <span data-ttu-id="40848-164">换句话说，它会尝试匹配单词 `a` 和 `an`。</span><span class="sxs-lookup"><span data-stu-id="40848-164">In other words, it tries to match the words `a` and `an`.</span></span> <span data-ttu-id="40848-165">下面的示例说明此正则表达式。</span><span class="sxs-lookup"><span data-stu-id="40848-165">The following example illustrates this regular expression.</span></span>  
  
 [!code-csharp[RegularExpressions.Quantifiers#3](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#3)]
 [!code-vb[RegularExpressions.Quantifiers#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#3)]  
  
 <span data-ttu-id="40848-166">正则表达式模式的定义如下表所示。</span><span class="sxs-lookup"><span data-stu-id="40848-166">The regular expression pattern is defined as shown in the following table.</span></span>  
  
|<span data-ttu-id="40848-167">模式</span><span class="sxs-lookup"><span data-stu-id="40848-167">Pattern</span></span>|<span data-ttu-id="40848-168">描述</span><span class="sxs-lookup"><span data-stu-id="40848-168">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="40848-169">在单词边界处开始。</span><span class="sxs-lookup"><span data-stu-id="40848-169">Start at a word boundary.</span></span>|  
|`an?`|<span data-ttu-id="40848-170">匹配后跟零个或一个“n”字符的“a”。</span><span class="sxs-lookup"><span data-stu-id="40848-170">Match an "a" followed by zero or one "n" character.</span></span>|  
|`\b`|<span data-ttu-id="40848-171">在字边界结束。</span><span class="sxs-lookup"><span data-stu-id="40848-171">End at a word boundary.</span></span>|  
  
### <a name="match-exactly-n-times-n"></a><span data-ttu-id="40848-172">恰好匹配 n 次：{n}</span><span class="sxs-lookup"><span data-stu-id="40848-172">Match Exactly n Times: {n}</span></span>  
 <span data-ttu-id="40848-173">`{`n`}` 限定符与前面的元素恰好匹配 n 次，其中 n 是任何整数  。</span><span class="sxs-lookup"><span data-stu-id="40848-173">The `{`*n*`}` quantifier matches the preceding element exactly *n* times, where *n* is any integer.</span></span> <span data-ttu-id="40848-174">`{`n`}` 是贪婪限定符，其惰性等效项是 `{`n`}?` 。</span><span class="sxs-lookup"><span data-stu-id="40848-174">`{`*n*`}` is a greedy quantifier whose lazy equivalent is `{`*n*`}?`.</span></span>  
  
 <span data-ttu-id="40848-175">例如，正则表达式 `\b\d+\,\d{3}\b` 会尝试匹配依次后跟一个或多个十进制数字、三个十进制数字、一个单词边界的单词边界。</span><span class="sxs-lookup"><span data-stu-id="40848-175">For example, the regular expression `\b\d+\,\d{3}\b` tries to match a word boundary followed by one or more decimal digits followed by three decimal digits followed by a word boundary.</span></span> <span data-ttu-id="40848-176">下面的示例说明此正则表达式。</span><span class="sxs-lookup"><span data-stu-id="40848-176">The following example illustrates this regular expression.</span></span>  
  
 [!code-csharp[RegularExpressions.Quantifiers#4](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#4)]
 [!code-vb[RegularExpressions.Quantifiers#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#4)]  
  
 <span data-ttu-id="40848-177">正则表达式模式的定义如下表所示。</span><span class="sxs-lookup"><span data-stu-id="40848-177">The regular expression pattern is defined as shown in the following table.</span></span>  
  
|<span data-ttu-id="40848-178">模式</span><span class="sxs-lookup"><span data-stu-id="40848-178">Pattern</span></span>|<span data-ttu-id="40848-179">描述</span><span class="sxs-lookup"><span data-stu-id="40848-179">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="40848-180">在单词边界处开始。</span><span class="sxs-lookup"><span data-stu-id="40848-180">Start at a word boundary.</span></span>|  
|`\d+`|<span data-ttu-id="40848-181">匹配一个或多个十进制数字。</span><span class="sxs-lookup"><span data-stu-id="40848-181">Match one or more decimal digits.</span></span>|  
|`\,`|<span data-ttu-id="40848-182">匹配逗号字符。</span><span class="sxs-lookup"><span data-stu-id="40848-182">Match a comma character.</span></span>|  
|`\d{3}`|<span data-ttu-id="40848-183">匹配三个十进制数字。</span><span class="sxs-lookup"><span data-stu-id="40848-183">Match three decimal digits.</span></span>|  
|`\b`|<span data-ttu-id="40848-184">在字边界结束。</span><span class="sxs-lookup"><span data-stu-id="40848-184">End at a word boundary.</span></span>|  
  
### <a name="match-at-least-n-times-n"></a><span data-ttu-id="40848-185">至少匹配 n 次：{n,}</span><span class="sxs-lookup"><span data-stu-id="40848-185">Match at Least n Times: {n,}</span></span>  
 <span data-ttu-id="40848-186">`{`n`,}` 限定符与前面的元素至少匹配 n 次，其中 n 是任何整数  。</span><span class="sxs-lookup"><span data-stu-id="40848-186">The `{`*n*`,}` quantifier matches the preceding element at least *n* times, where *n* is any integer.</span></span> <span data-ttu-id="40848-187">`{`n`,}` 是贪婪限定符，其惰性等效项是 `{`n`,}?` 。</span><span class="sxs-lookup"><span data-stu-id="40848-187">`{`*n*`,}` is a greedy quantifier whose lazy equivalent is `{`*n*`,}?`.</span></span>  
  
 <span data-ttu-id="40848-188">例如，正则表达式 `\b\d{2,}\b\D+` 会尝试匹配依次后跟至少两个数字、一个单词边界和一个非数字字符的单词边界。</span><span class="sxs-lookup"><span data-stu-id="40848-188">For example, the regular expression `\b\d{2,}\b\D+` tries to match a word boundary followed by at least two digits followed by a word boundary and a non-digit character.</span></span> <span data-ttu-id="40848-189">下面的示例说明此正则表达式。</span><span class="sxs-lookup"><span data-stu-id="40848-189">The following example illustrates this regular expression.</span></span> <span data-ttu-id="40848-190">正则表达式无法匹配短语 `"7 days"`，因为它只包含一个十进制数字，但可以成功匹配短语 `"10 weeks and 300 years"`。</span><span class="sxs-lookup"><span data-stu-id="40848-190">The regular expression fails to match the phrase `"7 days"` because it contains just one decimal digit, but it successfully matches the phrases `"10 weeks and 300 years"`.</span></span>  
  
 [!code-csharp[RegularExpressions.Quantifiers#5](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#5)]
 [!code-vb[RegularExpressions.Quantifiers#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#5)]  
  
 <span data-ttu-id="40848-191">正则表达式模式的定义如下表所示。</span><span class="sxs-lookup"><span data-stu-id="40848-191">The regular expression pattern is defined as shown in the following table.</span></span>  
  
|<span data-ttu-id="40848-192">模式</span><span class="sxs-lookup"><span data-stu-id="40848-192">Pattern</span></span>|<span data-ttu-id="40848-193">描述</span><span class="sxs-lookup"><span data-stu-id="40848-193">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="40848-194">在单词边界处开始。</span><span class="sxs-lookup"><span data-stu-id="40848-194">Start at a word boundary.</span></span>|  
|`\d{2,}`|<span data-ttu-id="40848-195">匹配至少两个十进制数字。</span><span class="sxs-lookup"><span data-stu-id="40848-195">Match at least two decimal digits.</span></span>|  
|`\b`|<span data-ttu-id="40848-196">与字边界匹配。</span><span class="sxs-lookup"><span data-stu-id="40848-196">Match a word boundary.</span></span>|  
|`\D+`|<span data-ttu-id="40848-197">匹配至少一个非十进制数字。</span><span class="sxs-lookup"><span data-stu-id="40848-197">Match at least one non-decimal digit.</span></span>|  
  
### <a name="match-between-n-and-m-times-nm"></a><span data-ttu-id="40848-198">匹配 n 到 m 次：{n,m}</span><span class="sxs-lookup"><span data-stu-id="40848-198">Match Between n and m Times: {n,m}</span></span>  
 <span data-ttu-id="40848-199">`{`n`,`m`}` 限定符与前面的元素至少匹配 n 次，但不超过 m 次，其中 n 和 m 是整数     。</span><span class="sxs-lookup"><span data-stu-id="40848-199">The `{`*n*`,`*m*`}` quantifier matches the preceding element at least *n* times, but no more than *m* times, where *n* and *m* are integers.</span></span> <span data-ttu-id="40848-200">`{`n`,`m`}` 是贪婪限定符，相当的惰性限定符是 `{`n`,`m`}?`   。</span><span class="sxs-lookup"><span data-stu-id="40848-200">`{`*n*`,`*m*`}` is a greedy quantifier whose lazy equivalent is `{`*n*`,`*m*`}?`.</span></span>  
  
 <span data-ttu-id="40848-201">在下面的示例中，正则表达式 `(00\s){2,4}` 尝试与后跟一个空格的两个零数字匹配两到四次。</span><span class="sxs-lookup"><span data-stu-id="40848-201">In the following example, the regular expression `(00\s){2,4}` tries to match between two and four occurrences of two zero digits followed by a space.</span></span> <span data-ttu-id="40848-202">请注意，输入字符串的最后一部分包含此模式五次，而不是最大值四次。</span><span class="sxs-lookup"><span data-stu-id="40848-202">Note that the final portion of the input string includes this pattern five times rather than the maximum of four.</span></span> <span data-ttu-id="40848-203">但是，只有此子字符串的初始部分（到空格和第五对零）与正则表达式模式匹配。</span><span class="sxs-lookup"><span data-stu-id="40848-203">However, only the initial portion of this substring (up to the space and the fifth pair of zeros) matches the regular expression pattern.</span></span>  
  
 [!code-csharp[RegularExpressions.Quantifiers#6](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#6)]
 [!code-vb[RegularExpressions.Quantifiers#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#6)]  
  
### <a name="match-zero-or-more-times-lazy-match-"></a><span data-ttu-id="40848-204">匹配零次或多次（惰性匹配）：\*?</span><span class="sxs-lookup"><span data-stu-id="40848-204">Match Zero or More Times (Lazy Match): \*?</span></span>  
 <span data-ttu-id="40848-205">`*?` 量符匹配上一元素零次或多次，但次数尽可能少。</span><span class="sxs-lookup"><span data-stu-id="40848-205">The `*?` quantifier matches the preceding element zero or more times, but as few times as possible.</span></span> <span data-ttu-id="40848-206">它是贪婪量符 `*` 对应的惰性量符。</span><span class="sxs-lookup"><span data-stu-id="40848-206">It is the lazy counterpart of the greedy quantifier `*`.</span></span>  
  
 <span data-ttu-id="40848-207">在下面的示例中，正则表达式 `\b\w*?oo\w*?\b` 匹配包含字符串 `oo` 的所有单词。</span><span class="sxs-lookup"><span data-stu-id="40848-207">In the following example, the regular expression `\b\w*?oo\w*?\b` matches all words that contain the string `oo`.</span></span>  
  
 [!code-csharp[RegularExpressions.Quantifiers#7](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#7)]
 [!code-vb[RegularExpressions.Quantifiers#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#7)]  
  
 <span data-ttu-id="40848-208">正则表达式模式的定义如下表所示。</span><span class="sxs-lookup"><span data-stu-id="40848-208">The regular expression pattern is defined as shown in the following table.</span></span>  
  
|<span data-ttu-id="40848-209">模式</span><span class="sxs-lookup"><span data-stu-id="40848-209">Pattern</span></span>|<span data-ttu-id="40848-210">描述</span><span class="sxs-lookup"><span data-stu-id="40848-210">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="40848-211">在单词边界处开始。</span><span class="sxs-lookup"><span data-stu-id="40848-211">Start at a word boundary.</span></span>|  
|`\w*?`|<span data-ttu-id="40848-212">匹配零个或多个单词字符，但字符要尽可能的少。</span><span class="sxs-lookup"><span data-stu-id="40848-212">Match zero or more word characters, but as few characters as possible.</span></span>|  
|`oo`|<span data-ttu-id="40848-213">匹配字符串“oo”。</span><span class="sxs-lookup"><span data-stu-id="40848-213">Match the string "oo".</span></span>|  
|`\w*?`|<span data-ttu-id="40848-214">匹配零个或多个单词字符，但字符要尽可能的少。</span><span class="sxs-lookup"><span data-stu-id="40848-214">Match zero or more word characters, but as few characters as possible.</span></span>|  
|`\b`|<span data-ttu-id="40848-215">在单词边界处结束。</span><span class="sxs-lookup"><span data-stu-id="40848-215">End on a word boundary.</span></span>|  
  
### <a name="match-one-or-more-times-lazy-match-"></a><span data-ttu-id="40848-216">匹配一次或多次（惰性匹配）：+?</span><span class="sxs-lookup"><span data-stu-id="40848-216">Match One or More Times (Lazy Match): +?</span></span>  
 <span data-ttu-id="40848-217">`+?` 量符匹配上一元素一次或多次，但次数尽可能少。</span><span class="sxs-lookup"><span data-stu-id="40848-217">The `+?` quantifier matches the preceding element one or more times, but as few times as possible.</span></span> <span data-ttu-id="40848-218">它是贪婪量符 `+` 对应的惰性量符。</span><span class="sxs-lookup"><span data-stu-id="40848-218">It is the lazy counterpart of the greedy quantifier `+`.</span></span>  
  
 <span data-ttu-id="40848-219">例如，正则表达式 `\b\w+?\b` 匹配由单词边界分隔的一个或多个字符。</span><span class="sxs-lookup"><span data-stu-id="40848-219">For example, the regular expression `\b\w+?\b` matches one or more characters separated by word boundaries.</span></span> <span data-ttu-id="40848-220">下面的示例说明此正则表达式。</span><span class="sxs-lookup"><span data-stu-id="40848-220">The following example illustrates this regular expression.</span></span>  
  
 [!code-csharp[RegularExpressions.Quantifiers#8](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#8)]
 [!code-vb[RegularExpressions.Quantifiers#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#8)]  
  
### <a name="match-zero-or-one-time-lazy-match-"></a><span data-ttu-id="40848-221">匹配零次或一次（惰性匹配）：??</span><span class="sxs-lookup"><span data-stu-id="40848-221">Match Zero or One Time (Lazy Match): ??</span></span>  
 <span data-ttu-id="40848-222">`??` 量符匹配上一元素零次或一次，但次数尽可能少。</span><span class="sxs-lookup"><span data-stu-id="40848-222">The `??` quantifier matches the preceding element zero or one time, but as few times as possible.</span></span> <span data-ttu-id="40848-223">它是贪婪量符 `?` 对应的惰性量符。</span><span class="sxs-lookup"><span data-stu-id="40848-223">It is the lazy counterpart of the greedy quantifier `?`.</span></span>  
  
 <span data-ttu-id="40848-224">例如，正则表达式 `^\s*(System.)??Console.Write(Line)??\(??` 尝试匹配字符串“Console.Write”或“Console.WriteLine”。</span><span class="sxs-lookup"><span data-stu-id="40848-224">For example, the regular expression `^\s*(System.)??Console.Write(Line)??\(??` attempts to match the strings "Console.Write" or "Console.WriteLine".</span></span> <span data-ttu-id="40848-225">字符串还可以在“Console”前面包含“System.”，</span><span class="sxs-lookup"><span data-stu-id="40848-225">The string can also include "System."</span></span> <span data-ttu-id="40848-226">并且可以后跟左括号。</span><span class="sxs-lookup"><span data-stu-id="40848-226">before "Console", and it can be followed by an opening parenthesis.</span></span> <span data-ttu-id="40848-227">字符串必须处于行的开头，不过前面可以是空格。</span><span class="sxs-lookup"><span data-stu-id="40848-227">The string must be at the beginning of a line, although it can be preceded by white space.</span></span> <span data-ttu-id="40848-228">下面的示例说明此正则表达式。</span><span class="sxs-lookup"><span data-stu-id="40848-228">The following example illustrates this regular expression.</span></span>  
  
 [!code-csharp[RegularExpressions.Quantifiers#9](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#9)]
 [!code-vb[RegularExpressions.Quantifiers#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#9)]  
  
 <span data-ttu-id="40848-229">正则表达式模式的定义如下表所示。</span><span class="sxs-lookup"><span data-stu-id="40848-229">The regular expression pattern is defined as shown in the following table.</span></span>  
  
|<span data-ttu-id="40848-230">模式</span><span class="sxs-lookup"><span data-stu-id="40848-230">Pattern</span></span>|<span data-ttu-id="40848-231">描述</span><span class="sxs-lookup"><span data-stu-id="40848-231">Description</span></span>|  
|-------------|-----------------|  
|`^`|<span data-ttu-id="40848-232">匹配输入流的开头。</span><span class="sxs-lookup"><span data-stu-id="40848-232">Match the start of the input stream.</span></span>|  
|`\s*`|<span data-ttu-id="40848-233">匹配零个或多个空白字符。</span><span class="sxs-lookup"><span data-stu-id="40848-233">Match zero or more white-space characters.</span></span>|  
|`(System.)??`|<span data-ttu-id="40848-234">匹配字符串“System.”的零个或一个匹配项。</span><span class="sxs-lookup"><span data-stu-id="40848-234">Match zero or one occurrence of the string "System.".</span></span>|  
|`Console.Write`|<span data-ttu-id="40848-235">匹配字符串“Console.Write”。</span><span class="sxs-lookup"><span data-stu-id="40848-235">Match the string "Console.Write".</span></span>|  
|`(Line)??`|<span data-ttu-id="40848-236">匹配字符串“Line”的零个或一个匹配项。</span><span class="sxs-lookup"><span data-stu-id="40848-236">Match zero or one occurrence of the string "Line".</span></span>|  
|`\(??`|<span data-ttu-id="40848-237">匹配左括号的零个或一个匹配项。</span><span class="sxs-lookup"><span data-stu-id="40848-237">Match zero or one occurrence of the opening parenthesis.</span></span>|  
  
### <a name="match-exactly-n-times-lazy-match-n"></a><span data-ttu-id="40848-238">恰好匹配 n 次（惰性匹配）：{n}?</span><span class="sxs-lookup"><span data-stu-id="40848-238">Match Exactly n Times (Lazy Match): {n}?</span></span>  
 <span data-ttu-id="40848-239">`{`n`}?` 限定符与前面的元素恰好匹配 `n` 次，其中 n 是任何整数 。</span><span class="sxs-lookup"><span data-stu-id="40848-239">The `{`*n*`}?` quantifier matches the preceding element exactly `n` times, where *n* is any integer.</span></span> <span data-ttu-id="40848-240">它是贪婪限定符 `{`n`}` 的惰性对应项。</span><span class="sxs-lookup"><span data-stu-id="40848-240">It is the lazy counterpart of the greedy quantifier `{`*n*`}`.</span></span>  
  
 <span data-ttu-id="40848-241">在下面的示例中，正则表达式 `\b(\w{3,}?\.){2}?\w{3,}?\b` 用于标识网站地址。</span><span class="sxs-lookup"><span data-stu-id="40848-241">In the following example, the regular expression `\b(\w{3,}?\.){2}?\w{3,}?\b` is used to identify a Web site address.</span></span> <span data-ttu-id="40848-242">请注意，它匹配“www.microsoft.com”和“msdn.microsoft.com”，但不匹配“mywebsite”或“mycompany.com”。</span><span class="sxs-lookup"><span data-stu-id="40848-242">Note that it matches "www.microsoft.com" and "msdn.microsoft.com", but does not match "mywebsite" or "mycompany.com".</span></span>  
  
 [!code-csharp[RegularExpressions.Quantifiers#10](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#10)]
 [!code-vb[RegularExpressions.Quantifiers#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#10)]  
  
 <span data-ttu-id="40848-243">正则表达式模式的定义如下表所示。</span><span class="sxs-lookup"><span data-stu-id="40848-243">The regular expression pattern is defined as shown in the following table.</span></span>  
  
|<span data-ttu-id="40848-244">模式</span><span class="sxs-lookup"><span data-stu-id="40848-244">Pattern</span></span>|<span data-ttu-id="40848-245">描述</span><span class="sxs-lookup"><span data-stu-id="40848-245">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="40848-246">在单词边界处开始。</span><span class="sxs-lookup"><span data-stu-id="40848-246">Start at a word boundary.</span></span>|  
|`(\w{3,}?\.)`|<span data-ttu-id="40848-247">匹配至少 3 个后跟一个点或句点字符的单词字符，但字符数尽可能少。</span><span class="sxs-lookup"><span data-stu-id="40848-247">Match at least 3 word characters, but as few characters as possible, followed by a dot or period character.</span></span> <span data-ttu-id="40848-248">这是第一个捕获组。</span><span class="sxs-lookup"><span data-stu-id="40848-248">This is the first capturing group.</span></span>|  
|`(\w{3,}?\.){2}?`|<span data-ttu-id="40848-249">匹配第一个组中的模式两次，但次数尽可能少。</span><span class="sxs-lookup"><span data-stu-id="40848-249">Match the pattern in the first group two times, but as few times as possible.</span></span>|  
|`\b`|<span data-ttu-id="40848-250">在单词边界处结束匹配。</span><span class="sxs-lookup"><span data-stu-id="40848-250">End the match on a word boundary.</span></span>|  
  
### <a name="match-at-least-n-times-lazy-match-n"></a><span data-ttu-id="40848-251">至少匹配 n 次（惰性匹配）：{n,}?</span><span class="sxs-lookup"><span data-stu-id="40848-251">Match at Least n Times (Lazy Match): {n,}?</span></span>  
 <span data-ttu-id="40848-252">`{`n`,}?` 限定符与前面的元素至少匹配 `n` 次，其中 n 是任何整数，但次数尽可能少 。</span><span class="sxs-lookup"><span data-stu-id="40848-252">The `{`*n*`,}?` quantifier matches the preceding element at least `n` times, where *n* is any integer, but as few times as possible.</span></span> <span data-ttu-id="40848-253">它是贪婪限定符 `{`n`,}` 的惰性对应项。</span><span class="sxs-lookup"><span data-stu-id="40848-253">It is the lazy counterpart of the greedy quantifier `{`*n*`,}`.</span></span>  
  
 <span data-ttu-id="40848-254">有关说明，请参阅上一部分中的 `{`n`}?` 限定符示例。</span><span class="sxs-lookup"><span data-stu-id="40848-254">See the example for the `{`*n*`}?` quantifier in the previous section for an illustration.</span></span> <span data-ttu-id="40848-255">该示例中的正则表达式使用 `{`n`,}` 限定符匹配包含后跟一个句点的至少三个字符的字符串。</span><span class="sxs-lookup"><span data-stu-id="40848-255">The regular expression in that example uses the `{`*n*`,}` quantifier to match a string that has at least three characters followed by a period.</span></span>  
  
### <a name="match-between-n-and-m-times-lazy-match-nm"></a><span data-ttu-id="40848-256">匹配 n 到 m 次（惰性匹配）：{n,m}?</span><span class="sxs-lookup"><span data-stu-id="40848-256">Match Between n and m Times (Lazy Match): {n,m}?</span></span>  
 <span data-ttu-id="40848-257">`{`n`,`m`}?` 限定符匹配上一元素 `n` 次到 `m` 次，其中 n 和 m 是整数，但次数尽可能少   。</span><span class="sxs-lookup"><span data-stu-id="40848-257">The `{`*n*`,`*m*`}?` quantifier matches the preceding element between `n` and `m` times, where *n* and *m* are integers, but as few times as possible.</span></span> <span data-ttu-id="40848-258">它是贪婪限定符 `{`n`,`m`}` 的惰性对应项 。</span><span class="sxs-lookup"><span data-stu-id="40848-258">It is the lazy counterpart of the greedy quantifier `{`*n*`,`*m*`}`.</span></span>  
  
 <span data-ttu-id="40848-259">在下面的示例中，正则表达式 `\b[A-Z](\w*?\s*?){1,10}[.!?]` 匹配包含一到十个单词的句子。</span><span class="sxs-lookup"><span data-stu-id="40848-259">In the following example, the regular expression `\b[A-Z](\w*?\s*?){1,10}[.!?]` matches sentences that contain between one and ten words.</span></span> <span data-ttu-id="40848-260">它可匹配输入字符串中的所有句子（除了包含 18 个单词的一个句子）。</span><span class="sxs-lookup"><span data-stu-id="40848-260">It matches all the sentences in the input string except for one sentence that contains 18 words.</span></span>  
  
 [!code-csharp[RegularExpressions.Quantifiers#12](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#12)]
 [!code-vb[RegularExpressions.Quantifiers#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#12)]  
  
 <span data-ttu-id="40848-261">正则表达式模式的定义如下表所示。</span><span class="sxs-lookup"><span data-stu-id="40848-261">The regular expression pattern is defined as shown in the following table.</span></span>  
  
|<span data-ttu-id="40848-262">模式</span><span class="sxs-lookup"><span data-stu-id="40848-262">Pattern</span></span>|<span data-ttu-id="40848-263">描述</span><span class="sxs-lookup"><span data-stu-id="40848-263">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="40848-264">在单词边界处开始。</span><span class="sxs-lookup"><span data-stu-id="40848-264">Start at a word boundary.</span></span>|  
|`[A-Z]`|<span data-ttu-id="40848-265">匹配从 A 到 Z 的大写字符。</span><span class="sxs-lookup"><span data-stu-id="40848-265">Match an uppercase character from A to Z.</span></span>|  
|`(\w*?\s*?)`|<span data-ttu-id="40848-266">匹配零个或多个后跟一个或多个空白字符的单词字符，但次数应尽可能少。</span><span class="sxs-lookup"><span data-stu-id="40848-266">Match zero or more word characters, followed by one or more white-space characters, but as few times as possible.</span></span> <span data-ttu-id="40848-267">这是第一个捕获组。</span><span class="sxs-lookup"><span data-stu-id="40848-267">This is the first capture group.</span></span>|  
|`{1,10}`|<span data-ttu-id="40848-268">与前面的模式匹配 1 到 10 次。</span><span class="sxs-lookup"><span data-stu-id="40848-268">Match the previous pattern between 1 and 10 times.</span></span>|  
|`[.!?]`|<span data-ttu-id="40848-269">匹配标点字符“.”、“!”或“?”中的任何一种。</span><span class="sxs-lookup"><span data-stu-id="40848-269">Match any one of the punctuation characters ".", "!", or "?".</span></span>|  
  
<a name="Greedy"></a>
## <a name="greedy-and-lazy-quantifiers"></a><span data-ttu-id="40848-270">贪婪与惰性限定符</span><span class="sxs-lookup"><span data-stu-id="40848-270">Greedy and Lazy Quantifiers</span></span>  
 <span data-ttu-id="40848-271">一些限定符具有两个版本：</span><span class="sxs-lookup"><span data-stu-id="40848-271">A number of the quantifiers have two versions:</span></span>  
  
- <span data-ttu-id="40848-272">贪婪版本。</span><span class="sxs-lookup"><span data-stu-id="40848-272">A greedy version.</span></span>  
  
     <span data-ttu-id="40848-273">贪婪限定符尝试尽可能多地匹配元素。</span><span class="sxs-lookup"><span data-stu-id="40848-273">A greedy quantifier tries to match an element as many times as possible.</span></span>  
  
- <span data-ttu-id="40848-274">非贪婪（或惰性）版本。</span><span class="sxs-lookup"><span data-stu-id="40848-274">A non-greedy (or lazy) version.</span></span>  
  
     <span data-ttu-id="40848-275">非贪婪限定符尝试尽可能少地匹配元素。</span><span class="sxs-lookup"><span data-stu-id="40848-275">A non-greedy quantifier tries to match an element as few times as possible.</span></span> <span data-ttu-id="40848-276">只需添加 `?`，即可将贪婪量符转换为惰性量符。</span><span class="sxs-lookup"><span data-stu-id="40848-276">You can turn a greedy quantifier into a lazy quantifier by simply adding a `?`.</span></span>  
  
 <span data-ttu-id="40848-277">请考虑一个简单的正则表达式，它旨在从数字字符串（如信用卡号）中提取最后四位数。</span><span class="sxs-lookup"><span data-stu-id="40848-277">Consider a simple regular expression that is intended to extract the last four digits from a string of numbers such as a credit card number.</span></span> <span data-ttu-id="40848-278">使用 `*`贪婪量符的正则表达式版本是 `\b.*([0-9]{4})\b`。</span><span class="sxs-lookup"><span data-stu-id="40848-278">The version of the regular expression that uses the `*` greedy quantifier is `\b.*([0-9]{4})\b`.</span></span> <span data-ttu-id="40848-279">但是，如果字符串包含两个数字，则此正则表达式仅匹配第二个数字的最后四位数，如下面的示例所示。</span><span class="sxs-lookup"><span data-stu-id="40848-279">However, if a string contains two numbers, this regular expression matches the last four digits of the second number only, as the following example shows.</span></span>  
  
 [!code-csharp[RegularExpressions.Quantifiers.Greedy#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers.Greedy/cs/Greedy.cs#1)]
 [!code-vb[RegularExpressions.Quantifiers.Greedy#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers.Greedy/vb/Greedy.vb#1)]  
  
 <span data-ttu-id="40848-280">正则表达式无法匹配第一个数字，因为 `*` 量符尝试在整个字符串中尽可能多地匹配上一元素，所以它会在字符串末尾找到匹配。</span><span class="sxs-lookup"><span data-stu-id="40848-280">The regular expression fails to match the first number because the `*` quantifier tries to match the previous element as many times as possible in the entire string, and so it finds its match at the end of the string.</span></span>  
  
 <span data-ttu-id="40848-281">这不是所需行为。</span><span class="sxs-lookup"><span data-stu-id="40848-281">This is not the desired behavior.</span></span> <span data-ttu-id="40848-282">相反，可以使用 `*?` 惰性量符，从这两个数字提取数字，如下面的示例所示。</span><span class="sxs-lookup"><span data-stu-id="40848-282">Instead, you can use the `*?`lazy quantifier to extract digits from both numbers, as the following example shows.</span></span>  
  
 [!code-csharp[RegularExpressions.Quantifiers.Greedy#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers.Greedy/cs/Greedy.cs#2)]
 [!code-vb[RegularExpressions.Quantifiers.Greedy#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers.Greedy/vb/Greedy.vb#2)]  
  
 <span data-ttu-id="40848-283">在大多数情况下，具有贪婪和惰性限定符的正则表达式返回相同匹配项。</span><span class="sxs-lookup"><span data-stu-id="40848-283">In most cases, regular expressions with greedy and lazy quantifiers return the same matches.</span></span> <span data-ttu-id="40848-284">与匹配任何字符的通配符 (`.`) 元字符一起使用时，它们通常会返回不同的结果。</span><span class="sxs-lookup"><span data-stu-id="40848-284">They most commonly return different results when they are used with the wildcard (`.`) metacharacter, which matches any character.</span></span>  
  
## <a name="quantifiers-and-empty-matches"></a><span data-ttu-id="40848-285">限定符和空匹配项</span><span class="sxs-lookup"><span data-stu-id="40848-285">Quantifiers and Empty Matches</span></span>  
 <span data-ttu-id="40848-286">如果已找到最小捕获数，限定符 `*`、`+` 和 `{`n`,`m`}` 及对应的惰性限定符绝不会在空匹配项后重复 。</span><span class="sxs-lookup"><span data-stu-id="40848-286">The quantifiers `*`, `+`, and `{`*n*`,`*m*`}` and their lazy counterparts never repeat after an empty match when the minimum number of captures has been found.</span></span> <span data-ttu-id="40848-287">此规则会在最大可能组捕获数是无限或接近无限时，阻止限定符在空的子表达式匹配项上进入无限循环。</span><span class="sxs-lookup"><span data-stu-id="40848-287">This rule prevents quantifiers from entering infinite loops on empty subexpression matches when the maximum number of possible group captures is infinite or near infinite.</span></span>  
  
 <span data-ttu-id="40848-288">例如，下面的代码展示了使用正则表达式模式 `(a?)*`（匹配零个或一个“a”字符零次或多次）调用 <xref:System.Text.RegularExpressions.Regex.Match%2A?displayProperty=nameWithType> 方法的结果。</span><span class="sxs-lookup"><span data-stu-id="40848-288">For example, the following code shows the result of a call to the <xref:System.Text.RegularExpressions.Regex.Match%2A?displayProperty=nameWithType> method with the regular expression pattern `(a?)*`, which matches zero or one "a" character zero or more times.</span></span> <span data-ttu-id="40848-289">请注意，一个捕获组捕获所有“a”以及 <xref:System.String.Empty?displayProperty=nameWithType>，但没有第二个空匹配，因为第一个空匹配导致量符停止重复运行。</span><span class="sxs-lookup"><span data-stu-id="40848-289">Note that the single capturing group captures each "a" as well as <xref:System.String.Empty?displayProperty=nameWithType>, but that there is no second empty match, because the first empty match causes the quantifier to stop repeating.</span></span>  
  
 [!code-csharp[RegularExpressions.Quantifiers.EmptyMatch#1](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.quantifiers.emptymatch/cs/emptymatch1.cs#1)]
 [!code-vb[RegularExpressions.Quantifiers.EmptyMatch#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.quantifiers.emptymatch/vb/emptymatch1.vb#1)]  
  
 <span data-ttu-id="40848-290">若要查看定义最小和最大捕获数的捕获组与定义固定捕获数的捕获组之间的实际差异，请考虑正则表达式模式 `(a\1|(?(1)\1)){0,2}` 和 `(a\1|(?(1)\1)){2}`。</span><span class="sxs-lookup"><span data-stu-id="40848-290">To see the practical difference between a capturing group that defines a minimum and a maximum number of captures and one that defines a fixed number of captures, consider the regular expression patterns `(a\1|(?(1)\1)){0,2}` and `(a\1|(?(1)\1)){2}`.</span></span> <span data-ttu-id="40848-291">这两个正则表达式包含单个捕获组，其定义如下表所示。</span><span class="sxs-lookup"><span data-stu-id="40848-291">Both regular expressions consist of a single capturing group, which is defined as shown in the following table.</span></span>  
  
|<span data-ttu-id="40848-292">模式</span><span class="sxs-lookup"><span data-stu-id="40848-292">Pattern</span></span>|<span data-ttu-id="40848-293">描述</span><span class="sxs-lookup"><span data-stu-id="40848-293">Description</span></span>|  
|-------------|-----------------|  
|`(a\1`|<span data-ttu-id="40848-294">匹配“a”以及第一个捕获组的值...</span><span class="sxs-lookup"><span data-stu-id="40848-294">Either match "a" along with the value of the first captured group …</span></span>|  
|<code>&#124;(?(1)</code>|<span data-ttu-id="40848-295">…</span><span class="sxs-lookup"><span data-stu-id="40848-295">…</span></span> <span data-ttu-id="40848-296">或测试是否定义了第一个捕获组。</span><span class="sxs-lookup"><span data-stu-id="40848-296">or test whether the first captured group has been defined.</span></span> <span data-ttu-id="40848-297">（请注意，`(?(1)` 构造不定义捕获组。）</span><span class="sxs-lookup"><span data-stu-id="40848-297">(Note that the `(?(1)` construct does not define a capturing group.)</span></span>|  
|`\1))`|<span data-ttu-id="40848-298">如果第一个捕获组存在，则匹配其值。</span><span class="sxs-lookup"><span data-stu-id="40848-298">If the first captured group exists, match its value.</span></span> <span data-ttu-id="40848-299">如果组不存在，组会匹配 <xref:System.String.Empty?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="40848-299">If the group does not exist, the group will match <xref:System.String.Empty?displayProperty=nameWithType>.</span></span>|  
  
 <span data-ttu-id="40848-300">第一个正则表达式尝试与此模式匹配零到二次；第二个正则表达式尝试恰好匹配两次。</span><span class="sxs-lookup"><span data-stu-id="40848-300">The first regular expression tries to match this pattern between zero and two times; the second, exactly two times.</span></span> <span data-ttu-id="40848-301">由于第一个模式在首次捕获 <xref:System.String.Empty?displayProperty=nameWithType> 时达到最小捕获数，因此它绝不会重复尝试匹配 `a\1`；`{0,2}` 量符仅允许在最后一个迭代中有空匹配。</span><span class="sxs-lookup"><span data-stu-id="40848-301">Because the first pattern reaches its minimum number of captures with its first capture of <xref:System.String.Empty?displayProperty=nameWithType>, it never repeats to try to match `a\1`; the `{0,2}` quantifier allows only empty matches in the last iteration.</span></span> <span data-ttu-id="40848-302">相反，第二个正则表达式匹配“a”，因为它会第二次计算 `a\1`；最小迭代数 2 会强制引擎在空匹配项后面重复。</span><span class="sxs-lookup"><span data-stu-id="40848-302">In contrast, the second regular expression does match "a" because it evaluates `a\1` a second time; the minimum number of iterations, 2, forces the engine to repeat after an empty match.</span></span>  
  
 [!code-csharp[RegularExpressions.Quantifiers.EmptyMatch#2](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.quantifiers.emptymatch/cs/emptymatch4.cs#2)]
 [!code-vb[RegularExpressions.Quantifiers.EmptyMatch#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.quantifiers.emptymatch/vb/emptymatch4.vb#2)]  
  
## <a name="see-also"></a><span data-ttu-id="40848-303">请参阅</span><span class="sxs-lookup"><span data-stu-id="40848-303">See also</span></span>

- [<span data-ttu-id="40848-304">正则表达式语言 - 快速参考</span><span class="sxs-lookup"><span data-stu-id="40848-304">Regular Expression Language - Quick Reference</span></span>](regular-expression-language-quick-reference.md)
- [<span data-ttu-id="40848-305">回溯</span><span class="sxs-lookup"><span data-stu-id="40848-305">Backtracking</span></span>](backtracking-in-regular-expressions.md)
