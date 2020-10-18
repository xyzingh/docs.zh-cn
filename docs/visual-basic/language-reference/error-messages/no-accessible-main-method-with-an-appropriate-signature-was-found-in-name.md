---
title: 在“<name>”中找不到任何具有合适签名的可访问“Main”方法
ms.date: 07/20/2015
f1_keywords:
- bc30737
- vbc30737
helpviewer_keywords:
- BC30737
ms.assetid: 3f40bacd-3fac-4741-b204-852f693d4340
ms.openlocfilehash: e1f95484a153bdcac9543508b7f2708dc6b7d942
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160036"
---
# <a name="bc30737-no-accessible-main-method-with-an-appropriate-signature-was-found-in-name"></a><span data-ttu-id="99414-102">BC30737：在 "" 中找不到带有适当签名的可访问 "Main" 方法 \<name></span><span class="sxs-lookup"><span data-stu-id="99414-102">BC30737: No accessible 'Main' method with an appropriate signature was found in '\<name>'</span></span>

<span data-ttu-id="99414-103">命令行应用程序必须具有 `Sub Main` 定义的。</span><span class="sxs-lookup"><span data-stu-id="99414-103">Command-line applications must have a `Sub Main` defined.</span></span> <span data-ttu-id="99414-104">`Main` 必须声明为 `Public Shared` ，如同它是在类中定义的一样，或与 `Public` 在模块中定义的一样。</span><span class="sxs-lookup"><span data-stu-id="99414-104">`Main` must be declared as `Public Shared` if it is defined in a class, or as `Public` if defined in a module.</span></span>

 <span data-ttu-id="99414-105">**错误 ID：** BC30737</span><span class="sxs-lookup"><span data-stu-id="99414-105">**Error ID:** BC30737</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="99414-106">更正此错误</span><span class="sxs-lookup"><span data-stu-id="99414-106">To correct this error</span></span>

- <span data-ttu-id="99414-107">定义 `Public Sub Main` 项目的过程。</span><span class="sxs-lookup"><span data-stu-id="99414-107">Define a `Public Sub Main` procedure for your project.</span></span> <span data-ttu-id="99414-108">当 `Shared` 且仅当在类中定义时，才将其声明为。</span><span class="sxs-lookup"><span data-stu-id="99414-108">Declare it as `Shared` if and only if you define it inside a class.</span></span>

## <a name="see-also"></a><span data-ttu-id="99414-109">另请参阅</span><span class="sxs-lookup"><span data-stu-id="99414-109">See also</span></span>

- [<span data-ttu-id="99414-110">Visual Basic 程序的结构</span><span class="sxs-lookup"><span data-stu-id="99414-110">Structure of a Visual Basic Program</span></span>](../../programming-guide/program-structure/structure-of-a-visual-basic-program.md)
- [<span data-ttu-id="99414-111">过程</span><span class="sxs-lookup"><span data-stu-id="99414-111">Procedures</span></span>](../../programming-guide/language-features/procedures/index.md)
