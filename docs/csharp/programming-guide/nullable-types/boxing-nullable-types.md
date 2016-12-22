---
title: "装箱可以为 null 的类型（C# 编程指南） | Microsoft Docs"
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
  - "装箱 [C#], 可以为 null 的类型"
  - "可以为 null 的类型 [C#], 装箱和取消装箱"
  - "取消装箱 [C#], 可以为 null 的类型"
ms.assetid: bdb5b626-abc0-405d-8f64-0f0a0bf883a4
caps.latest.revision: 12
caps.handback.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 装箱可以为 null 的类型（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

基于可以为 null 的类型的对象只在该对象为非空时装箱。  如果 <xref:System.Nullable%601.HasValue%2A> 为 `false`，则将对象引用赋值为 `null`，而不进行装箱。  例如：  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 如果对象非空，也就是说，如果 <xref:System.Nullable%601.HasValue%2A> 为 `true`，则会发生装箱过程，但只将可以为 null 的对象所基于的基础类型装箱。  如果将非空的可以为 null 的值类型装箱，将使值类型本身（而不是包装该值类型的 <xref:System.Nullable%601?displayProperty=fullName>）装箱。  例如：  
  
```  
bool? b = false;  
int? i = 44;  
object bBoxed = b; // bBoxed contains a boxed bool.  
object iBoxed = i; // iBoxed contains a boxed int.  
```  
  
 对于那些通过装箱非可以为 null 的类型而创建的类型来说，两种装箱对象是完全相同的。  并且，像非可以为 null 的装箱类型一样，可以将它们取消装箱，使其成为可以为 null 的类型，如以下示例所示：  
  
```  
bool? b2 = (bool?)bBoxed;  
int? i2 = (int?)iBoxed;  
```  
  
## 备注  
 可以为 null 的类型在装箱时的行为具有两个优点：  
  
1.  可以测试可以为 null 的对象及其装箱的对应项是否为空：  
  
    ```  
    bool? b = null;  
    object boxedB = b;  
    if (b == null)  
    {  
      // True.  
    }  
    if (boxedB == null)  
    {  
      // Also true.  
    }  
    ```  
  
2.  装箱的可以为 null 的类型完全支持基础类型的功能：  
  
    ```  
    double? d = 44.4;  
    object iBoxed = d;  
    // Access IConvertible interface implemented by double.  
    IConvertible ic = (IConvertible)iBoxed;  
    int i = ic.ToInt32(null);  
    string str = ic.ToString();  
    ```  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [可以为 null 的类型](../../../visual-basic/reference/command-line-compiler/index.md)   
 [如何：标识可以为 null 的类型](../../../csharp/programming-guide/nullable-types/how-to-identify-a-nullable-type.md)