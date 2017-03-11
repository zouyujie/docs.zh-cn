---
title: "如何：使用对象初始值设定项初始化对象（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "对象初始值设定项 [C#], 使用方法"
  - "对象 [C#], 初始化"
ms.assetid: 4b75ebb2-2e29-43de-929c-d736a8f27ce6
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# 如何：使用对象初始值设定项初始化对象（C# 编程指南）
可以使用对象初始值设定项以声明方式初始化类型对象，而无需显式调用类型的构造函数。  
  
 下面的示例演示如何将对象初始值设定项用于命名对象。  编译器通过先访问默认实例构造函数然后处理成员初始化处理对象初始值设定项。  因此，如果默认构造函数在类中声明为 `private`，那么需要公共访问权的对象初始值设定项将失败。  
  
 如果定义匿名类型，则必须使用对象初始值设定项。  有关更多信息，请参见[如何：在查询中返回元素属性的子集](../../../csharp/programming-guide/classes-and-structs/how-to-return-subsets-of-element-properties-in-a-query.md)。  
  
## 示例  
 下面的示例演示如何使用对象初始值设定项初始化新的 `StudentName` 类型。  
  
 [!code-cs[csProgGuideLINQ#35](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csRef30LangFeatures_2.cs#35)]  
  
## 示例  
 下面的示例演示如何使用集合初始值设定项初始化一个 `StudentName` 类型集合。  请注意，集合初始值设定项是一系列由逗号分隔的对象初始值设定项。  
  
 [!code-cs[csProgGuideLINQ#36](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csRef30LangFeatures_2.cs#36)]  
  
## 编译代码  
 若要运行这段代码，请将该类复制并粘贴到已经在 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 中创建的 Visual C\# 控制台应用程序项目中。  有关更多信息，请参见[How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md)。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [对象和集合初始值设定项](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)