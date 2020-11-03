---
title: 如何：使用数据保护
description: 了解如何通过访问 .NET 中的数据保护 API (DPAPI) 来使用数据保护。
ms.date: 07/14/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DPAPI
- encryption [.NET], data protection API
- data [.NET], decryption
- ProtectedMemory class, about ProtectedMemory class
- ProtectedData class, about ProtectedData class
- cryptography [.NET], data protection API
- data protection API [.NET]
- decryption
- data [.NET], encryption
ms.assetid: 606698b0-cb1a-42ca-beeb-0bea34205d20
ms.openlocfilehash: d3fe7ef3ddbc6e75a248101829b11a8abcb3c15a
ms.sourcegitcommit: 74d05613d6c57106f83f82ce8ee71176874ea3f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93282056"
---
# <a name="how-to-use-data-protection"></a><span data-ttu-id="910f7-103">如何：使用数据保护</span><span class="sxs-lookup"><span data-stu-id="910f7-103">How to: Use Data Protection</span></span>

> [!NOTE]
> <span data-ttu-id="910f7-104">本文适用于 Windows。</span><span class="sxs-lookup"><span data-stu-id="910f7-104">This article applies to Windows.</span></span>
>
> <span data-ttu-id="910f7-105">有关 ASP.NET Core 的信息，请参阅 [ASP.NET Core 数据保护](/aspnet/core/security/data-protection/introduction)。</span><span class="sxs-lookup"><span data-stu-id="910f7-105">For information about ASP.NET Core, see [ASP.NET Core Data Protection](/aspnet/core/security/data-protection/introduction).</span></span>

<span data-ttu-id="910f7-106">.NET 提供对数据保护 API 的访问 (DPAPI) ，这允许你使用来自当前用户帐户或计算机的信息加密数据。</span><span class="sxs-lookup"><span data-stu-id="910f7-106">.NET provides access to the data protection API (DPAPI), which allows you to encrypt data using information from the current user account or computer.</span></span>  <span data-ttu-id="910f7-107">当使用 DPAPI 时，你会使显式生成和存储加密密钥的困难问题得到缓解。</span><span class="sxs-lookup"><span data-stu-id="910f7-107">When you use the DPAPI, you alleviate the difficult problem of explicitly generating and storing a cryptographic key.</span></span>  
  
<span data-ttu-id="910f7-108">使用 <xref:System.Security.Cryptography.ProtectedData> 类来加密字节数组的副本。</span><span class="sxs-lookup"><span data-stu-id="910f7-108">Use the <xref:System.Security.Cryptography.ProtectedData> class to encrypt a copy of an array of bytes.</span></span> <span data-ttu-id="910f7-109">此功能在 .NET Framework、.NET Core 和 .NET 5 中可用。</span><span class="sxs-lookup"><span data-stu-id="910f7-109">This functionality is available in .NET Framework, .NET Core, and .NET 5.</span></span>  <span data-ttu-id="910f7-110">你可以指定由当前用户帐户加密的数据仅能通过相同的用户帐户解密，也可以指定由当前用户帐户加密的数据可以通过计算机上的任何帐户进行解密。</span><span class="sxs-lookup"><span data-stu-id="910f7-110">You can specify that data encrypted by the current user account can be decrypted only by the same user account, or you can specify that data encrypted by the current user account can be decrypted by any account on the computer.</span></span>  <span data-ttu-id="910f7-111">请参阅 <xref:System.Security.Cryptography.DataProtectionScope> 枚举以获取 <xref:System.Security.Cryptography.ProtectedData> 选项的详细说明。</span><span class="sxs-lookup"><span data-stu-id="910f7-111">See the <xref:System.Security.Cryptography.DataProtectionScope> enumeration for a detailed description of <xref:System.Security.Cryptography.ProtectedData> options.</span></span>  
  
## <a name="encrypt-data-to-a-file-or-stream-using-data-protection"></a><span data-ttu-id="910f7-112">使用数据保护将数据加密到文件或流</span><span class="sxs-lookup"><span data-stu-id="910f7-112">Encrypt data to a file or stream using data protection</span></span>  
  
1. <span data-ttu-id="910f7-113">创建随机平均信息量。</span><span class="sxs-lookup"><span data-stu-id="910f7-113">Create random entropy.</span></span>  
  
2. <span data-ttu-id="910f7-114">调用静态 <xref:System.Security.Cryptography.ProtectedData.Protect%2A> 方法，同时传递要加密的字节数组、平均信息量和数据保护范围。</span><span class="sxs-lookup"><span data-stu-id="910f7-114">Call the static <xref:System.Security.Cryptography.ProtectedData.Protect%2A> method while passing an array of bytes to encrypt, the entropy, and the data protection scope.</span></span>  
  
