---
title: 网络中断性变更
description: 列出 .NET Core 中网络的中断性变更。
ms.date: 05/05/2020
ms.openlocfilehash: fdbd3f3bdcae5048b4f01e4d827f8a0e876c5c15
ms.sourcegitcommit: 39b1d5f2978be15409c189a66ab30781d9082cd8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2020
ms.locfileid: "92050504"
---
# <a name="networking-breaking-changes"></a><span data-ttu-id="12b32-103">网络中断性变更</span><span class="sxs-lookup"><span data-stu-id="12b32-103">Networking breaking changes</span></span>

<span data-ttu-id="12b32-104">本页记录了以下中断性变更：</span><span class="sxs-lookup"><span data-stu-id="12b32-104">The following breaking changes are documented on this page:</span></span>

| <span data-ttu-id="12b32-105">重大更改</span><span class="sxs-lookup"><span data-stu-id="12b32-105">Breaking change</span></span> | <span data-ttu-id="12b32-106">引入的版本</span><span class="sxs-lookup"><span data-stu-id="12b32-106">Introduced version</span></span> |
| - | - |
| [<span data-ttu-id="12b32-107">NegotiateStream 和 SslStream 允许连续的“开始”操作</span><span class="sxs-lookup"><span data-stu-id="12b32-107">NegotiateStream and SslStream allow successive Begin operations</span></span>](#negotiatestream-and-sslstream-allow-successive-begin-operations) | <span data-ttu-id="12b32-108">5.0</span><span class="sxs-lookup"><span data-stu-id="12b32-108">5.0</span></span> |
| [<span data-ttu-id="12b32-109">调用 SendToAsync 后更新 Socket.LocalEndPoint</span><span class="sxs-lookup"><span data-stu-id="12b32-109">Socket.LocalEndPoint is updated after calling SendToAsync</span></span>](#socketlocalendpoint-is-updated-after-calling-sendtoasync) | <span data-ttu-id="12b32-110">5.0</span><span class="sxs-lookup"><span data-stu-id="12b32-110">5.0</span></span> |
| [<span data-ttu-id="12b32-111">已从 .NET 运行时中删除 WinHttpHandler</span><span class="sxs-lookup"><span data-stu-id="12b32-111">WinHttpHandler removed from .NET runtime</span></span>](#winhttphandler-removed-from-net-runtime) | <span data-ttu-id="12b32-112">5.0</span><span class="sxs-lookup"><span data-stu-id="12b32-112">5.0</span></span> |
| [<span data-ttu-id="12b32-113">MulticastOption.Group 不接受 Null 值</span><span class="sxs-lookup"><span data-stu-id="12b32-113">MulticastOption.Group doesn't accept a null value</span></span>](#multicastoptiongroup-doesnt-accept-a-null-value) | <span data-ttu-id="12b32-114">5.0</span><span class="sxs-lookup"><span data-stu-id="12b32-114">5.0</span></span> |
| [<span data-ttu-id="12b32-115">Cookie 路径处理现在符合 RFC 6265</span><span class="sxs-lookup"><span data-stu-id="12b32-115">Cookie Path handling now conforms to RFC 6265</span></span>](#cookie-path-handling-now-conforms-to-rfc-6265) | <span data-ttu-id="12b32-116">5.0</span><span class="sxs-lookup"><span data-stu-id="12b32-116">5.0</span></span> |
| [<span data-ttu-id="12b32-117">HttpRequestMessage.Version 的默认值已更改为 1.1</span><span class="sxs-lookup"><span data-stu-id="12b32-117">Default value of HttpRequestMessage.Version changed to 1.1</span></span>](#default-value-of-httprequestmessageversion-changed-to-11) | <span data-ttu-id="12b32-118">3.0</span><span class="sxs-lookup"><span data-stu-id="12b32-118">3.0</span></span> |
| [<span data-ttu-id="12b32-119">WebClient.CancelAsync 并不总是立即取消</span><span class="sxs-lookup"><span data-stu-id="12b32-119">WebClient.CancelAsync doesn't always cancel immediately</span></span>](#webclientcancelasync-doesnt-always-cancel-immediately) | <span data-ttu-id="12b32-120">2.0</span><span class="sxs-lookup"><span data-stu-id="12b32-120">2.0</span></span> |

## <a name="net-50"></a><span data-ttu-id="12b32-121">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="12b32-121">.NET 5.0</span></span>

[!INCLUDE [negotiatestream-sslstream-dont-fail-on-successive-begin-calls](../../../includes/core-changes/networking/5.0/negotiatestream-sslstream-dont-fail-on-successive-begin-calls.md)]

***

[!INCLUDE [localendpoint-updated-on-sendtoasync](../../../includes/core-changes/networking/5.0/localendpoint-updated-on-sendtoasync.md)]

***

[!INCLUDE [winhttphandler-removed-from-runtime](../../../includes/core-changes/networking/5.0/winhttphandler-removed-from-runtime.md)]

***

[!INCLUDE [multicastoption-group-doesnt-accept-null](../../../includes/core-changes/networking/5.0/multicastoption-group-doesnt-accept-null.md)]

***

[!INCLUDE [cookie-path-conforms-to-rfc6265](../../../includes/core-changes/networking/5.0/cookie-path-conforms-to-rfc6265.md)]

***

## <a name="net-core-30"></a><span data-ttu-id="12b32-122">.NET Core 3.0</span><span class="sxs-lookup"><span data-stu-id="12b32-122">.NET Core 3.0</span></span>

[!INCLUDE[Default value of HttpRequestMessage.Version changed to 1.1](~/includes/core-changes/networking/3.0/httprequestmessage-version-change.md)]

***

## <a name="net-core-20"></a><span data-ttu-id="12b32-123">.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="12b32-123">.NET Core 2.0</span></span>

[!INCLUDE [behavior-change-webclient-cancelasync](../../../includes/core-changes/networking/2.0/behavior-change-webclient-cancelasync.md)]

***
