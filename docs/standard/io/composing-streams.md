---
title: 撰写流
ms.date: 01/21/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- streams, base streams
- I/O [.NET], composing streams
- Stream class, composing streams
- base streams
- streams, backing stores
ms.assetid: da761658-a535-4f26-a452-b30df47f73d5
ms.openlocfilehash: 93295c1d70f510ef563abc3a191d6690b1174fa8
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188570"
---
# <a name="compose-streams"></a><span data-ttu-id="5548d-102">撰写流</span><span class="sxs-lookup"><span data-stu-id="5548d-102">Compose streams</span></span>
<span data-ttu-id="5548d-103">后备存储是磁盘或内存等存储介质  。</span><span class="sxs-lookup"><span data-stu-id="5548d-103">A *backing store* is a storage medium, such as a disk or memory.</span></span> <span data-ttu-id="5548d-104">各个后备存储都实现自己的流，作为 <xref:System.IO.Stream> 类的实现。</span><span class="sxs-lookup"><span data-stu-id="5548d-104">Each different backing store implements its own stream as an implementation of the <xref:System.IO.Stream> class.</span></span>

<span data-ttu-id="5548d-105">每个流类型对给定的后备存储执行字节读取和写入操作。</span><span class="sxs-lookup"><span data-stu-id="5548d-105">Each stream type reads and writes bytes from and to its given backing store.</span></span> <span data-ttu-id="5548d-106">连接到后备存储的流称为“基流”  。</span><span class="sxs-lookup"><span data-stu-id="5548d-106">Streams that connect to backing stores are called *base streams* .</span></span> <span data-ttu-id="5548d-107">基流的构造函数包含将流连接到后备存储所需的参数。</span><span class="sxs-lookup"><span data-stu-id="5548d-107">Base streams have constructors with the parameters necessary to connect the stream to the backing store.</span></span> <span data-ttu-id="5548d-108">例如，<xref:System.IO.FileStream> 包含指定路径参数的构造函数，此参数指定了进程如何共享文件。</span><span class="sxs-lookup"><span data-stu-id="5548d-108">For example, <xref:System.IO.FileStream> has constructors that specify a path parameter, which specifies how the file will be shared by processes.</span></span>  

<span data-ttu-id="5548d-109"><xref:System.IO> 类旨在简化流撰写。</span><span class="sxs-lookup"><span data-stu-id="5548d-109">The design of the <xref:System.IO> classes provides simplified stream composition.</span></span> <span data-ttu-id="5548d-110">可以将基流附加到一个或多个提供所需功能的直通流。</span><span class="sxs-lookup"><span data-stu-id="5548d-110">You can attach base streams to one or more pass-through streams that provide the functionality you want.</span></span> <span data-ttu-id="5548d-111">可以将读取器或编写器附加到链的末尾，这样便能轻松读取或编写首选类型。</span><span class="sxs-lookup"><span data-stu-id="5548d-111">You can attach a reader or writer to the end of the chain, so the preferred types can be read or written easily.</span></span>  

<span data-ttu-id="5548d-112">下面的代码示例根据现有 MyFile.txt 创建了 FileStream，以便缓冲 MyFile.txt    。</span><span class="sxs-lookup"><span data-stu-id="5548d-112">The following code examples create a **FileStream** around the existing *MyFile.txt* in order to buffer *MyFile.txt* .</span></span> <span data-ttu-id="5548d-113">请注意，FileStreams 默认缓冲  。</span><span class="sxs-lookup"><span data-stu-id="5548d-113">Note that **FileStreams** are buffered by default.</span></span>

>[!IMPORTANT]
><span data-ttu-id="5548d-114">这些示例假定名为 MyFile.txt 的文件已存在于与应用相同的文件夹中  。</span><span class="sxs-lookup"><span data-stu-id="5548d-114">The examples assume that a file named *MyFile.txt* already exists in the same folder as the app.</span></span>  

## <a name="example-use-streamreader"></a><span data-ttu-id="5548d-115">示例：使用 StreamReader</span><span class="sxs-lookup"><span data-stu-id="5548d-115">Example: Use StreamReader</span></span>
<span data-ttu-id="5548d-116">以下示例将创建从 FileStream 读取字符的 <xref:System.IO.StreamReader>，此读取器作为构造函数参数传递给 StreamReader   。</span><span class="sxs-lookup"><span data-stu-id="5548d-116">The following example creates a <xref:System.IO.StreamReader> to read characters from the **FileStream** , which is passed to the **StreamReader** as its constructor argument.</span></span> <span data-ttu-id="5548d-117">除非 <xref:System.IO.StreamReader.Peek%2A?displayProperty=nameWithType> 找不到更多字符，否则 <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=nameWithType> 会一直读取字符。</span><span class="sxs-lookup"><span data-stu-id="5548d-117"><xref:System.IO.StreamReader.ReadLine%2A?displayProperty=nameWithType> then reads until <xref:System.IO.StreamReader.Peek%2A?displayProperty=nameWithType> finds no more characters.</span></span>  
  
 [!code-csharp[System.IO.StreamReader#20](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.StreamReader/CS/source2.cs#20)]
 [!code-vb[System.IO.StreamReader#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.StreamReader/VB/source2.vb#20)]  
  
## <a name="example-use-binaryreader"></a><span data-ttu-id="5548d-118">示例：使用 BinaryReader</span><span class="sxs-lookup"><span data-stu-id="5548d-118">Example: Use BinaryReader</span></span>
<span data-ttu-id="5548d-119">以下示例将创建从 FileStream 读取字节的 <xref:System.IO.BinaryReader>，此读取器作为构造函数参数传递给 BinaryReader   。</span><span class="sxs-lookup"><span data-stu-id="5548d-119">The following example creates a <xref:System.IO.BinaryReader> to read bytes from the **FileStream** , which is passed to the **BinaryReader** as its constructor argument.</span></span> <span data-ttu-id="5548d-120">除非 <xref:System.IO.BinaryReader.PeekChar%2A> 找不到更多字节，否则 <xref:System.IO.BinaryReader.ReadByte%2A> 会一直读取字节。</span><span class="sxs-lookup"><span data-stu-id="5548d-120"><xref:System.IO.BinaryReader.ReadByte%2A> then reads until <xref:System.IO.BinaryReader.PeekChar%2A> finds no more bytes.</span></span>  
  
 [!code-csharp[System.IO.StreamReader#21](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.StreamReader/CS/source3.cs#21)]
 [!code-vb[System.IO.StreamReader#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.StreamReader/VB/source3.vb#21)]  
  
## <a name="see-also"></a><span data-ttu-id="5548d-121">请参阅</span><span class="sxs-lookup"><span data-stu-id="5548d-121">See also</span></span>

- <xref:System.IO.StreamReader>
- <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=nameWithType>
- <xref:System.IO.StreamReader.Peek%2A?displayProperty=nameWithType>
- <xref:System.IO.FileStream>
- <xref:System.IO.BinaryReader>
- <xref:System.IO.BinaryReader.ReadByte%2A?displayProperty=nameWithType>
- <xref:System.IO.BinaryReader.PeekChar%2A?displayProperty=nameWithType>