3. <span data-ttu-id="910f7-115">将加密的数据写入文件或流。</span><span class="sxs-lookup"><span data-stu-id="910f7-115">Write the encrypted data to a file or stream.</span></span>  
  
### <a name="to-decrypt-data-from-a-file-or-stream-using-data-protection"></a><span data-ttu-id="910f7-116">若要使用数据保护从文件或流解密数据</span><span class="sxs-lookup"><span data-stu-id="910f7-116">To decrypt data from a file or stream using data protection</span></span>  
  
1. <span data-ttu-id="910f7-117">从文件或流中读取加密的数据。</span><span class="sxs-lookup"><span data-stu-id="910f7-117">Read the encrypted data from a file or stream.</span></span>  
  
2. <span data-ttu-id="910f7-118">调用静态 <xref:System.Security.Cryptography.ProtectedData.Unprotect%2A> 方法，同时传递要解密的字节数组和数据保护范围。</span><span class="sxs-lookup"><span data-stu-id="910f7-118">Call the static <xref:System.Security.Cryptography.ProtectedData.Unprotect%2A> method while passing an array of bytes to decrypt and the data protection scope.</span></span>  
  
## <a name="example"></a><span data-ttu-id="910f7-119">示例</span><span class="sxs-lookup"><span data-stu-id="910f7-119">Example</span></span>

<span data-ttu-id="910f7-120">下面的代码示例演示加密和解密的两种形式。</span><span class="sxs-lookup"><span data-stu-id="910f7-120">The following code example demonstrates two forms of encryption and decryption.</span></span>  <span data-ttu-id="910f7-121">首先，该代码示例对内存中的字节数组进行加密，然后将其解密。</span><span class="sxs-lookup"><span data-stu-id="910f7-121">First, the code example encrypts and then decrypts an in-memory array of bytes.</span></span>  <span data-ttu-id="910f7-122">接下来，该代码示例对字节数组的副本进行加密、将其保存到文件、从文件加载回数据，然后对数据进行解密。</span><span class="sxs-lookup"><span data-stu-id="910f7-122">Next, the code example encrypts a copy of a byte array, saves it to a file, loads the data back from the file, and then decrypts the data.</span></span>  <span data-ttu-id="910f7-123">此示例显示原始数据、加密的数据和已解密的数据。</span><span class="sxs-lookup"><span data-stu-id="910f7-123">The example displays the original data, the encrypted data, and the decrypted data.</span></span>

[!code-csharp[DPAPI-HowTO#1](../../../samples/snippets/csharp/VS_Snippets_CLR/DPAPI-HowTO/cs/sample.cs#1)]
[!code-vb[DPAPI-HowTO#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DPAPI-HowTO/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a><span data-ttu-id="910f7-124">编译代码</span><span class="sxs-lookup"><span data-stu-id="910f7-124">Compiling the Code</span></span>  

<span data-ttu-id="910f7-125">此示例仅在面向 .NET Framework 并在 Windows 上运行时才会编译和运行。</span><span class="sxs-lookup"><span data-stu-id="910f7-125">This example compiles and runs only when targeting .NET Framework and running on Windows.</span></span>

- <span data-ttu-id="910f7-126">包括对 `System.Security.dll` 的引用。</span><span class="sxs-lookup"><span data-stu-id="910f7-126">Include a reference to `System.Security.dll`.</span></span>  
  
- <span data-ttu-id="910f7-127">包括 <xref:System>、<xref:System.IO>、<xref:System.Security.Cryptography> 和 <xref:System.Text> 命名空间。</span><span class="sxs-lookup"><span data-stu-id="910f7-127">Include the <xref:System>, <xref:System.IO>, <xref:System.Security.Cryptography>, and <xref:System.Text> namespace.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="910f7-128">另请参阅</span><span class="sxs-lookup"><span data-stu-id="910f7-128">See also</span></span>

- [<span data-ttu-id="910f7-129">加密模型</span><span class="sxs-lookup"><span data-stu-id="910f7-129">Cryptography Model</span></span>](cryptography-model.md)
- [<span data-ttu-id="910f7-130">加密服务</span><span class="sxs-lookup"><span data-stu-id="910f7-130">Cryptographic Services</span></span>](cryptographic-services.md)
- [<span data-ttu-id="910f7-131">跨平台加密</span><span class="sxs-lookup"><span data-stu-id="910f7-131">Cross-Platform Cryptography</span></span>](cross-platform-cryptography.md)
- <xref:System.Security.Cryptography.ProtectedMemory>
- <xref:System.Security.Cryptography.ProtectedData>
- [<span data-ttu-id="910f7-132">ASP.NET Core 数据保护</span><span class="sxs-lookup"><span data-stu-id="910f7-132">ASP.NET Core Data Protection</span></span>](/aspnet/core/security/data-protection/introduction)
