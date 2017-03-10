---
title: "继承的基础知识 (Visual Basic) | Microsoft Docs"
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
  - "抽象类, 继承"
  - "基类, 扩展属性和方法"
  - "基类, 继承"
  - "类 [Visual Basic], 派生"
  - "派生类, 继承"
  - "继承"
  - "Inherits 语句, 继承"
  - "MustInherit 类"
  - "MustInherit 关键字, using"
  - "MustOverride 关键字, using"
  - "MyBase 关键字, using"
  - "MyClass 关键字, using"
  - "NotInheritable 关键字, using"
  - "NotOverridable 关键字, using"
  - "Overrides 关键字, using"
  - "重写, Overridable 关键字"
  - "重写, Overrides 关键字"
ms.assetid: dfc8deba-f5b3-4d1d-a937-7cb826446fc5
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# 继承的基础知识 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

`Inherits` 语句用来声明基于现有类（也称为*“基类”*）的新类，称为*“派生类”*。  派生类继承并可扩展基类中定义的属性、方法、事件、字段和常数。  下面一节描述一些继承规则，以及一些可用来更改类继承或被继承方式的修饰符：  
  
-   默认情况下，所有类都是可继承的，除非用 `NotInheritable` 关键字标记。  类可以从项目中的其他类继承，也可以从项目引用的其他程序集中的类继承。  
  
-   与允许多重继承的语言不同，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 只允许类中有单一继承，即派生类只能有一个基类。  虽然类中不允许有多重继承，但类可以实现多个接口，这样可以有效地实现同样的目的。  
  
-   若要防止公开基类中的受限项，派生类的访问类型必须与其基类一样或比其基类所受限制更多。  例如，`Public` 类不能继承 `Friend` 或 `Private` 类，而 `Friend` 又不能继承 `Private` 类。  
  
## 继承修饰符  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 引入了以下类级别语句和修饰符以支持继承：  
  
-   `Inherits` 语句 — 指定基类。  
  
-   `NotInheritable` 修饰符 — 防止程序员将该类用作基类。  
  
-   `MustInherit` 修饰符 — 指定该类仅适于用作基类。  无法直接创建 `MustInherit` 类的实例，只能将它们创建为派生类的基类实例。  （其他编程语言，如 C\+\+ 和 C\#，则用术语*“抽象类”*来描述这样的类。）  
  
## 重写派生类中的属性和方法  
 默认情况下，派生类从其基类继承属性和方法。  如果继承的属性或方法需要在派生类中有不同的行为，可以将其“重写”。  也就是说，可以在派生类中定义该方法的新实现。  下列修饰符用于控制如何重写属性和方法：  
  
-   `Overridable` — 允许某个类中的属性或方法在派生类中被重写。  
  
-   `Overrides` — 重写基类中定义的 `Overridable` 属性或方法。  
  
-   `NotOverridable` — 防止方法或属性在继承的类中被重写。  默认情况下，`Public` 方法为 `NotOverridable`。  
  
