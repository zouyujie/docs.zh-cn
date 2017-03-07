---
title: ".NET 中的字符编码"
description: ".NET 中的字符编码"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: bce54e41-e9dc-493a-8988-1cbadc340fe8
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: a8f42fa6a37f8de6f13186ea2ac17b2b2ced1601
ms.lasthandoff: 03/02/2017

---

# <a name="character-encoding-in-net"></a>.NET 中的字符编码

字符是可以许多不同的方式表示的抽象实体。 字符编码是用代表字符的某个值与受支持的字符集中的每个字符配对的系统。 例如，莫尔斯电码就是一种用点线模式与罗马字母表中的每个字符（适合通过电报线路进行传输）进行配对的字符编码。 计算机的字符编码将代表字符的数字值与受支持的字符集中的每个字符配对。 一种字符编码有两个不同组件：

* 编码器，将一个字符序列转换为一个数字值（字节）序列。

* 解码器，将字节序列转换成字符序列。

字符编码描述编码器和解码器操作所依据的规则。 例如，[UTF8Encoding](xref:System.Text.UTF8Encoding) 类描述编码为 8 位 Unicode 转换格式 (UTF-8) 和从其进行解码的规则，该格式使用一至四个字节来表示单个 Unicode 字符。 编码和解码还可以包括验证。 例如，[UnicodeEncoding](xref:System.Text.UnicodeEncoding) 类检查所有代理项，确保它们构成有效的代理项对。 （代理项对由码位范围从 U + D800 到 U + DBFF 的字符后跟码位范围从 U + DC00 到 U + DFFF 的字符组成。）回退策略确定编码器处理无效字符的方式或解码器处理无效字节的方式。 

> [!WARNING]
> .NET 编码类提供一种存储和转换字符数据的方法。 它们不应用于存储字符串形式的二进制数据。 根据所使用的编码，用编码类将二进制数据转换为字符串格式可引起意外的行为，并生成不准确或损坏的数据。 若要将二进制数据转换为字符串形式，请使用 [Convert.ToBase64String](xref:System.Convert.ToBase64String(System.Byte[])) 方法。 
 
.NET 使用 UTF-16 编码（由 [UnicodeEncoding](xref:System.Text.UnicodeEncoding) 类表示）表示字符和字符串。 面向公共语言运行时的应用程序使用编码器将公共语言运行时支持的 Unicode 字符表示形式映射为其他的编码模式。 它们使用解码器将来自非 Unicode 的编码映射为 Unicode 字符。

本主题包括以下各节：

