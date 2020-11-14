---
title: dotnet new 命令
description: dotnet new 命令可根据指定模板新建 .NET Core 项目。
no-loc:
- ':::no-loc(Blazor):::'
- ':::no-loc(WebAssembly):::'
ms.date: 09/04/2020
ms.openlocfilehash: 2ee06c37cd950f3b9771db2f30fe353435641d67
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400586"
---
# <a name="dotnet-new"></a><span data-ttu-id="73879-103">dotnet new</span><span class="sxs-lookup"><span data-stu-id="73879-103">dotnet new</span></span>

<span data-ttu-id="73879-104">本文适用于： ✔️ .NET Core 2.0 SDK 及更高版本</span><span class="sxs-lookup"><span data-stu-id="73879-104">**This article applies to:** ✔️ .NET Core 2.0 SDK and later versions</span></span>

## <a name="name"></a><span data-ttu-id="73879-105">“属性”</span><span class="sxs-lookup"><span data-stu-id="73879-105">Name</span></span>

<span data-ttu-id="73879-106">`dotnet new` - 根据指定的模板，创建新的项目、配置文件或解决方案。</span><span class="sxs-lookup"><span data-stu-id="73879-106">`dotnet new` - Creates a new project, configuration file, or solution based on the specified template.</span></span>

## <a name="synopsis"></a><span data-ttu-id="73879-107">摘要</span><span class="sxs-lookup"><span data-stu-id="73879-107">Synopsis</span></span>

```dotnetcli
dotnet new <TEMPLATE> [--dry-run] [--force] [-i|--install {PATH|NUGET_ID}]
    [-lang|--language {"C#"|"F#"|VB}] [-n|--name <OUTPUT_NAME>]
    [--nuget-source <SOURCE>] [-o|--output <OUTPUT_DIRECTORY>]
    [-u|--uninstall] [--update-apply] [--update-check] [Template options]

dotnet new <TEMPLATE> [-l|--list] [--type <TYPE>]

dotnet new -h|--help
```

## <a name="description"></a><span data-ttu-id="73879-108">描述</span><span class="sxs-lookup"><span data-stu-id="73879-108">Description</span></span>

<span data-ttu-id="73879-109">`dotnet new` 命令基于模板创建 .NET Core 项目或其他项目。</span><span class="sxs-lookup"><span data-stu-id="73879-109">The `dotnet new` command creates a .NET Core project or other artifacts based on a template.</span></span>

