---
title: 如何：用前导零填充数字
description: 了解如何用前导零填充数字。 将前导零添加到整数或将数值添加到特定的总长度或特定数量的前导零。
ms.date: 02/25/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- numeric format strings [.NET]
- formatting [.NET], numbers
- number formatting [.NET]
- numbers [.NET], format strings
ms.assetid: 0b2c2cb5-c580-4891-8d81-cb632f5ec384
ms.openlocfilehash: 7c3ee376fde34663ee0599c0b1ae654871a71206
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888451"
---
# <a name="how-to-pad-a-number-with-leading-zeros"></a><span data-ttu-id="f8eef-104">如何：用前导零填充数字</span><span class="sxs-lookup"><span data-stu-id="f8eef-104">How to: Pad a Number with Leading Zeros</span></span>

<span data-ttu-id="f8eef-105">通过结合使用“D”[标准数字格式字符串](standard-numeric-format-strings.md)和精度说明符，将前导零添加到整数。</span><span class="sxs-lookup"><span data-stu-id="f8eef-105">You can add leading zeros to an integer by using the "D" [standard numeric format string](standard-numeric-format-strings.md) with a precision specifier.</span></span> <span data-ttu-id="f8eef-106">你可以通过使用[自定义数字格式字符串](custom-numeric-format-strings.md)，将前导零添加到整数和浮点数。</span><span class="sxs-lookup"><span data-stu-id="f8eef-106">You can add leading zeros to both integer and floating-point numbers by using a [custom numeric format string](custom-numeric-format-strings.md).</span></span> <span data-ttu-id="f8eef-107">本文介绍如何通过这两种方法用前导零填充数字。</span><span class="sxs-lookup"><span data-stu-id="f8eef-107">This article shows how to use both methods to pad a number with leading zeros.</span></span>

## <a name="to-pad-an-integer-with-leading-zeros-to-a-specific-length"></a><span data-ttu-id="f8eef-108">使用前导零将整数填充到特定的长度</span><span class="sxs-lookup"><span data-stu-id="f8eef-108">To pad an integer with leading zeros to a specific length</span></span>

1. <span data-ttu-id="f8eef-109">确定整数值要显示的最小位数。</span><span class="sxs-lookup"><span data-stu-id="f8eef-109">Determine the minimum number of digits you want the integer value to display.</span></span> <span data-ttu-id="f8eef-110">在此数字中包括任何前导位。</span><span class="sxs-lookup"><span data-stu-id="f8eef-110">Include any leading digits in this number.</span></span>

1. <span data-ttu-id="f8eef-111">确定是要将整数显示为十进制值还是十六进制值。</span><span class="sxs-lookup"><span data-stu-id="f8eef-111">Determine whether you want to display the integer as a decimal value or a hexadecimal value.</span></span>

    - <span data-ttu-id="f8eef-112">若要将整数显示为十进制值，则调用其 `ToString(String)` 方法，并传递字符串“Dn”作为 `format` 参数的值，其中 n 表示字符串的最小长度 。</span><span class="sxs-lookup"><span data-stu-id="f8eef-112">To display the integer as a decimal value, call its `ToString(String)` method, and pass the string "D *n* " as the value of the `format` parameter, where *n* represents the minimum length of the string.</span></span>

    - <span data-ttu-id="f8eef-113">若要将整数显示为十六进制值，则调用其 `ToString(String)` 方法，并传递字符串“Xn”作为 format 参数的值，其中 n 表示字符串的最小长度。</span><span class="sxs-lookup"><span data-stu-id="f8eef-113">To display the integer as a hexadecimal value, call its `ToString(String)` method and pass the string "X *n* " as the value of the format parameter, where *n* represents the minimum length of the string.</span></span>

