---
ms.openlocfilehash: 80d13609f1b02ae0ac875b2028e745670bb8f503
ms.sourcegitcommit: 39b1d5f2978be15409c189a66ab30781d9082cd8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2020
ms.locfileid: "92050556"
---
### <a name="frameworkdescriptions-value-is-net-instead-of-net-core"></a><span data-ttu-id="f2994-101">FrameworkDescription 的值是 .NET 而不是 .NET Core</span><span class="sxs-lookup"><span data-stu-id="f2994-101">FrameworkDescription's value is .NET instead of .NET Core</span></span>

<span data-ttu-id="f2994-102"><xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=nameWithType> 现在返回“.NET”而不是“.NET Core”。</span><span class="sxs-lookup"><span data-stu-id="f2994-102"><xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=nameWithType> now returns ".NET" instead of ".NET Core".</span></span>

#### <a name="change-description"></a><span data-ttu-id="f2994-103">更改描述</span><span class="sxs-lookup"><span data-stu-id="f2994-103">Change description</span></span>

<span data-ttu-id="f2994-104">在以前的 .NET 版本中，<xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=nameWithType> 返回“.NET Core”作为描述字符串的一部分，例如 `.NET Core 3.1.1`。</span><span class="sxs-lookup"><span data-stu-id="f2994-104">In previous .NET versions, <xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=nameWithType> returns ".NET Core" as part of the description string, for example, `.NET Core 3.1.1`.</span></span>

<span data-ttu-id="f2994-105">从 .NET 5.0 开始，<xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=nameWithType> 返回“.NET”作为描述字符串的一部分，例如 `.NET 5.0.0`。</span><span class="sxs-lookup"><span data-stu-id="f2994-105">Starting in .NET 5.0, <xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=nameWithType> returns ".NET" as part of the description string, for example, `.NET 5.0.0`.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="f2994-106">更改原因</span><span class="sxs-lookup"><span data-stu-id="f2994-106">Reason for change</span></span>

<span data-ttu-id="f2994-107">对于 .NET 5，`netcoreapp` 替换为 `net`，作为简短的目标框架名字对象。</span><span class="sxs-lookup"><span data-stu-id="f2994-107">With .NET 5, `netcoreapp` is replaced by `net` as the short target-framework moniker.</span></span> <span data-ttu-id="f2994-108">为了保持一致性，框架描述也进行了更新。</span><span class="sxs-lookup"><span data-stu-id="f2994-108">For consistency, the framework's description has also been updated.</span></span> <span data-ttu-id="f2994-109">该更改只浮于表面，因为除了在 <xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=nameWithType> 属性中，`FrameworkName` 未在其他任何地方进行编码。</span><span class="sxs-lookup"><span data-stu-id="f2994-109">The change is cosmetic, as the `FrameworkName` isn't encoded anywhere else than in the <xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=nameWithType> property.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="f2994-110">引入的版本</span><span class="sxs-lookup"><span data-stu-id="f2994-110">Version introduced</span></span>

<span data-ttu-id="f2994-111">5.0</span><span class="sxs-lookup"><span data-stu-id="f2994-111">5.0</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="f2994-112">建议操作</span><span class="sxs-lookup"><span data-stu-id="f2994-112">Recommended action</span></span>

<span data-ttu-id="f2994-113">更新搜索 <xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription> 返回的字符串中“.NET Core”的所有代码。</span><span class="sxs-lookup"><span data-stu-id="f2994-113">Update any code that searches for ".NET Core" in the string returned by <xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription>.</span></span>

#### <a name="category"></a><span data-ttu-id="f2994-114">类别</span><span class="sxs-lookup"><span data-stu-id="f2994-114">Category</span></span>

<span data-ttu-id="f2994-115">Core .NET 库</span><span class="sxs-lookup"><span data-stu-id="f2994-115">Core .NET libraries</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="f2994-116">受影响的 API</span><span class="sxs-lookup"><span data-stu-id="f2994-116">Affected APIs</span></span>

- <xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=fullName>

<!--

#### Affected APIs

- `P:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription`

-->
