---
title: "Visual Basic 中的运算符优先级 | Microsoft Docs"
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
  - "算术运算符, 优先级"
  - "运算符的关联性"
  - "比较运算符, 优先级"
  - "逻辑运算符, 优先级"
  - "数学运算符"
  - "运算符优先级"
  - "运算符 [Visual Basic], 关联性"
  - "运算符 [Visual Basic], 优先级"
  - "运算符 [Visual Basic], 解析"
  - "优先级顺序"
  - "优先级, 运算符"
ms.assetid: cbbdb282-f572-458e-a520-008a675f8063
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Visual Basic 中的运算符优先级
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

如果表达式中出现几种运算，将按照预先确定的称为“运算符优先级”的顺序计算和解析各个部分。  
  
## 优先级规则  
 当表达式包含不止一种运算符时，则按照下列规则对其进行计算：  
  
-   算术运算符和串联运算符的优先级在下面列出，它们的优先级均高于比较运算符、逻辑运算符和位运算符。  
  
-   所有比较运算符具有相同的优先级，它们的优先级均高于逻辑运算符和位运算符，但低于算术运算符和串联运算符。  
  
-   逻辑运算符和位运算符的优先级在下面列出，它们的优先级均低于算术运算符、串联运算符和比较运算符。  
  
-   具有相同优先顺序的运算符将按照它们在表达式中出现的顺序从左至右进行计算。  
  
## 优先级顺序  
 运算符的计算优先级顺序如下：  
  
### 等待运算符  
 Await  
  
### 算术运算符和串联运算符  
 求幂 \(`^`\)  
  
 一元标识和非（`+`、`–`）  
  
 乘法和浮点除法（`*`、`/`）  
  
 整数除法 \(`\`\)  
  
 取模 \(`Mod`\)  
  
 添加和减号 \(`+`，`–`\)  
  
 字符串连接 \(`&`\)  
  
 算术移位（`<<`、`>>`）  
  
### 比较运算符  
 所有比较运算符（`=`、`<>`、`<`、`<=`、`>`、`>=`、`Is`、`IsNot`、`Like`、`TypeOf`...`Is`）  
  
### 逻辑运算符和位运算符  
 非 \(`Not`\)  
  
 与 \(`And`、`AndAlso`\)  
  
 或 \(`Or`、`OrElse`\)  
  
 异或 \(`Xor`\)  
  
### 注释  
 `=` 运算符只是相等比较运算符，而不是赋值运算符。  
  
 字符串连接运算符 \(`&`\) 不是算术运算符，但它在优先级方面与算术运算符属于一组。  
  
 `Is` 和 `IsNot` 运算符是对象引用比较运算符。  它们不比较两个对象的值，只确定两个对象变量是否指向相同的对象实例。  
  
## 结合性  
 当具有相同优先级的运算符（例如乘法和除法）在表达式中一起出现时，编译器将按每个运算符出现的顺序从左至右进行计算。  下面的示例阐释了这一点。  
  
```  
Dim n1 As Integer = 96 / 8 / 4  
Dim n2 As Integer = (96 / 8) / 4  
Dim n3 As Integer = 96 / (8 / 4)  
```  
  
 第一个表达式首先计算除法 96 \/ 8（结果为 12），然后计算除法 12 \/ 4，结果为 3。  因为编译器从左到右对 `n1` 中的运算求值，所以其计算结果与显式指示运算顺序的 `n2` 相同。  `n1` 和 `n2` 的结果都为 3。  相反，`n3` 的结果为 48，这是因为括号强制编译器先计算 8 \/ 4。  
  
 因此，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的运算符具有“左结合性”。  
  
## 重写优先级和结合性  
 可以使用括号强制表达式中的某些部分先于其他部分计算。  这会重写优先级顺序和左结合性。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 总是执行括号内先将外部的操作。但是，在中，除非使用在括号内，的括号在括号内，它包含普通优先级和结合性。  下面的示例阐释了这一点。  
  
```  
Dim a, b, c, d, e, f, g As Double  
a = 8.0  
b = 3.0  
c = 4.0  
d = 2.0  
e = 1.0  
f = a - b + c / d * e  
' The preceding line sets f to 7.0. Because of natural operator   
' precedence and associativity, it is exactly equivalent to the   
' following line.  
f = (a - b) + ((c / d) * e)  
' The following line overrides the natural operator precedence   
' and left associativity.  
g = (a - (b + c)) / (d * e)  
' The preceding line sets g to 0.5.  
```  
  
## 请参阅  
 [\= 运算符](../../../visual-basic/language-reference/operators/assignment-operator.md)   
 [Is 运算符](../../../visual-basic/language-reference/operators/is-operator.md)   
 [IsNot 运算符](../../../visual-basic/language-reference/operators/isnot-operator.md)   
 [Like 运算符](../../../visual-basic/language-reference/operators/like-operator.md)   
 [TypeOf 运算符](../../../visual-basic/language-reference/operators/typeof-operator.md)   
 [Await 运算符](../../../visual-basic/language-reference/operators/await-operator.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [运算符和表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)