---
title: "如何：声明枚举 (Visual Basic) | Microsoft Docs"
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
  - "声明, 枚举"
  - "声明枚举"
  - "枚举 [Visual Basic], 声明"
ms.assetid: db4ca1c3-f429-4c81-ae81-29e0157b29fd
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# 如何：声明枚举 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

使用 `Enum` 语句创建枚举在类或模块的声明部分。  不能在方法中声明枚举。  若要指定适当的访问级别，请使用 `Private`、 `Protected`、 `Friend`或 `Public`。  
  
 `Enum` 类型具有名称，一个基础类型和一组字段，表示常数的每个。  该名称必须是有效的 [!INCLUDE[vbprvblong](../../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] 限定符。  基础类型必须是一个整数类型`Byte`、 `Short`、 `Long` 或 `Integer`。  `Integer` 是默认设置。  枚举始终是强类型的整数类型互换不可互换。  
  
 枚举不能具有浮点值。  如果枚举赋与 `Option Strict On`的浮点值，则会导致编译器错误。  如果 `Option Strict` 是 `Off`，该值被自动转换为 `Enum` 类型。  
  
 有关名称的信息，以及如何使用 `Imports` 语句使名称限定不必要，请参见 [枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)。  
  
### 声明枚举  
  
1.  编写一个包括代码访问级别、 `Enum` 关键字和一个有效的名称的声明，如下面的示例中，每个声明不同的 `Enum`。  
  
     [!code-vb[VbEnumsTask#3](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-enumerations_1.vb)]  
  
2.  在枚举中定义常量。  默认情况下，枚举中的第一个常数初始化为 `0`，并且，后续常数比前面的常数初始化为值为一个。  例如，下面的枚举， `Days`，包含一个常数命名为值 `0`，常量的 `Sunday` 命名为值 `1`，常量的 `Monday` 名为与 `2`的值 `Tuesday` ，依此类推。  
  
     [!code-vb[VbEnumsTask#4](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-enumerations_2.vb)]  
  
3.  使用赋值语句，可以将值显式赋予枚举中的常数。  可赋予任何整数值，包括负数。  例如，您可能希望值小于零的常数表示错误状态。  下面的枚举，常量 `Invalid` 将值显式赋予了 `–1`，因此，该常数 `Sunday` 被赋予值 `0`。  因为是枚举中的第一个常数， `Saturday` 还初始化为值 `0`。  `Monday` 的值是 `1` \(一个比 `Sunday`的值\); `Tuesday` 的值是 `2`，依此类推。  
  
     [!code-vb[VbEnumsTask#5](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-enumerations_3.vb)]  
  
### 将枚举声明为显式类型  
  
-   使用 `As` 子句，如下面的示例所示，指定枚举的类型，。  
  
     [!code-vb[VbEnumsTask#6](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-enumerations_4.vb)]  
  
## 请参阅  
 [枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [如何：引用枚举成员](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)   
 [如何：在 Visual Basic 中循环访问枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)   
 [如何：确定与枚举值关联的字符串](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)   
 [何时使用枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)   
 [常量概述](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [常量和 Literal 数据类型](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)   
 [常量和枚举](../../../../visual-basic/language-reference/constants-and-enumerations.md)