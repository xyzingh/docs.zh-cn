---
title: 切片
description: '了解如何使用现有 F # 数据类型的切片，以及如何为其他数据类型定义自己的切片。'
ms.date: 12/23/2019
ms.openlocfilehash: a3920ad9e1b205b506aaee92c4606bcebf94feba
ms.sourcegitcommit: f99115e12a5eb75638abe45072e023a3ce3351ac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2020
ms.locfileid: "94557072"
---
# <a name="slices"></a><span data-ttu-id="523d6-103">切片</span><span class="sxs-lookup"><span data-stu-id="523d6-103">Slices</span></span>

<span data-ttu-id="523d6-104">在 F # 中，切片是 `GetSlice` 在其定义或范围内 [类型扩展](type-extensions.md)中具有方法的任何数据类型的子集。</span><span class="sxs-lookup"><span data-stu-id="523d6-104">In F#, a slice is a subset of any data type that has a `GetSlice` method in its definition or in an in-scope [type extension](type-extensions.md).</span></span> <span data-ttu-id="523d6-105">它最常用于 F # 数组和列表。</span><span class="sxs-lookup"><span data-stu-id="523d6-105">It is most commonly used with F# arrays and lists.</span></span> <span data-ttu-id="523d6-106">本文介绍如何从现有的 F # 类型中获取切片，以及如何定义自己的切片。</span><span class="sxs-lookup"><span data-stu-id="523d6-106">This article explains how to take slices from existing F# types and how to define your own slices.</span></span>

<span data-ttu-id="523d6-107">切片与 [索引器](./members/indexed-properties.md)相似，但它不是从基础数据结构产生单个值，而是生成多个值。</span><span class="sxs-lookup"><span data-stu-id="523d6-107">Slices are similar to [indexers](./members/indexed-properties.md), but instead of yielding a single value from the underlying data structure, they yield multiple ones.</span></span>

<span data-ttu-id="523d6-108">F # 目前对切片字符串、列表、数组和二维数组具有内部支持。</span><span class="sxs-lookup"><span data-stu-id="523d6-108">F# currently has intrinsic support for slicing strings, lists, arrays, and 2D arrays.</span></span>

## <a name="basic-slicing-with-f-lists-and-arrays"></a><span data-ttu-id="523d6-109">带有 F # 列表和数组的基本切片</span><span class="sxs-lookup"><span data-stu-id="523d6-109">Basic slicing with F# lists and arrays</span></span>

<span data-ttu-id="523d6-110">切片最常见的数据类型是 F # 列表和数组。</span><span class="sxs-lookup"><span data-stu-id="523d6-110">The most common data types that are sliced are F# lists and arrays.</span></span> <span data-ttu-id="523d6-111">下面的示例演示如何通过列表执行此操作：</span><span class="sxs-lookup"><span data-stu-id="523d6-111">The following example demonstrates how to do this with lists:</span></span>

```fsharp
// Generate a list of 100 integers
let fullList = [ 1 .. 100 ]

// Create a slice from indices 1-5 (inclusive)
let smallSlice = fullList.[1..5]
printfn "Small slice: %A" smallSlice

// Create a slice from the beginning to index 5 (inclusive)
let unboundedBeginning = fullList.[..5]
printfn "Unbounded beginning slice: %A" unboundedBeginning

// Create a slice from an index to the end of the list
let unboundedEnd = fullList.[94..]
printfn "Unbounded end slice: %A" unboundedEnd
```

<span data-ttu-id="523d6-112">切片数组与切片列表类似：</span><span class="sxs-lookup"><span data-stu-id="523d6-112">Slicing arrays is just like slicing lists:</span></span>

```fsharp
// Generate an array of 100 integers
let fullArray = [| 1 .. 100 |]

// Create a slice from indices 1-5 (inclusive)
let smallSlice = fullArray.[1..5]
printfn "Small slice: %A" smallSlice

// Create a slice from the beginning to index 5 (inclusive)
let unboundedBeginning = fullArray.[..5]
printfn "Unbounded beginning slice: %A" unboundedBeginning

// Create a slice from an index to the end of the list
let unboundedEnd = fullArray.[94..]
printfn "Unbounded end slice: %A" unboundedEnd
```

## <a name="slicing-multidimensional-arrays"></a><span data-ttu-id="523d6-113">切片多维数组</span><span class="sxs-lookup"><span data-stu-id="523d6-113">Slicing multidimensional arrays</span></span>