-   `MustOverride` — 要求派生类重写属性或方法。  当使用 `MustOverride` 关键字时，方法定义仅由 `Sub`、`Function` 或 `Property` 语句组成。  不允许有任何其他语句，特别是没有 `End Sub` 或 `End Function` 语句。  `MustOverride` 方法必须在 `MustInherit` 类中声明。  
  
 假设您要定义类以处理工资单。  您可以定义一个泛型 `Payroll` 类，其中包含计算普通周工资单的 `RunPayroll` 方法。  然后可将 `Payroll` 用作更专用的 `BonusPayroll` 类（分发雇员奖金时可能会使用该类）的基类。  
  
 `BonusPayroll` 类可继承并重写在基类 `Payroll` 中定义的 `PayEmployee` 方法。  
  
 下例定义基类 `Payroll` 和派生类 `BonusPayroll`，该派生类重写继承方法 `PayEmployee`。  过程 `RunPayroll` 创建 `Payroll` 对象和 `BonusPayroll` 对象，然后将其传递给函数 `Pay`，该函数为这两个对象执行 `PayEmployee` 方法。  
  
 [!code-vb[VbVbalrOOP#28](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#28)]  
  
## MyBase 关键字  
 `MyBase` 关键字的行为方式类似于引用当前类实例的基类的对象变量。  `MyBase` 通常用于访问派生类中被重写或被隐藏的基类成员。  具体而言，`MyBase.New` 用于从派生类构造函数中显式调用基类构造函数。  
  
 例如，假设您正在设计一个重写从基类继承的方法的派生类。  重写的方法可以调用基类中的该方法，并修改返回值，如下面的代码片段中所示：  
  
 [!code-vb[VbVbalrOOP#109](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#109)]  
  
 下面的列表描述对使用 `MyBase` 的限制：  
  
-   `MyBase` 引用直接基类及其继承成员。  它不能用于访问类中的 `Private` 成员。  
  
-   `MyBase` 是关键字，而不是真实对象。  `MyBase` 不能指派给变量，不能传递给过程，也不能在 `Is` 比较中使用。  
  
-   `MyBase` 限定的方法不需要在直接基类中定义，它可以在间接继承的基类中定义。  为了正确编译 `MyBase` 限定的引用，一些基类必须包含与调用中出现的参数名称和类型匹配的方法。  
  
-   不能使用 `MyBase` 来调用 `MustOverride` 基类方法。  
  
-   `MyBase` 无法用于限定自身。  因此，下面的代码无效：  
  
     `MyBase.MyBase.BtnOK_Click()`  
  
-   `MyBase` 无法用在模块中。  
  
-   如果基类在不同的程序集中，则不能使用 `MyBase` 来访问标记为 `Friend` 的基类成员。  
  
 有关更多信息和另一个示例，请参见[如何：访问被派生类隐藏的变量](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-access-a-variable-hidden-by-a-derived-class.md)。  
  
## MyClass 关键字  
 `MyClass` 关键字的行为方式类似于最初实现时引用类的当前实例的对象变量。  `MyClass` 类似于 `Me`，但系统在处理针对 `MyClass` 调用的每个方法和属性时，都假定此方法或属性是 [NotOverridable](../../../../visual-basic/language-reference/modifiers/notoverridable.md)。  因此，方法或属性不受派生类中重写的影响。  
  
-   `MyClass` 是关键字，而不是真实对象。  `MyClass` 不能指派给变量，不能传递给过程，也不能在 `Is` 比较中使用。  
  
-   `MyClass` 引用包含类及其继承成员。  
  
-   `MyClass` 可用作 `Shared` 成员的修饰符。  
  
-   `MyClass` 不能在 `Shared` 方法内部使用，但可以在实例方法内部使用以访问类的共享成员。  
  
-   `MyClass` 无法用在标准模块中。  
  
-   `MyClass` 可用于限定这样的方法，该方法在基类中定义但没有在该类中提供该方法的实现。  这种引用的意义与 `MyBase.`*Method* 相同。  
  
 下面的示例对 `Me` 和 `MyClass` 进行了对比。  
  
```  
Class baseClass  
    Public Overridable Sub testMethod()  
        MsgBox("Base class string")  
    End Sub  
    Public Sub useMe()  
        ' The following call uses the calling class's method, even if   
        ' that method is an override.  
        Me.testMethod()  
    End Sub  
    Public Sub useMyClass()  
        ' The following call uses this instance's method and not any  
        ' override.  
        MyClass.testMethod()  
    End Sub  
End Class  
Class derivedClass : Inherits baseClass  
    Public Overrides Sub testMethod()  
        MsgBox("Derived class string")  
    End Sub  
End Class  
Class testClasses  
    Sub startHere()  
        Dim testObj As derivedClass = New derivedClass()  
        ' The following call displays "Derived class string".  
        testObj.useMe()  
        ' The following call displays "Base class string".  
        testObj.useMyClass()  
    End Sub  
End Class  
```  
  
 尽管 `derivedClass` 重写了 `testMethod`，但 `useMyClass` 中的 `MyClass` 关键字使重写的影响无效，编译器会将该调用解析为 `testMethod` 的基类版本。  
  
## 请参阅  
 [Inherits 语句](../../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [Me、My、MyBase 和 MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)