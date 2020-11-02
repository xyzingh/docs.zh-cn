---
title: 如何：枚举目录和文件
description: 了解如何使用可枚举集合来枚举目录和文件，可枚举集合在 .NET 中的性能优于数组。
ms.date: 12/27/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- I/O [.NET], enumerating directories and files
ms.assetid: 86b69a08-3bfa-4e5f-b4e1-3b7cb8478215
ms.openlocfilehash: 7a757fc97fd934f02592264c3a495c3efc435fd5
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93187887"
---
# <a name="how-to-enumerate-directories-and-files"></a><span data-ttu-id="0a158-103">如何：枚举目录和文件</span><span class="sxs-lookup"><span data-stu-id="0a158-103">How to: Enumerate directories and files</span></span>
<span data-ttu-id="0a158-104">在处理目录和文件的大型集合时，可枚举的集合能够比数组提供更好的性能。</span><span class="sxs-lookup"><span data-stu-id="0a158-104">Enumerable collections provide better performance than arrays when you work with large collections of directories and files.</span></span> <span data-ttu-id="0a158-105">要枚举目录和文件，请使用可返回目录和文件名的可枚举集合的方法或其 <xref:System.IO.DirectoryInfo>、<xref:System.IO.FileInfo> 或 <xref:System.IO.FileSystemInfo> 对象。</span><span class="sxs-lookup"><span data-stu-id="0a158-105">To enumerate directories and files, use methods that return an enumerable collection of directory or file names, or their <xref:System.IO.DirectoryInfo>, <xref:System.IO.FileInfo>, or <xref:System.IO.FileSystemInfo> objects.</span></span>  
  
<span data-ttu-id="0a158-106">如果只想搜索并返回目录名称或文件名，请使用 <xref:System.IO.Directory> 类的枚举方法。</span><span class="sxs-lookup"><span data-stu-id="0a158-106">If you want to search and return only the names of directories or files, use the enumeration methods of the <xref:System.IO.Directory> class.</span></span> <span data-ttu-id="0a158-107">若要搜索并返回目录或文件的其他属性，请使用 <xref:System.IO.DirectoryInfo> 和 <xref:System.IO.FileSystemInfo> 类。</span><span class="sxs-lookup"><span data-stu-id="0a158-107">If you want to search and return other properties of directories or files, use the <xref:System.IO.DirectoryInfo> and <xref:System.IO.FileSystemInfo> classes.</span></span>  
  
<span data-ttu-id="0a158-108">可以使用这些方法中的可枚举集合作为集合类（如 <xref:System.Collections.Generic.List%601>）的构造函数的 <xref:System.Collections.Generic.IEnumerable%601> 参数。</span><span class="sxs-lookup"><span data-stu-id="0a158-108">You can use enumerable collections from these methods as the <xref:System.Collections.Generic.IEnumerable%601> parameter for constructors of collection classes like <xref:System.Collections.Generic.List%601>.</span></span>  
  
<span data-ttu-id="0a158-109">下表总结了返回可枚举的文件和目录集合的方法：</span><span class="sxs-lookup"><span data-stu-id="0a158-109">The following table summarizes the methods that return enumerable collections of files and directories:</span></span>  
  
|<span data-ttu-id="0a158-110">搜索并返回</span><span class="sxs-lookup"><span data-stu-id="0a158-110">To search and return</span></span>|<span data-ttu-id="0a158-111">使用方法</span><span class="sxs-lookup"><span data-stu-id="0a158-111">Use method</span></span>|  
|------------------|-------------------------------------|-------------------|  
|<span data-ttu-id="0a158-112">目录名称</span><span class="sxs-lookup"><span data-stu-id="0a158-112">Directory names</span></span>|<xref:System.IO.Directory.EnumerateDirectories%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="0a158-113">目录信息 (<xref:System.IO.DirectoryInfo>)</span><span class="sxs-lookup"><span data-stu-id="0a158-113">Directory information (<xref:System.IO.DirectoryInfo>)</span></span>|<xref:System.IO.DirectoryInfo.EnumerateDirectories%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="0a158-114">文件名</span><span class="sxs-lookup"><span data-stu-id="0a158-114">File names</span></span>|<xref:System.IO.Directory.EnumerateFiles%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="0a158-115">文件信息 (<xref:System.IO.FileInfo>)</span><span class="sxs-lookup"><span data-stu-id="0a158-115">File information (<xref:System.IO.FileInfo>)</span></span>|<xref:System.IO.DirectoryInfo.EnumerateFiles%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="0a158-116">文件系统条目名称</span><span class="sxs-lookup"><span data-stu-id="0a158-116">File system entry names</span></span>|<xref:System.IO.Directory.EnumerateFileSystemEntries%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="0a158-117">文件系统条目信息 (<xref:System.IO.FileSystemInfo>)</span><span class="sxs-lookup"><span data-stu-id="0a158-117">File system entry information (<xref:System.IO.FileSystemInfo>)</span></span>|<xref:System.IO.DirectoryInfo.EnumerateFileSystemInfos%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="0a158-118">目录和文件名称</span><span class="sxs-lookup"><span data-stu-id="0a158-118">Directory and file names</span></span> |<xref:System.IO.Directory.EnumerateFileSystemEntries%2A?displayProperty=nameWithType>|  

