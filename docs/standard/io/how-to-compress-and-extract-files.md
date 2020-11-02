---
title: 如何：压缩和解压缩文件
description: 使用 System.IO.Compression 压缩和提取文件。 请参阅使用 ZipFile、ZipArchive、ZipArchiveEntry、DeflateStream 和 GZipStream 的示例。
ms.date: 01/14/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- I/O [.NET], compression
- compression
- compress files
ms.assetid: e9876165-3c60-4c84-a272-513e47acf579
ms.openlocfilehash: ea078099aba3161818844d14af221eb582e7f11b
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188284"
---
# <a name="how-to-compress-and-extract-files"></a><span data-ttu-id="201d3-104">如何：压缩和解压缩文件</span><span class="sxs-lookup"><span data-stu-id="201d3-104">How to: Compress and extract files</span></span>

<span data-ttu-id="201d3-105"><xref:System.IO.Compression> 命名空间包含以下类型来对文件和流进行压缩或解压缩。</span><span class="sxs-lookup"><span data-stu-id="201d3-105">The <xref:System.IO.Compression> namespace contains the following types for compressing and decompressing files and streams.</span></span> <span data-ttu-id="201d3-106">还可以使用这些类型来读取和修改压缩文件的内容。</span><span class="sxs-lookup"><span data-stu-id="201d3-106">You can also use these types to read and modify the contents of a compressed file.</span></span>

- <xref:System.IO.Compression.ZipFile>
- <xref:System.IO.Compression.ZipArchive>
- <xref:System.IO.Compression.ZipArchiveEntry>
- <xref:System.IO.Compression.DeflateStream>
- <xref:System.IO.Compression.GZipStream>

<span data-ttu-id="201d3-107">下面的示例演示使用压缩文件可以执行的某些操作。</span><span class="sxs-lookup"><span data-stu-id="201d3-107">The following examples show some of the operations you can perform with compressed files.</span></span> <span data-ttu-id="201d3-108">这些示例需要将以下 NuGet 包添加到项目中：</span><span class="sxs-lookup"><span data-stu-id="201d3-108">These examples require the following NuGet packages to be added to your project:</span></span>

