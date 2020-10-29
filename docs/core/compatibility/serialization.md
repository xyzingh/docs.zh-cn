---
title: 序列化中断性变更
description: 列出 .NET Core 和 .NET 5.0 及更高版本中序列化类别的中断性变更。
ms.date: 07/30/2020
ms.openlocfilehash: 67608c8e7a9745c060b7eb179fe5a956ede9f80f
ms.sourcegitcommit: dfcbc096ad7908cd58a5f0aeabd2256f05266bac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92332870"
---
# <a name="serialization-breaking-changes"></a><span data-ttu-id="8552a-103">序列化中断性变更</span><span class="sxs-lookup"><span data-stu-id="8552a-103">Serialization breaking changes</span></span>

<span data-ttu-id="8552a-104">本页记录了以下中断性变更：</span><span class="sxs-lookup"><span data-stu-id="8552a-104">The following breaking changes are documented on this page:</span></span>

| <span data-ttu-id="8552a-105">重大更改</span><span class="sxs-lookup"><span data-stu-id="8552a-105">Breaking change</span></span> | <span data-ttu-id="8552a-106">引入的版本</span><span class="sxs-lookup"><span data-stu-id="8552a-106">Introduced version</span></span> |
| - | - |
| [<span data-ttu-id="8552a-107">ASP.NET Core 应用允许反序列化带引号的数字</span><span class="sxs-lookup"><span data-stu-id="8552a-107">ASP.NET Core apps allow deserializing quoted numbers</span></span>](#aspnet-core-apps-allow-deserializing-quoted-numbers) | <span data-ttu-id="8552a-108">5.0</span><span class="sxs-lookup"><span data-stu-id="8552a-108">5.0</span></span> |
| [<span data-ttu-id="8552a-109">对键值对进行序列化和反序列化时，使用“PropertyNamingPolicy”、“PropertyNameCaseInsensitive”和“Encoder”选项</span><span class="sxs-lookup"><span data-stu-id="8552a-109">PropertyNamingPolicy, PropertyNameCaseInsensitive, and Encoder options are honored when serializing and deserializing key-value pairs</span></span>](#propertynamingpolicy-propertynamecaseinsensitive-and-encoder-options-are-honored-when-serializing-and-deserializing-key-value-pairs) | <span data-ttu-id="8552a-110">5.0</span><span class="sxs-lookup"><span data-stu-id="8552a-110">5.0</span></span> |
| [<span data-ttu-id="8552a-111">非公共的无参数构造函数不用于反序列化</span><span class="sxs-lookup"><span data-stu-id="8552a-111">Non-public, parameterless constructors not used for deserialization</span></span>](#non-public-parameterless-constructors-not-used-for-deserialization) | <span data-ttu-id="8552a-112">5.0</span><span class="sxs-lookup"><span data-stu-id="8552a-112">5.0</span></span> |
| [<span data-ttu-id="8552a-113">JsonSerializer.Serialize 在类型参数为 null 时引发 ArgumentNullException</span><span class="sxs-lookup"><span data-stu-id="8552a-113">JsonSerializer.Serialize throws ArgumentNullException when type parameter is null</span></span>](#jsonserializerserialize-throws-argumentnullexception-when-type-parameter-is-null) | <span data-ttu-id="8552a-114">5.0</span><span class="sxs-lookup"><span data-stu-id="8552a-114">5.0</span></span> |
| [<span data-ttu-id="8552a-115">JsonSerializer.Deserialize 需要单字符的字符串</span><span class="sxs-lookup"><span data-stu-id="8552a-115">JsonSerializer.Deserialize requires single-character string</span></span>](#jsonserializerdeserialize-requires-single-character-string) | <span data-ttu-id="8552a-116">5.0</span><span class="sxs-lookup"><span data-stu-id="8552a-116">5.0</span></span> |
| [<span data-ttu-id="8552a-117">BinaryFormatter.Deserialize 重新包装 SerializationException 中的一些异常</span><span class="sxs-lookup"><span data-stu-id="8552a-117">BinaryFormatter.Deserialize rewraps some exceptions in SerializationException</span></span>](#binaryformatterdeserialize-rewraps-some-exceptions-in-serializationexception) | <span data-ttu-id="8552a-118">5.0</span><span class="sxs-lookup"><span data-stu-id="8552a-118">5.0</span></span> |

## <a name="net-50"></a><span data-ttu-id="8552a-119">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="8552a-119">.NET 5.0</span></span>

[!INCLUDE [jsonserializer-allows-reading-numbers-as-strings](../../../includes/core-changes/serialization/5.0/jsonserializer-allows-reading-numbers-as-strings.md)]

***

[!INCLUDE [options-honored-when-serializing-key-value-pairs](../../../includes/core-changes/serialization/5.0/options-honored-when-serializing-key-value-pairs.md)]

<span data-ttu-id="8552a-120">\*\*_</span><span class="sxs-lookup"><span data-stu-id="8552a-120">\*\*_</span></span>

[!INCLUDE [non-public-parameterless-constructors-not-used-for-deserialization](../../../includes/core-changes/serialization/5.0/non-public-parameterless-constructors-not-used-for-deserialization.md)]

_*_

[!INCLUDE [jsonserializer-serialize-throws-argumentnullexception-for-null-type](../../../includes/core-changes/serialization/5.0/jsonserializer-serialize-throws-argumentnullexception-for-null-type.md)]

_*_

[!INCLUDE [deserializing-json-into-char-requires-single-character](../../../includes/core-changes/serialization/5.0/deserializing-json-into-char-requires-single-character.md)]

_*_

[!INCLUDE [binaryformatter-deserialize-rewraps-exceptions](../../../includes/core-changes/serialization/5.0/binaryformatter-deserialize-rewraps-exceptions.md)]

<span data-ttu-id="8552a-121">_\*\*</span><span class="sxs-lookup"><span data-stu-id="8552a-121">_\*\*</span></span>
