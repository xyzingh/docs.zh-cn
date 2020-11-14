---
title: .NET 中的基本字符串控制
description: 查看调用许多字符串方法的示例。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings [.NET], examples
ms.assetid: 121d1eae-251b-44c0-8818-57da04b8215e
ms.openlocfilehash: 659f01cc1d7ae03e12e83329e4fd2446b7512475
ms.sourcegitcommit: ffd4d5e824db6c5f0c3521c0e802fd9e8f0edcbe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2020
ms.locfileid: "93342613"
---
# <a name="how-to-perform-basic-string-manipulations-in-net"></a><span data-ttu-id="8f7fb-103">如何：执行 .NET 中的基本字符串控制</span><span class="sxs-lookup"><span data-stu-id="8f7fb-103">How to: Perform Basic String Manipulations in .NET</span></span>

<span data-ttu-id="8f7fb-104">下面的示例使用[基本字符串操作](basic-string-operations.md)主题中介绍的一些方法，构造模拟现实应用执行字符串控制的类。</span><span class="sxs-lookup"><span data-stu-id="8f7fb-104">The following example uses some of the methods discussed in the [Basic String Operations](basic-string-operations.md) topics to construct a class that performs string manipulations in a manner that might be found in a real-world application.</span></span> <span data-ttu-id="8f7fb-105">`MailToData` 类将个人的姓名和地址存储在单独的属性中，并提供一种将 `City`、`State` 和 `Zip` 字段合并成向用户显示的单个字符串的方式。</span><span class="sxs-lookup"><span data-stu-id="8f7fb-105">The `MailToData` class stores the name and address of an individual in separate properties and provides a way to combine the `City`, `State`, and `Zip` fields into a single string for display to the user.</span></span> <span data-ttu-id="8f7fb-106">此外，该类允许用户以单个字符串的形式输入城市、省/市/自治区和邮政编码信息。</span><span class="sxs-lookup"><span data-stu-id="8f7fb-106">Furthermore, the class allows the user to enter the city, state, and zip code information as a single string.</span></span> <span data-ttu-id="8f7fb-107">应用程序将自动分析单个字符串，并将正确的信息输入到相应的属性中。</span><span class="sxs-lookup"><span data-stu-id="8f7fb-107">The application automatically parses the single string and enters the proper information into the corresponding property.</span></span>

<span data-ttu-id="8f7fb-108">为简单起见，此示例使用带命令行接口的控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="8f7fb-108">For simplicity, this example uses a console application with a command-line interface.</span></span>

## <a name="example"></a><span data-ttu-id="8f7fb-109">示例</span><span class="sxs-lookup"><span data-stu-id="8f7fb-109">Example</span></span>

[!code-csharp[Conceptual.String.BasicOps#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/basicops.cs#1)]
[!code-vb[Conceptual.String.BasicOps#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/basicops.vb#1)]

<span data-ttu-id="8f7fb-110">执行上面的代码时，系统会要求用户输入其姓名和地址。</span><span class="sxs-lookup"><span data-stu-id="8f7fb-110">When the preceding code is executed, the user is asked to enter their name and address.</span></span> <span data-ttu-id="8f7fb-111">应用程序将这些信息放入相应的属性并将信息返回向用户显示，同时创建一个显示城市、省/市/自治区和邮政编码信息的字符串。</span><span class="sxs-lookup"><span data-stu-id="8f7fb-111">The application places the information in the appropriate properties and displays the information back to the user, creating a single string that displays the city, state, and zip code information.</span></span>

## <a name="see-also"></a><span data-ttu-id="8f7fb-112">请参阅</span><span class="sxs-lookup"><span data-stu-id="8f7fb-112">See also</span></span>

- [<span data-ttu-id="8f7fb-113">基本字符串操作</span><span class="sxs-lookup"><span data-stu-id="8f7fb-113">Basic String Operations</span></span>](basic-string-operations.md)