- [<span data-ttu-id="201d3-109">System.IO.Compression</span><span class="sxs-lookup"><span data-stu-id="201d3-109">System.IO.Compression</span></span>](https://www.nuget.org/packages/System.IO.Compression)
- [<span data-ttu-id="201d3-110">System.IO.Compression.ZipFile</span><span class="sxs-lookup"><span data-stu-id="201d3-110">System.IO.Compression.ZipFile</span></span>](https://www.nuget.org/packages/System.IO.Compression.ZipFile)

<span data-ttu-id="201d3-111">如果你使用的是 .NET Framework，请将对这两个库的引用添加到项目中：</span><span class="sxs-lookup"><span data-stu-id="201d3-111">If you're using .NET Framework, add references to these two libraries to your project:</span></span>

- `System.IO.Compression`
- `System.IO.Compression.FileSystem`

## <a name="example-1-create-and-extract-a-zip-file"></a><span data-ttu-id="201d3-112">示例 1：创建和提取 .zip 文件</span><span class="sxs-lookup"><span data-stu-id="201d3-112">Example 1: Create and extract a .zip file</span></span>

<span data-ttu-id="201d3-113">以下示例演示如何使用 <xref:System.IO.Compression.ZipFile> 类创建和提取压缩的 .zip 文件。</span><span class="sxs-lookup"><span data-stu-id="201d3-113">The following example shows how to create and extract a compressed *.zip* file by using the <xref:System.IO.Compression.ZipFile> class.</span></span> <span data-ttu-id="201d3-114">该示例将文件夹的内容压缩为一个新的 .zip 文件，然后将该 .zip 提取到一个新文件夹。</span><span class="sxs-lookup"><span data-stu-id="201d3-114">The example compresses the contents of a folder into a new *.zip* file, and then extracts the zip to a new folder.</span></span>

<span data-ttu-id="201d3-115">若要运行示例，请在程序文件夹中创建 start 文件夹，然后在其中放入要压缩的文件。</span><span class="sxs-lookup"><span data-stu-id="201d3-115">To run the sample, create a *start* folder in your program folder and populate it with files to zip.</span></span>

[!code-csharp[System.IO.Compression.ZipFile#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.zipfile/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipFile#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.zipfile/vb/program1.vb#1)]

## <a name="example-2-extract-specific-file-extensions"></a><span data-ttu-id="201d3-116">示例 2：提取特定文件扩展名</span><span class="sxs-lookup"><span data-stu-id="201d3-116">Example 2: Extract specific file extensions</span></span>

<span data-ttu-id="201d3-117">下一示例循环访问现有 .zip 文件的内容并提取扩展名为 .txt 的文件 。</span><span class="sxs-lookup"><span data-stu-id="201d3-117">The next example iterates through the contents of an existing *.zip* file and extracts files that have a *.txt* extension.</span></span> <span data-ttu-id="201d3-118">它使用 <xref:System.IO.Compression.ZipArchive> 类访问 zip，使用 <xref:System.IO.Compression.ZipArchiveEntry> 类检查各个条目。</span><span class="sxs-lookup"><span data-stu-id="201d3-118">It uses the <xref:System.IO.Compression.ZipArchive> class to access the zip, and the <xref:System.IO.Compression.ZipArchiveEntry> class to inspect the individual entries.</span></span> <span data-ttu-id="201d3-119">适用于 <xref:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A> 对象的扩展方法 <xref:System.IO.Compression.ZipArchiveEntry> 可以在 <xref:System.IO.Compression.ZipFileExtensions?displayProperty=nameWithType> 类中使用。</span><span class="sxs-lookup"><span data-stu-id="201d3-119">The extension method <xref:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A> for the <xref:System.IO.Compression.ZipArchiveEntry> object is available in the <xref:System.IO.Compression.ZipFileExtensions?displayProperty=nameWithType> class.</span></span>

<span data-ttu-id="201d3-120">若要运行示例，请将名为 result.zip 的 .zip 文件放到程序文件夹中 。</span><span class="sxs-lookup"><span data-stu-id="201d3-120">To run the sample, place a *.zip* file called *result.zip* in your program folder.</span></span> <span data-ttu-id="201d3-121">出现提示时，提供要提取到的文件夹名称。</span><span class="sxs-lookup"><span data-stu-id="201d3-121">When prompted, provide a folder name to extract to.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="201d3-122">在解压缩文件时，必须查找可以转义出你想要解压缩到的目录的恶意文件路径。</span><span class="sxs-lookup"><span data-stu-id="201d3-122">When unzipping files, you must look for malicious file paths, which can escape out of the directory you unzip into.</span></span> <span data-ttu-id="201d3-123">这被称为“路径遍历攻击”。</span><span class="sxs-lookup"><span data-stu-id="201d3-123">This is known as a path traversal attack.</span></span> <span data-ttu-id="201d3-124">下面的示例演示如何检查恶意文件路径，并提供一种安全的解压缩方法。</span><span class="sxs-lookup"><span data-stu-id="201d3-124">The following example demonstrates how to check for malicious file paths and provides a safe way to unzip.</span></span>

[!code-csharp[System.IO.Compression.ZipArchive#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchive/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipArchive#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchive/vb/program1.vb#1)]

## <a name="example-3-add-a-file-to-an-existing-zip"></a><span data-ttu-id="201d3-125">示例 3：将文件添加到现有 zip</span><span class="sxs-lookup"><span data-stu-id="201d3-125">Example 3: Add a file to an existing zip</span></span>

<span data-ttu-id="201d3-126">以下示例使用 <xref:System.IO.Compression.ZipArchive> 类访问现有的 .zip 文件，然后向其添加文件。</span><span class="sxs-lookup"><span data-stu-id="201d3-126">The following example uses the <xref:System.IO.Compression.ZipArchive> class to access an existing *.zip* file, and adds a file to it.</span></span> <span data-ttu-id="201d3-127">当将其添加到现有的 zip 时，会对新文件进行压缩。</span><span class="sxs-lookup"><span data-stu-id="201d3-127">The new file gets compressed when you add it to the existing zip.</span></span>

[!code-csharp[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/vb/program1.vb#1)]

## <a name="example-4-compress-and-decompress-gz-files"></a><span data-ttu-id="201d3-128">示例 4：压缩和解压缩 .gz 文件</span><span class="sxs-lookup"><span data-stu-id="201d3-128">Example 4: Compress and decompress .gz files</span></span>

<span data-ttu-id="201d3-129">您也可以使用 <xref:System.IO.Compression.GZipStream> 和 <xref:System.IO.Compression.DeflateStream> 类压缩和解压缩数据。</span><span class="sxs-lookup"><span data-stu-id="201d3-129">You can also use the <xref:System.IO.Compression.GZipStream> and <xref:System.IO.Compression.DeflateStream> classes to compress and decompress data.</span></span> <span data-ttu-id="201d3-130">它们使用相同的压缩算法。</span><span class="sxs-lookup"><span data-stu-id="201d3-130">They use the same compression algorithm.</span></span> <span data-ttu-id="201d3-131">可以使用许多常用工具解压缩写入 .gz 文件的 <xref:System.IO.Compression.GZipStream> 对象。</span><span class="sxs-lookup"><span data-stu-id="201d3-131">You can decompress <xref:System.IO.Compression.GZipStream> objects that are written to a *.gz* file by using many common tools.</span></span> <span data-ttu-id="201d3-132">以下示例展示了如何使用 <xref:System.IO.Compression.GZipStream> 类压缩和解压缩文件目录：</span><span class="sxs-lookup"><span data-stu-id="201d3-132">The following example shows how to compress and decompress a directory of files by using the <xref:System.IO.Compression.GZipStream> class:</span></span>

[!code-csharp[IO.Compression.GZip1#1](../../../samples/snippets/csharp/VS_Snippets_CLR/IO.Compression.GZip1/CS/gziptest.cs#1)]
[!code-vb[IO.Compression.GZip1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/IO.Compression.GZip1/VB/gziptest.vb#1)]

## <a name="see-also"></a><span data-ttu-id="201d3-133">请参阅</span><span class="sxs-lookup"><span data-stu-id="201d3-133">See also</span></span>

- <xref:System.IO.Compression.ZipArchive>  
- <xref:System.IO.Compression.ZipFile>  
- <xref:System.IO.Compression.ZipArchiveEntry>  
- <xref:System.IO.Compression.DeflateStream>  
- <xref:System.IO.Compression.GZipStream>  
- [<span data-ttu-id="201d3-134">文件和流 I/O</span><span class="sxs-lookup"><span data-stu-id="201d3-134">File and stream I/O</span></span>](index.md)
