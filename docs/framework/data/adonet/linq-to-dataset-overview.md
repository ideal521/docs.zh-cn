---
title: LINQ to DataSet 概述
ms.date: 03/30/2017
ms.assetid: dc20a8fb-03f6-4b68-9c2b-7f7299e3070b
ms.openlocfilehash: f60308b122841421613d8e1f84aa5b9a23cc3315
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67504437"
---
# <a name="linq-to-dataset-overview"></a>LINQ to DataSet 概述
<xref:System.Data.DataSet>是 ADO.NET 的更广泛使用的组件之一。 它是 ADO.NET 所基于的断开连接的编程模型的关键元素，它可以显式缓存不同数据源中。 在表示层上，<xref:System.Data.DataSet> 与 GUI 控件紧密集成，以进行数据绑定。 在中间层上，它提供保留数据关系形状的缓存并包括快速简单查询和层次结构导航服务。 用于减少对数据库的请求数的常用技术是使用 <xref:System.Data.DataSet> 以便在中间层进行缓存。 例如，考虑数据驱动的 ASP.NET Web 应用程序。 通常，应用程序的绝大部分数据不会经常更改，属于会话之间或用户之间的公共数据。 此数据可以保存在 Web 服务器的内存中，这会减少对数据库的请求数并加速用户的交互。 另一个有用特征的<xref:System.Data.DataSet>是它允许应用程序到应用程序空间从一个或多个数据源将数据子集。 然后，应用程序可以在内存中操作这些数据，同时保留其关系形状。  
  
 <xref:System.Data.DataSet> 虽然具有突出的优点，但其查询功能也存在限制。 <xref:System.Data.DataTable.Select%2A> 方法可用于筛选和排序，<xref:System.Data.DataRow.GetChildRows%2A> 和 <xref:System.Data.DataRow.GetParentRow%2A> 方法可用于层次结构导航。 但对于更复杂的情况，开发人员必须编写自定义查询。 这会使应用程序性能低下并且难以维护。  
  
 LINQ 到数据集可以更轻松和更快地对数据执行查询缓存在<xref:System.Data.DataSet>对象。 这些查询用编程语言本身表示，而不表示为嵌入在应用程序代码中的字符串。 这意味着开发人员不必学习单独的查询语言。 此外，LINQ to DataSet 使 Visual Studio 开发人员工作效率更高，因为 Visual Studio IDE 提供编译时语法检查、 静态类型化和 IntelliSense 支持[!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)]。 此外可以使用 LINQ to DataSet 对已从一个或多个数据源合并的数据执行查询。 这可以使许多需要灵活表示和处理数据的方案能够实现。 具体地说，一般报告、分析和业务智能应用程序将需要这种操作方法。  
  
## <a name="querying-datasets-using-linq-to-dataset"></a>使用 LINQ to DataSet 查询数据集  
 您可以开始查询之前<xref:System.Data.DataSet>对象使用 LINQ to DataSet，您必须填充<xref:System.Data.DataSet>。 有几种方法将数据加载到<xref:System.Data.DataSet>，例如，使用<xref:System.Data.Common.DataAdapter>类或[LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md)。 将数据加载到 <xref:System.Data.DataSet> 对象后，可以开始查询数据。 系统地阐明使用 LINQ to DataSet 查询是类似于使用[!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)]对其他[!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)]-启用数据源。 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 可以针对中的单个表执行查询<xref:System.Data.DataSet>或通过使用多个表针对<xref:System.Linq.Enumerable.Join%2A>和<xref:System.Linq.Enumerable.GroupJoin%2A>标准查询运算符。  
  
 支持对类型化和非类型化 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 对象执行 <xref:System.Data.DataSet> 查询。 如果在应用程序设计时已知 <xref:System.Data.DataSet> 的架构，则建议使用类型化 <xref:System.Data.DataSet>。 在类型化 <xref:System.Data.DataSet> 中，表和行对每个列都具有类型化成员，从而使查询更简单并且更具可读性。  
  
 除了 System.Core.dll 中实现的标准查询运算符，LINQ to DataSet 添加了多种<xref:System.Data.DataSet>的特定扩展，使其能够更轻松地查询一组<xref:System.Data.DataRow>对象。 这些 <xref:System.Data.DataSet> 特定扩展包括用于比较行序列的运算符以及用于访问 <xref:System.Data.DataRow> 的列值的方法。  
  
## <a name="n-tier-applications-and-linq-to-dataset"></a>N 层应用程序和 LINQ to DataSet  
 N 层数据应用程序是以数据为中心的应用程序，分为多个逻辑层（或层）。 典型的 N 层应用程序包括一个表示层、一个中间层和一个数据层。 将应用程序组件分离到不同的层可提高应用程序的可维护性和可伸缩性。 有关 N 层数据应用程序的详细信息，请参阅[使用 n 层应用程序中的数据集](/visualstudio/data-tools/work-with-datasets-in-n-tier-applications)。  
  
 在 N 层应用程序中，<xref:System.Data.DataSet> 通常用于中间层以缓存 Web 应用程序的信息。 LINQ to DataSet 查询功能通过扩展方法实现和扩展现有的 ADO.NET 2.0 <xref:System.Data.DataSet>。  
  
## <a name="see-also"></a>请参阅

- [查询数据集](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md)
- [语言集成查询 (LINQ) - C#](../../../csharp/programming-guide/concepts/linq/index.md)
- [语言集成查询 (LINQ) - Visual Basic](../../../visual-basic/programming-guide/concepts/linq/index.md)
- [LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md)
