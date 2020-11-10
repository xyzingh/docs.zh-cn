---
title: 解密数据
description: 了解如何使用对称算法或非对称算法解密 .NET 中的数据。
ms.date: 07/16/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data [.NET], decryption
- symmetric decryption
- asymmetric decryption
- decryption
ms.assetid: 9b266b6c-a9b2-4d20-afd8-b3a0d8fd48a0
ms.openlocfilehash: 7e8fe5a8b7ed7c217a31a8ee91a5d111257fed45
ms.sourcegitcommit: 30a686fd4377fe6472aa04e215c0de711bc1c322
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94440980"
---
# <a name="decrypting-data"></a><span data-ttu-id="689f2-103">解密数据</span><span class="sxs-lookup"><span data-stu-id="689f2-103">Decrypting Data</span></span>

<span data-ttu-id="689f2-104">解密是加密的反向操作。</span><span class="sxs-lookup"><span data-stu-id="689f2-104">Decryption is the reverse operation of encryption.</span></span> <span data-ttu-id="689f2-105">对于私钥加密，必须知道用于加密数据的密钥和 IV。</span><span class="sxs-lookup"><span data-stu-id="689f2-105">For secret-key encryption, you must know both the key and IV that were used to encrypt the data.</span></span> <span data-ttu-id="689f2-106">对于公钥加密，必须知道公钥（如果使用了私钥来加密数据）或私钥（如果使用了公钥来加密数据）。</span><span class="sxs-lookup"><span data-stu-id="689f2-106">For public-key encryption, you must know either the public key (if the data was encrypted using the private key) or the private key (if the data was encrypted using the public key).</span></span>

## <a name="symmetric-decryption"></a><span data-ttu-id="689f2-107">对称解密</span><span class="sxs-lookup"><span data-stu-id="689f2-107">Symmetric Decryption</span></span>

<span data-ttu-id="689f2-108">解密用对称算法加密的数据类似于用对称算法加密数据的过程。</span><span class="sxs-lookup"><span data-stu-id="689f2-108">The decryption of data encrypted with symmetric algorithms is similar to the process used to encrypt data with symmetric algorithms.</span></span> <span data-ttu-id="689f2-109"><xref:System.Security.Cryptography.CryptoStream>类与 .net 提供的对称加密类一起使用，对从任何托管流对象中读取的数据进行解密。</span><span class="sxs-lookup"><span data-stu-id="689f2-109">The <xref:System.Security.Cryptography.CryptoStream> class is used with symmetric cryptography classes provided by .NET to decrypt data read from any managed stream object.</span></span>

<span data-ttu-id="689f2-110">下面的示例演示如何创建算法的默认实现类的新实例 <xref:System.Security.Cryptography.Aes> 。</span><span class="sxs-lookup"><span data-stu-id="689f2-110">The following example illustrates how to create a new instance of the default implementation class for the <xref:System.Security.Cryptography.Aes> algorithm.</span></span> <span data-ttu-id="689f2-111">实例用于对对象执行解密 <xref:System.Security.Cryptography.CryptoStream> 。</span><span class="sxs-lookup"><span data-stu-id="689f2-111">The instance is used to perform decryption on a <xref:System.Security.Cryptography.CryptoStream> object.</span></span> <span data-ttu-id="689f2-112">此示例首先创建实现类的新实例 <xref:System.Security.Cryptography.Aes> 。</span><span class="sxs-lookup"><span data-stu-id="689f2-112">This example first creates a new instance of the <xref:System.Security.Cryptography.Aes> implementation class.</span></span> <span data-ttu-id="689f2-113">它从托管流变量中读取初始化向量 (IV) 值 `myStream` 。</span><span class="sxs-lookup"><span data-stu-id="689f2-113">It reads the initialization vector (IV) value from a managed stream variable, `myStream`.</span></span> <span data-ttu-id="689f2-114">接下来，它将实例化 <xref:System.Security.Cryptography.CryptoStream> 对象并将其初始化为 `myStream` 实例的值。</span><span class="sxs-lookup"><span data-stu-id="689f2-114">Next it instantiates a <xref:System.Security.Cryptography.CryptoStream> object and initializes it to the value of the `myStream` instance.</span></span> <span data-ttu-id="689f2-115">将向 <xref:System.Security.Cryptography.SymmetricAlgorithm.CreateDecryptor%2A?displayProperty=nameWithType> 实例中的方法 <xref:System.Security.Cryptography.Aes> 传递 IV 值和用于加密的相同密钥。</span><span class="sxs-lookup"><span data-stu-id="689f2-115">The <xref:System.Security.Cryptography.SymmetricAlgorithm.CreateDecryptor%2A?displayProperty=nameWithType> method from the <xref:System.Security.Cryptography.Aes> instance is passed the IV value and the same key that was used for encryption.</span></span>

