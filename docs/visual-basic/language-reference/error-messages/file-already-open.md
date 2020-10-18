---
title: 文件已打开
ms.date: 07/20/2015
f1_keywords:
- vbrID55
ms.assetid: d674a0fb-ef16-4cc2-9da7-709a8a07dbea
ms.openlocfilehash: ce8f8bf96d7355e45b2df82e8a131472c2ed2367
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162747"
---
# <a name="file-already-open"></a><span data-ttu-id="d94dd-102">文件已打开</span><span class="sxs-lookup"><span data-stu-id="d94dd-102">File already open</span></span>

<span data-ttu-id="d94dd-103">有时，必须先关闭文件，然后才能 `FileOpen` 进行其他或其他操作。</span><span class="sxs-lookup"><span data-stu-id="d94dd-103">Sometimes a file must be closed before another `FileOpen` or other operation can occur.</span></span> <span data-ttu-id="d94dd-104">此错误的可能原因包括：</span><span class="sxs-lookup"><span data-stu-id="d94dd-104">Among the possible causes of this error are:</span></span>

- <span data-ttu-id="d94dd-105">`FileOpen`为已打开的文件执行了顺序输出模式操作</span><span class="sxs-lookup"><span data-stu-id="d94dd-105">A sequential output mode `FileOpen` operation was executed for a file that is already open</span></span>

- <span data-ttu-id="d94dd-106">语句引用打开的文件。</span><span class="sxs-lookup"><span data-stu-id="d94dd-106">A statement refers to an open file.</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="d94dd-107">更正此错误</span><span class="sxs-lookup"><span data-stu-id="d94dd-107">To correct this error</span></span>

- <span data-ttu-id="d94dd-108">在执行语句前关闭文件。</span><span class="sxs-lookup"><span data-stu-id="d94dd-108">Close the file before executing the statement.</span></span>

## <a name="see-also"></a><span data-ttu-id="d94dd-109">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d94dd-109">See also</span></span>

- <xref:Microsoft.VisualBasic.FileSystem.FileOpen%2A>
