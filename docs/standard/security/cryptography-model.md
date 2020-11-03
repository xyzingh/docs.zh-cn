---
title: .NET 加密模型
description: 查看 .NET 中的常用加密算法实现。 了解对象继承、流设计、& 配置的可扩展加密模型。
ms.date: 07/14/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cryptography [.NET], model
- encryption [.NET], model
ms.assetid: 12fecad4-fbab-432a-bade-2f05976a2971
ms.openlocfilehash: a157a9a76f87a2a56c616b76c933e6d8d6415b03
ms.sourcegitcommit: 74d05613d6c57106f83f82ce8ee71176874ea3f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93281579"
---
# <a name="net-cryptography-model"></a><span data-ttu-id="d0e90-104">.NET 加密模型</span><span class="sxs-lookup"><span data-stu-id="d0e90-104">.NET Cryptography Model</span></span>

<span data-ttu-id="d0e90-105">.NET 提供许多标准加密算法的实现，.NET 加密模型是可扩展的。</span><span class="sxs-lookup"><span data-stu-id="d0e90-105">.NET provides implementations of many standard cryptographic algorithms, and the .NET cryptography model is extensible.</span></span>

## <a name="object-inheritance"></a><span data-ttu-id="d0e90-106">对象继承</span><span class="sxs-lookup"><span data-stu-id="d0e90-106">Object Inheritance</span></span>

<span data-ttu-id="d0e90-107">.NET 加密系统实现了派生类继承的可扩展模式。</span><span class="sxs-lookup"><span data-stu-id="d0e90-107">The .NET cryptography system implements an extensible pattern of derived class inheritance.</span></span> <span data-ttu-id="d0e90-108">层次结构如下所示：</span><span class="sxs-lookup"><span data-stu-id="d0e90-108">The hierarchy is as follows:</span></span>

- <span data-ttu-id="d0e90-109">算法类型类，如 <xref:System.Security.Cryptography.SymmetricAlgorithm> 、  <xref:System.Security.Cryptography.AsymmetricAlgorithm> 或 <xref:System.Security.Cryptography.HashAlgorithm> 。</span><span class="sxs-lookup"><span data-stu-id="d0e90-109">Algorithm type class, such as <xref:System.Security.Cryptography.SymmetricAlgorithm>,  <xref:System.Security.Cryptography.AsymmetricAlgorithm>, or <xref:System.Security.Cryptography.HashAlgorithm>.</span></span> <span data-ttu-id="d0e90-110">此级别是抽象的。</span><span class="sxs-lookup"><span data-stu-id="d0e90-110">This level is abstract.</span></span>

- <span data-ttu-id="d0e90-111">从算法类型类继承的算法类；例如，<xref:System.Security.Cryptography.Aes>、<xref:System.Security.Cryptography.RSA> 或 <xref:System.Security.Cryptography.ECDiffieHellman>。</span><span class="sxs-lookup"><span data-stu-id="d0e90-111">Algorithm class that inherits from an algorithm type class; for example, <xref:System.Security.Cryptography.Aes>, <xref:System.Security.Cryptography.RSA>, or <xref:System.Security.Cryptography.ECDiffieHellman>.</span></span> <span data-ttu-id="d0e90-112">此级别是抽象的。</span><span class="sxs-lookup"><span data-stu-id="d0e90-112">This level is abstract.</span></span>

- <span data-ttu-id="d0e90-113">从算法类继承的算法类实现；例如，<xref:System.Security.Cryptography.AesManaged>、<xref:System.Security.Cryptography.RC2CryptoServiceProvider> 或 <xref:System.Security.Cryptography.ECDiffieHellmanCng>。</span><span class="sxs-lookup"><span data-stu-id="d0e90-113">Implementation of an algorithm class that inherits from an algorithm class; for example, <xref:System.Security.Cryptography.AesManaged>, <xref:System.Security.Cryptography.RC2CryptoServiceProvider>, or <xref:System.Security.Cryptography.ECDiffieHellmanCng>.</span></span> <span data-ttu-id="d0e90-114">此级别已完全实现。</span><span class="sxs-lookup"><span data-stu-id="d0e90-114">This level is fully implemented.</span></span>

