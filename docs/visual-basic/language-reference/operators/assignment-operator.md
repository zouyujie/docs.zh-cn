---
title: "= 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Assign"
  - "vb.="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "= 赋值语句 [Visual Basic]"
  - "= 运算符 [Visual Basic]"
ms.assetid: 2dac2e49-86c8-42f8-80c1-458452fb5e29
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# = 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

给变量或属性赋值。  
  
## 语法  
  
```  
  
variableorproperty = value  
```  
  
## 部件  
 `variableorproperty`  
 任何可写的变量或任何属性。  
  
 `value`  
 任何文本、常数或表达式。  
  
## 备注  
 等号 \(`=`\) 左边的元素可以是简单的标量变量，也可以是属性或数组元素。  变量或属性不能为 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)。  `=` 运算符将其右边的值赋给其左边的变量或属性。  
  
> [!NOTE]
>  `=` 运算符也被用作比较运算符。  有关详细信息，请参见[比较运算符](../../../visual-basic/language-reference/operators/comparison-operators.md)。  
  
## 重载  
 `=` 运算符只能作为关系比较运算符重载，而不能作为赋值运算符重载。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例演示赋值运算符。  右边的值赋给左边的变量。  
  
 [!code-vb[VbVbalrOperators#9](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/assignment-operator_1.vb)]  
  
## 请参阅  
 [&\= 运算符](../../../visual-basic/language-reference/operators/and-assignment-operator.md)   
 [\*\= 运算符](../../../visual-basic/language-reference/operators/multiplication-assignment-operator.md)   
 [\+\= 运算符](../../../visual-basic/language-reference/operators/addition-assignment-operator.md)   
 [\-\= 运算符](../../../visual-basic/language-reference/operators/integer-division-assignment-operator.md)   
 [\/\= 运算符](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)   
 [\\\= 运算符](../../../visual-basic/language-reference/operators/subtraction-assignment-operator.md)   
 [^\= 运算符](../../../visual-basic/language-reference/operators/exponentiation-assignment-operator.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)   
 [比较运算符](../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)   
 [局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)