<span data-ttu-id="523d6-114">F # 支持 F # 核心库中的多维数组。</span><span class="sxs-lookup"><span data-stu-id="523d6-114">F# supports multidimensional arrays in the F# core library.</span></span> <span data-ttu-id="523d6-115">与一维数组一样，多维数组的切片也很有用。</span><span class="sxs-lookup"><span data-stu-id="523d6-115">As with one-dimensional arrays, slices of multidimensional arrays can also be useful.</span></span> <span data-ttu-id="523d6-116">但是，附加维度的引入要求使用略微不同的语法，以便能够获取特定行和列的切片。</span><span class="sxs-lookup"><span data-stu-id="523d6-116">However, the introduction of additional dimensions mandates a slightly different syntax so that you can take slices of specific rows and columns.</span></span>

<span data-ttu-id="523d6-117">下面的示例演示如何切分二维数组：</span><span class="sxs-lookup"><span data-stu-id="523d6-117">The following examples demonstrate how to slice a 2D array:</span></span>

```fsharp
// Generate a 3x3 2D matrix
let A = array2D [[1;2;3];[4;5;6];[7;8;9]]
printfn "Full matrix:\n %A" A

// Take the first row
let row0 = A.[0,*]
printfn "Row 0: %A" row0

// Take the first column
let col0 = A.[*,0]
printfn "Column 0: %A" col0

// Take all rows but only two columns
let subA = A.[*,0..1]
printfn "%A" subA

// Take two rows and all columns
let subA' = A.[0..1,*]
printfn "%A" subA'

// Slice a 2x2 matrix out of the full 3x3 matrix
let twoByTwo = A.[0..1,0..1]
printfn "%A" twoByTwo
```

<span data-ttu-id="523d6-118">F # core 库当前没有 `GetSlice` 为三维数组定义。</span><span class="sxs-lookup"><span data-stu-id="523d6-118">The F# core library does not currently define `GetSlice` for 3D arrays.</span></span> <span data-ttu-id="523d6-119">如果要对三维数组或其他维度的其他数组进行切片，请 `GetSlice` 自行定义成员。</span><span class="sxs-lookup"><span data-stu-id="523d6-119">If you wish to slice 3D arrays or other arrays of more dimensions, define the `GetSlice` member yourself.</span></span>

## <a name="defining-slices-for-other-data-structures"></a><span data-ttu-id="523d6-120">为其他数据结构定义切片</span><span class="sxs-lookup"><span data-stu-id="523d6-120">Defining slices for other data structures</span></span>

<span data-ttu-id="523d6-121">F # 核心库定义了有限类型集的切片。</span><span class="sxs-lookup"><span data-stu-id="523d6-121">The F# core library defines slices for a limited set of types.</span></span> <span data-ttu-id="523d6-122">如果要定义更多数据类型的切片，可以在类型定义本身或类型扩展中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="523d6-122">If you wish to define slices for more data types, you can do so either in the type definition itself or in a type extension.</span></span>

<span data-ttu-id="523d6-123">例如，下面介绍了如何为类定义切片， <xref:System.ArraySegment%601> 以方便进行数据操作：</span><span class="sxs-lookup"><span data-stu-id="523d6-123">For example, here's how you might define slices for the <xref:System.ArraySegment%601> class to allow for convenient data manipulation:</span></span>

```fsharp
open System

type ArraySegment<'TItem> with
    member segment.GetSlice(start, finish) =
        let start = defaultArg start 0
        let finish = defaultArg finish segment.Count
        ArraySegment(segment.Array, segment.Offset + start, finish - start)

let arr = ArraySegment [| 1 .. 10 |]
let slice = arr.[2..5] //[ 3; 4; 5]
```

<span data-ttu-id="523d6-124">使用和类型的另一个示例 <xref:System.Span%601> <xref:System.ReadOnlySpan%601> ：</span><span class="sxs-lookup"><span data-stu-id="523d6-124">Another example using the <xref:System.Span%601> and <xref:System.ReadOnlySpan%601> types:</span></span>

