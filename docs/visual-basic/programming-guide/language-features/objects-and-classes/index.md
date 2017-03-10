---
title: "Visual Basic 中的对象和类 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "类 [Visual Basic]"
  - "对象 [Visual Basic]"
ms.assetid: c68c5752-1006-46e1-975a-6717b62a42fc
caps.latest.revision: 26
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 26
---
# Visual Basic 中的对象和类
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

*“对象”*是可被视为一个单元的代码和数据的组合。  对象可以是一段应用程序，如控件或窗体。  整个应用程序也可以是一个对象。  
  
 在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中创建应用程序的过程，就是不断地处理对象的过程。  可以使用由 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供的对象，如控件、窗体和数据访问对象。  也可以在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 应用程序中使用来自其他应用程序的对象。  甚至可以创建自己的对象，并为它们定义其他属性和方法。  对象的作用类似于程序的预制生成块，它们使您得以只编写一次某段代码，然后反复重用它。  
  
 本主题详细讨论了对象。  
  
## 对象和类  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的每个对象都由“类”定义。  类描述对象的变量、属性、过程和事件。  对象是类的实例。创建了一个类后，可以创建所需的任意数量的对象。  
  
 若要理解对象与其类之间的关系，请想一下小甜饼成型机和小甜饼。  小甜饼成型机是类。  它定义每个小甜饼的特征，如大小和形状。  类用于创建对象。  这些对象是小甜饼。  
  
 必须先创建一个对象，然后才能访问它的成员。  
  
#### 从类创建对象  
  
1.  确定要创建对象的类。  
  
2.  编写 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md) 创建一个可向其分配类实例的变量。  变量的类型应为所需的类。  
  
    ```  
  
    Dim nextCustomer As customer   
    ```  
  
3.  添加 [New 运算符](../../../../visual-basic/language-reference/operators/new-operator.md) 关键字将该变量初始化为该类的新实例。  
  
    ```  
    Dim nextCustomer As New customer  
    ```  
  
4.  现在即可通过该对象变量访问该类的成员。  
  
    ```  
  
    nextCustomer.accountNumber = lastAccountNumber + 1  
    ```  
  
> [!NOTE]
>  只要可能，都应将变量声明为要向其赋值的类类型。  这称为*“早期绑定”*。  如果在编译时不知道类类型，则可以通过将变量声明为 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md) 来调用*“后期绑定”*。  但是，后期绑定可能导致性能降低并限制对运行时对象成员的访问。  有关更多信息，请参见[对象变量声明](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)。  
  
### 多个实例  
 通过类创建的对象刚开始通常都是相同的。  但是，它们作为单个对象存在后，其变量和属性就可以独立于其他实例进行更改。  例如，如果将三个复选框添加到窗体中，则每个复选框对象都是 <xref:System.Windows.Forms.CheckBox> 类的一个实例。  这些单个 <xref:System.Windows.Forms.CheckBox> 对象共享一组由该类定义的共同特性和功能（属性、变量、过程和事件）。  但是，每个对象都有各自的名称，可以分别启用和禁用，而且可以放置在窗体上的不同位置。  
  
## 对象成员  
 一个对象就是应用程序的一个元素，代表类的一个*“实例”*。  字段、属性、方法和事件是对象的生成块，以及构成它们的*“成员”*。  
  
### 成员访问  
 通过依次指定对象变量的名称、句点 \(`.`\) 和成员的名称来访问对象的成员。  下面的示例设置 <xref:System.Windows.Forms.Label> 对象的 <xref:System.Windows.Forms.Control.Text%2A> 属性。  
  
```  
warningLabel.Text = "Data not saved"  
```  
  
#### 成员的 IntelliSense 列表  
 IntelliSense 在您激活它的“列出成员”选项时列出类的成员，例如当您将句点 \(`.`\) 作为成员访问运算符键入时。  如果您键入的句点跟在某个声明为该类的一个实例的变量的名称之后，则 IntelliSense 列出所有实例成员，而不列出任何共享成员。  如果键入的句点跟在类名本身之后，则 IntelliSense 只列出所有共享成员，而不列出任何实例成员。  有关更多信息，请参见[使用 IntelliSense](/visual-studio/ide/using-intellisense)。  
  
