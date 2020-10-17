---
title: .NET API 分析器
description: 了解 .NET API 分析器如何有助于检测弃用的 API 和平台兼容性问题。
author: oliag
ms.date: 02/20/2020
ms.technology: dotnet-standard
ms.openlocfilehash: a689ae347efbc8c2dd933b2f6920ac6cc06cda7d
ms.sourcegitcommit: a8a205034eeffc7c3e1bdd6f506a75b0f7099ebf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91756190"
---
# <a name="net-api-analyzer"></a><span data-ttu-id="25478-103">.NET API 分析器</span><span class="sxs-lookup"><span data-stu-id="25478-103">.NET API analyzer</span></span>

<span data-ttu-id="25478-104">.NET API 分析器是 Roslyn 分析器，可用于发现不同平台上的潜在 C# API 兼容性风险，并检测是否调用了弃用的 API。</span><span class="sxs-lookup"><span data-stu-id="25478-104">The .NET API Analyzer is a Roslyn analyzer that discovers potential compatibility risks for C# APIs on different platforms and detects calls to deprecated APIs.</span></span> <span data-ttu-id="25478-105">可供所有 C# 开发人员在任何开发阶段使用。</span><span class="sxs-lookup"><span data-stu-id="25478-105">It can be useful for all C# developers at any stage of development.</span></span>