```vb
Dim aes As Aes = Aes.Create()
Dim cryptStream As New CryptoStream(myStream, aes.CreateDecryptor(key, iv), CryptoStreamMode.Read)
```

```csharp
Aes aes = Aes.Create();
CryptoStream cryptStream = new CryptoStream(myStream, aes.CreateDecryptor(key, iv), CryptoStreamMode.Read);
```

<span data-ttu-id="689f2-116">下面的示例显示创建流、解密流、从流中读取和关闭流的整个过程。</span><span class="sxs-lookup"><span data-stu-id="689f2-116">The following example shows the entire process of creating a stream, decrypting the stream, reading from the stream, and closing the streams.</span></span> <span data-ttu-id="689f2-117">将创建一个文件流对象，该对象读取名为 *TestData.txt* 的文件。</span><span class="sxs-lookup"><span data-stu-id="689f2-117">A file stream object is created that reads a file named *TestData.txt*.</span></span> <span data-ttu-id="689f2-118">然后，使用 **CryptoStream** 类和 **Aes** 类对文件流进行解密。</span><span class="sxs-lookup"><span data-stu-id="689f2-118">The file stream is then decrypted using the **CryptoStream** class and the **Aes** class.</span></span> <span data-ttu-id="689f2-119">此示例指定在对称加密示例中用于 [加密数据](encrypting-data.md)的键值。</span><span class="sxs-lookup"><span data-stu-id="689f2-119">This example specifies key value that is used in the symmetric encryption example for [Encrypting Data](encrypting-data.md).</span></span> <span data-ttu-id="689f2-120">它不会显示加密和传输这些值所需的代码。</span><span class="sxs-lookup"><span data-stu-id="689f2-120">It does not show the code needed to encrypt and transfer these values.</span></span>

:::code language="csharp" source="snippets/decrypting-data/csharp/aes-decrypt.cs":::
:::code language="vb" source="snippets/decrypting-data/vb/aes-decrypt.vb":::

<span data-ttu-id="689f2-121">前面的示例使用相同的密钥和对称加密示例中用于 [加密数据](encrypting-data.md)的算法。</span><span class="sxs-lookup"><span data-stu-id="689f2-121">The preceding example uses the same key, and algorithm used in the symmetric encryption example for [Encrypting Data](encrypting-data.md).</span></span> <span data-ttu-id="689f2-122">它对该示例创建的 *TestData.txt* 文件进行解密，并在控制台上显示原始文本。</span><span class="sxs-lookup"><span data-stu-id="689f2-122">It decrypts the *TestData.txt* file that is created by that example and displays the original text on the console.</span></span>

## <a name="asymmetric-decryption"></a><span data-ttu-id="689f2-123">不对称解密</span><span class="sxs-lookup"><span data-stu-id="689f2-123">Asymmetric Decryption</span></span>

<span data-ttu-id="689f2-124">通常，一方（A 方）同时生成公钥和私钥，并将其存储在内存或加密密钥容器中。</span><span class="sxs-lookup"><span data-stu-id="689f2-124">Typically, a party (party A) generates both a public and private key and stores the key either in memory or in a cryptographic key container.</span></span> <span data-ttu-id="689f2-125">然后 A 方将公钥发送到另一方（B 方）。</span><span class="sxs-lookup"><span data-stu-id="689f2-125">Party A then sends the public key to another party (party B).</span></span> <span data-ttu-id="689f2-126">使用公钥时，参与方 B 会对数据进行加密，然后将数据发送回 A 方。接收到数据后，A 方使用对应的私钥将其解密。</span><span class="sxs-lookup"><span data-stu-id="689f2-126">Using the public key, party B encrypts data and sends the data back to party A. After receiving the data, party A decrypts it using the private key that corresponds.</span></span> <span data-ttu-id="689f2-127">A 方只有使用与 B 方用于加密数据的公钥相对应的私钥，解密才能成功。</span><span class="sxs-lookup"><span data-stu-id="689f2-127">Decryption will be successful only if party A uses the private key that corresponds to the public key Party B used to encrypt the data.</span></span>

