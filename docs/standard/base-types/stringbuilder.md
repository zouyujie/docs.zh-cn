---
title: "使用 StringBuilder 类"
description: "使用 StringBuilder 类"
keywords: ".NET、.NET Core"
author: stevehoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: f4f5d1c7-d84d-4867-810f-2708cd6de0da
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 1e8453b78827d8c02f29135ddfb832956ab40f3c

---

# <a name="using-the-stringbuilder-class"></a>使用 StringBuilder 类

[String](xref:System.String) 对象是不可变的。 每次使用 [System.String](xref:System.String) 类中的一个方法时，都要在内存中创建一个新的字符串对象，这就需要为该新对象分配新的空间。 在需要对字符串执行重复修改的情况下，与创建新 [String](xref:System.String) 对象关联的开销可能非常大。 如果要修改字符串而不创建新的对象，则可以使用 [System.Text.StringBuilder](xref:System.Text.StringBuilder) 类。 例如，在一次循环中将许多字符串连接在一起时，使用 [StringBuilder](xref:System.Text.StringBuilder) 类可以提升性能。

## <a name="importing-the-systemtext-namespace"></a>导入 System.Text 命名空间

[StringBuilder](xref:System.Text.StringBuilder) 类位于 [System.Text](xref:System.Text) 命名空间。 为了避免必须在代码中提供完全限定的类型名称，可以导入 [System.Text](xref:System.Text) 命名空间： 

```csharp
using System;
using System.Text;
```

```vb
Imports System.Text
```

## <a name="instantiating-a-stringbuilder-object"></a>实例化 StringBuilder 对象

通过利用其中一个重载的构造函数方法初始化变量，可以创建 [StringBuilder](xref:System.Text.StringBuilder) 类的新实例，如以下示例所示。

```csharp
StringBuilder MyStringBuilder = new StringBuilder("Hello World!");
```

```vb
Dim MyStringBuilder As New StringBuilder("Hello World!")
```

## <a name="setting-the-capacity-and-length"></a>设置容量和长度

虽然 [StringBuilder](xref:System.Text.StringBuilder) 是动态对象，允许增加其所封装字符串中的字符数，但也可以指定该对象可保留的最大字符数的值。 此值称为该对象的容量，切勿将它与当前 [StringBuilder](xref:System.Text.StringBuilder) 所保留的字符串长度相混淆。 例如，可以使用长度为 5 的字符串“Hello”创建 [StringBuilder](xref:System.Text.StringBuilder) 类的新实例，同时可以指定该对象的最大容量为 25。 修改 [StringBuilder](xref:System.Text.StringBuilder) 时，在达到容量之前，该对象不会为自己重新分配空间。 当达到容量时，将自动分配新的空间且容量翻倍。 可以使用重载的构造函数之一来指定 [StringBuilder](xref:System.Text.StringBuilder) 类的容量。 下面的示例指定可以将 `MyStringBuilder` 对象增加到最多 25 个空间。

```csharp
StringBuilder MyStringBuilder = new StringBuilder("Hello World!", 25);
```

```vb
Dim MyStringBuilder As New StringBuilder("Hello World!", 25) 
```

另外，可以使用读/写 [Capacity](xref:System.Text.StringBuilder.Capacity) 属性来设置对象的最大长度。 下面的示例使用 [Capacity](xref:System.Text.StringBuilder.Capacity) 属性来定义对象的最大长度。

```csharp
MyStringBuilder.Capacity = 25;
```

```vb
MyStringBuilder.Capacity = 25
```

[EnsureCapacity](xref:System.Text.StringBuilder.EnsureCapacity(System.Int32)) 方法可用来检查当前 [StringBuilder](xref:System.Text.StringBuilder) 的容量。 如果容量大于传递的值，则不进行任何更改；但是，如果容量小于传递的值，则会更改当前的容量以使其与传递的值匹配。

也可以查看或设置 [Length](xref:System.Text.StringBuilder.Length) 属性。 如果将 [Length](xref:System.Text.StringBuilder.Length) 属性设置为大于 [Capacity](xref:System.Text.StringBuilder.Capacity) 属性的值，则自动将 [Capacity](xref:System.Text.StringBuilder.Capacity) 属性更改为与 [Length](xref:System.Text.StringBuilder.Length) 属性相同的值。 如果将 [Length](xref:System.Text.StringBuilder.Length) 属性设置为小于当前 [StringBuilder](xref:System.Text.StringBuilder) 对象内的字符串长度的值，则会缩短该字符串。

