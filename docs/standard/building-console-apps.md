---
title: 在 .NET 中生成控制台应用程序
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- .NET, building console applications
- application development [.NET], console
- console applications
ms.assetid: c21fb997-9f0e-40a5-8741-f73bba376bd8
ms.openlocfilehash: d5699fd41391c581b87c9d70000993f7a57c7af6
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162994"
---
# <a name="building-console-applications-in-net"></a><span data-ttu-id="75916-102">在 .NET 中生成控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="75916-102">Building Console Applications in .NET</span></span>

<span data-ttu-id="75916-103">.NET 应用程序可以使用 <xref:System.Console?displayProperty=nameWithType> 类在控制台中读取和写入字符。</span><span class="sxs-lookup"><span data-stu-id="75916-103">.NET applications can use the <xref:System.Console?displayProperty=nameWithType> class to read characters from and write characters to the console.</span></span> <span data-ttu-id="75916-104">读取自控制台的数据是从标准输入流读取的，而写入到控制台的数据将写入标准输出流，并且写入控制台的错误数据将写入标准错误输出流。</span><span class="sxs-lookup"><span data-stu-id="75916-104">Data from the console is read from the standard input stream, data to the console is written to the standard output stream, and error data to the console is written to the standard error output stream.</span></span> <span data-ttu-id="75916-105">应用程序启动时，这些数据流会自动与控制台关联，并分别表示为 <xref:System.Console.In%2A>、<xref:System.Console.Out%2A> 和 <xref:System.Console.Error%2A> 属性。</span><span class="sxs-lookup"><span data-stu-id="75916-105">These streams are automatically associated with the console when the application starts and are presented as the <xref:System.Console.In%2A>, <xref:System.Console.Out%2A>, and <xref:System.Console.Error%2A> properties, respectively.</span></span>

 <span data-ttu-id="75916-106"><xref:System.Console.In%2A?displayProperty=nameWithType> 属性的值是 <xref:System.IO.TextReader?displayProperty=nameWithType> 对象，而 <xref:System.Console.Out%2A?displayProperty=nameWithType> 和 <xref:System.Console.Error%2A?displayProperty=nameWithType> 属性的值都是 <xref:System.IO.TextWriter?displayProperty=nameWithType> 对象。</span><span class="sxs-lookup"><span data-stu-id="75916-106">The value of the <xref:System.Console.In%2A?displayProperty=nameWithType> property is a <xref:System.IO.TextReader?displayProperty=nameWithType> object, whereas the values of the <xref:System.Console.Out%2A?displayProperty=nameWithType> and <xref:System.Console.Error%2A?displayProperty=nameWithType> properties are <xref:System.IO.TextWriter?displayProperty=nameWithType> objects.</span></span> <span data-ttu-id="75916-107">你可以将这些属性与不表示控制台的流关联，以便可以将该流指向不同的输入位置或输出位置。</span><span class="sxs-lookup"><span data-stu-id="75916-107">You can associate these properties with streams that do not represent the console, making it possible for you to point the stream to a different location for input or output.</span></span> <span data-ttu-id="75916-108">例如，你可以通过将 <xref:System.Console.Out%2A?displayProperty=nameWithType> 属性设置为 <xref:System.IO.StreamWriter?displayProperty=nameWithType> 将输出重定向到一个文件，这将通过 <xref:System.Console.SetOut%2A?displayProperty=nameWithType> 方法封装 <xref:System.IO.FileStream?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="75916-108">For example, you can redirect the output to a file by setting the <xref:System.Console.Out%2A?displayProperty=nameWithType> property to a <xref:System.IO.StreamWriter?displayProperty=nameWithType>, which encapsulates a <xref:System.IO.FileStream?displayProperty=nameWithType> by means of the <xref:System.Console.SetOut%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="75916-109"><xref:System.Console.In%2A?displayProperty=nameWithType> 和 <xref:System.Console.Out%2A?displayProperty=nameWithType> 属性不需要引用相同流。</span><span class="sxs-lookup"><span data-stu-id="75916-109">The <xref:System.Console.In%2A?displayProperty=nameWithType> and <xref:System.Console.Out%2A?displayProperty=nameWithType> properties do not need to refer to the same stream.</span></span>

> [!NOTE]
> <span data-ttu-id="75916-110">有关生成控制台应用程序（包括 C#、Visual Basic 和 C++ 中的示例）的详细信息，请参阅 <xref:System.Console> 类文档。</span><span class="sxs-lookup"><span data-stu-id="75916-110">For more information about building console applications, including examples in C#, Visual Basic, and C++, see the documentation for the <xref:System.Console> class.</span></span>

 <span data-ttu-id="75916-111">如果不存在控制台（比如在基于 Windows 的应用程序中），写入标准输出流的输出将不可见，因为没有可以将信息写入的控制台。</span><span class="sxs-lookup"><span data-stu-id="75916-111">If the console does not exist, as in a Windows-based application, output written to the standard output stream will not be visible, because there is no console to write the information to.</span></span> <span data-ttu-id="75916-112">将信息写入不可访问的控制台不会引发异常。</span><span class="sxs-lookup"><span data-stu-id="75916-112">Writing information to an inaccessible console does not cause an exception to be raised.</span></span>

 <span data-ttu-id="75916-113">此外，若要使控制台在使用 Visual Studio 开发的基于 Windows 的应用程序内进行读取和写入，请打开项目的“属性”  对话框，单击“应用程序”  选项卡，并将“应用程序类型”  设置为“控制台应用程序”  。</span><span class="sxs-lookup"><span data-stu-id="75916-113">Alternately, to enable the console for reading and writing within a Windows-based application that is developed using Visual Studio, open the project's **Properties** dialog box, click the **Application** tab, and set the **Application type** to **Console Application**.</span></span>

 <span data-ttu-id="75916-114">控制台应用程序缺少在默认情况下启动的消息泵。</span><span class="sxs-lookup"><span data-stu-id="75916-114">Console applications lack a message pump that starts by default.</span></span> <span data-ttu-id="75916-115">因此，控制台调用 Microsoft Win32 计时器时可能会失败。</span><span class="sxs-lookup"><span data-stu-id="75916-115">Therefore, console calls to Microsoft Win32 timers might fail.</span></span>

 <span data-ttu-id="75916-116">System.Console  类具有从控制台读取单独的字符或整行的方法。</span><span class="sxs-lookup"><span data-stu-id="75916-116">The **System.Console** class has methods that can read individual characters or entire lines from the console.</span></span> <span data-ttu-id="75916-117">其他方法转换数据和格式字符串，然后将设置了格式的字符串写入控制台。</span><span class="sxs-lookup"><span data-stu-id="75916-117">Other methods convert data and format strings, and then write the formatted strings to the console.</span></span> <span data-ttu-id="75916-118">有关设置字符串格式的详细信息，请参阅[格式设置类型](base-types/formatting-types.md)。</span><span class="sxs-lookup"><span data-stu-id="75916-118">For more information on formatting strings, see [Formatting Types](base-types/formatting-types.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="75916-119">另请参阅</span><span class="sxs-lookup"><span data-stu-id="75916-119">See also</span></span>

- <xref:System.Console?displayProperty=nameWithType>
- [<span data-ttu-id="75916-120">格式设置类型</span><span class="sxs-lookup"><span data-stu-id="75916-120">Formatting Types</span></span>](base-types/formatting-types.md)
