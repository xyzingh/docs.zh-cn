---
title: .NET 中的基本字符串操作
description: 了解可对字符串执行的基本操作。
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- strings [.NET], basic string operations
- custom strings
ms.assetid: 8133d357-90b5-4b62-9927-43323d99b6b6
ms.custom: seadec18
ms.openlocfilehash: 6ec244ab6935f4a92b0f59fa6c1cb8bc45638ce4
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889109"
---
# <a name="basic-string-operations-in-net"></a><span data-ttu-id="60394-103">.NET 中的基本字符串操作</span><span class="sxs-lookup"><span data-stu-id="60394-103">Basic string operations in .NET</span></span>

<span data-ttu-id="60394-104">应用程序经常通过构造基于用户输入的消息来响应用户。</span><span class="sxs-lookup"><span data-stu-id="60394-104">Applications often respond to users by constructing messages based on user input.</span></span> <span data-ttu-id="60394-105">例如，网站用包含用户名的专用问候语来响应新登录的用户的情况并不少见。</span><span class="sxs-lookup"><span data-stu-id="60394-105">For example, it is not uncommon for websites to respond to a newly logged-on user with a specialized greeting that includes the user's name.</span></span>

<span data-ttu-id="60394-106">使用 <xref:System.String?displayProperty=nameWithType> 和 <xref:System.Text.StringBuilder?displayProperty=nameWithType> 类中的多个方法，可以动态构造要在用户界面中显示的自定义字符串。</span><span class="sxs-lookup"><span data-stu-id="60394-106">Several methods in the <xref:System.String?displayProperty=nameWithType> and <xref:System.Text.StringBuilder?displayProperty=nameWithType> classes allow you to dynamically construct custom strings to display in your user interface.</span></span> <span data-ttu-id="60394-107">借助这些方法还可执行许多基本字符串操作，例如，从字节数组创建新字符串，比较字符串的值和修改现有字符串。</span><span class="sxs-lookup"><span data-stu-id="60394-107">These methods also help you perform a number of basic string operations like creating new strings from arrays of bytes, comparing the values of strings, and modifying existing strings.</span></span>

## <a name="related-sections"></a><span data-ttu-id="60394-108">相关章节</span><span class="sxs-lookup"><span data-stu-id="60394-108">Related sections</span></span>

<span data-ttu-id="60394-109">[.NET 中的类型转换](type-conversion.md)</span><span class="sxs-lookup"><span data-stu-id="60394-109">[Type Conversion in .NET](type-conversion.md)</span></span>\
<span data-ttu-id="60394-110">介绍了如何从一种类型转换为另一种类型。</span><span class="sxs-lookup"><span data-stu-id="60394-110">Describes how to convert one type into another type.</span></span>  

<span data-ttu-id="60394-111">[格式设置类型](formatting-types.md)</span><span class="sxs-lookup"><span data-stu-id="60394-111">[Formatting Types](formatting-types.md)</span></span>\
<span data-ttu-id="60394-112">介绍了如何使用格式说明符设置字符串格式。</span><span class="sxs-lookup"><span data-stu-id="60394-112">Describes how to format strings using format specifiers.</span></span>
