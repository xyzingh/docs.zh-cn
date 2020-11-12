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
# <a name="types-c-programming-guide"></a>类型（C# 编程指南）

## <a name="types-variables-and-values"></a>类型、变量和值

C# 是一种强类型语言。 每个变量和常量都有一个类型，每个求值的表达式也是如此。 每个方法声明都为每个输入参数和返回值指定名称、参数数量以及类型和种类（值、引用或输出）。 .NET 类库定义了一组内置数值类型以及表示各种逻辑构造的更复杂类型（如文件系统、网络连接、对象的集合和数组以及日期）。 典型的 C# 程序使用类库中的类型，以及对程序问题域的专属概念进行建模的用户定义类型。

类型中可存储以下信息：

- 类型变量所需的存储空间。

- 可以表示的最大值和最小值。

- 包含的成员（方法、字段、事件等）。

- 继承自的基类型。

- 它实现的接口。

- 在运行时分配变量内存的位置。

- 允许执行的运算种类。

编译器使用类型信息来确保在代码中执行的所有操作都是 *类型安全* 。 例如，如果声明 [int](../../language-reference/builtin-types/integral-numeric-types.md) 类型的变量，那么编译器允许在加法和减法运算中使用此变量。 如果尝试对 [bool](../../language-reference/builtin-types/bool.md) 类型的变量执行这些相同操作，则编译器将生成错误，如以下示例所示：

