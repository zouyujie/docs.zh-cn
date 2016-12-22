---
title: "如何：创建文件或文件夹（C# 编程指南） | Microsoft Docs"
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
  - "创建文件 [C#]"
  - "创建文件夹 [C#]"
  - "文件 [C#]"
  - "文件夹 [C#]"
ms.assetid: 4582ee2d-d72d-4687-bcb9-08d336c62c25
caps.latest.revision: 22
caps.handback.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：创建文件或文件夹（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

您可通过编程方式在您的计算机上创建文件夹、子文件夹和子文件夹中的文件，并将数据写入文件。  
  
## 示例  
 [!CODE [csFilesandFolders#10](../CodeSnippet/VS_Snippets_VBCSharp/csFilesAndFolders#10)]  
  
 如果该文件夹已存在，则 <xref:System.IO.Directory.CreateDirectory%2A> 不执行任何操作，且不会引发异常。  但是，<xref:System.IO.File.Create%2A?displayProperty=fullName> 用新的文件替换现有文件。  该示例使用一个 `if`\-`else` 语句阻止现有文件被替换。  
  
 通过在示例中做出以下更改，您可以根据具有某个名称的程序是否存在来指定不同的结果。  如果该文件不存在，代码将创建一个文件。  如果该文件存在，代码将把数据添加到该文件中。  
  
-   指定一个非随机文件名。  
  
    ```c#  
    // Comment out the following line.  
    //string fileName = System.IO.Path.GetRandomFileName();  
  
    // Replace that line with the following assignment.  
    string fileName = "MyNewFile.txt";  
  
    ```  
  
-   用以下代码中的 `using` 语句替换 `if`\-`else` 语句。  
  
    ```c#  
    using (System.IO.FileStream fs = new System.IO.FileStream(pathString, FileMode.Append))   
    {  
        for (byte i = 0; i < 100; i++)  
        {  
            fs.WriteByte(i);  
        }  
    }  
  
    ```  
  
 运行该示例若干次以验证数据是否每次都添加到文件中。  
  
 有关更多可以尝试的 `FileMode` 值的信息，请参阅 <xref:System.IO.FileMode>。  
  
 以下情况可能会导致异常：  
  
-   文件夹名称格式不正确。  例如，它包含非法字符或仅仅是空白（<xref:System.ArgumentException> 类）。  使用 <xref:System.IO.Path> 类创建有效路径名。  
  
-   要创建的文件夹的父文件夹是只读的（<xref:System.IO.IOException> 类）。  
  
-   文件夹名称是 `null`（<xref:System.ArgumentNullException> 类）。  
  
-   文件夹名称太长（<xref:System.IO.PathTooLongException> 类）。  
  
-   文件夹名称只是冒号“:”（<xref:System.IO.PathTooLongException> 类）。  
  
## .NET Framework 安全性  
 在部分信任的情况下可能会引发 <xref:System.Security.SecurityException> 类的实例。  
  
 如果没有创建文件夹的权限，则该示例引发 <xref:System.UnauthorizedAccessException> 类的实例。  
  
## 请参阅  
 <xref:System.IO?displayProperty=fullName>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [文件系统和注册表](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)