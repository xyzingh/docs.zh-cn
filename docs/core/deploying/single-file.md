---
title: 单文件应用程序
description: 了解单文件应用程序的本质以及应考虑使用此应用程序部署模型的原因。
author: lakshanf
ms.author: lakshanf
ms.date: 08/28/2020
ms.openlocfilehash: 16e9586cfc29072fa2ca70dc482272a5a0e7306a
ms.sourcegitcommit: 39b1d5f2978be15409c189a66ab30781d9082cd8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2020
ms.locfileid: "92050411"
---
# <a name="single-file-deployment-and-executable"></a><span data-ttu-id="348da-103">单文件部署和可执行文件</span><span class="sxs-lookup"><span data-stu-id="348da-103">Single file deployment and executable</span></span>

<span data-ttu-id="348da-104">通过将所有依赖应用程序的文件捆绑到一个二进制文件中，为应用程序开发人员提供一个具有吸引力的选项，那就是将应用程序作为单个文件进行部署和分发。</span><span class="sxs-lookup"><span data-stu-id="348da-104">Bundling all application-dependent files into a single binary provides an application developer with the attractive option to deploy and distribute the application as a single file.</span></span> <span data-ttu-id="348da-105">此部署模型从 .NET Core 3.0 开始提供，在 .NET 5.0 中进行了增强。</span><span class="sxs-lookup"><span data-stu-id="348da-105">This deployment model has been available since .NET Core 3.0 and has been enhanced in .NET 5.0.</span></span> <span data-ttu-id="348da-106">之前在 .NET Core 3.0 中，当用户运行单文件应用时，.NET Core 主机先将所有文件提取到一个临时目录，然后再运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="348da-106">Previously in .NET Core 3.0, when a user runs your single-file app, .NET Core host first extracts all files to a temporary directory before running the application.</span></span> <span data-ttu-id="348da-107">.NET 5.0 改进了这一体验，它可直接运行代码，无需从应用中提取文件。</span><span class="sxs-lookup"><span data-stu-id="348da-107">.NET 5.0 improves this experience by directly running the code without the need to extract the files from the app.</span></span>

