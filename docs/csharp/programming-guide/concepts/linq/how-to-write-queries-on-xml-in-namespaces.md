---
title: 如何：针对命名空间中的 XML 编写查询 (C#)
ms.date: 07/20/2015
ms.assetid: 7c54df81-15e4-4091-8c81-a87637029130
ms.openlocfilehash: d33ecc22d8eb6ea4a08b56fbed6b6b437a5e3216
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2019
ms.locfileid: "66484641"
---
# <a name="how-to-write-queries-on-xml-in-namespaces-c"></a>如何：针对命名空间中的 XML 编写查询 (C#)
若要针对命名空间中的 XML 编写查询，必须使用具有正确命名空间的 <xref:System.Xml.Linq.XName> 对象。  
  
 对于 C#，最常用的方法是使用包含 URI 的字符串初始化 <xref:System.Xml.Linq.XNamespace>，然后使用加法运算符重载来组合命名空间和本地名称。  
  
 本主题的第一个示例集演示如何在默认命名空间中创建一个 XML 树。 第二个示例集演示如何在带有前缀的命名空间中创建一个 XML 树。  
  
## <a name="example"></a>示例  
 下面的示例创建一个位于默认命名空间中的 XML 树。 然后检索元素的集合。  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = XElement.Parse(  
@"<Root xmlns='http://www.adventure-works.com'>  
    <Child>1</Child>  
    <Child>2</Child>  
    <Child>3</Child>  
    <AnotherChild>4</AnotherChild>  
    <AnotherChild>5</AnotherChild>  
    <AnotherChild>6</AnotherChild>  
</Root>");  
IEnumerable<XElement> c1 =  
    from el in root.Elements(aw + "Child")  
    select el;  
foreach (XElement el in c1)  
    Console.WriteLine((int)el);  
```  
  
 该示例产生下面的输出：  
  
```  
1  
2  
3  
```  
  
## <a name="example"></a>示例  
 在 C# 中，无论是在使用带前缀的命名空间的 XML 树上编写查询，还是在使用默认命名空间的 XML 树上编写查询，都使用相同的方式。  
  
 下面的示例创建一个位于具有前缀的默认命名空间中的 XML 树。 然后检索元素的集合。  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = XElement.Parse(  
@"<aw:Root xmlns:aw='http://www.adventure-works.com'>  
    <aw:Child>1</aw:Child>  
    <aw:Child>2</aw:Child>  
    <aw:Child>3</aw:Child>  
    <aw:AnotherChild>4</aw:AnotherChild>  
    <aw:AnotherChild>5</aw:AnotherChild>  
    <aw:AnotherChild>6</aw:AnotherChild>  
</aw:Root>");  
IEnumerable<XElement> c1 =  
    from el in root.Elements(aw + "Child")  
    select el;  
foreach (XElement el in c1)  
    Console.WriteLine((int)el);  
```  
  
 该示例产生下面的输出：  
  
```  
1  
2  
3  
```  
  
## <a name="see-also"></a>请参阅

- [使用 XML 命名空间 (C#)](../../../../csharp/programming-guide/concepts/linq/namespaces-overview-linq-to-xml.md)
