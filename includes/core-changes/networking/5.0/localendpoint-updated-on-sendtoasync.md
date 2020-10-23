---
ms.openlocfilehash: 8de70b0c445aa48fc4c3249ccfc8c095890fb14c
ms.sourcegitcommit: 39b1d5f2978be15409c189a66ab30781d9082cd8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2020
ms.locfileid: "92050506"
---
### <a name="socketlocalendpoint-is-updated-after-calling-sendtoasync"></a><span data-ttu-id="e0546-101">调用 SendToAsync 后更新 Socket.LocalEndPoint</span><span class="sxs-lookup"><span data-stu-id="e0546-101">Socket.LocalEndPoint is updated after calling SendToAsync</span></span>

<span data-ttu-id="e0546-102"><xref:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)?displayProperty=nameWithType> 现将 <xref:System.Net.Sockets.Socket.LocalEndPoint?displayProperty=nameWithType> 属性的值更新为套接字的本地地址。</span><span class="sxs-lookup"><span data-stu-id="e0546-102"><xref:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)?displayProperty=nameWithType> now updates the value of the <xref:System.Net.Sockets.Socket.LocalEndPoint?displayProperty=nameWithType> property to the socket's local address.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="e0546-103">引入的版本</span><span class="sxs-lookup"><span data-stu-id="e0546-103">Version introduced</span></span>

<span data-ttu-id="e0546-104">5.0 RC1</span><span class="sxs-lookup"><span data-stu-id="e0546-104">5.0 RC1</span></span>

#### <a name="change-description"></a><span data-ttu-id="e0546-105">更改描述</span><span class="sxs-lookup"><span data-stu-id="e0546-105">Change description</span></span>

<span data-ttu-id="e0546-106">在以前的 .NET 版本中，<xref:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)?displayProperty=nameWithType> 不会更改套接字实例上 <xref:System.Net.Sockets.Socket.LocalEndPoint?displayProperty=nameWithType> 属性的值。</span><span class="sxs-lookup"><span data-stu-id="e0546-106">In previous .NET versions, <xref:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)?displayProperty=nameWithType> does not alter the value of the <xref:System.Net.Sockets.Socket.LocalEndPoint?displayProperty=nameWithType> property on the socket instance.</span></span> <span data-ttu-id="e0546-107">从 .NET 5.0 开始，<xref:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)> 成功完成后，<xref:System.Net.Sockets.Socket.LocalEndPoint?displayProperty=nameWithType> 的值为隐式绑定的套接字的本地地址。</span><span class="sxs-lookup"><span data-stu-id="e0546-107">Starting in .NET 5.0, when <xref:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)> successfully completes, the value of <xref:System.Net.Sockets.Socket.LocalEndPoint?displayProperty=nameWithType> is the implicitly bound socket's local address.</span></span> <span data-ttu-id="e0546-108">这一新行为与 <xref:System.Net.Sockets.Socket.SendTo(System.Byte[],System.Net.EndPoint)> 和 <xref:System.Net.Sockets.Socket.BeginSendTo(System.Byte[],System.Int32,System.Int32,System.Net.Sockets.SocketFlags,System.Net.EndPoint,System.AsyncCallback,System.Object)>/<xref:System.Net.Sockets.Socket.EndSendTo(System.IAsyncResult)> 的行为一致。</span><span class="sxs-lookup"><span data-stu-id="e0546-108">This new behavior is consistent with the behavior of <xref:System.Net.Sockets.Socket.SendTo(System.Byte[],System.Net.EndPoint)> and <xref:System.Net.Sockets.Socket.BeginSendTo(System.Byte[],System.Int32,System.Int32,System.Net.Sockets.SocketFlags,System.Net.EndPoint,System.AsyncCallback,System.Object)>/<xref:System.Net.Sockets.Socket.EndSendTo(System.IAsyncResult)>.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="e0546-109">更改原因</span><span class="sxs-lookup"><span data-stu-id="e0546-109">Reason for change</span></span>

<span data-ttu-id="e0546-110">此更改会[修复一个 bug](https://github.com/dotnet/runtime/issues/915)，并使该行为在 `SendTo` 变体中保持一致。</span><span class="sxs-lookup"><span data-stu-id="e0546-110">This change [fixes a bug](https://github.com/dotnet/runtime/issues/915) and makes the behavior consistent across `SendTo` variants.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="e0546-111">建议的操作</span><span class="sxs-lookup"><span data-stu-id="e0546-111">Recommended action</span></span>

<span data-ttu-id="e0546-112">更改所有假定 <xref:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)> 不会更改 <xref:System.Net.Sockets.Socket.LocalEndPoint?displayProperty=nameWithType> 的值的代码。</span><span class="sxs-lookup"><span data-stu-id="e0546-112">Alter any code that assumes that <xref:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)> won't alter the value of <xref:System.Net.Sockets.Socket.LocalEndPoint?displayProperty=nameWithType>.</span></span>

#### <a name="category"></a><span data-ttu-id="e0546-113">类别</span><span class="sxs-lookup"><span data-stu-id="e0546-113">Category</span></span>

<span data-ttu-id="e0546-114">网络</span><span class="sxs-lookup"><span data-stu-id="e0546-114">Networking</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="e0546-115">受影响的 API</span><span class="sxs-lookup"><span data-stu-id="e0546-115">Affected APIs</span></span>

- <xref:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)?displayProperty=fullName>

<!--

#### Affected APIs

- `M:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)`

-->
