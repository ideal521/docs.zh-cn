---
title: 在 Visual Studio 中创建一个 WPF 应用程序
ms.date: 03/20/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- getting started [WPF], WPF
- WPF [WPF], getting started
ms.assetid: b96bed40-8946-4285-8fe4-88045ab854ed
author: mairaw
ms.author: mairaw
ms.custom: vs-dotnet
ms.openlocfilehash: c3440ddf6cdae6b24bcf1059ab2c76d8fb957263
ms.sourcegitcommit: 11deacc8ec9f229ab8ee3cd537515d4c2826515f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66003856"
---
# <a name="walkthrough-my-first-wpf-desktop-application"></a>演练：我的第一个 WPF 桌面应用程序

本文介绍如何开发包括元素所共有的大多数 WPF 应用程序的 Windows Presentation Foundation (WPF) 桌面应用程序：Extensible Application Markup Language (XAML) 标记、 代码隐藏、 应用程序定义、 控件、 布局、 数据绑定和样式。 若要开发应用程序，您将使用 Visual Studio。 

本演练包含以下步骤：

- 使用 XAML 来设计应用程序的用户界面 (UI) 的外观。

- 编写代码以生成应用程序的行为。

- 创建应用程序定义管理应用程序。

- 将控件添加和创建布局以构成应用程序 UI。

- 创建应用程序的 UI 具有一致外观的样式。

- 绑定到数据，来填充数据从 UI 并保留数据和 UI 同步的用户界面。

本演练结束时，你将生成独立的 Windows 应用程序，允许用户查看所选人员的费用报表。 应用程序的托管在浏览器样式的窗口中的多个 WPF 页面组成。

> [!TIP]
> 用于生成此演练的示例代码是适用于这两个 Visual Basic 和C#处[演练 WPF 应用程序示例代码](https://github.com/Microsoft/WPF-Samples/tree/master/Getting%20Started/WalkthroughFirstWPFApp)。
>
> 您可以切换之间的示例代码的代码语言C#和使用 Visual Basic **\< />** 这篇文章右上角的下拉列表。

## <a name="prerequisites"></a>系统必备

- （本文使用 Visual Studio 2019） 的 visual Studio 2017 或更高版本

   有关安装 Visual Studio 的最新版本的详细信息，请参阅[安装 Visual Studio](/visualstudio/install/install-visual-studio)。

## <a name="create-the-application-project"></a>创建应用程序项目

第一步是创建应用程序基础结构，其中包括应用程序定义，两个页面和一个图像。

1. 在 Visual Basic 或 Visual C# 名为创建新的 WPF 应用程序项目 **`ExpenseIt`** :

   1. 打开 Visual Studio 并选择**创建一个新项目**下**开始**菜单。

      **创建一个新项目**对话框随即打开。

   2. 在中**语言**下拉列表中，选择**C#** 或**Visual Basic**。
      
   3. 选择**WPF 应用 (.NET Framework)** 模板，然后选择**下一步**。 
     
      ![创建新项目对话框](./media/walkthrough-my-first-wpf-desktop-application/create-new-project-dialog.png)
    
      **配置新项目**对话框随即打开。

   4. 输入项目名称 **`ExpenseIt`** ，然后选择**创建**。

      ![配置新项目对话框](./media/walkthrough-my-first-wpf-desktop-application/configure-new-project-dialog.png)

      Visual Studio 创建项目并打开名为的默认应用程序窗口的设计器**MainWindow.xaml**。

