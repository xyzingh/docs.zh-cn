---
title: Windows 系统中的文件路径格式
description: 本文介绍 Windows 系统上的文件路径格式，如传统 DOS 路径、DOS 设备路径和通用命名约定 (UNC) 路径。
ms.date: 06/06/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- I/O, long paths
- long paths
- path formats, Windows
ms.openlocfilehash: e24772ee9c9d22786c9cfece43017f8526434601
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188050"
---
# <a name="file-path-formats-on-windows-systems"></a><span data-ttu-id="dc17a-103">Windows 系统中的文件路径格式</span><span class="sxs-lookup"><span data-stu-id="dc17a-103">File path formats on Windows systems</span></span>

<span data-ttu-id="dc17a-104"><xref:System.IO> 命名空间中很多类型的成员都包括 `path` 参数，让你可以指定指向某个文件系统资源的绝对路径或相对路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-104">Members of many of the types in the <xref:System.IO> namespace include a `path` parameter that lets you specify an absolute or relative path to a file system resource.</span></span> <span data-ttu-id="dc17a-105">此路径随后会传递至 [Windows 文件系统 API](/windows/desktop/fileio/file-systems)。</span><span class="sxs-lookup"><span data-stu-id="dc17a-105">This path is then passed to [Windows file system APIs](/windows/desktop/fileio/file-systems).</span></span> <span data-ttu-id="dc17a-106">本主题讨论可在 Windows 系统上使用的文件路径格式。</span><span class="sxs-lookup"><span data-stu-id="dc17a-106">This topic discusses the formats for file paths that you can use on Windows systems.</span></span>

## <a name="traditional-dos-paths"></a><span data-ttu-id="dc17a-107">传统 DOS 路径</span><span class="sxs-lookup"><span data-stu-id="dc17a-107">Traditional DOS paths</span></span>

<span data-ttu-id="dc17a-108">标准的 DOS 路径可由以下三部分组成：</span><span class="sxs-lookup"><span data-stu-id="dc17a-108">A standard DOS path can consist of three components:</span></span>

- <span data-ttu-id="dc17a-109">卷号或驱动器号，后跟卷分隔符 (`:`)。</span><span class="sxs-lookup"><span data-stu-id="dc17a-109">A volume or drive letter followed by the volume separator (`:`).</span></span>
- <span data-ttu-id="dc17a-110">目录名称。</span><span class="sxs-lookup"><span data-stu-id="dc17a-110">A directory name.</span></span> <span data-ttu-id="dc17a-111">[目录分隔符](<xref:System.IO.Path.DirectorySeparatorChar>)用来分隔嵌套目录层次结构中的子目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-111">The [directory separator character](<xref:System.IO.Path.DirectorySeparatorChar>) separates subdirectories within the nested directory hierarchy.</span></span>
- <span data-ttu-id="dc17a-112">可选的文件名。</span><span class="sxs-lookup"><span data-stu-id="dc17a-112">An optional filename.</span></span> <span data-ttu-id="dc17a-113">[目录分隔符](<xref:System.IO.Path.DirectorySeparatorChar>)用来分隔文件路径和文件名。</span><span class="sxs-lookup"><span data-stu-id="dc17a-113">The [directory separator character](<xref:System.IO.Path.DirectorySeparatorChar>) separates the file path and the filename.</span></span>

<span data-ttu-id="dc17a-114">如果以上三项都存在，则为绝对路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-114">If all three components are present, the path is absolute.</span></span> <span data-ttu-id="dc17a-115">如未指定卷号或驱动器号，且目录名称的开头是[目录分隔符](<xref:System.IO.Path.DirectorySeparatorChar>)，则路径属于当前驱动器根路径上的相对路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-115">If no volume or drive letter is specified and the directory name begins with the [directory separator character](<xref:System.IO.Path.DirectorySeparatorChar>), the path is relative from the root of the current drive.</span></span> <span data-ttu-id="dc17a-116">否则路径相对于当前目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-116">Otherwise, the path is relative to the current directory.</span></span> <span data-ttu-id="dc17a-117">下表显示了一些可能出现的目录和文件路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-117">The following table shows some possible directory and file paths.</span></span>

|<span data-ttu-id="dc17a-118">路径</span><span class="sxs-lookup"><span data-stu-id="dc17a-118">Path</span></span>  |<span data-ttu-id="dc17a-119">描述</span><span class="sxs-lookup"><span data-stu-id="dc17a-119">Description</span></span>  |
| -- | -- |
| `C:\Documents\Newsletters\Summer2018.pdf` | <span data-ttu-id="dc17a-120">`C:` 驱动器的根目录中的绝对文件路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-120">An absolute file path from the root of drive `C:`.</span></span> |
| `\Program Files\Custom Utilities\StringFinder.exe` | <span data-ttu-id="dc17a-121">当前驱动器根路径上的绝对路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-121">An absolute path from the root of the current drive.</span></span> |
| `2018\January.xlsx` | <span data-ttu-id="dc17a-122">指向当前目录的子目录中的文件的相对路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-122">A relative path to a file in a subdirectory of the current directory.</span></span> |
| `..\Publications\TravelBrochure.pdf` | <span data-ttu-id="dc17a-123">指向当前目录的同级目录中的文件的相对路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-123">A relative path to file in a directory that is a peer of the current directory.</span></span> |
| `C:\Projects\apilibrary\apilibrary.sln` | <span data-ttu-id="dc17a-124">`C:` 驱动器的根目录中的文件的绝对路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-124">An absolute path to a file from the root of drive `C:`.</span></span> |
| `C:Projects\apilibrary\apilibrary.sln` | <span data-ttu-id="dc17a-125">`C:` 驱动器的当前目录中的相对路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-125">A relative path from the current directory of the `C:` drive.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="dc17a-126">请注意最后两个路径之间的差异。</span><span class="sxs-lookup"><span data-stu-id="dc17a-126">Note the difference between the last two paths.</span></span> <span data-ttu-id="dc17a-127">两者都指定了可选的卷说明符（均为 `C:`），但前者以指定的卷的根目录开头，而后者不是。</span><span class="sxs-lookup"><span data-stu-id="dc17a-127">Both specify the optional volume specifier (`C:` in both cases), but the first begins with the root of the specified volume, whereas the second does not.</span></span> <span data-ttu-id="dc17a-128">因此，前者表示 `C:` 驱动器的根目录中的绝对路径，而后者表示 `C:` 驱动器的当前目录中的相对路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-128">As result, the first is an absolute path from the root directory of drive `C:`, whereas the second is a relative path from the current directory of drive `C:`.</span></span> <span data-ttu-id="dc17a-129">应使用前者时使用了后者是涉及 Windows 文件路径的 bug 的常见原因。</span><span class="sxs-lookup"><span data-stu-id="dc17a-129">Use of the second form when the first is intended is a common source of bugs that involve Windows file paths.</span></span>