<span data-ttu-id="25478-106">API 分析器以 NuGet 包 [Microsoft.DotNet.Analyzers.Compatibility](https://www.nuget.org/packages/Microsoft.DotNet.Analyzers.Compatibility/) 的形式提供。</span><span class="sxs-lookup"><span data-stu-id="25478-106">API Analyzer comes as a NuGet package [Microsoft.DotNet.Analyzers.Compatibility](https://www.nuget.org/packages/Microsoft.DotNet.Analyzers.Compatibility/).</span></span> <span data-ttu-id="25478-107">在项目中引用此分析器后，它就会自动监视代码，并指出有问题的 API 使用。</span><span class="sxs-lookup"><span data-stu-id="25478-107">After you reference it in a project, it automatically monitors the code and indicates problematic API usage.</span></span> <span data-ttu-id="25478-108">还可以单击灯泡图标，获取有关可能解决方案的建议。</span><span class="sxs-lookup"><span data-stu-id="25478-108">You can also get suggestions on possible fixes by clicking on the light bulb.</span></span> <span data-ttu-id="25478-109">下拉菜单包括禁止显示警告的选项。</span><span class="sxs-lookup"><span data-stu-id="25478-109">The drop-down menu includes an option to suppress the warnings.</span></span>

> [!NOTE]
> <span data-ttu-id="25478-110">.NET API 分析器仍为预发行版。</span><span class="sxs-lookup"><span data-stu-id="25478-110">The .NET API analyzer is still a pre-release version.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25478-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="25478-111">Prerequisites</span></span>

- <span data-ttu-id="25478-112">Visual Studio 2017 及更高版本，或 Visual Studio for Mac（所有版本）。</span><span class="sxs-lookup"><span data-stu-id="25478-112">Visual Studio 2017 and later versions, or Visual Studio for Mac (all versions).</span></span>

## <a name="discover-deprecated-apis"></a><span data-ttu-id="25478-113">发现弃用的 API</span><span class="sxs-lookup"><span data-stu-id="25478-113">Discover deprecated APIs</span></span>

### <a name="what-are-deprecated-apis"></a><span data-ttu-id="25478-114">什么是弃用的 API？</span><span class="sxs-lookup"><span data-stu-id="25478-114">What are deprecated APIs?</span></span>

<span data-ttu-id="25478-115">.NET 系列是一组不断升级的大型产品，力求更好地满足客户需求。</span><span class="sxs-lookup"><span data-stu-id="25478-115">The .NET family is a set of large products that are constantly upgraded to better serve customer needs.</span></span> <span data-ttu-id="25478-116">弃用并将一些 API 替换为新 API 是很自然的。</span><span class="sxs-lookup"><span data-stu-id="25478-116">It's natural to deprecate some APIs and replace them with new ones.</span></span> <span data-ttu-id="25478-117">若有更好的替换 API，API 便会被视为弃用。</span><span class="sxs-lookup"><span data-stu-id="25478-117">An API is considered deprecated when a better alternative exists.</span></span> <span data-ttu-id="25478-118">指明 API 已遭弃用且不得使用的一种方法是，用 <xref:System.ObsoleteAttribute> 属性标记它。</span><span class="sxs-lookup"><span data-stu-id="25478-118">One way to inform that an API is deprecated and shouldn't be used is to mark it with the <xref:System.ObsoleteAttribute> attribute.</span></span> <span data-ttu-id="25478-119">这种方法的缺点是，所有已过时 API 都只有一个诊断 ID（对于 C#，ID 为 [CS0612](../../csharp/misc/cs0612.md)）。</span><span class="sxs-lookup"><span data-stu-id="25478-119">The disadvantage of this approach is that there is only one diagnostic ID for all obsolete APIs (for C#, [CS0612](../../csharp/misc/cs0612.md)).</span></span> <span data-ttu-id="25478-120">这表示：</span><span class="sxs-lookup"><span data-stu-id="25478-120">This means that:</span></span>

- <span data-ttu-id="25478-121">无法为每个事例设置专用文档。</span><span class="sxs-lookup"><span data-stu-id="25478-121">It's impossible to have dedicated documents for each case.</span></span>
- <span data-ttu-id="25478-122">无法禁止显示特定类别的警告。</span><span class="sxs-lookup"><span data-stu-id="25478-122">It's impossible to suppress certain category of warnings.</span></span> <span data-ttu-id="25478-123">要么禁止显示所有警告，要么允许显示所有警告。</span><span class="sxs-lookup"><span data-stu-id="25478-123">You can suppress either all or none of them.</span></span>
- <span data-ttu-id="25478-124">为了通知用户有新弃用，必须更新引用的程序集或目标包。</span><span class="sxs-lookup"><span data-stu-id="25478-124">To inform users of a new deprecation, a referenced assembly or targeting package has to be updated.</span></span>

<span data-ttu-id="25478-125">API 分析器使用 API 专用错误代码，这些代码以 DE（全称是“Deprecation Error”（弃用错误））开头，这样就可以单独控制各个警告的显示。</span><span class="sxs-lookup"><span data-stu-id="25478-125">The API Analyzer uses API-specific error codes that begin with DE (which stands for Deprecation Error), which allows control over the display of individual warnings.</span></span> <span data-ttu-id="25478-126">分析器发现的弃用的 API 在 [dotnet/platform-compat](https://github.com/dotnet/platform-compat) 存储库中进行定义。</span><span class="sxs-lookup"><span data-stu-id="25478-126">The deprecated APIs identified by the analyzer are defined in the [dotnet/platform-compat](https://github.com/dotnet/platform-compat) repo.</span></span>

### <a name="add-the-api-analyzer-to-your-project"></a><span data-ttu-id="25478-127">将 API 分析器添加到项目</span><span class="sxs-lookup"><span data-stu-id="25478-127">Add the API Analyzer to your project</span></span>

1. <span data-ttu-id="25478-128">打开 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="25478-128">Open Visual Studio.</span></span>
2. <span data-ttu-id="25478-129">打开要在其中运行分析器的项目。</span><span class="sxs-lookup"><span data-stu-id="25478-129">Open the project you want to run the analyzer on.</span></span>
3. <span data-ttu-id="25478-130">在解决方案资源管理器中，右键单击项目并选择“管理 NuGet 包”   。</span><span class="sxs-lookup"><span data-stu-id="25478-130">In **Solution Explorer**, right-click on your project and choose **Manage NuGet Packages**.</span></span> <span data-ttu-id="25478-131">（也可以在“项目”  菜单中选择此选项。）</span><span class="sxs-lookup"><span data-stu-id="25478-131">(This option is also available from the **Project** menu.)</span></span>
4. <span data-ttu-id="25478-132">在“NuGet 包管理器”选项卡上：</span><span class="sxs-lookup"><span data-stu-id="25478-132">On the NuGet Package Manager tab:</span></span>
   1. <span data-ttu-id="25478-133">选择“nuget.org”作为“包源”。</span><span class="sxs-lookup"><span data-stu-id="25478-133">Select "nuget.org" as the Package source.</span></span>
   2. <span data-ttu-id="25478-134">转到“浏览”  选项卡。</span><span class="sxs-lookup"><span data-stu-id="25478-134">Go to the **Browse** tab.</span></span>
   3. <span data-ttu-id="25478-135">选择“包括预发行版”。 </span><span class="sxs-lookup"><span data-stu-id="25478-135">Select **Include prerelease**.</span></span>
   4. <span data-ttu-id="25478-136">搜索 Microsoft.DotNet.Analyzers.Compatibility  。</span><span class="sxs-lookup"><span data-stu-id="25478-136">Search for **Microsoft.DotNet.Analyzers.Compatibility**.</span></span>
   5. <span data-ttu-id="25478-137">选择列表中的包。</span><span class="sxs-lookup"><span data-stu-id="25478-137">Select that package in the list.</span></span>
   6. <span data-ttu-id="25478-138">选择“安装”按钮  。</span><span class="sxs-lookup"><span data-stu-id="25478-138">Select the **Install** button.</span></span>
   7. <span data-ttu-id="25478-139">选择“预览更改”对话框上的“确定”按钮，如果你同意所列包的许可条款，则选择“接受许可”对话框上的“我接受”按钮。</span><span class="sxs-lookup"><span data-stu-id="25478-139">Select the **OK** button on the **Preview Changes** dialog and then select the **I Accept** button on the **License Acceptance** dialog if you agree with the license terms for the packages listed.</span></span>

### <a name="use-the-api-analyzer"></a><span data-ttu-id="25478-140">使用 API 分析器</span><span class="sxs-lookup"><span data-stu-id="25478-140">Use the API Analyzer</span></span>

<span data-ttu-id="25478-141">如果代码使用了弃用的 API（如 <xref:System.Net.WebClient>），API 分析器便会使用绿色波浪线突出显示它。</span><span class="sxs-lookup"><span data-stu-id="25478-141">When a deprecated API, such as <xref:System.Net.WebClient>, is used in a code, API Analyzer highlights it with a green squiggly line.</span></span> <span data-ttu-id="25478-142">如果将鼠标悬停在 API 调用之上，就会看到包含 API 弃用相关信息的灯泡，如下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="25478-142">When you hover over the API call, a light bulb is displayed with information about the API deprecation, as in the following example:</span></span>

![显示绿色波浪线且左侧有灯泡的 WebClient API 的屏幕截图。](media/api-analyzer/green-squiggle.jpg)

<span data-ttu-id="25478-144">弃用的 API 每出现一次，“错误列表”  窗口中都会显示具有唯一 ID 的警告，如下面的示例所示 (`DE004`)：</span><span class="sxs-lookup"><span data-stu-id="25478-144">The **Error List** window contains warnings with a unique ID per deprecated API, as shown in the following example (`DE004`):</span></span>

<span data-ttu-id="25478-145">![显示警告 ID 和说明的“错误列表”窗口的屏幕截图。](media/api-analyzer/warnings-id-and-descriptions.jpg "包含警告的错误列表窗口。")</span><span class="sxs-lookup"><span data-stu-id="25478-145">![Screenshot of the Error List window showing warning's ID and description.](media/api-analyzer/warnings-id-and-descriptions.jpg "Error List window that includes warnings.")</span></span>

<span data-ttu-id="25478-146">单击 ID 后，便会转到详细信息网页，其中说明了 API 遭弃用的原因，以及有关可用替换 API 的建议。</span><span class="sxs-lookup"><span data-stu-id="25478-146">By clicking on the ID, you go to a webpage with detailed information about why the API was deprecated and suggestions regarding alternative APIs that can be used.</span></span>

<span data-ttu-id="25478-147">可以禁止显示任何警告，具体方法是右键单击突出显示的成员，然后选择“禁止\<diagnostic ID>”。</span><span class="sxs-lookup"><span data-stu-id="25478-147">Any warnings can be suppressed by right-clicking on the highlighted member and selecting **Suppress \<diagnostic ID>**.</span></span> <span data-ttu-id="25478-148">禁止显示警告的方法有两种：</span><span class="sxs-lookup"><span data-stu-id="25478-148">There are two ways to suppress warnings:</span></span>

- [<span data-ttu-id="25478-149">本地（在源中）</span><span class="sxs-lookup"><span data-stu-id="25478-149">locally (in source)</span></span>](#suppress-warnings-locally)
- <span data-ttu-id="25478-150">[全局（在禁止文件中）](#suppress-warnings-globally)- 推荐方法</span><span class="sxs-lookup"><span data-stu-id="25478-150">[globally (in a suppression file)](#suppress-warnings-globally) - recommended</span></span>

### <a name="suppress-warnings-locally"></a><span data-ttu-id="25478-151">在本地禁止显示警告</span><span class="sxs-lookup"><span data-stu-id="25478-151">Suppress warnings locally</span></span>

<span data-ttu-id="25478-152">若要在本地禁止显示警告，请右键单击要对其禁止显示警告的成员，然后依次选择“快速操作和重构” > “禁止 诊断 ID \<diagnostic ID>” > “在源中”。</span><span class="sxs-lookup"><span data-stu-id="25478-152">To suppress warnings locally, right-click on the member you want to suppress warnings for and then select **Quick Actions and Refactorings** > **Suppress *diagnostic ID*\<diagnostic ID>** > **in Source**.</span></span> <span data-ttu-id="25478-153">此时，[#pragma](../../csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning.md) 警告预处理器指令会添加到定义的范围内的源代码中：![用 #pragma warning disable 指令框定的代码的屏幕截图。](media/api-analyzer/suppress-in-source.jpg)</span><span class="sxs-lookup"><span data-stu-id="25478-153">The [#pragma](../../csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning.md) warning preprocessor directive is added to your source code in the scope defined: ![Screenshot of code framed with #pragma warning disable.](media/api-analyzer/suppress-in-source.jpg)</span></span>

### <a name="suppress-warnings-globally"></a><span data-ttu-id="25478-154">在全局禁止显示警告</span><span class="sxs-lookup"><span data-stu-id="25478-154">Suppress warnings globally</span></span>

<span data-ttu-id="25478-155">若要在全局禁止显示警告，请右键单击要对其禁止显示警告的成员，然后依次选择“快速操作和重构” > “禁止诊断 ID\<diagnostic ID>” > “在禁止文件中”。</span><span class="sxs-lookup"><span data-stu-id="25478-155">To suppress warnings globally, right-click on the member you want to suppress warnings for and then select **Quick Actions and Refactorings** > **Suppress *diagnostic ID*\<diagnostic ID>** > **in Suppression File**.</span></span>

![右键单击菜单的屏幕截图，其中显示了用于在 Visual Studio 中禁止显示警告的选项。](media/api-analyzer/suppress-in-sup-file.jpg)

<span data-ttu-id="25478-157">首次禁止后，GlobalSuppressions.cs  文件会添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="25478-157">A *GlobalSuppressions.cs* file is added to your project after the first suppression.</span></span> <span data-ttu-id="25478-158">此时，新的全局禁止会追加到此文件中。</span><span class="sxs-lookup"><span data-stu-id="25478-158">New global suppressions are appended to this file.</span></span>

![解决方案资源管理器中 GlobalSuppressions.cs 文件的屏幕截图。](media/api-analyzer/suppression-file.jpg)

<span data-ttu-id="25478-160">全局禁止是推荐方法，可确保 API 使用跨项目保持一致。</span><span class="sxs-lookup"><span data-stu-id="25478-160">Global suppression is the recommended way to ensure consistency of API usage across projects.</span></span>

## <a name="discover-cross-platform-issues"></a><span data-ttu-id="25478-161">发现跨平台问题</span><span class="sxs-lookup"><span data-stu-id="25478-161">Discover cross-platform issues</span></span>

> [!NOTE]
> <span data-ttu-id="25478-162">.NET 5.0 引入[平台兼容性分析器](platform-compat-analyzer.md)作为此功能的替代。</span><span class="sxs-lookup"><span data-stu-id="25478-162">.NET 5.0 introduces the [Platform compatibility analyzer](platform-compat-analyzer.md) as a replacement of this feature.</span></span> <span data-ttu-id="25478-163">平台兼容性分析器包含在 .NET SDK 中（无需单独安装），并且默认启用。</span><span class="sxs-lookup"><span data-stu-id="25478-163">The platform compatibility analyzer is included in the .NET SDK (no need to install it separately) and is on by default.</span></span>

<span data-ttu-id="25478-164">与弃用的 API 类似，分析器可发现所有的非跨平台 API。</span><span class="sxs-lookup"><span data-stu-id="25478-164">Similar to deprecated APIs, the analyzer identifies all APIs that are not cross-platform.</span></span> <span data-ttu-id="25478-165">例如，<xref:System.Console.WindowWidth?displayProperty=nameWithType> 适用于 Windows，但不适用于 Linux 和 macOS。</span><span class="sxs-lookup"><span data-stu-id="25478-165">For example, <xref:System.Console.WindowWidth?displayProperty=nameWithType> works on Windows but not on Linux and macOS.</span></span> <span data-ttu-id="25478-166">诊断 ID 显示在“错误列表”  窗口中。</span><span class="sxs-lookup"><span data-stu-id="25478-166">The diagnostic ID is shown in the **Error List** window.</span></span> <span data-ttu-id="25478-167">可以禁止显示警告，具体方法是右键单击并选择“快速操作和重构”  。</span><span class="sxs-lookup"><span data-stu-id="25478-167">You can suppress that warning by right-clicking and selecting **Quick Actions and Refactorings**.</span></span> <span data-ttu-id="25478-168">与禁止显示 API 弃用警告时的两种选择（要么继续使用弃用的成员并禁止显示警告，要么根本就不使用弃用的成员）不同，如果仅对特定平台开发代码，可以对不打算在其上运行代码的其他所有平台禁止显示任何警告。</span><span class="sxs-lookup"><span data-stu-id="25478-168">Unlike deprecation cases where you have two options (either keep using the deprecated member and suppress warnings or not use it at all), here if you're developing your code only for certain platforms, you can suppress all warnings for all other platforms you don't plan to run your code on.</span></span> <span data-ttu-id="25478-169">为此，只需编辑项目文件，并添加列出要忽略的所有平台的 `PlatformCompatIgnore` 属性即可。</span><span class="sxs-lookup"><span data-stu-id="25478-169">To do so, you just need to edit your project file and add the `PlatformCompatIgnore` property that lists all platforms to be ignored.</span></span> <span data-ttu-id="25478-170">接受的值包括 `Linux`、`macOS` 和 `Windows`。</span><span class="sxs-lookup"><span data-stu-id="25478-170">The accepted values are: `Linux`, `macOS`, and `Windows`.</span></span>

```xml
<PropertyGroup>
    <PlatformCompatIgnore>Linux;macOS</PlatformCompatIgnore>
</PropertyGroup>
```

<span data-ttu-id="25478-171">如果代码定目标到多个平台，且要利用其中一些平台不支持的 API，可以使用 `if` 语句作为相应部分代码的临界子句：</span><span class="sxs-lookup"><span data-stu-id="25478-171">If your code targets multiple platforms and you want to take advantage of an API not supported on some of them, you can guard that part of the code with an `if` statement:</span></span>

```csharp
if (RuntimeInformation.IsOSPlatform(OSPlatform.Windows))
{
     var w = Console.WindowWidth;
     // More code
}
```

<span data-ttu-id="25478-172">可以每目标框架/操作系统进行有条件编译，但暂需要[手动](../frameworks.md#how-to-specify-a-target-framework)这样做。</span><span class="sxs-lookup"><span data-stu-id="25478-172">You can also conditionally compile per target framework/operating system, but you currently need to do that [manually](../frameworks.md#how-to-specify-a-target-framework).</span></span>

## <a name="supported-diagnostics"></a><span data-ttu-id="25478-173">支持的诊断</span><span class="sxs-lookup"><span data-stu-id="25478-173">Supported diagnostics</span></span>

<span data-ttu-id="25478-174">目前，分析器处理以下情况：</span><span class="sxs-lookup"><span data-stu-id="25478-174">Currently, the analyzer handles the following cases:</span></span>

- <span data-ttu-id="25478-175">使用抛出 <xref:System.PlatformNotSupportedException> 的 .NET Standard API (PC001)。</span><span class="sxs-lookup"><span data-stu-id="25478-175">Usage of a .NET Standard API that throws <xref:System.PlatformNotSupportedException> (PC001).</span></span>
- <span data-ttu-id="25478-176">使用 .NET Framework 4.6.1 不支持的 .NET Standard API (PC002)。</span><span class="sxs-lookup"><span data-stu-id="25478-176">Usage of a .NET Standard API that isn't available on the .NET Framework 4.6.1 (PC002).</span></span>
- <span data-ttu-id="25478-177">UWP (PC003) 中不存在的本机 API 的用法。</span><span class="sxs-lookup"><span data-stu-id="25478-177">Usage of a native API that doesn't exist in UWP (PC003).</span></span>
- <span data-ttu-id="25478-178">Delegate.BeginInvoke 和 EndInvoke APIs (PC004) 的用法。</span><span class="sxs-lookup"><span data-stu-id="25478-178">Usage of Delegate.BeginInvoke and EndInvoke APIs (PC004).</span></span>
- <span data-ttu-id="25478-179">使用标记为弃用的 API (DEXXXX)。</span><span class="sxs-lookup"><span data-stu-id="25478-179">Usage of an API that is marked as deprecated (DEXXXX).</span></span>

## <a name="ci-machine"></a><span data-ttu-id="25478-180">CI 计算机</span><span class="sxs-lookup"><span data-stu-id="25478-180">CI machine</span></span>

<span data-ttu-id="25478-181">所有这些诊断不仅可以通过 IDE 获取，还能通过命令行在生成项目期间获取（包括 CI 服务器）。</span><span class="sxs-lookup"><span data-stu-id="25478-181">All these diagnostics are available not only in the IDE, but also on the command line as part of building your project, which includes the CI server.</span></span>

## <a name="configuration"></a><span data-ttu-id="25478-182">Configuration</span><span class="sxs-lookup"><span data-stu-id="25478-182">Configuration</span></span>

<span data-ttu-id="25478-183">由用户确定应如何处理这些诊断，是生成警告、错误、建议，还是禁用诊断。</span><span class="sxs-lookup"><span data-stu-id="25478-183">The user decides how the diagnostics should be treated: as warnings, errors, suggestions, or to be turned off.</span></span> <span data-ttu-id="25478-184">例如，作为架构师，可以确定应将兼容性问题处理为错误，对调用某些弃用的 API 生成警告，而对其他情况仅生成建议。</span><span class="sxs-lookup"><span data-stu-id="25478-184">For example, as an architect, you can decide that compatibility issues should be treated as errors, calls to some deprecated APIs generate warnings, while others only generate suggestions.</span></span> <span data-ttu-id="25478-185">可以按诊断 ID 和按项目单独对此进行配置。</span><span class="sxs-lookup"><span data-stu-id="25478-185">You can configure this separately by diagnostic ID and by project.</span></span> <span data-ttu-id="25478-186">为此，请在“解决方案资源管理器”  中转到项目下的“依赖关系”  节点。</span><span class="sxs-lookup"><span data-stu-id="25478-186">To do so in **Solution Explorer**, navigate to the **Dependencies** node under your project.</span></span> <span data-ttu-id="25478-187">依次展开节点“依赖关系”   > “分析器”   > “Microsoft.DotNet.Analyzers.Compatibility”  。</span><span class="sxs-lookup"><span data-stu-id="25478-187">Expand the nodes **Dependencies** > **Analyzers** > **Microsoft.DotNet.Analyzers.Compatibility**.</span></span> <span data-ttu-id="25478-188">右键单击诊断 ID，选择“设置规则集严重性”，然后选中相应选项。</span><span class="sxs-lookup"><span data-stu-id="25478-188">Right-click on the diagnostic ID, select **Set Rule Set Severity**, and then pick the desired option.</span></span>

![“解决方案资源管理器”的屏幕截图，其中显示了诊断和带有规则集严重性的弹出对话框。](media/api-analyzer/disable-notifications.jpg)

## <a name="see-also"></a><span data-ttu-id="25478-190">另请参阅</span><span class="sxs-lookup"><span data-stu-id="25478-190">See also</span></span>

- <span data-ttu-id="25478-191">[API 分析器简介](https://devblogs.microsoft.com/dotnet/introducing-api-analyzer/)博客文章。</span><span class="sxs-lookup"><span data-stu-id="25478-191">[Introducing API Analyzer](https://devblogs.microsoft.com/dotnet/introducing-api-analyzer/) blog post.</span></span>
- <span data-ttu-id="25478-192">YouTube 上的 [API 分析器](https://youtu.be/eeBEahYXGd0)演示视频。</span><span class="sxs-lookup"><span data-stu-id="25478-192">[API Analyzer](https://youtu.be/eeBEahYXGd0) demo video on YouTube.</span></span>
- [<span data-ttu-id="25478-193">平台兼容性分析器</span><span class="sxs-lookup"><span data-stu-id="25478-193">Platform Compatibility Analyzer</span></span>](platform-compat-analyzer.md)
