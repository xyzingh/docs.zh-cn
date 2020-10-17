---
ms.openlocfilehash: 24b88b3ba1b6cfe9fb9fb1f6398a6daeb57596a9
ms.sourcegitcommit: a8a205034eeffc7c3e1bdd6f506a75b0f7099ebf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91756100"
---
### <a name="order-of-tags-in-activitytags-is-reversed"></a><span data-ttu-id="a1c9d-101">Activity.Tags 中的标记顺序是相反的</span><span class="sxs-lookup"><span data-stu-id="a1c9d-101">Order of tags in Activity.Tags is reversed</span></span>

<span data-ttu-id="a1c9d-102"><xref:System.Diagnostics.Activity.Tags?displayProperty=nameWithType> 现根据项目的添加顺序将其存储在列表中，也就是说，添加的第一个项目排在列表第一位。</span><span class="sxs-lookup"><span data-stu-id="a1c9d-102"><xref:System.Diagnostics.Activity.Tags?displayProperty=nameWithType> now stores items in the list according to the order they are added, that is, the first item that's added is first in the list.</span></span> <span data-ttu-id="a1c9d-103">此更改是为了与 [OpenTelemetry 属性规范](https://github.com/open-telemetry/opentelemetry-specification/blob/master/specification/common/common.md#attributes)一致。</span><span class="sxs-lookup"><span data-stu-id="a1c9d-103">This change was made to match the [OpenTelemetry Attributes specification](https://github.com/open-telemetry/opentelemetry-specification/blob/master/specification/common/common.md#attributes).</span></span>

#### <a name="change-description"></a><span data-ttu-id="a1c9d-104">更改描述</span><span class="sxs-lookup"><span data-stu-id="a1c9d-104">Change description</span></span>

<span data-ttu-id="a1c9d-105">在以前的 .NET 版本中，<xref:System.Diagnostics.Activity.Tags?displayProperty=nameWithType> 存储项目的顺序与项目的添加顺序相反。</span><span class="sxs-lookup"><span data-stu-id="a1c9d-105">In previous .NET versions, <xref:System.Diagnostics.Activity.Tags?displayProperty=nameWithType> stores items in the reverse order from which they're added.</span></span> <span data-ttu-id="a1c9d-106">也就是说，添加的第一个项目排在列表中的最后一位。</span><span class="sxs-lookup"><span data-stu-id="a1c9d-106">That is, the first item added is last in the list.</span></span> <span data-ttu-id="a1c9d-107">从 .NET 5.0 开始，项目的顺序是相反的，添加的第一项始终排在列表第一位。</span><span class="sxs-lookup"><span data-stu-id="a1c9d-107">Starting in .NET 5.0, the order of the items is reversed, and the first item added is always first in the list.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="a1c9d-108">引入的版本</span><span class="sxs-lookup"><span data-stu-id="a1c9d-108">Version introduced</span></span>

<span data-ttu-id="a1c9d-109">5.0</span><span class="sxs-lookup"><span data-stu-id="a1c9d-109">5.0</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="a1c9d-110">建议操作</span><span class="sxs-lookup"><span data-stu-id="a1c9d-110">Recommended action</span></span>

<span data-ttu-id="a1c9d-111">如果应用依赖于 <xref:System.Diagnostics.Activity.Tags?displayProperty=nameWithType> 列表顺序，并且要升级到 .NET 5.0 或更高版本，则需要你更改代码的此部分。</span><span class="sxs-lookup"><span data-stu-id="a1c9d-111">If your app has a dependency on the <xref:System.Diagnostics.Activity.Tags?displayProperty=nameWithType> list order and you're upgrading to .NET 5.0 or later, you'll need to change this part of your code.</span></span>

#### <a name="category"></a><span data-ttu-id="a1c9d-112">类别</span><span class="sxs-lookup"><span data-stu-id="a1c9d-112">Category</span></span>

<span data-ttu-id="a1c9d-113">Core .NET 库</span><span class="sxs-lookup"><span data-stu-id="a1c9d-113">Core .NET libraries</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="a1c9d-114">受影响的 API</span><span class="sxs-lookup"><span data-stu-id="a1c9d-114">Affected APIs</span></span>

- <xref:System.Diagnostics.Activity.Tags?displayProperty=fullName>

<!--

#### Affected APIs

- `P:System.Diagnostics.Activity.Tags`

-->
