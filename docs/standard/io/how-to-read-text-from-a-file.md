---
title: 如何：从文件中读取文本
description: 在本文中，查看有关如何使用适用于桌面应用的 .NET 中的 StreamReader 类以同步或异步方式从文本文件中读取文本。
ms.date: 01/03/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- streams, reading text from files
- reading text files
- reading data, text files
- data streams, reading text from files
- I/O [.NET], reading text from files
ms.assetid: ed180baa-dfc6-4c69-a725-46e87edafb27
ms.openlocfilehash: 0e90887c2cc4a54355c51facf91c9cc3da7e4320
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93189324"
---
# <a name="how-to-read-text-from-a-file"></a><span data-ttu-id="d7cb3-103">如何：从文件中读取文本</span><span class="sxs-lookup"><span data-stu-id="d7cb3-103">How to: Read text from a file</span></span>

<span data-ttu-id="d7cb3-104">下面的示例演示如何使用适用于桌面应用的 .NET 以异步方式和同步方式从文本文件中读取文本。</span><span class="sxs-lookup"><span data-stu-id="d7cb3-104">The following examples show how to read text synchronously and asynchronously from a text file using .NET for desktop apps.</span></span> <span data-ttu-id="d7cb3-105">在这两个示例中，当你创建 <xref:System.IO.StreamReader> 类的实例时，你会提供文件的绝对路径或相对路径。</span><span class="sxs-lookup"><span data-stu-id="d7cb3-105">In both examples, when you create the instance of the <xref:System.IO.StreamReader> class, you provide the relative or absolute path to the file.</span></span>
  
> [!NOTE]
> <span data-ttu-id="d7cb3-106">这些代码示例不适用于通用 Windows (UWP) 应用，因为 Windows 运行时提供了对文件进行读写操作的不同流类型。</span><span class="sxs-lookup"><span data-stu-id="d7cb3-106">These code examples do not apply to Universal Windows (UWP) apps, because the Windows Runtime provides different stream types for reading and writing to files.</span></span> <span data-ttu-id="d7cb3-107">有关演示如何在 UWP 应用中读取文本的示例，请参阅[快速入门：对文件执行读取和写入操作](/previous-versions/windows/apps/hh758325(v=win.10))。</span><span class="sxs-lookup"><span data-stu-id="d7cb3-107">For an example that shows how to read text from a file in a UWP app, see [Quickstart: Reading and writing files](/previous-versions/windows/apps/hh758325(v=win.10)).</span></span> <span data-ttu-id="d7cb3-108">有关演示如何在 .NET Framework 流和 Windows 运行时流之间进行转换的示例，请参阅[如何：在 .NET Framework 流和 Windows 运行时流之间进行转换](how-to-convert-between-dotnet-streams-and-winrt-streams.md)。</span><span class="sxs-lookup"><span data-stu-id="d7cb3-108">For examples that show how to convert between .NET Framework streams and Windows Runtime streams, see [How to: Convert between .NET Framework streams and Windows Runtime streams](how-to-convert-between-dotnet-streams-and-winrt-streams.md).</span></span>  
  
## <a name="example-synchronous-read-in-a-console-app"></a><span data-ttu-id="d7cb3-109">示例：控制台应用中的同步读取</span><span class="sxs-lookup"><span data-stu-id="d7cb3-109">Example: Synchronous read in a console app</span></span>  
<span data-ttu-id="d7cb3-110">以下示例演示控制台应用中的同步读取操作。</span><span class="sxs-lookup"><span data-stu-id="d7cb3-110">The following example shows a synchronous read operation within a console app.</span></span> <span data-ttu-id="d7cb3-111">此示例使用流读取器打开文本文件，将内容复制到字符串并将字符串输出到控制台。</span><span class="sxs-lookup"><span data-stu-id="d7cb3-111">This example opens the text file using a stream reader, copies the contents to a string, and outputs the string to the console.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="d7cb3-112">该示例假定名为 TestFile.txt 的文件已存在于与应用相同的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="d7cb3-112">The example assumes that a file named *TestFile.txt* already exists in the same folder as the app.</span></span>  

