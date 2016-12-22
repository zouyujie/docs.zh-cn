---
title: "如何：安全地将 bool? 强制转换为 bool（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
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
  - "强制转换 [C#], 可以为 null 的类型"
  - "可以为 null 的类型 [C#], 将 bool? 强制转换为 bool"
ms.assetid: e06e4274-a443-422d-8ef1-9dbf9df55237
caps.latest.revision: 9
caps.handback.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：安全地将 bool? 强制转换为 bool（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`bool?` 可以为 null 的类型可以包含三个不同的值：`true`、`false` 和 `null`。  因此，`bool?` 类型不能用于条件语句，如 `if`、`for` 或 `while`。  例如，以下代码会导致编译器错误。  
  
```  
bool? b = null;  
if (b) // Error CS0266.  
{  
}  
```  
  
 这是不允许的，因为 `null` 在条件上下文中的含义并不清楚。  若要在条件语句中使用 `bool?`，请首先检查其 <xref:System.Nullable%601.HasValue%2A> 属性以确保其值不是 `null`，然后将它强制转换为 `bool`。  有关更多信息，请参见 [bool](../../../csharp/language-reference/keywords/bool.md)。  如果对使用 `null` 值的 `bool?` 执行强制转换，则在条件测试中将引发 <xref:System.InvalidOperationException>。  下面的示例演示了一种从 `bool?` 安全地强制转换为 `bool` 的方法：  
  
## 示例  
  
```c#  
bool? test = null;  
// Other code that may or may not  
// give a value to test.  
if(!test.HasValue) //check for a value  
{  
    // Assume that IsInitialized  
    // returns either true or false.  
    test = IsInitialized();  
}  
if((bool)test) //now this cast is safe  
{  
   // Do something.  
}  
```  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [文字关键字](../../../csharp/language-reference/keywords/literal-keywords.md)   
 [可以为 null 的类型](../../../visual-basic/reference/command-line-compiler/index.md)   
 [?? 运算符](../../../csharp/language-reference/operators/null-conditional-operator.md)