```fsharp
open System

type ReadOnlySpan<'T> with
    member sp.GetSlice(startIdx, endIdx) =
        let s = defaultArg startIdx 0
        let e = defaultArg endIdx sp.Length
        sp.Slice(s, e - s)

type Span<'T> with
    member sp.GetSlice(startIdx, endIdx) =
        let s = defaultArg startIdx 0
        let e = defaultArg endIdx sp.Length
        sp.Slice(s, e - s)

let printSpan (sp: Span<int>) =
    let arr = sp.ToArray()
    printfn "%A" arr

let sp = [| 1; 2; 3; 4; 5 |].AsSpan()
printSpan sp.[0..] // [|1; 2; 3; 4; 5|]
printSpan sp.[..5] // [|1; 2; 3; 4; 5|]
printSpan sp.[0..3] // [|1; 2; 3|]
printSpan sp.[1..3] // |2; 3|]
```

## <a name="built-in-f-slices-are-end-inclusive"></a><span data-ttu-id="523d6-125">内置 F # 切片包含结尾</span><span class="sxs-lookup"><span data-stu-id="523d6-125">Built-in F# slices are end-inclusive</span></span>

<span data-ttu-id="523d6-126">F # 中的所有内部切片都是结尾的;也就是说，切片中包括上限。</span><span class="sxs-lookup"><span data-stu-id="523d6-126">All intrinsic slices in F# are end-inclusive; that is, the upper bound is included in the slice.</span></span> <span data-ttu-id="523d6-127">对于具有起始索引 `x` 和结束索引的给定切片 `y` ，生成的切片将包含 *yth* 值。</span><span class="sxs-lookup"><span data-stu-id="523d6-127">For a given slice with starting index `x` and ending index `y`, the resulting slice will include the *yth* value.</span></span>

```fsharp
// Define a new list
let xs = [1 .. 10]

printfn "%A" xs.[2..5] // Includes the 5th index
```

## <a name="built-in-f-empty-slices"></a><span data-ttu-id="523d6-128">内置 F # 空切片</span><span class="sxs-lookup"><span data-stu-id="523d6-128">Built-in F# empty slices</span></span>

<span data-ttu-id="523d6-129">如果语法可能生成不存在的切片，则 F # 列表、数组、序列、字符串、二维数组、3D 数组和4D 数组将生成一个空切片。</span><span class="sxs-lookup"><span data-stu-id="523d6-129">F# lists, arrays, sequences, strings, 2D arrays, 3D arrays, and 4D arrays will all produce an empty slice if the syntax could produce a slice that doesn't exist.</span></span>

<span data-ttu-id="523d6-130">考虑以下情况：</span><span class="sxs-lookup"><span data-stu-id="523d6-130">Consider the following:</span></span>

```fsharp
let l = [ 1..10 ]
let a = [| 1..10 |]
let s = "hello!"

let emptyList = l.[-2..(-1)]
let emptyArray = a.[-2..(-1)]
let emptyString = s.[-2..(-1)]
```

<span data-ttu-id="523d6-131">C # 开发人员可能希望它们引发异常，而不是生成空切片。</span><span class="sxs-lookup"><span data-stu-id="523d6-131">C# developers may expect these to throw an exception rather than produce an empty slice.</span></span> <span data-ttu-id="523d6-132">这是一个以 F # 编写的空集合为基础的设计决策。</span><span class="sxs-lookup"><span data-stu-id="523d6-132">This is a design decision rooted in the fact that empty collections compose in F#.</span></span> <span data-ttu-id="523d6-133">空 F # 列表可以用另一个 F # 列表撰写，空字符串可添加到现有字符串，等等。</span><span class="sxs-lookup"><span data-stu-id="523d6-133">An empty F# list can be composed with another F# list, an empty string can be added to an existing string, and so on.</span></span> <span data-ttu-id="523d6-134">基于作为参数传入的值拍摄切片很常见，并且通过生成一个空集合（与 F # 代码的复合特性相匹配），可以更容错。</span><span class="sxs-lookup"><span data-stu-id="523d6-134">It can be common to take slices based on values passed in as parameters, and being tolerant of out-of-bounds by producing an empty collection fits with the compositional nature of F# code.</span></span>

## <a name="fixed-index-slices-for-3d-and-4d-arrays"></a><span data-ttu-id="523d6-135">用于3D 和4D 数组的固定索引切片</span><span class="sxs-lookup"><span data-stu-id="523d6-135">Fixed-index slices for 3D and 4D arrays</span></span>

<span data-ttu-id="523d6-136">对于 F # 3D 和4D 数组，可以 "修复" 特定索引，并切分已修复索引的其他维度。</span><span class="sxs-lookup"><span data-stu-id="523d6-136">For F# 3D and 4D arrays, you can "fix" a particular index and slice other dimensions with that index fixed.</span></span>

