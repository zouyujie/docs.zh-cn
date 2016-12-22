---
title: "演练：用 COM 对象实现继承 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "基类, COM 可重用性"
  - "派生类, COM 可重用性"
  - "继承, COM 可重用性"
  - "继承, 演练"
ms.assetid: f8e7263a-de13-48d1-b67c-ca1adf3544d9
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 演练：用 COM 对象实现继承 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

可以从 COM 对象的 `Public` 类派生 Visual Basic 类，甚至是那些用 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 的早期版本创建的类。  可以重写或重载从 COM 对象继承的类的属性和方法，方式与重写或重载任何其他基类的属性和方法的方式相同。  当您拥有一个不想重新编译的现有类库时，从 COM 对象中继承是很有用的。  
  
 下面的过程说明如何使用 Visual Basic 6.0 创建包含类的 COM 对象，然后将它用作基类。  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### 生成在本演练中使用的 COM 对象  
  
1.  在 Visual Basic 6.0 中，打开一个新的 ActiveX DLL 项目。  则会创建名为 `Project1` 的项目。  它包含一个名为 `Class1` 的类。  
  
2.  在**“项目资源管理器”**中，右击**“Project1”**，再单击**“Project1 属性”**。  将显示**“项目属性”**对话框。  
  
3.  在**“项目属性”**对话框的**“常规”**选项卡上，通过在**“项目名称”**字段中键入 `ComObject1` 可更改该项目名称。  
  
4.  在**“项目资源管理器”**中，右击 `Class1`，再单击**“属性”**。  显示该类的**“属性”**窗口。  
  
5.  将 `Name` 属性更改为 `MathFunctions`。  
  
6.  在**“项目资源管理器”**中，右击 `MathFunctions`，再单击**“查看代码”**。  将显示**“代码编辑器”**。  
  
7.  添加一个局部变量以保留属性值：  
  
    ```  
    ' Local variable to hold property value  
    Private mvarProp1 As Integer  
    ```  
  
8.  添加属性 `Let` 和属性 `Get` 属性过程：  
  
    ```  
    Public Property Let Prop1(ByVal vData As Integer)  
       'Used when assigning a value to the property.  
       mvarProp1 = vData  
    End Property  
    Public Property Get Prop1() As Integer  
       'Used when retrieving a property's value.  
       Prop1 = mvarProp1  
    End Property  
    ```  
  
9. 添加一个函数：  
  
    ```  
    Function AddNumbers(   
       ByVal SomeNumber As Integer,   
       ByVal AnotherNumber As Integer) As Integer  
  
       AddNumbers = SomeNumber + AnotherNumber  
    End Function  
    ```  
  
10. 在**“文件”**菜单上，单击**“生成 ComObject1.dll”**，创建并注册 COM 对象。  
  
    > [!NOTE]
    >  虽然也可以将使用 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 创建的类公开为 COM 对象，但它并不是真正的 COM 对象，也不能在本演练中使用。  有关详细信息，请参见 [.NET Framework 应用程序中的 COM 互操作性](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)。  
  
## 互操作程序集  
 在下面的过程中，将创建一个互操作程序集，它将作为非托管代码（如 COM 对象）和 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 使用的托管代码之间的桥梁。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 创建的互操作程序集将处理使用 COM 对象的许多细节问题，如互操作封送处理，它是在与 COM 对象之间来回移动参数和返回值时，将这些参数和返回值打包为等效数据类型的过程。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 应用程序中的引用指向互操作程序集，而不是实际的 COM 对象。  
  
#### 在 Visual Basic 2005 及其更高版本中使用 COM 对象  
  
1.  打开一个新的 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] Windows 应用程序项目。  
  
2.  在**“项目”**菜单上，单击**“添加引用”**。  
  
     将显示**“添加引用”**对话框。  
  
3.  在**“COM”**选项卡上，双击**“组件名称”**列表中的 `ComObject1`，再单击**“确定”**。  
  
4.  在**“项目”**菜单上，单击**“添加新项”**。  
  
     显示**“添加新项”**对话框。  
  
5.  在**“模板”**窗格中单击**“类”**。  
  
     默认文件名 `Class1.vb` 将出现在**“名称”**字段中。  将此字段更改为 MathClass.vb，再单击**“添加”**。  这将创建一个名为 `MathClass` 的类，并显示其代码。  
  
6.  将以下代码添加到 `MathClass` 的顶部，以继承 COM 类。  
  
     [!code-vb[VbVbalrInterop#31](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_1.vb)]  
  
7.  通过将以下代码添加到 `MathClass` 来重载基类的公共方法：  
  
     [!code-vb[VbVbalrInterop#32](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_2.vb)]  
  
8.  通过将以下代码添加到 `MathClass` 来扩展继承类：  
  
     [!code-vb[VbVbalrInterop#33](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_3.vb)]  
  
 新类继承 COM 对象中基类的属性，重载一个方法并定义一个新方法来扩展该类。  
  
#### 要测试继承的类  
  
1.  将一个按钮添加到启动窗体中，然后双击该按钮以查看其代码。  
  
2.  在该按钮的 `Click` 事件处理程序过程中添加以下代码，创建 `MathClass` 的一个实例，并调用被重载的方法：  
  
     [!code-vb[VbVbalrInterop#34](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_4.vb)]  
  
3.  通过按 F5 键运行项目。  
  
 单击窗体上的按钮时，首次调用 `AddNumbers` 方法使用数据类型为 `Short` 的数值，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 会从基类中选择适当的方法。  第二次调用 `AddNumbers` 定向于 `MathClass` 的重载方法。  第三次调用调用了扩展该类的 `SubtractNumbers` 方法。  这样就设置了基类中的属性，并显示其值。  
  
## 后续步骤  
 您可能已经注意到，重载的 `AddNumbers` 函数与从 COM 对象的基类继承的方法具有相同的数据类型。  这是因为在 Visual Basic 6.0 中，基类方法的形参和实参被定义为 16 位整数，但它们在 Visual Basic 的更高版本中公开为 `Short` 类型的 16 位整数。  新的函数接受 32 位整数，并重载基类函数。  
  
 在使用 COM 对象时，请确保验证参数的大小和数据类型。  例如，在使用以参数形式接受 Visual Basic 6.0 集合对象的 COM 对象时，不能提供 Visual Basic 更高版本的集合。  
  
 可以重写从 COM 类继承的属性和方法，这意味着您可以声明局部属性或方法来代替从 COM 基类继承的属性和方法。  除以下不同之处外，重写继承的 COM 属性的规则与重写其他属性和方法的规则类似：  
  
-   如果要重写任何从 COM 类继承的属性或方法，必须重写所有其他继承的属性和方法。  
  
-   不能重写使用 `ByRef` 参数的属性。  
  
## 请参阅  
 [.NET Framework 应用程序中的 COM 互操作性](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)   
 [Inherits 语句](../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [Short 数据类型](../../../visual-basic/language-reference/data-types/short-data-type.md)