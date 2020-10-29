---
title: 如何确定 .NET Standard 对象是否可序列化
description: 演示如何在运行时确定是否可以序列化 .NET Standard 类型。
ms.date: 10/20/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- serializing objects
- objects, serializing steps
ms.openlocfilehash: a425d44ac3b58a568bd51e638f28a2b76ced9dec
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223991"
---
# <a name="how-to-determine-if-a-net-standard-object-is-serializable"></a><span data-ttu-id="526f6-103">如何确定 .NET Standard 对象是否可序列化</span><span class="sxs-lookup"><span data-stu-id="526f6-103">How to determine if a .NET Standard object is serializable</span></span>

<span data-ttu-id="526f6-104">.NET Standard 是一种规范，用于定义符合该标准版本的特定 .NET 实现上必须存在的类型和成员。</span><span class="sxs-lookup"><span data-stu-id="526f6-104">.NET Standard is a specification that defines the types and members that must be present on specific .NET implementations that conform to that version of the standard.</span></span> <span data-ttu-id="526f6-105">但 .NET Standard 未定义某个类型是否可序列化。</span><span class="sxs-lookup"><span data-stu-id="526f6-105">However, .NET Standard does not define whether a type is serializable.</span></span> <span data-ttu-id="526f6-106">.NET Standard 库中定义的类型未使用 <xref:System.SerializableAttribute> 属性进行标记。</span><span class="sxs-lookup"><span data-stu-id="526f6-106">The types defined in the .NET Standard Library are not marked with the <xref:System.SerializableAttribute> attribute.</span></span> <span data-ttu-id="526f6-107">相反，特定 .NET 实现（如 .NET Framework 和 .NET Core）可随意确定特定类型是否可序列化。</span><span class="sxs-lookup"><span data-stu-id="526f6-107">Instead, specific .NET implementations, such as the .NET Framework and .NET Core, are free to determine whether a particular type is serializable.</span></span>

<span data-ttu-id="526f6-108">如果你开发了面向 .NET Standard 的库，则支持 .NET Standard 的任何 .NET 实现都可以使用你的库。</span><span class="sxs-lookup"><span data-stu-id="526f6-108">If you've developed a library that targets .NET Standard, your library can be consumed by any .NET implementation that supports .NET Standard.</span></span> <span data-ttu-id="526f6-109">这意味着你无法提前知道特定类型是否可序列化；只能在运行时确定它是否可序列化。</span><span class="sxs-lookup"><span data-stu-id="526f6-109">This means that you cannot know in advance whether a particular type is serializable; you can only determine whether it is serializable at run time.</span></span>

<span data-ttu-id="526f6-110">可以通过检索表示对象类型的 <xref:System.Type> 对象的 <xref:System.Type.IsSerializable> 属性值，在运行时确定对象是否可序列化。</span><span class="sxs-lookup"><span data-stu-id="526f6-110">You can determine whether an object is serializable at run time by retrieving the value of the <xref:System.Type.IsSerializable> property of a <xref:System.Type> object that represents that object's type.</span></span> <span data-ttu-id="526f6-111">以下示例提供了一个实现。</span><span class="sxs-lookup"><span data-stu-id="526f6-111">The following example provides one implementation.</span></span> <span data-ttu-id="526f6-112">它定义一个 `IsSerializable(Object)` 扩展方法，用于指示任何 <xref:System.Object> 实例是否可以序列化。</span><span class="sxs-lookup"><span data-stu-id="526f6-112">It defines an `IsSerializable(Object)` extension method that indicates whether any <xref:System.Object> instance can be serialized.</span></span>

[!code-csharp[is-a-type-serializable](~/samples/snippets/standard/serialization/is-serializable/csharp/program.cs#2)]
[!code-vb[is-a-type-serializable](~/samples/snippets/standard/serialization/is-serializable/vb/library.vb#2)]

<span data-ttu-id="526f6-113">随后可以将任何对象传递给该方法，以确定它是否可以在当前 .NET 实现上进行序列化和反序列化，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="526f6-113">You can then pass any object to the method to determine whether it can be serialized and deserialized on the current .NET implementation, as the following example shows:</span></span>

[!code-csharp[test-is-a-type-serializable](~/samples/snippets/standard/serialization/is-serializable/csharp/program.cs#1)]
[!code-vb[test-is-a-type-serializable](~/samples/snippets/standard/serialization/is-serializable/vb/program.vb#1)]

## <a name="see-also"></a><span data-ttu-id="526f6-114">请参阅</span><span class="sxs-lookup"><span data-stu-id="526f6-114">See also</span></span>

- [<span data-ttu-id="526f6-115">二进制序列化</span><span class="sxs-lookup"><span data-stu-id="526f6-115">Binary serialization</span></span>](binary-serialization.md)
- <xref:System.SerializableAttribute?displayProperty=nameWithType>
- <xref:System.Type.IsSerializable?displayProperty=nameWithType>