### 字段和属性  
 *“字段”*和*“属性”* 表示对象中存储的信息。  可用像检索和设置过程中的局部变量那样，用赋值语句来检索和设置字段和属性的值。  下面的示例检索 <xref:System.Windows.Forms.Label> 对象的 <xref:System.Windows.Forms.Control.Width%2A> 的属性，并设置该对象的 <xref:System.Windows.Forms.Control.ForeColor%2A> 属性。  
  
```  
Dim warningWidth As Integer = warningLabel.Width  
warningLabel.ForeColor = System.Drawing.Color.Red  
```  
  
 注意，字段也称为*“成员变量”*。  
  
 在以下情况下使用属性过程：  
  
-   需要控制设置或检索值的时间和方式时。  
  
-   属性有定义完善的一组值需要进行验证时。  
  
-   设置值导致对象的状态发生某些明显的变化（如 `IsVisible` 属性）。  
  
-   设置属性会导致更改其他内部变量或其他属性的值时。  
  
-   必须先执行一组步骤，然后才能设置或检索属性时。  
  
 在以下情况下使用字段：  
  
-   值为自验证类型时。  例如，如果将 `True` 或 `False` 以外的值赋给 `Boolean` 变量，就会发生错误或自动数据转换。  
  
-   在数据类型所支持范围内的任何值均有效时。  `Single` 或 `Double` 类型的很多属性属于这种情况。  
  
-   属性是 `String` 数据类型，且对于字符串的大小或值没有任何约束时。  
  
-   有关更多信息，请参见[Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)。  
  
### 方法  
 *“方法”*是对象可以执行的操作。  例如，<xref:System.Windows.Forms.ComboBox.ObjectCollection.Add%2A> 是 <xref:System.Windows.Forms.ComboBox> 对象的一个方法，它向组合框中添加新项。  
  
 下面的示例阐释了 <xref:System.Windows.Forms.Timer> 对象的 <xref:System.Windows.Forms.Timer.Start%2A> 方法。  
  
```  
Dim safetyTimer As New System.Windows.Forms.Timer  
safetyTimer.Start()  
```  
  
 注意，一个方法只是由对象公开的一个*“过程”*。  
  
 有关更多信息，请参见[过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)。  
  
### 事件  
 事件是由对象识别的操作（如单击鼠标或按某个键），可以为其编写代码以进行响应。  事件可以作为用户操作或程序代码的结果发生，也可由系统引发。  发出事件信号的代码就是*“引发”*事件，而响应事件的代码就是*“处理”*事件。  
  
 您还可以开发自己的自定义事件，这些事件可由您的对象引发并由其他对象处理。  有关更多信息，请参见 [事件](../../../../visual-basic/programming-guide/language-features/events/events.md)。  
  
### 实例成员和共享成员  
 从某个类创建对象时，得到的就是该类的一个实例。  不用 [Shared](../../../../visual-basic/language-reference/modifiers/shared.md) 关键字声明的成员是*“实例成员”*，它们严格属于那个特定的实例。  一个实例中的实例成员与同一个类的其他实例中的相同成员无关。  例如，一个实例成员变量在不同的实例中可以有不同的值。  
  
 用 `Shared` 关键字声明的成员是*“共享成员”*，这些成员作为一个整体属于类，而不属于任何特定的实例。  共享成员仅存在一次，不管为它的类创建了多少实例，也不管是否未创建任何实例。  例如，一个共享成员变量只有一个值，这个值对可以访问该类的所有代码均可用。  
  
#### 访问非共享成员  
  
###### 访问对象的非共享成员  
  
1.  确保对象已经从对象的类创建并分配给了一个对象变量。  
  
    ```  
    Dim secondForm As New System.Windows.Forms.Form  
    ```  
  