<span data-ttu-id="73879-110">命令调用[模板引擎](https://github.com/dotnet/templating)，以根据指定的模板和选项在磁盘上创建项目。</span><span class="sxs-lookup"><span data-stu-id="73879-110">The command calls the [template engine](https://github.com/dotnet/templating) to create the artifacts on disk based on the specified template and options.</span></span>

### <a name="implicit-restore"></a><span data-ttu-id="73879-111">隐式还原</span><span class="sxs-lookup"><span data-stu-id="73879-111">Implicit restore</span></span>

[!INCLUDE[dotnet restore note](~/includes/dotnet-restore-note.md)]

## <a name="arguments"></a><span data-ttu-id="73879-112">自变量</span><span class="sxs-lookup"><span data-stu-id="73879-112">Arguments</span></span>

- **`TEMPLATE`**

  <span data-ttu-id="73879-113">调用命令时要实例化的模板。</span><span class="sxs-lookup"><span data-stu-id="73879-113">The template to instantiate when the command is invoked.</span></span> <span data-ttu-id="73879-114">每个模板可能具有可传递的特定选项。</span><span class="sxs-lookup"><span data-stu-id="73879-114">Each template might have specific options you can pass.</span></span> <span data-ttu-id="73879-115">有关详细信息，请参阅[模板选项](#template-options)。</span><span class="sxs-lookup"><span data-stu-id="73879-115">For more information, see [Template options](#template-options).</span></span>

  <span data-ttu-id="73879-116">可以运行 `dotnet new --list` 或 `dotnet new -l` 以查看所有已安装模板的列表。</span><span class="sxs-lookup"><span data-stu-id="73879-116">You can run `dotnet new --list` or `dotnet new -l` to see a list of all installed templates.</span></span> <span data-ttu-id="73879-117">如果 `TEMPLATE` 值与返回表中的“模板”或“短名称”列中的文本不完全匹配，则会对这两列执行 substring 匹配。</span><span class="sxs-lookup"><span data-stu-id="73879-117">If the `TEMPLATE` value isn't an exact match on text in the **Templates** or **Short Name** column from the returned table, a substring match is performed on those two columns.</span></span>

  <span data-ttu-id="73879-118">从 .NET Core 3.0 SDK 开始，当你在以下情况下调用 `dotnet new` 命令时，CLI 将在 NuGet.org 中搜索模板：</span><span class="sxs-lookup"><span data-stu-id="73879-118">Starting with .NET Core 3.0 SDK, the CLI searches for templates in NuGet.org when you invoke the `dotnet new` command in the following conditions:</span></span>

  - <span data-ttu-id="73879-119">如果在调用 `dotnet new` 时 CLI 找不到模板匹配项，即使是部分匹配也不行。</span><span class="sxs-lookup"><span data-stu-id="73879-119">If the CLI can't find a template match when invoking `dotnet new`, not even partial.</span></span>
  - <span data-ttu-id="73879-120">如果有较新版本的模板可用。</span><span class="sxs-lookup"><span data-stu-id="73879-120">If there's a newer version of the template available.</span></span> <span data-ttu-id="73879-121">在这种情况下，将创建项目或工件，但 CLI 会就模板的更新版本发出警告。</span><span class="sxs-lookup"><span data-stu-id="73879-121">In this case, the project or artifact is created but the CLI warns you about an updated version of the template.</span></span>

  <span data-ttu-id="73879-122">下表显示了随 .NET Core SDK 一起预安装的模板。</span><span class="sxs-lookup"><span data-stu-id="73879-122">The following table shows the templates that come pre-installed with the .NET Core SDK.</span></span> <span data-ttu-id="73879-123">模板的默认语言显示在括号内。</span><span class="sxs-lookup"><span data-stu-id="73879-123">The default language for the template is shown inside the brackets.</span></span> <span data-ttu-id="73879-124">单击短名称链接可查看特定的模板选项。</span><span class="sxs-lookup"><span data-stu-id="73879-124">Click on the short name link to see the specific template options.</span></span>

| <span data-ttu-id="73879-125">模板</span><span class="sxs-lookup"><span data-stu-id="73879-125">Templates</span></span>                                    | <span data-ttu-id="73879-126">短名称</span><span class="sxs-lookup"><span data-stu-id="73879-126">Short name</span></span>                      | <span data-ttu-id="73879-127">语言</span><span class="sxs-lookup"><span data-stu-id="73879-127">Language</span></span>     | <span data-ttu-id="73879-128">Tags</span><span class="sxs-lookup"><span data-stu-id="73879-128">Tags</span></span>                                  | <span data-ttu-id="73879-129">已引入</span><span class="sxs-lookup"><span data-stu-id="73879-129">Introduced</span></span> |
|----------------------------------------------|---------------------------------|--------------|---------------------------------------|------------|
| <span data-ttu-id="73879-130">控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="73879-130">Console Application</span></span>                          | [<span data-ttu-id="73879-131">控制台</span><span class="sxs-lookup"><span data-stu-id="73879-131">console</span></span>](#console)             | <span data-ttu-id="73879-132">[C#]、F#、VB</span><span class="sxs-lookup"><span data-stu-id="73879-132">[C#], F#, VB</span></span> | <span data-ttu-id="73879-133">常用/控制台</span><span class="sxs-lookup"><span data-stu-id="73879-133">Common/Console</span></span>                        | <span data-ttu-id="73879-134">1.0</span><span class="sxs-lookup"><span data-stu-id="73879-134">1.0</span></span>        |
| <span data-ttu-id="73879-135">类库</span><span class="sxs-lookup"><span data-stu-id="73879-135">Class library</span></span>                                | [<span data-ttu-id="73879-136">classlib</span><span class="sxs-lookup"><span data-stu-id="73879-136">classlib</span></span>](#classlib)           | <span data-ttu-id="73879-137">[C#]、F#、VB</span><span class="sxs-lookup"><span data-stu-id="73879-137">[C#], F#, VB</span></span> | <span data-ttu-id="73879-138">常用/库</span><span class="sxs-lookup"><span data-stu-id="73879-138">Common/Library</span></span>                        | <span data-ttu-id="73879-139">1.0</span><span class="sxs-lookup"><span data-stu-id="73879-139">1.0</span></span>        |
| <span data-ttu-id="73879-140">WPF 应用程序</span><span class="sxs-lookup"><span data-stu-id="73879-140">WPF Application</span></span>                              | [<span data-ttu-id="73879-141">wpf</span><span class="sxs-lookup"><span data-stu-id="73879-141">wpf</span></span>](#wpf)                     | <span data-ttu-id="73879-142">[C#]、VB</span><span class="sxs-lookup"><span data-stu-id="73879-142">[C#], VB</span></span>     | <span data-ttu-id="73879-143">常用/WPF</span><span class="sxs-lookup"><span data-stu-id="73879-143">Common/WPF</span></span>                            | <span data-ttu-id="73879-144">3.0（对于 VB，则为 5.0）</span><span class="sxs-lookup"><span data-stu-id="73879-144">3.0 (5.0 for VB)</span></span>|
| <span data-ttu-id="73879-145">WPF 类库</span><span class="sxs-lookup"><span data-stu-id="73879-145">WPF Class library</span></span>                            | [<span data-ttu-id="73879-146">wpflib</span><span class="sxs-lookup"><span data-stu-id="73879-146">wpflib</span></span>](#wpf)                  | <span data-ttu-id="73879-147">[C#]、VB</span><span class="sxs-lookup"><span data-stu-id="73879-147">[C#], VB</span></span>     | <span data-ttu-id="73879-148">常用/WPF</span><span class="sxs-lookup"><span data-stu-id="73879-148">Common/WPF</span></span>                            | <span data-ttu-id="73879-149">3.0（对于 VB，则为 5.0）</span><span class="sxs-lookup"><span data-stu-id="73879-149">3.0 (5.0 for VB)</span></span>|
| <span data-ttu-id="73879-150">WPF 自定义控件库</span><span class="sxs-lookup"><span data-stu-id="73879-150">WPF Custom Control Library</span></span>                   | [<span data-ttu-id="73879-151">wpfcustomcontrollib</span><span class="sxs-lookup"><span data-stu-id="73879-151">wpfcustomcontrollib</span></span>](#wpf)     | <span data-ttu-id="73879-152">[C#]、VB</span><span class="sxs-lookup"><span data-stu-id="73879-152">[C#], VB</span></span>     | <span data-ttu-id="73879-153">常用/WPF</span><span class="sxs-lookup"><span data-stu-id="73879-153">Common/WPF</span></span>                            | <span data-ttu-id="73879-154">3.0（对于 VB，则为 5.0）</span><span class="sxs-lookup"><span data-stu-id="73879-154">3.0 (5.0 for VB)</span></span>|
| <span data-ttu-id="73879-155">WPF 用户控件库</span><span class="sxs-lookup"><span data-stu-id="73879-155">WPF User Control Library</span></span>                     | [<span data-ttu-id="73879-156">wpfusercontrollib</span><span class="sxs-lookup"><span data-stu-id="73879-156">wpfusercontrollib</span></span>](#wpf)       | <span data-ttu-id="73879-157">[C#]、VB</span><span class="sxs-lookup"><span data-stu-id="73879-157">[C#], VB</span></span>     | <span data-ttu-id="73879-158">常用/WPF</span><span class="sxs-lookup"><span data-stu-id="73879-158">Common/WPF</span></span>                            | <span data-ttu-id="73879-159">3.0（对于 VB，则为 5.0）</span><span class="sxs-lookup"><span data-stu-id="73879-159">3.0 (5.0 for VB)</span></span>|
| <span data-ttu-id="73879-160">Windows 窗体 (WinForms) 应用程序</span><span class="sxs-lookup"><span data-stu-id="73879-160">Windows Forms (WinForms) Application</span></span>         | [<span data-ttu-id="73879-161">winforms</span><span class="sxs-lookup"><span data-stu-id="73879-161">winforms</span></span>](#winforms)           | <span data-ttu-id="73879-162">[C#]、VB</span><span class="sxs-lookup"><span data-stu-id="73879-162">[C#], VB</span></span>     | <span data-ttu-id="73879-163">常用/WinForms</span><span class="sxs-lookup"><span data-stu-id="73879-163">Common/WinForms</span></span>                       | <span data-ttu-id="73879-164">3.0（对于 VB，则为 5.0）</span><span class="sxs-lookup"><span data-stu-id="73879-164">3.0 (5.0 for VB)</span></span>|
| <span data-ttu-id="73879-165">Windows 窗体 (WinForms) 类库</span><span class="sxs-lookup"><span data-stu-id="73879-165">Windows Forms (WinForms) Class library</span></span>       | [<span data-ttu-id="73879-166">winformslib</span><span class="sxs-lookup"><span data-stu-id="73879-166">winformslib</span></span>](#winforms)        | <span data-ttu-id="73879-167">[C#]、VB</span><span class="sxs-lookup"><span data-stu-id="73879-167">[C#], VB</span></span>     | <span data-ttu-id="73879-168">常用/WinForms</span><span class="sxs-lookup"><span data-stu-id="73879-168">Common/WinForms</span></span>                       | <span data-ttu-id="73879-169">3.0（对于 VB，则为 5.0）</span><span class="sxs-lookup"><span data-stu-id="73879-169">3.0 (5.0 for VB)</span></span>|
| <span data-ttu-id="73879-170">Worker Service</span><span class="sxs-lookup"><span data-stu-id="73879-170">Worker Service</span></span>                               | [<span data-ttu-id="73879-171">worker</span><span class="sxs-lookup"><span data-stu-id="73879-171">worker</span></span>](#web-others)           | <span data-ttu-id="73879-172">[C#]</span><span class="sxs-lookup"><span data-stu-id="73879-172">[C#]</span></span>         | <span data-ttu-id="73879-173">常用/Worker/Web</span><span class="sxs-lookup"><span data-stu-id="73879-173">Common/Worker/Web</span></span>                     | <span data-ttu-id="73879-174">3.0</span><span class="sxs-lookup"><span data-stu-id="73879-174">3.0</span></span>        |
| <span data-ttu-id="73879-175">单元测试项目</span><span class="sxs-lookup"><span data-stu-id="73879-175">Unit Test Project</span></span>                            | [<span data-ttu-id="73879-176">mstest</span><span class="sxs-lookup"><span data-stu-id="73879-176">mstest</span></span>](#test)                 | <span data-ttu-id="73879-177">[C#]、F#、VB</span><span class="sxs-lookup"><span data-stu-id="73879-177">[C#], F#, VB</span></span> | <span data-ttu-id="73879-178">测试/MSTest</span><span class="sxs-lookup"><span data-stu-id="73879-178">Test/MSTest</span></span>                           | <span data-ttu-id="73879-179">1.0</span><span class="sxs-lookup"><span data-stu-id="73879-179">1.0</span></span>        |
| <span data-ttu-id="73879-180">NUnit 3 测试项目</span><span class="sxs-lookup"><span data-stu-id="73879-180">NUnit 3 Test Project</span></span>                         | [<span data-ttu-id="73879-181">nunit</span><span class="sxs-lookup"><span data-stu-id="73879-181">nunit</span></span>](#nunit)                 | <span data-ttu-id="73879-182">[C#]、F#、VB</span><span class="sxs-lookup"><span data-stu-id="73879-182">[C#], F#, VB</span></span> | <span data-ttu-id="73879-183">测试/NUnit</span><span class="sxs-lookup"><span data-stu-id="73879-183">Test/NUnit</span></span>                            | <span data-ttu-id="73879-184">2.1.400</span><span class="sxs-lookup"><span data-stu-id="73879-184">2.1.400</span></span>    |
| <span data-ttu-id="73879-185">NUnit 3 测试项</span><span class="sxs-lookup"><span data-stu-id="73879-185">NUnit 3 Test Item</span></span>                            | `nunit-test`                    | <span data-ttu-id="73879-186">[C#]、F#、VB</span><span class="sxs-lookup"><span data-stu-id="73879-186">[C#], F#, VB</span></span> | <span data-ttu-id="73879-187">测试/NUnit</span><span class="sxs-lookup"><span data-stu-id="73879-187">Test/NUnit</span></span>                            | <span data-ttu-id="73879-188">2.2</span><span class="sxs-lookup"><span data-stu-id="73879-188">2.2</span></span>        |
| <span data-ttu-id="73879-189">xUnit 测试项目</span><span class="sxs-lookup"><span data-stu-id="73879-189">xUnit Test Project</span></span>                           | [<span data-ttu-id="73879-190">xunit</span><span class="sxs-lookup"><span data-stu-id="73879-190">xunit</span></span>](#test)                  | <span data-ttu-id="73879-191">[C#]、F#、VB</span><span class="sxs-lookup"><span data-stu-id="73879-191">[C#], F#, VB</span></span> | <span data-ttu-id="73879-192">测试/xUnit</span><span class="sxs-lookup"><span data-stu-id="73879-192">Test/xUnit</span></span>                            | <span data-ttu-id="73879-193">1.0</span><span class="sxs-lookup"><span data-stu-id="73879-193">1.0</span></span>        |
| <span data-ttu-id="73879-194">Razor 组件</span><span class="sxs-lookup"><span data-stu-id="73879-194">Razor Component</span></span>                              | `razorcomponent`                | <span data-ttu-id="73879-195">[C#]</span><span class="sxs-lookup"><span data-stu-id="73879-195">[C#]</span></span>         | <span data-ttu-id="73879-196">Web/ASP.NET</span><span class="sxs-lookup"><span data-stu-id="73879-196">Web/ASP.NET</span></span>                           | <span data-ttu-id="73879-197">3.0</span><span class="sxs-lookup"><span data-stu-id="73879-197">3.0</span></span>        |
| <span data-ttu-id="73879-198">Razor 页</span><span class="sxs-lookup"><span data-stu-id="73879-198">Razor Page</span></span>                                   | [<span data-ttu-id="73879-199">page</span><span class="sxs-lookup"><span data-stu-id="73879-199">page</span></span>](#page)                   | <span data-ttu-id="73879-200">[C#]</span><span class="sxs-lookup"><span data-stu-id="73879-200">[C#]</span></span>         | <span data-ttu-id="73879-201">Web/ASP.NET</span><span class="sxs-lookup"><span data-stu-id="73879-201">Web/ASP.NET</span></span>                           | <span data-ttu-id="73879-202">2.0</span><span class="sxs-lookup"><span data-stu-id="73879-202">2.0</span></span>        |
| <span data-ttu-id="73879-203">MVC ViewImports</span><span class="sxs-lookup"><span data-stu-id="73879-203">MVC ViewImports</span></span>                              | [<span data-ttu-id="73879-204">viewimports</span><span class="sxs-lookup"><span data-stu-id="73879-204">viewimports</span></span>](#namespace)       | <span data-ttu-id="73879-205">[C#]</span><span class="sxs-lookup"><span data-stu-id="73879-205">[C#]</span></span>         | <span data-ttu-id="73879-206">Web/ASP.NET</span><span class="sxs-lookup"><span data-stu-id="73879-206">Web/ASP.NET</span></span>                           | <span data-ttu-id="73879-207">2.0</span><span class="sxs-lookup"><span data-stu-id="73879-207">2.0</span></span>        |
| <span data-ttu-id="73879-208">MVC ViewStart</span><span class="sxs-lookup"><span data-stu-id="73879-208">MVC ViewStart</span></span>                                | `viewstart`                     | <span data-ttu-id="73879-209">[C#]</span><span class="sxs-lookup"><span data-stu-id="73879-209">[C#]</span></span>         | <span data-ttu-id="73879-210">Web/ASP.NET</span><span class="sxs-lookup"><span data-stu-id="73879-210">Web/ASP.NET</span></span>                           | <span data-ttu-id="73879-211">2.0</span><span class="sxs-lookup"><span data-stu-id="73879-211">2.0</span></span>        |
| <span data-ttu-id="73879-212">:::no-loc(Blazor)::: 服务器应用</span><span class="sxs-lookup"><span data-stu-id="73879-212">:::no-loc(Blazor)::: Server App</span></span>                            | [<span data-ttu-id="73879-213">blazorserver</span><span class="sxs-lookup"><span data-stu-id="73879-213">blazorserver</span></span>](#blazorserver)   | <span data-ttu-id="73879-214">[C#]</span><span class="sxs-lookup"><span data-stu-id="73879-214">[C#]</span></span>         | <span data-ttu-id="73879-215">Web/:::no-loc(Blazor):::</span><span class="sxs-lookup"><span data-stu-id="73879-215">Web/:::no-loc(Blazor):::</span></span>                            | <span data-ttu-id="73879-216">3.0</span><span class="sxs-lookup"><span data-stu-id="73879-216">3.0</span></span>        |
| <span data-ttu-id="73879-217">:::no-loc(Blazor)::: :::no-loc(WebAssembly)::: 应用</span><span class="sxs-lookup"><span data-stu-id="73879-217">:::no-loc(Blazor)::: :::no-loc(WebAssembly)::: App</span></span>                       | [<span data-ttu-id="73879-218">blazorwasm</span><span class="sxs-lookup"><span data-stu-id="73879-218">blazorwasm</span></span>](#blazorwasm)       | <span data-ttu-id="73879-219">[C#]</span><span class="sxs-lookup"><span data-stu-id="73879-219">[C#]</span></span>         | <span data-ttu-id="73879-220">Web/:::no-loc(Blazor):::/:::no-loc(WebAssembly):::</span><span class="sxs-lookup"><span data-stu-id="73879-220">Web/:::no-loc(Blazor):::/:::no-loc(WebAssembly):::</span></span>                | <span data-ttu-id="73879-221">3.1.300</span><span class="sxs-lookup"><span data-stu-id="73879-221">3.1.300</span></span>    |
| <span data-ttu-id="73879-222">ASP.NET Core 空</span><span class="sxs-lookup"><span data-stu-id="73879-222">ASP.NET Core Empty</span></span>                           | [<span data-ttu-id="73879-223">web</span><span class="sxs-lookup"><span data-stu-id="73879-223">web</span></span>](#web)                     | <span data-ttu-id="73879-224">[C#]，F#</span><span class="sxs-lookup"><span data-stu-id="73879-224">[C#], F#</span></span>     | <span data-ttu-id="73879-225">Web/空</span><span class="sxs-lookup"><span data-stu-id="73879-225">Web/Empty</span></span>                             | <span data-ttu-id="73879-226">1.0</span><span class="sxs-lookup"><span data-stu-id="73879-226">1.0</span></span>        |
| <span data-ttu-id="73879-227">ASP.NET Core Web 应用程序 (Model-View-Controller)</span><span class="sxs-lookup"><span data-stu-id="73879-227">ASP.NET Core Web App (Model-View-Controller)</span></span> | [<span data-ttu-id="73879-228">mvc</span><span class="sxs-lookup"><span data-stu-id="73879-228">mvc</span></span>](#web-options)             | <span data-ttu-id="73879-229">[C#]，F#</span><span class="sxs-lookup"><span data-stu-id="73879-229">[C#], F#</span></span>     | <span data-ttu-id="73879-230">Web/MVC</span><span class="sxs-lookup"><span data-stu-id="73879-230">Web/MVC</span></span>                               | <span data-ttu-id="73879-231">1.0</span><span class="sxs-lookup"><span data-stu-id="73879-231">1.0</span></span>        |
| <span data-ttu-id="73879-232">ASP.NET Core Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="73879-232">ASP.NET Core Web App</span></span>                         | [<span data-ttu-id="73879-233">webapp、razor</span><span class="sxs-lookup"><span data-stu-id="73879-233">webapp, razor</span></span>](#web-options)   | <span data-ttu-id="73879-234">[C#]</span><span class="sxs-lookup"><span data-stu-id="73879-234">[C#]</span></span>         | <span data-ttu-id="73879-235">Web/MVC/Razor Pages</span><span class="sxs-lookup"><span data-stu-id="73879-235">Web/MVC/Razor Pages</span></span>                   | <span data-ttu-id="73879-236">2.2、2.0</span><span class="sxs-lookup"><span data-stu-id="73879-236">2.2, 2.0</span></span>   |
| <span data-ttu-id="73879-237">含 Angular 的 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="73879-237">ASP.NET Core with Angular</span></span>                    | [<span data-ttu-id="73879-238">angular</span><span class="sxs-lookup"><span data-stu-id="73879-238">angular</span></span>](#spa)                 | <span data-ttu-id="73879-239">[C#]</span><span class="sxs-lookup"><span data-stu-id="73879-239">[C#]</span></span>         | <span data-ttu-id="73879-240">Web/MVC/SPA</span><span class="sxs-lookup"><span data-stu-id="73879-240">Web/MVC/SPA</span></span>                           | <span data-ttu-id="73879-241">2.0</span><span class="sxs-lookup"><span data-stu-id="73879-241">2.0</span></span>        |
| <span data-ttu-id="73879-242">含 React.js 的 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="73879-242">ASP.NET Core with React.js</span></span>                   | [<span data-ttu-id="73879-243">react</span><span class="sxs-lookup"><span data-stu-id="73879-243">react</span></span>](#spa)                   | <span data-ttu-id="73879-244">[C#]</span><span class="sxs-lookup"><span data-stu-id="73879-244">[C#]</span></span>         | <span data-ttu-id="73879-245">Web/MVC/SPA</span><span class="sxs-lookup"><span data-stu-id="73879-245">Web/MVC/SPA</span></span>                           | <span data-ttu-id="73879-246">2.0</span><span class="sxs-lookup"><span data-stu-id="73879-246">2.0</span></span>        |
| <span data-ttu-id="73879-247">含 React.js 和 Redux 的 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="73879-247">ASP.NET Core with React.js and Redux</span></span>         | [<span data-ttu-id="73879-248">reactredux</span><span class="sxs-lookup"><span data-stu-id="73879-248">reactredux</span></span>](#reactredux)       | <span data-ttu-id="73879-249">[C#]</span><span class="sxs-lookup"><span data-stu-id="73879-249">[C#]</span></span>         | <span data-ttu-id="73879-250">Web/MVC/SPA</span><span class="sxs-lookup"><span data-stu-id="73879-250">Web/MVC/SPA</span></span>                           | <span data-ttu-id="73879-251">2.0</span><span class="sxs-lookup"><span data-stu-id="73879-251">2.0</span></span>        |
| <span data-ttu-id="73879-252">Razor 类库</span><span class="sxs-lookup"><span data-stu-id="73879-252">Razor Class Library</span></span>                          | [<span data-ttu-id="73879-253">razorclasslib</span><span class="sxs-lookup"><span data-stu-id="73879-253">razorclasslib</span></span>](#razorclasslib) | <span data-ttu-id="73879-254">[C#]</span><span class="sxs-lookup"><span data-stu-id="73879-254">[C#]</span></span>         | <span data-ttu-id="73879-255">Web/Razor/库/Razor 类库</span><span class="sxs-lookup"><span data-stu-id="73879-255">Web/Razor/Library/Razor Class Library</span></span> | <span data-ttu-id="73879-256">2.1</span><span class="sxs-lookup"><span data-stu-id="73879-256">2.1</span></span>        |
| <span data-ttu-id="73879-257">ASP.NET Core Web API</span><span class="sxs-lookup"><span data-stu-id="73879-257">ASP.NET Core Web API</span></span>                         | [<span data-ttu-id="73879-258">webapi</span><span class="sxs-lookup"><span data-stu-id="73879-258">webapi</span></span>](#webapi)               | <span data-ttu-id="73879-259">[C#]，F#</span><span class="sxs-lookup"><span data-stu-id="73879-259">[C#], F#</span></span>     | <span data-ttu-id="73879-260">Web/WebAPI</span><span class="sxs-lookup"><span data-stu-id="73879-260">Web/WebAPI</span></span>                            | <span data-ttu-id="73879-261">1.0</span><span class="sxs-lookup"><span data-stu-id="73879-261">1.0</span></span>        |
| <span data-ttu-id="73879-262">ASP.NET Core gRPC 服务</span><span class="sxs-lookup"><span data-stu-id="73879-262">ASP.NET Core gRPC Service</span></span>                    | [<span data-ttu-id="73879-263">grpc</span><span class="sxs-lookup"><span data-stu-id="73879-263">grpc</span></span>](#web-others)             | <span data-ttu-id="73879-264">[C#]</span><span class="sxs-lookup"><span data-stu-id="73879-264">[C#]</span></span>         | <span data-ttu-id="73879-265">Web/gRPC</span><span class="sxs-lookup"><span data-stu-id="73879-265">Web/gRPC</span></span>                              | <span data-ttu-id="73879-266">3.0</span><span class="sxs-lookup"><span data-stu-id="73879-266">3.0</span></span>        |
| <span data-ttu-id="73879-267">dotnet gitignore 文件</span><span class="sxs-lookup"><span data-stu-id="73879-267">dotnet gitignore file</span></span>                        | `gitignore`                     |              | <span data-ttu-id="73879-268">配置</span><span class="sxs-lookup"><span data-stu-id="73879-268">Config</span></span>                                | <span data-ttu-id="73879-269">3.0</span><span class="sxs-lookup"><span data-stu-id="73879-269">3.0</span></span>        |
| <span data-ttu-id="73879-270">global.json 文件</span><span class="sxs-lookup"><span data-stu-id="73879-270">global.json file</span></span>                             | [<span data-ttu-id="73879-271">globaljson</span><span class="sxs-lookup"><span data-stu-id="73879-271">globaljson</span></span>](#globaljson)       |              | <span data-ttu-id="73879-272">配置</span><span class="sxs-lookup"><span data-stu-id="73879-272">Config</span></span>                                | <span data-ttu-id="73879-273">2.0</span><span class="sxs-lookup"><span data-stu-id="73879-273">2.0</span></span>        |
| <span data-ttu-id="73879-274">NuGet 配置</span><span class="sxs-lookup"><span data-stu-id="73879-274">NuGet Config</span></span>                                 | `nugetconfig`                   |              | <span data-ttu-id="73879-275">配置</span><span class="sxs-lookup"><span data-stu-id="73879-275">Config</span></span>                                | <span data-ttu-id="73879-276">1.0</span><span class="sxs-lookup"><span data-stu-id="73879-276">1.0</span></span>        |
| <span data-ttu-id="73879-277">Dotnet 本地工具清单文件</span><span class="sxs-lookup"><span data-stu-id="73879-277">Dotnet local tool manifest file</span></span>              | `tool-manifest`                 |              | <span data-ttu-id="73879-278">配置</span><span class="sxs-lookup"><span data-stu-id="73879-278">Config</span></span>                                | <span data-ttu-id="73879-279">3.0</span><span class="sxs-lookup"><span data-stu-id="73879-279">3.0</span></span>        |
| <span data-ttu-id="73879-280">Web 配置</span><span class="sxs-lookup"><span data-stu-id="73879-280">Web Config</span></span>                                   | `webconfig`                     |              | <span data-ttu-id="73879-281">配置</span><span class="sxs-lookup"><span data-stu-id="73879-281">Config</span></span>                                | <span data-ttu-id="73879-282">1.0</span><span class="sxs-lookup"><span data-stu-id="73879-282">1.0</span></span>        |
| <span data-ttu-id="73879-283">解决方案文件</span><span class="sxs-lookup"><span data-stu-id="73879-283">Solution File</span></span>                                | `sln`                           |              | <span data-ttu-id="73879-284">解决方案</span><span class="sxs-lookup"><span data-stu-id="73879-284">Solution</span></span>                              | <span data-ttu-id="73879-285">1.0</span><span class="sxs-lookup"><span data-stu-id="73879-285">1.0</span></span>        |
| <span data-ttu-id="73879-286">协议缓冲区文件</span><span class="sxs-lookup"><span data-stu-id="73879-286">Protocol Buffer File</span></span>                         | [<span data-ttu-id="73879-287">proto</span><span class="sxs-lookup"><span data-stu-id="73879-287">proto</span></span>](#namespace)             |              | <span data-ttu-id="73879-288">Web/gRPC</span><span class="sxs-lookup"><span data-stu-id="73879-288">Web/gRPC</span></span>                              | <span data-ttu-id="73879-289">3.0</span><span class="sxs-lookup"><span data-stu-id="73879-289">3.0</span></span>        |

## <a name="options"></a><span data-ttu-id="73879-290">选项</span><span class="sxs-lookup"><span data-stu-id="73879-290">Options</span></span>

- **`--dry-run`**

  <span data-ttu-id="73879-291">显示有关以下内容的摘要：给定命令运行导致模板创建时发生的情况。</span><span class="sxs-lookup"><span data-stu-id="73879-291">Displays a summary of what would happen if the given command were run if it would result in a template creation.</span></span> <span data-ttu-id="73879-292">自 .NET Core 2.2 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="73879-292">Available since .NET Core 2.2 SDK.</span></span>

- **`--force`**

  <span data-ttu-id="73879-293">强制生成内容，即使会更改现有文件，也不例外。</span><span class="sxs-lookup"><span data-stu-id="73879-293">Forces content to be generated even if it would change existing files.</span></span> <span data-ttu-id="73879-294">当选择的模板将覆盖输出目录中的现有文件时，需要执行此操作。</span><span class="sxs-lookup"><span data-stu-id="73879-294">This is required when the template chosen would override existing files in the output directory.</span></span>

- **`-h|--help`**

  <span data-ttu-id="73879-295">打印命令帮助。</span><span class="sxs-lookup"><span data-stu-id="73879-295">Prints out help for the command.</span></span> <span data-ttu-id="73879-296">可针对 `dotnet new` 命令本身或任何模板调用它。</span><span class="sxs-lookup"><span data-stu-id="73879-296">It can be invoked for the `dotnet new` command itself or for any template.</span></span> <span data-ttu-id="73879-297">例如 `dotnet new mvc --help`。</span><span class="sxs-lookup"><span data-stu-id="73879-297">For example, `dotnet new mvc --help`.</span></span>

- **`-i|--install <PATH|NUGET_ID>`**

  <span data-ttu-id="73879-298">从提供的 `PATH` 或 `NUGET_ID` 安装模板包。</span><span class="sxs-lookup"><span data-stu-id="73879-298">Installs a template pack from the `PATH` or `NUGET_ID` provided.</span></span> <span data-ttu-id="73879-299">若要安装模板包的预发布版本，需要以 `<package-name>::<package-version>` 格式指定该版本。</span><span class="sxs-lookup"><span data-stu-id="73879-299">If you want to install a prerelease version of a template package, you need to specify the version in the format of `<package-name>::<package-version>`.</span></span> <span data-ttu-id="73879-300">默认情况下，`dotnet new` 为该版本传递 \*，它表示最新的稳定包版本。</span><span class="sxs-lookup"><span data-stu-id="73879-300">By default, `dotnet new` passes \* for the version, which represents the latest stable package version.</span></span> <span data-ttu-id="73879-301">请在[示例](#examples)部分查看示例。</span><span class="sxs-lookup"><span data-stu-id="73879-301">See an example in the [Examples](#examples) section.</span></span>
  
  <span data-ttu-id="73879-302">如果在运行此命令时已经安装了模板的某个版本，则该模板将更新到指定版本，如果没有指定版本，则将更新到最新的稳定版本。</span><span class="sxs-lookup"><span data-stu-id="73879-302">If a version of the template was already installed when you run this command, the template will be updated to the specified version, or to the latest stable version if no version was specified.</span></span>

  <span data-ttu-id="73879-303">若要了解如何创建自定义模板，请参阅 [dotnet new 自定义模板](custom-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="73879-303">For information on creating custom templates, see [Custom templates for dotnet new](custom-templates.md).</span></span>

- **`-l|--list`**

  <span data-ttu-id="73879-304">列出包含指定名称的模板。</span><span class="sxs-lookup"><span data-stu-id="73879-304">Lists templates containing the specified name.</span></span> <span data-ttu-id="73879-305">如果未指定名称，则列出所有模板。</span><span class="sxs-lookup"><span data-stu-id="73879-305">If no name is specified, lists all templates.</span></span>

- **`-lang|--language {C#|F#|VB}`**

  <span data-ttu-id="73879-306">要创建的模板的语言。</span><span class="sxs-lookup"><span data-stu-id="73879-306">The language of the template to create.</span></span> <span data-ttu-id="73879-307">接受的语言因模板而异（请参阅[参数](#arguments)部分中的默认值）。</span><span class="sxs-lookup"><span data-stu-id="73879-307">The language accepted varies by the template (see defaults in the [arguments](#arguments) section).</span></span> <span data-ttu-id="73879-308">对于某些模板无效。</span><span class="sxs-lookup"><span data-stu-id="73879-308">Not valid for some templates.</span></span>

  > [!NOTE]
  > <span data-ttu-id="73879-309">某些 shell 将 `#` 解释为特殊字符。</span><span class="sxs-lookup"><span data-stu-id="73879-309">Some shells interpret `#` as a special character.</span></span> <span data-ttu-id="73879-310">在这些情况下，请将语言参数值括在引号中。</span><span class="sxs-lookup"><span data-stu-id="73879-310">In those cases, enclose the language parameter value in quotes.</span></span> <span data-ttu-id="73879-311">例如 `dotnet new console -lang "F#"`。</span><span class="sxs-lookup"><span data-stu-id="73879-311">For example, `dotnet new console -lang "F#"`.</span></span>

- **`-n|--name <OUTPUT_NAME>`**

  <span data-ttu-id="73879-312">所创建的输出的名称。</span><span class="sxs-lookup"><span data-stu-id="73879-312">The name for the created output.</span></span> <span data-ttu-id="73879-313">如果未指定名称，使用的是当前目录的名称。</span><span class="sxs-lookup"><span data-stu-id="73879-313">If no name is specified, the name of the current directory is used.</span></span>

- **`--nuget-source <SOURCE>`**

  <span data-ttu-id="73879-314">指定在安装期间要使用的 NuGet 源。</span><span class="sxs-lookup"><span data-stu-id="73879-314">Specifies a NuGet source to use during install.</span></span> <span data-ttu-id="73879-315">自 .NET Core 2.1 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="73879-315">Available since .NET Core 2.1 SDK.</span></span>

- **`-o|--output <OUTPUT_DIRECTORY>`**

  <span data-ttu-id="73879-316">用于放置生成的输出的位置。</span><span class="sxs-lookup"><span data-stu-id="73879-316">Location to place the generated output.</span></span> <span data-ttu-id="73879-317">默认为当前目录。</span><span class="sxs-lookup"><span data-stu-id="73879-317">The default is the current directory.</span></span>

- **`--type <TYPE>`**

  <span data-ttu-id="73879-318">根据可用类型筛选模板。</span><span class="sxs-lookup"><span data-stu-id="73879-318">Filters templates based on available types.</span></span> <span data-ttu-id="73879-319">预定义的值为 `project` 和 `item`。</span><span class="sxs-lookup"><span data-stu-id="73879-319">Predefined values are `project` and `item`.</span></span>

- **`-u|--uninstall [PATH|NUGET_ID]`**

  <span data-ttu-id="73879-320">在提供的 `PATH` 或 `NUGET_ID` 中卸载模板包。</span><span class="sxs-lookup"><span data-stu-id="73879-320">Uninstalls a template pack at the `PATH` or `NUGET_ID` provided.</span></span> <span data-ttu-id="73879-321">如果未指定 `<PATH|NUGET_ID>` 值，将显示所有当前安装的模板包及其关联的模板。</span><span class="sxs-lookup"><span data-stu-id="73879-321">When the `<PATH|NUGET_ID>` value isn't specified, all currently installed template packs and their associated templates are displayed.</span></span> <span data-ttu-id="73879-322">指定 `NUGET_ID` 时，请勿包含版本号。</span><span class="sxs-lookup"><span data-stu-id="73879-322">When specifying `NUGET_ID`, don't include the version number.</span></span>

  <span data-ttu-id="73879-323">如果未指定此选项的参数，该命令将列出已安装的模板及其详细信息。</span><span class="sxs-lookup"><span data-stu-id="73879-323">If you don't specify a parameter to this option, the command lists the installed templates and details about them.</span></span>

  > [!NOTE]
  > <span data-ttu-id="73879-324">若要使用 `PATH` 卸载模板，需要完全限定路径。</span><span class="sxs-lookup"><span data-stu-id="73879-324">To uninstall a template using a `PATH`, you need to fully qualify the path.</span></span> <span data-ttu-id="73879-325">例如，C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp 有效，但是包含文件夹中的 ./GarciaSoftware.ConsoleTemplate.CSharp 无效 。</span><span class="sxs-lookup"><span data-stu-id="73879-325">For example, *C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp* will work, but *./GarciaSoftware.ConsoleTemplate.CSharp* from the containing folder will not.</span></span>
  > <span data-ttu-id="73879-326">模板路径中不要包含最后的终止目录斜杠。</span><span class="sxs-lookup"><span data-stu-id="73879-326">Don't include a final terminating directory slash on your template path.</span></span>

- **`--update-apply`**

  <span data-ttu-id="73879-327">检查是否有可用于当前安装的模板包的更新并安装这些更新。</span><span class="sxs-lookup"><span data-stu-id="73879-327">Checks if there are updates available for the template packs that are currently installed and installs them.</span></span> <span data-ttu-id="73879-328">自 .NET Core 3.0 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="73879-328">Available since .NET Core 3.0 SDK.</span></span>

- **`--update-check`**

  <span data-ttu-id="73879-329">检查是否有可用于当前安装的模板包的更新。</span><span class="sxs-lookup"><span data-stu-id="73879-329">Checks if there are updates available for the template packs that are currently installed.</span></span> <span data-ttu-id="73879-330">自 .NET Core 3.0 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="73879-330">Available since .NET Core 3.0 SDK.</span></span>

## <a name="template-options"></a><span data-ttu-id="73879-331">模板选项</span><span class="sxs-lookup"><span data-stu-id="73879-331">Template options</span></span>

<span data-ttu-id="73879-332">每个项目模板都可能有附加选项。</span><span class="sxs-lookup"><span data-stu-id="73879-332">Each project template may have additional options available.</span></span> <span data-ttu-id="73879-333">核心模板有以下附加选项：</span><span class="sxs-lookup"><span data-stu-id="73879-333">The core templates have the following additional options:</span></span>

### <a name="console"></a><span data-ttu-id="73879-334">控制台</span><span class="sxs-lookup"><span data-stu-id="73879-334">console</span></span>

- **`-f|--framework <FRAMEWORK>`**

  <span data-ttu-id="73879-335">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="73879-335">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="73879-336">自 .NET Core 3.0 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="73879-336">Available since .NET Core 3.0 SDK.</span></span>

  <span data-ttu-id="73879-337">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="73879-337">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="73879-338">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="73879-338">SDK version</span></span> | <span data-ttu-id="73879-339">默认值</span><span class="sxs-lookup"><span data-stu-id="73879-339">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="73879-340">3.1</span><span class="sxs-lookup"><span data-stu-id="73879-340">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="73879-341">3.0</span><span class="sxs-lookup"><span data-stu-id="73879-341">3.0</span></span>         | `netcoreapp3.0` |

- **`--langVersion <VERSION_NUMBER>`**

  <span data-ttu-id="73879-342">在已创建的项目文件中设置 `LangVersion` 属性。</span><span class="sxs-lookup"><span data-stu-id="73879-342">Sets the `LangVersion` property in the created project file.</span></span> <span data-ttu-id="73879-343">例如，使用 `--langVersion 7.3` 以使用 C# 7.3。</span><span class="sxs-lookup"><span data-stu-id="73879-343">For example, use `--langVersion 7.3` to use C# 7.3.</span></span> <span data-ttu-id="73879-344">不支持 F#。</span><span class="sxs-lookup"><span data-stu-id="73879-344">Not supported for F#.</span></span> <span data-ttu-id="73879-345">自 .NET Core 2.2 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="73879-345">Available since .NET Core 2.2 SDK.</span></span>

  <span data-ttu-id="73879-346">有关默认的 C# 版本列表，请参阅[默认](../../csharp/language-reference/configure-language-version.md#defaults)。</span><span class="sxs-lookup"><span data-stu-id="73879-346">For a list of default C# versions, see [Defaults](../../csharp/language-reference/configure-language-version.md#defaults).</span></span>

- **`--no-restore`**

  <span data-ttu-id="73879-347">如已指定，则在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="73879-347">If specified, doesn't execute an implicit restore during project creation.</span></span> <span data-ttu-id="73879-348">自 .NET Core 2.2 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="73879-348">Available since .NET Core 2.2 SDK.</span></span>

<span data-ttu-id="73879-349">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-349">\*\*_</span></span>

### <a name="classlib"></a><span data-ttu-id="73879-350">classlib</span><span class="sxs-lookup"><span data-stu-id="73879-350">classlib</span></span>

- <span data-ttu-id="73879-351">_ *`-f|--framework <FRAMEWORK>`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-351">_ *`-f|--framework <FRAMEWORK>`*\*</span></span>

  <span data-ttu-id="73879-352">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="73879-352">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="73879-353">值：`netcoreapp<version>`（要创建 .NET Core 类库的话）或 `netstandard<version>`（要创建 .NET Standard 类库的话）。</span><span class="sxs-lookup"><span data-stu-id="73879-353">Values: `netcoreapp<version>` to create a .NET Core Class Library or `netstandard<version>` to create a .NET Standard Class Library.</span></span> <span data-ttu-id="73879-354">默认值为 `netstandard2.0`。</span><span class="sxs-lookup"><span data-stu-id="73879-354">The default value is `netstandard2.0`.</span></span>

- **`--langVersion <VERSION_NUMBER>`**

  <span data-ttu-id="73879-355">在已创建的项目文件中设置 `LangVersion` 属性。</span><span class="sxs-lookup"><span data-stu-id="73879-355">Sets the `LangVersion` property in the created project file.</span></span> <span data-ttu-id="73879-356">例如，使用 `--langVersion 7.3` 以使用 C# 7.3。</span><span class="sxs-lookup"><span data-stu-id="73879-356">For example, use `--langVersion 7.3` to use C# 7.3.</span></span> <span data-ttu-id="73879-357">不支持 F#。</span><span class="sxs-lookup"><span data-stu-id="73879-357">Not supported for F#.</span></span> <span data-ttu-id="73879-358">自 .NET Core 2.2 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="73879-358">Available since .NET Core 2.2 SDK.</span></span>

  <span data-ttu-id="73879-359">有关默认的 C# 版本列表，请参阅[默认](../../csharp/language-reference/configure-language-version.md#defaults)。</span><span class="sxs-lookup"><span data-stu-id="73879-359">For a list of default C# versions, see [Defaults](../../csharp/language-reference/configure-language-version.md#defaults).</span></span>

- **`--no-restore`**

  <span data-ttu-id="73879-360">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="73879-360">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="73879-361">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-361">\*\*_</span></span>

### <a name="wpf-wpflib-wpfcustomcontrollib-wpfusercontrollib"></a><a name="wpf"></a> <span data-ttu-id="73879-362">wpf、wpflib、wpfcustomcontrollib、wpfusercontrollib</span><span class="sxs-lookup"><span data-stu-id="73879-362">wpf, wpflib, wpfcustomcontrollib, wpfusercontrollib</span></span>

- <span data-ttu-id="73879-363">_ *`-f|--framework <FRAMEWORK>`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-363">_ *`-f|--framework <FRAMEWORK>`*\*</span></span>

  <span data-ttu-id="73879-364">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="73879-364">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="73879-365">默认值为 `netcoreapp3.1`。</span><span class="sxs-lookup"><span data-stu-id="73879-365">The default value is `netcoreapp3.1`.</span></span> <span data-ttu-id="73879-366">自 .NET Core 3.1 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="73879-366">Available since .NET Core 3.1 SDK.</span></span>

- **`--langVersion <VERSION_NUMBER>`**

  <span data-ttu-id="73879-367">在已创建的项目文件中设置 `LangVersion` 属性。</span><span class="sxs-lookup"><span data-stu-id="73879-367">Sets the `LangVersion` property in the created project file.</span></span> <span data-ttu-id="73879-368">例如，使用 `--langVersion 7.3` 以使用 C# 7.3。</span><span class="sxs-lookup"><span data-stu-id="73879-368">For example, use `--langVersion 7.3` to use C# 7.3.</span></span>

  <span data-ttu-id="73879-369">有关默认的 C# 版本列表，请参阅[默认](../../csharp/language-reference/configure-language-version.md#defaults)。</span><span class="sxs-lookup"><span data-stu-id="73879-369">For a list of default C# versions, see [Defaults](../../csharp/language-reference/configure-language-version.md#defaults).</span></span>

- **`--no-restore`**

  <span data-ttu-id="73879-370">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="73879-370">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="73879-371">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-371">\*\*_</span></span>

### <a name="winforms-winformslib"></a><a name="winforms"></a> <span data-ttu-id="73879-372">winforms、winformslib</span><span class="sxs-lookup"><span data-stu-id="73879-372">winforms, winformslib</span></span>

- <span data-ttu-id="73879-373">_ *`--langVersion <VERSION_NUMBER>`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-373">_ *`--langVersion <VERSION_NUMBER>`*\*</span></span>

  <span data-ttu-id="73879-374">在已创建的项目文件中设置 `LangVersion` 属性。</span><span class="sxs-lookup"><span data-stu-id="73879-374">Sets the `LangVersion` property in the created project file.</span></span> <span data-ttu-id="73879-375">例如，使用 `--langVersion 7.3` 以使用 C# 7.3。</span><span class="sxs-lookup"><span data-stu-id="73879-375">For example, use `--langVersion 7.3` to use C# 7.3.</span></span>

  <span data-ttu-id="73879-376">有关默认的 C# 版本列表，请参阅[默认](../../csharp/language-reference/configure-language-version.md#defaults)。</span><span class="sxs-lookup"><span data-stu-id="73879-376">For a list of default C# versions, see [Defaults](../../csharp/language-reference/configure-language-version.md#defaults).</span></span>

- **`--no-restore`**

  <span data-ttu-id="73879-377">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="73879-377">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="73879-378">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-378">\*\*_</span></span>

### <a name="worker-grpc"></a><a name="web-others"></a> <span data-ttu-id="73879-379">worker、grpc</span><span class="sxs-lookup"><span data-stu-id="73879-379">worker, grpc</span></span>

- <span data-ttu-id="73879-380">_ *`-f|--framework <FRAMEWORK>`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-380">_ *`-f|--framework <FRAMEWORK>`*\*</span></span>

  <span data-ttu-id="73879-381">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="73879-381">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="73879-382">默认值为 `netcoreapp3.1`。</span><span class="sxs-lookup"><span data-stu-id="73879-382">The default value is `netcoreapp3.1`.</span></span> <span data-ttu-id="73879-383">自 .NET Core 3.1 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="73879-383">Available since .NET Core 3.1 SDK.</span></span>

- **`--exclude-launch-settings`**

  <span data-ttu-id="73879-384">从生成的模板中排除 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="73879-384">Excludes *launchSettings.json* from the generated template.</span></span>

- **`--no-restore`**

  <span data-ttu-id="73879-385">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="73879-385">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="73879-386">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-386">\*\*_</span></span>

### <a name="mstest-xunit"></a><a name="test"></a> <span data-ttu-id="73879-387">mstest、xunit</span><span class="sxs-lookup"><span data-stu-id="73879-387">mstest, xunit</span></span>

- <span data-ttu-id="73879-388">_ *`-f|--framework <FRAMEWORK>`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-388">_ *`-f|--framework <FRAMEWORK>`*\*</span></span>

  <span data-ttu-id="73879-389">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="73879-389">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="73879-390">自 .NET Core 3.0 SDK 起可用的选项。</span><span class="sxs-lookup"><span data-stu-id="73879-390">Option available since .NET Core 3.0 SDK.</span></span>

  <span data-ttu-id="73879-391">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="73879-391">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="73879-392">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="73879-392">SDK version</span></span> | <span data-ttu-id="73879-393">默认值</span><span class="sxs-lookup"><span data-stu-id="73879-393">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="73879-394">3.1</span><span class="sxs-lookup"><span data-stu-id="73879-394">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="73879-395">3.0</span><span class="sxs-lookup"><span data-stu-id="73879-395">3.0</span></span>         | `netcoreapp3.0` |

- **`-p|--enable-pack`**

  <span data-ttu-id="73879-396">允许使用 [dotnet pack](dotnet-pack.md) 为项目打包。</span><span class="sxs-lookup"><span data-stu-id="73879-396">Enables packaging for the project using [dotnet pack](dotnet-pack.md).</span></span>

- **`--no-restore`**

  <span data-ttu-id="73879-397">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="73879-397">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="73879-398">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-398">\*\*_</span></span>

### <a name="nunit"></a><span data-ttu-id="73879-399">nunit</span><span class="sxs-lookup"><span data-stu-id="73879-399">nunit</span></span>

- <span data-ttu-id="73879-400">_ *`-f|--framework <FRAMEWORK>`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-400">_ *`-f|--framework <FRAMEWORK>`*\*</span></span>

  <span data-ttu-id="73879-401">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="73879-401">Specifies the [framework](../../standard/frameworks.md) to target.</span></span>

  <span data-ttu-id="73879-402">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="73879-402">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="73879-403">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="73879-403">SDK version</span></span> | <span data-ttu-id="73879-404">默认值</span><span class="sxs-lookup"><span data-stu-id="73879-404">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="73879-405">3.1</span><span class="sxs-lookup"><span data-stu-id="73879-405">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="73879-406">3.0</span><span class="sxs-lookup"><span data-stu-id="73879-406">3.0</span></span>         | `netcoreapp3.0` |
  | <span data-ttu-id="73879-407">2.2</span><span class="sxs-lookup"><span data-stu-id="73879-407">2.2</span></span>         | `netcoreapp2.2` |
  | <span data-ttu-id="73879-408">2.1</span><span class="sxs-lookup"><span data-stu-id="73879-408">2.1</span></span>         | `netcoreapp2.1` |

- **`-p|--enable-pack`**

  <span data-ttu-id="73879-409">允许使用 [dotnet pack](dotnet-pack.md) 为项目打包。</span><span class="sxs-lookup"><span data-stu-id="73879-409">Enables packaging for the project using [dotnet pack](dotnet-pack.md).</span></span>

- **`--no-restore`**

  <span data-ttu-id="73879-410">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="73879-410">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="73879-411">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-411">\*\*_</span></span>

### <a name="page"></a><span data-ttu-id="73879-412">页</span><span class="sxs-lookup"><span data-stu-id="73879-412">page</span></span>

- <span data-ttu-id="73879-413">_ *`-na|--namespace <NAMESPACE_NAME>`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-413">_ *`-na|--namespace <NAMESPACE_NAME>`*\*</span></span>

  <span data-ttu-id="73879-414">已生成代码的命名空间。</span><span class="sxs-lookup"><span data-stu-id="73879-414">Namespace for the generated code.</span></span> <span data-ttu-id="73879-415">默认值为 `MyApp.Namespace`。</span><span class="sxs-lookup"><span data-stu-id="73879-415">The default value is `MyApp.Namespace`.</span></span>

- **`-np|--no-pagemodel`**

  <span data-ttu-id="73879-416">创建不含 PageModel 的页。</span><span class="sxs-lookup"><span data-stu-id="73879-416">Creates the page without a PageModel.</span></span>

<span data-ttu-id="73879-417">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-417">\*\*_</span></span>

### <a name="viewimports-proto"></a><a name="namespace"></a> <span data-ttu-id="73879-418">viewimports、proto</span><span class="sxs-lookup"><span data-stu-id="73879-418">viewimports, proto</span></span>

- <span data-ttu-id="73879-419">_ *`-na|--namespace <NAMESPACE_NAME>`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-419">_ *`-na|--namespace <NAMESPACE_NAME>`*\*</span></span>

  <span data-ttu-id="73879-420">已生成代码的命名空间。</span><span class="sxs-lookup"><span data-stu-id="73879-420">Namespace for the generated code.</span></span> <span data-ttu-id="73879-421">默认值为 `MyApp.Namespace`。</span><span class="sxs-lookup"><span data-stu-id="73879-421">The default value is `MyApp.Namespace`.</span></span>

<span data-ttu-id="73879-422">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-422">\*\*_</span></span>

### <a name="blazorserver"></a><span data-ttu-id="73879-423">blazorserver</span><span class="sxs-lookup"><span data-stu-id="73879-423">blazorserver</span></span>

- <span data-ttu-id="73879-424">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-424">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span></span>

  <span data-ttu-id="73879-425">要使用的身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="73879-425">The type of authentication to use.</span></span> <span data-ttu-id="73879-426">可能的值为：</span><span class="sxs-lookup"><span data-stu-id="73879-426">The possible values are:</span></span>

  - <span data-ttu-id="73879-427">`None` - 不进行身份验证（默认）。</span><span class="sxs-lookup"><span data-stu-id="73879-427">`None` - No authentication (Default).</span></span>
  - <span data-ttu-id="73879-428">`Individual` - 个人身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-428">`Individual` - Individual authentication.</span></span>
  - <span data-ttu-id="73879-429">`IndividualB2C` - 使用 Azure AD B2C 进行个人身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-429">`IndividualB2C` - Individual authentication with Azure AD B2C.</span></span>
  - <span data-ttu-id="73879-430">`SingleOrg` - 对一个租户进行组织身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-430">`SingleOrg` - Organizational authentication for a single tenant.</span></span>
  - <span data-ttu-id="73879-431">`MultiOrg` - 对多个租户进行组织身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-431">`MultiOrg` - Organizational authentication for multiple tenants.</span></span>
  - <span data-ttu-id="73879-432">`Windows` - Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-432">`Windows` - Windows authentication.</span></span>

- **`--aad-b2c-instance <INSTANCE>`**

  <span data-ttu-id="73879-433">要连接到的 Azure Active Directory B2C 实例。</span><span class="sxs-lookup"><span data-stu-id="73879-433">The Azure Active Directory B2C instance to connect to.</span></span> <span data-ttu-id="73879-434">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-434">Use with `IndividualB2C` authentication.</span></span> <span data-ttu-id="73879-435">默认值为 `https://login.microsoftonline.com/tfp/`。</span><span class="sxs-lookup"><span data-stu-id="73879-435">The default value is `https://login.microsoftonline.com/tfp/`.</span></span>

- **`-ssp|--susi-policy-id <ID>`**

  <span data-ttu-id="73879-436">此项目的登录和注册策略 ID。</span><span class="sxs-lookup"><span data-stu-id="73879-436">The sign-in and sign-up policy ID for this project.</span></span> <span data-ttu-id="73879-437">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-437">Use with `IndividualB2C` authentication.</span></span>

- **`-rp|--reset-password-policy-id <ID>`**

  <span data-ttu-id="73879-438">此项目的重置密码策略 ID。</span><span class="sxs-lookup"><span data-stu-id="73879-438">The reset password policy ID for this project.</span></span> <span data-ttu-id="73879-439">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-439">Use with `IndividualB2C` authentication.</span></span>

- **`-ep|--edit-profile-policy-id <ID>`**

  <span data-ttu-id="73879-440">此项目的编辑配置文件策略 ID。</span><span class="sxs-lookup"><span data-stu-id="73879-440">The edit profile policy ID for this project.</span></span> <span data-ttu-id="73879-441">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-441">Use with `IndividualB2C` authentication.</span></span>

- **`--aad-instance <INSTANCE>`**

  <span data-ttu-id="73879-442">要连接到的 Azure Active Directory 实例。</span><span class="sxs-lookup"><span data-stu-id="73879-442">The Azure Active Directory instance to connect to.</span></span> <span data-ttu-id="73879-443">与 `SingleOrg` 或 `MultiOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-443">Use with `SingleOrg` or `MultiOrg` authentication.</span></span> <span data-ttu-id="73879-444">默认值为 `https://login.microsoftonline.com/`。</span><span class="sxs-lookup"><span data-stu-id="73879-444">The default value is `https://login.microsoftonline.com/`.</span></span>

- **`--client-id <ID>`**

  <span data-ttu-id="73879-445">此项目的客户端 ID。</span><span class="sxs-lookup"><span data-stu-id="73879-445">The Client ID for this project.</span></span> <span data-ttu-id="73879-446">与 `IndividualB2C`、`SingleOrg` 或 `MultiOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-446">Use with `IndividualB2C`, `SingleOrg`, or `MultiOrg` authentication.</span></span> <span data-ttu-id="73879-447">默认值为 `11111111-1111-1111-11111111111111111`。</span><span class="sxs-lookup"><span data-stu-id="73879-447">The default value is `11111111-1111-1111-11111111111111111`.</span></span>

- **`--domain <DOMAIN>`**

  <span data-ttu-id="73879-448">目录租户的域。</span><span class="sxs-lookup"><span data-stu-id="73879-448">The domain for the directory tenant.</span></span> <span data-ttu-id="73879-449">与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-449">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="73879-450">默认值为 `qualified.domain.name`。</span><span class="sxs-lookup"><span data-stu-id="73879-450">The default value is `qualified.domain.name`.</span></span>

- **`--tenant-id <ID>`**

  <span data-ttu-id="73879-451">要连接到的目录的 TenantId ID。</span><span class="sxs-lookup"><span data-stu-id="73879-451">The TenantId ID of the directory to connect to.</span></span> <span data-ttu-id="73879-452">与 `SingleOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-452">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="73879-453">默认值为 `22222222-2222-2222-2222-222222222222`。</span><span class="sxs-lookup"><span data-stu-id="73879-453">The default value is `22222222-2222-2222-2222-222222222222`.</span></span>

- **`--callback-path <PATH>`**

  <span data-ttu-id="73879-454">重定向 URI 的应用程序基路径中的请求路径。</span><span class="sxs-lookup"><span data-stu-id="73879-454">The request path within the application's base path of the redirect URI.</span></span> <span data-ttu-id="73879-455">与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-455">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="73879-456">默认值为 `/signin-oidc`。</span><span class="sxs-lookup"><span data-stu-id="73879-456">The default value is `/signin-oidc`.</span></span>

- **`-r|--org-read-access`**

  <span data-ttu-id="73879-457">允许此应用程序对目录进行读取访问。</span><span class="sxs-lookup"><span data-stu-id="73879-457">Allows this application read-access to the directory.</span></span> <span data-ttu-id="73879-458">仅适用于 `SingleOrg` 或 `MultiOrg` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-458">Only applies to `SingleOrg` or `MultiOrg` authentication.</span></span>

- **`--exclude-launch-settings`**

  <span data-ttu-id="73879-459">从生成的模板中排除 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="73879-459">Excludes *launchSettings.json* from the generated template.</span></span>

- **`--no-https`**

  <span data-ttu-id="73879-460">关闭 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="73879-460">Turns off HTTPS.</span></span> <span data-ttu-id="73879-461">此选项仅适用于 `Individual`、`IndividualB2C`、`SingleOrg` 和 `MultiOrg` 未用于 `--auth` 的情况。</span><span class="sxs-lookup"><span data-stu-id="73879-461">This option only applies if `Individual`, `IndividualB2C`, `SingleOrg`, or `MultiOrg` aren't being used for `--auth`.</span></span>

- **`-uld|--use-local-db`**

  <span data-ttu-id="73879-462">指定应使用 LocalDB，而不使用 SQLite。</span><span class="sxs-lookup"><span data-stu-id="73879-462">Specifies LocalDB should be used instead of SQLite.</span></span> <span data-ttu-id="73879-463">仅适用于 `Individual` 或 `IndividualB2C` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-463">Only applies to `Individual` or `IndividualB2C` authentication.</span></span>

- **`--no-restore`**

  <span data-ttu-id="73879-464">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="73879-464">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="73879-465">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-465">\*\*_</span></span>

### <a name="blazorwasm"></a><span data-ttu-id="73879-466">blazorwasm</span><span class="sxs-lookup"><span data-stu-id="73879-466">blazorwasm</span></span>

- <span data-ttu-id="73879-467">_ *`-f|--framework <FRAMEWORK>`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-467">_ *`-f|--framework <FRAMEWORK>`*\*</span></span>

  <span data-ttu-id="73879-468">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="73879-468">Specifies the [framework](../../standard/frameworks.md) to target.</span></span>

  <span data-ttu-id="73879-469">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="73879-469">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="73879-470">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="73879-470">SDK version</span></span> | <span data-ttu-id="73879-471">默认值</span><span class="sxs-lookup"><span data-stu-id="73879-471">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="73879-472">5.0</span><span class="sxs-lookup"><span data-stu-id="73879-472">5.0</span></span>         | `net5.0`        |
  | <span data-ttu-id="73879-473">3.1</span><span class="sxs-lookup"><span data-stu-id="73879-473">3.1</span></span>         | `netcoreapp3.1` |

- **`--no-restore`**

  <span data-ttu-id="73879-474">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="73879-474">Doesn't execute an implicit restore during project creation.</span></span>

- **`-ho|--hosted`**

  <span data-ttu-id="73879-475">包括 :::no-loc(Blazor)::: :::no-loc(WebAssembly)::: 应用的 ASP.NET Core 主机。</span><span class="sxs-lookup"><span data-stu-id="73879-475">Includes an ASP.NET Core host for the :::no-loc(Blazor)::: :::no-loc(WebAssembly)::: app.</span></span>

- **`-au|--auth <AUTHENTICATION_TYPE>`**

  <span data-ttu-id="73879-476">要使用的身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="73879-476">The type of authentication to use.</span></span> <span data-ttu-id="73879-477">可能的值为：</span><span class="sxs-lookup"><span data-stu-id="73879-477">The possible values are:</span></span>

  - <span data-ttu-id="73879-478">`None` - 不进行身份验证（默认）。</span><span class="sxs-lookup"><span data-stu-id="73879-478">`None` - No authentication (Default).</span></span>
  - <span data-ttu-id="73879-479">`Individual` - 个人身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-479">`Individual` - Individual authentication.</span></span>
  - <span data-ttu-id="73879-480">`IndividualB2C` - 使用 Azure AD B2C 进行个人身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-480">`IndividualB2C` - Individual authentication with Azure AD B2C.</span></span>
  - <span data-ttu-id="73879-481">`SingleOrg` - 对一个租户进行组织身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-481">`SingleOrg` - Organizational authentication for a single tenant.</span></span>

- **`--authority <AUTHORITY>`**

  <span data-ttu-id="73879-482">OIDC 提供程序所属的机构。</span><span class="sxs-lookup"><span data-stu-id="73879-482">The authority of the OIDC provider.</span></span> <span data-ttu-id="73879-483">与 `Individual` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-483">Use with `Individual` authentication.</span></span> <span data-ttu-id="73879-484">默认值为 `https://login.microsoftonline.com/`。</span><span class="sxs-lookup"><span data-stu-id="73879-484">The default value is `https://login.microsoftonline.com/`.</span></span>

- **`--aad-b2c-instance <INSTANCE>`**

  <span data-ttu-id="73879-485">要连接到的 Azure Active Directory B2C 实例。</span><span class="sxs-lookup"><span data-stu-id="73879-485">The Azure Active Directory B2C instance to connect to.</span></span> <span data-ttu-id="73879-486">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-486">Use with `IndividualB2C` authentication.</span></span> <span data-ttu-id="73879-487">默认值为 `https://aadB2CInstance.b2clogin.com/`。</span><span class="sxs-lookup"><span data-stu-id="73879-487">The default value is `https://aadB2CInstance.b2clogin.com/`.</span></span>

- **`-ssp|--susi-policy-id <ID>`**

  <span data-ttu-id="73879-488">此项目的登录和注册策略 ID。</span><span class="sxs-lookup"><span data-stu-id="73879-488">The sign-in and sign-up policy ID for this project.</span></span> <span data-ttu-id="73879-489">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-489">Use with `IndividualB2C` authentication.</span></span>

- **`--aad-instance <INSTANCE>`**

  <span data-ttu-id="73879-490">要连接到的 Azure Active Directory 实例。</span><span class="sxs-lookup"><span data-stu-id="73879-490">The Azure Active Directory instance to connect to.</span></span> <span data-ttu-id="73879-491">与 `SingleOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-491">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="73879-492">默认值为 `https://login.microsoftonline.com/`。</span><span class="sxs-lookup"><span data-stu-id="73879-492">The default value is `https://login.microsoftonline.com/`.</span></span>

- **`--client-id <ID>`**

  <span data-ttu-id="73879-493">此项目的客户端 ID。</span><span class="sxs-lookup"><span data-stu-id="73879-493">The Client ID for this project.</span></span> <span data-ttu-id="73879-494">在独立方案中与 `IndividualB2C`、`SingleOrg` 或 `Individual` 身份验证一起使用。</span><span class="sxs-lookup"><span data-stu-id="73879-494">Use with `IndividualB2C`, `SingleOrg`, or `Individual` authentication in standalone scenarios.</span></span> <span data-ttu-id="73879-495">默认值为 `33333333-3333-3333-33333333333333333`。</span><span class="sxs-lookup"><span data-stu-id="73879-495">The default value is `33333333-3333-3333-33333333333333333`.</span></span>

- **`--domain <DOMAIN>`**

  <span data-ttu-id="73879-496">目录租户的域。</span><span class="sxs-lookup"><span data-stu-id="73879-496">The domain for the directory tenant.</span></span> <span data-ttu-id="73879-497">与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-497">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="73879-498">默认值为 `qualified.domain.name`。</span><span class="sxs-lookup"><span data-stu-id="73879-498">The default value is `qualified.domain.name`.</span></span>

- **`--app-id-uri <URI>`**

  <span data-ttu-id="73879-499">要调用的服务器 API 的应用 ID URI。</span><span class="sxs-lookup"><span data-stu-id="73879-499">The App ID Uri for the server API you want to call.</span></span> <span data-ttu-id="73879-500">与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-500">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="73879-501">默认值为 `api.id.uri`。</span><span class="sxs-lookup"><span data-stu-id="73879-501">The default value is `api.id.uri`.</span></span>

- **`--api-client-id <ID>`**

  <span data-ttu-id="73879-502">服务器承载的 API 的客户端 ID。</span><span class="sxs-lookup"><span data-stu-id="73879-502">The Client ID for the API that the server hosts.</span></span> <span data-ttu-id="73879-503">与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-503">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="73879-504">默认值为 `11111111-1111-1111-11111111111111111`。</span><span class="sxs-lookup"><span data-stu-id="73879-504">The default value is `11111111-1111-1111-11111111111111111`.</span></span>

- **`-s|--default-scope <SCOPE>`**

  <span data-ttu-id="73879-505">客户端为预配访问令牌所需请求的 API 作用域。</span><span class="sxs-lookup"><span data-stu-id="73879-505">The API scope the client needs to request to provision an access token.</span></span> <span data-ttu-id="73879-506">与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-506">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="73879-507">默认值为 `user_impersonation`。</span><span class="sxs-lookup"><span data-stu-id="73879-507">The default value is `user_impersonation`.</span></span>

- **`--tenant-id <ID>`**

  <span data-ttu-id="73879-508">要连接到的目录的 TenantId ID。</span><span class="sxs-lookup"><span data-stu-id="73879-508">The TenantId ID of the directory to connect to.</span></span> <span data-ttu-id="73879-509">与 `SingleOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-509">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="73879-510">默认值为 `22222222-2222-2222-2222-222222222222`。</span><span class="sxs-lookup"><span data-stu-id="73879-510">The default value is `22222222-2222-2222-2222-222222222222`.</span></span>

- **`-r|--org-read-access`**

  <span data-ttu-id="73879-511">允许此应用程序对目录进行读取访问。</span><span class="sxs-lookup"><span data-stu-id="73879-511">Allows this application read-access to the directory.</span></span> <span data-ttu-id="73879-512">仅适用于 `SingleOrg` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-512">Only applies to `SingleOrg` authentication.</span></span>

- **`--exclude-launch-settings`**

  <span data-ttu-id="73879-513">从生成的模板中排除 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="73879-513">Excludes *launchSettings.json* from the generated template.</span></span>

- **`-p|--pwa`**

  <span data-ttu-id="73879-514">生成支持安装和脱机使用的渐进式 Web 应用程序 (PWA)。</span><span class="sxs-lookup"><span data-stu-id="73879-514">produces a Progressive Web Application (PWA) supporting installation and offline use.</span></span>

- **`--no-https`**

  <span data-ttu-id="73879-515">关闭 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="73879-515">Turns off HTTPS.</span></span> <span data-ttu-id="73879-516">此选项仅适用于 `Individual`、`IndividualB2C` 和 `SingleOrg` 未用于 `--auth` 的情况。</span><span class="sxs-lookup"><span data-stu-id="73879-516">This option only applies if `Individual`, `IndividualB2C`, or `SingleOrg` aren't being used for `--auth`.</span></span>

- **`-uld|--use-local-db`**

  <span data-ttu-id="73879-517">指定应使用 LocalDB，而不使用 SQLite。</span><span class="sxs-lookup"><span data-stu-id="73879-517">Specifies LocalDB should be used instead of SQLite.</span></span> <span data-ttu-id="73879-518">仅适用于 `Individual` 或 `IndividualB2C` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-518">Only applies to `Individual` or `IndividualB2C` authentication.</span></span>

- **`--called-api-url <URL>`**

  <span data-ttu-id="73879-519">要从 Web 应用调用的 API 的 URL。</span><span class="sxs-lookup"><span data-stu-id="73879-519">URL of the API to call from the web app.</span></span> <span data-ttu-id="73879-520">仅适用于未指定 ASP.NET Core 主机的 `SingleOrg` 或 `IndividualB2C` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-520">Only applies to `SingleOrg` or `IndividualB2C` authentication without an ASP.NET Core host specified.</span></span> <span data-ttu-id="73879-521">默认值为 `https://graph.microsoft.com/v1.0/me`。</span><span class="sxs-lookup"><span data-stu-id="73879-521">The default value is `https://graph.microsoft.com/v1.0/me`.</span></span>

- **`--calls-graph`**

  <span data-ttu-id="73879-522">指定 Web 应用是否调用 Microsoft Graph。</span><span class="sxs-lookup"><span data-stu-id="73879-522">Specifies if the web app calls Microsoft Graph.</span></span> <span data-ttu-id="73879-523">仅适用于 `SingleOrg` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-523">Only applies to `SingleOrg` authentication.</span></span>

- **`--called-api-scopes <SCOPES>`**

  <span data-ttu-id="73879-524">为从 Web 应用调用 API 而请求的作用域。</span><span class="sxs-lookup"><span data-stu-id="73879-524">Scopes to request to call the API from the web app.</span></span> <span data-ttu-id="73879-525">仅适用于未指定 ASP.NET Core 主机的 `SingleOrg` 或 `IndividualB2C` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-525">Only applies to `SingleOrg` or `IndividualB2C` authentication without an ASP.NET Core host specified.</span></span> <span data-ttu-id="73879-526">默认值为 `user.read`。</span><span class="sxs-lookup"><span data-stu-id="73879-526">The default is `user.read`.</span></span>

<span data-ttu-id="73879-527">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-527">\*\*_</span></span>

### <a name="web"></a><span data-ttu-id="73879-528">Web</span><span class="sxs-lookup"><span data-stu-id="73879-528">web</span></span>

- <span data-ttu-id="73879-529">_ *`--exclude-launch-settings`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-529">_ *`--exclude-launch-settings`*\*</span></span>

  <span data-ttu-id="73879-530">从生成的模板中排除 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="73879-530">Excludes *launchSettings.json* from the generated template.</span></span>

- **`-f|--framework <FRAMEWORK>`**

  <span data-ttu-id="73879-531">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="73879-531">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="73879-532">选项在 .NET Core 2.2 SDK 中不可用。</span><span class="sxs-lookup"><span data-stu-id="73879-532">Option not available in .NET Core 2.2 SDK.</span></span>

  <span data-ttu-id="73879-533">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="73879-533">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="73879-534">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="73879-534">SDK version</span></span> | <span data-ttu-id="73879-535">默认值</span><span class="sxs-lookup"><span data-stu-id="73879-535">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="73879-536">3.1</span><span class="sxs-lookup"><span data-stu-id="73879-536">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="73879-537">3.0</span><span class="sxs-lookup"><span data-stu-id="73879-537">3.0</span></span>         | `netcoreapp3.0` |
  | <span data-ttu-id="73879-538">2.1</span><span class="sxs-lookup"><span data-stu-id="73879-538">2.1</span></span>         | `netcoreapp2.1` |

- **`--no-restore`**

  <span data-ttu-id="73879-539">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="73879-539">Doesn't execute an implicit restore during project creation.</span></span>

- **`--no-https`**

  <span data-ttu-id="73879-540">关闭 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="73879-540">Turns off HTTPS.</span></span>

<span data-ttu-id="73879-541">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-541">\*\*_</span></span>

### <a name="mvc-webapp"></a><a name="web-options"></a> <span data-ttu-id="73879-542">mvc、webapp</span><span class="sxs-lookup"><span data-stu-id="73879-542">mvc, webapp</span></span>

- <span data-ttu-id="73879-543">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-543">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span></span>

  <span data-ttu-id="73879-544">要使用的身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="73879-544">The type of authentication to use.</span></span> <span data-ttu-id="73879-545">可能的值为：</span><span class="sxs-lookup"><span data-stu-id="73879-545">The possible values are:</span></span>

  - <span data-ttu-id="73879-546">`None` - 不进行身份验证（默认）。</span><span class="sxs-lookup"><span data-stu-id="73879-546">`None` - No authentication (Default).</span></span>
  - <span data-ttu-id="73879-547">`Individual` - 个人身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-547">`Individual` - Individual authentication.</span></span>
  - <span data-ttu-id="73879-548">`IndividualB2C` - 使用 Azure AD B2C 进行个人身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-548">`IndividualB2C` - Individual authentication with Azure AD B2C.</span></span>
  - <span data-ttu-id="73879-549">`SingleOrg` - 对一个租户进行组织身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-549">`SingleOrg` - Organizational authentication for a single tenant.</span></span>
  - <span data-ttu-id="73879-550">`MultiOrg` - 对多个租户进行组织身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-550">`MultiOrg` - Organizational authentication for multiple tenants.</span></span>
  - <span data-ttu-id="73879-551">`Windows` - Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-551">`Windows` - Windows authentication.</span></span>

- **`--aad-b2c-instance <INSTANCE>`**

  <span data-ttu-id="73879-552">要连接到的 Azure Active Directory B2C 实例。</span><span class="sxs-lookup"><span data-stu-id="73879-552">The Azure Active Directory B2C instance to connect to.</span></span> <span data-ttu-id="73879-553">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-553">Use with `IndividualB2C` authentication.</span></span> <span data-ttu-id="73879-554">默认值为 `https://login.microsoftonline.com/tfp/`。</span><span class="sxs-lookup"><span data-stu-id="73879-554">The default value is `https://login.microsoftonline.com/tfp/`.</span></span>

- **`-ssp|--susi-policy-id <ID>`**

  <span data-ttu-id="73879-555">此项目的登录和注册策略 ID。</span><span class="sxs-lookup"><span data-stu-id="73879-555">The sign-in and sign-up policy ID for this project.</span></span> <span data-ttu-id="73879-556">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-556">Use with `IndividualB2C` authentication.</span></span>

- **`-rp|--reset-password-policy-id <ID>`**

  <span data-ttu-id="73879-557">此项目的重置密码策略 ID。</span><span class="sxs-lookup"><span data-stu-id="73879-557">The reset password policy ID for this project.</span></span> <span data-ttu-id="73879-558">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-558">Use with `IndividualB2C` authentication.</span></span>

- **`-ep|--edit-profile-policy-id <ID>`**

  <span data-ttu-id="73879-559">此项目的编辑配置文件策略 ID。</span><span class="sxs-lookup"><span data-stu-id="73879-559">The edit profile policy ID for this project.</span></span> <span data-ttu-id="73879-560">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-560">Use with `IndividualB2C` authentication.</span></span>

- **`--aad-instance <INSTANCE>`**

  <span data-ttu-id="73879-561">要连接到的 Azure Active Directory 实例。</span><span class="sxs-lookup"><span data-stu-id="73879-561">The Azure Active Directory instance to connect to.</span></span> <span data-ttu-id="73879-562">与 `SingleOrg` 或 `MultiOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-562">Use with `SingleOrg` or `MultiOrg` authentication.</span></span> <span data-ttu-id="73879-563">默认值为 `https://login.microsoftonline.com/`。</span><span class="sxs-lookup"><span data-stu-id="73879-563">The default value is `https://login.microsoftonline.com/`.</span></span>

- **`--client-id <ID>`**

  <span data-ttu-id="73879-564">此项目的客户端 ID。</span><span class="sxs-lookup"><span data-stu-id="73879-564">The Client ID for this project.</span></span> <span data-ttu-id="73879-565">与 `IndividualB2C`、`SingleOrg` 或 `MultiOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-565">Use with `IndividualB2C`, `SingleOrg`, or `MultiOrg` authentication.</span></span> <span data-ttu-id="73879-566">默认值为 `11111111-1111-1111-11111111111111111`。</span><span class="sxs-lookup"><span data-stu-id="73879-566">The default value is `11111111-1111-1111-11111111111111111`.</span></span>

- **`--domain <DOMAIN>`**

  <span data-ttu-id="73879-567">目录租户的域。</span><span class="sxs-lookup"><span data-stu-id="73879-567">The domain for the directory tenant.</span></span> <span data-ttu-id="73879-568">与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-568">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="73879-569">默认值为 `qualified.domain.name`。</span><span class="sxs-lookup"><span data-stu-id="73879-569">The default value is `qualified.domain.name`.</span></span>

- **`--tenant-id <ID>`**

  <span data-ttu-id="73879-570">要连接到的目录的 TenantId ID。</span><span class="sxs-lookup"><span data-stu-id="73879-570">The TenantId ID of the directory to connect to.</span></span> <span data-ttu-id="73879-571">与 `SingleOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-571">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="73879-572">默认值为 `22222222-2222-2222-2222-222222222222`。</span><span class="sxs-lookup"><span data-stu-id="73879-572">The default value is `22222222-2222-2222-2222-222222222222`.</span></span>

- **`--callback-path <PATH>`**

  <span data-ttu-id="73879-573">重定向 URI 的应用程序基路径中的请求路径。</span><span class="sxs-lookup"><span data-stu-id="73879-573">The request path within the application's base path of the redirect URI.</span></span> <span data-ttu-id="73879-574">与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-574">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="73879-575">默认值为 `/signin-oidc`。</span><span class="sxs-lookup"><span data-stu-id="73879-575">The default value is `/signin-oidc`.</span></span>

- **`-r|--org-read-access`**

  <span data-ttu-id="73879-576">允许此应用程序对目录进行读取访问。</span><span class="sxs-lookup"><span data-stu-id="73879-576">Allows this application read-access to the directory.</span></span> <span data-ttu-id="73879-577">仅适用于 `SingleOrg` 或 `MultiOrg` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-577">Only applies to `SingleOrg` or `MultiOrg` authentication.</span></span>

- **`--exclude-launch-settings`**

  <span data-ttu-id="73879-578">从生成的模板中排除 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="73879-578">Excludes *launchSettings.json* from the generated template.</span></span>

- **`--no-https`**

  <span data-ttu-id="73879-579">关闭 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="73879-579">Turns off HTTPS.</span></span> <span data-ttu-id="73879-580">此选项仅适用于未使用 `Individual`、`IndividualB2C`、`SingleOrg` 和 `MultiOrg` 的情况。</span><span class="sxs-lookup"><span data-stu-id="73879-580">This option only applies if `Individual`, `IndividualB2C`, `SingleOrg`, or `MultiOrg` aren't being used.</span></span>

- **`-uld|--use-local-db`**

  <span data-ttu-id="73879-581">指定应使用 LocalDB，而不使用 SQLite。</span><span class="sxs-lookup"><span data-stu-id="73879-581">Specifies LocalDB should be used instead of SQLite.</span></span> <span data-ttu-id="73879-582">仅适用于 `Individual` 或 `IndividualB2C` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-582">Only applies to `Individual` or `IndividualB2C` authentication.</span></span>

- **`-f|--framework <FRAMEWORK>`**

  <span data-ttu-id="73879-583">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="73879-583">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="73879-584">自 .NET Core 3.0 SDK 起可用的选项。</span><span class="sxs-lookup"><span data-stu-id="73879-584">Option available since .NET Core 3.0 SDK.</span></span>

  <span data-ttu-id="73879-585">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="73879-585">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="73879-586">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="73879-586">SDK version</span></span> | <span data-ttu-id="73879-587">默认值</span><span class="sxs-lookup"><span data-stu-id="73879-587">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="73879-588">3.1</span><span class="sxs-lookup"><span data-stu-id="73879-588">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="73879-589">3.0</span><span class="sxs-lookup"><span data-stu-id="73879-589">3.0</span></span>         | `netcoreapp3.0` |

- **`--no-restore`**

  <span data-ttu-id="73879-590">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="73879-590">Doesn't execute an implicit restore during project creation.</span></span>

- **`--use-browserlink`**

  <span data-ttu-id="73879-591">在项目中添加 BrowserLink。</span><span class="sxs-lookup"><span data-stu-id="73879-591">Includes BrowserLink in the project.</span></span> <span data-ttu-id="73879-592">选项在 .NET Core 2.2 和 3.1 SDK 中不可用。</span><span class="sxs-lookup"><span data-stu-id="73879-592">Option not available in .NET Core 2.2 and 3.1 SDK.</span></span>

- **`-rrc|--razor-runtime-compilation`**

  <span data-ttu-id="73879-593">确定项目是否配置为在调试生成中使用 [Razor 运行时编译](/aspnet/core/mvc/views/view-compilation#runtime-compilation)。</span><span class="sxs-lookup"><span data-stu-id="73879-593">Determines if the project is configured to use [Razor runtime compilation](/aspnet/core/mvc/views/view-compilation#runtime-compilation) in Debug builds.</span></span> <span data-ttu-id="73879-594">自 .NET Core 3.1.201 SDK 起可用的选项。</span><span class="sxs-lookup"><span data-stu-id="73879-594">Option available since .NET Core 3.1.201 SDK.</span></span>

<span data-ttu-id="73879-595">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-595">\*\*_</span></span>

### <a name="angular-react"></a><a name="spa"></a> <span data-ttu-id="73879-596">angular、react</span><span class="sxs-lookup"><span data-stu-id="73879-596">angular, react</span></span>

- <span data-ttu-id="73879-597">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-597">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span></span>

  <span data-ttu-id="73879-598">要使用的身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="73879-598">The type of authentication to use.</span></span> <span data-ttu-id="73879-599">自 .NET Core 3.0 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="73879-599">Available since .NET Core 3.0 SDK.</span></span>
  
  <span data-ttu-id="73879-600">可能的值为：</span><span class="sxs-lookup"><span data-stu-id="73879-600">The possible values are:</span></span>

  - <span data-ttu-id="73879-601">`None` - 不进行身份验证（默认）。</span><span class="sxs-lookup"><span data-stu-id="73879-601">`None` - No authentication (Default).</span></span>
  - <span data-ttu-id="73879-602">`Individual` - 个人身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-602">`Individual` - Individual authentication.</span></span>

- **`--exclude-launch-settings`**

  <span data-ttu-id="73879-603">从生成的模板中排除 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="73879-603">Excludes *launchSettings.json* from the generated template.</span></span>

- **`--no-restore`**

  <span data-ttu-id="73879-604">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="73879-604">Doesn't execute an implicit restore during project creation.</span></span>

- **`--no-https`**

  <span data-ttu-id="73879-605">关闭 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="73879-605">Turns off HTTPS.</span></span> <span data-ttu-id="73879-606">仅当身份验证为 `None` 时，此选项才适用。</span><span class="sxs-lookup"><span data-stu-id="73879-606">This option only applies if authentication is `None`.</span></span>

- **`-uld|--use-local-db`**

  <span data-ttu-id="73879-607">指定应使用 LocalDB，而不使用 SQLite。</span><span class="sxs-lookup"><span data-stu-id="73879-607">Specifies LocalDB should be used instead of SQLite.</span></span> <span data-ttu-id="73879-608">仅适用于 `Individual` 或 `IndividualB2C` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-608">Only applies to `Individual` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="73879-609">自 .NET Core 3.0 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="73879-609">Available since .NET Core 3.0 SDK.</span></span>

- **`-f|--framework <FRAMEWORK>`**

  <span data-ttu-id="73879-610">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="73879-610">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="73879-611">选项在 .NET Core 2.2 SDK 中不可用。</span><span class="sxs-lookup"><span data-stu-id="73879-611">Option not available in .NET Core 2.2 SDK.</span></span>

  <span data-ttu-id="73879-612">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="73879-612">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="73879-613">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="73879-613">SDK version</span></span> | <span data-ttu-id="73879-614">默认值</span><span class="sxs-lookup"><span data-stu-id="73879-614">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="73879-615">3.1</span><span class="sxs-lookup"><span data-stu-id="73879-615">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="73879-616">3.0</span><span class="sxs-lookup"><span data-stu-id="73879-616">3.0</span></span>         | `netcoreapp3.0` |
  | <span data-ttu-id="73879-617">2.1</span><span class="sxs-lookup"><span data-stu-id="73879-617">2.1</span></span>         | `netcoreapp2.0` |

<span data-ttu-id="73879-618">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-618">\*\*_</span></span>

### <a name="reactredux"></a><span data-ttu-id="73879-619">reactredux</span><span class="sxs-lookup"><span data-stu-id="73879-619">reactredux</span></span>

- <span data-ttu-id="73879-620">_ *`--exclude-launch-settings`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-620">_ *`--exclude-launch-settings`*\*</span></span>

  <span data-ttu-id="73879-621">从生成的模板中排除 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="73879-621">Excludes *launchSettings.json* from the generated template.</span></span>

- **`-f|--framework <FRAMEWORK>`**

  <span data-ttu-id="73879-622">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="73879-622">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="73879-623">选项在 .NET Core 2.2 SDK 中不可用。</span><span class="sxs-lookup"><span data-stu-id="73879-623">Option not available in .NET Core 2.2 SDK.</span></span>

  <span data-ttu-id="73879-624">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="73879-624">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="73879-625">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="73879-625">SDK version</span></span> | <span data-ttu-id="73879-626">默认值</span><span class="sxs-lookup"><span data-stu-id="73879-626">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="73879-627">3.1</span><span class="sxs-lookup"><span data-stu-id="73879-627">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="73879-628">3.0</span><span class="sxs-lookup"><span data-stu-id="73879-628">3.0</span></span>         | `netcoreapp3.0` |
  | <span data-ttu-id="73879-629">2.1</span><span class="sxs-lookup"><span data-stu-id="73879-629">2.1</span></span>         | `netcoreapp2.0` |

- **`--no-restore`**

  <span data-ttu-id="73879-630">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="73879-630">Doesn't execute an implicit restore during project creation.</span></span>

- **`--no-https`**

  <span data-ttu-id="73879-631">关闭 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="73879-631">Turns off HTTPS.</span></span>

<span data-ttu-id="73879-632">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-632">\*\*_</span></span>

### <a name="razorclasslib"></a><span data-ttu-id="73879-633">razorclasslib</span><span class="sxs-lookup"><span data-stu-id="73879-633">razorclasslib</span></span>

- <span data-ttu-id="73879-634">_ *`--no-restore`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-634">_ *`--no-restore`*\*</span></span>

  <span data-ttu-id="73879-635">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="73879-635">Doesn't execute an implicit restore during project creation.</span></span>

- **`-s|--support-pages-and-views`**

  <span data-ttu-id="73879-636">除了将组件添加到此库以外，还支持添加传统的 Razor 页面和视图。</span><span class="sxs-lookup"><span data-stu-id="73879-636">Supports adding traditional Razor pages and Views in addition to components to this library.</span></span> <span data-ttu-id="73879-637">自 .NET Core 3.0 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="73879-637">Available since .NET Core 3.0 SDK.</span></span>

<span data-ttu-id="73879-638">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-638">\*\*_</span></span>
  
### <a name="webapi"></a><span data-ttu-id="73879-639">webapi</span><span class="sxs-lookup"><span data-stu-id="73879-639">webapi</span></span>

- <span data-ttu-id="73879-640">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-640">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span></span>

  <span data-ttu-id="73879-641">要使用的身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="73879-641">The type of authentication to use.</span></span> <span data-ttu-id="73879-642">可能的值为：</span><span class="sxs-lookup"><span data-stu-id="73879-642">The possible values are:</span></span>

  - <span data-ttu-id="73879-643">`None` - 不进行身份验证（默认）。</span><span class="sxs-lookup"><span data-stu-id="73879-643">`None` - No authentication (Default).</span></span>
  - <span data-ttu-id="73879-644">`IndividualB2C` - 使用 Azure AD B2C 进行个人身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-644">`IndividualB2C` - Individual authentication with Azure AD B2C.</span></span>
  - <span data-ttu-id="73879-645">`SingleOrg` - 对一个租户进行组织身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-645">`SingleOrg` - Organizational authentication for a single tenant.</span></span>
  - <span data-ttu-id="73879-646">`Windows` - Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-646">`Windows` - Windows authentication.</span></span>

- **`--aad-b2c-instance <INSTANCE>`**

  <span data-ttu-id="73879-647">要连接到的 Azure Active Directory B2C 实例。</span><span class="sxs-lookup"><span data-stu-id="73879-647">The Azure Active Directory B2C instance to connect to.</span></span> <span data-ttu-id="73879-648">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-648">Use with `IndividualB2C` authentication.</span></span> <span data-ttu-id="73879-649">默认值为 `https://login.microsoftonline.com/tfp/`。</span><span class="sxs-lookup"><span data-stu-id="73879-649">The default value is `https://login.microsoftonline.com/tfp/`.</span></span>

- **`-ssp|--susi-policy-id <ID>`**

  <span data-ttu-id="73879-650">此项目的登录和注册策略 ID。</span><span class="sxs-lookup"><span data-stu-id="73879-650">The sign-in and sign-up policy ID for this project.</span></span> <span data-ttu-id="73879-651">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-651">Use with `IndividualB2C` authentication.</span></span>

- **`--aad-instance <INSTANCE>`**

  <span data-ttu-id="73879-652">要连接到的 Azure Active Directory 实例。</span><span class="sxs-lookup"><span data-stu-id="73879-652">The Azure Active Directory instance to connect to.</span></span> <span data-ttu-id="73879-653">与 `SingleOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-653">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="73879-654">默认值为 `https://login.microsoftonline.com/`。</span><span class="sxs-lookup"><span data-stu-id="73879-654">The default value is `https://login.microsoftonline.com/`.</span></span>

- **`--client-id <ID>`**

  <span data-ttu-id="73879-655">此项目的客户端 ID。</span><span class="sxs-lookup"><span data-stu-id="73879-655">The Client ID for this project.</span></span> <span data-ttu-id="73879-656">与 `IndividualB2C` 或 `SingleOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-656">Use with `IndividualB2C` or `SingleOrg` authentication.</span></span> <span data-ttu-id="73879-657">默认值为 `11111111-1111-1111-11111111111111111`。</span><span class="sxs-lookup"><span data-stu-id="73879-657">The default value is `11111111-1111-1111-11111111111111111`.</span></span>

- **`--domain <DOMAIN>`**

  <span data-ttu-id="73879-658">目录租户的域。</span><span class="sxs-lookup"><span data-stu-id="73879-658">The domain for the directory tenant.</span></span> <span data-ttu-id="73879-659">与 `IndividualB2C` 或 `SingleOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-659">Use with `IndividualB2C` or `SingleOrg` authentication.</span></span> <span data-ttu-id="73879-660">默认值为 `qualified.domain.name`。</span><span class="sxs-lookup"><span data-stu-id="73879-660">The default value is `qualified.domain.name`.</span></span>

- **`--tenant-id <ID>`**

  <span data-ttu-id="73879-661">要连接到的目录的 TenantId ID。</span><span class="sxs-lookup"><span data-stu-id="73879-661">The TenantId ID of the directory to connect to.</span></span> <span data-ttu-id="73879-662">与 `SingleOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="73879-662">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="73879-663">默认值为 `22222222-2222-2222-2222-222222222222`。</span><span class="sxs-lookup"><span data-stu-id="73879-663">The default value is `22222222-2222-2222-2222-222222222222`.</span></span>

- **`-r|--org-read-access`**

  <span data-ttu-id="73879-664">允许此应用程序对目录进行读取访问。</span><span class="sxs-lookup"><span data-stu-id="73879-664">Allows this application read-access to the directory.</span></span> <span data-ttu-id="73879-665">仅适用于 `SingleOrg` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-665">Only applies to `SingleOrg` authentication.</span></span>

- **`--exclude-launch-settings`**

  <span data-ttu-id="73879-666">从生成的模板中排除 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="73879-666">Excludes *launchSettings.json* from the generated template.</span></span>

- **`--no-https`**

  <span data-ttu-id="73879-667">关闭 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="73879-667">Turns off HTTPS.</span></span> <span data-ttu-id="73879-668">`app.UseHsts` 和 `app.UseHttpsRedirection` 未添加到 `Startup.Configure` 中。</span><span class="sxs-lookup"><span data-stu-id="73879-668">`app.UseHsts` and `app.UseHttpsRedirection` aren't added to `Startup.Configure`.</span></span> <span data-ttu-id="73879-669">此选项仅适用于 `IndividualB2C` 或 `SingleOrg` 未用于身份验证的情况。</span><span class="sxs-lookup"><span data-stu-id="73879-669">This option only applies if `IndividualB2C` or `SingleOrg` aren't being used for authentication.</span></span>

- **`-uld|--use-local-db`**

  <span data-ttu-id="73879-670">指定应使用 LocalDB，而不使用 SQLite。</span><span class="sxs-lookup"><span data-stu-id="73879-670">Specifies LocalDB should be used instead of SQLite.</span></span> <span data-ttu-id="73879-671">仅适用于 `IndividualB2C` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="73879-671">Only applies to `IndividualB2C` authentication.</span></span>

- **`-f|--framework <FRAMEWORK>`**

  <span data-ttu-id="73879-672">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="73879-672">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="73879-673">选项在 .NET Core 2.2 SDK 中不可用。</span><span class="sxs-lookup"><span data-stu-id="73879-673">Option not available in .NET Core 2.2 SDK.</span></span>

  <span data-ttu-id="73879-674">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="73879-674">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="73879-675">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="73879-675">SDK version</span></span> | <span data-ttu-id="73879-676">默认值</span><span class="sxs-lookup"><span data-stu-id="73879-676">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="73879-677">3.1</span><span class="sxs-lookup"><span data-stu-id="73879-677">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="73879-678">3.0</span><span class="sxs-lookup"><span data-stu-id="73879-678">3.0</span></span>         | `netcoreapp3.0` |
  | <span data-ttu-id="73879-679">2.1</span><span class="sxs-lookup"><span data-stu-id="73879-679">2.1</span></span>         | `netcoreapp2.1` |

- **`--no-restore`**

  <span data-ttu-id="73879-680">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="73879-680">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="73879-681">\*\*_</span><span class="sxs-lookup"><span data-stu-id="73879-681">\*\*_</span></span>

### <a name="globaljson"></a><span data-ttu-id="73879-682">globaljson</span><span class="sxs-lookup"><span data-stu-id="73879-682">globaljson</span></span>

- <span data-ttu-id="73879-683">_ *`--sdk-version <VERSION_NUMBER>`*\*</span><span class="sxs-lookup"><span data-stu-id="73879-683">_ *`--sdk-version <VERSION_NUMBER>`*\*</span></span>

  <span data-ttu-id="73879-684">指定要在 global.json 文件中使用的 .NET Core SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="73879-684">Specifies the version of the .NET Core SDK to use in the *global.json* file.</span></span>

***

## <a name="examples"></a><span data-ttu-id="73879-685">示例</span><span class="sxs-lookup"><span data-stu-id="73879-685">Examples</span></span>

- <span data-ttu-id="73879-686">通过指定模板名称，创建 C# 控制台应用程序项目：</span><span class="sxs-lookup"><span data-stu-id="73879-686">Create a C# console application project by specifying the template name:</span></span>

  ```dotnetcli
  dotnet new "Console Application"
  ```

- <span data-ttu-id="73879-687">在当前目录中创建 F# 控制台应用程序项目：</span><span class="sxs-lookup"><span data-stu-id="73879-687">Create an F# console application project in the current directory:</span></span>

  ```dotnetcli
  dotnet new console -lang "F#"
  ```

- <span data-ttu-id="73879-688">在指定的目录中创建 .NET Standard 类库项目：</span><span class="sxs-lookup"><span data-stu-id="73879-688">Create a .NET Standard class library project in the specified directory:</span></span>

  ```dotnetcli
  dotnet new classlib -lang VB -o MyLibrary
  ```

- <span data-ttu-id="73879-689">在当前目录中新建没有设置身份验证的 ASP.NET Core C# MVC 项目：</span><span class="sxs-lookup"><span data-stu-id="73879-689">Create a new ASP.NET Core C# MVC project in the current directory with no authentication:</span></span>

  ```dotnetcli
  dotnet new mvc -au None
  ```

- <span data-ttu-id="73879-690">创建新的 xUnit 项目：</span><span class="sxs-lookup"><span data-stu-id="73879-690">Create a new xUnit project:</span></span>

  ```dotnetcli
  dotnet new xunit
  ```

- <span data-ttu-id="73879-691">列出可用于单页应用程序 (SPA) 模板的所有模板：</span><span class="sxs-lookup"><span data-stu-id="73879-691">List all templates available for Single Page Application (SPA) templates:</span></span>

  ```dotnetcli
  dotnet new spa -l
  ```

- <span data-ttu-id="73879-692">列出与“we”子字符串匹配的所有模板。</span><span class="sxs-lookup"><span data-stu-id="73879-692">List all templates matching the *we* substring.</span></span> <span data-ttu-id="73879-693">找不到完全匹配，因此子字符串匹配针对短名称和名称列运行。</span><span class="sxs-lookup"><span data-stu-id="73879-693">No exact match is found, so substring matching runs against both the short name and name columns.</span></span>

  ```dotnetcli
  dotnet new we -l
  ```

- <span data-ttu-id="73879-694">尝试调用与 ng 匹配的模板。</span><span class="sxs-lookup"><span data-stu-id="73879-694">Attempt to invoke the template matching *ng*.</span></span> <span data-ttu-id="73879-695">如果无法确定单个匹配项，请列出部分匹配项的模板。</span><span class="sxs-lookup"><span data-stu-id="73879-695">If a single match can't be determined, list the templates that are partial matches.</span></span>

  ```dotnetcli
  dotnet new ng
  ```

- <span data-ttu-id="73879-696">安装 ASP.NET Core 的 SPA 模板 2.0 版：</span><span class="sxs-lookup"><span data-stu-id="73879-696">Install version 2.0 of the SPA templates for ASP.NET Core:</span></span>

  ```dotnetcli
  dotnet new -i Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0
  ```

- <span data-ttu-id="73879-697">列出已安装的模板及其详细信息，包括如何卸载它们：</span><span class="sxs-lookup"><span data-stu-id="73879-697">List the installed templates and details about them, including how to uninstall them:</span></span>

  ```dotnetcli
  dotnet new -u
  ```

- <span data-ttu-id="73879-698">在当前目录中创建 global.json，将 SDK 版本设置为 3.1.101：</span><span class="sxs-lookup"><span data-stu-id="73879-698">Create a *global.json* in the current directory setting the SDK version to 3.1.101:</span></span>

  ```dotnetcli
  dotnet new globaljson --sdk-version 3.1.101
  ```

## <a name="see-also"></a><span data-ttu-id="73879-699">请参阅</span><span class="sxs-lookup"><span data-stu-id="73879-699">See also</span></span>

- [<span data-ttu-id="73879-700">dotnet new 自定义模板</span><span class="sxs-lookup"><span data-stu-id="73879-700">Custom templates for dotnet new</span></span>](custom-templates.md)
- [<span data-ttu-id="73879-701">创建 dotnet new 自定义模板</span><span class="sxs-lookup"><span data-stu-id="73879-701">Create a custom template for dotnet new</span></span>](../tutorials/cli-templates-create-item-template.md)
- [<span data-ttu-id="73879-702">dotnet/dotnet-template-samples GitHub 存储库</span><span class="sxs-lookup"><span data-stu-id="73879-702">dotnet/dotnet-template-samples GitHub repo</span></span>](https://github.com/dotnet/dotnet-template-samples)
- [<span data-ttu-id="73879-703">dotnet new 可用模板</span><span class="sxs-lookup"><span data-stu-id="73879-703">Available templates for dotnet new</span></span>](https://github.com/dotnet/templating/wiki/Available-templates-for-dotnet-new)
