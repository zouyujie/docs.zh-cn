---
title: "如何：一次一行地读取文本文件 (Visual C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "读取文本文件, 逐行"
  - "ReadLine 方法 [C#]"
  - "文本文件 [C#]"
ms.assetid: d62e22c5-a13c-48db-af9b-f10c801b0cb1
caps.latest.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 11
---
# 如何：一次一行地读取文本文件 (Visual C#)
本示例使用 `StreamReader` 类的 `ReadLine` 方法将文本文件的内容读取（一次读取一行）到字符串中。  所有文本行都保存在字符串 `line` 中并显示在屏幕上。  
  
## 示例  
  
```  
int counter = 0;  
string line;  
  
// Read the file and display it line by line.  
System.IO.StreamReader file =   
    new System.IO.StreamReader(@"c:\test.txt");  
while((line = file.ReadLine()) != null)  
{  
    System.Console.WriteLine (line);  
    counter++;  
}  
  
file.Close();  
System.Console.WriteLine("There were {0} lines.", counter);  
// Suspend the screen.  
System.Console.ReadLine();  
```  
  
## 编译代码  
 复制该代码，并将其粘贴到某控制台应用程序的 `Main` 方法中。  
  
 将 `"c:\test.txt"` 替换为实际的文件名。  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   该文件可能不存在。  
  
## .NET Framework 安全性  
 不要根据文件的名称来判断文件的内容。  例如，文件 `myFile.cs` 可能不是 C\# 源文件。  
  
## 请参阅  
 <xref:System.IO?displayProperty=fullName>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [文件系统和注册表](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)