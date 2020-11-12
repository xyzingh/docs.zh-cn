---
title: 导入声明：open 关键字
description: '了解 F # 导入声明以及如何指定可在不使用完全限定名称的情况下引用其元素的模块或命名空间。'
ms.date: 08/15/2020
ms.openlocfilehash: ab208c53809e120bc216c8f8b4d04a322d67cf2f
ms.sourcegitcommit: f99115e12a5eb75638abe45072e023a3ce3351ac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2020
ms.locfileid: "94557176"
---
# <a name="import-declarations-the-open-keyword"></a><span data-ttu-id="c2fea-103">导入声明： `open` 关键字</span><span class="sxs-lookup"><span data-stu-id="c2fea-103">Import declarations: The `open` keyword</span></span>

<span data-ttu-id="c2fea-104">*导入声明* 指定了一个模块或命名空间，在不使用完全限定名称的情况下，可以引用这些元素。</span><span class="sxs-lookup"><span data-stu-id="c2fea-104">An *import declaration* specifies a module or namespace whose elements you can reference without using a fully qualified name.</span></span>

## <a name="syntax"></a><span data-ttu-id="c2fea-105">语法</span><span class="sxs-lookup"><span data-stu-id="c2fea-105">Syntax</span></span>

```fsharp
open module-or-namespace-name
open type type-name
```

## <a name="remarks"></a><span data-ttu-id="c2fea-106">备注</span><span class="sxs-lookup"><span data-stu-id="c2fea-106">Remarks</span></span>

<span data-ttu-id="c2fea-107">每次使用完全限定的命名空间或模块路径引用代码都可以创建难以编写、读取和维护的代码。</span><span class="sxs-lookup"><span data-stu-id="c2fea-107">Referencing code by using the fully qualified namespace or module path every time can create code that is hard to write, read, and maintain.</span></span> <span data-ttu-id="c2fea-108">相反，可以将关键字用于 `open` 经常使用的模块和命名空间，以便在引用该模块或命名空间的成员时，可以使用名称的缩写，而不是完全限定的名称。</span><span class="sxs-lookup"><span data-stu-id="c2fea-108">Instead, you can use the `open` keyword for frequently used modules and namespaces so that when you reference a member of that module or namespace, you can use the short form of the name instead of the fully qualified name.</span></span> <span data-ttu-id="c2fea-109">此关键字类似于 `using` c # 中的关键字、 `using namespace` Visual C++ 和 `Imports` Visual Basic 中的关键字。</span><span class="sxs-lookup"><span data-stu-id="c2fea-109">This keyword is similar to the `using` keyword in C#, `using namespace` in Visual C++, and `Imports` in Visual Basic.</span></span>

<span data-ttu-id="c2fea-110">提供的模块或命名空间必须位于同一项目或引用的项目或程序集中。</span><span class="sxs-lookup"><span data-stu-id="c2fea-110">The module or namespace provided must be in the same project or in a referenced project or assembly.</span></span> <span data-ttu-id="c2fea-111">如果不是，则可以添加对项目的引用，或者使用 `-reference` 命令行选项 (或其缩写 `-r`) 。</span><span class="sxs-lookup"><span data-stu-id="c2fea-111">If it is not, you can add a reference to the project, or use the `-reference` command-line option (or its abbreviation, `-r`).</span></span> <span data-ttu-id="c2fea-112">有关详细信息，请参阅 [编译器选项](compiler-options.md)。</span><span class="sxs-lookup"><span data-stu-id="c2fea-112">For more information, see [Compiler Options](compiler-options.md).</span></span>

<span data-ttu-id="c2fea-113">导入声明会使名称位于声明后的代码中，直到封闭命名空间、模块或文件的结尾。</span><span class="sxs-lookup"><span data-stu-id="c2fea-113">The import declaration makes the names available in the code that follows the declaration, up to the end of the enclosing namespace, module, or file.</span></span>

<span data-ttu-id="c2fea-114">当使用多个导入声明时，它们应该出现在单独的行上。</span><span class="sxs-lookup"><span data-stu-id="c2fea-114">When you use multiple import declarations, they should appear on separate lines.</span></span>

<span data-ttu-id="c2fea-115">下面的代码演示 `open` 如何使用关键字来简化代码。</span><span class="sxs-lookup"><span data-stu-id="c2fea-115">The following code shows the use of the `open` keyword to simplify code.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6801.fs)]