* [.NET 中的编码](#encodings-in-net)

* [选择编码类](#selecting-an-encoding-class)

* [使用编码对象](#using-an-encoding-object)

* [选择回退策略](#choosing-a-fallback-strategy)

* [实现自定义回退策略](#implementing-a-custom-fallback-strategy)

## <a name="encodings-in-net"></a>.NET 中的编码

.NET 中的所有字符编码类继承自 [System.Text.Encoding](xref:System.Text.Encoding) 类，该类是定义所有字符编码通用功能的一个抽象类。 若要访问在 .NET 中实现的单个编码对象，请执行以下操作：

* 使用 [Encoding](xref:System.Text.Encoding) 类的静态属性，该类返回表示 .NET 中可用标准字符编码（ASCII、UTF-7、UTF-8、UTF-16 和 UTF-32）的对象。 例如，[Encoding.Unicode](xref:System.Text.Encoding.Unicode) 属性返回 [UnicodeEncoding](xref:System.Text.UnicodeEncoding) 对象。 每个对象都使用替换回退处理不能进行编码的字符串和不能进行解码的字节。 （有关详细信息，请参阅[替换回退](#replacement-fallback)部分。）

* 调用编码的类构造函数。 以这种方式可以将 ASCII、utf-7、utf-8、utf-16 和 utf-32 编码对象实例化。 默认情况下，每个对象都使用替换回退处理不能进行编码的字符串和不能进行解码的字节，但你可指定应引发异常。 （有关详细信息，请参阅[替换回退](#replacement-fallback)和[异常回退](#exception-fallback)部分。）

* 调用 [Encoding.Encoding(Int32)](xref:System.Text.Encoding.GetEncoding(System.Int32)) 构造函数并向其传递一个表示编码的整数。 标准编码对象使用替换回退，代码页编码和双字节字符集 (DBCS) 编码对象使用最佳回退处理不能进行编码的字符串和不能进行解码的字节。 （有关详细信息，请参阅[最佳回退](#best-fit-fallback)部分。）

* 调用 [Encoding.GetEncoding](xref:System.Text.Encoding.GetEncoding(System.Int32)) 方法，此方法将返回在 .NET 中可用的任何标准编码、代码页编码或 DBCS 编码。 可通过重载同时指定编码器和解码器的回退对象。

> [!NOTE]
> Unicode Standard 将码位（数字）和名称指派给每个受支持脚本中的各字符。 例如，码位 U+0041 表示字符“A”，“LATIN CAPITAL LETTER A”表示名称。 Unicode 转换格式 (UTF) 编码定义将码位编码为一系列一个或多个字节的方式。 Unicode 编码方案简化全球通用的应用程序的开发，因为它允许以单个编码表示任何字符集中的字符。 应用程序开发人员不再需要跟踪用于为特定语言或写入系统生成字符的编码方案，且数据可以在全球系统间共享，而不被损坏。
>
>  .NET 支持由 Unicode 标准定义的三种编码：UTF-8、UTF-16 和 UTF-32。 有关详细信息，请访问 [Unicode](http://www.unicode.org/) 主页，查看 Unicode 标准。
 
.NET 支持下表中列出的字符编码系统。

编码 | 类 | 描述 | 优点/缺点
-------- | ----- | ----------- | ------------------------ 
ASCII | [ASCIIEncoding](xref:System.Text.ASCIIEncoding) | 通过使用较低的七位字节将有限范围的字符进行编码。 | 由于此编码仅支持从 U+0000 到 U+007F 的字符值，因此在大多数情况下不足以支持国际化的应用程序。
UTF-7 | [UTF7Encoding](xref:System.Text.UTF7Encoding) | 将字符表示为 7 位 ASCII 字符的序列。 非 ASCII Unicode 字符由 ASCII 字符的转义序列表示。 | Utf-7 支持诸如电子邮件和新闻组协议等协议。 但是，utf-7 不是特别安全或可靠。 在某些情况下，更改一位可以彻底更改对整个 utf-7 字符串的解释。 在其他情况下，不同的 utf-7 字符串可以对相同的文本进行编码。 对于包含非 ASCII 字符的序列，utf-7 需要比 utf-8 更多的空间，且编码/解码更慢。 因此，应尽可能使用 utf-8，而不是 utf-7。
UTF-8 | [UTF8Encoding](xref:System.Text.UTF8Encoding) | 将每个 Unicode 码位表示为一至四个字节的序列。 | Utf-8 支持 8 位数据大小，适用于许多现有的操作系统。 对于字符的 ASCII 范围，utf-8 等同于 ASCII 编码，并适用于范围更广的字符集。 但是，对于中日韩 (CJK) 脚本而言，针对每个字符 utf-8 可能需要三个字节，并且可能会导致比 utf-16 更大的数据大小。 请注意，有时 ASCII 数据（如 HTML 标记）的量证明了 CJK 范围大小增加的合理性。
UTF-16 | [UnicodeEncoding](xref:System.Text.UnicodeEncoding) | 将每个 Unicode 码位表示为一至两个 16 位整数的序列。 尽管 Unicode 补充字符（U+10000 和更高版本）需要两个 utf-16 代理项码位，但最常见的 Unicode 字符仅需一个 utf-16 码位。 little-endian 和 big endian 字节顺序均受支持。 | 公共语言运行时使用 UTF-16 编码表示 Char 和 String 值，Windows 操作系统使用它表示 WCHAR 值。
UTF-32 | [UTF32Encoding](xref:System.Text.UTF32Encoding) | 将每个 Unicode 码位表示为一个 32 位整数。 little-endian 和 big endian 字节顺序均受支持。 | 当应用程序想要避免操作系统上的 utf-16 编码的代理项码位行为时，则使用 utf-32 编码，编码空间对操作系统十分重要。 显示器上呈现的单个标志符号仍可使用多个 UTF-32 字符进行编码。

这些编码使你能够使用 Unicode 字符以及旧版应用程序中最常用的编码。 此外，通过定义从 [Encoding](xref:System.Text.Encoding) 派生的类并重写其成员，可创建自定义编码。

> [!NOTE]
> 默认情况下，.NET Core 不提供除代码页 28591 以外的其他任何代码页编码和 Unicode 编码，例如 UTF-8 和 UTF-16。 但是，可以将在面向 .NET Framework 的标准 Windows 应用中找到的代码页编码添加到你的应用程序中。 有关完整信息，请参阅 [EncodingProvider](xref:System.Text.EncodingProvider) 主题。 

## <a name="selecting-an-encoding-class"></a>选择编码类

如果有机会选择应用程序要使用的编码，则应使用 Unicode 编码，最好是 [UTF8Encoding](xref:System.Text.UTF8Encoding) 或 [UnicodeEncoding](xref:System.Text.UnicodeEncoding)。 （.NET 还支持第三种 Unicode 编码，[UTF32Encoding](xref:System.Text.UTF32Encoding)。） 

如果打算使用 ASCII 编码 ([ASCIIEncoding](xref:System.Text.ASCIIEncoding))，请选择 [UTF8Encoding](xref:System.Text.UTF8Encoding)。 这两个编码对于 ASCII 字符集而言是相同的，但 [UTF8Encoding](xref:System.Text.UTF8Encoding) 具有以下优点： 

* 它可以表示每个 Unicode 字符，而 [ASCIIEncoding](xref:System.Text.ASCIIEncoding) 仅支持 U+0000 到 U+007F 之间的 Unicode 字符值。

* 它提供错误检测，具有更高的安全性。

* 速度已达到最优，应快于任何其他编码。 即使对于全是 ASCII 的内容，使用 [UTF8Encoding](xref:System.Text.UTF8Encoding) 执行操作的速度要快于 [ASCIIEncoding](xref:System.Text.ASCIIEncoding)。

应考虑仅针对旧版应用程序使用 [ASCIIEncoding](xref:System.Text.ASCIIEncoding)。 但是，即使对于旧版应用程序，由于以下原因，[UTF8Encoding](xref:System.Text.UTF8Encoding) 可能是更好的选择（假定采用默认设置）：

* 如果应用程序具有的内容不完全是 ASCII 并使用 [ASCIIEncoding](xref:System.Text.ASCIIEncoding) 将其编码，则每个非 ASCII 字符将编码为一个问号 (?)。 如果应用程序随后对此数据进行解码，则信息丢失。


* 如果应用程序具有的内容不完全是 ASCII 并使用 [UTF8Encoding](xref:System.Text.UTF8Encoding) 将其编码，则结果看起来将无法识别（如果解释为 ASCII）。 但是，如果应用程序随后使用 utf-8 解码器将此数据进行解码，则数据成功执行一次往返过程。

在 web 应用程序中，发送到响应 web 请求的客户端中的字符应反映客户端上所使用的编码。 在大多数情况下，应将 [HttpResponse.ContentEncoding](xref:System.Net.HttpResponseHeader.ContentEncoding) 属性设置为 [HttpRequestHeader.ContentEncoding](xref:System.Net.HttpRequestHeader.ContentEncoding) 属性返回的值，从而以用户期望的编码显示文本。

## <a name="using-an-encoding-object"></a>使用编码对象

编码器将一个字符串（最常见的为 Unicode 字符）转换为其数字（字节）等效项。 例如，你可能会使用 ASCII 编码器将 Unicode 字符转换为 ASCII，以便可在控制台中显示。 若要执行转换，请调用 [Encoding.GetBytes](xref:System.Text.Encoding.GetBytes(System.Char[])) 方法。 如果想要在执行编码前确定需要多少个字节来存储编码字符，可调用 [GetByteCount](xref:System.Text.Encoding.GetByteCount(System.Char[])) 方法。

下面的示例使用单个字节数组，从而在两个单独的操作中对字符串进行编码。 它为下一组 ASCII 编码字节保持指示字节数组中的起始位置的索引。 它调用 [ASCIIEncoding.GetByteCount(String)](xref:System.Text.ASCIIEncoding.GetByteCount(System.String)) 方法，确保字节数组足够大，从而可容纳已编码的字符串。 然后调用 [ASCIIEncoding.GetBytes(String, Int32, Int32, Byte[], Int32)](xref:System.Text.ASCIIEncoding.GetBytes(System.Char[],System.Int32,System.Int32,System.Byte[],System.Int32)) 方法为字符串中的字符编码。

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      string[] strings= { "This is the first sentence. ", 
                          "This is the second sentence. " };
      Encoding asciiEncoding = Encoding.ASCII;

      // Create array of adequate size.
      byte[] bytes = new byte[49];
      // Create index for current position of array.
      int index = 0;

      Console.WriteLine("Strings to encode:");
      foreach (var stringValue in strings) {
         Console.WriteLine("   {0}", stringValue);

         int count = asciiEncoding.GetByteCount(stringValue);
         if (count + index >=  bytes.Length)
            Array.Resize(ref bytes, bytes.Length + 50);

         int written = asciiEncoding.GetBytes(stringValue, 0, 
                                              stringValue.Length, 
                                              bytes, index);    

         index = index + written; 
      } 
      Console.WriteLine("\nEncoded bytes:");
      Console.WriteLine("{0}", ShowByteValues(bytes, index));
      Console.WriteLine();

      // Decode Unicode byte array to a string.
      string newString = asciiEncoding.GetString(bytes, 0, index);
      Console.WriteLine("Decoded: {0}", newString);
   }

   private static string ShowByteValues(byte[] bytes, int last ) 
   {
      string returnString = "   ";
      for (int ctr = 0; ctr <= last - 1; ctr++) {
         if (ctr % 20 == 0)
            returnString += "\n   ";
         returnString += String.Format("{0:X2} ", bytes[ctr]);
      }
      return returnString;
   }
}
// The example displays the following output:
//       Strings to encode:
//          This is the first sentence.
//          This is the second sentence.
//       
//       Encoded bytes:
//       
//          54 68 69 73 20 69 73 20 74 68 65 20 66 69 72 73 74 20 73 65
//          6E 74 65 6E 63 65 2E 20 54 68 69 73 20 69 73 20 74 68 65 20
//          73 65 63 6F 6E 64 20 73 65 6E 74 65 6E 63 65 2E 20
//       
//       Decoded: This is the first sentence. This is the second sentence.
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      Dim strings() As String = { "This is the first sentence. ", 
                                  "This is the second sentence. " }
      Dim asciiEncoding As Encoding = Encoding.ASCII

      ' Create array of adequate size.
      Dim bytes(50) As Byte
      ' Create index for current position of array.
      Dim index As Integer = 0

      Console.WriteLine("Strings to encode:")
      For Each stringValue In strings
         Console.WriteLine("   {0}", stringValue)

         Dim count As Integer = asciiEncoding.GetByteCount(stringValue)
         If count + index >=  bytes.Length Then
            Array.Resize(bytes, bytes.Length + 50)
         End If
         Dim written As Integer = asciiEncoding.GetBytes(stringValue, 0, 
                                                         stringValue.Length, 
                                                         bytes, index)    

         index = index + written 
      Next 
      Console.WriteLine()
      Console.WriteLine("Encoded bytes:")
      Console.WriteLine("{0}", ShowByteValues(bytes, index))
      Console.WriteLine()

      ' Decode Unicode byte array to a string.
      Dim newString As String = asciiEncoding.GetString(bytes, 0, index)
      Console.WriteLine("Decoded: {0}", newString)
   End Sub

   Private Function ShowByteValues(bytes As Byte(), last As Integer) As String
      Dim returnString As String = "   "
      For ctr As Integer = 0 To last - 1
         If ctr Mod 20 = 0 Then returnString += vbCrLf + "   "
         returnString += String.Format("{0:X2} ", bytes(ctr))
      Next
      Return returnString
   End Function
End Module
' The example displays the following output:
'       Strings to encode:
'          This is the first sentence.
'          This is the second sentence.
'       
'       Encoded bytes:
'       
'          54 68 69 73 20 69 73 20 74 68 65 20 66 69 72 73 74 20 73 65
'          6E 74 65 6E 63 65 2E 20 54 68 69 73 20 69 73 20 74 68 65 20
'          73 65 63 6F 6E 64 20 73 65 6E 74 65 6E 63 65 2E 20
'       
'       Decoded: This is the first sentence. This is the second sentence.
```

解码器将反映特定字符编码的字节数组转换为字符数组或字符串中的一组字符。 若要将字节数组解码为字符数组，请调用 [Encoding.GetChars](xref:System.Text.Encoding.GetChars(System.Byte[])) 方法。 若要将字节数组解码为字符串，请调用 [GetString](xref:System.Text.Encoding.GetString(System.Byte[])) 方法。 如果想在执行解码前确定需要多少个字符来存储已解码的字节，可调用 [GetCharCount](xref:System.Text.Encoding.GetCharCount(System.Byte[])) 方法。

下面的示例对三个字符串进行编码，然后将它们解码为单个字符数组。 它为下一组解码的字符保持指示字符数组中的起始位置的索引。 它调用 [GetCharCount](xref:System.Text.Encoding.GetCharCount(System.Byte[])) 方法确保字符数组足够大，从而可容纳所有已解码的字符。 然后调用 [ASCIIEncoding.GetChars(Byte[], Int32, Int32, Char[], Int32)](xref:System.Text.ASCIIEncoding.GetChars(System.Byte[],System.Int32,System.Int32,System.Char[],System.Int32)) 方法将字节数组解码。

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      string[] strings = { "This is the first sentence. ", 
                           "This is the second sentence. ",
                           "This is the third sentence. " };
      Encoding asciiEncoding = Encoding.ASCII;
      // Array to hold encoded bytes.
      byte[] bytes;
      // Array to hold decoded characters.
      char[] chars = new char[50];
      // Create index for current position of character array.
      int index = 0;     

      foreach (var stringValue in strings) {
         Console.WriteLine("String to Encode: {0}", stringValue);
         // Encode the string to a byte array.
         bytes = asciiEncoding.GetBytes(stringValue);
         // Display the encoded bytes.
         Console.Write("Encoded bytes: ");
         for (int ctr = 0; ctr < bytes.Length; ctr++)
            Console.Write(" {0}{1:X2}", 
                          ctr % 20 == 0 ? Environment.NewLine : "", 
                          bytes[ctr]);
         Console.WriteLine();

         // Decode the bytes to a single character array.
         int count = asciiEncoding.GetCharCount(bytes);
         if (count + index >=  chars.Length)
            Array.Resize(ref chars, chars.Length + 50);

         int written = asciiEncoding.GetChars(bytes, 0, 
                                              bytes.Length, 
                                              chars, index);              
         index = index + written;
         Console.WriteLine();       
      }

      // Instantiate a single string containing the characters.
      string decodedString = new string(chars, 0, index - 1);
      Console.WriteLine("Decoded string: ");
      Console.WriteLine(decodedString);
   }
}
// The example displays the following output:
//    String to Encode: This is the first sentence.
//    Encoded bytes:
//    54 68 69 73 20 69 73 20 74 68 65 20 66 69 72 73 74 20 73 65
//    6E 74 65 6E 63 65 2E 20
//    
//    String to Encode: This is the second sentence.
//    Encoded bytes:
//    54 68 69 73 20 69 73 20 74 68 65 20 73 65 63 6F 6E 64 20 73
//    65 6E 74 65 6E 63 65 2E 20
//    
//    String to Encode: This is the third sentence.
//    Encoded bytes:
//    54 68 69 73 20 69 73 20 74 68 65 20 74 68 69 72 64 20 73 65
//    6E 74 65 6E 63 65 2E 20
//    
//    Decoded string:
//    This is the first sentence. This is the second sentence. This is the third sentence.
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      Dim strings() As String = { "This is the first sentence. ", 
                                  "This is the second sentence. ",
                                  "This is the third sentence. " }
      Dim asciiEncoding As Encoding = Encoding.ASCII
      ' Array to hold encoded bytes.
      Dim bytes() As Byte
      ' Array to hold decoded characters.
      Dim chars(50) As Char
      ' Create index for current position of character array.
      Dim index As Integer     

      For Each stringValue In strings
         Console.WriteLine("String to Encode: {0}", stringValue)
         ' Encode the string to a byte array.
         bytes = asciiEncoding.GetBytes(stringValue)
         ' Display the encoded bytes.
         Console.Write("Encoded bytes: ")
         For ctr As Integer = 0 To bytes.Length - 1
            Console.Write(" {0}{1:X2}", If(ctr Mod 20 = 0, vbCrLf, ""), 
                                        bytes(ctr))
         Next         
         Console.WriteLine()

         ' Decode the bytes to a single character array.
         Dim count As Integer = asciiEncoding.GetCharCount(bytes)
         If count + index >=  chars.Length Then
            Array.Resize(chars, chars.Length + 50)
         End If
         Dim written As Integer = asciiEncoding.GetChars(bytes, 0, 
                                                         bytes.Length, 
                                                         chars, index)              
         index = index + written
         Console.WriteLine()       
      Next

      ' Instantiate a single string containing the characters.
      Dim decodedString As New String(chars, 0, index - 1)
      Console.WriteLine("Decoded string: ")
      Console.WriteLine(decodedString)
   End Sub
End Module
' The example displays the following output:
'    String to Encode: This is the first sentence.
'    Encoded bytes:
'    54 68 69 73 20 69 73 20 74 68 65 20 66 69 72 73 74 20 73 65
'    6E 74 65 6E 63 65 2E 20
'    
'    String to Encode: This is the second sentence.
'    Encoded bytes:
'    54 68 69 73 20 69 73 20 74 68 65 20 73 65 63 6F 6E 64 20 73
'    65 6E 74 65 6E 63 65 2E 20
'    
'    String to Encode: This is the third sentence.
'    Encoded bytes:
'    54 68 69 73 20 69 73 20 74 68 65 20 74 68 69 72 64 20 73 65
'    6E 74 65 6E 63 65 2E 20
'    
'    Decoded string:
'    This is the first sentence. This is the second sentence. This is the third sentence.
```

从 [Encoding](xref:System.Text.Encoding) 派生的类的编码和解码方法旨在用于一组完整的数据；也就是说，在单个方法调用中提供要进行编码或解码的所有数据。 但是，在某些情况下，数据在流中可用，并且要编码或解码的数据可能仅可从单独的读取操作中获取。 这要求编码或解码操作记住其之前调用中保存的任何状态。 从 [Encoder](xref:System.Text.Encoder) 和 [Decoder](xref:System.Text.Decoder) 派生的类的方法能够处理跨多个方法调用的编码和解码操作。

特定编码的 [Encoder](xref:System.Text.Encoder) 对象可从此编码的 [Encoding.GetEncoder](xref:System.Text.Encoding.GetEncoder) 属性获取。 特定编码的 [Decoder](xref:System.Text.Decoder) 对象可从该编码的 [Encoding.GetDecoder](xref:System.Text.Encoding.GetDecoder) 属性获取。 对于解码操作，请注意，从 [Decoder](xref:System.Text.Decoder) 派生的类包含 [Decoder.GetChars](xref:System.Text.Decoder.GetChars(System.Byte[],System.Int32,System.Int32,System.Char[],System.Int32)) 方法，但不包含对应于 [Encoding.GetString](xref:System.Text.Encoding.GetString(System.Byte[])) 的方法。

下面的示例演示使用 [Encoding.GetChars](xref:System.Text.Encoding.GetChars(System.Byte[])) 和 [Decoder.GetChars](xref:System.Text.Decoder.GetChars(System.Byte[],System.Int32,System.Int32,System.Char[],System.Int32)) 方法解码 Unicode 字节数组的差异。 该示例将包含某些 Unicode 字符的字符串编码为文件，然后使用两种解码方法一次解码十个字节。 由于代理项对发生在第十个和第十一个字节，因此它在单独的方法调用中进行解码。 如输出所示，[Encoding.GetChars](xref:System.Text.Encoding.GetChars(System.Byte[])) 方法不能正确地对字节进行解码，而是将它们替换为 U+FFFD（替换字符）。 另一方面，[Decoder.GetChars](xref:System.Text.Decoder.GetChars(System.Byte[],System.Int32,System.Int32,System.Char[],System.Int32)) 方法能够成功地对字节数组进行解码以获取原始字符串。

```csharp
using System;
using System.IO;
using System.Text;

public class Example
{
   public static void Main()
   {
      // Use default replacement fallback for invalid encoding.
      UnicodeEncoding enc = new UnicodeEncoding(true, false, false);

      // Define a string with various Unicode characters.
      string str1 = "AB YZ 19 \uD800\udc05 \u00e4"; 
      str1 += "Unicode characters. \u00a9 \u010C s \u0062\u0308"; 
      Console.WriteLine("Created original string...\n");

      // Convert string to byte array.                     
      byte[] bytes = enc.GetBytes(str1);

      FileStream fs = File.Create(@".\characters.bin");
      BinaryWriter bw = new BinaryWriter(fs);
      bw.Write(bytes);
      bw.Close();

      // Read bytes from file.
      FileStream fsIn = File.OpenRead(@".\characters.bin");
      BinaryReader br = new BinaryReader(fsIn);

      const int count = 10;            // Number of bytes to read at a time. 
      byte[] bytesRead = new byte[10]; // Buffer (byte array).
      int read;                        // Number of bytes actually read. 
      string str2 = String.Empty;      // Decoded string.

      // Try using Encoding object for all operations.
      do { 
         read = br.Read(bytesRead, 0, count);
         str2 += enc.GetString(bytesRead, 0, read); 
      } while (read == count);
      br.Close();
      Console.WriteLine("Decoded string using UnicodeEncoding.GetString()...");
      CompareForEquality(str1, str2);
      Console.WriteLine();

      // Use Decoder for all operations.
      fsIn = File.OpenRead(@".\characters.bin");
      br = new BinaryReader(fsIn);
      Decoder decoder = enc.GetDecoder();
      char[] chars = new char[50];
      int index = 0;                   // Next character to write in array.
      int written = 0;                 // Number of chars written to array.
      do { 
         read = br.Read(bytesRead, 0, count);
         if (index + decoder.GetCharCount(bytesRead, 0, read) - 1 >= chars.Length) 
            Array.Resize(ref chars, chars.Length + 50);

         written = decoder.GetChars(bytesRead, 0, read, chars, index);
         index += written;                          
      } while (read == count);
      br.Close();            
      // Instantiate a string with the decoded characters.
      string str3 = new String(chars, 0, index); 
      Console.WriteLine("Decoded string using UnicodeEncoding.Decoder.GetString()...");
      CompareForEquality(str1, str3); 
   }

   private static void CompareForEquality(string original, string decoded)
   {
      bool result = original.Equals(decoded);
      Console.WriteLine("original = decoded: {0}", 
                        original.Equals(decoded, StringComparison.Ordinal));
      if (! result) {
         Console.WriteLine("Code points in original string:");
         foreach (var ch in original)
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));
         Console.WriteLine();

         Console.WriteLine("Code points in decoded string:");
         foreach (var ch in decoded)
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));
         Console.WriteLine();
      }
   }
}
// The example displays the following output:
//    Created original string...
//    
//    Decoded string using UnicodeEncoding.GetString()...
//    original = decoded: False
//    Code points in original string:
//    0041 0042 0020 0059 005A 0020 0031 0039 0020 D800 DC05 0020 00E4 0055 006E 0069 0063 006F
//    0064 0065 0020 0063 0068 0061 0072 0061 0063 0074 0065 0072 0073 002E 0020 00A9 0020 010C
//    0020 0073 0020 0062 0308
//    Code points in decoded string:
//    0041 0042 0020 0059 005A 0020 0031 0039 0020 FFFD FFFD 0020 00E4 0055 006E 0069 0063 006F
//    0064 0065 0020 0063 0068 0061 0072 0061 0063 0074 0065 0072 0073 002E 0020 00A9 0020 010C
//    0020 0073 0020 0062 0308
//    
//    Decoded string using UnicodeEncoding.Decoder.GetString()...
//    original = decoded: True
```

```vb
Imports System.IO
Imports System.Text

Module Example
   Public Sub Main()
      ' Use default replacement fallback for invalid encoding.
      Dim enc As New UnicodeEncoding(True, False, False)

      ' Define a string with various Unicode characters.
      Dim str1 As String = String.Format("AB YZ 19 {0}{1} {2}", 
                                         ChrW(&hD800), ChrW(&hDC05), ChrW(&h00e4))
      str1 += String.Format("Unicode characters. {0} {1} s {2}{3}", 
                            ChrW(&h00a9), ChrW(&h010C), ChrW(&h0062), ChrW(&h0308))
      Console.WriteLine("Created original string...")
      Console.WriteLine()

      ' Convert string to byte array.                     
      Dim bytes() As Byte = enc.GetBytes(str1)

      Dim fs As FileStream = File.Create(".\characters.bin")
      Dim bw As New BinaryWriter(fs)
      bw.Write(bytes)
      bw.Close()

      ' Read bytes from file.
      Dim fsIn As FileStream = File.OpenRead(".\characters.bin")
      Dim br As New BinaryReader(fsIn)

      Const count As Integer = 10      ' Number of bytes to read at a time. 
      Dim bytesRead(9) As Byte         ' Buffer (byte array).
      Dim read As Integer              ' Number of bytes actually read. 
      Dim str2 As String = ""          ' Decoded string.

      ' Try using Encoding object for all operations.
      Do 
         read = br.Read(bytesRead, 0, count)
         str2 += enc.GetString(bytesRead, 0, read) 
      Loop While read = count
      br.Close()
      Console.WriteLine("Decoded string using UnicodeEncoding.GetString()...")
      CompareForEquality(str1, str2)
      Console.WriteLine()

      ' Use Decoder for all operations.
      fsIn = File.OpenRead(".\characters.bin")
      br = New BinaryReader(fsIn)
      Dim decoder As Decoder = enc.GetDecoder()
      Dim chars(50) As Char
      Dim index As Integer = 0         ' Next character to write in array.
      Dim written As Integer = 0       ' Number of chars written to array.
      Do 
         read = br.Read(bytesRead, 0, count)
         If index + decoder.GetCharCount(bytesRead, 0, read) - 1 >= chars.Length Then 
            Array.Resize(chars, chars.Length + 50)
         End If   
         written = decoder.GetChars(bytesRead, 0, read, chars, index)
         index += written                          
      Loop While read = count
      br.Close()            
      ' Instantiate a string with the decoded characters.
      Dim str3 As New String(chars, 0, index) 
      Console.WriteLine("Decoded string using UnicodeEncoding.Decoder.GetString()...")
      CompareForEquality(str1, str3) 
   End Sub

   Private Sub CompareForEquality(original As String, decoded As String)
      Dim result As Boolean = original.Equals(decoded)
      Console.WriteLine("original = decoded: {0}", 
                        original.Equals(decoded, StringComparison.Ordinal))
      If Not result Then
         Console.WriteLine("Code points in original string:")
         For Each ch In original
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
         Next
         Console.WriteLine()

         Console.WriteLine("Code points in decoded string:")
         For Each ch In decoded
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
         Next
         Console.WriteLine()
      End If
   End Sub
End Module
' The example displays the following output:
'    Created original string...
'    
'    Decoded string using UnicodeEncoding.GetString()...
'    original = decoded: False
'    Code points in original string:
'    0041 0042 0020 0059 005A 0020 0031 0039 0020 D800 DC05 0020 00E4 0055 006E 0069 0063 006F
'    0064 0065 0020 0063 0068 0061 0072 0061 0063 0074 0065 0072 0073 002E 0020 00A9 0020 010C
'    0020 0073 0020 0062 0308
'    Code points in decoded string:
'    0041 0042 0020 0059 005A 0020 0031 0039 0020 FFFD FFFD 0020 00E4 0055 006E 0069 0063 006F
'    0064 0065 0020 0063 0068 0061 0072 0061 0063 0074 0065 0072 0073 002E 0020 00A9 0020 010C
'    0020 0073 0020 0062 0308
'    
'    Decoded string using UnicodeEncoding.Decoder.GetString()...
'    original = decoded: True
```

## <a name="choosing-a-fallback-strategy"></a>选择回退策略

当某个方法尝试对字符进行编码或解码，但不存在映射时，它必须实现回退策略，以确定应如何处理失败的映射。 有三种类型的回退策略： 

* 最佳回退

* 替换回退

* 异常回退

> [!IMPORTANT]
> 当某一 Unicode 字符不能映射到特定代码页编码时，在编码操作中将发生最常见的问题。 当无效的字节序列无法转换为有效的 Unicode 字符，在解码操作中将发生最常见的问题。 出于这些原因，应该了解特定的编码对象使用哪种回退策略。 只要有可能，应指定实例化对象时编码对象使用的回退策略。
 
### <a name="best-fit-fallback"></a>最佳回退

当一个字符在目标编码中不具有准确匹配时，编码器可以尝试将其映射到类似的字符。 （最佳回退主要是编码问题而非解码问题。 很少有代码页包含无法成功映射到 Unicode 的字符。）最佳回退是代码页的默认设置，此双字节字符集编码由 [Encoding.GetEncoding(Int32)](xref:System.Text.Encoding.GetEncoding(System.Int32)) 和 [Encoding.GetEncoding(String)](xref:System.Text.Encoding.GetEncoding(System.String)) 重载检索。

> [!NOTE]
> 从理论上讲，.NET 中提供的 Unicode 编码类（[UTF8Encoding](xref:System.Text.UTF8Encoding)、[UnicodeEncoding](xref:System.Text.UnicodeEncoding) 和 [UTF32Encoding](xref:System.Text.UTF32Encoding)）支持每个字符集中的每个字符，因此它们可用于消除最佳回退的问题。 
 

不同代码页的最佳策略不同，未对它们进行详细记录。 例如，对于某些代码页，全角拉丁字符映射到更常见的半角拉丁字符。 对于其他代码页，不进行此映射。 即使是在积极的最佳策略下，也不能完全适合某些编码中的某些字符。 例如，中文象形文字不具有到代码页 1252 的合理映射。 在这种情况下，使用替换字符串。 默认情况下，此字符串只是一个问号 (U+003F)。

下面的示例使用代码页 1252 （适合西欧语言 Windows 代码页）演示最佳映射及其缺点。 [Encoding.GetEncoding(Int32](xref:System.Text.Encoding.GetEncoding(System.Int32)) 方法用于检索代码页 1252 的编码对象。 默认情况下，它使用其不支持的 Unicode 字符的最佳映射。 该示例将包含三个非 ASCII 字符的字符串实例化，这三个字符分别为带圆圈拉丁文大写字母 S (U+24C8)、上标五 (U+2075) 和无穷大 (U+221E) 且由空格分隔。 如示例输出所示，当对字符串进行编码时，三个原始的非空格字符替换为问号 (U+003F)、数字五 (U+0035) 和数字八 (U+0038)。 数字八是对不受支持的无穷大字符的不良替换，问号指示没有映射可用于原始字符。

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      // Get an encoding for code page 1252 (Western Europe character set).
      Encoding cp1252 = Encoding.GetEncoding(1252);

      // Define and display a string.
      string str = "\u24c8 \u2075 \u221e";
      Console.WriteLine("Original string: " + str);
      Console.Write("Code points in string: ");
      foreach (var ch in str)
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

      Console.WriteLine("\n");   

      // Encode a Unicode string.
      Byte[] bytes = cp1252.GetBytes(str);
      Console.Write("Encoded bytes: ");
      foreach (byte byt in bytes)
         Console.Write("{0:X2} ", byt);
      Console.WriteLine("\n");

      // Decode the string.
      string str2 = cp1252.GetString(bytes);
      Console.WriteLine("String round-tripped: {0}", str.Equals(str2));
      if (! str.Equals(str2)) {
         Console.WriteLine(str2);
         foreach (var ch in str2)
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));
      }
   }
}
// The example displays the following output:
//       Original string: Ⓢ ⁵ ∞
//       Code points in string: 24C8 0020 2075 0020 221E
//       
//       Encoded bytes: 3F 20 35 20 38
//       
//       String round-tripped: False
//       ? 5 8
//       003F 0020 0035 0020 0038
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      ' Get an encoding for code page 1252 (Western Europe character set).
      Dim cp1252 As Encoding = Encoding.GetEncoding(1252)

      ' Define and display a string.
      Dim str As String = String.Format("{0} {1} {2}", ChrW(&h24c8), ChrW(&H2075), ChrW(&h221E))
      Console.WriteLine("Original string: " + str)
      Console.Write("Code points in string: ")
      For Each ch In str
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
      Next
      Console.WriteLine()   
      Console.WriteLine()

      ' Encode a Unicode string.
      Dim bytes() As Byte = cp1252.GetBytes(str)
      Console.Write("Encoded bytes: ")
      For Each byt In bytes
         Console.Write("{0:X2} ", byt)
      Next
      Console.WriteLine()
      Console.WriteLine()

      ' Decode the string.
      Dim str2 As String = cp1252.GetString(bytes)
      Console.WriteLine("String round-tripped: {0}", str.Equals(str2))
      If Not str.Equals(str2) Then
         Console.WriteLine(str2)
         For Each ch In str2
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
         Next
      End If
   End Sub
End Module
' The example displays the following output:
'       Original string: Ⓢ ⁵ ∞
'       Code points in string: 24C8 0020 2075 0020 221E
'       
'       Encoded bytes: 3F 20 35 20 38
'       
'       String round-tripped: False
'       ? 5 8
'       003F 0020 0035 0020 0038
```

最佳映射是 [Encoding](xref:System.Text.Encoding) 对象的默认行为，该对象将 Unicode 数据编码为代码页数据，并且存在依赖此行为的旧版应用程序。 但是，为了安全起见，大多数新应用程序应避免最佳行为。 例如，应用程序不应通过最佳编码放置域名。

> [!Note]
> 还可实现编码的自定义最佳回退映射。 有关详细信息，请参阅[实现自定义回退策略](#implementing-a-custom-fallback-strategy)部分。
 
如果最佳回退是编码对象的默认设置，当通过调用 [Encoding.GetEncoding(Int32, EncoderFallback, DecoderFallback)](xref:System.Text.Encoding.GetEncoding(System.Int32,System.Text.EncoderFallback,System.Text.DecoderFallback)) 或 [Encoding.GetEncoding(String, EncoderFallback, DecoderFallback)](xref:System.Text.Encoding.GetEncoding(System.String,System.Text.EncoderFallback,System.Text.DecoderFallback)) 重载检索.[Encoding](xref:System.Text.Encoding) 对象时，可选择另一个回退策略。 以下一节的内容包括一个示例，该示例用星号 (\*) 替换每个不可映射到代码页 1252 的每个字符。

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      Encoding cp1252r = Encoding.GetEncoding(1252, 
                                  new EncoderReplacementFallback("*"),
                                  new DecoderReplacementFallback("*"));

      string str1 = "\u24C8 \u2075 \u221E";
      Console.WriteLine(str1);
      foreach (var ch in str1)
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

      Console.WriteLine();

      byte[] bytes = cp1252r.GetBytes(str1);
      string str2 = cp1252r.GetString(bytes);
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2));
      if (! str1.Equals(str2)) {
         Console.WriteLine(str2);
         foreach (var ch in str2)
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

         Console.WriteLine();
      } 
   }
}
// The example displays the following output:
//       Ⓢ ⁵ ∞
//       24C8 0020 2075 0020 221E
//       Round-trip: False
//       * * *
//       002A 0020 002A 0020 002A
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      Dim cp1252r As Encoding = Encoding.GetEncoding(1252, 
                                         New EncoderReplacementFallback("*"),
                                         New DecoderReplacementFallback("*"))

      Dim str1 As String = String.Format("{0} {1} {2}", ChrW(&h24C8), ChrW(&h2075), ChrW(&h221E))
      Console.WriteLine(str1)
      For Each ch In str1
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
      Next    
      Console.WriteLine()

      Dim bytes() As Byte = cp1252r.GetBytes(str1)
      Dim str2 As String = cp1252r.GetString(bytes)
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2))
      If Not str1.Equals(str2) Then
         Console.WriteLine(str2)
         For Each ch In str2
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
         Next    
         Console.WriteLine()
      End If 
   End Sub
End Module
' The example displays the following output:
'       Ⓢ ⁵ ∞
'       24C8 0020 2075 0020 221E
'       Round-trip: False
'       * * *
'       002A 0020 002A 0020 002A
```

### <a name="replacement-fallback"></a>替换回退

当字符在目标方案中没有准确匹配，但是也没有其可映射到的相应字符，则应用程序可指定替换字符或字符串。 这是 Unicode 编码器的默认行为，此默认行为替换其无法用 REPLACEMENT_CHARACTER (U+FFFD) 进行解码的任何双字节序列。 它也是 [ASCIIEncoding](xref:System.Text.ASCIIEncoding) 类的默认行为，此默认行为替换其无法用问号进行编码或解码的每个字符。 下面的示例演示上一示例中 Unicode 字符串的字符替换。 如输出所示，不能解码为 ASCII 字节值的每个字符都替换为 0x3F，这是问号的 ASCII 代码。

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      Encoding enc = Encoding.ASCII;

      string str1 = "\u24C8 \u2075 \u221E";
      Console.WriteLine(str1);
      foreach (var ch in str1)
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

      Console.WriteLine("\n");

      // Encode the original string using the ASCII encoder.
      byte[] bytes = enc.GetBytes(str1);
      Console.Write("Encoded bytes: ");
      foreach (var byt in bytes)
         Console.Write("{0:X2} ", byt);
      Console.WriteLine("\n");

      // Decode the ASCII bytes.
      string str2 = enc.GetString(bytes);
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2));
      if (! str1.Equals(str2)) {
         Console.WriteLine(str2);
         foreach (var ch in str2)
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

         Console.WriteLine();
      } 
   }
}
// The example displays the following output:
//       Ⓢ ⁵ ∞
//       24C8 0020 2075 0020 221E
//       
//       Encoded bytes: 3F 20 3F 20 3F
//       
//       Round-trip: False
//       ? ? ?
//       003F 0020 003F 0020 003F
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      Dim enc As Encoding = Encoding.Ascii

      Dim str1 As String = String.Format("{0} {1} {2}", ChrW(&h24C8), ChrW(&h2075), ChrW(&h221E))
      Console.WriteLine(str1)
      For Each ch In str1
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
      Next    
      Console.WriteLine()
      Console.WriteLine() 

      ' Encode the original string using the ASCII encoder.
      Dim bytes() As Byte = enc.GetBytes(str1)
      Console.Write("Encoded bytes: ")
      For Each byt In bytes
         Console.Write("{0:X2} ", byt)
      Next
      Console.WriteLine()
      Console.WriteLine()

      ' Decode the ASCII bytes.
      Dim str2 As String = enc.GetString(bytes)
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2))
      If Not str1.Equals(str2) Then
         Console.WriteLine(str2)
         For Each ch In str2
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
         Next    
         Console.WriteLine()
      End If 
   End Sub
