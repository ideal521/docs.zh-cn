---
title: F# 概览
description: 通过示例来介绍 F# 语言中的一些主要特性。
ms.date: 11/06/2018
ms.openlocfilehash: 35b811b580cd7c3b4a620f45b602150a92479052
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630070"
---
# <a name="tour-of-f"></a>F 教程\#

了解 F# 语言的最好方式就是阅读和编写 F# 代码。 本文将介绍 F# 语言的一些关键特性，并提供一些可以在计算机上执行的代码片段。 若要了解如何设置开发环境，请查看[入门](./tutorials/getting-started/index.md)。

F# 中有两个主要概念：函数和类型。  本文主要介绍该语言中属于这两个概念范畴的特性。

## <a name="executing-the-code-online"></a>在线执行代码

如果未在计算机F#上安装, 则可以在浏览器[ F# ](https://tryfsharp.fsbolero.io/)中执行 WebAssembly 中的所有示例。 Fable 是一种用于直接在浏览器中执行 F# 的方言。 若要在 REPL 中查看以下示例，请查看 Fable REPL 左侧菜单栏中的“示例”>“了解”>“F# 概览”  。

## <a name="functions-and-modules"></a>函数和模块

任何 F# 程序的最基本的片段都是由***函数***组织成的***模块***。  [函数](./language-reference/functions/index.md)会处理输入并产生输出，并被组织到[模块](./language-reference/modules.md)中，模块是在 F # 中对事物进行归组的主要方式。  它们是使用[`let`绑定](./language-reference/functions/let-bindings.md)定义对的，后者为函数提供一个名称并定义其参数。

