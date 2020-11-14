---
title: 二进制序列化
description: 本文介绍了 .NET Core 支持的二进制序列化和类型。 请注意二进制序列化和替代项的危险。
ms.date: 01/02/2018
helpviewer_keywords:
- binary serialization
- serialization, about serialization
- deserialization
- binary serialization, about serialization
- binary serialization, .net core serialization
- serialization, cross-framework
ms.assetid: 2b1ea3be-1152-4032-b2b3-07794054c405
author: ViktorHofer
ms.openlocfilehash: bfb504862232345db07bdc92993069fc87afdbeb
ms.sourcegitcommit: 74d05613d6c57106f83f82ce8ee71176874ea3f0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93282090"
---
# <a name="binary-serialization"></a><span data-ttu-id="d23c9-104">二进制序列化</span><span class="sxs-lookup"><span data-stu-id="d23c9-104">Binary serialization</span></span>

<span data-ttu-id="d23c9-105">可以将序列化定义为一个将对象状态存储到存储介质的过程。</span><span class="sxs-lookup"><span data-stu-id="d23c9-105">Serialization can be defined as the process of storing the state of an object to a storage medium.</span></span> <span data-ttu-id="d23c9-106">在这个过程中，对象的公共字段和私有字段以及类（包括含有该类的程序集）的名称，将转换成字节流，而字节流接着将写入数据流。</span><span class="sxs-lookup"><span data-stu-id="d23c9-106">During this process, the public and private fields of the object and the name of the class, including the assembly containing the class, are converted to a stream of bytes, which is then written to a data stream.</span></span> <span data-ttu-id="d23c9-107">随后对该对象进行反序列化时，将创建原始对象的准确克隆。</span><span class="sxs-lookup"><span data-stu-id="d23c9-107">When the object is subsequently deserialized, an exact clone of the original object is created.</span></span>

<span data-ttu-id="d23c9-108">在面向对象的环境中实现序列化机制时，必须多在易用性与灵活性之间做出权衡。</span><span class="sxs-lookup"><span data-stu-id="d23c9-108">When implementing a serialization mechanism in an object-oriented environment, you have to make a number of tradeoffs between ease of use and flexibility.</span></span> <span data-ttu-id="d23c9-109">很大程度上，这个过程可以自动完成，但前提是您对该过程拥有足够的控制权。</span><span class="sxs-lookup"><span data-stu-id="d23c9-109">The process can be automated to a large extent, provided you are given sufficient control over the process.</span></span> <span data-ttu-id="d23c9-110">例如，如果简单的二进制序列化不足，或者可能有特定原因决定需要对类中的哪些字段进行序列化，可能就会出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="d23c9-110">For example, situations may arise where simple binary serialization is not sufficient, or there might be a specific reason to decide which fields in a class need to be serialized.</span></span> <span data-ttu-id="d23c9-111">以下章节验证了随 .NET Framework 一起提供的可靠序列化机制，并强调了根据需要自定义该过程所能使用的一些重要功能。</span><span class="sxs-lookup"><span data-stu-id="d23c9-111">The following sections examine the robust serialization mechanism provided with .NET and highlight a number of important features that allow you to customize the process to meet your needs.</span></span>

> [!NOTE]
> <span data-ttu-id="d23c9-112">如果使用不同的 .NET 版本序列化和反序列化以 UTF-8 或 UTF-7 编码的对象，则不保留该对象的状态。</span><span class="sxs-lookup"><span data-stu-id="d23c9-112">The state of a UTF-8 or UTF-7 encoded object is not preserved if the object is serialized and deserialized using different .NET versions.</span></span>

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]

<span data-ttu-id="d23c9-113">二进制序列化允许修改对象内部的私有成员，从而更改其状态。</span><span class="sxs-lookup"><span data-stu-id="d23c9-113">Binary serialization allows modifying private members inside an object and therefore changing the state of it.</span></span> <span data-ttu-id="d23c9-114">因此，建议采用在公共 API 表面运行的其他序列化框架，例如 <xref:System.Text.Json?displayProperty=fullName>。</span><span class="sxs-lookup"><span data-stu-id="d23c9-114">Because of this, other serialization frameworks, like <xref:System.Text.Json?displayProperty=fullName>, that operate on the public API surface are recommended.</span></span>

