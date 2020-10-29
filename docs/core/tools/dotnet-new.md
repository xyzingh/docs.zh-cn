---
title: dotnet new 命令
description: dotnet new 命令可根据指定模板新建 .NET Core 项目。
no-loc:
- ':::no-loc(Blazor):::'
- ':::no-loc(WebAssembly):::'
ms.date: 09/01/2020
ms.openlocfilehash: 4a4c8e2806fee663b5f6aa255a6f24250a072a85
ms.sourcegitcommit: 532b03d5bbab764d63356193b04cd2281bc01239
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2020
ms.locfileid: "92526612"
---
# <a name="dotnet-new"></a><span data-ttu-id="1cb02-103">dotnet new</span><span class="sxs-lookup"><span data-stu-id="1cb02-103">dotnet new</span></span>

<span data-ttu-id="1cb02-104">本文适用于： ✔️ .NET Core 2.0 SDK 及更高版本</span><span class="sxs-lookup"><span data-stu-id="1cb02-104">**This article applies to:** ✔️ .NET Core 2.0 SDK and later versions</span></span>

## <a name="name"></a><span data-ttu-id="1cb02-105">“属性”</span><span class="sxs-lookup"><span data-stu-id="1cb02-105">Name</span></span>

<span data-ttu-id="1cb02-106">`dotnet new` - 根据指定的模板，创建新的项目、配置文件或解决方案。</span><span class="sxs-lookup"><span data-stu-id="1cb02-106">`dotnet new` - Creates a new project, configuration file, or solution based on the specified template.</span></span>

## <a name="synopsis"></a><span data-ttu-id="1cb02-107">摘要</span><span class="sxs-lookup"><span data-stu-id="1cb02-107">Synopsis</span></span>

```dotnetcli
dotnet new <TEMPLATE> [--dry-run] [--force] [-i|--install {PATH|NUGET_ID}]
    [-lang|--language {"C#"|"F#"|VB}] [-n|--name <OUTPUT_NAME>]
    [--nuget-source <SOURCE>] [-o|--output <OUTPUT_DIRECTORY>]
    [-u|--uninstall] [--update-apply] [--update-check] [Template options]

dotnet new <TEMPLATE> [-l|--list] [--type <TYPE>]

dotnet new -h|--help
```

## <a name="description"></a><span data-ttu-id="1cb02-108">描述</span><span class="sxs-lookup"><span data-stu-id="1cb02-108">Description</span></span>

<span data-ttu-id="1cb02-109">`dotnet new` 命令基于模板创建 .NET Core 项目或其他项目。</span><span class="sxs-lookup"><span data-stu-id="1cb02-109">The `dotnet new` command creates a .NET Core project or other artifacts based on a template.</span></span>

