---
title: 将字符串转换为类型
description: 了解 .NET 中的字符串分析。 分析可将表示某种 .NET 基类型的字符串转换为该基类型。 分析是格式化的反向操作。
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- parsing strings, about parsing strings
- IFormatProvider interface, parsing strings
- base types, parsing strings
- Parse method
- parsing strings
ms.assetid: 5e758b41-db93-456b-8999-99b7304b090d
ms.openlocfilehash: 3d23fa9c7ecc3593f03f70dbd5ea7bda841e8f4f
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400848"
---
# <a name="parse-strings-in-net"></a><span data-ttu-id="0cc7b-105">分析 .NET 中的字符串</span><span class="sxs-lookup"><span data-stu-id="0cc7b-105">Parse strings in .NET</span></span>

<span data-ttu-id="0cc7b-106">分析操作将表示某种 .NET 基类型的字符串转换为该基类型。</span><span class="sxs-lookup"><span data-stu-id="0cc7b-106">A *parsing* operation converts a string that represents a .NET base type into that base type.</span></span> <span data-ttu-id="0cc7b-107">例如，分析操作用于将字符串转换为浮点数字或日期和时间值。</span><span class="sxs-lookup"><span data-stu-id="0cc7b-107">For example, a parsing operation is used to convert a string to a floating-point number or to a date-and-time value.</span></span> <span data-ttu-id="0cc7b-108">最常用于执行分析操作的方法是 `Parse` 方法。</span><span class="sxs-lookup"><span data-stu-id="0cc7b-108">The method most commonly used to perform a parsing operation is the `Parse` method.</span></span> <span data-ttu-id="0cc7b-109">因为分析是格式设置（涉及将基类型转换为其字符串表示形式）的反向操作，所以有许多相同规则和约定适用。</span><span class="sxs-lookup"><span data-stu-id="0cc7b-109">Because parsing is the reverse operation of formatting (which involves converting a base type into its string representation), many of the same rules and conventions apply.</span></span> <span data-ttu-id="0cc7b-110">就像格式设置使用对象来实现 <xref:System.IFormatProvider> 接口以提供区域性敏感型格式设置信息一样，分析也使用对象来实现 <xref:System.IFormatProvider> 接口，以确定如何解释字符串表示形式。</span><span class="sxs-lookup"><span data-stu-id="0cc7b-110">Just as formatting uses an object that implements the <xref:System.IFormatProvider> interface to provide culture-sensitive formatting information, parsing also uses an object that implements the <xref:System.IFormatProvider> interface to determine how to interpret a string representation.</span></span> <span data-ttu-id="0cc7b-111">有关详细信息，请参阅[格式类型](formatting-types.md)。</span><span class="sxs-lookup"><span data-stu-id="0cc7b-111">For more information, see [Format types](formatting-types.md).</span></span>

## <a name="in-this-section"></a><span data-ttu-id="0cc7b-112">本节内容</span><span class="sxs-lookup"><span data-stu-id="0cc7b-112">In This Section</span></span>
 <span data-ttu-id="0cc7b-113">[分析数值字符串](parsing-numeric.md)</span><span class="sxs-lookup"><span data-stu-id="0cc7b-113">[Parsing Numeric Strings](parsing-numeric.md)</span></span>\
 <span data-ttu-id="0cc7b-114">介绍了如何将字符串转换为 .NET 数字类型。</span><span class="sxs-lookup"><span data-stu-id="0cc7b-114">Describes how to convert strings into .NET numeric types.</span></span>

 <span data-ttu-id="0cc7b-115">[分析日期和时间字符串](parsing-datetime.md)</span><span class="sxs-lookup"><span data-stu-id="0cc7b-115">[Parsing Date and Time Strings](parsing-datetime.md)</span></span>\
 <span data-ttu-id="0cc7b-116">介绍了如何将字符串转换为 .NET DateTime 类型。</span><span class="sxs-lookup"><span data-stu-id="0cc7b-116">Describes how to convert strings into .NET **DateTime** types.</span></span>

 <span data-ttu-id="0cc7b-117">[分析其他字符串](parsing-other.md)</span><span class="sxs-lookup"><span data-stu-id="0cc7b-117">[Parsing Other Strings](parsing-other.md)</span></span>\
 <span data-ttu-id="0cc7b-118">介绍了如何将字符串转换为 Char、Boolean 和 Enum 类型。</span><span class="sxs-lookup"><span data-stu-id="0cc7b-118">Describes how to convert strings into **Char** , **Boolean** , and **Enum** types.</span></span>

## <a name="related-sections"></a><span data-ttu-id="0cc7b-119">相关章节</span><span class="sxs-lookup"><span data-stu-id="0cc7b-119">Related Sections</span></span>
 <span data-ttu-id="0cc7b-120">[格式设置类型](formatting-types.md)</span><span class="sxs-lookup"><span data-stu-id="0cc7b-120">[Formatting Types](formatting-types.md)</span></span>\
 <span data-ttu-id="0cc7b-121">介绍了基本格式设置概念，如格式说明符和格式提供程序。</span><span class="sxs-lookup"><span data-stu-id="0cc7b-121">Describes basic formatting concepts like format specifiers and format providers.</span></span>

 <span data-ttu-id="0cc7b-122">[.NET 中的类型转换](type-conversion.md)</span><span class="sxs-lookup"><span data-stu-id="0cc7b-122">[Type Conversion in .NET](type-conversion.md)</span></span>\
 <span data-ttu-id="0cc7b-123">介绍了如何转换类型。</span><span class="sxs-lookup"><span data-stu-id="0cc7b-123">Describes how to convert types.</span></span>
