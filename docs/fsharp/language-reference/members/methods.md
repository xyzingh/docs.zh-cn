---
title: 方法
description: '了解 F # 方法是与用于公开和实现对象和类型的功能和行为的类型相关联的函数。'
ms.date: 11/04/2019
ms.openlocfilehash: 6f5ae76ea450b07763eb58d0c95b18b30f634551
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92224110"
---
# <a name="methods"></a><span data-ttu-id="2b8b0-103">方法</span><span class="sxs-lookup"><span data-stu-id="2b8b0-103">Methods</span></span>

<span data-ttu-id="2b8b0-104">*方法*是与类型相关联的函数。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-104">A *method* is a function that is associated with a type.</span></span> <span data-ttu-id="2b8b0-105">在面向对象的编程中，方法用于公开和实现对象和类型的功能和行为。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-105">In object-oriented programming, methods are used to expose and implement the functionality and behavior of objects and types.</span></span>

## <a name="syntax"></a><span data-ttu-id="2b8b0-106">语法</span><span class="sxs-lookup"><span data-stu-id="2b8b0-106">Syntax</span></span>

```fsharp
// Instance method definition.
[ attributes ]
member [inline] self-identifier.method-name parameter-list [ : return-type ] =
    method-body

// Static method definition.
[ attributes ]
static member [inline] method-name parameter-list [ : return-type ] =
    method-body

// Abstract method declaration or virtual dispatch slot.
[ attributes ]
abstract member method-name : type-signature

// Virtual method declaration and default implementation.
[ attributes ]
abstract member method-name : type-signature
[ attributes ]
default self-identifier.method-name parameter-list [ : return-type ] =
    method-body

// Override of inherited virtual method.
[ attributes ]
override self-identifier.method-name parameter-list [ : return-type ] =
    method-body

// Optional and DefaultParameterValue attributes on input parameters
[ attributes ]
[ modifier ] member [inline] self-identifier.method-name ([<Optional; DefaultParameterValue( default-value )>] input) [ : return-type ]
```

## <a name="remarks"></a><span data-ttu-id="2b8b0-107">备注</span><span class="sxs-lookup"><span data-stu-id="2b8b0-107">Remarks</span></span>

<span data-ttu-id="2b8b0-108">在前面的语法中，可以看到各种形式的方法声明和定义。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-108">In the previous syntax, you can see the various forms of method declarations and definitions.</span></span> <span data-ttu-id="2b8b0-109">在较长的方法体中，等号 (=) ，并缩进整个方法体。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-109">In longer method bodies, a line break follows the equal sign (=), and the whole method body is indented.</span></span>

<span data-ttu-id="2b8b0-110">特性可应用于任何方法声明。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-110">Attributes can be applied to any method declaration.</span></span> <span data-ttu-id="2b8b0-111">它们位于方法定义的语法之前，通常在单独的行中列出。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-111">They precede the syntax for a method definition and are usually listed on a separate line.</span></span> <span data-ttu-id="2b8b0-112">有关更多信息，请参阅[特性](../attributes.md)。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-112">For more information, see [Attributes](../attributes.md).</span></span>

<span data-ttu-id="2b8b0-113">可以标记方法 `inline` 。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-113">Methods can be marked `inline`.</span></span> <span data-ttu-id="2b8b0-114">有关 `inline` 的信息，请参阅[内联函数](../functions/inline-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-114">For information about `inline`, see [Inline Functions](../functions/inline-functions.md).</span></span>

<span data-ttu-id="2b8b0-115">非内联方法可在类型内递归使用;无需显式使用 `rec` 关键字。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-115">Non-inline methods can be used recursively within the type; there is no need to explicitly use the `rec` keyword.</span></span>

## <a name="instance-methods"></a><span data-ttu-id="2b8b0-116">实例方法</span><span class="sxs-lookup"><span data-stu-id="2b8b0-116">Instance Methods</span></span>

