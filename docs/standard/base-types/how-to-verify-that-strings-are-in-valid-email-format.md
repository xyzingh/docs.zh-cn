---
title: 如何确认字符串是有效的电子邮件格式
description: 阅读有关正则表达式如何在 .NET 中验证字符串是否为有效电子邮件格式的示例。
ms.date: 06/30/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- regular expressions, examples
- user input, examples
- Regex.IsMatch method
- regular expressions [.NET], examples
- examples [Visual Basic], strings
- IsValidEmail
- validation, email strings
- input, checking
- strings [.NET], examples [Visual Basic]
- email [.NET], validating
- IsMatch method
ms.assetid: 7536af08-4e86-4953-98a1-a8298623df92
ms.openlocfilehash: 07b8e31e4a0203b87492eb01ab686a1c56f5565d
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889070"
---
# <a name="how-to-verify-that-strings-are-in-valid-email-format"></a><span data-ttu-id="83989-103">如何确认字符串是有效的电子邮件格式</span><span class="sxs-lookup"><span data-stu-id="83989-103">How to verify that strings are in valid email format</span></span>

<span data-ttu-id="83989-104">下面的示例使用正则表达式来验证一个字符串是否为有效的电子邮件格式。</span><span class="sxs-lookup"><span data-stu-id="83989-104">The following example uses a regular expression to verify that a string is in valid email format.</span></span>

<span data-ttu-id="83989-105">此正则表达式相对比实际上可用作电子邮件的表达式简单。</span><span class="sxs-lookup"><span data-stu-id="83989-105">This regular expression is comparatively simple to what can actually be used as an email.</span></span> <span data-ttu-id="83989-106">使用正则表达式来验证电子邮件，这对于确保电子邮件的结构正确是很有用的，但这不是验证电子邮件是否实际存在的替代方法。</span><span class="sxs-lookup"><span data-stu-id="83989-106">Using a regular expression to validate an email is useful to make sure the structure of an email is correct, but it isn't a substitution for verifying the email actually exists.</span></span>

<span data-ttu-id="83989-107">✔️ 请使用小型正则表达式来检查电子邮件的有效结构。</span><span class="sxs-lookup"><span data-stu-id="83989-107">✔️ DO use a small regular expression to check for the valid structure of an email.</span></span>

<span data-ttu-id="83989-108">✔️ 请将测试电子邮件发送到应用用户提供的地址。</span><span class="sxs-lookup"><span data-stu-id="83989-108">✔️ DO send a test email to the address provided by a user of your app.</span></span>

<span data-ttu-id="83989-109">❌ 请勿将正则表达式用作验证电子邮件的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="83989-109">❌ DON'T use a regular expression as the only way you validate an email.</span></span>

<span data-ttu-id="83989-110">如果尝试创建完美的正则表达式来验证电子邮件的结构是否正确，表达式会变得非常复杂，以至于很难进行调试或改进。</span><span class="sxs-lookup"><span data-stu-id="83989-110">If you try to create the _perfect_ regular expression to validate that the structure of an email is correct, the expression becomes so complex that it's incredibly difficult to debug or improve.</span></span> <span data-ttu-id="83989-111">即使电子邮件的结构正确，正则表达式也无法验证其是否存在。</span><span class="sxs-lookup"><span data-stu-id="83989-111">Regular expressions can't validate an email exists, even if it's structured correctly.</span></span> <span data-ttu-id="83989-112">验证电子邮件的最佳方法是将测试电子邮件发送到该地址。</span><span class="sxs-lookup"><span data-stu-id="83989-112">The best way to validate an email is to send a test email to the address.</span></span>

[!INCLUDE [regex](../../../includes/regex.md)]

## <a name="example"></a><span data-ttu-id="83989-113">示例</span><span class="sxs-lookup"><span data-stu-id="83989-113">Example</span></span>

<span data-ttu-id="83989-114">该示例定义 `IsValidEmail` 方法，如果字符串包含有效的电子邮件地址，则该方法返回 `true`；如果字符串不包含有效的电子邮件地址，但没有采取其他任何操作，该方法返回 `false`。</span><span class="sxs-lookup"><span data-stu-id="83989-114">The example defines an `IsValidEmail` method, which returns `true` if the string contains a valid email address and `false` if it doesn't, but takes no other action.</span></span>