2. 打开*Application.xaml* (Visual Basic) 或*App.xaml* (C#)。

    此 XAML 文件定义 WPF 应用程序和任何应用程序资源。 此外使用此文件来指定 UI 中，在这种情况下*MainWindow.xaml*，应用程序启动时自动显示。

    在 XAML 应如下所示在 Visual Basic 中所示：

    [!code-xaml[ExpenseIt#1_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/Application.xaml#1_a)]

    和类似中的以下C#:

    [!code-xaml[ExpenseIt#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/App.xaml#1)]

3. 打开*MainWindow.xaml*。

    此 XAML 文件是你的应用程序的主窗口，并显示在页面中创建的内容。 <xref:System.Windows.Window>类定义的属性窗口中，例如其标题、 大小或图标，并处理事件，例如关闭或隐藏。

4. 更改<xref:System.Windows.Window>元素<xref:System.Windows.Navigation.NavigationWindow>，如以下 XAML 所示：

   ```xaml
   <NavigationWindow x:Class="ExpenseIt.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        ...
   </NavigationWindow>
   ```

   此应用程序中导航到不同的内容，具体取决于用户输入。 这就是为什么主要<xref:System.Windows.Window>需要更改为<xref:System.Windows.Navigation.NavigationWindow>。 <xref:System.Windows.Navigation.NavigationWindow> 继承的所有属性<xref:System.Windows.Window>。 <xref:System.Windows.Navigation.NavigationWindow> XAML 文件中的元素创建的实例<xref:System.Windows.Navigation.NavigationWindow>类。 有关详细信息，请参阅[导航概述](../app-development/navigation-overview.md)。

5. 删除<xref:System.Windows.Controls.Grid>元素从之间<xref:System.Windows.Navigation.NavigationWindow>标记。

6. 更改下列属性的 XAML 代码中<xref:System.Windows.Navigation.NavigationWindow>元素：

    - 设置<xref:System.Windows.Window.Title%2A>属性设置为"`ExpenseIt`"。

    - 设置<xref:System.Windows.FrameworkElement.Height%2A>属性设置为 350 像素。

    - 设置<xref:System.Windows.FrameworkElement.Width%2A>属性设置为 500 像素。

    在 XAML 应如下所示适用于 Visual Basic:

    [!code-xaml[ExpenseIt#2_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt/MainWindow.xaml#2_a)]

    并如下所示的C#:

    [!code-xaml[ExpenseIt#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/MainWindow.xaml#2)]

7. 打开*MainWindow.xaml.vb*或*MainWindow.xaml.cs*。

    此文件是包含代码来处理中声明的事件的代码隐藏文件*MainWindow.xaml*。 此文件包含在 XAML 中定义的窗口的分部类。

8. 如果您使用的C#，更改`MainWindow`类派生自<xref:System.Windows.Navigation.NavigationWindow>。 （在 Visual Basic 中，自动发生此情况更改 XAML 中的窗口。）在C#代码现在应如下所示：

   [!code-csharp[ExpenseIt#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/MainWindow.xaml.cs?highlight=21)]

## <a name="add-files-to-the-application"></a>将文件添加到应用程序

本部分将向应用程序添加两个页面和一个图像。

1. 将新页面添加到项目中，并将其命名 *`ExpenseItHome.xaml`* :

   1. 在中**解决方案资源管理器**，右键单击 **`ExpenseIt`** 项目节点，然后选择**添加** > **页**。

   1. 在中**添加新项**对话框中，**页面 (WPF)** 尚未选择模板。 输入的名称 **`ExpenseItHome`** ，然后选择**添加**。

    此页是应用程序启动时显示的第一页。 它将显示要从中，以查看其费用报表的人员列表。

1. 打开 *`ExpenseItHome.xaml`* 。

1. 设置<xref:System.Windows.Controls.Page.Title%2A>到"`ExpenseIt - Home`"。

1. 设置`DesignHeight`和`DesignWidth`元素值为 300 像素。

    XAML 现在将出现，如下所示的 Visual Basic:

    [!code-xaml[ExpenseIt#6_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseItHome.xaml#6_a)]

    并如下所示的C#:

    [!code-xaml[ExpenseIt#6](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt2/ExpenseItHome.xaml#6)]

1. 打开*MainWindow.xaml*。

1. 添加<xref:System.Windows.Navigation.NavigationWindow.Source%2A>属性设置为<xref:System.Windows.Navigation.NavigationWindow>元素并将其设置为"`ExpenseItHome.xaml`"。

    这将设置 *`ExpenseItHome.xaml`* 的第一页时打开应用程序启动。 

    在 Visual Basic 中的 XAML 的示例：

    [!code-xaml[ExpenseIt#7_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/MainWindow.xaml#7_a)]

    和 C# 中：

    [!code-xaml[ExpenseIt#7](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt2/MainWindow.xaml#7)]

   > [!TIP]
   > 您还可以设置**源**属性中的**杂项**类别**属性**窗口。
   >
   > ![在属性窗口中的源属性](./media/properties-source.png)

1. 将另一个新的 WPF 页添加到项目中，并将其命名*ExpenseReportPage.xaml*::

   1. 在中**解决方案资源管理器**，右键单击 **`ExpenseIt`** 项目节点，然后选择**添加** > **页**。

   1. 在中**添加新项**对话框中，选择**页面 (WPF)** 模板。 输入的名称**ExpenseReportPage**，然后选择**添加**。

    此页会显示费用报表上选择的人员 **`ExpenseItHome`** 页。

1. 打开 *ExpenseReportPage.xaml*。

1. 设置<xref:System.Windows.Controls.Page.Title%2A>到"`ExpenseIt - View Expense`"。

1. 设置`DesignHeight`和`DesignWidth`元素值为 300 像素。

    *ExpenseReportPage.xaml*现在如下所示在 Visual Basic 中：

    [!code-xaml[ExpenseIt#4_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseReportPage.xaml#4_a)]

    和类似中的以下C#:

    [!code-xaml[ExpenseIt#4](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/ExpenseReportPage.xaml#4)]

1. 打开*ExpenseItHome.xaml.vb*并*ExpenseReportPage.xaml.vb*，或*ExpenseItHome.xaml.cs*和*ExpenseReportPage.xaml.cs*.

    创建新的页面文件时，Visual Studio 将自动创建其*代码隐藏*文件。 这些代码隐藏文件处理响应用户输入的逻辑。

    你的代码应如以下所示 **`ExpenseItHome`** :

    [!code-csharp[ExpenseIt#2_5](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt2/ExpenseItHome.xaml.cs#2_5)]

    [!code-vb[ExpenseIt#2_5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseItHome.xaml.vb#2_5)]

    和类似如下针对**ExpenseReportPage**:

    [!code-csharp[ExpenseIt#5](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/ExpenseReportPage.xaml.cs#5)]

    [!code-vb[ExpenseIt#5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseReportPage.xaml.vb#5)]

1. 添加名为图像*watermark.png*到项目。 可以创建自己的映像、 将文件从示例代码中，或获取它[此处](https://github.com/Microsoft/WPF-Samples/tree/master/Getting%20Started/WalkthroughFirstWPFApp)。

    1. 右键单击项目节点并选择**外** > **现有项**，或按**Shift**+**Alt**+ **A**。

    2. 在中**添加现有项**对话框中，将文件筛选器设置为**的所有文件**或**映像文件**，浏览到你想要使用，并选择图像文件**添加**.

## <a name="build-and-run-the-application"></a>编译和运行应用程序

1. 若要生成并运行应用程序，按**F5**或选择**开始调试**从**调试**菜单。

    下图显示了与应用程序<xref:System.Windows.Navigation.NavigationWindow>按钮：

    ![应用程序后生成并运行它。](./media/walkthrough-my-first-wpf-desktop-application/build-run-application.png)

2. 关闭要返回到 Visual Studio 的应用程序。

## <a name="create-the-layout"></a>创建布局

布局提供有序的方式来放置 UI 元素，并调整 UI 时还管理的大小和这些元素的位置。 通常使用以下布局控件之一来创建布局：

- <xref:System.Windows.Controls.Canvas> -定义区域，在其中可显式定位子元素使用相对于画布区域的坐标。
- <xref:System.Windows.Controls.DockPanel> -定义一个区域，其中您可以排列子元素水平或垂直，相对于彼此。
- <xref:System.Windows.Controls.Grid> -定义列和行组成的灵活网格区域。
- <xref:System.Windows.Controls.StackPanel> -将子元素排列成水平或垂直的一行。
- <xref:System.Windows.Controls.VirtualizingStackPanel> -排列并显示方向是水平还是垂直的一行上的内容。
- <xref:System.Windows.Controls.WrapPanel> -定位子元素顺序位置从左到右，将内容切换到下一行上包含框的边缘。 后续排序按照按顺序从上到下还是从右到左，取决于 Orientation 属性的值。

适用于其子元素，每个布局控件支持特定类型的布局。 `ExpenseIt` 页面可进行调整，但每个页面不水平或垂直排列以及其他元素的元素。 在此示例中，<xref:System.Windows.Controls.Grid>用作应用程序布局元素。

> [!TIP]
> 有关详细信息<xref:System.Windows.Controls.Panel>元素，请参阅[面板概述](../controls/panels-overview.md)。 有关布局的详细信息，请参阅[布局](../advanced/layout.md)。

在本部分中，您创建的单列的表具有三个行和 10 像素边距通过添加到的列和行定义<xref:System.Windows.Controls.Grid>中 *`ExpenseItHome.xaml`* 。

1. 在中 *`ExpenseItHome.xaml`* ，将<xref:System.Windows.FrameworkElement.Margin%2A>属性上的<xref:System.Windows.Controls.Grid>"10,0,10,10"，对应于左侧、 顶部、 右侧和底部边距的元素：

   ```xaml
   <Grid Margin="10,0,10,10">
   ```

   > [!TIP]
   > 您还可以设置**边距**中的值**属性**窗口下**布局**类别：
   >
   > ![在属性窗口中的边距值](./media/properties-margin.png)

2. 添加以下 XAML 之间<xref:System.Windows.Controls.Grid>标记以创建行和列定义：

    [!code-xaml[ExpenseIt#8](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt3/ExpenseItHome.xaml#8)]

    <xref:System.Windows.Controls.RowDefinition.Height%2A>的两个行设置为<xref:System.Windows.GridLength.Auto%2A>，这意味着行大小将调整根据行中的内容。 默认值<xref:System.Windows.Controls.RowDefinition.Height%2A>是<xref:System.Windows.GridUnitType.Star>大小调整，这意味着行的高度可用空间的加权的比例。 例如，如果两个行具有<xref:System.Windows.Controls.RowDefinition.Height%2A>的"*"，它们都有高度将会是可用空间的一半。

    你<xref:System.Windows.Controls.Grid>现在应包含以下 XAML:

    [!code-xaml[ExpenseIt#9](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt3/ExpenseItHome.xaml#9)]

## <a name="add-controls"></a>添加控件

在本部分中，将更新主页 UI 以显示一组人员，您在其中选择一个人即可显示其费用报表。 控件是允许用户与应用程序交互的 UI 对象。 有关详细信息，请参阅 [控件](../controls/index.md)。

若要创建此 UI，将添加到以下元素 *`ExpenseItHome.xaml`* :

- 一个<xref:System.Windows.Controls.ListBox>（适用于的人员列表）。
- 一个<xref:System.Windows.Controls.Label>（用于列表标题）。
- 一个<xref:System.Windows.Controls.Button>（可以单击以在列表中选择的人员查看费用报表）。

每个控件的某一行中放置<xref:System.Windows.Controls.Grid>通过设置<xref:System.Windows.Controls.Grid.Row%2A?displayProperty=nameWithType>附加属性。 有关附加属性的详细信息，请参阅[附加属性概述](../advanced/attached-properties-overview.md)。

1. 在中 *`ExpenseItHome.xaml`* ，添加以下 XAML 某处之间<xref:System.Windows.Controls.Grid>标记：

   [!code-xaml[ExpenseIt#10](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt4/ExpenseItHome.xaml#10)]

   > [!TIP]
   > 此外可以通过将其从拖动来创建控件**工具箱**窗口拖到设计窗口中，然后设置其属性**属性**窗口。

2. 生成并运行应用程序。

    下图显示了你创建的控件：

![ExpenseIt 示例屏幕截图显示名称的列表](./media/walkthrough-my-first-wpf-desktop-application/add-application-controls.png)

## <a name="add-an-image-and-a-title"></a>添加图像和标题

在本部分中，将更新主页 UI 的图像和页面标题。

1. 在中 *`ExpenseItHome.xaml`* ，添加到另一个列<xref:System.Windows.Controls.Grid.ColumnDefinitions%2A>具有固定<xref:System.Windows.Controls.ColumnDefinition.Width%2A>为 230 像素：

    [!code-xaml[ExpenseIt#11](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseItHome.xaml?highlight=52-55)]

2. 添加到另一行<xref:System.Windows.Controls.Grid.RowDefinitions%2A>，总共四行：

    [!code-xaml[ExpenseIt#11b](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseItHome.xaml?highlight=57-62)]

3. 将控件移动到第二列中，通过设置<xref:System.Windows.Controls.Grid.Column%2A?displayProperty=nameWithType>为 1 的三个控件 （边框、 列表框中，和按钮） 每个属性。

4. 每个控件下移一行通过递增其<xref:System.Windows.Controls.Grid.Row%2A?displayProperty=nameWithType>值加 1 每三个控件 （边框、 列表框中，和按钮） 和 Border 元素。

   三个控件的 XAML 现在看起来如下所示：

    [!code-xaml[ExpenseIt#12](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#12)]

5. 设置<xref:System.Windows.Controls.Panel.Background%2A?displayProperty=nameWithType>属性设置为*watermark.png*图像文件，添加以下 XAML 任意位置之间`<Grid>`和`</Grid>`标记：

    [!code-xaml[ExpenseIt#14](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#14)]

6. 之前<xref:System.Windows.Controls.Border>元素中，添加<xref:System.Windows.Controls.Label>"查看费用报表"的内容。 此标签是页面的标题。

    [!code-xaml[ExpenseIt#13](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#13)]

7. 生成并运行应用程序。

下图显示了刚添加的结果：

![ExpenseIt 示例屏幕截图显示了新的图像背景和页标题](./media/walkthrough-my-first-wpf-desktop-application/add-application-image-title.png)

## <a name="add-code-to-handle-events"></a>添加代码以处理事件

1. 在中 *`ExpenseItHome.xaml`* ，添加<xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件处理程序<xref:System.Windows.Controls.Button>元素。 有关详细信息，请参阅[如何：创建一个简单的事件处理程序](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/bb675300(v=vs.100))。

    [!code-xaml[ExpenseIt#15](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt6/ExpenseItHome.xaml#15)]

2. 打开 *`ExpenseItHome.xaml.vb`* 或 *`ExpenseItHome.xaml.cs`* 。

3. 将以下代码添加到`ExpenseItHome`类添加一个按钮单击事件处理程序。 事件处理程序打开**ExpenseReportPage**页。

    [!code-csharp[ExpenseIt#16](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt6/ExpenseItHome.xaml.cs#16)]
    [!code-vb[ExpenseIt#16](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt6/ExpenseItHome.xaml.vb#16)]

## <a name="create-the-ui-for-expensereportpage"></a>为 ExpenseReportPage 创建 UI

*ExpenseReportPage.xaml*选择的人员显示费用报表 **`ExpenseItHome`** 页。 在本部分中，您将创建的用户界面**ExpenseReportPage**。 此外将添加背景和填充到各种 UI 元素的颜色。

1. 打开 *ExpenseReportPage.xaml*。

2. 添加以下 XAML 之间<xref:System.Windows.Controls.Grid>标记：

    [!code-xaml[ExpenseIt#17](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt6/ExpenseReportPage.xaml#17)]

    此用户界面是类似于 *`ExpenseItHome.xaml`* ，但报表数据显示在<xref:System.Windows.Controls.DataGrid>。

3. 生成并运行应用程序。

4. 选择**视图**按钮。

    出现费用报告页。 另请注意，启用向后导航按钮。

下图显示了添加到的 UI 元素*ExpenseReportPage.xaml*。

![ExpenseIt 示例屏幕截图显示刚刚为 ExpenseReportPage 创建 UI。](./media/walkthrough-my-first-wpf-desktop-application/create-application-ui.png)

## <a name="style-controls"></a>控件的样式

各种元素的外观通常是相同的 UI 中的相同类型的所有元素。 使用 UI[样式](../controls/styling-and-templating.md)以使外观可重复使用跨多个元素。 重复使用样式有助于简化 XAML 创建和管理。 本部分替换在以前步骤中通过样式定义的按元素划分的属性。

1. 打开*Application.xaml*或*App.xaml*。

2. 添加以下 XAML 之间<xref:System.Windows.Application.Resources%2A?displayProperty=nameWithType>标记：

    [!code-xaml[ExpenseIt#18](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt7/App.xaml#18)]

    此 XAML 将添加以下样式：

    - `headerTextStyle`：设置页标题的格式<xref:System.Windows.Controls.Label>。

    - `labelStyle`：若要设置格式<xref:System.Windows.Controls.Label>控件。

    - `columnHeaderStyle`：若要设置格式<xref:System.Windows.Controls.Primitives.DataGridColumnHeader>。

    - `listHeaderStyle`：若要设置列表标头的格式<xref:System.Windows.Controls.Border>控件。

    - `listHeaderTextStyle`：若要设置列表标头的格式<xref:System.Windows.Controls.Label>。

    - `buttonStyle`：若要设置格式<xref:System.Windows.Controls.Button>上`ExpenseItHome.xaml`。

    请注意，这些样式是资源和子级的<xref:System.Windows.Application.Resources%2A?displayProperty=nameWithType>属性元素。 在此位置中，这些样式将应用到应用程序中的所有元素。 在.NET 应用中使用的资源的示例，请参阅[使用应用程序资源](../advanced/how-to-use-application-resources.md)。

3. 在中 *`ExpenseItHome.xaml`* ，将为之间的所有内容<xref:System.Windows.Controls.Grid>具有以下 XAML 元素：

    [!code-xaml[ExpenseIt#19](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt7/ExpenseItHome.xaml#19)]

    应用样式会删除和替换定义每个控件外观的属性（如 <xref:System.Windows.VerticalAlignment> 和 <xref:System.Windows.Media.FontFamily> 。 例如，`headerTextStyle`应用于"查看费用报表" <xref:System.Windows.Controls.Label>。

4. 打开 *ExpenseReportPage.xaml*。

5. 替换之间的所有内容<xref:System.Windows.Controls.Grid>具有以下 XAML 元素：

    [!code-xaml[ExpenseIt#20](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt7/ExpenseReportPage.xaml#20)]

    此 XAML 将添加到样式<xref:System.Windows.Controls.Label>和<xref:System.Windows.Controls.Border>元素。

6. 生成并运行应用程序。 窗口外观是与以前相同。

    ![ExpenseIt 示例屏幕截图，其中相同的外观如下所示的最后一节。](./media/walkthrough-my-first-wpf-desktop-application/create-application-ui.png)

7. 关闭要返回到 Visual Studio 的应用程序。

## <a name="bind-data-to-a-control"></a>将数据绑定到控件

在本部分中，将创建绑定到各种控件的 XML 数据。

1. 在中 *`ExpenseItHome.xaml`* ，打开之后<xref:System.Windows.Controls.Grid>元素中，添加以下 XAML 以创建<xref:System.Windows.Data.XmlDataProvider>包含数据的每个用户：

    [!code-xaml[ExpenseIt#23](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml?range=13,16-40,49)]

    作为创建数据<xref:System.Windows.Controls.Grid>资源。 通常情况下会作为一个文件，加载此数据，但为简单起见数据添加内联。

2. 内`<Grid.Resources>`元素中，添加以下`<xref:System.Windows.DataTemplate>`元素，它定义如何显示中的数据<xref:System.Windows.Controls.ListBox>后，`<XmlDataProvider>`元素：

    [!code-xaml[ExpenseIt#24](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml?range=13,43-46,49)]

    有关数据模板的详细信息，请参阅[数据模板化概述](../data/data-templating-overview.md)。

3. 替换现有<xref:System.Windows.Controls.ListBox>使用以下 XAML:

    [!code-xaml[ExpenseIt#25](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml#25)]

    此 XAML 绑定<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>的属性<xref:System.Windows.Controls.ListBox>到数据源，并应用数据模板作为<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>。

## <a name="connect-data-to-controls"></a>将数据连接到控件

接下来，将添加代码以检索名称上所选 **`ExpenseItHome`** 页上，并将其传递给构造函数的**ExpenseReportPage**。 **ExpenseReportPage**设置与所传递的项目，这是定义的控件的数据上下文中*ExpenseReportPage.xaml*将绑定到。

1. 打开 *ExpenseReportPage.xaml.vb* 或 *ExpenseReportPage.xaml.cs*。

2. 添加获取对象的构造函数，以便传递所选人员的费用报表数据。

    [!code-csharp[ExpenseIt#26](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseReportPage.xaml.cs#26)]
    [!code-vb[ExpenseIt#26](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt8/ExpenseReportPage.xaml.vb#26)]

3. 打开 *`ExpenseItHome.xaml.vb`* 或 *`ExpenseItHome.xaml.cs`* 。

4. 更改<xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件处理程序以调用新的构造函数传递所选人员的费用报表数据。

    [!code-csharp[ExpenseIt#27](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml.cs#27)]
    [!code-vb[ExpenseIt#27](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt8/ExpenseItHome.xaml.vb#27)]

## <a name="style-data-with-data-templates"></a>使用数据模板的样式数据

在本部分中，将使用数据模板来更新数据绑定列表中每个项的 UI。

1. 打开 *ExpenseReportPage.xaml*。

2. 将"Name"和"部门"的内容绑定<xref:System.Windows.Controls.Label>元素到相应的数据源属性。 有关数据绑定的详细信息，请参阅[数据绑定概述](../data/data-binding-overview.md)。

    [!code-xaml[ExpenseIt#31](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseReportPage.xaml#31)]

3. 打开之后<xref:System.Windows.Controls.Grid>元素中，添加以下数据模板，用于定义如何显示费用报表数据：

    [!code-xaml[ExpenseIt#30](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseReportPage.xaml#30)]

4. 替换<xref:System.Windows.Controls.DataGridTextColumn>具有的元素<xref:System.Windows.Controls.DataGridTemplateColumn>下<xref:System.Windows.Controls.DataGrid>元素并将模板应用于它们。

    [!code-xaml[ExpenseIt#32](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseReportPage.xaml#32)]

5. 生成并运行应用程序。

6. 选择 person，然后选择**视图**按钮。

下图显示的两个页面`ExpenseIt`控件、 布局、 样式、 数据绑定和数据模板应用与应用程序：

![显示名称列表和费用报表应用程序的两个页面。](./media/walkthrough-my-first-wpf-desktop-application/application-data-templates.png)

> [!NOTE]
> 此示例演示了 WPF 的特定功能并不遵循所有最佳实践等安全、 本地化和可访问性。 WPF 和.NET 应用程序开发最佳做法的全面介绍，请参阅以下主题：
>
> - [辅助功能](../../ui-automation/accessibility-best-practices.md)
>
> - [安全性](../security-wpf.md)
>
> - [WPF 全球化和本地化](../advanced/wpf-globalization-and-localization-overview.md)
>
> - [WPF 性能](../advanced/optimizing-wpf-application-performance.md)

## <a name="next-steps"></a>后续步骤

在本演练中介绍了大量用于创建使用 Windows Presentation Foundation (WPF) UI 技术。 现在应具有一个基本的了解数据绑定的.NET 应用程序的构建基块。 有关 WPF 体系结构和编程模型的详细信息，请参阅以下主题：

- [WPF 体系结构](../advanced/wpf-architecture.md)
- [XAML 概述 (WPF)](../advanced/xaml-overview-wpf.md)
- [依赖属性概述](../advanced/dependency-properties-overview.md)
- [布局](../advanced/layout.md)

有关创建应用程序的详细信息，请参阅以下主题：

- [应用程序开发](../app-development/index.md)
- [控件](../controls/index.md)
- [数据绑定概述](../data/data-binding-overview.md)
- [图形和多媒体](../graphics-multimedia/index.md)
- [WPF 中的文档](../advanced/documents-in-wpf.md)

## <a name="see-also"></a>请参阅

- [面板概述](../controls/panels-overview.md)
- [数据模板化概述](../data/data-templating-overview.md)
- [生成 WPF 应用程序](../app-development/building-a-wpf-application-wpf.md)
- [样式和模板](../controls/styles-and-templates.md)
