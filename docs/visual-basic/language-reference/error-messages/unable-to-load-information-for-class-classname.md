---
title: 无法加载类“<classname>”的信息
ms.date: 07/20/2015
f1_keywords:
- vbc30712
- bc30712
helpviewer_keywords:
- BC30712
ms.assetid: c7ffbd6d-05c6-4261-b44b-1bcd521bb350
ms.openlocfilehash: 05c3303db90a396479bc396c5c2395c3afbb59ae
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92161603"
---
# <a name="bc30712-unable-to-load-information-for-class-classname"></a><span data-ttu-id="73e7b-102">BC30712：无法加载类 "" 的信息 \<classname></span><span class="sxs-lookup"><span data-stu-id="73e7b-102">BC30712: Unable to load information for class '\<classname>'</span></span>

<span data-ttu-id="73e7b-103">对不提供的类进行了引用。</span><span class="sxs-lookup"><span data-stu-id="73e7b-103">A reference was made to a class that is not available.</span></span>

 <span data-ttu-id="73e7b-104">**错误 ID：** BC30712</span><span class="sxs-lookup"><span data-stu-id="73e7b-104">**Error ID:** BC30712</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="73e7b-105">更正此错误</span><span class="sxs-lookup"><span data-stu-id="73e7b-105">To correct this error</span></span>

1. <span data-ttu-id="73e7b-106">验证是否定义了类，并且是否正确拼写了名称。</span><span class="sxs-lookup"><span data-stu-id="73e7b-106">Verify that the class is defined and that you spelled the name correctly.</span></span>

2. <span data-ttu-id="73e7b-107">尝试访问该模块中声明的其中一个成员。</span><span class="sxs-lookup"><span data-stu-id="73e7b-107">Try accessing one of the members declared in the module.</span></span> <span data-ttu-id="73e7b-108">在某些情况下，调试环境找不到成员，因为尚未加载在其中声明成员的模块。</span><span class="sxs-lookup"><span data-stu-id="73e7b-108">In some cases, the debugging environment cannot locate members because the modules where they are declared have not been loaded yet.</span></span>

## <a name="see-also"></a><span data-ttu-id="73e7b-109">请参阅</span><span class="sxs-lookup"><span data-stu-id="73e7b-109">See also</span></span>

- [<span data-ttu-id="73e7b-110">在 Visual Studio 中进行调试</span><span class="sxs-lookup"><span data-stu-id="73e7b-110">Debugging in Visual Studio</span></span>](/visualstudio/debugger/debugger-feature-tour)
