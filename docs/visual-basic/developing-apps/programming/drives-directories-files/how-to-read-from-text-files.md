---
title: "如何：在 Visual Basic 中读取文本文件 | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- extended characters, reading
- reading text files
- reading data, text files
- examples [Visual Basic], reading text files
- text files, reading
ms.assetid: 735fe9d7-0f7a-4185-ba02-f35e580ec4b8
caps.latest.revision: 27
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 362745101d1a8f7dd61b5e3aabe1c27190c46c07
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-read-from-text-files-in-visual-basic"></a>如何：在 Visual Basic 中读取文本文件
`My.Computer.FileSystem` 对象的 <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.ReadAllText%2A> 方法使你可以读取文本文件。 如果文件的内容使用类似 ASCII 或 UTF-8 的编码，则可以指定文件编码。  
  
 若要读取包含扩展字符的文件，则需要指定文件编码。  
  
> [!NOTE]
>  若要一次一个文本行地读取文件，请使用 `My.Computer.FileSystem` 对象的 <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.OpenTextFileReader%2A> 方法。 `OpenTextFileReader` 方法返回 <xref:System.IO.StreamReader> 对象。 可以使用 `StreamReader` 对象的 <xref:System.IO.StreamReader.ReadLine%2A> 方法一次一行地读取文件。 你可以使用 `StreamReader` 对象的 <xref:System.IO.StreamReader.EndOfStream%2A> 方法测试文件的结尾。  
  
### <a name="to-read-from-a-text-file"></a>读取文本文件  
  
-   使用 `ReadAllText` 对象的 `My.Computer.FileSystem` 方法并提供路径，可以将文本文件的内容读入字符串中。 下面的示例将 test.txt 的内容读入字符串中，然后在消息框中显示内容。  
  
     [!code-vb[VbFileIORead#2](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-text-files_1.vb)]  
  
### <a name="to-read-from-a-text-file-that-is-encoded"></a>读取已编码的文本文件  
  
-   使用 `ReadAllText` 对象的 `My.Computer.FileSystem` 方法并提供路径和文件编码类型，可以将文本文件的内容读入字符串中。 下面的示例将 UTF32 文件 test.txt 的内容读入字符串中，然后在消息框中显示内容。  
  
     [!code-vb[VbFileIORead#3](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-text-files_2.vb)]  
  
## <a name="robust-programming"></a>可靠编程  
 以下情况可能会导致异常：  
  
-   路径由于以下原因之一而无效：是零长度字符串；仅包含空白；包含无效字符；是一个设备路径 (<xref:System.ArgumentException>)。  
  
-   路径无效，因为路径为 `Nothing` (<xref:System.ArgumentNullException>)。  
  
-   文件不存在 (<xref:System.IO.FileNotFoundException>)。  
  
-   文件正由另一个进程使用，或者出现 I/O 错误 (<xref:System.IO.IOException>)。  
  
-   路径超出了系统定义的最大长度 (<xref:System.IO.PathTooLongException>)。  
  
-   路径中的某个文件或目录名称包含冒号 (:) 或格式无效 (<xref:System.NotSupportedException>)。  
  
-   内存不足，无法将字符串写入缓冲区 (<xref:System.OutOfMemoryException>)。  
  
-   用户缺少必要的权限来查看路径 (<xref:System.Security.SecurityException>)。  
  
 不要根据文件的名称来判断文件的内容。 例如，文件 Form1.vb 可能不是 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 源文件。  
  
 在应用程序中使用输入的数据之前，需验证所有的输入内容。 文件的内容可能不是预期内容，并且用来读取该文件的方法可能失败。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllText%2A>   
 [从文件读取](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)   
 [如何：读取逗号分隔的文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-comma-delimited-text-files.md)   
 [如何：读取固定宽度的文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-fixed-width-text-files.md)   
 [如何：读取具有多种格式的文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md)   
 [疑难解答：读取和写入文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)   
 [演练：在 Visual Basic 中操作文件和目录](../../../../visual-basic/developing-apps/programming/drives-directories-files/walkthrough-manipulating-files-and-directories.md)   
 [文件编码](../../../../visual-basic/developing-apps/programming/drives-directories-files/file-encodings.md)
