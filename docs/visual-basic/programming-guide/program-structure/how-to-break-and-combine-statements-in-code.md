---
title: "如何：在代码中拆分和合并语句 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb._"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "冒号 (:)"
  - "续行符"
  - "_ 续行符"
  - ": 行分隔符"
  - "Visual Basic 代码, 其中的换行符"
  - "Visual Basic 代码, 换行符"
  - "Visual Basic 代码, 续行符"
  - "长代码行"
  - "行终止符"
  - "续行序列"
  - "下划线, 代码形式"
  - "语句 [Visual Basic], 其中的续行符"
  - "换行符, 代码形式"
  - "续行符"
  - "Visual Basic 代码, 其中的续行符"
  - "语句 [Visual Basic], 其中的换行符"
ms.assetid: dea01dad-a8ac-484a-bb3a-8c45a1b1eccc
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# 如何：在代码中拆分和合并语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

编写代码时，时常会创建一些很长的语句，使得您必须在代码编辑器中进行水平滚动。  尽管这不会影响该方法您的代码运行时，它使得难以让您或任何人都可以读取代码，则监视器上显示  在这种情况下，应该考虑将单个长语句拆分为几行。  
  
### 将单个语句拆分为多行  
  
-   在您要将该行断开的点处使用行继续符，它是一个下划线 \(`_`\)。  必须紧跟在消去并由行结束符后面紧跟一个下划线 \(回车\)。  
  
    > [!NOTE]
    >  有时，因此，如果省略行继续符，Visual Basic 编译器将在下一代码行隐式继续该语句。  有关语法元素列表可以省略行继续符，请参见中的“隐式行继续”[语句](../../../visual-basic/programming-guide/language-features/statements.md)。  
  
     在下面的示例中，语句被拆分为四行。除最后一行外，前三行都以行继续符结尾。  
  
     [!code-vb[VbVbcnConventions#20](../../../visual-basic/programming-guide/language-features/codesnippet/visualbasic/how-to-break-and-combine_1.vb)]  
  
     这样可以使代码更易于阅读，不管是在联机状态下还是在打印后。  
  
     行继续符必须是行的最后一个字符。  您不能跟有任何其他内容在同一行。  
  
     存在一些限制。可以使用行继续字符的位置；例如，不能在参数名中间使用它。  可以用行继续符拆分一个参数列表，但单个参数名必须保持完整。  
  
     使用行继续字符，则不能继续注释。  编译器将不检查在注释的字符特殊意义的。  要将注释拆分为多行，请在每行的前面重复使用注释符号 \(`'`\)。  
  
 虽然将每个语句在单独的行是推荐使用的方法，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 同样允许在同一行上放置多个语句。  
  
### 将多个语句置于同一行  
  
-   用冒号 \(`:`\) 将各语句分开，如下面的示例所示。  
  
     [!code-vb[VbVbcnConventions#10](../../../visual-basic/programming-guide/language-features/codesnippet/visualbasic/how-to-break-and-combine_2.vb)]  
  
## 请参阅  
 [程序结构和代码约定](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)