End Module
' The example displays the following output:
'       Ⓢ ⁵ ∞
'       24C8 0020 2075 0020 221E
'       
'       Encoded bytes: 3F 20 3F 20 3F
'       
'       Round-trip: False
'       ? ? ?
'       003F 0020 003F 0020 003F
```

.NET 包括 [EncoderReplacementFallback](xref:System.Text.EncoderReplacementFallback) 和 [DecoderReplacementFallback](xref:System.Text.DecoderReplacementFallback) 类，如果字符没有在编码和解码操作中准确映射，则这些类将代替替换字符串。 默认情况下，此替换字符串是一个问号，但可以调用类构造函数重载以选择不同的字符串。 通常，替换字符串是单个字符，但这不是一项要求。 下面的示例通过将以星号 (\*) 作为替换字符串的 [EncoderReplacementFallback](xref:System.Text.EncoderReplacementFallback) 对象实例化，更改代码页 1252 编码器的行为。

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      Encoding cp1252r = Encoding.GetEncoding(1252, 
                                  new EncoderReplacementFallback("*"),
                                  new DecoderReplacementFallback("*"));

      string str1 = "\u24C8 \u2075 \u221E";
      Console.WriteLine(str1);
      foreach (var ch in str1)
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

      Console.WriteLine();

      byte[] bytes = cp1252r.GetBytes(str1);
      string str2 = cp1252r.GetString(bytes);
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2));
      if (! str1.Equals(str2)) {
         Console.WriteLine(str2);
         foreach (var ch in str2)
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

         Console.WriteLine();
      } 
   }
}
// The example displays the following output:
//       Ⓢ ⁵ ∞
//       24C8 0020 2075 0020 221E
//       Round-trip: False
//       * * *
//       002A 0020 002A 0020 002A
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      Dim cp1252r As Encoding = Encoding.GetEncoding(1252, 
                                         New EncoderReplacementFallback("*"),
                                         New DecoderReplacementFallback("*"))

      Dim str1 As String = String.Format("{0} {1} {2}", ChrW(&h24C8), ChrW(&h2075), ChrW(&h221E))
      Console.WriteLine(str1)
      For Each ch In str1
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
      Next    
      Console.WriteLine()

      Dim bytes() As Byte = cp1252r.GetBytes(str1)
      Dim str2 As String = cp1252r.GetString(bytes)
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2))
      If Not str1.Equals(str2) Then
         Console.WriteLine(str2)
         For Each ch In str2
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
         Next    
         Console.WriteLine()
      End If 
   End Sub
End Module
' The example displays the following output:
'       Ⓢ ⁵ ∞
'       24C8 0020 2075 0020 221E
'       Round-trip: False
'       * * *
'       002A 0020 002A 0020 002A
```

