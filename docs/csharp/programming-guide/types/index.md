---
title: 类型 - C# 编程指南
description: 了解 C# 编程中的类型，例如内置类型、自定义类型、值类型和引用类型。
ms.date: 07/20/2015
helpviewer_keywords:
- value types [C#]
- reference types [C#]
- types [C#]
- C# language, data types
- common type system [C#]
- data types [C#]
- C# language, types
- strong typing [C#]
ms.assetid: f782d7cc-035e-4500-b1b1-36a9881130ad
ms.openlocfilehash: aba59f6626661145c10d23d4a2c167b8337ec559
ms.sourcegitcommit: 30a686fd4377fe6472aa04e215c0de711bc1c322
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94440375"
---
# <a name="types-c-programming-guide"></a><span data-ttu-id="a6e76-103">类型（C# 编程指南）</span><span class="sxs-lookup"><span data-stu-id="a6e76-103">Types (C# Programming Guide)</span></span>

## <a name="types-variables-and-values"></a><span data-ttu-id="a6e76-104">类型、变量和值</span><span class="sxs-lookup"><span data-stu-id="a6e76-104">Types, variables, and values</span></span>

<span data-ttu-id="a6e76-105">C# 是一种强类型语言。</span><span class="sxs-lookup"><span data-stu-id="a6e76-105">C# is a strongly typed language.</span></span> <span data-ttu-id="a6e76-106">每个变量和常量都有一个类型，每个求值的表达式也是如此。</span><span class="sxs-lookup"><span data-stu-id="a6e76-106">Every variable and constant has a type, as does every expression that evaluates to a value.</span></span> <span data-ttu-id="a6e76-107">每个方法声明都为每个输入参数和返回值指定名称、参数数量以及类型和种类（值、引用或输出）。</span><span class="sxs-lookup"><span data-stu-id="a6e76-107">Every method declaration specifies a name, number of parameters, and type and kind (value, reference, or output) for each input parameter and for the return value.</span></span> <span data-ttu-id="a6e76-108">.NET 类库定义了一组内置数值类型以及表示各种逻辑构造的更复杂类型（如文件系统、网络连接、对象的集合和数组以及日期）。</span><span class="sxs-lookup"><span data-stu-id="a6e76-108">The .NET class library defines a set of built-in numeric types as well as more complex types that represent a wide variety of logical constructs, such as the file system, network connections, collections and arrays of objects, and dates.</span></span> <span data-ttu-id="a6e76-109">典型的 C# 程序使用类库中的类型，以及对程序问题域的专属概念进行建模的用户定义类型。</span><span class="sxs-lookup"><span data-stu-id="a6e76-109">A typical C# program uses types from the class library as well as user-defined types that model the concepts that are specific to the program's problem domain.</span></span>

<span data-ttu-id="a6e76-110">类型中可存储以下信息：</span><span class="sxs-lookup"><span data-stu-id="a6e76-110">The information stored in a type can include the following:</span></span>

- <span data-ttu-id="a6e76-111">类型变量所需的存储空间。</span><span class="sxs-lookup"><span data-stu-id="a6e76-111">The storage space that a variable of the type requires.</span></span>

- <span data-ttu-id="a6e76-112">可以表示的最大值和最小值。</span><span class="sxs-lookup"><span data-stu-id="a6e76-112">The maximum and minimum values that it can represent.</span></span>

- <span data-ttu-id="a6e76-113">包含的成员（方法、字段、事件等）。</span><span class="sxs-lookup"><span data-stu-id="a6e76-113">The members (methods, fields, events, and so on) that it contains.</span></span>

- <span data-ttu-id="a6e76-114">继承自的基类型。</span><span class="sxs-lookup"><span data-stu-id="a6e76-114">The base type it inherits from.</span></span>

- <span data-ttu-id="a6e76-115">它实现的接口。</span><span class="sxs-lookup"><span data-stu-id="a6e76-115">The interface(s) it implements.</span></span>

- <span data-ttu-id="a6e76-116">在运行时分配变量内存的位置。</span><span class="sxs-lookup"><span data-stu-id="a6e76-116">The location where the memory for variables will be allocated at run time.</span></span>

- <span data-ttu-id="a6e76-117">允许执行的运算种类。</span><span class="sxs-lookup"><span data-stu-id="a6e76-117">The kinds of operations that are permitted.</span></span>

<span data-ttu-id="a6e76-118">编译器使用类型信息来确保在代码中执行的所有操作都是 *类型安全* 。</span><span class="sxs-lookup"><span data-stu-id="a6e76-118">The compiler uses type information to make sure that all operations that are performed in your code are *type safe*.</span></span> <span data-ttu-id="a6e76-119">例如，如果声明 [int](../../language-reference/builtin-types/integral-numeric-types.md) 类型的变量，那么编译器允许在加法和减法运算中使用此变量。</span><span class="sxs-lookup"><span data-stu-id="a6e76-119">For example, if you declare a variable of type [int](../../language-reference/builtin-types/integral-numeric-types.md), the compiler allows you to use the variable in addition and subtraction operations.</span></span> <span data-ttu-id="a6e76-120">如果尝试对 [bool](../../language-reference/builtin-types/bool.md) 类型的变量执行这些相同操作，则编译器将生成错误，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="a6e76-120">If you try to perform those same operations on a variable of type [bool](../../language-reference/builtin-types/bool.md), the compiler generates an error, as shown in the following example:</span></span>

[!code-csharp[csProgGuideTypes#42](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#42)]

> [!NOTE]
> <span data-ttu-id="a6e76-121">C 和 C++ 开发人员请注意，在 C# 中，[bool](../../language-reference/builtin-types/bool.md) 不能转换为 [int](../../language-reference/builtin-types/integral-numeric-types.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-121">C and C++ developers, notice that in C#, [bool](../../language-reference/builtin-types/bool.md) is not convertible to [int](../../language-reference/builtin-types/integral-numeric-types.md).</span></span>

<span data-ttu-id="a6e76-122">编译器将类型信息作为元数据嵌入可执行文件中。</span><span class="sxs-lookup"><span data-stu-id="a6e76-122">The compiler embeds the type information into the executable file as metadata.</span></span> <span data-ttu-id="a6e76-123">公共语言运行时 (CLR) 在运行时使用元数据，以在分配和回收内存时进一步保证类型安全性。</span><span class="sxs-lookup"><span data-stu-id="a6e76-123">The common language runtime (CLR) uses that metadata at run time to further guarantee type safety when it allocates and reclaims memory.</span></span>

### <a name="specifying-types-in-variable-declarations"></a><span data-ttu-id="a6e76-124">在变量声明中指定类型</span><span class="sxs-lookup"><span data-stu-id="a6e76-124">Specifying types in variable declarations</span></span>

<span data-ttu-id="a6e76-125">当在程序中声明变量或常量时，必须指定其类型或使用 [var](../../language-reference/keywords/var.md) 关键字让编译器推断类型。</span><span class="sxs-lookup"><span data-stu-id="a6e76-125">When you declare a variable or constant in a program, you must either specify its type or use the [var](../../language-reference/keywords/var.md) keyword to let the compiler infer the type.</span></span> <span data-ttu-id="a6e76-126">以下示例显示了一些使用内置数值类型和复杂用户定义类型的变量声明：</span><span class="sxs-lookup"><span data-stu-id="a6e76-126">The following example shows some variable declarations that use both built-in numeric types and complex user-defined types:</span></span>

[!code-csharp[csProgGuideTypes#36](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#36)]

<span data-ttu-id="a6e76-127">方法声明指定方法参数的类型和返回值。</span><span class="sxs-lookup"><span data-stu-id="a6e76-127">The types of method parameters and return values are specified in the method declaration.</span></span> <span data-ttu-id="a6e76-128">以下签名显示了需要 [int](../../language-reference/builtin-types/integral-numeric-types.md) 作为输入参数并返回字符串的方法：</span><span class="sxs-lookup"><span data-stu-id="a6e76-128">The following signature shows a method that requires an [int](../../language-reference/builtin-types/integral-numeric-types.md) as an input argument and returns a string:</span></span>

[!code-csharp[csProgGuideTypes#35](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#35)]

<span data-ttu-id="a6e76-129">在声明变量后，不能使用新类型重新声明该变量，并且不能为其分配与其声明的类型不兼容的值。</span><span class="sxs-lookup"><span data-stu-id="a6e76-129">After a variable is declared, it cannot be re-declared with a new type, and it cannot be assigned a value that is not compatible with its declared type.</span></span> <span data-ttu-id="a6e76-130">例如，不能声明 [int](../../language-reference/builtin-types/integral-numeric-types.md)再向它分配 `true` 的布尔值。</span><span class="sxs-lookup"><span data-stu-id="a6e76-130">For example, you cannot declare an [int](../../language-reference/builtin-types/integral-numeric-types.md) and then assign it a Boolean value of `true`.</span></span> <span data-ttu-id="a6e76-131">不过，可以将值转换成其他类型。例如，在将值赋给新变量或作为方法自变量传递时。</span><span class="sxs-lookup"><span data-stu-id="a6e76-131">However, values can be converted to other types, for example when they are assigned to new variables or passed as method arguments.</span></span> <span data-ttu-id="a6e76-132">编译器会自动执行不会导致数据丢失的 *类型转换* 。</span><span class="sxs-lookup"><span data-stu-id="a6e76-132">A *type conversion* that does not cause data loss is performed automatically by the compiler.</span></span> <span data-ttu-id="a6e76-133">如果类型转换可能会导致数据丢失，必须在源代码中进行 *显式转换* 。</span><span class="sxs-lookup"><span data-stu-id="a6e76-133">A conversion that might cause data loss requires a *cast* in the source code.</span></span>

<span data-ttu-id="a6e76-134">有关详细信息，请参阅[显式转换和类型转换](./casting-and-type-conversions.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-134">For more information, see [Casting and Type Conversions](./casting-and-type-conversions.md).</span></span>

## <a name="built-in-types"></a><span data-ttu-id="a6e76-135">内置类型</span><span class="sxs-lookup"><span data-stu-id="a6e76-135">Built-in types</span></span>

<span data-ttu-id="a6e76-136">C# 提供了一组标准的内置类型来表示整数、浮点值、布尔表达式、文本字符、十进制值和其他数据类型。</span><span class="sxs-lookup"><span data-stu-id="a6e76-136">C# provides a standard set of built-in types to represent integers, floating point values, Boolean expressions, text characters, decimal values, and other types of data.</span></span> <span data-ttu-id="a6e76-137">还有内置的 `string` 和 `object` 类型。</span><span class="sxs-lookup"><span data-stu-id="a6e76-137">There are also built-in `string` and `object` types.</span></span> <span data-ttu-id="a6e76-138">这些类型可供在任何 C# 程序中使用。</span><span class="sxs-lookup"><span data-stu-id="a6e76-138">These are available for you to use in any C# program.</span></span> <span data-ttu-id="a6e76-139">有关内置类型的完整列表，请参阅[内置类型](../../language-reference/builtin-types/built-in-types.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-139">For the complete list of the built-in types, see [Built-in types](../../language-reference/builtin-types/built-in-types.md).</span></span>

## <a name="custom-types"></a><span data-ttu-id="a6e76-140">自定义类型</span><span class="sxs-lookup"><span data-stu-id="a6e76-140">Custom types</span></span>

<span data-ttu-id="a6e76-141">可以使用[结构](../../language-reference/builtin-types/struct.md)、[类](../../language-reference/keywords/class.md)、[接口](../../language-reference/keywords/interface.md)，和[枚举](../../language-reference/builtin-types/enum.md)构造创建你自己的自定义类型。</span><span class="sxs-lookup"><span data-stu-id="a6e76-141">You use the [struct](../../language-reference/builtin-types/struct.md), [class](../../language-reference/keywords/class.md), [interface](../../language-reference/keywords/interface.md), and [enum](../../language-reference/builtin-types/enum.md) constructs to create your own custom types.</span></span> <span data-ttu-id="a6e76-142">.NET 类库本身就是 Microsoft 提供的一组自定义类型，以供你在自己的应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="a6e76-142">The .NET class library itself is a collection of custom types provided by Microsoft that you can use in your own applications.</span></span> <span data-ttu-id="a6e76-143">默认情况下，类库中最常用的类型在任何 C# 程序中均可用。</span><span class="sxs-lookup"><span data-stu-id="a6e76-143">By default, the most frequently used types in the class library are available in any C# program.</span></span> <span data-ttu-id="a6e76-144">对于其他类型，只有在显式添加对定义这些类型的程序集的项目引用时才可用。</span><span class="sxs-lookup"><span data-stu-id="a6e76-144">Others become available only when you explicitly add a project reference to the assembly in which they are defined.</span></span> <span data-ttu-id="a6e76-145">编译器引用程序集之后，你可以声明在源代码的此程序集中声明的类型的变量（和常量）。</span><span class="sxs-lookup"><span data-stu-id="a6e76-145">After the compiler has a reference to the assembly, you can declare variables (and constants) of the types declared in that assembly in source code.</span></span> <span data-ttu-id="a6e76-146">有关详细信息，请参阅 [.NET 类库](../../../standard/class-library-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-146">For more information, see [.NET Class Library](../../../standard/class-library-overview.md).</span></span>

## <a name="the-common-type-system"></a><span data-ttu-id="a6e76-147">通用类型系统</span><span class="sxs-lookup"><span data-stu-id="a6e76-147">The common type system</span></span>

<span data-ttu-id="a6e76-148">对于 .NET 中的类型系统，请务必了解以下两个基本要点：</span><span class="sxs-lookup"><span data-stu-id="a6e76-148">It is important to understand two fundamental points about the type system in .NET:</span></span>

- <span data-ttu-id="a6e76-149">它支持继承原则。</span><span class="sxs-lookup"><span data-stu-id="a6e76-149">It supports the principle of inheritance.</span></span> <span data-ttu-id="a6e76-150">类型可以派生自其他类型（称为 *基类型* ）。</span><span class="sxs-lookup"><span data-stu-id="a6e76-150">Types can derive from other types, called *base types*.</span></span> <span data-ttu-id="a6e76-151">派生类型继承（有一些限制）基类型的方法、属性和其他成员。</span><span class="sxs-lookup"><span data-stu-id="a6e76-151">The derived type inherits (with some restrictions) the methods, properties, and other members of the base type.</span></span> <span data-ttu-id="a6e76-152">基类型可以继而从某种其他类型派生，在这种情况下，派生类型继承其继承层次结构中的两种基类型的成员。</span><span class="sxs-lookup"><span data-stu-id="a6e76-152">The base type can in turn derive from some other type, in which case the derived type inherits the members of both base types in its inheritance hierarchy.</span></span> <span data-ttu-id="a6e76-153">所有类型（包括 <xref:System.Int32?displayProperty=nameWithType>C# 关键字：[int](../../language-reference/builtin-types/integral-numeric-types.md)等内置数值类型）最终都派生自单个基类型，即 <xref:System.Object?displayProperty=nameWithType>（C# 关键字：[object](../../language-reference/builtin-types/reference-types.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-153">All types, including built-in numeric types such as <xref:System.Int32?displayProperty=nameWithType> (C# keyword: [int](../../language-reference/builtin-types/integral-numeric-types.md)), derive ultimately from a single base type, which is <xref:System.Object?displayProperty=nameWithType> (C# keyword: [object](../../language-reference/builtin-types/reference-types.md)).</span></span> <span data-ttu-id="a6e76-154">这样的统一类型层次结构称为[通用类型系统](../../../standard/base-types/common-type-system.md) (CTS)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-154">This unified type hierarchy is called the [Common Type System](../../../standard/base-types/common-type-system.md) (CTS).</span></span> <span data-ttu-id="a6e76-155">若要详细了解 C# 中的继承，请参阅[继承](../classes-and-structs/inheritance.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-155">For more information about inheritance in C#, see [Inheritance](../classes-and-structs/inheritance.md).</span></span>

- <span data-ttu-id="a6e76-156">CTS 中的每种类型被定义为值类型或引用类型。 </span><span class="sxs-lookup"><span data-stu-id="a6e76-156">Each type in the CTS is defined as either a *value type* or a *reference type*.</span></span> <span data-ttu-id="a6e76-157">这包括 .NET 类库中的所有自定义类型以及你自己的用户定义类型。</span><span class="sxs-lookup"><span data-stu-id="a6e76-157">This includes all custom types in the .NET class library and also your own user-defined types.</span></span> <span data-ttu-id="a6e76-158">使用 [struct](../../language-reference/builtin-types/struct.md) 关键字定义的类型是值类型；所有内置数值类型都是 `structs`。</span><span class="sxs-lookup"><span data-stu-id="a6e76-158">Types that you define by using the [struct](../../language-reference/builtin-types/struct.md) keyword are value types; all the built-in numeric types are `structs`.</span></span> <span data-ttu-id="a6e76-159">使用 [class](../../language-reference/keywords/class.md) 关键字定义的类型是引用类型。</span><span class="sxs-lookup"><span data-stu-id="a6e76-159">Types that you define by using the [class](../../language-reference/keywords/class.md) keyword are reference types.</span></span> <span data-ttu-id="a6e76-160">引用类型和值类型遵循不同的编译时规则和运行时行为。</span><span class="sxs-lookup"><span data-stu-id="a6e76-160">Reference types and value types have different compile-time rules, and different run-time behavior.</span></span>

<span data-ttu-id="a6e76-161">下图展示了 CTS 中值类型和引用类型之间的关系。</span><span class="sxs-lookup"><span data-stu-id="a6e76-161">The following illustration shows the relationship between value types and reference types in the CTS.</span></span>

<span data-ttu-id="a6e76-162">下图显示 CTS 中的值类型和引用类型：</span><span class="sxs-lookup"><span data-stu-id="a6e76-162">The following image shows value types and reference types in the CTS:</span></span>

![屏幕截图显示了 CTS 值类型和引用类型。](./media/index/value-reference-types-common-type-system.png)

> [!NOTE]
> <span data-ttu-id="a6e76-164">你可能会发现，最常用的类型全都被整理到了 <xref:System> 命名空间中。</span><span class="sxs-lookup"><span data-stu-id="a6e76-164">You can see that the most commonly used types are all organized in the <xref:System> namespace.</span></span> <span data-ttu-id="a6e76-165">不过，包含类型的命名空间与类型是值类型还是引用类型没有关系。</span><span class="sxs-lookup"><span data-stu-id="a6e76-165">However, the namespace in which a type is contained has no relation to whether it is a value type or reference type.</span></span>

### <a name="value-types"></a><span data-ttu-id="a6e76-166">值类型</span><span class="sxs-lookup"><span data-stu-id="a6e76-166">Value types</span></span>

<span data-ttu-id="a6e76-167">值类型派生自<xref:System.ValueType?displayProperty=nameWithType>（派生自 <xref:System.Object?displayProperty=nameWithType>）。</span><span class="sxs-lookup"><span data-stu-id="a6e76-167">Value types derive from <xref:System.ValueType?displayProperty=nameWithType>, which derives from <xref:System.Object?displayProperty=nameWithType>.</span></span> <span data-ttu-id="a6e76-168">派生自 <xref:System.ValueType?displayProperty=nameWithType> 的类型在 CLR 中具有特殊行为。</span><span class="sxs-lookup"><span data-stu-id="a6e76-168">Types that derive from <xref:System.ValueType?displayProperty=nameWithType> have special behavior in the CLR.</span></span> <span data-ttu-id="a6e76-169">值类型变量直接包含它们的值，这意味着在声明变量的任何上下文中内联分配内存。</span><span class="sxs-lookup"><span data-stu-id="a6e76-169">Value type variables directly contain their values, which means that the memory is allocated inline in whatever context the variable is declared.</span></span> <span data-ttu-id="a6e76-170">对于值类型变量，没有单独的堆分配或垃圾回收开销。</span><span class="sxs-lookup"><span data-stu-id="a6e76-170">There is no separate heap allocation or garbage collection overhead for value-type variables.</span></span>

<span data-ttu-id="a6e76-171">值类型分为两类：[结构](../../language-reference/builtin-types/struct.md)和[枚举](../../language-reference/builtin-types/enum.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-171">There are two categories of value types: [struct](../../language-reference/builtin-types/struct.md) and [enum](../../language-reference/builtin-types/enum.md).</span></span>

<span data-ttu-id="a6e76-172">内置的数值类型是结构，它们具有可访问的字段和方法：</span><span class="sxs-lookup"><span data-stu-id="a6e76-172">The built-in numeric types are structs, and they have fields and methods that you can access:</span></span>

```csharp
// constant field on type byte.
byte b = byte.MaxValue;
```

<span data-ttu-id="a6e76-173">但可将这些类型视为简单的非聚合类型，为其声明并赋值：</span><span class="sxs-lookup"><span data-stu-id="a6e76-173">But you declare and assign values to them as if they were simple non-aggregate types:</span></span>

```csharp
byte num = 0xA;
int i = 5;
char c = 'Z';
```

<span data-ttu-id="a6e76-174">例如，值类型为“密封”，这意味着不能从 <xref:System.Int32?displayProperty=nameWithType> 派生类型，并且不能将结构定义为从任何用户定义的类或结构继承，因为结构只能从 <xref:System.ValueType?displayProperty=nameWithType> 继承。</span><span class="sxs-lookup"><span data-stu-id="a6e76-174">Value types are *sealed* , which means, for example, that you cannot derive a type from <xref:System.Int32?displayProperty=nameWithType>, and you cannot define a struct to inherit from any user-defined class or struct because a struct can only inherit from <xref:System.ValueType?displayProperty=nameWithType>.</span></span> <span data-ttu-id="a6e76-175">但是，一个结构可以实现一个或多个接口。</span><span class="sxs-lookup"><span data-stu-id="a6e76-175">However, a struct can implement one or more interfaces.</span></span> <span data-ttu-id="a6e76-176">可将结构类型强制转换为它实现的任何接口类型；这会导致装箱操作发生，以将结构包装在托管堆上的引用类型对象内。</span><span class="sxs-lookup"><span data-stu-id="a6e76-176">You can cast a struct type to any interface type that it implements; this causes a *boxing* operation to wrap the struct inside a reference type object on the managed heap.</span></span> <span data-ttu-id="a6e76-177">当你将值类型传递给使用 <xref:System.Object?displayProperty=nameWithType> 或任何接口类型作为输入参数的方法时，就会发生装箱操作。</span><span class="sxs-lookup"><span data-stu-id="a6e76-177">Boxing operations occur when you pass a value type to a method that takes a <xref:System.Object?displayProperty=nameWithType> or any interface type as an input parameter.</span></span> <span data-ttu-id="a6e76-178">有关详细信息，请参阅[装箱和取消装箱](./boxing-and-unboxing.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-178">For more information, see [Boxing and Unboxing](./boxing-and-unboxing.md).</span></span>

<span data-ttu-id="a6e76-179">使用 [struct](../../language-reference/builtin-types/struct.md) 关键字可以创建你自己的自定义值类型。</span><span class="sxs-lookup"><span data-stu-id="a6e76-179">You use the [struct](../../language-reference/builtin-types/struct.md) keyword to create your own custom value types.</span></span> <span data-ttu-id="a6e76-180">结构通常用作一小组相关变量的容器，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="a6e76-180">Typically, a struct is used as a container for a small set of related variables, as shown in the following example:</span></span>

[!code-csharp[csProgGuideObjects#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#1)]

<span data-ttu-id="a6e76-181">有关结构的详细信息，请参阅[结构类型](../../language-reference/builtin-types/struct.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-181">For more information about structs, see [Structure types](../../language-reference/builtin-types/struct.md).</span></span> <span data-ttu-id="a6e76-182">有关值类型的详细信息，请参阅[值类型](../../language-reference/builtin-types/value-types.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-182">For more information about value types, see [Value types](../../language-reference/builtin-types/value-types.md).</span></span>

<span data-ttu-id="a6e76-183">另一种值类型是[枚举](../../language-reference/builtin-types/enum.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-183">The other category of value types is [enum](../../language-reference/builtin-types/enum.md).</span></span> <span data-ttu-id="a6e76-184">枚举定义的是一组已命名的整型常量。</span><span class="sxs-lookup"><span data-stu-id="a6e76-184">An enum defines a set of named integral constants.</span></span> <span data-ttu-id="a6e76-185">例如，.NET 类库中的 <xref:System.IO.FileMode?displayProperty=nameWithType> 枚举包含一组已命名的常量整数，用于指定打开文件应采用的方式。</span><span class="sxs-lookup"><span data-stu-id="a6e76-185">For example, the <xref:System.IO.FileMode?displayProperty=nameWithType> enumeration in the .NET class library contains a set of named constant integers that specify how a file should be opened.</span></span> <span data-ttu-id="a6e76-186">下面的示例展示了具体定义：</span><span class="sxs-lookup"><span data-stu-id="a6e76-186">It is defined as shown in the following example:</span></span>

[!code-csharp[csProgGuideTypes#44](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#44)]

<span data-ttu-id="a6e76-187">`System.IO.FileMode.Create` 常量的值为 2。</span><span class="sxs-lookup"><span data-stu-id="a6e76-187">The `System.IO.FileMode.Create` constant has a value of 2.</span></span> <span data-ttu-id="a6e76-188">不过，名称对于阅读源代码的人来说更有意义，因此，最好使用枚举，而不是常量数字文本。</span><span class="sxs-lookup"><span data-stu-id="a6e76-188">However, the name is much more meaningful for humans reading the source code, and for that reason it is better to use enumerations instead of constant literal numbers.</span></span> <span data-ttu-id="a6e76-189">有关详细信息，请参阅 <xref:System.IO.FileMode?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="a6e76-189">For more information, see <xref:System.IO.FileMode?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="a6e76-190">所有枚举从 <xref:System.Enum?displayProperty=nameWithType>（继承自 <xref:System.ValueType?displayProperty=nameWithType>）继承。</span><span class="sxs-lookup"><span data-stu-id="a6e76-190">All enums inherit from <xref:System.Enum?displayProperty=nameWithType>, which inherits from <xref:System.ValueType?displayProperty=nameWithType>.</span></span> <span data-ttu-id="a6e76-191">适用于结构的所有规则也适用于枚举。</span><span class="sxs-lookup"><span data-stu-id="a6e76-191">All the rules that apply to structs also apply to enums.</span></span> <span data-ttu-id="a6e76-192">有关枚举的详细信息，请参阅[枚举类型](../../language-reference/builtin-types/enum.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-192">For more information about enums, see [Enumeration types](../../language-reference/builtin-types/enum.md).</span></span>

### <a name="reference-types"></a><span data-ttu-id="a6e76-193">引用类型</span><span class="sxs-lookup"><span data-stu-id="a6e76-193">Reference types</span></span>

<span data-ttu-id="a6e76-194">定义为 [类](../../language-reference/keywords/class.md)、 [委托](../../language-reference/builtin-types/reference-types.md)、数组或 [接口](../../language-reference/keywords/interface.md)的类型是 *引用类型* 。</span><span class="sxs-lookup"><span data-stu-id="a6e76-194">A type that is defined as a [class](../../language-reference/keywords/class.md), [delegate](../../language-reference/builtin-types/reference-types.md), array, or [interface](../../language-reference/keywords/interface.md) is a *reference type*.</span></span> <span data-ttu-id="a6e76-195">在运行时，当声明引用类型的变量时，该变量会一直包含值 [null](../../language-reference/keywords/null.md)，直至使用 [new](../../language-reference/operators/new-operator.md) 运算符显式创建对象，或者为该变量分配已经在其他位置使用 `new` 创建的对象，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a6e76-195">At run time, when you declare a variable of a reference type, the variable contains the value [null](../../language-reference/keywords/null.md) until you explicitly create an object by using the [new](../../language-reference/operators/new-operator.md) operator, or assign it an object that has been created elsewhere by using `new`, as shown in the following example:</span></span>

```csharp
MyClass mc = new MyClass();
MyClass mc2 = mc;
```

<span data-ttu-id="a6e76-196">接口必须与实现它的类对象一起初始化。</span><span class="sxs-lookup"><span data-stu-id="a6e76-196">An interface must be initialized together with a class object that implements it.</span></span> <span data-ttu-id="a6e76-197">如果 `MyClass` 实现 `IMyInterface`，则按以下示例所示创建 `IMyInterface` 的实例：</span><span class="sxs-lookup"><span data-stu-id="a6e76-197">If `MyClass` implements `IMyInterface`, you create an instance of `IMyInterface` as shown in the following example:</span></span>

```csharp
IMyInterface iface = new MyClass();
```

<span data-ttu-id="a6e76-198">创建对象后，内存会在托管堆上进行分配，并且变量只保留对对象位置的引用。</span><span class="sxs-lookup"><span data-stu-id="a6e76-198">When the object is created, the memory is allocated on the managed heap, and the variable holds only a reference to the location of the object.</span></span> <span data-ttu-id="a6e76-199">对于托管堆上的类型，在分配内存和 CLR 自动内存管理功能（称为“ *垃圾回收* ”）回收内存时都会产生开销。</span><span class="sxs-lookup"><span data-stu-id="a6e76-199">Types on the managed heap require overhead both when they are allocated and when they are reclaimed by the automatic memory management functionality of the CLR, which is known as *garbage collection*.</span></span> <span data-ttu-id="a6e76-200">不过，垃圾回收功能也已经过高度优化，大多数情况下，都不会导致性能问题出现。</span><span class="sxs-lookup"><span data-stu-id="a6e76-200">However, garbage collection is also highly optimized, and in most scenarios it does not create a performance issue.</span></span> <span data-ttu-id="a6e76-201">有关垃圾回收的详细信息，请参阅[自动内存管理](../../../standard/automatic-memory-management.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-201">For more information about garbage collection, see [Automatic Memory Management](../../../standard/automatic-memory-management.md).</span></span>

<span data-ttu-id="a6e76-202">所有数组都是引用类型，即使元素是值类型，也不例外。</span><span class="sxs-lookup"><span data-stu-id="a6e76-202">All arrays are reference types, even if their elements are value types.</span></span> <span data-ttu-id="a6e76-203">虽然数组隐式派生自 <xref:System.Array?displayProperty=nameWithType> 类，但可以使用 C# 提供的简化语法声明和使用数组，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="a6e76-203">Arrays implicitly derive from the <xref:System.Array?displayProperty=nameWithType> class, but you declare and use them with the simplified syntax that is provided by C#, as shown in the following example:</span></span>

[!code-csharp[csProgGuideTypes#45](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#45)]

<span data-ttu-id="a6e76-204">引用类型完全支持继承。</span><span class="sxs-lookup"><span data-stu-id="a6e76-204">Reference types fully support inheritance.</span></span> <span data-ttu-id="a6e76-205">创建类时，可以继承自其他任何未定义为[密封](../../language-reference/keywords/sealed.md)的接口或类，而其他类也可以继承自你的类并重写你的虚方法。</span><span class="sxs-lookup"><span data-stu-id="a6e76-205">When you create a class, you can inherit from any other interface or class that is not defined as [sealed](../../language-reference/keywords/sealed.md), and other classes can inherit from your class and override your virtual methods.</span></span> <span data-ttu-id="a6e76-206">若要详细了解如何创建你自己的类，请参阅[类和结构](../classes-and-structs/index.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-206">For more information about how to create your own classes, see [Classes and Structs](../classes-and-structs/index.md).</span></span> <span data-ttu-id="a6e76-207">有关继承和虚方法的详细信息，请参阅[继承](../classes-and-structs/inheritance.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-207">For more information about inheritance and virtual methods, see [Inheritance](../classes-and-structs/inheritance.md).</span></span>

## <a name="types-of-literal-values"></a><span data-ttu-id="a6e76-208">文本值的类型</span><span class="sxs-lookup"><span data-stu-id="a6e76-208">Types of literal values</span></span>

<span data-ttu-id="a6e76-209">在 C# 中，文本值从编译器接收类型。</span><span class="sxs-lookup"><span data-stu-id="a6e76-209">In C#, literal values receive a type from the compiler.</span></span> <span data-ttu-id="a6e76-210">可以通过在数字末尾追加一个字母来指定数字文本应采用的类型。</span><span class="sxs-lookup"><span data-stu-id="a6e76-210">You can specify how a numeric literal should be typed by appending a letter to the end of the number.</span></span> <span data-ttu-id="a6e76-211">例如，若要将值 4.56 指定为应按浮点值处理，请在数字后面追加“f”或“F”：`4.56f`。</span><span class="sxs-lookup"><span data-stu-id="a6e76-211">For example, to specify that the value 4.56 should be treated as a float, append an "f" or "F" after the number: `4.56f`.</span></span> <span data-ttu-id="a6e76-212">如果没有追加字母，那么编译器就会推断文本值的类型。</span><span class="sxs-lookup"><span data-stu-id="a6e76-212">If no letter is appended, the compiler will infer a type for the literal.</span></span> <span data-ttu-id="a6e76-213">若要详细了解可以使用字母后缀指定哪些类型，请参阅[整型数值类型](../../language-reference/builtin-types/integral-numeric-types.md)和[浮点数值类型](../../language-reference/builtin-types/floating-point-numeric-types.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-213">For more information about which types can be specified with letter suffixes, see [Integral numeric types](../../language-reference/builtin-types/integral-numeric-types.md) and [Floating-point numeric types](../../language-reference/builtin-types/floating-point-numeric-types.md).</span></span>

<span data-ttu-id="a6e76-214">由于文本已类型化，且所有类型最终都是从 <xref:System.Object?displayProperty=nameWithType> 派生，因此可以编写和编译如下所示的代码：</span><span class="sxs-lookup"><span data-stu-id="a6e76-214">Because literals are typed, and all types derive ultimately from <xref:System.Object?displayProperty=nameWithType>, you can write and compile code such as the following:</span></span>

[!code-csharp[csProgGuideTypes#37](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#37)]

## <a name="generic-types"></a><span data-ttu-id="a6e76-215">泛型类型</span><span class="sxs-lookup"><span data-stu-id="a6e76-215">Generic types</span></span>

<span data-ttu-id="a6e76-216">可使用一个或多个类型参数声明、作为客户端代码在创建类型实例时将提供的实际类型（具体类型）的占位符的类型。 </span><span class="sxs-lookup"><span data-stu-id="a6e76-216">A type can be declared with one or more *type parameters* that serve as a placeholder for the actual type (the *concrete type* ) that client code will provide when it creates an instance of the type.</span></span> <span data-ttu-id="a6e76-217">这种类型称为泛型类型。</span><span class="sxs-lookup"><span data-stu-id="a6e76-217">Such types are called *generic types*.</span></span> <span data-ttu-id="a6e76-218">例如，.NET 类型 <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> 具有一个类型参数，它按照惯例被命名为 *T* 。当创建类型的实例时，指定列表将包含的对象的类型，例如字符串：</span><span class="sxs-lookup"><span data-stu-id="a6e76-218">For example, the .NET type <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> has one type parameter that by convention is given the name *T*. When you create an instance of the type, you specify the type of the objects that the list will contain, for example, string:</span></span>

```csharp
List<string> stringList = new List<string>();
stringList.Add("String example");
// compile time error adding a type other than a string:
stringList.Add(4);
```

<span data-ttu-id="a6e76-219">通过使用类型参数，可重新使用相同类以保存任意类型的元素，且无需将每个元素转换为[对象](../../language-reference/builtin-types/reference-types.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-219">The use of the type parameter makes it possible to reuse the same class to hold any type of element, without having to convert each element to [object](../../language-reference/builtin-types/reference-types.md).</span></span> <span data-ttu-id="a6e76-220">泛型集合类称为强类型集合，因为编译器知道集合元素的具体类型，并能在编译时抛出错误，例如当尝试向上面示例中的 `stringList` 对象添加整数时。</span><span class="sxs-lookup"><span data-stu-id="a6e76-220">Generic collection classes are called *strongly typed collections* because the compiler knows the specific type of the collection's elements and can raise an error at compile-time if, for example, you try to add an integer to the `stringList` object in the previous example.</span></span> <span data-ttu-id="a6e76-221">有关详细信息，请参阅[泛型](../generics/index.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-221">For more information, see [Generics](../generics/index.md).</span></span>

## <a name="implicit-types-anonymous-types-and-nullable-value-types"></a><span data-ttu-id="a6e76-222">隐式类型、匿名类型和可以为 null 的值类型</span><span class="sxs-lookup"><span data-stu-id="a6e76-222">Implicit types, anonymous types, and nullable value types</span></span>

<span data-ttu-id="a6e76-223">如前所述，你可以使用 [var](../../language-reference/keywords/var.md) 关键字隐式键入一个局部变量（但不是类成员）。</span><span class="sxs-lookup"><span data-stu-id="a6e76-223">As stated previously, you can implicitly type a local variable (but not class members) by using the [var](../../language-reference/keywords/var.md) keyword.</span></span> <span data-ttu-id="a6e76-224">变量仍可在编译时获取类型，但类型是由编译器提供。</span><span class="sxs-lookup"><span data-stu-id="a6e76-224">The variable still receives a type at compile time, but the type is provided by the compiler.</span></span> <span data-ttu-id="a6e76-225">有关详细信息，请参阅[隐式类型局部变量](../classes-and-structs/implicitly-typed-local-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-225">For more information, see [Implicitly Typed Local Variables](../classes-and-structs/implicitly-typed-local-variables.md).</span></span>

<span data-ttu-id="a6e76-226">在某些情况下，为不打算在方法边界外存储或传递的各组简单的相关值创建已命名的类型并不方便。</span><span class="sxs-lookup"><span data-stu-id="a6e76-226">In some cases, it is inconvenient to create a named type for simple sets of related values that you do not intend to store or pass outside method boundaries.</span></span> <span data-ttu-id="a6e76-227">因此，可以创建 *匿名类型* 。</span><span class="sxs-lookup"><span data-stu-id="a6e76-227">You can create *anonymous types* for this purpose.</span></span> <span data-ttu-id="a6e76-228">有关详细信息，请参阅[匿名类型](../classes-and-structs/anonymous-types.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-228">For more information, see [Anonymous Types](../classes-and-structs/anonymous-types.md).</span></span>

<span data-ttu-id="a6e76-229">普通值类型不能包含值 [null](../../language-reference/keywords/null.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-229">Ordinary value types cannot have a value of [null](../../language-reference/keywords/null.md).</span></span> <span data-ttu-id="a6e76-230">不过，可以在类型后面附加 `?`，创建可以为 null 的值类型。</span><span class="sxs-lookup"><span data-stu-id="a6e76-230">However, you can create nullable value types by affixing a `?` after the type.</span></span> <span data-ttu-id="a6e76-231">例如，`int?` 是还可以包含值 [null](../../language-reference/keywords/null.md) 的 `int` 类型。</span><span class="sxs-lookup"><span data-stu-id="a6e76-231">For example, `int?` is an `int` type that can also have the value [null](../../language-reference/keywords/null.md).</span></span> <span data-ttu-id="a6e76-232">可以为 null 的值类型是泛型结构类型 <xref:System.Nullable%601?displayProperty=nameWithType> 的实例。</span><span class="sxs-lookup"><span data-stu-id="a6e76-232">Nullable value types are instances of the generic struct type <xref:System.Nullable%601?displayProperty=nameWithType>.</span></span> <span data-ttu-id="a6e76-233">在将数据传入和传出数据库（数值可能为 null）时，可以为 null 的值类型特别有用。</span><span class="sxs-lookup"><span data-stu-id="a6e76-233">Nullable value types are especially useful when you are passing data to and from databases in which numeric values might be null.</span></span> <span data-ttu-id="a6e76-234">有关详细信息，请参阅[可以为 null 的值类型](../../language-reference/builtin-types/nullable-value-types.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e76-234">For more information, see [Nullable value types](../../language-reference/builtin-types/nullable-value-types.md).</span></span>

## <a name="related-sections"></a><span data-ttu-id="a6e76-235">相关章节</span><span class="sxs-lookup"><span data-stu-id="a6e76-235">Related sections</span></span>

<span data-ttu-id="a6e76-236">有关详细信息，请参阅下列主题：</span><span class="sxs-lookup"><span data-stu-id="a6e76-236">For more information, see the following topics:</span></span>

- [<span data-ttu-id="a6e76-237">强制转换和类型转换</span><span class="sxs-lookup"><span data-stu-id="a6e76-237">Casting and Type Conversions</span></span>](./casting-and-type-conversions.md)

- [<span data-ttu-id="a6e76-238">装箱和取消装箱</span><span class="sxs-lookup"><span data-stu-id="a6e76-238">Boxing and Unboxing</span></span>](./boxing-and-unboxing.md)

- [<span data-ttu-id="a6e76-239">使用类型 dynamic</span><span class="sxs-lookup"><span data-stu-id="a6e76-239">Using Type dynamic</span></span>](./using-type-dynamic.md)

- [<span data-ttu-id="a6e76-240">值类型</span><span class="sxs-lookup"><span data-stu-id="a6e76-240">Value Types</span></span>](../../language-reference/builtin-types/value-types.md)

- [<span data-ttu-id="a6e76-241">引用类型</span><span class="sxs-lookup"><span data-stu-id="a6e76-241">Reference Types</span></span>](../../language-reference/keywords/reference-types.md)

- [<span data-ttu-id="a6e76-242">类和结构</span><span class="sxs-lookup"><span data-stu-id="a6e76-242">Classes and Structs</span></span>](../classes-and-structs/index.md)

- [<span data-ttu-id="a6e76-243">匿名类型</span><span class="sxs-lookup"><span data-stu-id="a6e76-243">Anonymous Types</span></span>](../classes-and-structs/anonymous-types.md)

- [<span data-ttu-id="a6e76-244">泛型</span><span class="sxs-lookup"><span data-stu-id="a6e76-244">Generics</span></span>](../generics/index.md)

## <a name="c-language-specification"></a><span data-ttu-id="a6e76-245">C# 语言规范</span><span class="sxs-lookup"><span data-stu-id="a6e76-245">C# language specification</span></span>

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a><span data-ttu-id="a6e76-246">请参阅</span><span class="sxs-lookup"><span data-stu-id="a6e76-246">See also</span></span>

- [<span data-ttu-id="a6e76-247">C# 参考</span><span class="sxs-lookup"><span data-stu-id="a6e76-247">C# Reference</span></span>](../../language-reference/index.md)
- [<span data-ttu-id="a6e76-248">C# 编程指南</span><span class="sxs-lookup"><span data-stu-id="a6e76-248">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="a6e76-249">XML 数据类型转换</span><span class="sxs-lookup"><span data-stu-id="a6e76-249">Conversion of XML Data Types</span></span>](../../../standard/data/xml/conversion-of-xml-data-types.md)
- [<span data-ttu-id="a6e76-250">整型类型</span><span class="sxs-lookup"><span data-stu-id="a6e76-250">Integral types</span></span>](../../language-reference/builtin-types/integral-numeric-types.md)