2.  在访问成员的语句中，对象变量名称后接*“成员访问运算符”*\(`.`\)，然后是成员名称。  
  
    ```  
    secondForm.Show()  
    ```  
  
#### 访问共享成员  
  
###### 访问对象的共享成员  
  
-   类名后接*“成员访问运算符”*\(`.`\)，然后是成员名称。  应始终直接通过类名访问对象的 `Shared` 成员。  
  
    ```  
    MsgBox("This computer is called " & Environment.MachineName)  
    ```  
  
-   如果已经从类创建了对象，也可以通过对象的变量访问 `Shared` 成员。  
  
### 类与模块之间的差异  
 类和模块之间的主要差异在于：类可以实例化为对象，而标准模块则不能。  由于标准模块的数据只有一个副本，因此当程序的一部分更改标准模块中的公共变量时，如果程序的其他任何部分随后读取该变量，都会获取同样的值。  与之相反，每个实例化对象的对象数据则单独存在。  另一个不同在于：不像标准模块，类可以实现接口。  
  
> [!NOTE]
>  当 `Shared` 修饰符应用于类成员时，它是与类本身相关联，而不是类的特定实例关联。  使用类名可直接访问类成员，与模块成员的访问方式相同。  
  
 类和模块对它们的成员使用不同的范围。  在类中定义的成员其作用范围在类的特定实例内，并且只存在于对象的生存期内。  要从类的外部访问类成员，必须使用“*对象*.*成员*”格式的全限定名称。  
  
 另一方面，在模块内声明的成员默认情况下是公共可访问成员，任何可访问该模块的代码都可以访问它。  这意味着标准模块中的变量是有效的全局变量，因为它们在项目中的任何地方均可见，且存在于程序的整个生存期。  
  
## 重用类和对象  
 对象使您得以只声明一次变量和过程，然后在任何需要的时候重用它们。  例如，如果要将拼写检查器添加到应用程序中，可以定义所有提供拼写检查功能的变量和支持函数。  如果将拼写检查器创建为一个类，则可以通过添加对已编译程序集的引用，在其他应用程序中重用该类。  更好的是，您可能能够通过使用其他人已经开发的拼写检查器类，省去自己的一些工作。  
  
 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] 提供了可以使用的组件的许多示例。  下面的示例使用 <xref:System> 命名空间中的 <xref:System.TimeZone> 类。  <xref:System.TimeZone> 提供的成员可用于检索有关当前计算机系统所在时区的信息。  
  
```  
Public Sub examineTimeZone()  
    Dim tz As System.TimeZone = System.TimeZone.CurrentTimeZone  
    Dim s As String = "Current time zone is "  
    s &= CStr(tz.GetUtcOffset(Now).Hours) & " hours and "  
    s &= CStr(tz.GetUtcOffset(Now).Minutes) & " minutes "  
    s &= "different from UTC (coordinated universal time)"  
    s &= vbCrLf & "and is currently "  
    If tz.IsDaylightSavingTime(Now) = False Then s &= "not "  
    s &= "on ""summer time""."  
    MsgBox(s)  
End Sub  
```  
  
 在前面的示例中，第一个 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md) 声明一个类型为 <xref:System.TimeZone> 的对象变量，并将由 <xref:System.TimeZone.CurrentTimeZone%2A> 属性返回的 <xref:System.TimeZone> 对象分配给它。  
  
## 对象之间的关系  
 对象之间相关的方式可以有若干种。  关系的主要类型为*“分层”*和*“包容”*。  
  
### 分层关系  
 当从多个基础类中派生类时，就可以说它们具有*“分层关系”*。  当描述作为更常规类的子类型的项时，类层次结构非常有用。  
  
 下面的示例假设要定义一种特殊的 <xref:System.Windows.Forms.Button>，它可用作常规 <xref:System.Windows.Forms.Button>，同时还公开一个反转前景色和背景色的方法。  
  
