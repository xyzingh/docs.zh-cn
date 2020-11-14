---
title: 使用 String.Split 拆分字符串（C# 指南）
description: Split 方法返回从一组分隔符中拆分的字符串数组。 这是从字符串中提取子字符串的一种简单方法。
ms.date: 01/03/2018
helpviewer_keywords:
- splitting strings [C#]
- Split method [C#]
- strings [C#], splitting
- parse strings
ms.assetid: 729c2923-4169-41c6-9c90-ef176c1e2953
ms.custom: mvc
ms.openlocfilehash: 5361a3c60905edd19b180c5ddb14064a85f64337
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400495"
---
# <a name="how-to-separate-strings-using-stringsplit-in-c"></a><span data-ttu-id="7df16-104">如何在 C\# 中使用 String.Split 分隔字符串</span><span class="sxs-lookup"><span data-stu-id="7df16-104">How to separate strings using String.Split in C\#</span></span>

<span data-ttu-id="7df16-105"><xref:System.String.Split%2A?displayProperty=nameWithType> 方法通过基于一个或多个分隔符拆分输入字符串来创建子字符串数组。</span><span class="sxs-lookup"><span data-stu-id="7df16-105">The <xref:System.String.Split%2A?displayProperty=nameWithType> method creates an array of substrings by splitting the input string based on one or more delimiters.</span></span> <span data-ttu-id="7df16-106">此方法通常是分隔字边界上的字符串的最简单方法。</span><span class="sxs-lookup"><span data-stu-id="7df16-106">This method is often the easiest way to separate a string on word boundaries.</span></span> <span data-ttu-id="7df16-107">它也用于拆分其他特定字符或字符串上的字符串。</span><span class="sxs-lookup"><span data-stu-id="7df16-107">It's also used to split strings on other specific characters or strings.</span></span>

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

<span data-ttu-id="7df16-108">下方代码将一个常用短语拆分为一个由每个单词组成的字符串数组。</span><span class="sxs-lookup"><span data-stu-id="7df16-108">The following code splits a common phrase into an array of strings for each word.</span></span>

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs" id="Snippet1":::

<span data-ttu-id="7df16-109">分隔符的每个实例都会在返回的数组中产生一个值。</span><span class="sxs-lookup"><span data-stu-id="7df16-109">Every instance of a separator character produces a value in the returned array.</span></span> <span data-ttu-id="7df16-110">连续的分隔符将生成空字符串作为返回的数组中的值。</span><span class="sxs-lookup"><span data-stu-id="7df16-110">Consecutive separator characters produce the empty string as a value in the returned array.</span></span> <span data-ttu-id="7df16-111">下面的示例介绍如何创建空字符串，该示例使用空格字符作为分隔符。</span><span class="sxs-lookup"><span data-stu-id="7df16-111">You can see how an empty string is created in the following example, which uses the space character as a separator.</span></span>

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs" id="Snippet2":::

<span data-ttu-id="7df16-112">该行为可以更容易地用逗号分隔值 (CSV) 文件之类的格式表示表格数据。</span><span class="sxs-lookup"><span data-stu-id="7df16-112">This behavior makes it easier for formats like comma-separated values (CSV) files representing tabular data.</span></span> <span data-ttu-id="7df16-113">连续的逗号表示空白列。</span><span class="sxs-lookup"><span data-stu-id="7df16-113">Consecutive commas represent a blank column.</span></span>

<span data-ttu-id="7df16-114">可传递可选 <xref:System.StringSplitOptions.RemoveEmptyEntries?displayProperty=nameWithType> 参数来排除返回数组中的任何空字符串。</span><span class="sxs-lookup"><span data-stu-id="7df16-114">You can pass an optional <xref:System.StringSplitOptions.RemoveEmptyEntries?displayProperty=nameWithType> parameter to exclude any empty strings in the returned array.</span></span> <span data-ttu-id="7df16-115">要对返回的集合进行更复杂的处理，可使用 [LINQ](../programming-guide/concepts/linq/index.md) 来处理结果序列。</span><span class="sxs-lookup"><span data-stu-id="7df16-115">For more complicated processing of the returned collection, you can use [LINQ](../programming-guide/concepts/linq/index.md) to manipulate the result sequence.</span></span>

<span data-ttu-id="7df16-116"><xref:System.String.Split%2A?displayProperty=nameWithType> 可使用多个分隔符。</span><span class="sxs-lookup"><span data-stu-id="7df16-116"><xref:System.String.Split%2A?displayProperty=nameWithType> can use multiple separator characters.</span></span>
<span data-ttu-id="7df16-117">下面的示例使用空格、逗号、句点、冒号和制表符作为分隔字符，这些分隔字符在数组中传递到 <xref:System.String.Split%2A>。</span><span class="sxs-lookup"><span data-stu-id="7df16-117">The following example uses spaces, commas, periods, colons, and tabs as separating characters, which are passed to <xref:System.String.Split%2A> in an array .</span></span>
<span data-ttu-id="7df16-118">代码底部的循环显示返回数组中的每个单词。</span><span class="sxs-lookup"><span data-stu-id="7df16-118">The loop at the bottom of the code displays each of the words in the returned array.</span></span>

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs" id="Snippet3":::

<span data-ttu-id="7df16-119">任何分隔符的连续实例都会在输出数组中生成空字符串：</span><span class="sxs-lookup"><span data-stu-id="7df16-119">Consecutive instances of any separator produce the empty string in the output array:</span></span>

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs" id="Snippet4":::

<span data-ttu-id="7df16-120"><xref:System.String.Split%2A?displayProperty=nameWithType> 可采用字符串数组（充当用于分析目标字符串的分隔符的字符序列，而非单个字符）。</span><span class="sxs-lookup"><span data-stu-id="7df16-120"><xref:System.String.Split%2A?displayProperty=nameWithType> can take an array of strings (character sequences that act as separators for parsing the target string, instead of single characters).</span></span>

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs" id="Snippet5":::

## <a name="see-also"></a><span data-ttu-id="7df16-121">请参阅</span><span class="sxs-lookup"><span data-stu-id="7df16-121">See also</span></span>

- [<span data-ttu-id="7df16-122">从字符串中提取元素</span><span class="sxs-lookup"><span data-stu-id="7df16-122">Extract elements from a string</span></span>](../../standard/base-types/divide-up-strings.md)
- [<span data-ttu-id="7df16-123">C# 编程指南</span><span class="sxs-lookup"><span data-stu-id="7df16-123">C# programming guide</span></span>](../programming-guide/index.md)
- [<span data-ttu-id="7df16-124">字符串</span><span class="sxs-lookup"><span data-stu-id="7df16-124">Strings</span></span>](../programming-guide/strings/index.md)
- [<span data-ttu-id="7df16-125">.NET 正则表达式</span><span class="sxs-lookup"><span data-stu-id="7df16-125">.NET regular expressions</span></span>](../../standard/base-types/regular-expressions.md)
