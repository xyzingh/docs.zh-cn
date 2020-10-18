---
title: XML 命名空间 URI“<uri>”可只绑定到“xmlns”
ms.date: 07/20/2015
f1_keywords:
- bc31183
- vbc31183
helpviewer_keywords:
- BC31183
ms.assetid: 0ab1dbce-8397-4959-b2cd-f58798b051a0
ms.openlocfilehash: 1aec6ac0a354bfe7e0378a2e46a70a7161bf6d36
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163241"
---
# <a name="bc31183-xml-namespace-uri-httpwwww3orgxml1998namespace-can-be-bound-only-to-xmlns"></a><span data-ttu-id="c37b0-102">BC31183： XML 命名空间 URI `http://www.w3.org/XML/1998/namespace` ; 只能绑定到 "xmlns"</span><span class="sxs-lookup"><span data-stu-id="c37b0-102">BC31183: XML namespace URI `http://www.w3.org/XML/1998/namespace`; can be bound only to 'xmlns'</span></span>

<span data-ttu-id="c37b0-103">URI `http://www.w3.org/XML/1998/namespace` 用于 XML 命名空间声明。</span><span class="sxs-lookup"><span data-stu-id="c37b0-103">The URI `http://www.w3.org/XML/1998/namespace` is used in an XML namespace declaration.</span></span> <span data-ttu-id="c37b0-104">此 URI 是保留命名空间，不能包含在 XML 命名空间声明中。</span><span class="sxs-lookup"><span data-stu-id="c37b0-104">This URI is a reserved namespace and cannot be included in an XML namespace declaration.</span></span>

 <span data-ttu-id="c37b0-105">**错误 ID：** BC31183</span><span class="sxs-lookup"><span data-stu-id="c37b0-105">**Error ID:** BC31183</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="c37b0-106">更正此错误</span><span class="sxs-lookup"><span data-stu-id="c37b0-106">To correct this error</span></span>

<span data-ttu-id="c37b0-107">删除 XML 命名空间声明，或将 URI 替换 `http://www.w3.org/XML/1998/namespace` 为有效的命名空间 URI。</span><span class="sxs-lookup"><span data-stu-id="c37b0-107">Remove the XML namespace declaration or replace the URI `http://www.w3.org/XML/1998/namespace` with a valid namespace URI.</span></span>

## <a name="see-also"></a><span data-ttu-id="c37b0-108">另请参阅</span><span class="sxs-lookup"><span data-stu-id="c37b0-108">See also</span></span>

- [<span data-ttu-id="c37b0-109">Imports 语句（XML 命名空间）</span><span class="sxs-lookup"><span data-stu-id="c37b0-109">Imports Statement (XML Namespace)</span></span>](../statements/imports-statement-xml-namespace.md)
- [<span data-ttu-id="c37b0-110">XML 文本</span><span class="sxs-lookup"><span data-stu-id="c37b0-110">XML Literals</span></span>](../xml-literals/index.md)
- [<span data-ttu-id="c37b0-111">XML</span><span class="sxs-lookup"><span data-stu-id="c37b0-111">XML</span></span>](../../programming-guide/language-features/xml/index.md)
