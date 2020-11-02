---
title: .NET 正则表达式中的字符转义
description: 了解 .NET 正则表达式中的特殊字符和转义字符。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- unescaped characters
- replacement patterns
- characters, escapes
- regular expressions, character escapes
- escape characters
- .NET regular expressions, character escapes
- constructs, character escapes
ms.assetid: f49cc9cc-db7d-4058-8b8a-422bc08b29b0
ms.openlocfilehash: 927fb32163a7b44561c19fdb35e38b488fc50fb7
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889512"
---
# <a name="character-escapes-in-regular-expressions"></a><span data-ttu-id="5cd22-103">正则表达式中的字符转义</span><span class="sxs-lookup"><span data-stu-id="5cd22-103">Character Escapes in Regular Expressions</span></span>
<span data-ttu-id="5cd22-104">正则表达式中的反斜杠 (\\) 指示以下值之一：</span><span class="sxs-lookup"><span data-stu-id="5cd22-104">The backslash (\\) in a regular expression indicates one of the following:</span></span>  
  
- <span data-ttu-id="5cd22-105">后接字符为特殊字符，如下节表中所示。</span><span class="sxs-lookup"><span data-stu-id="5cd22-105">The character that follows it is a special character, as shown in the table in the following section.</span></span> <span data-ttu-id="5cd22-106">例如，`\b` 是定位标记，用于指示正则表达式的匹配应从单词边界开始，`\t` 表示制表符，而 `\x020` 表示空格。</span><span class="sxs-lookup"><span data-stu-id="5cd22-106">For example, `\b` is an anchor that indicates that a regular expression match should begin on a word boundary, `\t` represents a tab, and `\x020` represents a space.</span></span>  
  
- <span data-ttu-id="5cd22-107">本应解释为未转义语言构造的字符应按字面意思进行解释。</span><span class="sxs-lookup"><span data-stu-id="5cd22-107">A character that otherwise would be interpreted as an unescaped language construct should be interpreted literally.</span></span> <span data-ttu-id="5cd22-108">例如，大括号 (`{`) 开始定义限定符，而反斜杠后接大括号 (`\{`) 表示正则表达式引擎应匹配大括号。</span><span class="sxs-lookup"><span data-stu-id="5cd22-108">For example, a brace (`{`) begins the definition of a quantifier, but a backslash followed by a brace (`\{`) indicates that the regular expression engine should match the brace.</span></span> <span data-ttu-id="5cd22-109">同样，单个反斜杠标记转义的语言构造的开始，而两个反斜杠 (`\\`) 表示正则表达式引擎应匹配反斜杠。</span><span class="sxs-lookup"><span data-stu-id="5cd22-109">Similarly, a single backslash marks the beginning of an escaped language construct, but two backslashes (`\\`) indicate that the regular expression engine should match the backslash.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="5cd22-110">字符转义可在正则表达式模式中识别，但无法在替换模式中识别。</span><span class="sxs-lookup"><span data-stu-id="5cd22-110">Character escapes are recognized in regular expression patterns but not in replacement patterns.</span></span>  
  
## <a name="character-escapes-in-net"></a><span data-ttu-id="5cd22-111">.NET 中的字符转义</span><span class="sxs-lookup"><span data-stu-id="5cd22-111">Character Escapes in .NET</span></span>  
 <span data-ttu-id="5cd22-112">下表列出了 .NET 中正则表达式支持的字符转义。</span><span class="sxs-lookup"><span data-stu-id="5cd22-112">The following table lists the character escapes supported by regular expressions in .NET.</span></span>  
  
