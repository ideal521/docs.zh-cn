---
title: 访问控制
description: 了解如何以F#编程语言控制对编程元素 (如类型、方法和函数) 的访问。
ms.date: 05/16/2016
ms.openlocfilehash: ed77a09cf87aabf9a4134276e89e84aa42abd3c3
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2019
ms.locfileid: "68629968"
---
# <a name="access-control"></a>访问控制

*访问控制*是指声明哪些客户端可以使用某些程序元素, 例如类型、方法和函数。

## <a name="basics-of-access-control"></a>访问控制基础知识

在F#中, 访问控制说明符`public`、 `internal`和`private`可应用于模块、类型、方法、值定义、函数、属性和显式字段。

- `public`指示所有调用方都可以访问该实体。

- `internal`指示只能从同一程序集访问实体。

- `private`指示只能从封闭类型或模块中访问实体。

> [!NOTE]
> 访问说明符不`protected`在中F#使用, 但如果您使用的是用支持`protected`访问的语言编写的类型, 则可以接受访问说明符。 因此, 如果你重写受保护的方法, 则方法只能在类及其子代内访问。

通常, 说明符放置在实体名称之前, 除非`mutable`使用或`inline`说明符, 后者显示在访问控制说明符之后。

如果未使用访问说明符, 则默认值为`public`, `let`但类型中的绑定 (始终`private`为类型) 除外。

中的F#签名提供了另一种机制F#来控制对程序元素的访问。 访问控制不需要签名。 有关详细信息，请参阅[签名](signatures.md)。

## <a name="rules-for-access-control"></a>访问控制规则

访问控制遵循以下规则:

- 继承声明 (即, 使用`inherit`来指定类的基类)、接口声明 (即指定类实现接口) 和抽象成员始终具有与封闭类型相同的可访问性。 因此, 不能对这些构造使用访问控制说明符。

- 可区分联合中各个事例的可访问性取决于可区分联合本身的可访问性。 也就是说, 特定联合用例的可访问性不如联合本身。

- 记录类型的单个字段的可访问性不能由记录本身的可访问性决定。 也就是说, 特定记录标签的可访问性比记录本身的可访问性低。

## <a name="example"></a>示例

下面的代码演示如何使用访问控制说明符。 项目中有两个文件, 即`Module1.fs`和`Module2.fs`。 每个文件都是隐式的模块。 因此, 有两个模块: `Module1`和`Module2`。 私有类型和内部类型在中`Module1`定义。 无法从`Module2`访问私有类型, 但内部类型可以。

[!code-fsharp[Main](~/samples/snippets/fsharp/access-control/snippet1.fs)]

下面的代码测试在中`Module1.fs`创建的类型的可访问性。

[!code-fsharp[Main](~/samples/snippets/fsharp/access-control/snippet2.fs)]

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [签名](signatures.md)