<span data-ttu-id="83989-115">若要验证电子邮件地址是否有效，方法 `IsValidEmail` 将使用 <xref:System.Text.RegularExpressions.Regex.Replace%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.MatchEvaluator%29?displayProperty=nameWithType> 正则表达式模式调用 `(@)(.+)$` 方法将域名从电子邮件地址分离。</span><span class="sxs-lookup"><span data-stu-id="83989-115">To verify that the email address is valid, the `IsValidEmail` method calls the <xref:System.Text.RegularExpressions.Regex.Replace%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.MatchEvaluator%29?displayProperty=nameWithType> method with the `(@)(.+)$` regular expression pattern to separate the domain name from the email address.</span></span> <span data-ttu-id="83989-116">第三个参数是表示了处理和替换匹配文本的方法的 <xref:System.Text.RegularExpressions.MatchEvaluator> 委托。</span><span class="sxs-lookup"><span data-stu-id="83989-116">The third parameter is a <xref:System.Text.RegularExpressions.MatchEvaluator> delegate that represents the method that processes and replaces the matched text.</span></span> <span data-ttu-id="83989-117">正则表达式模式的解释如下。</span><span class="sxs-lookup"><span data-stu-id="83989-117">The regular expression pattern is interpreted as follows.</span></span>

| <span data-ttu-id="83989-118">模式</span><span class="sxs-lookup"><span data-stu-id="83989-118">Pattern</span></span> | <span data-ttu-id="83989-119">描述</span><span class="sxs-lookup"><span data-stu-id="83989-119">Description</span></span>                                                                         |
|---------|-------------------------------------------------------------------------------------|
| `(@)`   | <span data-ttu-id="83989-120">匹配 @ 字符。</span><span class="sxs-lookup"><span data-stu-id="83989-120">Match the @ character.</span></span> <span data-ttu-id="83989-121">此部分是第一个捕获组。</span><span class="sxs-lookup"><span data-stu-id="83989-121">This part is the first capturing group.</span></span>                           |
| `(.+)`  | <span data-ttu-id="83989-122">匹配任意字符的一个或多个匹配项。</span><span class="sxs-lookup"><span data-stu-id="83989-122">Match one or more occurrences of any character.</span></span> <span data-ttu-id="83989-123">此部分是第二个捕获组。</span><span class="sxs-lookup"><span data-stu-id="83989-123">This part is the second capturing group.</span></span> |
| `$`     | <span data-ttu-id="83989-124">在字符串的结尾结束匹配。</span><span class="sxs-lookup"><span data-stu-id="83989-124">End the match at the end of the string.</span></span>                                             |

<span data-ttu-id="83989-125">使用 @ 字符的域名已传递给 `DomainMapper` 方法，该方法使用 <xref:System.Globalization.IdnMapping> 类将 US-ASCII 字符范围外的 Unicode 字符转换为 Punycode。</span><span class="sxs-lookup"><span data-stu-id="83989-125">The domain name along with the @ character is passed to the `DomainMapper` method, which uses the <xref:System.Globalization.IdnMapping> class to translate Unicode characters that are outside the US-ASCII character range to Punycode.</span></span> <span data-ttu-id="83989-126">如果 `invalid` 方法在域名中检测到任何无效字符，该方法还会将 `True` 标志设置为 <xref:System.Globalization.IdnMapping.GetAscii%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="83989-126">The method also sets the `invalid` flag to `True` if the <xref:System.Globalization.IdnMapping.GetAscii%2A?displayProperty=nameWithType> method detects any invalid characters in the domain name.</span></span> <span data-ttu-id="83989-127">该方法将冠以 @ 符号的 Punycode 域名返回给 `IsValidEmail` 方法。</span><span class="sxs-lookup"><span data-stu-id="83989-127">The method returns the Punycode domain name preceded by the @ symbol to the `IsValidEmail` method.</span></span>

> [!TIP]
> <span data-ttu-id="83989-128">建议使用简单的 `(@)(.+)$` 正则表达式模式对域进行规范化，然后返回一个值，指示该域是通过还是失败。</span><span class="sxs-lookup"><span data-stu-id="83989-128">It's recommended that you use use the simple `(@)(.+)$` regular expression pattern to normalize the domain and then return a value indicating that it passed or failed.</span></span> <span data-ttu-id="83989-129">但本文中的示例介绍如何进一步使用正则表达式来验证电子邮件。</span><span class="sxs-lookup"><span data-stu-id="83989-129">However, the example in this article describes how to further use a regular expression to validate the email.</span></span> <span data-ttu-id="83989-130">无论验证电子邮件的方式如何，你都应始终将测试电子邮件发送到该地址，以确保其存在。</span><span class="sxs-lookup"><span data-stu-id="83989-130">Regardless of how you validate an email, you should always send a test email to the address to make sure it exists.</span></span>

<span data-ttu-id="83989-131">然后 `IsValidEmail` 方法调用 <xref:System.Text.RegularExpressions.Regex.IsMatch%28System.String%2CSystem.String%29?displayProperty=nameWithType> 方法验证该地址是否符合正则表达式模式。</span><span class="sxs-lookup"><span data-stu-id="83989-131">The `IsValidEmail` method then calls the <xref:System.Text.RegularExpressions.Regex.IsMatch%28System.String%2CSystem.String%29?displayProperty=nameWithType> method to verify that the address conforms to a regular expression pattern.</span></span>