<span data-ttu-id="1cb02-110">命令调用[模板引擎](https://github.com/dotnet/templating)，以根据指定的模板和选项在磁盘上创建项目。</span><span class="sxs-lookup"><span data-stu-id="1cb02-110">The command calls the [template engine](https://github.com/dotnet/templating) to create the artifacts on disk based on the specified template and options.</span></span>

### <a name="implicit-restore"></a><span data-ttu-id="1cb02-111">隐式还原</span><span class="sxs-lookup"><span data-stu-id="1cb02-111">Implicit restore</span></span>

[!INCLUDE[dotnet restore note](~/includes/dotnet-restore-note.md)]

## <a name="arguments"></a><span data-ttu-id="1cb02-112">自变量</span><span class="sxs-lookup"><span data-stu-id="1cb02-112">Arguments</span></span>

- **`TEMPLATE`**

  <span data-ttu-id="1cb02-113">调用命令时要实例化的模板。</span><span class="sxs-lookup"><span data-stu-id="1cb02-113">The template to instantiate when the command is invoked.</span></span> <span data-ttu-id="1cb02-114">每个模板可能具有可传递的特定选项。</span><span class="sxs-lookup"><span data-stu-id="1cb02-114">Each template might have specific options you can pass.</span></span> <span data-ttu-id="1cb02-115">有关详细信息，请参阅[模板选项](#template-options)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-115">For more information, see [Template options](#template-options).</span></span>

  <span data-ttu-id="1cb02-116">可以运行 `dotnet new --list` 或 `dotnet new -l` 以查看所有已安装模板的列表。</span><span class="sxs-lookup"><span data-stu-id="1cb02-116">You can run `dotnet new --list` or `dotnet new -l` to see a list of all installed templates.</span></span> <span data-ttu-id="1cb02-117">如果 `TEMPLATE` 值与返回表中的“模板”或“短名称”列中的文本不完全匹配，则会对这两列执行 substring 匹配。</span><span class="sxs-lookup"><span data-stu-id="1cb02-117">If the `TEMPLATE` value isn't an exact match on text in the **Templates** or **Short Name** column from the returned table, a substring match is performed on those two columns.</span></span>

  <span data-ttu-id="1cb02-118">从 .NET Core 3.0 SDK 开始，当你在以下情况下调用 `dotnet new` 命令时，CLI 将在 NuGet.org 中搜索模板：</span><span class="sxs-lookup"><span data-stu-id="1cb02-118">Starting with .NET Core 3.0 SDK, the CLI searches for templates in NuGet.org when you invoke the `dotnet new` command in the following conditions:</span></span>

  - <span data-ttu-id="1cb02-119">如果在调用 `dotnet new` 时 CLI 找不到模板匹配项，即使是部分匹配也不行。</span><span class="sxs-lookup"><span data-stu-id="1cb02-119">If the CLI can't find a template match when invoking `dotnet new`, not even partial.</span></span>
  - <span data-ttu-id="1cb02-120">如果有较新版本的模板可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-120">If there's a newer version of the template available.</span></span> <span data-ttu-id="1cb02-121">在这种情况下，将创建项目或工件，但 CLI 会就模板的更新版本发出警告。</span><span class="sxs-lookup"><span data-stu-id="1cb02-121">In this case, the project or artifact is created but the CLI warns you about an updated version of the template.</span></span>

  <span data-ttu-id="1cb02-122">下表显示了随 .NET Core SDK 一起预安装的模板。</span><span class="sxs-lookup"><span data-stu-id="1cb02-122">The following table shows the templates that come pre-installed with the .NET Core SDK.</span></span> <span data-ttu-id="1cb02-123">模板的默认语言显示在括号内。</span><span class="sxs-lookup"><span data-stu-id="1cb02-123">The default language for the template is shown inside the brackets.</span></span> <span data-ttu-id="1cb02-124">单击短名称链接可查看特定的模板选项。</span><span class="sxs-lookup"><span data-stu-id="1cb02-124">Click on the short name link to see the specific template options.</span></span>

| <span data-ttu-id="1cb02-125">模板</span><span class="sxs-lookup"><span data-stu-id="1cb02-125">Templates</span></span>                                    | <span data-ttu-id="1cb02-126">短名称</span><span class="sxs-lookup"><span data-stu-id="1cb02-126">Short name</span></span>                      | <span data-ttu-id="1cb02-127">语言</span><span class="sxs-lookup"><span data-stu-id="1cb02-127">Language</span></span>     | <span data-ttu-id="1cb02-128">Tags</span><span class="sxs-lookup"><span data-stu-id="1cb02-128">Tags</span></span>                                  | <span data-ttu-id="1cb02-129">已引入</span><span class="sxs-lookup"><span data-stu-id="1cb02-129">Introduced</span></span> |
|----------------------------------------------|---------------------------------|--------------|---------------------------------------|------------|
| <span data-ttu-id="1cb02-130">控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="1cb02-130">Console Application</span></span>                          | [<span data-ttu-id="1cb02-131">控制台</span><span class="sxs-lookup"><span data-stu-id="1cb02-131">console</span></span>](#console)             | <span data-ttu-id="1cb02-132">[C#]、F#、VB</span><span class="sxs-lookup"><span data-stu-id="1cb02-132">[C#], F#, VB</span></span> | <span data-ttu-id="1cb02-133">常用/控制台</span><span class="sxs-lookup"><span data-stu-id="1cb02-133">Common/Console</span></span>                        | <span data-ttu-id="1cb02-134">1.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-134">1.0</span></span>        |
| <span data-ttu-id="1cb02-135">类库</span><span class="sxs-lookup"><span data-stu-id="1cb02-135">Class library</span></span>                                | [<span data-ttu-id="1cb02-136">classlib</span><span class="sxs-lookup"><span data-stu-id="1cb02-136">classlib</span></span>](#classlib)           | <span data-ttu-id="1cb02-137">[C#]、F#、VB</span><span class="sxs-lookup"><span data-stu-id="1cb02-137">[C#], F#, VB</span></span> | <span data-ttu-id="1cb02-138">常用/库</span><span class="sxs-lookup"><span data-stu-id="1cb02-138">Common/Library</span></span>                        | <span data-ttu-id="1cb02-139">1.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-139">1.0</span></span>        |
| <span data-ttu-id="1cb02-140">WPF 应用程序</span><span class="sxs-lookup"><span data-stu-id="1cb02-140">WPF Application</span></span>                              | [<span data-ttu-id="1cb02-141">wpf</span><span class="sxs-lookup"><span data-stu-id="1cb02-141">wpf</span></span>](#wpf)                     | <span data-ttu-id="1cb02-142">[C#]、VB</span><span class="sxs-lookup"><span data-stu-id="1cb02-142">[C#], VB</span></span>     | <span data-ttu-id="1cb02-143">常用/WPF</span><span class="sxs-lookup"><span data-stu-id="1cb02-143">Common/WPF</span></span>                            | <span data-ttu-id="1cb02-144">3.0（对于 VB，则为 5.0）</span><span class="sxs-lookup"><span data-stu-id="1cb02-144">3.0 (5.0 for VB)</span></span>|
| <span data-ttu-id="1cb02-145">WPF 类库</span><span class="sxs-lookup"><span data-stu-id="1cb02-145">WPF Class library</span></span>                            | [<span data-ttu-id="1cb02-146">wpflib</span><span class="sxs-lookup"><span data-stu-id="1cb02-146">wpflib</span></span>](#wpf)                  | <span data-ttu-id="1cb02-147">[C#]、VB</span><span class="sxs-lookup"><span data-stu-id="1cb02-147">[C#], VB</span></span>     | <span data-ttu-id="1cb02-148">常用/WPF</span><span class="sxs-lookup"><span data-stu-id="1cb02-148">Common/WPF</span></span>                            | <span data-ttu-id="1cb02-149">3.0（对于 VB，则为 5.0）</span><span class="sxs-lookup"><span data-stu-id="1cb02-149">3.0 (5.0 for VB)</span></span>|
| <span data-ttu-id="1cb02-150">WPF 自定义控件库</span><span class="sxs-lookup"><span data-stu-id="1cb02-150">WPF Custom Control Library</span></span>                   | [<span data-ttu-id="1cb02-151">wpfcustomcontrollib</span><span class="sxs-lookup"><span data-stu-id="1cb02-151">wpfcustomcontrollib</span></span>](#wpf)     | <span data-ttu-id="1cb02-152">[C#]、VB</span><span class="sxs-lookup"><span data-stu-id="1cb02-152">[C#], VB</span></span>     | <span data-ttu-id="1cb02-153">常用/WPF</span><span class="sxs-lookup"><span data-stu-id="1cb02-153">Common/WPF</span></span>                            | <span data-ttu-id="1cb02-154">3.0（对于 VB，则为 5.0）</span><span class="sxs-lookup"><span data-stu-id="1cb02-154">3.0 (5.0 for VB)</span></span>|
| <span data-ttu-id="1cb02-155">WPF 用户控件库</span><span class="sxs-lookup"><span data-stu-id="1cb02-155">WPF User Control Library</span></span>                     | [<span data-ttu-id="1cb02-156">wpfusercontrollib</span><span class="sxs-lookup"><span data-stu-id="1cb02-156">wpfusercontrollib</span></span>](#wpf)       | <span data-ttu-id="1cb02-157">[C#]、VB</span><span class="sxs-lookup"><span data-stu-id="1cb02-157">[C#], VB</span></span>     | <span data-ttu-id="1cb02-158">常用/WPF</span><span class="sxs-lookup"><span data-stu-id="1cb02-158">Common/WPF</span></span>                            | <span data-ttu-id="1cb02-159">3.0（对于 VB，则为 5.0）</span><span class="sxs-lookup"><span data-stu-id="1cb02-159">3.0 (5.0 for VB)</span></span>|
| <span data-ttu-id="1cb02-160">Windows 窗体 (WinForms) 应用程序</span><span class="sxs-lookup"><span data-stu-id="1cb02-160">Windows Forms (WinForms) Application</span></span>         | [<span data-ttu-id="1cb02-161">winforms</span><span class="sxs-lookup"><span data-stu-id="1cb02-161">winforms</span></span>](#winforms)           | <span data-ttu-id="1cb02-162">[C#]、VB</span><span class="sxs-lookup"><span data-stu-id="1cb02-162">[C#], VB</span></span>     | <span data-ttu-id="1cb02-163">常用/WinForms</span><span class="sxs-lookup"><span data-stu-id="1cb02-163">Common/WinForms</span></span>                       | <span data-ttu-id="1cb02-164">3.0（对于 VB，则为 5.0）</span><span class="sxs-lookup"><span data-stu-id="1cb02-164">3.0 (5.0 for VB)</span></span>|
| <span data-ttu-id="1cb02-165">Windows 窗体 (WinForms) 类库</span><span class="sxs-lookup"><span data-stu-id="1cb02-165">Windows Forms (WinForms) Class library</span></span>       | [<span data-ttu-id="1cb02-166">winformslib</span><span class="sxs-lookup"><span data-stu-id="1cb02-166">winformslib</span></span>](#winforms)        | <span data-ttu-id="1cb02-167">[C#]、VB</span><span class="sxs-lookup"><span data-stu-id="1cb02-167">[C#], VB</span></span>     | <span data-ttu-id="1cb02-168">常用/WinForms</span><span class="sxs-lookup"><span data-stu-id="1cb02-168">Common/WinForms</span></span>                       | <span data-ttu-id="1cb02-169">3.0（对于 VB，则为 5.0）</span><span class="sxs-lookup"><span data-stu-id="1cb02-169">3.0 (5.0 for VB)</span></span>|
| <span data-ttu-id="1cb02-170">Worker Service</span><span class="sxs-lookup"><span data-stu-id="1cb02-170">Worker Service</span></span>                               | [<span data-ttu-id="1cb02-171">worker</span><span class="sxs-lookup"><span data-stu-id="1cb02-171">worker</span></span>](#web-others)           | <span data-ttu-id="1cb02-172">[C#]</span><span class="sxs-lookup"><span data-stu-id="1cb02-172">[C#]</span></span>         | <span data-ttu-id="1cb02-173">常用/Worker/Web</span><span class="sxs-lookup"><span data-stu-id="1cb02-173">Common/Worker/Web</span></span>                     | <span data-ttu-id="1cb02-174">3.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-174">3.0</span></span>        |
| <span data-ttu-id="1cb02-175">单元测试项目</span><span class="sxs-lookup"><span data-stu-id="1cb02-175">Unit Test Project</span></span>                            | [<span data-ttu-id="1cb02-176">mstest</span><span class="sxs-lookup"><span data-stu-id="1cb02-176">mstest</span></span>](#test)                 | <span data-ttu-id="1cb02-177">[C#]、F#、VB</span><span class="sxs-lookup"><span data-stu-id="1cb02-177">[C#], F#, VB</span></span> | <span data-ttu-id="1cb02-178">测试/MSTest</span><span class="sxs-lookup"><span data-stu-id="1cb02-178">Test/MSTest</span></span>                           | <span data-ttu-id="1cb02-179">1.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-179">1.0</span></span>        |
| <span data-ttu-id="1cb02-180">NUnit 3 测试项目</span><span class="sxs-lookup"><span data-stu-id="1cb02-180">NUnit 3 Test Project</span></span>                         | [<span data-ttu-id="1cb02-181">nunit</span><span class="sxs-lookup"><span data-stu-id="1cb02-181">nunit</span></span>](#nunit)                 | <span data-ttu-id="1cb02-182">[C#]、F#、VB</span><span class="sxs-lookup"><span data-stu-id="1cb02-182">[C#], F#, VB</span></span> | <span data-ttu-id="1cb02-183">测试/NUnit</span><span class="sxs-lookup"><span data-stu-id="1cb02-183">Test/NUnit</span></span>                            | <span data-ttu-id="1cb02-184">2.1.400</span><span class="sxs-lookup"><span data-stu-id="1cb02-184">2.1.400</span></span>    |
| <span data-ttu-id="1cb02-185">NUnit 3 测试项</span><span class="sxs-lookup"><span data-stu-id="1cb02-185">NUnit 3 Test Item</span></span>                            | `nunit-test`                    | <span data-ttu-id="1cb02-186">[C#]、F#、VB</span><span class="sxs-lookup"><span data-stu-id="1cb02-186">[C#], F#, VB</span></span> | <span data-ttu-id="1cb02-187">测试/NUnit</span><span class="sxs-lookup"><span data-stu-id="1cb02-187">Test/NUnit</span></span>                            | <span data-ttu-id="1cb02-188">2.2</span><span class="sxs-lookup"><span data-stu-id="1cb02-188">2.2</span></span>        |
| <span data-ttu-id="1cb02-189">xUnit 测试项目</span><span class="sxs-lookup"><span data-stu-id="1cb02-189">xUnit Test Project</span></span>                           | [<span data-ttu-id="1cb02-190">xunit</span><span class="sxs-lookup"><span data-stu-id="1cb02-190">xunit</span></span>](#test)                  | <span data-ttu-id="1cb02-191">[C#]、F#、VB</span><span class="sxs-lookup"><span data-stu-id="1cb02-191">[C#], F#, VB</span></span> | <span data-ttu-id="1cb02-192">测试/xUnit</span><span class="sxs-lookup"><span data-stu-id="1cb02-192">Test/xUnit</span></span>                            | <span data-ttu-id="1cb02-193">1.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-193">1.0</span></span>        |
| <span data-ttu-id="1cb02-194">Razor 组件</span><span class="sxs-lookup"><span data-stu-id="1cb02-194">Razor Component</span></span>                              | `razorcomponent`                | <span data-ttu-id="1cb02-195">[C#]</span><span class="sxs-lookup"><span data-stu-id="1cb02-195">[C#]</span></span>         | <span data-ttu-id="1cb02-196">Web/ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1cb02-196">Web/ASP.NET</span></span>                           | <span data-ttu-id="1cb02-197">3.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-197">3.0</span></span>        |
| <span data-ttu-id="1cb02-198">Razor 页</span><span class="sxs-lookup"><span data-stu-id="1cb02-198">Razor Page</span></span>                                   | [<span data-ttu-id="1cb02-199">page</span><span class="sxs-lookup"><span data-stu-id="1cb02-199">page</span></span>](#page)                   | <span data-ttu-id="1cb02-200">[C#]</span><span class="sxs-lookup"><span data-stu-id="1cb02-200">[C#]</span></span>         | <span data-ttu-id="1cb02-201">Web/ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1cb02-201">Web/ASP.NET</span></span>                           | <span data-ttu-id="1cb02-202">2.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-202">2.0</span></span>        |
| <span data-ttu-id="1cb02-203">MVC ViewImports</span><span class="sxs-lookup"><span data-stu-id="1cb02-203">MVC ViewImports</span></span>                              | [<span data-ttu-id="1cb02-204">viewimports</span><span class="sxs-lookup"><span data-stu-id="1cb02-204">viewimports</span></span>](#namespace)       | <span data-ttu-id="1cb02-205">[C#]</span><span class="sxs-lookup"><span data-stu-id="1cb02-205">[C#]</span></span>         | <span data-ttu-id="1cb02-206">Web/ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1cb02-206">Web/ASP.NET</span></span>                           | <span data-ttu-id="1cb02-207">2.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-207">2.0</span></span>        |
| <span data-ttu-id="1cb02-208">MVC ViewStart</span><span class="sxs-lookup"><span data-stu-id="1cb02-208">MVC ViewStart</span></span>                                | `viewstart`                     | <span data-ttu-id="1cb02-209">[C#]</span><span class="sxs-lookup"><span data-stu-id="1cb02-209">[C#]</span></span>         | <span data-ttu-id="1cb02-210">Web/ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1cb02-210">Web/ASP.NET</span></span>                           | <span data-ttu-id="1cb02-211">2.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-211">2.0</span></span>        |
| <span data-ttu-id="1cb02-212">:::no-loc(Blazor)::: 服务器应用</span><span class="sxs-lookup"><span data-stu-id="1cb02-212">:::no-loc(Blazor)::: Server App</span></span>                            | [<span data-ttu-id="1cb02-213">blazorserver</span><span class="sxs-lookup"><span data-stu-id="1cb02-213">blazorserver</span></span>](#blazorserver)   | <span data-ttu-id="1cb02-214">[C#]</span><span class="sxs-lookup"><span data-stu-id="1cb02-214">[C#]</span></span>         | <span data-ttu-id="1cb02-215">Web/:::no-loc(Blazor):::</span><span class="sxs-lookup"><span data-stu-id="1cb02-215">Web/:::no-loc(Blazor):::</span></span>                            | <span data-ttu-id="1cb02-216">3.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-216">3.0</span></span>        |
| <span data-ttu-id="1cb02-217">:::no-loc(Blazor)::: :::no-loc(WebAssembly)::: 应用</span><span class="sxs-lookup"><span data-stu-id="1cb02-217">:::no-loc(Blazor)::: :::no-loc(WebAssembly)::: App</span></span>                       | `blazorwasm`                    | <span data-ttu-id="1cb02-218">[C#]</span><span class="sxs-lookup"><span data-stu-id="1cb02-218">[C#]</span></span>         | <span data-ttu-id="1cb02-219">Web/:::no-loc(Blazor):::/:::no-loc(WebAssembly):::</span><span class="sxs-lookup"><span data-stu-id="1cb02-219">Web/:::no-loc(Blazor):::/:::no-loc(WebAssembly):::</span></span>                | <span data-ttu-id="1cb02-220">3.1.300</span><span class="sxs-lookup"><span data-stu-id="1cb02-220">3.1.300</span></span>    |
| <span data-ttu-id="1cb02-221">ASP.NET Core 空</span><span class="sxs-lookup"><span data-stu-id="1cb02-221">ASP.NET Core Empty</span></span>                           | [<span data-ttu-id="1cb02-222">web</span><span class="sxs-lookup"><span data-stu-id="1cb02-222">web</span></span>](#web)                     | <span data-ttu-id="1cb02-223">[C#]，F#</span><span class="sxs-lookup"><span data-stu-id="1cb02-223">[C#], F#</span></span>     | <span data-ttu-id="1cb02-224">Web/空</span><span class="sxs-lookup"><span data-stu-id="1cb02-224">Web/Empty</span></span>                             | <span data-ttu-id="1cb02-225">1.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-225">1.0</span></span>        |
| <span data-ttu-id="1cb02-226">ASP.NET Core Web 应用程序 (Model-View-Controller)</span><span class="sxs-lookup"><span data-stu-id="1cb02-226">ASP.NET Core Web App (Model-View-Controller)</span></span> | [<span data-ttu-id="1cb02-227">mvc</span><span class="sxs-lookup"><span data-stu-id="1cb02-227">mvc</span></span>](#web-options)             | <span data-ttu-id="1cb02-228">[C#]，F#</span><span class="sxs-lookup"><span data-stu-id="1cb02-228">[C#], F#</span></span>     | <span data-ttu-id="1cb02-229">Web/MVC</span><span class="sxs-lookup"><span data-stu-id="1cb02-229">Web/MVC</span></span>                               | <span data-ttu-id="1cb02-230">1.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-230">1.0</span></span>        |
| <span data-ttu-id="1cb02-231">ASP.NET Core Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="1cb02-231">ASP.NET Core Web App</span></span>                         | [<span data-ttu-id="1cb02-232">webapp、razor</span><span class="sxs-lookup"><span data-stu-id="1cb02-232">webapp, razor</span></span>](#web-options)   | <span data-ttu-id="1cb02-233">[C#]</span><span class="sxs-lookup"><span data-stu-id="1cb02-233">[C#]</span></span>         | <span data-ttu-id="1cb02-234">Web/MVC/Razor Pages</span><span class="sxs-lookup"><span data-stu-id="1cb02-234">Web/MVC/Razor Pages</span></span>                   | <span data-ttu-id="1cb02-235">2.2、2.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-235">2.2, 2.0</span></span>   |
| <span data-ttu-id="1cb02-236">含 Angular 的 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="1cb02-236">ASP.NET Core with Angular</span></span>                    | [<span data-ttu-id="1cb02-237">angular</span><span class="sxs-lookup"><span data-stu-id="1cb02-237">angular</span></span>](#spa)                 | <span data-ttu-id="1cb02-238">[C#]</span><span class="sxs-lookup"><span data-stu-id="1cb02-238">[C#]</span></span>         | <span data-ttu-id="1cb02-239">Web/MVC/SPA</span><span class="sxs-lookup"><span data-stu-id="1cb02-239">Web/MVC/SPA</span></span>                           | <span data-ttu-id="1cb02-240">2.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-240">2.0</span></span>        |
| <span data-ttu-id="1cb02-241">含 React.js 的 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="1cb02-241">ASP.NET Core with React.js</span></span>                   | [<span data-ttu-id="1cb02-242">react</span><span class="sxs-lookup"><span data-stu-id="1cb02-242">react</span></span>](#spa)                   | <span data-ttu-id="1cb02-243">[C#]</span><span class="sxs-lookup"><span data-stu-id="1cb02-243">[C#]</span></span>         | <span data-ttu-id="1cb02-244">Web/MVC/SPA</span><span class="sxs-lookup"><span data-stu-id="1cb02-244">Web/MVC/SPA</span></span>                           | <span data-ttu-id="1cb02-245">2.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-245">2.0</span></span>        |
| <span data-ttu-id="1cb02-246">含 React.js 和 Redux 的 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="1cb02-246">ASP.NET Core with React.js and Redux</span></span>         | [<span data-ttu-id="1cb02-247">reactredux</span><span class="sxs-lookup"><span data-stu-id="1cb02-247">reactredux</span></span>](#reactredux)       | <span data-ttu-id="1cb02-248">[C#]</span><span class="sxs-lookup"><span data-stu-id="1cb02-248">[C#]</span></span>         | <span data-ttu-id="1cb02-249">Web/MVC/SPA</span><span class="sxs-lookup"><span data-stu-id="1cb02-249">Web/MVC/SPA</span></span>                           | <span data-ttu-id="1cb02-250">2.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-250">2.0</span></span>        |
| <span data-ttu-id="1cb02-251">Razor 类库</span><span class="sxs-lookup"><span data-stu-id="1cb02-251">Razor Class Library</span></span>                          | [<span data-ttu-id="1cb02-252">razorclasslib</span><span class="sxs-lookup"><span data-stu-id="1cb02-252">razorclasslib</span></span>](#razorclasslib) | <span data-ttu-id="1cb02-253">[C#]</span><span class="sxs-lookup"><span data-stu-id="1cb02-253">[C#]</span></span>         | <span data-ttu-id="1cb02-254">Web/Razor/库/Razor 类库</span><span class="sxs-lookup"><span data-stu-id="1cb02-254">Web/Razor/Library/Razor Class Library</span></span> | <span data-ttu-id="1cb02-255">2.1</span><span class="sxs-lookup"><span data-stu-id="1cb02-255">2.1</span></span>        |
| <span data-ttu-id="1cb02-256">ASP.NET Core Web API</span><span class="sxs-lookup"><span data-stu-id="1cb02-256">ASP.NET Core Web API</span></span>                         | [<span data-ttu-id="1cb02-257">webapi</span><span class="sxs-lookup"><span data-stu-id="1cb02-257">webapi</span></span>](#webapi)               | <span data-ttu-id="1cb02-258">[C#]，F#</span><span class="sxs-lookup"><span data-stu-id="1cb02-258">[C#], F#</span></span>     | <span data-ttu-id="1cb02-259">Web/WebAPI</span><span class="sxs-lookup"><span data-stu-id="1cb02-259">Web/WebAPI</span></span>                            | <span data-ttu-id="1cb02-260">1.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-260">1.0</span></span>        |
| <span data-ttu-id="1cb02-261">ASP.NET Core gRPC 服务</span><span class="sxs-lookup"><span data-stu-id="1cb02-261">ASP.NET Core gRPC Service</span></span>                    | [<span data-ttu-id="1cb02-262">grpc</span><span class="sxs-lookup"><span data-stu-id="1cb02-262">grpc</span></span>](#web-others)             | <span data-ttu-id="1cb02-263">[C#]</span><span class="sxs-lookup"><span data-stu-id="1cb02-263">[C#]</span></span>         | <span data-ttu-id="1cb02-264">Web/gRPC</span><span class="sxs-lookup"><span data-stu-id="1cb02-264">Web/gRPC</span></span>                              | <span data-ttu-id="1cb02-265">3.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-265">3.0</span></span>        |
| <span data-ttu-id="1cb02-266">dotnet gitignore 文件</span><span class="sxs-lookup"><span data-stu-id="1cb02-266">dotnet gitignore file</span></span>                        | `gitignore`                     |              | <span data-ttu-id="1cb02-267">配置</span><span class="sxs-lookup"><span data-stu-id="1cb02-267">Config</span></span>                                | <span data-ttu-id="1cb02-268">3.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-268">3.0</span></span>        |
| <span data-ttu-id="1cb02-269">global.json 文件</span><span class="sxs-lookup"><span data-stu-id="1cb02-269">global.json file</span></span>                             | [<span data-ttu-id="1cb02-270">globaljson</span><span class="sxs-lookup"><span data-stu-id="1cb02-270">globaljson</span></span>](#globaljson)       |              | <span data-ttu-id="1cb02-271">配置</span><span class="sxs-lookup"><span data-stu-id="1cb02-271">Config</span></span>                                | <span data-ttu-id="1cb02-272">2.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-272">2.0</span></span>        |
| <span data-ttu-id="1cb02-273">NuGet 配置</span><span class="sxs-lookup"><span data-stu-id="1cb02-273">NuGet Config</span></span>                                 | `nugetconfig`                   |              | <span data-ttu-id="1cb02-274">配置</span><span class="sxs-lookup"><span data-stu-id="1cb02-274">Config</span></span>                                | <span data-ttu-id="1cb02-275">1.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-275">1.0</span></span>        |
| <span data-ttu-id="1cb02-276">Dotnet 本地工具清单文件</span><span class="sxs-lookup"><span data-stu-id="1cb02-276">Dotnet local tool manifest file</span></span>              | `tool-manifest`                 |              | <span data-ttu-id="1cb02-277">配置</span><span class="sxs-lookup"><span data-stu-id="1cb02-277">Config</span></span>                                | <span data-ttu-id="1cb02-278">3.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-278">3.0</span></span>        |
| <span data-ttu-id="1cb02-279">Web 配置</span><span class="sxs-lookup"><span data-stu-id="1cb02-279">Web Config</span></span>                                   | `webconfig`                     |              | <span data-ttu-id="1cb02-280">配置</span><span class="sxs-lookup"><span data-stu-id="1cb02-280">Config</span></span>                                | <span data-ttu-id="1cb02-281">1.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-281">1.0</span></span>        |
| <span data-ttu-id="1cb02-282">解决方案文件</span><span class="sxs-lookup"><span data-stu-id="1cb02-282">Solution File</span></span>                                | `sln`                           |              | <span data-ttu-id="1cb02-283">解决方案</span><span class="sxs-lookup"><span data-stu-id="1cb02-283">Solution</span></span>                              | <span data-ttu-id="1cb02-284">1.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-284">1.0</span></span>        |
| <span data-ttu-id="1cb02-285">协议缓冲区文件</span><span class="sxs-lookup"><span data-stu-id="1cb02-285">Protocol Buffer File</span></span>                         | [<span data-ttu-id="1cb02-286">proto</span><span class="sxs-lookup"><span data-stu-id="1cb02-286">proto</span></span>](#namespace)             |              | <span data-ttu-id="1cb02-287">Web/gRPC</span><span class="sxs-lookup"><span data-stu-id="1cb02-287">Web/gRPC</span></span>                              | <span data-ttu-id="1cb02-288">3.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-288">3.0</span></span>        |

## <a name="options"></a><span data-ttu-id="1cb02-289">选项</span><span class="sxs-lookup"><span data-stu-id="1cb02-289">Options</span></span>

- **`--dry-run`**

  <span data-ttu-id="1cb02-290">显示有关以下内容的摘要：给定命令运行导致模板创建时发生的情况。</span><span class="sxs-lookup"><span data-stu-id="1cb02-290">Displays a summary of what would happen if the given command were run if it would result in a template creation.</span></span> <span data-ttu-id="1cb02-291">自 .NET Core 2.2 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-291">Available since .NET Core 2.2 SDK.</span></span>

- **`--force`**

  <span data-ttu-id="1cb02-292">强制生成内容，即使会更改现有文件，也不例外。</span><span class="sxs-lookup"><span data-stu-id="1cb02-292">Forces content to be generated even if it would change existing files.</span></span> <span data-ttu-id="1cb02-293">当选择的模板将覆盖输出目录中的现有文件时，需要执行此操作。</span><span class="sxs-lookup"><span data-stu-id="1cb02-293">This is required when the template chosen would override existing files in the output directory.</span></span>

- **`-h|--help`**

  <span data-ttu-id="1cb02-294">打印命令帮助。</span><span class="sxs-lookup"><span data-stu-id="1cb02-294">Prints out help for the command.</span></span> <span data-ttu-id="1cb02-295">可针对 `dotnet new` 命令本身或任何模板调用它。</span><span class="sxs-lookup"><span data-stu-id="1cb02-295">It can be invoked for the `dotnet new` command itself or for any template.</span></span> <span data-ttu-id="1cb02-296">例如 `dotnet new mvc --help`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-296">For example, `dotnet new mvc --help`.</span></span>

- **`-i|--install <PATH|NUGET_ID>`**

  <span data-ttu-id="1cb02-297">从提供的 `PATH` 或 `NUGET_ID` 安装模板包。</span><span class="sxs-lookup"><span data-stu-id="1cb02-297">Installs a template pack from the `PATH` or `NUGET_ID` provided.</span></span> <span data-ttu-id="1cb02-298">若要安装模板包的预发布版本，需要以 `<package-name>::<package-version>` 格式指定该版本。</span><span class="sxs-lookup"><span data-stu-id="1cb02-298">If you want to install a prerelease version of a template package, you need to specify the version in the format of `<package-name>::<package-version>`.</span></span> <span data-ttu-id="1cb02-299">默认情况下，`dotnet new` 为该版本传递 \*，它表示最新的稳定包版本。</span><span class="sxs-lookup"><span data-stu-id="1cb02-299">By default, `dotnet new` passes \* for the version, which represents the latest stable package version.</span></span> <span data-ttu-id="1cb02-300">请在[示例](#examples)部分查看示例。</span><span class="sxs-lookup"><span data-stu-id="1cb02-300">See an example in the [Examples](#examples) section.</span></span>
  
  <span data-ttu-id="1cb02-301">如果在运行此命令时已经安装了模板的某个版本，则该模板将更新到指定版本，如果没有指定版本，则将更新到最新的稳定版本。</span><span class="sxs-lookup"><span data-stu-id="1cb02-301">If a version of the template was already installed when you run this command, the template will be updated to the specified version, or to the latest stable version if no version was specified.</span></span>

  <span data-ttu-id="1cb02-302">若要了解如何创建自定义模板，请参阅 [dotnet new 自定义模板](custom-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-302">For information on creating custom templates, see [Custom templates for dotnet new](custom-templates.md).</span></span>

- **`-l|--list`**

  <span data-ttu-id="1cb02-303">列出包含指定名称的模板。</span><span class="sxs-lookup"><span data-stu-id="1cb02-303">Lists templates containing the specified name.</span></span> <span data-ttu-id="1cb02-304">如果未指定名称，则列出所有模板。</span><span class="sxs-lookup"><span data-stu-id="1cb02-304">If no name is specified, lists all templates.</span></span>

- **`-lang|--language {C#|F#|VB}`**

  <span data-ttu-id="1cb02-305">要创建的模板的语言。</span><span class="sxs-lookup"><span data-stu-id="1cb02-305">The language of the template to create.</span></span> <span data-ttu-id="1cb02-306">接受的语言因模板而异（请参阅[参数](#arguments)部分中的默认值）。</span><span class="sxs-lookup"><span data-stu-id="1cb02-306">The language accepted varies by the template (see defaults in the [arguments](#arguments) section).</span></span> <span data-ttu-id="1cb02-307">对于某些模板无效。</span><span class="sxs-lookup"><span data-stu-id="1cb02-307">Not valid for some templates.</span></span>

  > [!NOTE]
  > <span data-ttu-id="1cb02-308">某些 shell 将 `#` 解释为特殊字符。</span><span class="sxs-lookup"><span data-stu-id="1cb02-308">Some shells interpret `#` as a special character.</span></span> <span data-ttu-id="1cb02-309">在这些情况下，请将语言参数值括在引号中。</span><span class="sxs-lookup"><span data-stu-id="1cb02-309">In those cases, enclose the language parameter value in quotes.</span></span> <span data-ttu-id="1cb02-310">例如 `dotnet new console -lang "F#"`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-310">For example, `dotnet new console -lang "F#"`.</span></span>

- **`-n|--name <OUTPUT_NAME>`**

  <span data-ttu-id="1cb02-311">所创建的输出的名称。</span><span class="sxs-lookup"><span data-stu-id="1cb02-311">The name for the created output.</span></span> <span data-ttu-id="1cb02-312">如果未指定名称，使用的是当前目录的名称。</span><span class="sxs-lookup"><span data-stu-id="1cb02-312">If no name is specified, the name of the current directory is used.</span></span>

- **`--nuget-source <SOURCE>`**

  <span data-ttu-id="1cb02-313">指定在安装期间要使用的 NuGet 源。</span><span class="sxs-lookup"><span data-stu-id="1cb02-313">Specifies a NuGet source to use during install.</span></span> <span data-ttu-id="1cb02-314">自 .NET Core 2.1 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-314">Available since .NET Core 2.1 SDK.</span></span>

- **`-o|--output <OUTPUT_DIRECTORY>`**

  <span data-ttu-id="1cb02-315">用于放置生成的输出的位置。</span><span class="sxs-lookup"><span data-stu-id="1cb02-315">Location to place the generated output.</span></span> <span data-ttu-id="1cb02-316">默认为当前目录。</span><span class="sxs-lookup"><span data-stu-id="1cb02-316">The default is the current directory.</span></span>

- **`--type <TYPE>`**

  <span data-ttu-id="1cb02-317">根据可用类型筛选模板。</span><span class="sxs-lookup"><span data-stu-id="1cb02-317">Filters templates based on available types.</span></span> <span data-ttu-id="1cb02-318">预定义的值为 `project` 和 `item`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-318">Predefined values are `project` and `item`.</span></span>

- **`-u|--uninstall [PATH|NUGET_ID]`**

  <span data-ttu-id="1cb02-319">在提供的 `PATH` 或 `NUGET_ID` 中卸载模板包。</span><span class="sxs-lookup"><span data-stu-id="1cb02-319">Uninstalls a template pack at the `PATH` or `NUGET_ID` provided.</span></span> <span data-ttu-id="1cb02-320">如果未指定 `<PATH|NUGET_ID>` 值，将显示所有当前安装的模板包及其关联的模板。</span><span class="sxs-lookup"><span data-stu-id="1cb02-320">When the `<PATH|NUGET_ID>` value isn't specified, all currently installed template packs and their associated templates are displayed.</span></span> <span data-ttu-id="1cb02-321">指定 `NUGET_ID` 时，请勿包含版本号。</span><span class="sxs-lookup"><span data-stu-id="1cb02-321">When specifying `NUGET_ID`, don't include the version number.</span></span>

  <span data-ttu-id="1cb02-322">如果未指定此选项的参数，该命令将列出已安装的模板及其详细信息。</span><span class="sxs-lookup"><span data-stu-id="1cb02-322">If you don't specify a parameter to this option, the command lists the installed templates and details about them.</span></span>

  > [!NOTE]
  > <span data-ttu-id="1cb02-323">若要使用 `PATH` 卸载模板，需要完全限定路径。</span><span class="sxs-lookup"><span data-stu-id="1cb02-323">To uninstall a template using a `PATH`, you need to fully qualify the path.</span></span> <span data-ttu-id="1cb02-324">例如，C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp 有效，但是包含文件夹中的 ./GarciaSoftware.ConsoleTemplate.CSharp 无效 。</span><span class="sxs-lookup"><span data-stu-id="1cb02-324">For example, *C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp* will work, but *./GarciaSoftware.ConsoleTemplate.CSharp* from the containing folder will not.</span></span>
  > <span data-ttu-id="1cb02-325">模板路径中不要包含最后的终止目录斜杠。</span><span class="sxs-lookup"><span data-stu-id="1cb02-325">Don't include a final terminating directory slash on your template path.</span></span>

- **`--update-apply`**

  <span data-ttu-id="1cb02-326">检查是否有可用于当前安装的模板包的更新并安装这些更新。</span><span class="sxs-lookup"><span data-stu-id="1cb02-326">Checks if there are updates available for the template packs that are currently installed and installs them.</span></span> <span data-ttu-id="1cb02-327">自 .NET Core 3.0 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-327">Available since .NET Core 3.0 SDK.</span></span>

- **`--update-check`**

  <span data-ttu-id="1cb02-328">检查是否有可用于当前安装的模板包的更新。</span><span class="sxs-lookup"><span data-stu-id="1cb02-328">Checks if there are updates available for the template packs that are currently installed.</span></span> <span data-ttu-id="1cb02-329">自 .NET Core 3.0 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-329">Available since .NET Core 3.0 SDK.</span></span>

## <a name="template-options"></a><span data-ttu-id="1cb02-330">模板选项</span><span class="sxs-lookup"><span data-stu-id="1cb02-330">Template options</span></span>

<span data-ttu-id="1cb02-331">每个项目模板都可能有附加选项。</span><span class="sxs-lookup"><span data-stu-id="1cb02-331">Each project template may have additional options available.</span></span> <span data-ttu-id="1cb02-332">核心模板有以下附加选项：</span><span class="sxs-lookup"><span data-stu-id="1cb02-332">The core templates have the following additional options:</span></span>

### <a name="console"></a><span data-ttu-id="1cb02-333">控制台</span><span class="sxs-lookup"><span data-stu-id="1cb02-333">console</span></span>

- **`-f|--framework <FRAMEWORK>`**

  <span data-ttu-id="1cb02-334">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-334">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1cb02-335">自 .NET Core 3.0 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-335">Available since .NET Core 3.0 SDK.</span></span>

  <span data-ttu-id="1cb02-336">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="1cb02-336">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="1cb02-337">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="1cb02-337">SDK version</span></span> | <span data-ttu-id="1cb02-338">默认值</span><span class="sxs-lookup"><span data-stu-id="1cb02-338">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="1cb02-339">3.1</span><span class="sxs-lookup"><span data-stu-id="1cb02-339">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="1cb02-340">3.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-340">3.0</span></span>         | `netcoreapp3.0` |

- **`--langVersion <VERSION_NUMBER>`**

  <span data-ttu-id="1cb02-341">在已创建的项目文件中设置 `LangVersion` 属性。</span><span class="sxs-lookup"><span data-stu-id="1cb02-341">Sets the `LangVersion` property in the created project file.</span></span> <span data-ttu-id="1cb02-342">例如，使用 `--langVersion 7.3` 以使用 C# 7.3。</span><span class="sxs-lookup"><span data-stu-id="1cb02-342">For example, use `--langVersion 7.3` to use C# 7.3.</span></span> <span data-ttu-id="1cb02-343">不支持 F#。</span><span class="sxs-lookup"><span data-stu-id="1cb02-343">Not supported for F#.</span></span> <span data-ttu-id="1cb02-344">自 .NET Core 2.2 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-344">Available since .NET Core 2.2 SDK.</span></span>

  <span data-ttu-id="1cb02-345">有关默认的 C# 版本列表，请参阅[默认](../../csharp/language-reference/configure-language-version.md#defaults)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-345">For a list of default C# versions, see [Defaults](../../csharp/language-reference/configure-language-version.md#defaults).</span></span>

- **`--no-restore`**

  <span data-ttu-id="1cb02-346">如已指定，则在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="1cb02-346">If specified, doesn't execute an implicit restore during project creation.</span></span> <span data-ttu-id="1cb02-347">自 .NET Core 2.2 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-347">Available since .NET Core 2.2 SDK.</span></span>

<span data-ttu-id="1cb02-348">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-348">\*\*_</span></span>

### <a name="classlib"></a><span data-ttu-id="1cb02-349">classlib</span><span class="sxs-lookup"><span data-stu-id="1cb02-349">classlib</span></span>

- <span data-ttu-id="1cb02-350">_ *`-f|--framework <FRAMEWORK>`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-350">_ *`-f|--framework <FRAMEWORK>`*\*</span></span>

  <span data-ttu-id="1cb02-351">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-351">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1cb02-352">值：`netcoreapp<version>`（要创建 .NET Core 类库的话）或 `netstandard<version>`（要创建 .NET Standard 类库的话）。</span><span class="sxs-lookup"><span data-stu-id="1cb02-352">Values: `netcoreapp<version>` to create a .NET Core Class Library or `netstandard<version>` to create a .NET Standard Class Library.</span></span> <span data-ttu-id="1cb02-353">默认值为 `netstandard2.0`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-353">The default value is `netstandard2.0`.</span></span>

- **`--langVersion <VERSION_NUMBER>`**

  <span data-ttu-id="1cb02-354">在已创建的项目文件中设置 `LangVersion` 属性。</span><span class="sxs-lookup"><span data-stu-id="1cb02-354">Sets the `LangVersion` property in the created project file.</span></span> <span data-ttu-id="1cb02-355">例如，使用 `--langVersion 7.3` 以使用 C# 7.3。</span><span class="sxs-lookup"><span data-stu-id="1cb02-355">For example, use `--langVersion 7.3` to use C# 7.3.</span></span> <span data-ttu-id="1cb02-356">不支持 F#。</span><span class="sxs-lookup"><span data-stu-id="1cb02-356">Not supported for F#.</span></span> <span data-ttu-id="1cb02-357">自 .NET Core 2.2 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-357">Available since .NET Core 2.2 SDK.</span></span>

  <span data-ttu-id="1cb02-358">有关默认的 C# 版本列表，请参阅[默认](../../csharp/language-reference/configure-language-version.md#defaults)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-358">For a list of default C# versions, see [Defaults](../../csharp/language-reference/configure-language-version.md#defaults).</span></span>

- **`--no-restore`**

  <span data-ttu-id="1cb02-359">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="1cb02-359">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1cb02-360">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-360">\*\*_</span></span>

### <a name="wpf-wpflib-wpfcustomcontrollib-wpfusercontrollib"></a><a name="wpf"></a> <span data-ttu-id="1cb02-361">wpf、wpflib、wpfcustomcontrollib、wpfusercontrollib</span><span class="sxs-lookup"><span data-stu-id="1cb02-361">wpf, wpflib, wpfcustomcontrollib, wpfusercontrollib</span></span>

- <span data-ttu-id="1cb02-362">_ *`-f|--framework <FRAMEWORK>`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-362">_ *`-f|--framework <FRAMEWORK>`*\*</span></span>

  <span data-ttu-id="1cb02-363">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-363">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1cb02-364">默认值为 `netcoreapp3.1`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-364">The default value is `netcoreapp3.1`.</span></span> <span data-ttu-id="1cb02-365">自 .NET Core 3.1 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-365">Available since .NET Core 3.1 SDK.</span></span>

- **`--langVersion <VERSION_NUMBER>`**

  <span data-ttu-id="1cb02-366">在已创建的项目文件中设置 `LangVersion` 属性。</span><span class="sxs-lookup"><span data-stu-id="1cb02-366">Sets the `LangVersion` property in the created project file.</span></span> <span data-ttu-id="1cb02-367">例如，使用 `--langVersion 7.3` 以使用 C# 7.3。</span><span class="sxs-lookup"><span data-stu-id="1cb02-367">For example, use `--langVersion 7.3` to use C# 7.3.</span></span>

  <span data-ttu-id="1cb02-368">有关默认的 C# 版本列表，请参阅[默认](../../csharp/language-reference/configure-language-version.md#defaults)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-368">For a list of default C# versions, see [Defaults](../../csharp/language-reference/configure-language-version.md#defaults).</span></span>

- **`--no-restore`**

  <span data-ttu-id="1cb02-369">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="1cb02-369">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1cb02-370">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-370">\*\*_</span></span>

### <a name="winforms-winformslib"></a><a name="winforms"></a> <span data-ttu-id="1cb02-371">winforms、winformslib</span><span class="sxs-lookup"><span data-stu-id="1cb02-371">winforms, winformslib</span></span>

- <span data-ttu-id="1cb02-372">_ *`--langVersion <VERSION_NUMBER>`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-372">_ *`--langVersion <VERSION_NUMBER>`*\*</span></span>

  <span data-ttu-id="1cb02-373">在已创建的项目文件中设置 `LangVersion` 属性。</span><span class="sxs-lookup"><span data-stu-id="1cb02-373">Sets the `LangVersion` property in the created project file.</span></span> <span data-ttu-id="1cb02-374">例如，使用 `--langVersion 7.3` 以使用 C# 7.3。</span><span class="sxs-lookup"><span data-stu-id="1cb02-374">For example, use `--langVersion 7.3` to use C# 7.3.</span></span>

  <span data-ttu-id="1cb02-375">有关默认的 C# 版本列表，请参阅[默认](../../csharp/language-reference/configure-language-version.md#defaults)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-375">For a list of default C# versions, see [Defaults](../../csharp/language-reference/configure-language-version.md#defaults).</span></span>

- **`--no-restore`**

  <span data-ttu-id="1cb02-376">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="1cb02-376">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1cb02-377">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-377">\*\*_</span></span>

### <a name="worker-grpc"></a><a name="web-others"></a> <span data-ttu-id="1cb02-378">worker、grpc</span><span class="sxs-lookup"><span data-stu-id="1cb02-378">worker, grpc</span></span>

- <span data-ttu-id="1cb02-379">_ *`-f|--framework <FRAMEWORK>`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-379">_ *`-f|--framework <FRAMEWORK>`*\*</span></span>

  <span data-ttu-id="1cb02-380">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-380">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1cb02-381">默认值为 `netcoreapp3.1`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-381">The default value is `netcoreapp3.1`.</span></span> <span data-ttu-id="1cb02-382">自 .NET Core 3.1 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-382">Available since .NET Core 3.1 SDK.</span></span>

- **`--exclude-launch-settings`**

  <span data-ttu-id="1cb02-383">从生成的模板中排除 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="1cb02-383">Excludes *launchSettings.json* from the generated template.</span></span>

- **`--no-restore`**

  <span data-ttu-id="1cb02-384">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="1cb02-384">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1cb02-385">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-385">\*\*_</span></span>

### <a name="mstest-xunit"></a><a name="test"></a> <span data-ttu-id="1cb02-386">mstest、xunit</span><span class="sxs-lookup"><span data-stu-id="1cb02-386">mstest, xunit</span></span>

- <span data-ttu-id="1cb02-387">_ *`-f|--framework <FRAMEWORK>`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-387">_ *`-f|--framework <FRAMEWORK>`*\*</span></span>

  <span data-ttu-id="1cb02-388">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-388">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1cb02-389">自 .NET Core 3.0 SDK 起可用的选项。</span><span class="sxs-lookup"><span data-stu-id="1cb02-389">Option available since .NET Core 3.0 SDK.</span></span>

  <span data-ttu-id="1cb02-390">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="1cb02-390">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="1cb02-391">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="1cb02-391">SDK version</span></span> | <span data-ttu-id="1cb02-392">默认值</span><span class="sxs-lookup"><span data-stu-id="1cb02-392">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="1cb02-393">3.1</span><span class="sxs-lookup"><span data-stu-id="1cb02-393">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="1cb02-394">3.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-394">3.0</span></span>         | `netcoreapp3.0` |

- **`-p|--enable-pack`**

  <span data-ttu-id="1cb02-395">允许使用 [dotnet pack](dotnet-pack.md) 为项目打包。</span><span class="sxs-lookup"><span data-stu-id="1cb02-395">Enables packaging for the project using [dotnet pack](dotnet-pack.md).</span></span>

- **`--no-restore`**

  <span data-ttu-id="1cb02-396">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="1cb02-396">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1cb02-397">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-397">\*\*_</span></span>

### <a name="nunit"></a><span data-ttu-id="1cb02-398">nunit</span><span class="sxs-lookup"><span data-stu-id="1cb02-398">nunit</span></span>

- <span data-ttu-id="1cb02-399">_ *`-f|--framework <FRAMEWORK>`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-399">_ *`-f|--framework <FRAMEWORK>`*\*</span></span>

  <span data-ttu-id="1cb02-400">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-400">Specifies the [framework](../../standard/frameworks.md) to target.</span></span>

  <span data-ttu-id="1cb02-401">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="1cb02-401">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="1cb02-402">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="1cb02-402">SDK version</span></span> | <span data-ttu-id="1cb02-403">默认值</span><span class="sxs-lookup"><span data-stu-id="1cb02-403">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="1cb02-404">3.1</span><span class="sxs-lookup"><span data-stu-id="1cb02-404">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="1cb02-405">3.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-405">3.0</span></span>         | `netcoreapp3.0` |
  | <span data-ttu-id="1cb02-406">2.2</span><span class="sxs-lookup"><span data-stu-id="1cb02-406">2.2</span></span>         | `netcoreapp2.2` |
  | <span data-ttu-id="1cb02-407">2.1</span><span class="sxs-lookup"><span data-stu-id="1cb02-407">2.1</span></span>         | `netcoreapp2.1` |

- **`-p|--enable-pack`**

  <span data-ttu-id="1cb02-408">允许使用 [dotnet pack](dotnet-pack.md) 为项目打包。</span><span class="sxs-lookup"><span data-stu-id="1cb02-408">Enables packaging for the project using [dotnet pack](dotnet-pack.md).</span></span>

- **`--no-restore`**

  <span data-ttu-id="1cb02-409">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="1cb02-409">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1cb02-410">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-410">\*\*_</span></span>

### <a name="page"></a><span data-ttu-id="1cb02-411">页</span><span class="sxs-lookup"><span data-stu-id="1cb02-411">page</span></span>

- <span data-ttu-id="1cb02-412">_ *`-na|--namespace <NAMESPACE_NAME>`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-412">_ *`-na|--namespace <NAMESPACE_NAME>`*\*</span></span>

  <span data-ttu-id="1cb02-413">已生成代码的命名空间。</span><span class="sxs-lookup"><span data-stu-id="1cb02-413">Namespace for the generated code.</span></span> <span data-ttu-id="1cb02-414">默认值为 `MyApp.Namespace`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-414">The default value is `MyApp.Namespace`.</span></span>

- **`-np|--no-pagemodel`**

  <span data-ttu-id="1cb02-415">创建不含 PageModel 的页。</span><span class="sxs-lookup"><span data-stu-id="1cb02-415">Creates the page without a PageModel.</span></span>

<span data-ttu-id="1cb02-416">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-416">\*\*_</span></span>

### <a name="viewimports-proto"></a><a name="namespace"></a> <span data-ttu-id="1cb02-417">viewimports、proto</span><span class="sxs-lookup"><span data-stu-id="1cb02-417">viewimports, proto</span></span>

- <span data-ttu-id="1cb02-418">_ *`-na|--namespace <NAMESPACE_NAME>`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-418">_ *`-na|--namespace <NAMESPACE_NAME>`*\*</span></span>

  <span data-ttu-id="1cb02-419">已生成代码的命名空间。</span><span class="sxs-lookup"><span data-stu-id="1cb02-419">Namespace for the generated code.</span></span> <span data-ttu-id="1cb02-420">默认值为 `MyApp.Namespace`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-420">The default value is `MyApp.Namespace`.</span></span>

<span data-ttu-id="1cb02-421">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-421">\*\*_</span></span>

### <a name="blazorserver"></a><span data-ttu-id="1cb02-422">blazorserver</span><span class="sxs-lookup"><span data-stu-id="1cb02-422">blazorserver</span></span>

- <span data-ttu-id="1cb02-423">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-423">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span></span>

  <span data-ttu-id="1cb02-424">要使用的身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="1cb02-424">The type of authentication to use.</span></span> <span data-ttu-id="1cb02-425">可能的值为：</span><span class="sxs-lookup"><span data-stu-id="1cb02-425">The possible values are:</span></span>

  - <span data-ttu-id="1cb02-426">`None` - 不进行身份验证（默认）。</span><span class="sxs-lookup"><span data-stu-id="1cb02-426">`None` - No authentication (Default).</span></span>
  - <span data-ttu-id="1cb02-427">`Individual` - 个人身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-427">`Individual` - Individual authentication.</span></span>
  - <span data-ttu-id="1cb02-428">`IndividualB2C` - 使用 Azure AD B2C 进行个人身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-428">`IndividualB2C` - Individual authentication with Azure AD B2C.</span></span>
  - <span data-ttu-id="1cb02-429">`SingleOrg` - 对一个租户进行组织身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-429">`SingleOrg` - Organizational authentication for a single tenant.</span></span>
  - <span data-ttu-id="1cb02-430">`MultiOrg` - 对多个租户进行组织身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-430">`MultiOrg` - Organizational authentication for multiple tenants.</span></span>
  - <span data-ttu-id="1cb02-431">`Windows` - Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-431">`Windows` - Windows authentication.</span></span>

- **`--aad-b2c-instance <INSTANCE>`**

  <span data-ttu-id="1cb02-432">要连接到的 Azure Active Directory B2C 实例。</span><span class="sxs-lookup"><span data-stu-id="1cb02-432">The Azure Active Directory B2C instance to connect to.</span></span> <span data-ttu-id="1cb02-433">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-433">Use with `IndividualB2C` authentication.</span></span> <span data-ttu-id="1cb02-434">默认值为 `https://login.microsoftonline.com/tfp/`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-434">The default value is `https://login.microsoftonline.com/tfp/`.</span></span>

- **`-ssp|--susi-policy-id <ID>`**

  <span data-ttu-id="1cb02-435">此项目的登录和注册策略 ID。</span><span class="sxs-lookup"><span data-stu-id="1cb02-435">The sign-in and sign-up policy ID for this project.</span></span> <span data-ttu-id="1cb02-436">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-436">Use with `IndividualB2C` authentication.</span></span>

- **`-rp|--reset-password-policy-id <ID>`**

  <span data-ttu-id="1cb02-437">此项目的重置密码策略 ID。</span><span class="sxs-lookup"><span data-stu-id="1cb02-437">The reset password policy ID for this project.</span></span> <span data-ttu-id="1cb02-438">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-438">Use with `IndividualB2C` authentication.</span></span>

- **`-ep|--edit-profile-policy-id <ID>`**

  <span data-ttu-id="1cb02-439">此项目的编辑配置文件策略 ID。</span><span class="sxs-lookup"><span data-stu-id="1cb02-439">The edit profile policy ID for this project.</span></span> <span data-ttu-id="1cb02-440">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-440">Use with `IndividualB2C` authentication.</span></span>

- **`--aad-instance <INSTANCE>`**

  <span data-ttu-id="1cb02-441">要连接到的 Azure Active Directory 实例。</span><span class="sxs-lookup"><span data-stu-id="1cb02-441">The Azure Active Directory instance to connect to.</span></span> <span data-ttu-id="1cb02-442">与 `SingleOrg` 或 `MultiOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-442">Use with `SingleOrg` or `MultiOrg` authentication.</span></span> <span data-ttu-id="1cb02-443">默认值为 `https://login.microsoftonline.com/`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-443">The default value is `https://login.microsoftonline.com/`.</span></span>

- **`--client-id <ID>`**

  <span data-ttu-id="1cb02-444">此项目的客户端 ID。</span><span class="sxs-lookup"><span data-stu-id="1cb02-444">The Client ID for this project.</span></span> <span data-ttu-id="1cb02-445">与 `IndividualB2C`、`SingleOrg` 或 `MultiOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-445">Use with `IndividualB2C`, `SingleOrg`, or `MultiOrg` authentication.</span></span> <span data-ttu-id="1cb02-446">默认值为 `11111111-1111-1111-11111111111111111`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-446">The default value is `11111111-1111-1111-11111111111111111`.</span></span>

- **`--domain <DOMAIN>`**

  <span data-ttu-id="1cb02-447">目录租户的域。</span><span class="sxs-lookup"><span data-stu-id="1cb02-447">The domain for the directory tenant.</span></span> <span data-ttu-id="1cb02-448">与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-448">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="1cb02-449">默认值为 `qualified.domain.name`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-449">The default value is `qualified.domain.name`.</span></span>

- **`--tenant-id <ID>`**

  <span data-ttu-id="1cb02-450">要连接到的目录的 TenantId ID。</span><span class="sxs-lookup"><span data-stu-id="1cb02-450">The TenantId ID of the directory to connect to.</span></span> <span data-ttu-id="1cb02-451">与 `SingleOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-451">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="1cb02-452">默认值为 `22222222-2222-2222-2222-222222222222`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-452">The default value is `22222222-2222-2222-2222-222222222222`.</span></span>

- **`--callback-path <PATH>`**

  <span data-ttu-id="1cb02-453">重定向 URI 的应用程序基路径中的请求路径。</span><span class="sxs-lookup"><span data-stu-id="1cb02-453">The request path within the application's base path of the redirect URI.</span></span> <span data-ttu-id="1cb02-454">与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-454">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="1cb02-455">默认值为 `/signin-oidc`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-455">The default value is `/signin-oidc`.</span></span>

- **`-r|--org-read-access`**

  <span data-ttu-id="1cb02-456">允许此应用程序对目录进行读取访问。</span><span class="sxs-lookup"><span data-stu-id="1cb02-456">Allows this application read-access to the directory.</span></span> <span data-ttu-id="1cb02-457">仅适用于 `SingleOrg` 或 `MultiOrg` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-457">Only applies to `SingleOrg` or `MultiOrg` authentication.</span></span>

- **`--exclude-launch-settings`**

  <span data-ttu-id="1cb02-458">从生成的模板中排除 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="1cb02-458">Excludes *launchSettings.json* from the generated template.</span></span>

- **`--no-https`**

  <span data-ttu-id="1cb02-459">关闭 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1cb02-459">Turns off HTTPS.</span></span> <span data-ttu-id="1cb02-460">此选项仅适用于 `Individual`、`IndividualB2C`、`SingleOrg` 和 `MultiOrg` 未用于 `--auth` 的情况。</span><span class="sxs-lookup"><span data-stu-id="1cb02-460">This option only applies if `Individual`, `IndividualB2C`, `SingleOrg`, or `MultiOrg` aren't being used for `--auth`.</span></span>

- **`-uld|--use-local-db`**

  <span data-ttu-id="1cb02-461">指定应使用 LocalDB，而不使用 SQLite。</span><span class="sxs-lookup"><span data-stu-id="1cb02-461">Specifies LocalDB should be used instead of SQLite.</span></span> <span data-ttu-id="1cb02-462">仅适用于 `Individual` 或 `IndividualB2C` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-462">Only applies to `Individual` or `IndividualB2C` authentication.</span></span>

- **`--no-restore`**

  <span data-ttu-id="1cb02-463">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="1cb02-463">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1cb02-464">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-464">\*\*_</span></span>

### <a name="web"></a><span data-ttu-id="1cb02-465">Web</span><span class="sxs-lookup"><span data-stu-id="1cb02-465">web</span></span>

- <span data-ttu-id="1cb02-466">_ *`--exclude-launch-settings`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-466">_ *`--exclude-launch-settings`*\*</span></span>

  <span data-ttu-id="1cb02-467">从生成的模板中排除 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="1cb02-467">Excludes *launchSettings.json* from the generated template.</span></span>

- **`-f|--framework <FRAMEWORK>`**

  <span data-ttu-id="1cb02-468">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-468">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1cb02-469">选项在 .NET Core 2.2 SDK 中不可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-469">Option not available in .NET Core 2.2 SDK.</span></span>

  <span data-ttu-id="1cb02-470">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="1cb02-470">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="1cb02-471">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="1cb02-471">SDK version</span></span> | <span data-ttu-id="1cb02-472">默认值</span><span class="sxs-lookup"><span data-stu-id="1cb02-472">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="1cb02-473">3.1</span><span class="sxs-lookup"><span data-stu-id="1cb02-473">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="1cb02-474">3.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-474">3.0</span></span>         | `netcoreapp3.0` |
  | <span data-ttu-id="1cb02-475">2.1</span><span class="sxs-lookup"><span data-stu-id="1cb02-475">2.1</span></span>         | `netcoreapp2.1` |

- **`--no-restore`**

  <span data-ttu-id="1cb02-476">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="1cb02-476">Doesn't execute an implicit restore during project creation.</span></span>

- **`--no-https`**

  <span data-ttu-id="1cb02-477">关闭 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1cb02-477">Turns off HTTPS.</span></span>

<span data-ttu-id="1cb02-478">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-478">\*\*_</span></span>

### <a name="mvc-webapp"></a><a name="web-options"></a> <span data-ttu-id="1cb02-479">mvc、webapp</span><span class="sxs-lookup"><span data-stu-id="1cb02-479">mvc, webapp</span></span>

- <span data-ttu-id="1cb02-480">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-480">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span></span>

  <span data-ttu-id="1cb02-481">要使用的身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="1cb02-481">The type of authentication to use.</span></span> <span data-ttu-id="1cb02-482">可能的值为：</span><span class="sxs-lookup"><span data-stu-id="1cb02-482">The possible values are:</span></span>

  - <span data-ttu-id="1cb02-483">`None` - 不进行身份验证（默认）。</span><span class="sxs-lookup"><span data-stu-id="1cb02-483">`None` - No authentication (Default).</span></span>
  - <span data-ttu-id="1cb02-484">`Individual` - 个人身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-484">`Individual` - Individual authentication.</span></span>
  - <span data-ttu-id="1cb02-485">`IndividualB2C` - 使用 Azure AD B2C 进行个人身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-485">`IndividualB2C` - Individual authentication with Azure AD B2C.</span></span>
  - <span data-ttu-id="1cb02-486">`SingleOrg` - 对一个租户进行组织身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-486">`SingleOrg` - Organizational authentication for a single tenant.</span></span>
  - <span data-ttu-id="1cb02-487">`MultiOrg` - 对多个租户进行组织身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-487">`MultiOrg` - Organizational authentication for multiple tenants.</span></span>
  - <span data-ttu-id="1cb02-488">`Windows` - Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-488">`Windows` - Windows authentication.</span></span>

- **`--aad-b2c-instance <INSTANCE>`**

  <span data-ttu-id="1cb02-489">要连接到的 Azure Active Directory B2C 实例。</span><span class="sxs-lookup"><span data-stu-id="1cb02-489">The Azure Active Directory B2C instance to connect to.</span></span> <span data-ttu-id="1cb02-490">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-490">Use with `IndividualB2C` authentication.</span></span> <span data-ttu-id="1cb02-491">默认值为 `https://login.microsoftonline.com/tfp/`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-491">The default value is `https://login.microsoftonline.com/tfp/`.</span></span>

- **`-ssp|--susi-policy-id <ID>`**

  <span data-ttu-id="1cb02-492">此项目的登录和注册策略 ID。</span><span class="sxs-lookup"><span data-stu-id="1cb02-492">The sign-in and sign-up policy ID for this project.</span></span> <span data-ttu-id="1cb02-493">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-493">Use with `IndividualB2C` authentication.</span></span>

- **`-rp|--reset-password-policy-id <ID>`**

  <span data-ttu-id="1cb02-494">此项目的重置密码策略 ID。</span><span class="sxs-lookup"><span data-stu-id="1cb02-494">The reset password policy ID for this project.</span></span> <span data-ttu-id="1cb02-495">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-495">Use with `IndividualB2C` authentication.</span></span>

- **`-ep|--edit-profile-policy-id <ID>`**

  <span data-ttu-id="1cb02-496">此项目的编辑配置文件策略 ID。</span><span class="sxs-lookup"><span data-stu-id="1cb02-496">The edit profile policy ID for this project.</span></span> <span data-ttu-id="1cb02-497">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-497">Use with `IndividualB2C` authentication.</span></span>

- **`--aad-instance <INSTANCE>`**

  <span data-ttu-id="1cb02-498">要连接到的 Azure Active Directory 实例。</span><span class="sxs-lookup"><span data-stu-id="1cb02-498">The Azure Active Directory instance to connect to.</span></span> <span data-ttu-id="1cb02-499">与 `SingleOrg` 或 `MultiOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-499">Use with `SingleOrg` or `MultiOrg` authentication.</span></span> <span data-ttu-id="1cb02-500">默认值为 `https://login.microsoftonline.com/`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-500">The default value is `https://login.microsoftonline.com/`.</span></span>

- **`--client-id <ID>`**

  <span data-ttu-id="1cb02-501">此项目的客户端 ID。</span><span class="sxs-lookup"><span data-stu-id="1cb02-501">The Client ID for this project.</span></span> <span data-ttu-id="1cb02-502">与 `IndividualB2C`、`SingleOrg` 或 `MultiOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-502">Use with `IndividualB2C`, `SingleOrg`, or `MultiOrg` authentication.</span></span> <span data-ttu-id="1cb02-503">默认值为 `11111111-1111-1111-11111111111111111`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-503">The default value is `11111111-1111-1111-11111111111111111`.</span></span>

- **`--domain <DOMAIN>`**

  <span data-ttu-id="1cb02-504">目录租户的域。</span><span class="sxs-lookup"><span data-stu-id="1cb02-504">The domain for the directory tenant.</span></span> <span data-ttu-id="1cb02-505">与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-505">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="1cb02-506">默认值为 `qualified.domain.name`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-506">The default value is `qualified.domain.name`.</span></span>

- **`--tenant-id <ID>`**

  <span data-ttu-id="1cb02-507">要连接到的目录的 TenantId ID。</span><span class="sxs-lookup"><span data-stu-id="1cb02-507">The TenantId ID of the directory to connect to.</span></span> <span data-ttu-id="1cb02-508">与 `SingleOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-508">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="1cb02-509">默认值为 `22222222-2222-2222-2222-222222222222`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-509">The default value is `22222222-2222-2222-2222-222222222222`.</span></span>

- **`--callback-path <PATH>`**

  <span data-ttu-id="1cb02-510">重定向 URI 的应用程序基路径中的请求路径。</span><span class="sxs-lookup"><span data-stu-id="1cb02-510">The request path within the application's base path of the redirect URI.</span></span> <span data-ttu-id="1cb02-511">与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-511">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="1cb02-512">默认值为 `/signin-oidc`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-512">The default value is `/signin-oidc`.</span></span>

- **`-r|--org-read-access`**

  <span data-ttu-id="1cb02-513">允许此应用程序对目录进行读取访问。</span><span class="sxs-lookup"><span data-stu-id="1cb02-513">Allows this application read-access to the directory.</span></span> <span data-ttu-id="1cb02-514">仅适用于 `SingleOrg` 或 `MultiOrg` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-514">Only applies to `SingleOrg` or `MultiOrg` authentication.</span></span>

- **`--exclude-launch-settings`**

  <span data-ttu-id="1cb02-515">从生成的模板中排除 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="1cb02-515">Excludes *launchSettings.json* from the generated template.</span></span>

- **`--no-https`**

  <span data-ttu-id="1cb02-516">关闭 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1cb02-516">Turns off HTTPS.</span></span> <span data-ttu-id="1cb02-517">此选项仅适用于未使用 `Individual`、`IndividualB2C`、`SingleOrg` 和 `MultiOrg` 的情况。</span><span class="sxs-lookup"><span data-stu-id="1cb02-517">This option only applies if `Individual`, `IndividualB2C`, `SingleOrg`, or `MultiOrg` aren't being used.</span></span>

- **`-uld|--use-local-db`**

  <span data-ttu-id="1cb02-518">指定应使用 LocalDB，而不使用 SQLite。</span><span class="sxs-lookup"><span data-stu-id="1cb02-518">Specifies LocalDB should be used instead of SQLite.</span></span> <span data-ttu-id="1cb02-519">仅适用于 `Individual` 或 `IndividualB2C` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-519">Only applies to `Individual` or `IndividualB2C` authentication.</span></span>

- **`-f|--framework <FRAMEWORK>`**

  <span data-ttu-id="1cb02-520">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-520">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1cb02-521">自 .NET Core 3.0 SDK 起可用的选项。</span><span class="sxs-lookup"><span data-stu-id="1cb02-521">Option available since .NET Core 3.0 SDK.</span></span>

  <span data-ttu-id="1cb02-522">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="1cb02-522">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="1cb02-523">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="1cb02-523">SDK version</span></span> | <span data-ttu-id="1cb02-524">默认值</span><span class="sxs-lookup"><span data-stu-id="1cb02-524">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="1cb02-525">3.1</span><span class="sxs-lookup"><span data-stu-id="1cb02-525">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="1cb02-526">3.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-526">3.0</span></span>         | `netcoreapp3.0` |

- **`--no-restore`**

  <span data-ttu-id="1cb02-527">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="1cb02-527">Doesn't execute an implicit restore during project creation.</span></span>

- **`--use-browserlink`**

  <span data-ttu-id="1cb02-528">在项目中添加 BrowserLink。</span><span class="sxs-lookup"><span data-stu-id="1cb02-528">Includes BrowserLink in the project.</span></span> <span data-ttu-id="1cb02-529">选项在 .NET Core 2.2 和 3.1 SDK 中不可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-529">Option not available in .NET Core 2.2 and 3.1 SDK.</span></span>

- **`-rrc|--razor-runtime-compilation`**

  <span data-ttu-id="1cb02-530">确定项目是否配置为在调试生成中使用 [Razor 运行时编译](/aspnet/core/mvc/views/view-compilation#runtime-compilation)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-530">Determines if the project is configured to use [Razor runtime compilation](/aspnet/core/mvc/views/view-compilation#runtime-compilation) in Debug builds.</span></span> <span data-ttu-id="1cb02-531">自 .NET Core 3.1.201 SDK 起可用的选项。</span><span class="sxs-lookup"><span data-stu-id="1cb02-531">Option available since .NET Core 3.1.201 SDK.</span></span>

<span data-ttu-id="1cb02-532">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-532">\*\*_</span></span>

### <a name="angular-react"></a><a name="spa"></a> <span data-ttu-id="1cb02-533">angular、react</span><span class="sxs-lookup"><span data-stu-id="1cb02-533">angular, react</span></span>

- <span data-ttu-id="1cb02-534">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-534">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span></span>

  <span data-ttu-id="1cb02-535">要使用的身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="1cb02-535">The type of authentication to use.</span></span> <span data-ttu-id="1cb02-536">自 .NET Core 3.0 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-536">Available since .NET Core 3.0 SDK.</span></span>
  
  <span data-ttu-id="1cb02-537">可能的值为：</span><span class="sxs-lookup"><span data-stu-id="1cb02-537">The possible values are:</span></span>

  - <span data-ttu-id="1cb02-538">`None` - 不进行身份验证（默认）。</span><span class="sxs-lookup"><span data-stu-id="1cb02-538">`None` - No authentication (Default).</span></span>
  - <span data-ttu-id="1cb02-539">`Individual` - 个人身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-539">`Individual` - Individual authentication.</span></span>

- **`--exclude-launch-settings`**

  <span data-ttu-id="1cb02-540">从生成的模板中排除 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="1cb02-540">Excludes *launchSettings.json* from the generated template.</span></span>

- **`--no-restore`**

  <span data-ttu-id="1cb02-541">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="1cb02-541">Doesn't execute an implicit restore during project creation.</span></span>

- **`--no-https`**

  <span data-ttu-id="1cb02-542">关闭 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1cb02-542">Turns off HTTPS.</span></span> <span data-ttu-id="1cb02-543">仅当身份验证为 `None` 时，此选项才适用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-543">This option only applies if authentication is `None`.</span></span>

- **`-uld|--use-local-db`**

  <span data-ttu-id="1cb02-544">指定应使用 LocalDB，而不使用 SQLite。</span><span class="sxs-lookup"><span data-stu-id="1cb02-544">Specifies LocalDB should be used instead of SQLite.</span></span> <span data-ttu-id="1cb02-545">仅适用于 `Individual` 或 `IndividualB2C` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-545">Only applies to `Individual` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="1cb02-546">自 .NET Core 3.0 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-546">Available since .NET Core 3.0 SDK.</span></span>

- **`-f|--framework <FRAMEWORK>`**

  <span data-ttu-id="1cb02-547">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-547">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1cb02-548">选项在 .NET Core 2.2 SDK 中不可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-548">Option not available in .NET Core 2.2 SDK.</span></span>

  <span data-ttu-id="1cb02-549">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="1cb02-549">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="1cb02-550">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="1cb02-550">SDK version</span></span> | <span data-ttu-id="1cb02-551">默认值</span><span class="sxs-lookup"><span data-stu-id="1cb02-551">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="1cb02-552">3.1</span><span class="sxs-lookup"><span data-stu-id="1cb02-552">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="1cb02-553">3.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-553">3.0</span></span>         | `netcoreapp3.0` |
  | <span data-ttu-id="1cb02-554">2.1</span><span class="sxs-lookup"><span data-stu-id="1cb02-554">2.1</span></span>         | `netcoreapp2.0` |

<span data-ttu-id="1cb02-555">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-555">\*\*_</span></span>

### <a name="reactredux"></a><span data-ttu-id="1cb02-556">reactredux</span><span class="sxs-lookup"><span data-stu-id="1cb02-556">reactredux</span></span>

- <span data-ttu-id="1cb02-557">_ *`--exclude-launch-settings`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-557">_ *`--exclude-launch-settings`*\*</span></span>

  <span data-ttu-id="1cb02-558">从生成的模板中排除 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="1cb02-558">Excludes *launchSettings.json* from the generated template.</span></span>

- **`-f|--framework <FRAMEWORK>`**

  <span data-ttu-id="1cb02-559">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-559">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1cb02-560">选项在 .NET Core 2.2 SDK 中不可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-560">Option not available in .NET Core 2.2 SDK.</span></span>

  <span data-ttu-id="1cb02-561">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="1cb02-561">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="1cb02-562">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="1cb02-562">SDK version</span></span> | <span data-ttu-id="1cb02-563">默认值</span><span class="sxs-lookup"><span data-stu-id="1cb02-563">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="1cb02-564">3.1</span><span class="sxs-lookup"><span data-stu-id="1cb02-564">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="1cb02-565">3.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-565">3.0</span></span>         | `netcoreapp3.0` |
  | <span data-ttu-id="1cb02-566">2.1</span><span class="sxs-lookup"><span data-stu-id="1cb02-566">2.1</span></span>         | `netcoreapp2.0` |

- **`--no-restore`**

  <span data-ttu-id="1cb02-567">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="1cb02-567">Doesn't execute an implicit restore during project creation.</span></span>

- **`--no-https`**

  <span data-ttu-id="1cb02-568">关闭 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1cb02-568">Turns off HTTPS.</span></span>

<span data-ttu-id="1cb02-569">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-569">\*\*_</span></span>

### <a name="razorclasslib"></a><span data-ttu-id="1cb02-570">razorclasslib</span><span class="sxs-lookup"><span data-stu-id="1cb02-570">razorclasslib</span></span>

- <span data-ttu-id="1cb02-571">_ *`--no-restore`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-571">_ *`--no-restore`*\*</span></span>

  <span data-ttu-id="1cb02-572">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="1cb02-572">Doesn't execute an implicit restore during project creation.</span></span>

- **`-s|--support-pages-and-views`**

  <span data-ttu-id="1cb02-573">除了将组件添加到此库以外，还支持添加传统的 Razor 页面和视图。</span><span class="sxs-lookup"><span data-stu-id="1cb02-573">Supports adding traditional Razor pages and Views in addition to components to this library.</span></span> <span data-ttu-id="1cb02-574">自 .NET Core 3.0 SDK 起可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-574">Available since .NET Core 3.0 SDK.</span></span>

<span data-ttu-id="1cb02-575">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-575">\*\*_</span></span>
  
### <a name="webapi"></a><span data-ttu-id="1cb02-576">webapi</span><span class="sxs-lookup"><span data-stu-id="1cb02-576">webapi</span></span>

- <span data-ttu-id="1cb02-577">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-577">_ *`-au|--auth <AUTHENTICATION_TYPE>`*\*</span></span>

  <span data-ttu-id="1cb02-578">要使用的身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="1cb02-578">The type of authentication to use.</span></span> <span data-ttu-id="1cb02-579">可能的值为：</span><span class="sxs-lookup"><span data-stu-id="1cb02-579">The possible values are:</span></span>

  - <span data-ttu-id="1cb02-580">`None` - 不进行身份验证（默认）。</span><span class="sxs-lookup"><span data-stu-id="1cb02-580">`None` - No authentication (Default).</span></span>
  - <span data-ttu-id="1cb02-581">`IndividualB2C` - 使用 Azure AD B2C 进行个人身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-581">`IndividualB2C` - Individual authentication with Azure AD B2C.</span></span>
  - <span data-ttu-id="1cb02-582">`SingleOrg` - 对一个租户进行组织身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-582">`SingleOrg` - Organizational authentication for a single tenant.</span></span>
  - <span data-ttu-id="1cb02-583">`Windows` - Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-583">`Windows` - Windows authentication.</span></span>

- **`--aad-b2c-instance <INSTANCE>`**

  <span data-ttu-id="1cb02-584">要连接到的 Azure Active Directory B2C 实例。</span><span class="sxs-lookup"><span data-stu-id="1cb02-584">The Azure Active Directory B2C instance to connect to.</span></span> <span data-ttu-id="1cb02-585">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-585">Use with `IndividualB2C` authentication.</span></span> <span data-ttu-id="1cb02-586">默认值为 `https://login.microsoftonline.com/tfp/`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-586">The default value is `https://login.microsoftonline.com/tfp/`.</span></span>

- **`-ssp|--susi-policy-id <ID>`**

  <span data-ttu-id="1cb02-587">此项目的登录和注册策略 ID。</span><span class="sxs-lookup"><span data-stu-id="1cb02-587">The sign-in and sign-up policy ID for this project.</span></span> <span data-ttu-id="1cb02-588">与 `IndividualB2C` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-588">Use with `IndividualB2C` authentication.</span></span>

- **`--aad-instance <INSTANCE>`**

  <span data-ttu-id="1cb02-589">要连接到的 Azure Active Directory 实例。</span><span class="sxs-lookup"><span data-stu-id="1cb02-589">The Azure Active Directory instance to connect to.</span></span> <span data-ttu-id="1cb02-590">与 `SingleOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-590">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="1cb02-591">默认值为 `https://login.microsoftonline.com/`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-591">The default value is `https://login.microsoftonline.com/`.</span></span>

- **`--client-id <ID>`**

  <span data-ttu-id="1cb02-592">此项目的客户端 ID。</span><span class="sxs-lookup"><span data-stu-id="1cb02-592">The Client ID for this project.</span></span> <span data-ttu-id="1cb02-593">与 `IndividualB2C` 或 `SingleOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-593">Use with `IndividualB2C` or `SingleOrg` authentication.</span></span> <span data-ttu-id="1cb02-594">默认值为 `11111111-1111-1111-11111111111111111`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-594">The default value is `11111111-1111-1111-11111111111111111`.</span></span>

- **`--domain <DOMAIN>`**

  <span data-ttu-id="1cb02-595">目录租户的域。</span><span class="sxs-lookup"><span data-stu-id="1cb02-595">The domain for the directory tenant.</span></span> <span data-ttu-id="1cb02-596">与 `IndividualB2C` 或 `SingleOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-596">Use with `IndividualB2C` or `SingleOrg` authentication.</span></span> <span data-ttu-id="1cb02-597">默认值为 `qualified.domain.name`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-597">The default value is `qualified.domain.name`.</span></span>

- **`--tenant-id <ID>`**

  <span data-ttu-id="1cb02-598">要连接到的目录的 TenantId ID。</span><span class="sxs-lookup"><span data-stu-id="1cb02-598">The TenantId ID of the directory to connect to.</span></span> <span data-ttu-id="1cb02-599">与 `SingleOrg` 身份验证结合使用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-599">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="1cb02-600">默认值为 `22222222-2222-2222-2222-222222222222`。</span><span class="sxs-lookup"><span data-stu-id="1cb02-600">The default value is `22222222-2222-2222-2222-222222222222`.</span></span>

- **`-r|--org-read-access`**

  <span data-ttu-id="1cb02-601">允许此应用程序对目录进行读取访问。</span><span class="sxs-lookup"><span data-stu-id="1cb02-601">Allows this application read-access to the directory.</span></span> <span data-ttu-id="1cb02-602">仅适用于 `SingleOrg` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-602">Only applies to `SingleOrg` authentication.</span></span>

- **`--exclude-launch-settings`**

  <span data-ttu-id="1cb02-603">从生成的模板中排除 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="1cb02-603">Excludes *launchSettings.json* from the generated template.</span></span>

- **`--no-https`**

  <span data-ttu-id="1cb02-604">关闭 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1cb02-604">Turns off HTTPS.</span></span> <span data-ttu-id="1cb02-605">`app.UseHsts` 和 `app.UseHttpsRedirection` 未添加到 `Startup.Configure` 中。</span><span class="sxs-lookup"><span data-stu-id="1cb02-605">`app.UseHsts` and `app.UseHttpsRedirection` aren't added to `Startup.Configure`.</span></span> <span data-ttu-id="1cb02-606">此选项仅适用于 `IndividualB2C` 或 `SingleOrg` 未用于身份验证的情况。</span><span class="sxs-lookup"><span data-stu-id="1cb02-606">This option only applies if `IndividualB2C` or `SingleOrg` aren't being used for authentication.</span></span>

- **`-uld|--use-local-db`**

  <span data-ttu-id="1cb02-607">指定应使用 LocalDB，而不使用 SQLite。</span><span class="sxs-lookup"><span data-stu-id="1cb02-607">Specifies LocalDB should be used instead of SQLite.</span></span> <span data-ttu-id="1cb02-608">仅适用于 `IndividualB2C` 身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cb02-608">Only applies to `IndividualB2C` authentication.</span></span>

- **`-f|--framework <FRAMEWORK>`**

  <span data-ttu-id="1cb02-609">指定目标[框架](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1cb02-609">Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1cb02-610">选项在 .NET Core 2.2 SDK 中不可用。</span><span class="sxs-lookup"><span data-stu-id="1cb02-610">Option not available in .NET Core 2.2 SDK.</span></span>

  <span data-ttu-id="1cb02-611">下表根据所使用的 SDK 版本号列出了默认值：</span><span class="sxs-lookup"><span data-stu-id="1cb02-611">The following table lists the default values according to the SDK version number you're using:</span></span>

  | <span data-ttu-id="1cb02-612">SDK 版本</span><span class="sxs-lookup"><span data-stu-id="1cb02-612">SDK version</span></span> | <span data-ttu-id="1cb02-613">默认值</span><span class="sxs-lookup"><span data-stu-id="1cb02-613">Default value</span></span>   |
  |-------------|-----------------|
  | <span data-ttu-id="1cb02-614">3.1</span><span class="sxs-lookup"><span data-stu-id="1cb02-614">3.1</span></span>         | `netcoreapp3.1` |
  | <span data-ttu-id="1cb02-615">3.0</span><span class="sxs-lookup"><span data-stu-id="1cb02-615">3.0</span></span>         | `netcoreapp3.0` |
  | <span data-ttu-id="1cb02-616">2.1</span><span class="sxs-lookup"><span data-stu-id="1cb02-616">2.1</span></span>         | `netcoreapp2.1` |

- **`--no-restore`**

  <span data-ttu-id="1cb02-617">在项目创建期间不执行隐式还原。</span><span class="sxs-lookup"><span data-stu-id="1cb02-617">Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1cb02-618">\*\*_</span><span class="sxs-lookup"><span data-stu-id="1cb02-618">\*\*_</span></span>

### <a name="globaljson"></a><span data-ttu-id="1cb02-619">globaljson</span><span class="sxs-lookup"><span data-stu-id="1cb02-619">globaljson</span></span>

- <span data-ttu-id="1cb02-620">_ *`--sdk-version <VERSION_NUMBER>`*\*</span><span class="sxs-lookup"><span data-stu-id="1cb02-620">_ *`--sdk-version <VERSION_NUMBER>`*\*</span></span>

  <span data-ttu-id="1cb02-621">指定要在 global.json 文件中使用的 .NET Core SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="1cb02-621">Specifies the version of the .NET Core SDK to use in the *global.json* file.</span></span>

***

## <a name="examples"></a><span data-ttu-id="1cb02-622">示例</span><span class="sxs-lookup"><span data-stu-id="1cb02-622">Examples</span></span>

- <span data-ttu-id="1cb02-623">通过指定模板名称，创建 C# 控制台应用程序项目：</span><span class="sxs-lookup"><span data-stu-id="1cb02-623">Create a C# console application project by specifying the template name:</span></span>

  ```dotnetcli
  dotnet new "Console Application"
  ```

- <span data-ttu-id="1cb02-624">在当前目录中创建 F# 控制台应用程序项目：</span><span class="sxs-lookup"><span data-stu-id="1cb02-624">Create an F# console application project in the current directory:</span></span>

  ```dotnetcli
  dotnet new console -lang "F#"
  ```

- <span data-ttu-id="1cb02-625">在指定的目录中创建 .NET Standard 类库项目：</span><span class="sxs-lookup"><span data-stu-id="1cb02-625">Create a .NET Standard class library project in the specified directory:</span></span>

  ```dotnetcli
  dotnet new classlib -lang VB -o MyLibrary
  ```

- <span data-ttu-id="1cb02-626">在当前目录中新建没有设置身份验证的 ASP.NET Core C# MVC 项目：</span><span class="sxs-lookup"><span data-stu-id="1cb02-626">Create a new ASP.NET Core C# MVC project in the current directory with no authentication:</span></span>

  ```dotnetcli
  dotnet new mvc -au None
  ```

- <span data-ttu-id="1cb02-627">创建新的 xUnit 项目：</span><span class="sxs-lookup"><span data-stu-id="1cb02-627">Create a new xUnit project:</span></span>

  ```dotnetcli
  dotnet new xunit
  ```

- <span data-ttu-id="1cb02-628">列出可用于单页应用程序 (SPA) 模板的所有模板：</span><span class="sxs-lookup"><span data-stu-id="1cb02-628">List all templates available for Single Page Application (SPA) templates:</span></span>

  ```dotnetcli
  dotnet new spa -l
  ```

- <span data-ttu-id="1cb02-629">列出与“we”子字符串匹配的所有模板。</span><span class="sxs-lookup"><span data-stu-id="1cb02-629">List all templates matching the *we* substring.</span></span> <span data-ttu-id="1cb02-630">找不到完全匹配，因此子字符串匹配针对短名称和名称列运行。</span><span class="sxs-lookup"><span data-stu-id="1cb02-630">No exact match is found, so substring matching runs against both the short name and name columns.</span></span>

  ```dotnetcli
  dotnet new we -l
  ```

- <span data-ttu-id="1cb02-631">尝试调用与 ng 匹配的模板。</span><span class="sxs-lookup"><span data-stu-id="1cb02-631">Attempt to invoke the template matching *ng* .</span></span> <span data-ttu-id="1cb02-632">如果无法确定单个匹配项，请列出部分匹配项的模板。</span><span class="sxs-lookup"><span data-stu-id="1cb02-632">If a single match can't be determined, list the templates that are partial matches.</span></span>

  ```dotnetcli
  dotnet new ng
  ```

- <span data-ttu-id="1cb02-633">安装 ASP.NET Core 的 SPA 模板 2.0 版：</span><span class="sxs-lookup"><span data-stu-id="1cb02-633">Install version 2.0 of the SPA templates for ASP.NET Core:</span></span>

  ```dotnetcli
  dotnet new -i Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0
  ```

- <span data-ttu-id="1cb02-634">列出已安装的模板及其详细信息，包括如何卸载它们：</span><span class="sxs-lookup"><span data-stu-id="1cb02-634">List the installed templates and details about them, including how to uninstall them:</span></span>

  ```dotnetcli
  dotnet new -u
  ```

- <span data-ttu-id="1cb02-635">在当前目录中创建 global.json，将 SDK 版本设置为 3.1.101：</span><span class="sxs-lookup"><span data-stu-id="1cb02-635">Create a *global.json* in the current directory setting the SDK version to 3.1.101:</span></span>

  ```dotnetcli
  dotnet new globaljson --sdk-version 3.1.101
  ```

## <a name="see-also"></a><span data-ttu-id="1cb02-636">请参阅</span><span class="sxs-lookup"><span data-stu-id="1cb02-636">See also</span></span>

- [<span data-ttu-id="1cb02-637">dotnet new 自定义模板</span><span class="sxs-lookup"><span data-stu-id="1cb02-637">Custom templates for dotnet new</span></span>](custom-templates.md)
- [<span data-ttu-id="1cb02-638">创建 dotnet new 自定义模板</span><span class="sxs-lookup"><span data-stu-id="1cb02-638">Create a custom template for dotnet new</span></span>](../tutorials/cli-templates-create-item-template.md)
- [<span data-ttu-id="1cb02-639">dotnet/dotnet-template-samples GitHub 存储库</span><span class="sxs-lookup"><span data-stu-id="1cb02-639">dotnet/dotnet-template-samples GitHub repo</span></span>](https://github.com/dotnet/dotnet-template-samples)
- [<span data-ttu-id="1cb02-640">dotnet new 可用模板</span><span class="sxs-lookup"><span data-stu-id="1cb02-640">Available templates for dotnet new</span></span>](https://github.com/dotnet/templating/wiki/Available-templates-for-dotnet-new)