## <a name="modifying-the-stringbuilder-string"></a>修改 StringBuilder 字符串

下表列出了可用于修改 [StringBuilder](xref:System.Text.StringBuilder) 内容的方法。

方法名称 | 使用
----------- | ---
[StringBuilder.Append](xref:System.Text.StringBuilder.Append(System.Char)) | 将信息追加到当前 [StringBuilder](xref:System.Text.StringBuilder) 的末尾。
[StringBuilder.AppendFormat](xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider,System.String,System.Object)) | 用带格式文本替换字符串中传递的格式说明符。
[StringBuilder.Insert](xref:System.Text.StringBuilder.Insert(System.Int32,System.Char)) | 将字符串或对象插入到当前 [StringBuilder](xref:System.Text.StringBuilder) 的指定索引中。
[StringBuilder.Remove](xref:System.Text.StringBuilder.Remove(System.Int32,System.Int32)) | 从当前 [StringBuilder](xref:System.Text.StringBuilder) 中删除指定数量的字符。
[StringBuilder.Replace](xref:System.Text.StringBuilder.Replace(System.Char,System.Char)) | 替换指定索引处的指定字符。

### <a name="append"></a>追加

[StringBuilder.Append](xref:System.Text.StringBuilder.Append(System.Char)) 方法可用来将文本或对象的字符串表示形式添加到由当前 [StringBuilder](xref:System.Text.StringBuilder) 表示的字符串的末尾。 下面的示例将 [StringBuilder](xref:System.Text.StringBuilder) 对象初始化为“Hello World”，然后将一些文本追加到该对象的末尾。 将根据需要自动分配空间。

```csharp
StringBuilder MyStringBuilder = new StringBuilder("Hello World!");
MyStringBuilder.Append(" What a beautiful day.");
Console.WriteLine(MyStringBuilder);
// The example displays the following output:
//       Hello World! What a beautiful day.
```

```vb
Dim MyStringBuilder As New StringBuilder("Hello World!")
MyStringBuilder.Append(" What a beautiful day.")
Console.WriteLine(MyStringBuilder)
' The example displays the following output:
'       Hello World! What a beautiful day.
```

### <a name="appendformat"></a>AppendFormat

[StringBuilder.AppendFormat](xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider,System.String,System.Object)) 方法将文本添加到 [StringBuilder](xref:System.Text.StringBuilder) 对象的末尾。 该方法通过调用要设置格式的对象的 [IFormattable](xref:System.IFormattable) 实现来支持复合格式设置功能（有关详细信息，请参阅[复合格式设置](composite-format.md)）。 因此，它接受数字、日期和时间以及枚举值的标准格式字符串、数字以及日期和时间值的自定义格式字符串，以及为自定义类型定义的格式字符串。 （有关格式化的信息，请参阅[格式设置类型](formatting-types.md)。）可以使用此方法来自定义变量的格式并将这些值追加到 [StringBuilder](xref:System.Text.StringBuilder)。 下面的示例使用 AppendFormat 方法将设置为货币值格式的整数值放到 [StringBuilder](xref:System.Text.StringBuilder) 对象的末尾。

```csharp
int MyInt = 25; 
StringBuilder MyStringBuilder = new StringBuilder("Your total is ");
MyStringBuilder.AppendFormat("{0:C} ", MyInt);
Console.WriteLine(MyStringBuilder);
// The example displays the following output:
//       Your total is $25.00
```

```vb
Dim MyInt As Integer = 25
Dim MyStringBuilder As New StringBuilder("Your total is ")
MyStringBuilder.AppendFormat("{0:C} ", MyInt)
Console.WriteLine(MyStringBuilder)
' The example displays the following output:
'     Your total is $25.00 
```

### <a name="insert"></a>Insert

[StringBuilder.Insert](xref:System.Text.StringBuilder.Insert(System.Int32,System.Char)) 方法将字符串或对象添加到当前 [StringBuilder](xref:System.Text.StringBuilder) 对象中的指定位置。 下面的示例使用此方法将单词插入到 [StringBuilder](xref:System.Text.StringBuilder) 对象的第六个位置。

```csharp
StringBuilder MyStringBuilder = new StringBuilder("Hello World!");
MyStringBuilder.Insert(6,"Beautiful ");
Console.WriteLine(MyStringBuilder);
// The example displays the following output:
//       Hello Beautiful World!
```

```vb
Dim MyStringBuilder As New StringBuilder("Hello World!")
MyStringBuilder.Insert(6, "Beautiful ")
Console.WriteLine(MyStringBuilder)
' The example displays the following output:
'      Hello Beautiful World!
```