> [!NOTE]
> 还可以实现编码的替换类。 有关详细信息，请参阅[实现自定义回退策略](#implementing-a-custom-fallback-strategy)部分。
 
除了问号 (U+003F) 外，Unicode 替换字符 (U+FFFD) 通常用作替换字符串，特别是当解码无法成功转换为 Unicode 字符的字节序列时。 但是，你可以自由选择任何替换字符串，并且它可以包含多个字符。

### <a name="exception-fallback"></a>异常回退

如果编码器不能对一组字符进行编码，则它不会提供最佳回退或替换字符串，而可能引发 [EncoderFallbackException](xref:System.Text.EncoderFallbackException)；如果解码器不能对字节数组进行解码，则可能会引发 [DecoderFallbackException](xref:System.Text.DecoderFallbackException)。 若要在编码和解码操作中引发异常，请分别向 [Encoding.GetEncoding(String, EncoderFallback, DecoderFallback)](xref:System.Text.Encoding.GetEncoding(System.String,System.Text.EncoderFallback,System.Text.DecoderFallback)) 方法提供 [EncoderFallbackException](xref:System.Text.EncoderFallbackException) 对象和 [DecoderFallbackException](xref:System.Text.DecoderFallbackException) 对象。 下面的示例使用 ASCIIEncoding 类演示异常回退。

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      Encoding enc = Encoding.GetEncoding("us-ascii", 
                                          new EncoderExceptionFallback(), 
                                          new DecoderExceptionFallback());

      string str1 = "\u24C8 \u2075 \u221E";
      Console.WriteLine(str1);
      foreach (var ch in str1)
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

      Console.WriteLine("\n");

      // Encode the original string using the ASCII encoder.
      byte[] bytes = {};
      try {
         bytes = enc.GetBytes(str1);
         Console.Write("Encoded bytes: ");
         foreach (var byt in bytes)
            Console.Write("{0:X2} ", byt);

         Console.WriteLine();
      }
      catch (EncoderFallbackException e) {
         Console.Write("Exception: ");
         if (e.IsUnknownSurrogate())
            Console.WriteLine("Unable to encode surrogate pair 0x{0:X4} 0x{1:X3} at index {2}.", 
                              Convert.ToUInt16(e.CharUnknownHigh), 
                              Convert.ToUInt16(e.CharUnknownLow), 
                              e.Index);
         else
            Console.WriteLine("Unable to encode 0x{0:X4} at index {1}.", 
                              Convert.ToUInt16(e.CharUnknown), 
                              e.Index);
         return;
      }
      Console.WriteLine();

      // Decode the ASCII bytes.
      try {
         string str2 = enc.GetString(bytes);
         Console.WriteLine("Round-trip: {0}", str1.Equals(str2));
         if (! str1.Equals(str2)) {
            Console.WriteLine(str2);
            foreach (var ch in str2)
               Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

            Console.WriteLine();
         } 
      }
      catch (DecoderFallbackException e) {
         Console.Write("Unable to decode byte(s) ");
         foreach (byte unknown in e.BytesUnknown)
            Console.Write("0x{0:X2} ");

         Console.WriteLine("at index {0}", e.Index);
      }
   }
}
// The example displays the following output:
//       Ⓢ ⁵ ∞
//       24C8 0020 2075 0020 221E
//       
//       Exception: Unable to encode 0x24C8 at index 0.
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      Dim enc As Encoding = Encoding.GetEncoding("us-ascii", 
                                                 New EncoderExceptionFallback(), 
                                                 New DecoderExceptionFallback())

      Dim str1 As String = String.Format("{0} {1} {2}", ChrW(&h24C8), ChrW(&h2075), ChrW(&h221E))
      Console.WriteLine(str1)
      For Each ch In str1
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
      Next    
      Console.WriteLine()
      Console.WriteLine() 

      ' Encode the original string using the ASCII encoder.
      Dim bytes() As Byte = {}
      Try
         bytes = enc.GetBytes(str1)
         Console.Write("Encoded bytes: ")
         For Each byt In bytes
            Console.Write("{0:X2} ", byt)
         Next
         Console.WriteLine()
      Catch e As EncoderFallbackException
         Console.Write("Exception: ")
         If e.IsUnknownSurrogate() Then
            Console.WriteLine("Unable to encode surrogate pair 0x{0:X4} 0x{1:X3} at index {2}.", 
                              Convert.ToUInt16(e.CharUnknownHigh), 
                              Convert.ToUInt16(e.CharUnknownLow), 
                              e.Index)
         Else
            Console.WriteLine("Unable to encode 0x{0:X4} at index {1}.", 
                              Convert.ToUInt16(e.CharUnknown), 
                              e.Index)
         End If                              
         Exit Sub
      End Try
      Console.WriteLine()

      ' Decode the ASCII bytes.
      Try
         Dim str2 As String = enc.GetString(bytes)
         Console.WriteLine("Round-trip: {0}", str1.Equals(str2))
         If Not str1.Equals(str2) Then
            Console.WriteLine(str2)
            For Each ch In str2
               Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
            Next    
            Console.WriteLine()
         End If 
      Catch e As DecoderFallbackException
         Console.Write("Unable to decode byte(s) ")
         For Each unknown As Byte In e.BytesUnknown
            Console.Write("0x{0:X2} ")
         Next
         Console.WriteLine("at index {0}", e.Index)
      End Try
   End Sub