<span data-ttu-id="348da-108">单文件部署可用于[依赖框架的部署模型](index.md#publish-framework-dependent)和[独立应用程序](index.md#publish-self-contained)。</span><span class="sxs-lookup"><span data-stu-id="348da-108">Single File deployment is available for both the [framework-dependent deployment model](index.md#publish-framework-dependent) and [self-contained applications](index.md#publish-self-contained).</span></span> <span data-ttu-id="348da-109">独立应用程序中单个文件的大小很大，因为它包含运行时和框架库。</span><span class="sxs-lookup"><span data-stu-id="348da-109">The size of the single file in a self-contained application will be large since it will include the runtime and the framework libraries.</span></span> <span data-ttu-id="348da-110">单文件部署选项可与 [ReadyToRun](ready-to-run.md) 和 [Trim（.NET 5.0 中的一项试验功能）](trim-self-contained.md)发布选项结合使用。</span><span class="sxs-lookup"><span data-stu-id="348da-110">The single file deployment option can be combined with [ReadyToRun](ready-to-run.md) and [Trim (an experimental feature in .NET 5.0)](trim-self-contained.md) publish options.</span></span>

## <a name="api-incompatibility"></a><span data-ttu-id="348da-111">API 不兼容</span><span class="sxs-lookup"><span data-stu-id="348da-111">API incompatibility</span></span>

<span data-ttu-id="348da-112">某些 API 与单文件部署不兼容，如果应用程序使用这些 API，可能需要进行修改。</span><span class="sxs-lookup"><span data-stu-id="348da-112">Some APIs are not compatible with single-file deployment and applications may require modification if they use these APIs.</span></span> <span data-ttu-id="348da-113">如果使用第三方框架或包，则它们也可能使用了这样的 API 并需要修改。</span><span class="sxs-lookup"><span data-stu-id="348da-113">If you use a third-party framework or package, it's possible that they may also use one of these APIs and need modification.</span></span> <span data-ttu-id="348da-114">出现问题的最常见原因是依赖于应用程序附带的文件或 DLL 的文件路径。</span><span class="sxs-lookup"><span data-stu-id="348da-114">The most common cause of problems is dependence on file paths for files or DLLs shipped with the application.</span></span>

<span data-ttu-id="348da-115">下表提供了用于单文件的相关运行时库 API 详细信息。</span><span class="sxs-lookup"><span data-stu-id="348da-115">The table below has the relevant runtime library API details for single-file use.</span></span>

| <span data-ttu-id="348da-116">API</span><span class="sxs-lookup"><span data-stu-id="348da-116">API</span></span>                            | <span data-ttu-id="348da-117">注意</span><span class="sxs-lookup"><span data-stu-id="348da-117">Note</span></span>                                                                   |
|--------------------------------|------------------------------------------------------------------------|
| `Assembly.Location`            | <span data-ttu-id="348da-118">返回空字符串。</span><span class="sxs-lookup"><span data-stu-id="348da-118">Returns an empty string.</span></span>                                               |
| `Module.FullyQualifiedName`    | <span data-ttu-id="348da-119">返回值为 `<Unknown>` 的字符串，或引发异常。</span><span class="sxs-lookup"><span data-stu-id="348da-119">Returns a string with the value of `<Unknown>` or throws an exception.</span></span> |
| `Module.Name`                  | <span data-ttu-id="348da-120">返回值为 `<Unknown>` 的字符串。</span><span class="sxs-lookup"><span data-stu-id="348da-120">Returns a string with the value of `<Unknown>`.</span></span>                        |
| `Assembly.GetFile`             | <span data-ttu-id="348da-121">引发 <xref:System.IO.IOException>。</span><span class="sxs-lookup"><span data-stu-id="348da-121">Throws <xref:System.IO.IOException>.</span></span>                                   |
| `Assembly.GetFiles`            | <span data-ttu-id="348da-122">引发 <xref:System.IO.IOException>。</span><span class="sxs-lookup"><span data-stu-id="348da-122">Throws <xref:System.IO.IOException>.</span></span>                                   |
| `Assembly.CodeBase`            | <span data-ttu-id="348da-123">引发 <xref:System.PlatformNotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="348da-123">Throws <xref:System.PlatformNotSupportedException>.</span></span>                    |
| `Assembly.EscapedCodeBase`     | <span data-ttu-id="348da-124">引发 <xref:System.PlatformNotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="348da-124">Throws <xref:System.PlatformNotSupportedException>.</span></span>                    |
| `AssemblyName.CodeBase`        | <span data-ttu-id="348da-125">返回 `null`。</span><span class="sxs-lookup"><span data-stu-id="348da-125">Returns `null`.</span></span>                                                        |
| `AssemblyName.EscapedCodeBase` | <span data-ttu-id="348da-126">返回 `null`。</span><span class="sxs-lookup"><span data-stu-id="348da-126">Returns `null`.</span></span>                                                        |

<span data-ttu-id="348da-127">我们提供了关于修复常见问题的一些建议：</span><span class="sxs-lookup"><span data-stu-id="348da-127">We have some recommendations for fixing common scenarios:</span></span>

* <span data-ttu-id="348da-128">若要访问可执行文件旁边的文件，请使用 <xref:System.AppContext.BaseDirectory?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="348da-128">To access files next to the executable, use <xref:System.AppContext.BaseDirectory?displayProperty=nameWithType>.</span></span>

* <span data-ttu-id="348da-129">若要查找可执行文件的文件名，请使用 <xref:System.Environment.GetCommandLineArgs?displayProperty=nameWithType> 的第一个元素。</span><span class="sxs-lookup"><span data-stu-id="348da-129">To find the file name of the executable, use the first element of <xref:System.Environment.GetCommandLineArgs?displayProperty=nameWithType>.</span></span>

* <span data-ttu-id="348da-130">若要避免完全发送松散文件，请考虑使用[嵌入的资源](../../framework/resources/creating-resource-files-for-desktop-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="348da-130">To avoid shipping loose files entirely, consider using [embedded resources](../../framework/resources/creating-resource-files-for-desktop-apps.md).</span></span>

## <a name="attaching-a-debugger"></a><span data-ttu-id="348da-131">附加调试器</span><span class="sxs-lookup"><span data-stu-id="348da-131">Attaching a debugger</span></span>

<span data-ttu-id="348da-132">在 Linux 上，可以附加到自包含单文件进程或调试故障转储的唯一调试器是[有 LLDB 的 SOS](../diagnostics/dotnet-sos.md)。</span><span class="sxs-lookup"><span data-stu-id="348da-132">On Linux, the only debugger which can attach to self-contained single-file processes or debug crash dumps is [SOS with LLDB](../diagnostics/dotnet-sos.md).</span></span>

<span data-ttu-id="348da-133">在 Windows 和 Mac 上，可以使用 Visual Studio 和 VS Code 调试故障转储。</span><span class="sxs-lookup"><span data-stu-id="348da-133">On Windows and Mac, Visual Studio and VS Code can be used to debug crash dumps.</span></span> <span data-ttu-id="348da-134">要附加到运行自包含单文件可执行文件，需要额外的文件：_mscordbi.{dll,so}_</span><span class="sxs-lookup"><span data-stu-id="348da-134">Attaching to a running self-contained single-file executable requires an extra file: _mscordbi.{dll,so}_.</span></span>

<span data-ttu-id="348da-135">如果没有此文件，Visual Studio 可能会生成错误“无法附加到进程。</span><span class="sxs-lookup"><span data-stu-id="348da-135">Without this file Visual Studio may produce the error "Unable to attach to the process.</span></span> <span data-ttu-id="348da-136">未安装调试组件。”</span><span class="sxs-lookup"><span data-stu-id="348da-136">A debug component is not installed."</span></span> <span data-ttu-id="348da-137">而 VS Code 可能生成错误“未能附加到进程:未知错误:0x80131c3c。”</span><span class="sxs-lookup"><span data-stu-id="348da-137">and VS Code may produce the error "Failed to attach to process: Unknown Error: 0x80131c3c."</span></span>

<span data-ttu-id="348da-138">若要修复这些错误，需要将 mscordbi 复制到可执行文件旁边。</span><span class="sxs-lookup"><span data-stu-id="348da-138">To fix these errors, _mscordbi_ needs to be copied next to the executable.</span></span> <span data-ttu-id="348da-139">mscordbi 默认 `publish` 到具有应用程序运行时 ID 的子目录中。</span><span class="sxs-lookup"><span data-stu-id="348da-139">_mscordbi_ is `publish`ed by default in the subdirectory with the application's runtime ID.</span></span> <span data-ttu-id="348da-140">例如，如果使用适用于 Windows 的 `dotnet` CLI 并使用 `-r win-x64` 参数发布自包含单文件可执行文件，则可执行文件将置于 bin/Debug/net5.0/win-x64/publish 中。</span><span class="sxs-lookup"><span data-stu-id="348da-140">So, for example, if one were to publish a self-contained single-file executable using the `dotnet` CLI for Windows using the parameters `-r win-x64`, the executable would be placed in _bin/Debug/net5.0/win-x64/publish_.</span></span> <span data-ttu-id="348da-141">mscordbi.dll 的副本将存在于 bin/Debug/net5.0/win-x64 中。 </span><span class="sxs-lookup"><span data-stu-id="348da-141">A copy of _mscordbi.dll_ would be present in _bin/Debug/net5.0/win-x64_.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="348da-142">其他注意事项</span><span class="sxs-lookup"><span data-stu-id="348da-142">Other considerations</span></span>

<span data-ttu-id="348da-143">默认情况下，单文件不捆绑本机库。</span><span class="sxs-lookup"><span data-stu-id="348da-143">Single-file doesn't bundle native libraries by default.</span></span> <span data-ttu-id="348da-144">在 Linux 上，我们将运行时预链接到捆绑包中，并且仅将应用程序本机库部署到单文件应用所在的目录中。</span><span class="sxs-lookup"><span data-stu-id="348da-144">On Linux, we prelink the runtime into the bundle and only application native libraries are deployed to the same directory as the single-file app.</span></span> <span data-ttu-id="348da-145">在 Windows 上，我们仅预链接托管代码，而且运行时库和应用程序本机库都部署到单文件应用所在的目录中。</span><span class="sxs-lookup"><span data-stu-id="348da-145">On Windows, we prelink only the hosting code and both the runtime and application native libraries are deployed to the same directory as the single-file app.</span></span> <span data-ttu-id="348da-146">目的是确保提供良好的调试体验，这要求将本机文件从单文件中排除。</span><span class="sxs-lookup"><span data-stu-id="348da-146">This is to ensure a good debugging experience, which requires native files to be excluded from the single file.</span></span> <span data-ttu-id="348da-147">可选择设置标志 `IncludeNativeLibrariesForSelfExtract`，从而在单文件捆绑包中包含本机库，但在运行单文件应用程序时，这些文件将被提取到客户端计算机上的临时目录中。</span><span class="sxs-lookup"><span data-stu-id="348da-147">There is an option to set a flag, `IncludeNativeLibrariesForSelfExtract`, to include native libraries in the single file bundle, but these files will be extracted to a temporary directory in the client machine when the single file application is run.</span></span>

<span data-ttu-id="348da-148">单文件应用程序旁边将具有所有相关的 PDB 文件，并且默认情况下不会绑定。</span><span class="sxs-lookup"><span data-stu-id="348da-148">Single-file application will have all related PDB files alongside it and will not be bundled by default.</span></span> <span data-ttu-id="348da-149">如果要在生成的项目的程序集内包含 PDB，请将 `DebugType` 设置为 `embedded`，如[下方](#include-pdb-files-inside-the-bundle)所详述。</span><span class="sxs-lookup"><span data-stu-id="348da-149">If you want to include PDBs inside the assembly for projects you build, set the `DebugType` to `embedded` as described [below](#include-pdb-files-inside-the-bundle) in detail.</span></span>

<span data-ttu-id="348da-150">托管的 C++ 应组件不太适合进行单文件部署，建议使用 C# 或其他非托管 C++ 语言编写应用程序来实现单文件兼容。</span><span class="sxs-lookup"><span data-stu-id="348da-150">Managed C++ components aren't well suited for single-file deployment and we recommend that you write applications in C# or another non-managed C++ language to be single-file compatible.</span></span>

## <a name="exclude-files-from-being-embedded"></a><span data-ttu-id="348da-151">将文件排除在嵌入之外</span><span class="sxs-lookup"><span data-stu-id="348da-151">Exclude files from being embedded</span></span>

<span data-ttu-id="348da-152">通过设置以下元数据，可明确指定不在单文件中嵌入某些文件：</span><span class="sxs-lookup"><span data-stu-id="348da-152">Certain files can be explicitly excluded from being embedded in the single-file by setting following metadata:</span></span>

```xml
<ExcludeFromSingleFile>true</ExcludeFromSingleFile>
```

<span data-ttu-id="348da-153">例如，若要将某些文件放置在发布目录中，但不将它们捆绑到单文件中：</span><span class="sxs-lookup"><span data-stu-id="348da-153">For example, to place some files in the publish directory but not bundle them in the single-file:</span></span>

```xml
<ItemGroup>
  <Content Update="Plugin.dll">
    <CopyToPublishDirectory>PreserveNewest</CopyToPublishDirectory>
    <ExcludeFromSingleFile>true</ExcludeFromSingleFile>
  </Content>
</ItemGroup>
```

## <a name="include-pdb-files-inside-the-bundle"></a><span data-ttu-id="348da-154">在绑定内包括 PDB 文件</span><span class="sxs-lookup"><span data-stu-id="348da-154">Include PDB files inside the bundle</span></span>

<span data-ttu-id="348da-155">可以使用下面的设置将程序集的 PDB 文件嵌入到程序集本身 (`.dll`)。</span><span class="sxs-lookup"><span data-stu-id="348da-155">The PDB file for an assembly can be embedded into the assembly itself (the `.dll`) using the setting below.</span></span> <span data-ttu-id="348da-156">由于符号是程序集的一部分，因此，它们也会是单文件应用程序的一部分：</span><span class="sxs-lookup"><span data-stu-id="348da-156">Since the symbols are part of the assembly, they will be part of the single-file application as well:</span></span>

```xml
<DebugType>embedded</DebugType>
```

<span data-ttu-id="348da-157">例如，将以下属性添加到程序集的项目文件，以将 PDB 文件嵌入到该程序集：</span><span class="sxs-lookup"><span data-stu-id="348da-157">For example, add the following property to the project file of an assembly to embed the PDB file to that assembly:</span></span>

```xml
<PropertyGroup>
  <DebugType>embedded</DebugType>
</PropertyGroup>
```

## <a name="publish-a-single-file-app---cli"></a><span data-ttu-id="348da-158">发布单文件应用 - CLI</span><span class="sxs-lookup"><span data-stu-id="348da-158">Publish a single file app - CLI</span></span>

<span data-ttu-id="348da-159">使用 [dotnet publish](../tools/dotnet-publish.md) 命令发布单文件应用程序。</span><span class="sxs-lookup"><span data-stu-id="348da-159">Publish a single file application using the [dotnet publish](../tools/dotnet-publish.md) command.</span></span> <span data-ttu-id="348da-160">发布应用时，请设置以下属性：</span><span class="sxs-lookup"><span data-stu-id="348da-160">When you publish your app, set the following properties:</span></span>

- <span data-ttu-id="348da-161">针对特定运行时进行发布：`-r win-x64`</span><span class="sxs-lookup"><span data-stu-id="348da-161">Publish for a specific runtime: `-r win-x64`</span></span>
- <span data-ttu-id="348da-162">作为单个文件进行发布：`-p:PublishSingleFile=true`</span><span class="sxs-lookup"><span data-stu-id="348da-162">Publish as a single-file: `-p:PublishSingleFile=true`</span></span>

<span data-ttu-id="348da-163">以下示例将 Windows 应用作为独立的单文件应用程序发布。</span><span class="sxs-lookup"><span data-stu-id="348da-163">The following example publishes an app for Windows as a self-contained single file application.</span></span>

```dotnetcli
dotnet publish -r win-x64 -p:PublishSingleFile=true --self-contained true
```

<span data-ttu-id="348da-164">以下示例将 Linux 应用作为依赖框架的单文件应用程序发布。</span><span class="sxs-lookup"><span data-stu-id="348da-164">The following example publishes an app for Linux as a framework dependent single file application.</span></span>

```dotnetcli
dotnet publish -r linux-x64 -p:PublishSingleFile=true --self-contained false
```

<span data-ttu-id="348da-165">有关详细信息，请参阅[使用 .NET Core CLI 发布 .NET Core 应用](deploy-with-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="348da-165">For more information, see [Publish .NET Core apps with .NET Core CLI](deploy-with-cli.md).</span></span>

## <a name="publish-a-single-file-app---visual-studio"></a><span data-ttu-id="348da-166">发布单文件应用 - Visual Studio</span><span class="sxs-lookup"><span data-stu-id="348da-166">Publish a single file app - Visual Studio</span></span>

<span data-ttu-id="348da-167">Visual Studio 创建可重用的发布配置文件，用于控制应用程序的发布方式。</span><span class="sxs-lookup"><span data-stu-id="348da-167">Visual Studio creates reusable publishing profiles that control how your application is published.</span></span>

01. <span data-ttu-id="348da-168">在“解决方案资源管理器”窗格中，右键单击要发布的项目  。</span><span class="sxs-lookup"><span data-stu-id="348da-168">On the **Solution Explorer** pane, right-click on the project you want to publish.</span></span> <span data-ttu-id="348da-169">选择“发布”。</span><span class="sxs-lookup"><span data-stu-id="348da-169">Select **Publish**.</span></span>

    :::image type="content" source="media/single-file/visual-studio-solution-explorer.png" alt-text="解决方案资源管理器，其中右键单击菜单突出显示了“发布”选项。":::

    <span data-ttu-id="348da-171">如果还没有发布配置文件，请按照说明创建一个并选择“文件夹”目标类型  。</span><span class="sxs-lookup"><span data-stu-id="348da-171">If you don't already have a publishing profile, follow the instructions to create one and choose the **Folder** target-type.</span></span>

01. <span data-ttu-id="348da-172">选择“编辑”  。</span><span class="sxs-lookup"><span data-stu-id="348da-172">Choose **Edit**.</span></span>

    :::image type="content" source="media/single-file/visual-studio-publish-edit-settings.png" alt-text="解决方案资源管理器，其中右键单击菜单突出显示了“发布”选项。":::

01. <span data-ttu-id="348da-174">在“配置文件设置”对话框中，设置以下选项  ：</span><span class="sxs-lookup"><span data-stu-id="348da-174">In the **Profile settings** dialog, set the following options:</span></span>

    - <span data-ttu-id="348da-175">将“部署模式”设置为“自包含”   。</span><span class="sxs-lookup"><span data-stu-id="348da-175">Set **Deployment mode** to **Self-contained**.</span></span>
    - <span data-ttu-id="348da-176">将“目标运行时”设置为要发布到的平台  。</span><span class="sxs-lookup"><span data-stu-id="348da-176">Set **Target runtime** to the platform you want to publish to.</span></span>
    - <span data-ttu-id="348da-177">选择“生成单个文件”。</span><span class="sxs-lookup"><span data-stu-id="348da-177">Select **Produce single file**.</span></span>

    <span data-ttu-id="348da-178">选择“保存”保存设置并返回到“发布”对话框   。</span><span class="sxs-lookup"><span data-stu-id="348da-178">Choose **Save** to save the settings and return to the **Publish** dialog.</span></span>

    :::image type="content" source="media/single-file/visual-studio-publish-single-file-properties.png" alt-text="解决方案资源管理器，其中右键单击菜单突出显示了“发布”选项。":::

01. <span data-ttu-id="348da-180">选择“发布”，将应用作为单个文件发布。</span><span class="sxs-lookup"><span data-stu-id="348da-180">Choose **Publish** to publish your app as a single file.</span></span>

<span data-ttu-id="348da-181">有关详细信息，请参阅[使用 Visual Studio 发布 .NET Core 应用](deploy-with-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="348da-181">For more information, see [Publish .NET Core apps with Visual Studio](deploy-with-vs.md).</span></span>

## <a name="publish-a-single-file-app---visual-studio-for-mac"></a><span data-ttu-id="348da-182">发布单文件应用 - Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="348da-182">Publish a single file app - Visual Studio for Mac</span></span>

<span data-ttu-id="348da-183">Visual Studio for Mac 不提供将应用作为单个文件发布的选项。</span><span class="sxs-lookup"><span data-stu-id="348da-183">Visual Studio for Mac doesn't provide options to publish your app as a single file.</span></span> <span data-ttu-id="348da-184">你需要按照[发布单文件应用 - CLI](#publish-a-single-file-app---cli) 部分中的说明手动发布。</span><span class="sxs-lookup"><span data-stu-id="348da-184">You'll need to publish manually by following the instructions from the [Publish a single file app - CLI](#publish-a-single-file-app---cli) section.</span></span> <span data-ttu-id="348da-185">有关详细信息，请参阅[使用 .NET Core CLI 发布 .NET Core 应用](deploy-with-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="348da-185">For more information, see [Publish .NET Core apps with .NET Core CLI](deploy-with-cli.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="348da-186">请参阅</span><span class="sxs-lookup"><span data-stu-id="348da-186">See also</span></span>

- <span data-ttu-id="348da-187">[.NET Core 应用程序部署](index.md)。</span><span class="sxs-lookup"><span data-stu-id="348da-187">[.NET Core application deployment](index.md).</span></span>
- <span data-ttu-id="348da-188">[使用 .NET Core CLI 发布 .NET Core 应用](deploy-with-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="348da-188">[Publish .NET Core apps with .NET Core CLI](deploy-with-cli.md).</span></span>
- <span data-ttu-id="348da-189">[使用 Visual Studio 发布 .NET Core 应用](deploy-with-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="348da-189">[Publish .NET Core apps with Visual Studio](deploy-with-vs.md).</span></span>
- <span data-ttu-id="348da-190">[`dotnet publish` 命令](../tools/dotnet-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="348da-190">[`dotnet publish` command](../tools/dotnet-publish.md).</span></span>
