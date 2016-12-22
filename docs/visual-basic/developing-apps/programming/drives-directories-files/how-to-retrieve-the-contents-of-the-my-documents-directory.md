---
title: "如何：在 Visual Basic 中检索“我的文档”目录中的内容 | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "“我的文档”目录"
ms.assetid: 26560d01-7dda-4457-8e95-21db23d71aea
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：在 Visual Basic 中检索“我的文档”目录中的内容
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

可以使用 <xref:Microsoft.VisualBasic.FileIO.SpecialDirectories> 对象来读取**“All Users”**中的许多目录，如**“我的文档”**或**“桌面”**。  
  
### 读取“我的文档”文件夹  
  
-   使用 `ReadAllText` 方法读取特定目录中每个文件的文本。  下面的代码指定一个目录和一个文件，然后使用 `ReadAllText` 将它们读入名为 `patients` 的字符串中。  
  
     [!code-vb[VbVbcnMyFileSystem#15](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-retrieve-the-contents-of-the-my-documents-directory_1.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.SpecialDirectories>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllText%2A>