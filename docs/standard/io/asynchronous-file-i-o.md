---
title: 异步文件 I/O
description: 了解 .NET 中的异步文件 I/O。 了解异步方法来简化异步操作，例如 ReadAsync、WriteAsync 等。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- streams, synchronous streams
- asynchronous I/O
- synchronous I/O
- streams, asynchronous streams
- I/O [.NET], asynchronous I/O
- Stream class, synchronous I/O
- data streams, asynchronous streams
- Stream class, asynchronous I/O
- multiple I/O requests
- data streams, synchronous streams
ms.assetid: dbdd55e7-d6b9-4f9e-8abb-ab0edd4457f7
ms.openlocfilehash: a148e6e13ec0ee4ee469a0630f150199c5a3af13
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188596"
---
# <a name="asynchronous-file-io"></a><span data-ttu-id="c337f-104">异步文件 I/O</span><span class="sxs-lookup"><span data-stu-id="c337f-104">Asynchronous File I/O</span></span>

<span data-ttu-id="c337f-105">异步操作使您能在不阻塞主线程的情况下执行占用大量资源的 I/O 操作。</span><span class="sxs-lookup"><span data-stu-id="c337f-105">Asynchronous operations enable you to perform resource-intensive I/O operations without blocking the main thread.</span></span> <span data-ttu-id="c337f-106">在 Windows 8.x 应用商店应用或桌面应用中一个耗时的流操作可能阻塞 UI 线程并让应用看起来好像不工作时，这种性能的考虑就显得尤为重要了。</span><span class="sxs-lookup"><span data-stu-id="c337f-106">This performance consideration is particularly important in a Windows 8.x Store app or desktop app where a time-consuming stream operation can block the UI thread and make your app appear as if it is not working.</span></span>

<span data-ttu-id="c337f-107">从 .NET Framework 4.5 开始，I/O 类型包括了异步方法，以简化异步操作。</span><span class="sxs-lookup"><span data-stu-id="c337f-107">Starting with .NET Framework 4.5, the I/O types include async methods to simplify asynchronous operations.</span></span> <span data-ttu-id="c337f-108">异步方法在其名称中包括 `Async` ，例如 <xref:System.IO.Stream.ReadAsync%2A>、 <xref:System.IO.Stream.WriteAsync%2A>、 <xref:System.IO.Stream.CopyToAsync%2A>、 <xref:System.IO.Stream.FlushAsync%2A>、 <xref:System.IO.TextReader.ReadLineAsync%2A>和 <xref:System.IO.TextReader.ReadToEndAsync%2A>。</span><span class="sxs-lookup"><span data-stu-id="c337f-108">An async method contains `Async` in its name, such as <xref:System.IO.Stream.ReadAsync%2A>, <xref:System.IO.Stream.WriteAsync%2A>, <xref:System.IO.Stream.CopyToAsync%2A>, <xref:System.IO.Stream.FlushAsync%2A>, <xref:System.IO.TextReader.ReadLineAsync%2A>, and <xref:System.IO.TextReader.ReadToEndAsync%2A>.</span></span> <span data-ttu-id="c337f-109">这些异步方法基于流类（例如 <xref:System.IO.Stream>、 <xref:System.IO.FileStream>和 <xref:System.IO.MemoryStream>）和用来向流中读出或写入数据的类（例如 <xref:System.IO.TextReader> 和 <xref:System.IO.TextWriter>）实现。</span><span class="sxs-lookup"><span data-stu-id="c337f-109">These async methods are implemented on stream classes, such as <xref:System.IO.Stream>, <xref:System.IO.FileStream>, and <xref:System.IO.MemoryStream>, and on classes that are used for reading from or writing to streams, such <xref:System.IO.TextReader> and <xref:System.IO.TextWriter>.</span></span>

<span data-ttu-id="c337f-110">在 .NET Framework 4 和更早的版本中，你必须使用 <xref:System.IO.Stream.BeginRead%2A> 和 <xref:System.IO.Stream.EndRead%2A> 等方法来实现异步 I/O 操作。</span><span class="sxs-lookup"><span data-stu-id="c337f-110">In .NET Framework 4 and earlier versions, you have to use methods such as <xref:System.IO.Stream.BeginRead%2A> and <xref:System.IO.Stream.EndRead%2A> to implement asynchronous I/O operations.</span></span> <span data-ttu-id="c337f-111">这些方法仍然在当前 .NET 版本中可用，从而支持传统的代码；但是，异步方法能帮助你更轻松地实现异步 I/O 操作。</span><span class="sxs-lookup"><span data-stu-id="c337f-111">These methods are still available in current .NET versions to support legacy code; however, the async methods help you implement asynchronous I/O operations more easily.</span></span>

<span data-ttu-id="c337f-112">C# 和 Visual Basic 分别具有两个用于异步编程的关键字：</span><span class="sxs-lookup"><span data-stu-id="c337f-112">C# and Visual Basic each have two keywords for asynchronous programming:</span></span>