<span data-ttu-id="523d6-137">为了说明这一点，请考虑下面的三维数组：</span><span class="sxs-lookup"><span data-stu-id="523d6-137">To illustrate this, consider the following 3D array:</span></span>

<span data-ttu-id="523d6-138">*z = 0*</span><span class="sxs-lookup"><span data-stu-id="523d6-138">*z = 0*</span></span>
| <span data-ttu-id="523d6-139">x\y</span><span class="sxs-lookup"><span data-stu-id="523d6-139">x\y</span></span>   | <span data-ttu-id="523d6-140">0</span><span class="sxs-lookup"><span data-stu-id="523d6-140">0</span></span> | <span data-ttu-id="523d6-141">1</span><span class="sxs-lookup"><span data-stu-id="523d6-141">1</span></span> |
|-------|---|---|
| <span data-ttu-id="523d6-142">**0**</span><span class="sxs-lookup"><span data-stu-id="523d6-142">**0**</span></span> | <span data-ttu-id="523d6-143">0</span><span class="sxs-lookup"><span data-stu-id="523d6-143">0</span></span> | <span data-ttu-id="523d6-144">1</span><span class="sxs-lookup"><span data-stu-id="523d6-144">1</span></span> |
| <span data-ttu-id="523d6-145">**1**</span><span class="sxs-lookup"><span data-stu-id="523d6-145">**1**</span></span> | <span data-ttu-id="523d6-146">2</span><span class="sxs-lookup"><span data-stu-id="523d6-146">2</span></span> | <span data-ttu-id="523d6-147">3</span><span class="sxs-lookup"><span data-stu-id="523d6-147">3</span></span> |

<span data-ttu-id="523d6-148">*z = 1*</span><span class="sxs-lookup"><span data-stu-id="523d6-148">*z = 1*</span></span>
| <span data-ttu-id="523d6-149">x\y</span><span class="sxs-lookup"><span data-stu-id="523d6-149">x\y</span></span>   | <span data-ttu-id="523d6-150">0</span><span class="sxs-lookup"><span data-stu-id="523d6-150">0</span></span> | <span data-ttu-id="523d6-151">1</span><span class="sxs-lookup"><span data-stu-id="523d6-151">1</span></span> |
|-------|---|---|
| <span data-ttu-id="523d6-152">**0**</span><span class="sxs-lookup"><span data-stu-id="523d6-152">**0**</span></span> | <span data-ttu-id="523d6-153">4</span><span class="sxs-lookup"><span data-stu-id="523d6-153">4</span></span> | <span data-ttu-id="523d6-154">5</span><span class="sxs-lookup"><span data-stu-id="523d6-154">5</span></span> |
| <span data-ttu-id="523d6-155">**1**</span><span class="sxs-lookup"><span data-stu-id="523d6-155">**1**</span></span> | <span data-ttu-id="523d6-156">6</span><span class="sxs-lookup"><span data-stu-id="523d6-156">6</span></span> | <span data-ttu-id="523d6-157">7</span><span class="sxs-lookup"><span data-stu-id="523d6-157">7</span></span> |

<span data-ttu-id="523d6-158">如果要 `[| 4; 5 |]` 从数组中提取切片，请使用固定索引切片。</span><span class="sxs-lookup"><span data-stu-id="523d6-158">If you want to extract the slice `[| 4; 5 |]` from the array, use a fixed-index slice.</span></span>

```fsharp
let dim = 2
let m = Array3D.zeroCreate<int> dim dim dim

let mutable count = 0

for z in 0..dim-1 do
    for y in 0..dim-1 do
        for x in 0..dim-1 do
            m.[x,y,z] <- count
            count <- count + 1

// Now let's get the [4;5] slice!
m.[*, 0, 1]
```

<span data-ttu-id="523d6-159">最后一行修复了 `y` `z` 三维数组的和索引，并采用了对应于矩阵的其余 `x` 值。</span><span class="sxs-lookup"><span data-stu-id="523d6-159">The last line fixes the `y` and `z` indicies of the 3D array and takes the rest of the `x` values that correspond to the matrix.</span></span>

## <a name="see-also"></a><span data-ttu-id="523d6-160">请参阅</span><span class="sxs-lookup"><span data-stu-id="523d6-160">See also</span></span>

- [<span data-ttu-id="523d6-161">索引属性</span><span class="sxs-lookup"><span data-stu-id="523d6-161">Indexed properties</span></span>](./members/indexed-properties.md)