<span data-ttu-id="d0e90-115">这种派生类模式允许您添加新算法或现有算法的新实现。</span><span class="sxs-lookup"><span data-stu-id="d0e90-115">This pattern of derived classes lets you add a new algorithm or a new implementation of an existing algorithm.</span></span> <span data-ttu-id="d0e90-116">例如，要创建新的公共密钥算法，你会继承 <xref:System.Security.Cryptography.AsymmetricAlgorithm> 类。</span><span class="sxs-lookup"><span data-stu-id="d0e90-116">For example, to create a new public-key algorithm, you would inherit from the <xref:System.Security.Cryptography.AsymmetricAlgorithm> class.</span></span> <span data-ttu-id="d0e90-117">要创建特定算法的新实现，将需要创建该算法的非抽象派生类。</span><span class="sxs-lookup"><span data-stu-id="d0e90-117">To create a new implementation of a specific algorithm, you would create a non-abstract derived class of that algorithm.</span></span>

## <a name="how-algorithms-are-implemented-in-net"></a><span data-ttu-id="d0e90-118">如何在 .NET 中实现算法</span><span class="sxs-lookup"><span data-stu-id="d0e90-118">How Algorithms Are Implemented in .NET</span></span>

<span data-ttu-id="d0e90-119">作为可用于一种算法的不同实现的示例，请考虑对称算法。</span><span class="sxs-lookup"><span data-stu-id="d0e90-119">As an example of the different implementations available for an algorithm, consider symmetric algorithms.</span></span> <span data-ttu-id="d0e90-120">所有对称算法的基数都是 <xref:System.Security.Cryptography.SymmetricAlgorithm> ，它由 <xref:System.Security.Cryptography.Aes> 、和继承， <xref:System.Security.Cryptography.TripleDES> 并且不再推荐使用。</span><span class="sxs-lookup"><span data-stu-id="d0e90-120">The base for all symmetric algorithms is <xref:System.Security.Cryptography.SymmetricAlgorithm>, which is inherited by <xref:System.Security.Cryptography.Aes>, <xref:System.Security.Cryptography.TripleDES>, and others that are no longer recommended.</span></span>

<span data-ttu-id="d0e90-121"><xref:System.Security.Cryptography.Aes> 由 <xref:System.Security.Cryptography.AesCryptoServiceProvider> 、和继承 <xref:System.Security.Cryptography.AesCng> <xref:System.Security.Cryptography.AesManaged> 。</span><span class="sxs-lookup"><span data-stu-id="d0e90-121"><xref:System.Security.Cryptography.Aes> is inherited by <xref:System.Security.Cryptography.AesCryptoServiceProvider>, <xref:System.Security.Cryptography.AesCng>, and <xref:System.Security.Cryptography.AesManaged>.</span></span>

<span data-ttu-id="d0e90-122">在 Windows .NET Framework 中：</span><span class="sxs-lookup"><span data-stu-id="d0e90-122">In .NET Framework on Windows:</span></span>

* <span data-ttu-id="d0e90-123">`*CryptoServiceProvider` 算法类（如 <xref:System.Security.Cryptography.AesCryptoServiceProvider> ）是 (CAPI) 实现算法的 Windows 加密 API 的包装器。</span><span class="sxs-lookup"><span data-stu-id="d0e90-123">`*CryptoServiceProvider` algorithm classes, such as <xref:System.Security.Cryptography.AesCryptoServiceProvider>, are wrappers around the Windows Cryptography API (CAPI) implementation of an algorithm.</span></span>
* <span data-ttu-id="d0e90-124">`*Cng` 算法类（如 <xref:System.Security.Cryptography.ECDiffieHellmanCng> ）是围绕 Windows 加密下一代 (CNG) 实现的包装。</span><span class="sxs-lookup"><span data-stu-id="d0e90-124">`*Cng` algorithm classes, such as <xref:System.Security.Cryptography.ECDiffieHellmanCng>, are wrappers around the Windows Cryptography Next Generation (CNG) implementation.</span></span>
* <span data-ttu-id="d0e90-125">`*Managed` 类（如 <xref:System.Security.Cryptography.AesManaged> ）完全用托管代码编写而成。</span><span class="sxs-lookup"><span data-stu-id="d0e90-125">`*Managed` classes, such as <xref:System.Security.Cryptography.AesManaged>, are written entirely in managed code.</span></span> <span data-ttu-id="d0e90-126">`*Managed` 实现不是由 (FIPS) 的联邦信息处理标准认证的，可能比 `*CryptoServiceProvider` 和 `*Cng` 包装类更慢。</span><span class="sxs-lookup"><span data-stu-id="d0e90-126">`*Managed` implementations are not certified by the Federal Information Processing Standards (FIPS), and may be slower than the `*CryptoServiceProvider` and `*Cng` wrapper classes.</span></span>

