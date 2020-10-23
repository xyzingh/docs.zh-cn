---
ms.openlocfilehash: d312ba2a22797ff6afff6b893f998c965e68e86e
ms.sourcegitcommit: e078b7540a8293ca1b604c9c0da1ff1506f0170b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "91997752"
---
### <a name="default-tls-cipher-suites-for-net-on-linux"></a><span data-ttu-id="2c186-101">Linux 上的 .NET 的默认 TLS 密码套件</span><span class="sxs-lookup"><span data-stu-id="2c186-101">Default TLS cipher suites for .NET on Linux</span></span>

<span data-ttu-id="2c186-102">现在，在 Linux 上，.NET 通过 <xref:System.Net.Security.SslStream> 类或更高级别的操作（如通过 <xref:System.Net.Http.HttpClient> 类的 HTTPS）执行 TLS/SSL 时，将遵循默认密码套件的 OpenSSL 配置。</span><span class="sxs-lookup"><span data-stu-id="2c186-102">.NET, on Linux, now respects the OpenSSL configuration for default cipher suites when doing TLS/SSL via the <xref:System.Net.Security.SslStream> class or higher-level operations, such as HTTPS via the <xref:System.Net.Http.HttpClient> class.</span></span> <span data-ttu-id="2c186-103">如果未显式配置默认密码套件，则 Linux 上的 .NET 将使用严格限制的允许密码套件列表。</span><span class="sxs-lookup"><span data-stu-id="2c186-103">When default cipher suites aren't explicitly configured, .NET on Linux uses a tightly restricted list of permitted cipher suites.</span></span>

#### <a name="change-description"></a><span data-ttu-id="2c186-104">更改描述</span><span class="sxs-lookup"><span data-stu-id="2c186-104">Change description</span></span>

<span data-ttu-id="2c186-105">在以前的 .NET 版本中，.NET 不遵循默认密码套件的系统配置。</span><span class="sxs-lookup"><span data-stu-id="2c186-105">In previous .NET versions, .NET does not respect system configuration for default cipher suites.</span></span> <span data-ttu-id="2c186-106">Linux 上的 .NET 的默认密码套件列表非常宽松。</span><span class="sxs-lookup"><span data-stu-id="2c186-106">The default cipher suite list for .NET on Linux is very permissive.</span></span>

<span data-ttu-id="2c186-107">从 .NET 5.0 开始，若在 openssl.cnf 中指定了默认密码套件的 OpenSSL 配置，Linux 上的 .NET 会遵循该配置。</span><span class="sxs-lookup"><span data-stu-id="2c186-107">Starting in .NET 5.0, .NET on Linux respects the OpenSSL configuration for default cipher suites when it's specified in *openssl.cnf*.</span></span> <span data-ttu-id="2c186-108">如果未显式配置密码套件，则唯一允许的密码套件如下：</span><span class="sxs-lookup"><span data-stu-id="2c186-108">When cipher suites aren't explicitly configured, the only permitted cipher suites are as follows:</span></span>

- <span data-ttu-id="2c186-109">TLS 1.3 密码套件</span><span class="sxs-lookup"><span data-stu-id="2c186-109">TLS 1.3 cipher suites</span></span>
- <span data-ttu-id="2c186-110">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="2c186-110">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="2c186-111">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="2c186-111">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="2c186-112">TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="2c186-112">TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="2c186-113">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="2c186-113">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="2c186-114">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="2c186-114">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="2c186-115">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="2c186-115">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="2c186-116">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="2c186-116">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="2c186-117">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="2c186-117">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="2c186-118">由于此回退默认值不包括与 TLS 1.0 或 TLS 1.1 兼容的任何密码套件，因此默认情况下将有效禁用这些较旧的协议版本。</span><span class="sxs-lookup"><span data-stu-id="2c186-118">Since this fallback default doesn't include any cipher suites that are compatible with TLS 1.0 or TLS 1.1, these older protocol versions are effectively disabled by default.</span></span>

<span data-ttu-id="2c186-119">为特定会话的 SslStream 提供一个 CipherSuitePolicy 值仍将替换配置文件内容和/或 .NET 回退默认值。</span><span class="sxs-lookup"><span data-stu-id="2c186-119">Supplying a CipherSuitePolicy value to SslStream for a specific session will still replace the configuration file content and/or .NET fallback default.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="2c186-120">更改原因</span><span class="sxs-lookup"><span data-stu-id="2c186-120">Reason for change</span></span>