<span data-ttu-id="c2fea-116">如果在多个打开的模块或命名空间中出现多义性，则 F # 编译器不会发出错误或警告。</span><span class="sxs-lookup"><span data-stu-id="c2fea-116">The F# compiler does not emit an error or warning when ambiguities occur when the same name occurs in more than one open module or namespace.</span></span> <span data-ttu-id="c2fea-117">出现歧义时，F # 为最近打开的模块或命名空间赋予首选项。</span><span class="sxs-lookup"><span data-stu-id="c2fea-117">When ambiguities occur, F# gives preference to the more recently opened module or namespace.</span></span> <span data-ttu-id="c2fea-118">例如，在下面的代码中， `empty` `Seq.empty` 是指，即使 `empty` 同时位于 `List` 和模块中 `Seq` 。</span><span class="sxs-lookup"><span data-stu-id="c2fea-118">For example, in the following code, `empty` means `Seq.empty`, even though `empty` is located in both the `List` and `Seq` modules.</span></span>

```fsharp
open List
open Seq
printfn "%A" empty
```

<span data-ttu-id="c2fea-119">因此，当您打开包含具有相同名称的成员的模块或命名空间（如或）时，请务必小心 `List` `Seq` ; 相反，请考虑使用限定名。</span><span class="sxs-lookup"><span data-stu-id="c2fea-119">Therefore, be careful when you open modules or namespaces such as `List` or `Seq` that contain members that have identical names; instead, consider using the qualified names.</span></span> <span data-ttu-id="c2fea-120">应避免代码依赖于导入声明顺序的任何情况。</span><span class="sxs-lookup"><span data-stu-id="c2fea-120">You should avoid any situation in which the code is dependent upon the order of the import declarations.</span></span>

## <a name="open-type-declarations"></a><span data-ttu-id="c2fea-121">开放式类型声明</span><span class="sxs-lookup"><span data-stu-id="c2fea-121">Open type declarations</span></span>

<span data-ttu-id="c2fea-122">F # 支持 `open` 类型，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c2fea-122">F# supports `open` on a type like so:</span></span>

```fsharp
open type System.Math
PI
```

<span data-ttu-id="c2fea-123">这将公开此类型上所有可访问的静态字段和成员。</span><span class="sxs-lookup"><span data-stu-id="c2fea-123">This will expose all accessible static fields and members on the type.</span></span>

<span data-ttu-id="c2fea-124">还可以通过 `open` F # 定义的 [记录](records.md) 和可 [区分的联合](discriminated-unions.md) 类型来公开静态成员。</span><span class="sxs-lookup"><span data-stu-id="c2fea-124">You can also `open` F#-defined [record](records.md) and [discriminated union](discriminated-unions.md) types to expose static members.</span></span> <span data-ttu-id="c2fea-125">对于可区分联合，还可以公开联合用例。</span><span class="sxs-lookup"><span data-stu-id="c2fea-125">In the case of discriminated unions, you can also expose the union cases.</span></span> <span data-ttu-id="c2fea-126">这对于在你可能不想打开的模块内声明的类型中访问联合用例非常有用，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c2fea-126">This can be helpful for accessing union cases in a type declared inside of a module that you may not want to open, like so:</span></span>

```fsharp
module M =
    type DU = A | B | C

    let someOtherFunction x = x + 1

// Open only the type inside the module
open type M.DU

printfn "%A" A
```

## <a name="namespaces-that-are-open-by-default"></a><span data-ttu-id="c2fea-127">默认情况下打开的命名空间</span><span class="sxs-lookup"><span data-stu-id="c2fea-127">Namespaces That Are Open by Default</span></span>

<span data-ttu-id="c2fea-128">一些命名空间非常频繁地在 F # 代码中使用，而无需显式导入声明即可隐式打开它们。</span><span class="sxs-lookup"><span data-stu-id="c2fea-128">Some namespaces are so frequently used in F# code that they are opened implicitly without the need of an explicit import declaration.</span></span> <span data-ttu-id="c2fea-129">下表显示了默认情况下处于打开状态的命名空间。</span><span class="sxs-lookup"><span data-stu-id="c2fea-129">The following table shows the namespaces that are open by default.</span></span>

