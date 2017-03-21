---
title: "如何：将字节数组转换为 int（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "字节数组 [C#], 转换为 int"
  - "转换 [C#], 字节数组转换为 int"
ms.assetid: d6ac20e2-448e-4aea-99b9-faf04c6f1e79
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# 如何：将字节数组转换为 int（C# 编程指南）
此示例演示如何使用 <xref:System.BitConverter> 类将字节数组转换为 [int](../../../csharp/language-reference/keywords/int.md) 并返回字节数组。  例如，在从网络读取字节之后，可能需要将字节转换为内置数据类型。  除了示例中的 [ToInt32\(Byte\<xref:System.BitConverter.ToInt32%28System.Byte%5B%5D%2CSystem.Int32%29> 方法之外，下表列出了 <xref:System.BitConverter> 类中将字节（来自字节数组）转换为其他内置类型的方法。  
  
|返回类型|方法|  
|----------|--------|  
|`bool`|[ToBoolean\(Byte\<xref:System.BitConverter.ToBoolean%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`char`|[ToChar\(Byte\<xref:System.BitConverter.ToChar%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`double`|[ToDouble\(Byte\<xref:System.BitConverter.ToDouble%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`short`|[ToInt16\(Byte\<xref:System.BitConverter.ToInt16%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`int`|[ToInt32\(Byte\<xref:System.BitConverter.ToInt32%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`long`|[ToInt64\(Byte\<xref:System.BitConverter.ToInt64%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`float`|[ToSingle\(Byte\<xref:System.BitConverter.ToSingle%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`ushort`|[ToUInt16\(Byte\<xref:System.BitConverter.ToUInt16%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`uint`|[ToUInt32\(Byte\<xref:System.BitConverter.ToUInt32%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`ulong`|[ToUInt64\(Byte\<xref:System.BitConverter.ToUInt64%28System.Byte%5B%5D%2CSystem.Int32%29>|  
  
## 示例  
 此示例实例化字节数组，并在计算机结构为 little\-endian 的情况下反转数组（即首先存储最低有效字节），然后调用 [ToInt32\(Byte\<xref:System.BitConverter.ToInt32%28System.Byte%5B%5D%2CSystem.Int32%29> 方法以将数组中的四个字节转换为 `int`。  [ToInt32\(Byte\<xref:System.BitConverter.ToInt32%28System.Byte%5B%5D%2CSystem.Int32%29> 的第二个参数指定字节数组的起始索引。  
  
> [!NOTE]
>  输出可能会根据计算机结构的 endian 设置而不同。  
  
 [!code-cs[csProgGuideTypes#22](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-byte-array-to-an-int_1.cs)]  
  
## 示例  
 在此示例中，调用 <xref:System.BitConverter> 类的 <xref:System.BitConverter.GetBytes%28System.Int32%29> 方法以将 `int` 转换为字节数组。  
  
> [!NOTE]
>  输出可能会根据计算机结构的 endian 设置而不同。  
  
 [!code-cs[csProgGuideTypes#23](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-byte-array-to-an-int_2.cs)]  
  
## 请参阅  
 <xref:System.BitConverter>   
 <xref:System.BitConverter.IsLittleEndian>   
 [类型](../../../csharp/programming-guide/types/index.md)