---
title: 如何：在独立存储中查找现有文件和目录
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- stores, finding files and directories
- locating files in isolated storage file
- directories [.NET], isolated storage
- isolated storage, finding files and directories
- data storage using isolated storage, finding files and directories
- files [.NET], isolated storage
- data stores, finding files and directories
- locating directories in isolated storage file
- storing data using isolated storage, finding files and directories
ms.assetid: eb28458a-6161-4e7a-9ada-30ef93761b5c
ms.openlocfilehash: 00d960f536d4094f9f62a37637dfcaec3916fb5b
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188739"
---
# <a name="how-to-find-existing-files-and-directories-in-isolated-storage"></a><span data-ttu-id="4a337-102">如何：在独立存储中查找现有文件和目录</span><span class="sxs-lookup"><span data-stu-id="4a337-102">How to: Find Existing Files and Directories in Isolated Storage</span></span>

<span data-ttu-id="4a337-103">为了搜索独立存储中的目录，请使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="4a337-103">To search for a directory in isolated storage, use the <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="4a337-104">此方法接受表示搜索模式的字符串。</span><span class="sxs-lookup"><span data-stu-id="4a337-104">This method takes a string that represents a search pattern.</span></span> <span data-ttu-id="4a337-105">你可以在搜索模式中使用单字符 (?) 和多字符 (\*) 通配符，但是通配符必须出现在名称的最后一部分。</span><span class="sxs-lookup"><span data-stu-id="4a337-105">You can use both single-character (?) and multi-character (\*) wildcard characters in the search pattern, but the wildcard characters must appear in the final portion of the name.</span></span> <span data-ttu-id="4a337-106">例如，`directory1/*ect*` 是有效的搜索字符串，但 `*ect*/directory2` 不是。</span><span class="sxs-lookup"><span data-stu-id="4a337-106">For example, `directory1/*ect*` is a valid search string, but `*ect*/directory2` is not.</span></span>  
  
 <span data-ttu-id="4a337-107">若要搜索文件，请使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="4a337-107">To search for a file, use the <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="4a337-108">对适用于 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A> 的搜索字符串中通配符的限制也适用于 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A>。</span><span class="sxs-lookup"><span data-stu-id="4a337-108">The restriction for wildcard characters in search strings that applies to <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A> also applies to <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A>.</span></span>  
  
 <span data-ttu-id="4a337-109">这些方法都不是递归的；<xref:System.IO.IsolatedStorage.IsolatedStorageFile> 类不提供用于列出存储区中所有目录或文件的任何方法。</span><span class="sxs-lookup"><span data-stu-id="4a337-109">Neither of these methods is recursive; the <xref:System.IO.IsolatedStorage.IsolatedStorageFile> class does not supply any methods for listing all directories or files in your store.</span></span> <span data-ttu-id="4a337-110">但是，在下面的代码示例中显示有递归方法。</span><span class="sxs-lookup"><span data-stu-id="4a337-110">However, recursive methods are shown in the following code example.</span></span>  
  
## <a name="example"></a><span data-ttu-id="4a337-111">示例</span><span class="sxs-lookup"><span data-stu-id="4a337-111">Example</span></span>  
 <span data-ttu-id="4a337-112">下面的代码示例展示了如何在独立存储中创建文件和目录。</span><span class="sxs-lookup"><span data-stu-id="4a337-112">The following code example illustrates how to create files and directories in an isolated store.</span></span> <span data-ttu-id="4a337-113">首先，检索一个为用户、域和程序集隔离的存储区，并放入 `isoStore` 变量。</span><span class="sxs-lookup"><span data-stu-id="4a337-113">First, a store that is isolated for user, domain, and assembly is retrieved and placed in the `isoStore` variable.</span></span> <span data-ttu-id="4a337-114"><xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateDirectory%2A> 方法用于设置几个不同的目录，<xref:System.IO.IsolatedStorage.IsolatedStorageFileStream.%23ctor%28System.String%2CSystem.IO.FileMode%2CSystem.IO.IsolatedStorage.IsolatedStorageFile%29> 构造函数在这些目录中创建了一些文件。</span><span class="sxs-lookup"><span data-stu-id="4a337-114">The <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateDirectory%2A> method is used to set up a few different directories, and the <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream.%23ctor%28System.String%2CSystem.IO.FileMode%2CSystem.IO.IsolatedStorage.IsolatedStorageFile%29> constructor creates some files in these directories.</span></span> <span data-ttu-id="4a337-115">然后，代码循环访问 `GetAllDirectories` 方法的结果。</span><span class="sxs-lookup"><span data-stu-id="4a337-115">The code then loops through the results of the `GetAllDirectories` method.</span></span> <span data-ttu-id="4a337-116">该方法使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A> 来查找当前目录中的所有目录名。</span><span class="sxs-lookup"><span data-stu-id="4a337-116">This method uses <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A> to find all the directory names in the current directory.</span></span> <span data-ttu-id="4a337-117">这些名称存储在数组中，然后 `GetAllDirectories` 调用其本身，传入它所找到的每个目录。</span><span class="sxs-lookup"><span data-stu-id="4a337-117">These names are stored in an array, and then `GetAllDirectories` calls itself, passing in each directory it has found.</span></span> <span data-ttu-id="4a337-118">结果是所有目录名都返回到数组中。</span><span class="sxs-lookup"><span data-stu-id="4a337-118">As a result, all the directory names are returned in an array.</span></span> <span data-ttu-id="4a337-119">接下来，代码调用 `GetAllFiles` 方法。</span><span class="sxs-lookup"><span data-stu-id="4a337-119">Next, the code calls the `GetAllFiles` method.</span></span> <span data-ttu-id="4a337-120">该方法调用 `GetAllDirectories` 来查找所有目录的名称，然后它使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A> 方法检查文件的每个目录。</span><span class="sxs-lookup"><span data-stu-id="4a337-120">This method calls `GetAllDirectories` to find out the names of all the directories, and then it checks each directory for files by using the <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A> method.</span></span> <span data-ttu-id="4a337-121">结果是在数组中返回，以供显示。</span><span class="sxs-lookup"><span data-stu-id="4a337-121">The result is returned in an array for display.</span></span>  
  
 [!code-cpp[Conceptual.IsolatedStorage#9](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source8.cpp#9)]
 [!code-csharp[Conceptual.IsolatedStorage#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source8.cs#9)]
 [!code-vb[Conceptual.IsolatedStorage#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source8.vb#9)]  
  
## <a name="see-also"></a><span data-ttu-id="4a337-122">另请参阅</span><span class="sxs-lookup"><span data-stu-id="4a337-122">See also</span></span>

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile>
- [<span data-ttu-id="4a337-123">独立存储</span><span class="sxs-lookup"><span data-stu-id="4a337-123">Isolated Storage</span></span>](isolated-storage.md)
