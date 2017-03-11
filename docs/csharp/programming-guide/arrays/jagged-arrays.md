---
title: "交错数组（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "数组 [C#], 交错"
  - "交错数组 [C#]"
ms.assetid: 537c65a6-0e0a-4a00-a2b8-086f38519c70
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# 交错数组（C# 编程指南）
交错数组是元素为数组的数组。  交错数组元素的维度和大小可以不同。  交错数组有时称为“数组的数组”。以下示例说明如何声明、初始化和访问交错数组。  
  
 下面声明一个由三个元素组成的一维数组，其中每个元素都是一个一维整数数组：  
  
 [!code-cs[csProgGuideArrays#19](../../../csharp/programming-guide/arrays/codesnippet/csharp/jagged-arrays_1.cs)]  
  
 必须初始化 `jaggedArray` 的元素后才可以使用它。  可以如下例所示初始化该元素：  
  
 [!code-cs[csProgGuideArrays#20](../../../csharp/programming-guide/arrays/codesnippet/csharp/jagged-arrays_2.cs)]  
  
 每个元素都是一个一维整数数组。  第一个元素是由 5 个整数组成的数组，第二个是由 4 个整数组成的数组，而第三个是由 2 个整数组成的数组。  
  
 也可以使用初始值设定项用值填充数组元素，在这种情况下不需要数组大小。  例如：  
  
 [!code-cs[csProgGuideArrays#21](../../../csharp/programming-guide/arrays/codesnippet/csharp/jagged-arrays_3.cs)]  
  
 还可以在声明数组时将其初始化，如：  
  
 [!code-cs[csProgGuideArrays#22](../../../csharp/programming-guide/arrays/codesnippet/csharp/jagged-arrays_4.cs)]  
  
 可以使用下面的速记格式。  请注意：不能从元素初始化中省略 `new` 运算符，因为不存在元素的默认初始化：  
  
 [!code-cs[csProgGuideArrays#23](../../../csharp/programming-guide/arrays/codesnippet/csharp/jagged-arrays_5.cs)]  
  
 交错数组是数组的数组，因此其元素是引用类型并初始化为 `null`。  
  
 可以如下例所示访问个别数组元素：  
  
 [!code-cs[csProgGuideArrays#24](../../../csharp/programming-guide/arrays/codesnippet/csharp/jagged-arrays_6.cs)]  
  
 可以混合使用交错数组和多维数组。  下面声明和初始化一个一维交错数组，该数组包含大小不同的三个二维数组元素。  有关二维数组的详细信息，请参阅[多维数组](../../../csharp/programming-guide/arrays/multidimensional-arrays.md)。  
  
 [!code-cs[csProgGuideArrays#25](../../../csharp/programming-guide/arrays/codesnippet/csharp/jagged-arrays_7.cs)]  
  
 可以如本例所示访问个别元素，该示例显示第一个数组的元素 `[1,0]` 的值（值为 `5`）：  
  
 [!code-cs[csProgGuideArrays#26](../../../csharp/programming-guide/arrays/codesnippet/csharp/jagged-arrays_8.cs)]  
  
 方法 `Length` 返回包含在交错数组中的数组的数目。  例如，假定您已声明了前一个数组，则此行：  
  
 [!code-cs[csProgGuideArrays#27](../../../csharp/programming-guide/arrays/codesnippet/csharp/jagged-arrays_9.cs)]  
  
 返回值 3。  
  
## 示例  
 本例生成一个数组，该数组的元素为数组自身。  每一个数组元素都有不同的大小。  
  
 [!code-cs[csProgGuideArrays#18](../../../csharp/programming-guide/arrays/codesnippet/csharp/jagged-arrays_10.cs)]  
  
## 请参阅  
 <xref:System.Array>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [数组](../../../csharp/programming-guide/arrays/index.md)   
 [一维数组](../../../csharp/programming-guide/arrays/single-dimensional-arrays.md)   
 [多维数组](../../../csharp/programming-guide/arrays/multidimensional-arrays.md)