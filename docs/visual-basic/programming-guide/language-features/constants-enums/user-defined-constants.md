---
title: "用户定义的常量 (Visual Basic) | Microsoft Docs"
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
  - "常量之间的循环引用"
  - "Const 语句 [Visual Basic], 用户定义的常量"
  - "常量, 循环引用"
  - "常量, 用户定义的"
  - "范围, 常量"
  - "用户定义的常量"
ms.assetid: a1206d5c-c45e-4ac2-970a-4a0be6a05fdd
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 用户定义的常量 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

常数是有意义的名称，替代不变的数字或字符串。  顾名思义，常数存储那些在应用程序的整个执行过程中都保持不变的值。  您可以使用由您所用的控件或组件定义的常数，也可以创建您自己的常数。  您自己创建的常数称作*“用户定义的”*。  
  
 使用 `Const` 语句声明一个常数，遵循与创建变量名称相同的规则。  如果 `Option Strict` 为 `On`，则必须显式声明常数类型。  
  
## Const 语句用法  
 `Const` 语句可以表示数学数量或日期\/时间数量。  
  
 [!code-vb[VbEnumsTask#10](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/VisualBasic/user-defined-constants_1.vb)]  
  
 它也可定义 `String` 常数：  
  
 [!code-vb[VbEnumsTask#13](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/VisualBasic/user-defined-constants_2.vb)]  
  
 等号 \(`=`\) 右侧的表达式通常是数字或文本字符串，但也可以是结果为数字或字符串的表达式（虽然表达式不能包含函数调用）。  甚至可以依据前面已定义的常数来定义常数：  
  
 [!code-vb[VbEnumsTask#15](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/VisualBasic/user-defined-constants_3.vb)]  
  
## 用户定义常数的范围  
 一条 `Const` 语句的范围与在相同位置上声明的变量范围相同。  可以以下列任一方式指定范围：  
  
-   要创建一个仅存在于一个过程中的常数，须在该过程中声明它。  
  
-   若要创建对类内所有过程都可用而对该模块以外的任何代码都不可用的常数，请在该类的声明部分中声明它。  
  
-   若要创建对程序集的所有成员都可用而对该程序集的外部客户端不可用的常数，请在类的声明部分用 `Friend` 关键字声明该常数。  
  
-   若要创建在整个应用程序中都可用的常数，请在该类的声明部分用 `Public` 关键字声明它。  
  
 有关更多信息，请参见 [如何：声明常量](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md)。  
  
### 避免循环引用  
 因为常数可以依据其他常数进行定义，所以可能无意中在两个或更多常数之间产生*“循环”*（或循环引用）。  如果有两个或更多公共常数，当每个常数都依据另一个常数进行定义时，就发生循环，如下面的示例所示：  
  
 [!code-vb[VbEnumsTask#16](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/VisualBasic/user-defined-constants_4.vb)]  
[!code-vb[VbEnumsTask#17](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/VisualBasic/user-defined-constants_5.vb)]  
  
 如果发生循环，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 将生成编译器错误。  
  
## 请参阅  
 [Const 语句](../../../../visual-basic/language-reference/statements/const-statement.md)   
 [常量和 Literal 数据类型](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)   
 [常量和枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/index.md)   
 [常量和枚举](../../../../visual-basic/language-reference/constants-and-enumerations.md)   
 [枚举概述](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [常量概述](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [如何：声明枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)