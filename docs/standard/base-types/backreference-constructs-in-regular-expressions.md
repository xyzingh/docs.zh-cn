---
title: .NET 正则表达式中的反向引用构造
description: 了解如何通过在正则表达式中使用向后引用构造来识别重复的文本元素。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- backreferences
- constructs, backreference
- .NET regular expressions, backreference constructs
- regular expressions, backreference constructs
ms.assetid: 567a4b8d-0e79-49dc-8df9-f4b1aa376a2a
ms.openlocfilehash: bc0c6d3dcaa084c168a9c3fc0239116ec8899aae
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889148"
---
# <a name="backreference-constructs-in-regular-expressions"></a><span data-ttu-id="6d841-103">正则表达式中的反向引用构造</span><span class="sxs-lookup"><span data-stu-id="6d841-103">Backreference Constructs in Regular Expressions</span></span>

<span data-ttu-id="6d841-104">反向引用提供了标识字符串中的重复字符或子字符串的方便途径。</span><span class="sxs-lookup"><span data-stu-id="6d841-104">Backreferences provide a convenient way to identify a repeated character or substring within a string.</span></span> <span data-ttu-id="6d841-105">例如，如果输入字符串包含某任意子字符串的多个匹配项，可以使用捕获组匹配第一个出现的子字符串，然后使用反向引用匹配后面出现的子字符串。</span><span class="sxs-lookup"><span data-stu-id="6d841-105">For example, if the input string contains multiple occurrences of an arbitrary substring, you can match the first occurrence with a capturing group, and then use a backreference to match subsequent occurrences of the substring.</span></span>

