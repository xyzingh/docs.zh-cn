---
title: 如何：在独立存储中删除文件和目录
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- data storage using isolated storage, deleting files and directories
- directories [.NET], isolated storage
- files [.NET], isolated storage
- isolated storage, deleting files and directories
- data stores, deleting files and directories
- stores, creating files and directories
- deleting files within isolated stage file
- storing data using isolated storage, deleting files and directories
- deleting directories within isolated stage file
ms.assetid: 8fcc0dea-435b-4d40-ba4d-ba056265c202
ms.openlocfilehash: 7797f319ca3b143bac6a4e68eaf820e966f1560e
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93187939"
---
# <a name="how-to-delete-files-and-directories-in-isolated-storage"></a><span data-ttu-id="57979-102">如何：在独立存储中删除文件和目录</span><span class="sxs-lookup"><span data-stu-id="57979-102">How to: Delete Files and Directories in Isolated Storage</span></span>
<span data-ttu-id="57979-103">可以删除独立存储文件中的目录和文件。</span><span class="sxs-lookup"><span data-stu-id="57979-103">You can delete directories and files within an isolated storage file.</span></span> <span data-ttu-id="57979-104">在存储区中，文件名和目录名依赖于操作系统，并指定为虚拟文件系统根目录的相对路径。</span><span class="sxs-lookup"><span data-stu-id="57979-104">Within a store, file and directory names are operating-system dependent and are specified as relative to the root of the virtual file system.</span></span> <span data-ttu-id="57979-105">在 Windows 操作系统中，它们不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="57979-105">They are not case-sensitive on Windows operating systems.</span></span>  
  
 <span data-ttu-id="57979-106"><xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=nameWithType> 类提供了两个用于删除目录和文件的方法：<xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> 和 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteFile%2A>。</span><span class="sxs-lookup"><span data-stu-id="57979-106">The <xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=nameWithType> class supplies two methods for deleting directories and files: <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> and <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteFile%2A>.</span></span> <span data-ttu-id="57979-107">如果尝试删除并不存在的文件和目录，则会引发 <xref:System.IO.IsolatedStorage.IsolatedStorageException> 异常。</span><span class="sxs-lookup"><span data-stu-id="57979-107">An <xref:System.IO.IsolatedStorage.IsolatedStorageException> exception is thrown if you try to delete a file or directory that does not exist.</span></span> <span data-ttu-id="57979-108">如果在名称中包含通配符，<xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> 将引发 <xref:System.IO.IsolatedStorage.IsolatedStorageException> 异常，并且 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteFile%2A> 会引发 <xref:System.ArgumentException> 异常。</span><span class="sxs-lookup"><span data-stu-id="57979-108">If you include a wildcard character in the name, <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> throws an <xref:System.IO.IsolatedStorage.IsolatedStorageException> exception, and <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteFile%2A> throws an <xref:System.ArgumentException> exception.</span></span>  
  
 <span data-ttu-id="57979-109">如果目录中包含任何文件或子目录，<xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> 方法将会失败。</span><span class="sxs-lookup"><span data-stu-id="57979-109">The <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> method fails if the directory contains any files or subdirectories.</span></span> <span data-ttu-id="57979-110">可以使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A> 和 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A> 方法检索现有文件和目录。</span><span class="sxs-lookup"><span data-stu-id="57979-110">You can use the <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A> and <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A> methods to retrieve the existing files and directories.</span></span> <span data-ttu-id="57979-111">若要详细了解如何搜索存储的虚拟文件系统，请参阅[如何：在独立存储中查找现有文件和目录](how-to-find-existing-files-and-directories-in-isolated-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="57979-111">For more information about searching the virtual file system of a store, see [How to: Find Existing Files and Directories in Isolated Storage](how-to-find-existing-files-and-directories-in-isolated-storage.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="57979-112">示例</span><span class="sxs-lookup"><span data-stu-id="57979-112">Example</span></span>  
 <span data-ttu-id="57979-113">下面的代码示例创建并删除多个目录和文件。</span><span class="sxs-lookup"><span data-stu-id="57979-113">The following code example creates and then deletes several directories and files.</span></span>  
  
 [!code-cpp[Conceptual.IsolatedStorage#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source4.cpp#4)]
 [!code-csharp[Conceptual.IsolatedStorage#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source4.cs#4)]
 [!code-vb[Conceptual.IsolatedStorage#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source4.vb#4)]  
  
## <a name="see-also"></a><span data-ttu-id="57979-114">另请参阅</span><span class="sxs-lookup"><span data-stu-id="57979-114">See also</span></span>

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=nameWithType>
- [<span data-ttu-id="57979-115">独立存储</span><span class="sxs-lookup"><span data-stu-id="57979-115">Isolated Storage</span></span>](isolated-storage.md)
