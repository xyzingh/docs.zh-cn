---
title: 将字符串分离为子字符串
description: 了解用于提取字符串各个部分的不同技术，其中包括 String.Split、正则表达式和 String.Substring。
ms.date: 10/30/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings [.NET], breaking up
ms.openlocfilehash: 88947c4576b0496e4b4e45042d665e3ca5857c53
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2020
ms.locfileid: "93403467"
---
# <a name="extract-substrings-from-a-string"></a><span data-ttu-id="7e066-103">从字符串中提取子字符串</span><span class="sxs-lookup"><span data-stu-id="7e066-103">Extract substrings from a string</span></span>

<span data-ttu-id="7e066-104">本文介绍了一些用于提取字符串各个部分的不同技术。</span><span class="sxs-lookup"><span data-stu-id="7e066-104">This article covers some different techniques for extracting parts of a string.</span></span>

- <span data-ttu-id="7e066-105">当所需的子字符串由一个已知的分隔符（或多个分隔符）分隔时，请使用 [Split 方法](#stringsplit-method)。</span><span class="sxs-lookup"><span data-stu-id="7e066-105">Use the [Split method](#stringsplit-method) when the substrings you want are separated by a known delimiting character (or characters).</span></span>
- <span data-ttu-id="7e066-106">如果字符串符合某种固定模式，则可使用[正则表达式](#regular-expressions)。</span><span class="sxs-lookup"><span data-stu-id="7e066-106">[Regular expressions](#regular-expressions) are useful when the string conforms to a fixed pattern.</span></span>
- <span data-ttu-id="7e066-107">如果不需要提取字符串中的所有子字符串，请结合使用 [IndexOf 和 Substring 方法](#stringindexof-and-stringsubstring-methods)。</span><span class="sxs-lookup"><span data-stu-id="7e066-107">Use the [IndexOf and Substring methods](#stringindexof-and-stringsubstring-methods) in conjunction when you don't want to extract *all* of the substrings in a string.</span></span>

## <a name="stringsplit-method"></a><span data-ttu-id="7e066-108">String.Split 方法</span><span class="sxs-lookup"><span data-stu-id="7e066-108">String.Split method</span></span>

<span data-ttu-id="7e066-109"><xref:System.String.Split%2A?displayProperty=nameWithType> 可提供少量重载，来根据指定的一个或多个分隔符将字符串分解为一组子字符串。</span><span class="sxs-lookup"><span data-stu-id="7e066-109"><xref:System.String.Split%2A?displayProperty=nameWithType> provides a handful of overloads to help you break up a string into a group of substrings based on one or more delimiting characters that you specify.</span></span> <span data-ttu-id="7e066-110">可以选择限制最终结果中子字符串的总数、剪裁子字符串中的空白字符或排除空子字符串。</span><span class="sxs-lookup"><span data-stu-id="7e066-110">You can choose to limit the total number of substrings in the final result, trim white-space characters from substrings, or exclude empty substrings.</span></span>

<span data-ttu-id="7e066-111">下面的示例显示了三种不同的 `String.Split()` 重载。</span><span class="sxs-lookup"><span data-stu-id="7e066-111">The following examples show three different overloads of `String.Split()`.</span></span> <span data-ttu-id="7e066-112">第一个示例调用 <xref:System.String.Split(System.Char[])> 重载，而不传递任何分隔符。</span><span class="sxs-lookup"><span data-stu-id="7e066-112">The first example calls the <xref:System.String.Split(System.Char[])> overload without passing any separator characters.</span></span> <span data-ttu-id="7e066-113">如果未指定任何分隔符，`String.Split()` 将使用默认分隔符（空白字符）来拆分字符串。</span><span class="sxs-lookup"><span data-stu-id="7e066-113">When you don't specify any delimiting characters, `String.Split()` uses default delimiters, which are white-space characters, to split up the string.</span></span>

[!code-csharp-interactive[Intro#1](snippets/parse-strings/csharp/intro.cs#1)]
:::code language="vb" source="snippets/parse-strings/vb/intro.vb" id="1":::

<span data-ttu-id="7e066-114">正如你所看到的那样，两个子字符串之间包含句点字符 (`.`)。</span><span class="sxs-lookup"><span data-stu-id="7e066-114">As you can see, the period characters (`.`) are included in two of the substrings.</span></span> <span data-ttu-id="7e066-115">如果要排除句点字符，可以将句点字符添加为额外的分隔符。</span><span class="sxs-lookup"><span data-stu-id="7e066-115">If you want to exclude the period characters, you can add the period character as an additional delimiting character.</span></span> <span data-ttu-id="7e066-116">下面的示例演示了如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="7e066-116">The next example shows how to do this.</span></span>

[!code-csharp-interactive[Intro#1](snippets/parse-strings/csharp/intro.cs#2)]
:::code language="vb" source="snippets/parse-strings/vb/intro.vb" id="2":::

<span data-ttu-id="7e066-117">子字符串之间的句点消息，但现在包含了两个额外的空子字符串。</span><span class="sxs-lookup"><span data-stu-id="7e066-117">The periods are gone from the substrings, but now two extra empty substrings have been included.</span></span> <span data-ttu-id="7e066-118">这些空子字符串表示单词与紧跟单词之后的句点之间的子字符串。</span><span class="sxs-lookup"><span data-stu-id="7e066-118">These empty substring represent the substring between the word and the period that follows it.</span></span> <span data-ttu-id="7e066-119">若要从生成的数组中删除空字符串，可以调用 <xref:System.String.Split(System.Char[],System.StringSplitOptions)> 重载，并为 `options` 参数指定 <xref:System.StringSplitOptions.RemoveEmptyEntries?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="7e066-119">To omit empty substrings from the resulting array, you can call the <xref:System.String.Split(System.Char[],System.StringSplitOptions)> overload and specify <xref:System.StringSplitOptions.RemoveEmptyEntries?displayProperty=nameWithType> for the `options` parameter.</span></span>

[!code-csharp-interactive[Intro#1](snippets/parse-strings/csharp/intro.cs#3)]
:::code language="vb" source="snippets/parse-strings/vb/intro.vb" id="3":::

## <a name="regular-expressions"></a><span data-ttu-id="7e066-120">正则表达式</span><span class="sxs-lookup"><span data-stu-id="7e066-120">Regular expressions</span></span>

<span data-ttu-id="7e066-121">如果字符串符合某种固定模式，则可以使用正则表达式提取并处理其元素。</span><span class="sxs-lookup"><span data-stu-id="7e066-121">If your string conforms to a fixed pattern, you can use a regular expression to extract and handle its elements.</span></span> <span data-ttu-id="7e066-122">例如，如果字符串采用“数字 操作数 数字”  格式，则可以[使用正则表达式](regular-expressions.md)提取并处理字符串的元素。</span><span class="sxs-lookup"><span data-stu-id="7e066-122">For example, if strings take the form " *number* *operand* *number* ", you can use a [regular expression](regular-expressions.md) to extract and handle the string's elements.</span></span> <span data-ttu-id="7e066-123">下面是一个示例：</span><span class="sxs-lookup"><span data-stu-id="7e066-123">Here's an example:</span></span>

:::code language="csharp" source="snippets/parse-strings/csharp/regex.cs" id="1" interactive="try-dotnet":::
:::code language="vb" source="snippets/parse-strings/vb/regex.vb" id="1":::

<span data-ttu-id="7e066-124">正则表达式模式 `(\d+)\s+([-+*/])\s+(\d+)` 的定义如下：</span><span class="sxs-lookup"><span data-stu-id="7e066-124">The regular expression pattern `(\d+)\s+([-+*/])\s+(\d+)` is defined like this:</span></span>

|<span data-ttu-id="7e066-125">模式</span><span class="sxs-lookup"><span data-stu-id="7e066-125">Pattern</span></span>|<span data-ttu-id="7e066-126">说明</span><span class="sxs-lookup"><span data-stu-id="7e066-126">Description</span></span>|
|-------------|-----------------|
|`(\d+)`|<span data-ttu-id="7e066-127">匹配一个或多个十进制数字。</span><span class="sxs-lookup"><span data-stu-id="7e066-127">Match one or more decimal digits.</span></span> <span data-ttu-id="7e066-128">这是第一个捕获组。</span><span class="sxs-lookup"><span data-stu-id="7e066-128">This is the first capturing group.</span></span>|
|`\s+`|<span data-ttu-id="7e066-129">匹配一个或多个空白字符。</span><span class="sxs-lookup"><span data-stu-id="7e066-129">Match one or more white-space characters.</span></span>|
|`([-+*/])`|<span data-ttu-id="7e066-130">匹配算术运算符（+、-、\* 或 /）。</span><span class="sxs-lookup"><span data-stu-id="7e066-130">Match an arithmetic operator sign (+, -, \*, or /).</span></span> <span data-ttu-id="7e066-131">这是第二个捕获组。</span><span class="sxs-lookup"><span data-stu-id="7e066-131">This is the second capturing group.</span></span>|
|`\s+`|<span data-ttu-id="7e066-132">匹配一个或多个空白字符。</span><span class="sxs-lookup"><span data-stu-id="7e066-132">Match one or more white-space characters.</span></span>|
|`(\d+)`|<span data-ttu-id="7e066-133">匹配一个或多个十进制数字。</span><span class="sxs-lookup"><span data-stu-id="7e066-133">Match one or more decimal digits.</span></span> <span data-ttu-id="7e066-134">这是第三个捕获组。</span><span class="sxs-lookup"><span data-stu-id="7e066-134">This is the third capturing group.</span></span>|

<span data-ttu-id="7e066-135">你也可以使用正则表达式根据某种模式而非固定字符集提取字符串中的子字符串。</span><span class="sxs-lookup"><span data-stu-id="7e066-135">You can also use a regular expression to extract substrings from a string based on a pattern rather than a fixed set of characters.</span></span> <span data-ttu-id="7e066-136">在下面的任意一种情况下，常用此方案：</span><span class="sxs-lookup"><span data-stu-id="7e066-136">This is a common scenario when either of these conditions occurs:</span></span>

- <span data-ttu-id="7e066-137">一个或多个分隔符不总是用作 <xref:System.String> 实例中的分隔符。</span><span class="sxs-lookup"><span data-stu-id="7e066-137">One or more of the delimiter characters does not *always* serve as a delimiter in the <xref:System.String> instance.</span></span>

- <span data-ttu-id="7e066-138">分隔符的顺序和数量多变或未知。</span><span class="sxs-lookup"><span data-stu-id="7e066-138">The sequence and number of delimiter characters is variable or unknown.</span></span>

<span data-ttu-id="7e066-139">例如，不能使用 <xref:System.String.Split%2A> 方法拆分以下字符串，因为 `\n`（换行）符的数量是可变的，并且它们不总是用作分隔符。</span><span class="sxs-lookup"><span data-stu-id="7e066-139">For example, the <xref:System.String.Split%2A> method cannot be used to split the following string, because the number of `\n` (newline) characters is variable, and they don't always serve as delimiters.</span></span>

```text
[This is captured\ntext.]\n\n[\n[This is more captured text.]\n]
\n[Some more captured text:\n   Option1\n   Option2][Terse text.]
```

<span data-ttu-id="7e066-140">正则表达式可以轻松拆分此字符串，如下面的示例所示。</span><span class="sxs-lookup"><span data-stu-id="7e066-140">A regular expression can split this string easily, as the following example shows.</span></span>

:::code language="csharp" source="snippets/parse-strings/csharp/regex.cs" id="2" interactive="try-dotnet":::
:::code language="vb" source="snippets/parse-strings/vb/regex.vb" id="2":::

<span data-ttu-id="7e066-141">正则表达式模式 `\[([^\[\]]+)\]` 的定义如下：</span><span class="sxs-lookup"><span data-stu-id="7e066-141">The regular expression pattern `\[([^\[\]]+)\]` is defined like this:</span></span>

|<span data-ttu-id="7e066-142">模式</span><span class="sxs-lookup"><span data-stu-id="7e066-142">Pattern</span></span>|<span data-ttu-id="7e066-143">说明</span><span class="sxs-lookup"><span data-stu-id="7e066-143">Description</span></span>|
|-------------|-----------------|
|`\[`|<span data-ttu-id="7e066-144">匹配左方括号。</span><span class="sxs-lookup"><span data-stu-id="7e066-144">Match an opening bracket.</span></span>|
|`([^\[\]]+)`|<span data-ttu-id="7e066-145">一次或多次与非左或右方括号的字符匹配</span><span class="sxs-lookup"><span data-stu-id="7e066-145">Match any character that is not an opening or a closing bracket one or more times.</span></span> <span data-ttu-id="7e066-146">这是第一个捕获组。</span><span class="sxs-lookup"><span data-stu-id="7e066-146">This is the first capturing group.</span></span>|
|`\]`|<span data-ttu-id="7e066-147">匹配右方括号。</span><span class="sxs-lookup"><span data-stu-id="7e066-147">Match a closing bracket.</span></span>|

<span data-ttu-id="7e066-148"><xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> 方法几乎与 <xref:System.String.Split%2A?displayProperty=nameWithType> 相同，不同之处在于，它根据正则表达式模式而非固定字符集拆分字符串。</span><span class="sxs-lookup"><span data-stu-id="7e066-148">The <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> method is almost identical to <xref:System.String.Split%2A?displayProperty=nameWithType>, except that it splits a string based on a regular expression pattern instead of a fixed character set.</span></span> <span data-ttu-id="7e066-149">例如，下面的示例使用 <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> 方法拆分字符串，该字符串包含由连字符和其他字符的各种组合分隔的子字符串。</span><span class="sxs-lookup"><span data-stu-id="7e066-149">For example, the following example uses the <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> method to split a string that contains substrings delimited by various combinations of hyphens and other characters.</span></span>

:::code language="csharp" source="snippets/parse-strings/csharp/regex.cs" id="3" interactive="try-dotnet":::
:::code language="vb" source="snippets/parse-strings/vb/regex.vb" id="3":::

<span data-ttu-id="7e066-150">正则表达式模式 `\s-\s?[+*]?\s?-\s` 的定义如下：</span><span class="sxs-lookup"><span data-stu-id="7e066-150">The regular expression pattern `\s-\s?[+*]?\s?-\s` is defined like this:</span></span>

|<span data-ttu-id="7e066-151">模式</span><span class="sxs-lookup"><span data-stu-id="7e066-151">Pattern</span></span>|<span data-ttu-id="7e066-152">说明</span><span class="sxs-lookup"><span data-stu-id="7e066-152">Description</span></span>|
|-------------|-----------------|
|`\s-`|<span data-ttu-id="7e066-153">匹配后跟一个连字符的空白字符。</span><span class="sxs-lookup"><span data-stu-id="7e066-153">Match a white-space character followed by a hyphen.</span></span>|
|`\s?`|<span data-ttu-id="7e066-154">匹配零个或一个空白字符。</span><span class="sxs-lookup"><span data-stu-id="7e066-154">Match zero or one white-space character.</span></span>|
|`[+*]?`|<span data-ttu-id="7e066-155">与 + 或 \* 字符的零个或一个匹配项匹配。</span><span class="sxs-lookup"><span data-stu-id="7e066-155">Match zero or one occurrence of either the + or \* character.</span></span>|
|`\s?`|<span data-ttu-id="7e066-156">匹配零个或一个空白字符。</span><span class="sxs-lookup"><span data-stu-id="7e066-156">Match zero or one white-space character.</span></span>|
|`-\s`|<span data-ttu-id="7e066-157">匹配后跟一个空白字符的连字符。</span><span class="sxs-lookup"><span data-stu-id="7e066-157">Match a hyphen followed by a white-space character.</span></span>|

## <a name="stringindexof-and-stringsubstring-methods"></a><span data-ttu-id="7e066-158">String.IndexOf 和 String.Substring 方法</span><span class="sxs-lookup"><span data-stu-id="7e066-158">String.IndexOf and String.Substring methods</span></span>

<span data-ttu-id="7e066-159">如果并不需要字符串中的所有子字符串，则可能更想要使用一种字符串比较方法来返回匹配开始之处的索引。</span><span class="sxs-lookup"><span data-stu-id="7e066-159">If you aren't interested in all of the substrings in a string, you might prefer to work with one of the string comparison methods that returns the index at which the match begins.</span></span> <span data-ttu-id="7e066-160">然后，可以调用 <xref:System.String.Substring%2A> 方法来提取所需的子字符串。</span><span class="sxs-lookup"><span data-stu-id="7e066-160">You can then call the <xref:System.String.Substring%2A> method to extract the substring that you want.</span></span> <span data-ttu-id="7e066-161">字符串比较方法包括：</span><span class="sxs-lookup"><span data-stu-id="7e066-161">The string comparison methods include:</span></span>

- <span data-ttu-id="7e066-162"><xref:System.String.IndexOf%2A>，它返回字符串实例中的某个字符或字符串的第一个匹配项的从零开始的索引。</span><span class="sxs-lookup"><span data-stu-id="7e066-162"><xref:System.String.IndexOf%2A>, which returns the zero-based index of the first occurrence of a character or string in a string instance.</span></span>

- <span data-ttu-id="7e066-163"><xref:System.String.IndexOfAny%2A>，它返回在当前字符串实例中字符数组中任何字符的第一个匹配项的从零开始的索引。</span><span class="sxs-lookup"><span data-stu-id="7e066-163"><xref:System.String.IndexOfAny%2A>, which returns the zero-based index in the current string instance of the first occurrence of any character in a character array.</span></span>

- <span data-ttu-id="7e066-164"><xref:System.String.LastIndexOf%2A>，它返回字符串实例中的某个字符或字符串的最后一个匹配项的从零开始的索引。</span><span class="sxs-lookup"><span data-stu-id="7e066-164"><xref:System.String.LastIndexOf%2A>, which returns the zero-based index of the last occurrence of a character or string in a string instance.</span></span>

- <span data-ttu-id="7e066-165"><xref:System.String.LastIndexOfAny%2A>，它返回在当前字符串实例中字符数组中任何字符的最后一个匹配项的从零开始的索引。</span><span class="sxs-lookup"><span data-stu-id="7e066-165"><xref:System.String.LastIndexOfAny%2A>, which returns a zero-based index in the current string instance of the last occurrence of any character in a character array.</span></span>

<span data-ttu-id="7e066-166">以下示例使用 <xref:System.String.IndexOf%2A> 方法查找字符串中的句点。</span><span class="sxs-lookup"><span data-stu-id="7e066-166">The following example uses the <xref:System.String.IndexOf%2A> method to find the periods in a string.</span></span> <span data-ttu-id="7e066-167">然后，它使用 <xref:System.String.Substring%2A> 方法返回完整句子。</span><span class="sxs-lookup"><span data-stu-id="7e066-167">It then uses the <xref:System.String.Substring%2A> method to return full sentences.</span></span>

:::code language="csharp" source="snippets/parse-strings/csharp/indexof.cs" id="1" interactive="try-dotnet":::
:::code language="vb" source="snippets/parse-strings/vb/indexof.vb" id="1":::

## <a name="see-also"></a><span data-ttu-id="7e066-168">请参阅</span><span class="sxs-lookup"><span data-stu-id="7e066-168">See also</span></span>

- [<span data-ttu-id="7e066-169">.NET 中的基本字符串操作</span><span class="sxs-lookup"><span data-stu-id="7e066-169">Basic string operations in .NET</span></span>](basic-string-operations.md)
- [<span data-ttu-id="7e066-170">.NET 正则表达式</span><span class="sxs-lookup"><span data-stu-id="7e066-170">.NET regular expressions</span></span>](regular-expressions.md)
- [<span data-ttu-id="7e066-171">如何使用 C# 中的 String.Split 分析字符串</span><span class="sxs-lookup"><span data-stu-id="7e066-171">How to parse strings using String.Split in C#</span></span>](../../csharp/how-to/parse-strings-using-split.md)