<span data-ttu-id="2b8b0-117">实例方法使用 `member` 关键字和 *自标识符*进行声明，后跟一个句点 (。 ) 和方法名称和参数。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-117">Instance methods are declared with the `member` keyword and a *self-identifier*, followed by a period (.) and the method name and parameters.</span></span> <span data-ttu-id="2b8b0-118">与绑定的情况一样 `let` ， *参数列表* 可以是一种模式。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-118">As is the case for `let` bindings, the *parameter-list* can be a pattern.</span></span> <span data-ttu-id="2b8b0-119">通常，将方法参数括在元组形式的括号中，这是在以其他 .NET Framework 语言创建方法时方法在 F # 中的显示方式。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-119">Typically, you enclose method parameters in parentheses in a tuple form, which is the way methods appear in F# when they are created in other .NET Framework languages.</span></span> <span data-ttu-id="2b8b0-120">不过，扩充格式 (参数由空格分隔) 也很常见，并且还支持其他模式。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-120">However, the curried form (parameters separated by spaces) is also common, and other patterns are supported also.</span></span>

<span data-ttu-id="2b8b0-121">下面的示例演示如何定义和使用非抽象实例方法。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-121">The following example illustrates the definition and use of a non-abstract instance method.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3401.fs)]

<span data-ttu-id="2b8b0-122">在实例方法中，不要使用 self 标识符访问使用 let bindings 定义的字段。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-122">Within instance methods, do not use the self identifier to access fields defined by using let bindings.</span></span> <span data-ttu-id="2b8b0-123">在访问其他成员和属性时使用 self 标识符。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-123">Use the self identifier when accessing other members and properties.</span></span>

## <a name="static-methods"></a><span data-ttu-id="2b8b0-124">静态方法</span><span class="sxs-lookup"><span data-stu-id="2b8b0-124">Static Methods</span></span>

<span data-ttu-id="2b8b0-125">关键字 `static` 用于指定可在没有实例的情况下调用方法，并且不与对象实例相关联。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-125">The keyword `static` is used to specify that a method can be called without an instance and is not associated with an object instance.</span></span> <span data-ttu-id="2b8b0-126">否则，方法是实例方法。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-126">Otherwise, methods are instance methods.</span></span>

<span data-ttu-id="2b8b0-127">下一节中的示例演示使用关键字声明的字段 `let` 、使用关键字声明的属性成员 `member` 以及使用关键字声明的静态方法 `static` 。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-127">The example in the next section shows fields declared with the `let` keyword, property members declared with the `member` keyword, and a static method declared with the `static` keyword.</span></span>

<span data-ttu-id="2b8b0-128">下面的示例演示如何定义和使用静态方法。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-128">The following example illustrates the definition and use of static methods.</span></span> <span data-ttu-id="2b8b0-129">假设前面部分的类中有这些方法定义 `SomeType` 。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-129">Assume that these method definitions are in the `SomeType` class in the previous section.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3402.fs)]

## <a name="abstract-and-virtual-methods"></a><span data-ttu-id="2b8b0-130">抽象方法和虚方法</span><span class="sxs-lookup"><span data-stu-id="2b8b0-130">Abstract and Virtual Methods</span></span>

<span data-ttu-id="2b8b0-131">关键字 `abstract` 指示方法具有虚拟调度槽，并且在类中可能不具有定义。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-131">The keyword `abstract` indicates that a method has a virtual dispatch slot and might not have a definition in the class.</span></span> <span data-ttu-id="2b8b0-132">*虚拟调度槽*是在运行时用于在面向对象的类型中查找虚拟函数调用的函数的内部维护表中的条目。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-132">A *virtual dispatch slot* is an entry in an internally maintained table of functions that is used at run time to look up virtual function calls in an object-oriented type.</span></span> <span data-ttu-id="2b8b0-133">虚拟调度机制是实现 *多态性*的机制，这是面向对象编程的一项重要功能。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-133">The virtual dispatch mechanism is the mechanism that implements *polymorphism*, an important feature of object-oriented programming.</span></span> <span data-ttu-id="2b8b0-134">至少具有一个没有定义的抽象方法的类是一个 *抽象类*，这意味着不能创建该类的任何实例。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-134">A class that has at least one abstract method without a definition is an *abstract class*, which means that no instances can be created of that class.</span></span> <span data-ttu-id="2b8b0-135">有关抽象类的详细信息，请参阅 [抽象类](../abstract-classes.md)。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-135">For more information about abstract classes, see [Abstract Classes](../abstract-classes.md).</span></span>