<span data-ttu-id="2c186-121">在 Linux 上运行 .NET 的用户要求将 <xref:System.Net.Security.SslStream> 的默认配置更改为由第三方评估工具提供高安全等级的配置。</span><span class="sxs-lookup"><span data-stu-id="2c186-121">Users running .NET on Linux requested that the default configuration for <xref:System.Net.Security.SslStream> be changed to one that provided a high security rating from third-party assessment tools.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="2c186-122">引入的版本</span><span class="sxs-lookup"><span data-stu-id="2c186-122">Version introduced</span></span>

<span data-ttu-id="2c186-123">5.0 RC1</span><span class="sxs-lookup"><span data-stu-id="2c186-123">5.0 RC1</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="2c186-124">建议操作</span><span class="sxs-lookup"><span data-stu-id="2c186-124">Recommended action</span></span>

<span data-ttu-id="2c186-125">与新式客户端或服务器通信时，新的默认值可能会生效。</span><span class="sxs-lookup"><span data-stu-id="2c186-125">The new defaults are likely to work when communicating with modern clients or servers.</span></span> <span data-ttu-id="2c186-126">如果需要扩展默认密码套件列表以接受旧客户端（或联系旧服务器），请指定 `CipherSuitePolicy` 值或更改 OpenSSL 配置文件。</span><span class="sxs-lookup"><span data-stu-id="2c186-126">If you need to expand the default cipher suite list to accept legacy clients (or to contact legacy servers), either specify a `CipherSuitePolicy` value or change the OpenSSL configuration file.</span></span> <span data-ttu-id="2c186-127">在许多 Linux 发行版中，OpenSSL 配置文件位于 /etc/ssl/openssl.cnf。</span><span class="sxs-lookup"><span data-stu-id="2c186-127">On many Linux distributions, the OpenSSL configuration file is at */etc/ssl/openssl.cnf*.</span></span>

<span data-ttu-id="2c186-128">此示例 openssl.cnf 文件是与 Linux 上的 .NET 5.0 及更高版本的默认密码套件策略等效的最小文件。</span><span class="sxs-lookup"><span data-stu-id="2c186-128">This sample *openssl.cnf* file is a minimal file that's equivalent to the default cipher suites policy for .NET 5.0 and later on Linux.</span></span> <span data-ttu-id="2c186-129">不要替换系统文件，而是将这些概念与系统中的文件合并。</span><span class="sxs-lookup"><span data-stu-id="2c186-129">Instead of replacing the system file, merge these concepts with the file that's present on your system.</span></span>

```ini
openssl_conf = default_conf

[default_conf]
ssl_conf = ssl_sect

[ssl_sect]
system_default = system_default_sect

[system_default_sect]
CipherString = ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256
```

<span data-ttu-id="2c186-130">在 Red Hat Enterprise Linux、CentOS 和 Fedora 发行版上，.NET 应用程序默认使用系统范围的加密策略允许的密码套件。</span><span class="sxs-lookup"><span data-stu-id="2c186-130">On the Red Hat Enterprise Linux, CentOS, and Fedora distributions, .NET applications default to the cipher suites permitted by the system-wide cryptographic policies.</span></span> <span data-ttu-id="2c186-131">在这些发行版上，使用加密策略配置，而不是 openssl.cnf。</span><span class="sxs-lookup"><span data-stu-id="2c186-131">On these distributions, use the crypto-policies configuration instead of *openssl.cnf*.</span></span>

#### <a name="category"></a><span data-ttu-id="2c186-132">类别</span><span class="sxs-lookup"><span data-stu-id="2c186-132">Category</span></span>

- <span data-ttu-id="2c186-133">密码</span><span class="sxs-lookup"><span data-stu-id="2c186-133">Cryptography</span></span>
- <span data-ttu-id="2c186-134">安全性</span><span class="sxs-lookup"><span data-stu-id="2c186-134">Security</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="2c186-135">受影响的 API</span><span class="sxs-lookup"><span data-stu-id="2c186-135">Affected APIs</span></span>

<span data-ttu-id="2c186-136">无法通过 API 分析检测到。</span><span class="sxs-lookup"><span data-stu-id="2c186-136">Not detectible via API analysis.</span></span>

<!--

#### Affected APIs

- Not detectible via API analysis.

-->
