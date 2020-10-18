---
title: 友元程序集引用 <reference> 无效
ms.date: 07/20/2015
f1_keywords:
- vbc31535
- bc31535
helpviewer_keywords:
- BC31535
ms.assetid: 6540c1d0-bb19-4051-a579-2e4f9094585e
ms.openlocfilehash: a42dd99ffaa06dce4823ce5d022fac02ae99c6bd
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160706"
---
# <a name="bc31535-friend-assembly-reference-reference-is-invalid"></a><span data-ttu-id="dd45f-102">BC31535：友元程序集引用 \<reference> 无效</span><span class="sxs-lookup"><span data-stu-id="dd45f-102">BC31535: Friend assembly reference \<reference> is invalid</span></span>

<span data-ttu-id="dd45f-103">友元程序集引用 \<reference> 无效。</span><span class="sxs-lookup"><span data-stu-id="dd45f-103">Friend assembly reference \<reference> is invalid.</span></span> <span data-ttu-id="dd45f-104">用强名称签名的程序集必须在他们的 InternalsVisibleTo 声明中指定一个公钥。</span><span class="sxs-lookup"><span data-stu-id="dd45f-104">Strong-name signed assemblies must specify a public key in their InternalsVisibleTo declarations.</span></span>

 <span data-ttu-id="dd45f-105">传递给特性构造函数的程序集名称 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 标识强名称程序集，但不包括 `PublicKey` 特性。</span><span class="sxs-lookup"><span data-stu-id="dd45f-105">The assembly name passed to the <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> attribute constructor identifies a strong-named assembly, but it does not include a `PublicKey` attribute.</span></span>

 <span data-ttu-id="dd45f-106">**错误 ID：** BC31535</span><span class="sxs-lookup"><span data-stu-id="dd45f-106">**Error ID:** BC31535</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="dd45f-107">更正此错误</span><span class="sxs-lookup"><span data-stu-id="dd45f-107">To correct this error</span></span>

1. <span data-ttu-id="dd45f-108">确定强名称友元程序集的公钥。</span><span class="sxs-lookup"><span data-stu-id="dd45f-108">Determine the public key for the strong-named friend assembly.</span></span> <span data-ttu-id="dd45f-109">使用属性将公钥包含为传递给特性构造函数的程序集名称的一部分 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> `PublicKey` 。</span><span class="sxs-lookup"><span data-stu-id="dd45f-109">Include the public key as part of the assembly name passed to the <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> attribute constructor by using the `PublicKey` attribute.</span></span>

## <a name="see-also"></a><span data-ttu-id="dd45f-110">另请参阅</span><span class="sxs-lookup"><span data-stu-id="dd45f-110">See also</span></span>

- <xref:System.Reflection.AssemblyName>
- [<span data-ttu-id="dd45f-111">友元程序集</span><span class="sxs-lookup"><span data-stu-id="dd45f-111">Friend Assemblies</span></span>](../../../standard/assembly/friend.md)