<span data-ttu-id="f8eef-114">此外，你也可以在 [C#](../../csharp/language-reference/tokens/interpolated.md) 和 [Visual Basic](../../visual-basic/programming-guide/language-features/strings/interpolated-strings.md) 的内插字符串中使用格式字符串，或者可以调用一个 <xref:System.String.Format%2A?displayProperty=nameWithType> 或 <xref:System.Console.WriteLine%2A?displayProperty=nameWithType> 等使用[复合格式设置](composite-formatting.md)的方法。</span><span class="sxs-lookup"><span data-stu-id="f8eef-114">You can also use the format string in an interpolated string in both [C#](../../csharp/language-reference/tokens/interpolated.md) and [Visual Basic](../../visual-basic/programming-guide/language-features/strings/interpolated-strings.md), or you can call a method, such as <xref:System.String.Format%2A?displayProperty=nameWithType> or <xref:System.Console.WriteLine%2A?displayProperty=nameWithType>, that uses [composite formatting](composite-formatting.md).</span></span>

<span data-ttu-id="f8eef-115">以下示例使用前导零设置若干整数值的格式，以便格式化数字的总长度至少为八个字符。</span><span class="sxs-lookup"><span data-stu-id="f8eef-115">The following example formats several integer values with leading zeros so that the total length of the formatted number is at least eight characters.</span></span>

[!code-csharp[Formatting.HowTo.PadNumber#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#1)]
[!code-vb[Formatting.HowTo.PadNumber#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#1)]

## <a name="to-pad-an-integer-with-a-specific-number-of-leading-zeros"></a><span data-ttu-id="f8eef-116">使用特定数目的前导零填充整数</span><span class="sxs-lookup"><span data-stu-id="f8eef-116">To pad an integer with a specific number of leading zeros</span></span>

1. <span data-ttu-id="f8eef-117">确定希望整数值显示多少个前导零。</span><span class="sxs-lookup"><span data-stu-id="f8eef-117">Determine how many leading zeros you want the integer value to display.</span></span>

1. <span data-ttu-id="f8eef-118">确定是要将整数显示为十进制值还是十六进制值。</span><span class="sxs-lookup"><span data-stu-id="f8eef-118">Determine whether you want to display the integer as a decimal value or a hexadecimal value.</span></span>

    - <span data-ttu-id="f8eef-119">将其格式设置为十进制值需要使用“D”标准格式说明符。</span><span class="sxs-lookup"><span data-stu-id="f8eef-119">Formatting it as a decimal value requires that you use the "D" standard format specifier.</span></span>

    - <span data-ttu-id="f8eef-120">将其格式设置为十六进制值需要使用“X”标准格式说明符。</span><span class="sxs-lookup"><span data-stu-id="f8eef-120">Formatting it as a hexadecimal value requires that you use the "X" standard format specifier.</span></span>

1. <span data-ttu-id="f8eef-121">通过调用整数值的 `ToString("D").Length` 或 `ToString("X").Length` 方法，确定未填充的数字字符串的长度。</span><span class="sxs-lookup"><span data-stu-id="f8eef-121">Determine the length of the unpadded numeric string by calling the integer value's `ToString("D").Length` or `ToString("X").Length` method.</span></span>

1. <span data-ttu-id="f8eef-122">将你要在格式化字符串中包括的前导零的数目添加到未填充的数字字符串的长度上。</span><span class="sxs-lookup"><span data-stu-id="f8eef-122">Add the number of leading zeros that you want to include in the formatted string to the length of the unpadded numeric string.</span></span> <span data-ttu-id="f8eef-123">添加前导零的个数将定义填充字符串的总长度。</span><span class="sxs-lookup"><span data-stu-id="f8eef-123">Adding the number of leading zeros defines the total length of the padded string.</span></span>

1. <span data-ttu-id="f8eef-124">调用整数值的 `ToString(String)` 方法，并且对于十进制字符串传递字符串“Dn”，对于十六进制字符串传递“Xn”；其中，n 表示填充的字符串的总长度。</span><span class="sxs-lookup"><span data-stu-id="f8eef-124">Call the integer value's `ToString(String)` method, and pass the string "D *n* " for decimal strings and "X *n* " for hexadecimal strings, where *n* represents the total length of the padded string.</span></span> <span data-ttu-id="f8eef-125">也可以在支持复合格式设置的方法中使用“Dn”或“Xn”格式字符串。</span><span class="sxs-lookup"><span data-stu-id="f8eef-125">You can also use the "D *n* " or "X *n* " format string in a method that supports composite formatting.</span></span>

<span data-ttu-id="f8eef-126">下面的示例使用五个前导零来填充整数值。</span><span class="sxs-lookup"><span data-stu-id="f8eef-126">The following example pads an integer value with five leading zeros.</span></span>

[!code-csharp[Formatting.HowTo.PadNumber#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#2)]
[!code-vb[Formatting.HowTo.PadNumber#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#2)]

## <a name="to-pad-a-numeric-value-with-leading-zeros-to-a-specific-length"></a><span data-ttu-id="f8eef-127">使用前导零将数值填充到特定的长度</span><span class="sxs-lookup"><span data-stu-id="f8eef-127">To pad a numeric value with leading zeros to a specific length</span></span>

1. <span data-ttu-id="f8eef-128">确定数字的字符串表示形式要在小数点的左侧保留的位数。</span><span class="sxs-lookup"><span data-stu-id="f8eef-128">Determine how many digits to the left of the decimal you want the string representation of the number to have.</span></span> <span data-ttu-id="f8eef-129">在此总位数中包括任何前导零。</span><span class="sxs-lookup"><span data-stu-id="f8eef-129">Include any leading zeros in this total number of digits.</span></span>

1. <span data-ttu-id="f8eef-130">定义一个使用零占位符“0”来表示零的最小数目的自定义数字格式字符串。</span><span class="sxs-lookup"><span data-stu-id="f8eef-130">Define a custom numeric format string that uses the zero placeholder "0" to represent the minimum number of zeros.</span></span>

1. <span data-ttu-id="f8eef-131">调用数字的 `ToString(String)` 方法并向其传递自定义格式字符串。</span><span class="sxs-lookup"><span data-stu-id="f8eef-131">Call the number's `ToString(String)` method and pass it the custom format string.</span></span> <span data-ttu-id="f8eef-132">此外，你也可以将自定义格式字符串与字符串内插或与支持复合格式设置的方法一起使用。</span><span class="sxs-lookup"><span data-stu-id="f8eef-132">You can also use the custom format string with string interpolation or with a method that supports composite formatting.</span></span>

<span data-ttu-id="f8eef-133">下面的示例使用前导零设置几个数值的格式。</span><span class="sxs-lookup"><span data-stu-id="f8eef-133">The following example formats several numeric values with leading zeros.</span></span> <span data-ttu-id="f8eef-134">因此，格式化后的数字总长度是小数点左侧至少八位数字。</span><span class="sxs-lookup"><span data-stu-id="f8eef-134">As a result, the total length of the formatted number is at least eight digits to the left of the decimal.</span></span>

[!code-csharp[Formatting.HowTo.PadNumber#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#3)]
[!code-vb[Formatting.HowTo.PadNumber#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#3)]

## <a name="to-pad-a-numeric-value-with-a-specific-number-of-leading-zeros"></a><span data-ttu-id="f8eef-135">使用特定数目的前导零填充数值</span><span class="sxs-lookup"><span data-stu-id="f8eef-135">To pad a numeric value with a specific number of leading zeros</span></span>

1. <span data-ttu-id="f8eef-136">确定希望数值具有多少个前导零。</span><span class="sxs-lookup"><span data-stu-id="f8eef-136">Determine how many leading zeros you want the numeric value to have.</span></span>

1. <span data-ttu-id="f8eef-137">确定未填充数字字符串中小数点左侧的位数：</span><span class="sxs-lookup"><span data-stu-id="f8eef-137">Determine the number of digits to the left of the decimal in the unpadded numeric string:</span></span>

    1. <span data-ttu-id="f8eef-138">确定数字的字符串表示形式是否包括小数点符号。</span><span class="sxs-lookup"><span data-stu-id="f8eef-138">Determine whether the string representation of a number includes a decimal point symbol.</span></span>

    1. <span data-ttu-id="f8eef-139">如果它包括小数点符号，则确定小数点左侧的字符数。</span><span class="sxs-lookup"><span data-stu-id="f8eef-139">If it does include a decimal point symbol, determine the number of characters to the left of the decimal point.</span></span>

         <span data-ttu-id="f8eef-140">\- 或 -</span><span class="sxs-lookup"><span data-stu-id="f8eef-140">-or-</span></span>

         <span data-ttu-id="f8eef-141">如果它不包括小数点符号，则确定字符串的长度。</span><span class="sxs-lookup"><span data-stu-id="f8eef-141">If it doesn't include a decimal point symbol, determine the string's length.</span></span>

1. <span data-ttu-id="f8eef-142">创建使用以下格式的自定义格式字符串：</span><span class="sxs-lookup"><span data-stu-id="f8eef-142">Create a custom format string that uses:</span></span>

    - <span data-ttu-id="f8eef-143">零占位符“0”表示在字符串中出现的每个前导零。</span><span class="sxs-lookup"><span data-stu-id="f8eef-143">The zero placeholder "0" for each of the leading zeros to appear in the string.</span></span>

    - <span data-ttu-id="f8eef-144">零占位符或数字占位符“#”表示默认字符串中的每个数字。</span><span class="sxs-lookup"><span data-stu-id="f8eef-144">Either the zero placeholder or the digit placeholder "#" to represent each digit in the default string.</span></span>

1. <span data-ttu-id="f8eef-145">将自定义格式字符串作为对数字的 `ToString(String)` 方法或支持复合格式设置的方法的参数提供。</span><span class="sxs-lookup"><span data-stu-id="f8eef-145">Supply the custom format string as a parameter either to the number's `ToString(String)` method or to a method that supports composite formatting.</span></span>

<span data-ttu-id="f8eef-146">下面的示例使用五个前导零来填充两个 <xref:System.Double> 值。</span><span class="sxs-lookup"><span data-stu-id="f8eef-146">The following example pads two <xref:System.Double> values with five leading zeros.</span></span>

[!code-csharp[Formatting.HowTo.PadNumber#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#4)]
[!code-vb[Formatting.HowTo.PadNumber#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#4)]

## <a name="see-also"></a><span data-ttu-id="f8eef-147">请参阅</span><span class="sxs-lookup"><span data-stu-id="f8eef-147">See also</span></span>

- [<span data-ttu-id="f8eef-148">自定义数字格式字符串</span><span class="sxs-lookup"><span data-stu-id="f8eef-148">Custom Numeric Format Strings</span></span>](custom-numeric-format-strings.md)
- [<span data-ttu-id="f8eef-149">标准数字格式字符串</span><span class="sxs-lookup"><span data-stu-id="f8eef-149">Standard Numeric Format Strings</span></span>](standard-numeric-format-strings.md)
- [<span data-ttu-id="f8eef-150">复合格式设置</span><span class="sxs-lookup"><span data-stu-id="f8eef-150">Composite Formatting</span></span>](composite-formatting.md)
