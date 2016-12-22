---
title: "Visual Basic 中的隐藏 | Microsoft Docs"
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
  - "已声明的元素, 隐藏"
  - "已声明的元素, 引用"
  - "已声明的元素, 阴影操作"
  - "重复的名称"
  - "继承, 阴影操作"
  - "名称, 阴影操作"
  - "命名冲突, 阴影操作"
  - "对象 [Visual Basic], 名称"
  - "重写, 和阴影操作"
  - "范围, 阴影操作"
  - "阴影操作"
  - "阴影操作, 和重写"
  - "阴影操作, 按继承"
  - "阴影操作, 按范围"
  - "Shadows 关键字, 关于"
ms.assetid: 54bb4c25-12c4-4181-b4a0-93546053964e
caps.latest.revision: 24
caps.handback.revision: 24
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Visual Basic 中的隐藏
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

当两个编程元素共享同一个名称时，其中一个元素可能会掩藏（或者说*“隐藏”*）另一个元素。  在这种情况下，被隐藏的元素不能引用；相反，当您的代码使用该元素名时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器会将其解析为隐藏元素。  
  
## 用途  
 隐藏的主要目的是保护类成员的定义。  基类可能会经历这样的变化：用您已经定义的相同名称创建元素。  如果发生这种变化，`Shadows` 修饰符就会通过您的类强制引用被解析为您定义的成员，而不是解析为新的基类元素。  
  
## 隐藏类型  
 一个元素可以以两种不同的方式隐藏另一元素。  可以在包含被隐藏元素的区域的子区域内声明隐藏元素，这种情况下，隐藏是*“通过范围”*来完成的。  或者一个派生类可以重新定义一个基类成员，这种情况下，隐藏是*“通过继承”*来完成的。  
  
### 通过范围进行隐藏  
 同一模块、类或结构中的编程元素可以名称相同但范围不同。  当以这种方式声明了两个元素，并且代码引用了它们共享的名称时，范围较窄的元素将隐藏其他元素（块范围是最窄的）。  
  
 例如，模块可以定义一个名为 `temp` 的 `Public` 变量，并且该模块内的过程可以声明一个名称同样为 `temp` 的局部变量。  从过程内引用 `temp` 将访问局部变量，而从过程外引用 `temp` 访问 `Public` 变量。  这种情况下，过程变量 `temp` 隐藏模块变量 `temp`。  
  
 下图显示了两个变量，这两个变量的名称都是 `temp`。  当从局部变量自身的过程 `p` 内访问时，该局部变量 `temp` 隐藏了成员变量 `temp`。  不过，`MyClass` 关键字会绕开该隐藏并访问该成员变量。  
  
 ![通过范围进行隐藏示意图](../../../../visual-basic/programming-guide/language-features/declared-elements/media/shadowscope.gif "ShadowScope")  
通过范围进行隐藏  
  
 有关通过范围进行隐藏的示例，请参见 [如何：隐藏与您的变量同名的变量](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-a-variable-with-the-same-name-as-your-variable.md)。  
  
### 通过继承隐藏  
 如果一个派生类重新定义了一个继承基类的编程元素，重定义的元素将隐藏原始元素。  可以用任何其他类型的元素隐藏任意类型的已声明元素或一组重载元素。  例如，一个 `Integer` 变量可以隐藏一个 `Function` 过程。  如果用一个过程隐藏另一个过程，可以使用不同的参数列表和不同的返回类型。  
  
 下图显示的是基类 `b` 和从 `b` 继承的派生类 `d`。  该基类定义一个名为 `proc` 的过程，然后派生类用另一个同名过程隐藏该过程。  第一个 `Call` 语句访问派生类中隐藏的 `proc`。  不过，`MyBase` 关键字会绕开该隐藏并访问基类中隐藏的过程。  
  
 ![通过继承进行隐藏示意图](../../../../visual-basic/programming-guide/language-features/declared-elements/media/shadowinherit.gif "ShadowInherit")  
通过继承隐藏  
  
 有关通过继承进行隐藏的示例，请参见 [如何：隐藏与您的变量同名的变量](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-a-variable-with-the-same-name-as-your-variable.md) 和 [如何：隐藏继承的变量](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-an-inherited-variable.md)。  
  