- <span data-ttu-id="c337f-113">`Async` (Visual Basic) 或 `async` (C#) 修饰符，您可以用来标记包含异步操作的方法。</span><span class="sxs-lookup"><span data-stu-id="c337f-113">`Async` (Visual Basic) or `async` (C#) modifier, which is used to mark a method that contains an asynchronous operation.</span></span>

- <span data-ttu-id="c337f-114">`Await` (Visual Basic) 或 `await` (C#) 运算符，可以应用到异步方法的结果中。</span><span class="sxs-lookup"><span data-stu-id="c337f-114">`Await` (Visual Basic) or `await` (C#) operator, which is applied to the result of an async method.</span></span>

<span data-ttu-id="c337f-115">如下面的示例所示，若要实现异步 I/O 操作，请把这些关键字和异步方法结合使用。</span><span class="sxs-lookup"><span data-stu-id="c337f-115">To implement asynchronous I/O operations, use these keywords in conjunction with the async methods, as shown in the following examples.</span></span> <span data-ttu-id="c337f-116">有关详细信息，请参阅[使用 async 和 await 的异步编程 (C#)](../../csharp/programming-guide/concepts/async/index.md) 或 [使用 Async 和 Await 的异步编程 (Visual Basic)](../../visual-basic/programming-guide/concepts/async/index.md)。</span><span class="sxs-lookup"><span data-stu-id="c337f-116">For more information, see [Asynchronous programming with async and await (C#)](../../csharp/programming-guide/concepts/async/index.md) or [Asynchronous Programming with Async and Await (Visual Basic)](../../visual-basic/programming-guide/concepts/async/index.md).</span></span>

<span data-ttu-id="c337f-117">下面的示例演示如何使用两个 <xref:System.IO.FileStream> 对象把文件从一个目录异步复制到另一个目录。</span><span class="sxs-lookup"><span data-stu-id="c337f-117">The following example demonstrates how to use two <xref:System.IO.FileStream> objects to copy files asynchronously from one directory to another.</span></span> <span data-ttu-id="c337f-118">需要注意 <xref:System.Web.UI.WebControls.Button.Click> 控件的 <xref:System.Windows.Controls.Button> 事件处理程序具有 `async` 修饰符标记，因为它调用异步方法。</span><span class="sxs-lookup"><span data-stu-id="c337f-118">Notice that the <xref:System.Web.UI.WebControls.Button.Click> event handler for the <xref:System.Windows.Controls.Button> control is marked with the `async` modifier because it calls an asynchronous method.</span></span>

[!code-csharp[Asynchronous_File_IO_async#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Asynchronous_File_IO_async/cs/example.cs#1)]
[!code-vb[Asynchronous_File_IO_async#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Asynchronous_File_IO_async/vb/example.vb#1)]

<span data-ttu-id="c337f-119">下一个例子类似于前面的例子，但是使用 <xref:System.IO.StreamReader> 和 <xref:System.IO.StreamWriter> 对象以异步方式读取和写入文本文件的内容。</span><span class="sxs-lookup"><span data-stu-id="c337f-119">The next example is similar to the previous one but uses <xref:System.IO.StreamReader> and <xref:System.IO.StreamWriter> objects to read and write the contents of a text file asynchronously.</span></span>

[!code-csharp[Asynchronous_File_IO_async#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Asynchronous_File_IO_async/cs/example2.cs#2)]
[!code-vb[Asynchronous_File_IO_async#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Asynchronous_File_IO_async/vb/example2.vb#2)]

<span data-ttu-id="c337f-120">下一个示例演示用于在 Windows 8.x 应用商店应用中以 <xref:System.IO.Stream> 的形式打开文件的代码隐藏文件和 XAML 文件，并且通过使用 <xref:System.IO.StreamReader> 类的实例来读取其内容。</span><span class="sxs-lookup"><span data-stu-id="c337f-120">The next example shows the code-behind file and the XAML file that are used to open a file as a <xref:System.IO.Stream> in a Windows 8.x Store app, and read its contents by using an instance of the <xref:System.IO.StreamReader> class.</span></span> <span data-ttu-id="c337f-121">它使用异步方法以流的形式打开文件并读取其内容。</span><span class="sxs-lookup"><span data-stu-id="c337f-121">It uses asynchronous methods to open the file as a stream and to read its contents.</span></span>

[!code-csharp[System.IO.WindowsRuntimeStorageExtensions#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestorageextensions/cs/blankpage.xaml.cs#2)]
[!code-vb[System.IO.WindowsRuntimeStorageExtensions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestorageextensions/vb/blankpage.xaml.vb#2)]

[!code-xaml[System.IO.WindowsRuntimeStorageExtensions#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestorageextensions/cs/blankpage.xaml#1)]

## <a name="see-also"></a><span data-ttu-id="c337f-122">请参阅</span><span class="sxs-lookup"><span data-stu-id="c337f-122">See also</span></span>

- <xref:System.IO.Stream>
- [<span data-ttu-id="c337f-123">文件和流 I/O</span><span class="sxs-lookup"><span data-stu-id="c337f-123">File and Stream I/O</span></span>](index.md)
- [<span data-ttu-id="c337f-124">使用 Async 和 Await 的异步编程 (C#)</span><span class="sxs-lookup"><span data-stu-id="c337f-124">Asynchronous programming with async and await (C#)</span></span>](../../csharp/programming-guide/concepts/async/index.md)
- [<span data-ttu-id="c337f-125">使用 Async 和 Await 的异步编程 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="c337f-125">Asynchronous Programming with Async and Await (Visual Basic)</span></span>](../../visual-basic/programming-guide/concepts/async/index.md)
