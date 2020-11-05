---
title: 如何：使用 PLINQ 循环访问文件目录
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- PLINQ queries, how to iterate directories
ms.assetid: 354e8ce3-35c4-431c-99ca-7661d1f3901b
ms.openlocfilehash: 5033cc24fce5fc17a950e4797de1ef4071e2b98a
ms.sourcegitcommit: 6d09ae36acba0b0e2ba47999f8f1a725795462a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2020
ms.locfileid: "92925371"
---
# <a name="how-to-iterate-file-directories-with-plinq"></a><span data-ttu-id="91924-102">如何：使用 PLINQ 循环访问文件目录</span><span class="sxs-lookup"><span data-stu-id="91924-102">How to: Iterate File Directories with PLINQ</span></span>

<span data-ttu-id="91924-103">本文展示了两种方法，以对文件目录平行执行操作。</span><span class="sxs-lookup"><span data-stu-id="91924-103">This article shows two ways to parallelize operations on file directories.</span></span> <span data-ttu-id="91924-104">第一个查询使用 <xref:System.IO.Directory.GetFiles%2A> 方法，在数组中填充目录和所有子目录中的文件名。</span><span class="sxs-lookup"><span data-stu-id="91924-104">The first query uses the <xref:System.IO.Directory.GetFiles%2A> method to populate an array of file names in a directory and all subdirectories.</span></span> <span data-ttu-id="91924-105">在整个数组填充完成前，此方法不会返回数组，所以可能会在操作开始时引入延迟。</span><span class="sxs-lookup"><span data-stu-id="91924-105">This method can introduce latency at the beginning of the operation, because it doesn't return until the entire array is populated.</span></span> <span data-ttu-id="91924-106">不过，在填充数组后，PLINQ 可以快速地并行处理数组。</span><span class="sxs-lookup"><span data-stu-id="91924-106">However, after the array is populated, PLINQ can process it in parallel quickly.</span></span>  
  
<span data-ttu-id="91924-107">第二个查询使用立即开始返回结果的静态 <xref:System.IO.Directory.EnumerateDirectories%2A> 和 <xref:System.IO.DirectoryInfo.EnumerateFiles%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="91924-107">The second query uses the static <xref:System.IO.Directory.EnumerateDirectories%2A> and <xref:System.IO.DirectoryInfo.EnumerateFiles%2A> methods, which begin returning results immediately.</span></span> <span data-ttu-id="91924-108">循环访问大型目录树时，这种方法可能会比第一个示例更快，不过处理时间取决于很多因素。</span><span class="sxs-lookup"><span data-stu-id="91924-108">This approach can be faster when you're iterating over large directory trees, but the processing time compared to the first example depends on many factors.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="91924-109">这些示例用于演示用法，可能不会比相当的顺序 LINQ to Objects 查询快。</span><span class="sxs-lookup"><span data-stu-id="91924-109">These examples are intended to demonstrate usage and might not run faster than the equivalent sequential LINQ to Objects query.</span></span> <span data-ttu-id="91924-110">若要详细了解加速，请参阅[了解 PLINQ 中的加速](understanding-speedup-in-plinq.md)。</span><span class="sxs-lookup"><span data-stu-id="91924-110">For more information about speedup, see [Understanding Speedup in PLINQ](understanding-speedup-in-plinq.md).</span></span>  
  
