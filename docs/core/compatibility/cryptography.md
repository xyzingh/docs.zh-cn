---
title: 加密中断性变更
description: 列出 .NET Core 中与加密相关的中断性变更。
ms.date: 04/22/2020
ms.openlocfilehash: 6f37e5caacadc276562e63a728162c6b26f2e435
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92159543"
---
# <a name="cryptography-breaking-changes"></a><span data-ttu-id="4ae7e-103">加密中断性变更</span><span class="sxs-lookup"><span data-stu-id="4ae7e-103">Cryptography breaking changes</span></span>

<span data-ttu-id="4ae7e-104">本页记录了以下中断性变更：</span><span class="sxs-lookup"><span data-stu-id="4ae7e-104">The following breaking changes are documented on this page:</span></span>

| <span data-ttu-id="4ae7e-105">重大更改</span><span class="sxs-lookup"><span data-stu-id="4ae7e-105">Breaking change</span></span> | <span data-ttu-id="4ae7e-106">引入的版本</span><span class="sxs-lookup"><span data-stu-id="4ae7e-106">Version introduced</span></span> |
| - | :-: |
| [<span data-ttu-id="4ae7e-107">不支持对加密抽象的默认实现进行实例化</span><span class="sxs-lookup"><span data-stu-id="4ae7e-107">Instantiating default implementations of cryptographic abstractions is not supported</span></span>](#instantiating-default-implementations-of-cryptographic-abstractions-is-not-supported) | <span data-ttu-id="4ae7e-108">5.0</span><span class="sxs-lookup"><span data-stu-id="4ae7e-108">5.0</span></span> |
| [<span data-ttu-id="4ae7e-109">Linux 上的 .NET 的默认 TLS 密码套件</span><span class="sxs-lookup"><span data-stu-id="4ae7e-109">Default TLS cipher suites for .NET on Linux</span></span>](#default-tls-cipher-suites-for-net-on-linux) | <span data-ttu-id="4ae7e-110">5.0</span><span class="sxs-lookup"><span data-stu-id="4ae7e-110">5.0</span></span> |
| [<span data-ttu-id="4ae7e-111">Blazor WebAssembly 不支持的 System.Security.Cryptography API</span><span class="sxs-lookup"><span data-stu-id="4ae7e-111">System.Security.Cryptography APIs not supported on Blazor WebAssembly</span></span>](#systemsecuritycryptography-apis-not-supported-on-blazor-webassembly) | <span data-ttu-id="4ae7e-112">5.0</span><span class="sxs-lookup"><span data-stu-id="4ae7e-112">5.0</span></span> |
| [<span data-ttu-id="4ae7e-113">System.Security.Cryptography.Oid 在功能上仅用于初始化</span><span class="sxs-lookup"><span data-stu-id="4ae7e-113">System.Security.Cryptography.Oid is functionally init-only</span></span>](#systemsecuritycryptographyoid-is-functionally-init-only) | <span data-ttu-id="4ae7e-114">5.0</span><span class="sxs-lookup"><span data-stu-id="4ae7e-114">5.0</span></span> |
| [<span data-ttu-id="4ae7e-115">Linux 不再支持 BEGIN TRUSTED CERTIFICATE 语法</span><span class="sxs-lookup"><span data-stu-id="4ae7e-115">BEGIN TRUSTED CERTIFICATE syntax no longer supported on Linux</span></span>](#begin-trusted-certificate-syntax-no-longer-supported-for-root-certificates-on-linux) | <span data-ttu-id="4ae7e-116">3.0</span><span class="sxs-lookup"><span data-stu-id="4ae7e-116">3.0</span></span> |
| [<span data-ttu-id="4ae7e-117">EnvelopedCms 默认为 AES-256 加密</span><span class="sxs-lookup"><span data-stu-id="4ae7e-117">EnvelopedCms defaults to AES-256 encryption</span></span>](#envelopedcms-defaults-to-aes-256-encryption) | <span data-ttu-id="4ae7e-118">3.0</span><span class="sxs-lookup"><span data-stu-id="4ae7e-118">3.0</span></span> |
| [<span data-ttu-id="4ae7e-119">RSAOpenSsl 密钥生成的最小大小已增加</span><span class="sxs-lookup"><span data-stu-id="4ae7e-119">Minimum size for RSAOpenSsl key generation has increased</span></span>](#minimum-size-for-rsaopenssl-key-generation-has-increased) | <span data-ttu-id="4ae7e-120">3.0</span><span class="sxs-lookup"><span data-stu-id="4ae7e-120">3.0</span></span> |
| [<span data-ttu-id="4ae7e-121">.NET Core 3.0 倾向于使用 OpenSSL 1.1.x 而不是 OpenSSL 1.0.x</span><span class="sxs-lookup"><span data-stu-id="4ae7e-121">.NET Core 3.0 prefers OpenSSL 1.1.x to OpenSSL 1.0.x</span></span>](#net-core-30-prefers-openssl-11x-to-openssl-10x) | <span data-ttu-id="4ae7e-122">3.0</span><span class="sxs-lookup"><span data-stu-id="4ae7e-122">3.0</span></span> |
| [<span data-ttu-id="4ae7e-123">CryptoStream.Dispose 仅在写入时转换最终块</span><span class="sxs-lookup"><span data-stu-id="4ae7e-123">CryptoStream.Dispose transforms final block only when writing</span></span>](#cryptostreamdispose-transforms-final-block-only-when-writing) | <span data-ttu-id="4ae7e-124">3.0</span><span class="sxs-lookup"><span data-stu-id="4ae7e-124">3.0</span></span> |
| [<span data-ttu-id="4ae7e-125">已考虑 SignedCms.ComputeSignature 的布尔参数</span><span class="sxs-lookup"><span data-stu-id="4ae7e-125">Boolean parameter of SignedCms.ComputeSignature is respected</span></span>](#boolean-parameter-of-signedcmscomputesignature-is-respected) | <span data-ttu-id="4ae7e-126">2.1</span><span class="sxs-lookup"><span data-stu-id="4ae7e-126">2.1</span></span> |

## <a name="net-50"></a><span data-ttu-id="4ae7e-127">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="4ae7e-127">.NET 5.0</span></span>

[!INCLUDE [instantiating-default-implementations-of-cryptographic-abstractions-not-supported](../../../includes/core-changes/cryptography/5.0/instantiating-default-implementations-of-cryptographic-abstractions-not-supported.md)]

***

[!INCLUDE [default-cipher-suites-for-tls-on-linux](../../../includes/core-changes/cryptography/5.0/default-cipher-suites-for-tls-on-linux.md)]

***

[!INCLUDE[Cryptography APIs not supported on Blazor WebAssembly](~/includes/core-changes/cryptography/5.0/cryptography-apis-not-supported-on-blazor-webassembly.md)]

***

[!INCLUDE [cryptography-oid-init-only](../../../includes/core-changes/cryptography/5.0/cryptography-oid-init-only.md)]

***

## <a name="net-core-30"></a><span data-ttu-id="4ae7e-128">.NET Core 3.0</span><span class="sxs-lookup"><span data-stu-id="4ae7e-128">.NET Core 3.0</span></span>

[!INCLUDE [begin-trusted-cert-linux](~/includes/core-changes/cryptography/3.0/begin-trusted-cert-linux.md)]

***

[!INCLUDE[EnvelopedCms defaults to AES-256 encryption](~/includes/core-changes/cryptography/3.0/envelopedcms-defaults-to-aes256.md)]

***

[!INCLUDE[Minimum size for RSAOpenSsl key generation has increased](~/includes/core-changes/cryptography/3.0/minimum-rsaopenssl-key-size-change.md)]

***

[!INCLUDE[.NET Core 3.0 prefers OpenSSL 1.1.x to OpenSSL 1.0.x](~/includes/core-changes/cryptography/3.0/net-core-3-0-prefers-openssl-1-1-x.md)]

***

[!INCLUDE [CryptoStream.Dispose transforms final block only when writing](~/includes/core-changes/cryptography/3.0/cryptography-cryptostream-dispose-final-block-write.md)]

***

## <a name="net-core-21"></a><span data-ttu-id="4ae7e-129">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="4ae7e-129">.NET Core 2.1</span></span>

[!INCLUDE [Boolean parameter of SignedCms.ComputeSignature is respected](~/includes/core-changes/cryptography/2.1/compute-signature-silent-parameter.md)]

***
