---
title: 网络配置设置
description: 了解为 .NET Core 应用配置网络的运行时设置。
ms.date: 11/27/2019
ms.topic: reference
ms.openlocfilehash: bda608e83bb1b093d7d9b860de9607f6734720aa
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188297"
---
# <a name="run-time-configuration-options-for-networking"></a><span data-ttu-id="59f29-103">用于网络的运行时配置选项</span><span class="sxs-lookup"><span data-stu-id="59f29-103">Run-time configuration options for networking</span></span>

## <a name="http2-protocol"></a><span data-ttu-id="59f29-104">HTTP/2 协议</span><span class="sxs-lookup"><span data-stu-id="59f29-104">HTTP/2 protocol</span></span>

- <span data-ttu-id="59f29-105">配置是否启用对 HTTP/2 协议的支持。</span><span class="sxs-lookup"><span data-stu-id="59f29-105">Configures whether support for the HTTP/2 protocol is enabled.</span></span>

- <span data-ttu-id="59f29-106">已在 .NET Core 3.0 中引入。</span><span class="sxs-lookup"><span data-stu-id="59f29-106">Introduced in .NET Core 3.0.</span></span>

- <span data-ttu-id="59f29-107">仅限 .NET Core 3.0：如果省略此设置，则会禁用对 HTTP/2 协议的支持。</span><span class="sxs-lookup"><span data-stu-id="59f29-107">.NET Core 3.0 only: If you omit this setting, support for the HTTP/2 protocol is disabled.</span></span> <span data-ttu-id="59f29-108">它等效于将值设置为 `false`。</span><span class="sxs-lookup"><span data-stu-id="59f29-108">This is equivalent to setting the value to `false`.</span></span>

- <span data-ttu-id="59f29-109">.NET Core 3.1 和 .NET 5 +：如果省略此设置，则会启用对 HTTP/2 协议的支持。</span><span class="sxs-lookup"><span data-stu-id="59f29-109">.NET Core 3.1 and .NET 5+: If you omit this setting, support for the HTTP/2 protocol is enabled.</span></span> <span data-ttu-id="59f29-110">它等效于将值设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="59f29-110">This is equivalent to setting the value to `true`.</span></span>

| | <span data-ttu-id="59f29-111">设置名</span><span class="sxs-lookup"><span data-stu-id="59f29-111">Setting name</span></span> | <span data-ttu-id="59f29-112">值</span><span class="sxs-lookup"><span data-stu-id="59f29-112">Values</span></span> |
| - | - | - |
| <span data-ttu-id="59f29-113">**runtimeconfig.json**</span><span class="sxs-lookup"><span data-stu-id="59f29-113">**runtimeconfig.json**</span></span> | `System.Net.Http.SocketsHttpHandler.Http2Support` | <span data-ttu-id="59f29-114">`false` - 禁用</span><span class="sxs-lookup"><span data-stu-id="59f29-114">`false` - disabled</span></span><br/><span data-ttu-id="59f29-115">`true` - 启用</span><span class="sxs-lookup"><span data-stu-id="59f29-115">`true` - enabled</span></span> |
| <span data-ttu-id="59f29-116">**环境变量**</span><span class="sxs-lookup"><span data-stu-id="59f29-116">**Environment variable**</span></span> | `DOTNET_SYSTEM_NET_HTTP_SOCKETSHTTPHANDLER_HTTP2SUPPORT` | <span data-ttu-id="59f29-117">`0` - 禁用</span><span class="sxs-lookup"><span data-stu-id="59f29-117">`0` - disabled</span></span><br/><span data-ttu-id="59f29-118">`1` - 启用</span><span class="sxs-lookup"><span data-stu-id="59f29-118">`1` - enabled</span></span> |

## <a name="usesocketshttphandler"></a><span data-ttu-id="59f29-119">UseSocketsHttpHandler</span><span class="sxs-lookup"><span data-stu-id="59f29-119">UseSocketsHttpHandler</span></span>