<span data-ttu-id="689f2-128">有关如何将非对称密钥存储在安全加密密钥容器中以及随后如何获取非对称密钥的信息，请参阅 [How to: Store Asymmetric Keys in a Key Container](how-to-store-asymmetric-keys-in-a-key-container.md)。</span><span class="sxs-lookup"><span data-stu-id="689f2-128">For information on how to store an asymmetric key in secure cryptographic key container and how to later retrieve the asymmetric key, see [How to: Store Asymmetric Keys in a Key Container](how-to-store-asymmetric-keys-in-a-key-container.md).</span></span>

<span data-ttu-id="689f2-129">下面的示例阐释如何对表示一个对称密钥和 IV 的两个字节数组进行解密。</span><span class="sxs-lookup"><span data-stu-id="689f2-129">The following example illustrates the decryption of two arrays of bytes that represent a symmetric key and IV.</span></span> <span data-ttu-id="689f2-130">有关如何以可方便地发送到第三方的格式从 <xref:System.Security.Cryptography.RSA> 对象提取非对称公钥的信息，请参阅 [Encrypting Data](encrypting-data.md)的托管流的值。</span><span class="sxs-lookup"><span data-stu-id="689f2-130">For information on how to extract the asymmetric public key from the <xref:System.Security.Cryptography.RSA> object in a format that you can easily send to a third party, see [Encrypting Data](encrypting-data.md).</span></span>

```vb
'Create a new instance of the RSA class.
Dim rsa As RSA = RSA.Create()

' Export the public key information and send it to a third party.
' Wait for the third party to encrypt some data and send it back.

'Decrypt the symmetric key and IV.
symmetricKey = rsa.Decrypt(encryptedSymmetricKey, RSAEncryptionPadding.Pkcs1)
symmetricIV = rsa.Decrypt(encryptedSymmetricIV, RSAEncryptionPadding.Pkcs1)
```

```csharp
//Create a new instance of the RSA class.
RSA rsa = RSA.Create();

// Export the public key information and send it to a third party.
// Wait for the third party to encrypt some data and send it back.

//Decrypt the symmetric key and IV.
symmetricKey = rsa.Decrypt(encryptedSymmetricKey, RSAEncryptionPadding.Pkcs1);
symmetricIV = rsa.Decrypt(encryptedSymmetricIV , RSAEncryptionPadding.Pkcs1);
```

## <a name="see-also"></a><span data-ttu-id="689f2-131">另请参阅</span><span class="sxs-lookup"><span data-stu-id="689f2-131">See also</span></span>

- [<span data-ttu-id="689f2-132">生成加密和解密的密钥</span><span class="sxs-lookup"><span data-stu-id="689f2-132">Generating Keys for Encryption and Decryption</span></span>](generating-keys-for-encryption-and-decryption.md)
- [<span data-ttu-id="689f2-133">加密数据</span><span class="sxs-lookup"><span data-stu-id="689f2-133">Encrypting Data</span></span>](encrypting-data.md)
- [<span data-ttu-id="689f2-134">加密服务</span><span class="sxs-lookup"><span data-stu-id="689f2-134">Cryptographic Services</span></span>](cryptographic-services.md)
- [<span data-ttu-id="689f2-135">加密模型</span><span class="sxs-lookup"><span data-stu-id="689f2-135">Cryptography Model</span></span>](cryptography-model.md)
- [<span data-ttu-id="689f2-136">跨平台加密</span><span class="sxs-lookup"><span data-stu-id="689f2-136">Cross-Platform Cryptography</span></span>](cross-platform-cryptography.md)
- [<span data-ttu-id="689f2-137">使用填充对 CBC 模式对称解密的漏洞进行计时</span><span class="sxs-lookup"><span data-stu-id="689f2-137">Timing vulnerabilities with CBC-mode symmetric decryption using padding</span></span>](vulnerabilities-cbc-mode.md)
- [<span data-ttu-id="689f2-138">ASP.NET Core 数据保护</span><span class="sxs-lookup"><span data-stu-id="689f2-138">ASP.NET Core Data Protection</span></span>](/aspnet/core/security/data-protection/introduction)