## <a name="net-core"></a><span data-ttu-id="d23c9-115">.NET Core</span><span class="sxs-lookup"><span data-stu-id="d23c9-115">.NET Core</span></span>

<span data-ttu-id="d23c9-116">.NET Core 支持类型子集的二进制序列化。</span><span class="sxs-lookup"><span data-stu-id="d23c9-116">.NET Core supports binary serialization for a subset of types.</span></span> <span data-ttu-id="d23c9-117">可在下面的[可序列化类型](#serializable-types)部分查看受支持的类型列表。</span><span class="sxs-lookup"><span data-stu-id="d23c9-117">You can see the list of supported types in the [Serializable types](#serializable-types) section that follows.</span></span> <span data-ttu-id="d23c9-118">列出的类型是完全可以在 .NET Framework 4.5.1 及更高版本之间和 .NET Core 2.0 及更高版本之间进行序列化的。</span><span class="sxs-lookup"><span data-stu-id="d23c9-118">The listed types are guaranteed to be serializable between .NET Framework 4.5.1 and later versions and between .NET Core 2.0 and later versions.</span></span> <span data-ttu-id="d23c9-119">其他 .NET 实现（如 Mono）并未正式得到支持，但应该也能使用。</span><span class="sxs-lookup"><span data-stu-id="d23c9-119">Other .NET implementations, such as Mono, aren't officially supported but should also work.</span></span>

### <a name="serializable-types"></a><span data-ttu-id="d23c9-120">可序列化类型</span><span class="sxs-lookup"><span data-stu-id="d23c9-120">Serializable types</span></span>

> [!div class="mx-tdCol2BreakAll"]
> | <span data-ttu-id="d23c9-121">类型</span><span class="sxs-lookup"><span data-stu-id="d23c9-121">Type</span></span> | <span data-ttu-id="d23c9-122">说明</span><span class="sxs-lookup"><span data-stu-id="d23c9-122">Notes</span></span> |
> | - | - |
> | <xref:Microsoft.CSharp.RuntimeBinder.RuntimeBinderException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-123">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-123">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:Microsoft.CSharp.RuntimeBinder.RuntimeBinderInternalCompilerException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-124">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-124">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.AccessViolationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-125">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-125">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.AggregateException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-126">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-126">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.AppDomainUnloadedException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-127">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-127">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ApplicationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-128">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-128">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ArgumentException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-129">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-129">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ArgumentNullException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-130">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-130">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ArgumentOutOfRangeException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-131">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-131">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ArithmeticException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-132">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-132">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Array?displayProperty=nameWithType> | |
> | <xref:System.ArraySegment%601?displayProperty=nameWithType> | |
> | <xref:System.ArrayTypeMismatchException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-133">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-133">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Attribute?displayProperty=nameWithType> | |
> | <xref:System.BadImageFormatException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-134">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-134">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Boolean?displayProperty=nameWithType> | |
> | <xref:System.Byte?displayProperty=nameWithType> | |
> | <xref:System.CannotUnloadAppDomainException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-135">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-135">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Char?displayProperty=nameWithType> | |
> | <xref:System.Collections.ArrayList?displayProperty=nameWithType> | |
> | <xref:System.Collections.BitArray?displayProperty=nameWithType> | |
> | <xref:System.Collections.Comparer?displayProperty=nameWithType> | |
> | <xref:System.Collections.DictionaryEntry?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.Comparer%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.EqualityComparer%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.HashSet%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.KeyNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-136">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-136">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Collections.Generic.KeyValuePair%602?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.LinkedList%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.SortedDictionary%602?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.SortedList%602?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.SortedSet%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.Stack%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Hashtable?displayProperty=nameWithType> | |
> | <xref:System.Collections.ObjectModel.Collection%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.ObjectModel.KeyedCollection%602?displayProperty=nameWithType> | |
> | <xref:System.Collections.ObjectModel.ObservableCollection%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.ObjectModel.ReadOnlyDictionary%602?displayProperty=nameWithType> | |
> | <xref:System.Collections.ObjectModel.ReadOnlyObservableCollection%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Queue?displayProperty=nameWithType> | |
> | <xref:System.Collections.SortedList?displayProperty=nameWithType> | |
> | <xref:System.Collections.Specialized.HybridDictionary?displayProperty=nameWithType> | |
> | <xref:System.Collections.Specialized.ListDictionary?displayProperty=nameWithType> | |
> | <xref:System.Collections.Specialized.OrderedDictionary?displayProperty=nameWithType> | |
> | <xref:System.Collections.Specialized.StringCollection?displayProperty=nameWithType> | |
> | <xref:System.Collections.Specialized.StringDictionary?displayProperty=nameWithType> | |
> | <xref:System.Collections.Stack?displayProperty=nameWithType> | |
> | `System.Collections.Generic.NonRandomizedStringEqualityComparer` | <span data-ttu-id="d23c9-137">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-137">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ComponentModel.BindingList%601?displayProperty=nameWithType> | |
> | <xref:System.ComponentModel.DataAnnotations.ValidationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-138">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-138">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ComponentModel.Design.CheckoutException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-139">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-139">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ComponentModel.InvalidAsynchronousStateException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-140">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-140">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ComponentModel.InvalidEnumArgumentException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-141">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-141">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ComponentModel.LicenseException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-142">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-142">Starting in .NET Core 2.0.4.</span></span><br/><span data-ttu-id="d23c9-143">不支持从 .NET Framework 到 .NET Core 的序列化。</span><span class="sxs-lookup"><span data-stu-id="d23c9-143">Serialization from .NET Framework to .NET Core is not supported.</span></span> |
> | <xref:System.ComponentModel.WarningException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-144">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-144">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ComponentModel.Win32Exception?displayProperty=nameWithType> | <span data-ttu-id="d23c9-145">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-145">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Configuration.ConfigurationErrorsException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-146">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-146">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Configuration.ConfigurationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-147">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-147">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Configuration.Provider.ProviderException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-148">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-148">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Configuration.SettingsPropertyIsReadOnlyException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-149">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-149">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Configuration.SettingsPropertyNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-150">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-150">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Configuration.SettingsPropertyWrongTypeException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-151">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-151">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ContextMarshalException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-152">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-152">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DBNull?displayProperty=nameWithType> | <span data-ttu-id="d23c9-153">从 .NET Core 2.0.2 和更高版本开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-153">Starting in .NET Core 2.0.2 and later versions.</span></span> |
> | <xref:System.Data.Common.DbException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-154">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-154">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.ConstraintException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-155">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-155">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.DBConcurrencyException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-156">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-156">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.DataException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-157">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-157">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.DataSet?displayProperty=nameWithType> | |
> | <xref:System.Data.DataTable?displayProperty=nameWithType> | <span data-ttu-id="d23c9-158">如果将 `RemotingFormat` 设置为 `SerializationFormat.Binary`，则只能与 .NET Core 2.1 和更高版本进行交换。</span><span class="sxs-lookup"><span data-stu-id="d23c9-158">If you set `RemotingFormat` to `SerializationFormat.Binary`, it can only be exchanged with .NET Core 2.1 and later versions.</span></span> |
> | <xref:System.Data.DeletedRowInaccessibleException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-159">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-159">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.DuplicateNameException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-160">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-160">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.EvaluateException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-161">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-161">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.InRowChangingEventException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-162">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-162">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.InvalidConstraintException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-163">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-163">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.InvalidExpressionException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-164">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-164">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.MissingPrimaryKeyException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-165">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-165">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.NoNullAllowedException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-166">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-166">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.Odbc.OdbcException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-167">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-167">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.OperationAbortedException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-168">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-168">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.PropertyCollection?displayProperty=nameWithType> | |
> | <xref:System.Data.ReadOnlyException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-169">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-169">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.RowNotInTableException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-170">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-170">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.SqlClient.SqlException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-171">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-171">Starting in .NET Core 2.0.4.</span></span><br/><span data-ttu-id="d23c9-172">不支持从 .NET Framework 到 .NET Core 的序列化</span><span class="sxs-lookup"><span data-stu-id="d23c9-172">Serialization from .NET Framework to .NET Core is not supported</span></span> |
> | <xref:System.Data.SqlTypes.SqlAlreadyFilledException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-173">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-173">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.SqlTypes.SqlBoolean?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlByte?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlDateTime?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlDouble?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlGuid?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlInt16?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlInt32?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlInt64?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlNotFilledException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-174">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-174">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.SqlTypes.SqlNullValueException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-175">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-175">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.SqlTypes.SqlString?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlTruncateException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-176">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-176">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.SqlTypes.SqlTypeException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-177">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-177">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.StrongTypingException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-178">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-178">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.SyntaxErrorException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-179">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-179">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.VersionNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-180">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-180">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DataMisalignedException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-181">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-181">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DateTime?displayProperty=nameWithType> | |
> | <xref:System.DateTimeOffset?displayProperty=nameWithType> | |
> | <xref:System.Decimal?displayProperty=nameWithType> | |
> | `System.Diagnostics.Contracts.ContractException` | <span data-ttu-id="d23c9-182">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-182">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Diagnostics.Tracing.EventSourceException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-183">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-183">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.DirectoryNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-184">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-184">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.AccountManagement.MultipleMatchesException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-185">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-185">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.AccountManagement.NoMatchingPrincipalException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-186">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-186">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.AccountManagement.PasswordException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-187">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-187">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.AccountManagement.PrincipalException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-188">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-188">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.AccountManagement.PrincipalExistsException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-189">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-189">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.AccountManagement.PrincipalOperationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-190">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-190">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.AccountManagement.PrincipalServerDownException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-191">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-191">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryObjectExistsException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-192">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-192">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryObjectNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-193">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-193">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryOperationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-194">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-194">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryServerDownException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-195">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-195">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.ActiveDirectory.ForestTrustCollisionException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-196">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-196">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.ActiveDirectory.SyncFromAllServersOperationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-197">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-197">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.DirectoryServicesCOMException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-198">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-198">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.Protocols.BerConversionException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-199">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-199">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.Protocols.DirectoryException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-200">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-200">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.Protocols.DirectoryOperationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-201">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-201">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.Protocols.LdapException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-202">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-202">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.Protocols.TlsOperationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-203">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-203">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DivideByZeroException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-204">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-204">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DllNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-205">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-205">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Double?displayProperty=nameWithType> | |
> | <xref:System.Drawing.Color?displayProperty=nameWithType> | |
> | <xref:System.Drawing.Point?displayProperty=nameWithType> | |
> | <xref:System.Drawing.PointF?displayProperty=nameWithType> | |
> | <xref:System.Drawing.Rectangle?displayProperty=nameWithType> | |
> | <xref:System.Drawing.RectangleF?displayProperty=nameWithType> | |
> | <xref:System.Drawing.Size?displayProperty=nameWithType> | |
> | <xref:System.Drawing.SizeF?displayProperty=nameWithType> | |
> | <xref:System.DuplicateWaitObjectException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-206">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-206">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.EntryPointNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-207">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-207">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Enum?displayProperty=nameWithType> | |
> | <xref:System.EventArgs?displayProperty=nameWithType> | <span data-ttu-id="d23c9-208">从 .NET Core 2.0.6 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-208">Starting in .NET Core 2.0.6.</span></span> |
> | <xref:System.Exception?displayProperty=nameWithType> | |
> | <xref:System.ExecutionEngineException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-209">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-209">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.FieldAccessException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-210">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-210">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.FormatException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-211">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-211">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Globalization.CompareInfo?displayProperty=nameWithType> | |
> | <xref:System.Globalization.CultureNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-212">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-212">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Globalization.SortVersion?displayProperty=nameWithType> | |
> | <xref:System.Guid?displayProperty=nameWithType> | |
> | `System.IO.Compression.ZLibException` | <span data-ttu-id="d23c9-213">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-213">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.DriveNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-214">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-214">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.EndOfStreamException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-215">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-215">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.FileFormatException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-216">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-216">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.FileLoadException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-217">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-217">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.FileNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-218">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-218">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.IOException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-219">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-219">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.InternalBufferOverflowException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-220">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-220">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.InvalidDataException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-221">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-221">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.IsolatedStorage.IsolatedStorageException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-222">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-222">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.PathTooLongException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-223">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-223">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IndexOutOfRangeException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-224">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-224">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.InsufficientExecutionStackException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-225">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-225">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.InsufficientMemoryException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-226">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-226">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Int16?displayProperty=nameWithType> | |
> | <xref:System.Int32?displayProperty=nameWithType> | |
> | <xref:System.Int64?displayProperty=nameWithType> | |
> | <xref:System.IntPtr?displayProperty=nameWithType> | |
> | <xref:System.InvalidCastException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-227">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-227">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.InvalidOperationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-228">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-228">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.InvalidProgramException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-229">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-229">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.InvalidTimeZoneException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-230">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-230">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.MemberAccessException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-231">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-231">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.MethodAccessException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-232">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-232">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.MissingFieldException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-233">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-233">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.MissingMemberException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-234">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-234">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.MissingMethodException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-235">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-235">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.MulticastNotSupportedException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-236">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-236">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.Cookie?displayProperty=nameWithType> | |
> | <xref:System.Net.CookieCollection?displayProperty=nameWithType> | |
> | <xref:System.Net.CookieContainer?displayProperty=nameWithType> | |
> | <xref:System.Net.CookieException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-237">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-237">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.HttpListenerException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-238">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-238">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.Mail.SmtpException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-239">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-239">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.Mail.SmtpFailedRecipientException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-240">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-240">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.Mail.SmtpFailedRecipientsException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-241">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-241">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.NetworkInformation.NetworkInformationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-242">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-242">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.NetworkInformation.PingException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-243">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-243">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.ProtocolViolationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-244">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-244">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.Sockets.SocketException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-245">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-245">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.WebException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-246">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-246">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.WebSockets.WebSocketException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-247">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-247">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.NotFiniteNumberException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-248">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-248">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.NotImplementedException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-249">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-249">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.NotSupportedException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-250">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-250">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.NullReferenceException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-251">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-251">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Nullable%601?displayProperty=nameWithType> | |
> | <xref:System.Numerics.BigInteger?displayProperty=nameWithType> | |
> | <xref:System.Numerics.Complex?displayProperty=nameWithType> | |
> | <xref:System.Object?displayProperty=nameWithType> | |
> | <xref:System.ObjectDisposedException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-252">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-252">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.OperationCanceledException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-253">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-253">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.OutOfMemoryException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-254">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-254">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.OverflowException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-255">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-255">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.PlatformNotSupportedException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-256">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-256">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.RankException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-257">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-257">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Reflection.AmbiguousMatchException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-258">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-258">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Reflection.CustomAttributeFormatException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-259">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-259">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Reflection.InvalidFilterCriteriaException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-260">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-260">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Reflection.ReflectionTypeLoadException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-261">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-261">Starting in .NET Core 2.0.4.</span></span><br/><span data-ttu-id="d23c9-262">不支持从 .NET Framework 到 .NET Core 的序列化。</span><span class="sxs-lookup"><span data-stu-id="d23c9-262">Serialization from .NET Framework to .NET Core is not supported.</span></span> |
> | <xref:System.Reflection.TargetException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-263">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-263">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Reflection.TargetInvocationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-264">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-264">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Reflection.TargetParameterCountException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-265">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-265">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Resources.MissingManifestResourceException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-266">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-266">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Resources.MissingSatelliteAssemblyException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-267">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-267">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.CompilerServices.RuntimeWrappedException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-268">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-268">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.COMException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-269">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-269">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.ExternalException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-270">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-270">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.InvalidComObjectException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-271">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-271">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.InvalidOleVariantTypeException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-272">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-272">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.MarshalDirectiveException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-273">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-273">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.SEHException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-274">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-274">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.SafeArrayRankMismatchException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-275">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-275">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.SafeArrayTypeMismatchException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-276">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-276">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.Serialization.InvalidDataContractException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-277">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-277">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.Serialization.SerializationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-278">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-278">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.SByte?displayProperty=nameWithType> | |
> | <xref:System.Security.AccessControl.PrivilegeNotHeldException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-279">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-279">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.Authentication.AuthenticationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-280">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-280">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.Authentication.InvalidCredentialException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-281">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-281">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.Cryptography.CryptographicException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-282">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-282">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.Cryptography.CryptographicUnexpectedOperationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-283">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-283">Starting in .NET Core 2.0.4.</span></span> |
> | `System.Security.Cryptography.Xml.CryptoSignedXmlRecursionException` | <span data-ttu-id="d23c9-284">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-284">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.HostProtectionException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-285">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-285">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.Policy.PolicyException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-286">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-286">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.Principal.IdentityNotMappedException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-287">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-287">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.SecurityException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-288">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-288">Starting in .NET Core 2.0.4.</span></span><br/><span data-ttu-id="d23c9-289">有限的序列化数据。</span><span class="sxs-lookup"><span data-stu-id="d23c9-289">Limited serialization data.</span></span> |
> | <xref:System.Security.VerificationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-290">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-290">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.XmlSyntaxException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-291">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-291">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ServiceProcess.TimeoutException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-292">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-292">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Single?displayProperty=nameWithType> | |
> | <xref:System.StackOverflowException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-293">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-293">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.String?displayProperty=nameWithType> | |
> | <xref:System.StringComparer?displayProperty=nameWithType> | |
> | <xref:System.SystemException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-294">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-294">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Text.DecoderFallbackException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-295">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-295">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Text.EncoderFallbackException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-296">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-296">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Text.RegularExpressions.RegexMatchTimeoutException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-297">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-297">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Text.StringBuilder?displayProperty=nameWithType> | |
> | <xref:System.Threading.AbandonedMutexException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-298">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-298">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.BarrierPostPhaseException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-299">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-299">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.LockRecursionException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-300">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-300">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.SemaphoreFullException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-301">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-301">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.SynchronizationLockException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-302">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-302">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.Tasks.TaskCanceledException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-303">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-303">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.Tasks.TaskSchedulerException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-304">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-304">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.ThreadAbortException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-305">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-305">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.ThreadInterruptedException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-306">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-306">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.ThreadStartException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-307">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-307">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.ThreadStateException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-308">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-308">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.WaitHandleCannotBeOpenedException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-309">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-309">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.TimeSpan?displayProperty=nameWithType> | |
> | <xref:System.TimeZoneInfo.AdjustmentRule?displayProperty=nameWithType> | |
> | <xref:System.TimeZoneInfo?displayProperty=nameWithType> | |
> | <xref:System.TimeZoneNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-310">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-310">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.TimeoutException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-311">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-311">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Transactions.TransactionAbortedException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-312">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-312">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Transactions.TransactionException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-313">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-313">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Transactions.TransactionInDoubtException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-314">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-314">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Transactions.TransactionManagerCommunicationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-315">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-315">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Transactions.TransactionPromotionException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-316">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-316">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Tuple?displayProperty=nameWithType> | |
> | <xref:System.TypeAccessException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-317">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-317">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.TypeInitializationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-318">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-318">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.TypeLoadException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-319">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-319">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.TypeUnloadedException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-320">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-320">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.UInt16?displayProperty=nameWithType> | |
> | <xref:System.UInt32?displayProperty=nameWithType> | |
> | <xref:System.UInt64?displayProperty=nameWithType> | |
> | <xref:System.UIntPtr?displayProperty=nameWithType> | |
> | <xref:System.UnauthorizedAccessException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-321">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-321">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Uri?displayProperty=nameWithType> | |
> | <xref:System.UriFormatException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-322">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-322">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ValueTuple?displayProperty=nameWithType> | <span data-ttu-id="d23c9-323">在 .NET Framework 4.7 及早期版本中不可序列化。</span><span class="sxs-lookup"><span data-stu-id="d23c9-323">Not serializable in .NET Framework 4.7 and earlier versions.</span></span> |
> | <xref:System.ValueType?displayProperty=nameWithType> | |
> | <xref:System.Version?displayProperty=nameWithType> | |
> | <xref:System.WeakReference%601?displayProperty=nameWithType> | |
> | <xref:System.WeakReference?displayProperty=nameWithType> | |
> | <xref:System.Xml.Schema.XmlSchemaException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-324">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-324">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Xml.Schema.XmlSchemaInferenceException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-325">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-325">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Xml.Schema.XmlSchemaValidationException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-326">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-326">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Xml.XPath.XPathException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-327">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-327">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Xml.XmlException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-328">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-328">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Xml.Xsl.XsltCompileException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-329">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-329">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Xml.Xsl.XsltException?displayProperty=nameWithType> | <span data-ttu-id="d23c9-330">从 .NET Core 2.0.4 开始。</span><span class="sxs-lookup"><span data-stu-id="d23c9-330">Starting in .NET Core 2.0.4.</span></span> |

## <a name="see-also"></a><span data-ttu-id="d23c9-331">请参阅</span><span class="sxs-lookup"><span data-stu-id="d23c9-331">See also</span></span>

- <xref:System.Runtime.Serialization>\
<span data-ttu-id="d23c9-332">包含可用于序列化和反序列化对象的类。</span><span class="sxs-lookup"><span data-stu-id="d23c9-332">Contains classes that can be used for serializing and deserializing objects.</span></span>

- <span data-ttu-id="d23c9-333">[XML 和 SOAP 序列化](xml-and-soap-serialization.md)</span><span class="sxs-lookup"><span data-stu-id="d23c9-333">[XML and SOAP Serialization](xml-and-soap-serialization.md)</span></span>\
<span data-ttu-id="d23c9-334">描述随公共语言运行库一起提供的 XML 序列化机制。</span><span class="sxs-lookup"><span data-stu-id="d23c9-334">Describes the XML serialization mechanism that is included with the common language runtime.</span></span>

- <span data-ttu-id="d23c9-335">[安全和序列化](../../framework/misc/security-and-serialization.md)</span><span class="sxs-lookup"><span data-stu-id="d23c9-335">[Security and Serialization](../../framework/misc/security-and-serialization.md)</span></span>\
<span data-ttu-id="d23c9-336">描述写入执行序列化的代码时需要遵循的安全编码原则。</span><span class="sxs-lookup"><span data-stu-id="d23c9-336">Describes the secure coding guidelines to follow when writing code that performs serialization.</span></span>

- <span data-ttu-id="d23c9-337">[.NET 远程处理](/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="d23c9-337">[.NET Remoting](/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100))</span></span>\
<span data-ttu-id="d23c9-338">描述 .NET Framework 中提供的用于远程通信的多种方法。</span><span class="sxs-lookup"><span data-stu-id="d23c9-338">Describes the various methods in .NET Framework for remote communications.</span></span>

- <span data-ttu-id="d23c9-339">[使用 ASP.NET 创建的 XML Web service 以及 XML Web service 客户端](/previous-versions/dotnet/netframework-4.0/7bkzywba(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="d23c9-339">[XML Web Services Created Using ASP.NET and XML Web Service Clients](/previous-versions/dotnet/netframework-4.0/7bkzywba(v=vs.100))</span></span>\
<span data-ttu-id="d23c9-340">描述并解释如何对使用 ASP.NET 创建的 XML Web services 进行编程的文章。</span><span class="sxs-lookup"><span data-stu-id="d23c9-340">Articles that describe and explain how to program XML Web services created using ASP.NET.</span></span>