<span data-ttu-id="2b8b0-136">抽象方法声明不包括方法体。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-136">Abstract method declarations do not include a method body.</span></span> <span data-ttu-id="2b8b0-137">相反，方法的名称后跟一个冒号 (： ) 和方法的类型签名。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-137">Instead, the name of the method is followed by a colon (:) and a type signature for the method.</span></span> <span data-ttu-id="2b8b0-138">当你将鼠标指针悬停在 Visual Studio Code 编辑器中的方法名称上（不包含参数名称）时，方法的类型签名与 IntelliSense 显示的类型签名相同。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-138">The type signature of a method is the same as that shown by IntelliSense when you pause the mouse pointer over a method name in the Visual Studio Code Editor, except without parameter names.</span></span> <span data-ttu-id="2b8b0-139">当交互处理时，fsi.exe 的解释器也会显示类型签名。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-139">Type signatures are also displayed by the interpreter, fsi.exe, when you are working interactively.</span></span> <span data-ttu-id="2b8b0-140">方法的类型签名通过使用适当的分隔符符号列出参数的类型，后跟返回类型。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-140">The type signature of a method is formed by listing out the types of the parameters, followed by the return type, with appropriate separator symbols.</span></span> <span data-ttu-id="2b8b0-141">扩充参数由分隔 `->` ，元组参数由分隔 `*` 。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-141">Curried parameters are separated by `->` and tuple parameters are separated by `*`.</span></span> <span data-ttu-id="2b8b0-142">返回值始终与参数之间用 `->` 符号隔开。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-142">The return value is always separated from the arguments by a `->` symbol.</span></span> <span data-ttu-id="2b8b0-143">括号可用于对复杂参数分组，如函数类型为参数时，或指示将元组视为单个参数而不是两个参数的时间。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-143">Parentheses can be used to group complex parameters, such as when a function type is a parameter, or to indicate when a tuple is treated as a single parameter rather than as two parameters.</span></span>

<span data-ttu-id="2b8b0-144">还可以通过将定义添加到类并使用关键字来为抽象方法默认定义 `default` ，如本主题中的语法块中所示。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-144">You can also give abstract methods default definitions by adding the definition to the class and using the `default` keyword, as shown in the syntax block in this topic.</span></span> <span data-ttu-id="2b8b0-145">在同一个类中具有定义的抽象方法等效于其他 .NET Framework 语言的虚方法。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-145">An abstract method that has a definition in the same class is equivalent to a virtual method in other .NET Framework languages.</span></span> <span data-ttu-id="2b8b0-146">无论定义是否存在， `abstract` 关键字都会在类的虚拟函数表中创建新的调度槽。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-146">Whether or not a definition exists, the `abstract` keyword creates a new dispatch slot in the virtual function table for the class.</span></span>

<span data-ttu-id="2b8b0-147">无论基类是否实现其抽象方法，派生类都可以提供抽象方法的实现。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-147">Regardless of whether a base class implements its abstract methods, derived classes can provide implementations of abstract methods.</span></span> <span data-ttu-id="2b8b0-148">若要在派生类中实现抽象方法，请在派生类中定义具有相同名称和签名的方法，但使用 `override` 或 `default` 关键字，并提供方法体。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-148">To implement an abstract method in a derived class, define a method that has the same name and signature in the derived class, except use the `override` or `default` keyword, and provide the method body.</span></span> <span data-ttu-id="2b8b0-149">关键字 `override` 和 `default` 的含义完全相同。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-149">The keywords `override` and `default` mean exactly the same thing.</span></span> <span data-ttu-id="2b8b0-150">`override`如果新方法重写基类实现，则使用; 在与 `default` 原始抽象声明相同的类中创建实现时使用。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-150">Use `override` if the new method overrides a base class implementation; use `default` when you create an implementation in the same class as the original abstract declaration.</span></span> <span data-ttu-id="2b8b0-151">不要 `abstract` 在实现基类中声明为抽象的方法的方法上使用关键字。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-151">Do not use the `abstract` keyword on the method that implements the method that was declared abstract in the base class.</span></span>

