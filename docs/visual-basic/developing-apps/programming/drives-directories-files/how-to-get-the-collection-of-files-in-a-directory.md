---
title: "如何：在 Visual Basic 中获取目录中的文件集合 | Microsoft 文档"
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
- folders, working with
- files, accessing
ms.assetid: 6c8ba7e8-dd37-4853-92bf-762b67c98160
caps.latest.revision: 23
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
ms.openlocfilehash: d5b36baee302db0214844e0553473a05603090f1
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-get-the-collection-of-files-in-a-directory-in-visual-basic"></a>如何：在 Visual Basic 中获取目录中的文件集合
<xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A?displayProperty=fullName> 方法的重载返回只读的字符串集合，这些字符串表示目录中文件的名称：  
  
-   在指定的目录中使用 <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%28System.String%29> 重载进行简单的不搜索子目录的文件搜索。  
  
-   使用 <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles(System.String,Microsoft.VisualBasic.FileIO.SearchOption,System.String[])> 重载来指定搜索的其他选项。 可以使用 `wildCards` 参数来指定搜索模式。 若要在搜索中包含子目录，请将 `searchType` 参数设为 <xref:Microsoft.VisualBasic.FileIO.SearchOption?displayProperty=fullName>。  
  
 如果没有找到与指定模式匹配的文件，则返回一个空集合。  
  
### <a name="to-list-files-in-a-directory"></a>列出目录中的文件  
  
-   使用一个 <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A?displayProperty=fullName> 方法重载，在 `directory` 参数中提供要搜索的目录的名称和路径。 下面的示例返回目录中的所有文件，并将它们添加到 `ListBox1`。  
  
     [!code-vb[VbVbcnMyFileSystem#32](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-get-the-collection-of-files-in-a-directory_1.vb)]  
  
## <a name="robust-programming"></a>可靠编程  
 以下情况可能会导致异常：  
  
-   路径由于以下原因之一而无效：是零长度字符串；仅包含空白；包含无效字符；是一个设备路径（以 \\\\.\\ 开头）(<xref:System.ArgumentException>)。  
  
-   路径无效，因为路径为 `Nothing` (<xref:System.ArgumentNullException>)。  
  
-   `directory` 不存在 (<xref:System.IO.DirectoryNotFoundException>)。  
  
-   `directory` 指向现有文件 (<xref:System.IO.IOException>)。  
  
-   路径超出了系统定义的最大长度 (<xref:System.IO.PathTooLongException>)。  
  
-   路径中的某个文件或目录名称包含冒号 (:) 或格式无效 (<xref:System.NotSupportedException>)。  
  
-   用户缺少必要的权限来查看路径 (<xref:System.Security.SecurityException>)。  
  
-   用户缺少必要的权限 (<xref:System.UnauthorizedAccessException>)。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A>   
 [如何：查找具有特定模式的文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-files-with-a-specific-pattern.md)   
 [如何：查找具有特定模式的子目录](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-subdirectories-with-a-specific-pattern.md)

