---
title: 加密中断性变更
description: 列出 .NET Core 中与加密相关的中断性变更。
ms.date: 04/22/2020
ms.openlocfilehash: b755876624a7709cfe08b5993655e78be9f8e1f2
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888603"
---
# <a name="cryptography-breaking-changes"></a><span data-ttu-id="5abde-103">加密中断性变更</span><span class="sxs-lookup"><span data-stu-id="5abde-103">Cryptography breaking changes</span></span>

<span data-ttu-id="5abde-104">本页记录了以下中断性变更：</span><span class="sxs-lookup"><span data-stu-id="5abde-104">The following breaking changes are documented on this page:</span></span>

| <span data-ttu-id="5abde-105">重大更改</span><span class="sxs-lookup"><span data-stu-id="5abde-105">Breaking change</span></span> | <span data-ttu-id="5abde-106">引入的版本</span><span class="sxs-lookup"><span data-stu-id="5abde-106">Version introduced</span></span> |
| - | :-: |
| [<span data-ttu-id="5abde-107">TripleDES.Create 所创建实例的默认 FeedbackSize 值已更改</span><span class="sxs-lookup"><span data-stu-id="5abde-107">Default FeedbackSize value for instances created by TripleDES.Create changed</span></span>](#default-feedbacksize-value-for-instances-created-by-tripledescreate-changed) | <span data-ttu-id="5abde-108">5.0</span><span class="sxs-lookup"><span data-stu-id="5abde-108">5.0</span></span> |
| [<span data-ttu-id="5abde-109">不支持对加密抽象的默认实现进行实例化</span><span class="sxs-lookup"><span data-stu-id="5abde-109">Instantiating default implementations of cryptographic abstractions is not supported</span></span>](#instantiating-default-implementations-of-cryptographic-abstractions-is-not-supported) | <span data-ttu-id="5abde-110">5.0</span><span class="sxs-lookup"><span data-stu-id="5abde-110">5.0</span></span> |
| [<span data-ttu-id="5abde-111">Linux 上的 .NET 的默认 TLS 密码套件</span><span class="sxs-lookup"><span data-stu-id="5abde-111">Default TLS cipher suites for .NET on Linux</span></span>](#default-tls-cipher-suites-for-net-on-linux) | <span data-ttu-id="5abde-112">5.0</span><span class="sxs-lookup"><span data-stu-id="5abde-112">5.0</span></span> |
| [<span data-ttu-id="5abde-113">Blazor WebAssembly 不支持的 System.Security.Cryptography API</span><span class="sxs-lookup"><span data-stu-id="5abde-113">System.Security.Cryptography APIs not supported on Blazor WebAssembly</span></span>](#systemsecuritycryptography-apis-not-supported-on-blazor-webassembly) | <span data-ttu-id="5abde-114">5.0</span><span class="sxs-lookup"><span data-stu-id="5abde-114">5.0</span></span> |
| [<span data-ttu-id="5abde-115">System.Security.Cryptography.Oid 在功能上仅用于初始化</span><span class="sxs-lookup"><span data-stu-id="5abde-115">System.Security.Cryptography.Oid is functionally init-only</span></span>](#systemsecuritycryptographyoid-is-functionally-init-only) | <span data-ttu-id="5abde-116">5.0</span><span class="sxs-lookup"><span data-stu-id="5abde-116">5.0</span></span> |
| [<span data-ttu-id="5abde-117">Linux 不再支持 BEGIN TRUSTED CERTIFICATE 语法</span><span class="sxs-lookup"><span data-stu-id="5abde-117">BEGIN TRUSTED CERTIFICATE syntax no longer supported on Linux</span></span>](#begin-trusted-certificate-syntax-no-longer-supported-for-root-certificates-on-linux) | <span data-ttu-id="5abde-118">3.0</span><span class="sxs-lookup"><span data-stu-id="5abde-118">3.0</span></span> |
| [<span data-ttu-id="5abde-119">EnvelopedCms 默认为 AES-256 加密</span><span class="sxs-lookup"><span data-stu-id="5abde-119">EnvelopedCms defaults to AES-256 encryption</span></span>](#envelopedcms-defaults-to-aes-256-encryption) | <span data-ttu-id="5abde-120">3.0</span><span class="sxs-lookup"><span data-stu-id="5abde-120">3.0</span></span> |
| [<span data-ttu-id="5abde-121">RSAOpenSsl 密钥生成的最小大小已增加</span><span class="sxs-lookup"><span data-stu-id="5abde-121">Minimum size for RSAOpenSsl key generation has increased</span></span>](#minimum-size-for-rsaopenssl-key-generation-has-increased) | <span data-ttu-id="5abde-122">3.0</span><span class="sxs-lookup"><span data-stu-id="5abde-122">3.0</span></span> |
| [<span data-ttu-id="5abde-123">.NET Core 3.0 倾向于使用 OpenSSL 1.1.x 而不是 OpenSSL 1.0.x</span><span class="sxs-lookup"><span data-stu-id="5abde-123">.NET Core 3.0 prefers OpenSSL 1.1.x to OpenSSL 1.0.x</span></span>](#net-core-30-prefers-openssl-11x-to-openssl-10x) | <span data-ttu-id="5abde-124">3.0</span><span class="sxs-lookup"><span data-stu-id="5abde-124">3.0</span></span> |
| [<span data-ttu-id="5abde-125">CryptoStream.Dispose 仅在写入时转换最终块</span><span class="sxs-lookup"><span data-stu-id="5abde-125">CryptoStream.Dispose transforms final block only when writing</span></span>](#cryptostreamdispose-transforms-final-block-only-when-writing) | <span data-ttu-id="5abde-126">3.0</span><span class="sxs-lookup"><span data-stu-id="5abde-126">3.0</span></span> |
| [<span data-ttu-id="5abde-127">已考虑 SignedCms.ComputeSignature 的布尔参数</span><span class="sxs-lookup"><span data-stu-id="5abde-127">Boolean parameter of SignedCms.ComputeSignature is respected</span></span>](#boolean-parameter-of-signedcmscomputesignature-is-respected) | <span data-ttu-id="5abde-128">2.1</span><span class="sxs-lookup"><span data-stu-id="5abde-128">2.1</span></span> |

## <a name="net-50"></a><span data-ttu-id="5abde-129">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="5abde-129">.NET 5.0</span></span>

[!INCLUDE [tripledes-default-feedback-size-change](../../../includes/core-changes/cryptography/5.0/tripledes-default-feedback-size-change.md)]

***

[!INCLUDE [instantiating-default-implementations-of-cryptographic-abstractions-not-supported](../../../includes/core-changes/cryptography/5.0/instantiating-default-implementations-of-cryptographic-abstractions-not-supported.md)]

<span data-ttu-id="5abde-130">\*\*_</span><span class="sxs-lookup"><span data-stu-id="5abde-130">\*\*_</span></span>

[!INCLUDE [default-cipher-suites-for-tls-on-linux](../../../includes/core-changes/cryptography/5.0/default-cipher-suites-for-tls-on-linux.md)]

_*_

[!INCLUDE[Cryptography APIs not supported on Blazor WebAssembly](~/includes/core-changes/cryptography/5.0/cryptography-apis-not-supported-on-blazor-webassembly.md)]

_*_

[!INCLUDE [cryptography-oid-init-only](../../../includes/core-changes/cryptography/5.0/cryptography-oid-init-only.md)]

_*_

## <a name="net-core-30"></a><span data-ttu-id="5abde-131">.NET Core 3.0</span><span class="sxs-lookup"><span data-stu-id="5abde-131">.NET Core 3.0</span></span>

[!INCLUDE [begin-trusted-cert-linux](~/includes/core-changes/cryptography/3.0/begin-trusted-cert-linux.md)]

_*_

[!INCLUDE[EnvelopedCms defaults to AES-256 encryption](~/includes/core-changes/cryptography/3.0/envelopedcms-defaults-to-aes256.md)]

_*_

[!INCLUDE[Minimum size for RSAOpenSsl key generation has increased](~/includes/core-changes/cryptography/3.0/minimum-rsaopenssl-key-size-change.md)]

_*_

[!INCLUDE[.NET Core 3.0 prefers OpenSSL 1.1.x to OpenSSL 1.0.x](~/includes/core-changes/cryptography/3.0/net-core-3-0-prefers-openssl-1-1-x.md)]

_*_

[!INCLUDE [CryptoStream.Dispose transforms final block only when writing](~/includes/core-changes/cryptography/3.0/cryptography-cryptostream-dispose-final-block-write.md)]

_*_

## <a name="net-core-21"></a><span data-ttu-id="5abde-132">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="5abde-132">.NET Core 2.1</span></span>

[!INCLUDE [Boolean parameter of SignedCms.ComputeSignature is respected](~/includes/core-changes/cryptography/2.1/compute-signature-silent-parameter.md)]

<span data-ttu-id="5abde-133">_\*\*</span><span class="sxs-lookup"><span data-stu-id="5abde-133">_\*\*</span></span>
