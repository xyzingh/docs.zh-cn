---
title: 序列化中断性变更
description: 列出 .NET Core 和 .NET 5.0 及更高版本中序列化类别的中断性变更。
ms.date: 07/30/2020
ms.openlocfilehash: 65006e6fb45ed2d54699c9972e0489e3ac5ac8bc
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2020
ms.locfileid: "91955326"
---
# <a name="serialization-breaking-changes"></a><span data-ttu-id="c0997-103">序列化中断性变更</span><span class="sxs-lookup"><span data-stu-id="c0997-103">Serialization breaking changes</span></span>

<span data-ttu-id="c0997-104">本页记录了以下中断性变更：</span><span class="sxs-lookup"><span data-stu-id="c0997-104">The following breaking changes are documented on this page:</span></span>

| <span data-ttu-id="c0997-105">重大更改</span><span class="sxs-lookup"><span data-stu-id="c0997-105">Breaking change</span></span> | <span data-ttu-id="c0997-106">引入的版本</span><span class="sxs-lookup"><span data-stu-id="c0997-106">Introduced version</span></span> |
| - | - |
| [<span data-ttu-id="c0997-107">JsonSerializer.Serialize 在类型参数为 null 时引发 ArgumentNullException</span><span class="sxs-lookup"><span data-stu-id="c0997-107">JsonSerializer.Serialize throws ArgumentNullException when type parameter is null</span></span>](#jsonserializerserialize-throws-argumentnullexception-when-type-parameter-is-null) | <span data-ttu-id="c0997-108">5.0</span><span class="sxs-lookup"><span data-stu-id="c0997-108">5.0</span></span> |
| [<span data-ttu-id="c0997-109">JsonSerializer.Deserialize 需要单字符的字符串</span><span class="sxs-lookup"><span data-stu-id="c0997-109">JsonSerializer.Deserialize requires single-character string</span></span>](#jsonserializerdeserialize-requires-single-character-string) | <span data-ttu-id="c0997-110">5.0</span><span class="sxs-lookup"><span data-stu-id="c0997-110">5.0</span></span> |
| [<span data-ttu-id="c0997-111">BinaryFormatter.Deserialize 重新包装 SerializationException 中的一些异常</span><span class="sxs-lookup"><span data-stu-id="c0997-111">BinaryFormatter.Deserialize rewraps some exceptions in SerializationException</span></span>](#binaryformatterdeserialize-rewraps-some-exceptions-in-serializationexception) | <span data-ttu-id="c0997-112">5.0</span><span class="sxs-lookup"><span data-stu-id="c0997-112">5.0</span></span> |

## <a name="net-50"></a><span data-ttu-id="c0997-113">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="c0997-113">.NET 5.0</span></span>

[!INCLUDE [jsonserializer-serialize-throws-argumentnullexception-for-null-type](../../../includes/core-changes/serialization/5.0/jsonserializer-serialize-throws-argumentnullexception-for-null-type.md)]

***

[!INCLUDE [deserializing-json-into-char-requires-single-character](../../../includes/core-changes/serialization/5.0/deserializing-json-into-char-requires-single-character.md)]

***

[!INCLUDE [binaryformatter-deserialize-rewraps-exceptions](../../../includes/core-changes/serialization/5.0/binaryformatter-deserialize-rewraps-exceptions.md)]

***