- <span data-ttu-id="59f29-120">配置 <xref:System.Net.Http.HttpClientHandler?displayProperty=nameWithType> 是使用 <xref:System.Net.Http.SocketsHttpHandler?displayProperty=nameWithType> 还是使用旧的 HTTP 协议堆栈（在 Windows 上为 <xref:System.Net.Http.WinHttpHandler>，在 Linux 上为基于 [libcurl](https://curl.haxx.se/libcurl/) 实现的内部类 `CurlHandler`。）</span><span class="sxs-lookup"><span data-stu-id="59f29-120">Configures whether <xref:System.Net.Http.HttpClientHandler?displayProperty=nameWithType> uses <xref:System.Net.Http.SocketsHttpHandler?displayProperty=nameWithType> or older HTTP protocol stacks (<xref:System.Net.Http.WinHttpHandler> on Windows and `CurlHandler`, an internal class implemented on top of [libcurl](https://curl.haxx.se/libcurl/), on Linux).</span></span>

  > [!NOTE]
  > <span data-ttu-id="59f29-121">可使用高级别网络 API，而不是直接实例化 <xref:System.Net.Http.HttpClientHandler> 类。</span><span class="sxs-lookup"><span data-stu-id="59f29-121">You may be using high-level networking APIs instead of directly instantiating the <xref:System.Net.Http.HttpClientHandler> class.</span></span> <span data-ttu-id="59f29-122">此设置还会影响高级别网络 API 使用的 HTTP 协议堆栈类型，包括 <xref:System.Net.Http.HttpClient> 和 [HttpClientFactory](/previous-versions/aspnet/hh995280(v=vs.118))。</span><span class="sxs-lookup"><span data-stu-id="59f29-122">This setting also affects which HTTP protocol stack is used by high-level networking APIs, including <xref:System.Net.Http.HttpClient> and [HttpClientFactory](/previous-versions/aspnet/hh995280(v=vs.118)).</span></span>

- <span data-ttu-id="59f29-123">如果省略此设置，<xref:System.Net.Http.HttpClientHandler> 将使用 <xref:System.Net.Http.SocketsHttpHandler>。</span><span class="sxs-lookup"><span data-stu-id="59f29-123">If you omit this setting, <xref:System.Net.Http.HttpClientHandler> uses <xref:System.Net.Http.SocketsHttpHandler>.</span></span> <span data-ttu-id="59f29-124">它等效于将值设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="59f29-124">This is equivalent to setting the value to `true`.</span></span>

- <span data-ttu-id="59f29-125">可通过调用 <xref:System.AppContext.SetSwitch%2A?displayProperty=nameWithType> 方法，以编程方式配置此设置。</span><span class="sxs-lookup"><span data-stu-id="59f29-125">You can configure this setting programmatically by calling the <xref:System.AppContext.SetSwitch%2A?displayProperty=nameWithType> method.</span></span>

| | <span data-ttu-id="59f29-126">设置名</span><span class="sxs-lookup"><span data-stu-id="59f29-126">Setting name</span></span> | <span data-ttu-id="59f29-127">值</span><span class="sxs-lookup"><span data-stu-id="59f29-127">Values</span></span> |
| - | - | - |
| <span data-ttu-id="59f29-128">**runtimeconfig.json**</span><span class="sxs-lookup"><span data-stu-id="59f29-128">**runtimeconfig.json**</span></span> | `System.Net.Http.UseSocketsHttpHandler` | <span data-ttu-id="59f29-129">`true` - 允许使用 <xref:System.Net.Http.SocketsHttpHandler></span><span class="sxs-lookup"><span data-stu-id="59f29-129">`true` - enables the use of <xref:System.Net.Http.SocketsHttpHandler></span></span><br/><span data-ttu-id="59f29-130">`false` - 允许使用 Windows 上的 <xref:System.Net.Http.WinHttpHandler> 或 Linux 上的 [libcurl](https://curl.haxx.se/libcurl/)</span><span class="sxs-lookup"><span data-stu-id="59f29-130">`false` - enables the use of <xref:System.Net.Http.WinHttpHandler> on Windows or [libcurl](https://curl.haxx.se/libcurl/) on Linux</span></span> |
| <span data-ttu-id="59f29-131">**环境变量**</span><span class="sxs-lookup"><span data-stu-id="59f29-131">**Environment variable**</span></span> | `DOTNET_SYSTEM_NET_HTTP_USESOCKETSHTTPHANDLER` | <span data-ttu-id="59f29-132">`1` - 允许使用 <xref:System.Net.Http.SocketsHttpHandler></span><span class="sxs-lookup"><span data-stu-id="59f29-132">`1` - enables the use of <xref:System.Net.Http.SocketsHttpHandler></span></span><br/><span data-ttu-id="59f29-133">`0` - 允许使用 Windows 上的 <xref:System.Net.Http.WinHttpHandler> 或 Linux 上的 [libcurl](https://curl.haxx.se/libcurl/)</span><span class="sxs-lookup"><span data-stu-id="59f29-133">`0` - enables the use of <xref:System.Net.Http.WinHttpHandler> on Windows or [libcurl](https://curl.haxx.se/libcurl/) on Linux</span></span> |

> [!NOTE]
> <span data-ttu-id="59f29-134">从 .NET 5 开始，`System.Net.Http.UseSocketsHttpHandler` 设置不再可用。</span><span class="sxs-lookup"><span data-stu-id="59f29-134">Starting in .NET 5, the `System.Net.Http.UseSocketsHttpHandler` setting is no longer available.</span></span>

## <a name="latin1-headers-net-core-31-only"></a><span data-ttu-id="59f29-135">Latin1 标头（仅限 .NET Core 3.1）</span><span class="sxs-lookup"><span data-stu-id="59f29-135">Latin1 headers (.NET Core 3.1 only)</span></span>

- <span data-ttu-id="59f29-136">此开关允许放宽 HTTP 标头验证，从而使 <xref:System.Net.Http.SocketsHttpHandler> 可以在标头中发送 ISO-8859-1 (Latin-1) 编码的字符。</span><span class="sxs-lookup"><span data-stu-id="59f29-136">This switch allows relaxing the HTTP header validation, enabling <xref:System.Net.Http.SocketsHttpHandler> to send ISO-8859-1 (Latin-1) encoded characters in headers.</span></span>

- <span data-ttu-id="59f29-137">如果省略此设置，则尝试发送非 ASCII 字符将导致 <xref:System.Net.Http.HttpRequestException>。</span><span class="sxs-lookup"><span data-stu-id="59f29-137">If you omit this setting, an attempt to send a non-ASCII character will result in <xref:System.Net.Http.HttpRequestException>.</span></span> <span data-ttu-id="59f29-138">它等效于将值设置为 `false`。</span><span class="sxs-lookup"><span data-stu-id="59f29-138">This is equivalent to setting the value to `false`.</span></span>

| | <span data-ttu-id="59f29-139">设置名</span><span class="sxs-lookup"><span data-stu-id="59f29-139">Setting name</span></span> | <span data-ttu-id="59f29-140">值</span><span class="sxs-lookup"><span data-stu-id="59f29-140">Values</span></span> |
| - | - | - |
| <span data-ttu-id="59f29-141">**runtimeconfig.json**</span><span class="sxs-lookup"><span data-stu-id="59f29-141">**runtimeconfig.json**</span></span> | `System.Net.Http.SocketsHttpHandler.AllowLatin1Headers` | <span data-ttu-id="59f29-142">`false` - 禁用</span><span class="sxs-lookup"><span data-stu-id="59f29-142">`false` - disabled</span></span><br/><span data-ttu-id="59f29-143">`true` - 启用</span><span class="sxs-lookup"><span data-stu-id="59f29-143">`true` - enabled</span></span> |
| <span data-ttu-id="59f29-144">**环境变量**</span><span class="sxs-lookup"><span data-stu-id="59f29-144">**Environment variable**</span></span> | `DOTNET_SYSTEM_NET_HTTP_SOCKETSHTTPHANDLER_ALLOWLATIN1HEADERS` | <span data-ttu-id="59f29-145">`0` - 禁用</span><span class="sxs-lookup"><span data-stu-id="59f29-145">`0` - disabled</span></span><br/><span data-ttu-id="59f29-146">`1` - 启用</span><span class="sxs-lookup"><span data-stu-id="59f29-146">`1` - enabled</span></span> |

> [!NOTE]
> <span data-ttu-id="59f29-147">此选项仅在 3.1.9 版本之后 NET Core 3.1 中提供，先前版本或更高版本中则不提供。</span><span class="sxs-lookup"><span data-stu-id="59f29-147">This option is only available in .NET Core 3.1 since version 3.1.9, and not in previous or later versions.</span></span> <span data-ttu-id="59f29-148">在 .NET 5 中，我们建议使用 <xref:System.Net.Http.SocketsHttpHandler.RequestHeaderEncodingSelector>。</span><span class="sxs-lookup"><span data-stu-id="59f29-148">In .NET 5 we recommend using <xref:System.Net.Http.SocketsHttpHandler.RequestHeaderEncodingSelector>.</span></span>