|<span data-ttu-id="c2fea-130">命名空间</span><span class="sxs-lookup"><span data-stu-id="c2fea-130">Namespace</span></span>|<span data-ttu-id="c2fea-131">说明</span><span class="sxs-lookup"><span data-stu-id="c2fea-131">Description</span></span>|
|---------|-----------|
|`FSharp.Core`|<span data-ttu-id="c2fea-132">包含内置类型（例如和）的基本 F # 类型定义 `int` `float` 。</span><span class="sxs-lookup"><span data-stu-id="c2fea-132">Contains basic F# type definitions for built-in types such as `int` and `float`.</span></span>|
|`FSharp.Core.Operators`|<span data-ttu-id="c2fea-133">包含基本算术运算，例如 `+` 和 `*` 。</span><span class="sxs-lookup"><span data-stu-id="c2fea-133">Contains basic arithmetic operations such as `+` and `*`.</span></span>|
|`FSharp.Collections`|<span data-ttu-id="c2fea-134">包含不可变的集合类 `List` ，如和 `Array` 。</span><span class="sxs-lookup"><span data-stu-id="c2fea-134">Contains immutable collection classes such as `List` and `Array`.</span></span>|
|`FSharp.Control`|<span data-ttu-id="c2fea-135">包含控件构造的类型，例如迟缓计算和异步工作流。</span><span class="sxs-lookup"><span data-stu-id="c2fea-135">Contains types for control constructs such as lazy evaluation and asynchronous workflows.</span></span>|
|`FSharp.Text`|<span data-ttu-id="c2fea-136">包含格式化 IO 的函数，例如 `printf` 函数。</span><span class="sxs-lookup"><span data-stu-id="c2fea-136">Contains functions for formatted IO, such as the `printf` function.</span></span>|

## <a name="autoopen-attribute"></a><span data-ttu-id="c2fea-137">AutoOpen 特性</span><span class="sxs-lookup"><span data-stu-id="c2fea-137">AutoOpen Attribute</span></span>

<span data-ttu-id="c2fea-138">`AutoOpen`如果要在引用程序集时自动打开命名空间或模块，则可以将该特性应用于程序集。</span><span class="sxs-lookup"><span data-stu-id="c2fea-138">You can apply the `AutoOpen` attribute to an assembly if you want to automatically open a namespace or module when the assembly is referenced.</span></span> <span data-ttu-id="c2fea-139">您还可以将属性应用于 `AutoOpen` 模块，以便在打开父模块或命名空间时自动打开该模块。</span><span class="sxs-lookup"><span data-stu-id="c2fea-139">You can also apply the `AutoOpen` attribute to a module to automatically open that module when the parent module or namespace is opened.</span></span> <span data-ttu-id="c2fea-140">有关详细信息，请参阅 [AutoOpenAttribute](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-autoopenattribute.html)。</span><span class="sxs-lookup"><span data-stu-id="c2fea-140">For more information, see [AutoOpenAttribute](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-autoopenattribute.html).</span></span>

## <a name="requirequalifiedaccess-attribute"></a><span data-ttu-id="c2fea-141">RequireQualifiedAccess 特性</span><span class="sxs-lookup"><span data-stu-id="c2fea-141">RequireQualifiedAccess Attribute</span></span>

<span data-ttu-id="c2fea-142">某些模块、记录或联合类型可以指定 `RequireQualifiedAccess` 属性。</span><span class="sxs-lookup"><span data-stu-id="c2fea-142">Some modules, records, or union types may specify the `RequireQualifiedAccess` attribute.</span></span> <span data-ttu-id="c2fea-143">引用这些模块、记录或联合的元素时，必须使用限定名称，而不管是否包含导入声明。</span><span class="sxs-lookup"><span data-stu-id="c2fea-143">When you reference elements of those modules, records, or unions, you must use a qualified name regardless of whether you include an import declaration.</span></span> <span data-ttu-id="c2fea-144">如果在定义常用名称的类型上策略性地使用此属性，则有助于避免名称冲突，从而使代码更能更灵活地应对库中的更改。</span><span class="sxs-lookup"><span data-stu-id="c2fea-144">If you use this attribute strategically on types that define commonly used names, you help avoid name collisions and thereby make code more resilient to changes in libraries.</span></span> <span data-ttu-id="c2fea-145">有关详细信息，请参阅 [RequireQualifiedAccessAttribute](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-requirequalifiedaccessattribute.html)。</span><span class="sxs-lookup"><span data-stu-id="c2fea-145">For more information, see [RequireQualifiedAccessAttribute](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-requirequalifiedaccessattribute.html).</span></span>

## <a name="see-also"></a><span data-ttu-id="c2fea-146">另请参阅</span><span class="sxs-lookup"><span data-stu-id="c2fea-146">See also</span></span>

- [<span data-ttu-id="c2fea-147">F# 语言参考</span><span class="sxs-lookup"><span data-stu-id="c2fea-147">F# Language Reference</span></span>](index.md)
- [<span data-ttu-id="c2fea-148">命名空间</span><span class="sxs-lookup"><span data-stu-id="c2fea-148">Namespaces</span></span>](namespaces.md)
- [<span data-ttu-id="c2fea-149">模块</span><span class="sxs-lookup"><span data-stu-id="c2fea-149">Modules</span></span>](modules.md)
