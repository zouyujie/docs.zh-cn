---
title: "多维数组（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "数组 [C#], 多维"
  - "多维数组 [C#]"
ms.assetid: 020ce02e-7dff-4273-8e53-bf0b33747232
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# 多维数组（C# 编程指南）
数组可以具有多个维度。  例如，下列声明创建一个四行两列的二维数组。  
  
 [!code-cs[csProgGuideArrays#11](../../../csharp/programming-guide/arrays/codesnippet/csharp/multidimensional-arrays_1.cs)]  
  
 下列声明创建一个三维（4、2 和 3）数组。  
  
 [!code-cs[csProgGuideArrays#12](../../../csharp/programming-guide/arrays/codesnippet/csharp/multidimensional-arrays_2.cs)]  
  
## 数组初始化  
 可以在声明数组时将其初始化，如下例所示。  
  
 [!code-cs[csProgGuideArrays#13](../../../csharp/programming-guide/arrays/codesnippet/csharp/multidimensional-arrays_3.cs)]  
  
 也可以初始化数组但不指定级别。  
  
 [!code-cs[csProgGuideArrays#14](../../../csharp/programming-guide/arrays/codesnippet/csharp/multidimensional-arrays_4.cs)]  
  
 如果选择声明一个数组变量但不将其初始化，必须使用 `new` 运算符将一个数组分配给此变量。  以下示例显示 `new` 的用法。  
  
 [!code-cs[csProgGuideArrays#15](../../../csharp/programming-guide/arrays/codesnippet/csharp/multidimensional-arrays_5.cs)]  
  
 以下示例将值分配给特定的数组元素。  
  
 [!code-cs[csProgGuideArrays#16](../../../csharp/programming-guide/arrays/codesnippet/csharp/multidimensional-arrays_6.cs)]  
  
 同样，下面的示例获取特定数组元素的值，并将它赋给变量`elementValue`。  
  
 [!code-cs[csProgGuideArrays#42](../../../csharp/programming-guide/arrays/codesnippet/csharp/multidimensional-arrays_7.cs)]  
  
 以下代码示例将数组元素初始化为默认值（交错数组除外）：  
  
 [!code-cs[csProgGuideArrays#17](../../../csharp/programming-guide/arrays/codesnippet/csharp/multidimensional-arrays_8.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [数组](../../../csharp/programming-guide/arrays/index.md)   
 [一维数组](../../../csharp/programming-guide/arrays/single-dimensional-arrays.md)   
 [交错数组](../../../csharp/programming-guide/arrays/jagged-arrays.md)