End Module
' The example displays the following output:
'       Ⓢ ⁵ ∞
'       24C8 0020 2075 0020 221E
'       
'       Exception: Unable to encode 0x24C8 at index 0.
```

> [!NOTE]
> 还可以实现编码操作的自定义异常处理程序。 有关详细信息，请参阅[实现自定义回退策略](#implementing-a-custom-fallback-strategy)部分。
 
[EncoderFallbackException](xref:System.Text.EncoderFallbackException) 和 [DecoderFallbackException](xref:System.Text.DecoderFallbackException) 对象提供以下有关导致异常的条件的信息： 

* [EncoderFallbackException](xref:System.Text.EncoderFallbackException) 对象包括 [IsUnknownSurrogate](xref:System.Text.EncoderFallbackException.IsUnknownSurrogate) 方法，该方法指示不能对其进行编码的一个字符或多个字符是代表未知的代理项对（在这种情况下，该方法返回 `true`）还是未知的单个字符（在这种情况下，该方法将返回 `false`）。 代理项对中的字符可从 [EncoderFallbackException.CharUnknownHigh](xref:System.Text.EncoderFallbackException.CharUnknownHigh) 和 [EncoderFallbackException.CharUnknownLow](xref:System.Text.EncoderFallbackException.CharUnknownLow) 属性获取。 未知的单个字符可从 [EncoderFallbackException.CharUnknown](xref:System.Text.EncoderFallbackException.CharUnknown) 属性获取。 [EncoderFallbackException.Index](xref:System.Text.EncoderFallbackException.Index) 属性指示字符串中第一个无法进行编码的字符的位置。

* [DecoderFallbackException](xref:System.Text.DecoderFallbackException) 对象包含 [BytesUnknown](xref:System.Text.DecoderFallbackException.BytesUnknown) 属性，该属性返回一个无法解码的字节数组。 [DecoderFallbackException.Index](xref:System.Text.DecoderFallbackException.Index) 属性指示未知字节的起始位置。

尽管 [EncoderFallbackException](xref:System.Text.EncoderFallbackException) 和 [DecoderFallbackException](xref:System.Text.DecoderFallbackException) 对象提供足够的有关异常的诊断信息，但不提供对编码或解码缓冲区的访问权限。 因此，它们不允许在编码或解码方法内替换或更正无效数据。

## <a name="implementing-a-custom-fallback-strategy"></a>实现自定义回退策略

除了由代码页在内部实现的最佳映射，.NET 包括用于实现回退策略的以下类：

* 使用 [EncoderReplacementFallback](xref:System.Text.EncoderReplacementFallback) 和 [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer) 替换编码操作中的字符。

* 使用 [DecoderReplacementFallback](xref:System.Text.DecoderReplacementFallback) 和 [DecoderFallbackBuffer](xref:System.Text.DecoderFallbackBuffer) 替换解码操作中的字符。

* 当字符无法编码时，使用 [EncoderExceptionFallback](xref:System.Text.EncoderExceptionFallback) 和 [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer) 引发 [EncoderFallbackException](xref:System.Text.EncoderFallbackException)。

* 当字符无法解码时，使用 [DecoderExceptionFallback](xref:System.Text.DecoderExceptionFallback) 和 [DecoderFallbackBuffer](xref:System.Text.DecoderFallbackBuffer) 引发 [DecoderFallbackException](xref:System.Text.DecoderFallbackException)。

此外，通过执行以下步骤，可以实现使用最佳回退、替换回退或异常回退的自定义解决方案： 

1. 从 [EncoderFallback](xref:System.Text.EncoderFallback) 派生一个类用于编码操作，从 [DecoderFallback](xref:System.Text.DecoderFallback) 派生一个类用于解码操作。

2. 从 [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer) 派生一个类用于编码操作，从 [DecoderFallbackBuffer](xref:System.Text.DecoderFallbackBuffer) 派生一个类用于解码操作。

3. 对于异常回退，如果预定义的 [EncoderFallbackException](xref:System.Text.EncoderFallbackException) 和 [DecoderFallbackException](xref:System.Text.DecoderFallbackException) 类不能满足需要，可从异常对象中派生一个类，如 [Exception](xref:System.Exception) 或 [ArgumentException](xref:System.ArgumentException)。

### <a name="deriving-from-encoderfallback-or-decoderfallback"></a>从 EncoderFallback 或 DecoderFallback 中派生

若要实现自定义的回退解决方案，必须创建一个继承自 [EncoderFallback](xref:System.Text.EncoderFallback) 的类用于编码操作，以及一个继承自 [DecoderFallback](xref:System.Text.DecoderFallback) 的类用于解码操作。 这些类的实例传递给 [Encoding.GetEncoding(String, EncoderFallback, DecoderFallback)](xref:System.Text.Encoding.GetEncoding(System.String,System.Text.EncoderFallback,System.Text.DecoderFallback)) 方法，并作为编码类和回退实现之间的媒介。

当为编码器或解码器创建自定义回退解决方案时，必须实现以下成员：

* [EncoderFallback.MaxCharCount](xref:System.Text.EncoderFallback.MaxCharCount) 或 [DecoderFallback.MaxCharCount](xref:System.Text.DecoderFallback.MaxCharCount) 属性，返回最佳、替换或异常回退可能返回以替换单个字符的最大数量的字符数。 对于自定义异常回退，其值为&0;。 

* [EncoderFallback.CreateFallbackBuffer](xref:System.Text.EncoderFallback.CreateFallbackBuffer) 或 [DecoderFallback.CreateFallbackBuffer](xref:System.Text.DecoderFallback.CreateFallbackBuffer) 方法，该方法返回自定义的 [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer) 或 [DecoderFallbackBuffer](xref:System.Text.DecoderFallbackBuffer) 实现。 当遇到不能成功进行编码的第一个字节时或当遇到不能成功进行解码的第一个字节时，则解码器调用该方法。

### <a name="deriving-from-encoderfallbackbuffer-or-decoderfallbackbuffer"></a>从 EncoderFallbackBuffer 或 DecoderFallbackBuffer 中派生

若要实现自定义的回退解决方案，则还必须创建一个继承自 [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer) 的类用于编码操作，以及一个继承自 [DecoderFallbackBuffer](xref:System.Text.DecoderFallbackBuffer) 的类用于解码操作。 [EncoderFallback](xref:System.Text.EncoderFallback) 和 [DecoderFallback](xref:System.Text.DecoderFallback) 类的 `CreateFallbackBuffer` 方法返回这些类的实例。 当遇到不能对其进行编码第一个字符时，编码器调用 [EncoderFallback.CreateFallbackBuffer](xref:System.Text.EncoderFallback.CreateFallbackBuffer) 方法，当遇到不能对其进行解码的一个或多个字节时，解码器调用 [DecoderFallback.CreateFallbackBuffer](xref:System.Text.DecoderFallback.CreateFallbackBuffer) 方法。 [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer) 和 [DecoderFallbackBuffer](xref:System.Text.DecoderFallbackBuffer) 类提供回退实现。 每个实例表示一个包含回退字符的缓冲区，该回退字符将替换不能进行编码的字符或不能进行解码的字节序列。

当为编码器或解码器创建自定义回退解决方案时，必须实现以下成员：

* [EncoderFallbackBuffer.Fallback](xref:System.Text.EncoderFallbackBuffer.%23ctor) 或 [DecoderFallbackBuffer.Fallback](xref:System.Text.DecoderFallbackBuffer.Fallback(System.Byte[],System.Int32)) 方法。 编码器调用 [EncoderFallbackBuffer.Fallback](xref:System.Text.EncoderFallbackBuffer.Fallback(System.Char,System.Char,System.Int32)) 为回退缓冲区提供其不能进行编码的字符的相关信息。 因为要进行编码的字符可能是代理项对，此方法被重载。 向重载传递了字符串中将进行编码的字符及其索引。 向第二个重载传递了字符串中高代理项和低代理项及其索引。 解码器调用 [DecoderFallbackBuffer.Fallback](xref:System.Text.DecoderFallbackBuffer.Fallback(System.Byte[],System.Int32)) 方法为回退缓冲区提供有关无法解码的字节的信息。 向此方法传递了其无法解码的字节数组以及第一个字节的索引。 如果回退缓冲区可以提供一个或多个最佳或替换字符，则回退方法应返回 `true`，否则应返回 `false`。 对于异常回退，回退方法应引发异常。

* [EncoderFallbackBuffer.GetNextChar](xref:System.Text.EncoderFallbackBuffer.GetNextChar) 或 [DecoderFallbackBuffer.GetNextChar](xref:System.Text.DecoderFallbackBuffer.GetNextChar) 方法，编码器或解码器重复调用该方法以从回退缓冲区获取下一个字符。 返回所有回退字符后，该方法应返回 U+0000。 

* [EncoderFallbackBuffer.Remaining](xref:System.Text.EncoderFallbackBuffer.Remaining) 或 [DecoderFallbackBuffer.Remaining](xref:System.Text.DecoderFallbackBuffer.Remaining) 属性，返回回退缓冲区中的剩余字符数。

* [EncoderFallbackBuffer.MovePrevious](xref:System.Text.EncoderFallbackBuffer.MovePrevious) 或 [DecoderFallbackBuffer.MovePrevious](xref:System.Text.DecoderFallbackBuffer.MovePrevious) 方法，将回退缓冲区中的当前位置移到前一个字符。

* [EncoderFallbackBuffer.Reset](xref:System.Text.EncoderFallbackBuffer.Reset) 或 [DecoderFallbackBuffer.Reset](xref:System.Text.DecoderFallbackBuffer.Reset) 方法，将回退缓冲区重新初始化。

如果回退实现是最佳回退或替换回退，则从 [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer) 和 [DecoderFallbackBuffer](xref:System.Text.DecoderFallbackBuffer) 派生的类还保持两个私有实例字段：缓冲区中字符的精确数目；缓冲区中下一个要返回的字符的索引。

### <a name="an-encoderfallback-example"></a>EncoderFallback 示例

前面的一个示例使用替换回退替换与带星号 (\*) 的 ASCII 字符不对应的 Unicode 字符。 下面的示例改为使用自定义的最佳回退实现提供更好的非 ASCII 字符映射。

下面的代码定义一个名为 `CustomMapper`、派生自 [EncoderFallback](xref:System.Text.EncoderFallback) 的类，用以处理非 ASCII 字符的最佳映射。 其 `CreateFallbackBuffer` 方法返回 `CustomMapperFallbackBuffer` 对象，该对象提供 [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer) 实现。 `CustomMapper` 类使用 [Dictionary&lt;TKey, TValue&gt;](xref:System.Collections.Generic.Dictionary%602) 对象存储不受支持的 Unicode 字符（键值）和其对应的 8 位字符（以 64 位整数存储在两个连续字节中）的映射。 若要使此映射可用于回退缓冲区，将 `CustomMapper` 实例作为参数传递给 `CustomMapperFallbackBuffer` 类构造函数。 因为最长的映射是 Unicode 字符 U+221E 的字符串“INF”，所以 `MaxCharCount` 属性返回 3。 

```csharp
public class CustomMapper : EncoderFallback
{
   public string DefaultString;
   internal Dictionary<ushort, ulong> mapping;

