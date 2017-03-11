---
title: "比较运算符 (Visual Basic) | Microsoft Docs"
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
  - "比较运算符"
  - "比较运算符, 比较数值"
  - "比较运算符, 比较对象"
  - "比较运算符, 比较字符串"
  - "数字, 比较"
  - "数值, 比较"
  - "对象 [Visual Basic], 比较"
  - "运算符 [Visual Basic], 比较"
  - "字符串比较 [Visual Basic]"
  - "字符串比较 [Visual Basic], 运算符"
  - "字符串 [Visual Basic], 比较"
  - "Visual Basic 代码, 运算符"
ms.assetid: 0b570339-5407-474f-8421-e183a8b303ee
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 比较运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

比较运算符比较两个表达式，并返回表示两个值之间关系的 `Boolean` 值。  有用于比较数值的运算符、用于比较字符串的运算符以及用于比较对象的运算符。  下面讨论所有这三种类型的运算符。  
  
## 比较数值  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 使用六个数值比较运算符比较数值。  每个运算符以两个表达式作为操作数，这两个表达式的计算结果均为数值。  下表列出所有运算符及其示例。  
  
|运算符|测试的条件|示例|  
|---------|-----------|--------|  
|`=`（相等）|第一个表达式的值与第二个表达式的值是否相等？|`23`   `=`   `33    ' False`<br /><br /> `23`   `=`   `23    ' True`<br /><br /> `23`   `=`   `12    ' False`|  
|`<>`（不等）|第一个表达式的值与第二个表达式的值是否不等？|`23`   `<>`   `33    ' True`<br /><br /> `23`   `<>`   `23    ' False`<br /><br /> `23`   `<>`   `12    ' True`|  
|`<`（小于）|第一个表达式的值是否比第二个表达式的值小？|`23`   `<`   `33    ' True`<br /><br /> `23`   `<`   `23    ' False`<br /><br /> `23`   `<`   `12    ' False`|  
|`>`（大于）|第一个表达式的值是否比第二个表达式的值大？|`23`   `>`   `33    ' False`<br /><br /> `23`   `>`   `23    ' False`<br /><br /> `23`   `>`   `12    ' True`|  
|`<=`（小于或等于）|第一个表达式的值是否小于或等于第二个表达式的值？|`23`   `<=`   `33    ' True`<br /><br /> `23`   `<=`   `23    ' True`<br /><br /> `23`   `<=`   `12    ' False`|  
|`>=`（大于或等于）|第一个表达式的值是否大于或等于第二个表达式的值？|`23`   `>=`   `33    ' False`<br /><br /> `23`   `>=`   `23    ' True`<br /><br /> `23`   `>=`   `12    ' True`|  
  
## 比较字符串  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 使用 [Like 运算符](../../../../visual-basic/language-reference/operators/like-operator.md)和数值比较运算符比较字符串。  使用 `Like` 运算符可指定模式。  之后，就能将字符串与指定的模式进行比较，如果匹配，结果为 `True`。  否则，结果为 `False`。  数值运算符使您得以根据 `String` 值的排序顺序比较它们，如下例所示：  
  
 `"73" < "9"`  
  
 `' The result of the preceding comparison is True.`  
  
 上例中的结果为 `True`，因为第一个字符串中的第一个字符的排序位于第二个字符串中的第一个字符之前。  如果第一个字符相等，将继续比较两个字符串中的下一个字符，依此类推。  您也可以使用相等运算符测试字符串是否相等，如下例所示。  
  
 `"734" = "734"`  
  
 `' The result of the preceding comparison is True.`  
  
 如果一个字符串是另一个字符串的前缀，如“aa”和“aaa”，则认为较长的字符串大于较短的字符串。  下面的示例阐释了这一点。  
  
 `"aaa" > "aa"`  
  
 `' The result of the preceding comparison is True.`  
  
 排序顺序基于二进制比较或文本比较，具体取决于 `Option Compare` 的设置。  有关更多信息，请参见[Option Compare 语句](../../../../visual-basic/language-reference/statements/option-compare-statement.md)。  
  
## 比较对象  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 用 [Is 运算符](../../../../visual-basic/language-reference/operators/is-operator.md) 和 [IsNot 运算符](../../../../visual-basic/language-reference/operators/isnot-operator.md)比较两个对象引用变量。  使用其中任一运算符均可确定两个引用变量是否引用相同的对象实例。  下面的示例阐释了这一点。  
  
 [!code-vb[VbVbalrOperators#65](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/comparison-operators_1.vb)]  
  
 在上例中，由于两个变量引用同一个实例，因此 `x Is y` 计算结果为 `True`。  将此结果与下面的示例对比。  
  
 [!code-vb[VbVbalrOperators#66](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/comparison-operators_2.vb)]  
  
 在上例中，虽然两个变量引用同一类型对象，但它们引用该类型的不同实例，因此 `x Is y` 计算结果为 `False`。  
  
 在要测试指向不同实例的两个对象时，使用 `IsNot` 运算符可避免出现从语法角度而言不太妥当的 `Not` 和 `Is` 组合。  下面的示例阐释了这一点。  
  
 [!code-vb[VbVbalrOperators#67](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/comparison-operators_3.vb)]  
  
 在上例中，`If a IsNot b` 等同于 `If Not a Is b`。  
  
### 比较对象类型  
 可以用 `TypeOf`...`Is` 表达式测试对象是否为特定类型。  语法如下所示：  
  
 `TypeOf <objectexpression> Is <typename>`  
  
 当 `typename` 指定接口类型时，如果对象实现该接口类型，则 `TypeOf`...`Is` 表达式将返回 `True`。  当 `typename` 为类类型时，如果对象是指定类的实例或者是从指定类派生的类的实例，表达式将返回 `True`。  下面的示例阐释了这一点。  
  
 [!code-vb[VbVbalrOperators#68](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/comparison-operators_4.vb)]  
  
 在上例中，由于 `x` 的类型是从 `Control` 继承而来的 `Button`，因此 `TypeOf x Is Control` 表达式的计算结果为 `True`。  
  
 有关更多信息，请参见 [TypeOf 运算符](../../../../visual-basic/language-reference/operators/typeof-operator.md)。  
  
## 请参阅  
 [值的比较](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)   
 [比较运算符](../../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [运算符](../../../../visual-basic/language-reference/operators/index.md)   
 [算术运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [串联运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)   
 [Visual Basic 中的逻辑运算符和位运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)