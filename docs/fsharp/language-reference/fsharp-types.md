---
title: F# 类型
description: 了解中F#使用的类型以及如何F#命名和描述类型。
ms.date: 05/16/2016
ms.openlocfilehash: 44bd9d985e0ce1afa1bf2a8457dcd9470b13dfe1
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630229"
---
# <a name="f-types"></a>F# 类型

本主题介绍中F#使用的类型, 以及如何F#命名和描述类型。

## <a name="summary-of-f-types"></a>F#类型摘要
某些类型被视为*基元*类型 (如布尔类型`bool` ) 和各种大小的整型和浮点类型, 包括字节和字符的类型。 [基元类型](primitive-types.md)中描述了这些类型。

语言内置的其他类型包括元组、列表、数组、序列、记录和可区分联合。 如果你有其他 .NET 语言的经验并正在学习F#, 则应阅读每种类型的主题。 有关这些类型的详细信息的链接包含在本主题的 "[相关主题](https://msdn.microsoft.com/library/#rel)" 部分中。 这些F#特定类型支持函数编程语言通用的编程样式。 其中许多类型在F#库中具有相关联的模块, 这些模块支持这些类型的常见操作。

函数的类型包括有关参数类型和返回类型的信息。

.NET Framework 是对象类型、接口类型、委托类型和其他对象的源。 您可以定义自己的对象类型, 就像在任何其他 .NET 语言中一样。

此外, F#代码还可以定义别名, 它们是  类型的备用名称。 当类型将来可能会更改, 并且你希望避免更改依赖于类型的代码时, 你可以使用类型缩写。 或者, 您可以将类型缩写用作可使代码更易于阅读和理解的类型的友好名称。

F#提供了一些有用的集合类型, 这些类型在设计时需要考虑函数编程。 使用这些集合类型可帮助你编写更具样式的代码。 有关详细信息, 请参阅[ F#集合类型](fsharp-collection-types.md)。

## <a name="syntax-for-types"></a>类型的语法
在F#代码中, 通常必须写出类型的名称。 每个类型都有一个句法形式, 并且在类型注释、抽象方法声明、委托声明、签名和其他构造中使用这些语法形式。 每当在解释器中声明新的程序构造时, 解释器都将打印构造的名称及其类型的语法。 此语法可能只是用户定义类型的标识符或内置标识符 (如 for `int`或`string`) 的标识符, 但对于更复杂的类型, 语法更为复杂。

下表显示了类型的类型语法F#的各个方面。

|类型|类型语法|示例|
|----|-----------|--------|
|基元类型|*type-name*|`int`<br /><br />`float`<br /><br />`string`|
|聚合类型 (类、结构、联合、记录、枚举等)|*type-name*|`System.DateTime`<br /><br />`Color`|
|类型缩写|*type-abbreviation-name*|`bigint`|
|完全限定类型|*namespaces.type-name*<br /><br />或<br /><br />*modules.type-name*<br /><br />或<br /><br />*namespaces.modules.type-name*|`System.IO.StreamWriter`|
|array|*类型名称*[] 或<br /><br />*类型名称*数组|`int[]`<br /><br />`array<int>`<br /><br />`int array`|
|二维数组|*type-name*[,]|`int[,]`<br /><br />`float[,]`|
|三维数组|*type-name*[,,]|`float[,,]`|
|tuple|*类型-name1*&#42; *类型-name2* 。|例如, `(1,'b',3)`具有类型`int * char * int`|
|Generic Type — 泛型类型|*类型参数* *泛型类型名称*<br /><br />或<br /><br />*generic-type-name*&lt;*type-parameter-list*&gt;|`'a list`<br /><br />`list<'a>`<br /><br />`Dictionary<'key, 'value>`|
|构造类型 (提供了特定类型参数的泛型类型)|*类型实参* *泛型类型名称*<br /><br />或<br /><br />*generic-type-name*&lt;*type-argument-list*&gt;|`int option`<br /><br />`string list`<br /><br />`int ref`<br /><br />`option<int>`<br /><br />`list<string>`<br /><br />`ref<int>`<br /><br />`Dictionary<int, string>`|
|具有单个参数的函数类型|*parameter-type1* -&gt; *return-type*|一个函数, 它采用`int`并`string`返回具有类型`int -> string`|
|具有多个参数的函数类型|*参数-type1*  - 参数- - type2&gt; &gt; &gt;|一个函数, 它采用`int` `float`和并返回`string`具有类型`int -> float -> string`|
|高阶函数作为参数|(*函数类型*)|`List.map`具有类型`('a -> 'b) -> 'a list -> 'b list`|
|委托|*函数类型*的委托|`delegate of unit -> int`|
|灵活类型|#*type-name*|`#System.Windows.Forms.Control`<br /><br />`#seq<int>`|

## <a name="related-topics"></a>相关主题

|主题|描述|
|-----|-----------|
|[基元类型](primitive-types.md)|介绍内置简单类型, 如整型类型、布尔类型和字符类型。|
|[Unit 类型](unit-type.md)|描述类型, 该类型具有一个值, 并且由 () 指示, 后者与 Visual Basic `void`中C#的和`Nothing`相同。 `unit`|
|[元组](tuples.md)|描述元组类型, 一种类型, 该类型由以成对、三元组、可等分组的任何类型的关联值组成。|
|[选项](options.md)|描述选项类型, 该类型可能有值或为空。|
|[列表](lists.md)|描述列表, 这些列表是具有相同类型的已排序的不可变元素系列。|
|[数组](arrays.md)|描述数组, 数组是同一类型的有序的可变元素, 这些元素占用连续的内存块且大小固定。|
|[序列](sequences.md)|描述序列类型, 该类型表示一系列逻辑值;仅在必要时才计算各个值。|
|[记录](records.md)|描述命名值的一小部分记录类型。|
|[可区分联合](discriminated-unions.md)|描述可区分联合类型, 它的值可以是一组可能类型中的任何一种类型。|
|[函数](./functions/index.md)|描述函数值。|
|[类](classes.md)|描述类类型, 它是对应于 .NET 引用类型的对象类型。 类类型可以包含成员、属性、实现的接口和基类型。|
|[结构](structures.md)|`struct`描述类型, 该类型是与 .net 值类型相对应的对象类型。 `struct`类型通常表示一小部分数据。|
|[接口](interfaces.md)|介绍接口类型, 它们是表示一组成员的类型, 这些成员提供某些功能, 但不包含任何数据。 接口类型必须由对象类型实现才能发挥作用。|
|[委托](delegates.md)|描述委托类型, 该类型将函数表示为对象。|
|[枚举](enumerations.md)|描述枚举类型, 其值属于一组命名值。|
|[特性](attributes.md)|介绍用于指定另一种类型的元数据的特性。|
|[异常类型](/.exception-handling/exception-types.md)|描述用于指定错误信息的异常。|