<span data-ttu-id="dc17a-130">可以通过调用 <xref:System.IO.Path.IsPathFullyQualified%2A?displayProperty=nameWithType> 方法来确定文件路径是否完全限定（即是说，该路径独立于当前目录，且在当前目录更改时不发生变化）。</span><span class="sxs-lookup"><span data-stu-id="dc17a-130">You can determine whether a file path is fully qualified (that is, it the path is independent of the current directory and does not change when the current directory changes) by calling the <xref:System.IO.Path.IsPathFullyQualified%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="dc17a-131">请注意，如果解析的路径始终指向同样的位置，那么此类路径可以包括相对目录段（`.` 和 `..`），而同时依然是完全限定的。</span><span class="sxs-lookup"><span data-stu-id="dc17a-131">Note that such a path can include relative directory segments (`.` and `..`) and still be fully qualified if the resolved path always points to the same location.</span></span>

<span data-ttu-id="dc17a-132">以下示例演示绝对路径和相对路径之间的差异。</span><span class="sxs-lookup"><span data-stu-id="dc17a-132">The following example illustrates the difference between absolute and relative paths.</span></span> <span data-ttu-id="dc17a-133">假定存在目录 `D:\FY2018\`，且在运行该示例之前还没有通过命令提示符为 `D:\` 设置任何当前目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-133">It assumes that the directory `D:\FY2018\` exists, and that you haven't set any current directory for `D:\` from the command prompt before running the example.</span></span>

[!code-csharp[absolute-and-relative-paths](~/samples/snippets/standard/io/file-names/cs/paths.cs)]
[!code-vb[absolute-and-relative-paths](~/samples/snippets/standard/io/file-names/vb/paths.vb)]

[!INCLUDE [localized code comments](../../../includes/code-comments-loc.md)]

## <a name="unc-paths"></a><span data-ttu-id="dc17a-134">UNC 路径</span><span class="sxs-lookup"><span data-stu-id="dc17a-134">UNC paths</span></span>

<span data-ttu-id="dc17a-135">通用命名约定 (UNC) 路径，用于访问网络资源，具有以下格式：</span><span class="sxs-lookup"><span data-stu-id="dc17a-135">Universal naming convention (UNC) paths, which are used to access network resources, have the following format:</span></span>

- <span data-ttu-id="dc17a-136">一个以 `\\` 开头的服务器名或主机名。</span><span class="sxs-lookup"><span data-stu-id="dc17a-136">A server or host name, which is prefaced by `\\`.</span></span> <span data-ttu-id="dc17a-137">服务器名称可以为 NetBIOS 计算机名称或者 IP/FQDN 地址（支持 IPv4 和 IPv6）。</span><span class="sxs-lookup"><span data-stu-id="dc17a-137">The server name can be a NetBIOS machine name or an IP/FQDN address (IPv4 as well as v6 are supported).</span></span>
- <span data-ttu-id="dc17a-138">共享名，使用 `\` 将其与主机名分隔开。</span><span class="sxs-lookup"><span data-stu-id="dc17a-138">A share name, which is separated from the host name by `\`.</span></span> <span data-ttu-id="dc17a-139">服务器名和共享名共同组成了卷。</span><span class="sxs-lookup"><span data-stu-id="dc17a-139">Together, the server and share name make up the volume.</span></span>
- <span data-ttu-id="dc17a-140">目录名称。</span><span class="sxs-lookup"><span data-stu-id="dc17a-140">A directory name.</span></span> <span data-ttu-id="dc17a-141">[目录分隔符](<xref:System.IO.Path.DirectorySeparatorChar>)用来分隔嵌套目录层次结构中的子目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-141">The [directory separator character](<xref:System.IO.Path.DirectorySeparatorChar>) separates subdirectories within the nested directory hierarchy.</span></span>
- <span data-ttu-id="dc17a-142">可选的文件名。</span><span class="sxs-lookup"><span data-stu-id="dc17a-142">An optional filename.</span></span> <span data-ttu-id="dc17a-143">[目录分隔符](<xref:System.IO.Path.DirectorySeparatorChar>)用来分隔文件路径和文件名。</span><span class="sxs-lookup"><span data-stu-id="dc17a-143">The [directory separator character](<xref:System.IO.Path.DirectorySeparatorChar>) separates the file path and the filename.</span></span>

<span data-ttu-id="dc17a-144">以下是一些 UNC 路径的示例：</span><span class="sxs-lookup"><span data-stu-id="dc17a-144">The following are some examples of UNC paths:</span></span>

|<span data-ttu-id="dc17a-145">路径</span><span class="sxs-lookup"><span data-stu-id="dc17a-145">Path</span></span>  |<span data-ttu-id="dc17a-146">描述</span><span class="sxs-lookup"><span data-stu-id="dc17a-146">Description</span></span>  |
| -- | -- |
| `\\system07\C$\` | <span data-ttu-id="dc17a-147">`system07` 上 `C:` 驱动器的根目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-147">The root directory of the `C:` drive on `system07`.</span></span> |
| `\\Server2\Share\Test\Foo.txt` | <span data-ttu-id="dc17a-148">`\\Server2\Share` 卷的测试目录中的 `Foo.txt` 文件。</span><span class="sxs-lookup"><span data-stu-id="dc17a-148">The `Foo.txt` file in the Test directory of the `\\Server2\Share` volume.</span></span>|

<span data-ttu-id="dc17a-149">UNC 路径必须始终是完全限定的。</span><span class="sxs-lookup"><span data-stu-id="dc17a-149">UNC paths must always be fully qualified.</span></span> <span data-ttu-id="dc17a-150">它们可以包括相对目录段（`.` 和 `..`），但是这些目录段必须是完全限定的路径的一部分。</span><span class="sxs-lookup"><span data-stu-id="dc17a-150">They can include relative directory segments (`.` and `..`), but these must be part of a fully qualified path.</span></span> <span data-ttu-id="dc17a-151">只能通过将 UNC 路径映射至驱动器号来使用相对路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-151">You can use relative paths only by mapping a UNC path to a drive letter.</span></span>

## <a name="dos-device-paths"></a><span data-ttu-id="dc17a-152">DOS 设备路径</span><span class="sxs-lookup"><span data-stu-id="dc17a-152">DOS device paths</span></span>

<span data-ttu-id="dc17a-153">Windows 操作系统有一个指向所有资源（包括文件）的统一对象模型。</span><span class="sxs-lookup"><span data-stu-id="dc17a-153">The Windows operating system has a unified object model that points to all resources, including files.</span></span> <span data-ttu-id="dc17a-154">可从控制台窗口访问这些对象路径；并通过旧版 DOS 和 UNC 路径映射到的符号链接的特殊文件，将这些对象路径公开至 Win32 层。</span><span class="sxs-lookup"><span data-stu-id="dc17a-154">These object paths are accessible from the console window and are exposed to the Win32 layer through a special folder of symbolic links that legacy DOS and UNC paths are mapped to.</span></span> <span data-ttu-id="dc17a-155">此特殊文件夹可通过 DOS 设备路径语法（以下任一）进行访问：</span><span class="sxs-lookup"><span data-stu-id="dc17a-155">This special folder is accessed via the DOS device path syntax, which is one of:</span></span>

`\\.\C:\Test\Foo.txt`
`\\?\C:\Test\Foo.txt`

<span data-ttu-id="dc17a-156">除了通过驱动器号识别驱动器以外，还可以使用卷 GUID 来识别卷。</span><span class="sxs-lookup"><span data-stu-id="dc17a-156">In addition to identifying a drive by its drive letter, you can identify a volume by using its volume GUID.</span></span> <span data-ttu-id="dc17a-157">它采用以下形式：</span><span class="sxs-lookup"><span data-stu-id="dc17a-157">This takes the form:</span></span>

`\\.\Volume{b75e2c83-0000-0000-0000-602f00000000}\Test\Foo.txt`
`\\?\Volume{b75e2c83-0000-0000-0000-602f00000000}\Test\Foo.txt`

> [!NOTE]
> <span data-ttu-id="dc17a-158">从 NET Core 1.1 和 .NET Framework 4.6.2 开始，运行在 Windows 上的 .NET 实现支持 DOS 设备路径语法。</span><span class="sxs-lookup"><span data-stu-id="dc17a-158">DOS device path syntax is supported on .NET implementations running on Windows starting with .NET Core 1.1 and .NET Framework 4.6.2.</span></span>

<span data-ttu-id="dc17a-159">DOS 设备路径由以下部分组成：</span><span class="sxs-lookup"><span data-stu-id="dc17a-159">The DOS device path consists of the following components:</span></span>

- <span data-ttu-id="dc17a-160">设备路径说明符（`\\.\` 或 `\\?\`），它将路径标识为 DOS 设备路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-160">The device path specifier (`\\.\` or `\\?\`), which identifies the path as a DOS device path.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dc17a-161">.NET Core 和 .NET 5+ 的所有版本以及从 4.6.2 开始的 .NET Framework 版本都支持 `\\?\`。</span><span class="sxs-lookup"><span data-stu-id="dc17a-161">The `\\?\` is supported in all versions of .NET Core and .NET 5+ and in .NET Framework starting with version 4.6.2.</span></span>

- <span data-ttu-id="dc17a-162">“实际”设备对象的符号链接（如果是驱动器名称则为 C:，如果是卷 GUID 则为卷{b75e2c83-0000-0000-0000-602f00000000}）。</span><span class="sxs-lookup"><span data-stu-id="dc17a-162">A symbolic link to the "real" device object (C: in the case of a drive name, or Volume{b75e2c83-0000-0000-0000-602f00000000} in the case of a volume GUID).</span></span>

   <span data-ttu-id="dc17a-163">设备路径说明符后的第一个 DOS 设备路径段标识了卷或驱动器。</span><span class="sxs-lookup"><span data-stu-id="dc17a-163">The first segment of the DOS device path after the device path specifier identifies the volume or drive.</span></span> <span data-ttu-id="dc17a-164">（例如，`\\?\C:\` 和 `\\.\BootPartition\`。）</span><span class="sxs-lookup"><span data-stu-id="dc17a-164">(For example, `\\?\C:\` and `\\.\BootPartition\`.)</span></span>

   <span data-ttu-id="dc17a-165">UNC 有个特定的链接，很自然地名为 `UNC`。</span><span class="sxs-lookup"><span data-stu-id="dc17a-165">There is a specific link for UNCs that is called, not surprisingly, `UNC`.</span></span> <span data-ttu-id="dc17a-166">例如：</span><span class="sxs-lookup"><span data-stu-id="dc17a-166">For example:</span></span>

  `\\.\UNC\Server\Share\Test\Foo.txt`
  `\\?\UNC\Server\Share\Test\Foo.txt`

    <span data-ttu-id="dc17a-167">对于设备 UNC，服务器/共享部分构成了卷。</span><span class="sxs-lookup"><span data-stu-id="dc17a-167">For device UNCs, the server/share portion forms the volume.</span></span> <span data-ttu-id="dc17a-168">例如在 `\\?\server1\e:\utilities\\filecomparer\` 中，服务器/共享部分是 `server1\utilities`。</span><span class="sxs-lookup"><span data-stu-id="dc17a-168">For example, in `\\?\server1\e:\utilities\\filecomparer\`, the server/share portion is `server1\utilities`.</span></span> <span data-ttu-id="dc17a-169">使用相对目录段调用 <xref:System.IO.Path.GetFullPath(System.String,System.String)?displayProperty=nameWithType> 等方法时，这一点非常重要；决不可能越过卷。</span><span class="sxs-lookup"><span data-stu-id="dc17a-169">This is significant when calling a method such as <xref:System.IO.Path.GetFullPath(System.String,System.String)?displayProperty=nameWithType> with relative directory segments; it is never possible to navigate past the volume.</span></span>

<span data-ttu-id="dc17a-170">DOS 设备路径通过定义进行完全限定。</span><span class="sxs-lookup"><span data-stu-id="dc17a-170">DOS device paths are fully qualified by definition.</span></span> <span data-ttu-id="dc17a-171">不允许使用相对目录段（`.` 和 `..`）。</span><span class="sxs-lookup"><span data-stu-id="dc17a-171">Relative directory segments (`.` and `..`) are not allowed.</span></span> <span data-ttu-id="dc17a-172">也不会包含当前目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-172">Current directories never enter into their usage.</span></span>

## <a name="example-ways-to-refer-to-the-same-file"></a><span data-ttu-id="dc17a-173">示例：引用同一个文件的方法</span><span class="sxs-lookup"><span data-stu-id="dc17a-173">Example: Ways to refer to the same file</span></span>

<span data-ttu-id="dc17a-174">以下示例演示了一些方法，以此可在使用 <xref:System.IO> 命名空间中的 API 时引用文件。</span><span class="sxs-lookup"><span data-stu-id="dc17a-174">The following example illustrates some of the ways in which you can refer to a file when using the APIs in the <xref:System.IO> namespace.</span></span> <span data-ttu-id="dc17a-175">该示例实例化 <xref:System.IO.FileInfo> 对象，并使用它的 <xref:System.IO.FileInfo.Name> 和 <xref:System.IO.FileInfo.Length> 属性来显示文件名以及文件长度。</span><span class="sxs-lookup"><span data-stu-id="dc17a-175">The example instantiates a <xref:System.IO.FileInfo> object and uses its <xref:System.IO.FileInfo.Name> and <xref:System.IO.FileInfo.Length> properties to display the filename and the length of the file.</span></span>

[!code-csharp[referring-to-the-same-file](~/samples/snippets/standard/io/file-names/cs/file-refs.cs)]
[!code-vb[referring-to-the-same-file](~/samples/snippets/standard/io/file-names/vb/file-refs.vb)]

## <a name="path-normalization"></a><span data-ttu-id="dc17a-176">路径规范化</span><span class="sxs-lookup"><span data-stu-id="dc17a-176">Path normalization</span></span>

<span data-ttu-id="dc17a-177">几乎所有传递至 Windows API 的路径都经过规范化。</span><span class="sxs-lookup"><span data-stu-id="dc17a-177">Almost all paths passed to Windows APIs are normalized.</span></span> <span data-ttu-id="dc17a-178">规范化过程中，Windows 执行了以下步骤：</span><span class="sxs-lookup"><span data-stu-id="dc17a-178">During normalization, Windows performs the following steps:</span></span>

- <span data-ttu-id="dc17a-179">识别路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-179">Identifies the path.</span></span>
- <span data-ttu-id="dc17a-180">将当前目录应用于部分限定（相对）路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-180">Applies the current directory to partially qualified (relative) paths.</span></span>
- <span data-ttu-id="dc17a-181">规范化组件和目录分隔符。</span><span class="sxs-lookup"><span data-stu-id="dc17a-181">Canonicalizes component and directory separators.</span></span>
- <span data-ttu-id="dc17a-182">评估相对目录组件（当前目录是 `.`，父目录是 `..`）。</span><span class="sxs-lookup"><span data-stu-id="dc17a-182">Evaluates relative directory components (`.` for the current directory and `..` for the parent directory).</span></span>
- <span data-ttu-id="dc17a-183">剪裁特定字符。</span><span class="sxs-lookup"><span data-stu-id="dc17a-183">Trims certain characters.</span></span>

<span data-ttu-id="dc17a-184">这种规范化隐式进行，若想显式进行规范化，可以调用 <xref:System.IO.Path.GetFullPath%2A?displayProperty=nameWithType> 方法，这会包装对 [GetFullPathName() 函数](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea)的调用。</span><span class="sxs-lookup"><span data-stu-id="dc17a-184">This normalization happens implicitly, but you can do it explicitly by calling the <xref:System.IO.Path.GetFullPath%2A?displayProperty=nameWithType> method, which wraps a call to the  [GetFullPathName() function](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea).</span></span> <span data-ttu-id="dc17a-185">还可以使用 P/Invoke 直接调用 Windows [GetFullPathName() 函数](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea)。</span><span class="sxs-lookup"><span data-stu-id="dc17a-185">You can also call the Windows [GetFullPathName() function](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea) directly using P/Invoke.</span></span>

### <a name="identify-the-path"></a><span data-ttu-id="dc17a-186">标识路径</span><span class="sxs-lookup"><span data-stu-id="dc17a-186">Identify the path</span></span>

<span data-ttu-id="dc17a-187">路径规范化的第一步就是识别路径类型。</span><span class="sxs-lookup"><span data-stu-id="dc17a-187">The first step in path normalization is identifying the type of path.</span></span> <span data-ttu-id="dc17a-188">路径归为以下几个类别之一：</span><span class="sxs-lookup"><span data-stu-id="dc17a-188">Paths fall into one of a few categories:</span></span>

- <span data-ttu-id="dc17a-189">它们是设备路径；就是说，它们的开头是两个分隔符和一个问号或句点（`\\?` 或 `\\.`）。</span><span class="sxs-lookup"><span data-stu-id="dc17a-189">They are device paths; that is, they begin with two separators and a question mark or period (`\\?` or `\\.`).</span></span>
- <span data-ttu-id="dc17a-190">它们是 UNC 路径；就是说，它们的开头是两个分隔符，没有问号或句点。</span><span class="sxs-lookup"><span data-stu-id="dc17a-190">They are UNC paths; that is, they begin with two separators without a question mark or period.</span></span>
- <span data-ttu-id="dc17a-191">它们是完全限定的 DOS 路径；就是说，它们的开头是驱动器号、卷分隔符和组件分隔符 (`C:\`)。</span><span class="sxs-lookup"><span data-stu-id="dc17a-191">They are fully qualified DOS paths; that is, they begin with a drive letter, a volume separator, and a component separator (`C:\`).</span></span>
- <span data-ttu-id="dc17a-192">它们指定旧设备（`CON`、`LPT1`）。</span><span class="sxs-lookup"><span data-stu-id="dc17a-192">They designate a legacy device (`CON`, `LPT1`).</span></span>
- <span data-ttu-id="dc17a-193">它们相对于当前驱动器的根路径；就是说，它们的开头是单个组件分隔符 (`\`)。</span><span class="sxs-lookup"><span data-stu-id="dc17a-193">They are relative to the root of the current drive; that is, they begin with a single component separator (`\`).</span></span>
- <span data-ttu-id="dc17a-194">它们相对于指定驱动器的当前目录；就是说，它们的开头是驱动器号和卷分隔符，而没有组件分隔符 (`C:`)。</span><span class="sxs-lookup"><span data-stu-id="dc17a-194">They are relative to the current directory of a specified drive; that is, they begin with a drive letter, a volume separator, and no component separator (`C:`).</span></span>
- <span data-ttu-id="dc17a-195">它们相对于当前目录；就是说，它们的开头是上述情况以外的任何内容 (`temp\testfile.txt`)。</span><span class="sxs-lookup"><span data-stu-id="dc17a-195">They are relative to the current directory; that is, they begin with anything else (`temp\testfile.txt`).</span></span>

<span data-ttu-id="dc17a-196">路径的类型决定是否以某种方式应用当前目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-196">The type of the path determines whether or not a current directory is applied in some way.</span></span> <span data-ttu-id="dc17a-197">还决定该路径的“根”是什么。</span><span class="sxs-lookup"><span data-stu-id="dc17a-197">It also determines what the "root" of the path is.</span></span>

### <a name="handle-legacy-devices"></a><span data-ttu-id="dc17a-198">处理旧设备</span><span class="sxs-lookup"><span data-stu-id="dc17a-198">Handle legacy devices</span></span>

<span data-ttu-id="dc17a-199">如果路径是旧版 DOS 设备（例如 `CON`、`COM1` 或 `LPT1`），则会转换为设备路径（方法是在其前面追加 `\\.\`）并返回。</span><span class="sxs-lookup"><span data-stu-id="dc17a-199">If the path is a legacy DOS device such as `CON`, `COM1`, or `LPT1`, it is converted into a device path by prepending `\\.\` and returned.</span></span>

<span data-ttu-id="dc17a-200">开头为旧设备名的路径始终被 <xref:System.IO.Path.GetFullPath(System.String)?displayProperty=nameWithType> 方法解释为旧设备。</span><span class="sxs-lookup"><span data-stu-id="dc17a-200">A path that begins with a legacy device name is always interpreted as a legacy device by the <xref:System.IO.Path.GetFullPath(System.String)?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="dc17a-201">例如，`CON.TXT` 的 DOS 设备路径为 `\\.\CON`，而 `COM1.TXT\file1.txt` 的 DOS 设备路径为 `\\.\COM1`。</span><span class="sxs-lookup"><span data-stu-id="dc17a-201">For example, the DOS device path for `CON.TXT` is `\\.\CON`, and the DOS device path for `COM1.TXT\file1.txt` is `\\.\COM1`.</span></span>

### <a name="apply-the-current-directory"></a><span data-ttu-id="dc17a-202">应用当前目录</span><span class="sxs-lookup"><span data-stu-id="dc17a-202">Apply the current directory</span></span>

<span data-ttu-id="dc17a-203">如果路径非完全限定，Windows 会向其应用当前目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-203">If a path isn't fully qualified, Windows applies the current directory to it.</span></span> <span data-ttu-id="dc17a-204">不会向 UNC 和设备路径应用当前目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-204">UNCs and device paths do not have the current directory applied.</span></span> <span data-ttu-id="dc17a-205">带有分隔符的 `C:\` 完整驱动器也不会应用当前目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-205">Neither does a full drive with separator `C:\`.</span></span>

<span data-ttu-id="dc17a-206">如果路径的开头是单个组件分隔符，则会应用当前目录中的驱动器。</span><span class="sxs-lookup"><span data-stu-id="dc17a-206">If the path starts with a single component separator, the drive from the current directory is applied.</span></span> <span data-ttu-id="dc17a-207">例如，如果文件路径是 `\utilities` 且当前目录为 `C:\temp\`，规范化后路径则为 `C:\utilities`。</span><span class="sxs-lookup"><span data-stu-id="dc17a-207">For example, if the file path is `\utilities` and the current directory is `C:\temp\`, normalization produces `C:\utilities`.</span></span>

<span data-ttu-id="dc17a-208">如果路径开头是驱动器号和卷分隔符，而没有组件分隔符，则应用从命令行界面为指定驱动器设置的最新当前目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-208">If the path starts with a drive letter, volume separator, and no component separator, the last current directory set from the command shell for the specified drive is applied.</span></span> <span data-ttu-id="dc17a-209">如未设置最新当前目录，则只应用驱动器。</span><span class="sxs-lookup"><span data-stu-id="dc17a-209">If the last current directory was not set, the drive alone is applied.</span></span> <span data-ttu-id="dc17a-210">例如，如果文件路径为 `D:sources`，当前目录为 `C:\Documents\`，且 D: 盘上的最新当前目录为 `D:\sources\`，则结果为 `D:\sources\sources`。</span><span class="sxs-lookup"><span data-stu-id="dc17a-210">For example, if the file path is `D:sources`, the current directory is `C:\Documents\`, and the last current directory on drive D: was `D:\sources\`, the result is `D:\sources\sources`.</span></span> <span data-ttu-id="dc17a-211">这些“驱动器相对”路径是导致程序和脚本逻辑错误的常见原因。</span><span class="sxs-lookup"><span data-stu-id="dc17a-211">These "drive relative" paths are a common source of program and script logic errors.</span></span> <span data-ttu-id="dc17a-212">假设以字母和冒号开头的路径不是相对路径，显然是不正确的。</span><span class="sxs-lookup"><span data-stu-id="dc17a-212">Assuming that a path beginning with a letter and a colon isn't relative is obviously not correct.</span></span>

<span data-ttu-id="dc17a-213">如果路径不是以分隔符开头的，则应用当前驱动器和当前目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-213">If the path starts with something other than a separator, the current drive and current directory are applied.</span></span> <span data-ttu-id="dc17a-214">例如，如果路径是 `filecompare` 且当前目录是 `C:\utilities\`，则结果为 `C:\utilities\filecompare\`。</span><span class="sxs-lookup"><span data-stu-id="dc17a-214">For example, if the path is `filecompare` and the current directory is `C:\utilities\`, the result is `C:\utilities\filecompare\`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc17a-215">相对路径在多线程应用程序（也就是大多数应用程序）中很危险，因为当前目录是分进程的设置。</span><span class="sxs-lookup"><span data-stu-id="dc17a-215">Relative paths are dangerous in multithreaded applications (that is, most applications) because the current directory is a per-process setting.</span></span> <span data-ttu-id="dc17a-216">任何线程都能在任何时候更改当前目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-216">Any thread can change the current directory at any time.</span></span> <span data-ttu-id="dc17a-217">从 .NET Core 2.1 开始，可以调用 <xref:System.IO.Path.GetFullPath(System.String,System.String)?displayProperty=nameWithType> 方法，从想要据此解析绝对路径的相对路径和基础路径（当前目录）获取绝对路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-217">Starting with .NET Core 2.1, you can call the <xref:System.IO.Path.GetFullPath(System.String,System.String)?displayProperty=nameWithType> method to get an absolute path from a relative path and the base path (the current directory) that you want to resolve it against.</span></span>

### <a name="canonicalize-separators"></a><span data-ttu-id="dc17a-218">规范化分隔符</span><span class="sxs-lookup"><span data-stu-id="dc17a-218">Canonicalize separators</span></span>

<span data-ttu-id="dc17a-219">将所有正斜杠 (`/`) 转换为标准的 Windows 分隔符，也就是反斜杠 (`\`)。</span><span class="sxs-lookup"><span data-stu-id="dc17a-219">All forward slashes (`/`) are converted into the standard Windows separator, the back slash (`\`).</span></span> <span data-ttu-id="dc17a-220">如果存在斜杠，前两个斜杠后面的一系列斜杠都将折叠为一个斜杠。</span><span class="sxs-lookup"><span data-stu-id="dc17a-220">If they are present, a series of slashes that follow the first two slashes are collapsed into a single slash.</span></span>

### <a name="evaluate-relative-components"></a><span data-ttu-id="dc17a-221">评估相对组件</span><span class="sxs-lookup"><span data-stu-id="dc17a-221">Evaluate relative components</span></span>

<span data-ttu-id="dc17a-222">处理路径时，会评估所有由一个或两个句点（`.` 或 `..`）组成的组件或分段：</span><span class="sxs-lookup"><span data-stu-id="dc17a-222">As the path is processed, any components or segments that are composed of a single or a double period (`.` or `..`) are evaluated:</span></span>

- <span data-ttu-id="dc17a-223">如果是单句点，则删除当前分段，因为它表示当前目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-223">For a single period, the current segment is removed, since it refers to the current directory.</span></span>

- <span data-ttu-id="dc17a-224">如果是双句点，则删除当前分段和父级分段，因为双句点表示父级目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-224">For a double period, the current segment and the parent segment are removed, since the double period refers to the parent directory.</span></span>

   <span data-ttu-id="dc17a-225">仅当父级目录未越过路径的根时，才删除父级目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-225">Parent directories are only removed if they aren't past the root of the path.</span></span> <span data-ttu-id="dc17a-226">路径的根取决于路径的类型。</span><span class="sxs-lookup"><span data-stu-id="dc17a-226">The root of the path depends on the type of path.</span></span> <span data-ttu-id="dc17a-227">对于 DOS 路径，根是驱动器 (`C:\`)；对于UNC，根是服务器/共享 (`\\Server\Share`)；对于设备路径，则为设备路径前缀（`\\?\` 或 `\\.\`）。</span><span class="sxs-lookup"><span data-stu-id="dc17a-227">It is the drive (`C:\`) for DOS paths, the server/share for UNCs (`\\Server\Share`), and the device path prefix for device paths (`\\?\` or `\\.\`).</span></span>

### <a name="trim-characters"></a><span data-ttu-id="dc17a-228">剪裁字符</span><span class="sxs-lookup"><span data-stu-id="dc17a-228">Trim characters</span></span>

<span data-ttu-id="dc17a-229">随着分隔符的运行和相对段先遭删除，一些其他字符在规范化过程中也删除了：</span><span class="sxs-lookup"><span data-stu-id="dc17a-229">Along with the runs of separators and relative segments removed earlier, some additional characters are removed during normalization:</span></span>

- <span data-ttu-id="dc17a-230">如果某段以单个句点结尾，则删除此句点。</span><span class="sxs-lookup"><span data-stu-id="dc17a-230">If a segment ends in a single period, that period is removed.</span></span> <span data-ttu-id="dc17a-231">（单个或两个句点的段在之前的步骤中已规范化。</span><span class="sxs-lookup"><span data-stu-id="dc17a-231">(A segment of a single or double period is normalized in the previous step.</span></span> <span data-ttu-id="dc17a-232">三个或更多句点的段未规范化，并且实际上是有效的文件/目录名。）</span><span class="sxs-lookup"><span data-stu-id="dc17a-232">A segment of three or more periods is not normalized and is actually a valid file/directory name.)</span></span>

- <span data-ttu-id="dc17a-233">如果路径的结尾不是分隔符，则删除所有尾随句点和空格 (U+0020)。</span><span class="sxs-lookup"><span data-stu-id="dc17a-233">If the path doesn't end in a separator, all trailing periods and spaces (U+0020) are removed.</span></span> <span data-ttu-id="dc17a-234">如果最后的段只是单个或两个句点，则按上述相对组件规则处理。</span><span class="sxs-lookup"><span data-stu-id="dc17a-234">If the last segment is simply a single or double period, it falls under the relative components rule above.</span></span>

   <span data-ttu-id="dc17a-235">此规则意味着可以创建以空格结尾的目录名称，方法是在空格后添加结尾分隔符。</span><span class="sxs-lookup"><span data-stu-id="dc17a-235">This rule means that you can create a directory name with a trailing space by adding a trailing separator after the space.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="dc17a-236">请勿创建以空格结尾的目录名或文件名。</span><span class="sxs-lookup"><span data-stu-id="dc17a-236">You should **never** create a directory or filename with a trailing space.</span></span> <span data-ttu-id="dc17a-237">如果以空格结尾，则可能难以或者无法访问目录，并且应用程序在尝试处理这样的目录或文件时通常会操作失败。</span><span class="sxs-lookup"><span data-stu-id="dc17a-237">Trailing spaces can make it difficult or impossible to access a directory, and applications commonly fail when attempting to handle directories or files whose names include trailing spaces.</span></span>

## <a name="skip-normalization"></a><span data-ttu-id="dc17a-238">跳过规范化过程</span><span class="sxs-lookup"><span data-stu-id="dc17a-238">Skip normalization</span></span>

<span data-ttu-id="dc17a-239">一般来说，任何传递到 Windows API 的路径都会（有效地）传递到 [GetFullPathName 函数](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea)并进行规范化。</span><span class="sxs-lookup"><span data-stu-id="dc17a-239">Normally, any path passed to a Windows API is (effectively) passed to the [GetFullPathName function](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea) and normalized.</span></span> <span data-ttu-id="dc17a-240">但是有一种很重要的例外情况：以问号（而不是句点）开头的设备路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-240">There is one important exception: a device path that begins with a question mark instead of a period.</span></span> <span data-ttu-id="dc17a-241">除非路径确切地以 `\\?\` 开头（注意使用的是规范的反斜杠），否则会对它进行规范化。</span><span class="sxs-lookup"><span data-stu-id="dc17a-241">Unless the path starts exactly with `\\?\` (note the use of the canonical backslash), it is normalized.</span></span>

<span data-ttu-id="dc17a-242">为什么要跳过规范化过程？</span><span class="sxs-lookup"><span data-stu-id="dc17a-242">Why would you want to skip normalization?</span></span> <span data-ttu-id="dc17a-243">主要有三方面的原因：</span><span class="sxs-lookup"><span data-stu-id="dc17a-243">There are three major reasons:</span></span>

1. <span data-ttu-id="dc17a-244">为了访问那些通常无法访问但合法的路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-244">To get access to paths that are normally unavailable but are legal.</span></span> <span data-ttu-id="dc17a-245">例如名为 `hidden.` 的文件或目录，这是能访问它的唯一方式。</span><span class="sxs-lookup"><span data-stu-id="dc17a-245">A file or directory called `hidden.`, for example, is impossible to access in any other way.</span></span>

1. <span data-ttu-id="dc17a-246">为了在已规范化的情况下通过跳过规范化过程来提升性能。</span><span class="sxs-lookup"><span data-stu-id="dc17a-246">To improve performance by skipping normalization if you've already normalized.</span></span>

1. <span data-ttu-id="dc17a-247">为了跳过路径长度的 `MAX_PATH` 检查以允许多于 259 个字符的路径（仅在 .NET Framework 上）。</span><span class="sxs-lookup"><span data-stu-id="dc17a-247">On .NET Framework only, to skip the `MAX_PATH` check for path length to allow for paths that are greater than 259 characters.</span></span> <span data-ttu-id="dc17a-248">大多数 API 都允许这一点，也有一些例外情况。</span><span class="sxs-lookup"><span data-stu-id="dc17a-248">Most APIs allow this, with some exceptions.</span></span>

> [!NOTE]
> <span data-ttu-id="dc17a-249">.NET Core 和 .NET 5+ 显式处理长路径，且不执行 `MAX_PATH` 检查。</span><span class="sxs-lookup"><span data-stu-id="dc17a-249">.NET Core and .NET 5+ handles long paths implicitly and does not perform a `MAX_PATH` check.</span></span> <span data-ttu-id="dc17a-250">`MAX_PATH` 检查只适用于 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="dc17a-250">The `MAX_PATH` check applies only to .NET Framework.</span></span>

<span data-ttu-id="dc17a-251">跳过规范化和路径上限检查是两种设备路径语法之间唯一的区别；除此以外它们是完全相同的。</span><span class="sxs-lookup"><span data-stu-id="dc17a-251">Skipping normalization and max path checks is the only difference between the two device path syntaxes; they are otherwise identical.</span></span> <span data-ttu-id="dc17a-252">请谨慎地选择跳过规范化，因为很容易就会创建出“一般”应用程序难以处理的路径。</span><span class="sxs-lookup"><span data-stu-id="dc17a-252">Be careful with skipping normalization, since you can easily create paths that are difficult for "normal" applications to deal with.</span></span>

<span data-ttu-id="dc17a-253">如果将开头为 `\\?\` 的路径显式地传递至 [GetFullPathName 函数](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea)，则依然会对它们进行规范化。</span><span class="sxs-lookup"><span data-stu-id="dc17a-253">Paths that start with `\\?\` are still normalized if you explicitly pass them to the [GetFullPathName function](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea).</span></span>

<span data-ttu-id="dc17a-254">可将超过 `MAX_PATH` 字符数的路径传递至 [GetFullPathName](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea)，前提是该路径不含 `\\?\`。</span><span class="sxs-lookup"><span data-stu-id="dc17a-254">You can pass paths of more than `MAX_PATH` characters to [GetFullPathName](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea) without `\\?\`.</span></span> <span data-ttu-id="dc17a-255">支持任意长度的路径，只要其字符串大小在 Windows 能处理的范围内。</span><span class="sxs-lookup"><span data-stu-id="dc17a-255">It supports arbitrary length paths up to the maximum string size that Windows can handle.</span></span>

## <a name="case-and-the-windows-file-system"></a><span data-ttu-id="dc17a-256">大小写和 Windows 文件系统</span><span class="sxs-lookup"><span data-stu-id="dc17a-256">Case and the Windows file system</span></span>

<span data-ttu-id="dc17a-257">Windows 文件系统有一个让非 Window 用户和开发人员感到困惑的特性，就是路径和目录名称不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="dc17a-257">A peculiarity of the Windows file system that non-Windows users and developers find confusing is that path and directory names are case-insensitive.</span></span> <span data-ttu-id="dc17a-258">也就是说，目录名和文件名反映的是创建它们时所使用的字符串的大小写。</span><span class="sxs-lookup"><span data-stu-id="dc17a-258">That is, directory and file names reflect the casing of the strings used when they are created.</span></span> <span data-ttu-id="dc17a-259">例如，名为</span><span class="sxs-lookup"><span data-stu-id="dc17a-259">For example, the method call</span></span>

```csharp
Directory.Create("TeStDiReCtOrY");
```

```vb
Directory.Create("TeStDiReCtOrY")
```

<span data-ttu-id="dc17a-260">的方法创建名为 TeStDiReCtOrY 的目录。</span><span class="sxs-lookup"><span data-stu-id="dc17a-260">creates a directory named TeStDiReCtOrY.</span></span> <span data-ttu-id="dc17a-261">如果重命名目录或文件以改变大小写，则目录名或文件名反映的是重命名它们时所使用的字符串的大小写。</span><span class="sxs-lookup"><span data-stu-id="dc17a-261">If you rename a directory or file to change its case, the directory or file name reflects the case of the string used when you rename it.</span></span> <span data-ttu-id="dc17a-262">例如，以下代码将文件 test.txt 重命名为 Test.txt：</span><span class="sxs-lookup"><span data-stu-id="dc17a-262">For example, the following code renames a file named test.txt to Test.txt:</span></span>

[!code-csharp[case-and-renaming](~/samples/snippets/standard/io/file-names/cs/rename.cs)]
[!code-vb[case-and-renaming](~/samples/snippets/standard/io/file-names/vb/rename.vb)]

<span data-ttu-id="dc17a-263">但是比较目录名和文件名时不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="dc17a-263">However, directory and file name comparisons are case-insensitive.</span></span> <span data-ttu-id="dc17a-264">如果搜索名为“test.txt”的文件，.NET 文件系统 API 会在比较时忽略大小写问题。</span><span class="sxs-lookup"><span data-stu-id="dc17a-264">If you search for a file named "test.txt", .NET file system APIs ignore case in the comparison.</span></span> <span data-ttu-id="dc17a-265">“Test.txt”、“TEST.TXT”、“test.TXT”和其他任何大写和小写的字母组合都会成为“test.txt”的匹配项。</span><span class="sxs-lookup"><span data-stu-id="dc17a-265">"Test.txt", "TEST.TXT", "test.TXT", and any other combination of uppercase and lowercase letters will match "test.txt".</span></span>
