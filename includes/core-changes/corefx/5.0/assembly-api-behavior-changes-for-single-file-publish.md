---
ms.openlocfilehash: 0d6847b7a937094f36efae70ae450cc37824221d
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2020
ms.locfileid: "91955547"
---
### <a name="assembly-related-api-behavior-changes-for-single-file-publishing-format"></a><span data-ttu-id="b9997-101">适用于单文件发布格式的与程序集相关 API 行为更改</span><span class="sxs-lookup"><span data-stu-id="b9997-101">Assembly-related API behavior changes for single-file publishing format</span></span>

<span data-ttu-id="b9997-102">与程序集的文件位置相关的多个 API 在以单文件发布格式调用时行为发生更改。</span><span class="sxs-lookup"><span data-stu-id="b9997-102">Multiple APIs related to an assembly's file location have behavior changes when they're invoked in a single-file publishing format.</span></span>

#### <a name="change-description"></a><span data-ttu-id="b9997-103">更改描述</span><span class="sxs-lookup"><span data-stu-id="b9997-103">Change description</span></span>

<span data-ttu-id="b9997-104">在针对 .NET 5.0 及更高版本的单文件发布中，从内存中加载捆绑程序集，而不是提取到磁盘。</span><span class="sxs-lookup"><span data-stu-id="b9997-104">In single-file publishing for .NET 5.0 and later versions, bundled assemblies are loaded from memory instead of extracted to disk.</span></span> <span data-ttu-id="b9997-105">对于单文件发布的应用，这意味着某些与位置相关的 API 在 .NET 5.0 及更高版本上返回的值与在以前版本的 .NET 上返回的值不同。</span><span class="sxs-lookup"><span data-stu-id="b9997-105">For single-file published apps, this means that certain location-related APIs return different values on .NET 5.0 and later than on previous versions of .NET.</span></span> <span data-ttu-id="b9997-106">更改如下：</span><span class="sxs-lookup"><span data-stu-id="b9997-106">The changes are as follows:</span></span>

| <span data-ttu-id="b9997-107">API</span><span class="sxs-lookup"><span data-stu-id="b9997-107">API</span></span> | <span data-ttu-id="b9997-108">以前的版本</span><span class="sxs-lookup"><span data-stu-id="b9997-108">Previous versions</span></span> | <span data-ttu-id="b9997-109">.NET 5.0 及更高版本</span><span class="sxs-lookup"><span data-stu-id="b9997-109">.NET 5.0 and later</span></span> |
| - | - | - |
| <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType> | <span data-ttu-id="b9997-110">返回提取的 DLL 文件路径</span><span class="sxs-lookup"><span data-stu-id="b9997-110">Returns extracted DLL file path</span></span> | <span data-ttu-id="b9997-111">为捆绑的程序集返回空字符串</span><span class="sxs-lookup"><span data-stu-id="b9997-111">Returns empty string for bundled assemblies</span></span> |
| <xref:System.Reflection.Assembly.CodeBase?displayProperty=nameWithType> | <span data-ttu-id="b9997-112">返回提取的 DLL 文件路径</span><span class="sxs-lookup"><span data-stu-id="b9997-112">Returns extracted DLL file path</span></span> | <span data-ttu-id="b9997-113">引发捆绑的程序集的异常</span><span class="sxs-lookup"><span data-stu-id="b9997-113">Throws exception for bundled assemblies</span></span> |
| <xref:System.Reflection.Assembly.GetFile(System.String)?displayProperty=nameWithType> | <span data-ttu-id="b9997-114">为捆绑的程序集返回 `null`</span><span class="sxs-lookup"><span data-stu-id="b9997-114">Returns `null` for bundled assemblies</span></span> | <span data-ttu-id="b9997-115">引发捆绑的程序集的异常</span><span class="sxs-lookup"><span data-stu-id="b9997-115">Throws exception for bundled assemblies</span></span> |
| `Environment.GetCommandLineArgs()[0]` | <span data-ttu-id="b9997-116">值是入口点 DLL 的名称</span><span class="sxs-lookup"><span data-stu-id="b9997-116">Value is the name of the entry point DLL</span></span> | <span data-ttu-id="b9997-117">值是主机可执行文件的名称</span><span class="sxs-lookup"><span data-stu-id="b9997-117">Value is the name of the host executable</span></span> |
| <xref:System.AppContext.BaseDirectory?displayProperty=nameWithType> | <span data-ttu-id="b9997-118">值是临时提取目录</span><span class="sxs-lookup"><span data-stu-id="b9997-118">Value is the temporary extraction directory</span></span> | <span data-ttu-id="b9997-119">值是主机可执行文件的包含目录</span><span class="sxs-lookup"><span data-stu-id="b9997-119">Value is the containing directory of the host executable</span></span> |

#### <a name="version-introduced"></a><span data-ttu-id="b9997-120">引入的版本</span><span class="sxs-lookup"><span data-stu-id="b9997-120">Version introduced</span></span>

<span data-ttu-id="b9997-121">5.0</span><span class="sxs-lookup"><span data-stu-id="b9997-121">5.0</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="b9997-122">建议操作</span><span class="sxs-lookup"><span data-stu-id="b9997-122">Recommended action</span></span>

<span data-ttu-id="b9997-123">作为单个文件发布时，避免依赖程序集的文件位置。</span><span class="sxs-lookup"><span data-stu-id="b9997-123">Avoid dependencies on the file location of assemblies when publishing as a single file.</span></span>

#### <a name="category"></a><span data-ttu-id="b9997-124">类别</span><span class="sxs-lookup"><span data-stu-id="b9997-124">Category</span></span>

- <span data-ttu-id="b9997-125">Core .NET 库</span><span class="sxs-lookup"><span data-stu-id="b9997-125">Core .NET libraries</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="b9997-126">受影响的 API</span><span class="sxs-lookup"><span data-stu-id="b9997-126">Affected APIs</span></span>

- <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType>
- <xref:System.Reflection.Assembly.CodeBase?displayProperty=nameWithType>
- <xref:System.Reflection.Assembly.GetFile(System.String)?displayProperty=nameWithType>
- <xref:System.Environment.GetCommandLineArgs?displayProperty=nameWithType>
- <xref:System.AppContext.BaseDirectory?displayProperty=nameWithType>

<!--

#### Affected APIs

- `P:System.Reflection.Assembly.Location`
- `P:System.Reflection.Assembly.CodeBase`
- `M:System.Reflection.Assembly.GetFile(System.String)`
- `M:System.Environment.GetCommandLineArgs`
- `P:System.AppContext.BaseDirectory`

-->
