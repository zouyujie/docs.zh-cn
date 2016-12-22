---
title: "C# Features That Support LINQ | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "LINQ [C#], features supporting LINQ"
ms.assetid: 524b0078-ebfd-45a7-b390-f2ceb9d84797
caps.latest.revision: 23
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# C# Features That Support LINQ
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

下一节介绍 C\# 3.0 中引入的新语言构造。  虽然这些新功能在一定程度上都用于 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询，但并不限于 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]，如果认为有用，在任何情况下都可以使用这些新功能。  
  
## 查询表达式  
 查询表达式使用类似于 SQL 或 XQuery 的声明性语法来查询 IEnumerable 集合。  在编译时，查询语法转换为对 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 提供程序的标准查询运算符扩展方法实现的方法调用。  应用程序通过使用 `using` 指令指定适当的命名空间来控制范围内的标准查询运算符。  下面的查询表达式获取一个字符串数组，按字符串中的第一个字符对字符串进行分组，然后对各组进行排序。  
  
```  
var query = from str in stringArray  
            group str by str[0] into stringGroup  
            orderby stringGroup.Key  
            select stringGroup;  
```  
  
 有关更多信息，请参见 [LINQ 查询表达式](../../../../visual-basic/reference/command-line-compiler/index.md)。  
  
## 隐式类型化变量 \(var\)  
 不必在声明并初始化变量时显式指定类型，您可以使用 [var](../../../../csharp/language-reference/keywords/var.md) 修饰符来指示编译器推断并分配类型，如下所示：  
  
```  
var number = 5;  
var name = "Virginia";  
var query = from str in stringArray  
            where str[0] == 'm'  
            select str;  
```  
  
 声明为 `var` 的变量与显式指定其类型的变量一样都是强类型。  通过使用 `var`，可以创建匿名类型，但它可用于任何局部变量。  也可以使用隐式类型声明数组。  
  
 有关更多信息，请参见[隐式类型的局部变量](../../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)。  
  
## 对象和集合初始值设定项  
 通过对象和集合初始值设定项，初始化对象时无需为对象显式调用构造函数。  初始值设定项通常用在将源数据投影到新数据类型的查询表达式中。  假定一个类名为 `Customer`，具有公共 `Name` 和 `Phone` 属性，可以按下列代码中所示使用对象初始值设定项：  
  
```  
Customer cust = new Customer { Name = "Mike", Phone = "555-1212" };  
```  
  
 有关更多信息，请参见[对象和集合初始值设定项](../../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)。  
  
## 匿名类型  
 匿名类型由编译器构建，且类型名称只可用于编译器。  匿名类型提供了一种在查询结果中临时分组一组属性的方便方法，无需定义单独的命名类型。  使用新的表达式和对象初始值设定项初始化匿名类型，如下所示：  
  
```  
select new {name = cust.Name, phone = cust.Phone};  
```  
  
 有关更多信息，请参见[匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
## 扩展方法  
 扩展方法是一种可与类型关联的静态方法，因此可以像实例方法那样对类型调用它。  实际上，此功能使您能够将新方法“添加”到现有类型，而不会实际修改它们。  标准查询运算符是一组扩展方法，它们为实现 <xref:System.Collections.Generic.IEnumerable%601> 的任何类型提供 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询功能。  
  
 有关更多信息，请参见[扩展方法](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md)。  
  
## Lambda 表达式  
 Lambda 表达式是一种内联函数，该函数使用 \=\> 运算符将输入参数与函数体分离，并且可以在编译时转换为委托或表达式树。  在 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 编程中，在您对标准查询运算符进行直接方法调用时，会遇到 lambda 表达式。  
  
 有关更多信息，请参见：  
  
-   [匿名函数](../../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md)  
  
-   [Lambda 表达式](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)  
  
-   [表达式树](../Topic/Expression%20Trees%20\(C%23%20and%20Visual%20Basic\).md)  
  
## 自动实现的属性  
 通过自动实现的属性，可以更简明地声明属性。  当您如下面的示例中所示声明属性时，编译器将创建一个私有的匿名支持字段，该字段只能通过属性 getter 和 setter 进行访问。  
  
```  
public string Name {get; set;}  
```  
  
 有关更多信息，请参见[自动实现的属性](../../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)。  
  
## 请参阅  
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Visual Basic Features That Support LINQ](../../../../visual-basic/programming-guide/concepts/linq/features-that-support-linq.md)