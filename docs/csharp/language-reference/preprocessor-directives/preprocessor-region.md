---
title: "#region（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "#region"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#region 指令 [C#]"
ms.assetid: 672c87d1-9771-4f64-ab3f-0ad3d4ffb2b4
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# #region（C# 参考）
`#region` 使您可以在使用 Visual Studio 代码编辑器的[大纲显示](/visual-studio/ide/outlining)功能时指定可展开或折叠的代码块。  在较长的代码文件中，能够折叠或隐藏一个或多个区域会十分便利，这样，您可将精力集中于当前处理的文件部分。  下面的示例演示如何定义区域：  
  
```  
  
      #region MyClass definition  
public class MyClass   
{  
    static void Main()   
    {  
    }  
}  
#endregion  
```  
  
## 备注  
 `#region` 块必须以 [\#endregion](../../../csharp/language-reference/preprocessor-directives/preprocessor-endregion.md) 指令终止。  
  
 `#region` 块不能与 [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md) 块重叠。  但是，可以将 `#region` 块嵌套在 `#if` 块内，或将 `#if` 块嵌套在 `#region` 块内。  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 预处理器指令](../../../csharp/language-reference/preprocessor-directives/index.md)