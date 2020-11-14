---
title: 全球化和 ICU
ms.date: 05/21/2020
ms.technology: dotnet-standard
helpviewer_keywords:
- globalization [.NET], about globalization
- global applications, globalization
- international applications [.NET], globalization
- world-ready applications, globalization
- application development [.NET], globalization
- culture, globalization
- icu, icu on windows, ms-icu
ms.openlocfilehash: e0ca78871d1ddf851148096c8c6cfd10076763ab
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400874"
---
# <a name="net-globalization-and-icu"></a><span data-ttu-id="8cf74-102">.NET 全球化和 ICU</span><span class="sxs-lookup"><span data-stu-id="8cf74-102">.NET globalization and ICU</span></span>

<span data-ttu-id="8cf74-103">过去，.NET 全球化 API 在不同的平台上使用不同的基础库。</span><span class="sxs-lookup"><span data-stu-id="8cf74-103">In the past, the .NET globalization APIs used different underlying libraries on different platforms.</span></span> <span data-ttu-id="8cf74-104">在 Unix 上，API 使用 [Unicode 国际组件 (ICU)](http://site.icu-project.org/home)，在 Windows 上，API 使用 [区域语言支持 (NLS)](/windows/win32/intl/national-language-support)。</span><span class="sxs-lookup"><span data-stu-id="8cf74-104">On Unix, the APIs used [International Components for Unicode (ICU)](http://site.icu-project.org/home), and on Windows, they used [National Language Support (NLS)](/windows/win32/intl/national-language-support).</span></span> <span data-ttu-id="8cf74-105">这导致在不同平台上运行应用程序时，在少数全球化 API 中存在一些行为差异。</span><span class="sxs-lookup"><span data-stu-id="8cf74-105">This resulted in some behavioral differences in a handful of globalization APIs when running applications on different platforms.</span></span> <span data-ttu-id="8cf74-106">以下方面就存在明显的行为差异：</span><span class="sxs-lookup"><span data-stu-id="8cf74-106">Behavior differences were evident in these areas:</span></span>

- <span data-ttu-id="8cf74-107">区域性和区域性数据</span><span class="sxs-lookup"><span data-stu-id="8cf74-107">Cultures and culture data</span></span>
- <span data-ttu-id="8cf74-108">字符串大小写</span><span class="sxs-lookup"><span data-stu-id="8cf74-108">String casing</span></span>
- <span data-ttu-id="8cf74-109">字符串排序和搜索</span><span class="sxs-lookup"><span data-stu-id="8cf74-109">String sorting and searching</span></span>
- <span data-ttu-id="8cf74-110">排序关键字</span><span class="sxs-lookup"><span data-stu-id="8cf74-110">Sort keys</span></span>
- <span data-ttu-id="8cf74-111">字符串规范化</span><span class="sxs-lookup"><span data-stu-id="8cf74-111">String normalization</span></span>
- <span data-ttu-id="8cf74-112">国际化域名 (IDN) 支持</span><span class="sxs-lookup"><span data-stu-id="8cf74-112">Internationalized Domain Names (IDN) support</span></span>
- <span data-ttu-id="8cf74-113">Linux 上的时区显示名称</span><span class="sxs-lookup"><span data-stu-id="8cf74-113">Time zone display name on Linux</span></span>

<span data-ttu-id="8cf74-114">从 .NET 5.0 开始，开发人员可以更好地控制使用哪个基础库，从而使应用程序可以避免不同平台之间的差异。</span><span class="sxs-lookup"><span data-stu-id="8cf74-114">Starting with .NET 5.0, developers have more control over which underlying library is used, enabling applications to avoid differences across platforms.</span></span>

## <a name="icu-on-windows"></a><span data-ttu-id="8cf74-115">Windows 上的 ICU</span><span class="sxs-lookup"><span data-stu-id="8cf74-115">ICU on Windows</span></span>

<span data-ttu-id="8cf74-116">Windows 2019 年 5 月 10 日更新及更高版本将 [icu.dll](/windows/win32/intl/international-components-for-unicode--icu-) 作为 OS 的一部分，并且 .NET 5.0 和更高版本默认使用 ICU。</span><span class="sxs-lookup"><span data-stu-id="8cf74-116">Windows 10 May 2019 Update and later versions include [icu.dll](/windows/win32/intl/international-components-for-unicode--icu-) as part of the OS, and .NET 5.0 and later versions use ICU by default.</span></span> <span data-ttu-id="8cf74-117">在 Windows 上运行时，.NET 5.0 和更高版本尝试加载 `icu.dll`，如果此库可用，将使用它进行全球化实现。</span><span class="sxs-lookup"><span data-stu-id="8cf74-117">When running on Windows, .NET 5.0 and later versions try to load `icu.dll` and, if it's available, use it for the globalization implementation.</span></span> <span data-ttu-id="8cf74-118">如果无法找到或无法加载 ICU 库，如在较早版本的 Windows 上运行时，.NET 5.0 和更高版本将回退到基于 NLS 的实现。</span><span class="sxs-lookup"><span data-stu-id="8cf74-118">If the ICU library can't be found or loaded, such as when running on older versions of Windows, .NET 5.0 and later versions fall back to the NLS-based implementation.</span></span>

> [!NOTE]
> <span data-ttu-id="8cf74-119">即使使用 ICU，`CurrentCulture`、`CurrentUICulture` 和 `CurrentRegion` 成员仍使用 Windows 操作系统 API 来遵从用户设置。</span><span class="sxs-lookup"><span data-stu-id="8cf74-119">Even when using ICU, the `CurrentCulture`, `CurrentUICulture`, and `CurrentRegion` members still use Windows operating system APIs to honor user settings.</span></span>

### <a name="use-nls-instead-of-icu"></a><span data-ttu-id="8cf74-120">使用 NLS 而不是 ICU</span><span class="sxs-lookup"><span data-stu-id="8cf74-120">Use NLS instead of ICU</span></span>

<span data-ttu-id="8cf74-121">使用 ICU 代替 NLS 可能会导致与一些与全球化相关的操作存在行为差异。</span><span class="sxs-lookup"><span data-stu-id="8cf74-121">Using ICU instead of NLS may result in behavioral differences with some globalization-related operations.</span></span> <span data-ttu-id="8cf74-122">若要恢复为使用 NLS，开发人员可以选择退出 ICU 实现。</span><span class="sxs-lookup"><span data-stu-id="8cf74-122">To revert back to using NLS, a developer can opt out of the ICU implementation.</span></span> <span data-ttu-id="8cf74-123">应用程序可以通过以下任意方式启用 NLS 模式：</span><span class="sxs-lookup"><span data-stu-id="8cf74-123">Applications can enable NLS mode in any of the following ways:</span></span>

- <span data-ttu-id="8cf74-124">在项目文件中：</span><span class="sxs-lookup"><span data-stu-id="8cf74-124">In the project file:</span></span>

  ```xml
  <ItemGroup>
    <RuntimeHostConfigurationOption Include="System.Globalization.UseNls" Value="true" />
  </ItemGroup>
  ```

- <span data-ttu-id="8cf74-125">在 `runtimeconfig.json` 文件中：</span><span class="sxs-lookup"><span data-stu-id="8cf74-125">In the `runtimeconfig.json` file:</span></span>

  ```json
  {
    "runtimeOptions": {
       "configProperties": {
         "System.Globalization.UseNls": true
        }
    }
  }
  ```

- <span data-ttu-id="8cf74-126">通过将环境变量 `DOTNET_SYSTEM_GLOBALIZATION_USENLS` 设置为值 `true` 或 `1`。</span><span class="sxs-lookup"><span data-stu-id="8cf74-126">By setting the environment variable `DOTNET_SYSTEM_GLOBALIZATION_USENLS` to the value `true` or `1`.</span></span>

> [!NOTE]
> <span data-ttu-id="8cf74-127">在项目或 `runtimeconfig.json` 文件中设置的值优先于环境变量。</span><span class="sxs-lookup"><span data-stu-id="8cf74-127">A value set in the project or in the `runtimeconfig.json` file takes precedence over the environment variable.</span></span>

<span data-ttu-id="8cf74-128">有关详细信息，请参阅[运行时配置设置](../../core/run-time-config/globalization.md#nls)。</span><span class="sxs-lookup"><span data-stu-id="8cf74-128">For more information, see [Run-time config settings](../../core/run-time-config/globalization.md#nls).</span></span>

## <a name="app-local-icu"></a><span data-ttu-id="8cf74-129">应用本地 ICU</span><span class="sxs-lookup"><span data-stu-id="8cf74-129">App-local ICU</span></span>

<span data-ttu-id="8cf74-130">每个版本的 ICU 都可能附带了 bug 修复以及描述世界语言的更新公共区域设置数据存储库 (CLDR) 数据。</span><span class="sxs-lookup"><span data-stu-id="8cf74-130">Each release of ICU may bring with it bug fixes as well as updated Common Locale Data Repository (CLDR) data that describes the world's languages.</span></span> <span data-ttu-id="8cf74-131">当涉及与全球化相关的操作时，在 ICU 版本间移动可能会对应用行为产生细微影响。</span><span class="sxs-lookup"><span data-stu-id="8cf74-131">Moving between versions of ICU can subtly impact app behavior when it comes to globalization-related operations.</span></span> <span data-ttu-id="8cf74-132">为了帮助应用程序开发人员确保所有部署之间的一致性，.NET 5.0 和更高版本使 Windows 和 Unix 上的应用能够携带和使用其自己的 ICU 副本。</span><span class="sxs-lookup"><span data-stu-id="8cf74-132">To help application developers ensure consistency across all deployments, .NET 5.0 and later versions enable apps on both Windows and Unix to carry and use their own copy of ICU.</span></span>

<span data-ttu-id="8cf74-133">应用程序可以通过以下任一方式选择使用应用本地 ICU 实现模式：</span><span class="sxs-lookup"><span data-stu-id="8cf74-133">Applications can opt in to an app-local ICU implementation mode in any of the following ways:</span></span>

- <span data-ttu-id="8cf74-134">在项目文件中：</span><span class="sxs-lookup"><span data-stu-id="8cf74-134">In  the project file:</span></span>

  ```xml
  <ItemGroup>
    <RuntimeHostConfigurationOption Include="System.Globalization.AppLocalIcu" Value="<suffix>:<version> or <version>" />
  </ItemGroup>
  ```

- <span data-ttu-id="8cf74-135">在 `runtimeconfig.json` 文件中：</span><span class="sxs-lookup"><span data-stu-id="8cf74-135">In the `runtimeconfig.json` file:</span></span>

  ```json
  {
    "runtimeOptions": {
       "configProperties": {
         "System.Globalization.AppLocalIcu": "<suffix>:<version> or <version>"
       }
    }
  }
  ```

- <span data-ttu-id="8cf74-136">通过将环境变量 `DOTNET_SYSTEM_GLOBALIZATION_APPLOCALICU` 设置为值 `<suffix>:<version>` 或 `<version>`。</span><span class="sxs-lookup"><span data-stu-id="8cf74-136">By setting the environment variable `DOTNET_SYSTEM_GLOBALIZATION_APPLOCALICU` to the value `<suffix>:<version>` or `<version>`.</span></span>

  <span data-ttu-id="8cf74-137">`<suffix>`：长度小于 36 个字符的可选后缀，遵循公共 ICU 打包约定。</span><span class="sxs-lookup"><span data-stu-id="8cf74-137">`<suffix>`: Optional suffix of fewer than 36 characters in length, following the public ICU packaging conventions.</span></span> <span data-ttu-id="8cf74-138">在生成自定义 ICU 时，可以对其自定义以生成 lib 名称并导出符号名称以包含后缀，例如 `libicuucmyapp`，其中 `myapp` 是后缀。</span><span class="sxs-lookup"><span data-stu-id="8cf74-138">When building a custom ICU, you can customize it to produce the lib names and exported symbol names to contain a suffix, for example, `libicuucmyapp`, where `myapp` is the suffix.</span></span>

  <span data-ttu-id="8cf74-139">`<version>`：有效的 ICU 版本，例如 67.1。</span><span class="sxs-lookup"><span data-stu-id="8cf74-139">`<version>`: A valid ICU version, for example, 67.1.</span></span> <span data-ttu-id="8cf74-140">此版本用于加载二进制文件和获取导出的符号。</span><span class="sxs-lookup"><span data-stu-id="8cf74-140">This version is used to load the binaries and to get the exported symbols.</span></span>

<span data-ttu-id="8cf74-141">为了在设置应用本地开关时加载 ICU，.NET 使用 <xref:System.Runtime.InteropServices.NativeLibrary.TryLoad%2A?displayProperty=nameWithType> 方法探测多个路径。</span><span class="sxs-lookup"><span data-stu-id="8cf74-141">To load ICU when the app-local switch is set, .NET uses the <xref:System.Runtime.InteropServices.NativeLibrary.TryLoad%2A?displayProperty=nameWithType> method, which probes multiple paths.</span></span> <span data-ttu-id="8cf74-142">该方法首先尝试在 `NATIVE_DLL_SEARCH_DIRECTORIES` 属性中查找库，该属性由 dotnet 主机基于应用的 `deps.json` 文件创建。</span><span class="sxs-lookup"><span data-stu-id="8cf74-142">The method first tries to find the library in the `NATIVE_DLL_SEARCH_DIRECTORIES` property, which is created by the dotnet host based on the `deps.json` file for the app.</span></span> <span data-ttu-id="8cf74-143">有关更多信息，请参阅[默认探测](../../core/dependency-loading/default-probing.md)。</span><span class="sxs-lookup"><span data-stu-id="8cf74-143">For more information, see [Default probing](../../core/dependency-loading/default-probing.md).</span></span>

<span data-ttu-id="8cf74-144">对于独立应用，用户不需要执行任何特殊操作，只需确保 ICU 位于应用目录中（对于独立应用，工作目录默认为 `NATIVE_DLL_SEARCH_DIRECTORIES`）。</span><span class="sxs-lookup"><span data-stu-id="8cf74-144">For self-contained apps, no special action is required by the user, other than making sure ICU is in the app directory (for self-contained apps, the working directory defaults to `NATIVE_DLL_SEARCH_DIRECTORIES`).</span></span>

<span data-ttu-id="8cf74-145">如果通过 NuGet 包使用 ICU，则可在依赖框架的应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="8cf74-145">If you're consuming ICU via a NuGet package, this works in framework-dependent applications.</span></span> <span data-ttu-id="8cf74-146">NuGet 解析本机资产，并将它们包含在 `deps.json` 文件和 `runtimes` 目录下应用程序的输出目录中。</span><span class="sxs-lookup"><span data-stu-id="8cf74-146">NuGet resolves the native assets and includes them in the `deps.json` file and in the output directory for the application under the `runtimes` directory.</span></span> <span data-ttu-id="8cf74-147">.NET 从这里加载它。</span><span class="sxs-lookup"><span data-stu-id="8cf74-147">.NET loads it from there.</span></span>

<span data-ttu-id="8cf74-148">对于在本地版本使用 ICU 的依赖框架的应用（非独立应用），必须执行额外的步骤。</span><span class="sxs-lookup"><span data-stu-id="8cf74-148">For framework-dependent apps (not self contained) where ICU is consumed from a local build, you must take additional steps.</span></span> <span data-ttu-id="8cf74-149">.NET SDK 尚不具有用于将“松散”的本机二进制文件合并到 `deps.json` 中的功能（请参阅[此 SDK 问题](https://github.com/dotnet/sdk/issues/11373)）。</span><span class="sxs-lookup"><span data-stu-id="8cf74-149">The .NET SDK doesn't yet have a feature for "loose" native binaries to be incorporated into `deps.json` (see [this SDK issue](https://github.com/dotnet/sdk/issues/11373)).</span></span> <span data-ttu-id="8cf74-150">相反，你可以通过将其他信息添加到应用程序的项目文件来启用此功能。</span><span class="sxs-lookup"><span data-stu-id="8cf74-150">Instead, you can enable this by adding additional information into the application's project file.</span></span> <span data-ttu-id="8cf74-151">例如：</span><span class="sxs-lookup"><span data-stu-id="8cf74-151">For example:</span></span>

```xml
<ItemGroup>
  <IcuAssemblies Include="icu\*.so*" />
  <RuntimeTargetsCopyLocalItems Include="@(IcuAssemblies)" AssetType="native" CopyLocal="true" DestinationSubDirectory="runtimes/linux-x64/native/" DestinationSubPath="%(FileName)%(Extension)" RuntimeIdentifier="linux-x64" NuGetPackageId="System.Private.Runtime.UnicodeData" />
</ItemGroup>
```

<span data-ttu-id="8cf74-152">必须为支持的运行时的所有 ICU 二进制文件执行此操作。</span><span class="sxs-lookup"><span data-stu-id="8cf74-152">This must be done for all the ICU binaries for the supported runtimes.</span></span> <span data-ttu-id="8cf74-153">此外，`RuntimeTargetsCopyLocalItems` 项组中的 `NuGetPackageId` 元数据需要与项目实际引用的 NuGet 包匹配。</span><span class="sxs-lookup"><span data-stu-id="8cf74-153">Also, the `NuGetPackageId` metadata in the `RuntimeTargetsCopyLocalItems` item group needs to match a NuGet package that the project actually references.</span></span>

### <a name="macos-behavior"></a><span data-ttu-id="8cf74-154">macOS 行为</span><span class="sxs-lookup"><span data-stu-id="8cf74-154">macOS behavior</span></span>

<span data-ttu-id="8cf74-155">`macOS` 关于使用 `match-o` 文件中指定的加载命令解析依赖的动态库的行为与 Linux 加载程序不同。</span><span class="sxs-lookup"><span data-stu-id="8cf74-155">`macOS` has a different behavior for resolving dependent dynamic libraries from the load commands specified in the `match-o` file than the Linux loader.</span></span> <span data-ttu-id="8cf74-156">在 Linux 加载程序中，.NET 可以尝试使用 `libicudata`、`libicuuc` 和 `libicui18n`（按此顺序）来满足 ICU 依赖项关系图。</span><span class="sxs-lookup"><span data-stu-id="8cf74-156">In the Linux loader, .NET can try `libicudata`, `libicuuc`, and `libicui18n` (in that order) to satisfy ICU dependency graph.</span></span> <span data-ttu-id="8cf74-157">但在 macOS 上，这不起作用。</span><span class="sxs-lookup"><span data-stu-id="8cf74-157">However, on macOS, this doesn't work.</span></span> <span data-ttu-id="8cf74-158">在 macOS 上生成 ICU 时，默认情况下，可以使用 `libicuuc` 中的这些加载命令获取动态库。</span><span class="sxs-lookup"><span data-stu-id="8cf74-158">When building ICU on macOS, you, by default, get a dynamic library with these load commands in `libicuuc`.</span></span> <span data-ttu-id="8cf74-159">以下代码片段演示了一个示例。</span><span class="sxs-lookup"><span data-stu-id="8cf74-159">The following snippet shows an example.</span></span>

```sh
~/ % otool -L /Users/santifdezm/repos/icu-build/icu/install/lib/libicuuc.67.1.dylib
/Users/santifdezm/repos/icu-build/icu/install/lib/libicuuc.67.1.dylib:
 libicuuc.67.dylib (compatibility version 67.0.0, current version 67.1.0)
 libicudata.67.dylib (compatibility version 67.0.0, current version 67.1.0)
 /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1281.100.1)
 /usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 902.1.0)
```

<span data-ttu-id="8cf74-160">这些命令只引用 ICU 其他组件的依赖库的名称。</span><span class="sxs-lookup"><span data-stu-id="8cf74-160">These commands just reference the name of the dependent libraries for the other components of ICU.</span></span> <span data-ttu-id="8cf74-161">加载程序将按照 `dlopen` 约定执行搜索，这涉及到在系统目录中包含这些库，或设置 `LD_LIBRARY_PATH` env var，或在应用级目录中包含 ICU。</span><span class="sxs-lookup"><span data-stu-id="8cf74-161">The loader performs the search following the `dlopen` conventions, which involves having these libraries in the system directories or setting the `LD_LIBRARY_PATH` env vars, or having ICU at the app-level directory.</span></span> <span data-ttu-id="8cf74-162">如果无法设置 `LD_LIBRARY_PATH` 或无法确保 ICU 二进制文件位于应用级目录中，则需要执行一些额外的操作。</span><span class="sxs-lookup"><span data-stu-id="8cf74-162">If you can't set `LD_LIBRARY_PATH` or ensure that ICU binaries are at the app-level directory, you will need to do some extra work.</span></span>

<span data-ttu-id="8cf74-163">对于加载程序，有一些指令（如 `@loader_path`）会告知加载程序使用加载命令在与二进制文件相同的目录中搜索该依赖项。</span><span class="sxs-lookup"><span data-stu-id="8cf74-163">There are some directives for the loader, like `@loader_path`, which tell the loader to search for that dependency in the same directory as the binary with that load command.</span></span> <span data-ttu-id="8cf74-164">可通过两种方式实现此目的：</span><span class="sxs-lookup"><span data-stu-id="8cf74-164">There are two ways to achieve this:</span></span>

- `install_name_tool -change`

  <span data-ttu-id="8cf74-165">运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="8cf74-165">Run the following commands:</span></span>

  ```bash
  install_name_tool -change "libicudata.67.dylib" "@loader_path/libicudata.67.dylib" /path/to/libicuuc.67.1.dylib
  install_name_tool -change "libicudata.67.dylib" "@loader_path/libicudata.67.dylib" /path/to/libicui18n.67.1.dylib
  install_name_tool -change "libicuuc.67.dylib" "@loader_path/libicuuc.67.dylib" /path/to/libicui18n.67.1.dylib
  ```

- <span data-ttu-id="8cf74-166">修补 ICU 以生成含有 `@loader_path` 的安装名称</span><span class="sxs-lookup"><span data-stu-id="8cf74-166">Patch ICU to produce the install names with `@loader_path`</span></span>

  <span data-ttu-id="8cf74-167">在运行 autoconf (`./runConfigureICU`) 之前，将[这些行](https://github.com/unicode-org/icu/blob/ef91cc3673d69a5e00407cda94f39fcda3131451/icu4c/source/config/mh-darwin#L32-L37)更改为以下内容：</span><span class="sxs-lookup"><span data-stu-id="8cf74-167">Before running autoconf (`./runConfigureICU`), change [these lines](https://github.com/unicode-org/icu/blob/ef91cc3673d69a5e00407cda94f39fcda3131451/icu4c/source/config/mh-darwin#L32-L37) to:</span></span>

  ```
  LD_SONAME = -Wl,-compatibility_version -Wl,$(SO_TARGET_VERSION_MAJOR) -Wl,-current_version -Wl,$(SO_TARGET_VERSION) -install_name @loader_path/$(notdir $(MIDDLE_SO_TARGET))
  ```

## <a name="icu-on-webassembly"></a><span data-ttu-id="8cf74-168">WebAssembly 上的 ICU</span><span class="sxs-lookup"><span data-stu-id="8cf74-168">ICU on WebAssembly</span></span>

<span data-ttu-id="8cf74-169">存在专门针对 WebAssembly 工作负荷的 ICU 版本。</span><span class="sxs-lookup"><span data-stu-id="8cf74-169">A version of ICU is available that's specifically for WebAssembly workloads.</span></span> <span data-ttu-id="8cf74-170">此版本提供与桌面配置文件的全球化兼容性。</span><span class="sxs-lookup"><span data-stu-id="8cf74-170">This version provides globalization compatibility with desktop profiles.</span></span> <span data-ttu-id="8cf74-171">若要将 ICU 数据文件大小从 24 MB 减小到 1.4 MB（如果使用 Brotli 压缩，可压缩到约 0.3 MB），则此工作负荷有少量限制。</span><span class="sxs-lookup"><span data-stu-id="8cf74-171">To reduce the ICU data file size from 24 MB to 1.4 MB (or ~0.3 MB if compressed with Brotli), this workload has a handful of limitations.</span></span>

<span data-ttu-id="8cf74-172">不支持以下 API：</span><span class="sxs-lookup"><span data-stu-id="8cf74-172">The following APIs are not supported:</span></span>

- <xref:System.Globalization.CultureInfo.EnglishName?displayProperty=nameWithType>
- <xref:System.Globalization.CultureInfo.NativeName?displayProperty=nameWithType>
- <xref:System.Globalization.DateTimeFormatInfo.NativeCalendarName?displayProperty=nameWithType>
- <xref:System.Globalization.RegionInfo.NativeName?displayProperty=nameWithType>

<span data-ttu-id="8cf74-173">支持以下 API，但有一些限制：</span><span class="sxs-lookup"><span data-stu-id="8cf74-173">The following APIs are supported with limitations:</span></span>

- <span data-ttu-id="8cf74-174"><xref:System.String.Normalize(System.Text.NormalizationForm)?displayProperty=nameWithType> 和 <xref:System.String.IsNormalized(System.Text.NormalizationForm)?displayProperty=nameWithType> 不支持很少使用的 <xref:System.Text.NormalizationForm.FormKC> 和 <xref:System.Text.NormalizationForm.FormKD> 形式。</span><span class="sxs-lookup"><span data-stu-id="8cf74-174"><xref:System.String.Normalize(System.Text.NormalizationForm)?displayProperty=nameWithType> and <xref:System.String.IsNormalized(System.Text.NormalizationForm)?displayProperty=nameWithType> don't support the rarely used <xref:System.Text.NormalizationForm.FormKC> and <xref:System.Text.NormalizationForm.FormKD> forms.</span></span>
- <span data-ttu-id="8cf74-175"><xref:System.Globalization.RegionInfo.CurrencyNativeName?displayProperty=nameWithType> 返回与 <xref:System.Globalization.RegionInfo.CurrencyEnglishName?displayProperty=nameWithType> 相同的值。</span><span class="sxs-lookup"><span data-stu-id="8cf74-175"><xref:System.Globalization.RegionInfo.CurrencyNativeName?displayProperty=nameWithType> returns the same value as <xref:System.Globalization.RegionInfo.CurrencyEnglishName?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="8cf74-176">此外，还可以在 [dotnet/icu 存储库](https://github.com/dotnet/icu/blob/0f49268ddfd3331ca090f1c51d2baa2f75f6c6c0/icu-filters/optimal.json#L6-L54)中找到受支持区域设置的列表。</span><span class="sxs-lookup"><span data-stu-id="8cf74-176">In addition, a list of supported locales can be found on the [dotnet/icu repo](https://github.com/dotnet/icu/blob/0f49268ddfd3331ca090f1c51d2baa2f75f6c6c0/icu-filters/optimal.json#L6-L54).</span></span>