##### 定义一个从已存在的类派生的类  
  
1.  使用 [Class 语句](../../../../visual-basic/language-reference/statements/class-statement.md) 定义从中可创建所需对象的类。  
  
     `Public Class reversibleButton`  
  
     确保定义的类中最后一行代码后面有 `End Class` 语句。  默认情况下，集成开发环境 \(IDE\) 在输入 `Class` 语句时自动生成 `End Class`。  
  
2.  `Class` 语句之后紧接 [Inherits 语句](../../../../visual-basic/language-reference/statements/inherits-statement.md)。  指定派生新类的类。  
  
     `Inherits System.Windows.Forms.Button`  
  
     新类继承基类定义的所有成员。  
  
3.  向派生类公开的其他成员添加代码。  例如，可以添加一个 `reverseColors` 方法，派生类则如下所示：  
  
    ```  
    Public Class reversibleButton  
        Inherits System.Windows.Forms.Button  
        Public Sub reverseColors()   
            Dim saveColor As System.Drawing.Color = Me.BackColor  
            Me.BackColor = Me.ForeColor  
            Me.ForeColor = saveColor  
        End Sub  
    End Class   
    ```  
  
     如果从 `reversibleButton` 类创建一个对象，则它可以访问 <xref:System.Windows.Forms.Button> 类的所有成员、`reverseColors` 方法以及 `reversibleButton` 上定义的任何其他新成员。  
  
 派生类从其所基于的类继承成员，允许随着类层次结构的进展添加复杂性。  有关更多信息，请参见[继承的基础知识](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)。  
  
#### 编译代码  
 确保编译器能够访问要从中派生新类的类。  这可能意味着完全限定其名称，如前例所示，或在 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) 中标识其命名空间。  如果类在其他项目中，则可能需要添加对该项目的引用。  有关更多信息，请参见 [管理项目中的引用](/visual-studio/ide/managing-references-in-a-project)。  
  
### 包容关系  
 对象可以相关的另一种方式为*“包容关系”*。  容器对象从逻辑上封装其他对象。  例如，<xref:System.OperatingSystem> 对象逻辑上包含一个 <xref:System.Version> 对象，前者通过其 <xref:System.OperatingSystem.Version%2A> 属性返回后者。  请注意，容器对象在物理上并不包含任何其他对象。  
  
#### 集合  
 *“集合”*表示一种特定类型的对象包容。  集合是可以枚举的多个相似对象组成的组。  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 支持 [For Each...Next 语句](../../../../visual-basic/language-reference/statements/for-each-next-statement.md) 中的特定语法，该语法允许您循环访问集合中的项。  另外，集合通常允许您使用 <xref:Microsoft.VisualBasic.Collection.Item%2A> 按照元素的索引或通过将元素与某个唯一字符串相关联来检索元素。  集合比数组更易于使用，因为它们允许您在不使用索引的情况下添加或移除项。  因为它们的易用性，集合经常用于存储窗体和控件。  
  
## 相关主题  
 [演练：定义类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/walkthrough-defining-classes.md)  
 提供有关如何创建类的分步说明。  
  
 [重载属性和方法](../../../../visual-basic/programming-guide/language-features/objects-and-classes/overloaded-properties-and-methods.md)  
 重载属性和方法  
  
 [继承的基础知识](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)  
 涉及继承修饰符、重写方法和属性、MyClass 以及 MyBase。  
  
 [对象生存期：如何创建和销毁对象](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)  
 讨论类实例的创建和释放。  
  
 [匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)  
 介绍如何创建和使用匿名类型，使您能够在没有为数据类型编写类定义的情况下创建对象。  
  
 [对象初始值设定项：命名类型和匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)  
 讨论对象初始值设定项，通过使用单个表达式，可以利用这些初始值设定项来创建命名和匿名类型的实例。  
  
 [如何：推断匿名类型声明中的属性名和类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)  
 解释如何推断匿名类型声明中的属性名和类型。  提供成功推理和不成功推理的示例。