[!code-csharp[csProgGuideTypes#42](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#42)]

> [!NOTE]
> C 和 C++ 开发人员请注意，在 C# 中，[bool](../../language-reference/builtin-types/bool.md) 不能转换为 [int](../../language-reference/builtin-types/integral-numeric-types.md)。

编译器将类型信息作为元数据嵌入可执行文件中。 公共语言运行时 (CLR) 在运行时使用元数据，以在分配和回收内存时进一步保证类型安全性。

### <a name="specifying-types-in-variable-declarations"></a>在变量声明中指定类型

当在程序中声明变量或常量时，必须指定其类型或使用 [var](../../language-reference/keywords/var.md) 关键字让编译器推断类型。 以下示例显示了一些使用内置数值类型和复杂用户定义类型的变量声明：

[!code-csharp[csProgGuideTypes#36](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#36)]

方法声明指定方法参数的类型和返回值。 以下签名显示了需要 [int](../../language-reference/builtin-types/integral-numeric-types.md) 作为输入参数并返回字符串的方法：

[!code-csharp[csProgGuideTypes#35](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#35)]

在声明变量后，不能使用新类型重新声明该变量，并且不能为其分配与其声明的类型不兼容的值。 例如，不能声明 [int](../../language-reference/builtin-types/integral-numeric-types.md)再向它分配 `true` 的布尔值。 不过，可以将值转换成其他类型。例如，在将值赋给新变量或作为方法自变量传递时。 编译器会自动执行不会导致数据丢失的 *类型转换* 。 如果类型转换可能会导致数据丢失，必须在源代码中进行 *显式转换* 。

有关详细信息，请参阅[显式转换和类型转换](./casting-and-type-conversions.md)。

## <a name="built-in-types"></a>内置类型

C# 提供了一组标准的内置类型来表示整数、浮点值、布尔表达式、文本字符、十进制值和其他数据类型。 还有内置的 `string` 和 `object` 类型。 这些类型可供在任何 C# 程序中使用。 有关内置类型的完整列表，请参阅[内置类型](../../language-reference/builtin-types/built-in-types.md)。

## <a name="custom-types"></a>自定义类型

可以使用[结构](../../language-reference/builtin-types/struct.md)、[类](../../language-reference/keywords/class.md)、[接口](../../language-reference/keywords/interface.md)，和[枚举](../../language-reference/builtin-types/enum.md)构造创建你自己的自定义类型。 .NET 类库本身就是 Microsoft 提供的一组自定义类型，以供你在自己的应用程序中使用。 默认情况下，类库中最常用的类型在任何 C# 程序中均可用。 对于其他类型，只有在显式添加对定义这些类型的程序集的项目引用时才可用。 编译器引用程序集之后，你可以声明在源代码的此程序集中声明的类型的变量（和常量）。 有关详细信息，请参阅 [.NET 类库](../../../standard/class-library-overview.md)。

## <a name="the-common-type-system"></a>通用类型系统

对于 .NET 中的类型系统，请务必了解以下两个基本要点：

- 它支持继承原则。 类型可以派生自其他类型（称为 *基类型* ）。 派生类型继承（有一些限制）基类型的方法、属性和其他成员。 基类型可以继而从某种其他类型派生，在这种情况下，派生类型继承其继承层次结构中的两种基类型的成员。 所有类型（包括 <xref:System.Int32?displayProperty=nameWithType>C# 关键字：[int](../../language-reference/builtin-types/integral-numeric-types.md)等内置数值类型）最终都派生自单个基类型，即 <xref:System.Object?displayProperty=nameWithType>（C# 关键字：[object](../../language-reference/builtin-types/reference-types.md)。 这样的统一类型层次结构称为[通用类型系统](../../../standard/base-types/common-type-system.md) (CTS)。 若要详细了解 C# 中的继承，请参阅[继承](../classes-and-structs/inheritance.md)。

- CTS 中的每种类型被定义为值类型或引用类型。  这包括 .NET 类库中的所有自定义类型以及你自己的用户定义类型。 使用 [struct](../../language-reference/builtin-types/struct.md) 关键字定义的类型是值类型；所有内置数值类型都是 `structs`。 使用 [class](../../language-reference/keywords/class.md) 关键字定义的类型是引用类型。 引用类型和值类型遵循不同的编译时规则和运行时行为。

下图展示了 CTS 中值类型和引用类型之间的关系。

下图显示 CTS 中的值类型和引用类型：

![屏幕截图显示了 CTS 值类型和引用类型。](./media/index/value-reference-types-common-type-system.png)

> [!NOTE]
> 你可能会发现，最常用的类型全都被整理到了 <xref:System> 命名空间中。 不过，包含类型的命名空间与类型是值类型还是引用类型没有关系。

### <a name="value-types"></a>值类型

值类型派生自<xref:System.ValueType?displayProperty=nameWithType>（派生自 <xref:System.Object?displayProperty=nameWithType>）。 派生自 <xref:System.ValueType?displayProperty=nameWithType> 的类型在 CLR 中具有特殊行为。 值类型变量直接包含它们的值，这意味着在声明变量的任何上下文中内联分配内存。 对于值类型变量，没有单独的堆分配或垃圾回收开销。

值类型分为两类：[结构](../../language-reference/builtin-types/struct.md)和[枚举](../../language-reference/builtin-types/enum.md)。

内置的数值类型是结构，它们具有可访问的字段和方法：

```csharp
// constant field on type byte.
byte b = byte.MaxValue;
```

但可将这些类型视为简单的非聚合类型，为其声明并赋值：

```csharp
byte num = 0xA;
int i = 5;
char c = 'Z';
```

例如，值类型为“密封”，这意味着不能从 <xref:System.Int32?displayProperty=nameWithType> 派生类型，并且不能将结构定义为从任何用户定义的类或结构继承，因为结构只能从 <xref:System.ValueType?displayProperty=nameWithType> 继承。 但是，一个结构可以实现一个或多个接口。 可将结构类型强制转换为它实现的任何接口类型；这会导致装箱操作发生，以将结构包装在托管堆上的引用类型对象内。 当你将值类型传递给使用 <xref:System.Object?displayProperty=nameWithType> 或任何接口类型作为输入参数的方法时，就会发生装箱操作。 有关详细信息，请参阅[装箱和取消装箱](./boxing-and-unboxing.md)。

使用 [struct](../../language-reference/builtin-types/struct.md) 关键字可以创建你自己的自定义值类型。 结构通常用作一小组相关变量的容器，如以下示例所示：

[!code-csharp[csProgGuideObjects#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#1)]

有关结构的详细信息，请参阅[结构类型](../../language-reference/builtin-types/struct.md)。 有关值类型的详细信息，请参阅[值类型](../../language-reference/builtin-types/value-types.md)。

另一种值类型是[枚举](../../language-reference/builtin-types/enum.md)。 枚举定义的是一组已命名的整型常量。 例如，.NET 类库中的 <xref:System.IO.FileMode?displayProperty=nameWithType> 枚举包含一组已命名的常量整数，用于指定打开文件应采用的方式。 下面的示例展示了具体定义：

[!code-csharp[csProgGuideTypes#44](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#44)]

`System.IO.FileMode.Create` 常量的值为 2。 不过，名称对于阅读源代码的人来说更有意义，因此，最好使用枚举，而不是常量数字文本。 有关详细信息，请参阅 <xref:System.IO.FileMode?displayProperty=nameWithType>。

所有枚举从 <xref:System.Enum?displayProperty=nameWithType>（继承自 <xref:System.ValueType?displayProperty=nameWithType>）继承。 适用于结构的所有规则也适用于枚举。 有关枚举的详细信息，请参阅[枚举类型](../../language-reference/builtin-types/enum.md)。

### <a name="reference-types"></a>引用类型

定义为 [类](../../language-reference/keywords/class.md)、 [委托](../../language-reference/builtin-types/reference-types.md)、数组或 [接口](../../language-reference/keywords/interface.md)的类型是 *引用类型* 。 在运行时，当声明引用类型的变量时，该变量会一直包含值 [null](../../language-reference/keywords/null.md)，直至使用 [new](../../language-reference/operators/new-operator.md) 运算符显式创建对象，或者为该变量分配已经在其他位置使用 `new` 创建的对象，如下所示：

```csharp
MyClass mc = new MyClass();
MyClass mc2 = mc;
```

接口必须与实现它的类对象一起初始化。 如果 `MyClass` 实现 `IMyInterface`，则按以下示例所示创建 `IMyInterface` 的实例：

```csharp
IMyInterface iface = new MyClass();
```

创建对象后，内存会在托管堆上进行分配，并且变量只保留对对象位置的引用。 对于托管堆上的类型，在分配内存和 CLR 自动内存管理功能（称为“ *垃圾回收* ”）回收内存时都会产生开销。 不过，垃圾回收功能也已经过高度优化，大多数情况下，都不会导致性能问题出现。 有关垃圾回收的详细信息，请参阅[自动内存管理](../../../standard/automatic-memory-management.md)。

所有数组都是引用类型，即使元素是值类型，也不例外。 虽然数组隐式派生自 <xref:System.Array?displayProperty=nameWithType> 类，但可以使用 C# 提供的简化语法声明和使用数组，如以下示例所示：

[!code-csharp[csProgGuideTypes#45](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#45)]

引用类型完全支持继承。 创建类时，可以继承自其他任何未定义为[密封](../../language-reference/keywords/sealed.md)的接口或类，而其他类也可以继承自你的类并重写你的虚方法。 若要详细了解如何创建你自己的类，请参阅[类和结构](../classes-and-structs/index.md)。 有关继承和虚方法的详细信息，请参阅[继承](../classes-and-structs/inheritance.md)。

## <a name="types-of-literal-values"></a>文本值的类型

在 C# 中，文本值从编译器接收类型。 可以通过在数字末尾追加一个字母来指定数字文本应采用的类型。 例如，若要将值 4.56 指定为应按浮点值处理，请在数字后面追加“f”或“F”：`4.56f`。 如果没有追加字母，那么编译器就会推断文本值的类型。 若要详细了解可以使用字母后缀指定哪些类型，请参阅[整型数值类型](../../language-reference/builtin-types/integral-numeric-types.md)和[浮点数值类型](../../language-reference/builtin-types/floating-point-numeric-types.md)。

由于文本已类型化，且所有类型最终都是从 <xref:System.Object?displayProperty=nameWithType> 派生，因此可以编写和编译如下所示的代码：

[!code-csharp[csProgGuideTypes#37](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#37)]

## <a name="generic-types"></a>泛型类型

可使用一个或多个类型参数声明、作为客户端代码在创建类型实例时将提供的实际类型（具体类型）的占位符的类型。  这种类型称为泛型类型。 例如，.NET 类型 <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> 具有一个类型参数，它按照惯例被命名为 *T* 。当创建类型的实例时，指定列表将包含的对象的类型，例如字符串：

```csharp
List<string> stringList = new List<string>();
stringList.Add("String example");
// compile time error adding a type other than a string:
stringList.Add(4);
```

通过使用类型参数，可重新使用相同类以保存任意类型的元素，且无需将每个元素转换为[对象](../../language-reference/builtin-types/reference-types.md)。 泛型集合类称为强类型集合，因为编译器知道集合元素的具体类型，并能在编译时抛出错误，例如当尝试向上面示例中的 `stringList` 对象添加整数时。 有关详细信息，请参阅[泛型](../generics/index.md)。

## <a name="implicit-types-anonymous-types-and-nullable-value-types"></a>隐式类型、匿名类型和可以为 null 的值类型

如前所述，你可以使用 [var](../../language-reference/keywords/var.md) 关键字隐式键入一个局部变量（但不是类成员）。 变量仍可在编译时获取类型，但类型是由编译器提供。 有关详细信息，请参阅[隐式类型局部变量](../classes-and-structs/implicitly-typed-local-variables.md)。

在某些情况下，为不打算在方法边界外存储或传递的各组简单的相关值创建已命名的类型并不方便。 因此，可以创建 *匿名类型* 。 有关详细信息，请参阅[匿名类型](../classes-and-structs/anonymous-types.md)。

普通值类型不能包含值 [null](../../language-reference/keywords/null.md)。 不过，可以在类型后面附加 `?`，创建可以为 null 的值类型。 例如，`int?` 是还可以包含值 [null](../../language-reference/keywords/null.md) 的 `int` 类型。 可以为 null 的值类型是泛型结构类型 <xref:System.Nullable%601?displayProperty=nameWithType> 的实例。 在将数据传入和传出数据库（数值可能为 null）时，可以为 null 的值类型特别有用。 有关详细信息，请参阅[可以为 null 的值类型](../../language-reference/builtin-types/nullable-value-types.md)。

## <a name="related-sections"></a>相关章节

有关详细信息，请参阅下列主题：

- [强制转换和类型转换](./casting-and-type-conversions.md)

- [装箱和取消装箱](./boxing-and-unboxing.md)

- [使用类型 dynamic](./using-type-dynamic.md)

- [值类型](../../language-reference/builtin-types/value-types.md)

- [引用类型](../../language-reference/keywords/reference-types.md)

- [类和结构](../classes-and-structs/index.md)

- [匿名类型](../classes-and-structs/anonymous-types.md)

- [泛型](../generics/index.md)

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- [C# 参考](../../language-reference/index.md)
- [C# 编程指南](../index.md)
- [XML 数据类型转换](../../../standard/data/xml/conversion-of-xml-data-types.md)
- [整型类型](../../language-reference/builtin-types/integral-numeric-types.md)
