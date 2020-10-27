---
description: 了解 C# 中的内置字符类型
title: char 类型 - C# 引用
ms.date: 05/11/2020
f1_keywords:
- char
- char_CSharpKeyword
helpviewer_keywords:
- char data type [C#]
ms.assetid: b51cf4fb-124c-4067-af48-afbac122b228
ms.openlocfilehash: 1cb40759b81a1fcedcf5962b57d79cf3a64df561
ms.sourcegitcommit: 870bc4b4087510f6fba3c7b1c0d391f02bcc1f3e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2020
ms.locfileid: "92471871"
---
# <a name="char-c-reference"></a><span data-ttu-id="ba62e-103">char（C# 参考）</span><span class="sxs-lookup"><span data-stu-id="ba62e-103">char (C# reference)</span></span>

<span data-ttu-id="ba62e-104">`char` 类型关键字是 .NET <xref:System.Char?displayProperty=nameWithType> 结构类型的别名，它表示 Unicode UTF-16 字符。</span><span class="sxs-lookup"><span data-stu-id="ba62e-104">The `char` type keyword is an alias for the .NET <xref:System.Char?displayProperty=nameWithType> structure type that represents a Unicode UTF-16 character.</span></span>

|<span data-ttu-id="ba62e-105">类型</span><span class="sxs-lookup"><span data-stu-id="ba62e-105">Type</span></span>|<span data-ttu-id="ba62e-106">范围</span><span class="sxs-lookup"><span data-stu-id="ba62e-106">Range</span></span>|<span data-ttu-id="ba62e-107">大小</span><span class="sxs-lookup"><span data-stu-id="ba62e-107">Size</span></span>|<span data-ttu-id="ba62e-108">.NET 类型</span><span class="sxs-lookup"><span data-stu-id="ba62e-108">.NET type</span></span>|
|----------|-----------|----------|-------------------------|
|`char`|<span data-ttu-id="ba62e-109">U+0000 到 U+FFFF</span><span class="sxs-lookup"><span data-stu-id="ba62e-109">U+0000 to U+FFFF</span></span>|<span data-ttu-id="ba62e-110">16 位</span><span class="sxs-lookup"><span data-stu-id="ba62e-110">16 bit</span></span>|<xref:System.Char?displayProperty=nameWithType>|

<span data-ttu-id="ba62e-111">`char` 类型的默认值为 `\0`，即 U+0000。</span><span class="sxs-lookup"><span data-stu-id="ba62e-111">The default value of the `char` type is `\0`, that is, U+0000.</span></span>

<span data-ttu-id="ba62e-112">`char` 类型支持[比较](../operators/comparison-operators.md)、[相等](../operators/equality-operators.md)、[增量](../operators/arithmetic-operators.md#increment-operator-)和[减量](../operators/arithmetic-operators.md#decrement-operator---)运算符。</span><span class="sxs-lookup"><span data-stu-id="ba62e-112">The `char` type supports [comparison](../operators/comparison-operators.md), [equality](../operators/equality-operators.md), [increment](../operators/arithmetic-operators.md#increment-operator-), and [decrement](../operators/arithmetic-operators.md#decrement-operator---) operators.</span></span> <span data-ttu-id="ba62e-113">此外，对于 `char` 操作数，[算数](../operators/arithmetic-operators.md)和[逻辑位](../operators/bitwise-and-shift-operators.md)运算符对相应的字符代码执行操作，并得出 `int` 类型的结果。</span><span class="sxs-lookup"><span data-stu-id="ba62e-113">Moreover, for `char` operands, [arithmetic](../operators/arithmetic-operators.md) and [bitwise logical](../operators/bitwise-and-shift-operators.md) operators perform an operation on the corresponding character codes and produce the result of the `int` type.</span></span>

<span data-ttu-id="ba62e-114">[字符串](reference-types.md#the-string-type)类型将文本表示为 `char` 值的序列。</span><span class="sxs-lookup"><span data-stu-id="ba62e-114">The [string](reference-types.md#the-string-type) type represents text as a sequence of `char` values.</span></span>

## <a name="literals"></a><span data-ttu-id="ba62e-115">文本</span><span class="sxs-lookup"><span data-stu-id="ba62e-115">Literals</span></span>

<span data-ttu-id="ba62e-116">可以使用以下命令指定 `char` 值：</span><span class="sxs-lookup"><span data-stu-id="ba62e-116">You can specify a `char` value with:</span></span>

- <span data-ttu-id="ba62e-117">字符文本。</span><span class="sxs-lookup"><span data-stu-id="ba62e-117">a character literal.</span></span>
- <span data-ttu-id="ba62e-118">Unicode 转义序列，它是 `\u` 后跟字符代码的十六进制表示形式（四个符号）。</span><span class="sxs-lookup"><span data-stu-id="ba62e-118">a Unicode escape sequence, which is `\u` followed by the four-symbol hexadecimal representation of a character code.</span></span>
- <span data-ttu-id="ba62e-119">十六进制转义序列，它是 `\x` 后跟字符代码的十六进制表示形式。</span><span class="sxs-lookup"><span data-stu-id="ba62e-119">a hexadecimal escape sequence, which is `\x` followed by the hexadecimal representation of a character code.</span></span>

[!code-csharp-interactive[char literals](snippets/shared/CharType.cs#Literals)]

<span data-ttu-id="ba62e-120">如前面的示例所示，你还可以将字符代码的值转换为相应的 `char` 值。</span><span class="sxs-lookup"><span data-stu-id="ba62e-120">As the preceding example shows, you can also cast the value of a character code into the corresponding `char` value.</span></span>

> [!NOTE]
> <span data-ttu-id="ba62e-121">对于 Unicode 转义序列，必须指定全部四位十六进制值。</span><span class="sxs-lookup"><span data-stu-id="ba62e-121">In the case of a Unicode escape sequence, you must specify all four hexadecimal digits.</span></span> <span data-ttu-id="ba62e-122">也就是说，`\u006A` 是一个有效的转义序列，而 `\u06A` 和 `\u6A` 是无效的。</span><span class="sxs-lookup"><span data-stu-id="ba62e-122">That is, `\u006A` is a valid escape sequence, while `\u06A` and `\u6A` are not valid.</span></span>
>
> <span data-ttu-id="ba62e-123">对于十六进制转义序列，可以省略前导零。</span><span class="sxs-lookup"><span data-stu-id="ba62e-123">In the case of a hexadecimal escape sequence, you can omit the leading zeros.</span></span> <span data-ttu-id="ba62e-124">也就是说，`\x006A`、`\x06A` 和 `\x6A` 转义序列是有效的，并且对应于同一个字符。</span><span class="sxs-lookup"><span data-stu-id="ba62e-124">That is, the `\x006A`, `\x06A`, and `\x6A` escape sequences are valid and correspond to the same character.</span></span>

## <a name="conversions"></a><span data-ttu-id="ba62e-125">转换</span><span class="sxs-lookup"><span data-stu-id="ba62e-125">Conversions</span></span>

<span data-ttu-id="ba62e-126">`char` 类型可隐式转换为以下[整型](integral-numeric-types.md)类型：`ushort`、`int`、`uint`、`long` 和 `ulong`。</span><span class="sxs-lookup"><span data-stu-id="ba62e-126">The `char` type is implicitly convertible to the following [integral](integral-numeric-types.md) types: `ushort`, `int`, `uint`, `long`, and `ulong`.</span></span> <span data-ttu-id="ba62e-127">它也可以隐式转换为内置[浮点](floating-point-numeric-types.md)数值类型：`float`、`double` 和 `decimal`。</span><span class="sxs-lookup"><span data-stu-id="ba62e-127">It's also implicitly convertible to the built-in [floating-point](floating-point-numeric-types.md) numeric types: `float`, `double`, and `decimal`.</span></span> <span data-ttu-id="ba62e-128">它可以显式转换为 `sbyte`、`byte` 和 `short` 整型类型。</span><span class="sxs-lookup"><span data-stu-id="ba62e-128">It's explicitly convertible to `sbyte`, `byte`, and `short` integral types.</span></span>

<span data-ttu-id="ba62e-129">无法将其他类型隐式转换为 `char` 类型。</span><span class="sxs-lookup"><span data-stu-id="ba62e-129">There are no implicit conversions from other types to the `char` type.</span></span> <span data-ttu-id="ba62e-130">但是，任何[整型](integral-numeric-types.md)或[浮点](floating-point-numeric-types.md)数值类型都可显式转换为 `char`。</span><span class="sxs-lookup"><span data-stu-id="ba62e-130">However, any [integral](integral-numeric-types.md) or [floating-point](floating-point-numeric-types.md) numeric type is explicitly convertible to `char`.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="ba62e-131">C# 语言规范</span><span class="sxs-lookup"><span data-stu-id="ba62e-131">C# language specification</span></span>

<span data-ttu-id="ba62e-132">有关详细信息，请参阅 [C# 语言规范](~/_csharplang/spec/introduction.md)的[整型类型](~/_csharplang/spec/types.md#integral-types)部分。</span><span class="sxs-lookup"><span data-stu-id="ba62e-132">For more information, see the [Integral types](~/_csharplang/spec/types.md#integral-types) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="ba62e-133">请参阅</span><span class="sxs-lookup"><span data-stu-id="ba62e-133">See also</span></span>

- [<span data-ttu-id="ba62e-134">C# 参考</span><span class="sxs-lookup"><span data-stu-id="ba62e-134">C# reference</span></span>](../index.md)
- [<span data-ttu-id="ba62e-135">值类型</span><span class="sxs-lookup"><span data-stu-id="ba62e-135">Value types</span></span>](value-types.md)
- [<span data-ttu-id="ba62e-136">字符串</span><span class="sxs-lookup"><span data-stu-id="ba62e-136">Strings</span></span>](../../programming-guide/strings/index.md)
- <xref:System.Text.Rune?displayProperty=nameWithType>
- [<span data-ttu-id="ba62e-137">.NET 中的字符编码</span><span class="sxs-lookup"><span data-stu-id="ba62e-137">Character encoding in .NET</span></span>](../../../standard/base-types/character-encoding-introduction.md)