|<span data-ttu-id="5cd22-113">字符或序列</span><span class="sxs-lookup"><span data-stu-id="5cd22-113">Character or sequence</span></span>|<span data-ttu-id="5cd22-114">描述</span><span class="sxs-lookup"><span data-stu-id="5cd22-114">Description</span></span>|  
|---------------------------|-----------------|  
|<span data-ttu-id="5cd22-115">除以下字符外的所有字符：</span><span class="sxs-lookup"><span data-stu-id="5cd22-115">All characters except for the following:</span></span><br /><br /> <span data-ttu-id="5cd22-116">。</span><span class="sxs-lookup"><span data-stu-id="5cd22-116">.</span></span> <span data-ttu-id="5cd22-117">$ ^ { [ ( &#124; ) \* + ?</span><span class="sxs-lookup"><span data-stu-id="5cd22-117">$ ^ { [ ( &#124; ) \* + ?</span></span> \ |<span data-ttu-id="5cd22-118">“字符或序列”  列中未包含的字符在正则表达式中没有特殊含义；此类字符与自身匹配。</span><span class="sxs-lookup"><span data-stu-id="5cd22-118">Characters other than those listed in the **Character or sequence** column have no special meaning in regular expressions; they match themselves.</span></span><br /><br /> <span data-ttu-id="5cd22-119">“字符或序列”  列中包括的字符均为特殊的正则表达式语言元素。</span><span class="sxs-lookup"><span data-stu-id="5cd22-119">The characters included in the **Character or sequence** column are special regular expression language elements.</span></span> <span data-ttu-id="5cd22-120">若要在正则表达式中匹配这些字符，必须将其转义或纳入[正字符组](character-classes-in-regular-expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="5cd22-120">To match them in a regular expression, they must be escaped or included in a [positive character group](character-classes-in-regular-expressions.md).</span></span> <span data-ttu-id="5cd22-121">例如，正则表达式 `\$\d+` 或 `[$]\d+` 匹配“$1200”。</span><span class="sxs-lookup"><span data-stu-id="5cd22-121">For example, the regular expression `\$\d+` or `[$]\d+` matches "$1200".</span></span>|  
|`\a`|<span data-ttu-id="5cd22-122">匹配响铃（警报）字符，`\u0007`。</span><span class="sxs-lookup"><span data-stu-id="5cd22-122">Matches a bell (alarm) character, `\u0007`.</span></span>|  
|`\b`|<span data-ttu-id="5cd22-123">在 `[`character_group  `]` 字符类中，匹配退格，`\u0008`。</span><span class="sxs-lookup"><span data-stu-id="5cd22-123">In a `[`*character_group*`]` character class, matches a backspace, `\u0008`.</span></span>  <span data-ttu-id="5cd22-124">（请参阅[字符类](character-classes-in-regular-expressions.md)。）在字符类之外，`\b` 是匹配字边界的定位点。</span><span class="sxs-lookup"><span data-stu-id="5cd22-124">(See [Character Classes](character-classes-in-regular-expressions.md).) Outside a character class, `\b` is an anchor that matches a word boundary.</span></span> <span data-ttu-id="5cd22-125">（请参阅[定位标记](anchors-in-regular-expressions.md)）</span><span class="sxs-lookup"><span data-stu-id="5cd22-125">(See [Anchors](anchors-in-regular-expressions.md).)</span></span>|  
|`\t`|<span data-ttu-id="5cd22-126">匹配制表符，`\u0009`。</span><span class="sxs-lookup"><span data-stu-id="5cd22-126">Matches a tab, `\u0009`.</span></span>|  
|`\r`|<span data-ttu-id="5cd22-127">匹配回车，`\u000D`。</span><span class="sxs-lookup"><span data-stu-id="5cd22-127">Matches a carriage return, `\u000D`.</span></span> <span data-ttu-id="5cd22-128">请注意，`\r` 不等同于换行符，`\n`。</span><span class="sxs-lookup"><span data-stu-id="5cd22-128">Note that `\r` is not equivalent to the newline character, `\n`.</span></span>|  
|`\v`|<span data-ttu-id="5cd22-129">匹配垂直制表符，`\u000B`。</span><span class="sxs-lookup"><span data-stu-id="5cd22-129">Matches a vertical tab, `\u000B`.</span></span>|  
|`\f`|<span data-ttu-id="5cd22-130">匹配换页，`\u000C`。</span><span class="sxs-lookup"><span data-stu-id="5cd22-130">Matches a form feed, `\u000C`.</span></span>|  
|`\n`|<span data-ttu-id="5cd22-131">匹配换行，`\u000A`。</span><span class="sxs-lookup"><span data-stu-id="5cd22-131">Matches a new line, `\u000A`.</span></span>|  
|`\e`|<span data-ttu-id="5cd22-132">匹配转义，`\u001B`。</span><span class="sxs-lookup"><span data-stu-id="5cd22-132">Matches an escape, `\u001B`.</span></span>|  
|<span data-ttu-id="5cd22-133">`\` *nnn*</span><span class="sxs-lookup"><span data-stu-id="5cd22-133">`\` *nnn*</span></span>|<span data-ttu-id="5cd22-134">匹配 ASCII 字符，其中 nnn  包含表示八进制字符代码的两位数或三位数。</span><span class="sxs-lookup"><span data-stu-id="5cd22-134">Matches an ASCII character, where *nnn* consists of two or three digits that represent the octal character code.</span></span> <span data-ttu-id="5cd22-135">例如，`\040` 表示空格字符。</span><span class="sxs-lookup"><span data-stu-id="5cd22-135">For example, `\040` represents a space character.</span></span> <span data-ttu-id="5cd22-136">如果此构造仅包含一个数字（如 `\2`）或者它对应捕获组的编号，则将它解释为向后引用。</span><span class="sxs-lookup"><span data-stu-id="5cd22-136">This construct is interpreted as a backreference if it has only one digit (for example, `\2`) or if it corresponds to the number of a capturing group.</span></span> <span data-ttu-id="5cd22-137">（请参阅[向后引用构造](backreference-constructs-in-regular-expressions.md)。）</span><span class="sxs-lookup"><span data-stu-id="5cd22-137">(See [Backreference Constructs](backreference-constructs-in-regular-expressions.md).)</span></span>|  
|<span data-ttu-id="5cd22-138">`\x` *nn*</span><span class="sxs-lookup"><span data-stu-id="5cd22-138">`\x` *nn*</span></span>|<span data-ttu-id="5cd22-139">匹配 ASCII 字符，其中 nn  是两位数的十六进制字符代码。</span><span class="sxs-lookup"><span data-stu-id="5cd22-139">Matches an ASCII character, where *nn* is a two-digit hexadecimal character code.</span></span>|  
|<span data-ttu-id="5cd22-140">`\c` *X*</span><span class="sxs-lookup"><span data-stu-id="5cd22-140">`\c` *X*</span></span>|<span data-ttu-id="5cd22-141">匹配 ASCII 控制字符，其中 X 是控制字符的字母。</span><span class="sxs-lookup"><span data-stu-id="5cd22-141">Matches an ASCII control character, where X is the letter of the control character.</span></span> <span data-ttu-id="5cd22-142">例如，`\cC` 为 CTRL-C。</span><span class="sxs-lookup"><span data-stu-id="5cd22-142">For example, `\cC` is CTRL-C.</span></span>|  
|<span data-ttu-id="5cd22-143">`\u` *nnnn*</span><span class="sxs-lookup"><span data-stu-id="5cd22-143">`\u` *nnnn*</span></span>|<span data-ttu-id="5cd22-144">匹配的 UTF-16 代码单元，单元值是 nnnn  十六进制。</span><span class="sxs-lookup"><span data-stu-id="5cd22-144">Matches a UTF-16 code unit whose value is *nnnn* hexadecimal.</span></span> <span data-ttu-id="5cd22-145">**注意：** .NET 不支持用于指定 Unicode 的 Perl 5 字符转义。</span><span class="sxs-lookup"><span data-stu-id="5cd22-145">**Note:**  The Perl 5 character escape that is used to specify Unicode is not supported by .NET.</span></span> <span data-ttu-id="5cd22-146">Perl 5 字符转义采用以下格式 `\x{`####  `…}`，其中 ####  `…` 是一系列十六进制数字。</span><span class="sxs-lookup"><span data-stu-id="5cd22-146">The Perl 5 character escape has the form `\x{`*####*`…}`, where *####*`…` is a series of hexadecimal digits.</span></span> <span data-ttu-id="5cd22-147">改用 `\u`nnnn  。</span><span class="sxs-lookup"><span data-stu-id="5cd22-147">Instead, use `\u`*nnnn* .</span></span>|  
|`\`|<span data-ttu-id="5cd22-148">后接字符未识别为转义字符时，将匹配此字符。</span><span class="sxs-lookup"><span data-stu-id="5cd22-148">When followed by a character that is not recognized as an escaped character, matches that character.</span></span> <span data-ttu-id="5cd22-149">例如，`\*` 匹配星号 (\*) 并等同于 `\x2A`。</span><span class="sxs-lookup"><span data-stu-id="5cd22-149">For example, `\*` matches an asterisk (\*) and is the same as `\x2A`.</span></span>|  
  
## <a name="an-example"></a><span data-ttu-id="5cd22-150">示例</span><span class="sxs-lookup"><span data-stu-id="5cd22-150">An Example</span></span>  
 <span data-ttu-id="5cd22-151">以下示例说明了如何使用正则表达式中的字符转义。</span><span class="sxs-lookup"><span data-stu-id="5cd22-151">The following example illustrates the use of character escapes in a regular expression.</span></span> <span data-ttu-id="5cd22-152">分析了包含 2009 年世界上最大城市的名称及其人口的字符串。</span><span class="sxs-lookup"><span data-stu-id="5cd22-152">It parses a string that contains the names of the world's largest cities and their populations in 2009.</span></span> <span data-ttu-id="5cd22-153">使用制表符 (`\t`) 或垂直条（&#124; 或 `\u007c`）将每个城市名与其人口数量分开。</span><span class="sxs-lookup"><span data-stu-id="5cd22-153">Each city name is separated from its population by a tab (`\t`) or a vertical bar (&#124; or `\u007c`).</span></span> <span data-ttu-id="5cd22-154">使用回车符和换行符分隔各个城市及其人口。</span><span class="sxs-lookup"><span data-stu-id="5cd22-154">Individual cities and their populations are separated from each other by a carriage return and line feed.</span></span>  
  
 [!code-csharp[RegularExpressions.Language.Escapes#1](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.escapes/cs/escape1.cs#1)]
 [!code-vb[RegularExpressions.Language.Escapes#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.escapes/vb/escape1.vb#1)]  
  
 <span data-ttu-id="5cd22-155">正则表达式 `\G(.+)[\t\u007c](.+)\r?\n` 可以解释为下表中所示内容。</span><span class="sxs-lookup"><span data-stu-id="5cd22-155">The regular expression `\G(.+)[\t\u007c](.+)\r?\n` is interpreted as shown in the following table.</span></span>  
  
|<span data-ttu-id="5cd22-156">模式</span><span class="sxs-lookup"><span data-stu-id="5cd22-156">Pattern</span></span>|<span data-ttu-id="5cd22-157">描述</span><span class="sxs-lookup"><span data-stu-id="5cd22-157">Description</span></span>|  
|-------------|-----------------|  
|`\G`|<span data-ttu-id="5cd22-158">从上次匹配结束处开始匹配。</span><span class="sxs-lookup"><span data-stu-id="5cd22-158">Begin the match where the last match ended.</span></span>|  
|`(.+)`|<span data-ttu-id="5cd22-159">一次或多次匹配任何字符。</span><span class="sxs-lookup"><span data-stu-id="5cd22-159">Match any character one or more times.</span></span> <span data-ttu-id="5cd22-160">这是第一个捕获组。</span><span class="sxs-lookup"><span data-stu-id="5cd22-160">This is the first capturing group.</span></span>|  
|`[\t\u007c]`|<span data-ttu-id="5cd22-161">匹配制表符 (`\t`) 或垂直条 (&#124;)。</span><span class="sxs-lookup"><span data-stu-id="5cd22-161">Match a tab (`\t`) or a vertical bar (&#124;).</span></span>|  
|`(.+)`|<span data-ttu-id="5cd22-162">一次或多次匹配任何字符。</span><span class="sxs-lookup"><span data-stu-id="5cd22-162">Match any character one or more times.</span></span> <span data-ttu-id="5cd22-163">这是第二个捕获组。</span><span class="sxs-lookup"><span data-stu-id="5cd22-163">This is the second capturing group.</span></span>|  
|`\r?\n`|<span data-ttu-id="5cd22-164">匹配零次或一次回车符后接新行的情况。</span><span class="sxs-lookup"><span data-stu-id="5cd22-164">Match zero or one occurrence of a carriage return followed by a new line.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="5cd22-165">请参阅</span><span class="sxs-lookup"><span data-stu-id="5cd22-165">See also</span></span>

- [<span data-ttu-id="5cd22-166">正则表达式语言 - 快速参考</span><span class="sxs-lookup"><span data-stu-id="5cd22-166">Regular Expression Language - Quick Reference</span></span>](regular-expression-language-quick-reference.md)