<span data-ttu-id="83989-132">`IsValidEmail` 方法只能确定电子邮件地址的格式是否有效，而不能验证电子邮件是否存在。</span><span class="sxs-lookup"><span data-stu-id="83989-132">The `IsValidEmail` method merely determines whether the email format is valid for an email address, it doesn't validate that the email exists.</span></span> <span data-ttu-id="83989-133">同样，`IsValidEmail` 方法不会验证顶级域名是否是 [IANA 根区域数据库](https://www.iana.org/domains/root/db)上列出的有效域名，这需执行查找操作。</span><span class="sxs-lookup"><span data-stu-id="83989-133">Also, the `IsValidEmail` method doesn't verify that the top-level domain name is a valid domain name listed at the [IANA Root Zone Database](https://www.iana.org/domains/root/db), which would require a look-up operation.</span></span>

:::code language="csharp" source="snippets/how-to-verify-that-strings-are-in-valid-email-format/csharp/RegexUtilities.cs":::

:::code language="vb" source="snippets/how-to-verify-that-strings-are-in-valid-email-format/vb/RegexUtilities.vb":::

<span data-ttu-id="83989-134">在本例中，正则表达式模式 `^[^@\s]+@[^@\s]+\.[^@\s]+$` 按下表中的方式解释。</span><span class="sxs-lookup"><span data-stu-id="83989-134">In this example, the regular expression pattern `^[^@\s]+@[^@\s]+\.[^@\s]+$` is interpreted as shown in the following table.</span></span> <span data-ttu-id="83989-135">使用 <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType> 标志编译正则表达式。</span><span class="sxs-lookup"><span data-stu-id="83989-135">The regular expression is compiled using the <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType> flag.</span></span>

| <span data-ttu-id="83989-136">模式</span><span class="sxs-lookup"><span data-stu-id="83989-136">Pattern</span></span>   | <span data-ttu-id="83989-137">描述</span><span class="sxs-lookup"><span data-stu-id="83989-137">Description</span></span>                                                                              |
|-----------|------------------------------------------------------------------------------------------|
| `^`       | <span data-ttu-id="83989-138">从字符串的开头部分开始匹配。</span><span class="sxs-lookup"><span data-stu-id="83989-138">Begin the match at the start of the string.</span></span>                                              |
| `[^@\s]+` | <span data-ttu-id="83989-139">匹配一次或多次出现的任何字符，@ 字符或空格除外。</span><span class="sxs-lookup"><span data-stu-id="83989-139">Match one or more occurrences of any character other than the @ character or whitespace.</span></span> |
| `@`       | <span data-ttu-id="83989-140">匹配 @ 字符。</span><span class="sxs-lookup"><span data-stu-id="83989-140">Match the @ character.</span></span>                                                                   |
| `[^@\s]+` | <span data-ttu-id="83989-141">匹配一次或多次出现的任何字符，@ 字符或空格除外。</span><span class="sxs-lookup"><span data-stu-id="83989-141">Match one or more occurrences of any character other than the @ character or whitespace.</span></span> |
| `\.`      | <span data-ttu-id="83989-142">匹配一个句点字符。</span><span class="sxs-lookup"><span data-stu-id="83989-142">Match a single period character.</span></span>                                                         |
| `[^@\s]+` | <span data-ttu-id="83989-143">匹配一次或多次出现的任何字符，@ 字符或空格除外。</span><span class="sxs-lookup"><span data-stu-id="83989-143">Match one or more occurrences of any character other than the @ character or whitespace.</span></span> |
| `$`       | <span data-ttu-id="83989-144">在字符串的结尾结束匹配。</span><span class="sxs-lookup"><span data-stu-id="83989-144">End the match at the end of the string.</span></span>                                                  |

> [!IMPORTANT]
> <span data-ttu-id="83989-145">此正则表达式没有涵盖有效电子邮件地址的所有字符。</span><span class="sxs-lookup"><span data-stu-id="83989-145">This regular expression is not intended to cover every aspect of a valid email address.</span></span> <span data-ttu-id="83989-146">它作为示例提供，你可以按需对其进行扩展。</span><span class="sxs-lookup"><span data-stu-id="83989-146">It's provided as an example for you to extend as needed.</span></span>

## <a name="see-also"></a><span data-ttu-id="83989-147">请参阅</span><span class="sxs-lookup"><span data-stu-id="83989-147">See also</span></span>

- [<span data-ttu-id="83989-148">.NET 正则表达式</span><span class="sxs-lookup"><span data-stu-id="83989-148">.NET Regular Expressions</span></span>](regular-expressions.md)
- [<span data-ttu-id="83989-149">对电子邮件地址进行验证的频率应为多久一次？</span><span class="sxs-lookup"><span data-stu-id="83989-149">How far should one take e-mail address validation?</span></span>](https://softwareengineering.stackexchange.com/questions/78353/how-far-should-one-take-e-mail-address-validation#78363)
