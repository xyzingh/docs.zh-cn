---
ms.openlocfilehash: 3164233f1ac056de385faa119143d75d3c2dc50c
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92224334"
---
> [!CAUTION]
> <span data-ttu-id="8e9a7-101">代码访问安全性 (CA) 和部分受信任代码</span><span class="sxs-lookup"><span data-stu-id="8e9a7-101">Code Access Security (CAS) and Partially Trusted Code</span></span>
>
> <span data-ttu-id="8e9a7-102">.NET Framework 提供一种机制，对在相同应用程序中运行的不同代码强制实施不同的信任级别，该机制称为代码访问安全性 (CAS)。</span><span class="sxs-lookup"><span data-stu-id="8e9a7-102">The .NET Framework provides a mechanism for the enforcement of varying levels of trust on different code running in the same application called Code Access Security (CAS).</span></span>
>
> <span data-ttu-id="8e9a7-103">**.NET Core、.NET 5 或更高版本中不支持 CAS。低于7.0 的 c # 版本不支持 CAS。**</span><span class="sxs-lookup"><span data-stu-id="8e9a7-103">**CAS is not supported in .NET Core, .NET 5, or later versions. CAS is not supported by versions of C# later than 7.0.**</span></span>
>
> <span data-ttu-id="8e9a7-104">.NET Framework 中的 CAS 不应作为一种机制，用于根据代码来源或其他标识方面强制实施安全边界。</span><span class="sxs-lookup"><span data-stu-id="8e9a7-104">CAS in .NET Framework should not be used as a mechanism for enforcing security boundaries based on code origination or other identity aspects.</span></span> <span data-ttu-id="8e9a7-105">CA 和 Security-Transparent 代码不支持用作部分受信任的代码（尤其是未知来源的代码）的安全边界。</span><span class="sxs-lookup"><span data-stu-id="8e9a7-105">CAS and Security-Transparent Code are not supported as a security boundary with partially trusted code, especially code of unknown origin.</span></span> <span data-ttu-id="8e9a7-106">建议在未实施其他安全措施的情况下，不要加载和执行未知来源的代码。</span><span class="sxs-lookup"><span data-stu-id="8e9a7-106">We advise against loading and executing code of unknown origins without putting alternative security measures in place.</span></span> <span data-ttu-id="8e9a7-107">.NET Framework 不会为可能会针对 CAS 沙盒发现的任何特权提升攻击发出安全修补程序。</span><span class="sxs-lookup"><span data-stu-id="8e9a7-107">.NET Framework will not issue security patches for any elevation-of-privilege exploits that might be discovered against the CAS sandbox.</span></span>
>
> <span data-ttu-id="8e9a7-108">此策略适用于 .NET Framework 的所有版本，但不适用于 Silverlight 中所含的 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="8e9a7-108">This policy applies to all versions of .NET Framework, but does not apply to the .NET Framework included in Silverlight.</span></span>
