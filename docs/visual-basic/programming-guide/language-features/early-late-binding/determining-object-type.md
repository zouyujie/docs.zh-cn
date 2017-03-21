---
title: "确定对象类型 (Visual Basic) | Microsoft Docs"
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
  - "类 [Visual Basic], 发现对象的所属"
  - "对象变量, 测试值"
  - "对象 [Visual Basic], 类型确定"
  - "TypeName 函数"
  - "TypeOf...Is 表达式, 运行时的对象类型"
  - "类型 [Visual Basic], 确定 Visual Basic 对象类型"
ms.assetid: d95e7ad1-cd63-41d6-9a28-d7a1380d49c1
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 确定对象类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

一般对象变量（即声明为 `Object` 的变量）可以包含来自任何类的对象。  使用 `Object` 类型的变量时，可能需要根据对象的类采取不同的操作；例如，某些对象可能不支持特定的属性或方法。  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供以下两种方法来确定存储在对象变量中的对象类型：`TypeName` 函数和 `TypeOf...Is` 运算符。  
  
## TypeName 和 TypeOf...Is  
 `TypeName` 函数返回一个字符串，当您需要存储或显示对象的类名时，它是最佳选择，如以下代码片段中所示：  
  
 [!code-vb[VbVbalrOOP#92](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_1.vb)]  
  
 `TypeOf...Is` 运算符是测试对象类型的最佳选择，因为它比使用 `TypeName` 的等效字符串比较快得多。  以下代码片段在 `If...Then...Else` 语句中使用 `TypeOf...Is`：  
  
 [!code-vb[VbVbalrOOP#93](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_2.vb)]  
  
 这里应该提醒您几句。  如果对象属于某一特定类型或是从特定类型派生的，则 `TypeOf...Is` 运算符会返回 `True`。  您用 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 所做的几乎每项操作都涉及对象（包括通常不被视为对象的某些元素，例如字符串和整数）。  这些对象均从 <xref:System.Object> 派生并从其中继承方法。  当向 `TypeOf...Is` 运算符传递一个 `Integer` 并用 `Object` 计算它时，它返回 `True`。  下面的示例报告参数 `InParam` 既是 `Object` 也是 `Integer`：  
  
 [!code-vb[VbVbalrOOP#94](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_3.vb)]  
  
 下面的示例同时使用 `TypeOf...Is` 和 `TypeName` 来确定在 `Ctrl` 参数中传递给它的对象类型。  `TestObject` 过程使用三种不同的控件来调用 `ShowType`。  
  
#### 运行示例  
  
1.  创建新的 Windows 应用程序项目并将 <xref:System.Windows.Forms.Button> 控件、<xref:System.Windows.Forms.CheckBox> 控件和 <xref:System.Windows.Forms.RadioButton> 控件添加到窗体中。  
  
2.  从窗体上的按钮调用 `TestObject` 过程。  
  
3.  向窗体中添加以下代码：  
  
     [!code-vb[VbVbalrOOP#95](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_4.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Information.TypeName%2A>   
 [使用字符串名调用属性或方法](../../../../visual-basic/programming-guide/language-features/early-late-binding/calling-a-property-or-method-using-a-string-name.md)   
 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [If...Then...Else 语句](../../../../visual-basic/language-reference/statements/if-then-else-statement.md)   
 [String 数据类型](../../../../visual-basic/language-reference/data-types/string-data-type.md)   
 [Integer 数据类型](../../../../visual-basic/language-reference/data-types/integer-data-type.md)