---
title: "对象变量值 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数据类型 [Visual Basic], 对象变量"
  - "对象变量, values"
  - "values, 属于对象变量"
  - "变量 [Visual Basic], 对象"
ms.assetid: 31555704-58a3-49f1-9a0a-6421f605664f
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# 对象变量值 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

[Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md) 的变量可以引用任何类型的数据。  `Object` 变量中存储的值被保存在内存中的别处，而变量本身保存一个指向该数据的指针。  
  
## 对象分类器函数  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供的函数可返回有关 `Object` 变量所引用内容的信息，如下表所示。  
  
|功能|对象变量引用时返回 True|  
|--------|--------------------|  
|<xref:Microsoft.VisualBasic.Information.IsArray%2A>|值数组，而不是单个值|  
|<xref:Microsoft.VisualBasic.Information.IsDate%2A>|[日期数据类型](../../../../visual-basic/language-reference/data-types/date-data-type.md) 值，或可被解释为日期和时间值的字符串|  
|<xref:Microsoft.VisualBasic.Information.IsDBNull%2A>|<xref:System.DBNull> 类型的对象，它表示数据丢失或不存在|  
|<xref:Microsoft.VisualBasic.Information.IsError%2A>|异常对象，它从 <xref:System.Exception> 派生|  
|<xref:Microsoft.VisualBasic.Information.IsNothing%2A>|[Nothing](../../../../visual-basic/language-reference/nothing.md)，即当前没有对象分配给变量|  
|<xref:Microsoft.VisualBasic.Information.IsNumeric%2A>|数字，或可被解释为数字的字符串|  
|<xref:Microsoft.VisualBasic.Information.IsReference%2A>|引用类型（如字符串、数组、委托或类类型）|  
  
 使用这些函数可以避免提交给操作或过程无效值。  
  
## TypeOf 运算符  
 也可使用 [TypeOf 运算符](../../../../visual-basic/language-reference/operators/typeof-operator.md) 确定对象变量当前是否引用了特定的数据类型。  如果操作数的运行时类型是从指定类型派生的或者实现指定类型，则 `TypeOf`...`Is` 表达式计算为 `True`。  
  
 下面的示例在引用值的对象变量和引用类型上使用 `TypeOf`。  
  
```  
' The following statement puts a value type (Integer) in an Object variable.  
Dim num As Object = 10  
' The following statement puts a reference type (Form) in an Object variable.  
Dim frm As Object = New Form()  
If TypeOf num Is Long Then Debug.WriteLine("num is Long")  
If TypeOf num Is Integer Then Debug.WriteLine("num is Integer")  
If TypeOf num Is Short Then Debug.WriteLine("num is Short")  
If TypeOf num Is Object Then Debug.WriteLine("num is Object")  
If TypeOf frm Is Form Then Debug.WriteLine("frm is Form")  
If TypeOf frm Is Label Then Debug.WriteLine("frm is Label")  
If TypeOf frm Is Object Then Debug.WriteLine("frm is Object")  
```  
  
 前面的示例将下面的行写入**“调试”**窗口：  
  
 `num is Integer`  
  
 `num is Object`  
  
 `frm is Form`  
  
 `frm is Object`  
  
 对象变量 `num` 引用 `Integer` 类型的数据，`frm` 引用 <xref:System.Windows.Forms.Form> 类的对象。  
  
## 对象数组  
 可以声明和使用 `Object` 变量数组。  这在需要处理各种数据类型和对象类时很有用。  数组中的所有元素都必须具有相同的已声明数据类型。  将该数据类型声明为 `Object` 允许在数组中将对象和类实例同其他数据类型存储在一起。  
  
## 请参阅  
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [对象变量声明](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [对象变量赋值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)   
 [如何：引用对象的当前实例](../../../../visual-basic/programming-guide/language-features/variables/how-to-refer-to-the-current-instance-of-an-object.md)   
 [如何：确定对象变量引用的类型](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-what-type-an-object-variable-refers-to.md)   
 [如何：确定两个对象是否相关](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-related.md)   
 [如何：确定两个对象是否相同](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-identical.md)   
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)