---
title: .NET 中的 :::no-loc(char):::acter 编码简介
description: 了解 .NET 中的 :::no-loc(char):::acter 编码和解码。
ms.date: 03/09/2020
no-loc:
- ':::no-loc(Rune):::'
- ':::no-loc(char):::'
- ':::no-loc(string):::'
dev_langs:
- csharp
helpviewer_keywords:
- encoding, understanding
ms.openlocfilehash: 572fcd289eea720873d94e7fc71f3b4a030d1d70
ms.sourcegitcommit: 74d05613d6c57106f83f82ce8ee71176874ea3f0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93282317"
---
# <a name="character-encoding-in-net"></a><span data-ttu-id="a7dc0-103">.NET 中的字符编码</span><span class="sxs-lookup"><span data-stu-id="a7dc0-103">Character encoding in .NET</span></span>

<span data-ttu-id="a7dc0-104">本文介绍 .NET 使用的 :::no-loc(char):::acter 编码系统。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-104">This article provides an introduction to :::no-loc(char):::acter encoding systems that are used by .NET.</span></span> <span data-ttu-id="a7dc0-105">具体说明如何将 <xref:System.String>、<xref:System.Char>、<xref:System.Text.:::no-loc(Rune):::>和 <xref:System.Globalization.StringInfo> 类型用于 Unicode、UTF-16 和 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-105">The article explains how the <xref:System.String>, <xref:System.Char>, <xref:System.Text.:::no-loc(Rune):::>, and <xref:System.Globalization.StringInfo> types work with Unicode, UTF-16, and UTF-8.</span></span>