:::code language="csharp" source="snippets/how-to-read-text-from-a-file/csharp/sync-console/Program.cs":::
:::code language="vb" source="snippets/how-to-read-text-from-a-file/vb/sync-console/Program.vb":::
  
## <a name="example-asynchronous-read-in-a-wpf-app"></a><span data-ttu-id="d7cb3-113">示例：WPF 应用中的异步读取</span><span class="sxs-lookup"><span data-stu-id="d7cb3-113">Example: Asynchronous read in a WPF app</span></span>
 <span data-ttu-id="d7cb3-114">以下示例演示 Windows Presentation Foundation (WPF) 应用中的异步读取操作。</span><span class="sxs-lookup"><span data-stu-id="d7cb3-114">The following example shows an asynchronous read operation in a Windows Presentation Foundation (WPF) app.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="d7cb3-115">该示例假定名为 TestFile.txt 的文件已存在于与应用相同的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="d7cb3-115">The example assumes that a file named *TestFile.txt* already exists in the same folder as the app.</span></span>  

:::code language="csharp" source="snippets/how-to-read-text-from-a-file/csharp/async-wpf/MainWindow.xaml.cs":::
:::code language="vb" source="snippets/how-to-read-text-from-a-file/vb/async-wpf/MainWindow.xaml.vb":::
  
## <a name="see-also"></a><span data-ttu-id="d7cb3-116">请参阅</span><span class="sxs-lookup"><span data-stu-id="d7cb3-116">See also</span></span>

- <xref:System.IO.StreamReader>  
- <xref:System.IO.File.OpenText%2A?displayProperty=nameWithType>  
- <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=nameWithType>  
- [<span data-ttu-id="d7cb3-117">异步文件 I/O</span><span class="sxs-lookup"><span data-stu-id="d7cb3-117">Asynchronous file I/O</span></span>](asynchronous-file-i-o.md)  
- <span data-ttu-id="d7cb3-118">[如何：创建目录列表](/previous-versions/dotnet/netframework-4.0/5cf8zcfh(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="d7cb3-118">[How to: Create a directory listing](/previous-versions/dotnet/netframework-4.0/5cf8zcfh(v=vs.100))</span></span>  
- <span data-ttu-id="d7cb3-119">[快速入门：读取和写入文件](/previous-versions/windows/apps/hh758325(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="d7cb3-119">[Quickstart: Reading and writing files](/previous-versions/windows/apps/hh758325(v=win.10))</span></span>  
- [<span data-ttu-id="d7cb3-120">如何：在 .NET Framework 流和 Windows 运行时流之间进行转换</span><span class="sxs-lookup"><span data-stu-id="d7cb3-120">How to: Convert between .NET Framework streams and Windows Runtime streams</span></span>](how-to-convert-between-dotnet-streams-and-winrt-streams.md)  
- [<span data-ttu-id="d7cb3-121">如何：对新建的数据文件进行读取和写入</span><span class="sxs-lookup"><span data-stu-id="d7cb3-121">How to: Read and write to a newly created data file</span></span>](how-to-read-and-write-to-a-newly-created-data-file.md)  
- [<span data-ttu-id="d7cb3-122">如何：打开并追加到日志文件</span><span class="sxs-lookup"><span data-stu-id="d7cb3-122">How to: Open and append to a log file</span></span>](how-to-open-and-append-to-a-log-file.md)  
- [<span data-ttu-id="d7cb3-123">如何：将文本写入文件</span><span class="sxs-lookup"><span data-stu-id="d7cb3-123">How to: Write text to a file</span></span>](how-to-write-text-to-a-file.md)  
- [<span data-ttu-id="d7cb3-124">如何：从字符串中读取字符</span><span class="sxs-lookup"><span data-stu-id="d7cb3-124">How to: Read characters from a string</span></span>](how-to-read-characters-from-a-string.md)  
- [<span data-ttu-id="d7cb3-125">如何：向字符串写入字符</span><span class="sxs-lookup"><span data-stu-id="d7cb3-125">How to: Write characters to a string</span></span>](how-to-write-characters-to-a-string.md)  
- [<span data-ttu-id="d7cb3-126">文件和流 I/O</span><span class="sxs-lookup"><span data-stu-id="d7cb3-126">File and stream I/O</span></span>](index.md)
