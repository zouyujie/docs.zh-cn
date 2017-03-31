---
title: "如何：复制、删除和移动文件和文件夹（C# 编程指南）| Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- I/O [C#]
ms.assetid: 62e52cd7-9597-4e4a-acf9-1315f5cdbf05
caps.latest.revision: 13
author: BillWagner
ms.author: wiwagn
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
ms.openlocfilehash: c7e9a170882c4e8dbb04dc014642a28ad4365e39
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-copy-delete-and-move-files-and-folders-c-programming-guide"></a>如何：复制、删除和移动文件和文件夹（C# 编程指南）
以下示例说明如何使用 <xref:System.IO?displayProperty=fullName> 命名空间中的 <xref:System.IO.File?displayProperty=fullName>、<xref:System.IO.Directory?displayProperty=fullName>、<xref:System.IO.FileInfo?displayProperty=fullName> 和 <xref:System.IO.DirectoryInfo?displayProperty=fullName> 类以同步方式复制、移动和删除文件和文件夹。 这些示例未提供进度栏或其他任何用户界面。 如果希望提供一个标准进度对话框，请参阅[如何：提供文件操作进度对话框](how-to-provide-a-progress-dialog-box-for-file-operations.md)。  
  
 操作多个文件时，请使用 <xref:System.IO.FileSystemWatcher?displayProperty=fullName> 提供事件，以便可以计算进度。 另一种方法是使用平台调用来调用 Windows Shell 中相应的文件相关方法。 有关如何异步执行这些文件操作的信息，请参阅[异步文件 I/O](https://msdn.microsoft.com/library/kztecsys)。  
  
## <a name="example"></a>示例  
 以下示例演示如何复制文件和目录。  
  
 [!code-cs[csFilesandFolders#7](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-copy-delete-and-move-files-and-folders_1.cs)]  
  
## <a name="example"></a>示例  
 以下示例演示如何移动文件和目录。  
  
 [!code-cs[csFilesandFolders#8](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-copy-delete-and-move-files-and-folders_2.cs)]  
  
## <a name="example"></a>示例  
 以下示例演示如何删除文件和目录。  
  
 [!code-cs[csFilesandFolders#9](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-copy-delete-and-move-files-and-folders_3.cs)]  
  
## <a name="see-also"></a>请参阅  
 <xref:System.IO?displayProperty=fullName>   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [文件系统和注册表（C# 编程指南）](index.md)   
 [如何：提供文件操作进度对话框](how-to-provide-a-progress-dialog-box-for-file-operations.md)   
 [文件和流 I/O](https://msdn.microsoft.com/library/k3352a4t)   
 [通用 I/O 任务](https://msdn.microsoft.com/library/ms404278)