### <a name="remove"></a>删除

可以使用 [StringBuilder.Remove](xref:System.Text.StringBuilder.Remove(System.Int32,System.Int32)) 方法从当前 [StringBuilder](xref:System.Text.StringBuilder) 对象中删除指定数量的字符，删除过程从指定的从零开始的索引处开始。 下面的示例使用 [Remove](xref:System.Text.StringBuilder.Remove(System.Int32,System.Int32)) 方法缩短 [StringBuilder](xref:System.Text.StringBuilder) 对象。

```csharp
StringBuilder MyStringBuilder = new StringBuilder("Hello World!");
MyStringBuilder.Remove(5,7);
Console.WriteLine(MyStringBuilder);
// The example displays the following output:
//       Hello
```

```vb
Dim MyStringBuilder As New StringBuilder("Hello World!")
MyStringBuilder.Remove(5, 7)
Console.WriteLine(MyStringBuilder)
' The example displays the following output:
'       Hello
```

### <a name="replace"></a>替换

[StringBuilder.Replace](xref:System.Text.StringBuilder.Replace(System.Char,System.Char)) | 替换指定索引处的指定字符。
方法可用于将 [StringBuilder](xref:System.Text.StringBuilder) 对象内的字符替换为其他指定字符。 以下示例使用 [Replace](xref:System.Text.StringBuilder.Replace(System.Char,System.Char)) | 替换指定索引处的指定字符。
方法在 [StringBuilder](xref:System.Text.StringBuilder) 对象中搜索感叹号字符 (!) 的所有实例，并将其替换为问号字符 (?)。
 
 ```csharp
 StringBuilder MyStringBuilder = new StringBuilder("Hello World!");
MyStringBuilder.Replace('!', '?');
Console.WriteLine(MyStringBuilder);
// The example displays the following output:
//       Hello World?
```

```vb
Dim MyStringBuilder As New StringBuilder("Hello World!")
MyStringBuilder.Replace("!"c, "?"c)
Console.WriteLine(MyStringBuilder)
' The example displays the following output:
'       Hello World?
```

## <a name="converting-a-stringbuilder-object-to-a-string"></a>将 StringBuilder 对象转换为字符串

必须先将 [StringBuilder](xref:System.Text.StringBuilder) 对象转换为 [String](xref:System.String) 对象，然后才能将 [StringBuilder](xref:System.Text.StringBuilder) 对象表示的字符串传递给具有 [String](xref:System.String) 参数的方法，或在用户界面中显示它。 通过调用 [StringBuilder.ToString](xref:System.Text.StringBuilder.ToString) 方法来执行此转换。 下面的示例调用多种 [StringBuilder](xref:System.Text.StringBuilder) 方法，然后调用 [StringBuilder.ToString](xref:System.Text.StringBuilder.ToString) 方法来显示字符串。

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      StringBuilder sb = new StringBuilder();
      bool flag = true;
      string[] spellings = { "recieve", "receeve", "receive" };
      sb.AppendFormat("Which of the following spellings is {0}:", flag);
      sb.AppendLine();
      for (int ctr = 0; ctr <= spellings.GetUpperBound(0); ctr++) {
         sb.AppendFormat("   {0}. {1}", ctr, spellings[ctr]);
         sb.AppendLine();
      }
      sb.AppendLine();
      Console.WriteLine(sb.ToString());
   }
}
// The example displays the following output:
//       Which of the following spellings is True:
//          0. recieve
//          1. receeve
//          2. receive
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      Dim sb As New StringBuilder()
      Dim flag As Boolean = True
      Dim spellings() As String = { "recieve", "receeve", "receive" }
      sb.AppendFormat("Which of the following spellings is {0}:", flag)
      sb.AppendLine()
      For ctr As Integer = 0 To spellings.GetUpperBound(0)
         sb.AppendFormat("   {0}. {1}", ctr, spellings(ctr))
         sb.AppendLine()
      Next
      sb.AppendLine()
      Console.WriteLine(sb.ToString())
   End Sub
End Module
' The example displays the following output:
'       Which of the following spellings is True:
'          0. recieve
'          1. receeve
'          2. receive
```

## <a name="see-also"></a>另请参阅

[System.Text.StringBuilder](xref:System.Text.StringBuilder)

[基本字符串操作](basic-string-operations.md)

[格式设置类型](formatting-types.md)



<!--HONumber=Nov16_HO1-->