> [!NOTE]
> <span data-ttu-id="0a158-119">虽然可以使用可选的 <xref:System.IO.SearchOption> 枚举的 <xref:System.IO.SearchOption.AllDirectories> 选项迅速枚举父目录的子目录中的所有文件，但 <xref:System.UnauthorizedAccessException> 错误可能会使枚举不完整。</span><span class="sxs-lookup"><span data-stu-id="0a158-119">Although you can immediately enumerate all the files in the subdirectories of a parent directory by using the <xref:System.IO.SearchOption.AllDirectories> option of the optional <xref:System.IO.SearchOption> enumeration, <xref:System.UnauthorizedAccessException> errors may make the enumeration incomplete.</span></span> <span data-ttu-id="0a158-120">可以通过先枚举目录，然后枚举文件来捕获这些异常。</span><span class="sxs-lookup"><span data-stu-id="0a158-120">You can catch these exceptions by first enumerating directories and then enumerating files.</span></span>  
  
## <a name="examples-use-the-directory-class"></a><span data-ttu-id="0a158-121">示例：使用目录类</span><span class="sxs-lookup"><span data-stu-id="0a158-121">Examples: Use the Directory class</span></span>  
  
<span data-ttu-id="0a158-122">以下示例使用 <xref:System.IO.Directory.EnumerateDirectories%28System.String%29?displayProperty=nameWithType> 方法获取指定路径中顶级目录名称的列表。</span><span class="sxs-lookup"><span data-stu-id="0a158-122">The following example uses the <xref:System.IO.Directory.EnumerateDirectories%28System.String%29?displayProperty=nameWithType> method to get a list of the top-level directory names in a specified path.</span></span>  

[!code-csharp[System.IO.EnumDirs1#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.enumdirs1/cs/program.cs#1)]
[!code-vb[System.IO.EnumDirs1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.enumdirs1/vb/program.vb#1)]  

<span data-ttu-id="0a158-123">以下示例使用 <xref:System.IO.Directory.EnumerateFiles%28System.String%2CSystem.String%2CSystem.IO.SearchOption%29?displayProperty=nameWithType> 方法递归枚举目录中的所有文件名以及与特定模式匹配的子目录。</span><span class="sxs-lookup"><span data-stu-id="0a158-123">The following example uses the <xref:System.IO.Directory.EnumerateFiles%28System.String%2CSystem.String%2CSystem.IO.SearchOption%29?displayProperty=nameWithType> method to recursively enumerate all file names in a directory and subdirectories that match a certain pattern.</span></span> <span data-ttu-id="0a158-124">然后它读取每个文件的每一行，并显示包含指定字符串的行及其文件名和路径。</span><span class="sxs-lookup"><span data-stu-id="0a158-124">It then reads each line of each file and displays the lines that contain a specified string, with their filenames and paths.</span></span>

[!code-csharp[System.IO.Directory.EnumerateFiles#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.directory.enumeratefiles/cs/program.cs#1)]
[!code-vb[System.IO.Directory.EnumerateFiles#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.directory.enumeratefiles/vb/program.vb#1)]  
  
## <a name="examples-use-the-directoryinfo-class"></a><span data-ttu-id="0a158-125">示例：使用 DirectoryInfo 类</span><span class="sxs-lookup"><span data-stu-id="0a158-125">Examples: Use the DirectoryInfo class</span></span>  
  
<span data-ttu-id="0a158-126">下面的示例使用 <xref:System.IO.DirectoryInfo.EnumerateDirectories%2A?displayProperty=nameWithType> 方法列出顶级目录的集合，这些顶级目录的 <xref:System.IO.FileSystemInfo.CreationTimeUtc> 早于某个 <xref:System.DateTime> 值。</span><span class="sxs-lookup"><span data-stu-id="0a158-126">The following example uses the <xref:System.IO.DirectoryInfo.EnumerateDirectories%2A?displayProperty=nameWithType> method to list a collection of top-level directories whose <xref:System.IO.FileSystemInfo.CreationTimeUtc> is earlier than a certain <xref:System.DateTime> value.</span></span>  

[!code-csharp[System.IO.DirectoryInfo.EnumDirs#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.directoryinfo.enumdirs/cs/program.cs)]
[!code-vb[System.IO.DirectoryInfo.EnumDirs#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.directoryinfo.enumdirs/vb/module1.vb)]  
  
<span data-ttu-id="0a158-127">下例使用 <xref:System.IO.DirectoryInfo.EnumerateFiles%2A?displayProperty=nameWithType> 方法列出 <xref:System.IO.FileInfo.Length> 超过 10MB 的所有文件。</span><span class="sxs-lookup"><span data-stu-id="0a158-127">The following example uses the <xref:System.IO.DirectoryInfo.EnumerateFiles%2A?displayProperty=nameWithType> method to list all files whose <xref:System.IO.FileInfo.Length> exceeds 10MB.</span></span> <span data-ttu-id="0a158-128">此示例先枚举顶级目录以捕获可能的未授权访问异常，再枚举文件。</span><span class="sxs-lookup"><span data-stu-id="0a158-128">This example first enumerates the top-level directories, to catch possible unauthorized access exceptions, and then enumerates the files.</span></span>  

[!code-csharp[System.IO.DirectoryInfo.EnumerateDirectories#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.directoryinfo.enumeratedirectories/cs/program.cs#1)]
[!code-vb[System.IO.DirectoryInfo.EnumerateDirectories#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.directoryinfo.enumeratedirectories/vb/program.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="0a158-129">请参阅</span><span class="sxs-lookup"><span data-stu-id="0a158-129">See also</span></span>

- [<span data-ttu-id="0a158-130">文件和流 I/O</span><span class="sxs-lookup"><span data-stu-id="0a158-130">File and stream I/O</span></span>](index.md)