[!code-fsharp[BasicFunctions](../../samples/snippets/fsharp/tour.fs#L101-L133)]

`let` 绑定也是将值绑定到名称的方式，类似于其他语言中的变量。  默认情况下`let` 绑定是***不可变***的，这意味着，一旦值或函数绑定到一个名称，它不能在原位更改。  这与在其他语言中的变量相反，这些变量是***可变的***，意味着它们的值可以在任何位置任何时间被更改。  如果需要一个可变的绑定，可以使用 `let mutable ...` 语法。

[!code-fsharp[Immutability](../../samples/snippets/fsharp/tour.fs#L75-L94)]

## <a name="numbers-booleans-and-strings"></a>数值、布尔值和字符串

F# 是一种 .NET 语言，支持 .NET 中包含的相同的基本[基元类型](./language-reference/primitive-types.md)。

下面是各种数值类型在 F# 中的表示方式：

[!code-fsharp[Numbers](../../samples/snippets/fsharp/tour.fs#L49-L68)]

下面是布尔值的表示和基本条件逻辑的执行方式：

[!code-fsharp[Bools](../../samples/snippets/fsharp/tour.fs#L142-L152)]

下面是[字符串](./language-reference/strings.md)的基本操作方式：

[!code-fsharp[Strings](../../samples/snippets/fsharp/tour.fs#L158-L180)]

## <a name="tuples"></a>元组

[元组](./language-reference/tuples.md)是 F# 中的重要内容。  它们是一组未命名但已排序的值，可将其视为值进行处理。  将它们视为聚合自其他值的值。  元组有许多用途，比如，以便捷方式从函数返回多个值，或对值进行分组以提供暂时的便利。

[!code-fsharp[Tuples](../../samples/snippets/fsharp/tour.fs#L186-L203)]

从 F# 4.1 开始，还可以创建 `struct` 元组。  它们可以与 C# 7/Visual Basic 15 元组完全交互，因为后者也是 `struct` 元组：

[!code-fsharp[Tuples](../../samples/snippets/fsharp/tour.fs#L205-L218)]

请务必注意，由于 `struct` 元组是值类型，它们不能隐式转换为引用元组，反之亦然。  必须在引用元组和 struct 元组之间进行显式转换。

## <a name="pipelines-and-composition"></a>管道和组合

在 F# 中处理数据时，会广泛使用 `|>` 等管道运算符。 这些运算符是使你能够灵活建立函数的“管道”的函数。 下面的示例将完整演示如利用这些运算符来构建一个简单的功能管道：

[!code-fsharp[Pipelines](../../samples/snippets/fsharp/tour.fs#L227-L282)]

上面的示例使用了 F# 的许多特性，包括列表处理函数、头等函数和[偏函数应用](./language-reference/functions/index.md#partial-application-of-arguments)。 尽管深入理解所有这些概念有难度，但有一点应该非常明显 - 在构建管道时可以轻松使用函数来处理数据。

## <a name="lists-arrays-and-sequences"></a>列表、数组和序列

列表、数组和序列是 F# 核心库中的三个主要集合类型。

[列表](./language-reference/lists.md)是相同类型元素的有序、不可变集合。  “列表”是单向链接列表，即它们旨在用于枚举，较大时则不适合用于随机访问和串联。  请注意，这与其他常用语言中的“列表”相反，那些语言通常不使用单向链接列表表示“列表”。

[!code-fsharp[Lists](../../samples/snippets/fsharp/tour.fs#L309-L359)]

[数组](./language-reference/arrays.md)是具有相同类型的元素的固定大小、*可变*集合。  它们支持快速随机访问的元素，并不是 F# 列表，因为它们是只需连续内存块的速度更快。

[!code-fsharp[Arrays](../../samples/snippets/fsharp/tour.fs#L368-L407)]

[序列](./language-reference/sequences.md)是一系列逻辑元素, 它们都属于同一类型。  这些是比列表和数组更通用的类型, 可以是 "视图" 到任何逻辑序列的元素。  它们还会显得很明显, 因为它们可能是***延迟***的, 也就是说, 仅当需要时才可以计算元素。

[!code-fsharp[Sequences](../../samples/snippets/fsharp/tour.fs#L418-L452)]

## <a name="recursive-functions"></a>递归函数

在 F# 中，对元素集合与元素序列的操作往往通过[递归](./language-reference/functions/index.md#recursive-functions)完成。  尽管 F# 支持循环和命令式编程，但递归仍然是首选，因为它更容易保证正确性。

> [!NOTE]
> 下面的示例利用了通过 `match` 表达式匹配的模式。  本文后面部分将介绍这一构造。

[!code-fsharp[RecursiveFunctions](../../samples/snippets/fsharp/tour.fs#L461-L500)]

F# 还完全支持尾调用优化，这是一种优化递归调用并使其与循环构造具有相同速率的方式。

## <a name="record-and-discriminated-union-types"></a>记录和可区分联合类型

“记录”和“联合”是 F# 代码中使用的两种基本数据类型，它们通常是表示 F# 程序中数据的最佳方式。  尽管在这一点上它们与其他语言中的类很相似，但它们具有结构相等性语义，这是一个主要差异。  这意味着它们“天生”就可比较，相等性则非常简单 - 只需检查一项是否等于另一项。

[记录](./language-reference/records.md)是包含成员（例如，方法）的命名值的聚合。  如果熟悉 C# 或 Java，便会发现“记录”类似于 POCO 或 POCO - 只是比它们多了结构相等性，而且更易于使用。

[!code-fsharp[Records](../../samples/snippets/fsharp/tour.fs#L507-L559)]

从 F# 4.1 开始，还可以将“记录”表示为 `struct`。  此操作通过 `[<Struct>]` 属性实现：

[!code-fsharp[Records](../../samples/snippets/fsharp/tour.fs#L561-L568)]

[可区分联合 (DU)](./language-reference/discriminated-unions.md) 是一些值，可能是大量的已命名窗体或事例。  存储的该类型的值可能是多个非重复值之一。

[!code-fsharp[Unions](../../samples/snippets/fsharp/tour.fs#L575-L631)]

你还可以使用 Du 作为*单用例可区分联合*, 以帮助进行基于基元类型的域建模。  通常情况下, 字符串和其他基元类型用于表示某些内容, 因此具有特定的含义。  但是, 仅使用数据的基元表示形式可能会导致错误地分配不正确的值!  将每种类型的信息表示为不同的单用例联合可在这种情况下强制执行正确性。

[!code-fsharp[Unions](../../samples/snippets/fsharp/tour.fs#L633-L654)]

如上面的示例所示，若要获取单用例 DU 的基础值，则必须显式将其解包。

此外，DU 还支持递归定义，使你可以轻松地表示树和本质上的递归数据。  例如，下面演示了如何使用 `exists` 和 `insert` 函数表示二进制文件搜索树。

[!code-fsharp[Unions](../../samples/snippets/fsharp/tour.fs#L656-L683)]

由于 DU 可以表示该数据类型的树中的递归结构，因此对此类递归结构执行操作非常简单并且能保证正确性。  模式匹配中也支持此方法，如下所示。

此外，可以利用 `[<Struct>]` 属性将 DU 表示为 `struct`：

[!code-fsharp[Unions](../../samples/snippets/fsharp/tour.fs#L685-L696)]

但是，执行此操作时要牢记以下两个关键事项：

1. struct DU 不能以递归方式定义。
2. struct DU 的每个事例必须具有唯一的标识符。

未能遵循上述注意事项将导致编译错误。

## <a name="pattern-matching"></a>模式匹配

[模式匹配](./language-reference/pattern-matching.md)是 F# 语言的特性，可确保对 F# 类型执行操作时的正确性。  在上述示例中，你可能已经注意到了很多 `match x with ...` 语法。  使用某个数据类型时，此构造可允许编译器（可以理解数据类型的“形状”）通过所谓的穷举模式匹配来强制你考虑所有可能出现的情况。  此方法能有效确保正确性，可以将通常在运行时考虑的问题引入编译时。

[!code-fsharp[PatternMatching](../../samples/snippets/fsharp/tour.fs#L705-L742)]

你可能注意到的是使用`_`模式。  这称为[通配符模式](./language-reference/pattern-matching.md#wildcard-pattern), 这是一种 "我不在意什么内容" 的方法。  尽管很方便, 但如果不小心使用`_`, 则可能会意外绕过穷举模式匹配, 并且不再受益于编译时操作。  当您在模式匹配时不关心分解类型的某些部分时, 最好使用此方法; 当您枚举了模式匹配表达式中的所有有意义的事例时, 最好使用该方法。

[活动模式](./language-reference/active-patterns.md)是另一个功能强大的构造, 可与模式匹配一起使用。  它们允许您将输入数据分区为自定义窗体, 并在模式匹配调用站点分解它们。  它们也可以参数化, 从而允许将分区定义为函数。  扩展前面的示例以支持活动模式, 如下所示:

[!code-fsharp[ActivePatterns](../../samples/snippets/fsharp/tour.fs#L764-L786)]

## <a name="optional-types"></a>可选类型

可区分联合类型的一个特殊情况是选项类型，这是很有用，它是 F# 核心库的一部分。

[选项类型](./language-reference/options.md)是一种类型, 该类型表示以下两种情况之一: 值或根本不显示任何内容。  它用于某个值可能因特定操作而不会产生的任何情况。  这会强制你考虑这两种情况, 使其成为编译时问题, 而不是运行时问题。  这通常用于 api 中, 其中`null`用于表示 "无", 从而避免了`NullReferenceException`在许多情况下需要担心的情况。

[!code-fsharp[Options](../../samples/snippets/fsharp/tour.fs#L789-L814)]

## <a name="units-of-measure"></a>度量单位

F# 类型系统的一项独特功能是能够为通过度量单位的数字文本提供上下文。

[度量单位](./language-reference/units-of-measure.md)允许您将数值类型与单位 (例如计量) 相关联, 并使函数可对单元 (而不是数字文本) 执行工作。  这使编译器能够验证传入的数值类型在特定上下文中是否有效, 从而消除了与此类工作相关的运行时错误。

[!code-fsharp[UnitsOfMeasure](../../samples/snippets/fsharp/tour.fs#L817-L842)]

F# 核心库定义了许多的 SI 单位类型和单位转换。  若要了解详细信息, 请查看[Microsoft.FSharp.Data.UnitSystems.SI 命名空间](https://msdn.microsoft.com/visualfsharpdocs/conceptual/microsoft.fsharp.data.unitsystems.si-namespace-%5bfsharp%5d)。

## <a name="classes-and-interfaces"></a>类和接口

F# 还具有对.NET 类的完全支持[接口](./language-reference/interfaces.md)，[抽象类](./language-reference/abstract-classes.md)，[继承](./language-reference/inheritance.md)，依次类推。

[类](./language-reference/classes.md)是表示 .net 对象的类型, 这些对象可以具有属性、方法和事件作为其[成员](./language-reference/members/index.md)。

[!code-fsharp[Classes](../../samples/snippets/fsharp/tour.fs#L845-L880)]

定义泛型类也非常简单。

[!code-fsharp[Classes](../../samples/snippets/fsharp/tour.fs#L883-L908)]

若要实现接口, 可以使用`interface ... with`语法或[对象表达式](./language-reference/object-expressions.md)。

[!code-fsharp[Classes](../../samples/snippets/fsharp/tour.fs#L911-L934)]

## <a name="which-types-to-use"></a>要使用的类型

类、记录、可区分联合和元组的存在导致了重要问题: 应使用哪一个？  与生活中的大多数操作一样, 答案取决于你的情况。

元组非常适合从函数返回多个值, 并使用临时值聚合作为值本身。

记录是元组中的 "单步执行", 其命名标签和对可选成员的支持。  它们非常适用于通过您的程序传输的数据的低计划表示形式。  由于它们具有结构相等性, 因此它们可用于比较。

可区分联合具有许多用途, 但核心好处是能够将它们与模式匹配一起使用, 以考虑数据可以具有的所有可能的 "形状"。  

类对于大量原因非常有用, 例如, 当你需要表示信息并将该信息绑定到功能时。  作为经验法则, 当你具有在概念上与某些数据关联的功能时, 使用类和面向对象编程的原则是一项巨大的好处。  与C#和 Visual Basic 互操作时, 类也是首选的数据类型, 因为这些语言几乎都使用类。

## <a name="next-steps"></a>后续步骤

现在，已了解的一些主要功能的语言，您应准备好开始编写第一个 F# 程序 ！  请查看[入门](./tutorials/getting-started/index.md), 了解如何设置开发环境并编写一些代码。

用于了解详细信息的后续步骤可以是你喜欢的任何内容, 但建议你[在中F#介绍函数编程](./introduction-to-functional-programming/index.md), 以熟悉核心功能编程概念。  这些将是在中构建 F# 中的可靠程序必不可少。

此外，请查看[F# 语言参考](./language-reference/index.md)若要查看有关 F# 的概念内容全面集合。