   public CustomMapper() : this("*")
   {   
   }

   public CustomMapper(string defaultString)
   {
      this.DefaultString = defaultString;

      // Create table of mappings
      mapping = new Dictionary<ushort, ulong>();
      mapping.Add(0x24C8, 0x53);
      mapping.Add(0x2075, 0x35);
      mapping.Add(0x221E, 0x49004E0046);
   }

   public override EncoderFallbackBuffer CreateFallbackBuffer()
   {
      return new CustomMapperFallbackBuffer(this);
   }

   public override int MaxCharCount
   {
      get { return 3; }
   } 
}
```

```vb
Public Class CustomMapper : Inherits EncoderFallback
   Public DefaultString As String
   Friend mapping As Dictionary(Of UShort, ULong)

   Public Sub New()
      Me.New("?")
   End Sub

   Public Sub New(ByVal defaultString As String)
      Me.DefaultString = defaultString

      ' Create table of mappings
      mapping = New Dictionary(Of UShort, ULong)
      mapping.Add(&H24C8, &H53)
      mapping.Add(&H2075, &H35)
      mapping.Add(&H221E, &H49004E0046)
   End Sub

   Public Overrides Function CreateFallbackBuffer() As System.Text.EncoderFallbackBuffer
      Return New CustomMapperFallbackBuffer(Me)
   End Function

   Public Overrides ReadOnly Property MaxCharCount As Integer
      Get
         Return 3
      End Get
   End Property