<span data-ttu-id="d0e90-127">在 .NET Core 和 .NET 5 及更高版本中，所有实现类 (`*CryptoServiceProvider` 、 `*Managed` 和 `*Cng`) 都是操作系统 (OS) 算法的包装器。</span><span class="sxs-lookup"><span data-stu-id="d0e90-127">In .NET Core and .NET 5 and later versions, all implementation classes (`*CryptoServiceProvider`, `*Managed`, and `*Cng`) are wrappers for the operating system (OS) algorithms.</span></span> <span data-ttu-id="d0e90-128">如果 OS 算法经过 FIPS 认证，则 .NET 将使用 FIPS 认证的算法。</span><span class="sxs-lookup"><span data-stu-id="d0e90-128">If the OS algorithms are FIPS-certified, then .NET uses FIPS-certified algorithms.</span></span> <span data-ttu-id="d0e90-129">有关详细信息，请参阅 [跨平台加密](cross-platform-cryptography.md)。</span><span class="sxs-lookup"><span data-stu-id="d0e90-129">For more information, see [Cross-Platform Cryptography](cross-platform-cryptography.md).</span></span>

<span data-ttu-id="d0e90-130">大多数情况下，不需要直接引用算法实现类，如 `AesCryptoServiceProvider` 。</span><span class="sxs-lookup"><span data-stu-id="d0e90-130">In most cases, you don't need to directly reference an algorithm implementation class, such as `AesCryptoServiceProvider`.</span></span> <span data-ttu-id="d0e90-131">通常需要的方法和属性在基本算法类上，如 `Aes` 。</span><span class="sxs-lookup"><span data-stu-id="d0e90-131">The methods and properties you typically need are on the base algorithm class, such as `Aes`.</span></span> <span data-ttu-id="d0e90-132">使用基算法类的工厂方法创建默认实现类的实例，并引用基本算法类。</span><span class="sxs-lookup"><span data-stu-id="d0e90-132">Create an instance of a default implementation class by using a factory method on the base algorithm class, and refer to the base algorithm class.</span></span> <span data-ttu-id="d0e90-133">例如，请参阅以下示例中突出显示的代码行：</span><span class="sxs-lookup"><span data-stu-id="d0e90-133">For example, see the highlighted line of code in the following example:</span></span>

:::code language="csharp" source="snippets/encrypting-data/csharp/aes-encrypt.cs" highlight="16":::
:::code language="vb" source="snippets/encrypting-data/vb/aes-encrypt.vb" highlight="12":::

## <a name="cryptographic-configuration"></a><span data-ttu-id="d0e90-134">加密配置</span><span class="sxs-lookup"><span data-stu-id="d0e90-134">Cryptographic Configuration</span></span>

<span data-ttu-id="d0e90-135">加密配置允许你将算法的特定实现解析到算法名称，从而允许 .NET 加密类的可扩展性。</span><span class="sxs-lookup"><span data-stu-id="d0e90-135">Cryptographic configuration lets you resolve a specific implementation of an algorithm to an algorithm name, allowing extensibility of the .NET cryptography classes.</span></span> <span data-ttu-id="d0e90-136">可以添加自己算法的硬件或软件实现，并将该实现映射到所选择的算法名称。</span><span class="sxs-lookup"><span data-stu-id="d0e90-136">You can add your own hardware or software implementation of an algorithm and map the implementation to the algorithm name of your choice.</span></span> <span data-ttu-id="d0e90-137">如果配置文件中未指定算法，则使用默认设置。</span><span class="sxs-lookup"><span data-stu-id="d0e90-137">If an algorithm is not specified in the configuration file, the default settings are used.</span></span>

