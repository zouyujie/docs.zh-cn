---
title: "typeof（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "typeof"
  - "typeof_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "typeof 关键字 [C#]"
ms.assetid: 0c08d880-515e-46bb-8cd2-48b8dd62c08d
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# typeof（C# 参考）
用于获取类型的 `System.Type` 对象。  `typeof` 表达式采用以下形式：  
  
```  
System.Type type = typeof(int);  
```  
  
## 备注  
 若要获取表达式的运行时类型，可以使用 .NET Framework 方法 <xref:System.Object.GetType%2A>，如以下示例中所示：  
  
```  
int i = 0;  
System.Type type = i.GetType();  
```  
  
 不能重载 `typeof` 运算符。  
  
 `typeof` 运算符也能用于公开的泛型类型。  具有不止一个类型参数的类型的规范中必须有适当数量的逗号。  下面的示例演示如何确定方法的返回类型是否是泛型 <xref:System.Collections.Generic.IEnumerable%601>。  假定此方法是 MethodInfo 类型的实例：  
  
```  
string s = method.ReturnType.GetInterface  
    (typeof(System.Collections.Generic.IEnumerable<>).FullName);  
```  
  
## 示例  
 [!code-cs[csrefKeywordsOperator#12](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsOperator/csrefKeywordsOperators.cs#12)]  
  
## 示例  
 此示例使用 <xref:System.Object.GetType%2A> 方法确定用来包含数值计算的结果的类型。  这取决于结果数字的存储要求。  
  
 [!code-cs[csrefKeywordsOperator#13](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsOperator/csrefKeywordsOperators.cs#13)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 <xref:System.Type?displayProperty=fullName>   
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [is](../../../csharp/language-reference/keywords/is.md)   
 [运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)