<span data-ttu-id="2b8b0-152">下面的示例演示 `Rotate` 具有默认实现的抽象方法，该方法等效于 .NET Framework 虚方法。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-152">The following example illustrates an abstract method `Rotate` that has a default implementation, the equivalent of a .NET Framework virtual method.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3403.fs)]

<span data-ttu-id="2b8b0-153">下面的示例演示了一个重写基类方法的派生类。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-153">The following example illustrates a derived class that overrides a base class method.</span></span> <span data-ttu-id="2b8b0-154">在这种情况下，重写将更改行为，使方法不执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-154">In this case, the override changes the behavior so that the method does nothing.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3404.fs)]

## <a name="overloaded-methods"></a><span data-ttu-id="2b8b0-155">重载方法</span><span class="sxs-lookup"><span data-stu-id="2b8b0-155">Overloaded Methods</span></span>

<span data-ttu-id="2b8b0-156">重载方法是在给定类型中具有相同名称但具有不同参数的方法。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-156">Overloaded methods are methods that have identical names in a given type but that have different arguments.</span></span> <span data-ttu-id="2b8b0-157">在 F # 中，通常使用可选参数，而不是重载方法。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-157">In F#, optional arguments are usually used instead of overloaded methods.</span></span> <span data-ttu-id="2b8b0-158">但是，如果参数采用的是元组格式，而不是扩充形式，则允许使用重载方法。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-158">However, overloaded methods are permitted in the language, provided that the arguments are in tuple form, not curried form.</span></span>

## <a name="optional-arguments"></a><span data-ttu-id="2b8b0-159">可选实参</span><span class="sxs-lookup"><span data-stu-id="2b8b0-159">Optional Arguments</span></span>

<span data-ttu-id="2b8b0-160">从 F # 4.1 开始，还可以在方法中使用带有默认参数值的可选参数。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-160">Starting with F# 4.1, you can also have optional arguments with a default parameter value in methods.</span></span>  <span data-ttu-id="2b8b0-161">这有助于简化与 c # 代码的互操作。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-161">This is to help facilitate interoperation with C# code.</span></span>  <span data-ttu-id="2b8b0-162">下面的示例演示了语法：</span><span class="sxs-lookup"><span data-stu-id="2b8b0-162">The following example demonstrates the syntax:</span></span>

```fsharp
// A class with a method M, which takes in an optional integer argument.
type C() =
    _.M([<Optional; DefaultParameterValue(12)>] i) = i + 1
```

<span data-ttu-id="2b8b0-163">请注意，为传入的值 `DefaultParameterValue` 必须与输入类型匹配。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-163">Note that the value passed in for `DefaultParameterValue` must match the input type.</span></span>  <span data-ttu-id="2b8b0-164">在上面的示例中，它是一个 `int` 。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-164">In the above sample, it is an `int`.</span></span>  <span data-ttu-id="2b8b0-165">尝试将一个非整数值传递到 `DefaultParameterValue` 将导致编译错误。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-165">Attempting to pass a non-integer value into `DefaultParameterValue` would result in a compile error.</span></span>

## <a name="example-properties-and-methods"></a><span data-ttu-id="2b8b0-166">示例：属性和方法</span><span class="sxs-lookup"><span data-stu-id="2b8b0-166">Example: Properties and Methods</span></span>

<span data-ttu-id="2b8b0-167">下面的示例包含一个类型，该类型包含字段、私有函数、属性和静态方法的示例。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-167">The following example contains a type that has examples of fields, private functions, properties, and a static method.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3406.fs)]

## <a name="see-also"></a><span data-ttu-id="2b8b0-168">另请参阅</span><span class="sxs-lookup"><span data-stu-id="2b8b0-168">See also</span></span>

- [<span data-ttu-id="2b8b0-169">成员</span><span class="sxs-lookup"><span data-stu-id="2b8b0-169">Members</span></span>](index.md)