## <a name="choosing-an-algorithm"></a><span data-ttu-id="d0e90-138">选择算法</span><span class="sxs-lookup"><span data-stu-id="d0e90-138">Choosing an Algorithm</span></span>

<span data-ttu-id="d0e90-139">可以出于各种原因选择一种算法：例如，为了保护数据完整性，为了保护数据隐私或为了生成密钥。</span><span class="sxs-lookup"><span data-stu-id="d0e90-139">You can select an algorithm for different reasons: for example, for data integrity, for data privacy, or to generate a key.</span></span> <span data-ttu-id="d0e90-140">为了保护完整性（防止更改）或保护隐私（防止查看），对称算法和哈希算法用于保护数据。</span><span class="sxs-lookup"><span data-stu-id="d0e90-140">Symmetric and hash algorithms are intended for protecting data for either integrity reasons (protect from change) or privacy reasons (protect from viewing).</span></span> <span data-ttu-id="d0e90-141">哈希算法主要用于保护数据完整性。</span><span class="sxs-lookup"><span data-stu-id="d0e90-141">Hash algorithms are used primarily for data integrity.</span></span>

<span data-ttu-id="d0e90-142">下面是按应用程序分类的建议算法列表：</span><span class="sxs-lookup"><span data-stu-id="d0e90-142">Here is a list of recommended algorithms by application:</span></span>

- <span data-ttu-id="d0e90-143">数据隐私：</span><span class="sxs-lookup"><span data-stu-id="d0e90-143">Data privacy:</span></span>
  - <xref:System.Security.Cryptography.Aes>
- <span data-ttu-id="d0e90-144">数据完整性：</span><span class="sxs-lookup"><span data-stu-id="d0e90-144">Data integrity:</span></span>
  - <xref:System.Security.Cryptography.HMACSHA256>
  - <xref:System.Security.Cryptography.HMACSHA512>
- <span data-ttu-id="d0e90-145">数字签名：</span><span class="sxs-lookup"><span data-stu-id="d0e90-145">Digital signature:</span></span>
  - <xref:System.Security.Cryptography.ECDsa>
  - <xref:System.Security.Cryptography.RSA>
- <span data-ttu-id="d0e90-146">密钥交换：</span><span class="sxs-lookup"><span data-stu-id="d0e90-146">Key exchange:</span></span>
  - <xref:System.Security.Cryptography.ECDiffieHellman>
  - <xref:System.Security.Cryptography.RSA>
- <span data-ttu-id="d0e90-147">随机数生成：</span><span class="sxs-lookup"><span data-stu-id="d0e90-147">Random number generation:</span></span>
  - <xref:System.Security.Cryptography.RandomNumberGenerator.Create%2A?displayProperty=nameWithType>
- <span data-ttu-id="d0e90-148">从密码生成密钥：</span><span class="sxs-lookup"><span data-stu-id="d0e90-148">Generating a key from a password:</span></span>
  - <xref:System.Security.Cryptography.Rfc2898DeriveBytes>

## <a name="see-also"></a><span data-ttu-id="d0e90-149">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d0e90-149">See also</span></span>

- [<span data-ttu-id="d0e90-150">加密服务</span><span class="sxs-lookup"><span data-stu-id="d0e90-150">Cryptographic Services</span></span>](cryptographic-services.md)
- [<span data-ttu-id="d0e90-151">跨平台加密</span><span class="sxs-lookup"><span data-stu-id="d0e90-151">Cross-Platform Cryptography</span></span>](cross-platform-cryptography.md)
- [<span data-ttu-id="d0e90-152">ASP.NET Core 数据保护</span><span class="sxs-lookup"><span data-stu-id="d0e90-152">ASP.NET Core Data Protection</span></span>](/aspnet/core/security/data-protection/introduction)
