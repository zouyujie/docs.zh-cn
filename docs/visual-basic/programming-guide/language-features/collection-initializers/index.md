---
title: "集合初始值设定项 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.CollectionInitializer"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "集合初始值设定项 [Visual Basic]"
ms.assetid: a9290329-77b0-4fdf-ae75-8fc17287f469
caps.latest.revision: 23
caps.handback.revision: 23
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 集合初始值设定项 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

“集合初始值设定项”提供了短语法，供您创建集合并用一组初始值填充它。  当您从一组已知值创建集合时，集合初始值设定项十分有用。这组已知值如菜单选项或类别列表、一组初始数值、日期或月份名称之类字段串的静态列表或地理位置的静态列表（如用于验证目的的省\/市\/自治区列表）。  
  
 有关集合的更多信息，请参见 [集合](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 通过使用 `From` 关键字后跟大括号 \(`{}`\)，可以标识集合初始值设定项。  这与 [数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)中介绍的数组文本语法类似。  下面的示例演示使用集合初始值设定项创建集合的各种方法。  
  
 [!code-vb[VbVbalrCollectionInitializers#1](../../../../visual-basic/programming-guide/language-features/collection-initializers/codesnippet/VisualBasic/index_1.vb)]  
  
> [!NOTE]
>  C\# 也提供集合初始值设定项。  C\# 集合初始值设定项提供与 Visual Basic 集合初始值设定项相同的功能。  有关 C\# 初始值设定项的更多信息，请参见[对象和集合初始值设定项](../../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)。  
  
## 语法  
 集合初始值设定项由逗号分隔值列表组成，这些值用大括号 \(`{}`\) 括起，前面带有 `From` 关键字，如下面的代码所示。  
  
 [!code-vb[VbVbalrCollectionInitializers#2](../../../../visual-basic/programming-guide/language-features/collection-initializers/codesnippet/VisualBasic/index_2.vb)]  
  
 在创建集合（如 <xref:System.Collections.Generic.List%601> 或 <xref:System.Collections.Generic.Dictionary%602>）时，必须在集合初始值设定项前面提供集合类型，如下面的代码所示。  
  
 [!code-vb[VbVbalrCollectionInitializers#13](../../../../visual-basic/programming-guide/language-features/collection-initializers/codesnippet/VisualBasic/index_3.vb)]  
  
> [!NOTE]
>  不能通过组合集合初始值设定项和对象初始值设定项来初始化同一集合对象。  可以使用对象初始值设定项来初始化集合初始值设定项中的对象。  
  
## 使用集合初始值设定项创建集合  
 在使用集合初始值设定项创建集合时，在集合初始值设定项中提供的每个值都将传递给该集合相应的 `Add` 方法。  例如，如果使用集合初始值设定项创建 <xref:System.Collections.Generic.List%601>，则集合初始值设定项中的每个字符串值都将传递给 <xref:System.Collections.Generic.List%601.Add%2A> 方法。  若要使用集合初始值设定项创建集合，指定类型必须是有效的集合类型。  有效集合类型的示例包括实现 <xref:System.Collections.Generic.IEnumerable%601> 接口或继承 <xref:System.Collections.CollectionBase> 类的类。  此外，指定类型还必须公开符合以下条件的 `Add` 方法。  
  
-   调用集合初始值设定项的范围中必须存在可用的 `Add` 方法。  如果您在可访问集合的非公共方法的方案中使用集合初始值设定项，则 `Add` 方法不必是公共的。  
  
-   `Add` 方法必须是集合类的实例成员或 `Shared` 成员，或者必须是扩展方法。  
  
-   必须存在可按照重载决策规则与集合初始值设定项中所提供的类型匹配的 `Add` 方法。  
  
 例如，下面的代码示例演示如何使用集合初始值设定项创建 `List(Of Customer)` 集合。  在运行该代码时，每个 `Customer` 对象都将传递给泛型列表的 `Add(Customer)` 方法。  
  
 [!code-vb[VbVbalrCollectionInitializers#9](../../../../visual-basic/programming-guide/language-features/collection-initializers/codesnippet/VisualBasic/index_4.vb)]  
  
 下面的代码示例演示不使用集合初始值设定项的等效代码。  
  
 [!code-vb[VbVbalrCollectionInitializers#10](../../../../visual-basic/programming-guide/language-features/collection-initializers/codesnippet/VisualBasic/index_5.vb)]  
  
 如果集合具有 `Add` 方法并且该方法包含与 `Customer` 对象的构造函数相匹配的参数，则可以在集合初始值设定项中嵌套 `Add` 方法的参数值，如下一节内容所述。  如果集合没有这样的 `Add` 方法，则可以采用扩展方法形式创建一个。  有关如何以扩展方法形式为集合创建 `Add` 方法的示例，请参见[如何：创建集合初始值设定项所使用的 Add 扩展方法](../../../../visual-basic/programming-guide/language-features/collection-initializers/how-to-create-an-add-extension-method-used-by-a-collection-initializer.md)。  有关如何创建可与集合初始值设定项一起使用的自定义集合的示例，请参见[如何：创建集合初始值设定项所使用的集合](../../../../visual-basic/programming-guide/language-features/collection-initializers/how-to-create-a-collection-used-by-a-collection-initializer.md)。  
  
## 嵌套集合初始值设定项  
 可以在集合初始值设定项中嵌套值，从而为所创建的集合标识 `Add` 方法的特定重载。  传递给 `Add` 方法的值必须由逗号分隔，并用大括号 \(`{}`\) 括起，就像在数组文本或集合初始值设定项中的做法一样。  
  
 在使用嵌套值创建集合时，嵌套值列表的每个元素都将作为参数传递给与这些元素类型匹配的 `Add` 方法。  例如，下面的代码示例创建一个 <xref:System.Collections.Generic.Dictionary%602>，在该集合中键类型为 `Integer`，值类型为 `String`。  每个嵌套值列表都与 `Dictionary` 的 <xref:System.Collections.Generic.Dictionary%602.Add%2A> 方法相匹配。  
  
 [!code-vb[VbVbalrCollectionInitializers#5](../../../../visual-basic/programming-guide/language-features/collection-initializers/codesnippet/VisualBasic/index_6.vb)]  
  
 上一代码示例与下面的代码是等效的。  
  
 [!code-vb[VbVbalrCollectionInitializers#6](../../../../visual-basic/programming-guide/language-features/collection-initializers/codesnippet/VisualBasic/index_7.vb)]  
  
 仅将第一个嵌套层中的嵌套值列表发送到集合类型的 `Add` 方法。  更深的嵌套层被视为数组文本，因而其中的嵌套值列表不与任何集合的 `Add` 方法相匹配。  
  
## 相关主题  
  
|||  
|-|-|  
|标题|说明|  
|[如何：创建集合初始值设定项所使用的 Add 扩展方法](../../../../visual-basic/programming-guide/language-features/collection-initializers/how-to-create-an-add-extension-method-used-by-a-collection-initializer.md)|演示如何创建调用可用于填充值的集合从集合初始值设定项的 `Add` 的扩展方法。|  
|[如何：创建集合初始值设定项所使用的集合](../../../../visual-basic/programming-guide/language-features/collection-initializers/how-to-create-a-collection-used-by-a-collection-initializer.md)|演示如何通过包括 `Add` 方法启用对集合初始值设定项用于该集合的类实现 `IEnumerable`。|  
  
## 请参阅  
 [集合](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)   
 [数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [对象初始值设定项：命名类型和匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [New 运算符](../../../../visual-basic/language-reference/operators/new-operator.md)   
 [自动实现的属性](../../../../visual-basic/programming-guide/language-features/procedures/auto-implemented-properties.md)   
 [如何：在 Visual Basic 中初始化数组变量](../../../../visual-basic/programming-guide/language-features/arrays/how-to-initialize-an-array-variable.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [How to: Create a List of Items](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)