End Class
```

下面的代码定义 `CustomMapperFallbackBuffer` 类，该类派生自 [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer)。 包含最佳映射并在 `CustomMapper` 实例中定义的字典可从其类构造函数获取。 如果映射字典中定义了 ASCII 编码器无法对其进行编码的 Unicode 字符，则其 `Fallback` 方法返回 `true`；否则返回 `false`。 对于每个回退，私有 `count` 变量指示仍需返回的字符数目，私有 `index` 变量指示字符串缓冲区 `charsToReturn` 中下一个要返回的字符的位置。 

```csharp
public class CustomMapperFallbackBuffer : EncoderFallbackBuffer
{
   int count = -1;                   // Number of characters to return
   int index = -1;                   // Index of character to return
   CustomMapper fb; 
   string charsToReturn; 

   public CustomMapperFallbackBuffer(CustomMapper fallback)
   {
      this.fb = fallback;
   }

   public override bool Fallback(char charUnknownHigh, char charUnknownLow, int index)
   {
      // Do not try to map surrogates to ASCII.
      return false;
   }

   public override bool Fallback(char charUnknown, int index)
   {
      // Return false if there are already characters to map.
      if (count >= 1) return false;

      // Determine number of characters to return.
      charsToReturn = String.Empty;

      ushort key = Convert.ToUInt16(charUnknown);
      if (fb.mapping.ContainsKey(key)) {
         byte[] bytes = BitConverter.GetBytes(fb.mapping[key]);
         int ctr = 0;
         foreach (var byt in bytes) {
            if (byt > 0) {
               ctr++;
               charsToReturn += (char) byt;
            }
         }
         count = ctr;
      }
      else {
         // Return default.
         charsToReturn = fb.DefaultString;
         count = 1;
      }
      this.index = charsToReturn.Length - 1;

      return true;
   }

