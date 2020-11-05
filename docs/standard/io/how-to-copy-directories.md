---
title: 如何：复制目录
description: 了解如何使用 I/O 类来复制目录，这些类可将一个目录下的内容同步复制到另一个位置。
ms.date: 12/27/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- directory copying
- I/O [.NET], copying directories
- subdirectory copying
- copying directories
- directories [.NET], copying
ms.assetid: 5a969765-e5f8-4b4e-977e-90e2b0a1fe3c
ms.openlocfilehash: 476473d5c25ce29d070abbeef7fa29a7cb9621e1
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93187978"
---
# <a name="how-to-copy-directories"></a><span data-ttu-id="33e67-103">如何：复制目录</span><span class="sxs-lookup"><span data-stu-id="33e67-103">How to: Copy directories</span></span>

<span data-ttu-id="33e67-104">本文演示如何使用 I/O 类将目录下的内容同步复制到另一个位置。</span><span class="sxs-lookup"><span data-stu-id="33e67-104">This article demonstrates how to use I/O classes to synchronously copy the contents of a directory to another location.</span></span>

<span data-ttu-id="33e67-105">有关异步文件复制的示例，请参阅[异步文件 I/O](asynchronous-file-i-o.md)。</span><span class="sxs-lookup"><span data-stu-id="33e67-105">For an example of asynchronous file copy, see [Asynchronous file I/O](asynchronous-file-i-o.md).</span></span>

<span data-ttu-id="33e67-106">此示例通过将 `DirectoryCopy` 方法的 `copySubDirs` 设置为 `true` 来复制子目录。</span><span class="sxs-lookup"><span data-stu-id="33e67-106">This example copies subdirectories by setting the `copySubDirs` of the `DirectoryCopy` method to `true`.</span></span> <span data-ttu-id="33e67-107">`DirectoryCopy` 方法通过对每个子目录调用其自身的方法来递归复制它们，直到再也没有子目录可以复制为止。</span><span class="sxs-lookup"><span data-stu-id="33e67-107">The `DirectoryCopy` method recursively copies subdirectories by calling itself on each subdirectory until there are no more to copy.</span></span>  
  
## <a name="example"></a><span data-ttu-id="33e67-108">示例</span><span class="sxs-lookup"><span data-stu-id="33e67-108">Example</span></span>  
 [!code-csharp[System.IO.Directory_Copy#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Directory_Copy/cs/program.cs#1)]
 [!code-vb[System.IO.Directory_Copy#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Directory_Copy/vb/Program.vb#1)]  
  
[!INCLUDE [localized code comments](../../../includes/code-comments-loc.md)]

## <a name="see-also"></a><span data-ttu-id="33e67-109">请参阅</span><span class="sxs-lookup"><span data-stu-id="33e67-109">See also</span></span>

- <xref:System.IO.FileInfo>
- <xref:System.IO.DirectoryInfo>
- <xref:System.IO.FileStream>
- [<span data-ttu-id="33e67-110">文件和流 I/O</span><span class="sxs-lookup"><span data-stu-id="33e67-110">File and stream I/O</span></span>](index.md)
- [<span data-ttu-id="33e67-111">通用 I/O 任务</span><span class="sxs-lookup"><span data-stu-id="33e67-111">Common I/O tasks</span></span>](common-i-o-tasks.md)
- [<span data-ttu-id="33e67-112">异步文件 I/O</span><span class="sxs-lookup"><span data-stu-id="33e67-112">Asynchronous file I/O</span></span>](asynchronous-file-i-o.md)