## <a name="getfiles-example"></a><span data-ttu-id="91924-111">GetFiles 示例</span><span class="sxs-lookup"><span data-stu-id="91924-111">GetFiles example</span></span>

 <span data-ttu-id="91924-112">此示例展示了如何在以下简单方案中循环访问文件目录：有权访问树中的所有目录，文件大小不大，访问时间也不是很长。</span><span class="sxs-lookup"><span data-stu-id="91924-112">This example shows how to iterate over file directories in simple scenarios when you have access to all directories in the tree, the file sizes aren't large, and the access times are not significant.</span></span> <span data-ttu-id="91924-113">这种方法在最初构造文件名数组时有一段延迟。</span><span class="sxs-lookup"><span data-stu-id="91924-113">This approach involves a period of latency at the beginning while the array of file names is being constructed.</span></span>  
  
 [!code-csharp[PLINQ#33](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqfileiteration.cs#33)]  
  
## <a name="enumeratefiles-example"></a><span data-ttu-id="91924-114">EnumerateFiles 示例</span><span class="sxs-lookup"><span data-stu-id="91924-114">EnumerateFiles example</span></span>

 <span data-ttu-id="91924-115">此示例展示了如何在以下简单方案中循环访问文件目录：有权访问树中的所有目录，文件大小不大，访问时间也不是很长。</span><span class="sxs-lookup"><span data-stu-id="91924-115">This example shows how to iterate over file directories in simple scenarios when you have access to all directories in the tree, the file sizes aren't large, and the access times are not significant.</span></span> <span data-ttu-id="91924-116">这种方法比上一示例更快地开始生成结果。</span><span class="sxs-lookup"><span data-stu-id="91924-116">This approach begins producing results faster than the previous example.</span></span>  
  
 [!code-csharp[PLINQ#34](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqfileiteration.cs#34)]  
  
 <span data-ttu-id="91924-117">使用 <xref:System.IO.Directory.GetFiles%2A> 时，请确保有权访问树中的所有目录。</span><span class="sxs-lookup"><span data-stu-id="91924-117">When using <xref:System.IO.Directory.GetFiles%2A>, be sure that you have sufficient permissions on all directories in the tree.</span></span> <span data-ttu-id="91924-118">否则，将引发异常，且不会返回任何结果。</span><span class="sxs-lookup"><span data-stu-id="91924-118">Otherwise, an exception will be thrown and no results will be returned.</span></span> <span data-ttu-id="91924-119">如果在 PLINQ 查询中使用 <xref:System.IO.Directory.EnumerateDirectories%2A>，棘手的是合理处理 I/O 异常，以便能够继续循环访问。</span><span class="sxs-lookup"><span data-stu-id="91924-119">When using the <xref:System.IO.Directory.EnumerateDirectories%2A> in a PLINQ query, it is problematic to handle I/O exceptions in a graceful way that enables you to continue iterating.</span></span> <span data-ttu-id="91924-120">如果代码必须处理 I/O 或未经授权的访问异常，应考虑使用[如何：使用并行类循环访问文件目录](how-to-iterate-file-directories-with-the-parallel-class.md)中介绍的方法。</span><span class="sxs-lookup"><span data-stu-id="91924-120">If your code must handle I/O or unauthorized access exceptions, then you should consider the approach described in [How to: Iterate File Directories with the Parallel Class](how-to-iterate-file-directories-with-the-parallel-class.md).</span></span>  
  
 <span data-ttu-id="91924-121">如果 I/O 延迟造成问题（例如，对于通过网络的文件 I/O），请考虑使用 [TPL 和传统 .NET 异步编程](tpl-and-traditional-async-programming.md)和这篇[博客文章](https://devblogs.microsoft.com/pfxteam/parallel-extensions-and-io/)中介绍的某种异步 I/O 方法。</span><span class="sxs-lookup"><span data-stu-id="91924-121">If I/O latency is an issue, for example with file I/O over a network, consider using one of the asynchronous I/O techniques described in [TPL and Traditional .NET Asynchronous Programming](tpl-and-traditional-async-programming.md) and in this [blog post](https://devblogs.microsoft.com/pfxteam/parallel-extensions-and-io/).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="91924-122">请参阅</span><span class="sxs-lookup"><span data-stu-id="91924-122">See also</span></span>

- [<span data-ttu-id="91924-123">并行 LINQ (PLINQ)</span><span class="sxs-lookup"><span data-stu-id="91924-123">Parallel LINQ (PLINQ)</span></span>](introduction-to-plinq.md)