> [!NOTE]
> <span data-ttu-id="6d841-106">单独语法用于引用替换字符串中命名的和带编号的捕获组。</span><span class="sxs-lookup"><span data-stu-id="6d841-106">A separate syntax is used to refer to named and numbered capturing groups in replacement strings.</span></span> <span data-ttu-id="6d841-107">有关更多信息，请参见 [替代](substitutions-in-regular-expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="6d841-107">For more information, see [Substitutions](substitutions-in-regular-expressions.md).</span></span>

<span data-ttu-id="6d841-108">.NET 定义引用编号和命名捕获组的单独语言元素。</span><span class="sxs-lookup"><span data-stu-id="6d841-108">.NET defines separate language elements to refer to numbered and named capturing groups.</span></span> <span data-ttu-id="6d841-109">若要详细了解捕获组，请参阅[分组构造](grouping-constructs-in-regular-expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="6d841-109">For more information about capturing groups, see [Grouping Constructs](grouping-constructs-in-regular-expressions.md).</span></span>

## <a name="numbered-backreferences"></a><span data-ttu-id="6d841-110">带编号的反向引用</span><span class="sxs-lookup"><span data-stu-id="6d841-110">Numbered Backreferences</span></span>

<span data-ttu-id="6d841-111">带编号的反向引用使用以下语法：</span><span class="sxs-lookup"><span data-stu-id="6d841-111">A numbered backreference uses the following syntax:</span></span>

<span data-ttu-id="6d841-112">`\` *number*</span><span class="sxs-lookup"><span data-stu-id="6d841-112">`\` *number*</span></span>

<span data-ttu-id="6d841-113">其中 *number* 是正则表达式中捕获组的序号位置。</span><span class="sxs-lookup"><span data-stu-id="6d841-113">where *number* is the ordinal position of the capturing group in the regular expression.</span></span> <span data-ttu-id="6d841-114">例如，`\4` 匹配第四个捕获组的内容。</span><span class="sxs-lookup"><span data-stu-id="6d841-114">For example, `\4` matches the contents of the fourth capturing group.</span></span> <span data-ttu-id="6d841-115">如果正则表达式模式中未定义 number  ，将会发生分析错误，并且正则表达式引擎会抛出 <xref:System.ArgumentException>。</span><span class="sxs-lookup"><span data-stu-id="6d841-115">If *number* is not defined in the regular expression pattern, a parsing error occurs, and the regular expression engine throws an <xref:System.ArgumentException>.</span></span> <span data-ttu-id="6d841-116">例如，正则表达式 `\b(\w+)\s\1` 有效，因为 `(\w+)` 是表达式中的第一个也是唯一一个捕获组。</span><span class="sxs-lookup"><span data-stu-id="6d841-116">For example, the regular expression `\b(\w+)\s\1` is valid, because `(\w+)` is the first and only capturing group in the expression.</span></span> <span data-ttu-id="6d841-117">`\b(\w+)\s\2` 无效，该表达式会因为没有捕获组编号 `\2` 而引发自变量异常。</span><span class="sxs-lookup"><span data-stu-id="6d841-117">On the other hand, `\b(\w+)\s\2` is invalid and throws an argument exception, because there is no capturing group numbered `\2`.</span></span> <span data-ttu-id="6d841-118">此外，如果 number 标识特定序号位置中的捕获组，但该捕获组已被分配了一个不同于其序号位置的数字名称，则正则表达式分析器还会引发 <xref:System.ArgumentException>。</span><span class="sxs-lookup"><span data-stu-id="6d841-118">In addition, if *number* identifies a capturing group in a particular ordinal position, but that capturing group has been assigned a numeric name different than its ordinal position, the regular expression parser also throws an <xref:System.ArgumentException>.</span></span>

<span data-ttu-id="6d841-119">请注意八进制转义代码（如 `\16`）和使用相同表示法的 `\`number  反向引用之间的不明确问题。</span><span class="sxs-lookup"><span data-stu-id="6d841-119">Note the ambiguity between octal escape codes (such as `\16`) and `\`*number* backreferences that use the same notation.</span></span> <span data-ttu-id="6d841-120">这种多义性可通过如下方式解决：</span><span class="sxs-lookup"><span data-stu-id="6d841-120">This ambiguity is resolved as follows:</span></span>

- <span data-ttu-id="6d841-121">表达式 `\1` 到 `\9` 始终解释为反向应用，而不是八进制代码。</span><span class="sxs-lookup"><span data-stu-id="6d841-121">The expressions `\1` through `\9` are always interpreted as backreferences, and not as octal codes.</span></span>

- <span data-ttu-id="6d841-122">如果多位表达式的第一个数字是 8 或 9（如 `\80` 或 `\91`），该表达式将解释为文本。</span><span class="sxs-lookup"><span data-stu-id="6d841-122">If the first digit of a multidigit expression is 8 or 9 (such as `\80` or `\91`), the expression as interpreted as a literal.</span></span>

- <span data-ttu-id="6d841-123">对于编号为 `\10` 或更大值的表达式，如果存在与该编号对应的反向引用，则将该表达式视为反向引用；否则，将这些表达式解释为八进制代码。</span><span class="sxs-lookup"><span data-stu-id="6d841-123">Expressions from `\10` and greater are considered backreferences if there is a backreference corresponding to that number; otherwise, they are interpreted as octal codes.</span></span>

- <span data-ttu-id="6d841-124">如果正则表达式包含对未定义的组成员的反向引用，将会发生分析错误，并且正则表达式引擎会抛出 <xref:System.ArgumentException>。</span><span class="sxs-lookup"><span data-stu-id="6d841-124">If a regular expression contains a backreference to an undefined group number, a parsing error occurs, and the regular expression engine throws an <xref:System.ArgumentException>.</span></span>

<span data-ttu-id="6d841-125">如果存在不明确问题，可以使用 `\k<`name  `>` 表示法，此表示法非常明确，不会与八进制字符代码混淆。</span><span class="sxs-lookup"><span data-stu-id="6d841-125">If the ambiguity is a problem, you can use the `\k<`*name*`>` notation, which is unambiguous and cannot be confused with octal character codes.</span></span> <span data-ttu-id="6d841-126">同样，诸如 `\xdd` 的十六进制代码也是明确的，不会与反向引用混淆。</span><span class="sxs-lookup"><span data-stu-id="6d841-126">Similarly, hexadecimal codes such as `\xdd` are unambiguous and cannot be confused with backreferences.</span></span>

<span data-ttu-id="6d841-127">下面的示例查找字符串中双写的单词字符。</span><span class="sxs-lookup"><span data-stu-id="6d841-127">The following example finds doubled word characters in a string.</span></span> <span data-ttu-id="6d841-128">它定义一个由下列元素组成的正则表达式 `(\w)\1`。</span><span class="sxs-lookup"><span data-stu-id="6d841-128">It defines a regular expression, `(\w)\1`, which consists of the following elements.</span></span>

|<span data-ttu-id="6d841-129">元素</span><span class="sxs-lookup"><span data-stu-id="6d841-129">Element</span></span>|<span data-ttu-id="6d841-130">说明</span><span class="sxs-lookup"><span data-stu-id="6d841-130">Description</span></span>|
|-------------|-----------------|
|`(\w)`|<span data-ttu-id="6d841-131">匹配单词字符，并将其分配给第一个捕获组。</span><span class="sxs-lookup"><span data-stu-id="6d841-131">Match a word character and assign it to the first capturing group.</span></span>|
|`\1`|<span data-ttu-id="6d841-132">匹配值与第一捕获组相同的下一个字符。</span><span class="sxs-lookup"><span data-stu-id="6d841-132">Match the next character that is the same as the value of the first capturing group.</span></span>|

[!code-csharp[RegularExpressions.Language.Backreferences#1](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference1.cs#1)]
[!code-vb[RegularExpressions.Language.Backreferences#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference1.vb#1)]

## <a name="named-backreferences"></a><span data-ttu-id="6d841-133">命名的反向引用</span><span class="sxs-lookup"><span data-stu-id="6d841-133">Named Backreferences</span></span>

<span data-ttu-id="6d841-134">使用以下语法定义命名的反向引用：</span><span class="sxs-lookup"><span data-stu-id="6d841-134">A named backreference is defined by using the following syntax:</span></span>

<span data-ttu-id="6d841-135">`\k<` *name* `>`</span><span class="sxs-lookup"><span data-stu-id="6d841-135">`\k<` *name* `>`</span></span>

<span data-ttu-id="6d841-136">或：</span><span class="sxs-lookup"><span data-stu-id="6d841-136">or:</span></span>

<span data-ttu-id="6d841-137">`\k'` *name* `'`</span><span class="sxs-lookup"><span data-stu-id="6d841-137">`\k'` *name* `'`</span></span>

<span data-ttu-id="6d841-138">其中， *name* 是正则表达式模式中定义的捕获组的名称。</span><span class="sxs-lookup"><span data-stu-id="6d841-138">where *name* is the name of a capturing group defined in the regular expression pattern.</span></span> <span data-ttu-id="6d841-139">如果正则表达式模式中未定义 name  ，将会发生分析错误，并且正则表达式引擎会抛出 <xref:System.ArgumentException>。</span><span class="sxs-lookup"><span data-stu-id="6d841-139">If *name* is not defined in the regular expression pattern, a parsing error occurs, and the regular expression engine throws an <xref:System.ArgumentException>.</span></span>

<span data-ttu-id="6d841-140">下面的示例查找字符串中双写的单词字符。</span><span class="sxs-lookup"><span data-stu-id="6d841-140">The following example finds doubled word characters in a string.</span></span> <span data-ttu-id="6d841-141">它定义一个由下列元素组成的正则表达式 `(?<char>\w)\k<char>`。</span><span class="sxs-lookup"><span data-stu-id="6d841-141">It defines a regular expression, `(?<char>\w)\k<char>`, which consists of the following elements.</span></span>

|<span data-ttu-id="6d841-142">元素</span><span class="sxs-lookup"><span data-stu-id="6d841-142">Element</span></span>|<span data-ttu-id="6d841-143">说明</span><span class="sxs-lookup"><span data-stu-id="6d841-143">Description</span></span>|
|-------------|-----------------|
|`(?<char>\w)`|<span data-ttu-id="6d841-144">匹配字词字符，并将结果分配到 `char` 捕获组。</span><span class="sxs-lookup"><span data-stu-id="6d841-144">Match a word character and assign it to a capturing group named `char`.</span></span>|
|`\k<char>`|<span data-ttu-id="6d841-145">匹配下一个与 `char` 捕获组的值相同的字符。</span><span class="sxs-lookup"><span data-stu-id="6d841-145">Match the next character that is the same as the value of the `char` capturing group.</span></span>|

[!code-csharp[RegularExpressions.Language.Backreferences#2](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference2.cs#2)]
[!code-vb[RegularExpressions.Language.Backreferences#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference2.vb#2)]

## <a name="named-numeric-backreferences"></a><span data-ttu-id="6d841-146">已命名数值的反向引用</span><span class="sxs-lookup"><span data-stu-id="6d841-146">Named numeric backreferences</span></span>

<span data-ttu-id="6d841-147">在具有 `\k` 的已命名反向引用中，name 也可以是 number 的字符串表示形式  。</span><span class="sxs-lookup"><span data-stu-id="6d841-147">In a named backreference with `\k`, *name* can also be the string representation of a number.</span></span> <span data-ttu-id="6d841-148">例如，下面的示例使用正则表达式 `(?<2>\w)\k<2>` 查找字符串中双写的单词字符。</span><span class="sxs-lookup"><span data-stu-id="6d841-148">For example, the following example uses the regular expression `(?<2>\w)\k<2>` to find doubled word characters in a string.</span></span> <span data-ttu-id="6d841-149">在此情况下，该示例定义了显式命名为“2”的捕获组，反向引用相应地命名为“2”。</span><span class="sxs-lookup"><span data-stu-id="6d841-149">In this case, the example defines a capturing group that is explicitly named "2", and the backreference is correspondingly named "2".</span></span>

[!code-csharp[RegularExpressions.Language.Backreferences#3](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference3.cs#3)]
[!code-vb[RegularExpressions.Language.Backreferences#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference3.vb#3)]

<span data-ttu-id="6d841-150">如果 name 是 number 的字符串表示形式，且没有捕获组具有该名称，`\k<` name `>` 与反向引用 `\`number 相同，其中 number 是捕获的序号位置。</span><span class="sxs-lookup"><span data-stu-id="6d841-150">If *name* is the string representation of a number, and no capturing group has that name, `\k<`*name*`>` is the same as the backreference `\`*number* , where *number* is the ordinal position of the capture.</span></span> <span data-ttu-id="6d841-151">在以下示例中，有名为 `char` 的单个捕获组。</span><span class="sxs-lookup"><span data-stu-id="6d841-151">In the following example, there is a single capturing group named `char`.</span></span> <span data-ttu-id="6d841-152">反向引用构造将其称为 `\k<1>`。</span><span class="sxs-lookup"><span data-stu-id="6d841-152">The backreference construct refers to it as `\k<1>`.</span></span> <span data-ttu-id="6d841-153">正如示例中的输出所示，由于 `char` 是第一个捕获组，所以对 <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> 的调用成功。</span><span class="sxs-lookup"><span data-stu-id="6d841-153">As the output from the example shows, the call to the <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> succeeds because `char` is the first capturing group.</span></span>

[!code-csharp[Ordinal.Backreference](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference6.cs)]
[!code-vb[Ordinal.BackReference](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference6.vb)]

<span data-ttu-id="6d841-154">但是，如果 name 是 number 的字符串表示形式，并且已向该位置中的捕获组明确分配了数字名称，正则表达式分析器无法通过其序号位置识别捕获组  。</span><span class="sxs-lookup"><span data-stu-id="6d841-154">However, if *name* is the string representation of a number and the capturing group in that position has been explicitly assigned a numeric name, the regular expression parser cannot identify the capturing group by its ordinal position.</span></span> <span data-ttu-id="6d841-155">相反，它会引发 <xref:System.ArgumentException>。</span><span class="sxs-lookup"><span data-stu-id="6d841-155">Instead, it throws an <xref:System.ArgumentException>.</span></span> <span data-ttu-id="6d841-156">以下示例中的唯一捕获组名为“2”。</span><span class="sxs-lookup"><span data-stu-id="6d841-156">The only capturing group in the following example is named "2".</span></span> <span data-ttu-id="6d841-157">由于 `\k` 结构用于定义名为“1”的反向引用，因此正则表达式分析器无法识别第一个捕获组并引发异常。</span><span class="sxs-lookup"><span data-stu-id="6d841-157">Because the `\k` construct is used to define a backreference named "1", the regular expression parser is unable to identify the first capturing group and throws an exception.</span></span>

[!code-csharp[Ordinal.Backreference](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference7.cs)]
[!code-vb[Ordinal.BackReference](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference7.vb)]

## <a name="what-backreferences-match"></a><span data-ttu-id="6d841-158">反向引用匹配什么内容</span><span class="sxs-lookup"><span data-stu-id="6d841-158">What Backreferences Match</span></span>

<span data-ttu-id="6d841-159">反向引用引用组的最新定义（从左向右匹配时，最靠近左侧的定义）。</span><span class="sxs-lookup"><span data-stu-id="6d841-159">A backreference refers to the most recent definition of a group (the definition most immediately to the left, when matching left to right).</span></span> <span data-ttu-id="6d841-160">当组建立多个捕获时，反向引用会引用最新的捕获。</span><span class="sxs-lookup"><span data-stu-id="6d841-160">When a group makes multiple captures, a backreference refers to the most recent capture.</span></span>

<span data-ttu-id="6d841-161">下面的示例包含正则表达式模式 `(?<1>a)(?<1>\1b)*`，该模式重新定义 \1 命名组。</span><span class="sxs-lookup"><span data-stu-id="6d841-161">The following example includes a regular expression pattern, `(?<1>a)(?<1>\1b)*`, which redefines the \1 named group.</span></span> <span data-ttu-id="6d841-162">下表描述了正则表达式中的每个模式。</span><span class="sxs-lookup"><span data-stu-id="6d841-162">The following table describes each pattern in the regular expression.</span></span>

|<span data-ttu-id="6d841-163">模式</span><span class="sxs-lookup"><span data-stu-id="6d841-163">Pattern</span></span>|<span data-ttu-id="6d841-164">说明</span><span class="sxs-lookup"><span data-stu-id="6d841-164">Description</span></span>|
|-------------|-----------------|
|`(?<1>a)`|<span data-ttu-id="6d841-165">匹配字符“a”，并将结果分配到 `1` 捕获组。</span><span class="sxs-lookup"><span data-stu-id="6d841-165">Match the character "a" and assign the result to the capturing group named `1`.</span></span>|
|`(?<1>\1b)*`|<span data-ttu-id="6d841-166">匹配 `1` 组的 0 更大发生次数以及“b”，并将结果分配到 `1` 捕获组。</span><span class="sxs-lookup"><span data-stu-id="6d841-166">Match zero or more occurrences of the group named `1` along with a "b", and assign the result to the capturing group named `1`.</span></span>|

[!code-csharp[RegularExpressions.Language.Backreferences#4](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference4.cs#4)]
[!code-vb[RegularExpressions.Language.Backreferences#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference4.vb#4)]

<span data-ttu-id="6d841-167">在比较正则表达式与输入字符串（“aababb”）时，正则表达式引擎执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="6d841-167">In comparing the regular expression with the input string ("aababb"), the regular expression engine performs the following operations:</span></span>

1. <span data-ttu-id="6d841-168">从该字符串的开头开始，成功将“a”与表达式 `(?<1>a)` 匹配。</span><span class="sxs-lookup"><span data-stu-id="6d841-168">It starts at the beginning of the string, and successfully matches "a" with the expression `(?<1>a)`.</span></span> <span data-ttu-id="6d841-169">此时，`1` 组的值为“a”。</span><span class="sxs-lookup"><span data-stu-id="6d841-169">The value of the `1` group is now "a".</span></span>

2. <span data-ttu-id="6d841-170">继续匹配第二个字符，成功将字符串“ab”与表达式 `\1b` 或“ab”匹配。</span><span class="sxs-lookup"><span data-stu-id="6d841-170">It advances to the second character, and successfully matches the string "ab" with the expression `\1b`, or "ab".</span></span> <span data-ttu-id="6d841-171">然后，将结果“ab”分配到 `\1`。</span><span class="sxs-lookup"><span data-stu-id="6d841-171">It then assigns the result, "ab" to `\1`.</span></span>

3. <span data-ttu-id="6d841-172">继续匹配第四个字符。</span><span class="sxs-lookup"><span data-stu-id="6d841-172">It advances to the fourth character.</span></span> <span data-ttu-id="6d841-173">表达式 `(?<1>\1b)*` 要匹配零次或多次，因此会成功将字符串“abb”与表达式 `\1b` 匹配。</span><span class="sxs-lookup"><span data-stu-id="6d841-173">The expression `(?<1>\1b)*` is to be matched zero or more times, so it successfully matches the string "abb" with the expression `\1b`.</span></span> <span data-ttu-id="6d841-174">然后，将结果“abb”分配回到 `\1`。</span><span class="sxs-lookup"><span data-stu-id="6d841-174">It assigns the result, "abb", back to `\1`.</span></span>

<span data-ttu-id="6d841-175">在本示例中，`*` 是循环限定符 -- 它将被重复计算，直到正则表达式引擎不能与它定义的模式匹配为止。</span><span class="sxs-lookup"><span data-stu-id="6d841-175">In this example, `*` is a looping quantifier -- it is evaluated repeatedly until the regular expression engine cannot match the pattern it defines.</span></span> <span data-ttu-id="6d841-176">循环限定符不会清除组定义。</span><span class="sxs-lookup"><span data-stu-id="6d841-176">Looping quantifiers do not clear group definitions.</span></span>

<span data-ttu-id="6d841-177">如果某个组尚未捕获任何子字符串，则对该组的反向引用是不确定的，永远不会匹配。</span><span class="sxs-lookup"><span data-stu-id="6d841-177">If a group has not captured any substrings, a backreference to that group is undefined and never matches.</span></span> <span data-ttu-id="6d841-178">下面展示了正则表达式模式 `\b(\p{Lu}{2})(\d{2})?(\p{Lu}{2})\b` 的定义：</span><span class="sxs-lookup"><span data-stu-id="6d841-178">This is illustrated by the regular expression pattern `\b(\p{Lu}{2})(\d{2})?(\p{Lu}{2})\b`, which is defined as follows:</span></span>

|<span data-ttu-id="6d841-179">模式</span><span class="sxs-lookup"><span data-stu-id="6d841-179">Pattern</span></span>|<span data-ttu-id="6d841-180">说明</span><span class="sxs-lookup"><span data-stu-id="6d841-180">Description</span></span>|
|-------------|-----------------|
|`\b`|<span data-ttu-id="6d841-181">在单词边界处开始匹配。</span><span class="sxs-lookup"><span data-stu-id="6d841-181">Begin the match on a word boundary.</span></span>|
|`(\p{Lu}{2})`|<span data-ttu-id="6d841-182">匹配两个大写字母。</span><span class="sxs-lookup"><span data-stu-id="6d841-182">Match two uppercase letters.</span></span> <span data-ttu-id="6d841-183">这是第一个捕获组。</span><span class="sxs-lookup"><span data-stu-id="6d841-183">This is the first capturing group.</span></span>|
|`(\d{2})?`|<span data-ttu-id="6d841-184">匹配两个十进制数的零个或一个匹配项。</span><span class="sxs-lookup"><span data-stu-id="6d841-184">Match zero or one occurrence of two decimal digits.</span></span> <span data-ttu-id="6d841-185">这是第二个捕获组。</span><span class="sxs-lookup"><span data-stu-id="6d841-185">This is the second capturing group.</span></span>|
|`(\p{Lu}{2})`|<span data-ttu-id="6d841-186">匹配两个大写字母。</span><span class="sxs-lookup"><span data-stu-id="6d841-186">Match two uppercase letters.</span></span> <span data-ttu-id="6d841-187">这是第三个捕获组。</span><span class="sxs-lookup"><span data-stu-id="6d841-187">This is the third capturing group.</span></span>|
|`\b`|<span data-ttu-id="6d841-188">在单词边界处结束匹配。</span><span class="sxs-lookup"><span data-stu-id="6d841-188">End the match on a word boundary.</span></span>|

<span data-ttu-id="6d841-189">输入字符串可以匹配此正则表达式，即使第二个捕获组定义的两个十进制数字都不存在。</span><span class="sxs-lookup"><span data-stu-id="6d841-189">An input string can match this regular expression even if the two decimal digits that are defined by the second capturing group are not present.</span></span> <span data-ttu-id="6d841-190">下面的示例显示了即使匹配成功，也仍会在两个成功的捕获组之间找到空捕获组。</span><span class="sxs-lookup"><span data-stu-id="6d841-190">The following example shows that even though the match is successful, an empty capturing group is found between two successful capturing groups.</span></span>

[!code-csharp[RegularExpressions.Language.Backreferences#5](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference5.cs#5)]
[!code-vb[RegularExpressions.Language.Backreferences#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference5.vb#5)]

## <a name="see-also"></a><span data-ttu-id="6d841-191">另请参阅</span><span class="sxs-lookup"><span data-stu-id="6d841-191">See also</span></span>

- [<span data-ttu-id="6d841-192">正则表达式语言 - 快速参考</span><span class="sxs-lookup"><span data-stu-id="6d841-192">Regular Expression Language - Quick Reference</span></span>](regular-expression-language-quick-reference.md)
