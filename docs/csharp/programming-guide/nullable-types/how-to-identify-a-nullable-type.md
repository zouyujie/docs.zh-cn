---
title: "如何：标识可以为 null 的类型（C# 编程指南） | Microsoft Docs"
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
  - "可以为 null 的类型 [C#], 标识"
ms.assetid: d4b67ee2-66e8-40c1-ae9d-545d32c71387
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：标识可以为 null 的类型（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

可以使用 C\# [typeof](../../../csharp/language-reference/keywords/typeof.md) 运算符来创建表示可以为 null 的类型的 <xref:System.Type> 对象：  
  
```  
System.Type type = typeof(int?);  
```  
  
 还可以使用 <xref:System.Reflection> 命名空间的类和方法来生成表示可以为 null 的类型的 <xref:System.Type> 对象。  但是，如果您尝试使用 <xref:System.Object.GetType%2A> 方法或 `is` 运算符在运行时获得可以为 null 的类型变量的类型信息，得到的结果是表示基础类型而不是可以为 null 的类型本身的 <xref:System.Type> 对象。  
  
 如果对可以为 null 的类型调用 `GetType`，则在该类型被隐式转换为 <xref:System.Object> 时将执行装箱操作。  因此，<xref:System.Object.GetType%2A> 总是返回表示基础类型而不是可以为 null 的类型的 <xref:System.Type> 对象。  
  
```  
int? i = 5;  
Type t = i.GetType();  
Console.WriteLine(t.FullName); //"System.Int32"  
```  
  
 C\# 的 [is](../../../csharp/language-reference/keywords/is.md) 运算符还可以作用于可以为 null 的的基础类型。  因此，不能使用 `is` 来确定变量是否为可以为 null 的类型。  下面的示例演示 `is` 运算符将 Nullable\<int\> 变量视为 int 变量。  
  
```  
static void Main(string[] args)  
{  
  int? i = 5;  
  if (i is int) // true  
    //…  
}  
```  
  
## 示例  
 使用下面的代码来确定 <xref:System.Type> 对象是否表示可以为 null 的类型。  请记住，如果 `Type` 对象是通过调用 <xref:System.Object.GetType%2A> 返回的，则此代码始终返回 false，如本主题中先前所述。  
  
```  
if (type.IsGenericType && type.GetGenericTypeDefinition() == typeof(Nullable<>)) {…}  
```  
  
## 请参阅  
 [可以为 null 的类型](../../../visual-basic/reference/command-line-compiler/index.md)   
 [装箱可以为 null 的类型](../../../csharp/programming-guide/nullable-types/boxing-nullable-types.md)