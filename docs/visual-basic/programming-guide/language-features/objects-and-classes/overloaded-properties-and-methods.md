---
title: "重载属性和方法 (Visual Basic) | Microsoft Docs"
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
  - "类 [Visual Basic], 方法"
  - "类 [Visual Basic], 属性"
  - "方法重载"
  - "方法 [Visual Basic], 重载"
  - "名称, 多个过程，具有相同的"
  - "Overloads 关键字, 重载的成员"
  - "过程, 多个同名元素"
  - "属性 [Visual Basic], 重载"
  - "阴影操作"
ms.assetid: b686fb97-e7d7-4001-afaa-6650cba08f0d
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 重载属性和方法 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

重载是在一个类中用相同的名称但是不同的参数类型创建一个以上的过程、实例构造函数或属性。  
  
## 重载用法  
 当对象模型指示对于在不同数据类型上进行操作的过程使用同样名称时，重载非常有用。  例如，可显示几种不同数据类型的类可以具有类似如下所示 `Display` 过程：  
  
 [!code-vb[VbVbalrOOP#64](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#64)]  
  
 如果不使用重载，那么即使每个过程执行相同的操作，也需要为它们创建不同的名称，如下所示：  
  
 [!code-vb[VbVbalrOOP#65](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#65)]  
  
 因为重载提供了对可用数据类型的选择，所以它使得属性或方法的使用更为容易。  例如，可以用下列任一代码行调用前面讨论过的重载 `Display` 方法：  
  
 [!code-vb[VbVbalrOOP#66](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#66)]  
  
 在运行时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 根据指定参数的数据类型来调用正确的过程。  
  
## 重载规则  
 用同样名称添加两个或更多属性或方法可以创建类的一个重载成员。  除了重载派生成员，每一个重载成员必须具有不同的参数列表。当重载属性或过程时，下面的项不能用作区分特征：  
  
-   应用于成员或成员参数的修饰符，如 `ByVal` 或 `ByRef`。  
  
-   参数名  
  
-   过程的返回类型  
  
 重载时关键字 `Overloads` 是可选的，但如果任一重载成员使用了该 `Overloads` 关键字，则其他所有同名重载成员也必须指定该关键字。  
  
 派生类可以用具有相同参数和参数类型的成员重载继承成员，该过程称为*“按名称和签名隐藏”*。  如果按名称和签名隐藏时使用了 `Overloads` 关键字，将使用成员的派生类实现而不是基类中的实现，并且该成员的所有其他重载对于派生类的实例都可用。  
  
 如果用一个具有相同参数和参数类型的成员重载继承成员时省略 `Overloads` 关键字，则该重载称为*“按名称隐藏”*。  按名称隐藏替换成员的继承实现，使所有其他重载对于派生类及由其派生的类的实例都不可用。  
  
 `Overloads` 和 `Shadows` 修饰符不能同时被同一个属性或方法所使用。  
  
### 示例  
 下面的示例创建接受美元金额的 `String` 或 `Decimal` 表示形式并返回包含销售税的字符串的重载方法。  
  
##### 使用此示例创建重载方法  
  
1.  打开新项目，添加名为 `TaxClass` 的类。  
  
2.  向 `TaxClass` 类中添加下面的代码。  
  
     [!code-vb[VbVbalrOOP#67](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#67)]  
  
3.  向窗体中添加下面的过程。  
  
     [!code-vb[VbVbalrOOP#68](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#68)]  
  
4.  向窗体中添加按钮，并从该按钮的 `Button1_Click` 事件调用 `ShowTax` 过程。  
  
5.  运行该项目并单击窗体上的该按钮，以测试重载 `ShowTax` 过程。  
  
 在运行时，编译器选择与所用参数匹配的适当重载函数。  单击该按钮时，首先将使用字符串类型的 `Price` 参数调用重载方法，并显示信息：“Price is a String.  Tax is $5.12”。  第二次将使用 `Decimal` 值调用 `TaxAmount`，并显示消息“Price is a Decimal.  Tax is $5.12”。  
  
## 请参阅  
 [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Visual Basic 中的隐藏](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)   
 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [继承的基础知识](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)   
 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)   
 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)   
 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)   
 [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md)   
 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)