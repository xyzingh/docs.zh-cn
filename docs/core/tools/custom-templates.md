---
title: dotnet new 自定义模板
description: 了解任意类型 .NET 项目或文件的自定义模板。
author: adegeo
ms.date: 05/20/2020
ms.openlocfilehash: 62d98adab0122936957301ee737c366541b0cfe6
ms.sourcegitcommit: 870bc4b4087510f6fba3c7b1c0d391f02bcc1f3e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2020
ms.locfileid: "92471545"
---
# <a name="custom-templates-for-dotnet-new"></a><span data-ttu-id="e2508-103">dotnet new 自定义模板</span><span class="sxs-lookup"><span data-stu-id="e2508-103">Custom templates for dotnet new</span></span>

<span data-ttu-id="e2508-104">[.NET Core SDK](https://dotnet.microsoft.com/download) 随附了许多已安装并可供你使用的模板。</span><span class="sxs-lookup"><span data-stu-id="e2508-104">The [.NET Core SDK](https://dotnet.microsoft.com/download) comes with many templates already installed and ready for you to use.</span></span> <span data-ttu-id="e2508-105">[`dotnet new` 命令](dotnet-new.md)不仅用于使用模板，还用于说明如何安装和卸载模板。</span><span class="sxs-lookup"><span data-stu-id="e2508-105">The [`dotnet new` command](dotnet-new.md) isn't only the way to use a template, but also how to install and uninstall templates.</span></span> <span data-ttu-id="e2508-106">自.NET Core 2.0 起，可以为任何类型的项目（如应用程序、服务、工具或类库）创建自己的自定义模板。</span><span class="sxs-lookup"><span data-stu-id="e2508-106">Starting with .NET Core 2.0, you can create your own custom templates for any type of project, such as an app, service, tool, or class library.</span></span> <span data-ttu-id="e2508-107">甚至可以创建输出一个或多个独立文件（如配置文件）的模板。</span><span class="sxs-lookup"><span data-stu-id="e2508-107">You can even create a template that outputs one or more independent files, such as a configuration file.</span></span>

<span data-ttu-id="e2508-108">可以从任何 NuGet 源上的 NuGet 包安装自定义模板，具体方法是直接引用 NuGet .nupkg 文件，或指定包含模板的文件系统目录。</span><span class="sxs-lookup"><span data-stu-id="e2508-108">You can install custom templates from a NuGet package on any NuGet feed, by referencing a NuGet *.nupkg* file directly, or by specifying a file system directory that contains the template.</span></span> <span data-ttu-id="e2508-109">借助模板引擎提供的功能，可以替换值、包括和排除文件，并在使用模板时执行自定义处理操作。</span><span class="sxs-lookup"><span data-stu-id="e2508-109">The template engine offers features that allow you to replace values, include and exclude files, and execute custom processing operations when your template is used.</span></span>

<span data-ttu-id="e2508-110">模板引擎是开放源代码，在线代码存储库位于 GitHub 上的 [dotnet/templating](https://github.com/dotnet/templating/)。</span><span class="sxs-lookup"><span data-stu-id="e2508-110">The template engine is open source, and the online code repository is at [dotnet/templating](https://github.com/dotnet/templating/) on GitHub.</span></span> <span data-ttu-id="e2508-111">GitHub 上的 [dotnet new 可用模板](https://github.com/dotnet/templating/wiki/Available-templates-for-dotnet-new)收录了更多模板，包括第三方模板。</span><span class="sxs-lookup"><span data-stu-id="e2508-111">More templates, including templates from third parties, are found at [Available templates for dotnet new](https://github.com/dotnet/templating/wiki/Available-templates-for-dotnet-new) on GitHub.</span></span> <span data-ttu-id="e2508-112">若要详细了解如何创建和使用自定义模板，请参阅[如何创建自己的 dotnet new 模板](https://devblogs.microsoft.com/dotnet/how-to-create-your-own-templates-for-dotnet-new/)和 [dotnet/templating GitHub 存储库 Wiki](https://github.com/dotnet/templating/wiki)。</span><span class="sxs-lookup"><span data-stu-id="e2508-112">For more information about creating and using custom templates, see [How to create your own templates for dotnet new](https://devblogs.microsoft.com/dotnet/how-to-create-your-own-templates-for-dotnet-new/) and the [dotnet/templating GitHub repo Wiki](https://github.com/dotnet/templating/wiki).</span></span>

> [!NOTE]
> <span data-ttu-id="e2508-113">[dotnet/dotnet-template-samples](https://github.com/dotnet/dotnet-template-samples) GitHub 存储库提供了模板示例。</span><span class="sxs-lookup"><span data-stu-id="e2508-113">Template examples are available at the [dotnet/dotnet-template-samples](https://github.com/dotnet/dotnet-template-samples) GitHub repository.</span></span> <span data-ttu-id="e2508-114">尽管这些示例是了解模板工作方式的良好资源，但该存储库已存档且不再维护。</span><span class="sxs-lookup"><span data-stu-id="e2508-114">However, while these examples are good resource for learning how the templates work, the repository is archived and no longer maintained.</span></span> <span data-ttu-id="e2508-115">这些例子可能已过期且不再有效。</span><span class="sxs-lookup"><span data-stu-id="e2508-115">The examples may be out of date and no longer working.</span></span>

<span data-ttu-id="e2508-116">若要按照演示步骤操作并创建模板，请参阅[创建 dotnet new 自定义模板](../tutorials/cli-templates-create-item-template.md)教程。</span><span class="sxs-lookup"><span data-stu-id="e2508-116">To follow a walkthrough and create a template, see the [Create a custom template for dotnet new](../tutorials/cli-templates-create-item-template.md) tutorial.</span></span>

### <a name="net-default-templates"></a><span data-ttu-id="e2508-117">.NET 默认模板</span><span class="sxs-lookup"><span data-stu-id="e2508-117">.NET default templates</span></span>

<span data-ttu-id="e2508-118">安装 [.NET Core SDK](https://dotnet.microsoft.com/download) 时，将获取十多个用于创建项目和文件的内置模板，包括控制台应用程序、类库、单元测试项目、ASP.NET Core 应用程序（包括 [Angular](https://angular.io/) 和 [React](https://reactjs.org/) 项目）和配置文件。</span><span class="sxs-lookup"><span data-stu-id="e2508-118">When you install the [.NET Core SDK](https://dotnet.microsoft.com/download), you receive over a dozen built-in templates for creating projects and files, including console apps, class libraries, unit test projects, ASP.NET Core apps (including [Angular](https://angular.io/) and [React](https://reactjs.org/) projects), and configuration files.</span></span> <span data-ttu-id="e2508-119">若要列出内置模板，请运行带有 `-l|--list` 选项的 `dotnet new` 命令：</span><span class="sxs-lookup"><span data-stu-id="e2508-119">To list the built-in templates, run the `dotnet new` command with the `-l|--list` option:</span></span>

```dotnetcli
dotnet new --list
```

## <a name="configuration"></a><span data-ttu-id="e2508-120">Configuration</span><span class="sxs-lookup"><span data-stu-id="e2508-120">Configuration</span></span>

<span data-ttu-id="e2508-121">模板由以下部分组成：</span><span class="sxs-lookup"><span data-stu-id="e2508-121">A template is composed of the following parts:</span></span>

- <span data-ttu-id="e2508-122">源文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="e2508-122">Source files and folders.</span></span>
- <span data-ttu-id="e2508-123">配置文件 (template.json)。</span><span class="sxs-lookup"><span data-stu-id="e2508-123">A configuration file ( *template.json* ).</span></span>

### <a name="source-files-and-folders"></a><span data-ttu-id="e2508-124">源文件和文件夹</span><span class="sxs-lookup"><span data-stu-id="e2508-124">Source files and folders</span></span>

<span data-ttu-id="e2508-125">源文件和文件夹包含运行 `dotnet new <TEMPLATE>` 命令时用户希望模板引擎使用的任何文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="e2508-125">The source files and folders include whatever files and folders you want the template engine to use when the `dotnet new <TEMPLATE>` command is run.</span></span> <span data-ttu-id="e2508-126">模板引擎旨在将可运行项目用作源代码，以生成项目。</span><span class="sxs-lookup"><span data-stu-id="e2508-126">The template engine is designed to use *runnable projects* as source code to produce projects.</span></span> <span data-ttu-id="e2508-127">这样做有以下几个好处：</span><span class="sxs-lookup"><span data-stu-id="e2508-127">This has several benefits:</span></span>

- <span data-ttu-id="e2508-128">模板引擎不要求用户将特殊令牌注入项目的源代码。</span><span class="sxs-lookup"><span data-stu-id="e2508-128">The template engine doesn't require you to inject special tokens into your project's source code.</span></span>
- <span data-ttu-id="e2508-129">代码文件不必是特殊文件，也不必以任何方式进行修改，即可与模板引擎配合使用。</span><span class="sxs-lookup"><span data-stu-id="e2508-129">The code files aren't special files or modified in any way to work with the template engine.</span></span> <span data-ttu-id="e2508-130">因此，处理项目时通常使用的工具也适用于模板内容。</span><span class="sxs-lookup"><span data-stu-id="e2508-130">So, the tools you normally use when working with projects also work with template content.</span></span>
- <span data-ttu-id="e2508-131">生成、运行和调试模板项目，就像生成、运行和调试其他任何项目一样。</span><span class="sxs-lookup"><span data-stu-id="e2508-131">You build, run, and debug your template projects just like you do for any of your other projects.</span></span>
- <span data-ttu-id="e2508-132">只需将 ./.template.config/template.json 配置文件添加到项目，即可通过现有项目快速创建模板。</span><span class="sxs-lookup"><span data-stu-id="e2508-132">You can quickly create a template from an existing project just by adding a *./.template.config/template.json* configuration file to the project.</span></span>

<span data-ttu-id="e2508-133">模板中存储的文件和文件夹并不限于正式的 .NET 项目类型。</span><span class="sxs-lookup"><span data-stu-id="e2508-133">Files and folders stored in the template aren't limited to formal .NET project types.</span></span> <span data-ttu-id="e2508-134">源文件和文件夹可能包含用户希望在使用模板时创建的任何内容，即使模板引擎仅生成一个文件作为输出也不例外。</span><span class="sxs-lookup"><span data-stu-id="e2508-134">Source files and folders may consist of any content that you wish to create when the template is used, even if the template engine produces just one file as its output.</span></span>

<span data-ttu-id="e2508-135">可以基于在 template.json 配置文件中提供的逻辑和设置对模板生成的文件进行修改。</span><span class="sxs-lookup"><span data-stu-id="e2508-135">Files generated by the template can be modified based on logic and settings you've provided in the *template.json* configuration file.</span></span> <span data-ttu-id="e2508-136">用户可以将选项传递到 `dotnet new <TEMPLATE>` 命令以覆盖这些设置。</span><span class="sxs-lookup"><span data-stu-id="e2508-136">The user can override these settings by passing options to the `dotnet new <TEMPLATE>` command.</span></span> <span data-ttu-id="e2508-137">自定义逻辑的一个常见示例为模板部署的代码文件中的类或变量提供名称。</span><span class="sxs-lookup"><span data-stu-id="e2508-137">A common example of custom logic is providing a name for a class or variable in the code file that's deployed by a template.</span></span>

### <a name="templatejson"></a><span data-ttu-id="e2508-138">template.json</span><span class="sxs-lookup"><span data-stu-id="e2508-138">template.json</span></span>

<span data-ttu-id="e2508-139">template.json 文件位于模板根目录中的 .template.config 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e2508-139">The *template.json* file is placed in a *.template.config* folder in the root directory of the template.</span></span> <span data-ttu-id="e2508-140">此文件向模板引擎提供配置信息。</span><span class="sxs-lookup"><span data-stu-id="e2508-140">The file provides configuration information to the template engine.</span></span> <span data-ttu-id="e2508-141">最低配置必须包含下表中列出的成员，这足以创建功能模板。</span><span class="sxs-lookup"><span data-stu-id="e2508-141">The minimum configuration requires the members shown in the following table, which is sufficient to create a functional template.</span></span>

| <span data-ttu-id="e2508-142">成员</span><span class="sxs-lookup"><span data-stu-id="e2508-142">Member</span></span>            | <span data-ttu-id="e2508-143">类型</span><span class="sxs-lookup"><span data-stu-id="e2508-143">Type</span></span>          | <span data-ttu-id="e2508-144">描述</span><span class="sxs-lookup"><span data-stu-id="e2508-144">Description</span></span> |
| ----------------- | ------------- | ----------- |
| `$schema`         | <span data-ttu-id="e2508-145">URI</span><span class="sxs-lookup"><span data-stu-id="e2508-145">URI</span></span>           | <span data-ttu-id="e2508-146">template.json 文件的 JSON 架构。</span><span class="sxs-lookup"><span data-stu-id="e2508-146">The JSON schema for the *template.json* file.</span></span> <span data-ttu-id="e2508-147">如果指定架构，支持 JSON 架构的编辑器启用 JSON 编辑功能。</span><span class="sxs-lookup"><span data-stu-id="e2508-147">Editors that support JSON schemas enable JSON-editing features when the schema is specified.</span></span> <span data-ttu-id="e2508-148">例如，[Visual Studio Code](https://code.visualstudio.com/) 要求此成员启用 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="e2508-148">For example, [Visual Studio Code](https://code.visualstudio.com/) requires this member to enable IntelliSense.</span></span> <span data-ttu-id="e2508-149">使用值 `http://json.schemastore.org/template`。</span><span class="sxs-lookup"><span data-stu-id="e2508-149">Use a value of `http://json.schemastore.org/template`.</span></span> |
| `author`          | <span data-ttu-id="e2508-150">string</span><span class="sxs-lookup"><span data-stu-id="e2508-150">string</span></span>        | <span data-ttu-id="e2508-151">模板创建者。</span><span class="sxs-lookup"><span data-stu-id="e2508-151">The author of the template.</span></span> |
| `classifications` | <span data-ttu-id="e2508-152">array(string)</span><span class="sxs-lookup"><span data-stu-id="e2508-152">array(string)</span></span> | <span data-ttu-id="e2508-153">为了找到模板，用户可能会在搜索模板时使用的 0 个或多个模板特征。</span><span class="sxs-lookup"><span data-stu-id="e2508-153">Zero or more characteristics of the template that a user might use to find the template when searching for it.</span></span> <span data-ttu-id="e2508-154">如果出现在使用 `dotnet new -l|--list` 命令生成的模板列表中，classifications 还会出现在“Tags”列中。</span><span class="sxs-lookup"><span data-stu-id="e2508-154">The classifications also appear in the *Tags* column when it appears in a list of templates produced by using the `dotnet new -l|--list` command.</span></span> |
| `identity`        | <span data-ttu-id="e2508-155">string</span><span class="sxs-lookup"><span data-stu-id="e2508-155">string</span></span>        | <span data-ttu-id="e2508-156">此模板的唯一名称。</span><span class="sxs-lookup"><span data-stu-id="e2508-156">A unique name for this template.</span></span> |
| `name`            | <span data-ttu-id="e2508-157">string</span><span class="sxs-lookup"><span data-stu-id="e2508-157">string</span></span>        | <span data-ttu-id="e2508-158">用户应看到的模板名称。</span><span class="sxs-lookup"><span data-stu-id="e2508-158">The name for the template that users should see.</span></span> |
| `shortName`       | <span data-ttu-id="e2508-159">string</span><span class="sxs-lookup"><span data-stu-id="e2508-159">string</span></span>        | <span data-ttu-id="e2508-160">方便用户选择模板的默认速记名称，适用于模板名称由用户指定（而不是通过 GUI 选择）的环境。</span><span class="sxs-lookup"><span data-stu-id="e2508-160">A default shorthand name for selecting the template that applies to environments where the template name is specified by the user, not selected via a GUI.</span></span> <span data-ttu-id="e2508-161">例如，通过命令提示符和 CLI 命令使用模板时，短名称非常有用。</span><span class="sxs-lookup"><span data-stu-id="e2508-161">For example, the short name is useful when using templates from a command prompt with CLI commands.</span></span> |
| `sourceName`       | <span data-ttu-id="e2508-162">字符串</span><span class="sxs-lookup"><span data-stu-id="e2508-162">string</span></span>        | <span data-ttu-id="e2508-163">源树中的名称，它即将替换为用户指定的名称。</span><span class="sxs-lookup"><span data-stu-id="e2508-163">The name in the source tree to replace with the name the user specifies.</span></span> <span data-ttu-id="e2508-164">模板引擎将查找配置文件中提及并出现的任何 `sourceName`，并将其替换为文件名和文件内容。</span><span class="sxs-lookup"><span data-stu-id="e2508-164">The template engine will look for any occurrence of the `sourceName` mentioned in the config file and replace it in file names and file contents.</span></span> <span data-ttu-id="e2508-165">可以在运行模板时使用 `-n` 或 `--name` 选项提供要替换的值。</span><span class="sxs-lookup"><span data-stu-id="e2508-165">The value to be replaced with can be given using the `-n` or `--name` options while running a template.</span></span> <span data-ttu-id="e2508-166">如果未指定名称，则使用的是当前目录。</span><span class="sxs-lookup"><span data-stu-id="e2508-166">If no name is specified, the current directory is used.</span></span>|
| `preferNameDirectory`       | <span data-ttu-id="e2508-167">boolean</span><span class="sxs-lookup"><span data-stu-id="e2508-167">boolean</span></span>        | <span data-ttu-id="e2508-168">（如果指定了名称，但未设置输出目录）指示是否为模板创建目录（而不是直接在当前目录中创建内容）。</span><span class="sxs-lookup"><span data-stu-id="e2508-168">Indicates whether to create a directory for the template if name is specified but an output directory is not set (instead of creating the content directly in the current directory).</span></span> <span data-ttu-id="e2508-169">默认值是 False。</span><span class="sxs-lookup"><span data-stu-id="e2508-169">The default value is false.</span></span>|

<span data-ttu-id="e2508-170">template.json 文件的完整架构位于 [JSON 架构存储](http://json.schemastore.org/template)。</span><span class="sxs-lookup"><span data-stu-id="e2508-170">The full schema for the *template.json* file is found at the [JSON Schema Store](http://json.schemastore.org/template).</span></span> <span data-ttu-id="e2508-171">有关 template.json 文件的详细信息，请参阅 [dotnet 创建模板 wiki](https://github.com/dotnet/templating/wiki)。</span><span class="sxs-lookup"><span data-stu-id="e2508-171">For more information about the *template.json* file, see the [dotnet templating wiki](https://github.com/dotnet/templating/wiki).</span></span>

#### <a name="example"></a><span data-ttu-id="e2508-172">示例</span><span class="sxs-lookup"><span data-stu-id="e2508-172">Example</span></span>

<span data-ttu-id="e2508-173">例如，下面是包含两个内容文件的模板文件夹：console.cs 和 readme.txt。</span><span class="sxs-lookup"><span data-stu-id="e2508-173">For example, here is a template folder that contains two content files: *console.cs* and *readme.txt* .</span></span> <span data-ttu-id="e2508-174">请注意，其中有包含 template.json 文件的名为 .template.config 的所需文件夹。</span><span class="sxs-lookup"><span data-stu-id="e2508-174">Take notice that there is the required folder named *.template.config* that contains the *template.json* file.</span></span>

```text
└───mytemplate
    │   console.cs
    │   readme.txt
    │
    └───.template.config
            template.json
```

<span data-ttu-id="e2508-175">template.json 文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="e2508-175">The *template.json* file looks like the following:</span></span>

```json
{
  "$schema": "http://json.schemastore.org/template",
  "author": "Travis Chau",
  "classifications": [ "Common", "Console" ],
  "identity": "AdatumCorporation.ConsoleTemplate.CSharp",
  "name": "Adatum Corporation Console Application",
  "shortName": "adatumconsole"
}
```

<span data-ttu-id="e2508-176">mytemplate 文件夹是可安装的模板包。</span><span class="sxs-lookup"><span data-stu-id="e2508-176">The *mytemplate* folder is an installable template pack.</span></span> <span data-ttu-id="e2508-177">安装此包后，`shortName` 可与 `dotnet new` 命令结合使用。</span><span class="sxs-lookup"><span data-stu-id="e2508-177">Once the pack is installed, the `shortName` can be used with the `dotnet new` command.</span></span> <span data-ttu-id="e2508-178">例如，`dotnet new adatumconsole` 会将 `console.cs` 和 `readme.txt` 文件输出到当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="e2508-178">For example, `dotnet new adatumconsole` would output the `console.cs` and `readme.txt` files to the current folder.</span></span>

## <a name="packing-a-template-into-a-nuget-package-nupkg-file"></a><span data-ttu-id="e2508-179">将模板打包到 NuGet 包（nupkg 文件）</span><span class="sxs-lookup"><span data-stu-id="e2508-179">Packing a template into a NuGet package (nupkg file)</span></span>

<span data-ttu-id="e2508-180">自定义模板与 [dotnet pack](dotnet-pack.md) 命令和 .csproj 文件一起打包。</span><span class="sxs-lookup"><span data-stu-id="e2508-180">A custom template is packed with the [dotnet pack](dotnet-pack.md) command and a *.csproj* file.</span></span> <span data-ttu-id="e2508-181">或者，[NuGet](/nuget/tools/nuget-exe-cli-reference) 可与 [nuget pack](/nuget/tools/cli-ref-pack) 命令以及 .nuspec 文件一起使用。</span><span class="sxs-lookup"><span data-stu-id="e2508-181">Alternatively, [NuGet](/nuget/tools/nuget-exe-cli-reference) can be used with the [nuget pack](/nuget/tools/cli-ref-pack) command along with a *.nuspec* file.</span></span> <span data-ttu-id="e2508-182">但是，NuGet 在 Windows 上需要 .NET Framework，在 Linux 和 macOS 上需要 [Mono](https://www.mono-project.com/)。</span><span class="sxs-lookup"><span data-stu-id="e2508-182">However, NuGet requires the .NET Framework on Windows and [Mono](https://www.mono-project.com/) on Linux and macOS.</span></span>

<span data-ttu-id="e2508-183">该 .csproj 文件与传统代码项目 .csproj 文件略有不同。</span><span class="sxs-lookup"><span data-stu-id="e2508-183">The *.csproj* file is slightly different from a traditional code-project *.csproj* file.</span></span> <span data-ttu-id="e2508-184">请注意以下设置：</span><span class="sxs-lookup"><span data-stu-id="e2508-184">Note the following settings:</span></span>

01. <span data-ttu-id="e2508-185">添加 `<PackageType>` 设置并将其设为 `Template`。</span><span class="sxs-lookup"><span data-stu-id="e2508-185">The `<PackageType>` setting is added and set to `Template`.</span></span>
01. <span data-ttu-id="e2508-186">添加 `<PackageVersion>` 设置并将其设为有效的 [NuGet 版本号](/nuget/reference/package-versioning)。</span><span class="sxs-lookup"><span data-stu-id="e2508-186">The `<PackageVersion>` setting is added and set to a valid [NuGet version number](/nuget/reference/package-versioning).</span></span>
01. <span data-ttu-id="e2508-187">添加 `<PackageId>` 设置并将其设为唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="e2508-187">The `<PackageId>` setting is added and set to a unique identifier.</span></span> <span data-ttu-id="e2508-188">此标识符用于卸载模板包，NuGet 源用它来注册你的模板包。</span><span class="sxs-lookup"><span data-stu-id="e2508-188">This identifier is used to uninstall the template pack and is used by NuGet feeds to register your template pack.</span></span>
01. <span data-ttu-id="e2508-189">应设置泛型元数据设置：`<Title>`、`<Authors>`、`<Description>` 和 `<PackageTags>`。</span><span class="sxs-lookup"><span data-stu-id="e2508-189">Generic metadata settings should be set: `<Title>`, `<Authors>`, `<Description>`, and `<PackageTags>`.</span></span>
01. <span data-ttu-id="e2508-190">必须设置 `<TargetFramework>` 设置，即使未使用模板过程生成的二进制文件也必须设置。</span><span class="sxs-lookup"><span data-stu-id="e2508-190">The `<TargetFramework>` setting must be set, even though the binary produced by the template process isn't used.</span></span> <span data-ttu-id="e2508-191">在下面的示例中，它设置为 `netstandard2.0`。</span><span class="sxs-lookup"><span data-stu-id="e2508-191">In the example below it's set to `netstandard2.0`.</span></span>

<span data-ttu-id="e2508-192">.nupkg NuGet 包形式的模板包要求所有模板都存储在包中的 content 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="e2508-192">A template pack, in the form of a *.nupkg* NuGet package, requires that all templates be stored in the *content* folder within the package.</span></span> <span data-ttu-id="e2508-193">还有几个设置将添加到 .csproj 文件以确保生成的 .nupkg 作为模板包安装：</span><span class="sxs-lookup"><span data-stu-id="e2508-193">There are a few more settings to add to a *.csproj* file to ensure that the generated *.nupkg* can be installed as a template pack:</span></span>

01. <span data-ttu-id="e2508-194">`<IncludeContentInPack>` 设置设为 `true` 以包含项目在 NuGet 包中设为“内容”的任何文件。</span><span class="sxs-lookup"><span data-stu-id="e2508-194">The `<IncludeContentInPack>` setting is set to `true` to include any file the project sets as **content** in the NuGet package.</span></span>
01. <span data-ttu-id="e2508-195">`<IncludeBuildOutput>` 设置设为 `false` 以从 NuGet 包排除编译器生成的所有二进制文件。</span><span class="sxs-lookup"><span data-stu-id="e2508-195">The `<IncludeBuildOutput>` setting is set to `false` to exclude all binaries generated by the compiler from the NuGet package.</span></span>
01. <span data-ttu-id="e2508-196">`<ContentTargetFolders>` 设置设为 `content`。</span><span class="sxs-lookup"><span data-stu-id="e2508-196">The `<ContentTargetFolders>` setting is set to `content`.</span></span> <span data-ttu-id="e2508-197">这可确保设为“内容”的文件存储在 NuGet 包的 content 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="e2508-197">This makes sure that the files set as **content** are stored in the *content* folder in the NuGet package.</span></span> <span data-ttu-id="e2508-198">NuGet 包中的此文件夹由 dotnet 模板系统解析。</span><span class="sxs-lookup"><span data-stu-id="e2508-198">This folder in the NuGet package is parsed by the dotnet template system.</span></span>

<span data-ttu-id="e2508-199">使所有代码文件不被模板项目编译的一个简单的方法是使用 `<ItemGroup>` 元素内项目文件中的 `<Compile Remove="**\*" />` 项。</span><span class="sxs-lookup"><span data-stu-id="e2508-199">An easy way to exclude all code files from being compiled by your template project is by using the `<Compile Remove="**\*" />` item in your project file, inside an `<ItemGroup>` element.</span></span>

<span data-ttu-id="e2508-200">设置模板包结构的一个简单方法是将所有模板放在单独的文件夹中，然后放到位于 .csproj 文件所在目录的 templates 文件夹的每个模板文件夹中 。</span><span class="sxs-lookup"><span data-stu-id="e2508-200">An easy way to structure your template pack is to put all templates in individual folders, and then each template folder inside of a *templates* folder that is located in the same directory as your *.csproj* file.</span></span> <span data-ttu-id="e2508-201">这样，你可以使用单个项目项包括 templates 中的所有文件和文件夹作为“内容”。</span><span class="sxs-lookup"><span data-stu-id="e2508-201">This way, you can use a single project item to include all files and folders in the *templates* as **content** .</span></span> <span data-ttu-id="e2508-202">在 `<ItemGroup>` 元素中创建 `<Content Include="templates\**\*" Exclude="templates\**\bin\**;templates\**\obj\**" />` 项。</span><span class="sxs-lookup"><span data-stu-id="e2508-202">Inside of an `<ItemGroup>` element, create a `<Content Include="templates\**\*" Exclude="templates\**\bin\**;templates\**\obj\**" />` item.</span></span>

<span data-ttu-id="e2508-203">下面是一个遵循上述所有准则的示例 .csproj 文件。</span><span class="sxs-lookup"><span data-stu-id="e2508-203">Here is an example *.csproj* file that follows all of the guidelines above.</span></span> <span data-ttu-id="e2508-204">它将 templates 子文件夹打包为“内容”包文件夹，并使所有代码文件都不被编译。</span><span class="sxs-lookup"><span data-stu-id="e2508-204">It packs the *templates* child folder to the *content* package folder and excludes any code file from being compiled.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <PackageType>Template</PackageType>
    <PackageVersion>1.0</PackageVersion>
    <PackageId>AdatumCorporation.Utility.Templates</PackageId>
    <Title>AdatumCorporation Templates</Title>
    <Authors>Me</Authors>
    <Description>Templates to use when creating an application for Adatum Corporation.</Description>
    <PackageTags>dotnet-new;templates;contoso</PackageTags>
    <TargetFramework>netstandard2.0</TargetFramework>

    <IncludeContentInPack>true</IncludeContentInPack>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <ContentTargetFolders>content</ContentTargetFolders>
  </PropertyGroup>

  <ItemGroup>
    <Content Include="templates\**\*" Exclude="templates\**\bin\**;templates\**\obj\**" />
    <Compile Remove="**\*" />
  </ItemGroup>

</Project>
```

<span data-ttu-id="e2508-205">以下示例演示使用 .csproj 创建模板包的文件和文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="e2508-205">The example below demonstrates the file and folder structure of using a *.csproj* to create a template pack.</span></span> <span data-ttu-id="e2508-206">MyDotnetTemplates.csproj 文件和 templates文件夹都位于名为 project_folder 的根目录中。</span><span class="sxs-lookup"><span data-stu-id="e2508-206">The *MyDotnetTemplates.csproj* file and *templates* folder are both located at the root of a directory named *project_folder* .</span></span> <span data-ttu-id="e2508-207">templates 文件夹包含两个模板 mytemplate1 和 mytemplate2。</span><span class="sxs-lookup"><span data-stu-id="e2508-207">The *templates* folder contains two templates, *mytemplate1* and *mytemplate2* .</span></span> <span data-ttu-id="e2508-208">每个模板具有内容文件和包含 template.json 配置文件的 .template.config 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e2508-208">Each template has content files and a *.template.config* folder with a *template.json* config file.</span></span>

```text
project_folder
│   MyDotnetTemplates.csproj
│
└───templates
    ├───mytemplate1
    │   │   console.cs
    │   │   readme.txt
    │   │
    │   └───.template.config
    │           template.json
    │
    └───mytemplate2
        │   otherfile.cs
        │
        └───.template.config
                template.json
```

## <a name="installing-a-template"></a><span data-ttu-id="e2508-209">安装模板</span><span class="sxs-lookup"><span data-stu-id="e2508-209">Installing a template</span></span>

<span data-ttu-id="e2508-210">使用 [dotnet new -i|--install](dotnet-new.md) 命令以安装包。</span><span class="sxs-lookup"><span data-stu-id="e2508-210">Use the [dotnet new -i|--install](dotnet-new.md) command to install a package.</span></span>

### <a name="to-install-a-template-from-a-nuget-package-stored-at-nugetorg"></a><span data-ttu-id="e2508-211">从 nuget.org 中存储的 NuGet 包安装模板的具体步骤</span><span class="sxs-lookup"><span data-stu-id="e2508-211">To install a template from a NuGet package stored at nuget.org</span></span>

<span data-ttu-id="e2508-212">使用 NuGet 包标识符安装模板包。</span><span class="sxs-lookup"><span data-stu-id="e2508-212">Use the NuGet package identifier to install a template package.</span></span>

```dotnetcli
dotnet new -i <NUGET_PACKAGE_ID>
```

### <a name="to-install-a-template-from-a-local-nupkg-file"></a><span data-ttu-id="e2508-213">从本地 nupkg 文件安装模板的具体步骤</span><span class="sxs-lookup"><span data-stu-id="e2508-213">To install a template from a local nupkg file</span></span>

<span data-ttu-id="e2508-214">提供指向 .nupkg NuGet 包文件的路径。</span><span class="sxs-lookup"><span data-stu-id="e2508-214">Provide the path to a *.nupkg* NuGet package file.</span></span>

```dotnetcli
dotnet new -i <PATH_TO_NUPKG_FILE>
```

### <a name="to-install-a-template-from-a-file-system-directory"></a><span data-ttu-id="e2508-215">从文件系统目录安装模板的具体步骤</span><span class="sxs-lookup"><span data-stu-id="e2508-215">To install a template from a file system directory</span></span>

<span data-ttu-id="e2508-216">模板可从模板文件夹安装，如以上示例中的 mytemplate1 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e2508-216">Templates can be installed from a template folder, such as the *mytemplate1* folder from the example above.</span></span> <span data-ttu-id="e2508-217">指定 .template.config 文件夹的文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="e2508-217">Specify the folder path of the *.template.config* folder.</span></span> <span data-ttu-id="e2508-218">模板目录的路径不需要是绝对路径。</span><span class="sxs-lookup"><span data-stu-id="e2508-218">The path to the template directory does not need to be absolute.</span></span> <span data-ttu-id="e2508-219">但是，卸载从文件夹安装的模板时需要绝对路径。</span><span class="sxs-lookup"><span data-stu-id="e2508-219">However, an absolute path is required to uninstall a template that is installed from a folder.</span></span>

```dotnetcli
dotnet new -i <FILE_SYSTEM_DIRECTORY>
```

## <a name="get-a-list-of-installed-templates"></a><span data-ttu-id="e2508-220">获取已安装模板的列表</span><span class="sxs-lookup"><span data-stu-id="e2508-220">Get a list of installed templates</span></span>

<span data-ttu-id="e2508-221">在没有任何其他参数的情况下，卸载命令将列出所有已安装的模板。</span><span class="sxs-lookup"><span data-stu-id="e2508-221">The uninstall command, without any other parameters, will list all installed templates.</span></span>

```dotnetcli
dotnet new -u
```

<span data-ttu-id="e2508-222">该命令返回如下所示的输出：</span><span class="sxs-lookup"><span data-stu-id="e2508-222">That command returns something similar to the following output:</span></span>

```console
Template Instantiation Commands for .NET Core CLI

Currently installed items:
  Microsoft.DotNet.Common.ItemTemplates
    Templates:
      global.json file (globaljson)
      NuGet Config (nugetconfig)
      Solution File (sln)
      Dotnet local tool manifest file (tool-manifest)
      Web Config (webconfig)
  Microsoft.DotNet.Common.ProjectTemplates.3.0
    Templates:
      Class library (classlib) C#
      Class library (classlib) F#
      Class library (classlib) VB
      Console Application (console) C#
      Console Application (console) F#
      Console Application (console) VB
...
```

<span data-ttu-id="e2508-223">`Currently installed items:` 后面的第一级项是用于卸载模板的标识符。</span><span class="sxs-lookup"><span data-stu-id="e2508-223">The first level of items after `Currently installed items:` are the identifiers used in uninstalling a template.</span></span> <span data-ttu-id="e2508-224">在上述示例中，列出了 `Microsoft.DotNet.Common.ItemTemplates` 和 `Microsoft.DotNet.Common.ProjectTemplates.3.0`。</span><span class="sxs-lookup"><span data-stu-id="e2508-224">And in the example above, `Microsoft.DotNet.Common.ItemTemplates` and `Microsoft.DotNet.Common.ProjectTemplates.3.0` are listed.</span></span> <span data-ttu-id="e2508-225">如果使用文件系统路径安装模板，此标识符将是 .template.config 文件夹的文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="e2508-225">If the template was installed by using a file system path, this identifier will the folder path of the *.template.config* folder.</span></span>

## <a name="uninstalling-a-template"></a><span data-ttu-id="e2508-226">卸载模板</span><span class="sxs-lookup"><span data-stu-id="e2508-226">Uninstalling a template</span></span>

<span data-ttu-id="e2508-227">使用 [dotnet new -u|--uninstall](dotnet-new.md) 命令卸载包。</span><span class="sxs-lookup"><span data-stu-id="e2508-227">Use the [dotnet new -u|--uninstall](dotnet-new.md) command to uninstall a package.</span></span>

<span data-ttu-id="e2508-228">如果通过 NuGet 源或直接通过 .nupkg 文件安装包，请提供标识符。</span><span class="sxs-lookup"><span data-stu-id="e2508-228">If the package was installed by either a NuGet feed or by a *.nupkg* file directly, provide the identifier.</span></span>

```dotnetcli
dotnet new -u <NUGET_PACKAGE_ID>
```

<span data-ttu-id="e2508-229">如果通过指定 .template.config 文件夹的路径安装包，请使用该绝对路径卸载包。</span><span class="sxs-lookup"><span data-stu-id="e2508-229">If the package was installed by specifying a path to the *.template.config* folder, use that **absolute** path to uninstall the package.</span></span> <span data-ttu-id="e2508-230">你可以在 `dotnet new -u` 命令提供的输出中看到模板的绝对路径。</span><span class="sxs-lookup"><span data-stu-id="e2508-230">You can see the absolute path of the template in the output provided by the `dotnet new -u` command.</span></span> <span data-ttu-id="e2508-231">有关详细信息，请参阅上文的[获取已安装的模板列表](#get-a-list-of-installed-templates)部分。</span><span class="sxs-lookup"><span data-stu-id="e2508-231">For more information, see the [Get a list of installed templates](#get-a-list-of-installed-templates) section above.</span></span>

```dotnetcli
dotnet new -u <ABSOLUTE_FILE_SYSTEM_DIRECTORY>
```

## <a name="create-a-project-using-a-custom-template"></a><span data-ttu-id="e2508-232">使用自定义模板创建项目</span><span class="sxs-lookup"><span data-stu-id="e2508-232">Create a project using a custom template</span></span>

<span data-ttu-id="e2508-233">安装模板后，通过执行 `dotnet new <TEMPLATE>` 命令来使用模板，就像使用其他任何预安装模板一样。</span><span class="sxs-lookup"><span data-stu-id="e2508-233">After a template is installed, use the template by executing the `dotnet new <TEMPLATE>` command as you would with any other pre-installed template.</span></span> <span data-ttu-id="e2508-234">还可以为 `dotnet new` 命令指定[选项](dotnet-new.md#options)，包括在模板设置中配置的模板专用选项。</span><span class="sxs-lookup"><span data-stu-id="e2508-234">You can also specify [options](dotnet-new.md#options) to the `dotnet new` command, including template-specific options you configured in the template settings.</span></span> <span data-ttu-id="e2508-235">直接向命令提供模板的短名称：</span><span class="sxs-lookup"><span data-stu-id="e2508-235">Supply the template's short name directly to the command:</span></span>

```dotnetcli
dotnet new <TEMPLATE>
```

## <a name="see-also"></a><span data-ttu-id="e2508-236">请参阅</span><span class="sxs-lookup"><span data-stu-id="e2508-236">See also</span></span>

- [<span data-ttu-id="e2508-237">创建 dotnet new 自定义模板（教程）</span><span class="sxs-lookup"><span data-stu-id="e2508-237">Create a custom template for dotnet new (tutorial)</span></span>](../tutorials/cli-templates-create-item-template.md)
- [<span data-ttu-id="e2508-238">dotnet/templating GitHub 存储库 Wiki</span><span class="sxs-lookup"><span data-stu-id="e2508-238">dotnet/templating GitHub repo Wiki</span></span>](https://github.com/dotnet/templating/wiki)
- [<span data-ttu-id="e2508-239">dotnet/dotnet-template-samples GitHub 存储库</span><span class="sxs-lookup"><span data-stu-id="e2508-239">dotnet/dotnet-template-samples GitHub repo</span></span>](https://github.com/dotnet/dotnet-template-samples)
- [<span data-ttu-id="e2508-240">如何创建自己的 dotnet new 模板</span><span class="sxs-lookup"><span data-stu-id="e2508-240">How to create your own templates for dotnet new</span></span>](https://devblogs.microsoft.com/dotnet/how-to-create-your-own-templates-for-dotnet-new/)
- [<span data-ttu-id="e2508-241">JSON 架构存储中的 template.json 架构</span><span class="sxs-lookup"><span data-stu-id="e2508-241">*template.json* schema at the JSON Schema Store</span></span>](http://json.schemastore.org/template)
