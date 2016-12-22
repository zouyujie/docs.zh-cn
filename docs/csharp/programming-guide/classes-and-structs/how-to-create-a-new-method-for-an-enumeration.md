---
title: "如何：为枚举创建新方法（C# 编程指南） | Microsoft Docs"
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
  - "枚举扩展性 [C#]"
  - "枚举 [C#]"
  - "扩展方法 [C#], 用于枚举"
ms.assetid: 100106f9-1e54-462c-8ebe-3892fe23b6eb
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：为枚举创建新方法（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

可以使用扩展方法添加特定于某个特定枚举类型的功能。  
  
## 示例  
 在下面的示例中，`Grades` 枚举表示学生可能在班里收到的字母等级分。  该示例将一个名为 `Passing` 的扩展方法添加到 `Grades` 类型中，以便该类型的每个实例现在都“知道”它是否表示合格的等级分。  
  
 [!CODE [csProgGuideExtensionMethods#2](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideExtensionMethods#2)]  
  
 请注意，`Extensions` 类还包含一个动态更新的静态变量，并且扩展方法的返回值反映了该变量的当前值。  这表明在幕后，将在定义扩展方法的静态类上直接调用这些方法。  
  
## 编译代码  
 若要运行这段代码，请将其复制并粘贴到已经在 [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)] 中创建的 Visual C\# 控制台应用程序项目中。  默认情况下，此项目针对的是 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 3.5 版，并且具有一个对 System.Core.dll 的引用和一条针对 System.Linq 的 `using` 指令。  如果项目不满足上面的一个或多个要求，则您可以手动添加它们。  有关更多信息，请参见 [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md)。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [扩展方法](../../../csharp/programming-guide/classes-and-structs/extension-methods.md)