---
title: "如何：将 RTF 转换为纯文本（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "字符串 [C#], 从 RTF 转换"
ms.assetid: 3b386a87-899d-4d98-bc82-a980526ddaac
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# 如何：将 RTF 转换为纯文本（C# 编程指南）
RTF 格式是 Microsoft 于 20 世纪 80 年代后期开发的一种文件格式，旨在实现不同操作系统之间的文档交换。  Microsoft Word 和 WordPad 都可以读写 RTF 文件。  在 .NET Framework 中，可以使用 <xref:System.Windows.Forms.RichTextBox> 控件创建支持 RTF 且支持用户以 WYSIWIG 方式将格式应用于文本的字处理器。  
  
 也可以使用 <xref:System.Windows.Forms.RichTextBox> 以编程方式将 RTF 格式代码从文档中移除，从而将该文档转换为纯文本。  执行这种类型的操作无需在 Windows 窗体中嵌入该控件。  
  
### 在项目中使用 RichTextBox 控件  
  
1.  添加对 System.Windows.Forms.dll 的引用。  
  
2.  为 `System.Windows.Forms` 命名空间添加 using 指令（可选）。  
  
## 示例  
 下面的示例将示例 RTF 文件转换为纯文本。  文件包含 RTF 格式设置 \(如字体信息\)，四个 Unicode 字符和四个扩展的 ASCII 字符。  代码示例打开文件，将其内容设置为 <xref:System.Windows.Forms.RichTextBox>，当 RTF，检索该内容作为文本，并在 <xref:System.Windows.Forms.MessageBox>的文本和输出该文本到一个 UTF\-8 格式的文件。  
  
 `MessageBox` 和输出文件包含以下文本：  
  
```  
The Greek word for "psyche" is spelled ψυχή. The Greek letters are encoded in Unicode.  
These characters are from the extended ASCII character set (Windows code page 1252):  âäӑå  
  
```  
  
 [!code-cs[csProgGuideStrings#33](../../../csharp/programming-guide/strings/codesnippet/csharp/CSRefStrings/Strings.cs#33)]  
  
 RTF 字符以八位编码。  但是，除了从指定的代码页，扩展 ASCII 字符之外用户可以指定 Unicode 字符。  由于 <xref:System.Windows.Forms.RichTextBox.Text%2A?displayProperty=fullName> 属性为 [string](../../../csharp/language-reference/keywords/string.md) 类型，因此字符按 Unicode UTF\-16 进行编码。  源 RTF 文档中的所有扩展的 ASCII 字符和 Unicode 字符都在文本输出中进行了正确的编码。  
  
 如果使用 <xref:System.IO.File.WriteAllText%2A?displayProperty=fullName> 方法将文本写入磁盘，则文本将按 UTF\-8（没有字节顺序标记）进行编码。  
  
## 请参阅  
 <xref:System.Windows.Forms.RichTextBox?displayProperty=fullName>   
 [字符串](../../../csharp/programming-guide/strings/index.md)