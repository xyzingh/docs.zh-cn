---
title: 'F # 5.0 中的新增功能-F # 指南'
description: '获取 F # 5.0 中提供的新功能的概述。'
ms.date: 11/06/2020
ms.openlocfilehash: 51d6dd2457ee9966a86d0d9ac686f2af15772999
ms.sourcegitcommit: f99115e12a5eb75638abe45072e023a3ce3351ac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2020
ms.locfileid: "94557137"
---
# <a name="whats-new-in-f-50"></a><span data-ttu-id="14455-103">F# 5.0 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="14455-103">What's new in F# 5.0</span></span>

<span data-ttu-id="14455-104">F # 5.0 向 F # 语言和 F# 交互窗口增加了几项改进。</span><span class="sxs-lookup"><span data-stu-id="14455-104">F# 5.0 adds several improvements to the F# language and F# Interactive.</span></span> <span data-ttu-id="14455-105">它随 **.net 5** 一起发布。</span><span class="sxs-lookup"><span data-stu-id="14455-105">It is released with **.NET 5**.</span></span>

<span data-ttu-id="14455-106">可以从 [.net 下载页](https://dotnet.microsoft.com/download)下载最新的 .net SDK。</span><span class="sxs-lookup"><span data-stu-id="14455-106">You can download the latest .NET SDK from the [.NET downloads page](https://dotnet.microsoft.com/download).</span></span>

## <a name="get-started"></a><span data-ttu-id="14455-107">入门</span><span class="sxs-lookup"><span data-stu-id="14455-107">Get started</span></span>

<span data-ttu-id="14455-108">F # 5.0 适用于所有 .NET Core 分发版和 Visual Studio 工具。</span><span class="sxs-lookup"><span data-stu-id="14455-108">F# 5.0 is available in all .NET Core distributions and Visual Studio tooling.</span></span> <span data-ttu-id="14455-109">有关详细信息，请参阅 [F # 入门](../get-started/index.md) 以了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="14455-109">For more information, see [Get started with F#](../get-started/index.md) to learn more.</span></span>

## <a name="package-references-in-f-scripts"></a><span data-ttu-id="14455-110">F # 脚本中的包引用</span><span class="sxs-lookup"><span data-stu-id="14455-110">Package references in F# scripts</span></span>

<span data-ttu-id="14455-111">F # 5 通过语法为 F # 脚本中的包引用提供支持 `#r "nuget:..."` 。</span><span class="sxs-lookup"><span data-stu-id="14455-111">F# 5 brings support for package references in F# scripts with `#r "nuget:..."` syntax.</span></span> <span data-ttu-id="14455-112">例如，请考虑下面的包引用：</span><span class="sxs-lookup"><span data-stu-id="14455-112">For example, consider the following package reference:</span></span>

```fsharp
#r "nuget: Newtonsoft.Json"

open Newtonsoft.Json

let o = {| X = 2; Y = "Hello" |}

printfn "%s" (JsonConvert.SerializeObject o)
```

<span data-ttu-id="14455-113">你还可以在包名称后提供显式版本，如下所示：</span><span class="sxs-lookup"><span data-stu-id="14455-113">You can also supply an explicit version after the name of the package like this:</span></span>

```fsharp
#r "nuget: Newtonsoft.Json,11.0.1"
```

<span data-ttu-id="14455-114">包引用支持具有本机依赖项的包，如 ML.NET。</span><span class="sxs-lookup"><span data-stu-id="14455-114">Package references support packages with native dependencies, such as ML.NET.</span></span>

<span data-ttu-id="14455-115">包引用还支持具有有关引用依赖项的特殊要求的包 `.dll` 。</span><span class="sxs-lookup"><span data-stu-id="14455-115">Package references also support packages with special requirements about referencing dependent `.dll`s.</span></span> <span data-ttu-id="14455-116">例如， [FParsec](https://www.nuget.org/packages/FParsec/) 包，用于要求用户 `FParsecCS.dll` 在 F# 交互窗口引用之前手动确保引用其依赖项 `FParsec.dll` 。</span><span class="sxs-lookup"><span data-stu-id="14455-116">For example, the [FParsec](https://www.nuget.org/packages/FParsec/) package used to require that users manually ensure that its dependent `FParsecCS.dll` was referenced first before `FParsec.dll` was referenced in F# Interactive.</span></span> <span data-ttu-id="14455-117">不再需要此操作，你可以引用包，如下所示：</span><span class="sxs-lookup"><span data-stu-id="14455-117">This is no longer needed, and you can reference the package as follows:</span></span>

```fsharp
#r "nuget: FParsec"

open FParsec

let test p str =
    match run p str with
    | Success(result, _, _)   -> printfn "Success: %A" result
    | Failure(errorMsg, _, _) -> printfn "Failure: %s" errorMsg

test pfloat "1.234"
```

<span data-ttu-id="14455-118">有关包引用的详细信息，请参阅 [F# 交互窗口](../tutorials/fsharp-interactive/index.md) 教程。</span><span class="sxs-lookup"><span data-stu-id="14455-118">For more information on package references, see the [F# Interactive](../tutorials/fsharp-interactive/index.md) tutorial.</span></span>

## <a name="string-interpolation"></a><span data-ttu-id="14455-119">字符串内插</span><span class="sxs-lookup"><span data-stu-id="14455-119">String interpolation</span></span>

<span data-ttu-id="14455-120">F # 内插字符串非常类似于 c # 或 JavaScript 内插字符串，因为它们允许您在字符串文字中的 "洞" 中编写代码。</span><span class="sxs-lookup"><span data-stu-id="14455-120">F# interpolated strings are fairly similar to C# or JavaScript interpolated strings, in that they let you write code in "holes" inside of a string literal.</span></span> <span data-ttu-id="14455-121">下面是一个基本示例：</span><span class="sxs-lookup"><span data-stu-id="14455-121">Here's a basic example:</span></span>

```fsharp
let name = "Phillip"
let age = 29
printfn $"Name: {name}, Age: {age}"

printfn $"I think {3.0 + 0.14} is close to {System.Math.PI}!"
```

<span data-ttu-id="14455-122">但是，F # 内插字符串也允许类型化的内插，就像 `sprintf` 函数一样，强制插入上下文内的表达式符合特定类型。</span><span class="sxs-lookup"><span data-stu-id="14455-122">However, F# interpolated strings also allow for typed interpolations, just like the `sprintf` function, to enforce that an expression inside of an interpolated context conforms to a particular type.</span></span> <span data-ttu-id="14455-123">它使用相同的格式说明符。</span><span class="sxs-lookup"><span data-stu-id="14455-123">It uses the same format specifiers.</span></span>

```fsharp
let name = "Phillip"
let age = 29

printfn $"Name: %s{name}, Age: %d{age}"

// Error: type mismatch
printfn $"Name: %s{age}, Age: %d{name}"
```

<span data-ttu-id="14455-124">在前面的类型化内插示例中， `%s` 要求内插为类型 `string` ，而 `%d` 需要将内插成为 `integer` 。</span><span class="sxs-lookup"><span data-stu-id="14455-124">In the preceding typed interpolation example, the `%s` requires the interpolation to be of type `string`, whereas the `%d` requires the interpolation to be an `integer`.</span></span>

<span data-ttu-id="14455-125">此外，任何 (或表达式) 任意 F # 表达式都可以置于内插上下文的一边。</span><span class="sxs-lookup"><span data-stu-id="14455-125">Additionally, any arbitrary F# expression (or expressions) can be placed in side of an interpolation context.</span></span> <span data-ttu-id="14455-126">甚至可以编写更复杂的表达式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="14455-126">It is even possible to write a more complicated expression, like so:</span></span>

```fsharp
let str =
    $"""The result of squaring each odd item in {[1..10]} is:
{
    let square x = x * x
    let isOdd x = x % 2 <> 0
    let oddSquares xs =
        xs
        |> List.filter isOdd
        |> List.map square
    oddSquares [1..10]
}
"""
```

<span data-ttu-id="14455-127">尽管我们不建议在实践中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="14455-127">Although we don't recommend doing this too much in practice.</span></span>

## <a name="support-for-nameof"></a><span data-ttu-id="14455-128">对 nameof 的支持</span><span class="sxs-lookup"><span data-stu-id="14455-128">Support for nameof</span></span>

<span data-ttu-id="14455-129">F # 5 支持 `nameof` 运算符，该运算符解析其正用于的符号，并在 F # 源中生成其名称。</span><span class="sxs-lookup"><span data-stu-id="14455-129">F# 5 supports the `nameof` operator, which resolves the symbol it's being used for and produces its name in F# source.</span></span> <span data-ttu-id="14455-130">这在各种情况下非常有用，例如日志记录，并可防止日志记录在源代码中发生更改。</span><span class="sxs-lookup"><span data-stu-id="14455-130">This is useful in various scenarios, such as logging, and protects your logging against changes in source code.</span></span>

```fsharp
let months =
    [
        "January"; "February"; "March"; "April";
        "May"; "June"; "July"; "August"; "September";
        "October"; "November"; "December"
    ]

let lookupMonth month =
    if (month > 12 || month < 1) then
        invalidArg (nameof month) (sprintf "Value passed in was %d." month)

    months.[month-1]

printfn "%s" (lookupMonth 12)
printfn "%s" (lookupMonth 1)
printfn "%s" (lookupMonth 13)
```

<span data-ttu-id="14455-131">最后一行将引发异常，并且错误消息中将显示 "month"。</span><span class="sxs-lookup"><span data-stu-id="14455-131">The last line will throw an exception and "month" will be shown in the error message.</span></span>

<span data-ttu-id="14455-132">你可以创建几乎每个 F # 构造的名称：</span><span class="sxs-lookup"><span data-stu-id="14455-132">You can take a name of nearly every F# construct:</span></span>

```fsharp
module M =
    let f x = nameof x

printfn "%s" (M.f 12)
printfn "%s" (nameof M)
printfn "%s" (nameof M.f)
```

<span data-ttu-id="14455-133">三个最终添加操作对运算符的工作方式进行了更改：添加了 `nameof<'type-parameter>` 泛型类型参数的窗体，以及在 `nameof` 模式匹配表达式中用作模式的功能。</span><span class="sxs-lookup"><span data-stu-id="14455-133">Three final additions are changes to how operators work: the addition of the `nameof<'type-parameter>` form for generic type parameters, and the ability to use `nameof` as a pattern in a pattern match expression.</span></span>

<span data-ttu-id="14455-134">采用运算符的名称将提供其源字符串。</span><span class="sxs-lookup"><span data-stu-id="14455-134">Taking a name of an operator gives its source string.</span></span> <span data-ttu-id="14455-135">如果需要编译的窗体，请使用运算符的编译名称：</span><span class="sxs-lookup"><span data-stu-id="14455-135">If you need the compiled form, use the compiled name of an operator:</span></span>

```fsharp
nameof(+) // "+"
nameof op_Addition // "op_Addition"
```

<span data-ttu-id="14455-136">采用类型参数的名称需要略有不同的语法：</span><span class="sxs-lookup"><span data-stu-id="14455-136">Taking the name of a type parameter requires a slightly different syntax:</span></span>

```fsharp
type C<'TType> =
    member _.TypeName = nameof<'TType>
```

<span data-ttu-id="14455-137">这类似于 `typeof<'T>` 和 `typedefof<'T>` 运算符。</span><span class="sxs-lookup"><span data-stu-id="14455-137">This is similar to the `typeof<'T>` and `typedefof<'T>` operators.</span></span>

<span data-ttu-id="14455-138">F # 5 还添加了对 `nameof` 可在表达式中使用的模式的支持 `match` ：</span><span class="sxs-lookup"><span data-stu-id="14455-138">F# 5 also adds support for a `nameof` pattern that can be used in `match` expressions:</span></span>

```fsharp
[<Struct; IsByRefLike>]
type RecordedEvent = { EventType: string; Data: ReadOnlySpan<byte> }

type MyEvent =
    | AData of int
    | BData of string

let deserialize (e: RecordedEvent) : MyEvent =
    match e.EventType with
    | nameof AData -> AData (JsonSerializer.Deserialize<int> e.Data)
    | nameof BData -> BData (JsonSerializer.Deserialize<string> e.Data)
    | t -> failwithf "Invalid EventType: %s" t
```

<span data-ttu-id="14455-139">前面的代码使用 "nameof" 而不是 match 表达式中的字符串文字。</span><span class="sxs-lookup"><span data-stu-id="14455-139">The preceding code uses 'nameof' instead of the string literal in the match expression.</span></span>

## <a name="open-type-declarations"></a><span data-ttu-id="14455-140">开放式类型声明</span><span class="sxs-lookup"><span data-stu-id="14455-140">Open type declarations</span></span>

<span data-ttu-id="14455-141">F # 5 还添加了对开放类型声明的支持。</span><span class="sxs-lookup"><span data-stu-id="14455-141">F# 5 also adds support for open type declarations.</span></span> <span data-ttu-id="14455-142">开放式类型声明类似于打开 c # 中的静态类，但有一些不同的语法和一些略有不同的行为，以适合 F # 语义。</span><span class="sxs-lookup"><span data-stu-id="14455-142">An open type declaration is like opening a static class in C#, except with some different syntax and some slightly different behavior to fit F# semantics.</span></span>

<span data-ttu-id="14455-143">利用开放类型声明，你可以在 `open` 任何类型中公开其静态内容。</span><span class="sxs-lookup"><span data-stu-id="14455-143">With open type declarations, you can `open` any type to expose static contents inside of it.</span></span> <span data-ttu-id="14455-144">此外，还可以通过 `open` F # 定义的联合和记录来公开其内容。</span><span class="sxs-lookup"><span data-stu-id="14455-144">Additionally, you can `open` F#-defined unions and records to expose their contents.</span></span> <span data-ttu-id="14455-145">例如，如果在模块中定义了联合并想要访问其事例，但又不希望打开整个模块，则这会很有用。</span><span class="sxs-lookup"><span data-stu-id="14455-145">For example, this can be useful if you have a union defined in a module and want to access its cases, but don't want to open the entire module.</span></span>

```fsharp
open type System.Math

let x = Min(1.0, 2.0)

module M =
    type DU = A | B | C

    let someOtherFunction x = x + 1

// Open only the type inside the module
open type M.DU

printfn "%A" A
```

<span data-ttu-id="14455-146">与 c # 不同，当你 `open type` 在两个公开同名成员的类型上时，最后一个类型中的成员将 `open` 隐藏另一个名称。</span><span class="sxs-lookup"><span data-stu-id="14455-146">Unlike C#, when you `open type` on two types that expose a member with the same name, the member from the last type being `open`ed shadows the other name.</span></span> <span data-ttu-id="14455-147">这与围绕已存在的隐藏的 F # 语义一致。</span><span class="sxs-lookup"><span data-stu-id="14455-147">This is consistent with F# semantics around shadowing that exist already.</span></span>

## <a name="consistent-slicing-behavior-for-built-in-data-types"></a><span data-ttu-id="14455-148">内置数据类型的一致切片行为</span><span class="sxs-lookup"><span data-stu-id="14455-148">Consistent slicing behavior for built-in data types</span></span>

<span data-ttu-id="14455-149">用于切分内置数据类型的行为， `FSharp.Core` (数组、列表、string、二维数组、三维数组、4d 数组) 在 F # 5 之前用于不一致。</span><span class="sxs-lookup"><span data-stu-id="14455-149">Behavior for slicing the built-in `FSharp.Core` data types (array, list, string, 2D array, 3D array, 4D array) used to not be consistent prior to F# 5.</span></span> <span data-ttu-id="14455-150">有些边缘情况行为引发了异常，有些则是。</span><span class="sxs-lookup"><span data-stu-id="14455-150">Some edge-case behavior threw an exception and some wouldn't.</span></span> <span data-ttu-id="14455-151">在 F # 5 中，所有内置类型现在为无法生成的切片返回空切片：</span><span class="sxs-lookup"><span data-stu-id="14455-151">In F# 5, all built-in types now return empty slices for slices that are impossible to generate:</span></span>

```fsharp
let l = [ 1..10 ]
let a = [| 1..10 |]
let s = "hello!"

// Before: would return empty list
// F# 5: same
let emptyList = l.[-2..(-1)]

// Before: would throw exception
// F# 5: returns empty array
let emptyArray = a.[-2..(-1)]

// Before: would throw exception
// F# 5: returns empty string
let emptyString = s.[-2..(-1)]
```

## <a name="fixed-index-slices-for-3d-and-4d-arrays-in-fsharpcore"></a><span data-ttu-id="14455-152">为 Fsharp.core 中的3D 和4D 阵列固定索引切片</span><span class="sxs-lookup"><span data-stu-id="14455-152">Fixed-index slices for 3D and 4D arrays in FSharp.Core</span></span>

<span data-ttu-id="14455-153">F # 5.0 为内置3D 和4D 数组类型中具有固定索引的切片提供支持。</span><span class="sxs-lookup"><span data-stu-id="14455-153">F# 5.0 brings support for slicing with a fixed index in the built-in 3D and 4D array types.</span></span>

<span data-ttu-id="14455-154">为了说明这一点，请考虑下面的三维数组：</span><span class="sxs-lookup"><span data-stu-id="14455-154">To illustrate this, consider the following 3D array:</span></span>

<span data-ttu-id="14455-155">*z = 0*</span><span class="sxs-lookup"><span data-stu-id="14455-155">*z = 0*</span></span>
| <span data-ttu-id="14455-156">x\y</span><span class="sxs-lookup"><span data-stu-id="14455-156">x\y</span></span>   | <span data-ttu-id="14455-157">0</span><span class="sxs-lookup"><span data-stu-id="14455-157">0</span></span> | <span data-ttu-id="14455-158">1</span><span class="sxs-lookup"><span data-stu-id="14455-158">1</span></span> |
|-------|---|---|
| <span data-ttu-id="14455-159">**0**</span><span class="sxs-lookup"><span data-stu-id="14455-159">**0**</span></span> | <span data-ttu-id="14455-160">0</span><span class="sxs-lookup"><span data-stu-id="14455-160">0</span></span> | <span data-ttu-id="14455-161">1</span><span class="sxs-lookup"><span data-stu-id="14455-161">1</span></span> |
| <span data-ttu-id="14455-162">**1**</span><span class="sxs-lookup"><span data-stu-id="14455-162">**1**</span></span> | <span data-ttu-id="14455-163">2</span><span class="sxs-lookup"><span data-stu-id="14455-163">2</span></span> | <span data-ttu-id="14455-164">3</span><span class="sxs-lookup"><span data-stu-id="14455-164">3</span></span> |

<span data-ttu-id="14455-165">*z = 1*</span><span class="sxs-lookup"><span data-stu-id="14455-165">*z = 1*</span></span>
| <span data-ttu-id="14455-166">x\y</span><span class="sxs-lookup"><span data-stu-id="14455-166">x\y</span></span>   | <span data-ttu-id="14455-167">0</span><span class="sxs-lookup"><span data-stu-id="14455-167">0</span></span> | <span data-ttu-id="14455-168">1</span><span class="sxs-lookup"><span data-stu-id="14455-168">1</span></span> |
|-------|---|---|
| <span data-ttu-id="14455-169">**0**</span><span class="sxs-lookup"><span data-stu-id="14455-169">**0**</span></span> | <span data-ttu-id="14455-170">4</span><span class="sxs-lookup"><span data-stu-id="14455-170">4</span></span> | <span data-ttu-id="14455-171">5</span><span class="sxs-lookup"><span data-stu-id="14455-171">5</span></span> |
| <span data-ttu-id="14455-172">**1**</span><span class="sxs-lookup"><span data-stu-id="14455-172">**1**</span></span> | <span data-ttu-id="14455-173">6</span><span class="sxs-lookup"><span data-stu-id="14455-173">6</span></span> | <span data-ttu-id="14455-174">7</span><span class="sxs-lookup"><span data-stu-id="14455-174">7</span></span> |

<span data-ttu-id="14455-175">如果要从数组中提取切片，该怎么办 `[| 4; 5 |]` ？</span><span class="sxs-lookup"><span data-stu-id="14455-175">What if you wanted to extract the slice `[| 4; 5 |]` from the array?</span></span> <span data-ttu-id="14455-176">这现在非常简单！</span><span class="sxs-lookup"><span data-stu-id="14455-176">This is now very simple!</span></span>

```fsharp
// First, create a 3D array to slice

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

## <a name="f-quotations-improvements"></a><span data-ttu-id="14455-177">F # 报价改进</span><span class="sxs-lookup"><span data-stu-id="14455-177">F# quotations improvements</span></span>

<span data-ttu-id="14455-178">F # [代码引用](../language-reference/code-quotations.md) 现在能够保留类型约束信息。</span><span class="sxs-lookup"><span data-stu-id="14455-178">F# [code quotations](../language-reference/code-quotations.md) now have the ability to retain type constraint information.</span></span> <span data-ttu-id="14455-179">请看下面的示例：</span><span class="sxs-lookup"><span data-stu-id="14455-179">Consider the following example:</span></span>

```fsharp
open FSharp.Linq.RuntimeHelpers

let eval q = LeafExpressionConverter.EvaluateQuotation q

let inline negate x = -x
// val inline negate: x: ^a ->  ^a when  ^a : (static member ( ~- ) :  ^a ->  ^a)

<@ negate 1.0 @>  |> eval
```

<span data-ttu-id="14455-180">函数生成的约束 `inline` 保留在代码 qutoation 中。</span><span class="sxs-lookup"><span data-stu-id="14455-180">The constraint generated by the `inline` function is retained in the code qutoation.</span></span> <span data-ttu-id="14455-181">`negate`现在可以计算该函数的 quotated 窗体。</span><span class="sxs-lookup"><span data-stu-id="14455-181">The `negate` function's quotated form can now be evaluated.</span></span>

## <a name="applicative-computation-expressions"></a><span data-ttu-id="14455-182">Applicative 计算表达式</span><span class="sxs-lookup"><span data-stu-id="14455-182">Applicative Computation Expressions</span></span>

<span data-ttu-id="14455-183">当今使用[CEs)  (CEs 的计算表达式](../language-reference/computation-expressions.md)，用于对 "上下文计算" 进行建模，或以更功能编程友好术语一元计算。</span><span class="sxs-lookup"><span data-stu-id="14455-183">[Computation expressions (CEs)](../language-reference/computation-expressions.md) are used today to model "contextual computations", or in more functional programming friendly terminology, monadic computations.</span></span>

<span data-ttu-id="14455-184">F # 5 引入了 applicative CEs，后者提供不同的计算模型。</span><span class="sxs-lookup"><span data-stu-id="14455-184">F# 5 introduces applicative CEs, which offer a different computational model.</span></span> <span data-ttu-id="14455-185">Applicative CEs 允许进行更高效的计算，前提是每个计算都是独立的，并且其结果在结束时累计。</span><span class="sxs-lookup"><span data-stu-id="14455-185">Applicative CEs allow for more efficient computations provided that every computation is independent, and their results are accumulated at the end.</span></span> <span data-ttu-id="14455-186">当计算彼此独立时，它们也是完全可并行化，允许 CE 作者编写更高效的库。</span><span class="sxs-lookup"><span data-stu-id="14455-186">When computations are independent of one another, they are also trivially parallelizable, allowing CE authors to write more efficient libraries.</span></span> <span data-ttu-id="14455-187">不过，这种优势是一项限制：不允许使用依赖于先前计算的值的计算。</span><span class="sxs-lookup"><span data-stu-id="14455-187">This benefit comes at a restriction, though: computations that depend on previously-computed values are not allowed.</span></span>

<span data-ttu-id="14455-188">下面的示例显示了类型的基本 applicative CE `Result` 。</span><span class="sxs-lookup"><span data-stu-id="14455-188">The follow example shows a basic applicative CE for the `Result` type.</span></span>

```fsharp
// First, define a 'zip' function
module Result =
    let zip x1 x2 =
        match x1,x2 with
        | Ok x1res, Ok x2res -> Ok (x1res, x2res)
        | Error e, _ -> Error e
        | _, Error e -> Error e

// Next, define a builder with 'MergeSources' and 'BindReturn'
type ResultBuilder() =
    member _.MergeSources(t1: Result<'T,'U>, t2: Result<'T1,'U>) = Result.zip t1 t2
    member _.BindReturn(x: Result<'T,'U>, f) = Result.map f x

let result = ResultBuilder()

let run r1 r2 r3 =
    // And here is our applicative!
    let res1: Result<int, string> =
        result {
            let! a = r1
            and! b = r2
            and! c = r3
            return a + b - c
        }

    match res1 with
    | Ok x -> printfn "%s is: %d" (nameof res1) x
    | Error e -> printfn "%s is: %s" (nameof res1) e

let printApplicatives () =
    let r1 = Ok 2
    let r2 = Ok 3 // Error "fail!"
    let r3 = Ok 4

    run r1 r2 r3
    run r1 (Error "failure!") r3
```

<span data-ttu-id="14455-189">如果你是目前在其库中公开 CEs 的库作者，需要注意一些其他注意事项。</span><span class="sxs-lookup"><span data-stu-id="14455-189">If you're a library author who exposes CEs in their library today, there are some additional considerations you'll need to be aware of.</span></span>

## <a name="interfaces-can-be-implemeneted-at-different-generic-instantiations"></a><span data-ttu-id="14455-190">接口可以在不同的泛型实例化 implemeneted</span><span class="sxs-lookup"><span data-stu-id="14455-190">Interfaces can be implemeneted at different generic instantiations</span></span>

<span data-ttu-id="14455-191">你现在可以在不同的泛型实例化上实现相同的接口：</span><span class="sxs-lookup"><span data-stu-id="14455-191">You can now implement the same interface at different generic instantiations:</span></span>

```fsharp
type IA<'T> =
    abstract member Get : unit -> 'T

type MyClass() =
    interface IA<int> with
        member x.Get() = 1
    interface IA<string> with
        member x.Get() = "hello"

let mc = MyClass()
let iaInt = mc :> IA<int>
let iaString = mc :> IA<string>

iaInt.Get() // 1
iaString.Get() // "hello"
```

## <a name="default-interface-member-consumption"></a><span data-ttu-id="14455-192">默认接口成员消耗</span><span class="sxs-lookup"><span data-stu-id="14455-192">Default interface member consumption</span></span>

<span data-ttu-id="14455-193">F # 5 允许使用 [具有默认实现的接口](../../csharp/tutorials/default-interface-methods-versions.md)。</span><span class="sxs-lookup"><span data-stu-id="14455-193">F# 5 lets you consume [interfaces with default implementations](../../csharp/tutorials/default-interface-methods-versions.md).</span></span>

<span data-ttu-id="14455-194">请考虑 c # 中定义的接口，如下所示：</span><span class="sxs-lookup"><span data-stu-id="14455-194">Consider an interface defined in C# like this:</span></span>

```csharp
using System;

namespace CSharp
{
    public interface MyDimasd
    {
        public int Z => 0;
    }
}
```

<span data-ttu-id="14455-195">可以在 F # 中使用它来实现接口的任何标准方法：</span><span class="sxs-lookup"><span data-stu-id="14455-195">You can consume it in F# through any of the standard means of implementing an interface:</span></span>

```fsharp
open CSharp

// You can implement the interface via a class
type MyType() =
    member _.M() = ()

    interface MyDim

let md = MyType() :> MyDim
printfn "DIM from C#: %d" md.Z

// You can also implement it via an object expression
let md' = { new MyDim }
printfn "DIM from C# but via Object Expression: %d" md'.Z
```

<span data-ttu-id="14455-196">这使你能够在预期用户能够使用默认实现时，安全地利用在现代 c # 中编写的 c # 代码和 .NET 组件。</span><span class="sxs-lookup"><span data-stu-id="14455-196">This lets you safely take advantage of C# code and .NET components written in modern C# when they expect users to be able to consume a default implementation.</span></span>

## <a name="simplified-interop-with-nullable-value-types"></a><span data-ttu-id="14455-197">具有可以为 null 的值类型的简化互操作</span><span class="sxs-lookup"><span data-stu-id="14455-197">Simplified interop with nullable value types</span></span>

<span data-ttu-id="14455-198">[可以为 null 的 (值) 类型](https://docs.microsoft.com/dotnet/api/system.nullable-1) (早于 F # 支持的名称) 可以为 null 的类型，但与它们进行交互几乎有点困难，因为 `Nullable` `Nullable<SomeType>` 每次要传递值时都必须构造或包装。</span><span class="sxs-lookup"><span data-stu-id="14455-198">[Nullable (value) types](https://docs.microsoft.com/dotnet/api/system.nullable-1) (called Nullable Types historically) have long been supported by F#, but interacting with them has traditionally been somewhat of a pain since you'd have to construct a `Nullable` or `Nullable<SomeType>` wrapper every time you wanted to pass a value.</span></span> <span data-ttu-id="14455-199">现在， `Nullable<ThatValueType>` 如果目标类型匹配，则编译器会将值类型隐式转换为。</span><span class="sxs-lookup"><span data-stu-id="14455-199">Now the compiler will implicitly convert a value type into a `Nullable<ThatValueType>` if the target type matches.</span></span> <span data-ttu-id="14455-200">现在可以执行以下代码：</span><span class="sxs-lookup"><span data-stu-id="14455-200">The following code is now possible:</span></span>

```fsharp
#r "nuget: Microsoft.Data.Analysis"

open Microsoft.Data.Analysis

let dateTimes = PrimitiveDataFrameColumn<DateTime>("DateTimes")

// The following line used to fail to compile
dateTimes.Append(DateTime.Parse("2019/01/01"))

// The previous line is now equivalent to this line
dateTimes.Append(Nullable<DateTime>(DateTime.Parse("2019/01/01")))
```

## <a name="preview-reverse-indexes"></a><span data-ttu-id="14455-201">预览：反向索引</span><span class="sxs-lookup"><span data-stu-id="14455-201">Preview: reverse indexes</span></span>

<span data-ttu-id="14455-202">F # 5 还引入了允许反向索引的预览。</span><span class="sxs-lookup"><span data-stu-id="14455-202">F# 5 also introduces a preview for allowing reverse indexes.</span></span> <span data-ttu-id="14455-203">语法为 `^idx`。</span><span class="sxs-lookup"><span data-stu-id="14455-203">The syntax is `^idx`.</span></span> <span data-ttu-id="14455-204">下面介绍了从列表末尾的元素1值：</span><span class="sxs-lookup"><span data-stu-id="14455-204">Here's how you can an element 1 value from the end of a list:</span></span>

```fsharp
let xs = [1..10]

// Get element 1 from the end:
xs.[^1]

// From the end slices

let lastTwoOldStyle = xs.[(xs.Length-2)..]

let lastTwoNewStyle = xs.[^1..]

lastTwoOldStyle = lastTwoNewStyle // true
```

<span data-ttu-id="14455-205">你还可以为自己的类型定义反向索引。</span><span class="sxs-lookup"><span data-stu-id="14455-205">You can also define reverse indexes for your own types.</span></span> <span data-ttu-id="14455-206">为此，需要实现以下方法：</span><span class="sxs-lookup"><span data-stu-id="14455-206">To do so, you'll need to implement the following method:</span></span>

```fsharp
GetReverseIndex: dimension: int -> offset: int
```

<span data-ttu-id="14455-207">下面是该类型的示例 `Span<'T>` ：</span><span class="sxs-lookup"><span data-stu-id="14455-207">Here's an example for the `Span<'T>` type:</span></span>

```fsharp
open System

type Span<'T> with
    member sp.GetSlice(startIdx, endIdx) =
        let s = defaultArg startIdx 0
        let e = defaultArg endIdx sp.Length
        sp.Slice(s, e - s)

    member sp.GetReverseIndex(_, offset: int) =
        sp.Length - offset

let printSpan (sp: Span<int>) =
    let arr = sp.ToArray()
    printfn "%A" arr

let run () =
    let sp = [| 1; 2; 3; 4; 5 |].AsSpan()

    // Pre-# 5.0 slicing on a Span<'T>
    printSpan sp.[0..] // [|1; 2; 3; 4; 5|]
    printSpan sp.[..3] // [|1; 2; 3|]
    printSpan sp.[1..3] // |2; 3|]

    // Same slices, but only using from-the-end index
    printSpan sp.[..^0] // [|1; 2; 3; 4; 5|]
    printSpan sp.[..^2] // [|1; 2; 3|]
    printSpan sp.[^4..^2] // [|2; 3|]

run() // Prints the same thing twice
```

## <a name="preview-overloads-of-custom-keywords-in-computation-expressions"></a><span data-ttu-id="14455-208">预览：计算表达式中的自定义关键字的重载</span><span class="sxs-lookup"><span data-stu-id="14455-208">Preview: overloads of custom keywords in computation expressions</span></span>

<span data-ttu-id="14455-209">计算表达式是库和框架作者的强大功能。</span><span class="sxs-lookup"><span data-stu-id="14455-209">Computation expressions are a powerful feature for library and framework authors.</span></span> <span data-ttu-id="14455-210">它们允许您定义已知成员并为正在处理的域构建 DSL，从而极大地提高组件的表现力。</span><span class="sxs-lookup"><span data-stu-id="14455-210">They allow you to greatly improve the expressiveness of your components by letting you define well-known members and form a DSL for the domain you're working in.</span></span>

<span data-ttu-id="14455-211">F # 5 为计算表达式中的重载自定义操作添加了预览支持。</span><span class="sxs-lookup"><span data-stu-id="14455-211">F# 5 adds preview support for overloading custom operations in Computation Expressions.</span></span> <span data-ttu-id="14455-212">它允许写入和使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="14455-212">It allows the following code to be writen and consumed:</span></span>

```fsharp
open System

type InputKind =
    | Text of placeholder:string option
    | Password of placeholder: string option

type InputOptions =
  { Label: string option
    Kind : InputKind
    Validators : (string -> bool) array }

type InputBuilder() =
    member t.Yield(_) =
      { Label = None
        Kind = Text None
        Validators = [||] }

    [<CustomOperation("text")>]
    member this.Text(io, ?placeholder) =
        { io with Kind = Text placeholder }

    [<CustomOperation("password")>]
    member this.Password(io, ?placeholder) =
        { io with Kind = Password placeholder }

    [<CustomOperation("label")>]
    member this.Label(io, label) =
        { io with Label = Some label }

    [<CustomOperation("with_validators")>]
    member this.Validators(io, [<ParamArray>] validators) =
        { io with Validators = validators }

let input = InputBuilder()

let name =
    input {
    label "Name"
    text
    with_validators
        (String.IsNullOrWhiteSpace >> not)
    }

let email =
    input {
    label "Email"
    text "Your email"
    with_validators
        (String.IsNullOrWhiteSpace >> not)
        (fun s -> s.Contains "@")
    }

let password =
    input {
    label "Password"
    password "Must contains at least 6 characters, one number and one uppercase"
    with_validators
        (String.exists Char.IsUpper)
        (String.exists Char.IsDigit)
        (fun s -> s.Length >= 6)
    }
```

<span data-ttu-id="14455-213">在进行此更改之前，可以编写 `InputBuilder` 类型，但无法像在示例中使用它那样使用它。</span><span class="sxs-lookup"><span data-stu-id="14455-213">Prior to this change, you could write the `InputBuilder` type as it is, but you couldn't use it the way it's used in the example.</span></span> <span data-ttu-id="14455-214">由于允许使用重载、可选参数和 now `System.ParamArray` 类型，因此一切都按您预期的方式工作。</span><span class="sxs-lookup"><span data-stu-id="14455-214">Since overloads, optional parameters, and now `System.ParamArray` types are allowed, everything just works as you'd expect it to.</span></span>