#### 隐藏和访问级别  
 从使用派生类的代码中并不总是能够访问隐藏元素。  例如，它可能被声明为 `Private`。  在这种情况下，隐藏就会失败，并且如果以前没有隐藏，编译器就会将任何引用解析为它包含的同一个元素。  这是自隐藏类向后追溯时派生步骤最少的可访问元素。  如果被隐藏的元素是一个过程，则将解析为具有相同的名称、参数列表和返回类型的最近似的可访问版本。  
  
 下面的示例显示了三个类的继承层次结构。  每个类都定义一个 `Sub` 过程 `display`，并且每个派生类都隐藏其基类中的 `display` 过程。  
  
```  
Public Class firstClass  
    Public Sub display()  
        MsgBox("This is firstClass")  
    End Sub  
End Class  
Public Class secondClass  
    Inherits firstClass  
    Private Shadows Sub display()  
        MsgBox("This is secondClass")  
    End Sub  
End Class  
Public Class thirdClass  
    Inherits secondClass  
    Public Shadows Sub display()  
        MsgBox("This is thirdClass")  
    End Sub  
End Class  
Module callDisplay  
    Dim first As New firstClass  
    Dim second As New secondClass  
    Dim third As New thirdClass  
    Public Sub callDisplayProcedures()  
        ' The following statement displays "This is firstClass".  
        first.display()  
        ' The following statement displays "This is firstClass".  
        second.display()  
        ' The following statement displays "This is thirdClass".  
        third.display()  
    End Sub  
End Module  
```  
  
 在前一个示例中，派生类 `secondClass` 用一个 `Private` 过程隐藏 `display`。  模块 `callDisplay` 调用 `secondClass` 中的 `display` 时，调用代码在 `secondClass` 外部，因此不能访问私有的 `display` 过程。  隐藏失败，并且编译器将引用解析为基类 `display` 过程。  
  
 不过，进一步派生的类 `thirdClass` 将 `display` 声明为 `Public`，这样 `callDisplay` 中的代码就能访问它。  
  
## 隐藏与重写  
 不要将隐藏与重写混淆。  二者都在派生类继承基类时使用，并且都是用另外的元素重定义一个已声明的元素。  但二者之间有重大区别。  有关比较，请参见 [隐藏和重写之间的差异](../../../../visual-basic/programming-guide/language-features/declared-elements/differences-between-shadowing-and-overriding.md)。  
  
## 隐藏与重载  
 如果用派生类中的多个元素隐藏同一个基类元素，隐藏元素将变为该元素的重载版本。  有关更多信息，请参见 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)。  
  
## 访问被隐藏元素  
 当访问导出类中的元素时，通常要通过该导出类的当前实例，并用 `Me` 关键字限定元素名。  如果导出类隐藏了基类中的元素，则可以通过用 `MyBase` 关键字限定基类元素来访问它。  
  
 有关访问被隐藏元素的示例，请参见 [如何：访问被派生类隐藏的变量](../Topic/How%20to:%20Access%20a%20Variable%20Hidden%20by%20a%20Derived%20Class%20\(Visual%20Basic\).md)。  
  
### 对象变量的声明  
 创建对象变量的方式也会影响派生类是访问隐藏元素还是被隐藏的元素。  下面的示例从一个派生类创建两个对象，但一个对象被声明为基类，另一个被声明为派生类。  
  
```  
Public Class baseCls  
    ' The following statement declares the element that is to be shadowed.  
    Public z As Integer = 100  
End Class  
Public Class dervCls  
    Inherits baseCls  
    ' The following statement declares the shadowing element.  
    Public Shadows z As String = "*"  
End Class  
Public Class useClasses  
    ' The following statement creates the object declared as the base class.  
    Dim basObj As baseCls = New dervCls()  
    ' Note that dervCls widens to its base class baseCls.  
    ' The following statement creates the object declared as the derived class.  
    Dim derObj As dervCls = New dervCls()  
    Public Sub showZ()   
    ' The following statement outputs 100 (the shadowed element).  
        MsgBox("Accessed through base class: " & basObj.z)  
    ' The following statement outputs "*" (the shadowing element).  
        MsgBox("Accessed through derived class: " & derObj.z)  
    End Sub  
End Class  
```  
  
 在前面的示例中，变量 `basObj` 被声明为基类。  为它指定一个 `dervCls` 对象将继续一个扩展转换，因而是有效的。  但是，基类不能访问派生类中变量 `z` 的隐藏版本，因此编译器会将 `basObj.z` 解析为原始的基类值。  
  
## 请参阅  
 [对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Visual Basic 中的范围](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [扩大转换和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)   
 [Overrides](../../../../visual-basic/language-reference/modifiers/overrides.md)   
 [Me、My、MyBase 和 MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)   
 [继承的基础知识](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)