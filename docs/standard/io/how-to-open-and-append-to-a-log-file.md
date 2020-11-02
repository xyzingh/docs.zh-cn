---
title: 如何：打开并追加到日志文件
description: 使用 .NET 中的 StreamWriter 和 StreamReader 类打开并追加到日志文件，此操作会将字符写入流并从流中读取字符。
ms.date: 01/21/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- log files, opening
- streams, opening and appending to log file
- log files, appending to
- I/O [.NET], log files
ms.assetid: 74423362-1721-49cb-aa0a-e04005f72a06
ms.openlocfilehash: ed8345901dc5f44e947bd076944d7e61eac561da
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188167"
---
# <a name="how-to-open-and-append-to-a-log-file"></a><span data-ttu-id="2e097-103">如何：打开并追加到日志文件</span><span class="sxs-lookup"><span data-stu-id="2e097-103">How to: Open and append to a log file</span></span>

<span data-ttu-id="2e097-104"><xref:System.IO.StreamWriter> 和 <xref:System.IO.StreamReader> 对流执行字符写入和读取操作。</span><span class="sxs-lookup"><span data-stu-id="2e097-104"><xref:System.IO.StreamWriter> and <xref:System.IO.StreamReader> write characters to and read characters from streams.</span></span> <span data-ttu-id="2e097-105">下面的代码示例打开 log.txt 文件以供输入，或创建该文件（如果尚无文件的话），并将日志信息追加到文件末尾。</span><span class="sxs-lookup"><span data-stu-id="2e097-105">The following code example opens the *log.txt* file for input, or creates it if it doesn't exist, and appends log information to the end of the file.</span></span> <span data-ttu-id="2e097-106">然后，示例将文件内容写入标准输出以供显示。</span><span class="sxs-lookup"><span data-stu-id="2e097-106">The example then writes the contents of the file to standard output for display.</span></span>

<span data-ttu-id="2e097-107">作为此示例的替换方法，可以将信息存储为一个字符串或字符串数组，并使用 <xref:System.IO.File.WriteAllText%2A?displayProperty=nameWithType> 或 <xref:System.IO.File.WriteAllLines%2A?displayProperty=nameWithType> 方法实现相同的功能。</span><span class="sxs-lookup"><span data-stu-id="2e097-107">As an alternative to this example, you could store the information as a single string or string array, and use the <xref:System.IO.File.WriteAllText%2A?displayProperty=nameWithType> or <xref:System.IO.File.WriteAllLines%2A?displayProperty=nameWithType> method to achieve the same functionality.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="2e097-108">Visual Basic 用户可以选择使用 <xref:Microsoft.VisualBasic.Logging.Log> 类或 <xref:Microsoft.VisualBasic.FileIO.FileSystem> 类提供的方法和属性，以创建或写入日志文件。</span><span class="sxs-lookup"><span data-stu-id="2e097-108">Visual Basic users may choose to use the methods and properties provided by the <xref:Microsoft.VisualBasic.Logging.Log> class or <xref:Microsoft.VisualBasic.FileIO.FileSystem> class for creating or writing to log files.</span></span>  
  
## <a name="example"></a><span data-ttu-id="2e097-109">示例</span><span class="sxs-lookup"><span data-stu-id="2e097-109">Example</span></span>  
 [!code-csharp[Conceptual.BasicIO.TextFiles#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source2.cs#2)]
 [!code-vb[Conceptual.BasicIO.TextFiles#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source2.vb#2)]  
  
## <a name="see-also"></a><span data-ttu-id="2e097-110">请参阅</span><span class="sxs-lookup"><span data-stu-id="2e097-110">See also</span></span>

- <xref:System.IO.StreamWriter>  
- <xref:System.IO.StreamReader>  
- <xref:System.IO.File.AppendText%2A?displayProperty=nameWithType>  
- <xref:System.IO.File.OpenText%2A?displayProperty=nameWithType>  
- <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=nameWithType>  
- [<span data-ttu-id="2e097-111">如何：枚举目录和文件</span><span class="sxs-lookup"><span data-stu-id="2e097-111">How to: Enumerate directories and files</span></span>](how-to-enumerate-directories-and-files.md)  
- [<span data-ttu-id="2e097-112">如何：对新建的数据文件进行读取和写入</span><span class="sxs-lookup"><span data-stu-id="2e097-112">How to: Read and write to a newly created data file</span></span>](how-to-read-and-write-to-a-newly-created-data-file.md)  
- [<span data-ttu-id="2e097-113">如何：从文件中读取文本</span><span class="sxs-lookup"><span data-stu-id="2e097-113">How to: Read text from a file</span></span>](how-to-read-text-from-a-file.md)  
- [<span data-ttu-id="2e097-114">如何：将文本写入文件</span><span class="sxs-lookup"><span data-stu-id="2e097-114">How to: Write text to a file</span></span>](how-to-write-text-to-a-file.md)  
- [<span data-ttu-id="2e097-115">如何：从字符串中读取字符</span><span class="sxs-lookup"><span data-stu-id="2e097-115">How to: Read characters from a string</span></span>](how-to-read-characters-from-a-string.md)  
- [<span data-ttu-id="2e097-116">如何：向字符串写入字符</span><span class="sxs-lookup"><span data-stu-id="2e097-116">How to: Write characters to a string</span></span>](how-to-write-characters-to-a-string.md)  
- [<span data-ttu-id="2e097-117">文件和流 I/O</span><span class="sxs-lookup"><span data-stu-id="2e097-117">File and stream I/O</span></span>](index.md)
