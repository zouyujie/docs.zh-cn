---
title: "如何：使用集合初始值设定项初始化字典（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "集合初始值设定项 (C#), 用于字典"
ms.assetid: 25283922-f8ee-40dc-a639-fac30804ec71
caps.latest.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 10
---
# 如何：使用集合初始值设定项初始化字典（C# 编程指南）
<xref:System.Collections.Generic.Dictionary%602> 包含键\/值对集合。  它的 <xref:System.Collections.Generic.Dictionary%602.Add%2A> 方法采用两个参数，一个用于键，另一个用于值。  若要初始化 <xref:System.Collections.Generic.Dictionary%602> 或其 `Add` 方法采用多个参数的任何集合，请将每组参数括在大括号中，如下面的示例所示。  
  
## 示例  
 在下面的代码示例中，使用 `StudentName` 类型的实例初始化一个 <xref:System.Collections.Generic.Dictionary%602>。  
  
 [!code-cs[csProgGuideLINQ#34](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-initialize-a-dictionary-with-a-collection-initializer_1.cs)]  
  
 请注意集合的每个元素中的两对大括号。  最内层的大括号括起了 `StudentName` 的对象初始值，而最外层的大括号括起了将要添加到 `students` <xref:System.Collections.Generic.Dictionary%602> 中的键\/值对的初始值。  最后，字典的整个集合初始值括在一对大括号内。  
  
## 编译代码  
 若要运行这段代码，请将该类复制并粘贴到已经在 [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)] 中创建的 Visual C\# 控制台应用程序项目中。  默认情况下，此项目针对的是 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 3.5 版，并且具有一个对 System.Core.dll 的引用和一条针对 System.Linq 的 using 指令。  如果项目不满足上面的一个或多个要求，则您可以手动添加它们。  有关更多信息，请参见[How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md)。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [对象和集合初始值设定项](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)