<span data-ttu-id="a7dc0-106">本文中使用的术语“:::no-loc(char):::acter”从读者的角度通常是指单个显示元素 。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-106">The term *:::no-loc(char):::acter* is used here in the general sense of *what a reader perceives as a single display element*.</span></span> <span data-ttu-id="a7dc0-107">常见的示例是字母“a”、“@”和表情符号 🐂。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-107">Common examples are the letter "a", the symbol "@", and the emoji "🐂".</span></span> <span data-ttu-id="a7dc0-108">有时，一个 :::no-loc(char):::acter 实际上由多个独立的显示元素组成，具体可以参考介绍[字形群集](#grapheme-clusters)的部分。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-108">Sometimes what looks like one :::no-loc(char):::acter is actually composed of multiple independent display elements, as the section on [grapheme clusters](#grapheme-clusters) explains.</span></span>

## <a name="the-no-locstring-and-no-locchar-types"></a><span data-ttu-id="a7dc0-109">:::no-loc(string)::: 和 :::no-loc(char)::: 类型</span><span class="sxs-lookup"><span data-stu-id="a7dc0-109">The :::no-loc(string)::: and :::no-loc(char)::: types</span></span>

<span data-ttu-id="a7dc0-110">[:::no-loc(string):::](xref:System.String) 类的实例表示一些文本。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-110">An instance of the [:::no-loc(string):::](xref:System.String) class represents some text.</span></span> <span data-ttu-id="a7dc0-111">`:::no-loc(string):::` 在逻辑上是一个 16 位值的序列，其中每个值都是 [:::no-loc(char):::](xref:System.Char) 结构的实例。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-111">A `:::no-loc(string):::` is logically a sequence of 16-bit values, each of which is an instance of the [:::no-loc(char):::](xref:System.Char) struct.</span></span> <span data-ttu-id="a7dc0-112">[:::no-loc(string):::.Length](xref:System.String.Length) 属性返回 `:::no-loc(string):::` 实例中 `:::no-loc(char):::` 实例的数目。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-112">The [:::no-loc(string):::.Length](xref:System.String.Length) property returns the number of `:::no-loc(char):::` instances in the `:::no-loc(string):::` instance.</span></span>

<span data-ttu-id="a7dc0-113">下面的示例函数以十六进制表示法打印 `:::no-loc(string):::` 中所有 `:::no-loc(char):::` 实例的值：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-113">The following sample function prints out the values in hexadecimal notation of all the `:::no-loc(char):::` instances in a `:::no-loc(string):::`:</span></span>

<span data-ttu-id="a7dc0-114">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/PrintStringChars.cs" id="SnippetPrintChars":::</span><span class="sxs-lookup"><span data-stu-id="a7dc0-114">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/PrintStringChars.cs" id="SnippetPrintChars":::</span></span>

<span data-ttu-id="a7dc0-115">将 :::no-loc(string)::: "Hello" 传递给此函数，将获得以下输出：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-115">Pass the :::no-loc(string)::: "Hello" to this function, and you get the following output:</span></span>

```csharp
PrintChars("Hello");
```

```output
"Hello".Length = 5
s[0] = 'H' ('\u0048')
s[1] = 'e' ('\u0065')
s[2] = 'l' ('\u006c')
s[3] = 'l' ('\u006c')
s[4] = 'o' ('\u006f')
```

<span data-ttu-id="a7dc0-116">每个 :::no-loc(char):::acter 由一个 `:::no-loc(char):::` 值表示。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-116">Each :::no-loc(char):::acter is represented by a single `:::no-loc(char):::` value.</span></span> <span data-ttu-id="a7dc0-117">这种模式适用于世界上大多数语言。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-117">That pattern holds true for most of the world's languages.</span></span> <span data-ttu-id="a7dc0-118">例如，下面是两个中文 :::no-loc(char):::acter 的输出，听起来像“nǐ hǎo”，它们表示“Hello” ：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-118">For example, here's the output for two Chinese :::no-loc(char):::acters that sound like *nǐ hǎo* and mean *Hello* :</span></span>

```csharp
PrintChars("你好");
```

```output
"你好".Length = 2
s[0] = '你' ('\u4f60')
s[1] = '好' ('\u597d')
```

<span data-ttu-id="a7dc0-119">但是，对于某些语言以及某些符号和表情符号，需要两个 `:::no-loc(char):::` 实例来表示一个 :::no-loc(char):::acter。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-119">However, for some languages and for some symbols and emoji, it takes two `:::no-loc(char):::` instances to represent a single :::no-loc(char):::acter.</span></span> <span data-ttu-id="a7dc0-120">例如，比较奥塞治文中表示 Osage 的单词中的 :::no-loc(char):::acter 和 `:::no-loc(char):::` 实例：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-120">For example, compare the :::no-loc(char):::acters and `:::no-loc(char):::` instances in the word that means *Osage* in the Osage language:</span></span>

```csharp
PrintChars("𐓏𐓘𐓻𐓘𐓻𐓟 𐒻𐓟");
```

```output
"𐓏𐓘𐓻𐓘𐓻𐓟 𐒻𐓟".Length = 17
s[0] = '�' ('\ud801')
s[1] = '�' ('\udccf')
s[2] = '�' ('\ud801')
s[3] = '�' ('\udcd8')
s[4] = '�' ('\ud801')
s[5] = '�' ('\udcfb')
s[6] = '�' ('\ud801')
s[7] = '�' ('\udcd8')
s[8] = '�' ('\ud801')
s[9] = '�' ('\udcfb')
s[10] = '�' ('\ud801')
s[11] = '�' ('\udcdf')
s[12] = ' ' ('\u0020')
s[13] = '�' ('\ud801')
s[14] = '�' ('\udcbb')
s[15] = '�' ('\ud801')
s[16] = '�' ('\udcdf')
```

<span data-ttu-id="a7dc0-121">在前面的示例中，除空格以外的每个 :::no-loc(char):::acter 都由两个 `:::no-loc(char):::` 实例表示。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-121">In the preceding example, each :::no-loc(char):::acter except the space is represented by two `:::no-loc(char):::` instances.</span></span>

<span data-ttu-id="a7dc0-122">单个 Unicode 表情符号也由两个 `:::no-loc(char):::` 表示，如以下示例中所示的 ox 表情符号：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-122">A single Unicode emoji is also represented by two `:::no-loc(char):::`s, as seen in the following example showing an ox emoji:</span></span>

```output
"🐂".Length = 2
s[0] = '�' ('\ud83d')
s[1] = '�' ('\udc02')
```

<span data-ttu-id="a7dc0-123">这些示例表明，`:::no-loc(string):::.Length` 的值表示 `:::no-loc(char):::` 实例的数量，不一定表示显示的 :::no-loc(char):::acter 数。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-123">These examples show that the value of `:::no-loc(string):::.Length`, which indicates the number of `:::no-loc(char):::` instances, doesn't necessarily indicate the number of displayed :::no-loc(char):::acters.</span></span> <span data-ttu-id="a7dc0-124">一个 `:::no-loc(char):::` 实例本身不一定表示一个 :::no-loc(char):::acter。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-124">A single `:::no-loc(char):::` instance by itself doesn't necessarily represent a :::no-loc(char):::acter.</span></span>

<span data-ttu-id="a7dc0-125">映射到单个 :::no-loc(char):::acter 的 `:::no-loc(char):::` 对称为“代理项对”。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-125">The `:::no-loc(char):::` pairs that map to a single :::no-loc(char):::acter are called *surrogate pairs*.</span></span> <span data-ttu-id="a7dc0-126">若要了解它们的工作原理，需要了解 Unicode 和 UTF-16 编码。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-126">To understand how they work, you need to understand Unicode and UTF-16 encoding.</span></span>

## <a name="unicode-code-points"></a><span data-ttu-id="a7dc0-127">Unicode 码位</span><span class="sxs-lookup"><span data-stu-id="a7dc0-127">Unicode code points</span></span>

<span data-ttu-id="a7dc0-128">Unicode 是一种国际编码标准，可用于各种平台以及各种语言和脚本。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-128">Unicode is an international encoding standard for use on various platforms and with various languages and scripts.</span></span>

<span data-ttu-id="a7dc0-129">Unicode 标准定义了超过 110 万个[码位](https://www.unicode.org/glossary/#code_point)。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-129">The Unicode Standard defines over 1.1 million [code points](https://www.unicode.org/glossary/#code_point).</span></span> <span data-ttu-id="a7dc0-130">码位是一个整数值，范围从 0 到 `U+10FFFF`（十进制 1,114,111）。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-130">A code point is an integer value that can range from 0 to `U+10FFFF` (decimal 1,114,111).</span></span> <span data-ttu-id="a7dc0-131">一些码位被分配给字母、符号或表情符号。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-131">Some code points are assigned to letters, symbols, or emoji.</span></span> <span data-ttu-id="a7dc0-132">其他码位分配给控制文本或 :::no-loc(char):::acter 显示方式的操作，例如换行。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-132">Others are assigned to actions that control how text or :::no-loc(char):::acters are displayed, such as advance to a new line.</span></span> <span data-ttu-id="a7dc0-133">很多码位尚未经分配。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-133">Many code points are not yet assigned.</span></span>

<span data-ttu-id="a7dc0-134">下面是码位分配的一些示例，其中包含指向它们所在的 Unicode :::no-loc(char):::t 的链接：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-134">Here are some examples of code point assignments, with links to Unicode :::no-loc(char):::ts in which they appear:</span></span>

|<span data-ttu-id="a7dc0-135">十进制</span><span class="sxs-lookup"><span data-stu-id="a7dc0-135">Decimal</span></span>|<span data-ttu-id="a7dc0-136">Hex</span><span class="sxs-lookup"><span data-stu-id="a7dc0-136">Hex</span></span>       |<span data-ttu-id="a7dc0-137">示例</span><span class="sxs-lookup"><span data-stu-id="a7dc0-137">Example</span></span>|<span data-ttu-id="a7dc0-138">描述</span><span class="sxs-lookup"><span data-stu-id="a7dc0-138">Description</span></span>|
|------:|----------|-------|-----------|
|<span data-ttu-id="a7dc0-139">10</span><span class="sxs-lookup"><span data-stu-id="a7dc0-139">10</span></span>     | `U+000A` |<span data-ttu-id="a7dc0-140">不可用</span><span class="sxs-lookup"><span data-stu-id="a7dc0-140">N/A</span></span>| <span data-ttu-id="a7dc0-141">[换行](https://www.unicode.org/:::no-loc(char):::ts/PDF/U0000.pdf)</span><span class="sxs-lookup"><span data-stu-id="a7dc0-141">[LINE FEED](https://www.unicode.org/:::no-loc(char):::ts/PDF/U0000.pdf)</span></span> |
|<span data-ttu-id="a7dc0-142">97</span><span class="sxs-lookup"><span data-stu-id="a7dc0-142">97</span></span>     | `U+0061` | <span data-ttu-id="a7dc0-143">a</span><span class="sxs-lookup"><span data-stu-id="a7dc0-143">a</span></span> | <span data-ttu-id="a7dc0-144">[拉丁文小写字母 a](https://www.unicode.org/:::no-loc(char):::ts/PDF/U0000.pdf)</span><span class="sxs-lookup"><span data-stu-id="a7dc0-144">[LATIN SMALL LETTER A](https://www.unicode.org/:::no-loc(char):::ts/PDF/U0000.pdf)</span></span> |
|<span data-ttu-id="a7dc0-145">562</span><span class="sxs-lookup"><span data-stu-id="a7dc0-145">562</span></span>    | `U+0232` | <span data-ttu-id="a7dc0-146">Ȳ</span><span class="sxs-lookup"><span data-stu-id="a7dc0-146">Ȳ</span></span> | <span data-ttu-id="a7dc0-147">[带长音符的拉丁文大写字母 Y](https://www.unicode.org/:::no-loc(char):::ts/PDF/U0180.pdf)</span><span class="sxs-lookup"><span data-stu-id="a7dc0-147">[LATIN CAPITAL LETTER Y WITH MACRON](https://www.unicode.org/:::no-loc(char):::ts/PDF/U0180.pdf)</span></span> |
|<span data-ttu-id="a7dc0-148">68,675</span><span class="sxs-lookup"><span data-stu-id="a7dc0-148">68,675</span></span> | `U+10C43`| <span data-ttu-id="a7dc0-149">𐱃</span><span class="sxs-lookup"><span data-stu-id="a7dc0-149">𐱃</span></span> | <span data-ttu-id="a7dc0-150">[古突厥文字母鄂尔浑文 AT](https://www.unicode.org/:::no-loc(char):::ts/PDF/U10C00.pdf)</span><span class="sxs-lookup"><span data-stu-id="a7dc0-150">[OLD TURKIC LETTER ORKHON AT](https://www.unicode.org/:::no-loc(char):::ts/PDF/U10C00.pdf)</span></span> |
|<span data-ttu-id="a7dc0-151">127,801</span><span class="sxs-lookup"><span data-stu-id="a7dc0-151">127,801</span></span>| `U+1F339`| <span data-ttu-id="a7dc0-152">🌹</span><span class="sxs-lookup"><span data-stu-id="a7dc0-152">🌹</span></span> | <span data-ttu-id="a7dc0-153">[玫瑰花表情符号](https://www.unicode.org/:::no-loc(char):::ts/PDF/U1F300.pdf)</span><span class="sxs-lookup"><span data-stu-id="a7dc0-153">[ROSE emoji](https://www.unicode.org/:::no-loc(char):::ts/PDF/U1F300.pdf)</span></span> |

<span data-ttu-id="a7dc0-154">通常使用语法 `U+xxxx` 来表示码位，其中 `xxxx` 是十六进制编码的整数值。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-154">Code points are customarily referred to by using the syntax `U+xxxx`, where `xxxx` is the hex-encoded integer value.</span></span>

<span data-ttu-id="a7dc0-155">整个码位范围包含两个子范围：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-155">Within the full range of code points there are two subranges:</span></span>

* <span data-ttu-id="a7dc0-156">`U+0000..U+FFFF` 范围内的基本多语言平面 (BMP)。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-156">The **Basic Multilingual Plane (BMP)** in the range `U+0000..U+FFFF`.</span></span> <span data-ttu-id="a7dc0-157">这个 16 位范围提供 65,536 个码位，足以涵盖世界上大多数编写系统。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-157">This 16-bit range provides 65,536 code points, enough to cover the majority of the world's writing systems.</span></span>
* <span data-ttu-id="a7dc0-158">`U+10000..U+10FFFF` 范围内的补充码位。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-158">**Supplementary code points** in the range `U+10000..U+10FFFF`.</span></span> <span data-ttu-id="a7dc0-159">这个 21 位范围提供了超过一百万个额外的码位，可用于不太知名的语言和其他用途，例如表情符号。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-159">This 21-bit range provides more than a million additional code points that can be used for less well-known languages and other purposes such as emojis.</span></span>

<span data-ttu-id="a7dc0-160">下图说明了 BMP 与补充码位之间的关系。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-160">The following diagram illustrates the relationship between the BMP and the supplementary code points.</span></span>

:::image type="content" source="media/:::no-loc(char):::acter-encoding-introduction/bmp-and-supplementary.svg" alt-text="BMP and supplementary code points":::

## <a name="utf-16-code-units"></a><span data-ttu-id="a7dc0-162">UTF-16 代码单位</span><span class="sxs-lookup"><span data-stu-id="a7dc0-162">UTF-16 code units</span></span>

<span data-ttu-id="a7dc0-163">16 位 Unicode 转换格式 ([UTF-16](https://www.unicode.org/faq/utf_bom.html#UTF16)) 是一种 :::no-loc(char):::acter 编码系统，它使用 16 位代码单位来表示 Unicode 码位。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-163">16-bit Unicode Transformation Format ( [UTF-16](https://www.unicode.org/faq/utf_bom.html#UTF16)) is a :::no-loc(char):::acter encoding system that uses 16-bit *code units* to represent Unicode code points.</span></span> <span data-ttu-id="a7dc0-164">.NET 使用 UTF-16 对 `:::no-loc(string):::` 中的文本进行编码。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-164">.NET uses UTF-16 to encode the text in a `:::no-loc(string):::`.</span></span> <span data-ttu-id="a7dc0-165">`:::no-loc(char):::` 实例表示一个 16 位代码单位。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-165">A `:::no-loc(char):::` instance represents a 16-bit code unit.</span></span>

<span data-ttu-id="a7dc0-166">单个 16 位代码单位可以表示基本多语言平面的 16 位范围内的任何码位。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-166">A single 16-bit code unit can represent any code point in the 16-bit range of the Basic Multilingual Plane.</span></span> <span data-ttu-id="a7dc0-167">但对于补充范围内的码位，需要两个 `:::no-loc(char):::` 实例。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-167">But for a code point in the supplementary range, two `:::no-loc(char):::` instances are needed.</span></span>

## <a name="surrogate-pairs"></a><span data-ttu-id="a7dc0-168">代理项对</span><span class="sxs-lookup"><span data-stu-id="a7dc0-168">Surrogate pairs</span></span>

<span data-ttu-id="a7dc0-169">通过称为“代理项码位”的特殊范围（从 `U+D800` 到 `U+DFFF`，十进制 55,296 到 57,343，含限值），可以将两个 16 位值转换为一个 21 位值。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-169">The translation of two 16-bit values to a single 21-bit value is facilitated by a special range called the *surrogate code points* , from `U+D800` to `U+DFFF` (decimal 55,296 to 57,343), inclusive.</span></span>

<span data-ttu-id="a7dc0-170">下图说明了 BMP 与代理项码位之间的关系。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-170">The following diagram illustrates the relationship between the BMP and the surrogate code points.</span></span>

:::image type="content" source="media/:::no-loc(char):::acter-encoding-introduction/bmp-and-surrogate.svg" alt-text="BMP and surrogate code points":::

<span data-ttu-id="a7dc0-172">如果高代理项码位 (`U+D800..U+DBFF`) 后紧跟低代理项码位 (`U+DC00..U+DFFF`)，则通过使用以下公式，此代理项对将解释为补充码位：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-172">When a *high surrogate* code point (`U+D800..U+DBFF`) is immediately followed by a *low surrogate* code point (`U+DC00..U+DFFF`), the pair is interpreted as a supplementary code point by using the following formula:</span></span>

```
code point = 0x10000 +
  ((high surrogate code point - 0xD800) * 0x0400) +
  (low surrogate code point - 0xDC00)
```

<span data-ttu-id="a7dc0-173">下面是使用十进制表示法的相同公式：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-173">Here's the same formula using decimal notation:</span></span>

```
code point = 65,536 +
  ((high surrogate code point - 55,296) * 1,024) +
  (low surrogate code point - 56,320)
```

<span data-ttu-id="a7dc0-174">高代理项码位的数字值不高于低代理项码位的数字值。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-174">A *high* surrogate code point doesn't have a higher number value than a *low* surrogate code point.</span></span> <span data-ttu-id="a7dc0-175">高代理项码位之所以称为“高”，是因为它用于计算完整 21 位码位范围的高阶 11 位。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-175">The high surrogate code point is called "high" because it's used to calculate the higher-order 11 bits of the full 21-bit code point range.</span></span> <span data-ttu-id="a7dc0-176">低代理项码位用于计算低阶 10 位。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-176">The low surrogate code point is used to calculate the lower-order 10 bits.</span></span>

<span data-ttu-id="a7dc0-177">例如，与代理项对对应的实际码位 `0xD83C` 和 `0xDF39` 按如下方式计算：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-177">For example, the actual code point that corresponds to the surrogate pair `0xD83C` and `0xDF39`  is computed as follows:</span></span>

```
actual = 0x10000 + ((0xD83C - 0xD800) * 0x0400) + (0xDF39 - 0xDC00)
       = 0x10000 + (          0x003C  * 0x0400) +           0x0339
       = 0x10000 +                      0xF000  +           0x0339
       = 0x1F339
```

<span data-ttu-id="a7dc0-178">下面是使用十进制表示法的相同计算：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-178">Here's the same calculation using decimal notation:</span></span>

```
actual =  65,536 + ((55,356 - 55,296) * 1,024) + (57,145 - 56320)
       =  65,536 + (              60  * 1,024) +             825
       =  65,536 +                     61,440  +             825
       = 127,801
```

<span data-ttu-id="a7dc0-179">前一个示例展示的 `"\ud83c\udf39"` 是前面提到的 `U+1F339 ROSE ('🌹')` 码位的 UTF-16 编码。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-179">The preceding example demonstrates that `"\ud83c\udf39"` is the UTF-16 encoding of the `U+1F339 ROSE ('🌹')` code point mentioned earlier.</span></span>

## <a name="unicode-scalar-values"></a><span data-ttu-id="a7dc0-180">Unicode 标量值</span><span class="sxs-lookup"><span data-stu-id="a7dc0-180">Unicode scalar values</span></span>

<span data-ttu-id="a7dc0-181">术语“[Unicode 标量值](https://www.unicode.org/glossary/#unicode_scalar_value)”是指除代理项码位之外的所有码位。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-181">The term [Unicode scalar value](https://www.unicode.org/glossary/#unicode_scalar_value) refers to all code points other than the surrogate code points.</span></span> <span data-ttu-id="a7dc0-182">换句话说，标量值是分配有 :::no-loc(char):::acter 或将来可以为其分配 :::no-loc(char):::acter 的任何码位。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-182">In other words, a scalar value is any code point that is assigned a :::no-loc(char):::acter or can be assigned a :::no-loc(char):::acter in the future.</span></span> <span data-ttu-id="a7dc0-183">此处的“字符”是指可以分配给码位的任何内容，其中包括控制文本或 :::no-loc(char):::acter 显示方式的操作。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-183">"Character" here refers to anything that can be assigned to a code point, which includes such things as actions that control how text or :::no-loc(char):::acters are displayed.</span></span>

<span data-ttu-id="a7dc0-184">下图演示了标量值码位。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-184">The following diagram illustrates the scalar value code points.</span></span>

:::image type="content" source="media/:::no-loc(char):::acter-encoding-introduction/scalar-values.svg" alt-text="Scalar values":::

### <a name="the-no-locrune-type-as-a-scalar-value"></a><span data-ttu-id="a7dc0-186">作为标量值的 :::no-loc(Rune)::: 类型</span><span class="sxs-lookup"><span data-stu-id="a7dc0-186">The :::no-loc(Rune)::: type as a scalar value</span></span>

<span data-ttu-id="a7dc0-187">从 .NET Core 3.0 开始，<xref:System.Text.:::no-loc(Rune):::?displayProperty=fullName> 类型表示 Unicode 标量值。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-187">Beginning with .NET Core 3.0, the <xref:System.Text.:::no-loc(Rune):::?displayProperty=fullName> type represents a Unicode scalar value.</span></span> <span data-ttu-id="a7dc0-188">`:::no-loc(Rune):::` 在 .NET Core 2.x 或 .NET Framework 4.x 中不可用。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-188">**`:::no-loc(Rune):::` is not available in .NET Core 2.x or .NET Framework 4.x.**</span></span>

<span data-ttu-id="a7dc0-189">`:::no-loc(Rune):::` 构造函数验证生成的实例是否为有效的 Unicode 标量值，如果无效，则引发异常。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-189">The `:::no-loc(Rune):::` constructors validate that the resulting instance is a valid Unicode scalar value, otherwise they throw an exception.</span></span> <span data-ttu-id="a7dc0-190">下面的示例展示成功实例化 `:::no-loc(Rune):::` 实例的代码，因为输入代表有效的标量值：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-190">The following example shows code that successfully instantiates `:::no-loc(Rune):::` instances because the input represents valid scalar values:</span></span>

<span data-ttu-id="a7dc0-191">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/Instantiate:::no-loc(Rune):::s.cs" id="SnippetValid":::</span><span class="sxs-lookup"><span data-stu-id="a7dc0-191">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/Instantiate:::no-loc(Rune):::s.cs" id="SnippetValid":::</span></span>

<span data-ttu-id="a7dc0-192">下面的示例引发异常，因为码位在代理项范围内，但不是代理项对的一部分：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-192">The following example throws an exception because the code point is in the surrogate range and isn't part of a surrogate pair:</span></span>

<span data-ttu-id="a7dc0-193">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/Instantiate:::no-loc(Rune):::s.cs" id="SnippetInvalidSurrogate":::</span><span class="sxs-lookup"><span data-stu-id="a7dc0-193">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/Instantiate:::no-loc(Rune):::s.cs" id="SnippetInvalidSurrogate":::</span></span>

<span data-ttu-id="a7dc0-194">下面的示例引发异常，因为码位超出了补充范围：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-194">The following example throws an exception because the code point is beyond the supplementary range:</span></span>

<span data-ttu-id="a7dc0-195">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/Instantiate:::no-loc(Rune):::s.cs" id="SnippetInvalidHigh":::</span><span class="sxs-lookup"><span data-stu-id="a7dc0-195">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/Instantiate:::no-loc(Rune):::s.cs" id="SnippetInvalidHigh":::</span></span>

### <a name="no-locrune-usage-example-changing-letter-case"></a><span data-ttu-id="a7dc0-196">:::no-loc(Rune)::: 用法示例：更改字母大小写</span><span class="sxs-lookup"><span data-stu-id="a7dc0-196">:::no-loc(Rune)::: usage example: changing letter case</span></span>

<span data-ttu-id="a7dc0-197">如果 `:::no-loc(char):::` 来自代理项对，则采用 `:::no-loc(char):::` 并假设正在使用作为标量值的码位的 API 将无法正常工作。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-197">An API that takes a `:::no-loc(char):::` and assumes it is working with a code point that is a scalar value doesn't work correctly if the `:::no-loc(char):::` is from a surrogate pair.</span></span> <span data-ttu-id="a7dc0-198">例如，来看看以下方法，此方法对字符串 (:::no-loc(string)::: 中的每个 :::no-loc(char)::: 调用 <xref:System.Char.ToUpperInvariant%2A?displayProperty=nameWithType>：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-198">For example, consider the following method that calls <xref:System.Char.ToUpperInvariant%2A?displayProperty=nameWithType> on each :::no-loc(char)::: in a :::no-loc(string)::::</span></span>

<span data-ttu-id="a7dc0-199">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/ConvertToUpper.cs" id="SnippetBadExample":::</span><span class="sxs-lookup"><span data-stu-id="a7dc0-199">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/ConvertToUpper.cs" id="SnippetBadExample":::</span></span>

<span data-ttu-id="a7dc0-200">如果 `input` 字符串 (:::no-loc(string):::) 包含小写德塞莱特文字母 `er` (`𐑉`)，则此代码不会将其转换为大写形式 (`𐐡`)。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-200">If the `input` :::no-loc(string)::: contains the lowercase Deseret letter `er` (`𐑉`), this code won't convert it to uppercase (`𐐡`).</span></span> <span data-ttu-id="a7dc0-201">此代码对代理项码位 `U+D801` 和 `U+DC49` 分别调用 `:::no-loc(char):::.ToUpperInvariant`。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-201">The code calls `:::no-loc(char):::.ToUpperInvariant` separately on each surrogate code point, `U+D801` and `U+DC49`.</span></span> <span data-ttu-id="a7dc0-202">但 `U+D801` 本身没有足够的信息将其标识为小写字母，因此 `:::no-loc(char):::.ToUpperInvariant` 将其保持不变。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-202">But `U+D801` doesn't have enough information by itself to identify it as a lowercase letter, so `:::no-loc(char):::.ToUpperInvariant` leaves it alone.</span></span> <span data-ttu-id="a7dc0-203">它以相同的方式处理 `U+DC49`。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-203">And it handles `U+DC49` the same way.</span></span> <span data-ttu-id="a7dc0-204">结果是 `input` 字符串 (:::no-loc(string):::) 中的小写“𐑉”不会转换为大写的“𐑉”。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-204">The result is that lowercase '𐑉' in the `input` :::no-loc(string)::: doesn't get converted to uppercase '𐐡'.</span></span>

<span data-ttu-id="a7dc0-205">以下两个选项可用于将字符串 ( :::no-loc(string):::) 正确地转换为大写形式：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-205">Here are two options for correctly converting a :::no-loc(string)::: to uppercase:</span></span>

* <span data-ttu-id="a7dc0-206">对 input 字符串 (:::no-loc(string):::) 调用 <xref:System.String.ToUpperInvariant%2A?displayProperty=nameWithType>，而不是循环访问（一个 `:::no-loc(char):::` 接着一个 `:::no-loc(char):::`）。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-206">Call <xref:System.String.ToUpperInvariant%2A?displayProperty=nameWithType> on the input :::no-loc(string)::: rather than iterating `:::no-loc(char):::`-by-`:::no-loc(char):::`.</span></span> <span data-ttu-id="a7dc0-207">`:::no-loc(string):::.ToUpperInvariant` 方法可以访问每个代理项对的两个部分，因此它可以正确地处理所有 Unicode 码位。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-207">The `:::no-loc(string):::.ToUpperInvariant` method has access to both parts of each surrogate pair, so it can handle all Unicode code points correctly.</span></span>
* <span data-ttu-id="a7dc0-208">循环访问 Unicode 标量值作为 `:::no-loc(Rune):::` 实例，而不是 `:::no-loc(char):::` 实例，如以下示例中所示。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-208">Iterate through the Unicode scalar values as `:::no-loc(Rune):::` instances instead of `:::no-loc(char):::` instances, as shown in the following example.</span></span> <span data-ttu-id="a7dc0-209">由于 `:::no-loc(Rune):::` 实例是有效的 Unicode 标量值，因此可将其传递给应对标量值执行操作的 API。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-209">Since a `:::no-loc(Rune):::` instance is a valid Unicode scalar value, it can be passed to APIs that expect to operate on a scalar value.</span></span> <span data-ttu-id="a7dc0-210">例如，如以下示例中所示，调用 <xref:System.Text.:::no-loc(Rune):::.ToUpperInvariant%2A?displayProperty=nameWithType> 可以得到正确的结果：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-210">For example, calling <xref:System.Text.:::no-loc(Rune):::.ToUpperInvariant%2A?displayProperty=nameWithType> as shown in the following example gives correct results:</span></span>

  <span data-ttu-id="a7dc0-211">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/ConvertToUpper.cs" id="SnippetGoodExample":::</span><span class="sxs-lookup"><span data-stu-id="a7dc0-211">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/ConvertToUpper.cs" id="SnippetGoodExample":::</span></span>

### <a name="other-no-locrune-apis"></a><span data-ttu-id="a7dc0-212">其他 :::no-loc(Rune)::: API</span><span class="sxs-lookup"><span data-stu-id="a7dc0-212">Other :::no-loc(Rune)::: APIs</span></span>

<span data-ttu-id="a7dc0-213">`:::no-loc(Rune):::` 类型公开了许多 `:::no-loc(char):::` API 的类似 API。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-213">The `:::no-loc(Rune):::` type exposes analogs of many of the `:::no-loc(char):::` APIs.</span></span> <span data-ttu-id="a7dc0-214">例如，以下方法在 `:::no-loc(char):::` 类型上镜像静态 API：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-214">For example, the following methods mirror static APIs on the `:::no-loc(char):::` type:</span></span>

* <xref:System.Text.:::no-loc(Rune):::.IsLetter%2A?displayProperty=nameWithType>
* <xref:System.Text.:::no-loc(Rune):::.IsWhiteSpace%2A?displayProperty=nameWithType>
* <xref:System.Text.:::no-loc(Rune):::.IsLetterOrDigit%2A?displayProperty=nameWithType>
* <xref:System.Text.:::no-loc(Rune):::.GetUnicodeCategory%2A?displayProperty=nameWithType>

<span data-ttu-id="a7dc0-215">若要从 `:::no-loc(Rune):::` 实例获取原始标量值，请使用 <xref:System.Text.:::no-loc(Rune):::.Value%2A?displayProperty=nameWithType> 属性。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-215">To get the raw scalar value from a `:::no-loc(Rune):::` instance, use the <xref:System.Text.:::no-loc(Rune):::.Value%2A?displayProperty=nameWithType> property.</span></span>

<span data-ttu-id="a7dc0-216">若要将 `:::no-loc(Rune):::` 实例转换回一连串 `:::no-loc(char):::`，请使用 <xref:System.Text.:::no-loc(Rune):::.ToString%2A?displayProperty=nameWithType> 或 <xref:System.Text.:::no-loc(Rune):::.EncodeToUtf16%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-216">To convert a `:::no-loc(Rune):::` instance back to a sequence of `:::no-loc(char):::`s, use <xref:System.Text.:::no-loc(Rune):::.ToString%2A?displayProperty=nameWithType> or the <xref:System.Text.:::no-loc(Rune):::.EncodeToUtf16%2A?displayProperty=nameWithType> method.</span></span>

<span data-ttu-id="a7dc0-217">由于任何 Unicode 标量值都可以由单个 `:::no-loc(char):::` 或代理项对表示，因此任何 `:::no-loc(Rune):::` 实例最多可由 2 个 `:::no-loc(char):::` 实例表示。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-217">Since any Unicode scalar value is representable by a single `:::no-loc(char):::` or by a surrogate pair, any `:::no-loc(Rune):::` instance can be represented by at most 2 `:::no-loc(char):::` instances.</span></span> <span data-ttu-id="a7dc0-218">使用 <xref:System.Text.:::no-loc(Rune):::.Utf16SequenceLength%2A?displayProperty=nameWithType> 查看表示 `:::no-loc(Rune):::` 实例所需的 `:::no-loc(char):::` 实例数目。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-218">Use <xref:System.Text.:::no-loc(Rune):::.Utf16SequenceLength%2A?displayProperty=nameWithType> to see how many `:::no-loc(char):::` instances are required to represent a `:::no-loc(Rune):::` instance.</span></span>

<span data-ttu-id="a7dc0-219">有关 .NET `:::no-loc(Rune):::` 类型的详细信息，请参阅 [`:::no-loc(Rune):::` API 参考](xref:System.Text.:::no-loc(Rune):::)。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-219">For more information about the .NET `:::no-loc(Rune):::` type, see the [`:::no-loc(Rune):::` API reference](xref:System.Text.:::no-loc(Rune):::).</span></span>

## <a name="grapheme-clusters"></a><span data-ttu-id="a7dc0-220">字形群集</span><span class="sxs-lookup"><span data-stu-id="a7dc0-220">Grapheme clusters</span></span>

<span data-ttu-id="a7dc0-221">看起来像一个 :::no-loc(char):::acter 的内容可能由多个码位组合而成，因此，相比“:::no-loc(char):::acter”，“[字形群集](https://www.unicode.org/glossary/#grapheme_cluster)”术语的表述通常更贴合。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-221">What looks like one :::no-loc(char):::acter might result from a combination of multiple code points, so a more descriptive term that is often used in place of ":::no-loc(char):::acter" is [grapheme cluster](https://www.unicode.org/glossary/#grapheme_cluster).</span></span> <span data-ttu-id="a7dc0-222">在 .NET 中使用“[文本元素](xref:System.Globalization.StringInfo.GetTextElementEnumerator%2A)”术语表示相同的内容。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-222">The equivalent term in .NET is [text element](xref:System.Globalization.StringInfo.GetTextElementEnumerator%2A).</span></span>

<span data-ttu-id="a7dc0-223">比如，`:::no-loc(string):::` 实例“a”、“á”、“á”和“`👩🏽‍🚒`”。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-223">Consider the `:::no-loc(string):::` instances "a", "á", "á", and "`👩🏽‍🚒`".</span></span> <span data-ttu-id="a7dc0-224">如果你的操作系统按照 Unicode 标准指定的方式来处理，则这些 `:::no-loc(string):::` 实例中的每个实例都将显示为单个文本元素或字形群集。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-224">If your operating system handles them as specified by the Unicode standard, each of these `:::no-loc(string):::` instances appears as a single text element or grapheme cluster.</span></span> <span data-ttu-id="a7dc0-225">但最后两个实例用多个标量值码位表示。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-225">But the last two are represented by more than one scalar value code point.</span></span>

* <span data-ttu-id="a7dc0-226">字符串 (:::no-loc(string):::)“a”由一个标量值表示，并包含一个 `:::no-loc(char):::` 实例。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-226">The :::no-loc(string)::: "a" is represented by one scalar value and contains one `:::no-loc(char):::` instance.</span></span>

  * `U+0061 LATIN SMALL LETTER A`

* <span data-ttu-id="a7dc0-227">字符串 (:::no-loc(string):::)“á”由一个标量值表示，并包含一个 `:::no-loc(char):::` 实例。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-227">The :::no-loc(string)::: "á" is represented by one scalar value and contains one `:::no-loc(char):::` instance.</span></span>

  * `U+00E1 LATIN SMALL LETTER A WITH ACUTE`

* <span data-ttu-id="a7dc0-228">字符串 (:::no-loc(string):::)“á”看起来与“á”相同，但由两个标量值表示，并包含两个 `:::no-loc(char):::` 实例。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-228">The :::no-loc(string)::: "á" looks the same as "á" but is represented by two scalar values and contains two `:::no-loc(char):::` instances.</span></span>

  * `U+0061 LATIN SMALL LETTER A`
  * `U+0301 COMBINING ACUTE ACCENT`

* <span data-ttu-id="a7dc0-229">最后，字符串 (:::no-loc(string):::)“`👩🏽‍🚒`”由四个标量值表示，并包含七个 `:::no-loc(char):::` 实例。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-229">Finally, the :::no-loc(string)::: "`👩🏽‍🚒`" is represented by four scalar values and contains seven `:::no-loc(char):::` instances.</span></span>

  * <span data-ttu-id="a7dc0-230">`U+1F469 WOMAN`（补充范围，需要一个代理项对）</span><span class="sxs-lookup"><span data-stu-id="a7dc0-230">`U+1F469 WOMAN` (supplementary range, requires a surrogate pair)</span></span>
  * <span data-ttu-id="a7dc0-231">`U+1F3FD EMOJI MODIFIER FITZPATRICK TYPE-4`（补充范围，需要一个代理项对）</span><span class="sxs-lookup"><span data-stu-id="a7dc0-231">`U+1F3FD EMOJI MODIFIER FITZPATRICK TYPE-4` (supplementary range, requires a surrogate pair)</span></span>
  * `U+200D ZERO WIDTH JOINER`
  * <span data-ttu-id="a7dc0-232">`U+1F692 FIRE ENGINE`（补充范围，需要一个代理项对）</span><span class="sxs-lookup"><span data-stu-id="a7dc0-232">`U+1F692 FIRE ENGINE` (supplementary range, requires a surrogate pair)</span></span>

<span data-ttu-id="a7dc0-233">在前面的一些示例中（例如组合的重音修饰符或肤色修饰符），码位不会在屏幕上显示为独立元素。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-233">In some of the preceding examples - such as the combining accent modifier or the skin tone modifier - the code point does not display as a standalone element on the screen.</span></span> <span data-ttu-id="a7dc0-234">相反，它用于修改之前出现的文本元素的外观。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-234">Rather, it serves to modify the appearance of a text element that came before it.</span></span> <span data-ttu-id="a7dc0-235">这些示例表明，可能需要采用多个标量值来构成我们认为的单个“:::no-loc(char):::acter”或“字形群集”。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-235">These examples show that it might take multiple scalar values to make up what we think of as a single ":::no-loc(char):::acter," or "grapheme cluster."</span></span>

<span data-ttu-id="a7dc0-236">若要枚举 `:::no-loc(string):::` 的字形群集，请使用 <xref:System.Globalization.StringInfo> 类，如下面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-236">To enumerate the grapheme clusters of a `:::no-loc(string):::`, use the <xref:System.Globalization.StringInfo> class as shown in the following example.</span></span> <span data-ttu-id="a7dc0-237">如果你熟悉 Swift，那么 .NET `StringInfo` 类型在概念上类似于 [Swift `:::no-loc(char):::acter` 类型](https://developer.apple.com/documentation/swift/:::no-loc(char):::acter)。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-237">If you're familiar with Swift, the .NET `StringInfo` type is conceptually similar to [Swift's `:::no-loc(char):::acter` type](https://developer.apple.com/documentation/swift/:::no-loc(char):::acter).</span></span>

### <a name="example-count-no-locchar-no-locrune-and-text-element-instances"></a><span data-ttu-id="a7dc0-238">示例：:::no-loc(char):::、:::no-loc(Rune)::: 和文本元素实例计数</span><span class="sxs-lookup"><span data-stu-id="a7dc0-238">Example: count :::no-loc(char):::, :::no-loc(Rune):::, and text element instances</span></span>

<span data-ttu-id="a7dc0-239">在 .NET API 中，字形群集称为“文本元素”。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-239">In .NET APIs, a grapheme cluster is called a *text element*.</span></span> <span data-ttu-id="a7dc0-240">下面的方法演示 `:::no-loc(string):::`中 `:::no-loc(char):::`、`:::no-loc(Rune):::` 和文本元素实例之间的差异：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-240">The following method demonstrates the differences between `:::no-loc(char):::`, `:::no-loc(Rune):::`, and text element instances in a `:::no-loc(string):::`:</span></span>

<span data-ttu-id="a7dc0-241">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/CountTextElements.cs" id="SnippetCountMethod":::</span><span class="sxs-lookup"><span data-stu-id="a7dc0-241">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/CountTextElements.cs" id="SnippetCountMethod":::</span></span>

<span data-ttu-id="a7dc0-242">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/CountTextElements.cs" id="SnippetCallCountMethod":::</span><span class="sxs-lookup"><span data-stu-id="a7dc0-242">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/CountTextElements.cs" id="SnippetCallCountMethod":::</span></span>

<span data-ttu-id="a7dc0-243">如果在 .NET Framework 或 .NET Core 3.1 或更早版本中运行此代码，表情符号的文本元素计数将显示 `4`。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-243">If you run this code in .NET Framework or .NET Core 3.1 or earlier, the text element count for the emoji shows `4`.</span></span> <span data-ttu-id="a7dc0-244">这是由于 `StringInfo` 类中的 bug 所致（已在 .NET 5 中修复）。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-244">That is due to a bug in the `StringInfo` class that is fixed in .NET 5.</span></span>

### <a name="example-splitting-no-locstring-instances"></a><span data-ttu-id="a7dc0-245">示例：拆分 :::no-loc(string)::: 实例</span><span class="sxs-lookup"><span data-stu-id="a7dc0-245">Example: splitting :::no-loc(string)::: instances</span></span>

<span data-ttu-id="a7dc0-246">拆分 `:::no-loc(string):::` 实例时，请避免拆分代理项对和字形群集。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-246">When splitting `:::no-loc(string):::` instances, avoid splitting surrogate pairs and grapheme clusters.</span></span> <span data-ttu-id="a7dc0-247">下面的示例展示不正确的代码，此代码的目的是在 :::no-loc(string)::: 中每隔 10 个 :::no-loc(char):::acter 插入一个换行符：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-247">Consider the following example of incorrect code, which intends to insert line breaks every 10 :::no-loc(char):::acters in a :::no-loc(string)::::</span></span>

<span data-ttu-id="a7dc0-248">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/InsertNewlines.cs" id="SnippetBadExample":::</span><span class="sxs-lookup"><span data-stu-id="a7dc0-248">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/InsertNewlines.cs" id="SnippetBadExample":::</span></span>

<span data-ttu-id="a7dc0-249">由于此代码枚举 `:::no-loc(char):::` 实例，因此会拆分一个跨越 10 个 `:::no-loc(char):::` 边界的代理项对，并在它们之间插入一个换行符。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-249">Because this code enumerates `:::no-loc(char):::` instances, a surrogate pair that happens to straddle a 10-`:::no-loc(char):::` boundary will be split and a newline injected between them.</span></span> <span data-ttu-id="a7dc0-250">这种插入会导致数据损坏，因为代理项码位只有在作为代理项对时才具有意义。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-250">This insertion introduces data corruption, because surrogate code points are meaningful only as pairs.</span></span>

<span data-ttu-id="a7dc0-251">如果枚举 `:::no-loc(Rune):::` 实例（标量值）而不是 `:::no-loc(char):::` 实例，仍可能损坏数据。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-251">The potential for data corruption isn't eliminated if you enumerate `:::no-loc(Rune):::` instances (scalar values) instead of `:::no-loc(char):::` instances.</span></span> <span data-ttu-id="a7dc0-252">一组 `:::no-loc(Rune):::` 实例可能构成跨越 10 个 `:::no-loc(char):::` 边界的字形群集。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-252">A set of `:::no-loc(Rune):::` instances might make up a grapheme cluster that straddles a 10-`:::no-loc(char):::` boundary.</span></span> <span data-ttu-id="a7dc0-253">如果一组字形群集被拆分开，就不再有效。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-253">If the grapheme cluster set is split up, it can't be interpreted correctly.</span></span>

<span data-ttu-id="a7dc0-254">更好的方法是通过对字形群集或文本元素进行计数来中断 :::no-loc(string):::，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-254">A better approach is to break the :::no-loc(string)::: by counting grapheme clusters, or text elements, as in the following example:</span></span>

<span data-ttu-id="a7dc0-255">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/InsertNewlines.cs" id="SnippetGoodExample":::</span><span class="sxs-lookup"><span data-stu-id="a7dc0-255">:::code language="csharp" source="snippets/:::no-loc(char):::acter-encoding-introduction/csharp/InsertNewlines.cs" id="SnippetGoodExample":::</span></span>

<span data-ttu-id="a7dc0-256">但是，如前所述，在 .NET（而非 .NET 5）的实现中，`StringInfo` 类可能会错误地处理某些字形群集。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-256">As noted earlier, however, in implementations of .NET other than .NET 5, the `StringInfo` class might handle some grapheme clusters incorrectly.</span></span>

## <a name="utf-8-and-utf-32"></a><span data-ttu-id="a7dc0-257">UTF-8 和 UTF-32</span><span class="sxs-lookup"><span data-stu-id="a7dc0-257">UTF-8 and UTF-32</span></span>

<span data-ttu-id="a7dc0-258">前面几节着重于介绍 UTF-16，因为 .NET 要使用它对 `:::no-loc(string):::` 实例进行编码。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-258">The preceding sections focused on UTF-16 because that's what .NET uses to encode `:::no-loc(string):::` instances.</span></span> <span data-ttu-id="a7dc0-259">Unicode 还有其他编码系统：即 [UTF-8](https://www.unicode.org/faq/utf_bom.html#UTF8) 和 [UTF-32](https://www.unicode.org/faq/utf_bom.html#UTF32)。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-259">There are other encoding systems for Unicode - [UTF-8](https://www.unicode.org/faq/utf_bom.html#UTF8) and [UTF-32](https://www.unicode.org/faq/utf_bom.html#UTF32).</span></span> <span data-ttu-id="a7dc0-260">这些编码分别使用 8 位代码单位和 32 位代码单位。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-260">These encodings use 8-bit code units and 32-bit code units, respectively.</span></span>

<span data-ttu-id="a7dc0-261">与 UTF-16 类似，UTF-8 需要使用多个代码单位表示某些 Unicode 标量值。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-261">Like UTF-16, UTF-8 requires multiple code units to represent some Unicode scalar values.</span></span> <span data-ttu-id="a7dc0-262">UTF-32 可以表示单个 32 位代码单位中的任何标量值。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-262">UTF-32 can represent any scalar value in a single 32-bit code unit.</span></span>

<span data-ttu-id="a7dc0-263">下面的示例展示如何分别使用这三个 Unicode 编码系统表示同一个 Unicode 码位：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-263">Here are some examples showing how the same Unicode code point is represented in each of these three Unicode encoding systems:</span></span>

```
Scalar: U+0061 LATIN SMALL LETTER A ('a')
UTF-8 : [ 61 ]           (1x  8-bit code unit  = 8 bits total)
UTF-16: [ 0061 ]         (1x 16-bit code unit  = 16 bits total)
UTF-32: [ 00000061 ]     (1x 32-bit code unit  = 32 bits total)

Scalar: U+0429 CYRILLIC CAPITAL LETTER SHCHA ('Щ')
UTF-8 : [ D0 A9 ]        (2x  8-bit code units = 16 bits total)
UTF-16: [ 0429 ]         (1x 16-bit code unit  = 16 bits total)
UTF-32: [ 00000429 ]     (1x 32-bit code unit  = 32 bits total)

Scalar: U+A992 JAVANESE LETTER GA ('ꦒ')
UTF-8 : [ EA A6 92 ]     (3x  8-bit code units = 24 bits total)
UTF-16: [ A992 ]         (1x 16-bit code unit  = 16 bits total)
UTF-32: [ 0000A992 ]     (1x 32-bit code unit  = 32 bits total)

Scalar: U+104CC OSAGE CAPITAL LETTER TSHA ('𐓌')
UTF-8 : [ F0 90 93 8C ]  (4x  8-bit code units = 32 bits total)
UTF-16: [ D801 DCCC ]    (2x 16-bit code units = 32 bits total)
UTF-32: [ 000104CC ]     (1x 32-bit code unit  = 32 bits total)
```

<span data-ttu-id="a7dc0-264">如前文所述，[代理项对](#surrogate-pairs)中的单个 UTF-16 代码单位本身是没有意义的。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-264">As noted earlier, a single UTF-16 code unit from a [surrogate pair](#surrogate-pairs) is meaningless by itself.</span></span> <span data-ttu-id="a7dc0-265">同样，如果单个 UTF-8 代码单位处于由两个、三个或四个用于计算标量值的一连串代码单位中，那么它自身也毫无意义。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-265">In the same way, a single UTF-8 code unit is meaningless by itself if it's in a sequence of two, three, or four used to calculate a scalar value.</span></span>

### <a name="endianness"></a><span data-ttu-id="a7dc0-266">字节排序方式</span><span class="sxs-lookup"><span data-stu-id="a7dc0-266">Endianness</span></span>

<span data-ttu-id="a7dc0-267">在 .NET 中，:::no-loc(string)::: 的 UTF-16 代码单位以 16 位整数（`:::no-loc(char):::` 实例）的序列形式存储在连续内存中。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-267">In .NET, the UTF-16 code units of a :::no-loc(string)::: are stored in contiguous memory as a sequence of 16-bit integers (`:::no-loc(char):::` instances).</span></span> <span data-ttu-id="a7dc0-268">各个代码单位的位数根据当前体系结构的[字节顺序](https://en.wikipedia.org/wiki/Endianness)布局。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-268">The bits of individual code units are laid out according to the [endianness](https://en.wikipedia.org/wiki/Endianness) of the current architecture.</span></span>

<span data-ttu-id="a7dc0-269">在 little-endian 体系结构中，由 UTF-16 码位 `[ D801 DCCC ]` 组成的 :::no-loc(string)::: 会在内存中以 `[ 0x01, 0xD8, 0xCC, 0xDC ]` 字节进行布局。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-269">On a little-endian architecture, the :::no-loc(string)::: consisting of the UTF-16 code points `[ D801 DCCC ]` would be laid out in memory as the bytes `[ 0x01, 0xD8, 0xCC, 0xDC ]`.</span></span> <span data-ttu-id="a7dc0-270">在 big-endian 体系结构中，同一 :::no-loc(string)::: 将在内存中以 `[ 0xD8, 0x01, 0xDC, 0xCC ]` 字节进行布局。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-270">On a big-endian architecture that same :::no-loc(string)::: would be laid out in memory as the bytes `[ 0xD8, 0x01, 0xDC, 0xCC ]`.</span></span>

<span data-ttu-id="a7dc0-271">相互通信的计算机系统必须就跨网络数据的表示形式达成共识。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-271">Computer systems that communicate with each other must agree on the representation of data crossing the wire.</span></span> <span data-ttu-id="a7dc0-272">大多数网络协议在传输文本时都使用 UTF-8 标准，部分原因是为了避免 big-endian 计算机与 little-endian 计算机通信可能导致的问题。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-272">Most network protocols use UTF-8 as a standard when transmitting text, partly to avoid issues that might result from a big-endian machine communicating with a little-endian machine.</span></span> <span data-ttu-id="a7dc0-273">不管字节顺序如何，由 UTF-8 码位 `[ F0 90 93 8C ]` 组成的 :::no-loc(string)::: 将始终表示为字节 `[ 0xF0, 0x90, 0x93, 0x8C ]`。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-273">The :::no-loc(string)::: consisting of the UTF-8 code points `[ F0 90 93 8C ]` will always be represented as the bytes `[ 0xF0, 0x90, 0x93, 0x8C ]` regardless of endianness.</span></span>

<span data-ttu-id="a7dc0-274">若要使用 UTF-8 传输文本，.NET 应用程序通常使用类似于以下示例的代码：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-274">To use UTF-8 for transmitting text, .NET applications often use code like the following example:</span></span>

```csharp
:::no-loc(string)::: :::no-loc(string):::ToWrite = GetString();
byte[] :::no-loc(string):::AsUtf8Bytes = Encoding.UTF8.GetBytes(:::no-loc(string):::ToWrite);
await outputStream.WriteAsync(:::no-loc(string):::AsUtf8Bytes, 0, :::no-loc(string):::AsUtf8Bytes.Length);
```

<span data-ttu-id="a7dc0-275">在前面的示例中，方法 [Encoding.UTF8.GetBytes](xref:System.Text.UTF8Encoding.GetBytes%2A) 将 UTF-16 `:::no-loc(string):::` 解码回一系列 Unicode 标量值，然后将这些标量值重新编码为 UTF-8，并将生成的序列放入 `byte` 数组。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-275">In the preceding example, the method [Encoding.UTF8.GetBytes](xref:System.Text.UTF8Encoding.GetBytes%2A) decodes the UTF-16 `:::no-loc(string):::` back into a series of Unicode scalar values, then it re-encodes those scalar values into UTF-8 and places the resulting sequence into a `byte` array.</span></span> <span data-ttu-id="a7dc0-276">[Encoding.UTF8.GetString](xref:System.Text.UTF8Encoding.GetString%2A) 方法执行相反的转换，将 UTF-8 `byte` 数组转换为 UTF-16 `:::no-loc(string):::`。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-276">The method [Encoding.UTF8.GetString](xref:System.Text.UTF8Encoding.GetString%2A) performs the opposite transformation, converting a UTF-8 `byte` array to a UTF-16 `:::no-loc(string):::`.</span></span>

> [!WARNING]
> <span data-ttu-id="a7dc0-277">由于 UTF-8 在 Internet 上很普遍，因此从网络读取原始字节并将数据视为 UTF-8 会很有吸引力。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-277">Since UTF-8 is commonplace on the internet, it may be tempting to read raw bytes from the wire and to treat the data as if it were UTF-8.</span></span> <span data-ttu-id="a7dc0-278">但是，应验证它的格式是否正确。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-278">However, you should validate that it is indeed well-formed.</span></span> <span data-ttu-id="a7dc0-279">恶意客户端可能向你的服务提交格式错误的 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-279">A malicious client might submit ill-formed UTF-8 to your service.</span></span> <span data-ttu-id="a7dc0-280">如果你按正确的格式处理数据，可能会导致应用程序出错或存在安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-280">If you operate on that data as if it were well-formed, it could cause errors or security holes in your application.</span></span> <span data-ttu-id="a7dc0-281">要验证 UTF-8 数据，可以使用类似于 `Encoding.UTF8.GetString` 的方法，此方法在将传入数据转换为 `:::no-loc(string):::` 时将执行验证。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-281">To validate UTF-8 data, you can use a method like `Encoding.UTF8.GetString`, which will perform validation while converting the incoming data to a `:::no-loc(string):::`.</span></span>

### <a name="well-formed-encoding"></a><span data-ttu-id="a7dc0-282">格式正确的编码</span><span class="sxs-lookup"><span data-stu-id="a7dc0-282">Well-formed encoding</span></span>

<span data-ttu-id="a7dc0-283">格式正确的 Unicode 编码是一串 (:::no-loc(string):::) 代码单位，可以将它毫无歧义地正确解码为一系列 Unicode 标量值。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-283">A well-formed Unicode encoding is a :::no-loc(string)::: of code units that can be decoded unambiguously and without error into a sequence of Unicode scalar values.</span></span> <span data-ttu-id="a7dc0-284">格式正确的数据可以在 UTF-8、UTF-16 和 UTF-32 之间自由地来回转码。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-284">Well-formed data can be transcoded freely back and forth between UTF-8, UTF-16, and UTF-32.</span></span>

<span data-ttu-id="a7dc0-285">编码序列格式是否正确的问题与计算机体系结构的字节顺序无关。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-285">The question of whether an encoding sequence is well-formed or not is unrelated to the endianness of a machine's architecture.</span></span> <span data-ttu-id="a7dc0-286">在 big-endian 和 little-endian 计算机上，格式错误的 UTF-8 序列都具有相同的错误方式。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-286">An ill-formed UTF-8 sequence is ill-formed in the same way on both big-endian and little-endian machines.</span></span>

<span data-ttu-id="a7dc0-287">以下是一些格式错误的编码示例：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-287">Here are some examples of ill-formed encodings:</span></span>

* <span data-ttu-id="a7dc0-288">在 UTF-8 中，序列 `[ 6C C2 61 ]` 格式错误，因为 `C2` 后面不能跟有 `61`。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-288">In UTF-8, the sequence `[ 6C C2 61 ]` is ill-formed because `C2` cannot be followed by `61`.</span></span>

* <span data-ttu-id="a7dc0-289">在 UTF-16 中，序列 `[ DC00 DD00 ]`（或者，在 C# 中为字符串 (:::no-loc(string):::) `"\udc00\udd00"`）格式错误，因为低代理项 `DC00` 后面不能跟有另一个低代理项 `DD00`。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-289">In UTF-16, the sequence `[ DC00 DD00 ]` (or, in C#, the :::no-loc(string)::: `"\udc00\udd00"`) is ill-formed because the low surrogate `DC00` cannot be followed by another low surrogate `DD00`.</span></span>

* <span data-ttu-id="a7dc0-290">在 UTF-32 中，序列 `[ 0011ABCD ]` 格式错误，因为 `0011ABCD` 不在 Unicode 标量值的范围内。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-290">In UTF-32, the sequence `[ 0011ABCD ]` is ill-formed because `0011ABCD` is outside the range of Unicode scalar values.</span></span>

<span data-ttu-id="a7dc0-291">在 .NET 中，`:::no-loc(string):::` 实例几乎总是包含格式正确的 UTF-16 数据，但也不能百分之百地保证。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-291">In .NET, `:::no-loc(string):::` instances almost always contain well-formed UTF-16 data, but that isn't guaranteed.</span></span> <span data-ttu-id="a7dc0-292">以下示例展示有效的 C# 代码在 `:::no-loc(string):::` 实例中创建格式不正确的 UTF-16 数据。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-292">The following examples show valid C# code that creates ill-formed UTF-16 data in `:::no-loc(string):::` instances.</span></span>

* <span data-ttu-id="a7dc0-293">格式错误的文字：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-293">An ill-formed literal:</span></span>

  ```csharp
  const :::no-loc(string)::: s = "\ud800";
  ```

* <span data-ttu-id="a7dc0-294">拆分代理项对的 sub:::no-loc(string):::：</span><span class="sxs-lookup"><span data-stu-id="a7dc0-294">A sub:::no-loc(string)::: that splits up a surrogate pair:</span></span>

  ```csharp
  :::no-loc(string)::: x = "\ud83e\udd70"; // "🥰"
  :::no-loc(string)::: y = x.Sub:::no-loc(string):::(1, 1); // "\udd70" standalone low surrogate
  ```

<span data-ttu-id="a7dc0-295">像 [`Encoding.UTF8.GetString`](xref:System.Text.UTF8Encoding.GetString%2A) 这样的 API 永远不会返回格式错误的 `:::no-loc(string):::` 实例。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-295">APIs like [`Encoding.UTF8.GetString`](xref:System.Text.UTF8Encoding.GetString%2A) never return ill-formed `:::no-loc(string):::` instances.</span></span> <span data-ttu-id="a7dc0-296">`Encoding.GetString` 和 `Encoding.GetBytes` 方法检测输入中格式错误的序列，并在生成输出时执行 :::no-loc(char):::acter 替换。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-296">`Encoding.GetString` and `Encoding.GetBytes` methods detect ill-formed sequences in the input and perform :::no-loc(char):::acter substitution when generating the output.</span></span> <span data-ttu-id="a7dc0-297">例如，如果 [`Encoding.ASCII.GetString(byte[])`](xref:System.Text.ASCIIEncoding.GetString%2A) 在输入中发现非 ASCII 字节（超出 U+0000..U+007F 的范围），它会在返回的 `:::no-loc(string):::` 实例中插入一个“?”。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-297">For example, if [`Encoding.ASCII.GetString(byte[])`](xref:System.Text.ASCIIEncoding.GetString%2A) sees a non-ASCII byte in the input (outside the range U+0000..U+007F), it inserts a '?' into the returned `:::no-loc(string):::` instance.</span></span> <span data-ttu-id="a7dc0-298">[`Encoding.UTF8.GetString(byte[])`](xref:System.Text.UTF8Encoding.GetString%2A) 在返回的 `:::no-loc(string):::` 实例中将格式错误的 UTF-8 序列替换为 `U+FFFD REPLACEMENT CHARACTER ('�')`。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-298">[`Encoding.UTF8.GetString(byte[])`](xref:System.Text.UTF8Encoding.GetString%2A) replaces ill-formed UTF-8 sequences with `U+FFFD REPLACEMENT CHARACTER ('�')` in the returned `:::no-loc(string):::` instance.</span></span> <span data-ttu-id="a7dc0-299">有关详细信息，请参阅 5.22 和 3.9 小节中的 [Unicode 标准](https://www.unicode.org/versions/latest/)。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-299">For more information, see [the Unicode Standard](https://www.unicode.org/versions/latest/), Sections 5.22 and 3.9.</span></span>

<span data-ttu-id="a7dc0-300">在出现格式错误的序列时，也可以将内置 `Encoding` 类配置为引发异常，而不是执行 :::no-loc(char):::acter 替换。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-300">The built-in `Encoding` classes can also be configured to throw an exception rather than perform :::no-loc(char):::acter substitution when ill-formed sequences are seen.</span></span> <span data-ttu-id="a7dc0-301">在可能无法接受 :::no-loc(char):::acter 替换的安全敏感的应用程序中，通常可以使用这种方法。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-301">This approach is often used in security-sensitive applications where :::no-loc(char):::acter substitution might not be acceptable.</span></span>

```csharp
byte[] utf8Bytes = ReadFromNetwork();
UTF8Encoding encoding = new UTF8Encoding(encoderShouldEmitUTF8Identifier: false, throwOnInvalidBytes: true);
:::no-loc(string)::: asString = encoding.GetString(utf8Bytes); // will throw if 'utf8Bytes' is ill-formed
```

<span data-ttu-id="a7dc0-302">要了解如何使用内置 `Encoding` 类，请参阅[如何在 .NET 中使用 :::no-loc(char):::acter 编码类](:::no-loc(char):::acter-encoding.md)。</span><span class="sxs-lookup"><span data-stu-id="a7dc0-302">For information about how to use the built-in `Encoding` classes, see [How to use :::no-loc(char):::acter encoding classes in .NET](:::no-loc(char):::acter-encoding.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="a7dc0-303">请参阅</span><span class="sxs-lookup"><span data-stu-id="a7dc0-303">See also</span></span>

- <xref:System.String>
- <xref:System.Char>
- <xref:System.Text.:::no-loc(Rune):::>
- [<span data-ttu-id="a7dc0-304">全球化和本地化</span><span class="sxs-lookup"><span data-stu-id="a7dc0-304">Globalization and Localization</span></span>](../globalization-localization/index.md)
