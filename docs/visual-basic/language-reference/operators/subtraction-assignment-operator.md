---
title: "\= 运算符 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "\="
  - "vb.\="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "\= 运算符 [Visual Basic]"
  - "赋值语句, 复合"
  - "复合赋值语句"
  - "运算符 \= [Visual Basic]"
  - "语句 [Visual Basic], 复合赋值"
ms.assetid: 5ead0c37-ae50-48f7-8435-8e341d81cae1
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# \= 运算符
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

变量或属性的值除以表达式的值，并将整数结果赋给该变量或属性。  
  
## 语法  
  
```  
  
variableorproperty \= expression  
```  
  
## 部件  
 `variableorproperty`  
 必选。  任何数值变量或属性。  
  
 `expression`  
 必选。  任何数值表达式。  
  
## 备注  
 `\=` 运算符左边的元素可以是简单的标量变量，也可以是属性或数组元素。  变量或属性不能为 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)。  
  
 `\=` 运算符按值将一个变量或属性的值在其左在其右侧，然后将整数结果赋给变量或属性在其左  
  
 有关整数除法的详细信息，请参见 [\\ 运算符](../../../visual-basic/language-reference/operators/integer-division-operator.md)。  
  
## 重载  
 `\` 运算符可以被“重载”，这意味着当操作数的类型为类或结构时，该类或结构可以重新定义其行为。  重载 `\` 运算符会影响 `\=` 运算符的行为。  如果对重载了 `\` 的类或结构使用 `\=`，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `\=` 运算符将一个 `Integer` 变量除以另一个这种类型的变量，并把整数结果赋给第一个变量。  
  
 [!code-vb[VbVbalrOperators#19](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/subtraction-assignment-o_2_1.vb)]  
  
## 请参阅  
 [\\ 运算符](../../../visual-basic/language-reference/operators/integer-division-operator.md)   
 [\/\= 运算符](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)   
 [赋值运算符](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)