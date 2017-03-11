---
title: "/= 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb./="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/= 运算符 [Visual Basic]"
  - "赋值语句, 复合"
  - "复合赋值语句"
  - "运算符 /="
  - "语句 [Visual Basic], 复合赋值"
ms.assetid: a1e22d0e-8380-4761-9da1-84fb51c34821
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# /= 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

变量或属性的值除以表达式的值，并将浮点型结果赋给该变量或属性。  
  
## 语法  
  
```  
  
variableorproperty /= expression  
```  
  
## 部件  
 `variableorproperty`  
 必选。  任何数值变量或属性。  
  
 `expression`  
 必选。  任何数值表达式。  
  
## 备注  
 `/=` 运算符左边的元素可以是简单的标量变量，也可以是属性或数组元素。  变量或属性不能为 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)。  
  
 `/=` 运算符按该表达式的值先拆分为多个变量或属性的值 \(在运算符的左边\) \(在运算符的右侧\)。  运算符然后将该操作的浮点结果赋给变量或属性。  
  
 此语句将对象分配 `Double` 左侧的值赋给变量或属性。  如果 `Option Strict` 是 `On`，`variableorproperty` 则必须是 `Double`。  如果 `Option Strict` 为 `Off`，Visual Basic 会执行一个隐式转换，然后将得到的值赋给 `variableorproperty`，运行时可能会出现错误。  有关更多信息，请参见[扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)和 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)。  
  
## 重载  
 [\/ 运算符](../../../visual-basic/language-reference/operators/floating-point-division-operator.md) 可以被“重载”，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  重载 `/` 运算符会影响 `/=` 运算符的行为。  如果代码在重载了 `/` 的类或结构上使用 `/=`，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下例使用 `/=` 运算符将一个 `Integer` 变量除以第二个该变量，并将所得的商赋给第一个变量。  
  
 [!code-vb[VbVbalrOperators#17](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/floating-point-division-_0_1.vb)]  
  
## 请参阅  
 [\/ 运算符](../../../visual-basic/language-reference/operators/floating-point-division-operator.md)   
 [\\\= 运算符](../../../visual-basic/language-reference/operators/subtraction-assignment-operator.md)   
 [赋值运算符](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)