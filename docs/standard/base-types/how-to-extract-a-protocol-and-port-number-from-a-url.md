---
title: 如何：从 URL 中提取协议和端口号
ms.date: 06/30/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- searching with regular expressions, examples
- parsing text with regular expressions, examples
- regular expressions, examples
- .NET regular expressions, examples
- regular expressions [.NET], examples
- pattern-matching with regular expressions, examples
ms.assetid: ab7f62b3-6d2c-4efb-8ac6-28600df5fd5c
ms.openlocfilehash: 9c0ab3cc0d3bcbee1a28d53215a17840be216172
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888542"
---
# <a name="how-to-extract-a-protocol-and-port-number-from-a-url"></a><span data-ttu-id="0706d-102">如何：从 URL 中提取协议和端口号</span><span class="sxs-lookup"><span data-stu-id="0706d-102">How to: Extract a Protocol and Port Number from a URL</span></span>
<span data-ttu-id="0706d-103">下面的示例从 URL 中提取协议和端口号。</span><span class="sxs-lookup"><span data-stu-id="0706d-103">The following example extracts a protocol and port number from a URL.</span></span>  

[!INCLUDE [regex](../../../includes/regex.md)]

## <a name="example"></a><span data-ttu-id="0706d-104">示例</span><span class="sxs-lookup"><span data-stu-id="0706d-104">Example</span></span>  
 <span data-ttu-id="0706d-105">此示例使用 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 方法返回协议，后面依次跟的是冒号和端口号。</span><span class="sxs-lookup"><span data-stu-id="0706d-105">The example uses the <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> method to return the protocol followed by a colon followed by the port number.</span></span>  
  
 [!code-csharp[RegularExpressions.Examples.Protocol#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/cs/Example.cs#1)]
 [!code-vb[RegularExpressions.Examples.Protocol#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/vb/Example.vb#1)]  
  
 <span data-ttu-id="0706d-106">正则表达式模式 `^(?<proto>\w+)://[^/]+?(?<port>:\d+)?/` 可按下表中的方式解释。</span><span class="sxs-lookup"><span data-stu-id="0706d-106">The regular expression pattern `^(?<proto>\w+)://[^/]+?(?<port>:\d+)?/` can be interpreted as shown in the following table.</span></span>  
  
|<span data-ttu-id="0706d-107">模式</span><span class="sxs-lookup"><span data-stu-id="0706d-107">Pattern</span></span>|<span data-ttu-id="0706d-108">说明</span><span class="sxs-lookup"><span data-stu-id="0706d-108">Description</span></span>|  
|-------------|-----------------|  
|`^`|<span data-ttu-id="0706d-109">从字符串的开头部分开始匹配。</span><span class="sxs-lookup"><span data-stu-id="0706d-109">Begin the match at the start of the string.</span></span>|  
|`(?<proto>\w+)`|<span data-ttu-id="0706d-110">匹配一个或多个单词字符。</span><span class="sxs-lookup"><span data-stu-id="0706d-110">Match one or more word characters.</span></span> <span data-ttu-id="0706d-111">将此组命名为 `proto`。</span><span class="sxs-lookup"><span data-stu-id="0706d-111">Name this group `proto`.</span></span>|  
|`://`|<span data-ttu-id="0706d-112">匹配后跟两个正斜线的冒号。</span><span class="sxs-lookup"><span data-stu-id="0706d-112">Match a colon followed by two slash marks.</span></span>|  
|`[^/]+?`|<span data-ttu-id="0706d-113">匹配正斜线以外的任何字符的一次或多次出现（但尽可能少）。</span><span class="sxs-lookup"><span data-stu-id="0706d-113">Match one or more occurrences (but as few as possible) of any character other than a slash mark.</span></span>|  
|`(?<port>:\d+)?`|<span data-ttu-id="0706d-114">匹配后跟一个或多个数字字符的冒号的零次或一次出现。</span><span class="sxs-lookup"><span data-stu-id="0706d-114">Match zero or one occurrence of a colon followed by one or more digit characters.</span></span> <span data-ttu-id="0706d-115">将此组命名为 `port`。</span><span class="sxs-lookup"><span data-stu-id="0706d-115">Name this group `port`.</span></span>|  
|`/`|<span data-ttu-id="0706d-116">匹配正斜线。</span><span class="sxs-lookup"><span data-stu-id="0706d-116">Match a slash mark.</span></span>|  
  
 <span data-ttu-id="0706d-117"><xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 方法扩展 `${proto}${port}` 替换序列，以连接在正则表达式模式中捕获的两个命名组的值。</span><span class="sxs-lookup"><span data-stu-id="0706d-117">The <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> method expands the `${proto}${port}` replacement sequence, which concatenates the value of the two named groups captured in the regular expression pattern.</span></span> <span data-ttu-id="0706d-118">便捷的替换方法是，显式连接从 <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 属性返回的集合对象检索到的字符串。</span><span class="sxs-lookup"><span data-stu-id="0706d-118">It is a convenient alternative to explicitly concatenating the strings retrieved from the collection object returned by the <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> property.</span></span>  
  
 <span data-ttu-id="0706d-119">此示例使用有两处替换（`${proto}` 和 `${port}`）的 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 方法，在输出字符串中添加捕获组。</span><span class="sxs-lookup"><span data-stu-id="0706d-119">The example uses the <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> method with two substitutions, `${proto}` and `${port}`, to include the captured groups in the output string.</span></span> <span data-ttu-id="0706d-120">可以改为从匹配的 <xref:System.Text.RegularExpressions.GroupCollection> 对象检索捕获组，如下面的代码所示。</span><span class="sxs-lookup"><span data-stu-id="0706d-120">You can retrieve the captured groups from the match's <xref:System.Text.RegularExpressions.GroupCollection> object instead, as the following code shows.</span></span>  
  
 [!code-csharp[RegularExpressions.Examples.Protocol#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/cs/example2.cs#2)]
 [!code-vb[RegularExpressions.Examples.Protocol#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/vb/example2.vb#2)]  
  
## <a name="see-also"></a><span data-ttu-id="0706d-121">另请参阅</span><span class="sxs-lookup"><span data-stu-id="0706d-121">See also</span></span>

- [<span data-ttu-id="0706d-122">.NET 正则表达式</span><span class="sxs-lookup"><span data-stu-id="0706d-122">.NET Regular Expressions</span></span>](regular-expressions.md)
