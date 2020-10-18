---
title: 需要语句结束
ms.date: 07/20/2015
f1_keywords:
- bc30205
- vbc30205
helpviewer_keywords:
- BC30205
ms.assetid: 53c7f825-a737-4b76-a1fa-f67745b8bd40
ms.openlocfilehash: 36883989fe5aa0b5c70aa9ab1f7c991fab99e778
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163124"
---
# <a name="bc30205-end-of-statement-expected"></a><span data-ttu-id="7800e-102">BC30205：应为语句结尾</span><span class="sxs-lookup"><span data-stu-id="7800e-102">BC30205: End of statement expected</span></span>

<span data-ttu-id="7800e-103">语句在语法上完成，但在完成该语句的元素后附加了一个编程元素。</span><span class="sxs-lookup"><span data-stu-id="7800e-103">The statement is syntactically complete, but an additional programming element follows the element that completes the statement.</span></span> <span data-ttu-id="7800e-104">每个语句的末尾都需要行结束符。</span><span class="sxs-lookup"><span data-stu-id="7800e-104">A line terminator is required at the end of every statement.</span></span>

 <span data-ttu-id="7800e-105">行结束符将 Visual Basic 源文件中的字符分为多行。</span><span class="sxs-lookup"><span data-stu-id="7800e-105">A line terminator divides the characters of a Visual Basic source file into lines.</span></span> <span data-ttu-id="7800e-106">行结束符的示例包括 Unicode 回车符 ( # B0 HD) ，Unicode 换行符 ( # B1 HA) ，Unicode 回车符后跟 Unicode 换行符。</span><span class="sxs-lookup"><span data-stu-id="7800e-106">Examples of line terminators are the Unicode carriage return character (&HD), the Unicode linefeed character (&HA), and the Unicode carriage return character followed by the Unicode linefeed character.</span></span> <span data-ttu-id="7800e-107">有关行终止符的详细信息，请参阅 [Visual Basic 语言规范](~/_vblang/spec/lexical-grammar.md#line-terminators)。</span><span class="sxs-lookup"><span data-stu-id="7800e-107">For more information about line terminators, see the [Visual Basic Language Specification](~/_vblang/spec/lexical-grammar.md#line-terminators).</span></span>

 <span data-ttu-id="7800e-108">**错误 ID：** BC30205</span><span class="sxs-lookup"><span data-stu-id="7800e-108">**Error ID:** BC30205</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="7800e-109">更正此错误</span><span class="sxs-lookup"><span data-stu-id="7800e-109">To correct this error</span></span>

1. <span data-ttu-id="7800e-110">检查两个不同的语句是否被无意中放在同一行上。</span><span class="sxs-lookup"><span data-stu-id="7800e-110">Check to see if two different statements have inadvertently been put on the same line.</span></span>

2. <span data-ttu-id="7800e-111">在完成该语句的元素之后插入一个行结束符。</span><span class="sxs-lookup"><span data-stu-id="7800e-111">Insert a line terminator after the element that completes the statement.</span></span>

## <a name="see-also"></a><span data-ttu-id="7800e-112">另请参阅</span><span class="sxs-lookup"><span data-stu-id="7800e-112">See also</span></span>

- [<span data-ttu-id="7800e-113">如何：在代码中拆分和合并语句</span><span class="sxs-lookup"><span data-stu-id="7800e-113">How to: Break and Combine Statements in Code</span></span>](../../programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
- [<span data-ttu-id="7800e-114">语句</span><span class="sxs-lookup"><span data-stu-id="7800e-114">Statements</span></span>](../../programming-guide/language-features/statements.md)
