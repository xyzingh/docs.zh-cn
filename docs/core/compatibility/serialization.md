---
title: 序列化中断性变更
description: 列出 .NET Core 和 .NET 5.0 及更高版本中序列化类别的中断性变更。
ms.date: 07/30/2020
ms.openlocfilehash: bb6bd650afeba426edc6e102076f05f97f8e0598
ms.sourcegitcommit: 39b1d5f2978be15409c189a66ab30781d9082cd8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2020
ms.locfileid: "92050453"
---
# <a name="serialization-breaking-changes"></a><span data-ttu-id="5c668-103">序列化中断性变更</span><span class="sxs-lookup"><span data-stu-id="5c668-103">Serialization breaking changes</span></span>

<span data-ttu-id="5c668-104">本页记录了以下中断性变更：</span><span class="sxs-lookup"><span data-stu-id="5c668-104">The following breaking changes are documented on this page:</span></span>

| <span data-ttu-id="5c668-105">重大更改</span><span class="sxs-lookup"><span data-stu-id="5c668-105">Breaking change</span></span> | <span data-ttu-id="5c668-106">引入的版本</span><span class="sxs-lookup"><span data-stu-id="5c668-106">Introduced version</span></span> |
| - | - |
| [<span data-ttu-id="5c668-107">对键值对进行序列化和反序列化时，使用“PropertyNamingPolicy”、“PropertyNameCaseInsensitive”和“Encoder”选项</span><span class="sxs-lookup"><span data-stu-id="5c668-107">PropertyNamingPolicy, PropertyNameCaseInsensitive, and Encoder options are honored when serializing and deserializing key-value pairs</span></span>](#propertynamingpolicy-propertynamecaseinsensitive-and-encoder-options-are-honored-when-serializing-and-deserializing-key-value-pairs) | <span data-ttu-id="5c668-108">5.0</span><span class="sxs-lookup"><span data-stu-id="5c668-108">5.0</span></span> |
| [<span data-ttu-id="5c668-109">非公共的无参数构造函数不用于反序列化</span><span class="sxs-lookup"><span data-stu-id="5c668-109">Non-public, parameterless constructors not used for deserialization</span></span>](#non-public-parameterless-constructors-not-used-for-deserialization) | <span data-ttu-id="5c668-110">5.0</span><span class="sxs-lookup"><span data-stu-id="5c668-110">5.0</span></span> |
| [<span data-ttu-id="5c668-111">JsonSerializer.Serialize 在类型参数为 null 时引发 ArgumentNullException</span><span class="sxs-lookup"><span data-stu-id="5c668-111">JsonSerializer.Serialize throws ArgumentNullException when type parameter is null</span></span>](#jsonserializerserialize-throws-argumentnullexception-when-type-parameter-is-null) | <span data-ttu-id="5c668-112">5.0</span><span class="sxs-lookup"><span data-stu-id="5c668-112">5.0</span></span> |
| [<span data-ttu-id="5c668-113">JsonSerializer.Deserialize 需要单字符的字符串</span><span class="sxs-lookup"><span data-stu-id="5c668-113">JsonSerializer.Deserialize requires single-character string</span></span>](#jsonserializerdeserialize-requires-single-character-string) | <span data-ttu-id="5c668-114">5.0</span><span class="sxs-lookup"><span data-stu-id="5c668-114">5.0</span></span> |
| [<span data-ttu-id="5c668-115">BinaryFormatter.Deserialize 重新包装 SerializationException 中的一些异常</span><span class="sxs-lookup"><span data-stu-id="5c668-115">BinaryFormatter.Deserialize rewraps some exceptions in SerializationException</span></span>](#binaryformatterdeserialize-rewraps-some-exceptions-in-serializationexception) | <span data-ttu-id="5c668-116">5.0</span><span class="sxs-lookup"><span data-stu-id="5c668-116">5.0</span></span> |

## <a name="net-50"></a><span data-ttu-id="5c668-117">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="5c668-117">.NET 5.0</span></span>

[!INCLUDE [options-honored-when-serializing-key-value-pairs](../../../includes/core-changes/serialization/5.0/options-honored-when-serializing-key-value-pairs.md)]

***

[!INCLUDE [non-public-parameterless-constructors-not-used-for-deserialization](../../../includes/core-changes/serialization/5.0/non-public-parameterless-constructors-not-used-for-deserialization.md)]

***

[!INCLUDE [jsonserializer-serialize-throws-argumentnullexception-for-null-type](../../../includes/core-changes/serialization/5.0/jsonserializer-serialize-throws-argumentnullexception-for-null-type.md)]

***

[!INCLUDE [deserializing-json-into-char-requires-single-character](../../../includes/core-changes/serialization/5.0/deserializing-json-into-char-requires-single-character.md)]

***

[!INCLUDE [binaryformatter-deserialize-rewraps-exceptions](../../../includes/core-changes/serialization/5.0/binaryformatter-deserialize-rewraps-exceptions.md)]

***
