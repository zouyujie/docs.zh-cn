---
title: "-&gt; 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "->_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-> 运算符 [C#]"
  - "成员访问运算符 (->) [C#]"
ms.assetid: e39ccdc1-f1ff-4a92-bf1d-ac2c8c11316a
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# -&gt; 运算符（C# 参考）
`->` 运算符将指针取消引用与成员访问组合在一起。  
  
## 备注  
 以下形式的表达式  
  
```  
x->y  
```  
  
 （其中 `x` 为 `T*` 类型的指针，`y` 为 `T` 的成员）等效于  
  
```  
(*x).y  
```  
  
 只能在标记为[不安全](../../../csharp/language-reference/keywords/unsafe.md)的代码中使用 `->` 运算符。  
  
 不能重载 `->` 运算符。  
  
## 示例  
 [!code-cs[csRefOperators#15](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#15)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)