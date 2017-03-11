---
title: "代码中的特殊字符 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.)"
  - "vb.("
  - "vb.colon"
  - "vb.!"
  - "vb.."
  - "vb.:"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "! 运算符"
  - ". 运算符"
  - ": 分隔符"
  - "加法运算符"
  - "冒号 (:)"
  - "串联运算符, 代码中的特殊字符"
  - "串联运算符, 与加法运算符"
  - "字典访问运算符"
  - "点运算符 (.)"
  - "感叹号运算符 (!)"
  - "感叹号"
  - "成员访问运算符"
  - "运算符 [Visual Basic], 字典访问"
  - "运算符 [Visual Basic], 成员访问"
  - "括号, 在代码中使用"
  - "代码中的句号字符"
  - "分隔符"
  - "分隔符, 在代码中使用"
  - "特殊字符, 在代码中"
  - "Visual Basic 代码, 特殊字符"
ms.assetid: 310dce0c-45b5-4e0d-83e9-32df258d2a3e
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# 代码中的特殊字符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

有时必须在代码中使用特殊字符，即非字母或数字字符。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 字符集中的标点符号和特殊字符各有其用途，从组织程序文本到定义编译器或已编译程序所执行的任务。  它们不指定要执行的操作。  
  
## 括号  
 在定义过程（如 `Sub` 或 `Function`）时使用括号。  必须将所有过程参数列表放入括号内。  括号还可用来为变量或参数进行逻辑分组，特别是用来重写复杂表示式中运算符的默认优先顺序。  下面的示例阐释了这一点。  
  
 [!code-vb[VbVbcnConventions#11](../../../visual-basic/programming-guide/language-features/codesnippet/visualbasic/special-characters-in-code_1.vb)]  
  
 执行完前面的代码后，`d` 的值为 8.225，而 `e` 的值为 3。  计算 `d` 时使用默认优先顺序，即先 `/` 后 `+`，它等同于 `d = b + (c / a)`。  计算 `e` 值时使用的括号重写了默认优先顺序。  
  
## 分隔符  
 顾名思义，分隔符用于分隔各部分代码。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的分隔符为冒号 \(`:`\)。  当您想将多条语句放在一行而非多行上时，可以使用分隔符。  这样可以节省空间，并增强代码的可读性。  下面的示例演示了用冒号隔开的三个语句。  
  
 [!code-vb[VbVbcnConventions#12](../../../visual-basic/programming-guide/language-features/codesnippet/visualbasic/special-characters-in-code_2.vb)]  
  
 有关更多信息，请参见[如何：在代码中拆分和合并语句](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)。  
  
 冒号 \(`:`\) 字符还用于标识语句标签。  有关更多信息，请参见[如何：标记语句](../../../visual-basic/programming-guide/program-structure/how-to-label-statements.md)。  
  
## 串联  
 `&` 运算符用于将字符串“串联”或链接到一起。  不要把它和 `+` 运算符混淆，后者用于将数值相加。  如果使用 `+` 运算符串联数值，可能会得到错误的结果。  下面的示例说明了这一点。  
  
 [!code-vb[VbVbcnConventions#13](../../../visual-basic/programming-guide/language-features/codesnippet/visualbasic/special-characters-in-code_3.vb)]  
  
 执行完前面的代码后，`resultA` 的值为 21.01，而 `resultB` 的值为“10.0111”。  
  
## 成员访问运算符  
 若要访问某种类型的成员，请在类型名称和成员名称之间使用点 \(`.`\) 或惊叹号 \(`!`\) 运算符。  
  
### 点 \(.\)运算符  
 对于类、结构、接口或枚举，`.` 运算符用作成员访问运算符。  该成员可以是字段、属性、事件或方法。  下面的示例阐释了这一点。  
  
 [!code-vb[VbVbcnConventions#14](../../../visual-basic/programming-guide/language-features/codesnippet/visualbasic/special-characters-in-code_4.vb)]  
  
### 惊叹号 \(\!\)运算符  
 仅对类或接口，`!` 运算符用作字典访问运算符。  该类或接口必须有一个接受单个 `String` 参数的默认属性。  `!` 运算符后面紧跟着的标识符成为传递给默认属性的字符串形式的参数值。  下面的示例说明了这一点。  
  
 [!code-vb[VbVbcnConventions#15](../../../visual-basic/programming-guide/language-features/codesnippet/visualbasic/special-characters-in-code_5.vb)]  
  
 `MsgBox` 的三个输出行均显示 `32856` 这个值。  第一行使用对属性 `index` 的传统访问，第二行利用 `index` 是类 `hasDefault` 的默认属性这一情况，第三行使用对类的字典访问。  
  
 请注意，`!` 运算符的第二个操作数必须是不带双引号 \(`" "`\) 的有效 Visual Basic 标识符。  换句话说，不能使用字符串或字符串变量。  以下对 `MsgBox` 调用最后一行的更改将产生错误，因为 `"X"` 是用引号引起来的字符串。  
  
 `"Dictionary access returns " & hD!"X")`  
  
> [!NOTE]
>  对默认集合的引用必须是显式的。  特别是，不能对后期绑定变量使用 `!` 运算符。  
  
 `!` 字符也可用作 `Single` 类型的字符。  
  
## 请参阅  
 [程序结构和代码约定](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [类型字符](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)