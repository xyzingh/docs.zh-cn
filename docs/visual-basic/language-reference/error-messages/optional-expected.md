---
title: 需要“Optional”
ms.date: 07/20/2015
f1_keywords:
- bc30202
- vbc30202
helpviewer_keywords:
- BC30202
ms.assetid: 6f75060c-2db4-4a79-b5d1-5780c09a74cd
ms.openlocfilehash: 9c717cef2052722563e04595ef7a808ea103a75d
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92159815"
---
# <a name="bc30202-optional-expected"></a><span data-ttu-id="b0b85-102">BC30202：应为 "Optional"</span><span class="sxs-lookup"><span data-stu-id="b0b85-102">BC30202: 'Optional' expected</span></span>

<span data-ttu-id="b0b85-103">过程声明中的可选参数后跟必需的参数。</span><span class="sxs-lookup"><span data-stu-id="b0b85-103">An optional argument in a procedure declaration is followed by a required argument.</span></span> <span data-ttu-id="b0b85-104">可选参数后面的每个参数都必须是可选的。</span><span class="sxs-lookup"><span data-stu-id="b0b85-104">Every argument following an optional argument must also be optional.</span></span>

 <span data-ttu-id="b0b85-105">**错误 ID：** BC30202</span><span class="sxs-lookup"><span data-stu-id="b0b85-105">**Error ID:** BC30202</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="b0b85-106">更正此错误</span><span class="sxs-lookup"><span data-stu-id="b0b85-106">To correct this error</span></span>

- <span data-ttu-id="b0b85-107">如果需要参数，请将其移动到自变量列表中的第一个可选参数之前。</span><span class="sxs-lookup"><span data-stu-id="b0b85-107">If the argument is intended to be required, move it to precede the first optional argument in the argument list.</span></span>

- <span data-ttu-id="b0b85-108">如果参数旨在作为可选参数，请使用 `Optional` 关键字。</span><span class="sxs-lookup"><span data-stu-id="b0b85-108">If the argument is intended to be optional, use the `Optional` keyword.</span></span>

## <a name="see-also"></a><span data-ttu-id="b0b85-109">另请参阅</span><span class="sxs-lookup"><span data-stu-id="b0b85-109">See also</span></span>

- [<span data-ttu-id="b0b85-110">可选参数</span><span class="sxs-lookup"><span data-stu-id="b0b85-110">Optional Parameters</span></span>](../../programming-guide/language-features/procedures/optional-parameters.md)
