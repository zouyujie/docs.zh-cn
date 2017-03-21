---
title: "重载决策 (Visual Basic) | Microsoft Docs"
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
  - "重载决策"
  - "重载, 解析"
  - "过程重载, 重载决策"
  - "过程, 调用"
  - "过程, 重载"
  - "签名, 过程"
  - "Visual Basic 代码, 过程"
ms.assetid: 766115d1-4352-45fb-859f-6063e0de0ec0
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# 重载决策 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

当 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器遇到对在多个重载版本中定义的过程的调用时，编译器必须决定调用哪一个重载。  为此，它执行以下步骤：  
  
1.  **辅助功能。**它消除具有防止调用代码调用的访问级别的任何重载。  
  
2.  **参数的数量。**它消除所定义的参数数量与调用中提供的数量不同的任何重载。  
  
3.  **参数数据类型。**编译器赋予实例方法的优先级高于扩展方法。  如果找到任何只需要经过扩大转换就能匹配过程调用的实例方法，则忽略所有扩展方法，并且编译器仅使用实例方法候选继续进行编译。  如果未找到这样的实例方法，则编译器将使用实例方法和扩展方法继续进行编译。  
  
     在此步骤中，它消除调用实参的数据类型无法转换成重载中定义的形参类型的任何重载。  
  
4.  **收缩转换。**它消除需要从调用参数类型到定义的参数类型进行双字节到单字节转换的任何重载。  无论类型检查开关 \([Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)\) 是 `On` 还是 `Off` 都是如此。  
  
5.  **最小扩大。**编译器成对考虑其余的重载。  对于每一对重载，它比较已定义参数的数据类型。  如果其中一个重载中的类型全部扩展为另一个中的相应类型，编译器消除后者。  即，它保留要求最少量扩展的重载。  
  
6.  **单个候选项。**它继续成对考虑重载，直到只剩下一个重载为止，并解析对该重载的调用。  如果编译器不能将重载减少到一个候选项，将产生错误。  
  
 下图显示决定调用哪个重载版本的进程。  
  
 ![重载解析过程的流程图](../../../../visual-basic/programming-guide/language-features/procedures/media/overloadres.gif "OverloadRes")  
在重载版本中决策  
  
 下面的示例阐释了此重载决策过程。  
  
 [!code-vb[VbVbcnProcedures#62](./codesnippet/VisualBasic/overload-resolution_1.vb)]  
  
 [!code-vb[VbVbcnProcedures#63](./codesnippet/VisualBasic/overload-resolution_2.vb)]  
  
 在第一个调用中，编译器将消除第一个重载，因为第一个参数 \(Argument\) 的类型 \(`Short`\) 将收缩为相应参数 \(Parameter\) 的类型 \(`Byte`\)。  接着，编译器消除第三个重载，因为第二个重载中的每个参数 \(Argument\) 类型（`Short` 和 `Single`）都将扩大为第三个重载中的相应类型（`Integer` 和 `Single`）。  第二个重载需要的扩大量较少，因此编译器将用它进行调用。  
  
 在第二个调用中，编译器不能根据收缩消除任何重载。  与第一个调用中的原因相同，编译器将消除第三个重载，因为它可以用参数 \(Argument\) 类型的最少扩大量调用第二个重载。  然而，编译器无法在第一个和第二个重载之间解析。  每个重载都有一个已定义的参数类型，该类型将扩大到另一个重载中的相应类型（从 `Byte` 扩大为 `Short`，但从 `Single` 扩大为 `Double`）。  编译器因此生成重载决策错误。  
  
## 重载的 Optional 和 ParamArray 参数  
 如果一个过程的两个重载具有相同的签名，只是最后一个参数在一个重载中声明为 [Optional](../../../../visual-basic/language-reference/modifiers/optional.md) 而在另一个重载中声明为 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md)，则编译器将按照以下方式解析调用：  
  
|||  
|-|-|  
|如果该调用提供的最后一个参数为|编译器将把该调用解析到将最后一个参数声明为以下类型的重载|  
|无值（省略该参数）|`Optional`|  
|一个值|`Optional`|  
|逗号分隔的列表中的两个或多个值|`ParamArray`|  
|任何长度的数组（包括空数组）|`ParamArray`|  
  
## 请参阅  
 [可选参数](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [参数数组](../../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [过程疑难解答](../../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [如何：定义一个过程的多个版本](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-multiple-versions-of-a-procedure.md)   
 [如何：调用重载过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-overloaded-procedure.md)   
 [如何：重载带有可选参数的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [如何：重载参数数量不确定的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [重载过程注意事项](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)   
 [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md)   
 [扩展方法](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)