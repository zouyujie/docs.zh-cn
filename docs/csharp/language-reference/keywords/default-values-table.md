---
title: "默认值表（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "构造函数 [C#], 返回值"
  - "关键字 [C], 新"
  - "默认构造函数 [C#]"
  - "默认值 [C#]"
  - "值类型 [C#], 初始化"
  - "变量 [C#], 值类型"
  - "构造函数 [C#], 默认构造函数"
  - "类型 [C#], 默认构造函数返回值"
ms.assetid: 4af2c1df-9e3a-48c1-83ac-b192986fc5bc
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# 默认值表（C# 参考）
下表显示了由默认构造函数返回的值类型的默认值。  默认构造函数是通过 `new` 运算符来调用的，如下所示：  
  
```  
int myInt = new int();  
```  
  
 以上语句同下列语句效果相同：  
  
```  
int myInt = 0;  
```  
  
 请记住：在 C\# 中不允许使用未初始化的变量。  
  
|值类型|默认值|  
|---------|---------|  
|[bool](../../../csharp/language-reference/keywords/bool.md)|`false`|  
|[byte](../../../csharp/language-reference/keywords/byte.md)|0|  
|[char](../../../csharp/language-reference/keywords/char.md)|'\\0'|  
|[decimal](../../../csharp/language-reference/keywords/decimal.md)|0.0M|  
|[double](../../../csharp/language-reference/keywords/double.md)|0.0D|  
|[enum](../../../csharp/language-reference/keywords/enum.md)|表达式 \(E\)0 产生的值，其中 E 为 enum 标识符。|  
|[float](../../../csharp/language-reference/keywords/float.md)|0.0F|  
|[int](../../../csharp/language-reference/keywords/int.md)|0|  
|[long](../../../csharp/language-reference/keywords/long.md)|0L|  
|[sbyte](../../../csharp/language-reference/keywords/sbyte.md)|0|  
|[short](../../../csharp/language-reference/keywords/short.md)|0|  
|[struct](../../../csharp/language-reference/keywords/struct.md)|将所有的值类型字段设置为默认值并将所有的引用类型字段设置为 `null` 时产生的值。|  
|[uint](../../../csharp/language-reference/keywords/uint.md)|0|  
|[ulong](../../../csharp/language-reference/keywords/ulong.md)|0|  
|[ushort](../../../csharp/language-reference/keywords/ushort.md)|0|  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [值类型表](../../../csharp/language-reference/keywords/value-types-table.md)   
 [值类型](../../../csharp/language-reference/keywords/value-types.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [类型参考表](../../../csharp/language-reference/keywords/reference-tables-for-types.md)