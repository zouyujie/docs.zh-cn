---
title: "如何：在 Visual Basic 中重命名文件 | Microsoft Docs"
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
- I/O [Visual Basic], renaming files
- files, renaming
ms.assetid: 0ea7e0c8-2cb2-4bf5-a00d-7b6e3c08a3bc
caps.latest.revision: 21
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
ms.openlocfilehash: a0a31353ce3ee0c48907f9550f6961260f92b64a
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-rename-a-file-in-visual-basic"></a>如何：在 Visual Basic 中重命名文件
使用 `My.Computer.FileSystem` 对象的 `RenameFile` 方法可通过提供当前位置、文件名和新文件名来重命名文件。 此方法不能用于移动文件；使用 `MoveFile` 方法可移动并重命名文件。  
  
### <a name="to-rename-a-file"></a>重命名文件  
  
-   使用 `My.Computer.FileSystem.RenameFile` 方法可重命名文件。 此示例将名为 `Test.txt` 的文件重命名为 `SecondTest.txt`。  
  
     [!code-vb[VbVbcnMyFileSystem#9](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-rename-a-file_1.vb)]  
  
 此代码示例也可作为 IntelliSense 代码片段。 在代码片段选取器中，该代码段位于“文件系统 - 处理驱动器、文件夹和文件”****。 有关详细信息，请参阅[代码片段](https://docs.microsoft.com/visualstudio/ide/code-snippets)。  
  
## <a name="robust-programming"></a>可靠编程  
 以下情况可能会导致异常：  
  
-   路径由于以下原因之一而无效：是零长度字符串；仅包含空白；包含无效字符；是一个设备路径（以 \\\\.\\ 开头）(<xref:System.ArgumentException>)。  
  
-   `newName` 包含路径信息 (<xref:System.ArgumentException>)。  
  
-   路径无效，因为路径为 `Nothing` (<xref:System.ArgumentNullException>)。  
  
-   `newName` 是 `Nothing` 或空字符串 (<xref:System.ArgumentNullException>)。  
  
-   源文件无效或不存在 (<xref:System.IO.FileNotFoundException>)。  
  
-   不存在具有 `newName` 中指定的名称的现有文件或目录 (<xref:System.IO.IOException>)。  
  
-   路径超出了系统定义的最大长度 (<xref:System.IO.PathTooLongException>)。  
  
-   路径中的某个文件或目录名称包含冒号 (:) 或格式无效 (<xref:System.NotSupportedException>)。  
  
-   用户缺少必要的权限来查看路径 (<xref:System.Security.SecurityException>)。  
  
-   用户没有所需权限 (<xref:System.UnauthorizedAccessException>)。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.RenameFile%2A>   
 [如何：移动文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-move-a-file.md)   
 [创建、删除和移动文件和目录](../../../../visual-basic/developing-apps/programming/drives-directories-files/creating-deleting-and-moving-files-and-directories.md)   
 [如何：在同一目录中创建文件副本](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-create-a-copy-of-a-file-in-the-same-directory.md)   
 [如何：在不同的目录中创建文件的副本](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-create-a-copy-of-a-file-in-a-different-directory.md)
