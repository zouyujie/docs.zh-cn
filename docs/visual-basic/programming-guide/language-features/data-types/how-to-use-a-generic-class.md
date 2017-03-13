---
title: "如何：使用泛型类 (Visual Basic) | Microsoft Docs"
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
  - "类型参数, 定义"
  - "数据类型参数, 定义"
  - "参数 [Visual Basic], 数据类型"
  - "Of 关键字, 使用"
  - "泛型参数"
  - "数据类型参数"
  - "泛型 [Visual Basic], 关于泛型"
  - "数据类型 [Visual Basic], 作为参数"
  - "数据类型 [Visual Basic], 作为参数"
  - "参数, 类型"
  - "类型 [Visual Basic], 泛型"
  - "参数, 泛型"
  - "泛型 [Visual Basic], 创建泛型类型"
  - "数据类型参数"
  - "参数, 数据类型"
  - "数据类型参数, 定义"
  - "类型实参, 定义"
  - "自变量 [Visual Basic], 类型"
ms.assetid: 242dd2a6-86c4-4ce7-83f2-f2661803f752
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# 如何：使用泛型类 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

采用 *类型参数* 的类称为 *泛型类*。 如果使用一个泛型类，则可以通过为每个形参提供 *类型实参* ，从该类生成 *构造类* 。 随后可以声明构造类类型的一个变量，可以创建构造类的实例并将它分配给该变量。  
  
 除了类之外，你还可以定义和使用泛型结构、接口、过程和委托。  
  
 下面的过程采用在 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] 中定义的一个泛型类，并且通过它创建一个实例。  
  
### <a name="to-use-a-class-that-takes-a-type-parameter"></a>使用采用类型参数的类  
  
1.  在源文件的起始处，含入 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)以导入 <xref:System.Collections.Generic?displayProperty=fullName> 命名空间。 由此可以引用 <xref:System.Collections.Generic.Queue%601?displayProperty=fullName> 类，而不必完全限定它即可将它与其他队列类（如 <xref:System.Collections.Queue?displayProperty=fullName>）区分开来。  
  
2.  以正常方式创建对象，但是紧接在类名之后添加 `(Of` `type``)` 。  
  
     下面的示例使用相同类 (<xref:System.Collections.Generic.Queue%601?displayProperty=fullName>) 创建保存不同数据类型的项的两个队列对象。 它将项添加到每个队列末尾，然后从每个队列的前面删除并显示项。  
  
     [!code-vb[VbVbalrDataTypes#9](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/how-to-use-a-generic-class_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Visual Basic 中的泛型类型](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md)   
 [Of](../../../../visual-basic/language-reference/statements/of-clause.md)   
 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [如何：定义可对不同数据类型提供相同功能的类](../../../../visual-basic/programming-guide/language-features/data-types/how-to-define-a-class-that-can-provide-identical-functionality.md)   
 [迭代器](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)