   public override char GetNextChar()
   {
      // We'll return a character if possible, so subtract from the count of chars to return.
      count--;
      // If count is less than zero, we've returned all characters.
      if (count < 0) 
         return '\u0000';

      this.index--;
      return charsToReturn[this.index + 1];
   }

   public override bool MovePrevious()
   {
      // Original: if count >= -1 and pos >= 0
      if (count >= -1) {
         count++;
         return true;
      }
      else {
         return false;
      }
   }

   public override int Remaining 
   {
      get { return count < 0 ? 0 : count; }
   }

   public override void Reset()
   {
      count = -1;
      index = -1;
   }
}
```

```vb
Public Class CustomMapperFallbackBuffer : Inherits EncoderFallbackBuffer

   Dim count As Integer = -1        ' Number of characters to return
   Dim index As Integer = -1        ' Index of character to return
   Dim fb As CustomMapper
   Dim charsToReturn As String

   Public Sub New(ByVal fallback As CustomMapper)
      MyBase.New()
      Me.fb = fallback
   End Sub

   Public Overloads Overrides Function Fallback(ByVal charUnknownHigh As Char, ByVal charUnknownLow As Char, ByVal index As Integer) As Boolean
      ' Do not try to map surrogates to ASCII.
      Return False
   End Function

   Public Overloads Overrides Function Fallback(ByVal charUnknown As Char, ByVal index As Integer) As Boolean
      ' Return false if there are already characters to map.
      If count >= 1 Then Return False

      ' Determine number of characters to return.
      charsToReturn = String.Empty

      Dim key As UShort = Convert.ToUInt16(charUnknown)
      If fb.mapping.ContainsKey(key) Then
         Dim bytes() As Byte = BitConverter.GetBytes(fb.mapping.Item(key))
         Dim ctr As Integer
         For Each byt In bytes
            If byt > 0 Then
               ctr += 1
               charsToReturn += Chr(byt)
            End If
         Next
         count = ctr
      Else
         ' Return default.
         charsToReturn = fb.DefaultString
         count = 1
      End If
      Me.index = charsToReturn.Length - 1

      Return True
   End Function

   Public Overrides Function GetNextChar() As Char
      ' We'll return a character if possible, so subtract from the count of chars to return.
      count -= 1
      ' If count is less than zero, we've returned all characters.
      If count < 0 Then Return ChrW(0)

      Me.index -= 1
      Return charsToReturn(Me.index + 1)
   End Function

   Public Overrides Function MovePrevious() As Boolean
      ' Original: if count >= -1 and pos >= 0
      If count >= -1 Then
         count += 1
         Return True
      Else
         Return False
      End If
   End Function

   Public Overrides ReadOnly Property Remaining As Integer
      Get
         Return If(count < 0, 0, count)
      End Get
   End Property

   Public Overrides Sub Reset()
      count = -1
      index = -1
   End Sub
End Class
```

然后，下面的代码实例化 `CustomMapper` 对象并将它的一个实例传递给 [Encoding.GetEncoding(String, EncoderFallback, DecoderFallback)](xref:System.Text.Encoding.GetEncoding(System.String,System.Text.EncoderFallback,System.Text.DecoderFallback)) 方法。 输出指示最佳回退实现成功处理原始字符串中的三个非 ASCII 字符。

```csharp
using System;
using System.Collections.Generic;
using System.Text;

class Program
{
   static void Main()
   {
      Encoding enc = Encoding.GetEncoding("us-ascii", new CustomMapper(), new DecoderExceptionFallback());

      string str1 = "\u24C8 \u2075 \u221E";
      Console.WriteLine(str1);
      for (int ctr = 0; ctr <= str1.Length - 1; ctr++) {
         Console.Write("{0} ", Convert.ToUInt16(str1[ctr]).ToString("X4"));
         if (ctr == str1.Length - 1) 
            Console.WriteLine();
      }
      Console.WriteLine();

      // Encode the original string using the ASCII encoder.
      byte[] bytes = enc.GetBytes(str1);
      Console.Write("Encoded bytes: ");
      foreach (var byt in bytes)
         Console.Write("{0:X2} ", byt);

      Console.WriteLine("\n");

      // Decode the ASCII bytes.
      string str2 = enc.GetString(bytes);
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2));
      if (! str1.Equals(str2)) {
         Console.WriteLine(str2);
         foreach (var ch in str2)
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

         Console.WriteLine();
      }
   }
}
```

```vb
Imports System.Text
Imports System.Collections.Generic

Module Module1

   Sub Main()
      Dim enc As Encoding = Encoding.GetEncoding("us-ascii", New CustomMapper(), New DecoderExceptionFallback())

      Dim str1 As String = String.Format("{0} {1} {2}", ChrW(&H24C8), ChrW(&H2075), ChrW(&H221E))
      Console.WriteLine(str1)
      For ctr As Integer = 0 To str1.Length - 1
         Console.Write("{0} ", Convert.ToUInt16(str1(ctr)).ToString("X4"))
         If ctr = str1.Length - 1 Then Console.WriteLine()
      Next
      Console.WriteLine()

      ' Encode the original string using the ASCII encoder.
      Dim bytes() As Byte = enc.GetBytes(str1)
      Console.Write("Encoded bytes: ")
      For Each byt In bytes
         Console.Write("{0:X2} ", byt)
      Next
      Console.WriteLine()
      Console.WriteLine()

      ' Decode the ASCII bytes.
      Dim str2 As String = enc.GetString(bytes)
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2))
      If Not str1.Equals(str2) Then
         Console.WriteLine(str2)
         For Each ch In str2
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
         Next
         Console.WriteLine()
      End If
   End Sub
End Module
```

## <a name="see-also"></a>另请参阅

[System.Text.Encoder](xref:System.Text.Encoder)

[System.Text.EncoderFallback](xref:System.Text.EncoderFallback)

[System.Text.Decoder](xref:System.Text.Decoder)

[System.Text.DecoderFallback](xref:System.Text.DecoderFallback)

[System.Text.Encoding](xref:System.Text.Encoding)





