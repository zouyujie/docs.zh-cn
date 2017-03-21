---
title: "#pragma warning（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "#pragma warning"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#pragma warning [C#]"
ms.assetid: 723493d5-9753-4cec-babb-54e2b8eb36b6
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# #pragma warning（C# 参考）
`#pragma warning` 可启用或禁用某些警告。  
  
## 语法  
  
```  
#pragma warning disable warning-list  
#pragma warning restore warning-list  
```  
  
#### 参数  
 `warning-list`  
 警告编号的逗号分隔列表。  只输入数字，不包括前缀 "CS"。  
  
 当没有指定警告编号时，`disable` 禁用所有警告，而 `restore` 启用所有警告。  
  
> [!NOTE]
>  要在 Visual Studio 中查找警告编号，请先生成项目，再在“输出”窗口中查找警告编号。  
  
## 示例  
  
```  
// pragma_warning.cs  
using System;  
  
#pragma warning disable 414, 3021  
[CLSCompliant(false)]  
public class C  
{  
    int i = 1;  
    static void Main()  
    {  
    }  
}  
#pragma warning restore 3021  
[CLSCompliant(false)]  // CS3021  
public class D  
{  
    int i = 1;  
    public static void F()  
    {  
    }  
}  
```  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 预处理器指令](../../../csharp/language-reference/preprocessor-directives/index.md)   
 [C\# Compiler Errors](../../../csharp/language-reference/compiler-messages/index.md)